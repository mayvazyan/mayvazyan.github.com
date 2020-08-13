---
layout: post
title: Deployment Group provision in Azure Dev Ops (On Premise)
date: 2020-08-13 21:44
author: ayvazyan
comments: true
categories: [devops]
---
We are a long time users of Team Foundation Server (TFS). As you may know recently it's been renamed into Azure Dev Ops.
I absolutely love the new "Dev Ops" version (we are running v. 17.M153.5 by the way).

But we faced two issues with it, so I'd like to document these here.

## Build Agent registration
If you need to register Build Agent, you have to include Project Collection Name into the url. 

For example previously it worked fine if you specify `https://tfs.example.com/tfs/`.

But with Azure Dev Ops you have to include `https://tfs.example.com/tfs/FooBar/` (**FooBar** is a collection name here).

Otherwise you will get **Client authentication required** error.

## Deployment Agent regionstration
If you need to register agent into Deployment Group, you need to modify the PowerShell script a bit. In particular you have to add `--unattended --token {PAT_TOKEN_HERE}`

So instead of the command below which is part of the Registration script in Dev Ops "Deployment Group" screen.

`.\config.cmd --deploymentpool --deploymentpoolname "DEV" --agent $env:COMPUTERNAME --runasservice --work '_work' --url 'https://tfs.example.com/tfs/'`

it should be something like this

`.\config.cmd --deploymentpool --deploymentpoolname "DEV" --agent $env:COMPUTERNAME --runasservice --work '_work' --url 'https://tfs.example.com/tfs/' --unattended --token {PAT_TOKEN_HERE}`

Otherwise you will be asked to provide url to DevOps again and then get **Not Found** error if you try to include Collection Name into Url.

As I understand the second issue related to the same root case as a first one - without `--unattanded` flag it was complaining about the `https://tfs.example.com/tfs/` url.
Then I included Collection Name in the url it was showing "Not Found" error because collection name appeared twice:

`https://tfs.example.com/tfs/{COLLECTION_NAME}/{COLLECTION_NAME}/_apis/connectionData?connectOptions=1&lastChangeId=-1&lastChangeId64=-1 failed. HTTP Status: NotFound`

More details available at https://github.com/microsoft/azure-pipelines-agent/issues/2565#issuecomment-555448786
