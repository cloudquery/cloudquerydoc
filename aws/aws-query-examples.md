# AWS Query Examples

#### Find all public facing load balancers

```sql
SELECT * FROM aws_elbv2_load_balancers WHERE scheme = 'internet-facing';
```

#### Find all unencrypted RDS instances

```sql
SELECT * from aws_rds_clusters where storage_encrypted = 0;
```

#### Find all unencrypted buckets

```sql
SELECT * from aws_s3_buckets
    JOIN aws_s3_bucket_encryption_rules ON aws_s3_buckets.id != aws_s3_bucket_encryption_rules.bucket_id;
```

