---
title: "Microsoft Azure Media Services 시나리오 및 데이터 센터에서 기능의 사용 가능성 | Microsoft Docs"
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
ms.openlocfilehash: d9994dd7bfb6b6bf949a7708c07651d667929ae4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-and-availability-of-media-services-features-across-datacenters"></a><span data-ttu-id="4f026-103">시나리오 및 데이터 센터에서 Media Services 기능의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="4f026-103">Scenarios and availability of Media Services features across datacenters</span></span>

<span data-ttu-id="4f026-104">Microsoft AMS(Azure Media Services)는 다양한 클라이언트(예: TV, PC 및 모바일 장치)로의 주문형 및 라이브 스트리밍 배달을 위해 비디오 또는 오디오 콘텐츠를 안전하게 업로드, 저장, 인코딩 및 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-104">Microsoft Azure Media Services (AMS) enables you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="4f026-105">AMS는 전 세계 여러 데이터 센터에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-105">AMS operates in multiple data centers around the world.</span></span> <span data-ttu-id="4f026-106">이러한 데이터 센터는 지리적 영역으로 그룹화되므로 응용 프로그램을 빌드할 위치를 유연하게 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-106">These data centers are grouped in to geographic regions, giving you flexibility in choosing where to build your applications.</span></span> <span data-ttu-id="4f026-107">[지역 및 위치 목록](https://azure.microsoft.com/regions/)을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-107">You can review the [list of regions and their locations](https://azure.microsoft.com/regions/).</span></span> 

<span data-ttu-id="4f026-108">이 항목에서는 [라이브](#live_scenarios) 또는 [주문형](#vod_scenarios) 콘텐츠를 배달하는 일반적인 시나리오를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-108">This topic shows common scenarios for delivering your content [live](#live_scenarios) or [on-demand](#vod_scenarios).</span></span> <span data-ttu-id="4f026-109">이 항목에서는 데이터 센터에서 미디어 기능 및 서비스의 사용 가용성에 대한 세부 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-109">The topic also provides details about availability of media features and services across data centers.</span></span>

## <a name="overview"></a><span data-ttu-id="4f026-110">개요</span><span class="sxs-lookup"><span data-stu-id="4f026-110">Overview</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4f026-111">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4f026-111">Prerequisites</span></span>

<span data-ttu-id="4f026-112">Azure Media Services 사용을 시작하려면 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-112">To start using Azure Media Services, you should have the following:</span></span>

* <span data-ttu-id="4f026-113">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="4f026-113">An Azure account.</span></span> <span data-ttu-id="4f026-114">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4f026-115">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-115">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="4f026-116">Azure Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="4f026-116">An Azure Media Services account.</span></span> <span data-ttu-id="4f026-117">자세한 내용은 [계정 만들기](media-services-portal-create-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-117">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="4f026-118">콘텐츠를 스트리밍하려는 스트리밍 끝점이 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-118">The streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span>

    <span data-ttu-id="4f026-119">AMS 계정이 만들어질 때 **기본** 스트리밍 끝점은 **중지됨** 상태에서 계정에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-119">When your AMS account is created, a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="4f026-120">콘텐츠 스트리밍을 시작하고 동적 패키징 및 동적 암호화를 활용하려면 스트리밍 끝점이 **실행** 상태에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-120">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint has to be in the **Running** state.</span></span>

### <a name="commonly-used-objects-when-developing-against-the-ams-odata-model"></a><span data-ttu-id="4f026-121">AMS OData 모델에 대해 개발할 때 일반적으로 사용되는 개체</span><span class="sxs-lookup"><span data-stu-id="4f026-121">Commonly used objects when developing against the AMS OData model</span></span>

<span data-ttu-id="4f026-122">다음 이미지에서는 Media Services OData 모델에 대해 개발할 때 가장 일반적으로 사용되는 개체 중 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-122">The following image shows some of the most commonly used objects when developing against the Media Services OData model.</span></span>

<span data-ttu-id="4f026-123">전체 크기로 보려면 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-123">Click the image to view it full size.</span></span>  

<a href="./media/media-services-overview/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-overview/media-services-overview-object-model-small.png"></a> 

<span data-ttu-id="4f026-124">전체 모델은 [여기](https://media.windows.net/API/$metadata?api-version=2.15)서 볼 수 있습니다 .</span><span class="sxs-lookup"><span data-stu-id="4f026-124">You can view the whole model [here](https://media.windows.net/API/$metadata?api-version=2.15).</span></span>  

## <a name="protect-content-in-storage-and-deliver-streaming-media-in-the-clear-non-encrypted"></a><span data-ttu-id="4f026-125">저장소에서 콘텐츠 보호 및 암호화하지 않고 스트리밍 미디어 배달(암호화되지 않음)</span><span class="sxs-lookup"><span data-stu-id="4f026-125">Protect content in storage and deliver streaming media in the clear (non-encrypted)</span></span>

![VoD 워크플로](./media/scenarios-and-availability/scenarios-and-availability01.png)

1. <span data-ttu-id="4f026-127">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-127">Upload a high-quality media file into an asset.</span></span>

    <span data-ttu-id="4f026-128">업로드하는 동안 및 저장소에 있는 동안 콘텐츠를 보호하기 위해 자산에 저장소 암호화 옵션을 적용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-128">It is recommended to apply storage encryption option to your asset in order to protect your content during upload and while at rest in storage.</span></span>
2. <span data-ttu-id="4f026-129">적응 비트 전송률 MP4 파일 집합으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-129">Encode to a set of adaptive bitrate MP4 files.</span></span>

    <span data-ttu-id="4f026-130">그대로 있는 콘텐츠를 보호하기 위해 출력 자산에 저장소 암호화 옵션을 적용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-130">It is recommended to apply storage encryption option to the output asset in order to protect your content at rest.</span></span>
3. <span data-ttu-id="4f026-131">자산 배달 정책(동적 패키징에서 사용)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-131">Configure asset delivery policy (used by dynamic packaging).</span></span>

    <span data-ttu-id="4f026-132">자산이 암호화된 저장소인 경우 자산 배달 정책을 구성해야 **합니다** .</span><span class="sxs-lookup"><span data-stu-id="4f026-132">If your asset is storage encrypted, you **must** configure asset delivery policy.</span></span>
4. <span data-ttu-id="4f026-133">주문형 로케이터를 만들어 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-133">Publish the asset by creating an OnDemand locator.</span></span>
5. <span data-ttu-id="4f026-134">게시된 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-134">Stream published content.</span></span>

<span data-ttu-id="4f026-135">데이터 센터에서 사용 가용성에 대한 정보는 [사용 가능성](#availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-135">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="protect-content-in-storage-deliver-dynamically-encrypted-streaming-media"></a><span data-ttu-id="4f026-136">저장소에서 콘텐츠를 보호하고 암호화된 스트리밍 미디어를 동적으로 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-136">Protect content in storage, deliver dynamically encrypted streaming media</span></span>

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

1. <span data-ttu-id="4f026-138">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-138">Upload a high-quality media file into an asset.</span></span> <span data-ttu-id="4f026-139">저장소 암호화 옵션을 자산에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-139">Apply storage encryption option to the asset.</span></span>
2. <span data-ttu-id="4f026-140">적응 비트 전송률 MP4 파일 집합으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-140">Encode to a set of adaptive bitrate MP4 files.</span></span> <span data-ttu-id="4f026-141">저장소 암호화 옵션을 출력 자산에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-141">Apply storage encryption option to the output asset.</span></span>
3. <span data-ttu-id="4f026-142">재생하는 동안 동적으로 암호화하려는 경우 자산에 대한 암호화 콘텐츠 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-142">Create encryption content key for the asset you want to be dynamically encrypted during playback.</span></span>
4. <span data-ttu-id="4f026-143">콘텐츠 키 인증 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-143">Configure content key authorization policy.</span></span>
5. <span data-ttu-id="4f026-144">자산 배달 정책(동적 패키징 및 동적 암호화에서 사용)을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-144">Configure asset delivery policy (used by dynamic packaging and dynamic encryption).</span></span>
6. <span data-ttu-id="4f026-145">주문형 로케이터를 만들어 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-145">Publish the asset by creating an OnDemand locator.</span></span>
7. <span data-ttu-id="4f026-146">게시된 콘텐츠를 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-146">Stream published content.</span></span>

<span data-ttu-id="4f026-147">데이터 센터에서 사용 가용성에 대한 정보는 [사용 가능성](#availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-147">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="use-media-analytics-to-derive-actionable-insights-from-your-videos"></a><span data-ttu-id="4f026-148">미디어 분석을 사용하여 비디오에 대한 실질적인 통찰력 얻기</span><span class="sxs-lookup"><span data-stu-id="4f026-148">Use Media Analytics to derive actionable insights from your videos</span></span>

<span data-ttu-id="4f026-149">미디어 분석은 조직과 기업이 비디오 파일에서 실질적인 통찰력을 끌어내기 쉽도록 만드는 언어 및 시각 구성 요소 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-149">Media Analytics is a collection of speech and vision components that make it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="4f026-150">자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-150">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

1. <span data-ttu-id="4f026-151">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-151">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="4f026-152">[미디어 분석 개요](media-services-analytics-overview.md) 섹션에 설명된 미디어 분석 서비스 중 하나를 사용하여 비디오를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-152">Process your videos with one of the Media Analytics services described in the [Media Analytics overview](media-services-analytics-overview.md) section.</span></span>
3. <span data-ttu-id="4f026-153">미디어 분석 미디어 프로세서는 MP4 파일 또는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-153">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="4f026-154">미디어 프로세서가 MP4 파일을 생성한 경우 파일을 점진적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-154">If a media processor produced an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="4f026-155">미디어 프로세서가 JSON 파일을 생성한 경우 Azure Blob 저장소에서 해당 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-155">If a media processor produced a JSON file, you can download the file from the Azure blob storage.</span></span>

<span data-ttu-id="4f026-156">데이터 센터에서 사용 가용성에 대한 정보는 [사용 가능성](#availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-156">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="deliver-progressive-download"></a><span data-ttu-id="4f026-157">점진적 다운로드 제공</span><span class="sxs-lookup"><span data-stu-id="4f026-157">Deliver progressive download</span></span>

1. <span data-ttu-id="4f026-158">자산에 고품질 미디어 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-158">Upload a high-quality media file into an asset.</span></span>
2. <span data-ttu-id="4f026-159">하나의 MP4 파일로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-159">Encode to a single MP4 file.</span></span>
3. <span data-ttu-id="4f026-160">주문형 또는 SAS 로케이터를 만들어 자산을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-160">Publish the asset by creating an OnDemand or SAS locator.</span></span>

    <span data-ttu-id="4f026-161">SAS 로케이터를 사용하는 경우 콘텐츠는 Azure blob 저장소에서 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-161">If using SAS locator, the content is downloaded from the Azure blob storage.</span></span> <span data-ttu-id="4f026-162">이 경우 스트리밍 끝점이 시작된 상태에 있을 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-162">In this case, you do not need to have streaming endpoints in started state.</span></span>
4. <span data-ttu-id="4f026-163">콘텐츠를 점진적으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-163">Progressively download content.</span></span>

## <span data-ttu-id="4f026-164"><a id="live_scenarios"></a>라이브 스트리밍 이벤트 배달</span><span class="sxs-lookup"><span data-stu-id="4f026-164"><a id="live_scenarios"></a>Delivering live-streaming events</span></span> 

1. <span data-ttu-id="4f026-165">다양한 라이브 스트리밍 프로토콜(예: RTMP 또는 부드러운 스트리밍)을 사용하여 라이브 콘텐츠를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-165">Ingest live content using various live streaming protocols (for example RTMP or Smooth Streaming).</span></span>
2. <span data-ttu-id="4f026-166">(선택 사항)스트림을 적응 비트 전송률 스트림으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-166">(optionally) Encode your stream into adaptive bitrate stream.</span></span>
3. <span data-ttu-id="4f026-167">라이브 스트림을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-167">Preview your live stream.</span></span>
4. <span data-ttu-id="4f026-168">일반적인 스트리밍 프로토콜(예: MPEG DASH, 부드러운, HLS)을 통해 고객에게 직접 또는 추가 배포를 위해 CDN(Content Delivery Network)에 콘텐츠를 배달합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-168">Deliver the content through common streaming protocols (for example, MPEG DASH, Smooth, HLS) directly to your customers, or to a Content Delivery Network (CDN) for further distribution.</span></span>

    <span data-ttu-id="4f026-169">또는</span><span class="sxs-lookup"><span data-stu-id="4f026-169">-or-</span></span>

    <span data-ttu-id="4f026-170">나중에 스트리밍하기 위해 수집된 콘텐츠를 기록 및 저장합니다(주문형 비디오).</span><span class="sxs-lookup"><span data-stu-id="4f026-170">Record and store the ingested content in order to be streamed later (Video-on-Demand).</span></span>

<span data-ttu-id="4f026-171">라이브 스트리밍을 수행할 때 다음 경로 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-171">When doing live streaming, you can choose one of the following routes:</span></span>

### <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a><span data-ttu-id="4f026-172">온-프레미스 인코더(통과)에서 다중 비트 전송률 라이브 스트림을 받는 채널 작업</span><span class="sxs-lookup"><span data-stu-id="4f026-172">Working with channels that receive multi-bitrate live stream from on-premises encoders (pass-through)</span></span>

<span data-ttu-id="4f026-173">다음 다이어그램에서는 **통과** 워크플로에 관련된 AMS 플랫폼의 주요 부분을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-173">The following diagram shows the major parts of the AMS platform that are involved in the **pass-through** workflow.</span></span>

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-current.png)

<span data-ttu-id="4f026-175">자세한 내용은 [온-프레미스 인코더의 다중 비트 전송률 라이브 스트림을 수신하는 채널 사용](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-175">For more information, see [Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders](media-services-live-streaming-with-onprem-encoders.md).</span></span>

### <a name="working-with-channels-that-are-enabled-to-perform-live-encoding-with-azure-media-services"></a><span data-ttu-id="4f026-176">Azure Media Services를 사용하여 라이브 인코딩을 수행할 수 있는 채널 작업</span><span class="sxs-lookup"><span data-stu-id="4f026-176">Working with channels that are enabled to perform live encoding with Azure Media Services</span></span>

<span data-ttu-id="4f026-177">다음 다이어그램에서는 채널이 Media Services를 통해 라이브 인코딩을 수행할 수 있는 라이브 스트리밍 워크플로에 관련된 AMS 플랫폼의 주요 부분을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-177">The following diagram shows the major parts of the AMS platform that are involved in Live Streaming workflow where a Channel is enabled to perform live encoding with Media Services.</span></span>

![라이브 워크플로](./media/scenarios-and-availability/media-services-live-streaming-new.png)

<span data-ttu-id="4f026-179">자세한 내용은 [Azure 미디어 서비스를 사용하여 라이브 인코딩을 수행할 수 있는 채널 작업](media-services-manage-live-encoder-enabled-channels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-179">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="4f026-180">데이터 센터에서 사용 가용성에 대한 정보는 [사용 가능성](#availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-180">For information about availability in datacenters, see the [Availability](#availability) section.</span></span>

## <a name="consuming-content"></a><span data-ttu-id="4f026-181">콘텐츠 사용</span><span class="sxs-lookup"><span data-stu-id="4f026-181">Consuming content</span></span>

<span data-ttu-id="4f026-182">Azure Media Services는 iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 박스를 포함한 대부분의 플랫폼에서 풍부한 동적 클라이언트 플레이어 응용 프로그램을 만드는 데 필요한 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-182">Azure Media Services provides the tools you need to create rich, dynamic client player applications for most platforms including: iOS Devices, Android Devices, Windows, Windows Phone, Xbox, and Set-top boxes.</span></span> <span data-ttu-id="4f026-183">다음 항목에서 제공하는 SDK 및 플레이어 프레임워크 링크를 사용하여 Media Services의 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-183">The following topic provides links to SDKs and Player Frameworks that you can use to develop your own client applications that can consume streaming media from Media Services.</span></span> <span data-ttu-id="4f026-184">자세한 내용은 [비디오 플레이어 응용 프로그램 개발](media-services-develop-video-players.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-184">For more information, see [Developing video payer applications](media-services-develop-video-players.md)</span></span>

## <a name="enabling-azure-cdn"></a><span data-ttu-id="4f026-185">Azure CDN 사용하기</span><span class="sxs-lookup"><span data-stu-id="4f026-185">Enabling Azure CDN</span></span>

<span data-ttu-id="4f026-186">Media Services는 Azure CDN과의 통합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-186">Media Services supports integration with Azure CDN.</span></span> <span data-ttu-id="4f026-187">Azure CDN을 사용하도록 설정하는 방법에 대한 자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점을 관리하는 방법](media-services-portal-manage-streaming-endpoints.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-187">For information on how to enable Azure CDN, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>

## <span data-ttu-id="4f026-188"><a id="scaling"></a>Media Services 계정 크기 조정하기</span><span class="sxs-lookup"><span data-stu-id="4f026-188"><a id="scaling"></a>Scaling a Media Services account</span></span>

<span data-ttu-id="4f026-189">AMS 고객은 해당 AMS 계정에서 스트리밍 끝점, 미디어 처리 및 저장소의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-189">AMS customers can scale streaming endpoints, media processing, and storage in their AMS accounts.</span></span>

* <span data-ttu-id="4f026-190">Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-190">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="4f026-191">**표준** 스트리밍 끝점은 대부분의 스트리밍 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-191">A **Standard** streaming endpoint is suitable for most streaming workloads.</span></span> <span data-ttu-id="4f026-192">**프리미엄** 스트리밍 단위와 동일한 기능을 포함하고 아웃바운드 대역폭을 자동으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-192">It includes the same features as a **Premium** streaming endpoints and scales outbound bandwidth automatically.</span></span> 

    <span data-ttu-id="4f026-193">**프리미엄** 스트리밍 끝점은 고급 워크로드에 적합하며, 확장성 있는 전용 대역폭 용량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-193">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="4f026-194">**프리미엄** 스트리밍 끝점이 있는 고객은 기본적으로 하나의 SU(스트리밍 단위)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-194">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="4f026-195">SU를 추가하여 스트리밍 끝점의 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-195">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="4f026-196">각 SU는 응용 프로그램에 추가 대역폭 수용작업량을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-196">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="4f026-197">**프리미엄** 스트리밍 끝점의 크기를 조정하는 방법에 대한 자세한 내용은 [스트리밍 끝점 크기 조정](media-services-portal-scale-streaming-endpoints.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-197">For more information about scaling **Premium** streaming endpoints, see the [Scaling streaming endpoints](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

* <span data-ttu-id="4f026-198">미디어 서비스 계정은 미디어 처리 작업을 처리하는 속도를 결정하는 예약 단위 형식과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-198">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="4f026-199">**S1**, **S2**, **S3** 예약 단위 유형 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-199">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="4f026-200">예를 들어 **S2** 예약 단위 유형을 사용하는 경우 **S1** 유형에 비해 동일한 인코딩 작업이 더 빠르게 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-200">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

    <span data-ttu-id="4f026-201">예약 단위 유형을 지정하는 것 외에도 계정에 **RU(예약 단위)**를 프로비전하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-201">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="4f026-202">프로비전되는 RU의 수에 따라 특정 계정에서 동시에 처리할 수 있는 미디어 작업의 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-202">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4f026-203">RU는 Azure Media Indexer를 사용하는 인덱싱 작업을 비롯하여 모든 미디어 처리 병렬화에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-203">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="4f026-204">그러나 인코딩과 달리 인덱싱 작업은 예약 단위가 더 빠르게 실행되어도 더 빨리 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-204">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

    <span data-ttu-id="4f026-205">자세한 내용은 [미디어 처리 크기 조정](media-services-portal-scale-media-processing.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-205">For more information see, [Scale media processing](media-services-portal-scale-media-processing.md).</span></span>
* <span data-ttu-id="4f026-206">또한 저장소 계정을 추가하여 Media Services 계정을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-206">You can also scale your Media Services account by adding storage accounts to it.</span></span> <span data-ttu-id="4f026-207">각 저장소 계정은 500TB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-207">Each storage account is limited to 500 TB.</span></span> <span data-ttu-id="4f026-208">여러 저장소 계정을 단일 Media Services 계정에 연결하여 기본 제한 이상으로 저장소를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-208">To expand your storage beyond the default limitations, you can choose to attach multiple storage accounts to a single Media Services account.</span></span> <span data-ttu-id="4f026-209">자세한 내용은 [저장소 계정 관리](meda-services-managing-multiple-storage-accounts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-209">For more information, see [Manage storage accounts](meda-services-managing-multiple-storage-accounts.md).</span></span>

##<span data-ttu-id="4f026-210"><a id="availability"></a>데이터 센터에서 Media Services 기능의 사용 가용성</span><span class="sxs-lookup"><span data-stu-id="4f026-210"><a id="availability"></a> Availability of Media Services features across datacenters</span></span>

<span data-ttu-id="4f026-211">이 섹션에서는 데이터 센터에서 Media Services 기능 의 사용 가용성에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-211">This section provides details about availability of Media Services features across datacenters.</span></span>

### <a name="ams-accounts"></a><span data-ttu-id="4f026-212">AMS 계정</span><span class="sxs-lookup"><span data-stu-id="4f026-212">AMS accounts</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-213">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-213">Availability</span></span>

<span data-ttu-id="4f026-214">북유럽, 유럽 서부, 미국 서부, 미국 동부, 동남 아시아, 동아시아, 일본 서부, 일본 동부, 브라질 남부, 인도 서부, 인도 남부 및 인도 중부 지역에서 Media Services 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-214">You can create Media Services accounts in the following regions: North Europe, West Europe, West US, East US, Southeast Asia, East Asia, Japan West, Japan East, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="streaming-endpoints"></a><span data-ttu-id="4f026-215">스트리밍 끝점</span><span class="sxs-lookup"><span data-stu-id="4f026-215">Streaming endpoints</span></span> 

<span data-ttu-id="4f026-216">Media Services 고객은 **표준** 스트리밍 끝점이나 **프리미엄** 스트리밍 끝점을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-216">Media Services customers can choose either a **Standard** streaming endpoint or a **Premium** streaming endpoint.</span></span> <span data-ttu-id="4f026-217">자세한 내용은 [크기 조정](#scaling) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-217">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-218">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-218">Availability</span></span>

|<span data-ttu-id="4f026-219">이름</span><span class="sxs-lookup"><span data-stu-id="4f026-219">Name</span></span>|<span data-ttu-id="4f026-220">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4f026-220">Status</span></span>|<span data-ttu-id="4f026-221">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="4f026-221">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="4f026-222">Standard</span><span class="sxs-lookup"><span data-stu-id="4f026-222">Standard</span></span>|<span data-ttu-id="4f026-223">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-223">GA</span></span>|<span data-ttu-id="4f026-224">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-224">All</span></span>|
|<span data-ttu-id="4f026-225">Premium</span><span class="sxs-lookup"><span data-stu-id="4f026-225">Premium</span></span>|<span data-ttu-id="4f026-226">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-226">GA</span></span>|<span data-ttu-id="4f026-227">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-227">All</span></span>|

### <a name="live-encoding"></a><span data-ttu-id="4f026-228">라이브 인코딩</span><span class="sxs-lookup"><span data-stu-id="4f026-228">Live encoding</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-229">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-229">Availability</span></span>

<span data-ttu-id="4f026-230">독일, 브라질 남부, 인도 서부, 인도 남부 및 인도 중부를 제외한 모든 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-230">Available in all datacenters except: Germany, Brazil South, India West, India South, and India Central.</span></span> 

### <a name="encoding-media-processors"></a><span data-ttu-id="4f026-231">미디어 프로세서 인코딩</span><span class="sxs-lookup"><span data-stu-id="4f026-231">Encoding media processors</span></span>

<span data-ttu-id="4f026-232">AMS에서는 두 가지 주문형 인코더인 **Media Encoder Standard** 및 **Media Encoder Premium 워크플로**를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-232">AMS offers two on-demand encoders **Media Encoder Standard** and **Media Encoder Premium Workflow**.</span></span> <span data-ttu-id="4f026-233">자세한 내용은 [Azure 주문형 미디어 인코더의 개요 및 비교](media-services-encode-asset.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-233">For more information, see [Overview and comparison of Azure on-demand media encoders](media-services-encode-asset.md).</span></span> 

#### <a name="availability"></a><span data-ttu-id="4f026-234">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-234">Availability</span></span>

|<span data-ttu-id="4f026-235">미디어 프로세서 이름</span><span class="sxs-lookup"><span data-stu-id="4f026-235">Media processor name</span></span>|<span data-ttu-id="4f026-236">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4f026-236">Status</span></span>|<span data-ttu-id="4f026-237">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="4f026-237">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="4f026-238">미디어 인코더 표준</span><span class="sxs-lookup"><span data-stu-id="4f026-238">Media Encoder Standard</span></span>|<span data-ttu-id="4f026-239">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-239">GA</span></span>|<span data-ttu-id="4f026-240">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-240">All</span></span>|
|<span data-ttu-id="4f026-241">미디어 인코더 Premium 워크플로</span><span class="sxs-lookup"><span data-stu-id="4f026-241">Media Encoder Premium Workflow</span></span>|<span data-ttu-id="4f026-242">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-242">GA</span></span>|<span data-ttu-id="4f026-243">중국을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="4f026-243">All except China</span></span>|

### <a name="analytics-media-processors"></a><span data-ttu-id="4f026-244">분석 미디어 프로세서</span><span class="sxs-lookup"><span data-stu-id="4f026-244">Analytics media processors</span></span>

<span data-ttu-id="4f026-245">미디어 분석은 조직과 기업이 비디오 파일에서 실질적인 통찰력을 끌어내기 쉽도록 만드는 언어 및 시각 구성 요소 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-245">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="4f026-246">자세한 내용은 [Azure Media Services 분석 개요](media-services-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-246">For more information, see [Azure Media Services Analytics Overview](media-services-analytics-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-247">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-247">Availability</span></span>

|<span data-ttu-id="4f026-248">미디어 프로세서 이름</span><span class="sxs-lookup"><span data-stu-id="4f026-248">Media processor name</span></span>|<span data-ttu-id="4f026-249">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4f026-249">Status</span></span>|<span data-ttu-id="4f026-250">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="4f026-250">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="4f026-251">Azure 미디어 얼굴 탐지기</span><span class="sxs-lookup"><span data-stu-id="4f026-251">Azure Media Face Detector</span></span>|<span data-ttu-id="4f026-252">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-252">Preview</span></span>|<span data-ttu-id="4f026-253">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-253">All</span></span>|
|<span data-ttu-id="4f026-254">Azure 미디어 Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="4f026-254">Azure Media Hyperlapse</span></span>|<span data-ttu-id="4f026-255">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-255">Preview</span></span>|<span data-ttu-id="4f026-256">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-256">All</span></span>|
|<span data-ttu-id="4f026-257">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="4f026-257">Azure Media Indexer</span></span>|<span data-ttu-id="4f026-258">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-258">GA</span></span>|<span data-ttu-id="4f026-259">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-259">All</span></span>|
|<span data-ttu-id="4f026-260">Azure 미디어 동작 탐지기</span><span class="sxs-lookup"><span data-stu-id="4f026-260">Azure Media Motion Detector</span></span>|<span data-ttu-id="4f026-261">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-261">Preview</span></span>|<span data-ttu-id="4f026-262">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-262">All</span></span>|
|<span data-ttu-id="4f026-263">Azure 미디어 OCR</span><span class="sxs-lookup"><span data-stu-id="4f026-263">Azure Media OCR</span></span>|<span data-ttu-id="4f026-264">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-264">Preview</span></span>|<span data-ttu-id="4f026-265">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-265">All</span></span>|
|<span data-ttu-id="4f026-266">Azure Media Redactor</span><span class="sxs-lookup"><span data-stu-id="4f026-266">Azure Media Redactor</span></span>|<span data-ttu-id="4f026-267">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-267">Preview</span></span>|<span data-ttu-id="4f026-268">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-268">All</span></span>|
|<span data-ttu-id="4f026-269">Azure Media Stabilizer</span><span class="sxs-lookup"><span data-stu-id="4f026-269">Azure Media Stabilizer</span></span>|<span data-ttu-id="4f026-270">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-270">Preview</span></span>|<span data-ttu-id="4f026-271">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-271">All</span></span>|
|<span data-ttu-id="4f026-272">Azure 미디어 비디오 미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-272">Azure Media Video Thumbnails</span></span>|<span data-ttu-id="4f026-273">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-273">Preview</span></span>|<span data-ttu-id="4f026-274">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-274">All</span></span>|
|<span data-ttu-id="4f026-275">Azure Media Indexer 2</span><span class="sxs-lookup"><span data-stu-id="4f026-275">Azure Media Indexer 2</span></span>|<span data-ttu-id="4f026-276">미리 보기</span><span class="sxs-lookup"><span data-stu-id="4f026-276">Preview</span></span>|<span data-ttu-id="4f026-277">중국 및 연방 정부 지역을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="4f026-277">All except China and Federal Government region</span></span>|

### <a name="protection"></a><span data-ttu-id="4f026-278">보호</span><span class="sxs-lookup"><span data-stu-id="4f026-278">Protection</span></span>

<span data-ttu-id="4f026-279">Microsoft Azure 미디어 서비스를 사용하면 컴퓨터를 떠날 때부터 저장, 처리 및 배달에 이르는 과정 내내 미디어를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-279">Microsoft Azure Media Services enables you to secure your media from the time it leaves your computer through storage, processing, and delivery.</span></span> <span data-ttu-id="4f026-280">자세한 내용은 [AMS 콘텐츠 보호](media-services-content-protection-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-280">For more information, see [Protecting AMS content](media-services-content-protection-overview.md).</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-281">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-281">Availability</span></span>

|<span data-ttu-id="4f026-282">암호화</span><span class="sxs-lookup"><span data-stu-id="4f026-282">Encryption</span></span>|<span data-ttu-id="4f026-283">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4f026-283">Status</span></span>|<span data-ttu-id="4f026-284">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="4f026-284">Datacenters</span></span>|
|---|---|---| 
|<span data-ttu-id="4f026-285">저장소</span><span class="sxs-lookup"><span data-stu-id="4f026-285">Storage</span></span>|<span data-ttu-id="4f026-286">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-286">GA</span></span>|<span data-ttu-id="4f026-287">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-287">All</span></span>|
|<span data-ttu-id="4f026-288">AES-128 키</span><span class="sxs-lookup"><span data-stu-id="4f026-288">AES-128 keys</span></span>|<span data-ttu-id="4f026-289">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-289">GA</span></span>|<span data-ttu-id="4f026-290">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-290">All</span></span>|
|<span data-ttu-id="4f026-291">Fairplay</span><span class="sxs-lookup"><span data-stu-id="4f026-291">Fairplay</span></span>|<span data-ttu-id="4f026-292">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-292">GA</span></span>|<span data-ttu-id="4f026-293">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-293">All</span></span>|
|<span data-ttu-id="4f026-294">PlayReady</span><span class="sxs-lookup"><span data-stu-id="4f026-294">PlayReady</span></span>|<span data-ttu-id="4f026-295">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-295">GA</span></span>|<span data-ttu-id="4f026-296">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-296">All</span></span>|
|<span data-ttu-id="4f026-297">Widevine</span><span class="sxs-lookup"><span data-stu-id="4f026-297">Widevine</span></span>|<span data-ttu-id="4f026-298">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-298">GA</span></span>|<span data-ttu-id="4f026-299">독일, 연방 정부 및 중국을 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="4f026-299">All except Germany, Federal Government and China.</span></span>

### <a name="reserved-units-rus"></a><span data-ttu-id="4f026-300">RU(예약 단위)</span><span class="sxs-lookup"><span data-stu-id="4f026-300">Reserved units (RUs)</span></span>

<span data-ttu-id="4f026-301">프로비전되는 예약 단위의 수에 따라 특정 계정에서 동시에 처리할 수 있는 미디어 작업의 수가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-301">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> 

<span data-ttu-id="4f026-302">자세한 내용은 [크기 조정](#scaling) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-302">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-303">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-303">Availability</span></span>

<span data-ttu-id="4f026-304">모든 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-304">Available in all datacenters.</span></span>

### <a name="reserved-unit-ru-type"></a><span data-ttu-id="4f026-305">RU(예약 단위) 형식</span><span class="sxs-lookup"><span data-stu-id="4f026-305">Reserved unit (RU) type</span></span>

<span data-ttu-id="4f026-306">Media Services 계정은 미디어 처리 작업을 처리하는 속도를 결정하는 예약 단위 형식과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-306">A Media Services account is associated with a Reserved unit type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="4f026-307">S1, S2 또는 S3과 같은 예약 단위 형식 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-307">You can pick between the following reserved unit types: S1, S2, or S3.</span></span>

<span data-ttu-id="4f026-308">자세한 내용은 [크기 조정](#scaling) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f026-308">For more information, see the [scaling](#scaling) section.</span></span>

#### <a name="availability"></a><span data-ttu-id="4f026-309">Availability</span><span class="sxs-lookup"><span data-stu-id="4f026-309">Availability</span></span>

|<span data-ttu-id="4f026-310">RU 형식 이름</span><span class="sxs-lookup"><span data-stu-id="4f026-310">RU type name</span></span>|<span data-ttu-id="4f026-311">가동 상태</span><span class="sxs-lookup"><span data-stu-id="4f026-311">Status</span></span>|<span data-ttu-id="4f026-312">데이터 센터</span><span class="sxs-lookup"><span data-stu-id="4f026-312">Datacenters</span></span>
|---|---|---|
|<span data-ttu-id="4f026-313">S1</span><span class="sxs-lookup"><span data-stu-id="4f026-313">S1</span></span>|<span data-ttu-id="4f026-314">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-314">GA</span></span>|<span data-ttu-id="4f026-315">모두</span><span class="sxs-lookup"><span data-stu-id="4f026-315">All</span></span>|
|<span data-ttu-id="4f026-316">S2</span><span class="sxs-lookup"><span data-stu-id="4f026-316">S2</span></span>|<span data-ttu-id="4f026-317">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-317">GA</span></span>|<span data-ttu-id="4f026-318">브라질 남부 및 인도 서부를 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="4f026-318">All except Brazil South, and India West</span></span>|
|<span data-ttu-id="4f026-319">S3</span><span class="sxs-lookup"><span data-stu-id="4f026-319">S3</span></span>|<span data-ttu-id="4f026-320">GA</span><span class="sxs-lookup"><span data-stu-id="4f026-320">GA</span></span>|<span data-ttu-id="4f026-321">인도 서부를 제외한 모든 지역</span><span class="sxs-lookup"><span data-stu-id="4f026-321">All except India West</span></span>|

## <a name="next-steps"></a><span data-ttu-id="4f026-322">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f026-322">Next steps</span></span>

<span data-ttu-id="4f026-323">Media Services 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4f026-323">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4f026-324">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="4f026-324">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

