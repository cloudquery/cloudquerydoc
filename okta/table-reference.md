# Reference

### Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `okta` prefix\) 

### Config Reference

Available resource you can specify in `config.yml`. You can also generate a default config containing all resources via `./cloudquery gen config okta`

```yaml
  - name: okta
    domain: https://<CHANGE_THIS_TO_YOUR_OKTA_DOMAIN>.okta.com
    resources:
      - name: users
      - name: applications
```

