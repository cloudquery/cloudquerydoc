# clusters

#### YAML config

```text
- name: redshift.clusters
	// The unique identifier of a cluster whose properties you are requesting. This
	// parameter is case sensitive.
	//
	// The default is that all clusters defined for an account are returned.
	ClusterIdentifier: String // Optional
	
	// The maximum number of response records to return in each call. If the number
	// of remaining response records exceeds the specified MaxRecords value, a value
	// is returned in a marker field of the response. You can retrieve the next
	// set of records by retrying the command with the returned marker value.
	//
	// Default: 100
	//
	// Constraints: minimum 20, maximum 100.
	MaxRecords: Number // Optional

	// A tag key or keys for which you want to return all matching clusters that
	// are associated with the specified key or keys. For example, suppose that
	// you have clusters that are tagged with keys called owner and environment.
	// If you specify both of these tag keys in the request, Amazon Redshift returns
	// a response with the clusters that have either or both of these tag keys associated
	// with them.
	TagKeys: // Optional
		- "tag key"

	// A tag value or values for which you want to return all matching clusters
	// that are associated with the specified tag value or values. For example,
	// suppose that you have clusters that are tagged with values called admin and
	// test. If you specify both of these tag values in the request, Amazon Redshift
	// returns a response with the clusters that have either or both of these tag
	// values associated with them.
	TagValues: // Optional
		- "tag value"
```

#### Tables schemas

```text
create table aws_redshift_clusters
(
    id                                                             integer
        primary key,
    account_id                                                     text,
    region                                                         text,
    allow_version_upgrade                                          numeric,
    automated_snapshot_retention_period                            integer,
    availability_zone                                              text,
    cluster_availability_status                                    text,
    cluster_create_time                                            datetime,
    cluster_identifier                                             text,
    cluster_public_key                                             text,
    cluster_revision_number                                        text,
    cluster_snapshot_copy_status_destination_region                text,
    cluster_snapshot_copy_status_manual_snapshot_retention_period  integer,
    cluster_snapshot_copy_status_retention_period                  integer,
    cluster_snapshot_copy_status_snapshot_copy_grant_name          text,
    cluster_status                                                 text,
    cluster_subnet_group_name                                      text,
    cluster_version                                                text,
    db_name                                                        text,
    data_transfer_progress_current_rate_in_mega_bytes_per_second   real,
    data_transfer_progress_data_transferred_in_mega_bytes          integer,
    data_transfer_progress_elapsed_time_in_seconds                 integer,
    data_transfer_progress_estimated_time_to_completion_in_seconds integer,
    data_transfer_progress_status                                  text,
    data_transfer_progress_total_data_in_mega_bytes                integer,
    elastic_ip_status_elastic_ip                                   text,
    elastic_ip_status_status                                       text,
    elastic_resize_number_of_node_options                          text,
    encrypted                                                      numeric,
    endpoint_address                                               text,
    endpoint_port                                                  integer,
    enhanced_vpc_routing                                           numeric,
    expected_next_snapshot_schedule_time                           datetime,
    expected_next_snapshot_schedule_time_status                    text,
    hsm_status_hsm_client_certificate_identifier                   text,
    hsm_status_hsm_configuration_identifier                        text,
    hsm_status_status                                              text,
    kms_key_id                                                     text,
    maintenance_track_name                                         text,
    manual_snapshot_retention_period                               integer,
    master_username                                                text,
    modify_status                                                  text,
    next_maintenance_window_start_time                             datetime,
    node_type                                                      text,
    number_of_nodes                                                integer,
    pending_actions                                                text,
    pending_modified_values_automated_snapshot_retention_period    integer,
    pending_modified_values_cluster_identifier                     text,
    pending_modified_values_cluster_type                           text,
    pending_modified_values_cluster_version                        text,
    pending_modified_values_encryption_type                        text,
    pending_modified_values_enhanced_vpc_routing                   numeric,
    pending_modified_values_maintenance_track_name                 text,
    pending_modified_values_master_user_password                   text,
    pending_modified_values_node_type                              text,
    pending_modified_values_number_of_nodes                        integer,
    pending_modified_values_publicly_accessible                    numeric,
    preferred_maintenance_window                                   text,
    publicly_accessible                                            numeric,
    resize_info_allow_cancel_resize                                numeric,
    resize_info_resize_type                                        text,
    restore_status_current_restore_rate_in_mega_bytes_per_second   real,
    restore_status_elapsed_time_in_seconds                         integer,
    restore_status_estimated_time_to_completion_in_seconds         integer,
    restore_status_progress_in_mega_bytes                          integer,
    restore_status_snapshot_size_in_mega_bytes                     integer,
    restore_status_status                                          text,
    snapshot_schedule_identifier                                   text,
    snapshot_schedule_state                                        text,
    vpc_id                                                         text
);

create table aws_redshift_cluster_deferred_maintenance_windows
(
    id                           integer
        primary key,
    cluster_id                   integer
        constraint fk_aws_redshift_clusters_deferred_maintenance_windows
            references aws_redshift_clusters
            on delete cascade,
    defer_maintenance_end_time   datetime,
    defer_maintenance_identifier text,
    defer_maintenance_start_time datetime
);

create table aws_redshift_cluster_iam_roles
(
    id           integer
        primary key,
    cluster_id   integer
        constraint fk_aws_redshift_clusters_iam_roles
            references aws_redshift_clusters
            on delete cascade,
    apply_status text,
    iam_role_arn text
);

create table aws_redshift_cluster_nodes
(
    id                 integer
        primary key,
    cluster_id         integer
        constraint fk_aws_redshift_clusters_cluster_nodes
            references aws_redshift_clusters
            on delete cascade,
    node_role          text,
    private_ip_address text,
    public_ip_address  text
);

create table aws_redshift_cluster_parameter_group_statuses
(
    id                     integer
        primary key,
    cluster_id             integer
        constraint fk_aws_redshift_clusters_cluster_parameter_groups
            references aws_redshift_clusters
            on delete cascade,
    parameter_apply_status text,
    parameter_group_name   text
);

create table aws_redshift_cluster_security_group_memberships
(
    id                          integer
        primary key,
    cluster_id                  integer
        constraint fk_aws_redshift_clusters_cluster_security_groups
            references aws_redshift_clusters
            on delete cascade,
    cluster_security_group_name text,
    status                      text
);

create table aws_redshift_cluster_tags
(
    id         integer
        primary key,
    cluster_id integer
        constraint fk_aws_redshift_clusters_tags
            references aws_redshift_clusters
            on delete cascade,
    key        text,
    value      text
);

create table aws_redshift_cluster_vpc_security_group_memberships
(
    id                    integer
        primary key,
    cluster_id            integer
        constraint fk_aws_redshift_clusters_vpc_security_groups
            references aws_redshift_clusters
            on delete cascade,
    status                text,
    vpc_security_group_id text
);

create table aws_redshift_cluster_parameter_statuses
(
    id                                integer
        primary key,
    cluster_parameter_group_status_id integer
        constraint fk_aws_redshift_cluster_parameter_group_statuses_cluster_parameter_status_list
            references aws_redshift_cluster_parameter_group_statuses
            on delete cascade,
    parameter_apply_error_description text,
    parameter_apply_status            text,
    parameter_name                    text
);
```



