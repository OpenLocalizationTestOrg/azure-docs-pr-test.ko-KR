---
title: "개인 Docker 컨테이너 레지스트리 만들기 - Azure CLI | Microsoft Docs"
description: "Azure CLI 2.0을 사용하여 개인 Docker 컨테이너 레지스트리 만들기 및 관리 시작"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: c7cdb1b13bf32388d18c2a25af28337a81861c1e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-cli"></a><span data-ttu-id="46254-103">Azure CLI를 사용하여 관리되는 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="46254-103">Create a managed container registry using the Azure CLI</span></span>

<span data-ttu-id="46254-104">Azure Container Registry는 개인 Docker 컨테이너 이미지를 저장하는 데 사용되는 관리되는 Docker 컨테이너 레지스트리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="46254-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="46254-105">이 가이드에서는 Azure CLI를 사용하여 관리되는 Azure Container Registry 인스턴스를 만드는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-105">This guide details creating a managed Azure Container Registry instance using the Azure CLI.</span></span>

<span data-ttu-id="46254-106">관리되는 Azure 컨테이너 레지스트리는 미리 보기 상태이며 일부 지역에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="46254-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="46254-107">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 빠른 시작에서 Azure CLI 버전 2.0.4 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="46254-108">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="46254-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="46254-109">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="46254-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="46254-110">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="46254-110">Create a resource group</span></span>

<span data-ttu-id="46254-111">[az group create](/cli/azure/group#create) 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46254-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="46254-112">Azure 리소스 그룹은 Azure 리소스가 배포 및 관리되는 논리적 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="46254-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="46254-113">다음 예제에서는 *westcentralus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46254-113">The following example creates a resource group named *myResourceGroup* in the *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="46254-114">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="46254-114">Create a container registry</span></span>

<span data-ttu-id="46254-115">[az acr create](/cli/azure/acr#create) 명령을 사용하여 ACR 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="46254-115">Create an ACR instance using the [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="46254-116">레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="46254-117">이 예제의 레지스트리 이름은 *myContainerRegistry1*이며, 자신만의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="46254-117">The registry name in the example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="46254-118">레지스트리를 만들면 출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-118">When the registry is created, the output is similar to the following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="46254-119">ACR 인스턴스에 로그인</span><span class="sxs-lookup"><span data-stu-id="46254-119">Log in to ACR instance</span></span>

<span data-ttu-id="46254-120">컨테이너 이미지를 밀어넣고 끌어오려면 먼저 ACR 인스턴스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-120">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> <span data-ttu-id="46254-121">이렇게 하려면 [az acr login](/cli/azure/acr#login) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-121">To do so, use the [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="46254-122">이 명령은 완료되면 '로그인했습니다.'라는 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-122">The command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="46254-123">Azure Container Registry 사용</span><span class="sxs-lookup"><span data-stu-id="46254-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="46254-124">컨테이너 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="46254-124">List container images</span></span>

<span data-ttu-id="46254-125">리포지토리의 이미지 및 태그를 쿼리하려면 `az acr` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-125">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="46254-126">현재 Container Registry는 `docker search` 명령으로 이미지 및 태그를 쿼리하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46254-126">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="46254-127">리포지토리 나열</span><span class="sxs-lookup"><span data-stu-id="46254-127">List repositories</span></span>

<span data-ttu-id="46254-128">다음 예제는 레지스트리의 리포지토리를 JSON(JavaScript Object Notation) 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-128">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="46254-129">태그 나열</span><span class="sxs-lookup"><span data-stu-id="46254-129">List tags</span></span>

<span data-ttu-id="46254-130">다음 예제는 **samples/nginx** 리포지토리의 태그를 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="46254-130">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="46254-131">다음 단계</span><span class="sxs-lookup"><span data-stu-id="46254-131">Next steps</span></span>

<span data-ttu-id="46254-132">이 빠른 시작에서는 Azure CLI를 사용하여 관리되는 Azure Container Registry 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="46254-132">In this quick start, you've created a managed Azure Container Registry instance using the Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46254-133">Docker CLI를 사용하여 첫 번째 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="46254-133">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
