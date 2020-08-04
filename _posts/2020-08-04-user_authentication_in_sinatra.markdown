---
layout: post
title:      "User Authentication in Sinatra "
date:       2020-08-04 21:28:42 +0000
permalink:  user_authentication_in_sinatra
---

![Rusty Lock](https://cdn.pixabay.com/photo/2016/08/12/08/01/door-1587863_1280.jpg)


Logging in is basically second nature to most people at this point, but many who are new to programming don't necessarily know what is going on behind the scenes. In Sinatra there is a perfect chance for us early learners to focus on user authentication! 

The key to **authentication** really lies in our User model and the beauty that is the has_secure_password. By adding this simple line of code to our User model, we are actually creating an authenticate method INVISIBLY when we run our program.

In the meantime, over in our User controller, we have our POST '/login' method, which of course first identifies the user with find_by searching for a username. 

Then the invisible authenticate method from the User model is called on to verify the user's password. If so, a session is created!

```
post "/login" do
  user = User.find_by(:username => params[:username])
 
  if user && user.authenticate(params[:password])
    session[:user_id] = user.id
    redirect "/success"
  else
    redirect "/login"
  end
end
```


The code above describes a simple post action to a route called "/login". Assuming we've submitted a form with a user's login credentials, we first try to locate the user in the database with `User.find_by(...)`. Next, we test to make sure that, 

1. The user is a valid user AND
2. We can `.authenticate(...)` the user by passing in `params[:password]`


If we're successfull, we create a session with the user's `id`. Otherwise, we redirect to `"/login"`. 


