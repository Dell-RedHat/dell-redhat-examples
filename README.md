# DELL - Red Hat | Bare metal provisioning use cases

In this example, we retain the use cases to provision bare metal servers with RHEL and ESXi.
**The use cases require an NFS share to be present.**

## Prepare ISO to deploy RHEL/ESXi OS on Bare Metal

The playbooks *bm_00_preset_esxi* and *bm_00_preset_os* prepare a RHEL/ESXi ISO image with a kickstart file that provide the necessary information to automatically deploy the OS.
The original iso image should be in an accessible NFS Server, referenced in the appropriate variables.

## Deploy ISO to iDRAC

The playbooks *bm_01_deploy_os.yml* and *bm_01_deploy_esxi.yml* deploy the previously build ISO to iDRAC. Refer to the role documentation for details.

## Virtual machine registration and patching
There is one template based on the *02_registration_patching* playbook that will handle the required steps to configure the VMs to be attached to the Satellite instance running in the environment as well as the patching to the latest version of the installed packages.

## Users management
One template based on the *03_manage_users* will take care of creating a devops user and correctly set it up to be able to run commands with privileged access (sudo) on the machines.

## Message of the day (MOTD) manipulation
Another template based on *04_motd* will take care of setting up a customized message of the day in the VMs

## Webservers provisioning
The template using *05_provision_webservers* playbook will take care of provisioning the following:

httpd instance
firewall rules
static content

Both the instances will have customized content that will be made available to users.

## Use case variables - Group variables - baremetal_hosts

| Variable | Description | Required | Default |
| -- | -- | -- | -- |
| idrac_ip              | IP of the iDRAC - Defaults to ansible_host | :x: | ansible_host |
| idrac_username        | Username for the iDRAC - Defaults to ansible_username | :x: | ansible_user |
| idrac_password        | Password for the iDRAC - Defaults to ansible_password | :x: | ansible_password |
| idrac_validate_certs  | Boolean for certificate validation - Defaults to false | :x: | false |
| idrac_ca_path         | Path to the CA PEM to verify certs | :heavy_check_mark: if *validate_certs* is **true** | N/A |
| idrac_expose_duration | Exposure time for the ISO before being detached by the host | :x: | 300 |


## Use case variables - Group variables - Common vars - environment

| Variable | Description | Required | Default |
| -- | -- | -- | -- |
| idrac_nfs_host        | Hostname or IP of the NFS/CIFS share | :heavy_check_mark: | N/A |
| idrac_nfs_share       | Path of the NFS/CIFS share | :heavy_check_mark: | N/A |
| rhel_iso              | ISO filename for RHEL setup, presente under *idrac_nfs_share* folder | :heavy_check_mark: | N/A |
| esxi_iso              | ISO filename for ESXi setup, presente under *idrac_nfs_share* folder | :heavy_check_mark: | N/A |
| satellite_host            | Satellite Hostname | :heavy_check_mark: | N/A |
| satellite_ip              | Needed to support name resolution in /etc/hosts | :x: | Empty |
| satellite_activation_key  | Activation key to be used for the guests | :heavy_check_mark: | N/A |
| satellite_org_id          | Satellite organization | :heavy_check_mark: | N/A |
## Use case variables - Host vars - Variables file for each baremetal host, can override group_vars

| Variable | Subelements | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- | -- |
| idrac_nfs_host        | - | Hostname or IP of the NFS/CIFS share | :heavy_check_mark: | N/A | |
| idrac_nfs_share       | - | Path of the NFS/CIFS share | :heavy_check_mark: | N/A | |
| idrac_ip              | - | IP of the iDRAC - Defaults to ansible_host | :x: | ansible_host | |
| idrac_username        | - | Username for the iDRAC - Defaults to ansible_username | :x: | ansible_user | |
| idrac_password        | - | Password for the iDRAC - Defaults to ansible_password | :x: | ansible_password | |
| idrac_validate_certs  | - | Boolean for certificate validation - Defaults to false | :x: | false | |
| idrac_ca_path         | - | Path to the CA PEM to verify certs | :x: | N/A | Mandatory if *validate_certs* is **true** |
| idrac_expose_duration | - | Exposure time for the ISO before being detached by the host | :x: | 300 | |
| rhel_iso              | - | ISO filename for RHEL setup, presente under *idrac_nfs_share* folder| :heavy_check_mark: | N/A | |
| esxi_iso              | - | ISO filename for ESXi setup, presente under *idrac_nfs_share* folder| :heavy_check_mark: | N/A |  |
| ks_lang                 | - | System language                                 | :x: | en_US | |
| ks_keyboard             | - | Keyboard layout                                 | :x: | us | |
| ks_timezone             | - | Timezone                                        | :x: | Europe/Amsterdam | |
| ks_rootpw               | - | Plaintext password for the root user            | :x: | redhat | |
| ks_disk                 | - | Block device to be used for the installation    | :x: | sda | |
| ks_hostname             | - | Guest hostname                                  | :x: | N/A | Mandatory if primary interfaces is static |
| interfaces              | - | List of configured interfaces                   | :heavy_check_mark: | N/A |
| - | network_device    | Device name                                     | :heavy_check_mark: | N/A | |
|| ip                | IP of the interface                             | :x: | N/A | If set, other fields are mandatory for static configuration. If not set, DHCP will be used
|| netmask           | Netmask of the interface                        | :x: | N/A | Mandatory if *ip* is static
|| gateway           | Gateway for the interface                       | :x: | N/A | Mandatory if *ip* is static
|| nameserver        | Nameserver for the interface                    | :x: | N/A | Mandatory if *ip* is static
|| primary           | Boolean to check if interace is primary         | :x: | N/A | Mandatory if *ip* is static. If true, *ks_hostname* must be set
|| vlanid            | Vlan ID for the device                          | :x: | N/A | Mandatory if *ip* is static
