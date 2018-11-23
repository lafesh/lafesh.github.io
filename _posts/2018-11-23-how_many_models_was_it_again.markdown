---
layout: post
title:      "How many models was it again?"
date:       2018-11-23 23:11:34 +0000
permalink:  how_many_models_was_it_again
---


This month's project was fairly easy up until I ran into problems and got stuck. Let me start from the beginning though. I had an idea for an application right away. I was planning on building an organizational app where the user can create, edit, delete lists.
I started with creating the signup/login pages and the security measures I wanted to have included. Instead of redirecting to a failure page, I used Sinatra Flash to built error flash messages. 
Originally I created two models, one user that has many lists and a list that belongs to a user. There are three application controllers, the original applicaton controller, a users controller and a lists controller. I built all the routes and view files and everything worked the way I wanted to - mostly. 
My list table includes a list item and I was unhappy with the idea of me - the creator - putting down a set amount of list item fields when the user creates or updates their list. I have no idea what list that person is creating and if he needs 4 or 20 input fields. I looked into dynmaically adding input fields and found jquery which would make that work. After a lot of trial and error I finally figured out where and how to put it in my code to make it work for a sinatra application. 
The problem arose quickly after. Now that there was more than one list item input field, I got an array in my params that would not transfer over as an array but as an array wrapped in a string. A solution for that was to rollback my migrations, create a new table called list items and a new model list item that belongs to list. The list model then has many list items. This however, created a whole nother chain of events. It made everything stop working. I had to create and update the list a different way in the post and patch requests. Once that code was updated everything worked again. 
This project has potential to be built out a lot more. I have ideas for creating a settings page that will let you delete your account and update the user information. I also want to add a checkbox to each input field so that the user can check off that specific item. 
All in all I really enjoyed this project. Even though there were a few struggles, I had a lot of fun with it.
