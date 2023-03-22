---
layout: post
title:  "A picture sharing app"
date:   2023-03-27 03:00:00 -0500
categories: app rails devise postgres ruby
---

I have decided to create an awesome, simple rails app with postgres, css framework 
tailwindcss, and importmaps for the js imports. 
```
  ruby version 3.2.1
  rails version 7.0.4
```
I'm hoping to have this done by the end of next week since we will be on vacation 
trying to use it .. 😎.

---

Right now, I'm in the middle of setting up [devise](https://github.com/heartcombo/devise). 
Devise requests application config edits during installation:
  - required change in `config/environments/development.rb`
    - `config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }`
  - no-api-required change in `config/routes.rb`
    - `root "dens#index"`
  - no-api-required change in `app/views/layouts/application.html.erb`
    - `<p class="notice"><%= flash[:notice] %>`
    - `<p class="error"><%= flash[:error] %></p>`
The devise docs are organized and easy to navigate. I will be adding the 
omniauth settings once I design the model layer.

---

I was having an issue with setting up psql due to databases, users having 
capital letters from the name of my application 😒. My favorite commands so far: 
  - `DROP ROLE ...`
  - `DROP DATABASE ...`
In the future, my plan is to create a postgresql container and an app container. 
Scripts need to be written in these Dockerfiles depending on how deployment to 
my **in-progress** server project.  

---

![woodford2](/img/woodford2.jpg){: height="400px" width="300px" style="padding: 20px 0 20px 0" }
