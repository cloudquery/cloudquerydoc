# vpc\_peering\_connections

#### YAML config

```yaml
providers:
	- name: aws
		resources:
		- name: ec2.vpc_peering_connections
      Filters: // Optional
	// One or more filters.
	//
	//    * accepter-vpc-info.cidr-block - The IPv4 CIDR block of the accepter VPC.
	//
	//    * accepter-vpc-info.owner-id - The AWS account ID of the owner of the
	//    accepter VPC.
	//
	//    * accepter-vpc-info.vpc-id - The ID of the accepter VPC.
	//
	//    * expiration-time - The expiration date and time for the VPC peering connection.
	//
	//    * requester-vpc-info.cidr-block - The IPv4 CIDR block of the requester's
	//    VPC.
	//
	//    * requester-vpc-info.owner-id - The AWS account ID of the owner of the
	//    requester VPC.
	//
	//    * requester-vpc-info.vpc-id - The ID of the requester VPC.
	//
	//    * status-code - The status of the VPC peering connection (pending-acceptance
	//    | failed | expired | provisioning | active | deleting | deleted | rejected).
	//
	//    * status-message - A message that provides more information about the
	//    status of the VPC peering connection, if applicable.
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
	//    * vpc-peering-connection-id - The ID of the VPC peering connection.  
      - Name: "filter name"
        Values:
        - "Filter value"
```

#### Tables schemas

```sql
create table aws_ec2_vpc_peering_connections
(
    id                                                                  integer
        primary key,
    account_id                                                          text,
    region                                                              text,
    accepter_cidr_block                                                 text,
    accepter_owner_id                                                   text,
    accepter_option_allow_dns_resolution_from_remote_vpc                numeric,
    accepter_option_allow_egress_from_local_classic_link_to_remote_vpc  numeric,
    accepter_option_allow_egress_from_local_vpc_to_remote_classic_link  numeric,
    accepter_region                                                     text,
    accepter_vpc_id                                                     text,
    expiration_time                                                     datetime,
    requester_cidr_block                                                text,
    requester_owner_id                                                  text,
    requester_option_allow_dns_resolution_from_remote_vpc               numeric,
    requester_option_allow_egress_from_local_classic_link_to_remote_vpc numeric,
    requester_option_allow_egress_from_local_vpc_to_remote_classic_link numeric,
    requester_region                                                    text,
    requester_vpc_id                                                    text,
    status_code                                                         text,
    status_message                                                      text,
    vpc_peering_connection_id                                           text
);

create table aws_ec2_vpc_peering_connection_tags
(
    id                        integer
        primary key,
    vpc_peering_connection_id integer
        constraint fk_aws_ec2_vpc_peering_connections_tags
            references aws_ec2_vpc_peering_connections
            on delete cascade,
    key                       text,
    value                     text
);

create table aws_ec2_vpc_peering_connection_requester_ipv6_cidr_blocks
(
    id                        integer
        primary key,
    vpc_peering_connection_id integer
        constraint fk_aws_ec2_vpc_peering_connections_requester_ipv6_cidr_block_set
            references aws_ec2_vpc_peering_connections
            on delete cascade,
    ipv6_cidr_block           text
);

create table aws_ec2_vpc_peering_connection_requester_cidr_blocks
(
    id                        integer
        primary key,
    vpc_peering_connection_id integer
        constraint fk_aws_ec2_vpc_peering_connections_requester_cidr_block_set
            references aws_ec2_vpc_peering_connections
            on delete cascade,
    cidr_block                text
);

create table aws_ec2_vpc_peering_connection_accepter_ipv6_cidr_blocks
(
    id                        integer
        primary key,
    vpc_peering_connection_id integer
        constraint fk_aws_ec2_vpc_peering_connections_accepter_ipv6_cidr_block_set
            references aws_ec2_vpc_peering_connections
            on delete cascade,
    ipv6_cidr_block           text
);

create table aws_ec2_vpc_peering_connection_accepter_cidr_blocks
(
    id                        integer
        primary key,
    vpc_peering_connection_id integer
        constraint fk_aws_ec2_vpc_peering_connections_accepter_cidr_block_set
            references aws_ec2_vpc_peering_connections
            on delete cascade,
    cidr_block                text
);
```

