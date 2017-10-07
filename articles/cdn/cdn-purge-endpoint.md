---
title: "Azure CDN 끝점 aaaPurge | Microsoft Docs"
description: "모든 toopurge 캐시 하는 방법을 알아보려면 Azure CDN 끝점에서 콘텐츠입니다."
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
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="df3ae-103">Azure CDN 끝점 제거</span><span class="sxs-lookup"><span data-stu-id="df3ae-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="df3ae-104">개요</span><span class="sxs-lookup"><span data-stu-id="df3ae-104">Overview</span></span>
<span data-ttu-id="df3ae-105">Azure CDN 지 노드에 hello 자산 활성 시간 (TTL) 만료 될 때까지 자산을 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="df3ae-106">Hello 자산 TTL이 만료 되 면 클라이언트가 hello 가장자리 노드에서 hello 자산을 요청 하면, hello 가장자리 노드 hello 자산 tooserve hello 클라이언트 요청의 새 업데이트 된 복사본을 검색 하 고 hello 캐시 새로 고침을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="df3ae-107">hello 모범 사례 toomake 사용자는 항상 hello 자산의 최신 복사본 가져오기 있는지는 tooversion 각각에 대해 자산 업데이트 및 새 Url로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="df3ae-108">CDN에서 즉시 hello hello 다음 클라이언트 요청에 대 한 새 자산을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="df3ae-109">경우에 따라 toopurge 모든 가장자리 노드의 콘텐츠를 캐시 하 고 새 업데이트 된 모든 자산 tooretrieve를 강제로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="df3ae-110">이 기한 tooupdates tooyour 웹 응용 프로그램 또는 잘못 된 정보가 포함 된 tooquickly 업데이트 자산 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="df3ae-111">hello 지웁니다만 제거 하는 참고 hello CDN에 지 서버에서 콘텐츠를 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="df3ae-112">프록시 서버와 로컬 브라우저 캐시와 같은 모든 다운스트림 캐시 hello 파일의 캐시 된 복사본을 보유할 여전히 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="df3ae-113">중요 한 tooremember는이 설정 하면 파일의 활성 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="df3ae-114">업데이트 될 때마다 고유한 이름을 지정 하 여 또는의 이용 하 여 파일의 다운스트림 클라이언트 toorequest hello 최신 버전을 강제로 실행할 수 있습니다 [쿼리 문자열 캐싱](cdn-query-string.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="df3ae-115">이 자습서는 끝점의 모든 가장자리 노드에서 자산을 제거하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="df3ae-116">연습</span><span class="sxs-lookup"><span data-stu-id="df3ae-116">Walkthrough</span></span>
1. <span data-ttu-id="df3ae-117">Hello에 [Azure 포털](https://portal.azure.com), toopurge 원하는 hello 끝점을 포함 하는 toohello CDN 프로필을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="df3ae-118">Hello CDN 프로필 블레이드에서 hello 제거 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![CDN 프로필 블레이드](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="df3ae-120">hello 지우기 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-120">hello Purge blade opens.</span></span>
   
    ![CDN 제거 블레이드](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="df3ae-122">Hello 블레이드를 제거 하 고 toopurge hello URL에 대 한 드롭다운에서 원하는 hello 서비스 주소를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![양식 제거](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="df3ae-124">Hello를 클릭 하 여 toohello 지우기 블레이드를 가져올 수도 있습니다 **제거** hello CDN 끝점 블레이드에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="df3ae-125">이 경우 hello **URL** 필드는 해당 특정 끝점의 hello 서비스 주소와 미리 채워진 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="df3ae-126">어떤 자산 원하는 hello에서 toopurge 가장자리 노드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="df3ae-127">Tooclear 모든 자산을 클릭 하 여 hello **모두** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="df3ae-128">그렇지 않은 경우 각 자산의 hello 경로 형식의 toopurge에에서 원하는 hello **경로** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="df3ae-129">형식 아래 hello 경로에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="df3ae-130">**단일 URL 지우기**: hello 파일 확장명, 예: 유무 hello 전체 URL을 지정 하 여 개별 자산 지우기`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="df3ae-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="df3ae-131">**와일드 카드 제거**: 별표(\*)를 와일드 카드로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="df3ae-132">모든 폴더, 하위 폴더 및 파일 끝점에서 제거 `/*` 경로 hello 또는 이어서 hello 폴더를 지정 하 여 모든 하위 폴더와 특정 폴더 아래에 있는 파일을 제거 `/*`, 예:`/pictures/*`합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="df3ae-133">와일드 카드 제거는 현재 Akamai의 Azure CDN에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="df3ae-134">**루트 도메인 제거**: hello 경로에 "/"와 hello 끝점의 hello 루트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="df3ae-135">경로 제거에 대 한 지정 해야 하며 hello 다음에 맞는 상대 URL 이어야 [정규식](https://msdn.microsoft.com/library/az24scfc.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="df3ae-136">**모두 제거** 및 **와일드 카드 제거**는 현재 **Akamai의 Azure CDN**에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="df3ae-137">단일 URL 제거 `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="df3ae-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="df3ae-138">쿼리 문자열 `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="df3ae-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="df3ae-139">와일드 카드 제거 `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`</span><span class="sxs-lookup"><span data-stu-id="df3ae-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="df3ae-140">더 많은 **경로** tooallow 텍스트를 입력 한 후 입력란 나타납니다 toobuild 여러 자산 목록 중입니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="df3ae-141">Hello 줄임표 (...) 단추를 클릭 하 여 hello 목록에서 자산을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="df3ae-142">Hello 클릭 **제거** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-142">Click hello **Purge** button.</span></span>
   
    ![제거 단추](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="df3ae-144">지우기 요청으로 약 2-3 분 tooprocess 걸릴 **Verizon에서 Azure CDN** (Standard 및 Premium) 및 사용 하는 약 7 분 **Akamai에서 Azure CDN**합니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="df3ae-145">Azure CDN은 동시 제거 요청이 항상 50개로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="df3ae-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="df3ae-146">참고 항목</span><span class="sxs-lookup"><span data-stu-id="df3ae-146">See also</span></span>
* [<span data-ttu-id="df3ae-147">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="df3ae-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="df3ae-148">Azure CDN REST API 참조 - 끝점 제거 또는 미리 로드</span><span class="sxs-lookup"><span data-stu-id="df3ae-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

