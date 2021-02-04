# flow\_logs



#### YAML config

```yaml
- name: ec2.flow_logs
	// One or more filters (Optional).
	//
	//    * deliver-log-status - The status of the logs delivery (SUCCESS | FAILED).
	//
	//    * log-destination-type - The type of destination to which the flow log
	//    publishes data. Possible destination types include cloud-watch-logs and
	//    S3.
	//
	//    * flow-log-id - The ID of the flow log.
	//
	//    * log-group-name - The name of the log group.
	//
	//    * resource-id - The ID of the VPC, subnet, or network interface.
	//
	//    * traffic-type - The type of traffic (ACCEPT | REJECT | ALL).
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
create table aws_ec2_flow_logs
(
    id                          integer
        primary key,
    account_id                  text,
    region                      text,
    creation_time               datetime,
    deliver_logs_error_message  text,
    deliver_logs_permission_arn text,
    deliver_logs_status         text,
    flow_log_id                 text,
    flow_log_status             text,
    log_destination             text,
    log_destination_type        text,
    log_format                  text,
    log_group_name              text,
    max_aggregation_interval    integer,
    resource_id                 text,
    traffic_type                text
);

create table aws_ec2_flow_log_tags
(
    id          integer
        primary key,
    flow_log_id integer
        constraint fk_aws_ec2_flow_logs_tags
            references aws_ec2_flow_logs
            on delete cascade,
    key         text,
    value       text
);
```

