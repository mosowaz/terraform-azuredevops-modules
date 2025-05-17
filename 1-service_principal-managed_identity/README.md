<!-- BEGIN_TF_DOCS -->


```hcl

``` 

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_azuread"></a> [azuread](#requirement\_azuread) | ~> 3.3.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 4.28.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 3.5 |
| <a name="requirement_time"></a> [time](#requirement\_time) | 0.12.1 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [azuread_application.spn_application](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/application) | resource |
| [azuread_application_api_access.api_permission](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/application_api_access) | resource |
| [azuread_service_principal.service_principal](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/service_principal) | resource |
| [azurerm_resource_group.rg](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group) | resource |
| [azurerm_role_assignment.iam_roles](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment) | resource |
| [azurerm_role_assignment.owner](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment) | resource |
| [azuread_client_config.current](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/client_config) | data source |
| [azuread_service_principal.msgraph_api](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/service_principal) | data source |
| [azuread_service_principal.spn](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/service_principal) | data source |
| [azurerm_role_definition.owner_role](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/role_definition) | data source |
| [azurerm_subscription.primary](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/subscription) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_app_role_ids"></a> [app\_role\_ids](#input\_app\_role\_ids) | API permissions required by the service principal running terraform apply | `list(string)` | n/a | yes |
| <a name="input_iam_roles"></a> [iam\_roles](#input\_iam\_roles) | IAM roles required for the Service Principal to perform operations | `list(string)` | n/a | yes |
| <a name="input_resource_group"></a> [resource\_group](#input\_resource\_group) | Name and location of resource group | <pre>object({<br/>    name     = string<br/>    location = string<br/>  })</pre> | n/a | yes |
| <a name="input_use_msi"></a> [use\_msi](#input\_use\_msi) | Should Managed Identity be used for authentication? | `bool` | n/a | yes |
| <a name="input_use_spn_with_certificate"></a> [use\_spn\_with\_certificate](#input\_use\_spn\_with\_certificate) | Should the Service Principal be used to authenticate with Client Certificate? | `bool` | n/a | yes |
| <a name="input_use_spn_with_oidc"></a> [use\_spn\_with\_oidc](#input\_use\_spn\_with\_oidc) | Should the Service Principal be used to authenticate with OpenID Connect? | `bool` | n/a | yes |
| <a name="input_use_spn_with_secret"></a> [use\_spn\_with\_secret](#input\_use\_spn\_with\_secret) | Should the Service Principal be used to authenticate with Client Secret? | `bool` | n/a | yes |
| <a name="input_app_display_name"></a> [app\_display\_name](#input\_app\_display\_name) | The display name of the application associated with this service principal. | `string` | `"My_Automation_Account"` | no |
| <a name="input_description"></a> [description](#input\_description) | Description of the SPN being created | `string` | `"Service principal for automation"` | no |
| <a name="input_use_existing"></a> [use\_existing](#input\_use\_existing) | When true, any existing service principal linked to the same application will be automatically imported. <br/>When false, an import error will be raised for any pre-existing service principal. | `bool` | `true` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->