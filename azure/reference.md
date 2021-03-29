# Reference

## Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `azure` prefix\)

## Config Reference

Available resource you can specify in `config.yml`. You can also generate a default config containing all resources via `./cloudquery gen config azure`

```yaml
providers:
    - name: azure
#    subscriptions: # Optional. if you not specified, cloudquery tries to access all subscriptions available to tenant
#      - "subscription-id"
    resources:
      - name: resources.groups
      - name: sql.servers
      - name: sql.databases
      - name: postgresql.servers
      - name: mysql.servers
      - name: compute.disks
      - name: keyvault.vaults
```

