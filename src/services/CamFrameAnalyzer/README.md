# CamFrameAnalyzer

## Needed settings for [local.settings.json]

You need to create a new local.settings.json file in the root of the service and add/configure the following in order to be able to set the function locally and generate the KEDA deployment file correctly:

```json

{
  "IsEncrypted": false,
  "serviceBus": {
    "prefetchCount": 1,
    "messageHandlerOptions": {
        "autoComplete": true,
        "maxConcurrentCalls": 32,
        "maxAutoRenewDuration": "00:55:00"
    }
  },
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "serviceBusConnection": "",
    "APPINSIGHTS_INSTRUMENTATIONKEY": "",
    "camFrameStorageConnection": "",
    "cognitiveKey": "",
    "cognitiveEndpoint": "",
    "cosmosDbEndpoint": "",
    "cosmosDbKey": "",
    "faceWorkspaceDataFilter": "Contoso.CrowdAnalytics",
    "KEDA_SERVICE_BUS_CONNECTION": ""
  }
}

```

>NOTE: In the prerequisites provisioning, you created a topic specific service bus connection string. Update ```KEDA_SERVICE_BUS_CONNECTION``` value with the topic specific connection while the ```serviceBusConnection``` will use the namespace level connection.

## KEDA Deployment File Generation

```bash

func kubernetes deploy --name camframe-analyzer --registry $CONTAINER_REGISTRY_NAME.azurecr.io/crowdanalytics --dotnet --dry-run > deploy-updated.yaml

```
