---
layout: post
title:      "Cape Cod Beaches with a View of JS"
date:       2020-09-20 23:23:22 +0000
permalink:  cape_cod_beaches_with_a_view_of_js
---

![](https://www.whoi.edu/wp-content/uploads/2020/04/beach-stairs.jpg)


For this project, I decided to focus on something close to home, in fact exactly where my home is, Cape Cod, MA! There are many towns on Cape Cod. The beaches here are beautiful and I thought the relationship of them belonging to a town would set up nicely for this assignment. 

## Rails API

The first hurdle of this project was making the backend. However, since we've spent some significant time in Ruby on Rails, this really seemed to fly by. With the help of scaffolding, most everything I needed was set up immediately. All that I had to do now was change around my index and show actions to render in json.
``` 
def index
    @towns = Town.all
    render json: @towns.as_json(include: {beaches: {only: [:id, :name, :length_of_beach]}})
 end
	
```
In this code snippet above, I also use `.as_json(include)` in order to serialize the town and beach data into a nice json format (so that it is usable for the front end). Then, I was able to focus on setting up my seed data so that I would have something to work with on the front end. I chose to write seed data for the towns that would be unalterable by the user (towns can't be deleted) as well as some starter beaches.

## JS Front End

The second half of this project involved much more effort, as Javascript is newer to us, and we were asked to build out all of the files from scratch. Luckily, forms are fairly similar in JS and Ruby so writing out the index.html went quite smoothly actually. I made sure to connect the script for the different files to the index.html page so that it would run all the necessary files to operate properly. The script that I used is listed below:
```
<script type="text/javascript" src="services/api.js"></script>    
<script type="text/javascript" src="models/town.js"></script>
<script type="text/javascript" src="models/beach.js"></script>
<script type="text/javascript" src="src/index.js"></script>
```

Another huge piece for me was the creation of my api.js file. This file is where I chose to put all of my AJAX fetch requests so that they were neatly layed out and organized. I wrote 4 static methods in this file, to load Towns and Beaches, and then to add and delete Beaches. The toughest of these methods for me to write was my `addBeach` method that I have listed below:
```
static addBeach(e){
        e.preventDefault()
    
        //let sel = e.target.elements[3].options
        let data = {
            'name': e.target.name.value,
            'length_of_beach': e.target.length_of_beach.value,
            'image': e.target.img.value,
            'town_id': e.target.elements[3].options[e.target.elements[3].options.selectedIndex].value
        };
        
        fetch(`http://localhost:3000/beaches`, {
            method: 'POST',
            headers: {
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
        .then(resp => resp.json())
        .then(beach => {
            const { id, name,length_of_beach, image, town_id} = beach
            const newBeach = new Beach(id, name,length_of_beach, image, town_id)
            document.getElementById('beach-form').reset()
        })

    }
		```
These fetch methods are what keep the application together by creating communication between the front and back ends.

## Final Thoughts
Working on this application definitely had its challenges and pushed my understanding of JavaScript, but I am so grateful for it. I have a much better grasp on all the different elements we were taught and putting things all together in one application felt amazing, especially creating both a back and front end. I am as usual, nervous for my project review, but also excited for it! 
