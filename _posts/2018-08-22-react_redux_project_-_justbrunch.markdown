---
layout: post
title:      "React Redux Project - justBrunch"
date:       2018-08-22 16:53:13 +0000
permalink:  react_redux_project_-_justbrunch
---


Well, the day has finally arrived. I started this program five and a half months ago and now here I am at the final React/Redux project! I was nervous heading into it because, to be quite honest, I found this section to be really confusing. React allows you to do some really cool things and it makes sense to me at a high level, but when it comes to actual implementation, I just don’t find it to be very intuitive. I struggled to understand what was being passed and how all the pieces fit together. Based on my incessant Googling, I’m guessing I’m not alone in feeling that way! Nevertheless, I persisted, and I’ve built a functioning app that (mostly) does what I wanted it to do.

The requirements for this project are fairly open-ended. You have to create a single-page application (SPA) in React, use Redux middleware to manage state, and build a Rails API back-end to handle data persistence. But aside from that, the content can be anything you want it to be. I was interested in doing something food-related, but didn’t want to focus on recipes even though I really enjoy cooking. I decided to go with a Yelp-like app containing restaurant recommendations and to give it a little twist, the reviews are specifically for brunch spots. It’s called justBrunch. Why did I choose this idea? I always seem to be the one tasked with researching restaurants and making reservations and also, I really love brunch and think breakfast food is suitable for any meal during the day.

![](https://i.imgur.com/A9vcCgc.jpg?1)

This project required us to make use of ‘react-router’ and proper RESTful routing. I implemented the following:

* ‘/‘ - Welcome page
* ‘/new’ - Create new restaurant
* ‘/restaurants’ - See all brunch restaurants. From here, you can navigate to individual listings for brunch spots, e.g. /restaurants/1. Comments components are integrated into the restaurant show page, so you can view associated comments and submit a comment of your own from within the restaurant listing
* ‘/recipes’ - Static ‘Coming Soon’ page to share brunch recipes and hosting tips. Not functional, but includes a single pancake recipe!

It’s essentially a CRD app - CRUD minus the U part. In addition to creating, reading, and deleting brunch spots, you can also like or “yum” any establishment. On the index page, restaurants are sorted alphabetically by default prior to rendering. Those results can then be filtered if you prefer to view brunch places by price range: inexpensive, moderate, or pricey.

![](https://i.imgur.com/WfnD2zP.png?1)

Along the way, I encountered numerous challenges. After setting up my Rails back-end, I spent about a day and half trying to figure out why nothing was working. I was able to view pure json on my 3001 Rails API server, but couldn’t load anything on the React side. I had followed the instructions I’d read on several blogs and added both `gem 'foreman', '~> 0.82.0'` and a Procfile with the following, but still couldn’t successfully retrieve or render data.

```
web: cd client && npm start
api: bundle exec rails s -p 3001

```

Finally, after researching my error messages, I realized I was experiencing Cross-Origin Resource Sharing (CORS) issues, which can occur when calling an API from the front-end app. To resolve this issue, I installed `gem 'rack-cors' ` and then added the following to config/application.rb:

```
config.middleware.insert_before 0, Rack::Cors do
      allow do
        origins '*'
        resource(
          '*',
          headers: :any,
          methods: [:get, :post, :patch, :put, :delete, :options]
        )
      end
    end
		
```

Another big issue I encountered was related to how I’d set up my restaurantsReducer. I kept getting “is not a function” error messages and couldn’t figure out why because my code looked correct. It turns out, if your code is something like `export default (state={restaurants:[]}, action)`, then you have to write `restaurants.restaurants.map` to iterate over the data. Or just stick with `state=[]` and then `restaurants.map will work`. The React Developer Tools helped me debug this one. Over on the right side under Props, you can see what's being returned.

![](https://i.imgur.com/cXuadrZ.png?1)

Although this project was frustrating at times, I’m pretty happy with what I’ve built. I know I need much more practice with React and Redux, but I have a better understanding of it today than before I started my project, so that’s a good sign. Being a student again has been a great experience, but I’m super excited to focus on my career and put my new skills to use. I'm very much looking forward to this next chapter and can’t wait to see what’s next for me!
