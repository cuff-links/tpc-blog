---
layout: post
title: "Quality IS a Dev Task"
img: QA_and_Dev.jpg
date: 2015-07-12
description: This article talks about the misconception that quality and testing is just a job for QA. 
tag: [software-development, quality-engineering, test-engineering, QE, QA, quality-assurance, unit-testing, integration-testing, docker, vagrant, dev-testing]
---

*"**I am not a tester.**", "**QA will figure it out.**", "**Works for me. Should be good in production.**":* These words are uttered in development organizations across the globe. I can't lie. I even uttered it once during a production push as a production engineer myself. What contributes to this mentality?

#### What's In A Name?
**A**s most know, QA stands for Quality Assurance. A name like this can be one contributing factor to the fact that software quality often rests solely on the shoulders of the Quality Team. This should not be the case. It's QA's job to make sure the software is acceptable to the end user. 

**T**o ensure software quality, it has to be there in the first place. I am more fond with the term, Quality Engineering. We are engineers for the sake of quality (Yes, manual testers are still engineers). Quality engineers are engineers that function in the discipline of pushing the quality of software forward. 

## Technically, You ARE a Tester
**I**f you have written a line of code, chances are, you are a tester. Let's think of the example of the first program written by most developers. That's right. Hello World.


```python
print "Hello, World!"
```

**W**hen you create this application, likely, you will then run it. What do you do when you run it? You **test** to see if the right output was given. I have never seen a developer say "I refuse to look at the console output!  I am NOT a tester!".

**T**his is not unique. As a front end developer, you will check to see that your code looks right on different browsers, you check to see that your mobile app looks right on different devices, etc. You are **testing** your application. 



#### Quality Engineers Are Often Viewed as  Debuggers
**I**t's all too common for a quality engineer (especially one with a development background) to start being requested to dive deeper and deeper into the code. From being request to perform code reviews to reading stack traces, a quality engineer may find themselves performing many tasks that are owned by development. 

#### The Time It Takes To Test Is Minimized
**I**n software development, bugs are everywhere. Software is pretty infested when you get right down to it. As an engineer in quality, you will attack software from a variety of angles, in a variety of environments with a variety of different configurations. This takes a lot of time. Even with automation, CI jobs take considerable amounts of time to run. That coupled with the fact that quality engineering often has to build their own internal tools. It's not uncommon for quality to get some support on a task but for the support to be withdrawn before completion, often written off as "Not a priority". 

### What Devs Should Test
**O**f course, this depends. The term "developer" is a general term so coming up with a fixed rule would be difficult. But you could take a couple rules of thumb into consideration.

*1.) Developers should test functional units* **(Unit Tests)**

* Since developers are in the discipline of software design and construction, it's fitting to liken the units to individual blocks. So unit tests would be making sure that the bricks meet quality. Nothing will bring down your building quicker than building with wonky bricks. 


*2.) Developers should test the integration of their units* **(Integration Tests)**

* Would you have a construction worker build a house without checking that the bricks fit properly together? It is likely that a construction engineer would check that the bricks are symmetrical, fit properly together and can support the weight of other bricks. The construction engineer is a brick expert and mortar expert. This individual is the most qualified to see if the pieces coming together meet quality standards. Same is the case with development. Developers should write integration tests. Period.

![](http://uk-restoration.co.uk/wp-content/uploads/2015/04/Defective-Brick-Pointing.jpg)

### What QE Should Test
**Q**E should test the end product from as many angles as possible. Using our initial analogy, QE would walk in the house, open the doors, open the windows, turn on the lights, look at the foundation, etc. QE should not have to check the mortar and if the bricks align properly. The reason being: **The house is built.** Let's say we find a brick that is out of place. What's the process of fixing this issue? Would it have been better to find it back before the doors were put on and the windows were added? The answer is a resounding **YES**! 

**Q**uality engineering has a number of different tools and methods that are used to ensure quality on a product. But typically, it's from a [black box](https://en.wikipedia.org/wiki/Black-box_testing) standpoint. Even automated tests are typically from a black box point of view. 

**A**t the same time, we know that bugs will be found even if you have 100% test coverage. However, more coverage will prevent code being checked in that is overtly faulty and creating more work for all involved. It will also help you create a more stable software up front as your tests will ensure that existing functionality does not break due to a code change. 

#### Ways to Eliminate Variables In Testing
**O**ften, I am quite surprised to find how many development teams don't take advantage of virtualization. There are quite a few tools that have enabled quick setup of a development/testing environment that can really help speed things up and reduce variables. Products like [Vagrant](http://www.vagrantup.com) and [Docker](http://www.docker.com) are really light weight and can reduce/eliminate the whole "It works on my machine!" issue. 

**T**he cost of these types of tools are often minimal, except the investment in learning how they work. But the benefits can be prolific. It's definitely worth investigating.

 
## In Conclusion
**T**he shift from **QA** to **QE** is more mental than physical. It's a paradigm shift. It will often take pushing and produce push back. But once these hurdles are passed, the end result will be a more cohesive development unit. 