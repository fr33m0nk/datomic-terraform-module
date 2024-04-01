## Cognitect has made the Datomic Cloud template available in AWS marketplace and effectively deprecating this module.

# Terraform module for provisioning Datomic Transactor On-Prem version on AWS

### Input variables:

| Module variable                                          | Description                                                                                                                                                                                                                       | Value type     | Default value                                                                                                                                                                                                  |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `aws_region`                                             | AWS region in which resources for Datomic get provisioned                                                                                                                                                                         | `string`       | NA                                                                                                                                                                                                             |
| `vpc_id`                                                 | AWS VPC ID in which resources for Datomic get provisioned. If not provided uses the ID of the default VPC                                                                                                                         | `string`       | NA                                                                                                                                                                                                             |
| `datomic_peer_security_group_id`                         | Security group id already applied to peer to allow communication to Datomic transactor and related resources                                                                                                                      | `string`       | NA                                                                                                                                                                                                             |
| `datomic_peer_iam_role_name`                             | IAM role name of a role already applied to Peer. Serves as the Peer role name in Datomic Transactor configuration                                                                                                                 | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_availability_zone_names`             | List of availability zones for Datomic Transactor                                                                                                                                                                                 | `List(string)` | NA                                                                                                                                                                                                             |
| `datomic_transactor_subnet_ids`                          | List of Subnet IDs for Datomic Transactor                                                                                                                                                                                         | `List(string)` | NA                                                                                                                                                                                                             |
| `datomic_transactor_ami_name`                            | AMI name for the transactor. If AMI is ARM based, then select appropriate `datomic_transactor_instance_type`                                                                                                                      | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_ami_owner_id`                        | Owner ID of AMI for the transactor                                                                                                                                                                                                | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_ami_user`                            | AMI user with privileges for starting a Java process                                                                                                                                                                              | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_keypair_name`                        | AWS KeyPair name for SSH logins in Transactor instance                                                                                                                                                                            | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_metric_callback_library`             | Metric callback library for emitting stats to Datadog, Prometheus etc. Must be available on Datomic Transactor Classpath in Transactor AMI, e.g. [Datomic-Datadog-reporter](https://github.com/fr33m0nk/datomic-datadog-reporter) | `string`       | `null`                                                                                                                                                                                                         |
| `datomic_transactor_enable_datadog`                      | Enables Datadog if set to true and Datadog is installed in Datomic Transactor AMI                                                                                                                                                 | `bool`         | `false`                                                                                                                                                                                                        |
| `datomic_transactor_instance_type`                       | EBS optimised instance. [Details](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-optimized.html)                                                                                                                         | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_volume_type`                         | Volume type to be used as root volume, e.g. io1                                                                                                                                                                                   | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_jvm_xmx`                             | Datomic transactor -Xmx configuration. Ballpark the value at 70% of total RAM                                                                                                                                                     | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_jvm_xms`                             | Datomic transactor -Xms configuration                                                                                                                                                                                             | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_java_opts`                           | JAVA_OPTS for launching Datomic transactor                                                                                                                                                                                        | `string`       | `-XX:+UseG1GC -XX:MaxGCPauseMillis=50 -Dcom.sun.management.jmxremote=true -Dcom.sun.management.jmxremote.port=7199 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false` |
| `datomic_transactor_log_level`                           | Datomic transactor log level                                                                                                                                                                                                      | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_memory_index_threshold`              | Datomic Memory index size threshold                                                                                                                                                                                               | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_memory_index_max`                    | Datomic Memory index max size                                                                                                                                                                                                     | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_object_cache_max`                    | Datomic transactor Object cache max size                                                                                                                                                                                          | `string`       | NA                                                                                                                                                                                                             |
| `datomic_license`                                        | Datomic licence key                                                                                                                                                                                                               | `string`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_root_volume_size`                    | The size of the Datomic Transactor's root volume in gigabytes                                                                                                                                                                     | `number`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_root_iops`                           | The amount of provisioned IOPS for Datomic Transactor's root volume. [Details](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-io-characteristics.html)                                                                   | `number`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_write_concurrency`                   | Write concurrency factor for Transactor. [Details](https://docs.datomic.com/on-prem/operation/capacity.html)                                                                                                                      | `number`       | NA                                                                                                                                                                                                             |
| `datomic_transactor_read_concurrency`                    | Read concurrency factor for Transactor. Generally twice of write concurrency. [Details](https://docs.datomic.com/on-prem/operation/capacity.html)                                                                                 | `number`       | NA                                                                                                                                                                                                             |
| `datomic_transactors_max_instance_count`                 | The maximum capacity of the Auto Scaling Group                                                                                                                                                                                    | `number`       | `3`                                                                                                                                                                                                            |
| `datomic_transactors_desired_instance_count`             | The desired capacity of the Auto Scaling Group                                                                                                                                                                                    | `number`       | `2`                                                                                                                                                                                                            |
| `datomic_transactors_min_instance_count`                 | The minimum capacity of the Auto Scaling Group. Also serves as the desired capacity                                                                                                                                               | `number`       | `1`                                                                                                                                                                                                            |
| `datomic_dynamo_db_table_read_autoscaling_min_capacity`  | Minimum value for the read capacity for autoscaling. Also serves as base Dynamo DB Table read capacity                                                                                                                            | `string`       | NA                                                                                                                                                                                                             |
| `datomic_dynamo_db_table_read_autoscaling_max_capacity`  | Maximum value for the read capacity for autoscaling                                                                                                                                                                               | `string`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_read_autoscaling_scale_in_cooldown`     | The amount of time, in seconds, after a read capacity scale in activity completes before another scale in activity can start                                                                                                      | `number`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_read_autoscaling_scale_out_cooldown`    | The amount of time, in seconds, after a read capacity scale out activity completes before another scale out activity can start                                                                                                    | `number`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_read_autoscaling_target_value`          | The target value (%age) for triggering autoscaling of read capacity                                                                                                                                                               | `number`       | NA                                                                                                                                                                                                             |
| `datomic_dynamo_db_table_write_autoscaling_min_capacity` | Minimum value for the write capacity for autoscaling. Also serves as base Dynamo DB Table write capacity                                                                                                                          | `number`       | NA                                                                                                                                                                                                             |
| `datomic_dynamo_db_table_write_autoscaling_max_capacity` | Maximum value for the write capacity for autoscaling                                                                                                                                                                              | `number`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_write_autoscaling_scale_in_cooldown`    | The amount of time, in seconds, after a write capacity scale in activity completes before another scale in activity can start                                                                                                     | `number`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_write_autoscaling_scale_out_cooldown`   | The amount of time, in seconds, after a write capacity scale out activity completes before another scale out activity can start                                                                                                   | `number`       | NA                                                                                                                                                                                                             |
| `dynamo_db_table_write_autoscaling_target_value`         | The target value (%age) for triggering autoscaling of write capacity                                                                                                                                                              | `number`       | NA                                                                                                                                                                                                             |
| `memcached_version`                                      | Version of the engine of elasticache. [Details](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/supported-engine-versions.html)                                                                                       | `string`       | NA                                                                                                                                                                                                             |
| `memcached_exposed_port`                                 | Port exposed for accessing the cluster                                                                                                                                                                                            | `number`       | `11211`                                                                                                                                                                                                        |
| `memcached_instance_type`                                | Instance type to be used for the nodes of the cluster                                                                                                                                                                             | `string`       | NA                                                                                                                                                                                                             |
| `memcached_az_mode`                                      | Whether the nodes in this Memcached node group are created in a single Availability Zone or created across multiple Availability Zones in the cluster's region. Valid values for this parameter are `single-az` or `cross-az`     | `string`       | NA                                                                                                                                                                                                             |
| `memcached_number_of_instances`                          | Number of nodes in the cluster. [Details](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-optimized.html)                                                                                                                 | `string`       | NA                                                                                                                                                                                                             |
| `memcached_parameter_group_name`                         | Name of the parameter group to associate with this cache cluster. [Details](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticache_parameter_group)                                              | `string`       | NA                                                                                                                                                                                                             |
| `memcached_apply_changes_immediately`                    | Applies changes immediately if true else the changes are applied in the next maintenance window                                                                                                                                   | `bool`         | NA                                                                                                                                                                                                             |

### Output attributes:

| Module variable                                               | Description                                                                                                                                                                                                           |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `datomic_transactor.s3_logs`                                  | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket#attributes-reference) of the S3 resource provsioned to act as Datomic Transactor Write ahead logs         |
| `datomic_transactor.security_group`                           | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group#attributes-reference) of the security group provisioned for Datomic Transactor                       |
| `datomic_transactor.iam_role`                                 | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_role#attributes-reference) of the security group provisioned for Datomic Transactor                             |
| `datomic_transactor.iam_instance_profile`                     | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_instance_profile#attributes-reference) of the instance profile provisioned for Datomic Transactor               |
| `datomic_transactor.launch_config`                            | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/launch_configuration#attributes-reference) of the launch configuration provisioned for Datomic Transactor           |
| `datomic_transactor.autoscaling_group.id`                     | ID of the Cloudformation stack for the auto scaling group provisioned for Datomic Transactor                                                                                                                          |
| `datomic_transactor.autoscaling_group.outputs`                | Detailed attributes of the cloudformation stack and auto scaling group provisioned for Datomic Transactor                                                                                                             |
| `datomic_peer.iam_policy`                                     | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy#attributes-reference) of the IAM policy provisioned for Datomic Peer                                     |
| `datomic_peer.iam_policy_attachment`                          | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_policy_attachment#attributes-reference) of the Peer IAM policy attached to Datomic Peer IAM role name           |
| `datomic_transactor_dynamo_db.table`                          | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dynamodb_table#attributes-reference) of the Dynamo DB Table provisioned for Datomic Transactor                      |
| `datomic_transactor_dynamo_db.table_read_autoscaling_target`  | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/appautoscaling_target#attributes-reference) of the Dynamo DB Table Read Auto scaling Target for Datomic Transactor  |
| `datomic_transactor_dynamo_db.table_read_autoscaling_policy`  | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/appautoscaling_policy#attributes-reference) of the Dynamo DB Table Read Auto scaling Policy for Datomic Transactor  |
| `datomic_transactor_dynamo_db.table_write_autoscaling_target` | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/appautoscaling_target#attributes-reference) of the Dynamo DB Table Write Auto scaling Target for Datomic Transactor |
| `datomic_transactor_dynamo_db.table_write_autoscaling_policy` | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/appautoscaling_policy#attributes-reference) of the Dynamo DB Table Write Auto scaling Policy for Datomic Transactor |
| `datomic_transactor_memcached.cluster`                        | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elasticache_cluster#attributes-reference) of the Memcached cluster provisioned for Datomic Transactor               |
| `datomic_transactor_memcached.cluster_security_group`         | [Detailed attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group#attributes-reference) of the security group provisioned for Memcached used by Datomic Transactor     |

## License
##### Copyright © 2022 Prashant Sinha Distributed under the Eclipse Public License version 1.0.
