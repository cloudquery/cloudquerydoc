# vpcs

#### YAML config

```yaml
providers:
	- name: aws
		region: us-east-1 // required
		resources:
		- name: ec2.vpcs
      Filters: // Optional
	// One or more filters.
	//
	//    * cidr - The primary IPv4 CIDR block of the VPC. The CIDR block you specify
	//    must exactly match the VPC's CIDR block for information to be returned
	//    for the VPC. Must contain the slash followed by one or two digits (for
	//    example, /28).
	//
	//    * cidr-block-association.cidr-block - An IPv4 CIDR block associated with
	//    the VPC.
	//
	//    * cidr-block-association.association-id - The association ID for an IPv4
	//    CIDR block associated with the VPC.
	//
	//    * cidr-block-association.state - The state of an IPv4 CIDR block associated
	//    with the VPC.
	//
	//    * dhcp-options-id - The ID of a set of DHCP options.
	//
	//    * ipv6-cidr-block-association.ipv6-cidr-block - An IPv6 CIDR block associated
	//    with the VPC.
	//
	//    * ipv6-cidr-block-association.ipv6-pool - The ID of the IPv6 address pool
	//    from which the IPv6 CIDR block is allocated.
	//
	//    * ipv6-cidr-block-association.association-id - The association ID for
	//    an IPv6 CIDR block associated with the VPC.
	//
	//    * ipv6-cidr-block-association.state - The state of an IPv6 CIDR block
	//    associated with the VPC.
	//
	//    * isDefault - Indicates whether the VPC is the default VPC.
	//
	//    * owner-id - The ID of the AWS account that owns the VPC.
	//
	//    * state - The state of the VPC (pending | available).
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
	//    * vpc-id - The ID of the VPC.      
      - Name: "filter name"
        Values:
        - "Filter value"
```

#### Tables schemas

```sql
create table aws_ec2_vpcs
(
    id               integer
        primary key,
    account_id       text,
    region           text,
    cidr_block       text,
    dhcp_options_id  text,
    instance_tenancy text,
    is_default       numeric,
    owner_id         text,
    state            text,
    vpc_id           text
);

create table aws_ec2_vpc_tags
(
    id     integer
        primary key,
    vpc_id integer
        constraint fk_aws_ec2_vpcs_tags
            references aws_ec2_vpcs
            on delete cascade,
    key    text,
    value  text
);

create table aws_ec2_vpc_ipv6_cidr_block_associations
(
    id                                    integer
        primary key,
    vpc_id                                integer
        constraint fk_aws_ec2_vpcs_ipv6_cidr_block_association_set
            references aws_ec2_vpcs
            on delete cascade,
    association_id                        text,
    ipv6_cidr_block                       text,
    ipv_6_cidr_block_state_state          text,
    ipv_6_cidr_block_state_status_message text,
    ipv6_pool                             text,
    network_border_group                  text
);

create table aws_ec2_vpc_cidr_block_associations
(
    id                              integer
        primary key,
    vpc_id                          integer
        constraint fk_aws_ec2_vpcs_cidr_block_association_set
            references aws_ec2_vpcs
            on delete cascade,
    association_id                  text,
    cidr_block                      text,
    cidr_block_state_state          text,
    cidr_block_state_status_message text
);
```

