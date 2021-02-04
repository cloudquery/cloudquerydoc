# subnets

#### YAML config

```yaml
providers:
	- name: aws
		region: us-east-1 // required
		resources:
		- name: ec2.subnets
      Filters: // Optional
	// One or more filters.
	//
	//    * availability-zone - The Availability Zone for the subnet. You can also
	//    use availabilityZone as the filter name.
	//
	//    * availability-zone-id - The ID of the Availability Zone for the subnet.
	//    You can also use availabilityZoneId as the filter name.
	//
	//    * available-ip-address-count - The number of IPv4 addresses in the subnet
	//    that are available.
	//
	//    * cidr-block - The IPv4 CIDR block of the subnet. The CIDR block you specify
	//    must exactly match the subnet's CIDR block for information to be returned
	//    for the subnet. You can also use cidr or cidrBlock as the filter names.
	//
	//    * default-for-az - Indicates whether this is the default subnet for the
	//    Availability Zone. You can also use defaultForAz as the filter name.
	//
	//    * ipv6-cidr-block-association.ipv6-cidr-block - An IPv6 CIDR block associated
	//    with the subnet.
	//
	//    * ipv6-cidr-block-association.association-id - An association ID for an
	//    IPv6 CIDR block associated with the subnet.
	//
	//    * ipv6-cidr-block-association.state - The state of an IPv6 CIDR block
	//    associated with the subnet.
	//
	//    * owner-id - The ID of the AWS account that owns the subnet.
	//
	//    * state - The state of the subnet (pending | available).
	//
	//    * subnet-arn - The Amazon Resource Name (ARN) of the subnet.
	//
	//    * subnet-id - The ID of the subnet.
	//
	//    * tag:<key> - The key/value combination of a tag assigned to the resource.
	//    Use the tag key in the filter name and the tag value as the filter value.
	//    For example, to find all resources that have a tag with the key Owner
	//    and the value TeamA, specify tag:Owner for the filter name and TeamA for
	//    the filter value.
	//
	//    * tag-key - The key of a tag assigned to the resource. Use this filter
	//    to find all resources assigned a tag with a specific key, regardless of
	//    the tag value.
	//
	//    * vpc-id - The ID of the VPC for the subnet.
      - Name: "filter name"
        Values:
        - "Filter value"
```

#### Tables schemas

```sql
create table aws_ec2_subnets
(
    id                              integer
        primary key,
    account_id                      text,
    region                          text,
    assign_ipv6_address_on_creation numeric,
    availability_zone               text,
    availability_zone_id            text,
    available_ip_address_count      integer,
    cidr_block                      text,
    customer_owned_ipv4_pool        text,
    default_for_az                  numeric,
    map_customer_owned_ip_on_launch numeric,
    map_public_ip_on_launch         numeric,
    outpost_arn                     text,
    owner_id                        text,
    state                           text,
    subnet_arn                      text,
    subnet_id                       text,
    vpc_id                          text
);

create table aws_ec2_subnet_tags
(
    id        integer
        primary key,
    subnet_id integer
        constraint fk_aws_ec2_subnets_tags
            references aws_ec2_subnets
            on delete cascade,
    key       text,
    value     text
);

create table aws_ec2_subnet_ipv6_cidr_block_associations
(
    id                                    integer
        primary key,
    subnet_id                             integer
        constraint fk_aws_ec2_subnets_ipv6_cidr_block_association_set
            references aws_ec2_subnets
            on delete cascade,
    association_id                        text,
    ipv6_cidr_block                       text,
    ipv_6_cidr_block_state_state          text,
    ipv_6_cidr_block_state_status_message text
);
```

