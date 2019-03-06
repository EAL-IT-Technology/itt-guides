---
layout: guide
date:   2019-03-02 21:00:39 +0200
title:  How do I create a bug report?
categories: tech
status: beta
---

# Use case

Whenever you use software and the sodtware seems to be mis-behaving. You should consider contacting the author(s) of the software and work with them to fix the issue.

This usually involves creating an issues on github or gitlab or a bugreport on bugzilla or whereever and however the author has published the program and expects to get feedback.

As with all communication, there is an audience for you bug report and a purpose. The better the bug report, the more likely it is that the problem will get resolved - either by a bugfix or by you correcting a mistake in e.g. a config file.

The audience is the author and the community around the project. So anything implied in the bug report, because you know inside information is a bad thing, since everybody must be able to understand what the issue is.

The purpose of the bug report is for you to get help to solve your issue. Sometimes you made a mistake, sometimes the documentation is poor, sometimes there is a bug in the program, sometimes ...

Since you normally don't know which case you are in, be courteous and offer to supply more information or test solutions.

In the end, you will have a solution to your problem and the project will be improved either by improved documentation or by a bugfix.


# Create the issue

On github.com and gitlab.com, there are no technical difference in create bug report and creating normal issue. It is the content that is different.

When it comes to the content, read the following blog entries:

* Oldie but goodie: [https://www.chiark.greenend.org.uk/~sgtatham/bugs.html](https://www.chiark.greenend.org.uk/~sgtatham/bugs.html)
* from instabug: [How to Write a Bug Report: The Ideal Bug Report](https://instabug.com/blog/how-to-write-a-bug-report-the-ideal-bug-report/)

Sometimes the project or the author have a template for you to fill out in order to file a bug report. Use it. [Ansible on github](https://github.com/ansible/ansible/issues/new?template=bug_report.md) uses specific bug report template.

One of the reasons of having a bug-template, is to eliminate the "bugs" that relates to people being careless or confused. Going through the problem in detail to collect information for the bug report, will often result in you finding resources or mistakes that solves the issue for you. So be thourough - it is best for everybody.

From time to time, you will find a bug in the program yourself, and then you will do a [merge request](https://docs.gitlab.com/ee/user/project/merge_requests/#overview) (in gitlab) or [pull request](https://help.github.com/en/articles/about-pull-requests) (in github) with the solution.


# Follow up

Now you have filled a good bug report, and (hopefully) someone will answer.

Your job now is to follow up on any activity, and supply as much support as you can to the author/programmer/project to get the issue resolved. This is especially critical when they request ore information - dothat as quickly as possible, so they can continue solving the issue.

Remember to go back to the bug report, should you find the solution yourself. You will then write a summary of the solution and perhaps something extra "for whoever finds this using google" - links are always a good idea.
