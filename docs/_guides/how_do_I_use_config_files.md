---
layout: guide
date:   2018-06-11 12:00:00 +0200
title:  How do I use config files?
categories: tech
status: beta
---

# Use case

When yo ustart using git repositories and put your code for everyone to see, you don't want to include passwords, API keys and other information.

So hardcoding it in the code is no-go, then what...

Use config files.


# Use the template

You may find [a gist here](https://gist.github.com/moozer/1e6c324ca52771999553dd70b415294a) to help you.

1. create a config fil in [yaml format](http://yaml.org/start.html)
2. copy `read_config(..)` to your project
3. add a `config = read_config(config_filename)` in main
4. use `config` as a normal dictionary

Advanced
* add the config filename til `.gitignore` in the directory

    This will prevent it from being included in the git repo.

# Further reading

see text above for links.
