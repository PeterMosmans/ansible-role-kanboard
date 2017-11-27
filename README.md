Ansible Role: kanboard
=========

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-kanboard.svg)](https://travis-ci.org/PeterMosmans/ansible-role-kanboard)

This role installs, configures and/or upgrades Kanboard on a server. It does not
install a webserver like Apache by itself.

Requirements
------------

A webserver, and PHP. This role works seamlessy with (shameless plug) (https://github.com/PeterMosmans/ansible-role-apache2)[PeterMosmans.Ansible]

Role Variables
--------------

The defaults are set in `defaults/main.yml`:

```
kanboard_source: https://kanboard.net/kanboard-latest.zip
kanboard_base: /var/www/html
kanboard_preconfigure: true
kanboard_tmp: /tmp/kanboard
kanboard_upload: /var/www/html/data
kanboard_plugin_dir: data/plugins
kanboard_group: www-data
kanboard_user: root
```


Optionally, plugins can be specified, that will be installed as well, using the
`kanboard_plugins` list with plugin name (`name`) and remote source (`src`) pairs. Example:
```
kanboard_plugins:
  - name: Calendar
    src: https://github.com/kanboard/plugin-calendar/releases/download/v1.1.0/Calendar-1.1.0.zip
  - name: Gantt
    src: https://github.com/kanboard/plugin-gantt/releases/download/v1.0.2/Gantt-1.0.2.zip
```

Tags
----
Use the `upgrade` tag to upgrade an existing installation, including plugins.


Dependencies
------------

None.


Example Playbook
----------------

```
- hosts: all
  become: yes
  become_method: sudo
  roles:
  - role:PeterMosmans.kanboard
  vars:
    - name: Gantt
      src: https://github.com/kanboard/plugin-gantt/releases/download/v1.0.2/Gantt-1.0.2.zip
```

License
-------

GPLv3


Author Information
------------------

Created by Peter Mosmans. Suggestions, feedback and pull requests are always welcome.
