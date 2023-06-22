sonic_manage_vlans
=========

This role allows creating and deleting VLANs on DELL Sonic Switches

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

    sonic_vlans:
      - vlan_id:              # Id of the VLAN to be created/deleted
    sonic_vlan_delete:        # Boolean to manage VLANs deletion - Defaults to false

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

--- Create VLANs

    ---
    - name: Dell VLAN Management Demo
      hosts: dell_switches
      gather_facts: false
      connection: httpapi
      collections:
        - dellemc.enterprise_sonic
      tasks:
        - name: Include role to configure port access
          ansible.builtin.include_role:
            name: sonic_manage_vlan
          vars:
            sonic_vlans:
              - vlan_id: 10
              - vlan_id: 11
              - vlan_id: 42

--- Delete VLANs

    ---
    - name: Dell VLAN Management Demo
      hosts: dell_switches
      gather_facts: false
      connection: httpapi
      collections:
        - dellemc.enterprise_sonic
      tasks:
        - name: Include role to configure port access
          ansible.builtin.include_role:
            name: sonic_manage_vlan
          vars:
            sonic_vlans:
              - vlan_id: 10
              - vlan_id: 11
              - vlan_id: 42
            sonic_vlan_delete: true

License
-------

BSD

Author Information
------------------

Alessandro Rossi <alerossi@redhat.com>
Ahmed Gaber <agaber@redhat.com>
Thibaut Perrin <thibaut.perrin@dell.com>