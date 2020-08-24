---
layout: post
title:      "Ruby, Rails, Recipes"
date:       2020-08-24 17:11:04 +0000
permalink:  ruby_rails_recipes
---


Sinatra truly set us up so well for this Ruby on Rails project that it felt as if I still had my bearings! If anything, a lot of the time-consuming hard coding of Sinatra was simplified with the beauty of Rails. Gems like Devise and Omniauth, migrations, Active Record, and partials all seemed there to help you get to where you wanted to be, but faster. 

For my third project with the Flatiron School, I decided to create a fairly simple app in which a user can create or log into an existing account (with third-party auth) and create cookbooks and the recipes inside of them. 

# Devise 
Setting up Devise was my first true hurdle for this project. Devise is an awesome gem that takes care of user authentication and sessions. The only snag I came accross with this was that Devise does not set up a user's name (or username) automattically! Over time, that became a bit annoying because I wanted my user's name displayed on most of my view pages. Luckily enough, all I needed to run was a simple line of code and the problem was fixed.

```
rails g migration AddNameToUsers
```

Through this one line, Rails created a new migration `AddNameToUsers`. This allowed me to add a `:name` property to the `users` table that was originally made by Devise. 

# Omniauth
Because one of Devise's 10 major funtions is "Omniauthable", I was able to use the `omniauth` gem to allow for third-party sign up/ log in for my application. 

[Omniauth](https://github.com/omniauth/omniauth) was refreshingly simple as well. Because devise sets up the User model so well already with this:

If we take a look at `app/models/user.rb`: 

```
  class User
    devise :database_authenticatable, :registerable,
           :recoverable, :rememberable, :validatable
	end
```

In order to make our User model "omniauthable", we add this line:

```
devise :omniauthable, :omniauth_providers => [:facebook]
```

Next, you head over to your `Gemfile` to add the necessary dependencies. I chose to use Facebook's strategy for third-party auth in my app, and there's even a specific Omniauth gem for it! But as a precaution, I used that *and* the regular *omniauth* gem in case any core functionality was missing: 

```
  # Gemfile
	...
	
	  gem "omniauth"
		gem "omniauth-facebook"
	...
```

After that, run `bundle install` so you're good to go.

Then, back in the User model, you write a method, the only actually needed in that model:

In order for third-party authentication to be successful, I defined a special `.from_omniauth(auth)` method that mass-assigns the necessary user information for login (email, name, etc):

```
  def self.from_omniauth(auth)
    where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
      user.name = auth.info.name
      user.email = auth.info.email
      user.password = Devise.friendly_token[0,20]
    end
  end
```

Next, in our routes, we have configure a custom controller with the route `devise_for :users`. I chose to call mine "callbacks" but you can call it whatever you want:

```
devise_for :users, controllers: { :omniauth_callbacks => "callbacks"}
```

Finally, we have to actually create our `CallbacksController` class: 

```
# app/controllers/callbacks_controller.rb

class CallbacksController
    def facebook
    @user = User.from_omniauth(request.env["omniauth.auth"])
    if @user.persisted?
      sign_in_and_redirect @user
      #set_flash_message(:notice, :success, :kind => "Facebook") if is_navigational_format?
    else
      session["devise.facebook_data"] = request.env["omniauth.auth"]
      redirect_to new_user_registration_url
    end
  end

  def failure
    redirect_to new_user_registration_url
  end
end
```


# Conclusion
After I was finished setting up Devise and Omniauth for my application, the rest of my experience wasn't as anxiety-ridden. Similarly to how I built my Sinatra application, I set up the routes and controllers much the same way in Rails. The only difference was that Rails really does try to steer you in the right direction. It really does live up to its mantra, "convention over configuration". 
