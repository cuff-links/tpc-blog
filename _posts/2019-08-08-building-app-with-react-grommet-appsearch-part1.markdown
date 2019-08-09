---
layout: post
title: "Building A Review App Using ReactJS, Elasticsearch, App Search and Grommet — (Part 1: Data)"
date: 2019-08-08
description: This article is part 1 of a series in which we use React, Elasticsearch App Search and Grommit to build a web application. 
tag: [software-development, javascript, react, grommet, components, app search, elasticsearch, nodejs]
---

I have been wanting to build an app for a while now. As a test automation engineer, I get to work with a lot of really cool tech and web apps but as a former web developer, I find myself needing to scratch the itch to build a web application, work with some of the newer JS tech and relearn some of the patterns that have become less familiar to me. To get started, we are going to take some things from the inter-webs.

# Our Data

We are going to start off with a sample data set that is found on Kaggle. This data is for different types of ramen noodles that can be found around the world and their ratings. We want to be able to search through these different types of Ramen, sort them, etc.
Let’s get our data going. I don’t want to have to configure an Elasticsearch cluster and everything myself. I would rather have Elasticsearch look at my data and do what’s best for it. This can be done with the App Search tool.

We are going to start in the standard UI for App Search (not the Onboarding tool) and create our first Engine. Let’s call it `my-ramen-engine`. We are also going to leave the language as Universal.

![UI For Creating new App Engines](https://thepracticaldev.s3.amazonaws.com/i/wsbzlradbweg5u867usz.png)


I took a look at our data and our data came in a .csv file. We need the format to be in .json. So we are going to use an online converter to get our data in the format we want. Once that’s done and we have our ramen_ratings.json file, we will upload it into `App Search`.

![Upload JSON To App Search](https://thepracticaldev.s3.amazonaws.com/i/psbl4dxektu5gbhoqw6i.png)

**~NOTE~**

The .csv file has capitals and spaces in the header row. That threw errors in App Search when I tried to import the data. The way I handled this was to change all fields to lowercase words and use underscores for spaces. For example, I changed Review # to review_number. Once done, we can import the file.

![](https://thepracticaldev.s3.amazonaws.com/i/xb3suo0mv6ks0prbffld.png)

When that’s done, we will be taken back to the Engine Overview page. From there, we want to make some adjustments to the Schema as all fields are imported as text by default. Let’s go ahead and get those updated to reflect their actual values. When we look at our schema, we see that `review_number`, `stars`, and `top_ten` need to be updated to `number`.

![](https://thepracticaldev.s3.amazonaws.com/i/7b9z26lz7isjylxz75ge.png)

**Uh oh! We hit a snag!**

We have some data quality issues. Some of our fields have data that cannot be changed to the number type.

![Top_ten rows that have invalid data.](https://thepracticaldev.s3.amazonaws.com/i/x9kpzr1k4t7ucj5adc3q.png)


![Stars rows that contain invalid data.](https://thepracticaldev.s3.amazonaws.com/i/kp75bec503xeznksakxi.png)



There are a few ways we can handle this. We can update the record via the API as outlined on the home page, we can delete the faulty records, or we can fix the data at the source, delete all records and reupload the JSON. I am just going to delete the faulty records since there aren’t very many of them and this is test data. If it were our actual production data, it would make sense to either edit or reimport that data so those records are maintained.

Once this is done, we will be at the documents page. We now have our indexed documents in an Elasticsearch instance that we will be able to make calls to query, etc. App Search will even provide us a nicely packaged React component to just drop into our app!  For the next part of the article, I will be diving into creating the actual app using React and Grommit!