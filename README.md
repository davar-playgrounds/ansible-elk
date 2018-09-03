# elk

This is a basic layout for an ansible project that can be expanded to support a site with a common set of utilities to be run on all hosts.  It can be tested using Vagrant.

These roles are a home grown project as an alternative to elastic's own ansible role: https://github.com/elastic/ansible-elasticsearch purely for
my own learning

## How to use

To use these roles inside of ansible, 

* add the **elasticsearch, java, kibana, logstash, nginx, repo-elk, and repo-epel** directory trees to your roles/ directory inside your ansible repository
* edit your inventory file to use the common role for every host (or specific hosts)
* to add packages, services, files, etc. to the common role:
  - modify variable *base_packages* in **roles/common/defaults/main.yml**
  - modify type or distro files in **roles/common/vars** for OS-specific stuff


## Using Vagrant and Virtual Box for testing


## OS and Versions Tested

The following OS and versions have been tested:

- CentOS 6 and 7
- Debian 8 (jessie) and 9 (stretch)
