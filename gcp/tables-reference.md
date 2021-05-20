# Reference

### Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `gcp` prefix\) 

### Config Reference

Available resource you can specify in `config.hcl`. You can also generate a default config containing all resources via `./cloudquery init gcp`

```yaml
provider "gcp" {
  configuration {
    // Optional. Filter as described https://cloud.google.com/sdk/gcloud/reference/projects/list --filter
    project_filter = ""
    // Optional. If not specified either using all projects accessible.
    // project_ids = [<CHANGE_THIS_TO_YOUR_PROJECT_ID>
  }
  resources = [
  "compute.addresses",
  "compute.autoscalers",
  "compute.disk_types",
  "compute.images",
  "compute.instances",
  "compute.interconnects",
  "compute.ssl_certificates",
  "compute.vpn_gateways",
  "iam.project_roles",
  "iam.service_accounts",
  "storage.buckets",
  ]
}

```

