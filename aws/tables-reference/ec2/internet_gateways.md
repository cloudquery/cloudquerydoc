# internet\_gateways

#### YAML config

```yaml
- name: ec2.internet_gateways
	InternetGatewayIds: // Optional. Default: Describes all your internet gateways.
		- "gateway_id" // One or more internet gateway IDs.
	
	// One or more filters (Optional).
	//
	//    * attachment.state - The current state of the attachment between the gateway
	//    and the VPC (available). Present only if a VPC is attached.
	//
	//    * attachment.vpc-id - The ID of an attached VPC.
	//
	//    * internet-gateway-id - The ID of the Internet gateway.
	//
	//    * owner-id - The ID of the AWS account that owns the internet gateway.
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
  
	// The maximum number of results to return with a single call. 
	MaxResults: Number // Min 5
```



#### Tables schemas

```sql
create table aws_ec2_internet_gateways
(
    id                  integer
        primary key,
    account_id          text,
    region              text,
    internet_gateway_id text,
    owner_id            text
);

create table aws_ec2_internet_gateway_attachments
(
    id                  integer
        primary key,
    internet_gateway_id integer
        constraint fk_aws_ec2_internet_gateways_attachments
            references aws_ec2_internet_gateways
            on delete cascade,
    state               text,
    vpc_id              text
)

create table aws_ec2_internet_gateway_tags
(
    id                  integer
        primary key,
    internet_gateway_id integer
        constraint fk_aws_ec2_internet_gateways_tags
            references aws_ec2_internet_gateways
            on delete cascade,
    key                 text,
    value               text
);
```



