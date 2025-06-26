# Terraform AWS ACM Multiple Hosted Zone Example

This example provides guides on how to use terraform-aws-acm-multiple-hosted-zone with external certificate validation.
You may have a case where some of domains in the certificate is located in different AWS account.
In this case, you can provision the ACM certificate using this module and do the certificate validation in the root project.

This module will ignore registering domain to Route53 when there is no `zone` key in the domain object.

<!-- BEGIN_TF_DOCS -->


## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
| <a name="provider_aws.example_org"></a> [aws.example\_org](#provider\_aws.example\_org) | n/a |

## Resources

| Name | Type |
|------|------|
| [aws_acm_certificate_validation.self](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/acm_certificate_validation) | resource |
| [aws_route53_record.example_org_validation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) | resource |
| [aws_route53_zone.example_org](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/route53_zone) | data source |



## Outputs

| Name | Description |
|------|-------------|
| <a name="output_certificate_arn"></a> [certificate\_arn](#output\_certificate\_arn) | n/a |
| <a name="output_certificate_domains"></a> [certificate\_domains](#output\_certificate\_domains) | n/a |
<!-- END_TF_DOCS -->