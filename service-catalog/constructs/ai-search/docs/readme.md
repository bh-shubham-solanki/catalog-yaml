# Ai Search Services

Construct for using Azure AI Search Service with private endpoint.

## Details

{{Add detailed information about the module}}

## Parameters

| Name                         | Type            | Required | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| :--------------------------- | :-------------: | :------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                       | `string`        | Yes      | Required. The name of the Azure Cognitive Search service to create or update. Search service names must only contain lowercase letters, digits or dashes, cannot use dash as the first two or last one characters, cannot contain consecutive dashes, and must be between 2 and 60 characters in length. Search service names must be globally unique since they are part of the service URI (https://<name>.search.windows.net). You cannot change the service name after the service is created. |
| `authOptions`                | `object`        | No       | Optional. Defines the options for how the data plane API of a Search service authenticates requests. Must remain an empty object {} if 'disableLocalAuth' is set to true.                                                                                                                                                                                                                                                                                                                          |
| `disableLocalAuth`           | `bool`          | No       | Optional. When set to true, calls to the search service will not be permitted to utilize API keys for authentication. This cannot be set to true if 'authOptions' are defined.                                                                                                                                                                                                                                                                                                                     |
| `cmkEnforcement`             | `string`        | No       | Optional. Describes a policy that determines how resources within the search service are to be encrypted with Customer Managed Keys.                                                                                                                                                                                                                                                                                                                                                               |
| `hostingMode`                | `string`        | No       | Optional. Applicable only for the standard3 SKU. You can set this property to enable up to 3 high density partitions that allow up to 1000 indexes, which is much higher than the maximum indexes allowed for any other SKU. For the standard3 SKU, the value is either 'default' or 'highDensity'. For all other SKUs, this value must be 'default'.                                                                                                                                              |
| `location`                   | `string`        | No       | Optional. Location for all Resources.                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `networkRuleSet`             | `object`        | No       | Optional. Network specific rules that determine how the Azure Cognitive Search service may be reached.                                                                                                                                                                                                                                                                                                                                                                                             |
| `partitionCount`             | `int`           | No       | Optional. The number of partitions in the search service; if specified, it can be 1, 2, 3, 4, 6, or 12. Values greater than 1 are only valid for standard SKUs. For 'standard3' services with hostingMode set to 'highDensity', the allowed values are between 1 and 3.                                                                                                                                                                                                                            |
| `privateEndpoints`           | `null | array`  | No       | Optional. Configuration details for private endpoints. For security reasons, it is recommended to use private endpoints whenever possible.                                                                                                                                                                                                                                                                                                                                                         |
| `sharedPrivateLinkResources` | `array`         | No       | Optional. The sharedPrivateLinkResources to create as part of the search Service.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `publicNetworkAccess`        | `string`        | No       | Optional. This value can be set to 'Enabled' to avoid breaking changes on existing customer resources and templates. If set to 'Disabled', traffic over public interface is not allowed, and private endpoint connections would be the exclusive access method.                                                                                                                                                                                                                                    |
| `replicaCount`               | `int`           | No       | Optional. The number of replicas in the search service. If specified, it must be a value between 1 and 12 inclusive for standard SKUs or between 1 and 3 inclusive for basic SKU.                                                                                                                                                                                                                                                                                                                  |
| `semanticSearch`             | `null | string` | No       | Optional. Sets options that control the availability of semantic search. This configuration is only possible for certain search SKUs in certain locations.                                                                                                                                                                                                                                                                                                                                         |
| `sku`                        | `string`        | No       | Optional. Defines the SKU of an Azure Cognitive Search Service, which determines price tier and capacity limits.                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedIdentities`          | `null | object` | No       | Optional. The managed identity definition for this resource.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `diagnosticSettings`         | `null | array`  | No       | Optional. The diagnostic settings of the service.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| `tags`                       | `object`        | No       | Gets or sets a list of key value pairs that describe the resource. These tags can be used for viewing and grouping this resource (across resource groups). A maximum of 15 tags can be provided for a resource. Each tag must have a key with a length no greater than 128 characters and a value with a length no greater than 256 characters.                                                                                                                                                    |

## Outputs

| Name                          | Type     | Description                                                       |
| :---------------------------- | :------: | :---------------------------------------------------------------- |
| `name`                        | `string` | The name of the search service.                                   |
| `resourceId`                  | `string` | The resource ID of the search service.                            |
| `resourceGroupName`           | `string` | The name of the resource group the search service was created in. |
| `systemAssignedMIPrincipalId` | `string` | The principal ID of the system assigned identity.                 |
| `location`                    | `string` | The location the resource was deployed into.                      |
| `privateEndpoints`            | `array`  | The private endpoints of the search service.                      |

## Examples

### Example 1

```bicep
module aiSearch 'br:contregietbmrpet01.azurecr.io/bicep/constructs/ai-search:0.1.0' = {
    name: '${deployment().name}-aisearch'
    params: {
      name: name
      sku: 'standard'
      partitionCount: 1
      replicaCount:1
      disableLocalAuth: true
      location: location
      managedIdentities: {
        systemAssigned: true
      }
      publicNetworkAccess: 'Disabled'
      privateEndpoints: [
        {
          subnetResourceId: subnetId
        }
      ]
    }
  }
```

### Example 2

```bicep
```
