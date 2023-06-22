# DELL - Red Hat | Virtual machines provisioning use cases

In this example, we retain the use cases to spin virtual machines and configure balanced webserver instances serving a static page.


## Virtual machine deploy and removal

Two templates are created based on *00_deploy_vms* and *00_destroy_vms* playbooks, that control the creation and the destruction of the involved virtual machines on the DEVOPS vSphere instance.

This will spin up three machines (2x webservers, 1x load balancer) that will be used through the demo

## Virtual machine registration and patching

There is one template based on the *01_registration_patching* playbook that will handle the required steps to configure the VMs to be attached to the Satellite instance running in the environment as well as the patching to the latest version of the installed packages.

## Users management

One template based on the *02_manage_users* will take care of creating a **devops** user and correctly set it up to be able to run commands with privileged access (sudo) on the machines.

## Message of the day (MOTD) manipulation

Another template based on *03_motd* will take care of setting up a customized message of the day in the VMs

## Webservers provisioning

The template using 04_provision_webservers playbook will take care of provisioning the following:

- httpd instance
- firewall rules
- static content

Both the instances will have customized content that will be made available to users.

## Load balancer provisioning

The last template, that will be using 05_provision_haproxy will be configuring the following:

- haproxy packages
- haproxy tailored configuration via template
- firewall rules

This instance will be responsible for serving content in round-robin fashion to test and prove that is correctly working.


## Use case variables - Group variables - virtual_machines

**vSphere-related variables - vsphere_vars**

|Variable| Description | Required | Default |
|--------|--|--|--|
| deploy_vsphere_host       | IP or Hostname of the vCenter/ESXi | :heavy_check_mark: | N/A |
| deploy_vsphere_user       | Username of the vCenter/ESXi | :heavy_check_mark: | N/A |
| deploy_vsphere_password   | Password of the vCenter/ESXi | :heavy_check_mark: | N/A |
| deploy_target             | Name of the vCenter Cluster if using vCenter or ESXi hostname if using ESXi | :heavy_check_mark: | N/A |
| deploy_vsphere_datacenter | Datacenter in vSphere | :heavy_check_mark: | N/A |
| deploy_vsphere_datastore  | Datastore to be used for the VMs | :heavy_check_mark: | N/A |
| deploy_vsphere_folder     | VM Folder to be used, with trailing slash  | :heavy_check_mark: | N/A |
| guest_dns_servers | List of DNS servers for the VMs | :heavy_check_mark: | N/A |
| guest_domain_name | VMs domain name | :heavy_check_mark: |  |

**Satellite variables for all hosts - satellite_vars**

These variables are used by all hosts for provisioning.

|Variable| Description | Required | Default |
|--------|--|--|--|
| satellite_host            | Satellite Hostname | :heavy_check_mark: | N/A |
| satellite_ip              | Needed to support name resolution in /etc/hosts | :x: | Empty |
| satellite_activation_key  | Activation key to be used for the guests | :heavy_check_mark: | N/A |
| satellite_org_id          | Satellite organization | :heavy_check_mark: | N/A |


**Variables file for guest OS groups - vm_guest_vars**

|Variable| Subelement | Description | Required | Default |
|--------|--|--|--|--|
|users| | List of users to add to the VM | :x: | N/A |
| - | name | Name of the user to create | :x: | devops |
|  | password | Password of the user to create | :x: | redhat |

## Use case variables - Host variables

Host variables are needed to customize the VMs in vSphere

|Variable| Subelements | Description | Required | Default |
|--------|--|--|--|--|
| guest_hostname | - | Hostname of the VM | :heavy_check_mark: | N/A |
| guest_memory   | - | Assigned RAM | :heavy_check_mark: | N/A |
| guest_vcpu     | - | Assigned CPUs | :heavy_check_mark: | N/A |
| guest_disksize | - | Assigned disk space | :heavy_check_mark: | N/A |
| guest_template | - | Name of the templated available on on vCenter | :heavy_check_mark: | N/A |
| guest_networks | - | Networks to be attached to the VM| :heavy_check_mark: | N/A |
| - | name            | Name of the network on vCenter | :heavy_check_mark: | N/A |
| - | ip              | Assigned IP | :heavy_check_mark: for static network only | N/A |
| - | netmask         | Netmask | :heavy_check_mark: for static network only | N/A |
| - | start_connected | Boolean to start the network in connected state | :heavy_check_mark: | N/A |
| - | type            | Network config type, static or dhcp | :heavy_check_mark: | N/A |
| - | connected       | Boolean to ensure the net is connected :heavy_check_mark: | N/A |
