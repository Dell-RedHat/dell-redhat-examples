sonic_backup_restore
=========

This role allows backing up and restoring DELL Sonic switches configuration

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

    sonic_backup:
      path:                     # Absolute path on backup_host to store config
      archive_filename:         # Config backup archive name - Defaults to "{{ inventory_hostname }}_config"

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

--- Backup switch config

    ---
    - name: Dell switches configuration backup
      hosts: dell_switches
      gather_facts: true
      connection: network_cli

      tasks:
        - name: Include role to backup the configuration
          ansible.builtin.include_role:
            name: sonic_backup_restore
          vars:
            sonic_backup:
              path: /opt/sonic
              archive_filename: myconfig
            sonic_config_backup: true

--- Restore switch config

    ---
    - name: Dell switches configuration backup
      hosts: dell_switches
      gather_facts: true
      connection: network_cli

      tasks:
        - name: Include role to backup the configuration
          ansible.builtin.include_role:
            name: sonic_backup_restore
          vars:
            sonic_backup:
              path: /opt/sonic
              archive_filename: myconfig
            sonic_config_restore: true

License
-------

BSD

Author Information
------------------

Alessandro Rossi <alerossi@redhat.com>
Ahmed Gaber <agaber@redhat.com>
Thibaut Perrin <thibaut.perrin@dell.com>
