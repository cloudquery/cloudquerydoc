# service\_accounts

#### YAML config

```yaml
- name: iam.service_accounts
```

#### Tables schemas:

```sql
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

