---
title: "Azure CDN 끝점 제거 | Microsoft Docs"
description: "Azure CDN 끝점에서 캐시된 콘텐츠를 모두 제거하는 방법을 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="823ba-103">Azure CDN 끝점 제거</span><span class="sxs-lookup"><span data-stu-id="823ba-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="823ba-104">개요</span><span class="sxs-lookup"><span data-stu-id="823ba-104">Overview</span></span>
<span data-ttu-id="823ba-105">Azure CDN 가장자리 노드는 자산의 TTL(Time-to-Live)이 만료될 때 자산을 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="823ba-106">자산의 TTL이 만료된 후에 클라이언트가 가장자리 노드에서 자산을 요청하는 경우 가장자리 노드는 새로 업데이트된 자산 사본을 검색하여 클라이언트 요청을 처리하고 저장소는 캐시를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="823ba-107">사용자가 항상 자산의 최신 복사본을 받도록 보장하는 가장 좋은 방법은 각 업데이트에 대해 자산 버전 관리를 수행하여 자산을 새 URL로 게시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="823ba-108">CDN은 다음 클라이언트 요청에 대한 새 자산을 즉시 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="823ba-109">경우에 따라 모든 가장자리 노드에서 캐시된 콘텐츠를 제거하고 이러한 콘텐츠가 모두 새로 업데이트된 자산을 검색하도록 강제하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="823ba-110">웹 응용 프로그램에 대한 업데이트 또는 잘못된 정보가 포함된 신속한 업데이트 자산 때문일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="823ba-111">제거는 CDN 에지 서버에 캐시된 콘텐츠만 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="823ba-112">프록시 서버와 로컬 브라우저 캐시 같은 다운스트림 캐시에는, 캐시된 파일 사본이 유지될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="823ba-113">파일의 TTL(Time-To-Live)을 설정할 때 이것을 기억하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="823ba-114">업데이트할 때마다 고유한 이름을 부여하거나 [쿼리 문자열 캐싱](cdn-query-string.md)의 이점을 활용하여, 다운스트림 클라이언트가 파일의 최신 버전을 요청하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="823ba-115">이 자습서는 끝점의 모든 가장자리 노드에서 자산을 제거하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="823ba-116">연습</span><span class="sxs-lookup"><span data-stu-id="823ba-116">Walkthrough</span></span>
1. <span data-ttu-id="823ba-117">[Azure 포털](https://portal.azure.com)에서 제거하려는 끝점을 포함하는 CDN 프로필로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="823ba-118">CDN 프로필 블레이드에서 제거 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="823ba-120">제거 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-120">The Purge blade opens.</span></span>
   
    ![CDN 제거 블레이드](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="823ba-122">제거 블레이드에서 URL 드롭다운 목록에서 제거하려는 서비스 주소를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![양식 제거](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="823ba-124">또한 CDN 끝점 블레이드에서 **제거** 단추를 클릭하여 제거 블레이드로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="823ba-125">이 경우에 **URL** 필드는 해당 특정 끝점의 서비스 주소로 미리 채워질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="823ba-126">가장자리 노드에서 제거하려는 자산을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="823ba-127">모든 자산을 지우려면 **모두 제거** 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="823ba-128">그렇지 않은 경우 제거하려는 각 자산의 경로를 **경로** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="823ba-129">경로에 지원되는 형식은 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="823ba-130">**단일 URL 제거**: 파일 확장명(예: `/pictures/strasbourg.png`; `/pictures/strasbourg`)이 포함된 또는 포함되지 않은 전체 URL을 지정하여 개별 자산을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="823ba-131">**와일드 카드 제거**: 별표(\*)를 와일드 카드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="823ba-132">경로에 `/*`가 포함된 끝점의 모든 폴더, 하위 폴더 및 파일을 제거하거나 폴더를 지정하고 맨 뒤에 `/*`를 붙여(예: `/pictures/*`) 특정 폴더의 모든 하위 폴더 및 파일을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="823ba-133">와일드 카드 제거는 현재 Akamai의 Azure CDN에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="823ba-134">**루트 도메인 제거**: 경로에 "/"가 포함된 끝점의 루트를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="823ba-135">제거할 경로를 지정해야 하며 경로는 다음 [정규식](https://msdn.microsoft.com/library/az24scfc.aspx)에 맞는 상대 URL이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="823ba-136">**모두 제거** 및 **와일드 카드 제거**는 현재 **Akamai의 Azure CDN**에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="823ba-137">단일 URL 제거 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="823ba-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="823ba-138">쿼리 문자열 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="823ba-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="823ba-139">와일드 카드 제거 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`</span><span class="sxs-lookup"><span data-stu-id="823ba-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="823ba-140">여러 자산 목록을 작성할 수 있도록 하는 텍스트를 입력한 후에 더 많은 **경로** 텍스트 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="823ba-141">목록에서 줄임표(...) 단추를 클릭하여 자산을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="823ba-142">**제거** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-142">Click the **Purge** button.</span></span>
   
    ![제거 단추](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="823ba-144">제거 요청은 **Verizon의 Azure CDN**(Standard 및 Premium)으로 처리하려면 약 2-3분, **Akamai의 Azure CDN**으로 처리하려면 약 7분이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="823ba-145">Azure CDN은 동시 제거 요청이 항상 50개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="823ba-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="823ba-146">참고 항목</span><span class="sxs-lookup"><span data-stu-id="823ba-146">See also</span></span>
* [<span data-ttu-id="823ba-147">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="823ba-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="823ba-148">Azure CDN REST API 참조 - 끝점 제거 또는 미리 로드</span><span class="sxs-lookup"><span data-stu-id="823ba-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

