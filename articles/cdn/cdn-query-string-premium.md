---
title: "쿼리 문자열-프리미엄을 사용한 Azure CDN 캐싱 동작 aaaControl | Microsoft Docs"
description: "Azure CDN 쿼리 문자열 캐싱 방법을 파일은 쿼리 문자열을 포함 하는 경우 캐시 toobe 컨트롤입니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a><span data-ttu-id="ff454-103">쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어 - Premium</span><span class="sxs-lookup"><span data-stu-id="ff454-103">Control Azure CDN caching behavior with query strings - Premium</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff454-104">Standard</span><span class="sxs-lookup"><span data-stu-id="ff454-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="ff454-105">Verizon의 Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="ff454-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ff454-106">개요</span><span class="sxs-lookup"><span data-stu-id="ff454-106">Overview</span></span>
<span data-ttu-id="ff454-107">쿼리 문자열 캐싱 방법을 파일은 쿼리 문자열을 포함 하는 경우 캐시 toobe 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-107">Query string caching controls how files are toobe cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff454-108">hello Standard 및 Premium CDN 제품은 hello 같은 쿼리 문자열 캐싱 기능 하지만 hello 사용자 인터페이스 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-108">hello Standard and Premium CDN products provide hello same query string caching functionality, but hello user interface differs.</span></span>  <span data-ttu-id="ff454-109">이 문서에는 hello 인터페이스에 설명 **Verizon에서 Azure CDN Premium**합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-109">This document describes hello interface for **Azure CDN Premium from Verizon**.</span></span>  <span data-ttu-id="ff454-110">**Akamai의 Azure CDN Standard** 및 **Verizon의 Azure CDN Standard**를 사용한 쿼리 문자열 캐싱에 대해서는 [쿼리 문자열이 포함된 CDN 요청의 캐싱 동작 제어](cdn-query-string.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff454-110">For query string caching with **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**, see [Controlling caching behavior of CDN requests with query strings](cdn-query-string.md).</span></span>
> 
> 

<span data-ttu-id="ff454-111">다음 세 가지 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-111">Three modes are available:</span></span>

* <span data-ttu-id="ff454-112">**표준 캐시**: hello 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-112">**standard-cache**:  This is hello default mode.</span></span>  <span data-ttu-id="ff454-113">hello CDN 가장자리 노드 hello 첫 번째 요청 및 캐시 hello 자산에 hello 요청자 toohello 원점에서 hello 쿼리 문자열을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-113">hello CDN edge node will pass hello query string from hello requestor toohello origin on hello first request and cache hello asset.</span></span>  <span data-ttu-id="ff454-114">Hello 가장자리 노드에서 처리 되는 해당 자산에 대 한 모든 후속 요청은 캐시 된 자산 hello 만료 될 때까지 hello 쿼리 문자열을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-114">All subsequent requests for that asset that are served from hello edge node will ignore hello query string until hello cached asset expires.</span></span>
* <span data-ttu-id="ff454-115">**no 캐시**:이 모드에서는 쿼리 문자열을 사용 하 여 요청에 hello CDN 가장자리 노드에서 캐시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-115">**no-cache**:  In this mode, requests with query strings are not cached at hello CDN edge node.</span></span>  <span data-ttu-id="ff454-116">hello 가장자리 노드 hello 원본에서 직접 hello 자산을 검색 하 고 각 요청과 함께 toohello 요청자에 게 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-116">hello edge node retrieves hello asset directly from hello origin and passes it toohello requestor with each request.</span></span>
* <span data-ttu-id="ff454-117">**unique-cache**: 이 모드는 쿼리 문자열이 포함된 각 요청을 자체 캐시를 가진 고유한 자산으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-117">**unique-cache**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="ff454-118">예를 들어 hello 출처에 대 한 요청에 대 한 응답을 hello *foo.ashx?q=bar* hello 가장자리 노드에 캐시 되 고 후속 캐시의 해당 동일한 쿼리 문자열로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-118">For example, hello response from hello origin for a request for *foo.ashx?q=bar* would be cached at hello edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="ff454-119">에 대 한 요청 *foo.ashx?q=somethingelse* toolive 자체 시간과 함께 별도 자산으로 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time toolive.</span></span>

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a><span data-ttu-id="ff454-120">Premium CDN 프로필에 대한 쿼리 문자열 캐싱 설정 변경</span><span class="sxs-lookup"><span data-stu-id="ff454-120">Changing query string caching settings for premium CDN profiles</span></span>
1. <span data-ttu-id="ff454-121">Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-121">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    <span data-ttu-id="ff454-123">hello CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-123">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="ff454-124">마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-124">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="ff454-125">**Query-String Caching**(쿼리 문자열 캐싱)을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-125">Click on **Query-String Caching**.</span></span>
   
    <span data-ttu-id="ff454-126">쿼리 문자열 캐싱 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-126">Query string caching options are displayed.</span></span>
   
    ![CDN 쿼리 문자열 캐싱 옵션](./media/cdn-query-string-premium/cdn-query-string.png)
3. <span data-ttu-id="ff454-128">선택한 후 클릭 hello **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-128">After making your selection, click hello **Update** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff454-129">hello CDN 통해 hello 등록 toopropagate 시간이 걸립니다 대로 hello 설정 변경 수 즉시 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-129">hello settings changes may not be immediately visible, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="ff454-130"><b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff454-130">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

