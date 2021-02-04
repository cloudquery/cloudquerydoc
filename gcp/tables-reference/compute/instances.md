# instances

#### YAML config

```yaml
- name: compute.instances
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```sql
create table gcp_compute_instances
(
    id                                                          integer
        primary key,
    project_id                                                  text,
    can_ip_forward                                              numeric,
    confidential_instance_config_enable_confidential_compute    numeric,
    cpu_platform                                                text,
    creation_timestamp                                          text,
    deletion_protection                                         numeric,
    description                                                 text,
    display_device_enable_display                               numeric,
    fingerprint                                                 text,
    hostname                                                    text,
    resource_id                                                 integer,
    kind                                                        text,
    label_fingerprint                                           text,
    last_start_timestamp                                        text,
    last_stop_timestamp                                         text,
    last_suspended_timestamp                                    text,
    machine_type                                                text,
    min_cpu_platform                                            text,
    name                                                        text,
    private_ipv6_google_access                                  text,
    reservation_affinity_consume_reservation_type               text,
    reservation_affinity_key                                    text,
    scheduling_automatic_restart                                numeric,
    scheduling_min_node_cpus                                    integer,
    scheduling_on_host_maintenance                              text,
    scheduling_preemptible                                      numeric,
    self_link                                                   text,
    shielded_instance_config_enable_integrity_monitoring        numeric,
    shielded_instance_config_enable_secure_boot                 numeric,
    shielded_instance_config_enable_vtpm                        numeric,
    shielded_instance_integrity_policy_update_auto_learn_policy numeric,
    start_restricted                                            numeric,
    status                                                      text,
    status_message                                              text,
    zone                                                        text
);

create table gcp_compute_instance_tags
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_gcp_compute_instances_tags
            references gcp_compute_instances
            on delete cascade,
    fingerprint text,
    value       text
);

create table gcp_compute_instance_service_accounts
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_gcp_compute_instances_service_accounts
            references gcp_compute_instances
            on delete cascade,
    email       text,
    scope       text
);

create table gcp_compute_instance_scheduling_node_affinities
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_gcp_compute_instances_scheduling_node_affinities
            references gcp_compute_instances
            on delete cascade,
    key         text,
    operator    text,
    value       text
);

create table gcp_compute_instance_network_interfaces
(
    id           integer
        primary key,
    instance_id  integer
        constraint fk_gcp_compute_instances_network_interfaces
            references gcp_compute_instances
            on delete cascade,
    fingerprint  text,
    ipv6_address text,
    kind         text,
    name         text,
    network      text,
    network_ip   text,
    subnetwork   text
);

create table gcp_compute_instance_metadata_items
(
    id          integer
        primary key,
    instance_id integer
        constraint fk_gcp_compute_instances_metadata
            references gcp_compute_instances
            on delete cascade,
    fingerprint text,
    key         text,
    value       text,
    kind        text
);

create table gcp_compute_instance_guest_os_features
(
    id                        integer
        primary key,
    instance_attached_disk_id integer
        constraint fk_gcp_compute_instance_attached_disks_guest_os_features
            references gcp_compute_instance_attached_disks
            on delete cascade,
    type                      text
);

create table gcp_compute_instance_attached_disks
(
    id                          integer
        primary key,
    instance_id                 integer
        constraint fk_gcp_compute_instances_disks
            references gcp_compute_instances
            on delete cascade,
    auto_delete                 numeric,
    boot                        numeric,
    device_name                 text,
    disk_size_gb                integer,
    "index"                     integer,
    initialize_description      text,
    initialize_disk_name        text,
    initialize_disk_size_gb     integer,
    initialize_disk_type        text,
    initialize_on_update_action text,
    initialize_source_image     text,
    initialize_source_snapshot  text,
    interface                   text,
    kind                        text,
    mode                        text,
    source                      text,
    type                        text
);

create table gcp_compute_instance_attached_disk_licenses
(
    id                        integer
        primary key,
    instance_attached_disk_id integer
        constraint fk_gcp_compute_instance_attached_disks_licenses
            references gcp_compute_instance_attached_disks
            on delete cascade,
    value                     text
);

create table gcp_compute_instance_alias_ip_ranges
(
    id                            integer
        primary key,
    instance_network_interface_id integer
        constraint fk_gcp_compute_instance_network_interfaces_alias_ip_ranges
            references gcp_compute_instance_network_interfaces
            on delete cascade,
    ip_cidr_range                 text,
    subnetwork_range_name         text
);

create table gcp_compute_instance_access_configs
(
    id                            integer
        primary key,
    instance_network_interface_id integer
        constraint fk_gcp_compute_instance_network_interfaces_access_configs
            references gcp_compute_instance_network_interfaces
            on delete cascade,
    kind                          text,
    name                          text,
    nat_ip                        text,
    network_tier                  text,
    public_ptr_domain_name        text,
    set_public_ptr                numeric,
    type                          text
);

create table gcp_compute_instance_accelerator_configs
(
    id                integer
        primary key,
    instance_id       integer
        constraint fk_gcp_compute_instances_guest_accelerators
            references gcp_compute_instances
            on delete cascade,
    accelerator_count integer,
    accelerator_type  text
);
```

