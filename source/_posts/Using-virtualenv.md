---
title: Using virtualenv
date: 2018-01-31 11:08:44
tags:
---
It is a good practice to use virtualenv to setup independent pythoon envirnoment. Especially, there are multi-version of python this machine.
For details check [here](https://virtualenv.pypa.io/en/stable/)

<!-- more -->

## Install
Using Pip (>1.3) install
{% codeblock lang:bash line_number:false %}
$ [sudo] pip install virtualenv
{% endcodeblock %}

## Using
1. Create a folder for this env (trying to setup a python2.7 env)
{% codeblock lang:bash line_number:false %}
$ mkdir py27env
$ cd py27env
{% endcodeblock %}
1. Create virtualenv for python2.7, in my mac the python27 is located at `/usr/bin/python2.7`
thus a virtualenv is created with then name (folder) `py27env` by python2.7
{% codeblock lang:bash line_number:false %}
$ virtualenv --python=/usr/bin/python2.7 py27env
{% endcodeblock %}
1. Active the env
{% codeblock lang:bash line_number:false %}
$ cd py27env
$ source bin/activate
{% endcodeblock %}
Then you can see the shell prompt is changed, py27env is added to the shell prompt
{% codeblock lang:bash line_number:false %}
(py27env) C02NF73EG3QD:py27env guyu$
{% endcodeblock %}
1. Leave the env
Run the following script under the env 
{% codeblock lang:bash line_number:false %}
$ deactivate
{% endcodeblock %}
if you want to clean all the env, then you can remove the folder
{% codeblock lang:bash line_number:false %}
$ rm -r path/to/env
{% endcodeblock %}