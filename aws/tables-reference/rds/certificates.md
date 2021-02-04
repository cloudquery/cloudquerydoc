# certificates

#### YAML config

```yaml
- name: rds.certificates
	// The user-supplied certificate identifier. If this parameter is specified,
	// information for only the identified certificate is returned. This parameter
	// isn't case-sensitive.
	//
	// Constraints:
	//
	//    * Must match an existing CertificateIdentifier.
	CertificateIdentifier: String // Optional

	// The maximum number of records to include in the response. 
	//
	// Default: 100
	//
	// Constraints: Minimum 20, maximum 100.
	MaxRecords: Number // Optional
```

#### Tables schemas

```sql
create table aws_rds_certificates
(
    id                           integer
        primary key,
    account_id                   text,
    region                       text,
    certificate_arn              text,
    certificate_identifier       text,
    certificate_type             text,
    customer_override            numeric,
    customer_override_valid_till datetime,
    thumbprint                   text,
    valid_from                   datetime,
    valid_till                   datetime
);
```

