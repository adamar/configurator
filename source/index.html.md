---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>


search: true
---

# Introduction

Configurator is a rudimentary configuration management tool used to configure servers for production service of a simple PHP web application.




# Use

> To run a build, simply pass the yaml file to cfg as the first argument.

<code>
./cfg test.yml
</code>

<aside class="notice">
You must ensure that <code>test.yml</code> with a valid yml file in the local directory.
</aside>


# Installation

To install configurator first you need to ensure that the required dependencies are installed. This can be achieved by running bootstrap.sh.


# Example YML

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

