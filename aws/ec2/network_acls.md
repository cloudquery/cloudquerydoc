# network\_acls

#### YAML config

```text
- name: ec2.network_acls
	NetworkAclIds: // Optional. Default: Describes all your network ACLs.
		- "aclID" // One or more network ACL IDs.

	// One or more filters (Optional).
	//
	//    * association.association-id - The ID of an association ID for the ACL.
	//
	//    * association.network-acl-id - The ID of the network ACL involved in the
	//    association.
	//
	//    * association.subnet-id - The ID of the subnet involved in the association.
	//
	//    * default - Indicates whether the ACL is the default network ACL for the
	//    VPC.
	//
	//    * entry.cidr - The IPv4 CIDR range specified in the entry.
	//
	//    * entry.icmp.code - The ICMP code specified in the entry, if any.
	//
	//    * entry.icmp.type - The ICMP type specified in the entry, if any.
	//
	//    * entry.ipv6-cidr - The IPv6 CIDR range specified in the entry.
	//
	//    * entry.port-range.from - The start of the port range specified in the
	//    entry.
	//
	//    * entry.port-range.to - The end of the port range specified in the entry.
	//
	//    * entry.protocol - The protocol specified in the entry (tcp | udp | icmp
	//    or a protocol number).
	//
	//    * entry.rule-action - Allows or denies the matching traffic (allow | deny).
	//
	//    * entry.rule-number - The number of an entry (in other words, rule) in
	//    the set of ACL entries.
	//
	//    * network-acl-id - The ID of the network ACL.
	//
	//    * owner-id - The ID of the AWS account that owns the network ACL.
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
	//    * vpc-id - The ID of the VPC for the network ACL.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// The maximum number of results to return with a single call. 
	MaxResults: Number // Min 5
```

#### Tables schemas

```text
create table aws_ec2_network_acls
(
    id             integer
        primary key,
    account_id     text,
    region         text,
    is_default     numeric,
    network_acl_id text,
    owner_id       text,
    vpc_id         text
);

create table aws_ec2_network_acl_associations
(
    id                         integer
        primary key,
    network_acl_id             integer
        constraint fk_aws_ec2_network_acls_associations
            references aws_ec2_network_acls
            on delete cascade,
    network_acl_association_id text,
    subnet_id                  text
);

create table aws_ec2_network_acl_entries
(
    id                  integer
        primary key,
    network_acl_id      integer
        constraint fk_aws_ec2_network_acls_entries
            references aws_ec2_network_acls
            on delete cascade,
    cidr_block          text,
    egress              numeric,
    icmp_type_code_code integer,
    icmp_type_code_type integer,
    ipv6_cidr_block     text,
    port_range_from     integer,
    port_range_to       integer,
    protocol            text,
    rule_action         text,
    rule_number         integer
);

create table aws_ec2_network_acl_tags
(
    id             integer
        primary key,
    network_acl_id integer
        constraint fk_aws_ec2_network_acls_tags
            references aws_ec2_network_acls
            on delete cascade,
    key            text,
    value          text
);
```



