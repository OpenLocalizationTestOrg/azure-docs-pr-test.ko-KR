---
title: "Azure CDN에서 파일을 압축하여 성능 향상 | Microsoft Docs"
description: "Azure CDN에서 파일을 압축하여 파일 전송 속도를 개선하고 페이지 로드 성능을 향상시키는 방법을 알아봅니다."
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="b7c49-103">Azure CDN에서 파일을 압축하여 성능 향상</span><span class="sxs-lookup"><span data-stu-id="b7c49-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="b7c49-104">압축은 파일이 서버에서 전송되기 전에 파일 크기를 줄여서 파일 전송 속도를 개선하고 페이지 로드 성능을 높이는 간단하고 효과적인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="b7c49-105">대역폭 비용을 절감하고 사용자에게 반응이 빠른 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="b7c49-106">압축을 사용하도록 설정하는 방법은 두 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="b7c49-107">원본 서버에서 압축을 사용하도록 설정할 수 있으며, 이런 경우 CDN은 압축된 파일을 거쳐서 압축된 파일을 요청한 클라이언트에 압축된 파일을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="b7c49-108">CDN 에지 서버에서 직접 압축을 사용하도록 설정할 수 있으며, 이런 경우 CDN이 파일을 압축하여(원본 서버에 의해 압축되지 않더라도) 최종 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7c49-109">CDN 구성 변경이 네트워크 전체에 전파되려면 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="b7c49-110"><b>Akamai의 Azure CDN</b> 프로필의 경우, 일반적으로 1분 이내에 전파가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="b7c49-111"><b>Verizon의 Azure CDN</b> 프로필의 경우, 변경 내용이 일반적으로 90분 내에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="b7c49-112">CDN 끝점에 압축을 처음으로 설정한 경우 압축 설정이 POP까지 전파되도록 1~2시간 기다렸다가 문제 해결을 시도하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="b7c49-113">압축을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b7c49-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="b7c49-114">표준 및 프리미엄 CDN 계층은 동일한 압축 기능을 제공하지만 사용자 인터페이스는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="b7c49-115">표준과 프리미엄 CDN 계층 간의 차이점에 대한 자세한 내용은 [Azure CDN 개요](cdn-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7c49-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="b7c49-116">표준 계층</span><span class="sxs-lookup"><span data-stu-id="b7c49-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="b7c49-117">이 섹션은 **Verizon의 Azure CDN Standard** 및 **Akamai의 Azure CDN Standard** 프로필에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="b7c49-118">CDN 페이지에서 관리하려는 CDN 끝점을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![CDN 프로필 페이지 끝점](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="b7c49-120">CDN 끝점 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="b7c49-121">**구성** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-121">Click the **Configure** button.</span></span>
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="b7c49-123">CDN 구성 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="b7c49-124">**압축**을 켭니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-124">Turn on **Compression**.</span></span>
   
    ![CDN 압축 옵션](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="b7c49-126">기본 형식을 사용하거나 파일 형식을 추가 또는 제거하여 목록을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b7c49-127">가능하기는 하지만 ZIP, MP3, MP4, JPG, 등 압축된 형식에 압축을 적용하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="b7c49-128">변경한 후 **저장** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="b7c49-129">프리미엄 계층</span><span class="sxs-lookup"><span data-stu-id="b7c49-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="b7c49-130">이 섹션은 **Verizon의 Azure CDN Premium** 프로필에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="b7c49-131">CDN 프로필 페이지에서 **관리** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![CDN 프로필 페이지 관리 단추](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="b7c49-133">CDN 관리 포털이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="b7c49-134">**HTTP Large** 탭을 가리킨 다음 **캐시 설정** 플라이아웃을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="b7c49-135">**압축**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-135">Click on **Compression**.</span></span>

    ![파일 압축 선택](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="b7c49-137">압축 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-137">Compression options are displayed.</span></span>
   
    ![파일 압축](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="b7c49-139">**압축 사용** 라디오 단추를 클릭하여 압축을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="b7c49-140">쉼표로 구분된 목록(공백 없음)으로 압축하려는 MIME 유형을 **파일 유형** 텍스트 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="b7c49-141">가능하기는 하지만 ZIP, MP3, MP4, JPG, 등 압축된 형식에 압축을 적용하는 것은 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="b7c49-142">변경한 후 **업데이트** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="b7c49-143">압축 규칙</span><span class="sxs-lookup"><span data-stu-id="b7c49-143">Compression rules</span></span>
<span data-ttu-id="b7c49-144">이 테이블은 모든 시나리오에 적용되는 Azure CDN 압축 동작을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7c49-145">**Verizon의 Azure CDN** (Standard 및 Premium)의 경우, 적합한 파일만 압축될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="b7c49-146">압축이 가능하려면 파일이 다음 조건을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="b7c49-147">128바이트 초과.</span><span class="sxs-lookup"><span data-stu-id="b7c49-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="b7c49-148">1MB 미만.</span><span class="sxs-lookup"><span data-stu-id="b7c49-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="b7c49-149">**Akamai의 Azure CDN**의 경우, 모든 파일이 압축에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="b7c49-150">모든 Azure CDN 제품의 경우, 파일은 [압축용으로 구성된](#enabling-compression)MIME 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="b7c49-151">**Verizon의 Azure CDN** 프로필(Standard 및 Premium)은 **gzip**(GNU zip), **deflate** 또는 **bzip2** 또는 **br**(Brotli) 인코딩을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="b7c49-152">Brotli 인코딩의 경우 에지에서만 압축이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="b7c49-153">클라이언트/브라우저는 Brotli 인코딩에 대한 요청을 전송해야 하고 압축된 자산은 처음에 원본 쪽에서 먼저 압축되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="b7c49-154">**Akamai의 Azure CDN** 프로필은 **gzip** 인코딩만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="b7c49-155">**Akamai의 Azure CDN** 끝점은 클라이언트 요청에 상관없이, 원본으로부터 항상 **gzip** 인코딩 파일을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="b7c49-156">압축이 비활성화되었거나 파일이 압축에 부적합</span><span class="sxs-lookup"><span data-stu-id="b7c49-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="b7c49-157">클라이언트 요청 형식(Accept-Encoding 헤더를 통한)</span><span class="sxs-lookup"><span data-stu-id="b7c49-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="b7c49-158">캐시된 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b7c49-158">Cached file format</span></span> | <span data-ttu-id="b7c49-159">클라이언트에 대한 CDN 응답</span><span class="sxs-lookup"><span data-stu-id="b7c49-159">CDN response to the client</span></span> | <span data-ttu-id="b7c49-160">참고</span><span class="sxs-lookup"><span data-stu-id="b7c49-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b7c49-161">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-161">Compressed</span></span> |<span data-ttu-id="b7c49-162">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-162">Compressed</span></span> |<span data-ttu-id="b7c49-163">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-163">Compressed</span></span> | |
| <span data-ttu-id="b7c49-164">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-164">Compressed</span></span> |<span data-ttu-id="b7c49-165">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-165">Uncompressed</span></span> |<span data-ttu-id="b7c49-166">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-166">Uncompressed</span></span> | |
| <span data-ttu-id="b7c49-167">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-167">Compressed</span></span> |<span data-ttu-id="b7c49-168">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="b7c49-168">Not cached</span></span> |<span data-ttu-id="b7c49-169">압축 또는 미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="b7c49-170">원본 응답에 따라 결정</span><span class="sxs-lookup"><span data-stu-id="b7c49-170">Depends on origin response</span></span> |
| <span data-ttu-id="b7c49-171">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-171">Uncompressed</span></span> |<span data-ttu-id="b7c49-172">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-172">Compressed</span></span> |<span data-ttu-id="b7c49-173">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-173">Uncompressed</span></span> | |
| <span data-ttu-id="b7c49-174">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-174">Uncompressed</span></span> |<span data-ttu-id="b7c49-175">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-175">Uncompressed</span></span> |<span data-ttu-id="b7c49-176">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-176">Uncompressed</span></span> | |
| <span data-ttu-id="b7c49-177">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-177">Uncompressed</span></span> |<span data-ttu-id="b7c49-178">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="b7c49-178">Not cached</span></span> |<span data-ttu-id="b7c49-179">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="b7c49-180">압축이 활성화되고 파일이 압축에 적합</span><span class="sxs-lookup"><span data-stu-id="b7c49-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="b7c49-181">클라이언트 요청 형식(Accept-Encoding 헤더를 통한)</span><span class="sxs-lookup"><span data-stu-id="b7c49-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="b7c49-182">캐시된 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b7c49-182">Cached file format</span></span> | <span data-ttu-id="b7c49-183">클라이언트에 대한 CDN 응답</span><span class="sxs-lookup"><span data-stu-id="b7c49-183">CDN response to the client</span></span> | <span data-ttu-id="b7c49-184">참고</span><span class="sxs-lookup"><span data-stu-id="b7c49-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b7c49-185">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-185">Compressed</span></span> |<span data-ttu-id="b7c49-186">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-186">Compressed</span></span> |<span data-ttu-id="b7c49-187">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-187">Compressed</span></span> |<span data-ttu-id="b7c49-188">지원되는 형식 간 CDN 코드 변환</span><span class="sxs-lookup"><span data-stu-id="b7c49-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="b7c49-189">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-189">Compressed</span></span> |<span data-ttu-id="b7c49-190">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-190">Uncompressed</span></span> |<span data-ttu-id="b7c49-191">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-191">Compressed</span></span> |<span data-ttu-id="b7c49-192">CDN이 압축 수행</span><span class="sxs-lookup"><span data-stu-id="b7c49-192">CDN performs compression</span></span> |
| <span data-ttu-id="b7c49-193">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-193">Compressed</span></span> |<span data-ttu-id="b7c49-194">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="b7c49-194">Not cached</span></span> |<span data-ttu-id="b7c49-195">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-195">Compressed</span></span> |<span data-ttu-id="b7c49-196">원본이 미압축 상태로 반환되면 CDN가 압축을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="b7c49-197">**Verizon에서 Azure CDN** 은 첫 번째 요청에 압축되지 않은 파일을 전달한 다음 후속 요청에 대한 파일을 압축하고 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="b7c49-198">`Cache-Control: no-cache` 헤더를 포함한 파일을 압축되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="b7c49-199">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-199">Uncompressed</span></span> |<span data-ttu-id="b7c49-200">압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-200">Compressed</span></span> |<span data-ttu-id="b7c49-201">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-201">Uncompressed</span></span> |<span data-ttu-id="b7c49-202">CDN이 압축 해제 수행</span><span class="sxs-lookup"><span data-stu-id="b7c49-202">CDN performs decompression</span></span> |
| <span data-ttu-id="b7c49-203">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-203">Uncompressed</span></span> |<span data-ttu-id="b7c49-204">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-204">Uncompressed</span></span> |<span data-ttu-id="b7c49-205">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-205">Uncompressed</span></span> | |
| <span data-ttu-id="b7c49-206">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-206">Uncompressed</span></span> |<span data-ttu-id="b7c49-207">캐시되지 않음</span><span class="sxs-lookup"><span data-stu-id="b7c49-207">Not cached</span></span> |<span data-ttu-id="b7c49-208">미압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="b7c49-209">미디어 서비스 CDN 압축</span><span class="sxs-lookup"><span data-stu-id="b7c49-209">Media Services CDN Compression</span></span>
<span data-ttu-id="b7c49-210">미디어 서비스 CDN 사용 스트리밍 끝점의 경우 다음 콘텐츠 형식에 대해 기본적으로 압축이 사용됩니다. application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="b7c49-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="b7c49-211">Azure 포털에서 언급된 형식에 대해 압축을 사용하거나 사용하지 않도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b7c49-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="b7c49-212">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b7c49-212">See also</span></span>
* [<span data-ttu-id="b7c49-213">CDN 파일 압축 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b7c49-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

