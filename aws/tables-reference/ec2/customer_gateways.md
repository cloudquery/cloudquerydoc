# customer\_gateways

#### YAML config

```yaml
- name: ec2.customer_gateways
  CustomerGatewayIds: // Optional. Default: Describes all your customer gateways.
    - "gateway_id" // One or more customer gateway IDs.

	// One or more filters (Optional).
	//
	//    * bgp-asn - The customer gateway's Border Gateway Protocol (BGP) Autonomous
	//    System Number (ASN).
	//
	//    * customer-gateway-id - The ID of the customer gateway.
	//
	//    * ip-address - The IP address of the customer gateway's Internet-routable
	//    external interface.
	//
	//    * state - The state of the customer gateway (pending | available | deleting
	//    | deleted).
	//
	//    * type - The type of customer gateway. Currently, the only supported type
	//    is ipsec.1.
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
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"
```

#### Tables schemas

```sql
create table aws_ec2_customer_gateways
(
    id                  integer
        primary key,
    account_id          text,
    region              text,
    bgp_asn             text,
    certificate_arn     text,
    customer_gateway_id text,
    device_name         text,
    ip_address          text,
    state               text,
    type                text
);

create table aws_ec2_customer_gateway_tags
(
    id                  integer
        primary key,
    customer_gateway_id integer
        constraint fk_aws_ec2_customer_gateways_tags
            references aws_ec2_customer_gateways
            on delete cascade,
    key                 text,
    value               text
);
```

