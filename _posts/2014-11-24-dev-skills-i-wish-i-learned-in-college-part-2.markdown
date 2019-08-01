---
layout: post
title: Dev Skills I Wish I Learned In College - Part 2
image: https://s3-us-west-2.amazonaws.com/thepowercoder/2016/11/digiletmemewithorder-e1410837673231.png
date: 2014-11-24
published: false
tags:
- software-development
- java
- debugging
- oop
- git
- javascript
- hoisting
- vcs
- version-control
- mercurial
- subversion
- github
- bitbucket
---

#Foreword
####What This Post Is Not
* This post is not to bash the education systems, college curriculums, or any other programs offered by institutions of higher learning. This is just a sharing of my experience while acquiring my degrees. While I was in school, I was also working in the industry and I noticed a very large disconnect between the content of our curriculums and the standards of the industry. 
* This post is not an experience that is based on every institution out there. This means that experiences will vary. 

<h6>This post is a continuation of the <a href="http://www.thepowercoder.com/blog/dev-skills-i-wish-i-learned-in-college-part-1/" target="_blank">Dev Skills I Wish I Learned In College</a> Series</h6>

<br />
###Linux
Knowing how to work with *Unix* based operating systems is a much valued skill for any who want to do work in IT outside of the realm of **.NET**. If you are working with web applications, you will notice that tons of web hosts provide *Linux* based operating systems. Many of our favorite platforms derive from the Linux platform like *Mac OSX* and *Android*. Unfortunately, I didn't even hear of *Linux* in my curriculum. We exclusively worked with *Windows* based machines and tools. Shell scripting is something else I didn't hear of until I branched out and did some experimenting with different tools and operating systems. 

###JavaScript
I was so disappointed when found out how prominent **JavaScript** is in the development world, post-graduation. In my curriculum, I wrote more lines of **VB.NET** and **Perl** than **JavaScript**. I find that to be very sad. The little **JavaScript** we wrote was core **JavaScript**. But we really didn't get much extra information about how **JavaScript** works and how it's so different from other programming languages. A few things that would have been nice to learn:

* **`Object Oriented JavaScript`** -  I spent a long time trying to find out how to write a class in **JavaScript**. Want knowledge of prototypes? Get it on your own time!
* **`Scope`** - Global namespace? What? This concept didn't register because **C#** and **Java** don't function the same way. 
* **`Debugging`** - Well, since you debug **JavaScript** in a browser, one must know that those developer tools exist.
* **`== vs ===`** - I had only worked with languages that used == for comparisons. I thought all of the code samples I saw had typos. 
* **`Hoisting`** - I had no idea that it was actually a variable declaration may be hoisted to the top of the function. This could cause issues if you are coming from a language like **Java** where the variable would already be in scope and it's value would be used rather than looking for that variable in the function. Example time!

**Java** Example:
```java
//Code
...
private int number = 1;
public static void someFunction(){
	System.out.println(number);
    int number = 2;
    System.out.println(number);
}
```
```
Output:
1
2
```
**JavaScript** Example
```javascript
//Code
...
var number = 1;

function printStuff(){
	console.log(number);
    var number = 2;
    console.log(number);
}
```
```
Output:
Undefined
2
```

Due to the way the scoping mechanism works in **JavaScript**, it searches the function for declarations of the variable first. It found it, though it was undefined. Hence, the output. 


With front-end development being red hot right now, it's a bit of a disservice not having it in the curriculum. **JavaScript** has become a full-fledged language that can run on all platforms. There are mobile applications written in **HTML5** and **CSS**, server-side **JavaScript** applications allowing for manipulating files on the server and of course web applications using **JavaScript**. As a developer, keeping up with current tech is imperative to stay competitive. Having skills that can be applied to a number of different areas definitely helps with that. 

###Version Control Systems
Since developers hardly ever work on a project alone, an important concept is to be able to collaborate on a source code level. Knowing how to effectively use a **VCS** (i.e *git*, *Subversion*, *Mercurial*) is key. *Git* is very popular these days and many hosted git solutions offer free accounts for students and open source projects (i.e *Github* and *BitBucket*) to house your code. 
Fortunately for me, a developer that I worked with was kind enough to mention that I should familiarize myself with version control. Since my curriculum had no team projects, or pre-existing code to make modifications to, I decided to just use *Git* (via *Github*) to familiarize myself with the tool. I learned how to merge and branch, though I was a solo developer on all projects. I also got to access other open source projects and learn from them.  

In part 3 of this series, I am going voice to cover a few more concepts that would have been beneficial to learn and give my opinion on some possible changes that could be me made to improve the content of the curriculums. Of course, these are all my opinion. But I can say, from my experience, the industry is moving more rapidly than the educational system and it's creating a large gap. Emerging students are shocked at the interview questions they are expected to know and companies are spending tons of money on a recruiting process that often seems unfruitful. 