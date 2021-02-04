# groups



#### YAML config

```yaml
- name: iam.groups
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

	// The path prefix for filtering the results. For example, the prefix /division_abc/subdivision_xyz/
	// gets all groups whose path starts with /division_abc/subdivision_xyz/.
	//
	// This parameter is optional. If it is not included, it defaults to a slash
	// (/), listing all groups. This parameter allows (through its regex pattern
	// (http://wikipedia.org/wiki/regex)) a string of characters consisting of either
	// a forward slash (/) by itself or a string that must begin and end with forward
	// slashes. In addition, it can contain any ASCII character from the ! (\u0021)
	// through the DEL character (\u007F), including most punctuation characters,
	// digits, and upper and lowercased letters.
	PathPrefix: String // Optional
```

#### Tables schemas

```sql
create table aws_iam_groups
(
    id          integer
        primary key,
    account_id  text,
    region      text,
    arn         text,
    create_date datetime,
    group_id    text,
    group_name  text,
    path        text
);
```



