# backups

#### YAML config

```yaml
- name: fsx.backups
	// IDs of the backups you want to retrieve (String). This overrides any filters.
	// If any IDs are not found, BackupNotFound will be thrown.
	BackupIds: // Optional
		- "id"

	// Filters structure. Supported names are file-system-id and backup-type.
  Filters: // Optional
    Name: "filter name"
    Values:
      - "Filter value"

	// Maximum number of backups to return in the response (integer). This parameter
	// value must be greater than 0. The number of items that Amazon FSx returns
	// is the minimum of the MaxResults parameter specified in the request and the
	// service's internal maximum number of items per page.
	MaxResults: Number // Optional
```

#### Tables schemas

```sql
create table aws_fsx_backups
(
    id                                        integer
        primary key,
    account_id                                text,
    region                                    text,
    backup_id                                 text,
    creation_time                             datetime,
    directory_information_active_directory_id text,
    directory_information_domain_name         text,
    failure_details_message                   text,
    kms_key_id                                text,
    lifecycle                                 text,
    progress_percent                          integer,
    resource_arn                              text,
    type                                      text
);

create table aws_fsx_backup_tags
(
    id        integer
        primary key,
    backup_id integer
        constraint fk_aws_fsx_backups_tags
            references aws_fsx_backups
            on delete cascade,
    key       text,
    value     text
);
```



