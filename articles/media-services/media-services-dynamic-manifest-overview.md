---
title: "aaaFilters 및 동적 매니페스트 | Microsoft Docs"
description: "이 항목에서는 클라이언트 toostream 스트림의 특정 섹션 사용할 수 있도록 toocreate 필터링 하는 방법을 설명 합니다. 미디어 서비스 스트리밍이 선택적 tooarchive를 동적 매니페스트를 만듭니다."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a><span data-ttu-id="c374e-104">필터 및 동적 매니페스트</span><span class="sxs-lookup"><span data-stu-id="c374e-104">Filters and dynamic manifests</span></span>
<span data-ttu-id="c374e-105">2.11 버전부터 미디어 서비스를 사용 하면 자산에 대 한 toodefine 필터.</span><span class="sxs-lookup"><span data-stu-id="c374e-105">Starting with 2.11 release, Media Services enables you toodefine filters for your assets.</span></span> <span data-ttu-id="c374e-106">이러한 필터는 고객에 게 toochoose toodo 등으로 나눌 수 있는 서버 쪽 규칙: 재생 (재생 하지 않고 hello 전체 비디오), 비디오의 섹션만 고객의 장치 (처리할 수 있도록 하는 오디오 및 비디오 변환의 하위 집합을 지정 하거나 모든 hello 변환 하는 대신 연결 된 hello 자산에).</span><span class="sxs-lookup"><span data-stu-id="c374e-106">These filters are server side rules that will allow your customers toochoose toodo things like: playback only a section of a video (instead of playing hello whole video), or specify only a subset of audio and video renditions that your customer's device can handle (instead of all hello renditions that are associated with hello asset).</span></span> <span data-ttu-id="c374e-107">자산의 필터링이 통해 보관 **동적 매니페스트**비디오 고객의 요청 toostream 시 생성 되는 지정 된 필터에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-107">This filtering of your assets is archived through **Dynamic Manifest**s that are created upon your customer's request toostream a video based on specified filter(s).</span></span>

<span data-ttu-id="c374e-108">이 항목에서는 일반적인 시나리오에 필터를 사용 하 여 유익함 tooyour 고객과 링크 tootopics toocreate를 프로그래밍 방식으로 필터링 하는 방법을 보여 주는 것 (현재 필터를 만들 있습니다 REST Api와만).</span><span class="sxs-lookup"><span data-stu-id="c374e-108">This topics discusses common scenarios in which using filters would be very beneficial tooyour customers and links tootopics that demonstrate how toocreate filters programmatically (currently, you can create filters with REST APIs only).</span></span>

## <a name="overview"></a><span data-ttu-id="c374e-109">개요</span><span class="sxs-lookup"><span data-stu-id="c374e-109">Overview</span></span>
<span data-ttu-id="c374e-110">여기서의 목표 (스트리밍 라이브 이벤트 또는 주문형 비디오) 사용자 콘텐츠 toocustomers 배달할 때 toodeliver 다양 한 네트워크 조건에서 고품질의 비디오 toovarious 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-110">When delivering your content toocustomers (streaming live events or video-on-demand) your goal is toodeliver a high quality video toovarious devices under different network conditions.</span></span> <span data-ttu-id="c374e-111">tooachieve이이 목표 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-111">tooachieve this goal do hello following:</span></span>

* <span data-ttu-id="c374e-112">프로그램 스트림 toomulti 비트 전송률 인코딩 ([적응 비트 전송률](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) 비디오 스트림 (이 하므로 품질 및 네트워크 상태) 및</span><span class="sxs-lookup"><span data-stu-id="c374e-112">encode your stream toomulti-bitrate ([adaptive bitrate](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) video stream (this will take care of quality and network conditions) and</span></span> 
* <span data-ttu-id="c374e-113">미디어 서비스를 사용 하 여 [동적 패키징](media-services-dynamic-packaging-overview.md) toodynamically 다시 패키지할 스트림을 서로 다른 프로토콜 (이 하므로 서로 다른 장치에서 스트리밍).</span><span class="sxs-lookup"><span data-stu-id="c374e-113">use Media Services [Dynamic Packaging](media-services-dynamic-packaging-overview.md) toodynamically re-package your stream into different protocols (this will take care of streaming on different devices).</span></span> <span data-ttu-id="c374e-114">미디어 서비스는 hello 적응 비트 전송률 스트리밍 기술 뒤의 배달을 지원: HTTP 라이브 스트리밍 (HLS), 부드러운 스트리밍 및 MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-114">Media Services supports delivery of hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, and MPEG DASH.</span></span> 

### <a name="manifest-files"></a><span data-ttu-id="c374e-115">매니페스트 파일</span><span class="sxs-lookup"><span data-stu-id="c374e-115">Manifest files</span></span>
<span data-ttu-id="c374e-116">적응 비트 전송률 스트리밍에 대 한 자산을 인코딩하는 경우는 **매니페스트** (재생 목록) 파일이 생성 됩니다 (hello 파일은 텍스트 기반 또는 XML 기반).</span><span class="sxs-lookup"><span data-stu-id="c374e-116">When you encode an asset for adaptive bitrate streaming, a **manifest** (playlist) file is created (hello file is text-based or XML-based).</span></span> <span data-ttu-id="c374e-117">hello **매니페스트** 와 같은 메타 데이터를 스트리밍 파일 포함: 이름, 시작 및 종료 시간, 비트 전송률 (특성), 트랙 언어, 프레젠테이션 창 (슬라이딩 윈도우 고정 기간), 비디오 추적, 형식 (오디오, 비디오 또는 텍스트)를 추적 합니다. 코덱의 (FourCC)입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-117">hello **manifest** file includes streaming metadata such as: track type (audio, video, or text), track name, start and end time, bitrate (qualities), track languages, presentation window (sliding window of fixed duration), video codec (FourCC).</span></span> <span data-ttu-id="c374e-118">또한 hello 다음 재생할 수 있는 비디오 조각을 사용할 수와 그 위치에 대 한 정보를 제공 하 여 hello 플레이어 tooretrieve hello 다음 단편을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-118">It also instructs hello player tooretrieve hello next fragment by providing information about hello next playable video fragments available and their location.</span></span> <span data-ttu-id="c374e-119">조각 또는 세그먼트는 hello 실제 "청크" 비디오 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-119">Fragments (or segments) are hello actual “chunks” of a video content.</span></span>

<span data-ttu-id="c374e-120">다음은 매니페스트 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-120">Here is an example of a manifest file:</span></span> 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a><span data-ttu-id="c374e-121">동적 매니페스트</span><span class="sxs-lookup"><span data-stu-id="c374e-121">Dynamic manifests</span></span>
<span data-ttu-id="c374e-122">[시나리오](media-services-dynamic-manifest-overview.md#scenarios) 클라이언트 hello 기본 자산 매니페스트 파일에 설명 된 것 보다 더 높은 유연성을 필요로 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c374e-122">There are [scenarios](media-services-dynamic-manifest-overview.md#scenarios) when your client needs more flexibility than what's described in hello default asset's manifest file.</span></span> <span data-ttu-id="c374e-123">예:</span><span class="sxs-lookup"><span data-stu-id="c374e-123">For example:</span></span>

* <span data-ttu-id="c374e-124">특정 장치: hello에 지정 된 변환 및/또는 지정 된만 배달 hello 장치에 사용 되는 tooplayback에서 지 원하는 언어 트랙 hello 콘텐츠 ("변환 필터링").</span><span class="sxs-lookup"><span data-stu-id="c374e-124">Device specific: deliver only hello specified renditions and\or specified language tracks that are supported by hello device that is used tooplayback hello content ("rendition filtering").</span></span> 
* <span data-ttu-id="c374e-125">Hello 매니페스트 tooshow 라이브 이벤트 ("하위 클립 필터링")의 하위 클립을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-125">Reduce hello manifest tooshow a sub-clip of a live event ("sub-clip filtering").</span></span>
* <span data-ttu-id="c374e-126">트림 hello 시작 비디오 ("트리밍 비디오")입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-126">Trim hello start of a video ("trimming a video").</span></span>
* <span data-ttu-id="c374e-127">순서 tooprovide hello 플레이어 ("프레젠테이션 창 조정")의 hello DVR 창 길이 제한에 프레젠테이션 창 (DVR)를 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-127">Adjust Presentation Window (DVR) in order tooprovide a limited length of hello DVR window in hello player ("adjusting presentation window") .</span></span>

<span data-ttu-id="c374e-128">tooachieve 유연성, 미디어 서비스 제공이 **동적 매니페스트** 기반에 미리 정의 된 [필터](media-services-dynamic-manifest-overview.md#filters)합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-128">tooachieve this flexibility, Media Services offers **Dynamic Manifests** based on pre-defined [filters](media-services-dynamic-manifest-overview.md#filters).</span></span>  <span data-ttu-id="c374e-129">Hello 필터를 정의한 다음 클라이언트 수 toostream 특정 한 변환 하거나 사용할 하위 클립 비디오.</span><span class="sxs-lookup"><span data-stu-id="c374e-129">Once you define hello filters, your clients could use them toostream a specific rendition or sub-clips of your video.</span></span> <span data-ttu-id="c374e-130">Hello 스트리밍 URL에서에서 필터를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-130">They would specify filter(s) in hello streaming URL.</span></span> <span data-ttu-id="c374e-131">필터 적용된 tooadaptive 비트 전송률 스트리밍 프로토콜에서 지 원하는 수 [동적 패키징](media-services-dynamic-packaging-overview.md): HLS, MPEG DASH, 부드러운 스트리밍 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-131">Filters could be applied tooadaptive bitrate streaming protocols supported by [Dynamic Packaging](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH, and Smooth Streaming.</span></span> <span data-ttu-id="c374e-132">예:</span><span class="sxs-lookup"><span data-stu-id="c374e-132">For example:</span></span>

<span data-ttu-id="c374e-133">필터가 있는 MPEG DASH URL</span><span class="sxs-lookup"><span data-stu-id="c374e-133">MPEG DASH URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

<span data-ttu-id="c374e-134">필터가 있는 부드러운 스트리밍 URL</span><span class="sxs-lookup"><span data-stu-id="c374e-134">Smooth Streaming URL with filter</span></span>

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


<span data-ttu-id="c374e-135">방법에 대 한 자세한 내용은 toodeliver 콘텐츠 및 스트리밍 Url을 빌드 참조 [콘텐츠 개요를 제공 하](media-services-deliver-content-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-135">For more information about how toodeliver your content and build streaming URLs, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c374e-136">동적 매니페스트 변경 hello 자산을 하는 대신 해당 자산에 대 한 기본 매니페스트 hello 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-136">Note that Dynamic Manifests do not change hello asset and hello default manifest for that asset.</span></span> <span data-ttu-id="c374e-137">클라이언트 또는 필터 없이 스트림을 toorequest를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-137">Your client can choose toorequest a stream with or without filters.</span></span> 
> 
> 

### <span data-ttu-id="c374e-138"><a id="filters"></a>필터</span><span class="sxs-lookup"><span data-stu-id="c374e-138"><a id="filters"></a>Filters</span></span>
<span data-ttu-id="c374e-139">자산 필터에는 두 가지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-139">There are two types of asset filters:</span></span> 

* <span data-ttu-id="c374e-140">전역 필터 (수 hello Azure 미디어 서비스 계정에에서 적용 된 tooany 자산 수, hello 계정의 수명은) 및</span><span class="sxs-lookup"><span data-stu-id="c374e-140">Global filters (can be applied tooany asset in hello Azure Media Services account, have a lifetime of hello account) and</span></span> 
* <span data-ttu-id="c374e-141">로컬 필터 (수만 필터는 hello로 생성 될 때 연결 되어 적용 된 tooan 자산 수, hello asset의 수명은).</span><span class="sxs-lookup"><span data-stu-id="c374e-141">Local filters (can only be applied tooan asset with which hello filter was associated upon creation, have a lifetime of hello asset).</span></span> 

<span data-ttu-id="c374e-142">전역 및 로컬 필터 형식에는 정확히 동일한 속성 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-142">Global and local filter types have exactly hello same properties.</span></span> <span data-ttu-id="c374e-143">hello 두 hello 간의 주요 차이점은 하나의 필터의 종류를 더 적합 한 시나리오에 대 한.</span><span class="sxs-lookup"><span data-stu-id="c374e-143">hello main difference between hello two is for which scenarios what type of a filer is more suitable.</span></span> <span data-ttu-id="c374e-144">전역 필터는 로컬 필터 사용된 tootrim 특정 자산을 될 수 있는 장치 프로필 (변환 필터링) 일반적으로 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-144">Global filters are generally suitable for device profiles (rendition filtering) where local filters could be used tootrim a specific asset.</span></span>

## <span data-ttu-id="c374e-145"><a id="scenarios"></a>일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="c374e-145"><a id="scenarios"></a>Common scenarios</span></span>
<span data-ttu-id="c374e-146">언급 한 대로 전에 toovarious 장치에서 다른 네트워크 상태 때 (라이브 스트리밍 이벤트 또는 주문형 비디오) 사용자 콘텐츠 toocustomers 목표를 전달 하 toodeliver 비디오 높은 품질입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-146">As was mentioned before, when delivering your content toocustomers (streaming live events or video-on-demand) your goal is toodeliver a high quality video toovarious devices under different network conditions.</span></span> <span data-ttu-id="c374e-147">또한 자산 필터링 및 **동적 매니페스트**사용과 관련된 다른 요구 사항이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-147">In addition, your might have other requirements that involve filtering your assets and using of **Dynamic Manifest**s.</span></span> <span data-ttu-id="c374e-148">다음 섹션 hello 필터링 다양 한 시나리오에 대 한 간략 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-148">hello following sections give a short overview of different filtering scenarios.</span></span>

* <span data-ttu-id="c374e-149">특정 장치 (hello 자산에 연결 된 모든 hello 변환) 하는 대신 처리할 수 있는 오디오 및 비디오 변환의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-149">Specify only a subset of audio and video renditions that certain devices can handle (instead of all hello renditions that are associated with hello asset).</span></span> 
* <span data-ttu-id="c374e-150">섹션 (hello 전체 비디오 재생) 대신 비디오를 재생 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c374e-150">Playing back only a section of a video (instead of playing hello whole video).</span></span>
* <span data-ttu-id="c374e-151">DVR 프레젠테이션 창을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-151">Adjust DVR presentation window.</span></span>

## <a name="rendition-filtering"></a><span data-ttu-id="c374e-152">변환 필터링</span><span class="sxs-lookup"><span data-stu-id="c374e-152">Rendition filtering</span></span>
<span data-ttu-id="c374e-153">자산 toomultiple 인코딩 (H.264 기본, H.264 High, AACL, AACH, Dolby Digital Plus) 프로필과 여러 품질 비트 전송률 tooencode를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-153">You may choose tooencode your asset toomultiple encoding profiles (H.264 Baseline, H.264 High, AACL, AACH, Dolby Digital Plus) and multiple quality bitrates.</span></span> <span data-ttu-id="c374e-154">그러나 모든 클라이언트 장치가 모든 자산 프로필 및 비트 전송률을 지원하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-154">However, not all client devices will support all your asset's profiles and bitrates.</span></span> <span data-ttu-id="c374e-155">예를 들어 이전 Android 장치는 H.264 Baseline+AACL만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-155">For example, older Android devices only supports H.264 Baseline+AACL.</span></span> <span data-ttu-id="c374e-156">Hello 이점을 얻을 수 있는 더 높은 비트 전송률 tooa 장치 보내기, 대역폭 및 장치 계산을 낭비입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-156">Sending higher bitrates tooa device which cannot get hello benefits, wastes bandwidth and device computation.</span></span> <span data-ttu-id="c374e-157">이러한 장치 디코딩할 해야 모든 hello tooscale만 정보를 지정한 것 아래로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-157">Such device must decode all hello given information, only tooscale it down for display.</span></span>

<span data-ttu-id="c374e-158">동적 매니페스트 사용 장치 프로필을 만들 수 있습니다 모바일, 예: HD/SD 등 콘솔 및 hello 트랙 및 품질을 포함 toobe 각 프로필의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-158">With Dynamic Manifest, you can create device profiles such as mobile, console, HD/SD, etc. and include hello tracks and qualities which you want toobe a part of each profile.</span></span>

![변환 필터링 예제][renditions2]

<span data-ttu-id="c374e-160">다음 예제는 hello, 인코더에서는 중 2 층 자산 (180 p too1080p)에서 7 개의 ISO mp4 비디오 변환에 사용 되는 tooencode를 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-160">In hello following example, an encoder was used tooencode a mezzanine asset into seven ISO MP4s video renditions (from 180p too1080p).</span></span> <span data-ttu-id="c374e-161">hello 인코딩된 자산 수 동적으로 패키지에 포함 될 hello 스트리밍 프로토콜을 다음 중 하나: HLS, 부드러운 스트리밍, 및 MPEG DASH 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-161">hello encoded asset can be dynamically packaged into any of hello following streaming protocols: HLS, Smooth, and MPEG DASH.</span></span>  <span data-ttu-id="c374e-162">HLS 자산 hello에 대 한 필터가 없는 매니페스트 hello hello 다이어그램의 hello 위에 표시 됩니다 (모든 7 변환 포함).</span><span class="sxs-lookup"><span data-stu-id="c374e-162">At hello top of hello diagram, hello HLS manifest for hello asset with no filters is shown (it contains all seven renditions).</span></span>  <span data-ttu-id="c374e-163">Hello 아래 왼쪽에 HLS 매니페스트 toowhich "ott" 라는 필터를 적용 하는 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-163">In hello bottom left, hello HLS manifest toowhich a filter named "ott" was applied is shown.</span></span> <span data-ttu-id="c374e-164">hello "ott" 필터 tooremove hello 아래쪽 두 품질 수준 hello 응답에서 제거 되어 1Mbps 아래 모든 비트 전송률을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-164">hello "ott" filter specifies tooremove all bitrates below 1Mbps, which resulted in hello bottom two quality levels being stripped off in hello response.</span></span>  <span data-ttu-id="c374e-165">Hello 오른쪽 아래 HLS hello 라는 "모바일" 필터를 적용 하는 매니페스트 toowhich 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-165">In hello bottom right,   hello HLS manifest toowhich a filter named "mobile" was applied is shown.</span></span> <span data-ttu-id="c374e-166">hello "모바일" 필터에는 여기서 hello 해상도 hello 두 1080p 변환을 제거 되어 720p 보다 큰 tooremove 변환을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-166">hello "mobile" filter specifies tooremove renditions where hello resolution is larger than 720p, which resulted in hello two 1080p renditions being stripped off.</span></span>

![변환 필터링][renditions1]

## <a name="removing-language-tracks"></a><span data-ttu-id="c374e-168">언어 트랙 제거</span><span class="sxs-lookup"><span data-stu-id="c374e-168">Removing language tracks</span></span>
<span data-ttu-id="c374e-169">자산에는 영어, 스페인어, 프랑스어 등 여러 오디오 언어가 포함될 수 있습니다. 일반적으로 hello 플레이어 SDK 관리자 기본 오디오 트랙 선택 하 고 사용자 선택 당 사용 가능한 오디오 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-169">Your assets might include multiple audio languages such as English, Spanish, French, etc. Usually, hello Player SDK managers default audio track selection and available audio tracks per user selection.</span></span> <span data-ttu-id="c374e-170">재미가 toodevelop 이러한 플레이어 Sdk 장치별 플레이어 프레임 워크에서 서로 다른 구현이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-170">It is challenging toodevelop such Player SDKs, it requires different implementations across device-specific player-frameworks.</span></span> <span data-ttu-id="c374e-171">또한 일부 플랫폼에서는 플레이어 Api 제한 되며 사용자가 선택 하거나 hello 기본 오디오 트랙을 변경할 수 없습니다 오디오 선택 기능을 넣지 마십시오. 자산 필터를 사용만 원하는 오디오 언어를 포함 하는 필터를 만들어 hello 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-171">Also, on some platforms, Player APIs are limited and do not include audio selection feature where users cannot select or change hello default audio track. With asset filters, you can control hello behavior by creating filters that only include desired audio languages.</span></span>

![언어 트랙 필터링][language_filter]

## <a name="trimming-start-of-an-asset"></a><span data-ttu-id="c374e-173">자산의 시작 부분 트리밍</span><span class="sxs-lookup"><span data-stu-id="c374e-173">Trimming start of an asset</span></span>
<span data-ttu-id="c374e-174">라이브 스트리밍 이벤트 대부분 연산자 hello 실제 이벤트 전에 일부 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-174">In most live streaming events, operators run some tests before hello actual event.</span></span> <span data-ttu-id="c374e-175">예를 들어 hello 이벤트의 hello 시작 하기 전에 다음과 같은 슬레이트 포함 될 수 있습니다 있습니다: "프로그램은 시작 일시적 으로" 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-175">For example, they might include a slate like this before hello start of hello event: "Program will begin momentarily".</span></span> <span data-ttu-id="c374e-176">Hello 프로그램을 보관 하는 경우 hello 테스트 및 슬레이트 데이터도 보관 됩니다 및 hello 프레젠테이션에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-176">If hello program is archiving, hello test and slate data are also archived and will be included in hello presentation.</span></span> <span data-ttu-id="c374e-177">그러나이 정보 표시 되지 않음을 toohello 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-177">However, this information should not be shown toohello clients.</span></span> <span data-ttu-id="c374e-178">동적 매니페스트와 시작 시간 필터를 만들고 hello 매니페스트에서 hello 원치 않는 데이터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-178">With Dynamic Manifest, you can create a start time filter and remove hello unwanted data from hello manifest.</span></span>

![트리밍 시작][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a><span data-ttu-id="c374e-180">라이브 보관에서 하위 클립(뷰) 만들기</span><span class="sxs-lookup"><span data-stu-id="c374e-180">Creating sub-clips (views) from a live archive</span></span>
<span data-ttu-id="c374e-181">많은 라이브 이벤트가 장시간 실행되며 라이브 보관에는 여러 이벤트가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-181">Many live events are long running and live archive might include multiple events.</span></span> <span data-ttu-id="c374e-182">논리 프로그램 시작에 보관 라이브 및 중지 시퀀스를 후 hello 라이브 이벤트 끝 방송국 toobreak hello 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-182">After hello live event ends broadcasters may want toobreak up hello live archive into logical program start and stop sequences.</span></span> <span data-ttu-id="c374e-183">Hello 라이브 보관을 처리 하 고 (hello Cdn에서에서 기존 캐시 된 조각은 hello의 혜택을 가져오지 것입니다)는 별도 자산을 생성 하지 않아 게시 하지 않고 이러한 가상 프로그램을 별도로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-183">Then, publish these virtual programs separately without post processing hello live archive and not creating separate assets (which will not get benefit of hello existing cached fragments in hello CDNs).</span></span> <span data-ttu-id="c374e-184">이러한 가상 프로그램 (하위 클립)의 예로 football 또는 야구 게임, 야구에 hello 이닝 hello 분기 또는 올림픽 프로그램의 오후의 개별 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-184">Examples of such virtual programs (sub-clips) are hello quarters of a football or basketball game, hello innings in baseball, or individual events of an afternoon of Olympics program.</span></span>

<span data-ttu-id="c374e-185">동적 매니페스트와 시작/종료 시간을 사용 하 여 필터를 만들 하 고 라이브 보관 hello 맨 위에 가상 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-185">With Dynamic Manifest, you can create filters using start/end times and create virtual views over hello top of your live archive.</span></span> 

![하위 클립 필터][subclip_filter]

<span data-ttu-id="c374e-187">필터링된 자산:</span><span class="sxs-lookup"><span data-stu-id="c374e-187">Filtered Asset:</span></span>

![스키][skiing]

## <a name="adjusting-presentation-window-dvr"></a><span data-ttu-id="c374e-189">프레젠테이션 창(DVR) 조정</span><span class="sxs-lookup"><span data-stu-id="c374e-189">Adjusting Presentation Window (DVR)</span></span>
<span data-ttu-id="c374e-190">현재 Azure 미디어 서비스는 5 분 사이-25 시간 hello 기간 구성할 수 있는 순환 보관 파일을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-190">Currently, Azure Media Services offers circular archive where hello duration can be configured between 5 minutes - 25 hours.</span></span> <span data-ttu-id="c374e-191">매니페스트 필터링 사용된 toocreate 롤링 DVR 창 hello 보관 미디어를 삭제 하지 않고 hello 맨 위에 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-191">Manifest filtering can be used toocreate a rolling DVR window over hello top of hello archive, without deleting media.</span></span> <span data-ttu-id="c374e-192">많은 시나리오가 있습니다 방송국 tooprovide 풀려면 라이브 가장자리와 hello에 동시 유지 큰 보관 창 hello로 이동 하는 제한 된 DVR 창.</span><span class="sxs-lookup"><span data-stu-id="c374e-192">There are many scenarios where broadcasters want tooprovide a limited DVR window which moves with hello live edge and at hello same time keep a bigger archiving window.</span></span> <span data-ttu-id="c374e-193">브로드캐스트 toouse hello 데이터 hello DVR 창 toohighlight 클립, 하지 않는 경우가 또는 he\she 다양 한 장치에 대 한 가지 DVR 창 tooprovide 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-193">A broadcaster may want toouse hello data that is out of hello DVR window toohighlight clips, or he\she may want tooprovide different DVR windows for different devices.</span></span> <span data-ttu-id="c374e-194">예를 들어 대부분의 hello 모바일 장치를 큰 DVR windows (데스크톱 클라이언트에 대 한 모바일 장치에 대 한 및 1 시간에 2 분 DVR 창 있을 수 있습니다) 처리 하지 않으며 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-194">For example, most of hello mobile devices don’t handle big DVR windows (you can have a 2 minute DVR window for mobile devices and 1 hour for desktop clients).</span></span>

![DVR 창][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a><span data-ttu-id="c374e-196">LiveBackoff(라이브 위치) 조정</span><span class="sxs-lookup"><span data-stu-id="c374e-196">Adjusting LiveBackoff (live position)</span></span>
<span data-ttu-id="c374e-197">매니페스트 필터링 될 사용된 tooremove hello 라이브 프로그램의 라이브 가장자리에서 몇 초 정도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-197">Manifest filtering can be used tooremove several seconds from hello live edge of a live program.</span></span> <span data-ttu-id="c374e-198">따라서 방송국을 toowatch hello 프레젠테이션 hello 미리 보기 게시에서 지점 및 hello 뷰어 hello 스트림 (일반적으로 백업-해제 시간을 30 초)을 받기 전에 광고 삽입 지점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-198">This allows broadcasters toowatch hello presentation on hello preview publication point and create advertisement insertion points before hello viewers receive hello stream (usually backed-off by 30 seconds).</span></span> <span data-ttu-id="c374e-199">방송국 밀어 넣을 수 있으며 이러한 광고 tootheir 클라이언트 프레임 워크에 대 한 hello 광고 기회 하기 전에 tooreceived 및 프로세스 hello 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-199">Broadcasters can then push these advertisements tootheir client frameworks in time for them tooreceived and process hello information before hello advertisement opportunity.</span></span>

<span data-ttu-id="c374e-200">또한 toohello 광고 지원, LiveBackoff 조각 404 또는 412 HTTP 오류가 발생 했습니다. 대신 서버에서 여전히 얻을 수 있습니다 클라이언트가 드리프트을 hello 라이브 가장자리에 도달할 때 수 있도록 클라이언트 라이브 다운로드 위치를 조정 하기 위해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-200">In addition toohello advertisement support, LiveBackoff can be used for adjusting client live download position so that when clients drift and hit hello live edge they can still get fragments from server instead of getting 404 or 412 HTTP errors.</span></span>

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a><span data-ttu-id="c374e-202">단일 필터에 여러 규칙 결합</span><span class="sxs-lookup"><span data-stu-id="c374e-202">Combining multiple rules in a single filter</span></span>
<span data-ttu-id="c374e-203">단일 필터에 여러 필터링 규칙을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-203">You can combine multiple filtering rules in a single filter.</span></span> <span data-ttu-id="c374e-204">예를 들어 범위 규칙 tooremove 슬레이트 라이브 보관 파일에서 정의할 수 있으며 또한 사용 가능한 비트 전송률을 필터링 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-204">As an example you can define a range rule tooremove slate from a live archive and also filter available bitrates.</span></span> <span data-ttu-id="c374e-205">여러 필터링 규칙 hello 끝에 대 한 결과 이러한 규칙의 hello 조합 (겹치는 부분에만 해당).</span><span class="sxs-lookup"><span data-stu-id="c374e-205">For multiple filtering rules hello end result is hello composition (intersection only) of these rules.</span></span>

![다중 규칙][multiple-rules]

## <a name="create-filters-programmatically"></a><span data-ttu-id="c374e-207">프로그래밍 방식으로 필터 만들기</span><span class="sxs-lookup"><span data-stu-id="c374e-207">Create filters programmatically</span></span>
<span data-ttu-id="c374e-208">hello 항목 관련된 toofilters 있는 미디어 서비스 엔터티를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-208">hello following topic discusses Media Services entities that are related toofilters.</span></span> <span data-ttu-id="c374e-209">또한 hello 항목 tooprogrammatically 필터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-209">hello topic also shows how tooprogrammatically create filters.</span></span>  

<span data-ttu-id="c374e-210">[REST API를 사용하여 필터 만들기](media-services-rest-dynamic-manifest.md)</span><span class="sxs-lookup"><span data-stu-id="c374e-210">[Create filters with REST APIs](media-services-rest-dynamic-manifest.md).</span></span>

## <a name="combining-multiple-filters-filter-composition"></a><span data-ttu-id="c374e-211">여러 개의 필터 결합(필터 컴퍼지션)</span><span class="sxs-lookup"><span data-stu-id="c374e-211">Combining multiple filters (filter composition)</span></span>
<span data-ttu-id="c374e-212">단일 URL로 여러 개의 필터를 결합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-212">You can also combine multiple filters in a single URL.</span></span> 

<span data-ttu-id="c374e-213">hello 다음 시나리오에서는 보여줍니다 toocombine 필터 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-213">hello following scenario demonstrates why you might want toocombine filters:</span></span>

1. <span data-ttu-id="c374e-214">Android 또는 순서 toolimit 비디오 품질) (방향의 iPAD와 같은 모바일 장치 toofilter 사용자 비디오 품질 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-214">You need toofilter your video qualities for mobile devices such as Android or iPAD (in order toolimit video qualities).</span></span> <span data-ttu-id="c374e-215">tooremove hello 원치 않는 품질, 장치 프로필에 대 한 적합 한 전역 필터를 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-215">tooremove hello unwanted qualities, you would create a global filter which is suitable for device profiles.</span></span> <span data-ttu-id="c374e-216">위에서 설명 했 듯이 hello에서 모든 자산에 대 한 전역 필터를 사용할 수 있습니다 같은 미디어 서비스는 더 이상 연결 하지 않고 계정.</span><span class="sxs-lookup"><span data-stu-id="c374e-216">As mentioned above, global filters can be used for all your assets under hello same media services account without any further association.</span></span> 
2. <span data-ttu-id="c374e-217">또한 tootrim hello 시작 하 고 종료 시간 자산의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-217">You also want tootrim hello start and end time of an asset.</span></span> <span data-ttu-id="c374e-218">tooachieve이를 로컬 필터를 만들고 hello 시작/종료 시간을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-218">tooachieve this, you would create a local filter and set hello start/end time.</span></span> 
3. <span data-ttu-id="c374e-219">이러한 필터의 toocombine 원하는 (하지 않으면 조합 해야 tooadd 품질 필터링 toohello 트리밍 필터는 필터 사용을 어렵게 됩니다).</span><span class="sxs-lookup"><span data-stu-id="c374e-219">You want toocombine both of these filters (without combination you would need tooadd quality filtering toohello trimming filter which will make filter usage difficult).</span></span>

<span data-ttu-id="c374e-220">tooset hello 필터 이름 toohello 매니페스트/재생 해야 toocombine 필터를 세미콜론으로 구분 된 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-220">toocombine filters, you need tooset hello filter names toohello manifest/playlist URL with semicolon delimited.</span></span> <span data-ttu-id="c374e-221">필터 이름 있다고 가정해 보겠습니다 *MyMobileDevice* 품질을 필터링 하 고 다른 이름이 있는 *MyStartTime* tooset 특정 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-221">Let’s assume you have a filter named *MyMobileDevice* that filters qualities and you have another named *MyStartTime* tooset a specific start time.</span></span> <span data-ttu-id="c374e-222">이러한 필터를 다음과 같이 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-222">You can combine them like this:</span></span>

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

<span data-ttu-id="c374e-223">Too3 필터를 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-223">You can combine up too3 filters.</span></span> 

<span data-ttu-id="c374e-224">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c374e-224">For more information see [this](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.</span></span>

## <a name="know-issues-and-limitations"></a><span data-ttu-id="c374e-225">알려진 문제 및 제한 사항</span><span class="sxs-lookup"><span data-stu-id="c374e-225">Know issues and limitations</span></span>
* <span data-ttu-id="c374e-226">동적 매니페스트는 GOP 경계(키 프레임)에서 작동하므로 트리밍에는 GOP 정확도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-226">Dynamic manifest operates in GOP boundaries (Key Frames) hence trimming has GOP accuracy.</span></span> 
* <span data-ttu-id="c374e-227">로컬 및 전역 필터에 동일한 필터 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-227">You can use same filter name for local and global filters.</span></span> <span data-ttu-id="c374e-228">로컬 필터의 우선 순위가 더 높으며 전역 필터에 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-228">Note that local filter have higher precedence and will override global filters.</span></span>
* <span data-ttu-id="c374e-229">필터를 업데이트 하는 경우 스트리밍 끝점 toorefresh hello 규칙에 대 일 분까지 걸릴 수 있으므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-229">If you update a filter, it can take up too2 minutes for streaming endpoint toorefresh hello rules.</span></span> <span data-ttu-id="c374e-230">Hello 콘텐츠 일부 필터를 사용 하 여 제공 된 (그리고 캐시 프록시 및 CDN에 캐시 된) 하는 경우 플레이어에서 오류가 발생할 수 있습니다 이러한 필터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-230">If hello content was served using some filters (and cached in proxies and CDN caches), updating these filters can result in player failures.</span></span> <span data-ttu-id="c374e-231">되기 tooclear hello 캐시 hello 필터를 업데이트 한 후 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-231">It is recommend tooclear hello cache after updating hello filter.</span></span> <span data-ttu-id="c374e-232">이 옵션을 사용할 수 없는 경우에 서로 다른 필터를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-232">If this option is not possible, consider using a different filter.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c374e-233">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="c374e-233">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c374e-234">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c374e-234">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="c374e-235">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c374e-235">See Also</span></span>
[<span data-ttu-id="c374e-236">콘텐츠 tooCustomers 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c374e-236">Delivering Content tooCustomers Overview</span></span>](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
