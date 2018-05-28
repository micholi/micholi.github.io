---
layout: post
title:      "Sinatra Project: TV Watchlist"
date:       2018-05-28 22:46:03 +0000
permalink:  sinatra_project_tv_watchlist
---


As Memorial Day weekend comes to a close, I'm trying to wrap up my Sinatra project. I had approached this project with mixed emotions. One the one hand, I was excited to practice my new skills from this section of the curriculum and build an actual website with database persistence from scratch, but I was also fighting off a bout of impostor syndrome. I remember having similar feelings while working on my CLI project and hoped they would eventually dissipate.

After considering and rejecting several ideas, I ultimately decided on a TV Watchlist because I like TV and used to work for a digital streaming service. To get started, I built out my own file structure. I referred to the Corneal gem and previous labs to guide me through my setup, but I thought it would be worthwhile to go through the process of creating my own directories and files.

![](https://i.imgur.com/npdXHTw.png)

The first day and a half went pretty smoothly. I spent time thinking through what databases I'd need and what fields they should include as well as which models I'd have to build and how they'd relate to each other. I also created some placeholder erb files so that I could test the RESTful routes I was adding to my controllers just to make sure everything was linking as intended.

Despite my planning, I spent a good part of day 3 working through one roadblock after another. There were several issues, but the biggest one was related to some functionality I planned to include. In addition to the basic Create, Read, Udate, Delete requirements specified in the project, I wanted to enable the following: allow the user to add another user's show to their watchlist and then later remove that show from their watchlist without permanently deleting it. This added an extra layer of complexity and I needed to re-work a few things before I could continue.

**Database Changes**

I added 2 new database migrations. My shows table already had a user_id foreign key, but I renamed it owner_id to distnguish the owner/creator of a show from other users/viewers who simply want to add it to their watchlist.

```
class RenameColumnInShows < ActiveRecord::Migration
  def change
    rename_column :shows, :user_id, :owner_id
  end
end
```

I also added a join table because of the many-to-many relationship that exists between users and shows. A user can have many shows and a show can have many users.

```
class UserShows < ActiveRecord::Migration
  def change
    create_table :user_shows do |t|
      t.integer :user_id
      t.integer :show_id
    end
  end
end
```

**Model Updates**

Lastly, I added a new UserShow model and modified both my User and Show models. Here's my updated Show model.

```
class Show < ActiveRecord::Base
  has_many :user_shows
  has_many :users, through: :user_shows
  belongs_to :network
  belongs_to :owner, class_name: "User", foreign_key: "owner_id"
end
```

With these changes, I could now display a watchlist that included all of the user's shows, both the ones they created and the ones they added from other users. But I could also differentiate between owners and users and adjust their views and permissions accordingly.

For example, both of these shows are in Offred's watchlist, but the show detail views differ because only one show is owned by her, whereas the other show was created by another user and simply added to her watchlist. I've also ensured that no one can circumvent that and manually alter a show by adding 'edit' or 'delete' to the URL as those actions will return error messages.

![](https://i.imgur.com/6ys73ai.png?1)

![](https://i.imgur.com/nLii1NI.png?1)

Well, that's my project! I need to go through another round of testing to make sure I haven't overlooked anything and then I'll record my video walkthrough. Overall, I've had a lot of fun working on this and learned a ton. Looking forward to finishing up and moving on to Rails in the very near future.

