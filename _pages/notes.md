---
layout: page
title: Notes
permalink: /notes/
toc: true
---

This is my notes pages, I plan on putting a lot of the things I learn and some important syntax in here as well as in the notebook which demonstrates my learning. That means most of the information here can be found somewhere else, but it will all be organized and in one place on this page.


## Python Learns
> Also in the [QnA w/Python](https://toby-leeder.github.io/CSPFastpages/newcode/2022/08/24/pythonQnA.html) post.

I've had very little experience with Python before I used it so here's some of the new functionality I learned and the syntax for it.

| Code | Syntax | Notes |
|-|-|-|
| Variables | key = value | Unlike Java, it looks like Python doesn't really use variable assignments like java. Instead variables can just be assigned "any" and then can be assigned numbers, letters, strings or pretty much watever other value you want including lists. |
| Functions | def function_name(parameter1, parameter2, parameterX): code return value | Functions are pretty similar to other languages for the most part. It is a little different than java in that you don't really use keywords before to define it like int, string or void for the return type or static, private and public. They still function (get it?) pretty much the same though. |
| For loops | for newVar in definedVar: code | For loops are probably the most different from Java. This is because they go through a list of a variable instead of creating a new integer and going until that integer reaches a value. That interger is suprisingly useful, so to me it seems like this change removes some of the functionality of a for loop. Despite this though I still found ways around it and was able to accomplish my goals. 

## Bash Learns
> Also in the [Checks w/Bash](https://toby-leeder.github.io/CSPFastpages/newcode/2022/08/28/Checks.html) post.

I've had basically no experience with Bash before this so it was interesting to learn some of the new functionality now as well. Here is some of what I learned. 

| Code | Syntax | Notes |
|-|-|-|
| Variables | key=value | Most variables work the same and it looks like bash works a similar way as well. You don't put a space in between the key and the value. If you do it looks like bash reads the key as a command and so the variable doesn't work. Also, to call a variable it looks like you need a $ sign in front, otherwise it just reads it as a string. |
| Echo | echo "what you want to print" | Echo is the bash version of print and pretty much works the same, though you can do some cool stuff with periods with it. |
| If then | if [[ condition ]] then code else code fi | This again is pretty similar to java or python though there are some differences. For example the condition needs [[]] which is different. Also, you need a then statement to run the code and at the end you need fi to finish the if statement. |

## More Python Learns
> Also in the [Lists and Dictionaries w/Python](https://toby-leeder.github.io/CSPFastpages/newcode/2022/08/29/python_lists.html)

| Code | Syntax | Notes |
|-|-|-|
| List | key = [value, value, ...] | Lists in python are sorta like arrays in Java. They are different because a list can have multiple different data types within it. Lists can also have multiple dictionary entries in which each dictionary has multiple key and value pairs within it. Entries can be added into a list using the .append() method or just use + and adding it. | 
| Dictionary | dictionary_key = {key: value, key: value ...} | Dictionaries are similar to lists, but instead of just holding values with one single key, each individual value is paired with its own key. That means you can call each value using its unique key. This is useful for a lot of things. You can also create a list of dictionaries, in which a list has multiple dictionary entries. Each dictionary can have multiple key and value pairs and is only considered one entry in the list. |
| Try, except | try: code except error: code except: code | This is an interesting code that I already knew about from previous experience, but I found it could be useful here. Essentially the try portion is what runs initially and it will keep running the code within it until it runs and returns an error. Then the except code runs after. You can change what the except code is depending on the error or you can leave it generic so it runs for any error.|

