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
## Python/yaml

You may find [a gist here](https://gist.github.com/moozer/1e6c324ca52771999553dd70b415294a) to help you.

1. Create a config file in [yaml format](http://yaml.org/start.html)
2. Copy `read_config(..)` to your project
3. Add a `config = read_config(config_filename)` in main
4. Use `config` as a normal dictionary

Advanced
* add the config filename to `.gitignore` in the directory

    This will prevent it from being included in the git repo.

## Bash

Here is a [gist](https://gist.github.com/Azarion196/e39e2f70ae08c6ff6362a1c4f4d27c72) with an example.

1. Create a config file using bash syntax.
2. Copy the `CONFIG`and `Source $CONFIG` lines to your project.
3. Reference the variable you need from the config file.

# Further reading

see text above for links.
