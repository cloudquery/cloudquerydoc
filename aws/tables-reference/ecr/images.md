# images

#### YAML config

```yaml
- name: ecr.images
  RepositoryName: String // Required. The repository with image IDs to be listed.
  
 	// The AWS account ID associated with the registry that contains the repository
	// in which to list images. If you do not specify a registry, the default registry
	// is assumed.
  RegistryId: String // Optional
  
 	// The filter key and value with which to filter your ListImages results.
	Filter: // Optional
		TagStatus: "status"

	// The maximum number of image results returned by ListImages in paginated output.
	// When this parameter is used, ListImages only returns maxResults results in
	// a single page along with a nextToken response element. 
	// This value can be between 1 and 1000.
	// If this parameter is not used, then ListImages returns up to 100 results.
	MaxResults: Number // Optional
```

#### Tables schemas

```sql
create table aws_ecr_images
(
    id           integer
        primary key,
    account_id   text,
    region       text,
    image_digest text,
    image_tag    text
);
```



