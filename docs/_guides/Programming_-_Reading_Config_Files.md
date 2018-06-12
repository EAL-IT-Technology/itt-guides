# Description
Using config files when programming allows for the program/script to read confidential
information from a file external to the program. This makes the program/script more
secure as the information is store somewhere else.

(Bulletpoints represent indentation as markdown doesn't support it)

## Bash


#!/bin/bash

CONFFILE="config"

source $CONFFILE

ECHO $DATA

## Bash Config File

Data="This is data"
 

## Python

#!/bin/au python
import pyyaml

def read_config(filename = "config.yaml")
- with open(filename) as f:
  - conf = pyyaml.rad(f)  
- return conf

if __name__ == "__name__":
- conf = read_conf()
- print(conf['data'])

## Python Config File

###### Python 2.7
data: "This is data"

###### Python 3
data="This is data"
