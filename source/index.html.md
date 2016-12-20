---
title: API Reference

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>


search: true
---

# Configurator

## Introduction

Configurator is a rudimentary configuration management tool used to configure servers for production service of a simple PHP web application.




# Use

To configure a server using Configurator, simply pass the yaml file to the Cfg executable as the first argument. Please ensure that the yml file is in the same directory as the Cfg executable and that the file is formatted correctly.

<code>
./cfg test.yml
</code>

<aside class="notice">
You must ensure that <code>test.yml</code> with a valid yml file in the local directory.
</aside>

You can run Configurator in "Verbose" mode by setting the environment variable "VERBOSE" to true

<code>
VERBOSE=true ./cfg test.yml
</code>


# Installation

To install configurator first you need to ensure that the required dependencies are installed. This can be achieved by running bootstrap.sh.
Now your ready to configure your system using Configurator!

# Example YML

The example yml file shown on the right performs two actions. Firstly it adds a ssh public key to a user and then it installs the Nginx Package from Apt.


```
---
- templateFile:
    template: "authorized_keys.tmpl"
    dest: "/home/jjohnson/.ssh/authorized_keys"
    user: "jjohnson"
    group: "jjohnson"
    mode: "0400"
    variables:
        pubkey: "ssh-rsa AAAAB3Nz"

- installPackage:
    action: "install"
    name: "nginx"

```


# DSL

These are the currently implemented and aavailble functions that can be included in a yml config file along with their requisite parameters.


## installPackage 

Install a package from Apt

Parameter | Required | Description
--------- | ------- | -----------
action | True | The action to take (ie. install, uninstall, upgrade)
name | True | The name of the package to install


## repo

Clone a Git Repo

Parameter | Required | Description
--------- | ------- | -----------
url | True | The git Repo URL
dest | False | The local directory to clone the repo into


## changeOwner

Change the ownership of a file or directory

Parameter | Required | Description
--------- | ------- | -----------
user | True | The user to chown the file or directory to
file | True | The file to chown
group | False | The group to chown the file or directory to
recursive | False | Should the chown be recursive


## templateFile

Create a file from a template

More info about Jinja2 templates can be found here: [Jinja2](http://jinja.pocoo.org/docs/dev/)

Parameter | Required | Description
--------- | ------- | -----------
template | True | The filename of the Jinja2 template file
dest | True | The file that should be created
user | False | The user that should own the file
group | False | The group that should own the file
mode | False | The File permissions in Octal
notify | False | Service to restart on file change or creation
variables | False | A Dict of variables to pass to the Template


## symlink

Create a symlink to an existing file or directory

Parameter | Required | Description
--------- | ------- | -----------
action | True | The action to take (ie. create, remove)
dest | True | The location of the symlink
source | False | The original file or directory


## service

Parameter | Required | Description
--------- | ------- | -----------
name | True | The name of the service
action | True | The action to take on the service (i.e restart, stop, start)

