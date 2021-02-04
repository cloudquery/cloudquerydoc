# gateways

#### YAML config

```text
- name: directconnect.gateways
  DirectConnectGatewayId: "ID" // options
```

#### Tables schemas

```text
create table aws_directconnect_gateways
(
    id                           integer primary key,
    account_id                   text,
    region                       text,
    amazon_side_asn              integer,
    direct_connect_gateway_id    text,
    direct_connect_gateway_name  text,
    direct_connect_gateway_state text,
    owner_account                text,
    state_change_error           text
);
```

