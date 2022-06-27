---
# generated by https://github.com/hashicorp/terraform-plugin-docs
page_title: "k0s_cluster Resource - terraform-provider-k0s"
subcategory: ""
description: |-
  Manages a k0s cluster.
---

# k0s_cluster (Resource)

Manages a k0s cluster.

## Example Usage

```terraform
resource "k0s_cluster" "example" {
  name    = "example"
  version = "1.23.8+k0s.0"

  hosts = [
    {
      role = "controller"

      ssh = {
        address  = "10.0.0.1"
        port     = 22
        user     = "root"
        key_path = "~/.ssh/id_ed25519.pub"
      }
    },
    {
      role = "worker"

      ssh = {
        address  = "10.0.0.2"
        port     = 22
        user     = "root"
        key_path = "~/.ssh/id_ed25519.pub"
      }
    }
  ]
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `hosts` (Attributes Set) Hosts configuration. (see [below for nested schema](#nestedatt--hosts))
- `name` (String) Name of the cluster.
- `version` (String) Desired k0s version.

### Read-Only

- `id` (String) Unique ID of the cluster.
- `kubeconfig` (String, Sensitive) Admin kubeconfig of the cluster.

<a id="nestedatt--hosts"></a>
### Nested Schema for `hosts`

Required:

- `hostname` (String) Override host's hostname. When not set, the hostname reported by the operating system is used.
- `no_taints` (Boolean) When `true` and used in conjuction with the `controller+worker` role, the default taints are disabled making regular workloads schedulable on the node. By default, k0s sets a node-role.kubernetes.io/master:NoSchedule taint on `controller+worker` nodes and only workloads with toleration for it will be scheduled.
- `role` (String) Role of the host. One of `controller`, `controller+worker`, `single`, `worker`.
- `ssh` (Attributes) SSH connection options. (see [below for nested schema](#nestedatt--hosts--ssh))

<a id="nestedatt--hosts--ssh"></a>
### Nested Schema for `hosts.ssh`

Required:

- `address` (String) IP address of the host.
- `key_path` (String) Path to an SSH private key file.
- `port` (Number) TCP port of the SSH service on the host.
- `user` (String) Username to log in as.

