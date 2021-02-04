# byoip\_cidrs

#### YAML config

```yaml
- name: ec2.byoip_cidrs
  MaxResults: Number // required
```

#### Tables schemas

```sql
create table aws_ec2_byoip_cidrs
(
    id             integer
        primary key,
    account_id     text,
    region         text,
    cidr           text,
    description    text,
    state          text,
    status_message text
);
```



