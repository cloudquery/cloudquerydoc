# Users

#### YAML config

```yaml
providers:
    - name: okta
      domain: https://<your_domain>.okta.com
      resources:
        - name: users
```

#### Tables schemas:

```sql
create table okta_users
(
    id                        integer
        primary key,
    domain                    text,
    activated                 datetime,
    created                   datetime,
    credentials_provider_name text,
    credentials_provider_type text,
    resource_id               text,
    last_login                datetime,
    last_updated              datetime,
    password_changed          datetime,
    status                    text,
    status_changed            datetime,
    transitioning_to_status   text,
    last_name                 text,
    mobile_phone              text,
    primary_phone             text,
    state                     text,
    postal_address            text,
    manager_id                text,
    honorific_suffix          text,
    nick_name                 text,
    timezone                  text,
    user_type                 text,
    cost_center               text,
    department                text,
    first_name                text,
    email                     text,
    second_email              text,
    city                      text,
    honorific_prefix          text,
    login                     text,
    title                     text,
    country_code              text,
    zip_code                  text,
    preferred_language        text,
    locale                    text,
    middle_name               text,
    street_address            text,
    employee_number           text,
    organization              text,
    division                  text,
    profile_url               text,
    manager                   text,
    display_name              text
);

create table okta_user_groups
(
    user_group_id           integer
        primary key,
    user_id                 integer
        constraint fk_okta_users_groups
            references okta_users
            on delete cascade,
    created                 datetime,
    group_id                text,
    last_membership_updated datetime,
    last_updated            datetime,
    name                    text,
    description             text,
    type                    text
);

```

