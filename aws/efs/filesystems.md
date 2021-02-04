# filesystems

#### YAML config

```text
- name: efs.filesystems
	// (Optional) Restricts the list to the file system with this creation token
	// (String). You specify a creation token when you create an Amazon EFS file
	// system.
	CreationToken: String

	// (Optional) ID of the file system whose description you want to retrieve (String).
	FileSystemId: String

	// (Optional) Opaque pagination token returned from a previous DescribeFileSystems
	// operation (String). If present, specifies to continue the list from where
	// the returning call had left off.
	Marker: String

	// (Optional) Specifies the maximum number of file systems to return in the
	// response (integer). This number is automatically set to 100. The response
	// is paginated at 100 per page if you have more than 100 file systems.
	MaxItems: Number
```

#### Tables schemas

```text
create table aws_efs_file_system_descriptions
(
    id                              integer
        primary key,
    account_id                      text,
    region                          text,
    creation_time                   datetime,
    creation_token                  text,
    encrypted                       numeric,
    file_system_arn                 text,
    file_system_id                  text,
    kms_key_id                      text,
    life_cycle_state                text,
    name                            text,
    number_of_mount_targets         integer,
    owner_id                        text,
    performance_mode                text,
    provisioned_throughput_in_mibps real,
    size_in_bytes_timestamp         datetime,
    size_in_bytes_value             integer,
    size_in_bytes_value_in_ia       integer,
    size_in_bytes_value_in_standard integer,
    throughput_mode                 text
);

create table aws_efs_file_system_description_tags
(
    id                         integer
        primary key,
    file_system_description_id integer
        constraint fk_aws_efs_file_system_descriptions_tags
            references aws_efs_file_system_descriptions
            on delete cascade,
    key                        text,
    value                      text
);
```

