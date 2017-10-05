---
title: "Azure Media Services 입력 메타데이터 스키마 | Microsoft 문서"
description: "이 항목에서는 Azure Media Services 입력 메타데이터 스키마에 대한 개요를 제공합니다."
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
ms.openlocfilehash: 4787e4033e1afda6339b0b917263ecc165e400ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="input-metadata"></a><span data-ttu-id="6b2d1-103">입력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="6b2d1-103">Input Metadata</span></span>
<span data-ttu-id="6b2d1-104">인코딩 작업은 일부 인코딩 태스크를 수행할 입력 자산(또는 자산)과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-104">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span>  <span data-ttu-id="6b2d1-105">태스크가 완료되는 즉시 출력 자산이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="6b2d1-106">출력 자산에는 비디오, 오디오, 미리 보기, 매니페스트 등이 포함됩니다. 출력 자산에는 입력된 자산에 대한 메타데이터가 있는 파일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-106">The output asset contains video, audio, thumbnails, manifest, etc. The output asset also contains a file with metadata about the input asset.</span></span> <span data-ttu-id="6b2d1-107">메타데이터 XML 파일의 이름 형식은 &lt;asset_id&gt;_metadata.xml입니다(예: 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml). 여기서 &lt;asset_id&gt;는 입력 자산의 AssetId 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-107">The name of the metadata XML file has the following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is the AssetId value of the input asset.</span></span>  

<span data-ttu-id="6b2d1-108">메타데이터 파일을 검사하려는 경우 **SAS** 로케이터를 만들어 로컬 컴퓨터에 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-108">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span> <span data-ttu-id="6b2d1-109">[Media Services .NET SDK 확장을 사용](media-services-dotnet-get-started.md)하면 SAS 로케이터를 만들고 파일을 다운로드하는 방법에 대한 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-109">You can find an example on how to create a SAS locator and download a file  [Using the Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="6b2d1-110">이 항목에서는 입력 메타데이터(&lt; asset_id &gt; _metadata.xml)의 기초가 되는 XML 스키마의 요소 및 형식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-110">This topic discusses the elements and types of the XML schema on which the input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="6b2d1-111">출력 자산에 대한 메타데이터가 포함된 파일에 대한 자세한 내용은 [출력 메타데이터](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-111">For information about the file that contains metadata about the output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="6b2d1-112">[스키마 코드](media-services-input-metadata-schema.md#code) 및 [XML 예제](media-services-input-metadata-schema.md#xml)는 이 항목의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-112">You can find the [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at the end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="6b2d1-113"><a name="AssetFiles"></a> AssetFiles 요소(루트 요소)</span><span class="sxs-lookup"><span data-stu-id="6b2d1-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="6b2d1-114">인코딩 작업에 대한 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile) 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for the encoding job.</span></span>  

<span data-ttu-id="6b2d1-115">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-115">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="6b2d1-116">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-116">Name</span></span> | <span data-ttu-id="6b2d1-117">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b2d1-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="6b2d1-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="6b2d1-120">단일 자식 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-120">A single child element.</span></span> <span data-ttu-id="6b2d1-121">자세한 내용은 [AssetFile 요소](media-services-input-metadata-schema.md#AssetFile)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="6b2d1-122"><a name="AssetFile"></a> AssetFile 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="6b2d1-123">자산 파일을 설명하는 속성과 요소를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="6b2d1-124">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-124">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-125">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-125">Attributes</span></span>
| <span data-ttu-id="6b2d1-126">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-126">Name</span></span> | <span data-ttu-id="6b2d1-127">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-127">Type</span></span> | <span data-ttu-id="6b2d1-128">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-129">**Name**</span></span><br /><br /> <span data-ttu-id="6b2d1-130">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-130">Required</span></span> |<span data-ttu-id="6b2d1-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-131">**xs:string**</span></span> |<span data-ttu-id="6b2d1-132">자산 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-132">Asset file name.</span></span> |
| <span data-ttu-id="6b2d1-133">**크기**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-133">**Size**</span></span><br /><br /> <span data-ttu-id="6b2d1-134">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-134">Required</span></span> |<span data-ttu-id="6b2d1-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-135">**xs:long**</span></span> |<span data-ttu-id="6b2d1-136">자산 파일의 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="6b2d1-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-137">**Duration**</span></span><br /><br /> <span data-ttu-id="6b2d1-138">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-138">Required</span></span> |<span data-ttu-id="6b2d1-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-139">**xs:duration**</span></span> |<span data-ttu-id="6b2d1-140">콘텐츠 재생 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-140">Content play back duration.</span></span> <span data-ttu-id="6b2d1-141">예제: Duration="PT25M37.757S"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="6b2d1-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="6b2d1-143">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-143">Required</span></span> |<span data-ttu-id="6b2d1-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-144">**xs:int**</span></span> |<span data-ttu-id="6b2d1-145">자산 파일의 스트림 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-145">Number of streams in the asset file.</span></span> |
| <span data-ttu-id="6b2d1-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="6b2d1-147">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-147">Required</span></span> |<span data-ttu-id="6b2d1-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-148">**xs:string**</span></span> |<span data-ttu-id="6b2d1-149">형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-149">Format names.</span></span> |
| <span data-ttu-id="6b2d1-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="6b2d1-151">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-151">Required</span></span> |<span data-ttu-id="6b2d1-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-152">**xs:string**</span></span> |<span data-ttu-id="6b2d1-153">자세한 형식 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-153">Format verbose names.</span></span> |
| <span data-ttu-id="6b2d1-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-154">**StartTime**</span></span> |<span data-ttu-id="6b2d1-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-155">**xs:duration**</span></span> |<span data-ttu-id="6b2d1-156">콘텐츠 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-156">Content start time.</span></span> <span data-ttu-id="6b2d1-157">예제: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="6b2d1-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-158">**OverallBitRate**</span></span> |<span data-ttu-id="6b2d1-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-159">**xs:int**</span></span> |<span data-ttu-id="6b2d1-160">자산 파일의 평균 비트 전송률(Kbps)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-160">Average bitrate of the asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="6b2d1-161">다음 4개의 자식 요소가 순서대로 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-161">The following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6b2d1-162">자식 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-162">Child elements</span></span>
| <span data-ttu-id="6b2d1-163">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-163">Name</span></span> | <span data-ttu-id="6b2d1-164">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-164">Type</span></span> | <span data-ttu-id="6b2d1-165">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-166">**Programs**</span></span><br /><br /> <span data-ttu-id="6b2d1-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-167">minOccurs="0"</span></span> | |<span data-ttu-id="6b2d1-168">자산 파일의 형식이 MPEG-TS인 경우 모든 [Programs 요소](media-services-input-metadata-schema.md#Programs)의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when the asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="6b2d1-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="6b2d1-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-170">minOccurs="0"</span></span> | |<span data-ttu-id="6b2d1-171">각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6b2d1-172">이 요소에는 자산 파일의 일부인 모든 [VideoTracks 요소](media-services-input-metadata-schema.md#VideoTracks)의 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="6b2d1-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="6b2d1-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-174">minOccurs="0"</span></span> | |<span data-ttu-id="6b2d1-175">각각의 실제 자산 파일에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="6b2d1-176">이 요소에는 자산 파일의 일부인 모든 [AudioTracks 요소](media-services-input-metadata-schema.md#AudioTracks)의 컬렉션이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of the asset file.</span></span> |
| <span data-ttu-id="6b2d1-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="6b2d1-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6b2d1-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6b2d1-180">key/value 문자열로 표시되는 자산 파일의 메타데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="6b2d1-181">예:</span><span class="sxs-lookup"><span data-stu-id="6b2d1-181">For example:</span></span><br /><br /> <span data-ttu-id="6b2d1-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="6b2d1-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="6b2d1-184">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-184">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-185">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-185">Attributes</span></span>
| <span data-ttu-id="6b2d1-186">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-186">Name</span></span> | <span data-ttu-id="6b2d1-187">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-187">Type</span></span> | <span data-ttu-id="6b2d1-188">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-189">**Id**</span></span><br /><br /> <span data-ttu-id="6b2d1-190">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-190">Required</span></span> |<span data-ttu-id="6b2d1-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-191">**xs:int**</span></span> |<span data-ttu-id="6b2d1-192">이 오디오 또는 비디오 트랙의 0 기준 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="6b2d1-193">반드시 MP4 파일에 사용되는 TrackID일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-193">This is not necessarily that the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="6b2d1-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-194">**Codec**</span></span> |<span data-ttu-id="6b2d1-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-195">**xs:string**</span></span> |<span data-ttu-id="6b2d1-196">비디오 트랙 코덱 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-196">Video track codec string.</span></span> |
| <span data-ttu-id="6b2d1-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-197">**CodecLongName**</span></span> |<span data-ttu-id="6b2d1-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-198">**xs:string**</span></span> |<span data-ttu-id="6b2d1-199">오디오 또는 비디오 트랙 코덱의 긴 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="6b2d1-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="6b2d1-201">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-201">Required</span></span> |<span data-ttu-id="6b2d1-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-202">**xs:string**</span></span> |<span data-ttu-id="6b2d1-203">시간 기준입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-203">Time base.</span></span> <span data-ttu-id="6b2d1-204">예제: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="6b2d1-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-205">**NumberOfFrames**</span></span> |<span data-ttu-id="6b2d1-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-206">**xs:int**</span></span> |<span data-ttu-id="6b2d1-207">프레임 수입니다(비디오 트랙의 경우).</span><span class="sxs-lookup"><span data-stu-id="6b2d1-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="6b2d1-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-208">**StartTime**</span></span> |<span data-ttu-id="6b2d1-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-209">**xs:duration**</span></span> |<span data-ttu-id="6b2d1-210">트랙 시작 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-210">Track start time.</span></span> <span data-ttu-id="6b2d1-211">예제: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="6b2d1-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-212">**Duration**</span></span> |<span data-ttu-id="6b2d1-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-213">**xs:duration**</span></span> |<span data-ttu-id="6b2d1-214">트랙 지속 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-214">Track duration.</span></span> <span data-ttu-id="6b2d1-215">예제: Duration="PTSampleFormat M37.757S"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="6b2d1-216">다음 2개의 자식 요소가 순서대로 나타나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-216">The following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="6b2d1-217">자식 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-217">Child elements</span></span>
| <span data-ttu-id="6b2d1-218">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-218">Name</span></span> | <span data-ttu-id="6b2d1-219">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-219">Type</span></span> | <span data-ttu-id="6b2d1-220">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="6b2d1-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="6b2d1-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="6b2d1-224">프레젠테이션 정보가 포함됩니다(예: 특정 오디오 트랙이 시각 장애 시청자를 위한 것인지 여부).</span><span class="sxs-lookup"><span data-stu-id="6b2d1-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="6b2d1-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="6b2d1-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6b2d1-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="6b2d1-228">다양한 정보를 저장하는 데 사용할 수 있는 일반 key/value 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-228">Generic key/value strings that can be used to hold a variety of information.</span></span> <span data-ttu-id="6b2d1-229">예제: key=”language” 및 value=”eng”</span><span class="sxs-lookup"><span data-stu-id="6b2d1-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="6b2d1-230"><a name="AudioTrackType"></a> AudioTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="6b2d1-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="6b2d1-231">**AudioTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="6b2d1-232">형식은 자산 파일의 특정 오디오 트랙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-232">The type represents a specific audio track in the asset file.</span></span>  

 <span data-ttu-id="6b2d1-233">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-233">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-234">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-234">Attributes</span></span>
| <span data-ttu-id="6b2d1-235">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-235">Name</span></span> | <span data-ttu-id="6b2d1-236">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-236">Type</span></span> | <span data-ttu-id="6b2d1-237">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-238">**SampleFormat**</span></span> |<span data-ttu-id="6b2d1-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-239">**xs:string**</span></span> |<span data-ttu-id="6b2d1-240">샘플 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-240">Sample format.</span></span> |
| <span data-ttu-id="6b2d1-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-241">**ChannelLayout**</span></span> |<span data-ttu-id="6b2d1-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-242">**xs:string**</span></span> |<span data-ttu-id="6b2d1-243">채널 레이아웃입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-243">Channel layout.</span></span> |
| <span data-ttu-id="6b2d1-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-244">**Channels**</span></span><br /><br /> <span data-ttu-id="6b2d1-245">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-245">Required</span></span> |<span data-ttu-id="6b2d1-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-246">**xs:int**</span></span> |<span data-ttu-id="6b2d1-247">오디오 채널 수입니다(0개 이상).</span><span class="sxs-lookup"><span data-stu-id="6b2d1-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="6b2d1-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="6b2d1-249">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-249">Required</span></span> |<span data-ttu-id="6b2d1-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-250">**xs:int**</span></span> |<span data-ttu-id="6b2d1-251">오디오 샘플링 속도(샘플/초 또는 Hz)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="6b2d1-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-252">**Bitrate**</span></span> |<span data-ttu-id="6b2d1-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-253">**xs:int**</span></span> |<span data-ttu-id="6b2d1-254">자산 파일에서 계산되는 평균 오디오 비트 전송률(bps)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-254">Average audio bit rate in bits per second, as calculated from the asset file.</span></span> <span data-ttu-id="6b2d1-255">기본 스트림 페이로드만 계산되며, 패키징 오버헤드는 이 개수에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-255">Only the elementary stream payload is counted, and the packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="6b2d1-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-256">**BitsPerSample**</span></span> |<span data-ttu-id="6b2d1-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-257">**xs:int**</span></span> |<span data-ttu-id="6b2d1-258">wFormatTag 형식 샘플당 비트입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-258">Bits per sample for the wFormatTag format type.</span></span> |

## <span data-ttu-id="6b2d1-259"><a name="VideoTrackType"></a> VideoTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="6b2d1-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="6b2d1-260">**VideoTrackType**는 [TrackType](media-services-input-metadata-schema.md#TrackType)에서 상속되는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="6b2d1-261">형식은 자산 파일의 특정 비디오 트랙을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-261">The type represents a specific video track in the asset file.</span></span>  

<span data-ttu-id="6b2d1-262">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-262">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-263">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-263">Attributes</span></span>
| <span data-ttu-id="6b2d1-264">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-264">Name</span></span> | <span data-ttu-id="6b2d1-265">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-265">Type</span></span> | <span data-ttu-id="6b2d1-266">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="6b2d1-268">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-268">Required</span></span> |<span data-ttu-id="6b2d1-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-269">**xs:string**</span></span> |<span data-ttu-id="6b2d1-270">비디오 코덱 FourCC 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="6b2d1-271">**프로필**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-271">**Profile**</span></span> |<span data-ttu-id="6b2d1-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-272">**xs:string**</span></span> |<span data-ttu-id="6b2d1-273">비디오 트랙의 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-273">Video track's profile.</span></span> |
| <span data-ttu-id="6b2d1-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-274">**Level**</span></span> |<span data-ttu-id="6b2d1-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-275">**xs:string**</span></span> |<span data-ttu-id="6b2d1-276">비디오 트랙의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-276">Video track's level.</span></span> |
| <span data-ttu-id="6b2d1-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-277">**PixelFormat**</span></span> |<span data-ttu-id="6b2d1-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-278">**xs:string**</span></span> |<span data-ttu-id="6b2d1-279">비디오 트랙의 픽셀 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="6b2d1-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-280">**Width**</span></span><br /><br /> <span data-ttu-id="6b2d1-281">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-281">Required</span></span> |<span data-ttu-id="6b2d1-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-282">**xs:int**</span></span> |<span data-ttu-id="6b2d1-283">인코딩된 비디오 너비(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="6b2d1-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-284">**Height**</span></span><br /><br /> <span data-ttu-id="6b2d1-285">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-285">Required</span></span> |<span data-ttu-id="6b2d1-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-286">**xs:int**</span></span> |<span data-ttu-id="6b2d1-287">인코딩된 비디오 높이(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="6b2d1-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="6b2d1-289">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-289">Required</span></span> |<span data-ttu-id="6b2d1-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-290">**xs:double**</span></span> |<span data-ttu-id="6b2d1-291">비디오 디스플레이 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="6b2d1-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6b2d1-293">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-293">Required</span></span> |<span data-ttu-id="6b2d1-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-294">**xs:double**</span></span> |<span data-ttu-id="6b2d1-295">비디오 디스플레이 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="6b2d1-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="6b2d1-297">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-297">Required</span></span> |<span data-ttu-id="6b2d1-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-298">**xs:double**</span></span> |<span data-ttu-id="6b2d1-299">비디오 샘플 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6b2d1-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6b2d1-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-301">**xs:double**</span></span> |<span data-ttu-id="6b2d1-302">비디오 샘플 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="6b2d1-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="6b2d1-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-304">**xs:double**</span></span> |<span data-ttu-id="6b2d1-305">비디오 샘플 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="6b2d1-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="6b2d1-307">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-307">Required</span></span> |<span data-ttu-id="6b2d1-308">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-308">**xs:decimal**</span></span> |<span data-ttu-id="6b2d1-309">.3f 형식으로 측정된 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="6b2d1-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-310">**Bitrate**</span></span> |<span data-ttu-id="6b2d1-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-311">**xs:int**</span></span> |<span data-ttu-id="6b2d1-312">자산 파일에서 계산되는 평균 비디오 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-312">Average video bit rate in kilobits per second, as calculated from the asset file.</span></span> <span data-ttu-id="6b2d1-313">기본 스트림 페이로드만 계산되며, 패키징 오버헤드는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-313">Only the elementary stream payload is counted, and the packaging overhead is not included.</span></span> |
| <span data-ttu-id="6b2d1-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="6b2d1-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-315">**xs:int**</span></span> |<span data-ttu-id="6b2d1-316">이 비디오 트랙의 최대 GOP 평균 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="6b2d1-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-317">**HasBFrames**</span></span> |<span data-ttu-id="6b2d1-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-318">**xs:int**</span></span> |<span data-ttu-id="6b2d1-319">B 프레임의 비디오 트랙 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="6b2d1-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="6b2d1-321">**MetadataType**은 자산 파일의 메타데이터를 key/value 문자열로 설명하는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="6b2d1-322">예제: key=”language” 및 value=”eng”</span><span class="sxs-lookup"><span data-stu-id="6b2d1-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="6b2d1-323">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-323">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-324">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-324">Attributes</span></span>
| <span data-ttu-id="6b2d1-325">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-325">Name</span></span> | <span data-ttu-id="6b2d1-326">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-326">Type</span></span> | <span data-ttu-id="6b2d1-327">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-328">**key**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-328">**key**</span></span><br /><br /> <span data-ttu-id="6b2d1-329">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-329">Required</span></span> |<span data-ttu-id="6b2d1-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-330">**xs:string**</span></span> |<span data-ttu-id="6b2d1-331">key/value 쌍의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-331">The key in the key/value pair.</span></span> |
| <span data-ttu-id="6b2d1-332">**값**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-332">**value**</span></span><br /><br /> <span data-ttu-id="6b2d1-333">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-333">Required</span></span> |<span data-ttu-id="6b2d1-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-334">**xs:string**</span></span> |<span data-ttu-id="6b2d1-335">key/value 쌍의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-335">The value in the key/value pair.</span></span> |

## <span data-ttu-id="6b2d1-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="6b2d1-337">**ProgramType**은 프로그램을 설명하는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-338">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-338">Attributes</span></span>
| <span data-ttu-id="6b2d1-339">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-339">Name</span></span> | <span data-ttu-id="6b2d1-340">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-340">Type</span></span> | <span data-ttu-id="6b2d1-341">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="6b2d1-343">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-343">Required</span></span> |<span data-ttu-id="6b2d1-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-344">**xs:int**</span></span> |<span data-ttu-id="6b2d1-345">Program ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-345">Program Id</span></span> |
| <span data-ttu-id="6b2d1-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="6b2d1-347">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-347">Required</span></span> |<span data-ttu-id="6b2d1-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-348">**xs:int**</span></span> |<span data-ttu-id="6b2d1-349">프로그램 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-349">Number of programs.</span></span> |
| <span data-ttu-id="6b2d1-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="6b2d1-351">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-351">Required</span></span> |<span data-ttu-id="6b2d1-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-352">**xs:int**</span></span> |<span data-ttu-id="6b2d1-353">PMT(프로그램 맵 테이블)에는 프로그램에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="6b2d1-354">자세한 내용은 [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="6b2d1-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="6b2d1-356">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-356">Required</span></span> |<span data-ttu-id="6b2d1-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-357">**xs:int**</span></span> |<span data-ttu-id="6b2d1-358">디코더에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-358">Used by decoder.</span></span> <span data-ttu-id="6b2d1-359">자세한 내용은 [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="6b2d1-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-360">**StartPTS**</span></span> |<span data-ttu-id="6b2d1-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-361">**xs: long**</span></span> |<span data-ttu-id="6b2d1-362">프레젠테이션 시작 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="6b2d1-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-363">**EndPTS**</span></span> |<span data-ttu-id="6b2d1-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-364">**xs: long**</span></span> |<span data-ttu-id="6b2d1-365">프레젠테이션 끝 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="6b2d1-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="6b2d1-367">**StreamDispositionType**은 스트림을 설명하는 전역 복합 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-367">**StreamDispositionType** is a global complex type that describes the stream.</span></span>  

<span data-ttu-id="6b2d1-368">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-368">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="6b2d1-369">특성</span><span class="sxs-lookup"><span data-stu-id="6b2d1-369">Attributes</span></span>
| <span data-ttu-id="6b2d1-370">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-370">Name</span></span> | <span data-ttu-id="6b2d1-371">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-371">Type</span></span> | <span data-ttu-id="6b2d1-372">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-373">**기본값**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-373">**Default**</span></span><br /><br /> <span data-ttu-id="6b2d1-374">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-374">Required</span></span> |<span data-ttu-id="6b2d1-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-375">**xs:int**</span></span> |<span data-ttu-id="6b2d1-376">기본 프레젠테이션임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-376">Set this attribute to 1 to indicate this is the default presentation.</span></span> |
| <span data-ttu-id="6b2d1-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-377">**Dub**</span></span><br /><br /> <span data-ttu-id="6b2d1-378">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-378">Required</span></span> |<span data-ttu-id="6b2d1-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-379">**xs:int**</span></span> |<span data-ttu-id="6b2d1-380">더빙된 프레젠테이션임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-380">Set this attribute to 1 to indicate this is the dubbed presentation.</span></span> |
| <span data-ttu-id="6b2d1-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-381">**Original**</span></span><br /><br /> <span data-ttu-id="6b2d1-382">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-382">Required</span></span> |<span data-ttu-id="6b2d1-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-383">**xs:int**</span></span> |<span data-ttu-id="6b2d1-384">원본 프레젠테이션임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-384">Set this attribute to 1 to indicate this is the original presentation.</span></span> |
| <span data-ttu-id="6b2d1-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-385">**Comment**</span></span><br /><br /> <span data-ttu-id="6b2d1-386">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-386">Required</span></span> |<span data-ttu-id="6b2d1-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-387">**xs:int**</span></span> |<span data-ttu-id="6b2d1-388">이 트랙에 해설이 있음을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-388">Set this attribute to 1 to indicate this track contains commentary.</span></span> |
| <span data-ttu-id="6b2d1-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="6b2d1-390">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-390">Required</span></span> |<span data-ttu-id="6b2d1-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-391">**xs:int**</span></span> |<span data-ttu-id="6b2d1-392">이 트랙에 가사가 있음을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-392">Set this attribute to 1 to indicate this track contains lyrics.</span></span> |
| <span data-ttu-id="6b2d1-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="6b2d1-394">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-394">Required</span></span> |<span data-ttu-id="6b2d1-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-395">**xs:int**</span></span> |<span data-ttu-id="6b2d1-396">가라오케 트랙(배경 음악, 보컬 없음)임을 나타내려면 이 성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-396">Set this attribute to 1 to indicate this represents the karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="6b2d1-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-397">**Forced**</span></span><br /><br /> <span data-ttu-id="6b2d1-398">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-398">Required</span></span> |<span data-ttu-id="6b2d1-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-399">**xs:int**</span></span> |<span data-ttu-id="6b2d1-400">강제 프레젠테이션임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-400">Set this attribute to 1 to indicate this is the forced presentation.</span></span> |
| <span data-ttu-id="6b2d1-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="6b2d1-402">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-402">Required</span></span> |<span data-ttu-id="6b2d1-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-403">**xs:int**</span></span> |<span data-ttu-id="6b2d1-404">청각 장애자용 트랙임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-404">Set this attribute to 1 to indicate this track is for the hearing impaired.</span></span> |
| <span data-ttu-id="6b2d1-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="6b2d1-406">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-406">Required</span></span> |<span data-ttu-id="6b2d1-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-407">**xs:int**</span></span> |<span data-ttu-id="6b2d1-408">시각 장애자용 트랙임을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-408">Set this attribute to 1 to indicate this track is for the visually impaired.</span></span> |
| <span data-ttu-id="6b2d1-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="6b2d1-410">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-410">Required</span></span> |<span data-ttu-id="6b2d1-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-411">**xs:int**</span></span> |<span data-ttu-id="6b2d1-412">이 트랙에 새 효과가 있음을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-412">Set this attribute to 1 to indicate this track has clean effects.</span></span> |
| <span data-ttu-id="6b2d1-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="6b2d1-414">필수</span><span class="sxs-lookup"><span data-stu-id="6b2d1-414">Required</span></span> |<span data-ttu-id="6b2d1-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-415">**xs:int**</span></span> |<span data-ttu-id="6b2d1-416">이 트랙에 그림이 있음을 나타내려면 이 속성을 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-416">Set this attribute to 1 to indicate this track has pictures.</span></span> |

## <span data-ttu-id="6b2d1-417"><a name="Programs"></a> Programs 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="6b2d1-418">여러 **Program** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6b2d1-419">자식 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-419">Child elements</span></span>
| <span data-ttu-id="6b2d1-420">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-420">Name</span></span> | <span data-ttu-id="6b2d1-421">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-421">Type</span></span> | <span data-ttu-id="6b2d1-422">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-423">**Program**</span></span><br /><br /> <span data-ttu-id="6b2d1-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6b2d1-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="6b2d1-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="6b2d1-426">MPEG-TS 형식의 자산 파일에는 자산 파일의 프로그램에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-426">For asset files that are in MPEG-TS format, contains information about programs in the asset file.</span></span> |

## <span data-ttu-id="6b2d1-427"><a name="VideoTracks"></a> VideoTracks 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="6b2d1-428">여러 **VideoTrack** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="6b2d1-429">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-429">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="6b2d1-430">자식 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-430">Child elements</span></span>
| <span data-ttu-id="6b2d1-431">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-431">Name</span></span> | <span data-ttu-id="6b2d1-432">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-432">Type</span></span> | <span data-ttu-id="6b2d1-433">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="6b2d1-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6b2d1-436">VideoTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="6b2d1-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="6b2d1-437">자산 파일의 비디오 트랙에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-437">Contains information about video tracks in the asset file.</span></span> |

## <span data-ttu-id="6b2d1-438"><a name="AudioTracks"></a> AudioTracks 요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="6b2d1-439">여러 **AudioTrack** 요소를 보유하는 래퍼 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="6b2d1-440">이 항목 끝에 있는 [XML 예제](media-services-input-metadata-schema.md#xml)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-440">See an XML example at the end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="6b2d1-441">요소</span><span class="sxs-lookup"><span data-stu-id="6b2d1-441">elements</span></span>
| <span data-ttu-id="6b2d1-442">이름</span><span class="sxs-lookup"><span data-stu-id="6b2d1-442">Name</span></span> | <span data-ttu-id="6b2d1-443">형식</span><span class="sxs-lookup"><span data-stu-id="6b2d1-443">Type</span></span> | <span data-ttu-id="6b2d1-444">설명</span><span class="sxs-lookup"><span data-stu-id="6b2d1-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b2d1-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="6b2d1-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="6b2d1-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="6b2d1-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="6b2d1-447">AudioTrackType(TrackType에서 상속)</span><span class="sxs-lookup"><span data-stu-id="6b2d1-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="6b2d1-448">자산 파일의 오디오 트랙에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-448">Contains information about audio tracks in the asset file.</span></span> |

## <span data-ttu-id="6b2d1-449"><a name="code"></a> 스키마 코드</span><span class="sxs-lookup"><span data-stu-id="6b2d1-449"><a name="code"></a> Schema Code</span></span>
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
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
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
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
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
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
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
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
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
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
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
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
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
                    <xs:documentation>the media asset file name</xs:documentation>  
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
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
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


## <span data-ttu-id="6b2d1-450"><a name="xml"></a> XML 예제</span><span class="sxs-lookup"><span data-stu-id="6b2d1-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="6b2d1-451">다음은 입력 메타데이터 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="6b2d1-451">The following is an example of the Input metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="6b2d1-452">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6b2d1-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6b2d1-453">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="6b2d1-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

