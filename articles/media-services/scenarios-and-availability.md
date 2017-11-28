---
title: "Azure 미디어 서비스 aaaMicrosoft 시나리오 및 사용 가능한 데이터 센터 간에 기능 | Microsoft Docs"
description: "이 항목은 Microsoft Azure Media Services 시나리오 및 데이터 센터에서 기능 및 서비스의 사용 가용성 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 3dbab6998ed5da738baf8f1e2fb096dfba336e19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="30d1c-103">시나리오 및 데이터 센터에서 Media Services 기능의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="30d1c-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="30d1c-104">Microsoft Azure 미디어 서비스 AMS ()를 사용 하면 toosecurely 업로드, 저장, 인코딩 및 주문형 및 라이브 스트리밍 배달 toovarious 클라이언트 모두 (예를 들어, TV, PC 및 모바일 장치)에 대 한 비디오 또는 오디오 콘텐츠를 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-104">Microsoft Azure Media Services (AMS) enables you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="30d1c-105">AMS는 hello 전 세계 여러 데이터 센터에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-105">AMS operates in multiple data centers around hello world.</span></span> <span data-ttu-id="30d1c-106">이러한 데이터 센터 위치 선택에 유연성을 제공, toogeographic 영역에 그룹화 되어 toobuild 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-106">These data centers are grouped in toogeographic regions, giving you flexibility in choosing where toobuild your applications.</span></span> <span data-ttu-id="30d1c-107">Hello를 검토할 수 있습니다 [지역 및 해당 위치의 목록](https://azure.microsoft.com/regions/)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-107">You can review hello [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="30d1c-108">이 항목에서는 [라이브](#live_scenarios) 또는 [주문형](#vod_scenarios) 콘텐츠를 배달하는 일반적인 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="30d1c-109">또한 hello 항목 데이터 센터 간 미디어 기능 및 서비스의 가용성에 대 한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-109">hello topic also provides details about availability of media features and services across data centers.</span></span>

## <a name="overview"></a><span data-ttu-id="30d1c-110">개요</span><span class="sxs-lookup"><span data-stu-id="30d1c-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="30d1c-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30d1c-111">Prerequisites</span></span>

<span data-ttu-id="30d1c-112">Azure 미디어 서비스를 사용 하 여 toostart hello 다음 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-112">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="30d1c-113">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="30d1c-113">An Azure account.</span></span> <span data-ttu-id="30d1c-114">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="30d1c-115">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="30d1c-116">Azure Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="30d1c-116">An Azure Media Services account.</span></span> <span data-ttu-id="30d1c-117">자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="30d1c-118">스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 대 한 toobe **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-118">hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

    <span data-ttu-id="30d1c-119">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-119">When your AMS account is created, a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="30d1c-120">동적 패키징 및 동적 암호화를 hello 스트리밍 끝점의 콘텐츠 및 take 있다는 이점이 스트리밍 toostart hello에 대 한 toobe **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-120">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint has toobe in hello **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-hello-ams-odata-model"></a><span data-ttu-id="30d1c-121">일반적으로 사용 되는 개체 hello AMS OData 모델에 대해 개발할 때</span><span class="sxs-lookup"><span data-stu-id="30d1c-121">Commonly used objects when developing against hello AMS OData model</span></span>

<span data-ttu-id="30d1c-122">hello 다음 이미지에서는 가장 일반적으로 사용 하는 hello 개체 중 일부를 hello 미디어 서비스 OData 모델에 대해 개발할 때</span><span class="sxs-lookup"><span data-stu-id="30d1c-122">hello following image shows some of hello most commonly used objects when developing against hello Media Services OData model.</span></span>

<span data-ttu-id="30d1c-123">전체 크기로 hello 이미지 tooview를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-123">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="30d1c-124">Hello 전체 모델을 볼 수 있습니다 [여기](https://media.windows.net/API/$metadata?api-version=2.15)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-124">You can view hello whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-hello-clear-non-encrypted"></a><span data-ttu-id="30d1c-125">저장소의 콘텐츠를 보호 하 고 hello에서 스트리밍 미디어 배달 (암호화 되지 않은)의 선택을 취소합니다</span><span class="sxs-lookup"><span data-stu-id="30d1c-125">Protect content in storage and deliver streaming media in hello clear (non-encrypted)</span></span>

![VoD 워크플로](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="30d1c-127">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="30d1c-128">순서 tooprotect 하는 동안 콘텐츠를 업로드 및 저장소에 저장 된 상태의에서 tooapply 저장소 암호화 옵션 tooyour 자산 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-128">It is recommended tooapply storage encryption option tooyour asset in order tooprotect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="30d1c-129">Tooa 적응 비트 전송률 MP4 파일 집합을으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="30d1c-129">Encode tooa set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="30d1c-130">Tooapply 저장소 암호화 옵션 toohello 미사용 콘텐츠 순서 tooprotect에 자산을 출력 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-130">It is recommended tooapply storage encryption option toohello output asset in order tooprotect your content at rest.</span></span>
3. <span data-ttu-id="30d1c-131">자산 배달 정책(동적 패키징에서 사용)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="30d1c-132">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 **합니다** .</span><span class="sxs-lookup"><span data-stu-id="30d1c-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="30d1c-133">OnDemand 로케이터를 만들어 hello 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-133">Publish hello asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="30d1c-134">게시된 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-134">Stream published content.</span></span>

<span data-ttu-id="30d1c-135">데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-135">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="30d1c-136">저장소에서 콘텐츠를 보호하고 암호화된 스트리밍 미디어를 동적으로 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="30d1c-138">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="30d1c-139">저장소 암호화 옵션 toohello 자산을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-139">Apply storage encryption option toohello asset.</span></span>
2. <span data-ttu-id="30d1c-140">Tooa 적응 비트 전송률 MP4 파일 집합을으로 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="30d1c-140">Encode tooa set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="30d1c-141">저장소 암호화 옵션 toohello 출력 자산을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-141">Apply storage encryption option toohello output asset.</span></span>
3. <span data-ttu-id="30d1c-142">동적으로 재생 하는 동안 암호화 toobe 원하는 hello 자산에 대 한 암호화 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-142">Create encryption content key for hello asset you want toobe dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="30d1c-143">콘텐츠 키 인증 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="30d1c-144">자산 배달 정책(동적 패키징 및 동적 암호화에서 사용)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="30d1c-145">OnDemand 로케이터를 만들어 hello 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-145">Publish hello asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="30d1c-146">게시된 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-146">Stream published content.</span></span>

<span data-ttu-id="30d1c-147">데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-147">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-tooderive-actionable-insights-from-your-videos"></a><span data-ttu-id="30d1c-148">미디어 분석 tooderive 비디오에서 실행 가능한 통찰력을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="30d1c-148">Use Media Analytics tooderive actionable insights from your videos</span></span>

<span data-ttu-id="30d1c-149">미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 / 비전 구성 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="30d1c-150">자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="30d1c-151">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="30d1c-152">Hello에 설명 된 hello 미디어 분석 서비스 중 하나가 지정 된 비디오 처리 [미디어 분석 개요](media-services-analytics-overview.md) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-152">Process your videos with one of hello Media Analytics services described in hello [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="30d1c-153">미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="30d1c-154">미디어 프로세서 MP4 파일을 생성 하는 경우에 hello 파일을 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-154">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="30d1c-155">미디어 프로세서는 JSON 파일을 생성 하는 경우에 hello Azure blob 저장소에서에서 hello 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-155">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span>

<span data-ttu-id="30d1c-156">데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-156">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="30d1c-157">점진적 다운로드 제공</span><span class="sxs-lookup"><span data-stu-id="30d1c-157">Deliver progressive download</span></span>

1. <span data-ttu-id="30d1c-158">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="30d1c-159">Tooa 단일 MP4 파일로를 인코딩하십시오.</span><span class="sxs-lookup"><span data-stu-id="30d1c-159">Encode tooa single MP4 file.</span></span>
3. <span data-ttu-id="30d1c-160">요청 시 또는 SAS 로케이터를 만들어 hello 자산을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-160">Publish hello asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="30d1c-161">SAS 로케이터를 사용 하 여 hello 콘텐츠 hello Azure blob 저장소에서에서 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-161">If using SAS locator, hello content is downloaded from hello Azure blob storage.</span></span> <span data-ttu-id="30d1c-162">이 경우 toohave 스트리밍 채널 시작 됨된 상태에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-162">In this case, you do not need toohave streaming endpoints in started state.</span></span>
4. <span data-ttu-id="30d1c-163">콘텐츠를 점진적으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-163">Progressively download content.</span></span>

## <span data-ttu-id="30d1c-164"><a id="live_scenarios"></a>라이브 스트리밍 이벤트 배달</span><span class="sxs-lookup"><span data-stu-id="30d1c-164"><a id="live_scenarios"></a>Delivering live-streaming events</span></span> 

1. <span data-ttu-id="30d1c-165">다양한 라이브 스트리밍 프로토콜(예: RTMP 또는 부드러운 스트리밍)을 사용하여 라이브 콘텐츠를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="30d1c-166">(선택 사항)스트림을 적응 비트 전송률 스트림으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="30d1c-167">라이브 스트림을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-167">Preview your live stream.</span></span>
4. <span data-ttu-id="30d1c-168">일반 스트리밍 프로토콜 (예: MPEG DASH, 부드러운 스트리밍, HLS)를 통해 hello 콘텐츠 제공 직접 tooyour 고객 또는 향후 배포를 위해 tooa 네트워크 CDN (콘텐츠 배달).</span><span class="sxs-lookup"><span data-stu-id="30d1c-168">Deliver hello content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly tooyour customers, or tooa Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="30d1c-169">또는</span><span class="sxs-lookup"><span data-stu-id="30d1c-169">-or-</span></span>

    <span data-ttu-id="30d1c-170">순서 toobe의 레코드와 저장소 hello 수집 된 콘텐츠 이상 (주문형 비디오) 스트리밍.</span><span class="sxs-lookup"><span data-stu-id="30d1c-170">Record and store hello ingested content in order toobe streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="30d1c-171">라이브 스트리밍을 수행할 때 라우팅합니다 hello 다음 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-171">When doing live streaming, you can choose one of hello following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="30d1c-172">온-프레미스 인코더(통과)에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업</span><span class="sxs-lookup"><span data-stu-id="30d1c-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="30d1c-173">hello 다음 다이어그램에서는 hello와 관련 된 hello AMS 플랫폼의 주요 부분 hello **통과** 워크플로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-173">hello following diagram shows hello major parts of hello AMS platform that are involved in hello **pass-through** workflow.</span></span>

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="30d1c-175">자세한 내용은 [온-프레미스 인코더의 다중 비트 전송률 라이브 스트림을 수신하는 채널 사용](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a><span data-ttu-id="30d1c-176">채널을 사용 활성화 tooperform 라이브 Azure 미디어 서비스로 인코딩</span><span class="sxs-lookup"><span data-stu-id="30d1c-176">Working with channels that are enabled tooperform live encoding with Azure Media Services</span></span>

<span data-ttu-id="30d1c-177">hello 다음 그림에 hello를 주요 부분 hello AMS 플랫폼의 라이브 스트리밍 워크플로에 포함 되는 여기서 채널은 라이브 미디어 서비스로 인코딩 tooperform 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-177">hello following diagram shows hello major parts of hello AMS platform that are involved in Live Streaming workflow where a Channel is enabled tooperform live encoding with Media Services.</span></span>

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="30d1c-179">자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-179">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="30d1c-180">데이터 센터의 가용성에 대 한 정보를 참조 hello [가용성](#availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-180">For information about availability in datacenters, see hello [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="30d1c-181">콘텐츠 사용</span><span class="sxs-lookup"><span data-stu-id="30d1c-181">Consuming content</span></span>

<span data-ttu-id="30d1c-182">Azure 미디어 서비스는 hello 도구 toocreate rich 필요 등 대부분의 플랫폼에 대 한 동적 클라이언트 플레이어 응용 프로그램: iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-182">Azure Media Services provides hello tools you need toocreate rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="30d1c-183">hello 항목 링크 tooSDKs 및 플레이어 프레임 워크를 사용할 수 있는 toodevelop 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-183">hello following topic provides links tooSDKs and Player Frameworks that you can use toodevelop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="30d1c-184">자세한 내용은 [비디오 플레이어 응용 프로그램 개발](media-services-develop-video-players.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="30d1c-185">Azure CDN 사용하기</span><span class="sxs-lookup"><span data-stu-id="30d1c-185">Enabling Azure CDN</span></span>

<span data-ttu-id="30d1c-186">Media Services는 Azure CDN과의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="30d1c-187">방법에 대 한 Azure CDN tooenable 참조 [방법을 미디어 서비스 계정에서 tooManage 스트리밍 끝점](media-services-portal-manage-streaming-endpoints.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-187">For information on how tooenable Azure CDN, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <span data-ttu-id="30d1c-188"><a id="scaling"></a>Media Services 계정 크기 조정하기</span><span class="sxs-lookup"><span data-stu-id="30d1c-188"><a id="scaling"></a>Scaling a Media Services account</span></span>

<span data-ttu-id="30d1c-189">AMS 고객은 해당 AMS 계정에서 스트리밍 끝점, 미디어 처리 및 저장소의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="30d1c-190">Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="30d1c-191">**표준** 스트리밍 끝점은 대부분의 스트리밍 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="30d1c-192">Hello로 동일한 기능을 포함 한 **프리미엄** 끝점 및 배율 아웃 바운드 대역폭을 자동으로 스트리밍.</span><span class="sxs-lookup"><span data-stu-id="30d1c-192">It includes hello same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="30d1c-193">**프리미엄** 스트리밍 끝점은 고급 워크로드에 적합하며, 확장성 있는 전용 대역폭 용량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="30d1c-194">**프리미엄** 스트리밍 끝점이 있는 고객은 기본적으로 하나의 SU(스트리밍 단위)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="30d1c-195">SUs를 추가 하 여 hello 스트리밍 끝점을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-195">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="30d1c-196">각 SU 대역폭도 추가로 용량 toohello 응용 프로그램을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-196">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="30d1c-197">확장에 대 한 자세한 내용은 **프리미엄** hello 참조 스트리밍 끝점을 [스트리밍 끝점 확장](media-services-portal-scale-streaming-endpoints.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-197">For more information about scaling **Premium** streaming endpoints, see hello [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="30d1c-198">미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약 된 단위 유형과 연관 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-198">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="30d1c-199">Hello 다음 중에서 선택할 수 예약 단위 형식: **S1**, **S2**, 또는 **S3**합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-199">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="30d1c-200">Hello를 사용할 때 동일한 인코딩 작업이 더 빠르게 실행 하는 hello 예를 들어 **S2** toohello 비교 하는 예약된 단위 형식 **S1** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-200">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

    <span data-ttu-id="30d1c-201">또한 toospecifying hello 예약 단위 형식, tooprovision를 사용 하 여 계정을 지정할 수 있습니다 **예약 단위** (RUs).</span><span class="sxs-lookup"><span data-stu-id="30d1c-201">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="30d1c-202">프로 비전 된 RUs hello 수 hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-202">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="30d1c-203">RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="30d1c-204">그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="30d1c-205">자세한 내용은 [미디어 처리 크기 조정](media-services-portal-scale-media-processing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="30d1c-206">또한 저장소 계정 tooit를 추가 하 여 미디어 서비스 계정에 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-206">You can also scale your Media Services account by adding storage accounts tooit.</span></span> <span data-ttu-id="30d1c-207">각 저장소 계정은 제한 된 too500 TB입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-207">Each storage account is limited too500 TB.</span></span> <span data-ttu-id="30d1c-208">tooexpand hello 기본 제한 보다 크게 저장소를 선택할 수 있습니다 tooattach 여러 저장소 계정을 tooa 단일 미디어 서비스 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-208">tooexpand your storage beyond hello default limitations, you can choose tooattach multiple storage accounts tooa single Media Services account.</span></span> <span data-ttu-id="30d1c-209">자세한 내용은 [저장소 계정 관리](meda-services-managing-multiple-storage-accounts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<span data-ttu-id="30d1c-210"><a id="availability"></a>데이터 센터에서 Media Services 기능의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="30d1c-210"><a id="availability"></a> Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="30d1c-211">이 섹션에서는 데이터 센터에서 Media Services 기능 의 사용 가용성에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="30d1c-212">AMS 계정</span><span class="sxs-lookup"><span data-stu-id="30d1c-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-213">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-213">Availability</span></span>

<span data-ttu-id="30d1c-214">Hello 다음 지역에서에서 미디어 서비스 계정을 만들 수 있습니다: 북유럽, 서유럽, 미국 서 부, 미국 동부, 동남 아시아, 아시아 동부, 일본 서 부, 일본 동쪽, 브라질 남쪽, 인도 서 부, 인도 남부 및 중앙 인도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-214">You can create Media Services accounts in hello following regions: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="streaming-endpoints"></a><span data-ttu-id="30d1c-215">스트리밍 끝점</span><span class="sxs-lookup"><span data-stu-id="30d1c-215">Streaming endpoints</span></span> 

<span data-ttu-id="30d1c-216">Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="30d1c-217">자세한 내용은 참조 hello [배율](#scaling) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-217">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-218">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-218">Availability</span></span>

|<span data-ttu-id="30d1c-219">이름</span><span class="sxs-lookup"><span data-stu-id="30d1c-219">Name</span></span>|<span data-ttu-id="30d1c-220">가동 상태</span><span class="sxs-lookup"><span data-stu-id="30d1c-220">Status</span></span>|<span data-ttu-id="30d1c-221">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="30d1c-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="30d1c-222">Standard</span><span class="sxs-lookup"><span data-stu-id="30d1c-222">Standard</span></span>|<span data-ttu-id="30d1c-223">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-223">GA</span></span>|<span data-ttu-id="30d1c-224">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-224">All</span></span>|
|<span data-ttu-id="30d1c-225">Premium</span><span class="sxs-lookup"><span data-stu-id="30d1c-225">Premium</span></span>|<span data-ttu-id="30d1c-226">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-226">GA</span></span>|<span data-ttu-id="30d1c-227">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="30d1c-228">라이브 인코딩</span><span class="sxs-lookup"><span data-stu-id="30d1c-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-229">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-229">Availability</span></span>

<span data-ttu-id="30d1c-230">독일, 브라질 남부, 인도 서부, 인도 남부 및 인도 중부를 제외한 모든 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="30d1c-231">미디어 프로세서 인코딩</span><span class="sxs-lookup"><span data-stu-id="30d1c-231">Encoding media processors</span></span>

<span data-ttu-id="30d1c-232">AMS에서는 두 가지 주문형 인코더인 **Media Encoder Standard** 및 **Media Encoder Premium 워크플로**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="30d1c-233">자세한 내용은 [Azure 주문형 미디어 인코더의 개요 및 비교](media-services-encode-asset.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="30d1c-234">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-234">Availability</span></span>

|<span data-ttu-id="30d1c-235">미디어 프로세서 이름</span><span class="sxs-lookup"><span data-stu-id="30d1c-235">Media processor name</span></span>|<span data-ttu-id="30d1c-236">가동 상태</span><span class="sxs-lookup"><span data-stu-id="30d1c-236">Status</span></span>|<span data-ttu-id="30d1c-237">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="30d1c-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="30d1c-238">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="30d1c-238">Media Encoder Standard</span></span>|<span data-ttu-id="30d1c-239">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-239">GA</span></span>|<span data-ttu-id="30d1c-240">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-240">All</span></span>|
|<span data-ttu-id="30d1c-241">미디어 인코더 Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="30d1c-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="30d1c-242">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-242">GA</span></span>|<span data-ttu-id="30d1c-243">중국을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="30d1c-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="30d1c-244">분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="30d1c-244">Analytics media processors</span></span>

<span data-ttu-id="30d1c-245">미디어 분석은 쉽게 조직 및 기업 tooderive 실행 가능한 통찰력에 대 한 비디오 파일에서 음성 및 비전 구성 요소 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="30d1c-246">자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-247">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-247">Availability</span></span>

|<span data-ttu-id="30d1c-248">미디어 프로세서 이름</span><span class="sxs-lookup"><span data-stu-id="30d1c-248">Media processor name</span></span>|<span data-ttu-id="30d1c-249">가동 상태</span><span class="sxs-lookup"><span data-stu-id="30d1c-249">Status</span></span>|<span data-ttu-id="30d1c-250">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="30d1c-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="30d1c-251">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="30d1c-251">Azure Media Face Detector</span></span>|<span data-ttu-id="30d1c-252">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-252">Preview</span></span>|<span data-ttu-id="30d1c-253">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-253">All</span></span>|
|<span data-ttu-id="30d1c-254">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="30d1c-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="30d1c-255">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-255">Preview</span></span>|<span data-ttu-id="30d1c-256">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-256">All</span></span>|
|<span data-ttu-id="30d1c-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="30d1c-257">Azure Media Indexer</span></span>|<span data-ttu-id="30d1c-258">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-258">GA</span></span>|<span data-ttu-id="30d1c-259">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-259">All</span></span>|
|<span data-ttu-id="30d1c-260">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="30d1c-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="30d1c-261">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-261">Preview</span></span>|<span data-ttu-id="30d1c-262">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-262">All</span></span>|
|<span data-ttu-id="30d1c-263">Azure 미디어 OCR</span><span class="sxs-lookup"><span data-stu-id="30d1c-263">Azure Media OCR</span></span>|<span data-ttu-id="30d1c-264">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-264">Preview</span></span>|<span data-ttu-id="30d1c-265">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-265">All</span></span>|
|<span data-ttu-id="30d1c-266">Azure Media Redactor</span><span class="sxs-lookup"><span data-stu-id="30d1c-266">Azure Media Redactor</span></span>|<span data-ttu-id="30d1c-267">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-267">Preview</span></span>|<span data-ttu-id="30d1c-268">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-268">All</span></span>|
|<span data-ttu-id="30d1c-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="30d1c-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="30d1c-270">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-270">Preview</span></span>|<span data-ttu-id="30d1c-271">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-271">All</span></span>|
|<span data-ttu-id="30d1c-272">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="30d1c-273">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-273">Preview</span></span>|<span data-ttu-id="30d1c-274">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-274">All</span></span>|
|<span data-ttu-id="30d1c-275">Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="30d1c-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="30d1c-276">미리 보기</span><span class="sxs-lookup"><span data-stu-id="30d1c-276">Preview</span></span>|<span data-ttu-id="30d1c-277">중국 및 연방 정부 지역을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="30d1c-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="30d1c-278">보호</span><span class="sxs-lookup"><span data-stu-id="30d1c-278">Protection</span></span>

<span data-ttu-id="30d1c-279">Microsoft Azure 미디어 서비스 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-279">Microsoft Azure Media Services enables you toosecure your media from hello time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="30d1c-280">자세한 내용은 [AMS 콘텐츠 보호](media-services-content-protection-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30d1c-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-281">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-281">Availability</span></span>

|<span data-ttu-id="30d1c-282">암호화</span><span class="sxs-lookup"><span data-stu-id="30d1c-282">Encryption</span></span>|<span data-ttu-id="30d1c-283">가동 상태</span><span class="sxs-lookup"><span data-stu-id="30d1c-283">Status</span></span>|<span data-ttu-id="30d1c-284">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="30d1c-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="30d1c-285">저장소</span><span class="sxs-lookup"><span data-stu-id="30d1c-285">Storage</span></span>|<span data-ttu-id="30d1c-286">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-286">GA</span></span>|<span data-ttu-id="30d1c-287">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-287">All</span></span>|
|<span data-ttu-id="30d1c-288">AES-128 키</span><span class="sxs-lookup"><span data-stu-id="30d1c-288">AES-128 keys</span></span>|<span data-ttu-id="30d1c-289">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-289">GA</span></span>|<span data-ttu-id="30d1c-290">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-290">All</span></span>|
|<span data-ttu-id="30d1c-291">Fairplay</span><span class="sxs-lookup"><span data-stu-id="30d1c-291">Fairplay</span></span>|<span data-ttu-id="30d1c-292">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-292">GA</span></span>|<span data-ttu-id="30d1c-293">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-293">All</span></span>|
|<span data-ttu-id="30d1c-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="30d1c-294">PlayReady</span></span>|<span data-ttu-id="30d1c-295">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-295">GA</span></span>|<span data-ttu-id="30d1c-296">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-296">All</span></span>|
|<span data-ttu-id="30d1c-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="30d1c-297">Widevine</span></span>|<span data-ttu-id="30d1c-298">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-298">GA</span></span>|<span data-ttu-id="30d1c-299">독일, 연방 정부 및 중국을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="30d1c-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="30d1c-300">RU(예약 단위)</span><span class="sxs-lookup"><span data-stu-id="30d1c-300">Reserved units (RUs)</span></span>

<span data-ttu-id="30d1c-301">제공된 된 예약된 단위 수가 hello hello 지정된 된 계정에서 동시에 처리할 수 있는 미디어 작업 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-301">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="30d1c-302">자세한 내용은 참조 hello [배율](#scaling) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-302">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-303">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-303">Availability</span></span>

<span data-ttu-id="30d1c-304">모든 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="30d1c-305">RU(예약 단위) 형식</span><span class="sxs-lookup"><span data-stu-id="30d1c-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="30d1c-306">미디어 서비스 계정 작업을 처리 하 여 미디어 처리 되는 hello 속도 결정 하는 예약된 단위 형식과 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-306">A Media Services account is associated with a Reserved unit type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="30d1c-307">Hello 다음 중에서 선택할 수 예약 단위 형식: S1, S2 또는 s 3입니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-307">You can pick between hello following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="30d1c-308">자세한 내용은 참조 hello [배율](#scaling) 섹션.</span><span class="sxs-lookup"><span data-stu-id="30d1c-308">For more information, see hello [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="30d1c-309">Availability</span><span class="sxs-lookup"><span data-stu-id="30d1c-309">Availability</span></span>

|<span data-ttu-id="30d1c-310">RU 형식 이름</span><span class="sxs-lookup"><span data-stu-id="30d1c-310">RU type name</span></span>|<span data-ttu-id="30d1c-311">가동 상태</span><span class="sxs-lookup"><span data-stu-id="30d1c-311">Status</span></span>|<span data-ttu-id="30d1c-312">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="30d1c-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="30d1c-313">S1</span><span class="sxs-lookup"><span data-stu-id="30d1c-313">S1</span></span>|<span data-ttu-id="30d1c-314">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-314">GA</span></span>|<span data-ttu-id="30d1c-315">모두</span><span class="sxs-lookup"><span data-stu-id="30d1c-315">All</span></span>|
|<span data-ttu-id="30d1c-316">S2</span><span class="sxs-lookup"><span data-stu-id="30d1c-316">S2</span></span>|<span data-ttu-id="30d1c-317">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-317">GA</span></span>|<span data-ttu-id="30d1c-318">브라질 남부 및 인도 서부를 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="30d1c-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="30d1c-319">S3</span><span class="sxs-lookup"><span data-stu-id="30d1c-319">S3</span></span>|<span data-ttu-id="30d1c-320">GA</span><span class="sxs-lookup"><span data-stu-id="30d1c-320">GA</span></span>|<span data-ttu-id="30d1c-321">인도 서부를 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="30d1c-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="30d1c-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30d1c-322">Next steps</span></span>

<span data-ttu-id="30d1c-323">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="30d1c-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="30d1c-324">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="30d1c-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

