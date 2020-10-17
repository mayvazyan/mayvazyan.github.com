---
layout: post
title: Tracking Application Response Time with NGINX, Filebeat and Elastic Search
date: 2020-10-17 16:13
author: ayvazyan
comments: true
categories: [devops]
---

Recently we needed to enable Response Time monitoring on NGINX server. Let me try to summarise steps needed to bring response times from NGINX into [Elastic Search](https://www.elastic.co/).

## NGINX Configuration
In order to do so we had to define a new log format. That topic is covered in much detail at [lincolnloop.com](https://lincolnloop.com/blog/tracking-application-response-time-nginx/) back in Nov 09, 2010!

In short you need to add log format into `nginx.conf`
```
log_format timed_combined '$remote_addr - $remote_user [$time_local] '
    '"$request" $status $body_bytes_sent '
    '"$http_referer" "$http_user_agent" '
    '$request_time $upstream_response_time $pipe';
```

Next step is to modify `access_log` directives to use the new format:
```
access_log /var/log/nginx/yourdomain.com.access.log timed_combined;
```

Once configuration files have been updated run `nginx -t` to test them.
If NGINX likes your new configuration run `nginx -s reload` so it will start using them.

## Filebeat Configuration
[Filebeat](https://www.elastic.co/beats/filebeat) is a lightweight shipper for logs. We are using it to deliver logs to [Elastic Search](https://www.elastic.co/) cluster. To review logs and mertics we are using [Kibana](https://www.elastic.co/kibana).

Filebeat is using `grok` patterns to parse log files. Basically all you need is to update a `grok` pattern which is being used by Filebeat to parse NGINX logs.
In my case it's located at 
```
/usr/share/filebeat/module/nginx/access/ingest/pipeline.yml
```
I added a new line to the end of the `patterns:` definition:
```
%{NUMBER:http.request.time:double} %{NUMBER:upstream.request.time:double} %{DATA:pipelined}
```
Which is what I've got after that
```
  ...  
  patterns:
    - (%{NGINX_HOST} )?"?(?:%{NGINX_ADDRESS_LIST:nginx.access.remote_ip_list}|%{NOTSPACE:source.address})
      - (-|%{DATA:user.name}) \[%{HTTPDATE:nginx.access.time}\] "%{DATA:nginx.access.info}"
      %{NUMBER:http.response.status_code:long} %{NUMBER:http.response.body.bytes:long}
      "(-|%{DATA:http.request.referrer})" "(-|%{DATA:user_agent.original})"
      %{NUMBER:http.request.time:double} %{NUMBER:upstream.request.time:double} %{DATA:pipelined}
  ...
```

- **http.request.time** variable represents full request time, starting when NGINX reads the first byte from the client and ending when NGINX sends the last byte of the response body.
- **upstream.request.time** variable represents time between establishing a connection to an upstream server and receiving the last byte of the response body.
- **pipelined** variable has “p” if request was pipelined, “.” otherwise.

Please note that you can name these new variables as you would like. For example instead of **http.request.time** it could be named as **requesttime**.

### Filebeat pipeline update
Please not that once you updated `pipeline.yml` file you will need to make Filebeat to push it to Elastic Search. You have several options here:

1. You can run `filebeat setup` command which will make sure everything is up-to-date in Elastic Search.
2. You can remove index manually from Elastic Search  by running `DELETE _ingest/pipeline/filebeat-*-nginx*` command. Then start Filebeat - it will setup everything during start-up procedure.
