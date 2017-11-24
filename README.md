Icinga 2 ansible module
===
### A ansible module to deploy your Icinga 2 infrastruktur

In the actual state the module is capable to deploy a master and clients.
We install all necessary packages and will setup a CA to authorize the clients.
___
Sub-roles
===
* common

  manages common tasks like repositories and installing packages

* icinga2-base

  disables the example configuration on the client

* icinga2-ca

   installs the ca on the CA master and signs it

* icinga2-certs

  manages certificate requests and signing on the clients

* icinga2-client

  ready to use role which includes (common, icinga2-base, icinga2-ca, icinga2-certs)

* icinga2-feature-handler

  handles enabled features and configures them in their configuration directory

* icinga2-IDO

  manages the icinga 2 IDO feature, supports pgsql and mysql

* icinga2-master

  ready to use role, sets up a whole icinga 2 master with basic configuration.
___

Disclaimer
======

This isn't ready for use a this time
___
Installation
======

todo

___
Example site.yml
===
```
- name: provision all master hosts ayy
  hosts: gazorpazorp
  become: true
  vars_files:
    - roles/icinga2-ansible/group_vars/icinga2.yml
    - roles/icinga2-ansible/group_vars/icinga2-master.yml
    - roles/icinga2-ansible/group_vars/secret_vault.yml
  roles:
    - { role: mysql }
    - { role: roles/icinga2-ansible/roles/common }
    - { role: roles/icinga2-ansible/roles/icinga2-base }
    - { role: roles/icinga2-ansible/roles/icinga2-ca }
    - { role: roles/icinga2-ansible/roles/icinga2-certs }
    - { role: roles/icinga2-ansible/roles/icinga2-IDO }
    - { role: roles/icinga2-ansible/roles/icinga2-feature-handler }


- name: provision all icinga2 clients ayy
  hosts: screamingsunearth
  become: true
  vars_files:
    - roles/icinga2-ansible/group_vars/icinga2.yml
  roles:
    - { role: roles/icinga2-ansible/roles/icinga2-client, icinga2_manage_certs: force}
```
