---
title: "쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어 | Microsoft Docs"
description: "Azure CDN 쿼리 문자열 캐싱은 파일에 쿼리 문자열이 포함된 경우 파일이 캐시되는 방법을 제어합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 8d79626fa8516f226a82d3dac693c2033904c91d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a><span data-ttu-id="e3333-103">쿼리 문자열을 사용하여 Azure CDN 캐싱 동작 제어</span><span class="sxs-lookup"><span data-stu-id="e3333-103">Control Azure CDN caching behavior with query strings</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3333-104">Standard</span><span class="sxs-lookup"><span data-stu-id="e3333-104">Standard</span></span>](cdn-query-string.md)
> * [<span data-ttu-id="e3333-105">Verizon의 Azure CDN Premium</span><span class="sxs-lookup"><span data-stu-id="e3333-105">Azure CDN Premium from Verizon</span></span>](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e3333-106">개요</span><span class="sxs-lookup"><span data-stu-id="e3333-106">Overview</span></span>
<span data-ttu-id="e3333-107">쿼리 문자열 캐싱은 파일에 쿼리 문자열이 들어 있을 때 파일이 캐시되는 방법을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-107">Query string caching controls how files are to be cached when they contain query strings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3333-108">표준 및 프리미엄 CDN 제품은 동일한 쿼리 문자열 캐싱 기능을 제공하지만 사용자 인터페이스는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-108">The Standard and Premium CDN products provide the same query string caching functionality, but the user interface differs.</span></span>  <span data-ttu-id="e3333-109">이 문서는 **Akamai의 Azure CDN Standard** 및 **Verizon의 Azure CDN Standard**에 대한 인터페이스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-109">This document describes the interface for **Azure CDN Standard from Akamai** and **Azure CDN Standard from Verizon**.</span></span>  <span data-ttu-id="e3333-110">**Verizon의 Azure CDN Premium**을 사용한 쿼리 문자열 캐싱은 [쿼리 문자열이 포함된 CDN 요청의 캐싱 동작 제어 - 프리미엄](cdn-query-string-premium.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3333-110">For query string caching with **Azure CDN Premium from Verizon**, see [Controlling caching behavior of CDN requests with query strings - Premium](cdn-query-string-premium.md).</span></span>
> 
> 

<span data-ttu-id="e3333-111">다음 세 가지 모드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-111">Three modes are available:</span></span>

* <span data-ttu-id="e3333-112">**쿼리 문자열 무시**: 기본 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-112">**Ignore query strings**:  This is the default mode.</span></span>  <span data-ttu-id="e3333-113">CDN 에지 노드가 첫 번째 요청에서 요청자의 쿼리 문자열을 원본으로 전달하고 자산을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-113">The CDN edge node will pass the query string from the requestor to the origin on the first request and cache the asset.</span></span>  <span data-ttu-id="e3333-114">캐시된 자산이 만료될 때까지 에지 노드에서 제공되는 해당 자산의 모든 후속 요청은 쿼리 문자열을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-114">All subsequent requests for that asset that are served from the edge node will ignore the query string until the cached asset expires.</span></span>
* <span data-ttu-id="e3333-115">**쿼리 문자열이 포함된 URL에 대한 캐싱 바이패스**:이 모드에서 쿼리 문자열이 포함된 요청은 CDN 에지 노드에서 캐시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-115">**Bypass caching for URL with query strings**:  In this mode, requests with query strings are not cached at the CDN edge node.</span></span>  <span data-ttu-id="e3333-116">에지 노드가 원본에서 직접 자산을 검색하고 각 요청과 함께 요청자에게 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-116">The edge node retrieves the asset directly from the origin and passes it to the requestor with each request.</span></span>
* <span data-ttu-id="e3333-117">**모든 고유한 URL 캐시**: 이 모드는 쿼리 문자열이 포함된 각 요청을 자체 캐시를 가진 고유한 자산으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-117">**Cache every unique URL**:  This mode treats each request with a query string as a unique asset with its own cache.</span></span>  <span data-ttu-id="e3333-118">예를 들어 *foo.ashx?q=bar* 에 대한 요청의 경우 원본에서의 응답이 에지 노드에서 캐시되고 그와 동일한 쿼리 문자열을 가진 후속 캐시에 대해 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-118">For example, the response from the origin for a request for *foo.ashx?q=bar* would be cached at the edge node and returned for subsequent caches with that same query string.</span></span>  <span data-ttu-id="e3333-119">*foo.ashx?q=somethingelse* 에 대한 요청은 자체 TTL(Time To Live)과 함께 별도의 자산으로 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-119">A request for *foo.ashx?q=somethingelse* would be cached as a separate asset with its own time to live.</span></span>

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a><span data-ttu-id="e3333-120">Standard CDN 프로필에 대한 쿼리 문자열 캐싱 설정 변경</span><span class="sxs-lookup"><span data-stu-id="e3333-120">Changing query string caching settings for standard CDN profiles</span></span>
1. <span data-ttu-id="e3333-121">CDN 프로필 블레이드에서 관리하려는 CDN 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-121">From the CDN profile blade, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN 프로필 블레이드 끝점](./media/cdn-query-string/cdn-endpoints.png)
   
    <span data-ttu-id="e3333-123">CDN 끝점 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-123">The CDN endpoint blade opens.</span></span>
2. <span data-ttu-id="e3333-124">**구성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-124">Click the **Configure** button.</span></span>
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-query-string/cdn-config-btn.png)
   
    <span data-ttu-id="e3333-126">CDN 구성 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-126">The CDN Configuration blade opens.</span></span>
3. <span data-ttu-id="e3333-127">**쿼리 문자열 캐싱 동작** 드롭다운에서 설정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-127">Select a setting from the **Query string caching behavior** dropdown.</span></span>
   
    ![CDN 쿼리 문자열 캐싱 옵션](./media/cdn-query-string/cdn-query-string.png)
4. <span data-ttu-id="e3333-129">선택한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-129">After making your selection, click the **Save** button.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3333-130">등록이 CDN 전체에 전파되기까지 시간이 걸리기 때문에, 설정 변경은 즉시 보이지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-130">The settings changes may not be immediately visible, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="e3333-131"><b>Akamai의 Azure CDN</b> 프로필의 경우 일반적으로 1분 이내에 전파가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-131">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="e3333-132"><b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3333-132">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
> 
> 

