owncloud
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-owncloud.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-owncloud)

Provides owncloud for your system.

Context
-------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/robertdebock.github.io/artifacts/owncloud.png "Dependency")

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
|alpine-3.6|yes|yes|yes|
|alpine-3.7|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|no|no|no|
|centos-7|yes|yes|yes|
|debian-buster|yes|yes|yes|
|debian-stretch|yes|yes|yes|
|debian-wheezy|yes|yes|yes|
|fedora-27|yes|yes|yes|
|fedora-28|yes|yes|yes|
|opensuse-42.2|yes|yes|yes|
|opensuse-42.3|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-bionic|yes|yes|yes|

Example Playbook
----------------

The simplest way possible:
```
- hosts: servers
  become: true

  roles:
    - robertdebock.bootstrap
    - robertdebock.epel
    - robertdebock.buildtools
    - robertdebock.scl
    - robertdebock.python-pip
    - robertdebock.php
    - robertdebock.httpd
    - robertdebock.owncloud
```

You can also call this role without having `become: true`, because the tasks that require elevated privileges have `become: true` added.

Install this role using `galaxy install robertdebock.owncloud`.

License
-------

Apache License, Version 2.0

Author Information
------------------

Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
