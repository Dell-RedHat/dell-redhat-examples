sonic_manage_vlan_access_mode
=========

This role allows configuring VLANs access mode on DELL Sonic Switches.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

    sonic_interfaces:
      - name:                       # Name of the interface to perform the operation on
        access_vlan:                # VLAN to be configured in access mode
    sonic_remove_port_access:       # Boolean, toggles set/unset - Default false

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

--- Enabling port access for VLAN 42 on interface eth1/1/4
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
            name: sonic_manage_vlan_access_mode
          vars:
            sonic_interfaces:
              - name: Eth1/1/4
                access_vlan: 42

--- Disabling port access for VLAN 42 on interface eth1/1/4

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
            name: sonic_manage_vlan_access_mode
          vars:
            sonic_interfaces:
              - name: Eth1/1/4
                access_vlan: 42
            sonic_remove_port_access: true

License
-------

BSD

Author Information
------------------

Alessandro Rossi <alerossi@redhat.com>
Ahmed Gaber <agaber@redhat.com>
Thibaut Perrin <thibaut.perrin@dell.com>