---
layout: post
title:      "Enumerables, Return Values, & Learning to Slow Down"
date:       2018-04-10 16:39:09 +0000
permalink:  enumerables_return_values_and_learning_to_slow_down
---


I’m about a month into my coding journey at Flatiron School and quickly approaching the end of the Ruby module and the start of my first project. During the past four weeks or so, I’ve experienced some highs and lows. There were moments in which I felt a great sense of accomplishment, but in between, I also felt confused and frustrated at times. As the labs grew more complicated, my sense of frustration grew as well. 

After a bit of reflection, I realized I was trying to get through the material at a fast pace so that I could finish the program and start the next phase of my career, even if I didn’t fully grasp what was being taught in each lesson. This is a bad idea. If you don’t completely understand something, don’t assume it’s just going to magically click one day. Instead, it’s more likely that you’ll struggle with more complex subject matter because you didn’t fully comprehend what preceded it.

In my case, I had a tough time with enumerables and iterators. At a high level, I understood the concept of iteration and how it could be useful when writing code. I didn’t totally get the specifics of the various methods available or the situations in which each one should be used, but I figured it would all make sense once I got to practice during labs. I was wrong. When I got to a series of labs focused on iteration,  I found myself randomly trying every enumerator method I was aware of until I stumbled up on one that got my tests to pass.

**Cartoon Collections Lab**

Take, for instance, the Cartoon Collections lab. Looking back, this shouldn’t have been too difficult to solve. There were 3 objectives: get familiar iterating through arrays using enumerator methods, build methods and control their return values, and practice control flow with if and else statements. But if you don’t fully understand iterators and their return values, it can easily become an exercise in futility. I built the first 2 methods without much trouble, but then had a tough time with the last 2.

METHOD 3 - LONG_PLANETEER_CALLS: This method should accept an array of calls and tell us if any of the calls are longer than four characters. The instructions clearly note that the return method will be either true or false. However, due to my lack of understanding of return values, I basically cycled through all the methods I could think of, hoping one would work. This was one of my final attempts, which was clearly wrong.

```
def long_planeteer_calls(calls)
  calls.detect { |call| call.length > 4 } 
end
```

My error message was "expected: true, got: earth". Fortunately, I did understand what this particular error message was conveying (unlike some of my previous attempts), so I made the following modification. It got the tests to pass, though is *not* the best solution (more on that later).

```
def long_planeteer_calls(calls)
  calls.detect { |call| call.length > 4 } ? true : false
end
```

METHOD 4 - FIND_THE_CHEESE: This method should accept an array of strings and look through them to find and return the first string that is a type of cheese. The instructions indicate that you’re being asked to return a string value. Because I was still confused (and also because I wasn’t paying attention to the lab instructions or the tests), I incorrectly added true/false logic to this method and course, got an error.

```
def find_the_cheese(foods)
  cheese_types = ["cheddar", "gouda", "camembert"]
  foods.detect { |food| cheese_types.include? food } ? true : false
end
```

I knew what I’d done wrong and fixed it. All errors were resolved and the lab was complete, but I realized that I didn’t have a firm grasp of this topic, so I went back to re-read some lessons and did some additional external research. I’m far from an expert on this subject, and it's a lot to keep track of, but it's starting to sink in. Here are some of the basics I now try to keep in mind.

**A Quick Guide to Enumerables**

*Enumerable* is a Ruby module offering a series of methods that can be used to search, sort, and manipulate collections. You may find yourself working with arrays and hashes containing large amounts of data that need to be examined, compared, or changed. Rather than building this logic from scratch, you can incorporate existing enumerable methods into your code, greatly simplifying and streamlining it.  Knowing which method to employ requires some understanding of what it does and how it works. Also, note that every method in Ruby returns a value, so you need to be aware of what each method returns if you want your code to work as desired.

**Common Iterators**: Some common Enumerable methods are #each and #map (or the identical #collect). These are similar in that they will iterate over all elements in an array, but their return values differ. Whereas #each simply returns the original array, #map returns a new array with manipulated data. Therefore, while #each is useful in iterating over or processing an array, #map can be used to do something with an array that’s been processed.

**Search Enumerators**: Methods that are useful in searching an array are #select and #find (#detect is synonymous with #find). These are similar, but differ in an important way. Both #find and #detect will return the first item in a collection for which the block evaluates as true. Once that condition is met, there is no further iteration. If nothing is found, the methods return nil. Meanwhile, #select will iterate over an entire array until it reaches the end and return ALL items in the array which evaluate as true. It’s important to note here that although these methods are evaluating whether a condition is true, the return value itself will never be true.  Instead, when the true condition is met, the return value will be the matching element(s).

**Boolean Enumerators**: Boolean can seem like a strange concept at first. It’s a binary variable with two possible values: true or false. In Ruby, boolean enumerators can be useful if you need to return a value of true or false. Some of these methods are #all? (iterates over a collection, passes each element to the block, and returns true if the block never returns false or nil), #any? (passes each element to the block and returns true if at least one member of the collection returns true), and #none? (passes each element to the block and returns true if the block never returns true for any of the items). The #include? method is somewhat similar to #any?, but doesn’t involve passing elements to a block for evaluation. Rather, it’s useful if you have a known value, e.g. “a” and want to determine whether an array includes that same value.

Circling back to the Cartoon Collections Lab, it’s now obvious to me that I was still having a hard time with the basics of enumerators. When the lab instructions told me that I needed to return a value of true or false, I should have focused on booleans instead of search enumerators.

**Some Parting Lessons**

* If you’re confused, don’t try to power through by yourself. Ask questions! I can be very stubborn when it comes to seeking help, but there are resources available including study groups, the ability to ask a question and pair with a technical coach, and connecting with fellow students on Slack.
* Revisit lessons you’ve already completed and read other material until you’re clear. You're not going to win any awards for rushing through the curriculum. In fact, you'll only make things harder for yourself in the long run.
* Read labs carefully and make sure you understand what’s being asked of you. This should be obvious, but I didn't always do it.
* Learn to use pry. It took me a little while to understand pry, but once you get the hang of it, it can be useful in determining what your code is returning. This will be especially helpful as you get further along and have to rely almost entirely on test driven development.



