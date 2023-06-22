# DELL - Red Hat | PowerFlex automation use cases

This branch of the repository shows automation use cases for Dell PowerFlex storage servers.

## Remove Storage Data Client (SDC) from ESXi/RHEL hosts

The playbooks *sto_00_wipe_sdc_esxi* and *sto_00_wipe_sdc_* will support the removal of the SDC component in an ESXi/RHEL setup, taking care of package removal, volume removal and cleanup of records in the Management Console.

## Remove PowerFlex volumes from ESXi

The playbook *sto_00_wipe_vols_esxi.yml* allows you to remove a VMFS datastore in ESXi backed by PowerFlex and wipe the associated volumes.

## Configure PowerFlex based storage on ESXi/RHEL

The playbooks *sto_01_setup_esxi.yml* and *sto_01_setup_rhel.yml* take care of all necessary steps required on ESXi (using esxcli) and RHEL to configure required packages and settings to prepare the hosts to attach and use PowerFlex backed storage.

## PowerFlex volume creation and mapping on ESXi

The playbook *sto_02_create_map_volume_esxi.yml* will create volumes on PowerFlex and map them to a datastore created in ESXi.


## Use case variables - Group variables - Common variables - all

| Variable | Description | Required | Default |
| -- | -- | -- | -- |
| MDM_IP | IP Of the MetaData Manager | :heavy_check_mark: | N/A |
| FLEX_MGMT_IP | IP of Powerflex management | :heavy_check_mark: | N/A |
| FLEX_MGMT_USER | Powerflex Management username | :heavy_check_mark: | N/A |
| FLEX_MGMT_PASS | Powerflex Management password | :heavy_check_mark: | N/A |
| FLEX_MGMT_PORT | Powerflex Management port | :heavy_check_mark: | N/A |
| sdc_hostname:  | SDC Hostname | :heavy_check_mark: | N/A |
| vol_name | Volume name | :heavy_check_mark: | N/A |
| vol_size | Volume size, it needs to be a multiple of 8GB | :heavy_check_mark: | N/A |
| vol_pool | Volume pool | :heavy_check_mark: | N/A |
| vol_pd | Volume Protection domain | :heavy_check_mark: | N/A |
| powerflex_subnet | IP Subnet Powerflex belongs to | :heavy_check_mark: | N/A |

## Use case variables - Group variables - ESXi variables

| Variable | Subelement | Description | Required | Default |
| -- | -- | -- | -- | -- |
| vcenter_hostname | | vCenter hostname/IP | :heavy_check_mark: | N/A |
| vcenter_username | | vCenter admin username | :heavy_check_mark: | N/A |
| vcenter_password | | vCenter admin password | :heavy_check_mark: | N/A |
| ansible_ssh_user | | ESXI root user | :heavy_check_mark: | N/A |
| volumes_esxi | | List of volumes to define on ESXI | :heavy_check_mark: | N/A |
| - | vol_name | Volume name  | :heavy_check_mark: | N/A |
|   | vol_size | Volume size | :heavy_check_mark: | N/A |
|   | vol_pool | Volume pool | :heavy_check_mark: | N/A |
|   | vol_pd | Volume Protection Domain | :heavy_check_mark: | N/A |
