---
title: "aaaCreate 개인 Docker 레지스트리-Azure 포털 | Microsoft Docs"
description: "만들기 및 관리 사설 Docker 컨테이너 레지스트리 Azure 포털 hello로 시작."
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
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="39313-103">Hello Azure 포털을 사용 하 여 관리 되는 컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="39313-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="39313-104">Azure Container Registry는 개인 Docker 컨테이너 이미지를 저장하는 데 사용되는 관리되는 Docker 컨테이너 레지스트리 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="39313-105">이 가이드 hello Azure 포털을 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만드는 방법을 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="39313-106">관리되는 Azure 컨테이너 레지스트리는 미리 보기 상태이며 일부 지역에서는 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="39313-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="39313-107">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="39313-107">Log in tooAzure</span></span>

<span data-ttu-id="39313-108">Azure 포털에서 http://portal.azure.com toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="39313-109">컨테이너 레지스트리 만들기</span><span class="sxs-lookup"><span data-stu-id="39313-109">Create a container registry</span></span>

1. <span data-ttu-id="39313-110">Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39313-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="39313-111">에 대 한 검색 hello 마켓플레이스 **Azure 컨테이너 레지스트리** 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="39313-112">클릭 **만들기** hello ACR 만들기 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="39313-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![컨테이너 레지스트리 설정](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="39313-114">Hello에 **Azure 컨테이너 레지스트리** 블레이드에서 hello 다음 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="39313-115">완료하면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="39313-116">a.</span><span class="sxs-lookup"><span data-stu-id="39313-116">a.</span></span> <span data-ttu-id="39313-117">**레지스트리 이름**: 특정 레지스트리에 대한 전역적으로 고유한 최상위 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="39313-118">이 예제에서는 hello 레지스트리 이름이 *myAzureContainerRegistry1*, 되지만 대신 사용자 고유의의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="39313-119">hello 이름에는 문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39313-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="39313-120">b.</span><span class="sxs-lookup"><span data-stu-id="39313-120">b.</span></span> <span data-ttu-id="39313-121">**리소스 그룹**: 기존 선택 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="39313-122">c.</span><span class="sxs-lookup"><span data-stu-id="39313-122">c.</span></span> <span data-ttu-id="39313-123">**위치**: 여기서 hello 서비스는 Azure 데이터 센터 위치를 선택 [사용 가능한](https://azure.microsoft.com/regions/services/)와 같은 **미국 중남부**합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="39313-124">d.</span><span class="sxs-lookup"><span data-stu-id="39313-124">d.</span></span> <span data-ttu-id="39313-125">**관리: 사용자**:는 관리자 사용자 tooaccess hello 레지스트리를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="39313-126">Hello 레지스트리를 만든 후이 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39313-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="39313-127">e.</span><span class="sxs-lookup"><span data-stu-id="39313-127">e.</span></span> <span data-ttu-id="39313-128">**사용 하 여 관리 되는 레지스트리**: Select 예 toohave ACR 자동으로 hello 레지스트리 저장소 관리, webhook을 사용 하 고 AAD 인증을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="39313-129">f.</span><span class="sxs-lookup"><span data-stu-id="39313-129">f.</span></span> <span data-ttu-id="39313-130">**가격 책정 계층**: 가격 책정 계층을 선택합니다. 자세한 내용은 ACR 가격 책정을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39313-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="39313-131">TooACR 인스턴스 로그인</span><span class="sxs-lookup"><span data-stu-id="39313-131">Log in tooACR instance</span></span>

<span data-ttu-id="39313-132">밀어넣기 전에 컨테이너 이미지를 끌어오려면 toohello ACR 인스턴스 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="39313-133">따라서, toodo hello Azure CLI 2.0을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="39313-134">필요한 경우 hello를 사용 하 여 Azure에 로그인 하는 첫째, [az 로그인](/cli/azure/#login) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="39313-135">를 사용 하 여 hello [az acr 로그인](/cli/azure/acr#login) toohello Azure 컨테이너 레지스트리에서에서 toolog 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="39313-136">Azure Container Registry 사용</span><span class="sxs-lookup"><span data-stu-id="39313-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="39313-137">컨테이너 이미지 나열</span><span class="sxs-lookup"><span data-stu-id="39313-137">List container images</span></span>

<span data-ttu-id="39313-138">사용 하 여 hello `az acr` CLI 명령을 tooquery hello 이미지와 저장소의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="39313-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="39313-139">현재 컨테이너 레지스트리 hello 지원 하지 않는 `docker search` 이미지 및 태그에 대 한 명령 tooquery 합니다.</span><span class="sxs-lookup"><span data-stu-id="39313-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="39313-140">리포지토리 나열</span><span class="sxs-lookup"><span data-stu-id="39313-140">List repositories</span></span>

<span data-ttu-id="39313-141">hello 다음 예에서는 나열 JSON (JavaScript Object Notation) 형식의 레지스트리에 hello 저장소:</span><span class="sxs-lookup"><span data-stu-id="39313-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="39313-142">태그 나열</span><span class="sxs-lookup"><span data-stu-id="39313-142">List tags</span></span>

<span data-ttu-id="39313-143">hello 다음 예에서는 나열 hello hello 태그 **샘플/nginx** JSON 형식의 저장소:</span><span class="sxs-lookup"><span data-stu-id="39313-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="39313-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="39313-144">Next steps</span></span>

<span data-ttu-id="39313-145">이 빠른 시작 hello Azure 포털을 사용 하 여 관리 되는 Azure 컨테이너 레지스트리 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="39313-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39313-146">Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제</span><span class="sxs-lookup"><span data-stu-id="39313-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
