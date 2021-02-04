# clusters

#### YAML config

```yaml
- name: rds.clusters
	// The user-supplied DB cluster identifier. If this parameter is specified,
	// information from only the specific DB cluster is returned. This parameter
	// isn't case-sensitive.
	//
	// Constraints:
	//
	//    * If supplied, must match an existing DBClusterIdentifier.
	DBClusterIdentifier: String // Optional

	// A filter that specifies one or more DB clusters to describe.
	//
	// Supported filters:
	//
	//    * db-cluster-id - Accepts DB cluster identifiers and DB cluster Amazon
	//    Resource Names (ARNs). The results list will only include information
	//    about the DB clusters identified by these ARNs.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"
      
	// Optional Boolean parameter that specifies whether the output includes information
	// about clusters shared from other AWS accounts.
	IncludeShared: Bool // Optional

	// The maximum number of records to include in the response. If more records
	// exist than the specified MaxRecords value, a pagination token called a marker
	// is included in the response so you can retrieve the remaining results.
	//
	// Default: 100
	//
	// Constraints: Minimum 20, maximum 100.
	MaxRecords: Number // Optional
```

#### Tables schemas

```sql
create table aws_rds_clusters
(
    id                                                  integer
        primary key,
    account_id                                          text,
    region                                              text,
    activity_stream_kinesis_stream_name                 text,
    activity_stream_kms_key_id                          text,
    activity_stream_mode                                text,
    activity_stream_status                              text,
    allocated_storage                                   integer,
    availability_zones                                  text,
    backtrack_consumed_change_records                   integer,
    backtrack_window                                    integer,
    backup_retention_period                             integer,
    capacity                                            integer,
    character_set_name                                  text,
    clone_group_id                                      text,
    cluster_create_time                                 datetime,
    copy_tags_to_snapshot                               numeric,
    cross_account_clone                                 numeric,
    custom_endpoints                                    text,
    cluster_arn                                         text,
    cluster_identifier                                  text,
    cluster_parameter_group                             text,
    subnet_group                                        text,
    database_name                                       text,
    db_cluster_resource_id                              text,
    deletion_protection                                 numeric,
    earliest_backtrack_time                             datetime,
    earliest_restorable_time                            datetime,
    enabled_cloudwatch_logs_exports                     text,
    endpoint                                            text,
    engine                                              text,
    engine_mode                                         text,
    engine_version                                      text,
    global_write_forwarding_requested                   numeric,
    global_write_forwarding_status                      text,
    hosted_zone_id                                      text,
    http_endpoint_enabled                               numeric,
    iam_database_authentication_enabled                 numeric,
    kms_key_id                                          text,
    latest_restorable_time                              datetime,
    master_username                                     text,
    multi_az                                            numeric,
    percent_progress                                    text,
    port                                                integer,
    preferred_backup_window                             text,
    preferred_maintenance_window                        text,
    read_replica_identifiers                            text,
    reader_endpoint                                     text,
    replication_source_identifier                       text,
    scaling_configuration_info_auto_pause               numeric,
    scaling_configuration_info_max_capacity             integer,
    scaling_configuration_info_min_capacity             integer,
    scaling_configuration_info_seconds_until_auto_pause integer,
    scaling_configuration_info_timeout_action           text,
    status                                              text,
    storage_encrypted                                   numeric
);

create table aws_rds_cluster_domain_memberships
(
    id            integer
        primary key,
    cluster_id    integer
        constraint fk_aws_rds_clusters_domain_memberships
            references aws_rds_clusters
            on delete cascade,
    domain        text,
    fqdn          text,
    iam_role_name text,
    status        text
);

create table aws_rds_cluster_members
(
    id                             integer
        primary key,
    cluster_id                     integer
        constraint fk_aws_rds_clusters_cluster_members
            references aws_rds_clusters
            on delete cascade,
    cluster_parameter_group_status text,
    instance_identifier            text,
    is_cluster_writer              numeric,
    promotion_tier                 integer
);

create table aws_rds_cluster_option_group_statuses
(
    id                        integer
        primary key,
    cluster_id                integer
        constraint fk_aws_rds_clusters_cluster_option_group_memberships
            references aws_rds_clusters
            on delete cascade,
    cluster_option_group_name text,
    status                    text
);

create table aws_rds_cluster_roles
(
    id           integer
        primary key,
    cluster_id   integer
        constraint fk_aws_rds_clusters_associated_roles
            references aws_rds_clusters
            on delete cascade,
    feature_name text,
    role_arn     text,
    status       text
);

create table aws_rds_cluster_vpc_security_group_memberships
(
    id                    integer
        primary key,
    cluster_id            integer
        constraint fk_aws_rds_clusters_vpc_security_groups
            references aws_rds_clusters
            on delete cascade,
    status                text,
    vpc_security_group_id text
);
```



