---
layout: post
title:      "CLI Data Gem Project - Museum Finder"
date:       2018-04-19 15:01:16 +0000
permalink:  cli_data_gem_project_-_museum_finder
---


I’m currently putting the finishing touches on my CLI Data Gem Project and it’s been an interesting experience so far. While there’s definitely a learning curve when building something from scratch for the first time, if you’ve gotten through the Music Library CLI and Tic-Tac-Toe with AI labs, you’re more than prepared to face this challenge!

It took me a little while to settle on an idea. I initially considered doing something food-related, but ultimately decided to go with a Museum Finder focused on the Smithsonian because my mom recently visited me in DC and we toured some of their museums while she was in town. The Smithsonian website includes a landing page where you can browse all museums, then click on any individual museum to pull up a dedicated page with additional details. My goal was to mimic that experience, except in CLI format.

**Getting Started**

While I was waiting for the green light to proceed, I watched Avi’s video. I later found myself returning to it several times to replay things that still weren’t clear. I highly recommend checking it out before you get started because it’s really helpful in getting a basic file structure set up as well as thinking through a high-level project plan. I followed his advice and used 'bundle museum_finder' to stub out a directory. I also ran chmod +x museum-finder to make my file executable, but I couldn't get it to work. After a few tries and a couple of days, I finally realized I’d placed `#!user/bin/env ruby` at the top of my file instead of the correct `#!/usr/bin/env ruby`. I consider myself to be pretty detail-oriented, so it’s pretty frustrating when something fails because I left out a character.

A good part of day 1 was focused on getting all my files in place, writing some placeholder code, and setting up dependencies. One early issue I encountered is that I created museum.rb and scraper.rb files, but then neglected to require them in my museum_finder.rb file. The other thing consuming much of my time that day was Github. I was a little confused by those lessons the first time around, mainly because I have a hard time absorbing information if I don’t have an immediate use for it. So, I reviewed that module again to make sure I understood how to add, commit, and push changes. Getting comfortable with Github takes some time, especially when you’re used to just saving your work and typing ‘learn submit’ when you’re done. I’m not quite there yet, but it’s less of a mystery now than it was just a few days ago.

Scraping was also a bit of a challenge for me because it’s not my strongest area. Fortunately, the Smithsonian website is manageable and all the individual museum pages have an identical structure, which made things a bit easier. There was still a lot of trial and error and experimenting with Pry, but it wasn’t nearly as difficult as I had anticipated. 

**Museum Finder**

As for my actual project, here’s how I have it structured.

* My executable file does only 1 thing, which is to call my CLI
* I have a scraper file that gets the museum’s landing page and identifies the div class containing the info I need
* My museum file includes an initialize method and a class method that creates museums with the scraped name, location, and url
* It also includes instance methods that scrape additional details such as description and hours from the individual museum pages
* Back to my CLI, the call method invokes the MuseumFinder::Museum.create_museums method to get everything started and then displays a greeting
* The CLI is also where I’ve built out all the logic behind displaying the main menu, asking for and processing user input, and printing information for each museum the user has selected

![](https://imgur.com/GDkmDd2)

![](https://imgur.com/LIJoo4N)

Overall, this has been a fun project. I went from feeling a bit overwhelmed to frustrated to satisfied with the progress I was making. I look forward to making some final tweaks and seeing what comes next.
