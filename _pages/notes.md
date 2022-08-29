---
layout: page
title: Notes
permalink: /notes/
toc: true
---

{% include info.html text="This is my notes pages, I plan on putting a lot of the things I learn and some important syntax in here as well as in the notebook which demonstrates my learning. That means most of the information here can be found somewhere else, but it will all be organized and in one place on this page. " %}


## Python Learns
> Also in the [QnA w/Python](https://toby-leeder.github.io/CSPFastpages/newcode/2022/08/24/pythonQnA.html) post.

I've had very little experience with Python before I used it so here's some of the new functionality I learned and the syntax for it.

| Code | Syntax | Notes |
|-|-|-|
| Variables | key = value | Unlike Java, it looks like Python doesn't really use <br> variable assignments like java. Instead variables <br> can just be assigned "any" and then can be <br> assigned numbers, letters, strings or pretty much <br> watever other value you want including lists. |
| Functions | def function_name(parameter1, parameter2, parameterX): <br>   code <br>   return value | Functions are pretty similar to other languages <br> for the most part. It is a little different than java <br> in that you don't really use keywords before to define <br> it like int, string or void for the return type or <br> static, private and public. They still function (get it?) <br> pretty much the same though. |
| For loops | for newVar in definedVar: <br> code | For loops are probably the most different from Java. <br> This is because they go through a list of a variable <br> instead of creating a new integer and going until that <br> integer reaches a value. That interger is suprisingly <br> useful, so to me it seems like this change removes <br> some of the functionality of a for loop. Despite this <br> though I still found ways around it and was able <br> to accomplish my goals. 

## Bash Learns
> Also in the [Checks w/Bash](https://toby-leeder.github.io/CSPFastpages/newcode/2022/08/28/Checks.html) post.

I've had basically no experience with Bash before this so it was interesting to learn some of the new functionality now as well. Here is some of what I learned. 

| Code | Syntax | Notes |
|-|-|-|
| Variables | key=value | Most variables work the same and it looks like bash works a similar <br> way as well. You don't put a space in between the key and the value. <br> If you do it looks like bash reads the key as a command and so the <br> variable doesn't work. Also, to call a variable it looks like you need <br> a $ sign in front, otherwise it just reads it as a string. |
| Echo | echo "what you want to print" | Echo is the bash version of print and pretty much works the same, <br> though you can do some cool stuff with periods with it. |
| If then | if [[ condition ]] <br> then <br> code <br> else <br> code <br> fi | This again is pretty similar to java or python though there are some <br> differences. For example the condition needs [[]] which is different. <br> Also, you need a then statement to run the code and at the end you <br> need fi to finish the if statement. |
