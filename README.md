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

> 2. Install admin tools

Now you can install de admin tools and get the credentials to manage AKS

```
az aks install-cli
```

Get the credentials using the command:

```
az aks get-credentials --resource-group LABSECURITY --name SECURITYAKSDEMO
```

Done! you can check if you can manage the AKS cluster using some commands like:

```
 kubectl get node
 kubectl get pod
 kubectl cluster-info
 ```

 > 2. Create ACR

 Use this command to create Azure Container Registry )ACR):

```
az acr create --resource-group LABSECURITY --name acrlabsecurity --sku Standard
```
> Note: try to use a unique name for --name parameter

After executing this command take note of the parameter **loginServer**. Will be something like acrname.azurecr.io

> Before proceding you need to install a Docker client on your computer in order to upload images.
>  
> Link: https://docs.docker.com/docker-for-windows/install/


- Log in to registry

```
az acr login --name acrlabsecurity.azurecr.io
```

- Push image to registry

Publish these 2 images to ACR. Also you can push another public image.

- - Hello-world
```
docker pull hello-world
docker tag hello-world acrlabsecurity.azurecr.io/hello-world:v1
docker push acrlabsecurity.azurecr.io/hello-world:v1
docker rmi acrlabsecurity.azurecr.io/hello-world:v1
```

- - Nginx


```
docker pull nginx
docker tag nginx acrlabsecurity.azurecr.io/nginx:v1
docker push acrlabsecurity.azurecr.io/nginx:v1
docker rmi acrlabsecurity.azurecr.io/nginx:v1
```

- List container images

Here you can check if both images (Hello-world and Nginx) are available at ACR.

```
az acr repository list --name acrlabsecurity --output table
```
You can also open the Azure Portal and check the ACR.












