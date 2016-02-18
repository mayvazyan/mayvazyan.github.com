---
layout: post
title: Machine.Specifications under TFS 2012
date: 2012-12-05 18:38
author: ayvazyan
comments: true
categories: [.NET, Agile, Continuous Integration, I recommend, Productivity, TDD, BDD, etc.]
---
About year ago we started to use <a href="https://github.com/machine/machine.specifications#readme">Machine.Specifications</a> (<a href="http://vimeo.com/11642767">screencast</a>) on one of our projects. It was really nice to have executable specifications and well organized tests. The only issue was is that TFS 2010 Build wasn't able to run Machine.Specifications. Finally I've added some T4 templates to create MSTest wrappers for MSpec code. 
So we were able to run our tests and see the coverage on the CI server.

What's amazing TFS 2012 support test runner extensions. Hence now we can easily configure our CI server to run Machine.Specifications and show us the code coverage!

The step by step guide for NUnit available at <a href="http://blog.accentient.com/2012/04/30/RunningNUnitInATFS11BuildOn64BitServer.aspx">http://blog.accentient.com/2012/04/30/RunningNUnitInATFS11BuildOn64BitServer.aspx</a>.
For the Machine.Specifications it's pretty much the same.
The only change is that you'll need to install <a href="http://visualstudiogallery.msdn.microsoft.com/4abcb54b-53b5-4c44-877f-0397556c5c44">MSpec Test Adapter</a> instead of NUnit.
Also please make sure you selected <strong>Visual Studio Test Runner</strong> in the build configuration. 


