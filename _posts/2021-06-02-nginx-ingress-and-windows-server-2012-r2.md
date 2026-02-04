---
layout: post
title: Nginx Ingress and Windows Server 2012 R2 TLS issue
date: 2021-06-02 13:16
author: ayvazyan
comments: true
categories: [kubernetes]
---

Several months ago I configured [Elastic APM](https://www.elastic.co/apm) on our  kubernetes ([microk8s](https://microk8s.io)) cluster. 
It worked just fine for a `.NET 5` workloads running on the **Linux** containers.
Recently I needed to enable APM for another `.NET 5` project running on **Windows 2012 R2** and I faced the following error:
```
System.Net.Http.HttpRequestException: The SSL connection could not be established, see inner exception.
 ---> System.Security.Authentication.AuthenticationException: Authentication failed because the remote party sent a TLS alert: 'HandshakeFailure'.
 ---> System.ComponentModel.Win32Exception (0x80090326): The message received was unexpected or badly formatted.
```

<!--more-->

Thanks to [Qualys SSL Labs](https://www.ssllabs.com/ssltest/index.html) I was able to quickly find out that our **nginx-ingress** is using **TLS 1.2** and **TLS 1.3** only, with a [secure set of TLS ciphers](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#default-tls-version-and-ciphers).

Unfortunately **Windows Server 2012 R2** does not support secure TLS ciphers. So I had to enable TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (0xc028) (weak) cipher as a workaround for now. 

1. To do so I first examined the arguments our ingress pods are using (see below) and found that I should name Config Map as **nginx-load-balancer-microk8s-conf** (and use the same namespace as ingress pods are using).
```
/nginx-ingress-controller --configmap=$(POD_NAMESPACE)/nginx-load-balancer-microk8s-conf --tcp-services-configmap=$(POD_NAMESPACE)/nginx-ingress-tcp-microk8s-conf --udp-services-configmap=$(POD_NAMESPACE)/nginx-ingress-udp-microk8s-conf --publish-status-address=127.0.0.1
```

2. Then I created a ConfigMap I needed and then I pushed that template by running `kubectl apply -f config-map.yaml`
```
kind: ConfigMap
apiVersion: v1
metadata:
  name: nginx-load-balancer-microk8s-conf
  namespace: ingress
data:
  ssl-ciphers: "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384"
  ssl-protocols: "TLSv1.2 TLSv1.3"
```

3. And the final step was to restart daemonset `kubectl rollout restart deployment nginx-ingress-microk8s-controller -n ingress`

More details available in [NGINX Ingress Controller documentation](https://kubernetes.github.io/ingress-nginx/user-guide/tls/#default-tls-version-and-ciphers)

Hopefully, soon we will be able to migrate to **Windows Server 2019**, then we will be able to switch back to default.

