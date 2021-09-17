Alibaba Cloud E-MapReduce Terraform Module  
terraform-alicloud-emr-zookeeper
=====================================================================

English | [简体中文](https://github.com/terraform-alicloud-modules/terraform-alicloud-emr-zookeeper/blob/master/README-CN.md)

Terraform module which creates emr cluster instance(s) which cluster type is zookeeper on Alibaba Cloud. 

These types of resources are supported:

* [Alicloud_emr_cluster](https://www.terraform.io/docs/providers/alicloud/r/emr_cluster.html)

# Terraform versions

This module requires Terraform 0.12 和 阿里云 Provider 1.71.0+.

Usage
-----

```hcl
data "alicloud_emr_main_versions" "default" {
  cluster_type = ["ZOOKEEPER"]
}

data "alicloud_vpcs" "default" {
  is_default = true
}

data "alicloud_vswitches" "all" {
  vpc_id = data.alicloud_vpcs.default.ids.0
}

module "security_group" {
  source  = "alibaba/security-group/alicloud"
  region  = "cn-hangzhou"
  profile = "Your-Profile-Name"
  vpc_id  = data.alicloud_vpcs.default.ids.0
  version = "~> 2.0"
}

module "emr-zookeeper" {
  source = "terraform-alicloud-modules/emr-zookeeper/alicloud"

  region  = "cn-hangzhou"
  profile = "Your-Profile-Name"

  emr_version = data.alicloud_emr_main_versions.default.main_versions.0.emr_version
  charge_type = "PostPaid"

  vswitch_id        = data.alicloud_vswitches.all.ids.0
  security_group_id = module.security_group.this_security_group_id
}
```

## Examples

* [emr-zookeeper example](https://github.com/terraform-alicloud-modules/terraform-alicloud-emr-zookeeper/tree/master/example)

## Notes

* This module using AccessKey and SecretKey are from `profile` and `shared_credentials_file`.
If you have not set them yet, please install [aliyun-cli](https://github.com/aliyun/aliyun-cli#installation) and configure it.

Submit Issues
-------------
If you have any problems when using this module, please opening a [provider issue](https://github.com/terraform-providers/terraform-provider-alicloud/issues/new) and let us know.

**Note:** There does not recommend to open an issue on this repo.

Authors
-------
Created and maintained by Alibaba Cloud Terraform Team(terraform@alibabacloud.com).

License
----
Apache 2 Licensed. See LICENSE for full details.

Reference
---------
* [Terraform-Provider-Alicloud Github](https://github.com/terraform-providers/terraform-provider-alicloud)
* [Terraform-Provider-Alicloud Release](https://releases.hashicorp.com/terraform-provider-alicloud/)
* [Terraform-Provider-Alicloud Docs](https://www.terraform.io/docs/providers/alicloud/index.html)