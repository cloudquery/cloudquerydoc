# access\_keys

#### YAML config

```yaml
- name: iam.access_keys
```

#### Tables schemas

```sql
create table aws_iam_users
(
    id                                             integer
        primary key,
    account_id                                     text,
    region                                         text,
    arn                                            text,
    create_date                                    datetime,
    password_last_used                             datetime,
    path                                           text,
    permissions_boundary_permissions_boundary_arn  text,
    permissions_boundary_permissions_boundary_type text,
    user_id                                        text,
    user_name                                      text
);

create table aws_iam_user_tags
(
    id      integer
        primary key,
    user_id integer
        constraint fk_aws_iam_users_tags
            references aws_iam_users
            on delete cascade,
    key     text,
    value   text
);
```

