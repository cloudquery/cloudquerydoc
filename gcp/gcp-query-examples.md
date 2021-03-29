# GCP Query Examples

## Find all buckets that have public facing read permissions

```sql
SELECT gcp_storage_buckets.name
FROM gcp_storage_buckets
         JOIN gcp_storage_bucket_policy_bindings ON gcp_storage_bucket_policy_bindings.bucket_id = gcp_storage_buckets.id
         JOIN gcp_storage_bucket_policy_bindings_members ON gcp_storage_bucket_policy_bindings_members.bucket_policy_binding_id = gcp_storage_bucket_policy_bindings.id
WHERE gcp_storage_bucket_policy_bindings_members.name = 'allUsers' AND gcp_storage_bucket_policy_bindings.role = 'roles/storage.objectViewer';
```

