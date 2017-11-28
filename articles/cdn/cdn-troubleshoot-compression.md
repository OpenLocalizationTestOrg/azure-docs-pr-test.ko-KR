---
title: "Azure CDN에서 파일 압축 aaaTroubleshooting | Microsoft Docs"
description: "Azure CDN 파일 압축과 관련된 문제를 해결합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="510e2-103">CDN 파일 압축 문제 해결</span><span class="sxs-lookup"><span data-stu-id="510e2-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="510e2-104">이 문서는 [CDN 파일 압축](cdn-improve-performance.md)관련 문제를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="510e2-105">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="510e2-106">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="510e2-107">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 클릭 **Get Support**합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="510e2-108">증상</span><span class="sxs-lookup"><span data-stu-id="510e2-108">Symptom</span></span>
<span data-ttu-id="510e2-109">끝점에 대한 압축이 활성화되어 있지만 파일이 압축되지 않은 상태로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="510e2-110">toocheck 파일 반환 되는 압축 된, toouse 도구와 같은 필요한 [Fiddler](http://www.telerik.com/fiddler) 또는 브라우저의 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="510e2-111">검사 hello HTTP 응답 헤더와 함께 반환 캐시 된 CDN 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="510e2-112">명명된 `Content-Encoding` 헤더에 **gzip**, **bzip2** 또는 **deflate** 값이 있는 경우 콘텐츠가 압축된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding 헤더](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="510e2-114">원인</span><span class="sxs-lookup"><span data-stu-id="510e2-114">Cause</span></span>
<span data-ttu-id="510e2-115">몇 가지 가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="510e2-116">hello 요청 콘텐츠는 압축에 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="510e2-117">압축 hello를 사용 하지 않는 요청 된 파일 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="510e2-118">hello HTTP 요청에 유효한 압축 유형 요청 헤더를 포함 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="510e2-119">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="510e2-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="510e2-120">새 끝점을 배포할 때와 CDN 구성 변경은 몇 시간 toopropagate hello 네트워크를 통해.</span><span class="sxs-lookup"><span data-stu-id="510e2-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="510e2-121">일반적으로 변경 내용은 90분 이내에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="510e2-122">인 경우 hello 처음으로 CDN 끝점에 대 한 압축을 설정 했으면 1 ~ 2 시간 toobe hello 압축 설정을 toohello Pop 전파 되었는지 대기 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="510e2-123">Hello 요청 확인</span><span class="sxs-lookup"><span data-stu-id="510e2-123">Verify hello request</span></span>
<span data-ttu-id="510e2-124">첫째, hello 요청에 대 한 빠른 온전성 검사를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="510e2-125">브라우저의을 사용할 수 있습니다 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello 전송 되는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="510e2-126">Hello 요청 tooyour 끝점 URL 보내는 확인 `<endpointname>.azureedge.net`, 및 원본 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="510e2-127">Hello 요청에 포함 되어 확인는 **Accept-encoding** 머리글과 hello 값에 해당 헤더에 포함 되어 **gzip**, **deflate**, 또는 **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="510e2-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="510e2-128">**Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN 요청 헤더](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="510e2-130">압축 설정 확인(Standard CDN 프로필)</span><span class="sxs-lookup"><span data-stu-id="510e2-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="510e2-131">이 단계는 CDN 프로필이 **Verizon의 Azure CDN Standard** 또는 **Akamai의 Azure CDN Standard** 프로필인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="510e2-132">Hello에 tooyour 끝점 이동 [Azure 포털](https://portal.azure.com) hello 클릭 **구성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="510e2-133">압축이 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="510e2-134">콘텐츠 압축 toobe 압축 된 형식의 hello 목록에 포함 되어 hello에 대 한 hello MIME 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="510e2-136">압축 설정 확인(Premium CDN 프로필)</span><span class="sxs-lookup"><span data-stu-id="510e2-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="510e2-137">이 단계는 CDN 프로필이 **Verizon의 Azure CDN Premium** 프로필인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="510e2-138">Hello에 tooyour 끝점 이동 [Azure 포털](https://portal.azure.com) hello 클릭 **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="510e2-139">hello 보조 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="510e2-140">마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="510e2-141">**압축**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-141">Click **Compression**.</span></span> 

* <span data-ttu-id="510e2-142">압축이 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="510e2-143">Hello 확인 **파일 형식을** 목록 MIME 형식 (공백 없이)는 쉼표로 구분 된 목록에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="510e2-144">콘텐츠 압축 toobe 압축 된 형식의 hello 목록에 포함 되어 hello에 대 한 hello MIME 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![CDN 프리미엄 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="510e2-146">Hello 콘텐츠가 캐시 되 고 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="510e2-147">이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="510e2-148">브라우저의 개발자 도구를 사용 하 여 hello 응답 헤더 tooensure hello 파일 요청 되는 hello 지역에 캐시 된 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="510e2-149">Hello 확인 **서버** 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="510e2-150">hello 헤더에는 hello 형식 있어야 **플랫폼 (POP/서버 ID)**hello 다음 예제와 같이, 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="510e2-151">Hello 확인 **X 캐시** 응답 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="510e2-152">hello 헤더를 읽어야 **적중**합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-152">hello header should read **HIT**.</span></span>  

![CDN 응답 헤더](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="510e2-154">Hello 파일 hello 크기 요구 사항을 충족 하는지 확인</span><span class="sxs-lookup"><span data-stu-id="510e2-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="510e2-155">이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="510e2-156">압축에 적합 toobe, 파일 크기 요구 사항을 준수 하는 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="510e2-157">128바이트 초과.</span><span class="sxs-lookup"><span data-stu-id="510e2-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="510e2-158">1MB 미만.</span><span class="sxs-lookup"><span data-stu-id="510e2-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="510e2-159">Hello 요청에 대 한 hello 원본 서버에서 확인 한 **통해** 헤더</span><span class="sxs-lookup"><span data-stu-id="510e2-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="510e2-160">hello **통해** HTTP 헤더는 프록시 서버에 의해 전달 되 고 요청 hello toohello 웹 서버를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="510e2-161">기본적으로 Microsoft IIS 웹 서버 hello 요청에 포함 되어 있으면 응답을 압축 하지 않습니다는 **통해** 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="510e2-162">toooverride이이 동작을 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="510e2-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="510e2-163">**IIS 6**: [설정 HcNoCompressionForProxies hello IIS 메타 베이스 속성에서 = "FALSE"](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="510e2-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="510e2-164">**IIS 7 이상**: [모두 설정 **noCompressionForHttp10** 및 **noCompressionForProxies** tooFalse hello 서버 구성](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="510e2-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

