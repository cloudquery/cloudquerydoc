# environments

#### YAML config

```text
- name: elasticbeanstalk.environments
	// If specified, AWS Elastic Beanstalk restricts the returned descriptions to
	// include only those that are associated with this application.
	ApplicationName: String // Optional

	// If specified, AWS Elastic Beanstalk restricts the returned descriptions to
	// include only those that have the specified IDs.
	EnvironmentIds: // Optional
		- "id"

	// If specified, AWS Elastic Beanstalk restricts the returned descriptions to
	// include only those that have the specified names.
	EnvironmentNames: // Optional
		- "name"

	// Indicates whether to include deleted environments:
	//
	// true: Environments that have been deleted after IncludedDeletedBackTo are
	// displayed.
	//
	// false: Do not include deleted environments.
	IncludeDeleted: Bool // Optional

	// For a paginated request. Specify a maximum number of environments to include
	// in each response.
	//
	// If no MaxRecords is specified, all available environments are retrieved in
	// a single response.
	MaxRecords: Number // Optional

	// If specified, AWS Elastic Beanstalk restricts the returned descriptions to
	// include only those that are associated with this application version.
	VersionLabel: String // Optional
```

#### Tables schemas

```text
create table aws_elasticbeanstalk_environments
(
    id                              integer
        primary key,
    account_id                      text,
    region                          text,
    abortable_operation_in_progress numeric,
    application_name                text,
    cname                           text,
    date_created                    datetime,
    date_updated                    datetime,
    description                     text,
    endpoint_url                    text,
    environment_arn                 text,
    environment_id                  text,
    environment_name                text,
    health                          text,
    health_status                   text,
    operations_role                 text,
    platform_arn                    text,
    solution_stack_name             text,
    status                          text,
    template_name                   text,
    tier_name                       text,
    tier_type                       text,
    tier_version                    text,
    version_label                   text
);

create table aws_elasticbeanstalk_environment_links
(
    id               integer
        primary key,
    environment_id   integer
        constraint fk_aws_elasticbeanstalk_environments_environment_links
            references aws_elasticbeanstalk_environments
            on delete cascade,
    environment_name text,
    link_name        text
);

create table aws_elasticbeanstalk_environment_resources
(
    id             integer
        primary key,
    environment_id integer
        constraint fk_aws_elasticbeanstalk_environments_resources
            references aws_elasticbeanstalk_environments
            on delete cascade
);

create table aws_elasticbeanstalk_environment_load_balancers
(
    id                      integer
        primary key,
    environment_resource_id integer
        constraint fk_aws_elasticbeanstalk_environment_resources_load_balancer
            references aws_elasticbeanstalk_environment_resources
            on delete cascade,
    domain                  text,
    load_balancer_name      text
);

create table aws_elasticbeanstalk_environment_listeners
(
    id                           integer
        primary key,
    environment_load_balancer_id integer
        constraint fk_aws_elasticbeanstalk_environment_load_balancers_listeners
            references aws_elasticbeanstalk_environment_load_balancers
            on delete cascade,
    port                         integer,
    protocol                     text
);
```

