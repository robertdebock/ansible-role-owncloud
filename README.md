owncloud
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-owncloud"> <img src="https://travis-ci.org/robertdebock/ansible-role-owncloud.svg?branch=master" alt="Build status"/></a> <img src="https://img.shields.io/ansible/role/d/27060"/> <img src="https://img.shields.io/ansible/quality/27060"/>

<a href="https://github.com/robertdebock/ansible-role-owncloud/actions"><img src="https://github.com/robertdebock/ansible-role-owncloud/workflows/GitHub%20Action/badge.svg"/></a>

Install and configure owncloud on your system.

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.httpd
    - role: robertdebock.owncloud
```

The machine you are running this on, may need to be prepared, I use this playbook to ensure everything is in place to let the role work.
```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.buildtools
    - role: robertdebock.epel
    - role: robertdebock.python_pip
    - role: robertdebock.httpd
    - role: robertdebock.redis
    - role: robertdebock.remi
      remi_enabled_repositories:
        - php73
    - role: robertdebock.php
    - role: robertdebock.php_fpm
```


Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for owncloud

# The version of owncloud to install.
owncloud_version: 10.0.10

# The domain under which this server will be available. For example:
# "localhost" or "owncloud.example.com". Does not include protocol identifier,
# (https://) or directories. (/owncloud)
owncloud_domain_url: "{{ ansible_fqdn }}"

# Database connection details.
owncloud_database_name: owncloud
owncloud_database_user: owncloud
owncloud_database_pass: 0wnCl0uD
owncloud_database_host: localhost
owncloud_admin_user: admin
owncloud_admin_pass: OwnCl0uD
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.core_dependencies
- robertdebock.epel
- robertdebock.buildtools
- robertdebock.python_pip
- robertdebock.httpd
- robertdebock.redis
- robertdebock.remi
- robertdebock.php_fpm
- robertdebock.php

```

Dependencies
------------

Most roles require some kind of preparation, this is done in `molecule/default/prepare.yml`. This role has a "hard" dependency on the following roles:

- robertdebock.httpd

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/owncloud.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|amazon|all|
|alpine|all|
|debian|all|
|el|7, 8|
|fedora|all|
|opensuse|all|
|ubuntu|bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| CentOS latest | No package php73 available. |


Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-owncloud) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-owncloud/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
