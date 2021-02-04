---
description: Kubernetes support is currently in alpha. feel free to open Issues at GitHub.
---

# Reference

### Schema Reference

Schema is available at [https://schema.cloudquery.io](https://schema.cloudquery.io) \(filter by `k8s` prefix\) 

### Config Reference

Available resource you can specify in `config.yml`. You can also generate a default config containing all resources via `./cloudquery gen config k8s`

```yaml
providers:
  - name: k8s
    resources:
      - name: pods
      - name: services
```

