# elk

This is a basic layout for an ansible project that can be expanded to support a site with a common set of utilities to be run on all hosts.  It can be tested using Vagrant.

These roles are a home grown project as an alternative to elastic's own ansible role: 

https://github.com/elastic/ansible-elasticsearch 

purely for my own learning with Ansible.

## How to use these roles

To use these roles inside of ansible, 

* add the **elasticsearch, java, kibana, logstash, nginx, repo-elk, and repo-epel** directory trees to your roles/ directory inside your ansible repository
* edit your inventory file to use the common role for every host (or specific hosts)
* to add packages, services, files, etc. to the common role:
  - modify variable *base_packages* in **roles/common/defaults/main.yml**
  - modify type or distro files in **roles/common/vars** for OS-specific stuff


## Using Vagrant and Virtual Box for testing

I developed this model on MacOS using Vagrant and Virtual Box.  To use this repo, install the following on your Mac:

- [Vagrant](https://www.vagrantup.com/downloads.html)
- [Virtual Box](https://www.virtualbox.org/wiki/Downloads)
- [Python 2.7.15](https://www.python.org/downloads/release/python-2715/])
- [Ansible](https://hvops.com/articles/ansible-mac-osx/)

Make sure your .bashrc or .bash_profile has the environment variables for the Oracle proxy server:

    export http_proxy="http://www-proxy.us.oracle.com:80”
    export https_proxy="https://www-proxy.us.oracle.com:80”

After you’ve installed Vagrant, install the proxy-server plugin:

    vagrant plugin install vagrant-proxyconf

And that you’ve defined the proxy server in your global git configuration:

    git config --global http.proxy http://www-proxy.us.oracle.com:80

And finally clone the repo in your home directory

    git clone https://github.com/mvilain/elk.git

**Note:** getting files from your Mac to the vagrant box is easy.  The box is setup to share the elk directory that’s running the model with /vagrant on the running box.  So once you login to the box with

    vagrant ssh <box name>

you will be able to move files from a live server or wherever to /var/log for logstash to digest and try to send to the running elasticsearch box.

This should work fine on the Oracle network.  But to run the model, you’ll need to be on a regular wifi connection without a proxy server:

    vagrant up

The model creates 

- 2 logstash instances (Ubuntu 18.04 and CentOS7)
- 2 elasticsearch instances (CentOS6)
- 1 kibana instance (CentOS6)

But only the elasticsearch running on the kibana instance is used as a Proof-Of-Concept.  I haven’t tried putting logs on the logstash instances and seeing if they push the values to the elasticsearch instances.  That would be the next step for this POC.

You should be able access kibana on the kibana1 instance from your browser:

    http://192.168.10.101:81


## OS and Versions Tested

The following OS and versions have been tested:

- CentOS 6 and 7
- Ubuntu 18, Debian 8 (jessie), and 9 (stretch)
