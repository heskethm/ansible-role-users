Ansible Role: Users and Groups
==============================

[![Build Status](https://travis-ci.org/heskethm/ansible-role-users.svg)](https://travis-ci.org/heskethm/ansible-role-users)

Ansible role for managing system users and groups.

Installation
------------

```
$ ansible-galaxy install heskethm.users
```

Role Variables
--------------

All available variables and default values are listed below. You may override these in your Playbook, `group_vars`, command line etc.

```yml
# Default value
users_groups: []

# Available options
users_groups:
- name: ""              # Group name
  gid ""                # (optional) Specify GID
  system: no            # (optional) Setting to 'yes' makes this user a system group
```

Groups to add / modify on the system. Takes optional parameters from the [Group module](http://docs.ansible.com/ansible/group_module.html).

```yml
# Default value
users_groups_removed: []
```

List of groups to remove from the system.

```yml
# Default value
users_users: []

# Available options
users_users:
- name: ""              # Username
  authorized_keys: []   # List of file paths to public keys to add to the user's authorized keys list
  password: ""          # (optional) Password
  group: ""             # (optional) Sets user's primary group
  groups: []            # (optional) Groups to add the user to. Takes a YAML list.
  comment: ""           # (optional) User's description
  home: ""              # (optional) User's home directory
  shell: ""             # (optional) User's shell
  uid: ""               # (optional) User's UID
  system: no            # (optional) Setting to 'yes' makes this user a system account
  generate_ssh_key: no  # (optional) Create an SSH key for this user. Does not override an existing key
```

Users to add / modify on the system. Takes optional parameters from the [Users module](http://docs.ansible.com/ansible/user_module.html).

```yml
# Default value
users_users_removed: []
```

List of users to remove from the system.

Dependencies
------------

None

Example Playbook
----------------

```yml
- hosts: web
  roles:
     - { role: heskethm.users }
```

Example Usage
-------------

```yml
users_groups:
- name: "winterfell"
- name: "nightswatch"
- name: "wildlings"

users_groups_removed:
- name: "targaryen"

users_users:
# Robb
- name: "robb"
  group: "winterfell"
  authorized_keys:
  - "files/keys/ned.pub"
  - "files/keys/robb-home-pc.pub"

# John
- name: "john"
  group: "winterfell"
  groups:
  - "nightswatch"
  - "wildlings"
  generate_ssh_key: yes
  authorized_keys:
  - "files/keys/ned.pub"
  - "files/keys/john-work.pub"

users_users_removed:
- name: "ned"
- name: "cat"
```

Author
------

* Web: [markhesketh.co.uk](http://www.markhesketh.co.uk/)
* Email: [contact@markhesketh.co.uk](mailto:contact@markhesketh.co.uk)
* Twitter: [twitter.com/markyhesketh](http://www.twitter.com/markyhesketh/)
* Github: [github.com/heskethm](http://www.github.com/heskethm/)

License
-------

[MIT](http://opensource.org/licenses/MIT)
