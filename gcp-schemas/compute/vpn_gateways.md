# vpn\_gateways

#### YAML config

```text
- name: compute.vpn_gateways
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```text
create table gcp_compute_vpn_gateways
(
    id                 integer
        primary key,
    project_id         text,
    creation_timestamp text,
    description        text,
    resource_id        integer,
    kind               text,
    label_fingerprint  text,
    name               text,
    network            text,
    region             text,
    self_link          text
);

create table gcp_compute_vpn_gateway_vpn_gateway_interfaces
(
    id             integer
        primary key,
    vpn_gateway_id integer
        constraint fk_gcp_compute_vpn_gateways_vpn_interfaces
            references gcp_compute_vpn_gateways
            on delete cascade,
    resource_id    integer,
    ip_address     text
);

create table gcp_compute_vpn_gateway_labels
(
    id             integer
        primary key,
    vpn_gateway_id integer
        constraint fk_gcp_compute_vpn_gateways_labels
            references gcp_compute_vpn_gateways
            on delete cascade,
    key            text,
    value          text
);
```

