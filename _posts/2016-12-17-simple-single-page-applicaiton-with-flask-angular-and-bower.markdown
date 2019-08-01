---
layout: post
title: "Simple Single Page Applicaiton with Flask, AngularJS  and Bower"
img: angularjs_flask.jpg
date: 2016-12-17
description: This article gives us an easy way to start building a Single Page Application with Flask, AngularJS and Bower
tag: [software-development, javascript, angularjs, flask, python, bower, SPA, MVC, virtualenv, pip, nodejs, npm, hello-world]
---


With the whole host of new Angular goodness making its way to the mainstream, I asked myself whether it was worth it to learn the entire new Angular2 workflow and set of tools for my small site. For this project, the answer is no but I did go ahead and work with one new tool. [Flask](http://flask.pocoo.org/). I am writing this post to document my process and to help anyone else who may be trying the same.  

Oh, before we start. This project's code lives in a [Github](https://github.com/silne30/flask-angular-hello-world) repository. 

## New Project Setup

Project Prerequisites:
`nodejs > 6.0` <br />
`npm > 3.0` <br />
`Python == 2.7`

This project will also assume that you know how to set up a virtual environment for python. If not, [see this post](http://docs.python-guide.org/en/latest/dev/virtualenvs/).

Let's create the directory structure for your hello flask project.
```
hello_flask (root)
└── hello_flask
    ├── static
    │   ├── css
    │   ├── img
    │   ├── js
    │   │   └── vendor
    │   └── partials
    └── templates
```
Now that we have the skeleton of our project ready, we can start getting our environment together.

We are going to need the Flask framework as it is the server side of our project. (Make sure you are in your virtual environment!)

`pip install flask`

You will notice that [Flask](http://flask.pocoo.org/) installed but also something called [Jinja2](http://jinja.pocoo.org/docs/dev/) installed. That's our templating engine. We will work with that more later.

We are also going to be using bower to manage our JS dependencies. So let's install [Flask-Bower](https://pypi.python.org/pypi/Flask-Bower/). It's a python package that helps Flask work with Bower. 

`pip install Flask-Bower`

That's all for the python package installations. Let's go ahead and configure bower.

Create a file at the root of your project called .bowerrc

Open that file and add the following line:

`.bowerrc`

```
{ "directory" : "hello_flask/static/js/vendor" }
```
What this does is make it so when you install any libraries via bower, it gets placed right into the vendor folder. (If you are using git, place the vendor folder in your .gitignore)

Now we will initialize bower.

`bower init`

You will be asked some basic questions about your project. My answers (in quotes) were something along these lines.

```
? name  "hello_flask"
? description "hello world application in flask"
? main file "hello_flask.py"
? keywords "flask, angular, bower, grunt, hello world"
? authors "John Dorlus <jsdorlus@gmail.com>"
? license "MIT"
? homepage "https://www.github.com/silne30/hello_flask"
? set currently installed components as dependencies? "Y"
? add commonly ignored files to ignore list? "Y"
? would you like to mark this package as private which prevents 
it from being accidentally published to the registry? "N"
? Looks good? "Y"
```
OK. We will come back to Bower later. For now, let's start getting our flask bits together. Within the child hello\_flask directory, create a python file called hello\_flask.py

In it, add the following code.

`hello_flask.py`
```python
from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello_world():
	return "Hello World"

if __name__ == '__main__':
    app.run()
```
Your directory structure should now look like this.
```
hello_flask (root)
├── bower.json
└── hello_flask
    ├── hello_flask.py
    ├── static
    │   ├── css
    │   ├── img
    │   ├── js
    │   │   └── vendor
    │   └── partials
    └── templates
```
If all looks well, let's run our app! 

`python hello_flask.py`

Now go to your browser navigate to `localhost:5000`

![Hello_World](https://s3-us-west-2.amazonaws.com/thepowercoder/2016/12/Screen+Shot+2016-12-16+at+1.05.14+PM.png)


Congrats! You now have a basic hello world, app. But this is not the Angular app we were looking for. What we are going to do now is use flask to serve the landing page for the site and let Angular serve the subpages. This will turn your app into a Single Page Application. 

Let's go into your hello\_flask.py file again and make a change. Instead of the hello\_world method, we are going to do a catch all. We are also going to set up Flask-Bower to work with your application and name your application. 

`hello_flask.py`
```python
from flask import Flask, redirect, render_template
from flask_bower import Bower

app = Flask('hello_flask')


@app.route('/', defaults={'path': ''})
@app.route('/<path:path>')
def catch_all(path):
    return render_template('index.html')


if __name__ == '__main__':
    Bower(app)
    app.run()
```
This code is doing a couple of things. It's routing all requests through the default path and rendering the index page. From there, Angular will intercept the request display the desired page (or 404).
Don't run this just yet because it's not going to work. We don't have an index.html template.....yet.

Create a new file within your templates folder called......you guessed it. 

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello Flask Application</title>
</head>
<body>
	<h1> This is our awesome Hello Flask app!</h1>
</body>
</html>
```
If you refresh your page, you will see this:

![Awesome_Flask_App](https://s3-us-west-2.amazonaws.com/thepowercoder/2016/12/Screen+Shot+2016-12-16+at+9.20.16+PM.png)

Now, this is good. But you will notice one thing. If you visit `localhost:5000/about`, you get the same page. In fact, no matter what page you visit, you get the exact same page. This is where Angular will come in to handle some more of our routing.

We are going to enlist the help of a few Angular packages. Namely, Angular and Angular Route.

`bower install angular --save`

`bower install angular-route --save`

Your directory structure should look like this now:
```
hello_flask (root)
├── bower.json
└── hello_flask
    ├── hello_flask.py
    ├── static
    │   ├── css
    │   ├── img
    │   ├── js
    │   │   └── vendor
    │   │       ├── angular
    │   │       └── angular-route
    │   └── partials
    └── templates
        └── index.html
```

Now we are going to modify the index.html page to load the 2 Angular scripts and to add the entry point for injection of the data received from the controller.

`index.html`
```html
<!DOCTYPE html>
<html lang="en" ng-app="hello_flask">
<head>
    <meta charset="UTF-8">
    <title>Hello Flask Application</title>
    <script src="/static/js/vendor/angular/angular.js"></script>
    <script src="/static/js/vendor/angular-route/angular-route.js"></script>
</head>
<body>
	<h1> This is our awesome Hello Flask app!</h1>
	<div ng-view></div>
</body>
</html>
```
Now we need to add a few JS files. It's going to go under the js directory. 

`app.js`

~~~javascript
'use strict';

var app = angular.module('hello_flask', [
    'ngRoute',
    'controllers',
]);

app.config(['$routeProvider','$locationProvider', '$interpolateProvider',
    function($routeProvider, $locationProvider, $interpolateProvider){
        $routeProvider
        .when('/', {
            templateUrl : 'static/partials/home.html',
            controller  : 'HomeController'
        })

        .when('/about', {
            templateUrl : 'static/partials/about.html',
            controller  : 'AboutController'
        })

        .otherwise({redirectTo: '/'});

        $interpolateProvider.startSymbol('{a');
        $interpolateProvider.endSymbol('a}');

        $locationProvider.html5Mode({
            enabled: true,
            requireBase: false
        });
}]);

~~~

`controllers.js`

```javascript
'use strict';

var app = angular.module('controllers', []);

app.controller('HomeController', ['$scope', function($scope){
    $scope.message = 'Hello from HomeController';
}]);

app.controller('AboutController', ['$scope', function($scope){
    $scope.message = 'Hello from AboutController';
}]); //No comment
```
There is a lot going on here. We'll start with app.js.

We declare the angular app called "hello_flask" and list its dependencies, [`ngRoute`](https://docs.angularjs.org/api/ngRoute) and controllers. We then configure the application. We use [`$routeProvider`](https://docs.angularjs.org/api/ngRoute/provider/$routeProvider) to route our URLs to different template files. These templates will handle injection of data for that specific URL. So the '/' route will route to the home template which will have stuff pertaining to home. We will create those templates in a bit. That will be injected into the layout page (index.html).

The [`$locationProvider`](https://docs.angularjs.org/api/ng/provider/$locationProvider) prettifies our URLs so we don't wind up with `http://localhost:5000/#!/about`, just `http://localhost:5000/about`.

The [`$interpolateProvider`](https://docs.angularjs.org/api/ng/provider/$interpolateProvider) changes the syntax for injecting data into the templates. Both flask and Angular use double curly braces "{{}}" to inject data. So we will change the Angular side to use "{a a}"

Now, let's take a look at controller.js

Controllers in Angular are responsible for getting data to the [`$scope`](https://docs.angularjs.org/guide/scope) which is accessible from the templates. This $scope variable in this example is given a string that will be displayed in your template (i.e home.html). Angular has a bunch of nifty ways to display, filter and manipulate the data presented by $scope.

OK. So let's create home.html and about.html in the partials folder. They will be very simple but have obvious differences so we know that Angular is working.

`home.html`
```html
<h2> {a message a} </h2>
```
`about.html`
```html
<ul>
  <li>{a message a}</li>
  <li>{a message a}</li>
</ul>
```
So it will be obvious when the page switches. Our last change will be to index.html. We need to include the other files we created and add some links on the main layout for easy navigation. 

`index.html`

```html
<!DOCTYPE html>
<html lang="en" ng-app="hello_flask">
<head>
    <meta charset="UTF-8">
    <title>Hello Flask Application</title>
    <script src="/static/js/vendor/angular/angular.js"></script>
    <script src="/static/js/vendor/angular-route/angular-route.js"></script>
    <script src="/static/js/app.js"></script>
    <script src="/static/js/controllers.js"></script>
</head>
<body>
	<h1> This is our awesome Hello Flask app!</h1>
    <a href="/">Home</a>
    <a href="/about">About</a>
   	<div ng-view></div>
</body>
</html>
```
At the end of all of this, you should have a directory structure like this:

```
hello_flask (root)
├── hello_flask.py
├── static
│   ├── css
│   ├── img
│   ├── js
│   │   ├── app.js
│   │   ├── controllers.js
│   │   └── vendor
│   │       ├── angular
│   │       └── angular-route
│   └── partials
│       ├── about.html
│       └── home.html
└── templates
    └── index.html
```

Now we can run this! The home page should display this:

![Angular_App_Home_Page](https://s3-us-west-2.amazonaws.com/thepowercoder/2016/12/Screen+Shot+2016-12-16+at+9.39.49+PM.png)

If you click on the About link, you should see this.

![Angular_App_About_Page](https://s3-us-west-2.amazonaws.com/thepowercoder/2016/12/Screen+Shot+2016-12-16+at+9.40.09+PM.png)

That's it! You have written your hello flask app with a little Angular flare! Should I make a part 2 of this? Did I make any mistakes? Please comment! 

# Credits

My wife for helping me bounce ideas off her. Thanks, honey! ^_^

Thanks to [@tarek_ziade](https://twitter.com/tarek_ziade) for introducing me to Flask and giving me a crash course on it.

[Simple SPA in Angular](https://tests4geeks.com/single-page-application-using-angularjs-tutorial/) (Needed a refresher)

This [Stack Overflow Answer](http://stackoverflow.com/questions/30362950/is-it-possible-to-use-angular-with-the-jinja2-template-engine) Regarding Jinja2 and Angular conflict

Post Photo Credit: [Robert W Dempsey](http://robertwdempsey.com/application-skeleton-flask-angularjs/)

