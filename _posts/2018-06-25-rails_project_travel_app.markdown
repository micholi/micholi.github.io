---
layout: post
title:      "Rails Project: Travel App"
date:       2018-06-25 22:50:04 +0000
permalink:  rails_project_travel_app
---


I'm close to submitting my Rails project, provided I don't run into any unforeseen issues during my next round of testing. This has been a challenging process for me and I encountered multiple roadblocks to get to this point. I had previously struggled a bit with Sinatra and then once I finally felt comfortable with it, I had to re-learn routes the Rails way. I initially had mixed feelings about Rails and found it confusing, but I now have a greater appreciation for it. It's extremely powerful and I'm sure I'm just scratching the surface of its capabilities.

For my project, I chose to build a travel app that enables users, aka travelers, to add and rate trips. I had considered a travel app for Sinatra before nixing the idea and then decided to revive it for Rails. My app has 4 models: User, City, Country, Trip.

* A user has_many trips and has_many cities through trips
* A city belongs_to a country, has_many trips, and has_many users through trips
* A country has_many cities
* A trip, which is my join table, belongs_to a user and belongs_to a city

My trip form allows a user to either choose an existing city, or add a new one, and then if they choose the latter, they need to choose an existing country, or a add a new one. The city and rating fields are required, while Must See Attraction and Comments are optional. I added some validations, along with a few custom error messages because the default messages were oddly worded and confusing.

```
  validates :city, presence: true
  validates_uniqueness_of :city_id, :scope => :user_id, message: "already added to your trips!"
  validates :rating, presence: true
  validates_numericality_of :rating, :only_integer => true, message: "must be a whole number"
  validates_inclusion_of :rating, :in => 1..5, message: "must be between 1 and 5"

```

At first, my app was set up to only allow cities to be created via the new trip form, but I later added an additional form for creating cities separate from the trip submission. I then decided to give users the option to link directly from the city show page to the trip form, which was more difficult than I expected. The link itself was simple. The hard part was that I didn't think the user should have to choose the city if they were linking from a city show page and so I had to figure out how to carry the city.id through to my trips controller. A lot of googling occurred and I tried a bunch of suggestions before finally finding one that actually worked:

```
<% if !Trip.exists?(user_id: current_user.id, city_id: @city.id) %>
    <%= link_to "Been to #{@city.name}? Add it to your trips!", new_user_trip_path(:user_id, :city_id => @city.id) %>
  <% end %>

```

Basically, this first checks whether the user has already added this city to their trips. If they have not, they'll be shown a link that will take them to the trip form, while passing through the city_id and city.id. I then added the following to the new and create actions in my trips controller:

```
@city = City.find_by(id: params[:city_id])

```

Lastly, I added an if statement to my new trip form in order to modify the view in cases where @city has been passed. Instead of displaying all the city/country fields, it shows the name of the city that's been carried over and then sends the city_id as a hidden value. I'm not certain whether this is the best solution for what I was trying to implement, but after playing with multiple variations, this was the only one that worked for me.

```
<% if @city %>
        <%= f.hidden_field :city_id, value: @city.id %>
        <%= f.label :city %>
        <%= f.text_field :city, value: @city.name %>

```

Finally, I added some scope methods, per the project requirements. Here's one that identifies all trip reviews with a 5-star rating. On the main user show page, you can see the total number of trips as well as the last one added.

![](https://i.imgur.com/TTQax3L.png?2)

When you click on the link, you can view all the cities given a rating of 5.

![](https://i.imgur.com/sMXQVa2.png)

This was the most challenging project for me so far, and it took me long than the others,  but I really learned a great deal. I've learned to love Rails, though I must admit I'm really looking forward to checking out JavaScript next!
