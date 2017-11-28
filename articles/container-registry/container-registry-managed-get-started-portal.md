---
title: "개인 Docker 레지스트리 만들기 - Azure Portal | Microsoft Docs"
description: "Azure Portal을 사용하여 개인 Docker 컨테이너 레지스트리 만들기 및 관리 시작"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="b5caf-103">Azure Portal을 사용하여 관리 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="b5caf-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="b5caf-104">Azure Container Registry는 개인 Docker 컨테이너 이미지를 저장하는 데 사용되는 관리되는 Docker 컨테이너 레지스트리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="b5caf-105">이 가이드에서는 Azure Portal을 사용하여 관리되는 Azure Container Registry 인스턴스를 만드는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="b5caf-106">관리되는 Azure 컨테이너 레지스트리는 미리 보기 상태이며 일부 지역에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b5caf-107">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="b5caf-107">Log in to Azure</span></span>

<span data-ttu-id="b5caf-108">Azure Portal( http://portal.azure.com )에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b5caf-109">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="b5caf-109">Create a container registry</span></span>

1. <span data-ttu-id="b5caf-110">Azure Portal의 왼쪽 위에 있는 **새로 만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="b5caf-111">마켓플레이스에서 **Azure 컨테이너 레지스트리**를 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="b5caf-112">**만들기**를 클릭하면 ACR 만들기 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="b5caf-114">**Azure 컨테이너 레지스트리** 블레이드에서 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="b5caf-115">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="b5caf-116">a.</span><span class="sxs-lookup"><span data-stu-id="b5caf-116">a.</span></span> <span data-ttu-id="b5caf-117">**레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="b5caf-118">이 예제에서 레지스트리 이름은 *myAzureContainerRegistry1*이지만 자신만의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="b5caf-119">이름은 문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="b5caf-120">b.</span><span class="sxs-lookup"><span data-stu-id="b5caf-120">b.</span></span> <span data-ttu-id="b5caf-121">**리소스 그룹**: 기존 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 선택하거나 새 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="b5caf-122">c.</span><span class="sxs-lookup"><span data-stu-id="b5caf-122">c.</span></span> <span data-ttu-id="b5caf-123">**위치**: **미국 중남부**와 같이 서비스를 [사용할 수 있는](https://azure.microsoft.com/regions/services/) Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="b5caf-124">d.</span><span class="sxs-lookup"><span data-stu-id="b5caf-124">d.</span></span> <span data-ttu-id="b5caf-125">**관리 사용자**: 필요한 경우 관리 사용자가 레지스트리에 액세스할 수 있도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="b5caf-126">이 설정은 레지스트리를 만든 후에 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="b5caf-127">e.</span><span class="sxs-lookup"><span data-stu-id="b5caf-127">e.</span></span> <span data-ttu-id="b5caf-128">**관리되는 레지스트리 사용**: ACR에서 자동으로 레지스트리 저장소를 관리하고, 웹후크를 사용하고, AAD 인증을 사용하도록 하려면 '예'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="b5caf-129">f.</span><span class="sxs-lookup"><span data-stu-id="b5caf-129">f.</span></span> <span data-ttu-id="b5caf-130">**가격 책정 계층**: 가격 책정 계층을 선택합니다. 자세한 내용은 ACR 가격 책정을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b5caf-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="b5caf-131">ACR 인스턴스에 로그인</span><span class="sxs-lookup"><span data-stu-id="b5caf-131">Log in to ACR instance</span></span>

<span data-ttu-id="b5caf-132">컨테이너 이미지를 밀어넣고 끌어오려면 먼저 ACR 인스턴스에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="b5caf-133">이렇게 하려면 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="b5caf-134">먼저 필요한 경우 [az login](/cli/azure/#login) 명령을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="b5caf-135">다음으로 [az acr login](/cli/azure/acr#login) 명령을 사용하여 Azure Container Registry에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="b5caf-136">Azure Container Registry 사용</span><span class="sxs-lookup"><span data-stu-id="b5caf-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="b5caf-137">컨테이너 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="b5caf-137">List container images</span></span>

<span data-ttu-id="b5caf-138">리포지토리의 이미지 및 태그를 쿼리하려면 `az acr` CLI 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b5caf-139">현재 Container Registry는 `docker search` 명령으로 이미지 및 태그를 쿼리하도록 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="b5caf-140">리포지토리 나열</span><span class="sxs-lookup"><span data-stu-id="b5caf-140">List repositories</span></span>

<span data-ttu-id="b5caf-141">다음 예제는 레지스트리의 리포지토리를 JSON(JavaScript Object Notation) 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="b5caf-142">태그 나열</span><span class="sxs-lookup"><span data-stu-id="b5caf-142">List tags</span></span>

<span data-ttu-id="b5caf-143">다음 예제는 **samples/nginx** 리포지토리의 태그를 JSON 형식으로 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="b5caf-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b5caf-144">Next steps</span></span>

<span data-ttu-id="b5caf-145">이 빠른 시작에서는 Azure Portal을 사용하여 관리되는 Azure Container Registry 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b5caf-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b5caf-146">Docker CLI를 사용하여 첫 번째 이미지 푸시</span><span class="sxs-lookup"><span data-stu-id="b5caf-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)