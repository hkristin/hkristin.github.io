---
layout: post
title:      "My First Sinatra App!"
date:       2020-07-27 01:22:25 +0000
permalink:  my_first_sinatra_app
---



For my Sinatra project at the Flatiron School, I decided to try my hand at a Makeup Tracker App, in which a user creates an account that can keep track of their favorite makeup brands. Since I have a personal interest in makeup, this seemed to be a nice opportunity to incorporate an outside hobby into one of my coding projects!

**How It Runs**
My Sinatra Application allows a user to log in, sign up, and log out. Once an account is created,  a user will then be able to create a new makeup brand entry, see all the brands they have previously entered, edit those brands, and delete brands from their list. 

**Corneal Gem & Wireframing**
The Corneal gem is literally the best gem EVER! It took so much of the early work of making directories and files off of my shoulders. The usual panic of “where do I start?” was gone. 

From there, my wireframing felt much smoother. I set up my models, their attributes, and their associations fairly easily. My user model would have a name, email, and password. My user would have a has_many relationship to brands. My brands model would have a user id, palettes made by the brand, the age of the brand, and a boolean of whether the brand is considered clean or not. Brands then have a belongs_to relationship with the user.

This project tested my recently-learned knowledge of the Sinatra along with concepts including: 

MVC 
CRUD
Active Record
Validations

This project felt a bit heftier than my first, but overall really helped my understanding of how Sinatra works and why it is such a useful and timesaving programming application.

**Road Blocks**
There were definitely a lot of ups and downs during this project, especially when working with the validations. But with time (and a lot of help from the previous lessons and labs) I was able to eventually have my program protect the user’s information in the way I wanted.



**What’s Next**

There is definitely room for improvement with this project but I am proud of what I was able to make an entire application with only a few months of coding under my belt! I am excited for my next review to show what I’ve been able to make!!

Check out my project by forking/cloning my repo [here]!(https://github.com/hkristin/my_makeup_tracker_app.git)

Best, 
Kristin

