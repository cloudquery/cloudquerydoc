# Quick Start

## Download & Install

You can download the precompiled binary from [releases](https://github.com/cloudquery/cloudquery/releases), or using CLI:

{% tabs %}
{% tab title="Pre-Compiled Binaries" %}
Download latest version:

```bash
export OS=Darwin # Possible values: Linux,Windows,Darwin
curl -L https://github.com/cloudquery/cloudquery/releases/latest/download/cloudquery_${OS}_x86_64 -o cloudquery
chmod a+x cloudquery
```

Download specific version:

```bash
export OS=Darwin # Possible values: Linux,Windows,Darwin
export VERSION= # specifiy a version
curl -L https://github.com/cloudquery/cloudquery/releases/download/${VERSION}/cloudquery_${OS}_x86_64 -o cloudquery
```
{% endtab %}

{% tab title="Homebrew" %}
```bash
brew install cloudquery/tap/cloudquery
# After initial install you can upgrade the version via:
brew upgrade cloudquery
```
{% endtab %}

{% tab title="Docker" %}
`config.yml` should be mounted so cloudquery can read it

```
# Dockers are hosted at github container registry https://github.com/orgs/cloudquery/packages/container/package/cloudquery
docker pull ghcr.io/cloudquery/cloudquery:latest
docker run -v /data:/data -it ghcr.io/cloudquery/cloudquery:latest --path /data/config.yml --dsn "host=localhost user=postgres password=pass DB.name=postgres port=5432"
```
{% endtab %}
{% endtabs %}

## Running

Currently, we support: [AWS](https://docs.cloudquery.io/aws), [Azure](https://docs.cloudquery.io/azure), [GCP](https://docs.cloudquery.io/gcp), [Okta](https://docs.cloudquery.io/okta/table-reference). If you want us to add a new provider or resource please open an [Issue](https://github.com/cloudquery/cloudquery/issues).

First generate a `config.hcl` file that will describe which resources you want cloudquery to pull, normalize and transform resources to the specified SQL database by running the following command:

```text
./cloudquery init aws
# ./cloudquery init gcp aws # This will generate a config containing gcp and aws providers
# ./cloudquery init --help # Show all possible auto generated configs and flags
```

Once your `config.hcl` is generated run the following command to fetch the resources \(you need to be authenticated - see relevant section under each provider\):

```text
./cloudquery fetch
# ./cloudquery fetch --help # Show all possible fetch flags
```

Once your provider has fetched resources you can run the following example queries

#### List ec2\_images:

```sql
SELECT * FROM aws_ec2_images;
```

#### Find all public facing AWS load balancers:

```sql
SELECT * FROM aws_elbv2_load_balancers WHERE scheme = 'internet-facing';
```

**Running policy packs**

CloudQuery comes with some ready compliance policy pack which you can use as is or modify to fit your use-case.

Currently, cloudquery support [AWS CIS](https://d0.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf) policy pack \(it is under active development, so it doesn't cover the whole spec yet\).

To run a pack enter the following commands \(make sure you fetched all the resources beforehand by the `fetch` command\):

```bash
./cloudquery policy --path=<PATH_TO_POLICY_FILE> --output=<PATH_TO_OUTPUT_POLICY_RESULT>
```

