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
idrac:
  nfs_host: '' # Hostname or IP of the NFS/CIFS share
  nfs_share: '' # Path of the NFS/CIFS share
  deploy_iso: '' # ISO file name to be deployed
#### Optional ####
  ip: '' # IP of the iDRAC - Defaults to ansible_host
  username: '' # Username for the iDRAC - Defaults to ansible_username
  password: '' # Password for the iDRAC - Defaults to ansible_password
  validate_certs: '' # Boolean for certificate validation - Defaults to false
  ca_path: '' # Path to the CA PEM to verify certs - Mandatory if validate_certs is true
  expose_duration: 300 # Exposure time for the ISO before being detached by the host - Defaults to 300

```

Dependencies
------------

You need to create an iso file with kickstarter ks.cfg https://access.redhat.com/solutions/60959 in order to automatically do a deployment.

you can use the playbook named bm_00_preset_os.yml to prepare iso file

License
-------

BSD
