---
title: "Azure CDN에서 파일을 압축 하 여 aaaImprove 성능을 | Microsoft Docs"
description: "Tooimprove 파일 속도 증가 페이지 로드 성능 Azure CDN에서 파일을 압축 하 여 전송 하는 방법에 대해 알아봅니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="86958-103">Azure CDN에서 파일을 압축하여 성능 향상</span><span class="sxs-lookup"><span data-stu-id="86958-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="86958-104">압축은 단순 하 고 효과적인 방법 tooimprove 파일 전송 속도 및 하기 전에 파일 크기를 줄여 증가 페이지 로드 성능 hello 서버에서 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86958-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="86958-105">대역폭 비용을 절감하고 사용자에게 반응이 빠른 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="86958-106">두 가지가 tooenable 압축:</span><span class="sxs-lookup"><span data-stu-id="86958-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="86958-107">이 경우 hello CDN 통과 hello 압축 된 파일 및 배달 요청 하는 압축 된 파일 tooclients 원본 서버에서 압축을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="86958-108">압축 사례 hello CDN 압축 파일 hello 및 hello 원본 서버에 의해 압축 되지 않은 경우에 tooend 사용자 제공 CDN 지 서버에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86958-109">CDN 구성 변경 내용이 hello 네트워크를 통해 일부 시간 toopropagate 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="86958-110"><b>Akamai의 Azure CDN</b> 프로필의 경우, 일반적으로 1분 이내에 전파가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="86958-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="86958-111"><b>Verizon의 Azure CDN</b> 프로필의 경우, 변경 내용이 일반적으로 90분 내에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="86958-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="86958-112">대기 하는 1 ~ 2 시간 toobe hello 압축 설정 문제를 해결 하기 전에 toohello Pop 전파 있는지 고려해 야 인 경우 hello 처음으로 CDN 끝점에 대 한 압축을 설정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="86958-113">압축을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="86958-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="86958-114">hello Standard 및 Premium CDN 계층 제공 hello 같은 압축 기능을 하지만 hello 사용자 인터페이스 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="86958-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="86958-115">Standard 및 Premium CDN 계층 hello 차이점에 대 한 자세한 내용은 참조 [Azure CDN 개요](cdn-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="86958-116">표준 계층</span><span class="sxs-lookup"><span data-stu-id="86958-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="86958-117">이 섹션을 너무 적용**Verizon에서 Azure CDN 표준** 및 **Akamai에서 Azure CDN 표준** 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="86958-118">Hello CDN 프로필 페이지에서 원하는 toomanage hello CDN 끝점을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![CDN 프로필 페이지 끝점](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="86958-120">hello CDN 끝점 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86958-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="86958-121">Hello 클릭 **구성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-121">Click hello **Configure** button.</span></span>
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="86958-123">hello CDN 구성 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86958-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="86958-124">**압축**을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="86958-124">Turn on **Compression**.</span></span>
   
    ![CDN 압축 옵션](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="86958-126">Hello 기본 형식을 사용 하거나 제거 하거나 파일 형식을 추가 하 여 hello 목록을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="86958-127">While 가능한 ZIP, MP3, MP4, JPG 등 tooapply 압축 toocompressed 형식을 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="86958-128">Hello을 클릭 하 여 변경한 후 **저장** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="86958-129">프리미엄 계층</span><span class="sxs-lookup"><span data-stu-id="86958-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="86958-130">이 섹션을 너무 적용**Verizon에서 Azure CDN Premium** 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="86958-131">Hello CDN 프로필 페이지에서 클릭 hello **관리** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="86958-133">hello CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="86958-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="86958-134">마우스 포인터를 놓고 hello **HTTP 큰** 누른 마우스 포인터를 놓고 hello **캐시 설정** 플라이 아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="86958-135">**압축**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-135">Click on **Compression**.</span></span>

    ![파일 압축 선택](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="86958-137">압축 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="86958-137">Compression options are displayed.</span></span>
   
    ![파일 압축](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="86958-139">Hello를 클릭 하 여 압축을 사용 하도록 설정 **압축 사용** 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="86958-140">Hello MIME 형식을 입력 toocompress hello에 쉼표로 구분 된 목록 (공백 없이)으로 원하는 **파일 형식을** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="86958-141">While 가능한 ZIP, MP3, MP4, JPG 등 tooapply 압축 toocompressed 형식을 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="86958-142">Hello을 클릭 하 여 변경한 후 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="86958-143">압축 규칙</span><span class="sxs-lookup"><span data-stu-id="86958-143">Compression rules</span></span>
<span data-ttu-id="86958-144">이 테이블은 모든 시나리오에 적용되는 Azure CDN 압축 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86958-145">**Verizon의 Azure CDN** (Standard 및 Premium)의 경우, 적합한 파일만 압축될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="86958-146">압축에 적합 toobe, 파일을 수행 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="86958-147">128바이트 초과.</span><span class="sxs-lookup"><span data-stu-id="86958-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="86958-148">1MB 미만.</span><span class="sxs-lookup"><span data-stu-id="86958-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="86958-149">**Akamai의 Azure CDN**의 경우, 모든 파일이 압축에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="86958-150">모든 Azure CDN 제품의 경우, 파일은 [압축용으로 구성된](#enabling-compression)MIME 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="86958-151">**Verizon의 Azure CDN** 프로필(Standard 및 Premium)은 **gzip**(GNU zip), **deflate** 또는 **bzip2** 또는 **br**(Brotli) 인코딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="86958-152">Brotli 인코딩에 hello 압축 hello 가장자리에만 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="86958-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="86958-153">hello 클라이언트/브라우저가 Brotli 인코딩에 대 한 hello 요청을 전송 해야 하 고 hello 압축된 자산 해야 압축 된 hello 원본 쪽에서 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="86958-154">**Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="86958-155">**Akamai에서 azure CDN** 끝점 항상 요청 **gzip** 인코드된 hello 클라이언트 요청에 관계 없이 hello 원점에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="86958-156">압축이 비활성화되었거나 파일이 압축에 부적합</span><span class="sxs-lookup"><span data-stu-id="86958-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="86958-157">클라이언트 요청 형식(Accept-Encoding 헤더를 통한)</span><span class="sxs-lookup"><span data-stu-id="86958-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="86958-158">캐시된 파일 형식</span><span class="sxs-lookup"><span data-stu-id="86958-158">Cached file format</span></span> | <span data-ttu-id="86958-159">CDN 응답 toohello 클라이언트</span><span class="sxs-lookup"><span data-stu-id="86958-159">CDN response toohello client</span></span> | <span data-ttu-id="86958-160">참고 사항</span><span class="sxs-lookup"><span data-stu-id="86958-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="86958-161">압축</span><span class="sxs-lookup"><span data-stu-id="86958-161">Compressed</span></span> |<span data-ttu-id="86958-162">압축</span><span class="sxs-lookup"><span data-stu-id="86958-162">Compressed</span></span> |<span data-ttu-id="86958-163">압축</span><span class="sxs-lookup"><span data-stu-id="86958-163">Compressed</span></span> | |
| <span data-ttu-id="86958-164">압축</span><span class="sxs-lookup"><span data-stu-id="86958-164">Compressed</span></span> |<span data-ttu-id="86958-165">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-165">Uncompressed</span></span> |<span data-ttu-id="86958-166">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-166">Uncompressed</span></span> | |
| <span data-ttu-id="86958-167">압축</span><span class="sxs-lookup"><span data-stu-id="86958-167">Compressed</span></span> |<span data-ttu-id="86958-168">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="86958-168">Not cached</span></span> |<span data-ttu-id="86958-169">압축 또는 미압축</span><span class="sxs-lookup"><span data-stu-id="86958-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="86958-170">원본 응답에 따라 결정</span><span class="sxs-lookup"><span data-stu-id="86958-170">Depends on origin response</span></span> |
| <span data-ttu-id="86958-171">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-171">Uncompressed</span></span> |<span data-ttu-id="86958-172">압축</span><span class="sxs-lookup"><span data-stu-id="86958-172">Compressed</span></span> |<span data-ttu-id="86958-173">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-173">Uncompressed</span></span> | |
| <span data-ttu-id="86958-174">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-174">Uncompressed</span></span> |<span data-ttu-id="86958-175">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-175">Uncompressed</span></span> |<span data-ttu-id="86958-176">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-176">Uncompressed</span></span> | |
| <span data-ttu-id="86958-177">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-177">Uncompressed</span></span> |<span data-ttu-id="86958-178">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="86958-178">Not cached</span></span> |<span data-ttu-id="86958-179">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="86958-180">압축이 활성화되고 파일이 압축에 적합</span><span class="sxs-lookup"><span data-stu-id="86958-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="86958-181">클라이언트 요청 형식(Accept-Encoding 헤더를 통한)</span><span class="sxs-lookup"><span data-stu-id="86958-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="86958-182">캐시된 파일 형식</span><span class="sxs-lookup"><span data-stu-id="86958-182">Cached file format</span></span> | <span data-ttu-id="86958-183">CDN 응답 toohello 클라이언트</span><span class="sxs-lookup"><span data-stu-id="86958-183">CDN response toohello client</span></span> | <span data-ttu-id="86958-184">참고 사항</span><span class="sxs-lookup"><span data-stu-id="86958-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="86958-185">압축</span><span class="sxs-lookup"><span data-stu-id="86958-185">Compressed</span></span> |<span data-ttu-id="86958-186">압축</span><span class="sxs-lookup"><span data-stu-id="86958-186">Compressed</span></span> |<span data-ttu-id="86958-187">압축</span><span class="sxs-lookup"><span data-stu-id="86958-187">Compressed</span></span> |<span data-ttu-id="86958-188">지원되는 형식 간 CDN 코드 변환</span><span class="sxs-lookup"><span data-stu-id="86958-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="86958-189">압축</span><span class="sxs-lookup"><span data-stu-id="86958-189">Compressed</span></span> |<span data-ttu-id="86958-190">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-190">Uncompressed</span></span> |<span data-ttu-id="86958-191">압축</span><span class="sxs-lookup"><span data-stu-id="86958-191">Compressed</span></span> |<span data-ttu-id="86958-192">CDN이 압축 수행</span><span class="sxs-lookup"><span data-stu-id="86958-192">CDN performs compression</span></span> |
| <span data-ttu-id="86958-193">압축</span><span class="sxs-lookup"><span data-stu-id="86958-193">Compressed</span></span> |<span data-ttu-id="86958-194">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="86958-194">Not cached</span></span> |<span data-ttu-id="86958-195">압축</span><span class="sxs-lookup"><span data-stu-id="86958-195">Compressed</span></span> |<span data-ttu-id="86958-196">원본이 미압축 상태로 반환되면 CDN가 압축을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="86958-197">**Azure CDN에서 Verizon** 전달 hello hello 첫 번째 요청과 다음 압축에 대해 압축 되지 않은 파일 및 캐시 hello 후속 요청에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="86958-198">`Cache-Control: no-cache` 헤더를 포함한 파일을 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="86958-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="86958-199">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-199">Uncompressed</span></span> |<span data-ttu-id="86958-200">압축</span><span class="sxs-lookup"><span data-stu-id="86958-200">Compressed</span></span> |<span data-ttu-id="86958-201">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-201">Uncompressed</span></span> |<span data-ttu-id="86958-202">CDN이 압축 해제 수행</span><span class="sxs-lookup"><span data-stu-id="86958-202">CDN performs decompression</span></span> |
| <span data-ttu-id="86958-203">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-203">Uncompressed</span></span> |<span data-ttu-id="86958-204">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-204">Uncompressed</span></span> |<span data-ttu-id="86958-205">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-205">Uncompressed</span></span> | |
| <span data-ttu-id="86958-206">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-206">Uncompressed</span></span> |<span data-ttu-id="86958-207">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="86958-207">Not cached</span></span> |<span data-ttu-id="86958-208">미압축</span><span class="sxs-lookup"><span data-stu-id="86958-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="86958-209">미디어 서비스 CDN 압축</span><span class="sxs-lookup"><span data-stu-id="86958-209">Media Services CDN Compression</span></span>
<span data-ttu-id="86958-210">미디어 서비스 CDN 사용 스트리밍 끝점을 압축 콘텐츠 유형만 hello에 대 한 기본으로 설정 됩니다: 응용 프로그램/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, 응용 프로그램/f4m + xml입니다.</span><span class="sxs-lookup"><span data-stu-id="86958-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="86958-211">있습니다 수 없는 설정/해제 hello에 대 한 압축 hello Azure 포털을 사용 하 여 형식을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="86958-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="86958-212">참고 항목</span><span class="sxs-lookup"><span data-stu-id="86958-212">See also</span></span>
* [<span data-ttu-id="86958-213">CDN 파일 압축 문제 해결</span><span class="sxs-lookup"><span data-stu-id="86958-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

