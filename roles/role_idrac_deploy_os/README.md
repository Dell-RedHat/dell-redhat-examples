Deploy OS
=========

Deploy an OS from a iso file on IDrac Dell baremetal servers.


Requirements
------------

This role is part of the dellemc.openmanage collection ( version 5.4.0 )

To install it, use: `ansible-galaxy collection install dellemc.openmanage`.


Role Variables
--------------

```
idrac_nfs_host: '' # Hostname or IP of the NFS/CIFS share
idrac_nfs_share: '' # Path of the NFS/CIFS share
idrac_deploy_iso: '' # ISO file name to be deployed
#### Optional ####
idrac_ip: '' # IP of the iDRAC - Defaults to ansible_host
idrac_username: '' # Username for the iDRAC - Defaults to ansible_username
idrac_password: '' # Password for the iDRAC - Defaults to ansible_password
idrac_validate_certs: '' # Boolean for certificate validation - Defaults to false
idrac_ca_path: '' # Path to the CA PEM to verify certs - Mandatory if validate_certs is true
idrac_expose_duration: 300 # Exposure time for the ISO before being detached by the host - Defaults to 300

```

Dependencies
------------

You need to create an iso file with kickstarter ks.cfg https://access.redhat.com/solutions/60959 in order to automatically do a deployment.

you can use the playbook named bm_00_preset_os.yml to prepare iso file

License
-------

BSD
