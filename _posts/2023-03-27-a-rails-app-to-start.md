---
layout: post
title:  "A rails app to start"
date:   2023-03-27 04:00:00 -0500
categories: app rails devise postgres server
---

I have decided to start creating simple rails apps with tailwindcss and importmaps.
Noteworthy gems in my Gemfile:

  - `ruby "3.2.1"`
  - `gem "rails", "~> 7.0.4", ">= 7.0.4.3"`
  - `gem "devise"`
  - `gem "omniauth-google-oauth2"`
  - `gem "omniauth-rails_csrf_protection"`
  - `gem "pg", "~> 1.1"`


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
The devise docs are organized and easy to navigate. I've added omniauth with one provider which 
is google.

---

### Server Update

I started to work on my server again. Below I have uploaded images for reference. 
During the process of removing the old motherboard & cables, I figured out how to 
rewire the front panel at spot #2. Here are some other points of interest:

![capybara-server1](/img/capybara-server1.jpg){: maxwidth="100%" style="padding: 20px 0 20px 0" }

  1. `_SATA Drives 2/2_`
  2. `_Front Panel (I/O Ports)_`
  3. `_MB LED light / indicator_`
  4. `_M.2 SSD 1/3_`
  5. `_SATA SSDs 3/6_`
  6. `_CMOS_`

After I installed the mb, power, processor & fans, graphics card, ram, HD, etc... I hooked up the power and connected 
a monitor, mouse, & keyboard. Spot #3 is the LED Tuf light that cycles through a rainbow of colors. I've read this is normal 
behavior. When I turned on the computer, the fans powered on for about 1-2 seconds and the powered off. Nothing else happened. 
I've double checked all my connections, the processor & it's sockett, and different HDs and ram combinations. I also powered 
the computer with the bare minimum to start outside the case to rule out the case grounding the board. There are only  
a few more options to try in order to narrow down what is at fault. More updates to come!

---

![woodford2](/img/woodford2.jpg){: maxwidth="100%" style="padding: 20px 0 20px 0" }
