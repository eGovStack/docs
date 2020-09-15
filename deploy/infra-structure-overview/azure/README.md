# Azure

## Azure

### Prepare Azure Environment <a id="prepare-azure-environment"></a>

For provisioning Kubernetes clusters with the [Azure cloud provider](https://github.com/kubermatic/machine-controller/tree/master/pkg/cloudprovider/provider/azure) Kubermatic needs a service account with \(at least\) the the Azure role `Contributor`. Please follow the following steps to create an matching service account:

#### Login to Azure and Get Basic Information <a id="login-to-azure-and-get-basic-information"></a>

Login to Azure with [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) `az`.

This command will open in your default browser a window where you can authenticate. After you succefull logged in get your subscription ID.

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

