owncloud
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-owncloud.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-owncloud)

Provides owncloud for your system.

Context
-------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/owncloud.png "Dependency")

Requirements
------------

Access to a repository containing packages, likely on the internet.

Role Variables
--------------

None known.

Dependencies
------------

This role can be used to prepare your system:

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)
- [robertdebock.buildtools](https://travis-ci.org/robertdebock/ansible-role-buildtools)
- [robertdebock.epel](https://travis-ci.org/robertdebock/ansible-role-epel)
- [robertdebock.scl](https://travis-ci.org/robertdebock/ansible-role-scl)
- [robertdebock.python-pip](https://travis-ci.org/robertdebock/ansible-role-python-pip)
- [robertdebock.httpd](https://travis-ci.org/robertdebock/ansible-role-httpd)
- [robertdebock.php](https://travis-ci.org/robertdebock/ansible-role-php)


Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.3|ansible 2.4|ansible 2.5|
|------------|-----------|-----------|-----------|
|alpine-3.6|no|yes|yes|
|alpine-3.7|no|yes|yes|
|archlinux|no|yes|yes|
|centos-6|no|no|no|
|centos-7|no|yes|yes|
|debian-buster|no|yes|yes|
|debian-stretch|no|yes|yes|
|fedora-27|no|yes|yes|
|fedora-28|no|yes|yes|
|opensuse-42.2|no|yes|yes|
|opensuse-42.3|no|yes|yes|
|ubuntu-artful|no|yes|yes|
|ubuntu-bionic|no|yes|yes|

Example Playbook
----------------

The simplest way possible:
```
- hosts: servers
  become: true
  gather_facts: no

  tasks:
    - name: include bootstrap role
      include_role:
        name: robertdebock.bootstrap

    - name: include mysql role
      include_role:
        name: robertdebock.mysql

    - name: create mysql database
      mysql_db:
        name: owncloud

    - name: create mysql user
      mysql_user:
        name: owncloud
        password: OwnCl0uD
        priv: "*.*:ALL"

    - name: include epel role
      include_role:
        name: robertdebock.epel

    - name: include buildtools role
      include_role:
        name: robertdebock.buildtools

    - name: include scl role
      include_role:
        name: robertdebock.scl

    - name: include python-pip role
      include_role:
        name: robertdebock.python-pip

    - name: include php role
      include_role:
        name: robertdebock.php

    - name: include role httpd
      include_role:
        name: robertdebock.httpd

    - name: include owncloud role
      include_role:
        name: robertdebock.owncloud
```

You can also call this role without having `become: true`, because the tasks that require elevated privileges have `become: true` added.

Install this role using `galaxy install robertdebock.owncloud`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
