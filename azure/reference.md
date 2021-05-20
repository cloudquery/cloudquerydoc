# Reference

### Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `azure` prefix\) 

### Config Reference

Available resource you can specify in `config.hcl`. You can also generate a default config containing all resources via `./cloudquery init azure`

```yaml
provider "azure" {
  configuration {
		//  Optional. if you not specified, cloudquery tries to access all subscriptions available to tenant
		// subscriptions = ["<YOU_SUBSCRIPTION_ID_HERE">]
  }
  resources = [
   "resources.groups",
   "sql.servers",
   "sql.databases",
   "postgresql.servers",
   "mysql.servers",
   "compute.disks",
   "keyvault.vaults",
  ]
}
```

### 

