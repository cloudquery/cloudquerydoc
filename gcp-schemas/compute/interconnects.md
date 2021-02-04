# interconnects

#### YAML config

```text
- name: compute.interconnects
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```text
create table gcp_compute_interconnects
(
    id                     integer
        primary key,
    project_id             text,
    admin_enabled          numeric,
    creation_timestamp     text,
    customer_name          text,
    description            text,
    google_ip_address      text,
    google_reference_id    text,
    resource_id            integer,
    interconnect_type      text,
    kind                   text,
    link_type              text,
    location               text,
    name                   text,
    noc_contact_email      text,
    operational_status     text,
    peer_ip_address        text,
    provisioned_link_count integer,
    requested_link_count   integer,
    self_link              text,
    state                  text
);

create table gcp_compute_interconnect_outage_notifications
(
    id              integer
        primary key,
    interconnect_id integer
        constraint fk_gcp_compute_interconnects_expected_outages
            references gcp_compute_interconnects
            on delete cascade,
    description     text,
    end_time        integer,
    issue_type      text,
    name            text,
    source          text,
    start_time      integer,
    state           text
);

create table gcp_compute_interconnect_outage_notification_affected_circuits
(
    id                                  integer
        primary key,
    interconnect_outage_notification_id integer
        constraint fk_gcp_compute_interconnect_outage_notifications_affected_circuits
            references gcp_compute_interconnect_outage_notifications
            on delete cascade,
    value                               text
);

create table gcp_compute_interconnect_circuit_infos
(
    id                 integer
        primary key,
    interconnect_id    integer
        constraint fk_gcp_compute_interconnects_circuit_infos
            references gcp_compute_interconnects
            on delete cascade,
    customer_demarc_id text,
    google_circuit_id  text,
    google_demarc_id   text
);

create table gcp_compute_interconnect_attachments
(
    id              integer
        primary key,
    interconnect_id integer
        constraint fk_gcp_compute_interconnects_interconnect_attachments
            references gcp_compute_interconnects
            on delete cascade,
    value           text
);
```

