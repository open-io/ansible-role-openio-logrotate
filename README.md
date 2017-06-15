Role Name
=========

This Ansible role is intended initially to manage OpenIO logrotate file (/etc/logrotate.d/openio-sds) and it installs logrotate pkg.
But it manage /etc/logrotate.conf and other files in /etc/logrotate.d/ too.

Requirements
------------

Ansible: 2.2

Role Variables
--------------

All variables for OpenIO logrotate are configured in defaults/main.yml.
It's afford all existing option in logrotate software (see man logrotate)

If you want to add a file it could be done by:
```
  - filename: app.conf
    sections:
    - logs: [ '/var/log/app/app.log' ]
      options: |
        missingok
        notifempty
        hourly
        rotate 24
        compress
        sharedscripts
        postrotate: '/bin/kill -HUP `cat /var/run/app.pid 2> /dev/null` 2> /dev/null || true'
```


Playbook
---------

There are two possible playbooks (it always install logrotate if not present):

One for only configure OpenIO logrotate:
```
---
- name: Install and configure logrotate for OpenIO
  hosts: servers
  roles:
    - { role: ansible-role-openio-logrotate }
```

And the second that manage /etc/logrotate.conf too:
```
---
- name: Install and configure logrotate for OpenIO
  hosts: servers
  roles:
    - { role: ansible-role-openio-logrotate, logrotate__enabled: True }
```


License
-------

Apache 2.0

Author Information
------------------

Lapierre Sébastien (http://www.openio.io/)

