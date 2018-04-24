---
layout: post
title:      "What is Self?"
date:       2018-04-24 22:49:51 +0000
permalink:  what_is_self
---


Self is a concept that I've struggled to fully comprehend. Not in the psychological or philosophical sense, but rather in the world of Ruby. I've encountered and used it quite a bit while working my way through Object Oriented Programming, but I've had a hard time articulating what it is.

Self is considered a keyword (or reserved word) in Ruby, meaning it's reserved to perform a certain job within our code and should not be used outside of its intended purpose. The simplest way to define the self keyword is that it refers to the object itself. It's been said that *almost* everything in Ruby is an object, though I've also read that this statement is *almost* (but not quite) true. To the extent that it is true, the exact definition of self and the object to which it is referring will depend on the context in which it's used. 

Another way to think about self is that it provides access to the current object, which is receiving the current message. In Ruby, every method has both a sender and a receiver. Let's consider the case of object.method, where method has been defined in our program. Within that method, object can receive a message sent by the method and if we think of self as that object, then self can receive that message as well.

**Examples of Self**

Let's start with a simple example. Here, we've defined a show_self method in our Restaurant class.

```
class Restaurant
  def show_self
    self
  end	 
end
```
We can then use the following to create a new restaurant and invoke the show_self method.

```
r = Restaurant.new
r.show_self
```
This will return self, which in this case is the restaurant instance that we've created and then called on.
```
#<Restaurant:0x00000001b8ad20>
```

In the below example, we're using self within an **Instance Method**.  Here, we're using the shovel operator to add self to the @@all variable we defined earlier in the program.  In this context, self refers to a new restaurant instance that we're instantiating via the initialize method. By adding self to @@all, we're insuring that each new instance we create is added to the array that's storing all individual restaurant instances.

![](https://i.imgur.com/0Go9nCN.png)

Another use of self can be seen in the following open_restaurant method. In this example, we're getting the @name instance variable of self, which refers to a restaurant instance.

![](https://i.imgur.com/7aLm6LS.png)

Now, we can do something like this:
nobu = Restaurant.new("Nobu"), followed by nobu.open_restaurant, which outputs "Nobu is open for business. Welcome!".

Keyword self may also be used to indicate that a method is a **Class Method**, one that refers to the entire class and not just individual instances of that class. Perhaps our Restaurant class represents all new restaurants opening in a given month. On the first of each month, the previous month's restaurants are replaced by new ones. Since the entire Restaurant class is impacted and not just particular restaurants, we may want a way to delete all restaurants at once rather than one by one. We can accomplish this by adding a new class method called self.empty_all to our previous code. Now, when we invoke this method, we can clear all saved restaurants in our class so we can start over.

![](https://i.imgur.com/r1vodns.png)

Self is a complex subject, especially for someone who's new to programming. However, I'm sure that with continued exposure and practice, it'll become less and less enigmatic. I look forward to learning even more about it as I continue on my coding journey and expand my knowledge of Ruby.


