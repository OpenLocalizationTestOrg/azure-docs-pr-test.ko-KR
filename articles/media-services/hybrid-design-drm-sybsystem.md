---
title: "Azure 미디어 서비스를 사용 하 여 DRM 하위 시스템의 aaaHybrid 디자인 | Microsoft Docs"
description: "이 항목에서는 Azure Media Services를 사용하는 DRM 하위 시스템의 하이브리드 디자인에 대해 설명합니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="4d219-103">DRM 하위 시스템의 하이브리드 디자인</span><span class="sxs-lookup"><span data-stu-id="4d219-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="4d219-104">이 항목에서는 Azure Media Services를 사용하는 DRM 하위 시스템의 하이브리드 디자인에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="4d219-105">개요</span><span class="sxs-lookup"><span data-stu-id="4d219-105">Overview</span></span>

<span data-ttu-id="4d219-106">Azure 미디어 서비스에는 다음 세 가지 DRM 시스템 hello에 대 한 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="4d219-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="4d219-107">PlayReady</span></span>
* <span data-ttu-id="4d219-108">Widevine(모듈)</span><span class="sxs-lookup"><span data-stu-id="4d219-108">Widevine (Modular)</span></span>
* <span data-ttu-id="4d219-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="4d219-109">FairPlay</span></span>

<span data-ttu-id="4d219-110">hello DRM 지원 브라우저 플레이어 SDK로 모든 3 DRMs를 지 원하는 Azure Media player DRM 암호화 (동적 암호화) 및 라이선스 배달에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="4d219-111">DRM/CENC 하위 시스템 디자인 및 구현 세부 처리로 라는 hello 문서를 참조 하십시오 [다중 DRM 및 액세스 제어 CENC](media-services-cenc-with-multidrm-access-control.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="4d219-112">하지만 세 가지 DRM 시스템에 대 한 전체 지원 제공, 경우에 따라 고객 할 필요는 toouse 자신의 인프라/하위 시스템에 추가 tooAzure 미디어 서비스 toobuild 하이브리드 DRM 하위 시스템의 다양 한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="4d219-113">고객이 묻는 몇 가지 일반적인 질문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="4d219-114">"나만의 DRM 라이선스 서버를 사용할 수 있습니까?"</span><span class="sxs-lookup"><span data-stu-id="4d219-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="4d219-115">(이 경우 고객은 비즈니스 논리가 포함된 DRM 라이선스 서버 팜에 투자했습니다.)</span><span class="sxs-lookup"><span data-stu-id="4d219-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="4d219-116">"AMS(Azure Media Services) 콘텐츠를 호스팅하지 않고 AMS에서 DRM 라이선스 배달만 사용할 수 있습니까?"</span><span class="sxs-lookup"><span data-stu-id="4d219-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="4d219-117">Hello AMS DRM 플랫폼의 모듈성</span><span class="sxs-lookup"><span data-stu-id="4d219-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="4d219-118">포괄적인 클라우드 비디오 플랫폼의 일부인 Azure Media Services DRM은 유연성과 모듈성을 고려하여 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="4d219-119">다음 (hello 테이블에 사용 되는 hello 표기법에 대 한 설명을 따릅니다) hello 테이블에 설명 된 다양 한 조합을 hello를 사용 하 여 Azure 미디어 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="4d219-120">**콘텐츠 호스팅 및 원본**</span><span class="sxs-lookup"><span data-stu-id="4d219-120">**Content hosting & origin**</span></span>|<span data-ttu-id="4d219-121">**콘텐츠 암호화**</span><span class="sxs-lookup"><span data-stu-id="4d219-121">**Content encryption**</span></span>|<span data-ttu-id="4d219-122">**DRM 라이선스 배달**</span><span class="sxs-lookup"><span data-stu-id="4d219-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="4d219-123">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-123">AMS</span></span>|<span data-ttu-id="4d219-124">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-124">AMS</span></span>|<span data-ttu-id="4d219-125">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-125">AMS</span></span>|
|<span data-ttu-id="4d219-126">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-126">AMS</span></span>|<span data-ttu-id="4d219-127">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-127">AMS</span></span>|<span data-ttu-id="4d219-128">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-128">Third-party</span></span>|
|<span data-ttu-id="4d219-129">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-129">AMS</span></span>|<span data-ttu-id="4d219-130">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-130">Third-party</span></span>|<span data-ttu-id="4d219-131">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-131">AMS</span></span>|
|<span data-ttu-id="4d219-132">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-132">AMS</span></span>|<span data-ttu-id="4d219-133">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-133">Third-party</span></span>|<span data-ttu-id="4d219-134">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-134">Third-party</span></span>|
|<span data-ttu-id="4d219-135">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-135">Third-party</span></span>|<span data-ttu-id="4d219-136">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-136">Third-party</span></span>|<span data-ttu-id="4d219-137">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="4d219-138">콘텐츠 호스팅 및 원본</span><span class="sxs-lookup"><span data-stu-id="4d219-138">Content hosting & origin</span></span>

* <span data-ttu-id="4d219-139">AMS: AMS에서 비디오 자산을 호스팅하고, AMS 스트리밍 끝점을 통해 스트리밍합니다(반드시 동적 패키징일 필요는 없음).</span><span class="sxs-lookup"><span data-stu-id="4d219-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="4d219-140">타사: AMS 외부의 타사 스트리밍 플랫폼에서 비디오를 호스팅하고 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="4d219-141">콘텐츠 암호화</span><span class="sxs-lookup"><span data-stu-id="4d219-141">Content encryption</span></span>

* <span data-ttu-id="4d219-142">AMS: AMS 동적 암호화를 통해 동적으로/요청 시 콘텐츠 암호화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="4d219-143">타사: AMS 외부에서 사전 처리 워크플로를 통해 콘텐츠 암호화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="4d219-144">DRM 라이선스 배달</span><span class="sxs-lookup"><span data-stu-id="4d219-144">DRM license delivery</span></span>

* <span data-ttu-id="4d219-145">AMS: AMS 라이선스 배달 서비스를 통해 DRM 라이선스를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="4d219-146">타사: AMS 외부의 타사 DRM 라이선스 서버에서 DRM 라이선스를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="4d219-147">하이브리드 시나리오에 따른 구성</span><span class="sxs-lookup"><span data-stu-id="4d219-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="4d219-148">콘텐츠 키</span><span class="sxs-lookup"><span data-stu-id="4d219-148">Content key</span></span>

<span data-ttu-id="4d219-149">콘텐츠 키의 구성을 통해 hello 다음 AMS 동적 암호화와 AMS 라이선스 배달 서비스의 특성을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="4d219-150">동적 DRM 암호화에 사용 되는 hello 콘텐츠 키입니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="4d219-151">DRM 라이선스 콘텐츠 toobe 라이선스 배달 서비스에서 전달한: 권한, 콘텐츠 키 및 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="4d219-152">**콘텐츠 키 인증 정책 제한** 유형: 공개, IP 또는 토큰 제한</span><span class="sxs-lookup"><span data-stu-id="4d219-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="4d219-153">경우 **토큰** 유형의 **콘텐츠 키 권한 부여 정책 제한은 사용**, hello **콘텐츠 키 권한 부여 정책 제한** 라이선스를 발급 하기 전에 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="4d219-154">자산 배달 정책</span><span class="sxs-lookup"><span data-stu-id="4d219-154">Asset delivery policy</span></span>

<span data-ttu-id="4d219-155">자산 배달 정책 구성을 통해 사용 되는 특성 AMS 동적 packager는 AMS 스트리밍 끝점의 동적 암호화를 수행 하는 hello를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="4d219-156">CENC(PlayReady 및 Widevine)에서 DASH, PlayReady에서 부드러운 스트리밍, Widevine 또는 PlayReady에서 HLS와 같은 스트리밍 프로토콜 및 DRM 암호화의 조합</span><span class="sxs-lookup"><span data-stu-id="4d219-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="4d219-157">각 hello에 대 한 라이선스 배달 Url 기본/포함 hello DRMs에 관련 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="4d219-158">DASH MPD 또는 HLS 재생 목록의 라이선스 획득 URL(LA_URL)에서 Widevine 및 FairPlay 각각에 대한 키 ID(KID) 쿼리 문자열을 포함하는지 여부</span><span class="sxs-lookup"><span data-stu-id="4d219-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="4d219-159">시나리오 및 샘플</span><span class="sxs-lookup"><span data-stu-id="4d219-159">Scenarios and samples</span></span>

<span data-ttu-id="4d219-160">Hello 이전 단원의 hello 설명에 따라, hello 다음 5 개의 하이브리드 시나리오 사용 하 여 해당 **콘텐츠 키**-**자산 배달 정책** 구성 조합은 (hello hello 마지막 열에 언급 된 샘플 다음과 hello 테이블).</span><span class="sxs-lookup"><span data-stu-id="4d219-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="4d219-161">**콘텐츠 호스팅 및 원본**</span><span class="sxs-lookup"><span data-stu-id="4d219-161">**Content hosting & origin**</span></span>|<span data-ttu-id="4d219-162">**DRM 암호화**</span><span class="sxs-lookup"><span data-stu-id="4d219-162">**DRM encryption**</span></span>|<span data-ttu-id="4d219-163">**DRM 라이선스 배달**</span><span class="sxs-lookup"><span data-stu-id="4d219-163">**DRM license delivery**</span></span>|<span data-ttu-id="4d219-164">**콘텐츠 키 구성**</span><span class="sxs-lookup"><span data-stu-id="4d219-164">**Configure content key**</span></span>|<span data-ttu-id="4d219-165">**자산 배달 정책 구성**</span><span class="sxs-lookup"><span data-stu-id="4d219-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="4d219-166">**샘플**</span><span class="sxs-lookup"><span data-stu-id="4d219-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="4d219-167">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-167">AMS</span></span>|<span data-ttu-id="4d219-168">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-168">AMS</span></span>|<span data-ttu-id="4d219-169">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-169">AMS</span></span>|<span data-ttu-id="4d219-170">예</span><span class="sxs-lookup"><span data-stu-id="4d219-170">Yes</span></span>|<span data-ttu-id="4d219-171">예</span><span class="sxs-lookup"><span data-stu-id="4d219-171">Yes</span></span>|<span data-ttu-id="4d219-172">샘플 1</span><span class="sxs-lookup"><span data-stu-id="4d219-172">Sample 1</span></span>|
|<span data-ttu-id="4d219-173">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-173">AMS</span></span>|<span data-ttu-id="4d219-174">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-174">AMS</span></span>|<span data-ttu-id="4d219-175">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-175">Third-party</span></span>|<span data-ttu-id="4d219-176">예</span><span class="sxs-lookup"><span data-stu-id="4d219-176">Yes</span></span>|<span data-ttu-id="4d219-177">예</span><span class="sxs-lookup"><span data-stu-id="4d219-177">Yes</span></span>|<span data-ttu-id="4d219-178">샘플 2</span><span class="sxs-lookup"><span data-stu-id="4d219-178">Sample 2</span></span>|
|<span data-ttu-id="4d219-179">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-179">AMS</span></span>|<span data-ttu-id="4d219-180">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-180">Third-party</span></span>|<span data-ttu-id="4d219-181">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-181">AMS</span></span>|<span data-ttu-id="4d219-182">예</span><span class="sxs-lookup"><span data-stu-id="4d219-182">Yes</span></span>|<span data-ttu-id="4d219-183">아니요</span><span class="sxs-lookup"><span data-stu-id="4d219-183">No</span></span>|<span data-ttu-id="4d219-184">샘플 3</span><span class="sxs-lookup"><span data-stu-id="4d219-184">Sample 3</span></span>|
|<span data-ttu-id="4d219-185">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-185">AMS</span></span>|<span data-ttu-id="4d219-186">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-186">Third-party</span></span>|<span data-ttu-id="4d219-187">외부</span><span class="sxs-lookup"><span data-stu-id="4d219-187">Outside</span></span>|<span data-ttu-id="4d219-188">아니요</span><span class="sxs-lookup"><span data-stu-id="4d219-188">No</span></span>|<span data-ttu-id="4d219-189">아니요</span><span class="sxs-lookup"><span data-stu-id="4d219-189">No</span></span>|<span data-ttu-id="4d219-190">샘플 4</span><span class="sxs-lookup"><span data-stu-id="4d219-190">Sample 4</span></span>|
|<span data-ttu-id="4d219-191">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-191">Third-party</span></span>|<span data-ttu-id="4d219-192">타사</span><span class="sxs-lookup"><span data-stu-id="4d219-192">Third-party</span></span>|<span data-ttu-id="4d219-193">AMS</span><span class="sxs-lookup"><span data-stu-id="4d219-193">AMS</span></span>|<span data-ttu-id="4d219-194">예</span><span class="sxs-lookup"><span data-stu-id="4d219-194">Yes</span></span>|<span data-ttu-id="4d219-195">아니요</span><span class="sxs-lookup"><span data-stu-id="4d219-195">No</span></span>|    

<span data-ttu-id="4d219-196">Hello 샘플에서 PlayReady 보호 대시 및 부드러운 스트리밍에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="4d219-197">아래 hello 비디오 Url은 부드러운 스트리밍 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="4d219-198">tooget hello 해당 DASH Url, 추가 "(형식 = mpd-시간-csf)"입니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="4d219-199">Hello를 사용할 수 있습니다 [azure 미디어 플레이어 테스트](http://aka.ms/amtest) 브라우저에서 tootest 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="4d219-200">Tooconfigure 수 있는 기술에서 프로토콜 toouse 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="4d219-201">Windows 10의 IE11 및 MS Edge는 EME를 통해 PlayReady를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="4d219-202">자세한 내용은 참조 [hello에 대 한 세부 정보 도구를 테스트할](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="4d219-203">샘플 1</span><span class="sxs-lookup"><span data-stu-id="4d219-203">Sample 1</span></span>

* <span data-ttu-id="4d219-204">원본(기본) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="4d219-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="4d219-205">PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="4d219-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="4d219-206">Widevine LA_URL(DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="4d219-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="4d219-207">FairPlay LA_URL(HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="4d219-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="4d219-208">샘플 2</span><span class="sxs-lookup"><span data-stu-id="4d219-208">Sample 2</span></span>

* <span data-ttu-id="4d219-209">원본(기본) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="4d219-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="4d219-210">PlayReady LA_URL(DASH 및 부드러운 스트리밍): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="4d219-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="4d219-211">샘플 3</span><span class="sxs-lookup"><span data-stu-id="4d219-211">Sample 3</span></span>

* <span data-ttu-id="4d219-212">원본 URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="4d219-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="4d219-213">PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="4d219-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="4d219-214">샘플 4</span><span class="sxs-lookup"><span data-stu-id="4d219-214">Sample 4</span></span>

* <span data-ttu-id="4d219-215">원본 URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="4d219-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="4d219-216">PlayReady LA_URL(DASH 및 부드러운 스트리밍): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="4d219-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="4d219-217">요약</span><span class="sxs-lookup"><span data-stu-id="4d219-217">Summary</span></span>

<span data-ttu-id="4d219-218">요약하면 Azure Media Services DRM 구성 요소는 유연합니다. 이 항목에서 설명한 대로 콘텐츠 키와 자산 배달 정책을 올바르게 구성하여 하이브리드 시나리오에서 이러한 구성 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d219-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d219-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4d219-219">Next steps</span></span>
<span data-ttu-id="4d219-220">Media Services 학습 경로 보기.</span><span class="sxs-lookup"><span data-stu-id="4d219-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4d219-221">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="4d219-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

