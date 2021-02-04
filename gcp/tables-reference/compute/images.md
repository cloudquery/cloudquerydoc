# images

#### YAML config

```yaml
- name: compute.images
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```sql
create table gcp_compute_images
(
    id                      integer
        primary key,
    project_id              text,
    region                  text,
    archive_size_bytes      integer,
    creation_timestamp      text,
    deprecated_deleted      text,
    deprecated_deprecated   text,
    deprecated_obsolete     text,
    deprecated_replacement  text,
    deprecated_state        text,
    description             text,
    disk_size_gb            integer,
    family                  text,
    resource_id             integer,
    kind                    text,
    label_fingerprint       text,
    name                    text,
    raw_disk_container_type text,
    raw_disk_sha1_checksum  text,
    raw_disk_source         text,
    self_link               text,
    source_disk             text,
    source_disk_id          text,
    source_image            text,
    source_image_id         text,
    source_snapshot         text,
    source_snapshot_id      text,
    source_type             text,
    status                  text
);

create table gcp_compute_image_storage_locations
(
    id       integer
        primary key,
    image_id integer
        constraint fk_gcp_compute_images_storage_locations
            references gcp_compute_images
            on delete cascade,
    value    text
);

create table gcp_compute_image_licenses
(
    id       integer
        primary key,
    image_id integer
        constraint fk_gcp_compute_images_licenses
            references gcp_compute_images
            on delete cascade,
    value    text
);

create table gcp_compute_image_license_codes
(
    id       integer
        primary key,
    image_id integer
        constraint fk_gcp_compute_images_license_codes
            references gcp_compute_images
            on delete cascade,
    value    integer
);

create table gcp_compute_image_guest_os_features
(
    id       integer
        primary key,
    image_id integer
        constraint fk_gcp_compute_images_guest_os_features
            references gcp_compute_images
            on delete cascade,
    type     text
);
```

