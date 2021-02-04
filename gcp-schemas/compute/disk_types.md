# disk\_types

#### YAML config

```text
- name: compute.disk_types
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```text
create table gcp_compute_disk_types
(
    id                     integer
        primary key,
    project_id             text,
    creation_timestamp     text,
    default_disk_size_gb   integer,
    deprecated_deleted     text,
    deprecated_deprecated  text,
    deprecated_obsolete    text,
    deprecated_replacement text,
    deprecated_state       text,
    description            text,
    resource_id            integer,
    kind                   text,
    name                   text,
    region                 text,
    self_link              text,
    valid_disk_size        text,
    zone                   text
);
```

