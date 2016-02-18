---
layout: post
title: Entity Framework (EF), UnitOfWork & Repository patterns
date: 2012-03-12 00:10
author: ayvazyan
comments: true
categories: [.NET, EF, TDD, BDD, etc.]
---
<p>There are some debates on the network about if we need to add abstraction layer on the top of Entity Framework. Or it’s redundant. Sure, I have my own opinion as well <img style="border-bottom-style: none; border-left-style: none; border-top-style: none; border-right-style: none" class="wlEmoticon wlEmoticon-smile" alt="Smile" src="http://ayvazyan.net/wp-content/uploads/2012/03/wlEmoticon-smile.png" /></p>  <p>Entity Framework (EF) object context provides us ability to make whatever we want with any table in database. So if our business logic uses EF directly our data access code will be spread through it.&#160; </p>  <p>Me personally like Persistence Ignorance pattern so business logic shouldn’t be aware of the data layer details.</p>  <p>Furthermore I like then each repository contains some related methods. Usually it’s something like UserRepository, ChangeRepository, PostRepository, etc. It helps to structure code since in this case we don’t have huge repositories.</p>  <p>EF implements UnitOfWork pattern and that’s amazing. So that we did in our last project is used EF object context as UnitOfWork and passed it to our Repositories. (it was wrapped into IUnitOfWork, probably I’ll post some technical details later)</p>  <p>We used Code First approach and all our POCOs were located in the Model. So business logic worked with Model not with data.</p>  <p>That’s worked like a charm. We got clean data layer and business logic. It’s very easy to unit test and maintain.</p>
