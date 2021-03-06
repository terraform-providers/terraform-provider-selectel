---
layout: "selectel"
page_title: "Selectel: selectel_mks_cluster_v1"
sidebar_current: "docs-selectel-resource-mks-cluster-v1"
description: |-
  Manages a V1 cluster resource within Selectel Managed Kubernetes Service.
---

# selectel\_mks\_cluster\_v1

Manages a V1 cluster resource within Selectel Managed Kubernetes Service.

## Example usage

```hcl
resource "selectel_vpc_project_v2" "project_1" {
  auto_quotas = true
}

resource "selectel_mks_cluster_v1" "cluster_1" {
  name         = "cluster-1"
  project_id   = "${selectel_vpc_project_v2.project_1.id}"
  region       = "ru-3"
  kube_version = "1.16.8"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) The name of the cluster.
  Changing this creates a new cluster.

* `project_id` - (Required) An associated Selectel VPC project.
  Changing this creates a new cluster.

* `region` - (Required) A Selectel VPC region of where the cluster is located.
  Changing this creates a new cluster.

* `kube_version` - (Required) The current Kubernetes version of the cluster.
  Changing this upgrades the current version of the cluster.
  To upgrade a patch version, the desired version should match the latest available patch version for
  the current minor release.
  To upgrade a minor version, the desired version should match the next available minor release with
  the latest patch version.

* `enable_autorepair` - (Optional) Reflects if worker nodes are allowed to be reinstalled automatically.
  Accepts true or false. Defaults to true.

* `enable_patch_version_auto_upgrade` - (Optional) Specifies if Kubernetes patch version of the cluster
  is allowed to be upgraded automatically.
  Accepts true or false. Defaults to true.

* `network_id` - (Optional) An associated OpenStack Networking service network ID.
  Changing this creates a new cluster.

* `subnet_id` - (Optional) associated OpenStack Networking service subnet ID.
  Changing this creates a new cluster.

* `maintenance_window_start` - (Optional) Represents UTC time in "hh:mm:ss" format of when the cluster
   will start its maintenance tasks.
   Changing this updates maintenance window start time.

## Attributes Reference

The following attributes are exported:

* `maintenance_window_end` - Shows UTC time in "hh:mm:ss" format of when the cluster
   will end its maintenance tasks.

* `kube_api_ip` - Shows the IP of the Kubernetes API.

* `status` - Shows the current status of the cluster.

## Import

Cluster can be imported using the `id`, e.g.

```shell
$ env SEL_TOKEN=SELECTEL_API_TOKEN SEL_PROJECT_ID=SELECTEL_VPC_PROJECT_ID SEL_REGION=SELECTEL_VPC_REGION terraform import selectel_mks_cluster_v1.cluster_1 b311ce58-2658-46b5-b733-7a0f418703f2
```
