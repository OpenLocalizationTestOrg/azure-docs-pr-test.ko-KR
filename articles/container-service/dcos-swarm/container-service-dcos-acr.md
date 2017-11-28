---
title: "Azure DC/OS 클러스터에 ACR 사용| Microsoft Docs"
description: "Azure Container Service에서 DC/OS 클러스터에 Azure Container Registry 사용"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, 컨테이너, 마이크로 서비스, Mesos, Azure, FileShare, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="09c0e-104">DC/OS 클러스터에 ACR을 사용하여 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="09c0e-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="09c0e-105">이 문서에서는 DC/OS 클러스터에 Azure Container Registry를 사용하는 방법을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="09c0e-106">ACR을 사용하여 컨테이너 이미지를 비공개로 저장하고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="09c0e-107">이 자습서에서 다루는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09c0e-108">Azure Container Registry 배포(필요한 경우)</span><span class="sxs-lookup"><span data-stu-id="09c0e-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="09c0e-109">DC/OS 클러스터에서 ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="09c0e-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="09c0e-110">Azure Container Registry에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="09c0e-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="09c0e-111">Azure Container Registry에서 컨테이너 이미지 실행</span><span class="sxs-lookup"><span data-stu-id="09c0e-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="09c0e-112">이 자습서의 단계를 완료하려면 ACS DC/OS 클러스터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="09c0e-113">필요한 경우 [이 스크립트 샘플](./../kubernetes/scripts/container-service-cli-deploy-dcos.md)을 사용하여 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="09c0e-114">이 자습서에는 Azure CLI 버전 2.0.4 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="09c0e-115">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="09c0e-116">업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09c0e-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="09c0e-117">Azure Container Registry 배포</span><span class="sxs-lookup"><span data-stu-id="09c0e-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="09c0e-118">필요한 경우 [az acr create](/cli/azure/acr#create) 명령으로 Azure Container Registry를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="09c0e-119">다음 예제에서는 임의로 생성된 이름으로 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="09c0e-120">또한 레지스트리는 `--admin-enabled` 인수를 사용하여 관리자 계정으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="09c0e-121">레지스트리가 만들어지면 Azure CLI에서 다음과 유사한 데이터를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="09c0e-122">`name` 및 `loginServer`는 이후 단계에서 사용되므로 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="09c0e-123">[az acr credential show](/cli/azure/acr/credential) 명령을 사용하여 컨테이너 레지스트리 자격 증명을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="09c0e-124">`--name`을 마지막 단계에서 기록한 이름으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="09c0e-125">이후 단계에서 필요하므로 하나의 암호를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="09c0e-126">Azure Container Registry에 대한 자세한 내용은 [개인 Docker 컨테이너 레지스트리 소개](../../container-registry/container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09c0e-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="09c0e-127">ACR 인증 관리</span><span class="sxs-lookup"><span data-stu-id="09c0e-127">Manage ACR authentication</span></span>

<span data-ttu-id="09c0e-128">개인 레지스트리에서 이미지를 밀어넣고 끌어오는 일반적인 방법은 먼저 레지스트리를 인증하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="09c0e-129">이렇게 하려면 개인 레지스트리에 액세스해야 하는 모든 클라이언트에서 `docker login` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="09c0e-130">DC/OS 클러스터는 모두 ACR에 인증되어야 하는 많은 노드를 포함할 수 있으므로 각 노드에서 이 프로세스를 자동화하면 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="09c0e-131">공유 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="09c0e-131">Create shared storage</span></span>

<span data-ttu-id="09c0e-132">이 프로세스에서는 클러스터의 각 노드에 탑재된 Azure 파일 공유를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="09c0e-133">아직 공유 저장소를 설정하지 않은 경우 [DC/OS 클러스터 내부에서 파일 공유 설정](container-service-dcos-fileshare.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09c0e-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="09c0e-134">ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="09c0e-134">Configure ACR authentication</span></span>

<span data-ttu-id="09c0e-135">먼저 DC/OS 마스터의 FQDN을 가져와서 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="09c0e-136">DC/OS 기반 클러스터의 마스터(또는 첫 번째 마스터)와의 SSH 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="09c0e-137">클러스터를 만들 때 기본값이 아닌 값이 사용된 경우 사용자 이름을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="09c0e-138">다음 명령을 실행하여 Azure Container Registry에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="09c0e-139">`--username`을 컨테이너 레지스트리의 이름으로 바꾸고 `--password`를 제공된 암호 중 하나로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="09c0e-140">예제의 마지막 인수 *mycontainerregistry.azurecr.io*를 컨테이너 레지스트리의 loginServer 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="09c0e-141">이 명령은 `~/.docker` 경로 아래에 로컬로 인증 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="09c0e-142">컨테이너 레지스트리 인증 값이 포함된 압축 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="09c0e-143">클러스터 공유 저장소에 이 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="09c0e-144">이 단계를 수행하면 DC/OS 클러스터의 모든 노드에서 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="09c0e-145">ACR에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="09c0e-145">Upload image to ACR</span></span>

<span data-ttu-id="09c0e-146">이제 개발 컴퓨터나 Docker가 설치된 다른 시스템에서 이미지를 만들어 Azure Container Registry에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="09c0e-147">Ubuntu 이미지에서 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="09c0e-148">이제 컨테이너를 새 이미지에 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-148">Now capture the container into a new image.</span></span> <span data-ttu-id="09c0e-149">이미지 이름은 `loginServer/imageName` 형식으로 컨테이너 레지스트리의 `loginServer` 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="09c0e-150">Azure Container Registry에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="09c0e-151">이름을 loginServer 이름으로 바꾸고, --username을 컨테이너 레지스트리의 이름으로 바꾸고, --password를 제공된 암호 중 하나로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="09c0e-152">마지막으로 ACR 레지스트리에 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="09c0e-153">이 예제에서는 dcos-demo라는 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="09c0e-154">ACR에서 이미지 실행</span><span class="sxs-lookup"><span data-stu-id="09c0e-154">Run an image from ACR</span></span>

<span data-ttu-id="09c0e-155">ACR 레지스트리에서 이미지를 사용하려면 파일 이름 *acrDemo.json*을 만들고 다음 텍스트를 이 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="09c0e-156">이미지 이름을 컨테이너 레지스트리 loginServer 이름 및 이미지 이름(예: `loginServer/imageName`)으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="09c0e-157">`uris` 속성을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-157">Take note of the `uris` property.</span></span> <span data-ttu-id="09c0e-158">이 속성은 컨테이너 레지스트리 인증 파일의 위치를 저장하며, 이 경우에는 DC/OS 클러스터의 각 노드에 탑재된 Azure 파일 공유입니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="09c0e-159">DC/OC CLI를 사용하여 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="09c0e-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09c0e-160">Next steps</span></span>

<span data-ttu-id="09c0e-161">이 자습서에서는 다음 작업을 포함하여 Azure Container Registry를 사용하도록 DC/OS를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="09c0e-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09c0e-162">Azure Container Registry 배포(필요한 경우)</span><span class="sxs-lookup"><span data-stu-id="09c0e-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="09c0e-163">DC/OS 클러스터에서 ACR 인증 구성</span><span class="sxs-lookup"><span data-stu-id="09c0e-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="09c0e-164">Azure Container Registry에 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="09c0e-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="09c0e-165">Azure Container Registry에서 컨테이너 이미지 실행</span><span class="sxs-lookup"><span data-stu-id="09c0e-165">Run a container image from the Azure Container Registry</span></span>
