---
title: "Azure CDN 끝점에 부하 aaaPre 자산 | Microsoft Docs"
description: "Toopre 부하 Azure CDN 끝점에서 콘텐츠를 캐시 하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a><span data-ttu-id="c90ab-103">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="c90ab-103">Pre-load assets on an Azure CDN endpoint</span></span>
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

<span data-ttu-id="c90ab-104">기본적으로 요청되었으므로 자산이 먼저 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-104">By default, assets are first cached as they are requested.</span></span> <span data-ttu-id="c90ab-105">즉, 각 지역에서 첫 번째 요청 hello 오래 걸릴 수 있습니다, hello에 지 서버 됩니다 하지 않았으므로 hello 캐시 된 콘텐츠와 tooforward hello 요청 toohello 원본 서버에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-105">This means that hello first request from each region may take longer, since hello edge servers will not have hello content cached and will need tooforward hello request toohello origin server.</span></span> <span data-ttu-id="c90ab-106">콘텐츠를 미리 로드하면 첫 번째 적중 대기 시간이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-106">Pre-loading content avoids this first hit latency.</span></span>

<span data-ttu-id="c90ab-107">또한 캐시 된 자산을 미리 로드 더 나은 고객 만족도 tooproviding hello 원본 서버에서 네트워크 트래픽을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-107">In addition tooproviding a better customer experience, pre-loading your cached assets can also reduce network traffic on hello origin server.</span></span>

> [!NOTE]
> <span data-ttu-id="c90ab-108">자산을 미리 로드 큰 이벤트에 대 한 유용한 되거나 동시에 사용할 수 있는 tooa 수가 많은 사용자가 새 동영상 릴리스 또는 소프트웨어 업데이트와 같은 됩니다 하는 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-108">Pre-loading assets is useful for  large events or content that becomes simultaneously available tooa large number of users, such as a new movie release or a software update.</span></span>
> 
> 

<span data-ttu-id="c90ab-109">이 자습서는 모든 Azure CDN 에지 노드에 캐시된 콘텐츠 미리 로드에 대해 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-109">This tutorial walks you through pre-loading cached content on all Azure CDN edge nodes.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="c90ab-110">연습</span><span class="sxs-lookup"><span data-stu-id="c90ab-110">Walkthrough</span></span>
1. <span data-ttu-id="c90ab-111">Hello에 [Azure 포털](https://portal.azure.com), toopre 부하를 원하는 hello 끝점을 포함 하는 toohello CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-111">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopre-load.</span></span>  <span data-ttu-id="c90ab-112">hello 프로필 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-112">hello profile blade opens.</span></span>
2. <span data-ttu-id="c90ab-113">Hello 목록의 hello 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-113">Click hello endpoint in hello list.</span></span>  <span data-ttu-id="c90ab-114">hello 끝점 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-114">hello endpoint blade opens.</span></span>
3. <span data-ttu-id="c90ab-115">Hello CDN 끝점 블레이드에서 hello 로드 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-115">From hello CDN endpoint blade, click hello load button.</span></span>
   
    ![CDN 끝점 블레이드](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    <span data-ttu-id="c90ab-117">hello 부하 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-117">hello Load blade opens.</span></span>
   
    ![CDN 로드 블레이드](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. <span data-ttu-id="c90ab-119">Hello 전체 경로 입력 합니다. 원하는 tooload 각 자산 (예: `/pictures/kitten.png`) hello에 **경로** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-119">Enter hello full path of each asset you wish tooload (e.g., `/pictures/kitten.png`) in hello **Path** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="c90ab-120">더 많은 **경로** tooallow 텍스트를 입력 한 후 입력란 나타납니다 toobuild 여러 자산 목록 중입니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-120">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="c90ab-121">Hello 줄임표 (...) 단추를 클릭 하 여 hello 목록에서 자산을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-121">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
   > <span data-ttu-id="c90ab-122">경로 hello 다음 적합 한 상대 URL 이어야 합니다. [정규식](https://msdn.microsoft.com/library/az24scfc.aspx):</span><span class="sxs-lookup"><span data-stu-id="c90ab-122">Paths must be a relative URL that fits hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx):</span></span>  
   > ><span data-ttu-id="c90ab-123">단일 파일 경로 `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-123">Load a single file path `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;</span></span>  
   > ><span data-ttu-id="c90ab-124">쿼리 문자열 `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`을 사용하여 단일 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-124">Load a single file with query string `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`</span></span>  
   > 
   > <span data-ttu-id="c90ab-125">각 자산에는 자체 경로가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-125">Each asset must have its own path.</span></span>  <span data-ttu-id="c90ab-126">미리 로드한 자산에 대한 와일드카드 기능은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-126">There is no wildcard functionality for pre-loading assets.</span></span>
   > 
   > 
   
    ![로드 단추](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. <span data-ttu-id="c90ab-128">Hello 클릭 **부하** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-128">Click hello **Load** button.</span></span>
   
    ![로드 단추](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> <span data-ttu-id="c90ab-130">로드 요청은 CDN 프로필별로 분당 10개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-130">There is a limitation of 10 load requests per minute per CDN profile.</span></span> <span data-ttu-id="c90ab-131">요청당 50개의 경로만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-131">50 paths are allowed per request.</span></span> <span data-ttu-id="c90ab-132">각 경로의 길이는 1024자로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="c90ab-132">Each path has a path-length limit of 1024 characters.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="c90ab-133">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c90ab-133">See also</span></span>
* [<span data-ttu-id="c90ab-134">Azure CDN 끝점 제거</span><span class="sxs-lookup"><span data-stu-id="c90ab-134">Purge an Azure CDN endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="c90ab-135">Azure CDN REST API 참조 - 끝점 제거 또는 미리 로드</span><span class="sxs-lookup"><span data-stu-id="c90ab-135">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

