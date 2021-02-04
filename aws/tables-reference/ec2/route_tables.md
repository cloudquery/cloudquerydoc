# route\_tables

#### YAML config

```yaml
- name: ec2.route_tables
	RouteTableIds: // Optional. Default: Describes all your route tables.
		- "tableID" // One or more route table IDs.

	// One or more filters (Optional).
	//
	//    * association.route-table-association-id - The ID of an association ID
	//    for the route table.
	//
	//    * association.route-table-id - The ID of the route table involved in the
	//    association.
	//
	//    * association.subnet-id - The ID of the subnet involved in the association.
	//
	//    * association.main - Indicates whether the route table is the main route
	//    table for the VPC (true | false). Route tables that do not have an association
	//    ID are not returned in the response.
	//
	//    * owner-id - The ID of the AWS account that owns the route table.
	//
	//    * route-table-id - The ID of the route table.
	//
	//    * route.destination-cidr-block - The IPv4 CIDR range specified in a route
	//    in the table.
	//
	//    * route.destination-ipv6-cidr-block - The IPv6 CIDR range specified in
	//    a route in the route table.
	//
	//    * route.destination-prefix-list-id - The ID (prefix) of the AWS service
	//    specified in a route in the table.
	//
	//    * route.egress-only-internet-gateway-id - The ID of an egress-only Internet
	//    gateway specified in a route in the route table.
	//
	//    * route.gateway-id - The ID of a gateway specified in a route in the table.
	//
	//    * route.instance-id - The ID of an instance specified in a route in the
	//    table.
	//
	//    * route.nat-gateway-id - The ID of a NAT gateway.
	//
	//    * route.transit-gateway-id - The ID of a transit gateway.
	//
	//    * route.origin - Describes how the route was created. CreateRouteTable
	//    indicates that the route was automatically created when the route table
	//    was created; CreateRoute indicates that the route was manually added to
	//    the route table; EnableVgwRoutePropagation indicates that the route was
	//    propagated by route propagation.
	//
	//    * route.state - The state of a route in the route table (active | blackhole).
	//    The blackhole state indicates that the route's target isn't available
	//    (for example, the specified gateway isn't attached to the VPC, the specified
	//    NAT instance has been terminated, and so on).
	//
	//    * route.vpc-peering-connection-id - The ID of a VPC peering connection
	//    specified in a route in the table.
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
	//    * vpc-id - The ID of the VPC for the route table.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// The maximum number of results to return with a single call. 
	MaxResults: Number // Min 5
```

#### Tables schemas

```sql
create table aws_ec2_route_tables
(
    id             integer
        primary key,
    account_id     text,
    region         text,
    owner_id       text,
    route_table_id text,
    vpc_id         text
);

create table aws_ec2_route_table_routes
(
    id                              integer
        primary key,
    route_table_id                  integer
        constraint fk_aws_ec2_route_tables_routes
            references aws_ec2_route_tables
            on delete cascade,
    carrier_gateway_id              text,
    destination_cidr_block          text,
    destination_ipv6_cidr_block     text,
    destination_prefix_list_id      text,
    egress_only_internet_gateway_id text,
    gateway_id                      text,
    instance_id                     text,
    instance_owner_id               text,
    local_gateway_id                text,
    nat_gateway_id                  text,
    network_interface_id            text,
    origin                          text,
    state                           text,
    transit_gateway_id              text,
    vpc_peering_connection_id       text
)

create table aws_ec2_route_table_associations
(
    id                               integer
        primary key,
    route_table_id                   integer
        constraint fk_aws_ec2_route_tables_associations
            references aws_ec2_route_tables
            on delete cascade,
    association_state_state          text,
    association_state_status_message text,
    gateway_id                       text,
    main                             numeric,
    route_table_association_id       text,
    subnet_id                        text
);

create table aws_ec2_route_table_propagating_vgws
(
    id             integer
        primary key,
    route_table_id integer
        constraint fk_aws_ec2_route_tables_propagating_vgws
            references aws_ec2_route_tables
            on delete cascade,
    gateway_id     text
);

create table aws_ec2_route_table_tags
(
    id             integer
        primary key,
    route_table_id integer
        constraint fk_aws_ec2_route_tables_tags
            references aws_ec2_route_tables
            on delete cascade,
    key            text,
    value          text
);
```



