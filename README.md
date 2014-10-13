marklee77.mariadb
=================

[![Build Status](https://travis-ci.org/marklee77/ansible-role-mariadb.svg?branch=master)](https://travis-ci.org/marklee77/ansible-role-mariadb)

The purpose of this role is to deploy MariaDB onto Ubuntu. There is also an
support for an experimental "dockerized" deployment. This dockerized deployment
copies the role to the target machine and uses the original ansible-based
functionality to build a docker image, and then uses recent ansible features to
manage the running service. The dockerized deployment can theoretically deploy
to any Linux platform with a running docker install and the docker-py python
client library installed.

Travis status above refers only to the non-dockerized deployment, as docker does 
not (easily) run on travis.

Role Variables
--------------

- mariadb_repository_mirror: http://mirrors.coreix.net/mariadb by default.
- mariadb_version: 10.0
- mariadb_mysql_root_password: random value
- mariadb_enable_remote: false
- mariadb_set_root_password: true

The variables below only affect the dockerized deployment:

- mariadb_dockerized_deployment: false
- mariadb_docker_username: default
- mariadb_docker_imagename: mariadb
- mariadb_docker_containername: mariadb
- mariadb_port: 3306

Example Playbook
-------------------------

    - hosts: all
      sudo: True
      roles:
        - marklee77.mariadb

License
-------

GPLv2

Author Information
------------------

http://stillwell.me

Known Issues
------------

- the dockerized deployment still requires sudo access, even though a member of 
  the docker group should be able to build and deploy containers without sudo.

Todo
----

- delegate_to in order to allow for installing on hosts different from mariadb host...
- combine offline/run/online with startup script? config info could be passed via environment variables as normal...
- keystone token flush cron job
