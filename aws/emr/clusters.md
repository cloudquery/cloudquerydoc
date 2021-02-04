# clusters

#### YAML config

```text
- name: emr.clusters
	// The cluster state filters to apply when listing clusters.
	ClusterStates: // Optional
		- "state filter"
```

#### Tables Schema

```text
create table aws_emr_clusters
(
    id                        integer
        primary key,
    account_id                text,
    region                    text,
    cluster_arn               text,
    name                      text,
    normalized_instance_hours integer,
    outpost_arn               text
);

create table aws_emr_cluster_statuses
(
    id                          integer
        primary key,
    cluster_id                  integer
        constraint fk_aws_emr_clusters_status
            references aws_emr_clusters
            on delete cascade,
    state                       text,
    state_change_reason_code    text,
    state_change_reason_message text,
    timeline_creation_date_time datetime,
    timeline_end_date_time      datetime,
    timeline_ready_date_time    datetime
);
```



#### 

