---
layout: post
title: Dev Skills I Wish I Learned In College - Part 1
image: https://s3-us-west-2.amazonaws.com/thepowercoder/2016/11/digiletmemewithorder-e1410837673231.png
date: '2014-11-05 00:20:01'
published: false
tags:
- software-development
- java
- debugging
- curriculum
- interfaces
- abstraction
- oop
- logging
- c
---

#Foreword
####What This Post Is Not
* This post is not to bash the education systems, college curriculums, or any other programs offered by institutions of higher learning. This is just a sharing of my experience while acquiring my degrees. While I was in school, I was also working in the industry and I noticed a very large disconnect between the content of our curriculums and the standards of the industry. 
* This post is not an experience that is based on every instution out there. This means that experiences will vary. 
####My Educational Background
I am 2 courses away from finishing my Bachelor's of Applied Science in Software Development (They are more of a formality since the courses have nothing to do with Software Development). I springboarded into that degree track from an Associates of Applied Science in Computer Programming and Analysis *(how I went from pursuing an Associates in Arts and Bachelor's in Computer Science to this track is a topic for another post)*.

###Debugging Skills
   Lack of debugging skills are a sad situation that many new developers with that shiny new degree find themselves having to deal with. You see, in the *"School World"*, students are given a number of different projects to work on, from scratch. All of the code they work on and troubleshoot is their own. This would be great for the students if the *"Real World"* mimicked this model. 
   But the truth is, in the real world, a developer is interacting with code that was created by MANY developers. Perhaps in many different languages, using different patterns and architecture styles. I have witnessed certain things happening to new developers that have little experience debugging.

**1. A fear of errors**<br />
This is a sad thing to see. I had a classmate develop a program with the following code:

<pre><code class='java'>
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello World"; //The missing parenthesis is not an accident.
	}
}
</code></pre>
Naturally, the above displayed code has a small error in syntax. For 3 days, my classmate filled our forums with posts (in all caps) saying Eclipse is broken. The program doesn't work. Eclipse placed a nice little message in his console saying "Error: Missing parenthesis )". He never read the error. We told him to and he refused. As a developer, your errors and stack traces become your breadcrumbs when you are finding what went wrong in your application. They are to be investigated, not avoided. This trend did not stop, unfortunately. He eventually switched majors. 
This is an extreme example of what can happen. There is a fear of errors and since students are usually working with their own code, they are not used to handling different errors like Runtime Exceptions. When they get out into the world with this lack of training, it's a shocker to them to say the least. 
  
**2. No concept of logging**<br />
Since there were no existing systems for the new students to work on, it was up to the students to develop their own systems. More often than not, there was no logging because it was not part of the curriculum nor the programming book that was used to teach the course (which normally have very poor reviews) so the student did not have any introduction to logging. Imagine their surprise when they are told to check the tomcat logs to see what went wrong in their first job. It's an avoidable issue. 

**3. Copy and Paste Syndrome**<br />
This issue is perhaps the most serious. Enough time working with software and can get over your fear of errors. You can also learn to use logs and create logs in your own code. But copy and paste syndrome can become a vicious habit that seeps into the very core of their development habits. I am not saying that searching the internet for help with an issue is wrong, but some developers simply copy and paste solutions from Stack Overflow into their code without digging deeper as to why it fixed the issue. A couple of suggestions when using Stack Overflow (or any other source for help with your problems):

* Read all of the answers and comments. See why the answer is the answer and how the developer explains it. 

* Before pasting the code into your own, check to see how it differs from what you attempted and see if you can find out why theirs worked instead of yours.

Debugging skills are integral for a software developer. Unlike other roles where one can hit the "Send Error Report" button and wait for a solution, we are the ones responding to those reports. So we **have** to be able to sort through the code and resolve issues as they arise. 

##Software Architecture (i.e. S.O.L.I.D Principles, SoC, SOA)
Of all of the skills I wish were a focus of my curriculum, **this would have to be number one**. You can figure out how to use logs and , if one is diligent enough, you can get over your fear of errors, but if you don't properly learn about software architecture, object oriented analysis and design, you are severely crippled in the industry. Before I go on, I'd like to mention:

* I did all assignments given, plus many that were not assigned. 
* I did my own side projects to familiarize myself with things not covered in classes. 
* I actively helped out classmates with their assignments and even lead some Meet-ups with fellow classmates that were struggling. 

With that said, I would like to say that I had no idea what an *interface* was until after I completed my A.S. Degree. When I say *interface*, I am not speaking of the user interface. I mean the construct in Java or C# (those were the languages I took) that allows you to define behavior that objects are to have. In these languages, the interface is an important construct. 
Another concept that didn't get introduced were *abstract classes*. In other words, the concept of **abstraction** was completely foreign to me, yet I was a graduate that was supposed to be able to start working in the industry. 
Needless to say, adhearing to S.O.L.I.D or any other methodology that allows for extensible, maintainable code is more difficult in these languages if you aren't aware of important constructs. 

To illustrate we have an example of something I would have written prior to learning about abstraction:
######Cow Class
```java
public class Cow {
	public void moo() {
    	System.out.println("Mooooo!");
    }
}
```

```java
public class Snake {
	public void hiss() {
    	System.out.println("Hissssss!");
    }
}
```

```java
public class Dog {
	public void bark() {
    	System.out.println("Woof! Woof!");
    }
}
```
```java
public class Cat {
	public void meow() {
    	System.out.println("Meeeoow!");
    }
}
```
```java
public class CreatureTest {
	public static void main(String[] args) {
    	Cow cow =  new Cow();
        Cat cat = new Cat();
        Dog dog = new Dog();
        Snake snake = new Snake();
        
        cow.moo();
        cat.meow();
        dog.bark();
        snake.hiss();   
    }
}
```

```
Output:
Mooooo!
Meeoow!
Woof! Woof!
Hissssssss!
```

Now, a couple comments about the  aforementioned code. This would have gotten me an A. Not only that, I would not have gotten feedback about abstractions, at all. I could understand perhaps in "Intro to Programming" this passing for a first try but I really think that a developer's eyes should be opened to writing software to support the big picture. Objects can be categorized by how they relate instead of taking them on one by one. If this code were to continue, I would have a Parakeet object with the tweet method, a Pig object with an oink method, a Fox object with a **"what does the fox say?"** method, etc. 

A simple example of the same functionality using abstractions would be something to this effect: 

```java
public abstract class LivingThing {
	abstract void drinkWater();
    abstract void eatFood();
}
```
Small note about what is going on here. This system seems to be working with LivingThings so we make an abstract class that means any classes derived from this abstract class are also living things. All living things need water and food so we have those behaviors apply to all living things. We won't go into the implementation of **drinkWater()** and **eatFood()**. They are shown to illustrate how an abstract class can be used. 

But we may have some living things that don't behave like others. Some may move, some may not. Some may speak, some may not. For the sake of our previous examples, we notice that all of our objects are Land Animals. They are all performing land animal type behavior as well. Why did I choose **Land Animal** rather than just **Animal**. Well, if we had a Sea Snail as an example, would it speak? Does it behave like animals on land do? Not exactly. So, I created a specific interface as close to my objects as possible.
<pre><code data-language="java">
public interface LandAnimal {
	public void speak();
}
</code></pre>

So how can we use these abstract ideas an apply them to our examples. Let's look at the Cow. Is the Cow a living thing? Yes. Is the Cow a land animal? Yes. So the Cow object can be a derived class from LivingThing and implement the Animal interface.

```java
public class Cow extends LivingThing implements LandAnimal {
	public void drinkWater() {...}
    	
    public void eatFood() {...}
    
    @Override
    public void speak() {
    	System.out.println("Mooooo!");
    }
}	
```

```java
public class Dog extends LivingThing implements LandAnimal {
	public void drinkWater() {...}
    	
    public void eatFood() {...}
    
    @Override
    public void speak() {
    	System.out.println("Woof! Woof!");
    }
}	
```

<pre><code data-language="java">

public class Cat extends LivingThing implements LandAnimal {
	public void drinkWater() {...}
    	
    public void eatFood() {...}
    
    @Override
    public void speak() {
    	System.out.println("Meeeoow!");
    }
}	
</code></pre>

```java
public class Snake extends LivingThing implements LandAnimal {
	public void drinkWater() {...}
    	
    public void eatFood() {...}
    
    @Override
    public void speak() {
    	System.out.println("Hissssss!");
    }
}	
```
```java
public class CreatureTest {
	public static void main(String[] args) {
    	LandAnimal cow =  new Cow();
        LandAnimal cat = new Cat();
        LandAnimal dog = new Dog();
        LandAnimal snake = new Snake();
        
        cow.speak();
        cat.speak();
        dog.speak();
        snake.speak();   
    }
}
```
```
Output:
Mooooo!
Meeoow!
Woof! Woof!
Hissssssss!
```

As you could see by the second example, the objects are grouped into categories and ideas that keeps code structured and organized. If I add a new LandAnimal, I just need to make sure it implements the **speak()** method with its own implementation of it. Of course, these were simple examples to illustrate the ideas that I was not familiar with by the time I got my A.S. Degree. 

Part two of this series is going to go a bit deeper into concepts that were not part of my curriculum as well as technologies that were not introduced that I feel are integral to a developer. Stay tuned for more. This is my first blog so feel free to comment below about what you think. 