# buckets

#### YAML config

```text
- name: s3.buckets
```

#### Tables schemas

```text
create table aws_s3_buckets
(
    id            integer
        primary key,
    account_id    text,
    region        text,
    creation_date datetime,
    name          text,
    policy        text,
    mfa_delete    text,
    status        text
);

create table aws_s3_bucket_grants
(
    id                       integer
        primary key,
    bucket_id                integer
        constraint fk_aws_s3_buckets_grants
            references aws_s3_buckets
            on delete cascade,
    s3_grantee_display_name  text,
    s3_grantee_email_address text,
    s3_grantee_id            text,
    s3_grantee_type          text,
    s3_grantee_uri           text,
    permission               text
);
```



