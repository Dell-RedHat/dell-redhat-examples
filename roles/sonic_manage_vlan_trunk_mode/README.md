sonic_manage_vlan_trunk_mode
=========

This role allows configuring VLANs in trunk mode on DELL Sonic Switches.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

    sonic_interfaces:
      - name:                 # Name of the interface to perform the operation on
        allowed_vlans:        # List of LANS to be configured in trunk mode
        unallowed_vlans:      # List of LANS to be removed in trunk mode

    sonic_remove_trunk_mode:  # Boolean to toggle enable/disable of trunk mode - Defaults to false

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

--- Configure interfaces set of VLANs to trunk mode

    ---
    - name: Dell VLAN Management Demo
      hosts: dell_switches
      gather_facts: false
      connection: httpapi
      collections:
        - dellemc.enterprise_sonic
      tasks:
        - name: Include role to configure trunk mode
          ansible.builtin.include_role:
            name: sonic_manage_vlan_trunk_mode
          vars:
            sonic_interfaces:
              - name: Eth1/1/4
                allowed_vlans:
                  - 10
                  - 11
                  - 42
                  - 50
                  - 100
                  - 112
                  - 113

--- Configure interfaces set of VLANs to disable trunk mode

    ---
    - name: Dell VLAN Management Demo
      hosts: dell_switches
      gather_facts: false
      connection: httpapi
      collections:
        - dellemc.enterprise_sonic
      tasks:
        - name: Include role to configure trunk mode
          ansible.builtin.include_role:
            name: sonic_manage_vlan_trunk_mode
          vars:
            sonic_interfaces:
              - name: Eth1/1/4
                unaallowed_vlans:
                  - 100
                  - 112
                  - 113
            sonic_remove_trunk_mode: true

License
-------

BSD

Author Information
------------------

Alessandro Rossi <alerossi@redhat.com>
Ahmed Gaber <agaber@redhat.com>
Thibaut Perrin <thibaut.perrin@dell.com>