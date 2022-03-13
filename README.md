# terraform-aws-orc8r

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 2.6.0 |
| <a name="requirement_kubernetes"></a> [kubernetes](#requirement\_kubernetes) | ~> 1.11.1 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 2.1 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 2.1 |
| <a name="requirement_tls"></a> [tls](#requirement\_tls) | ~> 2.1 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 2.6.0 |
| <a name="provider_random"></a> [random](#provider\_random) | ~> 2.1 ~> 2.1 |
| <a name="provider_tls"></a> [tls](#provider\_tls) | ~> 2.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_eks"></a> [eks](#module\_eks) | terraform-aws-modules/eks/aws | ~> 17.0.3 |
| <a name="module_vpc"></a> [vpc](#module\_vpc) | terraform-aws-modules/vpc/aws | ~> 2.17.0 |

## Resources

| Name | Type |
|------|------|
| [aws_db_event_subscription.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_event_subscription) | resource |
| [aws_db_instance.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance) | resource |
| [aws_efs_file_system.eks_pv](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_file_system) | resource |
| [aws_efs_mount_target.eks_pv_mnt](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/efs_mount_target) | resource |
| [aws_elasticsearch_domain.es](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticsearch_domain) | resource |
| [aws_elasticsearch_domain_policy.es_management_access](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticsearch_domain_policy) | resource |
| [aws_iam_policy.cert_manager_route53_iam_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy) | resource |
| [aws_iam_role.cert_manager_route53_iam_role](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.efs_provisioner](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role.external_dns](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role) | resource |
| [aws_iam_role_policy.external_dns](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy) | resource |
| [aws_iam_role_policy_attachment.efs_provisioner](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role_policy_attachment) | resource |
| [aws_iam_service_linked_role.es](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_service_linked_role) | resource |
| [aws_key_pair.eks_workers](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/key_pair) | resource |
| [aws_route53_zone.orc8r](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_zone) | resource |
| [aws_secretsmanager_secret.orc8r_secrets](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/secretsmanager_secret) | resource |
| [aws_security_group.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) | resource |
| [aws_sns_topic.sns_orc8r_topic](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/sns_topic) | resource |
| [aws_sns_topic_subscription.sns_orc8r_db_subscription_email](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/sns_topic_subscription) | resource |
| [random_id.cert_manager_route53_random_id](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |
| [tls_private_key.eks_workers](https://registry.terraform.io/providers/hashicorp/tls/latest/docs/resources/private_key) | resource |
| [aws_availability_zones.available](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/availability_zones) | data source |
| [aws_eks_cluster.cluster](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster) | data source |
| [aws_eks_cluster_auth.cluster](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster_auth) | data source |
| [aws_iam_policy_document.cert_manager_route53_iam_policy_document](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.cert_manager_route53_iam_policy_document_assume](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.eks_worker_assumable](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.es-management](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |
| [aws_iam_policy_document.external_dns](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/iam_policy_document) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_blue_green_worker_groups"></a> [blue\_green\_worker\_groups](#input\_blue\_green\_worker\_groups) | Worker group configuration for EKS. Default value is 1 worker group consisting of 5 t3.medium instances. | `any` | <pre>[<br>  {<br>    "asg_desired_capacity": 8,<br>    "asg_max_size": 8,<br>    "asg_min_size": 1,<br>    "autoscaling_enabled": false,<br>    "instance_type": "t3.medium",<br>    "kubelet_extra_args": "",<br>    "name": "wg-1"<br>  }<br>]</pre> | no |
| <a name="input_cluster_name"></a> [cluster\_name](#input\_cluster\_name) | Name for the Orchestrator EKS cluster. | `string` | `"orc8r"` | no |
| <a name="input_cluster_version"></a> [cluster\_version](#input\_cluster\_version) | Kubernetes version for the EKS cluster. | `string` | `"1.21"` | no |
| <a name="input_deploy_elasticsearch"></a> [deploy\_elasticsearch](#input\_deploy\_elasticsearch) | Flag to deploy AWS Elasticsearch service as the datasink for aggregated logs. | `bool` | `false` | no |
| <a name="input_deploy_elasticsearch_service_linked_role"></a> [deploy\_elasticsearch\_service\_linked\_role](#input\_deploy\_elasticsearch\_service\_linked\_role) | Flag to deploy AWS Elasticsearch service linked role with cluster. If you've already created an ES service linked role for another cluster, you should set this to false. | `bool` | `true` | no |
| <a name="input_efs_project_name"></a> [efs\_project\_name](#input\_efs\_project\_name) | Project name for EFS file system | `string` | `"orc8r"` | no |
| <a name="input_eks_enable_irsa"></a> [eks\_enable\_irsa](#input\_eks\_enable\_irsa) | Enable IAM Roles for Service Accounts (IRSA) on the EKS cluster. | `bool` | `true` | no |
| <a name="input_eks_map_roles"></a> [eks\_map\_roles](#input\_eks\_map\_roles) | EKS IAM role mapping. Note that by default, the creator of the cluster will be in the system:master group. | <pre>list(<br>    object({<br>      rolearn  = string,<br>      username = string,<br>      groups   = list(string),<br>    })<br>  )</pre> | `[]` | no |
| <a name="input_eks_map_users"></a> [eks\_map\_users](#input\_eks\_map\_users) | Additional IAM users to add to the aws-auth ConfigMap. | <pre>list(object({<br>    userarn  = string<br>    username = string<br>    groups   = list(string)<br>  }))</pre> | `[]` | no |
| <a name="input_eks_worker_additional_policy_arns"></a> [eks\_worker\_additional\_policy\_arns](#input\_eks\_worker\_additional\_policy\_arns) | Additional IAM policy ARNs to attach to EKS worker nodes. | `list(string)` | `[]` | no |
| <a name="input_eks_worker_additional_sg_ids"></a> [eks\_worker\_additional\_sg\_ids](#input\_eks\_worker\_additional\_sg\_ids) | Additional security group IDs to attach to EKS worker nodes. | `list(string)` | `[]` | no |
| <a name="input_eks_worker_group_key"></a> [eks\_worker\_group\_key](#input\_eks\_worker\_group\_key) | If specified, the worker nodes for EKS will use this EC2 keypair. | `string` | `null` | no |
| <a name="input_eks_worker_groups"></a> [eks\_worker\_groups](#input\_eks\_worker\_groups) | Worker group configuration for EKS. Default value is 1 worker group consisting of 3 t3.large instances. | `any` | <pre>[<br>  {<br>    "asg_desired_capacity": 3,<br>    "asg_max_size": 3,<br>    "asg_min_size": 1,<br>    "autoscaling_enabled": false,<br>    "instance_type": "t3.large",<br>    "kubelet_extra_args": "",<br>    "name": "wg-1"<br>  }<br>]</pre> | no |
| <a name="input_elasticsearch_az_count"></a> [elasticsearch\_az\_count](#input\_elasticsearch\_az\_count) | AZ count for ES. | `number` | `2` | no |
| <a name="input_elasticsearch_dedicated_master_count"></a> [elasticsearch\_dedicated\_master\_count](#input\_elasticsearch\_dedicated\_master\_count) | Number of dedicated ES master nodes. | `number` | `null` | no |
| <a name="input_elasticsearch_dedicated_master_enabled"></a> [elasticsearch\_dedicated\_master\_enabled](#input\_elasticsearch\_dedicated\_master\_enabled) | Enable/disable dedicated master nodes for ES. | `bool` | `false` | no |
| <a name="input_elasticsearch_dedicated_master_type"></a> [elasticsearch\_dedicated\_master\_type](#input\_elasticsearch\_dedicated\_master\_type) | Instance type for ES dedicated master nodes. | `string` | `null` | no |
| <a name="input_elasticsearch_domain_name"></a> [elasticsearch\_domain\_name](#input\_elasticsearch\_domain\_name) | Name for the ES domain. | `string` | `null` | no |
| <a name="input_elasticsearch_domain_tags"></a> [elasticsearch\_domain\_tags](#input\_elasticsearch\_domain\_tags) | Extra tags for the ES domain. | `map` | `{}` | no |
| <a name="input_elasticsearch_ebs_enabled"></a> [elasticsearch\_ebs\_enabled](#input\_elasticsearch\_ebs\_enabled) | Use EBS for ES storage. See https://aws.amazon.com/elasticsearch-service/pricing/ to check if your chosen instance types can use non-EBS storage. | `bool` | `false` | no |
| <a name="input_elasticsearch_ebs_iops"></a> [elasticsearch\_ebs\_iops](#input\_elasticsearch\_ebs\_iops) | IOPS for ES EBS volumes. | `number` | `null` | no |
| <a name="input_elasticsearch_ebs_volume_size"></a> [elasticsearch\_ebs\_volume\_size](#input\_elasticsearch\_ebs\_volume\_size) | Size in GB to allocate for ES EBS data volumes. | `number` | `null` | no |
| <a name="input_elasticsearch_ebs_volume_type"></a> [elasticsearch\_ebs\_volume\_type](#input\_elasticsearch\_ebs\_volume\_type) | EBS volume type for ES data volumes. | `string` | `null` | no |
| <a name="input_elasticsearch_instance_count"></a> [elasticsearch\_instance\_count](#input\_elasticsearch\_instance\_count) | Number of instances to allocate for ES domain. | `number` | `null` | no |
| <a name="input_elasticsearch_instance_type"></a> [elasticsearch\_instance\_type](#input\_elasticsearch\_instance\_type) | AWS instance type for ES domain. | `string` | `null` | no |
| <a name="input_elasticsearch_version"></a> [elasticsearch\_version](#input\_elasticsearch\_version) | ES version for ES domain. | `string` | `"7.1"` | no |
| <a name="input_enable_aws_db_notifications"></a> [enable\_aws\_db\_notifications](#input\_enable\_aws\_db\_notifications) | Flag to enable AWS RDS notifications | `bool` | `false` | no |
| <a name="input_enable_orc8r_blue_green_deployment"></a> [enable\_orc8r\_blue\_green\_deployment](#input\_enable\_orc8r\_blue\_green\_deployment) | Flag to enable the deployment for a blue & green Orc8r instances in the same infrastructure | `bool` | `false` | no |
| <a name="input_global_tags"></a> [global\_tags](#input\_global\_tags) | n/a | `map` | `{}` | no |
| <a name="input_magma_uuid"></a> [magma\_uuid](#input\_magma\_uuid) | UUID to identify Orc8r deployment | `string` | `"default"` | no |
| <a name="input_orc8r_db_apply_immediately"></a> [orc8r\_db\_apply\_immediately](#input\_orc8r\_db\_apply\_immediately) | Flag to immediately upgrade RDS without waiting for a maintenance window | `bool` | `false` | no |
| <a name="input_orc8r_db_backup_retention"></a> [orc8r\_db\_backup\_retention](#input\_orc8r\_db\_backup\_retention) | Database backup retention period | `number` | `7` | no |
| <a name="input_orc8r_db_backup_window"></a> [orc8r\_db\_backup\_window](#input\_orc8r\_db\_backup\_window) | Database daily backup window in UTC with a 30-minute minimum | `string` | `"01:00-01:30"` | no |
| <a name="input_orc8r_db_dialect"></a> [orc8r\_db\_dialect](#input\_orc8r\_db\_dialect) | Database dialect for Orchestrator DB. | `string` | `"postgres"` | no |
| <a name="input_orc8r_db_engine_version"></a> [orc8r\_db\_engine\_version](#input\_orc8r\_db\_engine\_version) | Postgres engine version for Orchestrator DB. | `string` | `"12.8"` | no |
| <a name="input_orc8r_db_event_subscription"></a> [orc8r\_db\_event\_subscription](#input\_orc8r\_db\_event\_subscription) | Database event subscription | `string` | `"orc8r-rds-events"` | no |
| <a name="input_orc8r_db_identifier"></a> [orc8r\_db\_identifier](#input\_orc8r\_db\_identifier) | Identifier for the RDS instance for Orchestrator. | `string` | `"orc8rdb"` | no |
| <a name="input_orc8r_db_instance_class"></a> [orc8r\_db\_instance\_class](#input\_orc8r\_db\_instance\_class) | RDS instance type for Orchestrator DB. | `string` | `"db.m4.large"` | no |
| <a name="input_orc8r_db_name"></a> [orc8r\_db\_name](#input\_orc8r\_db\_name) | DB name for Orchestrator RDS instance. | `string` | `"orc8r"` | no |
| <a name="input_orc8r_db_password"></a> [orc8r\_db\_password](#input\_orc8r\_db\_password) | Password for the Orchestrator DB. Must be at least 8 characters. | `string` | n/a | yes |
| <a name="input_orc8r_db_storage_gb"></a> [orc8r\_db\_storage\_gb](#input\_orc8r\_db\_storage\_gb) | Capacity in GB to allocate for Orchestrator RDS instance. | `number` | `64` | no |
| <a name="input_orc8r_db_username"></a> [orc8r\_db\_username](#input\_orc8r\_db\_username) | Username for default DB user for Orchestrator DB. | `string` | `"orc8r"` | no |
| <a name="input_orc8r_domain_name"></a> [orc8r\_domain\_name](#input\_orc8r\_domain\_name) | Base domain name for AWS Route 53 hosted zone. | `string` | n/a | yes |
| <a name="input_orc8r_sns_email"></a> [orc8r\_sns\_email](#input\_orc8r\_sns\_email) | SNS email endpoint to send notifications | `string` | `""` | no |
| <a name="input_orc8r_sns_name"></a> [orc8r\_sns\_name](#input\_orc8r\_sns\_name) | SNS for Orc8r to redirect alerts and notifications | `string` | `"orc8r-sns"` | no |
| <a name="input_region"></a> [region](#input\_region) | AWS region to deploy Orchestrator components into. The chosen region must provide EKS. | `string` | n/a | yes |
| <a name="input_secretsmanager_orc8r_secret"></a> [secretsmanager\_orc8r\_secret](#input\_secretsmanager\_orc8r\_secret) | AWS Secret Manager secret to store Orchestrator secrets. | `string` | n/a | yes |
| <a name="input_setup_cert_manager"></a> [setup\_cert\_manager](#input\_setup\_cert\_manager) | Create IAM role and policy for cert-manager. | `bool` | `false` | no |
| <a name="input_thanos_enabled"></a> [thanos\_enabled](#input\_thanos\_enabled) | Enable thanos infrastructure | `bool` | `false` | no |
| <a name="input_thanos_worker_groups"></a> [thanos\_worker\_groups](#input\_thanos\_worker\_groups) | Worker group configuration for Thanos. Default consists of 1 group consisting of 1 m5d.xlarge for thanos. | `any` | <pre>[<br>  {<br>    "asg_desired_capacity": 1,<br>    "asg_max_size": 1,<br>    "asg_min_size": 1,<br>    "autoscaling_enabled": false,<br>    "instance_type": "m5d.xlarge",<br>    "kubelet_extra_args": "--node-labels=compute-type=thanos",<br>    "name": "thanos-1"<br>  }<br>]</pre> | no |
| <a name="input_vpc_cidr"></a> [vpc\_cidr](#input\_vpc\_cidr) | CIDR block for the VPC. | `string` | `"10.10.0.0/16"` | no |
| <a name="input_vpc_database_subnets"></a> [vpc\_database\_subnets](#input\_vpc\_database\_subnets) | CIDR blocks for the VPC's database subnets. | `list(string)` | <pre>[<br>  "10.10.200.0/24",<br>  "10.10.201.0/24",<br>  "10.10.202.0/24"<br>]</pre> | no |
| <a name="input_vpc_extra_tags"></a> [vpc\_extra\_tags](#input\_vpc\_extra\_tags) | Tags to add to the VPC. | `map` | `{}` | no |
| <a name="input_vpc_name"></a> [vpc\_name](#input\_vpc\_name) | Name for the VPC that will contain all the Orchestrator components. | `string` | `"orc8r_vpc"` | no |
| <a name="input_vpc_private_subnets"></a> [vpc\_private\_subnets](#input\_vpc\_private\_subnets) | CIDR blocks for the VPC's private subnets. | `list(string)` | <pre>[<br>  "10.10.100.0/24",<br>  "10.10.101.0/24",<br>  "10.10.102.0/24"<br>]</pre> | no |
| <a name="input_vpc_public_subnets"></a> [vpc\_public\_subnets](#input\_vpc\_public\_subnets) | CIDR blocks for the VPC's public subnets. | `list(string)` | <pre>[<br>  "10.10.0.0/24",<br>  "10.10.1.0/24",<br>  "10.10.2.0/24"<br>]</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_cert_manager_route53_iam_role_arn"></a> [cert\_manager\_route53\_iam\_role\_arn](#output\_cert\_manager\_route53\_iam\_role\_arn) | IAM role ARN for cert-manager. |
| <a name="output_efs_file_system_id"></a> [efs\_file\_system\_id](#output\_efs\_file\_system\_id) | ID of the EFS file system created for K8s persistent volumes. |
| <a name="output_efs_provisioner_role_arn"></a> [efs\_provisioner\_role\_arn](#output\_efs\_provisioner\_role\_arn) | ARN of the IAM role for the EFS provisioner. |
| <a name="output_eks_cluster_id"></a> [eks\_cluster\_id](#output\_eks\_cluster\_id) | Cluster ID for the EKS cluster |
| <a name="output_eks_config_map_aws_auth"></a> [eks\_config\_map\_aws\_auth](#output\_eks\_config\_map\_aws\_auth) | A K8s ConfigMap to allow authentication to the EKS cluster. |
| <a name="output_es_endpoint"></a> [es\_endpoint](#output\_es\_endpoint) | Endpoint of the ES cluster if deployed. |
| <a name="output_es_volume_size"></a> [es\_volume\_size](#output\_es\_volume\_size) | Endpoint of the ES cluster if deployed. |
| <a name="output_external_dns_role_arn"></a> [external\_dns\_role\_arn](#output\_external\_dns\_role\_arn) | IAM role ARN for external-dns |
| <a name="output_kubeconfig"></a> [kubeconfig](#output\_kubeconfig) | kubectl config file to access the EKS cluster |
| <a name="output_orc8r_db_dialect"></a> [orc8r\_db\_dialect](#output\_orc8r\_db\_dialect) | Database dialect for Orchestrator RDS instance |
| <a name="output_orc8r_db_host"></a> [orc8r\_db\_host](#output\_orc8r\_db\_host) | Hostname of the Orchestrator RDS instance |
| <a name="output_orc8r_db_name"></a> [orc8r\_db\_name](#output\_orc8r\_db\_name) | Database name for Orchestrator RDS instance |
| <a name="output_orc8r_db_pass"></a> [orc8r\_db\_pass](#output\_orc8r\_db\_pass) | Orchestrator DB password |
| <a name="output_orc8r_db_port"></a> [orc8r\_db\_port](#output\_orc8r\_db\_port) | Database connection port for Orchestrator RDS instance |
| <a name="output_orc8r_db_user"></a> [orc8r\_db\_user](#output\_orc8r\_db\_user) | Database username for Orchestrator RDS instance |
| <a name="output_orc8r_domain_name"></a> [orc8r\_domain\_name](#output\_orc8r\_domain\_name) | Base domain name for Orchestrator application components. |
| <a name="output_route53_nameservers"></a> [route53\_nameservers](#output\_route53\_nameservers) | Route53 zone nameservers for external DNS configuration. |
| <a name="output_route53_zone_id"></a> [route53\_zone\_id](#output\_route53\_zone\_id) | Route53 zone ID for Orchestrator domain name |
| <a name="output_secretsmanager_secret_name"></a> [secretsmanager\_secret\_name](#output\_secretsmanager\_secret\_name) | Name of the Secrets Manager secret for deployment secrets |
| <a name="output_setup_cert_manager"></a> [setup\_cert\_manager](#output\_setup\_cert\_manager) | Create IAM role and policy for cert-manager. |
<!-- END_TF_DOCS -->