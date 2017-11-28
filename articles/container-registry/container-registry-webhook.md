---
title: "컨테이너 레지스트리 webhook aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="31878-104">Azure Container Registry 웹후크 사용 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="31878-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="31878-105">Azure 컨테이너 레지스트리에 저장 및 전용 Docker 컨테이너 이미지를 Docker 허브 공용 Docker 이미지를 저장 하는 비슷한 toohello 방식으로 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="31878-106">레지스트리 리포지토리 중 하나에서 특정 작업이 수행 될 때 webhook tootrigger 이벤트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="31878-107">또한 Webhook tooevents hello 레지스트리 수준에서 응답할 수 또는 tooa 특정 저장소 태그 아래로 범위 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31878-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="31878-108">자세한 배경 및 개념에 대 한 참조 hello [개요](./container-registry-intro.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31878-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31878-109">Prerequisites</span></span> 

- <span data-ttu-id="31878-110">Azure 컨테이너 관리 레지스트리 - Azure 구독에서 관리되는 컨테이너 레지스트리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31878-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="31878-111">예를 들어 hello Azure 포털을 사용 하 여 또는 Azure CLI 2.0을 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="31878-112">Docker CLI-tooset는 Docker 호스트 및 액세스 hello Docker CLI 명령으로 로컬 컴퓨터를 Docker 엔진을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="31878-113">웹후크 Azure Portal 만들기</span><span class="sxs-lookup"><span data-stu-id="31878-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="31878-114">Azure 포털 toohello을 고 toocreate webhook 원하는 toohello 레지스트리를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="31878-115">Hello 컨테이너 블레이드 hello "Webhook" 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="31878-116">Hello webhook 블레이드 도구 모음에서 "추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="31878-117">전체 hello *Webhook 만들기* 양식에 다음 정보는 hello로:</span><span class="sxs-lookup"><span data-stu-id="31878-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="31878-118">값</span><span class="sxs-lookup"><span data-stu-id="31878-118">Value</span></span> | <span data-ttu-id="31878-119">설명</span><span class="sxs-lookup"><span data-stu-id="31878-119">Description</span></span> |
|---|---|
| <span data-ttu-id="31878-120">이름</span><span class="sxs-lookup"><span data-stu-id="31878-120">Name</span></span> | <span data-ttu-id="31878-121">hello 이름 toogive toohello webhook입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="31878-122">소문자와 숫자만 사용할 수 있으며 5-50자 사이입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="31878-123">서비스 URI</span><span class="sxs-lookup"><span data-stu-id="31878-123">Service URI</span></span> | <span data-ttu-id="31878-124">hello hello webhook POST 알림을 보내야 위치 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="31878-125">사용자 지정 헤더</span><span class="sxs-lookup"><span data-stu-id="31878-125">Custom headers</span></span> | <span data-ttu-id="31878-126">Hello POST 요청과 함께 toopass 원하는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="31878-127">"키: 값" 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="31878-128">트리거 동작</span><span class="sxs-lookup"><span data-stu-id="31878-128">Trigger actions</span></span> | <span data-ttu-id="31878-129">Hello webhook을 트리거하는 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="31878-130">현재 webhook 푸시에 의해 트리거될 수 및/또는 동작 tooan 이미지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="31878-131">가동 상태</span><span class="sxs-lookup"><span data-stu-id="31878-131">Status</span></span> | <span data-ttu-id="31878-132">hello webhook 만든 후에 대 한 hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="31878-133">기본적으로 사용하도록 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31878-133">It's enabled by default.</span></span> |
| <span data-ttu-id="31878-134">범위</span><span class="sxs-lookup"><span data-stu-id="31878-134">Scope</span></span> | <span data-ttu-id="31878-135">hello 범위는 hello webhook 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="31878-136">기본 hello 레지스트리의 모든 이벤트에 대 한 hello 범위가입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="31878-137">Hello 형식을 사용 하 여 저장소 또는 태그를 지정할 수 있습니다 "저장소: 태그"입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="31878-138">웹후크 양식 예제:</span><span class="sxs-lookup"><span data-stu-id="31878-138">Example webhook form:</span></span>

![DCOS UI](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="31878-140">웹후크 Azure CLI 만들기</span><span class="sxs-lookup"><span data-stu-id="31878-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="31878-141">사용 하 여 webhook toocreate hello Azure CLI를 사용 하 여 hello [az acr webhook 만들기](/cli/azure/acr/webhook#create) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="31878-142">웹후크 테스트</span><span class="sxs-lookup"><span data-stu-id="31878-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="31878-143">Azure portal</span><span class="sxs-lookup"><span data-stu-id="31878-143">Azure portal</span></span>

<span data-ttu-id="31878-144">Hello를 사용 하 여 테스트할 수 있습니다, 컨테이너에 이전 toousing hello webhook 밀어넣기 이미지 및 삭제 작업 **Ping** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="31878-145">을 사용 하는 제네릭 post 요청 toohello 지정한 끝점 및 로그 hello 응답 Ping hello가 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31878-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="31878-146">이 기능은 유용 webhook hello tooverify가 올바르게 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31878-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="31878-147">원하는 tootest hello webhook을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="31878-148">Hello 맨 위의 도구 모음에서 hello "Ping" 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="31878-149">Hello 요청 및 응답을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31878-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="31878-150">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31878-150">Azure CLI</span></span>

<span data-ttu-id="31878-151">tootest hello Azure CLI로 ACR webhook hello를 사용 하 여 [az acr webhook ping](/cli/azure/acr/webhook#ping) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="31878-152">toosee hello 결과 사용 하 여 hello [az acr webhook 목록 이벤트](/cli/azure/acr/webhook#list-events) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="31878-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="31878-153">웹후크 삭제</span><span class="sxs-lookup"><span data-stu-id="31878-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="31878-154">Azure portal</span><span class="sxs-lookup"><span data-stu-id="31878-154">Azure portal</span></span>

<span data-ttu-id="31878-155">Hello webhook 및 hello Azure 포털에서 hello 삭제 단추를 선택 하 여 각 webhook은 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31878-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="31878-156">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="31878-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```