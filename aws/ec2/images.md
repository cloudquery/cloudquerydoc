# images



#### YAML config

```text
- name: ec2.images
  ImageIds: // Optional (Default: Describes all images available to you)
  		- "id"
	
	// Owners (Optional).
	// Scopes the results to images with the specified owners. You can specify a
	// combination of AWS account IDs, self, amazon, and aws-marketplace. If you
	// omit this parameter, the results include all images for which you have launch
	// permissions, regardless of ownership.  
  Owners: // Optional
  		- "owner"
  // The filters (Optional).
	//
	//    * architecture - The image architecture (i386 | x86_64 | arm64).
	//
	//    * block-device-mapping.delete-on-termination - A Boolean value that indicates
	//    whether the Amazon EBS volume is deleted on instance termination.
	//
	//    * block-device-mapping.device-name - The device name specified in the
	//    block device mapping (for example, /dev/sdh or xvdh).
	//
	//    * block-device-mapping.snapshot-id - The ID of the snapshot used for the
	//    EBS volume.
	//
	//    * block-device-mapping.volume-size - The volume size of the EBS volume,
	//    in GiB.
	//
	//    * block-device-mapping.volume-type - The volume type of the EBS volume
	//    (gp2 | io1 | io2 | st1 | sc1 | standard).
	//
	//    * block-device-mapping.encrypted - A Boolean that indicates whether the
	//    EBS volume is encrypted.
	//
	//    * description - The description of the image (provided during image creation).
	//
	//    * ena-support - A Boolean that indicates whether enhanced networking with
	//    ENA is enabled.
	//
	//    * hypervisor - The hypervisor type (ovm | xen).
	//
	//    * image-id - The ID of the image.
	//
	//    * image-type - The image type (machine | kernel | ramdisk).
	//
	//    * is-public - A Boolean that indicates whether the image is public.
	//
	//    * kernel-id - The kernel ID.
	//
	//    * manifest-location - The location of the image manifest.
	//
	//    * name - The name of the AMI (provided during image creation).
	//
	//    * owner-alias - The owner alias, from an Amazon-maintained list (amazon
	//    | aws-marketplace). This is not the user-configured AWS account alias
	//    set using the IAM console. We recommend that you use the related parameter
	//    instead of this filter.
	//
	//    * owner-id - The AWS account ID of the owner. We recommend that you use
	//    the related parameter instead of this filter.
	//
	//    * platform - The platform. To only list Windows-based AMIs, use windows.
	//
	//    * product-code - The product code.
	//
	//    * product-code.type - The type of the product code (devpay | marketplace).
	//
	//    * ramdisk-id - The RAM disk ID.
	//
	//    * root-device-name - The device name of the root device volume (for example,
	//    /dev/sda1).
	//
	//    * root-device-type - The type of the root device volume (ebs | instance-store).
	//
	//    * state - The state of the image (available | pending | failed).
	//
	//    * state-reason-code - The reason code for the state change.
	//
	//    * state-reason-message - The message for the state change.
	//
	//    * sriov-net-support - A value of simple indicates that enhanced networking
	//    with the Intel 82599 VF interface is enabled.
	//
	//    * tag:<key> - The key/value combination of a tag assigned to the resource.
	//    Use the tag key in the filter name and the tag value as the filter value.
	//    For example, to find all resources that have a tag with the key Owner
	//    and the value TeamA, specify tag:Owner for the filter name and TeamA for
	//    the filter value.
	//
	//    * tag-key - The key of a tag assigned to the resource. Use this filter
	//    to find all resources assigned a tag with a specific key, regardless of
	//    the tag value.
	//
	//    * virtualization-type - The virtualization type (paravirtual | hvm).
  Filters: // Optional
  Name: "filter name"
  Values:
    - "Filter value"
```

#### Tables schemas

```text
create table aws_ec2_images
(
    id                   integer primary key,
    account_id           text,
    region               text,
    architecture         text,
    creation_date        text,
    description          text,
    ena_support          numeric,
    hypervisor           text,
    image_id             text,
    image_location       text,
    image_owner_alias    text,
    image_type           text,
    kernel_id            text,
    name                 text,
    owner_id             text,
    platform             text,
    platform_details     text,
    public               numeric,
    ramdisk_id           text,
    root_device_name     text,
    root_device_type     text,
    sriov_net_support    text,
    state                text,
    state_reason_code    text,
    state_reason_message text,
    usage_operation      text,
    virtualization_type  text
);

create table aws_ec2_image_tags
(
    id       integer primary key,
    image_id integer
        constraint fk_aws_ec2_images_tags
            references aws_ec2_images
            on delete cascade,
    key      text,
    value    text
);

create table aws_ec2_image_product_codes
(
    id                integer primary key,
    image_id          integer
        constraint fk_aws_ec2_images_product_codes
            references aws_ec2_images
            on delete cascade,
    product_code_id   text,
    product_code_type text
);

create table aws_ec2_image_block_device_mappings
(
    id                        integer
        primary key,
    image_id                  integer
        constraint fk_aws_ec2_images_block_device_mappings
            references aws_ec2_images
            on delete cascade,
    device_name               text,
    ebs_delete_on_termination numeric,
    ebs_encrypted             numeric,
    ebs_iops                  integer,
    ebs_kms_key_id            text,
    ebs_snapshot_id           text,
    ebs_volume_size           integer,
    ebs_volume_type           text,
    no_device                 text,
    virtual_name              text
);

```

