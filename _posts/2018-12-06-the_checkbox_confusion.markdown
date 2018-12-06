---
layout: post
title:      "The Checkbox Confusion"
date:       2018-12-06 20:26:04 +0000
permalink:  the_checkbox_confusion
---


12/6  13:25
In my previous blog I talked about my Sinatra Project. I decided to not mention the fact that I was trying to implement a checkbox feature where the user can check if a list or potentially even its list items is completed. I had such a big issue with it though that eventually I decided to just leave it out. It is still bothering me that I did not focus on it more at that point. There was a study group where the bossman had issues with the checkboxes also - granted he figured it out fairly quickly - but it motivated me to take a deeper dive into the issue. 
Where exactly is the problem with checkboxes? My main issue was that when it is unchecked, it does not send a value. Kind of as if it does not exist. So how can there be a boolean if it is either true or nothing, not even nil - to my understanding at least. 
In the study group the issue arose in a form_for situation where the value was always 1, even when it was unchecked. The solution for that was to set values to 1 and 0 in its f.checkbox field. This basically gave me the idea to think about the situation a little more and at this point, this is as far as I have gotten. The post will be ongoing until I can find a solution or answer that is appropriate for me.
