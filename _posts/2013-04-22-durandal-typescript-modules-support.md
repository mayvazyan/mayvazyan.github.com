---
layout: post
title: "Durandal: TypeScript modules support"
date: 2013-04-22 22:21
author: ayvazyan
comments: true
categories: [durandal, Open Source, spa, typescript]
---
<p>I’m working on a prototype of HTML5 Single Page Application (SPA).</p>  <p>I’m happy to use plumbing provided by <a href="http://durandaljs.com/">Durandal</a>. It’s really exciting SPA framework.&#160; Unfortunately it doesn’t support TypeScript modules.</p>  <p>According to Rob Eisenberg it won’t be fixed for now (quote below)</p>  <blockquote>   <p>I'd rather not make a change in the core based on the current state of TypeScript. Rather, I'd prefer a plugin that re-configures durandal for this case. But, it will get fixed in TypeScript before v1.0 I confirmed that by checking their roadmap. Also Luke Hoban responded to me via codeplex to say they have every intent to fix it</p>    <p><a href="https://github.com/BlueSpire/Durandal/pull/13">https://github.com/BlueSpire/Durandal/pull/13</a></p> </blockquote>  <p>So if we are going to start to use TypeScript with Durandal… we need some workaround.</p>  <p>So here we go.</p>  <p>First we need to apply below lines into <strong>router.js</strong>. It will add basic TypeScript modules support.</p>  <p><img src="https://dl.dropboxusercontent.com/u/936929/Blog/typescript_durandal/routerjs.PNG" /></p>  <p>Second step is to enable master\detail scenario by adding below lines into <strong>system.js</strong></p>  <p><img src="https://dl.dropboxusercontent.com/u/936929/Blog/typescript_durandal/systemjs.PNG" /></p>  <p>Would be happy to get some feedback on this.</p>
