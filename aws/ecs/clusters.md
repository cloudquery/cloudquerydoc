# clusters

#### YAML config

```text
- name: ecs.clusters
	// A list of up to 100 cluster names or full cluster Amazon Resource Name (ARN)
	// entries. 
	Clusters: // Optional. If you do not specify a cluster, the default cluster is assumed.
		- "cluster"

	// Optional. Whether to include additional information about your clusters in the response.
	// If this field is omitted, the attachments, statistics, and tags are not included.
	//
	// If ATTACHMENTS is specified, the attachments for the container instances
	// or tasks within the cluster are included.
	//
	// If SETTINGS is specified, the settings for the cluster are included.
	//
	// If STATISTICS is specified, the following additional information, separated
	// by launch type, is included:
	//
	//    * runningEC2TasksCount
	//
	//    * runningFargateTasksCount
	//
	//    * pendingEC2TasksCount
	//
	//    * pendingFargateTasksCount
	//
	//    * activeEC2ServiceCount
	//
	//    * activeFargateServiceCount
	//
	//    * drainingEC2ServiceCount
	//
	//    * drainingFargateServiceCount
	//
	// If TAGS is specified, the metadata tags associated with the cluster are included.
	Include: // Optional
		- "additional info"
```

#### Tables schemas

```text
create table aws_ecs_clusters
(
    id                                   integer
        primary key,
    account_id                           text,
    region                               text,
    active_services_count                integer,
    attachments_status                   text,
    capacity_providers                   text,
    cluster_arn                          text,
    cluster_name                         text,
    pending_tasks_count                  integer,
    registered_container_instances_count integer,
    running_tasks_count                  integer,
    status                               text
);

create table aws_ecs_cluster_capacity_provider_strategy_items
(
    id                integer
        primary key,
    cluster_id        integer
        constraint fk_aws_ecs_clusters_default_capacity_provider_strategy
            references aws_ecs_clusters
            on delete cascade,
    base              integer,
    capacity_provider text,
    weight            integer
);

create table aws_ecs_cluster_key_value_pairs
(
    id         integer
        primary key,
    cluster_id integer
        constraint fk_aws_ecs_clusters_statistics
            references aws_ecs_clusters
            on delete cascade,
    name       text,
    value      text
);

create table aws_ecs_cluster_settings
(
    id         integer
        primary key,
    cluster_id integer
        constraint fk_aws_ecs_clusters_settings
            references aws_ecs_clusters
            on delete cascade,
    name       text,
    value      text
);

create table aws_ecs_cluster_tags
(
    id         integer
        primary key,
    cluster_id integer
        constraint fk_aws_ecs_clusters_tags
            references aws_ecs_clusters
            on delete cascade,
    key        text,
    value      text
);
```



