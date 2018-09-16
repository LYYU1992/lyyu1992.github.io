---
layout: post
title: Function Decorator
description: "test posting"
tags: [sample post]
author: Linyang Yu
image:
  background: triangular.png
---

# A special gift: decorating your function by wrapping it up!
## —brief introduction about function decorating in python

People always have this confusion, if I already get the perfect gift, why do I still need to wrap it up and decorate it? Decorating a gift is not just cover it with colourful wrapping papers. It is like the icing on the cake, final touch on the paint and wedding dress for the bride. It is protecting the current beauty, and at the same time adding another dimension to make your gift even prettier.

In Python, if we consider **function** as a “gift”. It will follow the same rules. Decorating your function with “wrapping papers” (often called *decorator* in Python)  will add another dimension to the performance of the original function.

In this post, I will give a brief introduction about the “function” object in python, the reason why we have to decorate it, and dive into how to decorate your Python functions. 

### What is Function?

In the world of Python, everything is considered to be an **object**. Just like human, an object has its unique name, job title (*type*) and soul (*values*). There are a variety of objects as building blocks in Python, such as integer, float, list, string, dictionary and Function. Among all the objects in Python, “functions” are definitely to be the top-class celebrities (*first-class objects*). 

**Function**, in beginners’ opinions, is considered as a machine to convert the inputs arguments to an output. However, in Python, functions can be passed around, modified and used as arguments and even output as well. 

We can define a **function**, and pass the function to a new **variable**:

```Python
def function_1():
    p = 1 + 1
    return p
q = function_1()
```

We can use the **function** as an input **argument** to another function:

```Python
def function_2(function_1):
    q = function_1()
    return q
```


Or we can also define a function and its **output** is actually a **function** as well:

```Python
def function_3():
    function = function_1()
    return function
```

From all the samples above, we now have a better understanding about function in Python and how we can “play around” with it. Now, we can move into the next topic: why do we need to decorate the function?


### Why we need to decorate the function?

In python, decorating a function is just like wrapping the gift. Even you already wrote a great code, there will always be a greater one. For example, you wrote a 1000-line program and then you want add a time-control function to one of your loops within this 1000-line. What should you do? Go back line by line and find the loop, change it and spend the whole weekend debugging the code that might be influenced by the change? For a program with high complexity, this action mostly ends up with screwing your “great Python program”, or, sometimes, even your computer. 

Luckily there is an alternate solution for this issue: **decorating your function**. You don’t have to make any change on your original function, which is considered to be the "*gift-function*”. Instead of modifying the “*gift*”, we can define other functions as “*wrapping papers*” to decorate the “*gift*”. In this case, the **original function** is protected, and multiple layers of **decorating function** is added (*wrapped*) in an elegant way as “wrapping papers”. We can modify the final version of the wrapped-gift-function by adding or removing different decorating functions to achieve different goals.

Another thing we should be excited about function decorating is the original “gift-function” and the “wrapping-paper-functions” are all individual. You can wrap the “gift” using different combinations of “wrapping-papers”, or you can use the “wrapping papers” on other “gifts” as well. Pretty realistic!

### How to decorate a function?

If we consider the function is a gift, how could we design the wrapping paper and wrap it?
My friend is big fan of the Pokemon Go game from Nintendo, so I designed this simple program named “Pikachu Fight”. 

First, we need to import the `random package`, which will help you to generate random variables:

```Python
import random
```
We define the function as `Pikachu_Fight()`, and set the movements of Pikachu as a list, which contains three common skills of Pikachu: Static, Lightning rod, and Defence. 

```Python
def Pikachu_Fight():
    movements = ["Static", "Lightning_Rod", "Defence"]
```

After that we can define a `while true` condition, to generate infinite random yield:

```Python
while True: 
        random_movement = random.choices(list(movements))
        yield random_movement
```

Then we can start a Pikachu fight by using this function:

```Python
time_play = input("How many times you want to play?")
for _ in range(int(time_play)):
         print("Pikachu moved! Pikachu used", next(Pikachu_Fight()))
```

If the input number is 10, the program immediately return us with 10 generated answers:


<img src= "https://github.ubc.ca/MDS-2018-19/DSCI_542_lab2_lyyu/blob/master/img/Pikachu_F_returns_nonD.png?raw=true" width="500">

It is definitely dull with all the answer generated at the same time. However, to make the function more interesting, we can add sleep time between each function call. That means we need to decorate the function by introducing a time control *decorator* as the “wrapping paper”.

We need first to name decorator, then define a wrap function as a inner function:


```Python
def movement_timer_decorator(function):
    def wrapper_func():
```
    
Use `random.randint` to generate a random int from 1 to 3, this int will be the cooldown time between each movement, and use the `time.sleep` to set the sleep time from each function call.

```Python
def movement_timer_decorator(function):
    def wrapper_func():
        skill_cooldown_time = random.randint(1,3)
        print("Pikachu will make a movement in ", skill_cooldown_time, "seconds")
        time.sleep(skill_cooldown_time)
        return function()
    return wrapper_func
```


Now we have the "gift" as function `Pikachu_Fight`, and the "Wrapping paper" as a decorator `movement_timer_decorator`, we can decorate our gift right now with one simple `@` code: 

<img src= "https://github.ubc.ca/MDS-2018-19/DSCI_542_lab2_lyyu/blob/master/img/function_dec.png?raw=true" width = "500">

If we run the same function to call the decorated `Pikachu_Fight`:

```Python
time_play = input("How many times you want to play?")
for _ in range(int(time_play)):
         print("Pikachu moved! Pikachu used", next(Pikachu_Fight()))
```

The output will be more interesting: 

<img src= "https://media.giphy.com/media/9rcytvXO6R80l1H8FL/giphy.gif" width = "500">


### Conclusion

So far we introduced the basic information about the function object in Python, how we can use the functions during our programming and the reason why we need a decorator. We have seen how to create a simple decorator and decorate the function. The time control decorator can also be used in many other situations rather than just this simple case. And there are also many fancy decorators waiting for us to explore. 


### Reference 

"Pragmatic AI: An Introduction to Cloud-Based Machine Learning", *by Noah Gift*, 2018, Addison Wesley

