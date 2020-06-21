---
layout: post
title:      "First Flatiron Project (CLI application)"
date:       2020-06-21 23:24:21 +0000
permalink:  first_flatiron_project_cli_application
---


![](https://cdn.pixabay.com/photo/2016/03/31/19/21/ballot-1294935_960_720.png)


For my first project at the Flatiron School, I decided to make a CLI application that could help people easily find information about their local elections. Since many overlook the importance of these local elections, this seemed to be a nice opportunity to both highlight them as well as make them easily accessible. 



**How it Runs**

My Ruby CLI application welcomes a new user and prompts them to enter their street address to get election information in their area. They can then choose any election in the returned list to learn more about the candidates running in that election. I chose to use the [Google Civic Information API ](https://developers.google.com/civic-information)because it contained the content I wanted and was also free and easy to use. 



**Taking the Training Wheels OFF**

It felt as if I started creating my project with a skeleton of classes and methods and then slowly layered the rest on bit by bit.

This project tested my recently learned knowledge of the Ruby language along with concepts including: 

* Object-oriented programming
* Working with API data
* Arrays and Hashes (JSON, in particular)
* Control flow (allow the user to do different things before exiting the program)

The project was definitely more challenging than the labs we’ve done at Flatiron School, but it was an opportunity for growth. It proved to show any cracks in my learning foundation and helped me to know what concepts I was comfortable with and what ones I was not. 


**Road Blocks**

There were definitely a lot of ups and downs during this project, especially when working with the API. But with time (and a lot of help from the `pry` gem and the API documentation) I was able to eventually have my program access the information I wanted. I later faced the problem of “what happens if a user gives invalid street address?” I wanted to have some kind of a check against such a situation. I coded the following to handle this situation:

```
    invalidAddress = true
    
    while(invalidAddress)
    
    puts "Please enter a valid street address (1263 Pacific Ave. Kansas City, KS) to see upcoming elections in your local area:"
    
    street_address = gets.strip
    
    if street_address == "exit" 
      exit
    elsif !/\d+.+(?=AL|AK|AS|AZ|AR|CA|CO|CT|DE|DC|FM|FL|GA|GU|HI|ID|IL|IN|IA|KS|KY|LA|ME|MH|MD|MA|MI|MN|MS|MO|MT|NE|NV|NH|NJ|NM|NY|NC|ND|MP|OH|OK|OR|PW|PA|PR|RI|SC|SD|TN|TX|UT|VT|VI|VA|WA|WV|WI|WY)[A-Z]{2}?/.match(street_address)
      puts "Invalid address! Please try again."
    else 
      invalidAddress = false
    end
    
  end
```



**What’s Next?**

There is definitely room for improvement with my project but I am proud of what I was able to make with only one month of learning code under my belt. I am super nervous for my first review but also excited to show what I’ve been able to make!!



*Check out my project by forking/cloning my repo [here](https://github.com/hkristin/my_cli)*



Best, 
Kristin

