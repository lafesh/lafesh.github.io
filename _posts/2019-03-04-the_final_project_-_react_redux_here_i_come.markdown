---
layout: post
title:      "The Final Project - React/Redux Here I Come!"
date:       2019-03-04 21:41:26 +0000
permalink:  the_final_project_-_react_redux_here_i_come
---


It has been 6 months of an incredible experience and I have arrived at the last project. As everybody always says: Time flew. I cannot believe I have arrived at the end already. The best part about it was that I already knew what I was going to do about my project and that I was incredibly excited about it. Today is Thursday, I started on Monday and my project is done as far as requirements go. It always took me over a week and there was a lot of stress involved. This time though it was just pure determination and excitement.

So let me tell you about my  project. It is a one page application that lets you choose a charity and donate to them. You immediately see an accordion style list of charities. Once you click on one, there will be a dropdown with its category, a short description and the percentage of your donation that will go directly to their cause. A donate button is also in there and when you click on it you get directed to a form where you put in your credit card information and your donation amount. Once successfully filled out you will see a donation confirmation and can go back to all the charities. I also implemented a search bar to be able to specifically look for a charity. In order to comply with the projects' requirements I also created a new charity form that will send a post fetch request to my rails charity application to add said charity to the database. Not all the features are implemented yet, the donation form does not actually do anything yet and I would like to implement a paypal option eventually but neither of those are part of the requirements so this will be a future project once I finished my school program. 

Debugger, as always, was my best friend in this project. If I ran into any issues I just added it into one part that could have been the issue and then kept going back further until I figured it out. A lot of the coding was actually a lot of styling. I had a vision in my head and I wanted it to look somewhat similar, so everytime I created a component I immediately designed it to my liking to make sure it would look the way I wanted it to.

The biggest issue I had was getting my fetch post request to work. I did not fully understand the significance of the headers key so it took me a little bit to figure out how to make this work. I also decided to add error handling for both my fetch requests so my charityActions file ended up looking like this:

```export function fetchCharities() {
    return (dispatch) => {
        dispatch({ type: 'LOADING_CHARITIES' })
        return fetch('http://localhost:5000/charities')
        .then(handleErrors)
        .then(response => response.json())
        .then(charities => {dispatch({ type: 'FETCH_CHARITIES', charities})})    
        .catch(console.log)    
    }
}

export function addCharity(charity) {
    return (dispatch) => {
        fetch('http://localhost:5000/charities', {
        method: 'post',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify( charity) 
    }).then(handleErrors)
    .then(res => res.json())
    .then(charity => dispatch({ type: 'ADD_CHARITY', charity}))
    .catch(console.log)
    } 
}

function handleErrors(response) {
    if (!response.ok) {
        throw Error(response.statusText);  
    }
    return response;
}
```

So now I just need to figure out the Paypal and Credit Card situation and once that is figured out I have not just a demo but a fully functioning application which is absolutely amazing!



