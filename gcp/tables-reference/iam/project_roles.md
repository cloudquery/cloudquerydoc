# project\_roles

#### YAML config

```yaml
- name: iam.project_roles
```

#### Tables schemas:

```sql
create table gcp_iam_roles
(
    id          integer
        primary key,
    project_id  text,
    region      text,
    deleted     numeric,
    description text,
    etag        text,
    name        text,
    stage       text,
    title       text
);

create table gcp_iam_role_permissions
(
    id      integer
        primary key,
    role_id integer
        constraint fk_gcp_iam_roles_included_permissions
            references gcp_iam_roles
            on delete cascade,
    value   text
);
```

