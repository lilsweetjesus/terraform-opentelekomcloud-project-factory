# Common Terraform Modules for Open Telekom Cloud

[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](hhttps://github.com/iits-consulting/terraform-opentelekomcloud-project-factory/blob/main/LICENSE)
![Terraform Lint](https://github.com/iits-consulting/terraform-opentelekomcloud-project-factory/workflows/terraform-lint/badge.svg)
![ViewCount](https://views.whatilearened.today/views/github/iits-consulting/terraform-opentelekomcloud-project-factory.svg)

These are commonly usable Terraform Modules for the [Open Telekom Cloud](https://open-telekom-cloud.com) based on the
awesome [Terraform OTC Provider](https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs).

*These modules are developed by [iits-consulting](https://iits-consulting.de/) - your Cloud-Native Innovation Teams as a
Service!*

## Usage:

You can import this whole repo as one module (quickstart) or utilize the modules individually (recommended for production).

## Quickstart

1. We recommend this kind of terraform folder structure:
   
   ![terraform-architecture](docs/terraform-architecture.png?raw=true "Title")
   
2. (optional) [Set up a secure remote terraform state](https://github.com/iits-consulting/terraform-opentelekomcloud-obs-tf-state).
   Copy the backend output of that module to your settings.tf
2. Add the project factory module

```terraform
# System variables that have to be set for this example environment:
# - OS_ACCESS_KEY
# - OS_SECRET_KEY
# - OS_DOMAIN_NAME
# - OS_TENANT_NAME or OS_PROJECT_NAME

module "iits-otc-demo" {
  source  = "iits/project-factory/opentelekomcloud"
  version = "1.0.0"
  ...
}
```

## Importing Modules Individually

```terraform
module "vpc" {
  source                = "iits/project-factory/opentelekomcloud//modules/vpc"
  version               = "1.0.0"
  vpc_cidr              = local.vpc_cidr
  vpc_name              = "vpc-otc-demo-dev"
  stage_name            = "dev"
  vpc_subnet_cidr       = local.vpc_cidr
  vpc_subnet_gateway_ip = local.vpc_subnet_gateway_ip
}
```

# Common Concepts behind the modules

There are some variables that occur on multiple modules. The ideas behind them are explained here.

## Context

The "context_name" variable should be a human-readable name of the project you are working on or the team you are
provisioning infrastructure for.

## Stage

The "stage" variable is utilized to distinguish between multiple mostly equal, but separate environments like "dev", "
test", "qa", "prod".
