# Tables Reference

### Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `gcp` prefix\) 

### Config Reference

Available resource you can specify in `config.yml`. You can also generate a default config containing all resources via `./cloudquery gen config aws`

```yaml
providers:  
  - name: gcp
    project_id: <CHANGE_THIS_TO_YOUR_PROJECT_ID>
    resources:
      - name: compute.instances
      - name: compute.autoscalers
      - name: compute.disk_types
      - name: compute.images
      - name: compute.instances
      - name: compute.interconnects
      - name: compute.ssl_certificates
      - name: compute.vpn_gateways
      - name: iam.project_roles
      - name: iam.service_accounts
      - name: storage.buckets
```

