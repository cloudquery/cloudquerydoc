# load\_balancers

#### YAML config

```text
- name: elbv2.load_balancers
	// The Amazon Resource Names (ARN) of the load balancers. You can specify up
	// to 20 load balancers in a single call.
	LoadBalancerArns: // Optional
		- "load balancer"

	// The names of the load balancers.
	Names: // Optional
		- "LB name"

	// The maximum number of results to return with this call.
	PageSize: Number // Optional
```

#### Tables schemas

```text
create table aws_elbv2_load_balancers
(
    id                       integer
        primary key,
    account_id               text,
    region                   text,
    canonical_hosted_zone_id text,
    created_time             datetime,
    customer_owned_ipv4_pool text,
    dns_name                 text,
    ip_address_type          text,
    load_balancer_arn        text,
    load_balancer_name       text,
    scheme                   text,
    security_groups          text,
    state_code               text,
    state_reason             text,
    type                     text,
    vpc_id                   text
);

create table aws_elbv2_load_balancer_availability_zones
(
    id               integer
        primary key,
    load_balancer_id integer
        constraint fk_aws_elbv2_load_balancers_availability_zones
            references aws_elbv2_load_balancers
            on delete cascade,
    outpost_id       text,
    subnet_id        text,
    zone_name        text
);

create table aws_elbv2_load_balancer_addresses
(
    id                                 integer
        primary key,
    load_balancer_availability_zone_id integer
        constraint fk_aws_elbv2_load_balancer_availability_zones_load_balancer_addresses
            references aws_elbv2_load_balancer_availability_zones
            on delete cascade,
    allocation_id                      text,
    ip_address                         text,
    private_ipv4_address               text
);
```



