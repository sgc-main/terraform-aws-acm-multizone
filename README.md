# Terraform AWS Certificate Manager (ACM) Multizone Module

A Terraform module for provisioning an [AWS ACM Certificate](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html) with domains spread across multiple [Route53](https://aws.amazon.com/route53/) hosted zones.

---

## Features

- Request a single ACM certificate for domains in different Route53 hosted zones.
- Supports public Route53 zones only (in the same AWS account as the certificate).
- Flexible mapping for primary and SAN domains.
- Suitable for cross-account ACM/Route53 scenarios.

---

## Usage

```hcl
provider "aws" {}

module "acm" {
    source = "../../"

    providers = {
        aws.acm = aws
        aws.route53 = aws
    }

    domain_name = {
        zone = "example.com"
        domain = "example.com"
    }

    subject_alternative_names = [
        {
            zone = "example.com"
            domain = "*.example.com"
        },
        {
            zone = "example.org"
            domain = "example.org"
        },
        {
          zone   = "another-zone.com"
          domain = "api.another-zone.com"
        }
    ]

    tags = {
        Name = "Test ACM multiple hosted zone"
    }
}
```

## Examples

- [Basic usage example](./examples/basic/)
- [Use existing domain validations records](./examples/without-domain-validation)
- [Different AWS account between ACM and Route53](./examples/different-aws-account)
- [External certificate validations](./examples/external-validation)

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.12.31 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws.acm"></a> [aws.acm](#provider\_aws.acm) | n/a |
| <a name="provider_aws.route53"></a> [aws.route53](#provider\_aws.route53) | n/a |

## Resources

| Name | Type |
|------|------|
| [aws_acm_certificate.self](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/acm_certificate) | resource |
| [aws_acm_certificate_validation.self](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/acm_certificate_validation) | resource |
| [aws_route53_record.validation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_route53_zone.self](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/route53_zone) | data source |

## Inputs

| Name | Description | Type | Default |
|------|-------------|------|---------|
| <a name="input_domain_name"></a> [domain\_name](#input\_domain\_name) | Domain name for the ACM certificate | `map(string)` | n/a |
| <a name="input_subject_alternative_names"></a> [subject\_alternative\_names](#input\_subject\_alternative\_names) | List of subject alternative names for the ACM certificate | `list(map(string))` | n/a |
| <a name="input_tags"></a> [tags](#input\_tags) | Key and value pair that will be added as tag | `map(string)` | `{}` |
| <a name="input_validate_certificate"></a> [validate\_certificate](#input\_validate\_certificate) | Whether to validate certificate | `bool` | `true` |
| <a name="input_validation_allow_overwrite_records"></a> [validation\_allow\_overwrite\_records](#input\_validation\_allow\_overwrite\_records) | Whether to allow overwrite of Route53 records | `bool` | `true` |
| <a name="input_validation_set_records"></a> [validation\_set\_records](#input\_validation\_set\_records) | Whether to configure Route53 records for validation | `bool` | `true` |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_certificate_arn"></a> [certificate\_arn](#output\_certificate\_arn) | The ARN of the certificate |
| <a name="output_certificate_domain_validation_options"></a> [certificate\_domain\_validation\_options](#output\_certificate\_domain\_validation\_options) | A list of attributes to feed into other resources to complete certificate validation |
| <a name="output_certificate_domains"></a> [certificate\_domains](#output\_certificate\_domains) | List of domain names covered by the certificate |
<!-- END_TF_DOCS -->