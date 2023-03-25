---
layout: post
title:  "A picture sharing app"
date:   2023-03-24 03:00:00 -0500
categories: app rails devise postgres ruby
---

I have decided to create an awesome, simple rails app with postgres, css framework 
tailwindcss, and importmaps for the js imports. 

  - `ruby version 3.2.1`
  - `rails version 7.0.4`

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

---

### Server Update

I have completed cleaning the computer case and installing all the new hardware I have bargain shopped  
over the past few months. It is a micro atx size case with some damage to one of the two sata harddrive 
compartments. I decided to cut the metal and smooth out the remaining walls. Below this blurb, you can see 
spot #1 with a few dents. During the process of removing the old motherboard & cables, I figured out how to 
rewire the front panel at spot #2. Here are some other spots of interest:

![capybara-server1](/img/capybara-server1.jpg){: maxwidth="100%" style="padding: 20px 0 20px 0" }

  1. `_SATA Drives 2/2_`
  2. `_Front Panel (I/O Ports)_`
  3. `_MB LED light / indicator_`
  4. `_M.2 SSD 1/3_`
  5. `_SATA SSDs 3/6_`
  6. `_CMOS_`

After I installed the mb, power, processor & fans, graphics card, ram, HD, etc... I hooked up the power and connected 
a monitor. Spot #3 is the LED Tuf light that cycles the rainbow of colors. I've read that is normal behavior but need 
to double check.  When I turned on the computer, the fans powered on for about 1-2 seconds and the powered off.  Nothing 
else happened. I've double checked all my connections, integrity of the processor & it's sockett, different HDs, and with 
minimal connections and variables as possible. My next move is to check to see if the case is grounding the motherboard by 
running it live on a table.  More updates to come!

<!-- TODO fix blockquote, code, img syntax -->

---

![woodford2](/img/woodford2.jpg){: maxwidth="100%" style="padding: 20px 0 20px 0" }