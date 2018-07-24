---
layout: post
title:      "Adding jQuery to My Rails Travel App"
date:       2018-07-24 21:25:08 +0000
permalink:  adding_jquery_to_my_rails_travel_app
---


At first glance, the requirements for the Rails/jQuery project don’t seem too difficult. After all, we’re taking an app that’s already been built and then utilizing jQuery and JSON API’s to add dynamic features to it. However, re-building one’s front-end is no simple task, especially when you’ve faced a steep learning curve while transitioning from Ruby to JavaScript. Also, like me, you might think less planning is required if you’re not creating a brand new app from scratch, but as I soon learned, that is not the case at all!

I had been pretty satisfied with my Rails project, so it was disheartening to watch my app break as I attempted to add new functionality. I thought that adding a ‘Next’ feature would be a good place to start since it was covered in the curriculum, but the code we learned didn’t work for my app since I had gaps in my id numbers and couldn’t just add 1 to retrieve the next record. (More on that later.) This is how I felt for the first couple of days.

![](https://i.imgur.com/PohDwb0.gif)

One of the great things about the coding community is that if you’re experiencing an issue with your code, there’s a good chance someone else has encountered that same problem. It can take some practice to get your search terms just right, but when you do, Google can either lead you directly to the solution or at least provide enough additional info to help you figure out the solution on your own. Stack Overflow, in particular, has been a terrific resource for me, but a variety of blogs and other sites have been very helpful as well.

**RAILS/JQUERY TRAVEL APP**

Getting back to my project, here's a run-through of what I added to comply with the requirements.

**Must Render at Least 1 Index Page via jQuery & an Active Model Serialization JSON Backend**

On the User show page, clicking a button triggers an AJAX get request to the Trips index resource. A new object is created, which then invokes a prototype function that formats the JSON response into HTML, and finally, that formatted response is appended to the page.

```
$(".js-load-trips").one("click", function(event) {
    let currentUserId = $(this).data("user-id");
    $.get(`/users/${currentUserId}/trips.json`, function(data) {
      const currentUser = new User(data);
      let userIndexHtml = currentUser.formatUserIndex(currentUserId)
      $("#my-trips").append(userIndexHtml);
    })
      event.preventDefault()
  })
```

**Must Render at Least 1 Show Page via jQuery & an Active Model Serialization JSON Backend**

For both Cities and Trips, you can scroll through all instances via 'Next' and 'Previous' links. As I mentioned earlier, I struggled quite a bit with this since there are gaps in my id numbers due to deleted records during testing and the fact that Trips is a nested resource and a particular User's trips might skip several numbers depending on the order in which they were created. I don't know if this is the best or most elegant solution, but it works. Basically, this function uses the JSON response to create an array containing all the City id's. It then looks up the index of the current record, adds or subtracts 1 based on the value passed by the event handler, uses the updated index to retrieve the id of the next or previous City, and finally passes that id to the loadCity function, which can then make a get request for the show resource and use the response to update the page.

```
function getNewCityId(cityId, op) {
  $.get("/cities.json", function(data) {
    citiesArray = data
    cityIndex = citiesArray.map(c => c.id).indexOf(cityId)
    if (op === "add") {
      cityIndex += 1
    } else if (op === "sub") {
      cityIndex -= 1
    }
    newCityId = citiesArray[cityIndex]["id"]
    loadCity(newCityId)
  })
}
```

**Rails API Must Reveal at Least 1 Has-Many Relationship in JSON Rendered to Page **

I added this to both the City show page and Travelers (aka Users) index page. A City has many Trips and as you scroll through the Cities, you can click on a link that displays all the comments made about it through Trip submissions. A User has many Cities through Trips and on the Travelers page, clicking the link under a User's name will render all Cities they've visited, as well as their favorite attraction. All of this occurs without a page refresh.

![](https://i.imgur.com/uMyeHFv.png?2)

**Must Use Rails API & Form to Create Resource & Render Response without Page Refresh**

I integrated the new Trip form into the User show page. Clicking the submit button now prevents the default action and instead makes an AJAX POST request to instantiate a new Trip. An object model is created, which then calls on a prototype to format the JSON response. The returned HTML string is then appended to the Trips index on the page. Google helped me locate some code to reset my form and re-enable the auto-disabled submit button after submission.

**Must Translate JSON Responses into JS Model Objects that Must Have at Least 1 Method on the Prototype**

These are in place throughout my app for Users, Cities, and Trips. I mostly used prototype methods for formatting, but also created a couple to count how many Trips were created for each City and to calculate the average rating for each City based on the ratings assigned during Trip submissions.


**CLOSING THOUGHTS**

JS is really difficult and complex and quirky. On numerous occasions, I was elated that I'd gotten one thing to work, only to discover that I had accidentally broken something else in the process. For example, it took many attempts to create my new resource and correctly append it to the page. I want to bed feeling pleased with my progress and then this morning, I couldn't log into my app because I'd forgetten to indicate which form I wanted to hijack. I plan to run through my app a few more times to make sure there's nothing weird or unexpected going on. 

I still love the Ruby language, but I've also come to appreciate the ways that JS can make your apps more dynamic and contemporary. I have so much left to learn and I look forward to further exploring JS! For now, I'm just grateful to have an app that appears to be working. This project has been incredibly frustrating at times, but I enjoyed adding new features to the previous iteration of my app and I'm happy with how it's turned out so far! 

![](https://i.imgur.com/d96OMWl.gif)


[Feel free to check out my repo on Github ](https://github.com/micholi/rails-travel-app/tree/rails_jquery)




