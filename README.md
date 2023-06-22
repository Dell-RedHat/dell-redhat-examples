# DELL - Red Hat | OME use cases

In this example, we will orchestrate some of the OME features around an existing environment

## Provide credentials for Server-initiated discovery

The playbook *01-ome-discovery.yml* is used to provide credentials for iDRACs that will be discovered using the server-initiated discovery that needs to be setup initially using the following procedure: https://www.dell.com/support/manuals/en-us/dell-openmanage-enterprise/ome_p_310_users_guide_drop2/server-initiated-discovery?guid=guid-23bd252f-9651-410a-88de-3f332d748b55&lang=en-us

## Remediate config compliance baselines

The playbooks *02-Compliance-Auto.yml* and *02-Compliance-RAC Name.yml* are used to remediate an existing baseline in OME that has the appropriate name.

They can be modified to be used with a Survey to request the Baseline to remediate.

Both the instances will have customized content that will be made available to users.

## Use case variables - Group variables - ome

| Variable | Description | Required | Default |
| -- | -- | -- | -- |
| ome_user              | Username for the OME instance - Defaults to the OME credential ome_user | :x: | ome_credential value |
| idrac_password        | Password for the iDRAC - Defaults to ansible_password | :x: | ansible_password |
| idrac_validate_certs  | Boolean for certificate validation - Defaults to false | :x: | false |
| idrac_ca_path         | Path to the CA PEM to verify certs | :heavy_check_mark: if *validate_certs* is **true** | N/A |
| idrac_expose_duration | Exposure time for the ISO before being detached by the host | :x: | 300 |


