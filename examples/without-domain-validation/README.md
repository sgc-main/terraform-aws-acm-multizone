# Terraform AWS ACM Multiple Hosted Zone Example

This example provides guides on how to use terraform-aws-acm-multiple-hosted-zone module without creating domain validation records on Route53.
In general it is okay to overwrite domain validation records on Route53.
This example cater to the case in which we don't want to overwrite existing domain validation for any reason.

<!-- BEGIN_TF_DOCS -->








## Outputs

| Name | Description |
|------|-------------|
| <a name="output_certificate_arn"></a> [certificate\_arn](#output\_certificate\_arn) | n/a |
| <a name="output_certificate_domains"></a> [certificate\_domains](#output\_certificate\_domains) | n/a |
<!-- END_TF_DOCS -->