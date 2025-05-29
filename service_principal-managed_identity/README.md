<!-- BEGIN_TF_DOCS -->
# Terraform Azure Service Principal and Managed Identity Module
This module creates Service Principal (with client secrets, OIDC, or client certificate) and Managed Identity.\
This module also creates Azure Key Vault to store Service Principal secret value and its related attributes,\
 as well as storage account for terraform states used by the Service Principal.

Set one of the service principal/managed identity input variable to "true" to activate the deployment.\
Here, `use_secret` is used as an example.
```hcl
use_secret      = true
use_oidc        = false # if "true", its associated attributes MUST BE PROVIDED!
use_certificate = false
use_msi         = false
```
## Note
The user principal assigning the API permissions to the newly created Service Principal must have a `Global Administrator` role\
or `Application.ReadWrite.All` and `Directory.ReadWrite.All` API permission assigned to a Service Principal to successfully assign those permissions for newly created Service Principals.\
Then, go to the portal to explicitly grant `admin consent` to the Service Principal.

### Example - Service Principal with client secret
This example shows how to use the module to create spn with client secret. Other authentication methods can be used as well by setting the respective variable to `true`

```hcl
module "service-principal" {
  source = "git::https://github.com/mosowaz/terraform-azuredevops-modules/tree/main/service_principal-managed_identity?ref=v1.0.0"

  use_secret = true
  use_oidc = false
  use_certificate = false
  use_msi = false
}
``` 

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_azuread"></a> [azuread](#requirement\_azuread) | ~> 3.3.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 4.28.0 |
| <a name="requirement_http"></a> [http](#requirement\_http) | ~> 3.5 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 3.5 |
| <a name="requirement_time"></a> [time](#requirement\_time) | 0.12.1 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_avm-res-keyvault-vault"></a> [avm-res-keyvault-vault](#module\_avm-res-keyvault-vault) | git::https://github.com/Azure/terraform-azurerm-avm-res-keyvault-vault.git | 6e49111ba5 |
| <a name="module_avm-res-storage-storageaccount"></a> [avm-res-storage-storageaccount](#module\_avm-res-storage-storageaccount) | git::https://github.com/Azure/terraform-azurerm-avm-res-storage-storageaccount | daf3cad |
| <a name="module_naming"></a> [naming](#module\_naming) | git::https://github.com/Azure/terraform-azurerm-naming.git | 75d5afae |

## Resources

| Name | Type |
|------|------|
| [azuread_application.spn_application](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/application) | resource |
| [azuread_application_api_access.api_permission](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/application_api_access) | resource |
| [azuread_application_federated_identity_credential.spn_azuredevops_oidc](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/application_federated_identity_credential) | resource |
| [azuread_service_principal.service_principal](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/service_principal) | resource |
| [azuread_service_principal_password.spn_secret](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/resources/service_principal_password) | resource |
| [azurerm_resource_group.rg](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group) | resource |
| [azurerm_role_assignment.iam_roles](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment) | resource |
| [azurerm_role_assignment.owner](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/role_assignment) | resource |
| [azuread_service_principal.msgraph_api](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/service_principal) | data source |
| [azuread_service_principal.spn](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/service_principal) | data source |
| [azuread_user.primary_owner](https://registry.terraform.io/providers/hashicorp/azuread/latest/docs/data-sources/user) | data source |
| [azurerm_role_definition.owner_role](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/role_definition) | data source |
| [azurerm_subscription.primary](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/subscription) | data source |
| [http_http.ip](https://registry.terraform.io/providers/hashicorp/http/latest/docs/data-sources/http) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_app_role_ids"></a> [app\_role\_ids](#input\_app\_role\_ids) | (Required) API permissions required by the service principal running terraform apply | `list(string)` | n/a | yes |
| <a name="input_iam_roles"></a> [iam\_roles](#input\_iam\_roles) | (Required) IAM roles required for the Service Principal to perform operations | `list(string)` | n/a | yes |
| <a name="input_keyvault_name"></a> [keyvault\_name](#input\_keyvault\_name) | (Required) Name of the Key Vault | `string` | n/a | yes |
| <a name="input_my_publicIP"></a> [my\_publicIP](#input\_my\_publicIP) | (Required) Your public IP address to allow access Key Vault and Storage account | `any` | n/a | yes |
| <a name="input_resource_group"></a> [resource\_group](#input\_resource\_group) | (Required) Name and location of resource group | <pre>object({<br/>    name     = string<br/>    location = string<br/>  })</pre> | n/a | yes |
| <a name="input_spn_client_id_name"></a> [spn\_client\_id\_name](#input\_spn\_client\_id\_name) | (Required) Name given to the service principal's client ID | `string` | n/a | yes |
| <a name="input_spn_secret_name"></a> [spn\_secret\_name](#input\_spn\_secret\_name) | (Required) Name given to the service principal's secret value | `string` | n/a | yes |
| <a name="input_spn_subscription_id_name"></a> [spn\_subscription\_id\_name](#input\_spn\_subscription\_id\_name) | (Required) Name given to the service principal's subscription ID | `string` | n/a | yes |
| <a name="input_spn_tenant_id_name"></a> [spn\_tenant\_id\_name](#input\_spn\_tenant\_id\_name) | (Required) Name given to the service principal's tenant ID | `string` | n/a | yes |
| <a name="input_storage_account_name"></a> [storage\_account\_name](#input\_storage\_account\_name) | (Required) Name of the storage account created for the SPN | `string` | n/a | yes |
| <a name="input_storage_container_name"></a> [storage\_container\_name](#input\_storage\_container\_name) | (Required) Name of the storage container created for the SPN | `string` | n/a | yes |
| <a name="input_use_certificate"></a> [use\_certificate](#input\_use\_certificate) | (Required) Should the Service Principal be used to authenticate with Client Certificate? | `bool` | n/a | yes |
| <a name="input_use_existing"></a> [use\_existing](#input\_use\_existing) | (Required) When true, any existing service principal linked to the same application will be automatically imported. <br/>When false, an import error will be raised for any pre-existing service principal. | `bool` | n/a | yes |
| <a name="input_use_msi"></a> [use\_msi](#input\_use\_msi) | (Required) Should Managed Identity be used for authentication? | `bool` | n/a | yes |
| <a name="input_use_oidc"></a> [use\_oidc](#input\_use\_oidc) | (Required) Should the Service Principal be used to authenticate with OpenID Connect?<br/>If true, azdo\_organization\_name, azdo\_project\_name, azdo\_repo\_name and azdo\_branch MUST BE PROVIDED.<br/>This assumes you already have a repository and a project in your organization. | <pre>object({<br/>    enabled                = bool<br/>    azdo_organization_name = optional(string, null)<br/>    azdo_project_name      = optional(string, null)<br/>    azdo_repo_name         = optional(string, null)<br/>    azdo_branch            = optional(string, "*")<br/>  })</pre> | n/a | yes |
| <a name="input_use_secret"></a> [use\_secret](#input\_use\_secret) | (Required) Should the Service Principal be used to authenticate with Client Secret? | `bool` | n/a | yes |
| <a name="input_app_display_name"></a> [app\_display\_name](#input\_app\_display\_name) | (Optional) The display name of the application associated with this service principal. | `string` | `"My_Automation_Account"` | no |
| <a name="input_description"></a> [description](#input\_description) | (Optional) Description of the SPN being created | `string` | `"Service principal for automation"` | no |
| <a name="input_spn_password"></a> [spn\_password](#input\_spn\_password) | (Optional) List of object references to the Service Principal password | <pre>object({<br/>    display_name = optional(string, null)<br/>    start_date   = optional(any, null)<br/>    end_date     = optional(any, null)<br/>  })</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_application_client_id"></a> [application\_client\_id](#output\_application\_client\_id) | Client ID for the application |
| <a name="output_application_id"></a> [application\_id](#output\_application\_id) | n/a |
| <a name="output_application_object_id"></a> [application\_object\_id](#output\_application\_object\_id) | Application's object ID |
| <a name="output_service_principal_id"></a> [service\_principal\_id](#output\_service\_principal\_id) | n/a |
| <a name="output_service_principal_object_id"></a> [service\_principal\_object\_id](#output\_service\_principal\_object\_id) | n/a |
| <a name="output_service_principal_secret_value"></a> [service\_principal\_secret\_value](#output\_service\_principal\_secret\_value) | n/a |
<!-- END_TF_DOCS -->