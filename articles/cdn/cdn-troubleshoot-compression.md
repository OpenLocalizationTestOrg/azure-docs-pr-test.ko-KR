---
title: "Azure CDN의 파일 압축 문제 해결 | Microsoft Docs"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="58608-103">CDN 파일 압축 문제 해결</span><span class="sxs-lookup"><span data-stu-id="58608-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="58608-104">이 문서는 [CDN 파일 압축](cdn-improve-performance.md)관련 문제를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="58608-105">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="58608-106">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="58608-107">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 이동하여 **지원 받기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="58608-108">증상</span><span class="sxs-lookup"><span data-stu-id="58608-108">Symptom</span></span>
<span data-ttu-id="58608-109">끝점에 대한 압축이 활성화되어 있지만 파일이 압축되지 않은 상태로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="58608-110">반환된 파일이 압축되었는지 확인하려면 [Fiddler](http://www.telerik.com/fiddler) 또는 브라우저의 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/)와 같은 도구를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="58608-111">캐시된 CDN 콘텐츠와 함께 반환된 HTTP 응답 헤더를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="58608-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="58608-112">명명된 `Content-Encoding` 헤더에 **gzip**, **bzip2** 또는 **deflate** 값이 있는 경우 콘텐츠가 압축된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58608-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Content-Encoding 헤더](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="58608-114">원인</span><span class="sxs-lookup"><span data-stu-id="58608-114">Cause</span></span>
<span data-ttu-id="58608-115">몇 가지 가능한 원인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="58608-116">요청된 콘텐츠에 압축을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="58608-117">압축은 요청된 파일 형식에 대해 활성화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="58608-118">HTTP 요청에 유효한 압축 형식을 요청하는 헤더가 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="58608-119">문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="58608-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="58608-120">새 끝점 배포와 마찬가지로, CDN 구성 변경이 네트워크 전체에 전파되려면 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="58608-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="58608-121">일반적으로 변경 내용은 90분 이내에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="58608-122">CDN 끝점에 압축을 처음으로 설정한 경우 압축 설정이 POP까지 전파되도록 1~2시간 기다리는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="58608-123">요청 확인</span><span class="sxs-lookup"><span data-stu-id="58608-123">Verify the request</span></span>
<span data-ttu-id="58608-124">우선, 요청에 대해 빠른 온전성 검사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="58608-125">브라우저의 [개발자 도구](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) 를 사용하여 생성되는 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="58608-126">요청이 원본이 아닌 끝점 URL, `<endpointname>.azureedge.net`에 전송되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="58608-127">요청에 **Accept-Encoding** 헤더가 포함되는지, 헤더 값에 **gzip**, **deflate** 또는 **bzip2**가 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="58608-128">**Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![CDN 요청 헤더](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="58608-130">압축 설정 확인(Standard CDN 프로필)</span><span class="sxs-lookup"><span data-stu-id="58608-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="58608-131">이 단계는 CDN 프로필이 **Verizon의 Azure CDN Standard** 또는 **Akamai의 Azure CDN Standard** 프로필인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="58608-132">[Azure 포털](https://portal.azure.com) 에서 끝점으로 이동하여 **구성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="58608-133">압축이 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="58608-134">압축될 콘텐츠에 대한 MIME 형식이 압축된 형식의 목록에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="58608-136">압축 설정 확인(Premium CDN 프로필)</span><span class="sxs-lookup"><span data-stu-id="58608-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="58608-137">이 단계는 CDN 프로필이 **Verizon의 Azure CDN Premium** 프로필인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="58608-138">[Azure 포털](https://portal.azure.com) 에서 끝점으로 이동하여 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="58608-139">보조 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58608-139">The supplemental portal will open.</span></span>  <span data-ttu-id="58608-140">**HTTP Large** 탭을 가리킨 다음 **캐시 설정** 플라이아웃을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="58608-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="58608-141">**압축**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-141">Click **Compression**.</span></span> 

* <span data-ttu-id="58608-142">압축이 활성화되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="58608-143">**파일 형식** 목록에 쉼표로 구분된(공백 없음) MIME 형식 목록이 포함되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="58608-144">압축될 콘텐츠에 대한 MIME 형식이 압축된 형식의 목록에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![CDN 프리미엄 압축 설정](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="58608-146">콘텐츠 캐시 여부 확인</span><span class="sxs-lookup"><span data-stu-id="58608-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="58608-147">이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="58608-148">브라우저의 개발자 도구를 사용하여, 요청되는 지역에서 파일이 캐시되는지 응답 헤더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="58608-149">**Server** 응답 헤더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-149">Check the **Server** response header.</span></span>  <span data-ttu-id="58608-150">헤더에는 **Platform(POP/Server ID)**형식이 포함되어야 합니다(다음 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="58608-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="58608-151">**X-Cache** 응답 헤더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="58608-152">헤더는 **HIT**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-152">The header should read **HIT**.</span></span>  

![CDN 응답 헤더](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="58608-154">파일의 크기 요건 충족 여부 확인</span><span class="sxs-lookup"><span data-stu-id="58608-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="58608-155">이 단계는 CDN 프로필이 **Verizon의 Azure CDN** 프로필(Standard 또는 Premium)인 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="58608-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="58608-156">압축을 적용할 수 있으려면, 파일은 다음과 같은 크기 요건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="58608-157">128바이트 초과.</span><span class="sxs-lookup"><span data-stu-id="58608-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="58608-158">1MB 미만.</span><span class="sxs-lookup"><span data-stu-id="58608-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="58608-159">원본 서버의 요청에서 **Via** 헤더 확인</span><span class="sxs-lookup"><span data-stu-id="58608-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="58608-160">**Via** HTTP 헤더는 요청이 프록시 서버에 의해 전달되고 있음을 웹 서버에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="58608-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="58608-161">기본적으로 Microsoft IIS 웹 서버는 요청에 **Via** 헤더가 들어 있으면 응답을 압축하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58608-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="58608-162">이 동작을 재정의하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58608-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="58608-163">**IIS 6**: [IIS 메타베이스 속성에서 HcNoCompressionForProxies="FALSE" 설정](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="58608-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="58608-164">**IIS 7 이상**: [서버 구성에서 **noCompressionForHttp10** 및 **noCompressionForProxies**를 둘 다 False로 설정](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="58608-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

