# autoscalers

#### YAML config

```yaml
- name: compute.autoscalers
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```sql
create table gcp_compute_addresses
(
    id                 integer
        primary key,
    project_id         text,
    address            text,
    address_type       text,
    creation_timestamp text,
    description        text,
    resource_id        integer,
    ip_version         text,
    kind               text,
    name               text,
    network            text,
    network_tier       text,
    prefix_length      integer,
    purpose            text,
    region             text,
    self_link          text,
    status             text,
    subnetwork         text
);

create table gcp_compute_address_users
(
    id         integer
        primary key,
    address_id integer
        constraint fk_gcp_compute_addresses_users
            references gcp_compute_addresses
            on delete cascade,
    value      text
);
```

