---
layout: post
title:      "Ruby Classes and Instances"
date:       2018-04-25 02:53:31 +0000
permalink:  ruby_classes_and_instances
---


Ruby is an Object Oriented Programming (OOP) language. A lot can be said about OOP and people have written entire books about it. For now, I'll simply note that at a high level, it involves organizing around objects that can be designed and manipulated.

In Object Oriented Ruby, a class is essentially a blueprint or framework that defines how to build an object. This includes such things as what its characteristics are and what behaviors it can perform. A basic class definition looks like this:

```
class Cat

# code goes here

end
```
You'll notice a few things:

* The name of the class (Cat in this case) is always capitalized because it's stored in Ruby constants
* Every class must end with the end keyword
* In between the class name and end is where you'll code characteristics, behaviors, etc.

**Creating Objects in a Class**

We use a special Ruby method called initialize to create new objects in a given class. The initialize method can take in one or more parameters and allows us to set instance variables (more on that in a bit) at the time we instantiate or create a new object. Consider the following example in which we define a class called Senator as well as specify the arguments required by our initialize method.

![](https://i.imgur.com/kajvv2U.png)

Let's also take a look at this irb session to see what happens when we set up our class and then instantiate a new object in our Senator class.

![](https://i.imgur.com/I2713Fn.png)

**Senator vs. senator**

It's important to differentiate between Senator and senator. Uppercase Senator refers to the class that we previously defined, whereas lowercase senator refers to a particular instance or occurrence within the Senator class. The Senator class defines the blueprint for all objects in the class; a senator instance is an individual senator, e.g. Chuck Schumer or Kamala Harris. As we saw in the irb example above, every time we instantiate a new senator, we require name, state, and party parameters, which we then store as instance variables. Unlike local variables that can't be accessed outside of the method in which they're defined, instance variables are visible and accessible anywhere within the object's scope. Instance variables are always preceded by the @ sign, e.g. @name.

In addition to instantiating new senators, we can also define behaviors for our senators via instance methods. Let's review some instance methods that we've added to our code:

![](https://i.imgur.com/QYaxYjg.png)

Once we create new instances of senators, we can then invoke our instance methods to enact these new behaviors that are now part of the Senator class.

```
gillibrand = Senator.new("Kirsten Gillibrand", "NY", "Democratic")
=> #<Senator:0x000000020f0170 @name="Kirsten Gillibrand", @state="NY", @party="Democratic">

booker = Senator.new("Cory Booker", "NJ", "Democratic")
 => #<Senator:0x000000020d3d40 @name="Cory Booker", @state="NJ", @party="Democratic">
 
 mccain = Senator.new("John McCain", "AZ", "Republican")
 => #<Senator:0x000000020b7348 @name="John McCain", @state="AZ", @party="Republican">
 
 gillibrand.run_campaign_ad
 I'm Kirsten Gillibrand and I approve this message!
 
 booker.filibuster
 I can stand here and talk all night long!
 
 mccain.vote_on_bill("nay")
 John McCain: NAY!

```
Within a class, we can also define class methods. We denote a class method by placing the word self before it. For example, the method self.vote_them_out clears out all the senators saved in the @@all array so that we can get ready to replace them with brand new senators. Since only 1/3 of the US Senate is up for reelection every 2 years, this is obviously hypothetical.

![](https://i.imgur.com/gDoxc4T.png)

**Note on Class Methods vs. Instance Methods**

When defining a method, we should think about whose responsibility it is to perform that behavior or action. In our self.vote_them_out method, an individual senator wouldn't or shouldn't be responsible for things that impact the class as a whole. We use a class variable @@all to store all the senators, so it makes sense that if we want to empty the array being stored in @@all, our class should be responsible for that as well. Likewise, while voting is a behavior available to the entire class, each senator must cast a vote individually. The same is true of filibustering and running a campaign ad. These actions are carried out by individual senators, therefore we would set these up as instance methods.





