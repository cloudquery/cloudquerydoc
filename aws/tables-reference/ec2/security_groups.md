# security\_groups

#### YAML config

```yaml
- name: ec2.security_groups
	GroupIds: // Optional. Default: Describes all your security groups.
		- "id" // The IDs of the security groups. Required for security groups in a nondefault VPC.

	// Optional. [EC2-Classic and default VPC only] The names of the security groups. You
	// can specify either the security group name or the security group ID. For
	// security groups in a nondefault VPC, use the group-name filter to describe
	// security groups by name.	
	GroupNames: //Default: Describes all your security groups.
		- "nameOrID" 

	// The filters (Optional). 
	// If using multiple filters for rules, the results include security
	// groups for which any combination of rules - not necessarily a single rule
	// - match all filters.
	//
	//    * description - The description of the security group.
	//
	//    * egress.ip-permission.cidr - An IPv4 CIDR block for an outbound security
	//    group rule.
	//
	//    * egress.ip-permission.from-port - For an outbound rule, the start of
	//    port range for the TCP and UDP protocols, or an ICMP type number.
	//
	//    * egress.ip-permission.group-id - The ID of a security group that has
	//    been referenced in an outbound security group rule.
	//
	//    * egress.ip-permission.group-name - The name of a security group that
	//    has been referenced in an outbound security group rule.
	//
	//    * egress.ip-permission.ipv6-cidr - An IPv6 CIDR block for an outbound
	//    security group rule.
	//
	//    * egress.ip-permission.prefix-list-id - The ID of a prefix list to which
	//    a security group rule allows outbound access.
	//
	//    * egress.ip-permission.protocol - The IP protocol for an outbound security
	//    group rule (tcp | udp | icmp or a protocol number).
	//
	//    * egress.ip-permission.to-port - For an outbound rule, the end of port
	//    range for the TCP and UDP protocols, or an ICMP code.
	//
	//    * egress.ip-permission.user-id - The ID of an AWS account that has been
	//    referenced in an outbound security group rule.
	//
	//    * group-id - The ID of the security group.
	//
	//    * group-name - The name of the security group.
	//
	//    * ip-permission.cidr - An IPv4 CIDR block for an inbound security group
	//    rule.
	//
	//    * ip-permission.from-port - For an inbound rule, the start of port range
	//    for the TCP and UDP protocols, or an ICMP type number.
	//
	//    * ip-permission.group-id - The ID of a security group that has been referenced
	//    in an inbound security group rule.
	//
	//    * ip-permission.group-name - The name of a security group that has been
	//    referenced in an inbound security group rule.
	//
	//    * ip-permission.ipv6-cidr - An IPv6 CIDR block for an inbound security
	//    group rule.
	//
	//    * ip-permission.prefix-list-id - The ID of a prefix list from which a
	//    security group rule allows inbound access.
	//
	//    * ip-permission.protocol - The IP protocol for an inbound security group
	//    rule (tcp | udp | icmp or a protocol number).
	//
	//    * ip-permission.to-port - For an inbound rule, the end of port range for
	//    the TCP and UDP protocols, or an ICMP code.
	//
	//    * ip-permission.user-id - The ID of an AWS account that has been referenced
	//    in an inbound security group rule.
	//
	//    * owner-id - The AWS account ID of the owner of the security group.
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
	//    * vpc-id - The ID of the VPC specified when the security group was created.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// The maximum number of results to return with a single call. 
	MaxResults: Number // Min 5
```

#### Tables schemas

```sql
create table aws_ec2_security_groups
(
    id          integer
        primary key,
    account_id  text,
    region      text,
    description text,
    group_id    text,
    group_name  text,
    owner_id    text,
    vpc_id      text
);

create table aws_ec2_security_group_ip_permissions
(
    id                integer
        primary key,
    security_group_id integer
        constraint fk_aws_ec2_security_groups_ip_permissions
            references aws_ec2_security_groups
            on delete cascade,
    from_port         integer,
    ip_protocol       text,
    to_port           integer
);

create table aws_ec2_security_group_ip_ranges
(
    id                              integer
        primary key,
    security_group_ip_permission_id integer
        constraint fk_aws_ec2_security_group_ip_permissions_ip_ranges
            references aws_ec2_security_group_ip_permissions
            on delete cascade,
    cidr_ip                         text,
    description                     text
);

create table aws_ec2_security_group_ipv6_ranges
(
    id                              integer
        primary key,
    security_group_ip_permission_id integer
        constraint fk_aws_ec2_security_group_ip_permissions_ipv6_ranges
            references aws_ec2_security_group_ip_permissions
            on delete cascade,
    cidr_ipv6                       text,
    description                     text
);

create table aws_ec2_security_group_prefix_list_ids
(
    id                              integer
        primary key,
    security_group_ip_permission_id integer
        constraint fk_aws_ec2_security_group_ip_permissions_prefix_list_ids
            references aws_ec2_security_group_ip_permissions
            on delete cascade,
    description                     text,
    prefix_list_id                  text
);

create table aws_ec2_security_group_user_id_group_pairs
(
    id                              integer
        primary key,
    security_group_ip_permission_id integer
        constraint fk_aws_ec2_security_group_ip_permissions_user_id_group_pairs
            references aws_ec2_security_group_ip_permissions
            on delete cascade,
    description                     text,
    group_id                        text,
    group_name                      text,
    peering_status                  text,
    user_id                         text,
    vpc_id                          text,
    vpc_peering_connection_id       text
);

create table aws_ec2_security_group_tags
(
    id                integer
        primary key,
    security_group_id integer
        constraint fk_aws_ec2_security_groups_tags
            references aws_ec2_security_groups
            on delete cascade,
    key               text,
    value             text
);
```



