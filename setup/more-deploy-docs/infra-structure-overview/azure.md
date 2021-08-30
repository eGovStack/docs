# Azure

## Prepare Azure Environment

For provisioning Kubernetes clusters with the [Azure cloud provider](https://github.com/kubermatic/machine-controller/tree/master/pkg/cloudprovider/provider/azure) Kubermatic needs a service account with \(at least\) the Azure role `Contributor`. Please follow the following steps to create a matching service account.

## Login to Azure and Get Basic Information

Login to Azure with [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) `az`.

This command will open in your default browser a window where you can authenticate. After you succefully logged in get your subscription ID.

```text
az account show --query id -o json

********-****-****-****-************
```

Get your Tenant ID

```text
az account show --query tenantId -o json

********-****-****-****-************
```

create a new app with

```text
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/********-****-****-****-************"

Retrying role assignment creation: 1/36
Retrying role assignment creation: 2/36
Retrying role assignment creation: 3/36
{
  "appId": "********-****-****-****-************",
  "displayName": "azure-cli-2018-11-25-08-01-39",
  "name": "http://azure-cli-2018-11-25-08-01-39",
  "password": "********-****-****-****-************",
  "tenant": "********-****-****-****-************"
}
```

Enter provider credentials using the values from step “Prepare Azure Environment” into Kubermatic Dashboard:

* `Client ID`: Take the value of `appId`
* `Client Secret`: Take the value of `password`
* `Tenant ID`: your tenant ID
* `Subscription ID`: your subscription ID

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

