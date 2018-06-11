# Description
Using config files when programming allows for the program/script to read confidential
information from a file external to the program. This makes the program/script more
secure as the information is store somewhere else.

# Source Code

		SOURCING(Bash)                  |		Config File
                                                |
#!/bin/bash                                     |	Data="this is data"
CONFFILE="config"                               |
                                                |
source $CONFFILE                                |
echo $DATA                                      |
                                                |
_______________________________________________________________________________
                                                |
		SOURCING(Python)                |		Config File
                                                |
#!/bin/ua	python                          |	data: "this is data"
import pyyaml                                   |
                                                |
def read_config(filename = "config.yaml")       |
	with open(filename) as f:               |
		conf = pyyaml.read(f)           |
	return conf                             |
                                                |
if __name__ == "__main__":                      |
	conf = read_conf()                      |
	print(conf['data'])                     |
    
    
    
    