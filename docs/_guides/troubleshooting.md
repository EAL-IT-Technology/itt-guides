---
date: 2018-04-17 12:00:00 +0000
layout: guide
title:  Structured troubleshooting
categories: tech
status: beta
---

Unstructured vs. strutcuted troubleshoothing
=========================================

Troubleshooting is an arcane art, that a lot people just do by trying out different things, and hoping it works.

In most cases, with a bit of experience, unstructured troubleshooting will solve your problem. It will not however ensure that you know what happened and tell you if it will happen againg. Worse, you wil have changed stuff back and forth in your system,and often created new problems for yourself.

Structured troubleshooting done right, will ensure that you find root cause, and that you, in time, becomes an expert with the system. This brings us to the concept of [the expert beginner](https://daedtech.com/how-developers-stop-learning-rise-of-the-expert-beginner)- don't become him.

Structured troubleshooting
======================

This is basically a series of questions, that should guide you whenever you get stuck or stuff start acting up.

1. What are you trying to do?

    This is the fundamental questions. It is very relevant, since it counters the effect of being super-focussed on some very small detail - which you tend to do when debugging.
    
2. What is working? What is not working?

    Formulate what you think is working, and what you think is not working. This help you narrow donw were to focus
    
3. How do you know?

    You think you know the state of your system, and you have some clues. Figure out whether or not you are on solid ground with your working/not wokring assumptions.
    This could includes tests to make it obvious.

4. What do you think is wrong?

    You now know the state, you know what you want to achieve and it is not obvious why stuff i not working. Make a hypothesis, ie. give it your best guess. Now would be a good time to include others and ask for help, if you don't have any ideas. 
    Going through point 1, 2 and 3, while telling what you see, will force you to formulate what you are doing, and will often result in the solution being obvious. Really - this is the magic IT supporter trick
    
5. How to test?

    Having decided on a candidate for what is wrong, devise a test that shows whether or not your hypothesis is correct.
    
6. Test it

    This can have one of two outcomes: 1) you were right and now you know what is wrong or 2) you were wrong.
    In case 2, you must go back review 2 and 3, and come up with new ideas for 3 and 4.
    
7. Fix it

    Sounds easy, and sometimes it is. At other times, finding the solution is difficult or it desn't exist. 
    If the solution is not to be found, point 1 must be revised.
