## Load Balancer

This module manages a load balancer (opentelekomcloud_lb_loadbalancer_v2). The public IP is an output.

Example:

```hcl
module "vpc" {
  source     = "iits-consulting/vpc/opentelekomcloud"
  name       = "${var.context}-${var.stage}-vpc"
  cidr_block = var.vpc_cidr
  subnets = {
    "my-subnet" = cidrsubnet(var.vpc_cidr, 1, 0)
  }
  tags = local.tags
}

module "loadbalancer" {
  source               = "iits-consulting/loadbalancer/opentelekomcloud"
  context_name = var.context
  subnet_id    = module.vpc.subnets["my-subnet"].subnet_id
}
```

<!-- BEGIN_TF_DOCS -->

## Requirements

| Name                                                                                          | Version  |
| --------------------------------------------------------------------------------------------- | -------- |
| <a name="requirement_opentelekomcloud"></a> [opentelekomcloud](#requirement_opentelekomcloud) | >=1.31.5 |

## Providers

| Name                                                                                    | Version  |
| --------------------------------------------------------------------------------------- | -------- |
| <a name="provider_opentelekomcloud"></a> [opentelekomcloud](#provider_opentelekomcloud) | >=1.31.5 |

## Modules

No modules.

## Resources

| Name                                                                                                                                                          | Type     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| [opentelekomcloud_lb_loadbalancer_v2.elb](https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs/resources/lb_loadbalancer_v2) | resource |
| [opentelekomcloud_vpc_eip_v1.ingress_eip](https://registry.terraform.io/providers/opentelekomcloud/opentelekomcloud/latest/docs/resources/vpc_eip_v1)         | resource |

## Inputs

| Name                                                                  | Description                                                                                                           | Type     | Default | Required |
| --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | ------- | :------: |
| <a name="input_context_name"></a> [context_name](#input_context_name) | Short descriptive, readable label of the project you are working on. Is utilized as a part of resource names.         | `string` | n/a     |   yes    |
| <a name="input_subnet_id"></a> [subnet_id](#input_subnet_id)          | Subnet where the elastic load balancer will be created.                                                               | `string` | n/a     |   yes    |
| <a name="input_bandwidth"></a> [bandwidth](#input_bandwidth)          | The bandwidth size. The value ranges from 1 to 1000 Mbit/s.                                                           | `number` | `300`   |    no    |
| <a name="input_stage_name"></a> [stage_name](#input_stage_name)       | Utilized to distinguish separate, but mostly equal environments within the same project. Usually dev, test, qa, prod. | `string` | `"dev"` |    no    |

## Outputs

| Name                                                                          | Description |
| ----------------------------------------------------------------------------- | ----------- |
| <a name="output_elb_id"></a> [elb_id](#output_elb_id)                         | n/a         |
| <a name="output_elb_private_ip"></a> [elb_private_ip](#output_elb_private_ip) | n/a         |
| <a name="output_elb_public_ip"></a> [elb_public_ip](#output_elb_public_ip)    | n/a         |

<!-- END_TF_DOCS -->
