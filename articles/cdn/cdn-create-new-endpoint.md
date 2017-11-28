---
title: "Azure CDN 시작 aaaGetting | Microsoft Docs"
description: "이 항목에서는 tooenable Azure 콘텐츠 배달 네트워크 (CDN) hello 하는 방법을 보여 줍니다. hello 자습서 hello 새 CDN 프로필 및 끝점 만들기를 안내합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="8749d-104">Azure CDN 시작</span><span class="sxs-lookup"><span data-stu-id="8749d-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="8749d-105">이 항목에서는 새로운 CDN 프로필 및 끝점을 만들어서 Azure CDN을 활성화하는 단계를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8749d-106">소개 toohow CDN 작동으로 기능 목록은 참조 hello [CDN 개요](cdn-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="8749d-107">새 CDN 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="8749d-107">Create a new CDN profile</span></span>
<span data-ttu-id="8749d-108">CDN 프로필은 CDN 끝점의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="8749d-109">각 프로필에는 CDN 끝점이 하나 이상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="8749d-110">여러 프로필 tooorganize toouse를 지정할 수 있습니다 인터넷 도메인, 웹 응용 프로그램 또는 기타 일부 조건에 의해 CDN 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="8749d-111">기본적으로 단일 Azure 구독은 제한 tooeight CDN 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="8749d-112">CDN 프로필 각는 제한 된 tooten CDN 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="8749d-113">CDN 가격 hello CDN 프로필 수준에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="8749d-114">원할 경우 toouse Azure CDN을 혼합 하 여 가격 책정 계층이 여러 CDN 프로필을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="8749d-115">새 CDN 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="8749d-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="8749d-116">**새 CDN 끝점 toocreate**</span><span class="sxs-lookup"><span data-stu-id="8749d-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="8749d-117">Hello에 [Azure 포털](https://portal.azure.com), tooyour CDN 프로필을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="8749d-118">수 있는 고정 toohello 대시보드 hello 이전 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="8749d-119">경우 not, 있습니다 찾을 수 있습니다 것을 클릭 하 여 **찾아보기**, 다음 **CDN 프로필**, 인증서 및 hello 프로필 클릭 하면 tooadd를 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="8749d-120">CDN 프로필 블레이드 hello 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-120">hello CDN profile blade appears.</span></span>
   
    ![CDN 프로필][cdn-profile-settings]
2. <span data-ttu-id="8749d-122">Hello 클릭 **끝점 추가** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-122">Click hello **Add Endpoint** button.</span></span>
   
    ![끝점 추가 단추][cdn-new-endpoint-button]
   
    <span data-ttu-id="8749d-124">hello **끝점 추가** 블레이드 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![끝점 추가 블레이드][cdn-add-endpoint]
3. <span data-ttu-id="8749d-126">이 CDN 끝점에 대한 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="8749d-127">이 이름은 hello 도메인에서 캐시 된 리소스 사용된 tooaccess 됩니다 `<endpointname>.azureedge.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="8749d-128">Hello에 **원본 형식을** 드롭다운에서 원본 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="8749d-129">Azure Storage 계정에 대해 **저장소**, Azure 클라우드 서비스에 대해 **클라우드 서비스**, Azure 웹앱에 대해 **웹앱**을 선택하고 기타 공개적으로 액세스할 수 있는 웹 서버 원본(Azure 또는 다른 곳에서 호스팅)에 대해 **사용자 지정 원본**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![CDN 원본 형식](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="8749d-131">Hello에 **원본 호스트 이름을** 드롭다운을 선택 하거나 원본 도메인을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="8749d-132">hello 드롭다운 4 단계에서 지정한 hello 형식의 모든 사용할 수 있는 원본을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="8749d-133">선택한 경우 *사용자 지정 원본* 으로 프로그램 **원본 형식을**, 사용자 지정 원본의 hello 도메인에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="8749d-134">Hello에 **원래 경로** 텍스트 상자에 원하는 toocache, 또는 leave 빈 tooallow 캐시 5 단계에서 지정한 hello 도메인에서 리소스 hello 경로 toohello 리소스를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="8749d-135">Hello에 **원본 호스트 헤더**각 요청과 함께 CDN toosend hello 원하는 hello 호스트 헤더를 입력 하거나 hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="8749d-136">원본 Azure 저장소 및 웹 응용 프로그램 같은 일부 유형의 hello 원본 hello 호스트 헤더 toomatch hello 도메인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="8749d-137">해당 도메인에서 다른 호스트 헤더를 요구 하는 원본이 없는 경우 hello 기본값을 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="8749d-138">에 대 한 **프로토콜** 및 **원본 포트**hello 프로토콜을 지정 하 고 hello 원점에 리소스 사용 되는 tooaccess 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="8749d-139">프로토콜을 적어도 하나는(HTTP 또는 HTTPS) 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8749d-140">hello **원본 포트** hello 원점에서 tooretrieve 정보를 사용 하는 어떤 포트 hello 끝점에만 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="8749d-141">hello 자체 끝점에만 됩니다 hello 기본 HTTP 및 HTTPS 포트 (80 및 443) hello에 관계 없이 사용할 수 있는 tooend 클라이언트 **원본 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="8749d-142">**Akamai에서 azure CDN** 끝점 출처에 대 한 hello 전체 TCP 포트 범위를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="8749d-143">허용되지 않는 원본 포트 목록을 보려면 [Akamai 허용된 원본 포트의 Azure CDN](https://msdn.microsoft.com/library/mt757337.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8749d-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="8749d-144">CDN에 액세스할 HTTPS를 사용 하 여 콘텐츠 hello 제약 조건 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="8749d-145">Hello CDN에서 제공 하는 hello SSL 인증서를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="8749d-146">타사 인증서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="8749d-147">Hello CDN에서 제공한 도메인을 사용 해야 합니다 (`<endpointname>.azureedge.net`) tooaccess HTTPS 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="8749d-148">HTTPS 지원을 사용할 수 없는 경우 사용자 지정 도메인 이름 (Cname)에 대 한 hello CDN이 이번에 사용자 지정 인증서를 지원 하지 않으므로</span><span class="sxs-lookup"><span data-stu-id="8749d-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="8749d-149">Hello 클릭 **추가** 단추 toocreate hello 새 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="8749d-150">Hello 끝점을 만들 되 면 hello 프로필에 대 한 끝점의 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="8749d-151">hello 목록 보기 hello URL toouse tooaccess 캐시 hello 원본 도메인 뿐만 아니라 콘텐츠를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![CDN 끝점][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="8749d-153">hello 끝점 즉시 됩니다 사용 하기 위해 사용할 수 있는 대로 hello CDN 통해 hello 등록 toopropagate 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="8749d-154"><b>Akamai의 Azure CDN</b> 프로필의 경우 일반적으로 1분 이내에 전파가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="8749d-155"><b>Verizon의 Azure CDN</b> 프로필의 경우 일반적으로 90분 이내에 전파가 완료되지만 더 오래 소요될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="8749d-156">사용자가 hello 끝점 구성을 toohello Pop 전파 전에 toouse hello CDN 도메인 이름을 시도 HTTP 404 응답 코드를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8749d-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="8749d-157">끝점을 만든 후 몇 시간 후에도 404 응답이 수신되는 경우 [404 상태를 반환하는 CDN 끝점 문제 해결](cdn-troubleshoot-endpoint.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8749d-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="8749d-158">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8749d-158">See Also</span></span>
* [<span data-ttu-id="8749d-159">쿼리 문자열이 포함된 요청의 캐싱 동작 제어</span><span class="sxs-lookup"><span data-stu-id="8749d-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="8749d-160">어떻게 tooMap CDN 콘텐츠 tooa 사용자 지정 도메인</span><span class="sxs-lookup"><span data-stu-id="8749d-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="8749d-161">Azure CDN 끝점에 자산 미리 로드</span><span class="sxs-lookup"><span data-stu-id="8749d-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="8749d-162">Azure CDN 끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="8749d-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="8749d-163">404 상태를 반환하는 CDN 끝점 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8749d-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
