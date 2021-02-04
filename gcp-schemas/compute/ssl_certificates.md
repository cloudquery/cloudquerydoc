# ssl\_certificates

#### YAML config

```text
- name: compute.ssl_certificates
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```text
create table gcp_compute_ssl_certificates
(
    id                       integer
        primary key,
    project_id               text,
    certificate              text,
    creation_timestamp       text,
    description              text,
    expire_time              text,
    resource_id              integer,
    kind                     text,
    managed_status           text,
    name                     text,
    region                   text,
    self_link                text,
    self_managed_certificate text,
    type                     text
);

create table gcp_compute_ssl_certificate_subject_alternative_names
(
    id                 integer
        primary key,
    ssl_certificate_id integer
        constraint fk_gcp_compute_ssl_certificates_subject_alternative_names
            references gcp_compute_ssl_certificates
            on delete cascade,
    value              text
);

create table gcp_compute_ssl_certificate_managed_domains
(
    id                 integer
        primary key,
    ssl_certificate_id integer
        constraint fk_gcp_compute_ssl_certificates_managed_domains
            references gcp_compute_ssl_certificates
            on delete cascade,
    value              text
);
```

