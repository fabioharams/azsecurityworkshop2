# Azure Security Workshop | Part 2
This second part will focus on containers (Azure Kubernetes Service and Azure Container Registry) protected by Azure Security Center.

> Note: You will need to deploy the first part of this workshop. Link available here: https://github.com/fabioharams/azsecurityworkshop2


> 1. Create AKS Cluster

Before you start just remember to create the Service Principal for AKS:

```
az ad sp create-for-rbac --skip-assignment --name serviceprincipalaksdemo1
```
> Note: try to use a unique name for --name parameter

The output will be something like this:

```
{
  "appId": "rrrrrrrr-rrrr-4b3c-rrrr-rrrrrrrrrrrr",
  "displayName": "serviceprincipalaksdemo1",
  "name": "http://serviceprincipalaksdemo1",
  "password": "yy-yy_yyyylFk5yyyyy-yyyyy7yyyyyq73",
  "tenant": "72xxxxxx-8xxx-4xxx-xxxx-xxxxxxxxxxxx"
}
```

Now using these values you can create an AKS Cluster

```
az aks create --resource-group LABSECURITY --name SECURITYAKSDEMO --service principal <appId> --client-secret <password>
```

If you need more information about this procedure please follow [this link](https://docs.microsoft.com/en-us/azure/aks/kubernetes-service-principal)

Wait few minutes and your AKS Cluster will be finished. 



