# Quick Start

## Download & Install

You can download the precompiled binary from [releases](https://github.com/cloudquery/cloudquery/releases), or using CLI:

```bash
export OS=Darwin # Possible values: Linux,Windows,Darwin
curl -L https://github.com/cloudquery/cloudquery/releases/latest/download/cloudquery_${OS}_x86_64 -o cloudquery
chmod a+x cloudquery
./cloudquery --help

# if you want to download a specific version and not latest use the following endpoint
export VERSION= # specifiy a version
curl -L https://github.com/cloudquery/cloudquery/releases/download/${VERSION}/cloudquery_${OS}_x86_64 -o cloudquery
```

For mac you can also install cloudquery via hombrew

```bash
brew install cloudquery/tap/cloudquery
# After initial install you can upgrade the version via:
brew upgrade cloudquery
```

## Running

Currently, we support: [AWS](https://docs.cloudquery.io/aws), [Azure](https://docs.cloudquery.io/azure), [GCP](https://docs.cloudquery.io/gcp), [Okta](https://docs.cloudquery.io/okta/table-reference). If you want us to add a new provider or resource please open an [Issue](https://github.com/cloudquery/cloudquery/issues).

First generate a `config.yml` file that will describe which resources you want cloudquery to pull, normalize and transform resources to the specified SQL database by running the following command:

```text
./cloudquery gen config aws
# ./cloudquery gen config gcp okta # This will generate a config containing gcp and okta providers
# ./cloudquery gen config --help # Show all possible auto generated configs and flags
```

Once your `config.yml` is generated run the following command to fetch the resources \(you need to be authenticated - see relevant section under each provider\):

```text
./cloudquery fetch
# ./cloudquery fetch --help # Show all possible fetch flags
```

If you used the default `sqlite` provider you can run the following example queries

#### List ec2\_images:

```sql
SELECT * FROM aws_ec2_images;
```

#### Find all public facing AWS load balancers:

```sql
SELECT * FROM aws_elbv2_load_balancers WHERE scheme = 'internet-facing';
```

**Running policy packs**

cloudquery comes with some ready compliance policy pack which you can use as is or modify to fit your use-case.

Currently, cloudquery support [AWS CIS](https://d0.awsstatic.com/whitepapers/compliance/AWS_CIS_Foundations_Benchmark.pdf) policy pack \(it is under active development, so it doesn't cover the whole spec yet\).

To run AWS CIS pack enter the following commands \(make sure you fetched all the resources beforehand by the `fetch` command\):

```bash
./cloudquery gen policy aws_cis
./cloudquery query 
```

