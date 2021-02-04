# addresses

#### YAML config

```yaml
- name: compute.addresses
  filter: "" // Optional filter see https://cloud.google.com/monitoring/api/v3/sorting-and-filtering
```

#### Tables schemas:

```sql
create table gcp_compute_autoscalers
(
    id                                            integer
        primary key,
    project_id                                    text,
    cool_down_period_sec                          integer,
    cpu_utilization_utilization_target            real,
    load_balancing_utilization_utilization_target real,
    max_num_replicas                              integer,
    min_num_replicas                              integer,
    mode                                          text,
    max_scaled_in_replicas_calculated             integer,
    max_scaled_in_replicas_fixed                  integer,
    max_scaled_in_replicas_percent                integer,
    time_window_sec                               integer,
    creation_timestamp                            text,
    description                                   text,
    resource_id                                   integer,
    kind                                          text,
    name                                          text,
    recommended_size                              integer,
    region                                        text,
    self_link                                     text,
    status                                        text,
    target                                        text,
    zone                                          text
);

create table gcp_compute_autoscaler_status_details
(
    id            integer
        primary key,
    autoscaler_id integer
        constraint fk_gcp_compute_autoscalers_status_details
            references gcp_compute_autoscalers
            on delete cascade,
    message       text,
    type          text
);

create table gcp_compute_autoscaler_policy_custom_metric_utilizations
(
    id                         integer
        primary key,
    autoscaler_id              integer
        constraint fk_gcp_compute_autoscalers_custom_metric_utilizations
            references gcp_compute_autoscalers
            on delete cascade,
    filter                     text,
    metric                     text,
    single_instance_assignment real,
    utilization_target         real,
    utilization_target_type    text
);
```

