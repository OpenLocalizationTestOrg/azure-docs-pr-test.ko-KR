---
title: "미디어 서비스 입력된 메타 데이터 스키마 aaaAzure | Microsoft Docs"
description: "hello 항목에서는 Azure 미디어 서비스 입력된 메타 데이터 스키마에 대 한 개요를 제공 합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="c6b82-103">입력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="c6b82-103">Input Metadata</span></span>
<span data-ttu-id="c6b82-104">인코딩 작업은 입력된 자산 (또는 자산)와 연결 하려는 tooperform 몇 가지 인코딩 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="c6b82-105">태스크가 완료되는 즉시 출력 자산이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="c6b82-106">hello 출력 자산은 비디오, 오디오, 미리 보기, 매니페스트 포함, 등 hello 출력 자산도 hello 입력된 자산 관련 메타 데이터가 있는 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="c6b82-107">hello hello 메타 데이터 XML 파일의 이름에 형식에 따라 hello: &lt;t _ i d&gt;_ m e (예를 들어 41114ad3 eb5e-4 c-57-8 d 92-5354e2b7d4a4_metadata.xml), 여기서 &lt;t _ i d&gt; 는 hello AssetId hello 입력 자산의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="c6b82-108">Tooexamine hello 메타 데이터 파일을 원하는 경우 만들 수 있습니다는 **SAS** 로케이터 및 다운로드 hello 파일 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="c6b82-109">방법에 대 한 예제를 찾을 수 toocreate SAS 로케이터 파일을 다운로드 하 고 [hello 미디어 서비스.NET SDK Extensions를 사용 하 여](media-services-dotnet-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="c6b82-110">이 항목에서는 어떤 hello 입력된 메타 데이터가에 hello 요소 및 형식의 hello XML 스키마를 설명 (&lt;t _ i d&gt;_ m e) 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="c6b82-111">Hello 출력 자산 관련 메타 데이터가 포함 된 hello 파일에 대 한 정보를 참조 하십시오. [출력 메타 데이터](media-services-output-metadata-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="c6b82-112">Hello를 찾을 수 있습니다 [스키마 코드](media-services-input-metadata-schema.md#code) 는 [XML 예제](media-services-input-metadata-schema.md#xml) 이 항목의 hello 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="c6b82-113"><a name="AssetFiles"></a> AssetFiles 요소(루트 요소)</span><span class="sxs-lookup"><span data-stu-id="c6b82-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="c6b82-114">컬렉션을 포함 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile)hello 인코딩 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="c6b82-115">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="c6b82-116">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-116">Name</span></span> | <span data-ttu-id="c6b82-117">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6b82-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="c6b82-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="c6b82-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="c6b82-120">단일 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-120">A single child element.</span></span> <span data-ttu-id="c6b82-121">자세한 내용은 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6b82-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="c6b82-122"><a name="AssetFile"></a> AssetFile 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="c6b82-123">자산 파일을 설명하는 속성과 요소를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="c6b82-124">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-125">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-125">Attributes</span></span>
| <span data-ttu-id="c6b82-126">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-126">Name</span></span> | <span data-ttu-id="c6b82-127">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-127">Type</span></span> | <span data-ttu-id="c6b82-128">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="c6b82-129">**Name**</span></span><br /><br /> <span data-ttu-id="c6b82-130">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-130">Required</span></span> |<span data-ttu-id="c6b82-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-131">**xs:string**</span></span> |<span data-ttu-id="c6b82-132">자산 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-132">Asset file name.</span></span> |
| <span data-ttu-id="c6b82-133">**크기**</span><span class="sxs-lookup"><span data-stu-id="c6b82-133">**Size**</span></span><br /><br /> <span data-ttu-id="c6b82-134">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-134">Required</span></span> |<span data-ttu-id="c6b82-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="c6b82-135">**xs:long**</span></span> |<span data-ttu-id="c6b82-136">바이트 단위로 hello 자산 파일의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="c6b82-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-137">**Duration**</span></span><br /><br /> <span data-ttu-id="c6b82-138">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-138">Required</span></span> |<span data-ttu-id="c6b82-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-139">**xs:duration**</span></span> |<span data-ttu-id="c6b82-140">콘텐츠 재생 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-140">Content play back duration.</span></span> <span data-ttu-id="c6b82-141">예제: Duration="PT25M37.757S"</span><span class="sxs-lookup"><span data-stu-id="c6b82-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="c6b82-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="c6b82-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="c6b82-143">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-143">Required</span></span> |<span data-ttu-id="c6b82-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-144">**xs:int**</span></span> |<span data-ttu-id="c6b82-145">Hello 자산 파일의 스트림 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="c6b82-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="c6b82-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="c6b82-147">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-147">Required</span></span> |<span data-ttu-id="c6b82-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-148">**xs:string**</span></span> |<span data-ttu-id="c6b82-149">형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-149">Format names.</span></span> |
| <span data-ttu-id="c6b82-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="c6b82-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="c6b82-151">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-151">Required</span></span> |<span data-ttu-id="c6b82-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-152">**xs:string**</span></span> |<span data-ttu-id="c6b82-153">자세한 형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-153">Format verbose names.</span></span> |
| <span data-ttu-id="c6b82-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="c6b82-154">**StartTime**</span></span> |<span data-ttu-id="c6b82-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-155">**xs:duration**</span></span> |<span data-ttu-id="c6b82-156">콘텐츠 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-156">Content start time.</span></span> <span data-ttu-id="c6b82-157">예제: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="c6b82-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="c6b82-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-158">**OverallBitRate**</span></span> |<span data-ttu-id="c6b82-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-159">**xs:int**</span></span> |<span data-ttu-id="c6b82-160">Kbps에서 hello 자산 파일의 평균 비트입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="c6b82-161">다음과 같은 4 자식 요소가 hello 시퀀스에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="c6b82-162">자식 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-162">Child elements</span></span>
| <span data-ttu-id="c6b82-163">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-163">Name</span></span> | <span data-ttu-id="c6b82-164">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-164">Type</span></span> | <span data-ttu-id="c6b82-165">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="c6b82-166">**Programs**</span></span><br /><br /> <span data-ttu-id="c6b82-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="c6b82-167">minOccurs="0"</span></span> | |<span data-ttu-id="c6b82-168">모든 컬렉션 [프로그램 요소](media-services-input-metadata-schema.md#Programs) 때 hello 자산 파일이 MPEG-TS 형태로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="c6b82-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="c6b82-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="c6b82-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="c6b82-170">minOccurs="0"</span></span> | |<span data-ttu-id="c6b82-171">각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="c6b82-172">이 요소는 모든 컬렉션을 포함 [VideoTracks 요소](media-services-input-metadata-schema.md#VideoTracks) hello 자산 파일의 일부인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="c6b82-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="c6b82-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="c6b82-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="c6b82-174">minOccurs="0"</span></span> | |<span data-ttu-id="c6b82-175">각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="c6b82-176">이 요소는 모든 컬렉션을 포함 [AudioTracks 요소](media-services-input-metadata-schema.md#AudioTracks) hello 자산 파일의 일부인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="c6b82-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="c6b82-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="c6b82-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="c6b82-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="c6b82-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="c6b82-180">key/value 문자열로 표시되는 자산 파일의 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="c6b82-181">예:</span><span class="sxs-lookup"><span data-stu-id="c6b82-181">For example:</span></span><br /><br /> <span data-ttu-id="c6b82-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="c6b82-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="c6b82-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="c6b82-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="c6b82-184">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-185">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-185">Attributes</span></span>
| <span data-ttu-id="c6b82-186">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-186">Name</span></span> | <span data-ttu-id="c6b82-187">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-187">Type</span></span> | <span data-ttu-id="c6b82-188">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="c6b82-189">**Id**</span></span><br /><br /> <span data-ttu-id="c6b82-190">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-190">Required</span></span> |<span data-ttu-id="c6b82-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-191">**xs:int**</span></span> |<span data-ttu-id="c6b82-192">이 오디오 또는 비디오 트랙의 0 기준 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="c6b82-193">이 아닌 경우 반드시 해당 hello MP4 파일에서 사용 되는 TrackID</span><span class="sxs-lookup"><span data-stu-id="c6b82-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="c6b82-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="c6b82-194">**Codec**</span></span> |<span data-ttu-id="c6b82-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-195">**xs:string**</span></span> |<span data-ttu-id="c6b82-196">비디오 트랙 코덱 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-196">Video track codec string.</span></span> |
| <span data-ttu-id="c6b82-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="c6b82-197">**CodecLongName**</span></span> |<span data-ttu-id="c6b82-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-198">**xs:string**</span></span> |<span data-ttu-id="c6b82-199">오디오 또는 비디오 트랙 코덱의 긴 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="c6b82-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="c6b82-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="c6b82-201">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-201">Required</span></span> |<span data-ttu-id="c6b82-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-202">**xs:string**</span></span> |<span data-ttu-id="c6b82-203">시간 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-203">Time base.</span></span> <span data-ttu-id="c6b82-204">예제: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="c6b82-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="c6b82-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="c6b82-205">**NumberOfFrames**</span></span> |<span data-ttu-id="c6b82-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-206">**xs:int**</span></span> |<span data-ttu-id="c6b82-207">프레임 수입니다(비디오 트랙의 경우).</span><span class="sxs-lookup"><span data-stu-id="c6b82-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="c6b82-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="c6b82-208">**StartTime**</span></span> |<span data-ttu-id="c6b82-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-209">**xs:duration**</span></span> |<span data-ttu-id="c6b82-210">트랙 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-210">Track start time.</span></span> <span data-ttu-id="c6b82-211">예제: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="c6b82-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="c6b82-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-212">**Duration**</span></span> |<span data-ttu-id="c6b82-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="c6b82-213">**xs:duration**</span></span> |<span data-ttu-id="c6b82-214">트랙 지속 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-214">Track duration.</span></span> <span data-ttu-id="c6b82-215">예제: Duration="PTSampleFormat M37.757S"</span><span class="sxs-lookup"><span data-stu-id="c6b82-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="c6b82-216">다음과 같은 2 자식 요소가 hello 시퀀스에 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="c6b82-217">자식 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-217">Child elements</span></span>
| <span data-ttu-id="c6b82-218">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-218">Name</span></span> | <span data-ttu-id="c6b82-219">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-219">Type</span></span> | <span data-ttu-id="c6b82-220">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="c6b82-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="c6b82-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="c6b82-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="c6b82-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="c6b82-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="c6b82-224">프레젠테이션 정보가 포함됩니다(예: 특정 오디오 트랙이 시각 장애 시청자를 위한 것인지 여부).</span><span class="sxs-lookup"><span data-stu-id="c6b82-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="c6b82-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="c6b82-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="c6b82-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="c6b82-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="c6b82-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="c6b82-228">사용 되는 toohold 다양 한 일 수 있는 일반 키/값 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="c6b82-229">예제: key=”language” 및 value=”eng”</span><span class="sxs-lookup"><span data-stu-id="c6b82-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="c6b82-230"><a name="AudioTrackType"></a> AudioTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="c6b82-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="c6b82-231">**AudioTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="c6b82-232">hello 형식은 hello 자산 파일의 특정 오디오 트랙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="c6b82-233">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-234">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-234">Attributes</span></span>
| <span data-ttu-id="c6b82-235">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-235">Name</span></span> | <span data-ttu-id="c6b82-236">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-236">Type</span></span> | <span data-ttu-id="c6b82-237">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="c6b82-238">**SampleFormat**</span></span> |<span data-ttu-id="c6b82-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-239">**xs:string**</span></span> |<span data-ttu-id="c6b82-240">샘플 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-240">Sample format.</span></span> |
| <span data-ttu-id="c6b82-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="c6b82-241">**ChannelLayout**</span></span> |<span data-ttu-id="c6b82-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-242">**xs:string**</span></span> |<span data-ttu-id="c6b82-243">채널 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-243">Channel layout.</span></span> |
| <span data-ttu-id="c6b82-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="c6b82-244">**Channels**</span></span><br /><br /> <span data-ttu-id="c6b82-245">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-245">Required</span></span> |<span data-ttu-id="c6b82-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-246">**xs:int**</span></span> |<span data-ttu-id="c6b82-247">오디오 채널 수입니다(0개 이상).</span><span class="sxs-lookup"><span data-stu-id="c6b82-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="c6b82-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="c6b82-249">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-249">Required</span></span> |<span data-ttu-id="c6b82-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-250">**xs:int**</span></span> |<span data-ttu-id="c6b82-251">오디오 샘플링 속도(샘플/초 또는 Hz)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="c6b82-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-252">**Bitrate**</span></span> |<span data-ttu-id="c6b82-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-253">**xs:int**</span></span> |<span data-ttu-id="c6b82-254">Hello 자산 파일에서 계산 되는 초당 비트 단위의 평균 오디오 비트 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="c6b82-255">Hello 기본 스트림 페이로드만 계산 되며 및 hello 패키징 오버 헤드는이 개수에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="c6b82-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="c6b82-256">**BitsPerSample**</span></span> |<span data-ttu-id="c6b82-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-257">**xs:int**</span></span> |<span data-ttu-id="c6b82-258">Hello wFormatTag 형식에 대 한 샘플당 비트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="c6b82-259"><a name="VideoTrackType"></a> VideoTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="c6b82-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="c6b82-260">**VideoTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="c6b82-261">hello 형식은 hello 자산 파일의 특정 비디오 트랙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="c6b82-262">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-263">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-263">Attributes</span></span>
| <span data-ttu-id="c6b82-264">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-264">Name</span></span> | <span data-ttu-id="c6b82-265">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-265">Type</span></span> | <span data-ttu-id="c6b82-266">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="c6b82-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="c6b82-268">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-268">Required</span></span> |<span data-ttu-id="c6b82-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-269">**xs:string**</span></span> |<span data-ttu-id="c6b82-270">비디오 코덱 FourCC 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="c6b82-271">**프로필**</span><span class="sxs-lookup"><span data-stu-id="c6b82-271">**Profile**</span></span> |<span data-ttu-id="c6b82-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-272">**xs:string**</span></span> |<span data-ttu-id="c6b82-273">비디오 트랙의 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-273">Video track's profile.</span></span> |
| <span data-ttu-id="c6b82-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="c6b82-274">**Level**</span></span> |<span data-ttu-id="c6b82-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-275">**xs:string**</span></span> |<span data-ttu-id="c6b82-276">비디오 트랙의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-276">Video track's level.</span></span> |
| <span data-ttu-id="c6b82-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="c6b82-277">**PixelFormat**</span></span> |<span data-ttu-id="c6b82-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-278">**xs:string**</span></span> |<span data-ttu-id="c6b82-279">비디오 트랙의 픽셀 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="c6b82-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="c6b82-280">**Width**</span></span><br /><br /> <span data-ttu-id="c6b82-281">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-281">Required</span></span> |<span data-ttu-id="c6b82-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-282">**xs:int**</span></span> |<span data-ttu-id="c6b82-283">인코딩된 비디오 너비(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="c6b82-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="c6b82-284">**Height**</span></span><br /><br /> <span data-ttu-id="c6b82-285">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-285">Required</span></span> |<span data-ttu-id="c6b82-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-286">**xs:int**</span></span> |<span data-ttu-id="c6b82-287">인코딩된 비디오 높이(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="c6b82-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="c6b82-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="c6b82-289">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-289">Required</span></span> |<span data-ttu-id="c6b82-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="c6b82-290">**xs:double**</span></span> |<span data-ttu-id="c6b82-291">비디오 디스플레이 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="c6b82-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="c6b82-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="c6b82-293">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-293">Required</span></span> |<span data-ttu-id="c6b82-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="c6b82-294">**xs:double**</span></span> |<span data-ttu-id="c6b82-295">비디오 디스플레이 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="c6b82-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="c6b82-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="c6b82-297">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-297">Required</span></span> |<span data-ttu-id="c6b82-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="c6b82-298">**xs:double**</span></span> |<span data-ttu-id="c6b82-299">비디오 샘플 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="c6b82-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="c6b82-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="c6b82-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="c6b82-301">**xs:double**</span></span> |<span data-ttu-id="c6b82-302">비디오 샘플 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="c6b82-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="c6b82-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="c6b82-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="c6b82-304">**xs:double**</span></span> |<span data-ttu-id="c6b82-305">비디오 샘플 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="c6b82-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="c6b82-307">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-307">Required</span></span> |<span data-ttu-id="c6b82-308">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="c6b82-308">**xs:decimal**</span></span> |<span data-ttu-id="c6b82-309">.3f 형식으로 측정된 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="c6b82-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-310">**Bitrate**</span></span> |<span data-ttu-id="c6b82-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-311">**xs:int**</span></span> |<span data-ttu-id="c6b82-312">Hello 자산 파일에서 계산 된 대로 k b / 초, 평균 비디오 비트 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="c6b82-313">Hello 기본 스트림 페이로드만 계산 되며 및 hello 패키징 오버 헤드는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="c6b82-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="c6b82-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="c6b82-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-315">**xs:int**</span></span> |<span data-ttu-id="c6b82-316">이 비디오 트랙의 최대 GOP 평균 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="c6b82-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="c6b82-317">**HasBFrames**</span></span> |<span data-ttu-id="c6b82-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-318">**xs:int**</span></span> |<span data-ttu-id="c6b82-319">B 프레임의 비디오 트랙 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="c6b82-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="c6b82-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="c6b82-321">**MetadataType**은 자산 파일의 메타데이터를 key/value 문자열로 설명하는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="c6b82-322">예제: key=”language” 및 value=”eng”</span><span class="sxs-lookup"><span data-stu-id="c6b82-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="c6b82-323">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-324">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-324">Attributes</span></span>
| <span data-ttu-id="c6b82-325">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-325">Name</span></span> | <span data-ttu-id="c6b82-326">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-326">Type</span></span> | <span data-ttu-id="c6b82-327">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-328">**key**</span><span class="sxs-lookup"><span data-stu-id="c6b82-328">**key**</span></span><br /><br /> <span data-ttu-id="c6b82-329">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-329">Required</span></span> |<span data-ttu-id="c6b82-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-330">**xs:string**</span></span> |<span data-ttu-id="c6b82-331">hello 키/값 쌍의 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="c6b82-332">**값**</span><span class="sxs-lookup"><span data-stu-id="c6b82-332">**value**</span></span><br /><br /> <span data-ttu-id="c6b82-333">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-333">Required</span></span> |<span data-ttu-id="c6b82-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="c6b82-334">**xs:string**</span></span> |<span data-ttu-id="c6b82-335">hello 키/값 쌍의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="c6b82-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="c6b82-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="c6b82-337">**ProgramType**은 프로그램을 설명하는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-338">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-338">Attributes</span></span>
| <span data-ttu-id="c6b82-339">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-339">Name</span></span> | <span data-ttu-id="c6b82-340">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-340">Type</span></span> | <span data-ttu-id="c6b82-341">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="c6b82-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="c6b82-343">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-343">Required</span></span> |<span data-ttu-id="c6b82-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-344">**xs:int**</span></span> |<span data-ttu-id="c6b82-345">Program ID입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-345">Program Id</span></span> |
| <span data-ttu-id="c6b82-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="c6b82-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="c6b82-347">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-347">Required</span></span> |<span data-ttu-id="c6b82-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-348">**xs:int**</span></span> |<span data-ttu-id="c6b82-349">프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-349">Number of programs.</span></span> |
| <span data-ttu-id="c6b82-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="c6b82-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="c6b82-351">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-351">Required</span></span> |<span data-ttu-id="c6b82-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-352">**xs:int**</span></span> |<span data-ttu-id="c6b82-353">PMT(프로그램 맵 테이블)에는 프로그램에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="c6b82-354">자세한 내용은 [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6b82-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="c6b82-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="c6b82-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="c6b82-356">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-356">Required</span></span> |<span data-ttu-id="c6b82-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-357">**xs:int**</span></span> |<span data-ttu-id="c6b82-358">디코더에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-358">Used by decoder.</span></span> <span data-ttu-id="c6b82-359">자세한 내용은 [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6b82-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="c6b82-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="c6b82-360">**StartPTS**</span></span> |<span data-ttu-id="c6b82-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="c6b82-361">**xs: long**</span></span> |<span data-ttu-id="c6b82-362">프레젠테이션 시작 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="c6b82-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="c6b82-363">**EndPTS**</span></span> |<span data-ttu-id="c6b82-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="c6b82-364">**xs: long**</span></span> |<span data-ttu-id="c6b82-365">프레젠테이션 끝 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="c6b82-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="c6b82-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="c6b82-367">**StreamDispositionType** 는 hello 스트림을 설명 하는 전역 복합 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="c6b82-368">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="c6b82-369">특성</span><span class="sxs-lookup"><span data-stu-id="c6b82-369">Attributes</span></span>
| <span data-ttu-id="c6b82-370">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-370">Name</span></span> | <span data-ttu-id="c6b82-371">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-371">Type</span></span> | <span data-ttu-id="c6b82-372">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-373">**기본값**</span><span class="sxs-lookup"><span data-stu-id="c6b82-373">**Default**</span></span><br /><br /> <span data-ttu-id="c6b82-374">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-374">Required</span></span> |<span data-ttu-id="c6b82-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-375">**xs:int**</span></span> |<span data-ttu-id="c6b82-376">이이 특성 too1 tooindicate hello 기본 표시가 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="c6b82-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="c6b82-377">**Dub**</span></span><br /><br /> <span data-ttu-id="c6b82-378">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-378">Required</span></span> |<span data-ttu-id="c6b82-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-379">**xs:int**</span></span> |<span data-ttu-id="c6b82-380">설정 합니다.이 특성 too1 tooindicate 프레젠테이션 더빙 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="c6b82-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="c6b82-381">**Original**</span></span><br /><br /> <span data-ttu-id="c6b82-382">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-382">Required</span></span> |<span data-ttu-id="c6b82-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-383">**xs:int**</span></span> |<span data-ttu-id="c6b82-384">이이 특성 too1 tooindicate hello 원본 표시를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="c6b82-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="c6b82-385">**Comment**</span></span><br /><br /> <span data-ttu-id="c6b82-386">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-386">Required</span></span> |<span data-ttu-id="c6b82-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-387">**xs:int**</span></span> |<span data-ttu-id="c6b82-388">설정 합니다.이 특성 too1 tooindicate 트랙에 설명이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="c6b82-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="c6b82-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="c6b82-390">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-390">Required</span></span> |<span data-ttu-id="c6b82-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-391">**xs:int**</span></span> |<span data-ttu-id="c6b82-392">설정 합니다.이 특성 too1 tooindicate 트랙에 가사가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="c6b82-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="c6b82-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="c6b82-394">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-394">Required</span></span> |<span data-ttu-id="c6b82-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-395">**xs:int**</span></span> |<span data-ttu-id="c6b82-396">설정 합니다.이 특성 too1 tooindicate 나타냅니다 hello이 항목이 가라오케 트랙 (배경 음악, 보컬 없음).</span><span class="sxs-lookup"><span data-stu-id="c6b82-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="c6b82-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="c6b82-397">**Forced**</span></span><br /><br /> <span data-ttu-id="c6b82-398">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-398">Required</span></span> |<span data-ttu-id="c6b82-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-399">**xs:int**</span></span> |<span data-ttu-id="c6b82-400">이이 특성 too1 tooindicate 강제 hello 프레젠테이션을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="c6b82-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="c6b82-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="c6b82-402">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-402">Required</span></span> |<span data-ttu-id="c6b82-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-403">**xs:int**</span></span> |<span data-ttu-id="c6b82-404">이 특성 too1 tooindicate hello 항목이 청각 장애 자용 임을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="c6b82-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="c6b82-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="c6b82-406">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-406">Required</span></span> |<span data-ttu-id="c6b82-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-407">**xs:int**</span></span> |<span data-ttu-id="c6b82-408">이 트랙은 시각 장애가 있는 hello에 대 한이 특성 too1 tooindicate를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="c6b82-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="c6b82-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="c6b82-410">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-410">Required</span></span> |<span data-ttu-id="c6b82-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-411">**xs:int**</span></span> |<span data-ttu-id="c6b82-412">이 트랙에이 특성 too1 tooindicate 클린 효과 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="c6b82-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="c6b82-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="c6b82-414">필수</span><span class="sxs-lookup"><span data-stu-id="c6b82-414">Required</span></span> |<span data-ttu-id="c6b82-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="c6b82-415">**xs:int**</span></span> |<span data-ttu-id="c6b82-416">이 트랙에이 특성 too1 tooindicate 그림을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="c6b82-417"><a name="Programs"></a> Programs 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="c6b82-418">여러 **Program** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="c6b82-419">자식 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-419">Child elements</span></span>
| <span data-ttu-id="c6b82-420">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-420">Name</span></span> | <span data-ttu-id="c6b82-421">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-421">Type</span></span> | <span data-ttu-id="c6b82-422">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="c6b82-423">**Program**</span></span><br /><br /> <span data-ttu-id="c6b82-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="c6b82-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="c6b82-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="c6b82-426">MPEG-TS 형식인 자산 파일에 대 한 hello 자산 파일의 프로그램에 대 한 정보를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="c6b82-427"><a name="VideoTracks"></a> VideoTracks 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="c6b82-428">여러 **VideoTrack** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="c6b82-429">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="c6b82-430">자식 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-430">Child elements</span></span>
| <span data-ttu-id="c6b82-431">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-431">Name</span></span> | <span data-ttu-id="c6b82-432">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-432">Type</span></span> | <span data-ttu-id="c6b82-433">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="c6b82-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="c6b82-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="c6b82-436">VideoTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="c6b82-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="c6b82-437">Hello 자산 파일의 비디오 트랙에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="c6b82-438"><a name="AudioTracks"></a> AudioTracks 요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="c6b82-439">여러 **AudioTrack** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="c6b82-440">이 항목의 hello 끝에 XML 예제: [XML 예제](media-services-input-metadata-schema.md#xml)합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="c6b82-441">요소</span><span class="sxs-lookup"><span data-stu-id="c6b82-441">elements</span></span>
| <span data-ttu-id="c6b82-442">이름</span><span class="sxs-lookup"><span data-stu-id="c6b82-442">Name</span></span> | <span data-ttu-id="c6b82-443">형식</span><span class="sxs-lookup"><span data-stu-id="c6b82-443">Type</span></span> | <span data-ttu-id="c6b82-444">설명</span><span class="sxs-lookup"><span data-stu-id="c6b82-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6b82-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="c6b82-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="c6b82-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="c6b82-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="c6b82-447">AudioTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="c6b82-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="c6b82-448">Hello 자산 파일의 오디오 트랙에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="c6b82-449"><a name="code"></a> 스키마 코드</span><span class="sxs-lookup"><span data-stu-id="c6b82-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="c6b82-450"><a name="xml"></a> XML 예제</span><span class="sxs-lookup"><span data-stu-id="c6b82-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="c6b82-451">hello 다음은 hello 입력 메타 데이터 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c6b82-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="c6b82-452">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6b82-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6b82-453">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="c6b82-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

