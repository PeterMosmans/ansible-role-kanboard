Ansible Role: kanboard
=========

Build status for this role: [![Build Status](https://travis-ci.org/PeterMosmans/ansible-role-kanboard.svg)](https://travis-ci.org/PeterMosmans/ansible-role-kanboard)

This role installs, configures and/or upgrades Kanboard on a server. It does not
install a webserver like Apache by itself.

Requirements
------------

A webserver, and PHP. This role works seamlessy with (shameless plug) (https://github.com/PeterMosmans/ansible-role-apache2)[PeterMosmans.Ansible]
Remember to check the latest Kanboard release (# check the latest release here https://github.com/kanboard/kanboard/releases/latest) and set the kanboard_source variable. 

Role Variables
--------------

The defaults are set in `defaults/main.yml`:

```
# check the latest release here https://github.com/kanboard/kanboard/releases/latest
kanboard_source: https://kanboard.net/kanboard-latest.zip
kanboard_base: /var/www/ # last / is important to build paths
kanboard_directory_name: html
kanboad_complete_path: "{{ kanboard_base }}{{ kanboard_directory_name }}/"
kanboard_preconfigure: true
kanboard_tmp: /tmp/kanboard
kanboard_upload: "{{ kanboard_base }}{{ kanboard_directory_name }}/data"
kanboard_plugin_dir: "{{ kanboard_upload }}/plugins"
kanboard_group: www-data
kanboard_user: root
kanboard_files_mode: 0770
php_package_version: php # could be php7.3 php7.0 ... Useful if you use https://deb.sury.org/
kanboard_configuration_file: false
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
