---
description: Policy command explained
---

# Policy

The `cloudquery policy` command allows the management and execution of so-called policies.

## Policy Download

Policies can be directly download from GitHub with the `cloudquery policy download` command:

```text
cloudquery policy download (<github-organization>/)<repository-name>
```

* `github-organization` (Optional): The GitHub organization (or user account name) where the repository is located
  at. If unspecified, the `cloudquery` organization will be automatically picked.
* `repository-name`: The GitHub repository name that should be downloaded.

All downloaded repositories will be stored locally in the `CQ_POLICY_DIR`.

### Examples

Downloads the CQ AWS policy and stores it locally:

```text
cloudquery policy download cq-policy-aws
```

Downloads a policy from a private repository:

```text
cloudquery policy download my-github-user/my-awesome-policy
```

## Policy Run

The policy run command executes the given policy against the database that has been configured in the cloudquery
configuration file:

```bash
cloudquery policy run (<github-organization>/)<repository-name>(@<tag>) (<repository-sub-path>) 
```

* `github-organization` (Optional): The GitHub organization (or user account name) where the repository is located
  at. If unspecified, the `cloudquery` organization will be automatically picked.
* `repository-name`: The GitHub repository name where the policy has been defined.
* `tag` (Optional): The repository tag (e.g. version) that should be used. If no tag was specified the latest tag
  will be used.
* `repository-sub-path` (Optional): The repository internal sub path where the policy definition file is located at.

Arguments:
* `--sub-path`: Allows the execution of sub policies/queries only.
* `--output`: Generates an output file at the given path with the result of the execution (in JSON).
* `--stop-on-failure`: Stops the execution as soon as a query execution has failed its criteria.

### Examples

Runs the `cq-policy-aws` policy at the latest version/tag:

```text
cloudquery policy run cq-policy-aws
```

Runs a private policy at the version/tag `v1.0.5`:

```text
cloudquery policy run my-github-user/my-awesome-policy@v1.0.5
```

Runs a policy that is contained in a sub-folder:

```text
cloudquery policy run my-github-user/my-awesome-policy policies/
```

Runs only a sub query of a policy:

```text
cloudquery policy run cq-policy-aws --sub-path cq-policy-aws.query-1
```
