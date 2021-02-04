# buckets

#### YAML config

```yaml
- name: storage.buckets
  prefix: "" // optional: filter bucket by prefix
```

#### Tables schemas:

```sql
create table gcp_storage_buckets
(
    id                                      integer
        primary key,
    project_id                              text,
    billing_requester_pays                  numeric,
    default_event_based_hold                numeric,
    encryption_default_kms_key_name         text,
    etag                                    text,
    bucket_policy_only_enabled              numeric,
    bucket_policy_only_locked_time          text,
    uniform_bucket_level_access_enabled     numeric,
    uniform_bucket_level_access_locked_time text,
    resource_id                             text,
    kind                                    text,
    location                                text,
    location_type                           text,
    logging_log_bucket                      text,
    logging_log_object_prefix               text,
    metageneration                          integer,
    name                                    text,
    owner_entity                            text,
    owner_entity_id                         text,
    project_number                          integer,
    retention_policy_effective_time         text,
    retention_policy_is_locked              numeric,
    retention_policy_retention_period       integer,
    self_link                               text,
    storage_class                           text,
    time_created                            text,
    updated                                 text,
    versioning_enabled                      numeric,
    website_main_page_suffix                text,
    website_not_found_page                  text
);

create table gcp_storage_bucket_zone_affinities
(
    id        integer
        primary key,
    bucket_id integer
        constraint fk_gcp_storage_buckets_zone_affinity
            references gcp_storage_buckets
            on delete cascade,
    value     text
);

create table gcp_storage_bucket_object_access_controls
(
    id                          integer
        primary key,
    bucket_id                   integer
        constraint fk_gcp_storage_buckets_default_object_acl
            references gcp_storage_buckets
            on delete cascade,
    bucket                      text,
    domain                      text,
    email                       text,
    entity                      text,
    entity_id                   text,
    etag                        text,
    generation                  integer,
    resource_id                 text,
    kind                        text,
    object                      text,
    project_team_project_number text,
    project_team_team           text,
    role                        text,
    self_link                   text
);

create table gcp_storage_bucket_lifecycle_rules
(
    id                         integer
        primary key,
    bucket_id                  integer
        constraint fk_gcp_storage_buckets_lifecycle_rules
            references gcp_storage_buckets
            on delete cascade,
    action_storage_class       text,
    action_type                text,
    age                        integer,
    created_before             text,
    custom_time_before         text,
    days_since_custom_time     integer,
    days_since_noncurrent_time integer,
    is_live                    numeric,
    matches_pattern            text,
    noncurrent_time_before     text,
    num_newer_versions         integer
);

create table gcp_storage_bucket_labels
(
    id        integer
        primary key,
    bucket_id integer
        constraint fk_gcp_storage_buckets_labels
            references gcp_storage_buckets
            on delete cascade,
    key       text,
    value     text
);

create table gcp_storage_bucket_cors_response_headers
(
    id             integer
        primary key,
    bucket_cors_id integer
        constraint fk_gcp_storage_bucket_cors_response_header
            references gcp_storage_bucket_cors
            on delete cascade,
    value          text
);

create table gcp_storage_bucket_cors_origins
(
    id             integer
        primary key,
    bucket_cors_id integer
        constraint fk_gcp_storage_bucket_cors_origin
            references gcp_storage_bucket_cors
            on delete cascade,
    value          text
);

create table gcp_storage_bucket_cors_methods
(
    id             integer
        primary key,
    bucket_cors_id integer
        constraint fk_gcp_storage_bucket_cors_method
            references gcp_storage_bucket_cors
            on delete cascade,
    value          text
);

create table gcp_storage_bucket_cors
(
    id              integer
        primary key,
    bucket_id       integer
        constraint fk_gcp_storage_buckets_cors
            references gcp_storage_buckets
            on delete cascade,
    max_age_seconds integer
);

create table gcp_storage_bucket_access_controls
(
    id                          integer
        primary key,
    bucket_id                   integer
        constraint fk_gcp_storage_buckets_acl
            references gcp_storage_buckets
            on delete cascade,
    bucket                      text,
    domain                      text,
    email                       text,
    entity                      text,
    entity_id                   text,
    etag                        text,
    resource_id                 text,
    kind                        text,
    project_team_project_number text,
    project_team_team           text,
    role                        text,
    self_link                   text
);
```

