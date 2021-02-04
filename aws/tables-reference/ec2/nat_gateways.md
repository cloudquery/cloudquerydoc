# nat\_gateways

#### YAML config

```yaml
- name: ec2.nat_gateways
	NatGatewayIds: // Optional. 
		- "gateway_id" // One or more NAT gateway IDs.
		
	// One or more filters (Optional).
	//
	//    * nat-gateway-id - The ID of the NAT gateway.
	//
	//    * state - The state of the NAT gateway (pending | failed | available |
	//    deleting | deleted).
	//
	//    * subnet-id - The ID of the subnet in which the NAT gateway resides.
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
	//    * vpc-id - The ID of the VPC in which the NAT gateway resides.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// The maximum number of results to return with a single call. 
	MaxResults: Number // Min 5
```

#### Tables schemas

```sql
create table aws_ec2_nat_gateways
(
    id                                   integer
        primary key,
    account_id                           text,
    region                               text,
    create_time                          datetime,
    delete_time                          datetime,
    failure_code                         text,
    failure_message                      text,
    nat_gateway_id                       text,
    provisioned_bandwidth_provision_time datetime,
    provisioned_bandwidth_provisioned    text,
    provisioned_bandwidth_request_time   datetime,
    provisioned_bandwidth_requested      text,
    provisioned_bandwidth_status         text,
    state                                text,
    subnet_id                            text,
    vpc_id                               text
);

create table aws_ec2_nat_gateway_addresses
(
    id                   integer
        primary key,
    nat_gateway_id       integer
        constraint fk_aws_ec2_nat_gateways_nat_gateway_addresses
            references aws_ec2_nat_gateways
            on delete cascade,
    allocation_id        text,
    network_interface_id text,
    private_ip           text,
    public_ip            text
);

create table aws_ec2_nat_gateway_tags
(
    id             integer
        primary key,
    nat_gateway_id integer
        constraint fk_aws_ec2_nat_gateways_tags
            references aws_ec2_nat_gateways
            on delete cascade,
    key            text,
    value          text
);
```

