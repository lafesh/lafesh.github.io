---
layout: post
title:      "How many models was it again?"
date:       2018-11-23 18:11:35 -0500
permalink:  how_many_models_was_it_again
---

Hello everybody! Welcome to another episode of the Gina Struggles.
This month's project was all about building a complete Sinatra application with an MVC paradigm, ActiveRecord, has_many/belongs_to relationships, user information, validations and error messages. I decided to go with a list application that lets a user create, update and delete his own lists,  offers a community tab where you can see other user's lists and search for specific people's lists. 
It was fairly straight forward to set up. I started  with creating the signup/login pages in a users_controller and security measures that would render flash messages instead of redirecting to an error page, like so:

```
post '/login' do
        user = User.find_by(email: params[:email])
        if user && user.authenticate(params[:password])
            session[:user_id] = user.id
            redirect '/lists'
        elsif params[:email].empty? || params[:password].empty?
            flash[:message] = "Please fill out all the fields."
            redirect '/login'
        else 
            flash[:message] = "We could not find you in the database. Please Sign Up"
            redirect '/signup'
        end
    end
```

I created two models, one was a user that has many lists and the other was a list that belongs to a user. Once signed in, I wanted all the routes within to be written in the lists_controller for easy understanding. View files got created according to the routes and they worked perfectly. 
A problem arose when I realized that I needed to put a set amount of list_item in a form to create a list. But since I, as the creator have no idea how many item a user wants in a list, I felt the need to fix this somehow. What I needed was to dynamically add input fields on the press of a button by a user. In comes jQuery. Even though it was not part of the requirements - Javascript and jQuery we would learn two months later - I needed to use it anyways. This app needed to be perfect and without that it just did not make sense. There is not that much documentation out there on how to implement jQuery into a Sinatra application. Most projects that use Javascript would be Rails instead. After a lot of trial and error I finally figured out where and how to put it in my code to make it work for a sinatra application. The layout file was the perfect place, and I implemented jQuery right there: 

```
<head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge, chrome=1" />

    <title>ListsApplication</title>

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>
    <script>
      $(document).ready(function() {
        $("#add").click(function(e){
          $(".items").append('<div>List Item: <input type="text" name="list[list_items][][item]">' + '<input type="button" value="delete" id="delete"></div>')
        });
        $(".items").on("click", "#delete", function(e){
          e.preventDefault(); $(this).parent('div').remove();
        });
      });
    </script>

    <link rel="stylesheet" href="/stylesheets/main.css" />
  </head>
```

The biggest issue arose quickly after. Now that there was more than one list item input field, I got an array in my list params that would not transfer over as an array but as an array wrapped in a string. I was stumped for a long time, thinking that there must be an easy way to fix it. As it turns out, there wasn't so as a solution, I had to rollback my migrations, create a new table called list items and a new model list item that belongs to list. So I basically needed to rework my whole application including its post and patch requests. 
The new list_items model belongs to a list and the list model has many list items in return.  Once that code was updated everything worked again. 

I added some simple CSS to improve the looks of it but mainly just focused on the app working properly. I tried to think of as many edge cases as possible to eliminate any errors in those areas. 

Overall I am very proud of what I have achieved. The debugging and problem solving was definitely not easy but I still enjoyed every minute of it! Onto the next project!

