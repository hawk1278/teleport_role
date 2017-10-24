Role Name
=========

This role installs and configures Gravitational Teleport


Role Variables
--------------
The only main role variable is the "teleport_config".  This is the yaml used to build the configuration file for teleport depending on the type of node being deployed.

Dependencies
------------

Right now the only dependency is supervisord being installed.


Example Playbook
----------------

```---
- name: Install Teleport
  hosts: all
  gather_facts: true
  become: true
  roles:
  - role: teleport
    teleport_config: |
      teleport:
        nodename: auth2
        data_dir: /var/lib/teleport
        log:
          output: syslog
          severity: INFO
        storage:
          type: dynamodb
          region: us-east-1
          table_name: teleport.state
          access_key: 
          secret_key: 
        advertise_ip: 
        auth_token: hello
      auth_service:
        cluster_name: tele-test
        enabled: "yes"
        listen_addr: 0.0.0.0:3025
        tokens:
          - "proxy,node:hello"
        authentication:
          type: local
          second_factor: off
      ssh_service:
        enabled: "no"
      proxy_service:
        enabled: "no"
```
License
-------

BSD
