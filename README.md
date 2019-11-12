# Terraform Google Cloud Storage Module

This module makes it easy to create one or more GCS buckets, and assign basic permissions on them to arbitrary users.

The resources/services/activations/deletions that this module will create/trigger are:

- One or more GCS buckets
- Zero or more IAM bindings for those buckets

## Compatibility

 This module is meant for use with Terraform 0.12. If you haven't [upgraded](https://www.terraform.io/upgrade-guides/0-12.html)
  and need a Terraform 0.11.x-compatible version of this module, the last released version intended for
  Terraform 0.11.x is [0.1.0](https://registry.terraform.io/modules/terraform-google-modules/cloud-storage/google/0.1.0).

## Usage

Basic usage of this module is as follows:

```hcl
module "gcs_buckets" {
  source  = "terraform-google-modules/cloud-storage/google"
  version = "~> 0.1"
  project_id  = "<PROJECT ID>"
  names = ["first", "second"]
  prefix = "my-unique-prefix"
  set_admin_roles = true
  admins = ["group:foo-admins@example.com"]
  versioning = {
    first = true
  }
  bucket_admins = {
    second = "user:spam@example.com,eggs@example.com"
  }
}
```

Functional examples are included in the
[examples](./examples/) directory.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| admins | IAM-style members who will be granted roles/storage.objectAdmin on all buckets. | list(string) | `<list>` | no |
| bucket\_admins | Map of lowercase unprefixed name => comma-delimited IAM-style per-bucket object admins. | map(string) | `<map>` | no |
| bucket\_creators | Map of lowercase unprefixed name => comma-delimited IAM-style per-bucket object creators. | map(string) | `<map>` | no |
| bucket\_hmackey\_admins | Map of lowercase unprefixed name => comma-delimited IAM-style per-bucket hmacKey admins. | map(string) | `<map>` | no |
| bucket\_policy\_only | Disable ad-hoc ACLs on specified buckets. Defaults to true. Map of lowercase unprefixed name => boolean | map(bool) | `<map>` | no |
| bucket\_storage\_admins | Map of lowercase unprefixed name => comma-delimited IAM-style bucket storage admins. | map(string) | `<map>` | no |
| bucket\_viewers | Map of lowercase unprefixed name => comma-delimited IAM-style per-bucket object viewers. | map(string) | `<map>` | no |
| creators | IAM-style members who will be granted roles/storage.objectCreators on all buckets. | list(string) | `<list>` | no |
| force\_destroy | Optional map of lowercase unprefixed name => boolean, defaults to false. | map(bool) | `<map>` | no |
| hmackey\_admins | IAM-style members who will be granted roles/storage.hmacKeyAdmin on all buckets. | list(string) | `<list>` | no |
| labels | Labels to be attached to the buckets | map(string) | `<map>` | no |
| location | Bucket location. | string | `"EU"` | no |
| names | Bucket name suffixes. | list(string) | n/a | yes |
| prefix | Prefix used to generate the bucket name. | string | n/a | yes |
| project\_id | Bucket project id. | string | n/a | yes |
| set\_admin\_roles | Grant roles/storage.objectAdmin role to admins and bucket_admins. | bool | `"false"` | no |
| set\_creator\_roles | Grant roles/storage.objectCreator role to creators and bucket_creators. | bool | `"false"` | no |
| set\_hmackey\_admin\_roles | Grant roles/storage.hmacKeyAdmin role to storage_admins and bucket_storage_admins. | bool | `"false"` | no |
| set\_storage\_admin\_roles | Grant roles/storage.admin role to storage_admins and bucket_storage_admins. | bool | `"false"` | no |
| set\_viewer\_roles | Grant roles/storage.objectViewer role to viewers and bucket_viewers. | bool | `"false"` | no |
| storage\_admins | IAM-style members who will be granted roles/storage.admin on all buckets. | list(string) | `<list>` | no |
| storage\_class | Bucket storage class. | string | `"MULTI_REGIONAL"` | no |
| versioning | Optional map of lowercase unprefixed name => boolean, defaults to false. | map(bool) | `<map>` | no |
| viewers | IAM-style members who will be granted roles/storage.objectViewer on all buckets. | list(string) | `<list>` | no |

## Outputs

| Name | Description |
|------|-------------|
| bucket | Bucket resource (for single use). |
| buckets | Bucket resources. |
| name | Bucket name (for single use). |
| names | Bucket names. |
| names\_list | List of bucket names. |
| url | Bucket URL (for single use). |
| urls | Bucket URLs. |
| urls\_list | List of bucket URLs. |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

These sections describe requirements for using this module.

### Software

The following dependencies must be available:

- [Terraform][terraform] v0.11
- [Terraform Provider for GCP][terraform-provider-gcp] plugin v2.0

### Service Account

User or service account credentials with the following roles must be used to provision the resources of this module:

- Storage Admin: `roles/storage.admin`

The [Project Factory module][project-factory-module] and the
[IAM module][iam-module] may be used in combination to provision a
service account with the necessary roles applied.

### APIs

A project with the following APIs enabled must be used to host the
resources of this module:

- Google Cloud Storage JSON API: `storage-api.googleapis.com`

The [Project Factory module][project-factory-module] can be used to
provision a project with the necessary APIs enabled.

## Contributing

Refer to the [contribution guidelines](./CONTRIBUTING.md) for
information on contributing to this module.

[iam-module]: https://registry.terraform.io/modules/terraform-google-modules/iam/google
[project-factory-module]: https://registry.terraform.io/modules/terraform-google-modules/project-factory/google
[terraform-provider-gcp]: https://www.terraform.io/docs/providers/google/index.html
[terraform]: https://www.terraform.io/downloads.html

