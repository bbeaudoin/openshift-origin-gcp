# OpenShift on Google Compute Platform (GCP)

This set of Jinja templates and YAML configuration files may be used to provision OpenShift on GCP.

## Requirements
1. Pre-configured images loaded in the project
1. To use the DNS functionality, the DNS zone added to the project
1. Appropriate privilege
1. API access enabled for dns runtimeconfig

## Basic Operation
After cloning the repository, edit `deployment-manager/jinja/openshift-origin.yaml` to set the dns_name (zone) and other parameters for instance sizing, disks, and other parameters as required. Ensure the disk types and other parameters fit within your project's quota.

Please see this page for quota information: https://cloud.google.com/compute/quotas

### Creating a deployment
```sh
gcloud deployment-manager deployments create openshift-origin --config=openshift-origin.yaml
```

### Deleting a deployment
```sh
gcloud deployment-manager deployments delete openshift-origin
```

## Composite Templates (beta)
To create a composite type using the beta API:
```sh
gcloud beta deployment-manager types create openshift-origin --template=jinja/openshift-origin.jinja
```

For more information, please see https://cloud.google.com/deployment-manager/docs/configuration/templates/create-composite-types.

## Permissions Used
Should it be required to limit access, it is recommended that Stackdriver logging be referenced for the list of permissions used. By default, an account administrator has the required privileges.

These permissions may include, but not necessarily be limited to, the following:

* iam.serviceAccountUser
* compute.admin
* deploymentmanager.editor
* storage.admin
* dns.admin

During deployment using the template here, the following permissions were used:

* compute.addresses.create
* compute.addresses.delete
* compute.autoscalers.create
* compute.autoscalers.delete
* compute.backendServices.create
* compute.backendServices.delete
* compute.backendServices.use
* compute.disks.create
* compute.disks.delete
* compute.disks.setLabels
* compute.firewalls.create
* compute.firewalls.delete
* compute.healthChecks.create
* compute.healthChecks.delete
* compute.instanceGroupManagers.create
* compute.instanceGroupManagers.delete
* compute.instanceGroupManagers.update
* compute.instanceGroupManagers.use
* compute.instanceGroups.create
* compute.instanceGroups.delete
* compute.instanceGroups.update
* compute.instanceTemplates.create
* compute.instanceTemplates.delete
* compute.instances.create
* compute.instances.delete
* compute.instances.setLabels
* compute.instances.setMetadata
* compute.instances.setServiceAccount
* compute.instances.setTags
* compute.instances.use
* compute.networks.create
* compute.networks.delete
* compute.networks.updatePolicy
* compute.sslCertificates.create
* compute.subnetworks.use
* compute.subnetworks.useExternalIp
* compute.targetSslProxies.create
* compute.targetSslProxies.delete
* deploymentmanager.deployments.create
* deploymentmanager.deployments.delete
* deploymentmanager.deployments.update
* dns.managedZones.create
* dns.managedZones.delete
* logging.sinks.create
* monitoring.groups.create
* storage.buckets.create
* storage.buckets.delete
