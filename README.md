owncloud
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-owncloud.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-owncloud)

Provides owncloud for your system.

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-owncloud) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-owncloud/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many scenarios available, please have a look in the `molecule/` directory.

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

- owncloud_version: The version of owncloud to install.

- owncloud_domain_url: The domain under which this server will be available.

- owncloud_database_name: The database to connect to.
- owncloud_database_user: The username to connect to the database.
- owncloud_database_pass: The password to connect to the database.
- owncloud_database_host: The host where the database is hosted.
- owncloud_admin_user: A username to create in Owncloud.
- owncloud_admin_pass: A password for that user.

Dependencies
------------

This role can be used to prepare your system:

- [robertdebock.bootstrap](https://travis-ci.org/robertdebock/ansible-role-bootstrap)
- [robertdebock.buildtools](https://travis-ci.org/robertdebock/ansible-role-buildtools)
- [robertdebock.epel](https://travis-ci.org/robertdebock/ansible-role-epel)
- [robertdebock.python_pip](https://travis-ci.org/robertdebock/ansible-role-python_pip)
- [robertdebock.httpd](https://travis-ci.org/robertdebock/ansible-role-httpd)
- [robertdebock.php](https://travis-ci.org/robertdebock/ansible-role-php)


Download the dependencies by issuing this command:
```
ansible-galaxy install --role-file requirements.yml
```

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|
|------------|-----------|-----------|-----------|
|alpine-edge|yes|yes|yes|
|alpine-latest|yes|yes|yes|
|archlinux|yes|yes|yes|
|centos-6|no|no|no|
|centos-latest|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|yes|yes|yes|
|opensuse-tumbleweed|yes|yes|yes|
|ubuntu-artful|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

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

    - name: include python_pip role
      include_role:
        name: robertdebock.python_pip

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

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
