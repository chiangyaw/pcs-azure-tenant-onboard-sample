# Prisma Cloud Azure Tenant Onboarding Terraform Template Sample
## Overview
This is an example of a Terraform template generated from Prisma Cloud to onboard an Azure Tenant. The following items have been enabled as part of this onboarding:

Default/Mandatory:
*   Misconfiguration (CSPM)
*   Identity Security
*   Threat Detection

Optional Security Capabilities:
*   Agentless Workload Scanning
*   Serverless Function Scanning

Optional security capabilities can be disabled as per organizations' needs and requirement.

## Terraform Script Details

This Terraform script automates the creation and configuration of Azure Active Directory (Azure AD) application and service principal, along with setting up necessary Azure Resource Manager (ARM) role assignments for Prisma Cloud.

Here is a summary of the items covered in the Terraform Script:

* Creates an Azure AD application and service principal.
* Generates a client secret for the specific Azure AD application.
* Creates custom Azure roles for Prisma Cloud.
* Assigns necessary roles to the service principal at the tenant and resource group scopes.
* Creates resource groups as needed for agentless scanning.
* Runs checks for proper user permissions.
* Return the required details such as Application ID, client secret, and Object ID once the provisioning is completed.

### Permission required for custom roles
There are 2 custom roles created on top of `Reader` role, one for generic posture security, and another for agentless workload scanning, and here are the list of permissions required:

custom_agentless_resource_group_role_actions
```
[
    "Microsoft.Compute/disks/delete",
    "Microsoft.Compute/disks/write",
    "Microsoft.Compute/snapshots/delete",
    "Microsoft.Compute/snapshots/write",
    "Microsoft.Compute/virtualMachines/delete",
    "Microsoft.Compute/virtualMachines/write",
    "Microsoft.Network/networkInterfaces/delete",
    "Microsoft.Network/networkInterfaces/join/action",
    "Microsoft.Network/networkInterfaces/write",
    "Microsoft.Network/networkSecurityGroups/delete",
    "Microsoft.Network/networkSecurityGroups/join/action",
    "Microsoft.Network/networkSecurityGroups/write",
    "Microsoft.Network/virtualNetworks/delete",
    "Microsoft.Network/virtualNetworks/subnets/join/action",
    "Microsoft.Network/virtualNetworks/write"
]
```
custom_role_actions
```
[
    "Microsoft.Advisor/configurations/read",
    "Microsoft.AlertsManagement/prometheusRuleGroups/read",
    "Microsoft.AlertsManagement/smartDetectorAlertRules/read",
    "Microsoft.AnalysisServices/servers/read",
    "Microsoft.ApiManagement/service/apis/diagnostics/read",
    "Microsoft.ApiManagement/service/apis/policies/read",
    "Microsoft.ApiManagement/service/apis/read",
    "Microsoft.ApiManagement/service/identityProviders/read",
    "Microsoft.ApiManagement/service/portalsettings/read",
    "Microsoft.ApiManagement/service/products/policies/read",
    "Microsoft.ApiManagement/service/products/read",
    "Microsoft.ApiManagement/service/read",
    "Microsoft.ApiManagement/service/subscriptions/read",
    "Microsoft.ApiManagement/service/tenant/read",
    "Microsoft.AppConfiguration/configurationStores/read",
    "Microsoft.AppPlatform/Spring/apps/read",
    "Microsoft.AppPlatform/Spring/read",
    "Microsoft.Attestation/attestationProviders/read",
    "Microsoft.Authorization/classicAdministrators/read",
    "Microsoft.Authorization/locks/read",
    "Microsoft.Authorization/permissions/read",
    "Microsoft.Authorization/policyAssignments/read",
    "Microsoft.Authorization/policyDefinitions/read",
    "Microsoft.Authorization/roleAssignments/read",
    "Microsoft.Authorization/roleDefinitions/read",
    "Microsoft.Automanage/configurationProfiles/Read",
    "Microsoft.Automation/automationAccounts/credentials/read",
    "Microsoft.Automation/automationAccounts/hybridRunbookWorkerGroups/hybridRunbookWorkers/read",
    "Microsoft.Automation/automationAccounts/hybridRunbookWorkerGroups/read",
    "Microsoft.Automation/automationAccounts/read",
    "Microsoft.Automation/automationAccounts/runbooks/read",
    "Microsoft.Automation/automationAccounts/variables/read",
    "Microsoft.AzureStackHCI/Clusters/Read",
    "Microsoft.Batch/batchAccounts/applications/read",
    "Microsoft.Batch/batchAccounts/pools/read",
    "Microsoft.Batch/batchAccounts/read",
    "Microsoft.Blueprint/blueprints/read",
    "Microsoft.BotService/botServices/read",
    "Microsoft.Cache/redis/firewallRules/read",
    "Microsoft.Cache/redis/read",
    "Microsoft.Cache/redisEnterprise/read",
    "Microsoft.Cdn/profiles/afdendpoints/read",
    "Microsoft.Cdn/profiles/afdendpoints/routes/read",
    "Microsoft.Cdn/profiles/customdomains/read",
    "Microsoft.Cdn/profiles/endpoints/customdomains/read",
    "Microsoft.Cdn/profiles/endpoints/read",
    "Microsoft.Cdn/profiles/origingroups/read",
    "Microsoft.Cdn/profiles/read",
    "Microsoft.Cdn/profiles/securitypolicies/read",
    "Microsoft.Chaos/experiments/read",
    "Microsoft.ClassicCompute/VirtualMachines/read",
    "Microsoft.ClassicNetwork/networkSecurityGroups/read",
    "Microsoft.ClassicNetwork/reservedIps/read",
    "Microsoft.ClassicNetwork/virtualNetworks/read",
    "Microsoft.ClassicStorage/StorageAccounts/read",
    "Microsoft.CognitiveServices/accounts/read",
    "Microsoft.Communication/CommunicationServices/Read",
    "Microsoft.Compute/availabilitySets/read",
    "Microsoft.Compute/cloudServices/read",
    "Microsoft.Compute/cloudServices/roleInstances/read",
    "Microsoft.Compute/diskEncryptionSets/read",
    "Microsoft.Compute/disks/beginGetAccess/action",
    "Microsoft.Compute/disks/read",
    "Microsoft.Compute/galleries/images/read",
    "Microsoft.Compute/galleries/read",
    "Microsoft.Compute/hostGroups/read",
    "Microsoft.Compute/proximityPlacementGroups/read",
    "Microsoft.Compute/restorePointCollections/read",
    "Microsoft.Compute/snapshots/read",
    "Microsoft.Compute/virtualMachineScaleSets/networkInterfaces/read",
    "Microsoft.Compute/virtualMachineScaleSets/publicIPAddresses/read",
    "Microsoft.Compute/virtualMachineScaleSets/read",
    "Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/ipConfigurations/publicIPAddresses/read",
    "Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read",
    "Microsoft.Compute/virtualMachineScaleSets/virtualmachines/instanceView/read",
    "Microsoft.Compute/virtualMachines/extensions/read",
    "Microsoft.Compute/virtualMachines/instanceView/read",
    "Microsoft.Compute/virtualMachines/read",
    "Microsoft.Confluent/organizations/Read",
    "Microsoft.ContainerInstance/containerGroups/containers/exec/action",
    "Microsoft.ContainerInstance/containerGroups/read",
    "Microsoft.ContainerRegistry/registries/cacheRules/read",
    "Microsoft.ContainerRegistry/registries/metadata/read",
    "Microsoft.ContainerRegistry/registries/pull/read",
    "Microsoft.ContainerRegistry/registries/read",
    "Microsoft.ContainerRegistry/registries/webhooks/getCallbackConfig/action",
    "Microsoft.ContainerService/managedClusters/read",
    "Microsoft.DBforMariaDB/servers/firewallRules/read",
    "Microsoft.DBforMariaDB/servers/read",
    "Microsoft.DBforMySQL/flexibleServers/configurations/read",
    "Microsoft.DBforMySQL/flexibleServers/databases/read",
    "Microsoft.DBforMySQL/flexibleServers/firewallRules/read",
    "Microsoft.DBforMySQL/flexibleServers/read",
    "Microsoft.DBforMySQL/servers/firewallRules/read",
    "Microsoft.DBforMySQL/servers/read",
    "Microsoft.DBforMySQL/servers/virtualNetworkRules/read",
    "Microsoft.DBforPostgreSQL/flexibleServers/configurations/read",
    "Microsoft.DBforPostgreSQL/flexibleServers/databases/read",
    "Microsoft.DBforPostgreSQL/flexibleServers/firewallRules/read",
    "Microsoft.DBforPostgreSQL/flexibleServers/read",
    "Microsoft.DBforPostgreSQL/servers/configurations/read",
    "Microsoft.DBforPostgreSQL/servers/firewallRules/read",
    "Microsoft.DBforPostgreSQL/servers/read",
    "Microsoft.DBforPostgreSQL/serversv2/firewallRules/read",
    "Microsoft.Dashboard/grafana/read",
    "Microsoft.DataBoxEdge/dataBoxEdgeDevices/read",
    "Microsoft.DataFactory/datafactories/read",
    "Microsoft.DataFactory/factories/integrationruntimes/read",
    "Microsoft.DataFactory/factories/linkedservices/read",
    "Microsoft.DataFactory/factories/read",
    "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts/read",
    "Microsoft.DataLakeAnalytics/accounts/firewallRules/read",
    "Microsoft.DataLakeAnalytics/accounts/read",
    "Microsoft.DataLakeAnalytics/accounts/storageAccounts/read",
    "Microsoft.DataLakeStore/accounts/firewallRules/read",
    "Microsoft.DataLakeStore/accounts/read",
    "Microsoft.DataLakeStore/accounts/trustedIdProviders/read",
    "Microsoft.DataLakeStore/accounts/virtualNetworkRules/read",
    "Microsoft.DataMigration/services/read",
    "Microsoft.DataProtection/backupVaults/backupInstances/read",
    "Microsoft.DataProtection/backupVaults/backupInstances/recoveryPoints/read",
    "Microsoft.DataProtection/backupVaults/backupJobs/read",
    "Microsoft.DataProtection/backupVaults/backupPolicies/read",
    "Microsoft.DataProtection/backupVaults/read",
    "Microsoft.DataShare/accounts/read",
    "Microsoft.Databricks/accessConnectors/read",
    "Microsoft.Databricks/workspaces/read",
    "Microsoft.Datadog/monitors/read",
    "Microsoft.DesktopVirtualization/applicationgroups/read",
    "Microsoft.DesktopVirtualization/hostpools/read",
    "Microsoft.DesktopVirtualization/hostpools/sessionhostconfigurations/read",
    "Microsoft.DesktopVirtualization/hostpools/sessionhosts/read",
    "Microsoft.DesktopVirtualization/workspaces/providers/Microsoft.Insights/diagnosticSettings/read",
    "Microsoft.DesktopVirtualization/workspaces/read",
    "Microsoft.DevCenter/devcenters/read",
    "Microsoft.DevTestLab/schedules/read",
    "Microsoft.Devices/iotHubs/Read",
    "Microsoft.Devices/iotHubs/privateLinkResources/Read",
    "Microsoft.DigitalTwins/digitalTwinsInstances/read",
    "Microsoft.DocumentDB/cassandraClusters/read",
    "Microsoft.DocumentDB/databaseAccounts/listConnectionStrings/action",
    "Microsoft.DocumentDB/databaseAccounts/listKeys/action",
    "Microsoft.DocumentDB/databaseAccounts/read",
    "Microsoft.DocumentDB/databaseAccounts/readonlykeys/action",
    "Microsoft.DomainRegistration/domains/Read",
    "Microsoft.Easm/workspaces/read",
    "Microsoft.Elastic/monitors/read",
    "Microsoft.EventGrid/domains/privateLinkResources/read",
    "Microsoft.EventGrid/domains/read",
    "Microsoft.EventGrid/namespaces/read",
    "Microsoft.EventGrid/partnerNamespaces/read",
    "Microsoft.EventGrid/topics/privateLinkResources/read",
    "Microsoft.EventGrid/topics/read",
    "Microsoft.EventHub/Namespaces/PrivateEndpointConnections/read",
    "Microsoft.EventHub/clusters/read",
    "Microsoft.EventHub/namespaces/authorizationRules/read",
    "Microsoft.EventHub/namespaces/eventhubs/authorizationRules/read",
    "Microsoft.EventHub/namespaces/eventhubs/read",
    "Microsoft.EventHub/namespaces/ipfilterrules/read",
    "Microsoft.EventHub/namespaces/read",
    "Microsoft.EventHub/namespaces/virtualnetworkrules/read",
    "Microsoft.HDInsight/clusters/applications/read",
    "Microsoft.HDInsight/clusters/read",
    "Microsoft.HealthBot/healthBots/Read",
    "Microsoft.HealthcareApis/workspaces/read",
    "Microsoft.HybridCompute/machines/read",
    "Microsoft.Insights/ActivityLogAlerts/read",
    "Microsoft.Insights/Components/read",
    "Microsoft.Insights/DataCollectionEndpoints/Read",
    "Microsoft.Insights/DataCollectionRules/Read",
    "Microsoft.Insights/DiagnosticSettings/Read",
    "Microsoft.Insights/LogProfiles/read",
    "Microsoft.Insights/MetricAlerts/Read",
    "Microsoft.Insights/Workbooks/Read",
    "Microsoft.Insights/actionGroups/read",
    "Microsoft.Insights/diagnosticSettings/read",
    "Microsoft.Insights/eventtypes/values/read",
    "Microsoft.IoTCentral/IoTApps/read",
    "Microsoft.KeyVault/vaults/keys/read",
    "Microsoft.KeyVault/vaults/privateLinkResources/read",
    "Microsoft.KeyVault/vaults/read",
    "Microsoft.Kusto/Clusters/Databases/DataConnections/read",
    "Microsoft.Kusto/Clusters/Databases/read",
    "Microsoft.Kusto/Clusters/read",
    "Microsoft.Kusto/clusters/read",
    "Microsoft.LabServices/labs/read",
    "Microsoft.LoadTestService/loadTests/outboundNetworkDependenciesEndpoints/read",
    "Microsoft.LoadTestService/loadTests/read",
    "Microsoft.Logic/integrationAccounts/read",
    "Microsoft.Logic/workflows/read",
    "Microsoft.Logic/workflows/versions/read",
    "Microsoft.MachineLearningServices/workspaces/computes/read",
    "Microsoft.MachineLearningServices/workspaces/outboundRules/read",
    "Microsoft.MachineLearningServices/workspaces/read",
    "Microsoft.ManagedIdentity/userAssignedIdentities/read",
    "Microsoft.ManagedServices/marketplaceRegistrationDefinitions/read",
    "Microsoft.ManagedServices/registrationAssignments/read",
    "Microsoft.Management/managementGroups/descendants/read",
    "Microsoft.Management/managementGroups/read",
    "Microsoft.Management/managementGroups/subscriptions/read",
    "Microsoft.Maps/accounts/read",
    "Microsoft.Migrate/moveCollections/read",
    "Microsoft.MixedReality/ObjectAnchorsAccounts/read",
    "Microsoft.NetApp/netAppAccounts/capacityPools/read",
    "Microsoft.NetApp/netAppAccounts/capacityPools/volumes/read",
    "Microsoft.NetApp/netAppAccounts/read",
    "Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies/read",
    "Microsoft.Network/applicationGateways/read",
    "Microsoft.Network/applicationSecurityGroups/read",
    "Microsoft.Network/azurefirewalls/read",
    "Microsoft.Network/bastionHosts/read",
    "Microsoft.Network/connections/read",
    "Microsoft.Network/ddosProtectionPlans/read",
    "Microsoft.Network/dnsZones/read",
    "Microsoft.Network/expressRouteCircuits/authorizations/read",
    "Microsoft.Network/expressRouteCircuits/peerings/connections/read",
    "Microsoft.Network/expressRouteCircuits/peerings/peerConnections/read",
    "Microsoft.Network/expressRouteCircuits/peerings/read",
    "Microsoft.Network/expressRouteCircuits/read",
    "Microsoft.Network/expressRouteCrossConnections/peerings/read",
    "Microsoft.Network/expressRouteCrossConnections/read",
    "Microsoft.Network/expressRouteGateways/expressRouteConnections/read",
    "Microsoft.Network/expressRouteGateways/read",
    "Microsoft.Network/expressRoutePorts/authorizations/read",
    "Microsoft.Network/expressRoutePorts/links/read",
    "Microsoft.Network/expressRoutePorts/read",
    "Microsoft.Network/expressRoutePortsLocations/read",
    "Microsoft.Network/firewallPolicies/read",
    "Microsoft.Network/frontDoorWebApplicationFirewallPolicies/read",
    "Microsoft.Network/frontDoors/backendPools/read",
    "Microsoft.Network/frontDoors/frontendEndpoints/read",
    "Microsoft.Network/frontDoors/healthProbeSettings/read",
    "Microsoft.Network/frontDoors/loadBalancingSettings/read",
    "Microsoft.Network/frontDoors/read",
    "Microsoft.Network/frontDoors/routingRules/read",
    "Microsoft.Network/frontDoors/rulesEngines/read",
    "Microsoft.Network/loadBalancers/read",
    "Microsoft.Network/localnetworkgateways/read",
    "Microsoft.Network/locations/usages/read",
    "Microsoft.Network/natGateways/read",
    "Microsoft.Network/networkInterfaces/effectiveNetworkSecurityGroups/action",
    "Microsoft.Network/networkInterfaces/effectiveRouteTable/action",
    "Microsoft.Network/networkInterfaces/read",
    "Microsoft.Network/networkManagers/read",
    "Microsoft.Network/networkSecurityGroups/defaultSecurityRules/read",
    "Microsoft.Network/networkSecurityGroups/read",
    "Microsoft.Network/networkSecurityGroups/securityRules/read",
    "Microsoft.Network/networkWatchers/queryFlowLogStatus/*",
    "Microsoft.Network/networkWatchers/read",
    "Microsoft.Network/networkWatchers/securityGroupView/action",
    "Microsoft.Network/p2sVpnGateways/read",
    "Microsoft.Network/privateDnsZones/ALL/read",
    "Microsoft.Network/privateDnsZones/read",
    "Microsoft.Network/privateEndpoints/privateDnsZoneGroups/read",
    "Microsoft.Network/privateEndpoints/read",
    "Microsoft.Network/privateLinkServices/read",
    "Microsoft.Network/publicIPAddresses/read",
    "Microsoft.Network/publicIPPrefixes/read",
    "Microsoft.Network/routeFilters/read",
    "Microsoft.Network/routeFilters/routeFilterRules/read",
    "Microsoft.Network/routeTables/read",
    "Microsoft.Network/routeTables/routes/read",
    "Microsoft.Network/serviceEndpointPolicies/read",
    "Microsoft.Network/serviceEndpointPolicies/serviceEndpointPolicyDefinitions/read",
    "Microsoft.Network/trafficManagerProfiles/read",
    "Microsoft.Network/virtualHubs/read",
    "Microsoft.Network/virtualNetworkGateways/read",
    "Microsoft.Network/virtualNetworks/read",
    "Microsoft.Network/virtualNetworks/subnets/read",
    "Microsoft.Network/virtualNetworks/virtualNetworkPeerings/read",
    "Microsoft.Network/virtualWans/read",
    "Microsoft.Network/virtualwans/vpnconfiguration/action",
    "Microsoft.Network/vpnServerConfigurations/read",
    "Microsoft.NetworkFunction/azureTrafficCollectors/read",
    "Microsoft.NotificationHubs/Namespaces/NotificationHubs/read",
    "Microsoft.NotificationHubs/Namespaces/read",
    "Microsoft.OperationalInsights/clusters/read",
    "Microsoft.OperationalInsights/querypacks/read",
    "Microsoft.OperationalInsights/workspaces/read",
    "Microsoft.OperationalInsights/workspaces/tables/read",
    "Microsoft.Orbital/spacecrafts/read",
    "Microsoft.PowerBIDedicated/capacities/read",
    "Microsoft.PowerBIDedicated/servers/read",
    "Microsoft.Quantum/Workspaces/Read",
    "Microsoft.RecoveryServices/Vaults/backupProtectedItems/read",
    "Microsoft.RecoveryServices/Vaults/read",
    "Microsoft.RecoveryServices/vaults/backupPolicies/read",
    "Microsoft.RedHatOpenShift/openShiftClusters/read",
    "Microsoft.Relay/Namespaces/read",
    "Microsoft.Resources/Resources/read",
    "Microsoft.Resources/subscriptions/providers/read",
    "Microsoft.Resources/subscriptions/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Resources/subscriptions/resourceGroups/write",
    "Microsoft.Resources/templateSpecs/read",
    "Microsoft.SaaS/applications/read",
    "Microsoft.Search/searchServices/read",
    "Microsoft.Security/advancedThreatProtectionSettings/read",
    "Microsoft.Security/autoProvisioningSettings/read",
    "Microsoft.Security/automations/read",
    "Microsoft.Security/iotSecuritySolutions/read",
    "Microsoft.Security/locations/jitNetworkAccessPolicies/read",
    "Microsoft.Security/locations/read",
    "Microsoft.Security/pricings/read",
    "Microsoft.Security/secureScores/read",
    "Microsoft.Security/securityContacts/read",
    "Microsoft.Security/settings/read",
    "Microsoft.Security/workspaceSettings/read",
    "Microsoft.ServiceBus/namespaces/authorizationRules/read",
    "Microsoft.ServiceBus/namespaces/networkrulesets/read",
    "Microsoft.ServiceBus/namespaces/privateEndpointConnections/read",
    "Microsoft.ServiceBus/namespaces/providers/Microsoft.Insights/diagnosticSettings/read",
    "Microsoft.ServiceBus/namespaces/queues/read",
    "Microsoft.ServiceBus/namespaces/read",
    "Microsoft.ServiceBus/namespaces/topics/read",
    "Microsoft.ServiceBus/namespaces/topics/subscriptions/read",
    "Microsoft.ServiceFabric/clusters/read",
    "Microsoft.SignalRService/SignalR/read",
    "Microsoft.SignalRService/WebPubSub/read",
    "Microsoft.Solutions/applications/read",
    "Microsoft.Sql/managedInstances/databases/read",
    "Microsoft.Sql/managedInstances/databases/transparentDataEncryption/read",
    "Microsoft.Sql/managedInstances/encryptionProtector/Read",
    "Microsoft.Sql/managedInstances/read",
    "Microsoft.Sql/managedInstances/vulnerabilityAssessments/Read",
    "Microsoft.Sql/servers/administrators/read",
    "Microsoft.Sql/servers/auditingSettings/read",
    "Microsoft.Sql/servers/databases/auditingSettings/read",
    "Microsoft.Sql/servers/databases/dataMaskingPolicies/read",
    "Microsoft.Sql/servers/databases/dataMaskingPolicies/rules/read",
    "Microsoft.Sql/servers/databases/read",
    "Microsoft.Sql/servers/databases/securityAlertPolicies/read",
    "Microsoft.Sql/servers/databases/transparentDataEncryption/read",
    "Microsoft.Sql/servers/encryptionProtector/read",
    "Microsoft.Sql/servers/firewallRules/read",
    "Microsoft.Sql/servers/read",
    "Microsoft.Sql/servers/securityAlertPolicies/read",
    "Microsoft.Sql/servers/vulnerabilityAssessments/read",
    "Microsoft.SqlVirtualMachine/sqlVirtualMachines/read",
    "Microsoft.Storage/storageAccounts/blobServices/read",
    "Microsoft.Storage/storageAccounts/fileServices/read",
    "Microsoft.Storage/storageAccounts/fileServices/shares/read",
    "Microsoft.Storage/storageAccounts/listKeys/action",
    "Microsoft.Storage/storageAccounts/providers/Microsoft.Insights/diagnosticSettings/read",
    "Microsoft.Storage/storageAccounts/queueServices/read",
    "Microsoft.Storage/storageAccounts/read",
    "Microsoft.Storage/storageAccounts/tableServices/read",
    "Microsoft.StorageCache/Subscription/caches/read",
    "Microsoft.StorageCache/caches/read",
    "Microsoft.StorageMover/storageMovers/read",
    "Microsoft.StorageSync/storageSyncServices/privateLinkResources/read",
    "Microsoft.StorageSync/storageSyncServices/read",
    "Microsoft.StreamAnalytics/clusters/Read",
    "Microsoft.StreamAnalytics/streamingjobs/Read",
    "Microsoft.Subscription/Policies/default/read",
    "Microsoft.Synapse/privateLinkHubs/privateLinkResources/read",
    "Microsoft.Synapse/privateLinkHubs/read",
    "Microsoft.Synapse/workspaces/privateLinkResources/read",
    "Microsoft.Synapse/workspaces/read",
    "Microsoft.Synapse/workspaces/sparkConfigurations/read",
    "Microsoft.Synapse/workspaces/sqlPools/geoBackupPolicies/read",
    "Microsoft.Synapse/workspaces/sqlPools/read",
    "Microsoft.VideoIndexer/accounts/read",
    "Microsoft.VisualStudio/Account/Read",
    "Microsoft.Web/certificates/read",
    "Microsoft.Web/connections/Read",
    "Microsoft.Web/customApis/read",
    "Microsoft.Web/hostingEnvironments/Read",
    "Microsoft.Web/serverfarms/Read",
    "Microsoft.Web/sites/Read",
    "Microsoft.Web/sites/basicPublishingCredentialsPolicies/Read",
    "Microsoft.Web/sites/config/list/Action",
    "Microsoft.Web/sites/config/list/action",
    "Microsoft.Web/sites/config/read",
    "Microsoft.Web/sites/privateEndpointConnections/Read",
    "Microsoft.Web/sites/publishxml/action",
    "Microsoft.Web/sites/read",
    "Microsoft.Web/sites/slots/Read",
    "Microsoft.Web/staticSites/Read",
    "Microsoft.Workloads/monitors/read",
    "Microsoft.classicCompute/domainNames/read",
    "Microsoft.web/sites/functions/action",
    "Microsoft.web/sites/functions/read",
    "microsoft.app/containerapps/read",
    "microsoft.monitor/accounts/read",
    "microsoft.network/virtualnetworkgateways/connections/read",
    "microsoft.web/serverfarms/sites/read"
]
```

## Other References
To onboard an Azure Tenant manually without using Terraform script, refer to the techdoc [here](https://docs.prismacloud.io/en/enterprise-edition/content-collections/connect/connect-cloud-accounts/onboard-your-azure-account/connect-azure-tenant).

## Conclusion
This is just a sample Terraform script to onboard Azure Tenant. For actual Terraform script, please generate the updated script from Prisma Cloud.