# service\_accounts

#### YAML config

```text
- name: iam.service_accounts
```

#### Tables schemas:

```text
create table gcp_iam_service_accounts
(
    id               integer
        primary key,
    project_id       text,
    region           text,
    description      text,
    disabled         numeric,
    display_name     text,
    email            text,
    etag             text,
    name             text,
    oauth2_client_id text,
    unique_id        text
);
```

