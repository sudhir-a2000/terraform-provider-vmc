---
layout: "vmc"

page_title: "VMC: vmc_public_ip"
sidebar_current: "docs-vmc-resource-public-ip"

description: |-
  Provides a resource to manage public IPs.
---

# vmc_public_ip

Provides a resource to manage public IPs.
~> **Note:** Public IP resource implicitly depends on SDDC resource creation. SDDC must be provisioned before a public IP can be created. For details on how to provision a SDDC refer to [vmc_sddc](https://www.terraform.io/docs/providers/vmc/r/sddc.html).

## Example Usage

```hcl

provider "vmc" {
  refresh_token = var.api_token
  org_id = var.org_id
}

resource "vmc_public_ip" "public_ip_1" {
  nsxt_reverse_proxy_url = vmc_sddc.sddc_1.nsxt_reverse_proxy_url
  display_name = var.public_ip_displayname
}

```

## Argument Reference

The following arguments are supported for vmc_public_ip resource:

* `nsxt_reverse_proxy_url` - (Required) NSXT reverse proxy url for managing public IP. Computed after SDDC creation.

* `display_name` - (Optional) Display name for public IP.

## Attributes Reference

In addition to arguments listed above, the following attributes are exported after public IP creation:

* `id` - Public IP identifier.

* `ip` - Public IP.

* `display_name` - Display name for public IP.

## Import

Public IP resource can be imported using the `nsxt_reverse_proxy_url` and `id` , e.g.

`$ terraform import vmc_public_ip.public_ip_1 nsxt_reverse_proxy_url,id`

- nsxt_reverse_proxy_url = NSX API public endpoint url used for public IP resource management
- id = Public IP Identifier

`$ terraform import vmc_public_ip.public_ip_1 'https://nsx-44-228-76-55.rp.vmwarevmc.com/vmc/reverse-proxy/api/orgs/{orgI}/sddcs/afe7a0fd-3f0a-48b2-9ddb-0489c22732ae/sks-nsxt-manager,8d730ad4-aa6b-4f9f-9679-ec17beeaceaf'
`

