# policies

#### YAML config

```yaml
- name: iam.policies
	// Use this only when paginating results to indicate the maximum number of items
	// you want in the response. If additional items exist beyond the maximum you
	// specify, the IsTruncated response element is true.
	//
	// If you do not include this parameter, the number of items defaults to 100.
	// Note that IAM might return fewer results, even when there are more results
	// available. In that case, the IsTruncated response element returns true, and
	// Marker contains a value to include in the subsequent call that tells the
	// service where to continue from.
	MaxItems: Number // Optional

	// A flag to filter the results to only the attached policies.
	//
	// When OnlyAttached is true, the returned list contains only the policies that
	// are attached to an IAM user, group, or role. When OnlyAttached is false,
	// or when the parameter is not included, all policies are returned.
	OnlyAttached: Bool // Optional

	// The path prefix for filtering the results. This parameter is optional. If
	// it is not included, it defaults to a slash (/), listing all policies. This
	// parameter allows (through its regex pattern (http://wikipedia.org/wiki/regex))
	// a string of characters consisting of either a forward slash (/) by itself
	// or a string that must begin and end with forward slashes. In addition, it
	// can contain any ASCII character from the ! (\u0021) through the DEL character
	// (\u007F), including most punctuation characters, digits, and upper and lowercased
	// letters.
	PathPrefix: String // Optional

	// The policy usage method to use for filtering the results.
	//
	// To list only permissions policies, set PolicyUsageFilter to PermissionsPolicy.
	// To list only the policies used to set permissions boundaries, set the value
	// to PermissionsBoundary.
	//
	// This parameter is optional. If it is not included, all policies are returned.
	PolicyUsageFilter: String // Optional

	// The scope to use for filtering the results.
	//
	// To list only AWS managed policies, set Scope to AWS. To list only the customer
	// managed policies in your AWS account, set Scope to Local.
	//
	// This parameter is optional. If it is not included, or if it is set to All,
	// all policies are returned.
	Scope: String // Optional
```

#### Tables schemas

```sql
create table aws_iam_policies
(
    id                               integer
        primary key,
    account_id                       text,
    region                           text,
    arn                              text,
    attachment_count                 integer,
    create_date                      datetime,
    default_version_id               text,
    description                      text,
    is_attachable                    numeric,
    path                             text,
    permissions_boundary_usage_count integer,
    policy_id                        text,
    policy_name                      text,
    update_date                      datetime
);
```



