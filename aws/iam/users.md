# users

#### YAML config

```text
- name: iam.users
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

	// The path prefix for filtering the results. For example: /division_abc/subdivision_xyz/,
	// which would get all user names whose path starts with /division_abc/subdivision_xyz/.
	//
	// This parameter is optional. If it is not included, it defaults to a slash
	// (/), listing all user names. This parameter allows (through its regex pattern
	// (http://wikipedia.org/wiki/regex)) a string of characters consisting of either
	// a forward slash (/) by itself or a string that must begin and end with forward
	// slashes. In addition, it can contain any ASCII character from the ! (\u0021)
	// through the DEL character (\u007F), including most punctuation characters,
	// digits, and upper and lowercased letters.
	PathPrefix: String // Optional
```

#### Tables schemas

```text
create table aws_iam_users
(
    id                                             integer
        primary key,
    account_id                                     text,
    region                                         text,
    arn                                            text,
    create_date                                    datetime,
    password_last_used                             datetime,
    path                                           text,
    permissions_boundary_permissions_boundary_arn  text,
    permissions_boundary_permissions_boundary_type text,
    user_id                                        text,
    user_name                                      text
);

create table aws_iam_user_tags
(
    id      integer
        primary key,
    user_id integer
        constraint fk_aws_iam_users_tags
            references aws_iam_users
            on delete cascade,
    key     text,
    value   text
);
```



