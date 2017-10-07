---
title: "Eclipse 용 Azure 탐색기 hello aaaManaging Redis 캐시를 사용 하 여 | Microsoft Docs"
description: "Toomanage 프로그램 Azure redis 캐시 하는 방식을 Eclipse 용 Azure 탐색기 hello를 사용 하 여에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="7c294-103">Eclipse 용 Azure 탐색기 hello를 사용 하 여 Redis 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="7c294-103">Managing Redis Caches using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="7c294-104">hello hello Eclipse 용 Azure 도구 키트의 일부인 Java 개발자가 사용 하기 쉬운 솔루션 내에서 Azure 계정과에 캐시가 redis 관리에 대 한 hello Eclipse IDE를 제공 하는 Azure 탐색기.</span><span class="sxs-lookup"><span data-stu-id="7c294-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="7c294-105">Eclipse를 사용하여 Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="7c294-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="7c294-106">단계를 수행 하는 hello 과정을 단계별로 hello 단계 toocreate hello Azure 탐색기를 사용 하 여 redis 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="7c294-107">Tooyour hello hello 단계를 사용 하는 Azure 계정 로그인 [hello Eclipse 용 Azure 도구 키트에 대 한 로그인에 지침] 문서.</span><span class="sxs-lookup"><span data-stu-id="7c294-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="7c294-108">Hello에 **Azure 탐색기** 도구 창, hello 확장 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **Redis 캐시**, 클릭 하 고 **Create Redis Cache**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Redis Cache 만들기 메뉴][CR01]

1. <span data-ttu-id="7c294-110">Hello 때 **새 Redis 캐시** hello 다음 옵션을 지정 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![새 Redis Cache 만들기 대화 상자][CR02]

   <span data-ttu-id="7c294-112">a.</span><span class="sxs-lookup"><span data-stu-id="7c294-112">a.</span></span> <span data-ttu-id="7c294-113">**DNS 이름**: 너무 앞에 추가 hello 새 redis 캐시에 대 한 hello DNS 하위 도메인을 지정 ". redis.cache.windows.net"; 예: *wingtiptoys.redis.cache.windows.net*합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which is prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="7c294-114">b.</span><span class="sxs-lookup"><span data-stu-id="7c294-114">b.</span></span> <span data-ttu-id="7c294-115">**구독**: hello toouse hello 새 redis 캐시에 사용할 Azure 구독을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="7c294-116">c.</span><span class="sxs-lookup"><span data-stu-id="7c294-116">c.</span></span> <span data-ttu-id="7c294-117">**리소스 그룹**: redis 캐시에 대 한 hello 리소스 그룹을 지정 합니다. 즉 hello 다음 옵션 중 하나를 toochoose 필요:</span><span class="sxs-lookup"><span data-stu-id="7c294-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="7c294-118">**새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="7c294-119">**기존 그룹 사용**: Azure 계정과 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="7c294-120">d.</span><span class="sxs-lookup"><span data-stu-id="7c294-120">d.</span></span> <span data-ttu-id="7c294-121">**위치**: redis 캐시를 만들 위치; hello 위치를 지정 예를 들어 *West US*합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="7c294-122">e.</span><span class="sxs-lookup"><span data-stu-id="7c294-122">e.</span></span> <span data-ttu-id="7c294-123">**가격 책정 계층**: redis 캐시를 사용 하는 가격 책정 계층을 지정 5d;이 설정은 hello 클라이언트 연결 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="7c294-124">자세한 내용은 [Redis Cache 가격]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c294-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="7c294-125">f.</span><span class="sxs-lookup"><span data-stu-id="7c294-125">f.</span></span> <span data-ttu-id="7c294-126">**비SSL 포트**: Redis Cache에서 비SSL 연결을 허용하는지 여부를 지정합니다. 기본적으로 SSL 연결만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="7c294-127">모든 Redis Cache 설정을 지정한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="7c294-128">Redis 캐시를 만든 후 hello Azure 탐색기에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Azure 탐색기의 Redis Cache][CR03]

> [!NOTE]
>
> <span data-ttu-id="7c294-130">Redis cache 설정 Azure를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconfigure Azure Redis Cache]합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="7c294-131">Eclipse에서 Redis 캐시에 대 한 hello 속성을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-131">Display hello properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="7c294-132">에 Azure 탐색기 hello redis 캐시를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Redis 캐시에 대 한 azure 탐색기 상황에 맞는 메뉴 toodisplay 속성][SP01]

1. <span data-ttu-id="7c294-134">hello Azure 탐색기 redis 캐시에 대 한 hello 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Redis Cache 속성][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="7c294-136">Eclipse를 사용하여 Redis Cache 삭제</span><span class="sxs-lookup"><span data-stu-id="7c294-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="7c294-137">에 Azure 탐색기 hello redis 캐시를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure 탐색기 상황에 맞는 메뉴 toodelete redis 캐시][DE01]

1. <span data-ttu-id="7c294-139">클릭 **확인** 때 toodelete redis 캐시 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c294-139">Click **OK** when prompted toodelete your redis cache.</span></span>

   ![Redis Cache 삭제 프롬프트][DE02]

## <a name="next-steps"></a><span data-ttu-id="7c294-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c294-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="7c294-142">Azure redis 캐시, 구성 설정 및 가격에 대 한 자세한 내용은 hello 다음 링크 참조:</span><span class="sxs-lookup"><span data-stu-id="7c294-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="7c294-143">[Azure Redis 캐시(영문)]</span><span class="sxs-lookup"><span data-stu-id="7c294-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="7c294-144">[Redis Cache 설명서]</span><span class="sxs-lookup"><span data-stu-id="7c294-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="7c294-145">[Redis Cache 가격]</span><span class="sxs-lookup"><span data-stu-id="7c294-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="7c294-146">[어떻게 tooconfigure Azure Redis Cache]</span><span class="sxs-lookup"><span data-stu-id="7c294-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Redis Cache 가격]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis 캐시(영문)]: https://azure.microsoft.com/services/cache/
[Redis Cache 설명서]: ./redis-cache/index.md
[어떻게 tooconfigure Azure Redis Cache]: ./redis-cache/cache-configure.md
[hello Eclipse 용 Azure 도구 키트에 대 한 로그인에 지침]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
