---
title: "Azure Container Registry 웹후크 | Microsoft Docs"
description: "Azure Container Registry 웹후크"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: "Docker, 컨테이너, ACR"
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: d0190f5725671c320d92b897f0dcef7a526a86e3
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="4518f-104">Azure Container Registry 웹후크 사용 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4518f-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="4518f-105">Azure Container Registry는 Docker 허브에서 공개 Docker 이미지를 저장하는 것과 유사한 방식으로 개인 Docker 컨테이너 이미지를 저장하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-105">An Azure container registry stores and manages private Docker container images, similar to the way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="4518f-106">레지스트리 리포지토리 중 하나에서 특정 작업이 수행되는 경우 웹후크를 사용하여 이벤트를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-106">You use webhooks to trigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="4518f-107">웹후크는 레지스트리 수준에서 이벤트에 응답하거나 특정 리포지토리 태그로 범위를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-107">Webhooks can respond to events at the registry level or they can be scoped down to a specific repository tag.</span></span> 

<span data-ttu-id="4518f-108">자세한 배경 지식 및 개념은 [개요](./container-registry-intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4518f-108">For more background and concepts, see the [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4518f-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4518f-109">Prerequisites</span></span> 

- <span data-ttu-id="4518f-110">Azure 컨테이너 관리 레지스트리 - Azure 구독에서 관리되는 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="4518f-111">예를 들어 Azure Portal 또는 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-111">For example, use the Azure portal or the Azure CLI 2.0.</span></span> 
- <span data-ttu-id="4518f-112">Docker CLI - 로컬 컴퓨터를 Docker 호스트로 설정하고 Docker CLI 명령에 액세스하려면 Docker 엔진을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-112">Docker CLI - To set up your local computer as a Docker host and access the Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="4518f-113">웹후크 Azure Portal 만들기</span><span class="sxs-lookup"><span data-stu-id="4518f-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="4518f-114">Azure Portal에 로그인하여 웹후크를 만들려는 레지스트리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-114">Log in to the Azure portal and navigate to the registry in which you want to create webhooks.</span></span> 

2. <span data-ttu-id="4518f-115">컨테이너 블레이드에서 "웹후크" 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-115">In the container blade, select the "Webhooks" tab.</span></span> 

3. <span data-ttu-id="4518f-116">웹후크 블레이드 도구 모음에서 "추가"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-116">Select "Add" from the webhook blade toolbar.</span></span> 

4. <span data-ttu-id="4518f-117">*웹후크 만들기* 양식을 다음 정보로 완성합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-117">Complete the *Create Webhook* form with the following information:</span></span>

| <span data-ttu-id="4518f-118">값</span><span class="sxs-lookup"><span data-stu-id="4518f-118">Value</span></span> | <span data-ttu-id="4518f-119">설명</span><span class="sxs-lookup"><span data-stu-id="4518f-119">Description</span></span> |
|---|---|
| <span data-ttu-id="4518f-120">이름</span><span class="sxs-lookup"><span data-stu-id="4518f-120">Name</span></span> | <span data-ttu-id="4518f-121">웹후크에 지정하려는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-121">The name you want to give to the webhook.</span></span> <span data-ttu-id="4518f-122">소문자와 숫자만 사용할 수 있으며 5-50자 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="4518f-123">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="4518f-123">Service URI</span></span> | <span data-ttu-id="4518f-124">웹후크가 POST 알림을 보내야 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-124">The URI where the webhook should send POST notifications.</span></span> |
| <span data-ttu-id="4518f-125">사용자 지정 헤더</span><span class="sxs-lookup"><span data-stu-id="4518f-125">Custom headers</span></span> | <span data-ttu-id="4518f-126">POST 요청과 함께 전달하려는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-126">Headers you want to pass along with the POST request.</span></span> <span data-ttu-id="4518f-127">"키: 값" 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="4518f-128">트리거 동작</span><span class="sxs-lookup"><span data-stu-id="4518f-128">Trigger actions</span></span> | <span data-ttu-id="4518f-129">웹후크를 트리거하는 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-129">Actions that trigger the webhook.</span></span> <span data-ttu-id="4518f-130">현재 웹후크는 이미지에 대한 밀어넣기 및/또는 삭제 동작에 의해 트리거될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-130">Currently webhooks can be triggered by push and/or delete actions to an image.</span></span> |
| <span data-ttu-id="4518f-131">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4518f-131">Status</span></span> | <span data-ttu-id="4518f-132">웹후크가 만들어진 후의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-132">The status for the webhook after it's created.</span></span> <span data-ttu-id="4518f-133">기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-133">It's enabled by default.</span></span> |
| <span data-ttu-id="4518f-134">범위</span><span class="sxs-lookup"><span data-stu-id="4518f-134">Scope</span></span> | <span data-ttu-id="4518f-135">웹후크가 작동하는 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-135">The scope at which the webhook works.</span></span> <span data-ttu-id="4518f-136">기본적으로 이 범위는 레지스트리의 모든 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-136">By default the scope is for all events in the registry.</span></span> <span data-ttu-id="4518f-137">"리포지토리: 태그" 형식을 사용하여 리포지토리 또는 태그에 대해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-137">It can be specified for a repository or a tag by using the format "repository: tag".</span></span> |

<span data-ttu-id="4518f-138">웹후크 양식 예제:</span><span class="sxs-lookup"><span data-stu-id="4518f-138">Example webhook form:</span></span>

![DCOS UI](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="4518f-140">웹후크 Azure CLI 만들기</span><span class="sxs-lookup"><span data-stu-id="4518f-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="4518f-141">Azure CLI를 사용하여 웹후크를 만들려면 [az acr webhook create](/cli/azure/acr/webhook#create) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-141">To create a webhook using the Azure CLI, use the [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="4518f-142">웹후크 테스트</span><span class="sxs-lookup"><span data-stu-id="4518f-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4518f-143">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4518f-143">Azure portal</span></span>

<span data-ttu-id="4518f-144">컨테이너 이미지 밀어넣기 및 삭제 작업에서 웹후크를 사용하기 전에 **Ping** 단추를 사용하여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-144">Prior to using the webhook on container image push and delete actions, it can be tested using the **Ping** button.</span></span> <span data-ttu-id="4518f-145">Ping을 사용하는 경우 지정된 끝점에 일반 post 요청을 보내고 응답을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-145">When used, the Ping sends a generic post request to the specified endpoint and logs the response.</span></span> <span data-ttu-id="4518f-146">웹후크가 올바르게 설정되었는지 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-146">This is helpful to verify that the webhook has been set up correctly.</span></span>

1. <span data-ttu-id="4518f-147">테스트하려는 웹후크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-147">Select the webhook you want to test.</span></span> 
2. <span data-ttu-id="4518f-148">맨 위의 도구 모음에서 "Ping" 작업을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-148">In the top toolbar, select the "Ping" action.</span></span> 
3. <span data-ttu-id="4518f-149">요청 및 응답을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-149">Check the request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="4518f-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4518f-150">Azure CLI</span></span>

<span data-ttu-id="4518f-151">Azure CLI를 사용하여 ACR 웹후크를 테스트하려면 [az acr webhook ping](/cli/azure/acr/webhook#ping) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-151">To test an ACR webhook with the Azure CLI, use the [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="4518f-152">결과를 보려면 [az acr webhook list-events](/cli/azure/acr/webhook#list-events) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-152">To see the results, use the [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="4518f-153">웹후크 삭제</span><span class="sxs-lookup"><span data-stu-id="4518f-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="4518f-154">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4518f-154">Azure portal</span></span>

<span data-ttu-id="4518f-155">각 웹후크는 Azure Portal에서 웹후크를 선택하고 삭제 단추를 선택하여 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4518f-155">Each webhook can be deleted by selecting the webhook and then the delete button on the Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="4518f-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4518f-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```