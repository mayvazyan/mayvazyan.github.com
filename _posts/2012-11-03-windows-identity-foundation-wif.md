---
layout: post
title: Windows Identity Foundation (WIF)
date: 2012-11-03 22:28
author: ayvazyan
comments: true
categories: [.NET]
---
I'm really excited by the Windows Identity Foundation (WIF). And now it's a part of .NET Framework, so it can be used in any .NET application.

The team did great work by providing us awesome "plumbing" code, so now we can build truly separated systems very easily.

Also WIF provides 100% backward capability to the old (<em>IIdentity/IPrincipal</em>) approach!

Claims allow us to describe identity using key/value pairs. So we can deal with claims such as name, email, etc.

WIF allows to make Claims <strong>Transformation</strong>. So the application will have to deal only with domain specific claims, and it won't have dependency on the underlain authorization mechanism. For example we can transform  AD Groups into domain specific roles. Sure we can also make any custom Claims <strong>Validation</strong> as well.

Claims-based <strong>Authorization</strong> is a piece of cake. Again you deal with domain specific terms. Here's simple example:

```csharp
[ClaimsPrincipalPermission(SecurityAction.Demand, Operation = "Add", Resource = "Customer")]
public void AddCustomer() { ... }
```

As you can see your business logic says - this is "Add" operation and "Customer" is resource.
And we have a single method to implement authorization logic:

```csharp
public override bool CheckAccess(AuthorizationContext context)
{
	// please note that we deal with arrays here, so we can use more complex expressions in describing our business logic requirements.
	var resource = context.Resource.First().Value;
	var action = context.Action.First().Value;
	if (action == "Add" && resource == "Customer")
	{
		return context.Principal.HasClaim("http://myclaims/someclaim");
	}
	return false;
}
```

As you can see on above example we could move authorization logic to the separate assembly or even Web Service.
It needs to mention that WIF supports Claims caching. For example you can use AppFabric cache to store transformed claims instead of make transformations for each request.
And it support SAML tokens to seamless third party authentication. So you can use AD FS  or even Windows Azure.
