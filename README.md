# Image Registry terraform module

Terraform module to set up the cluster to use an external image registry for CI pipelines. The module creates
the configmap and secret in the provided namespace and creates the ConsoleLink on ocp 4.x.

## Software dependencies

The module depends on the following software components:

### Command-line tools

- terraform - v12
- kubectl

### Terraform providers

- Helm provider >= 1.1.1 (provided by Terraform)

## Module dependencies

This module makes use of the output from other modules:

- Cluster - github.com/ibm-garage-cloud/terraform-ibm-container-platform.git
- Namespace - github.com/ibm-garage-cloud/terraform-cluster-namespace.git

## Example usage

```hcl-terraform
module "registry" {
  source = "github.com/ibm-garage-cloud/terraform-k8s-image-registry"

  config_file_path = module.dev_cluster.config_file_path
  registry_namespace = "ibmgaragecloud"
  registry_host = "docker.io"
  registry_url = "https://hub.docker.com/o/ibmgaragecloud"
  registry_user = "me"
  registry_password = "password"
  cluster_namespace = module.dev_capture_tools_state.namespace
}
```
