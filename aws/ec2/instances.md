# instances

#### YAML config

```text
- name: ec2.instances
	InstanceIds: // Optional. Default: Describes all your instances.
		- "id" // The instance IDs.

	// The filters (Optional).
	//
	//    * affinity - The affinity setting for an instance running on a Dedicated
	//    Host (default | host).
	//
	//    * architecture - The instance architecture (i386 | x86_64 | arm64).
	//
	//    * availability-zone - The Availability Zone of the instance.
	//
	//    * block-device-mapping.attach-time - The attach time for an EBS volume
	//    mapped to the instance, for example, 2010-09-15T17:15:20.000Z.
	//
	//    * block-device-mapping.delete-on-termination - A Boolean that indicates
	//    whether the EBS volume is deleted on instance termination.
	//
	//    * block-device-mapping.device-name - The device name specified in the
	//    block device mapping (for example, /dev/sdh or xvdh).
	//
	//    * block-device-mapping.status - The status for the EBS volume (attaching
	//    | attached | detaching | detached).
	//
	//    * block-device-mapping.volume-id - The volume ID of the EBS volume.
	//
	//    * client-token - The idempotency token you provided when you launched
	//    the instance.
	//
	//    * dns-name - The public DNS name of the instance.
	//
	//    * group-id - The ID of the security group for the instance. EC2-Classic
	//    only.
	//
	//    * group-name - The name of the security group for the instance. EC2-Classic
	//    only.
	//
	//    * hibernation-options.configured - A Boolean that indicates whether the
	//    instance is enabled for hibernation. A value of true means that the instance
	//    is enabled for hibernation.
	//
	//    * host-id - The ID of the Dedicated Host on which the instance is running,
	//    if applicable.
	//
	//    * hypervisor - The hypervisor type of the instance (ovm | xen). The value
	//    xen is used for both Xen and Nitro hypervisors.
	//
	//    * iam-instance-profile.arn - The instance profile associated with the
	//    instance. Specified as an ARN.
	//
	//    * image-id - The ID of the image used to launch the instance.
	//
	//    * instance-id - The ID of the instance.
	//
	//    * instance-lifecycle - Indicates whether this is a Spot Instance or a
	//    Scheduled Instance (spot | scheduled).
	//
	//    * instance-state-code - The state of the instance, as a 16-bit unsigned
	//    integer. The high byte is used for internal purposes and should be ignored.
	//    The low byte is set based on the state represented. The valid values are:
	//    0 (pending), 16 (running), 32 (shutting-down), 48 (terminated), 64 (stopping),
	//    and 80 (stopped).
	//
	//    * instance-state-name - The state of the instance (pending | running |
	//    shutting-down | terminated | stopping | stopped).
	//
	//    * instance-type - The type of instance (for example, t2.micro).
	//
	//    * instance.group-id - The ID of the security group for the instance.
	//
	//    * instance.group-name - The name of the security group for the instance.
	//
	//    * ip-address - The public IPv4 address of the instance.
	//
	//    * kernel-id - The kernel ID.
	//
	//    * key-name - The name of the key pair used when the instance was launched.
	//
	//    * launch-index - When launching multiple instances, this is the index
	//    for the instance in the launch group (for example, 0, 1, 2, and so on).
	//
	//    * launch-time - The time when the instance was launched.
	//
	//    * metadata-options.http-tokens - The metadata request authorization state
	//    (optional | required)
	//
	//    * metadata-options.http-put-response-hop-limit - The http metadata request
	//    put response hop limit (integer, possible values 1 to 64)
	//
	//    * metadata-options.http-endpoint - Enable or disable metadata access on
	//    http endpoint (enabled | disabled)
	//
	//    * monitoring-state - Indicates whether detailed monitoring is enabled
	//    (disabled | enabled).
	//
	//    * network-interface.addresses.private-ip-address - The private IPv4 address
	//    associated with the network interface.
	//
	//    * network-interface.addresses.primary - Specifies whether the IPv4 address
	//    of the network interface is the primary private IPv4 address.
	//
	//    * network-interface.addresses.association.public-ip - The ID of the association
	//    of an Elastic IP address (IPv4) with a network interface.
	//
	//    * network-interface.addresses.association.ip-owner-id - The owner ID of
	//    the private IPv4 address associated with the network interface.
	//
	//    * network-interface.association.public-ip - The address of the Elastic
	//    IP address (IPv4) bound to the network interface.
	//
	//    * network-interface.association.ip-owner-id - The owner of the Elastic
	//    IP address (IPv4) associated with the network interface.
	//
	//    * network-interface.association.allocation-id - The allocation ID returned
	//    when you allocated the Elastic IP address (IPv4) for your network interface.
	//
	//    * network-interface.association.association-id - The association ID returned
	//    when the network interface was associated with an IPv4 address.
	//
	//    * network-interface.attachment.attachment-id - The ID of the interface
	//    attachment.
	//
	//    * network-interface.attachment.instance-id - The ID of the instance to
	//    which the network interface is attached.
	//
	//    * network-interface.attachment.instance-owner-id - The owner ID of the
	//    instance to which the network interface is attached.
	//
	//    * network-interface.attachment.device-index - The device index to which
	//    the network interface is attached.
	//
	//    * network-interface.attachment.status - The status of the attachment (attaching
	//    | attached | detaching | detached).
	//
	//    * network-interface.attachment.attach-time - The time that the network
	//    interface was attached to an instance.
	//
	//    * network-interface.attachment.delete-on-termination - Specifies whether
	//    the attachment is deleted when an instance is terminated.
	//
	//    * network-interface.availability-zone - The Availability Zone for the
	//    network interface.
	//
	//    * network-interface.description - The description of the network interface.
	//
	//    * network-interface.group-id - The ID of a security group associated with
	//    the network interface.
	//
	//    * network-interface.group-name - The name of a security group associated
	//    with the network interface.
	//
	//    * network-interface.ipv6-addresses.ipv6-address - The IPv6 address associated
	//    with the network interface.
	//
	//    * network-interface.mac-address - The MAC address of the network interface.
	//
	//    * network-interface.network-interface-id - The ID of the network interface.
	//
	//    * network-interface.owner-id - The ID of the owner of the network interface.
	//
	//    * network-interface.private-dns-name - The private DNS name of the network
	//    interface.
	//
	//    * network-interface.requester-id - The requester ID for the network interface.
	//
	//    * network-interface.requester-managed - Indicates whether the network
	//    interface is being managed by AWS.
	//
	//    * network-interface.status - The status of the network interface (available)
	//    | in-use).
	//
	//    * network-interface.source-dest-check - Whether the network interface
	//    performs source/destination checking. A value of true means that checking
	//    is enabled, and false means that checking is disabled. The value must
	//    be false for the network interface to perform network address translation
	//    (NAT) in your VPC.
	//
	//    * network-interface.subnet-id - The ID of the subnet for the network interface.
	//
	//    * network-interface.vpc-id - The ID of the VPC for the network interface.
	//
	//    * owner-id - The AWS account ID of the instance owner.
	//
	//    * placement-group-name - The name of the placement group for the instance.
	//
	//    * placement-partition-number - The partition in which the instance is
	//    located.
	//
	//    * platform - The platform. To list only Windows instances, use windows.
	//
	//    * private-dns-name - The private IPv4 DNS name of the instance.
	//
	//    * private-ip-address - The private IPv4 address of the instance.
	//
	//    * product-code - The product code associated with the AMI used to launch
	//    the instance.
	//
	//    * product-code.type - The type of product code (devpay | marketplace).
	//
	//    * ramdisk-id - The RAM disk ID.
	//
	//    * reason - The reason for the current state of the instance (for example,
	//    shows "User Initiated [date]" when you stop or terminate the instance).
	//    Similar to the state-reason-code filter.
	//
	//    * requester-id - The ID of the entity that launched the instance on your
	//    behalf (for example, AWS Management Console, Auto Scaling, and so on).
	//
	//    * reservation-id - The ID of the instance's reservation. A reservation
	//    ID is created any time you launch an instance. A reservation ID has a
	//    one-to-one relationship with an instance launch request, but can be associated
	//    with more than one instance if you launch multiple instances using the
	//    same launch request. For example, if you launch one instance, you get
	//    one reservation ID. If you launch ten instances using the same launch
	//    request, you also get one reservation ID.
	//
	//    * root-device-name - The device name of the root device volume (for example,
	//    /dev/sda1).
	//
	//    * root-device-type - The type of the root device volume (ebs | instance-store).
	//
	//    * source-dest-check - Indicates whether the instance performs source/destination
	//    checking. A value of true means that checking is enabled, and false means
	//    that checking is disabled. The value must be false for the instance to
	//    perform network address translation (NAT) in your VPC.
	//
	//    * spot-instance-request-id - The ID of the Spot Instance request.
	//
	//    * state-reason-code - The reason code for the state change.
	//
	//    * state-reason-message - A message that describes the state change.
	//
	//    * subnet-id - The ID of the subnet for the instance.
	//
	//    * tag:<key> - The key/value combination of a tag assigned to the resource.
	//    Use the tag key in the filter name and the tag value as the filter value.
	//    For example, to find all resources that have a tag with the key Owner
	//    and the value TeamA, specify tag:Owner for the filter name and TeamA for
	//    the filter value.
	//
	//    * tag-key - The key of a tag assigned to the resource. Use this filter
	//    to find all resources that have a tag with a specific key, regardless
	//    of the tag value.
	//
	//    * tenancy - The tenancy of an instance (dedicated | default | host).
	//
	//    * virtualization-type - The virtualization type of the instance (paravirtual
	//    | hvm).
	//
	//    * vpc-id - The ID of the VPC that the instance is running in.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// The maximum number of results to return with a single call. This
	// value can be between 5 and 1000. You cannot specify this parameter and the
	// instance IDs parameter in the same call.
	MaxResults: Number // Optional
```



#### Tables schemas

```text
create table aws_ec2_instances
(
    id                                           integer
        primary key,
    account_id                                   text,
    region                                       text,
    ami_launch_index                             integer,
    architecture                                 text,
    capacity_reservation_id                      text,
    client_token                                 text,
    cpu_options_core_count                       integer,
    cpu_options_threads_per_core                 integer,
    ebs_optimized                                numeric,
    ena_support                                  numeric,
    hibernation_options_configured               numeric,
    hypervisor                                   text,
    iam_instance_profile_arn                     text,
    iam_instance_profile_id                      text,
    image_id                                     text,
    instance_id                                  text,
    instance_lifecycle                           text,
    instance_type                                text,
    kernel_id                                    text,
    key_name                                     text,
    launch_time                                  datetime,
    metadata_options_http_endpoint               text,
    metadata_options_http_put_response_hop_limit integer,
    metadata_options_http_tokens                 text,
    metadata_options_state                       text,
    monitoring_state                             text,
    outpost_arn                                  text,
    placement_affinity                           text,
    placement_availability_zone                  text,
    placement_group_name                         text,
    placement_host_id                            text,
    placement_host_resource_group_arn            text,
    placement_partition_number                   integer,
    placement_spread_domain                      text,
    placement_tenancy                            text,
    platform                                     text,
    private_dns_name                             text,
    private_ip_address                           text,
    public_dns_name                              text,
    public_ip_address                            text,
    ramdisk_id                                   text,
    root_device_name                             text,
    root_device_type                             text,
    source_dest_check                            numeric,
    spot_instance_request_id                     text,
    sriov_net_support                            text,
    state_code                                   integer,
    state_name                                   text,
    state_reason_code                            text,
    state_reason_message                         text,
    state_transition_reason                      text,
    subnet_id                                    text,
    virtualization_type                          text,
    vpc_id                                       text
);

create table aws_ec2_instance_block_device_mappings
(
    id                        integer
        primary key,
    instance_id               integer
        constraint fk_aws_ec2_instances_block_device_mappings
            references aws_ec2_instances
            on delete cascade,
    device_name               text,
    ebs_attach_time           datetime,
    ebs_delete_on_termination numeric,
    ebs_status                text,
    ebs_volume_id             text
);

create table aws_ec2_instance_capacity_reservation_specification_responses
(
    id                                                                  integer
        primary key,
    instance_id                                                         integer
        constraint fk_aws_ec2_instances_capacity_reservation_specification
            references aws_ec2_instances
            on delete cascade,
    capacity_reservation_preference                                     text,
    capacity_reservation_target_capacity_reservation_id                 text,
    capacity_reservation_target_capacity_reservation_resource_group_arn text
);

create table aws_ec2_instance_elastic_gpu_associations
(
    id                            integer
        primary key,
    instance_id                   integer
        constraint fk_aws_ec2_instances_elastic_gpu_associations
            references aws_ec2_instances
            on delete cascade,
    elastic_gpu_association_id    text,
    elastic_gpu_association_state text,
    elastic_gpu_association_time  text,
    elastic_gpu_id                text
);

create table aws_ec2_instance_elastic_inference_accelerator_associations
(
    id                                              integer
        primary key,
    instance_id                                     integer
        constraint fk_aws_ec2_instances_elastic_inference_accelerator_associations
            references aws_ec2_instances
            on delete cascade,
    elastic_inference_accelerator_arn               text,
    elastic_inference_accelerator_association_id    text,
    elastic_inference_accelerator_association_state text,
    elastic_inference_accelerator_association_time  datetime
);

create table aws_ec2_instance_group_identifiers
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_aws_ec2_instances_security_groups
            references aws_ec2_instances
            on delete cascade,
    group_id    text,
    group_name  text
);

create table aws_ec2_instance_license_configurations
(
    id                        integer
        primary key,
    instance_id               integer
        constraint fk_aws_ec2_instances_licenses
            references aws_ec2_instances
            on delete cascade,
    license_configuration_arn text
);

create table aws_ec2_instance_product_codes
(
    id                integer
        primary key,
    instance_id       integer
        constraint fk_aws_ec2_instances_product_codes
            references aws_ec2_instances
            on delete cascade,
    product_code_id   text,
    product_code_type text
);

create table aws_ec2_instance_network_interfaces
(
    id                               integer
        primary key,
    instance_id                      integer
        constraint fk_aws_ec2_instances_network_interfaces
            references aws_ec2_instances
            on delete cascade,
    association_carrier_ip           text,
    association_ip_owner_id          text,
    association_public_dns_name      text,
    association_public_ip            text,
    attachment_attach_time           datetime,
    attachment_attachment_id         text,
    attachment_delete_on_termination numeric,
    attachment_device_index          integer,
    attachment_status                text,
    description                      text,
    interface_type                   text,
    mac_address                      text,
    network_interface_id             text,
    owner_id                         text,
    private_dns_name                 text,
    private_ip_address               text,
    source_dest_check                numeric,
    status                           text,
    subnet_id                        text,
    vpc_id                           text
);

create table aws_ec2_instance_ipv6_addresses
(
    id                            integer
        primary key,
    instance_network_interface_id integer
        constraint fk_aws_ec2_instance_network_interfaces_ipv6_addresses
            references aws_ec2_instance_network_interfaces
            on delete cascade,
    ipv6_address                  text
);

create table aws_ec2_instance_private_ip_addresses
(
    id                            integer
        primary key,
    instance_network_interface_id integer
        constraint fk_aws_ec2_instance_network_interfaces_private_ip_addresses
            references aws_ec2_instance_network_interfaces
            on delete cascade,
    association_carrier_ip        text,
    association_ip_owner_id       text,
    association_public_dns_name   text,
    association_public_ip         text,
    "primary"                     numeric,
    private_dns_name              text,
    private_ip_address            text
);

create table aws_ec2_instance_tags
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_aws_ec2_instances_tags
            references aws_ec2_instances
            on delete cascade,
    key         text,
    value       text
);
```

