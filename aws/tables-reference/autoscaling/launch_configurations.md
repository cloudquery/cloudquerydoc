# launch\_configurations

#### YAML config

```yaml
- name: autoscaling.launch_configuration
  LaunchConfigurationNames: // Optional filter
    - "The launch configuration names."
```

#### Tables schemas:

```sql
create table aws_autoscaling_launch_configurations
(
    id                                           integer primary key,
    account_id                                   text,
    region                                       text,
    associate_public_ip_address                  numeric,
    classic_link_vpc_id                          text,
    classic_link_vpc_security_groups             text,
    created_time                                 datetime,
    ebs_optimized                                numeric,
    iam_instance_profile                         text,
    image_id                                     text,
    instance_monitoring_enabled                  numeric,
    instance_type                                text,
    kernel_id                                    text,
    key_name                                     text,
    launch_configuration_arn                     text,
    launch_configuration_name                    text,
    metadata_options_http_endpoint               text,
    metadata_options_http_put_response_hop_limit integer,
    metadata_options_http_tokens                 text,
    placement_tenancy                            text,
    ramdisk_id                                   text,
    security_groups                              text,
    spot_price                                   text,
    user_data                                    text
);

create table aws_autoscaling_launch_configuration_block_device_mappings
(
    id                        integer primary key,
    launch_configuration_id   integer
        constraint fk_aws_autoscaling_launch_configurations_block_device_mappings
            references aws_autoscaling_launch_configurations
            on delete cascade,
    device_name               text,
    ebs_delete_on_termination numeric,
    ebs_encrypted             numeric,
    ebs_iops                  integer,
    ebs_snapshot_id           text,
    ebs_volume_size           integer,
    ebs_volume_type           text,
    no_device                 numeric,
    virtual_name              text
);
```

#### 

