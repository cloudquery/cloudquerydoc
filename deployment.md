# Deployment

## AWS lambda deployment

CloudQuery currently has out-of-the box [terraforms](https://github.com/cloudquery/cloudquery/tree/main/deploy/aws/terraform) that will deploy it as a lambda function and a MySQL RDS instance.

To apply the terraform files you should be [authenticated](aws/authentication.md) with your AWS account.

```bash
make config # Compiles the binary and creates config.yml
make plan # run terraform plan command
make apply # run terraform apply command
```

{% hint style="info" %}
If you are interested in other deployments feel free to open an [issue](https://github.com/cloudquery/cloudquery/issues) or a pull-request.
{% endhint %}

