# Applications

#### YAML config

```yaml
providers:
    - name: okta
      domain: https://<your_domain>.okta.com
      resources:
        - name: applications
```

#### Tables schemas:

```sql
create table okta_applications
(
    id                                      integer
        primary key,
    domain_id                               text,
    accessibility_error_redirect_url        text,
    accessibility_login_redirect_url        text,
    accessibility_self_service              numeric,
    created                                 datetime,
    credentials_signing_last_rotated        datetime,
    credentials_signing_next_rotation       datetime,
    credentials_signing_rotation_mode       text,
    credentials_user_name_template_suffix   text,
    credentials_user_name_template_template text,
    credentials_user_name_template_type     text,
    application_id                          text,
    label                                   text,
    last_updated                            datetime,
    licensing_seat_count                    integer,
    name                                    text,
    settings_implicit_assignment            numeric,
    settings_inline_hook_id                 text,
    settings_notifications_vpn_help_url     text,
    settings_notifications_vpn_message      text,
    sign_on_mode                            text,
    status                                  text,
    visibility_auto_submit_toolbar          numeric,
    visibility_hide_ios                     numeric,
    visibility_hide_web                     numeric,
    domain                                  text
);

create table okta_application_features
(
    id             integer
        primary key,
    application_id integer
        constraint fk_okta_applications_features
            references okta_applications
            on delete cascade,
    value          text
);
```

