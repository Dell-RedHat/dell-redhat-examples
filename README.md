# DELL - Red Hat | Openshift provisioning

In this example, we retain the use cases to provision bare metal servers with RHEL and ESXi.

**The use cases require an NFS server.**

## Prepare ISO to deploy Single Node Openshift

The playbook *sno_00_pre_install_openshift* prepares an ISO image with the baremetal installer for deploying Single Node Openshift (SNO) on a Bare Metal host

## Deploy SNO ISO to iDRAC

The playbook *sno_01_deploy_openshift.yml* deploys the previously built ISO on a Bare Metal host to start OCP setup

## Check OCP Deploy

The playbook *sno_02_ocp_deploy_check.yml* verifies the OCP setup progress

## Enable Powerflex-backed Storage in OCP using CSI Drivers

The playbook *sno_03_add_powerflex_storage.yml* takes care of setting up the DELL CSI Operator to provide connectivity to an existing PowerFlex storage cluster to allow dynamic provisionig of storage inside the cluster

## Deploy a test container in OCP with storage

The playbook *sno_04_deploy_test_container* deploys a simple container in OCP, which attaches dynamic storage provisioned via the DELL CSI Storage Class.


## Use case variables - Group variables - baremetal_hosts

| Variable | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- |
| idrac_ip              | IP of the iDRAC - Defaults to ansible_host | :x: | ansible_host |
| idrac_username        | Username for the iDRAC - Defaults to ansible_username | :x: | ansible_user |
| idrac_password        | Password for the iDRAC - Defaults to ansible_password | :x: | ansible_password |
| idrac_validate_certs  | Boolean for certificate validation - Defaults to false | :x: | false |
| idrac_ca_path         | Path to the CA PEM to verify certs - Mandatory if validate_certs is true | :heavy_check_mark: if *validate_certs* is **true** | N/A |
| idrac_expose_duration | Exposure time for the ISO before being detached by the host | :x: | 300 |

## Use case variables - Group variables - environment

### common_vars

| Variable | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- |
| idrac_nfs_host        | Hostname or IP of the NFS/CIFS share | :heavy_check_mark: | N/A |
| idrac_nfs_share       | Path of the NFS/CIFS share | :heavy_check_mark: | N/A |

### ocp_vars

| Variable | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- |
| ocp_workdir | Folder name to store OCP related files into | :x: | *openshift* |
| ocp_pull_secret | Pull secret needed for downloading OCP Images | :heavy_check_mark: | N/A | | Can be retrieved here https://console.redhat.com/openshift/install/pull-secret |
| ocp_coreos_ssh_key | Public key of the core user on the Single Node Host | :heavy_check_mark: | N/A | Needed for SSH access in case of troubleshooting during setup
| ocp_version                 | OCP version to install | :x: | stable-4.11 | Versions are available here https://mirror.openshift.com/pub/openshift-v4/clients/ocp/
| ocp_arch                    | OCP Architecture | :x: | x86_64 |
| ocp_admin_username:         | OCP admin username | :x: | kubeadmin |
| ocp_admin_password:         | OCP admin password | :x: | N/A | If not provided will be fetched by the installer
| ocp_api_url                 | API URL to interact with OCP cluster | :x: | https://api.{{ ocp_cluster_name }}.{{ ocp_cluster_domain }}:6443 |
### powerflex_vars

| Variable | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- |
| powerflex_mdm_ip            | List of ip address(es) for the management device | :heavy_check_mark: | N/A |
| powerflex_namespace         | name of the namespace to be used for testing powerflex storage access in OpenShift | :heavy_check_mark: | defaults to *powerflex* |
| powerflex_system_id         | System ID of the powerflex cluster. get this from the powerflex SDS  | :heavy_check_mark: | N/A |
| powerflex_storagepool       | Name of storage pool to use on the Powerflex SDS  | :heavy_check_mark: | N/A |
| powerflex_protectiondomain  | Name of protection domain on the Powerflex SDS  | :heavy_check_mark: | N/A |
| powerflex_username          | the username account to be used to logon onto the Powerflex API Gateway   | :heavy_check_mark: | N/A |
| powerflex_password          | Password for the username account to be used to logon onto the Powerflex API Gateway  | :heavy_check_mark: | N/A |
| powerflex_endpoint          | Specify the IP address(s) of the Powerflex API Gateway | :heavy_check_mark: | N/A |


## Use case variables - Host vars - Variables file for each baremetal host, can override group_vars

The following variables are specific for each Single Node Openshift

| Variable | Description | Required | Default | Notes |
| -- | -- | -- | -- | -- |
| ocp_cluster_name | Name of the OCP Cluster | :heavy_check_mark: | N/A |
| ocp_cluster_domain | Domain of the OCP Cluster | :heavy_check_mark: | N/A |
| ocp_setup_device | iDRAC clean block device to install OCP | :x: | /dev/sda |
