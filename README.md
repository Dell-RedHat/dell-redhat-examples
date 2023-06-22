# DELL - Red Hat | Ansible network automation use cases

This branch of the repository shows ansible network automation use cases for Dell switches to backup/restore switch configurations, create/delete vlans, set access vlan on a switch-port and to set allowed vlans on switch-ports.

Ansible Automation Platform 2, Automation Hub with dell sonic collections in execution environments  are used in this demo.

## Backup and/or Restore Dell switch configuration

Two templates are created based on *net_01_switch_config_backup.yml* and *net_01_config_restore.yml* playbooks, that perform configuration backup and configuration restore, respectively, on the Dell z9100 switches on the network.

The resulting switch backup files will have the following naming naming convention i.e. <switch_name>_config. The backup file is copied to and stored at a network hosts other than the switch. The restore will reference the backup file to restore the switch configuration.

## Create/Delete vlan

Two templates are created based on *net_03_vlan_create.yml* and *net_03_vlan_delete.yml* playbooks, that perform vlan creation and vlan deletion, respectively, on the Dell z9100 switches on the network.

## Setting/Unsetting Vlan Access on a switchport

Two templates are created based on *net_04_set_port_access_vlan.yml* and *net_04_unset_port_access_vlan.yml* playbooks, that set a ports vlan in access when in access mode and vice versa, respectively, on the Dell z9100 switches on the network.

## Setting/Unsetting Allowed Vlans on a switch-port

Two templates are created based on *net_05_set_port_trunk_allowed_vlans.yml* and *net_05_unset_port_trunk_allowed_vlans.yml* playbooks, that set a ports allowed vlan(s) when in trunk mode mode and removes a named vlan id from the switch-port's allowed vlan(s) list, respectively, on the Dell z9100 switches on the network.

## Port-Channel and MCLag configuration

A playbook net_02_config_mclag_z9100_01_02.yml performs port-channel creation, port-channel configuration and Dell mclag configuration on the Dell z9100-01 and z9100-02 switches.


## Use case variables - Group variables - dell_switches

| Variable | Description | Required | Default |
| -- | -- | -- | -- |
| sonic_backup_path        | Backup folder on the DELL switch | :x: | */opt/sonic-backups* |
| sonic_backup_archive_filename       | Filename for the backup archive | :x: | {{ inventory_hostname }}_config |

## Use case variables - Host variables - sonic_interfaces

| Variable | Subelement | Description | Required |
| -- | -- | -- | -- |
| sonic_interfaces | | Interface definition | :heavy_check_mark: |
| - | name | Interface name | :heavy_check_mark: |
| | access_vlan | VLAN to be configured in access mode | :heavy_check_mark: |
| | allowed_vlans | List of LANS to be configured in trunk mode | :heavy_check_mark: |
| | unallowed_vlans | List of LANS to be removed in trunk mode | :heavy_check_mark: |

## Use case variables - Host variables - sonic_vlans

| Variable | Subelement | Description | Required |
| -- | -- | -- | -- |
| sonic_vlans | | VLAN definition | :heavy_check_mark: |
| - | vlan_id | Id of the VLAN to be created/deleted | :heavy_check_mark: |
| | deletable | Safety check to prevent deletion of crucial VLANs | :heavy_check_mark: |
