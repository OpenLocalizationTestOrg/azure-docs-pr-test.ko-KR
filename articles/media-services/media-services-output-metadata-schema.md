---
title: "Azure Media Services 출력 메타데이터 스키마 | Microsoft 문서"
description: "이 항목에서는 Azure Media Services 출력 메타데이터 스키마에 대한 개요를 제공합니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: c175d359f93e7cd8cd73aa498ad8b71c4ec497f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="output-metadata"></a><span data-ttu-id="e448e-103">출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="e448e-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="e448e-104">개요</span><span class="sxs-lookup"><span data-stu-id="e448e-104">Overview</span></span>
<span data-ttu-id="e448e-105">인코딩 작업은 일부 인코딩 태스크를 수행할 입력 자산(또는 자산)과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="e448e-106">예를 들어 MP4 파일을 H.264 MP4 적응 비트 전송률 집합으로 인코딩하며, 미리 보기 이미지와 오버레이를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="e448e-107">태스크가 완료되는 즉시 출력 자산이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="e448e-108">출력 자산에는 비디오, 오디오, 미리 보기 등이 포함됩니다. 출력 자산에는 출력된 자산에 대한 메타데이터가 있는 파일도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="e448e-109">메타데이터 XML 파일의 이름은 &lt;source_file_name&gt;_manifest.xml 형식입니다(예: BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="e448e-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="e448e-110">메타데이터 파일을 검사하려는 경우 **SAS** 로케이터를 만들어 로컬 컴퓨터에 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="e448e-111">이 항목에서는 출력 메타데이터(&lt;source_file_name&gt;_manifest.xml)의 기초가 되는 XML 스키마의 요소 및 형식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="e448e-112">입력 자산에 대한 메타데이터가 포함된 파일에 대한 자세한 내용은 [입력 메타데이터](media-services-input-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="e448e-113">스키마 코드 및 XML 예제는 이 항목의 끝에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-113">You can find the complete schema code and XML example at the end of this topic.</span></span>  
>
>

## <span data-ttu-id="e448e-114"><a name="AssetFiles "></a> AssetFiles 루트 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="e448e-115">인코딩 작업에 대한 AssetFile 항목의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e448e-116">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-116">Child elements</span></span>
| <span data-ttu-id="e448e-117">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-117">Name</span></span> | <span data-ttu-id="e448e-118">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="e448e-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="e448e-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e448e-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e448e-121">AssetFiles 콜렉션의 일부인 [AssetFile 요소](media-services-output-metadata-schema.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <span data-ttu-id="e448e-122"><a name="AssetFile "></a> AssetFile 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="e448e-123">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e448e-124">특성</span><span class="sxs-lookup"><span data-stu-id="e448e-124">Attributes</span></span>
| <span data-ttu-id="e448e-125">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-125">Name</span></span> | <span data-ttu-id="e448e-126">형식</span><span class="sxs-lookup"><span data-stu-id="e448e-126">Type</span></span> | <span data-ttu-id="e448e-127">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e448e-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="e448e-128">**Name**</span></span><br/><br/> <span data-ttu-id="e448e-129">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-129">Required</span></span> |<span data-ttu-id="e448e-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-130">**xs:string**</span></span> |<span data-ttu-id="e448e-131">미디어 자산 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-131">The media asset file name.</span></span> |
| <span data-ttu-id="e448e-132">**크기**</span><span class="sxs-lookup"><span data-stu-id="e448e-132">**Size**</span></span><br/><br/> <span data-ttu-id="e448e-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-134">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-134">Required</span></span> |<span data-ttu-id="e448e-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="e448e-135">**xs:long**</span></span> |<span data-ttu-id="e448e-136">자산 파일의 크기(바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="e448e-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="e448e-137">**Duration**</span></span><br/><br/> <span data-ttu-id="e448e-138">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-138">Required</span></span> |<span data-ttu-id="e448e-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="e448e-139">**xs:duration**</span></span> |<span data-ttu-id="e448e-140">콘텐츠 재생 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="e448e-141">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-141">Child elements</span></span>
| <span data-ttu-id="e448e-142">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-142">Name</span></span> | <span data-ttu-id="e448e-143">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="e448e-144">**Sources**</span></span> |<span data-ttu-id="e448e-145">이 AssetFile을 생성하기 위해 처리된 입력/원본 미디어 파일의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="e448e-146">자세한 내용은 [Source 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="e448e-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="e448e-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="e448e-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e448e-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e448e-149">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e448e-150">이 요소는 이러한 모든 비디오 트랙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-150">This is the collection of all those video tracks.</span></span> <span data-ttu-id="e448e-151">자세한 내용은 [VideoTracks 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="e448e-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="e448e-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="e448e-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e448e-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e448e-154">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e448e-155">이 요소는 이러한 모든 오디오 트랙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-155">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="e448e-156">자세한 내용은 [AudioTracks 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="e448e-157"><a name="Sources "></a> Sources 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="e448e-158">이 AssetFile을 생성하기 위해 처리된 입력/원본 미디어 파일의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="e448e-159">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e448e-160">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-160">Child elements</span></span>
| <span data-ttu-id="e448e-161">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-161">Name</span></span> | <span data-ttu-id="e448e-162">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-163">**원본**</span><span class="sxs-lookup"><span data-stu-id="e448e-163">**Source**</span></span><br/><br/> <span data-ttu-id="e448e-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e448e-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e448e-165">이 자산을 생성할 때 사용되는 입력/원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="e448e-166">자세한 내용은 [Source 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="e448e-167"><a name="Source "></a> Source 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="e448e-168">이 자산을 생성할 때 사용되는 입력/원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="e448e-169">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e448e-170">특성</span><span class="sxs-lookup"><span data-stu-id="e448e-170">Attributes</span></span>
| <span data-ttu-id="e448e-171">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-171">Name</span></span> | <span data-ttu-id="e448e-172">형식</span><span class="sxs-lookup"><span data-stu-id="e448e-172">Type</span></span> | <span data-ttu-id="e448e-173">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e448e-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="e448e-174">**Name**</span></span><br/><br/> <span data-ttu-id="e448e-175">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-175">Required</span></span> |<span data-ttu-id="e448e-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-176">**xs:string**</span></span> |<span data-ttu-id="e448e-177">입력 원본 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-177">Input source file name.</span></span> |

## <span data-ttu-id="e448e-178"><a name="VideoTracks "></a> VideoTracks 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="e448e-179">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e448e-180">이 요소는 이러한 모든 비디오 트랙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-180">This is the collection of all those video tracks.</span></span>  

<span data-ttu-id="e448e-181">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e448e-182">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-182">Child elements</span></span>
| <span data-ttu-id="e448e-183">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-183">Name</span></span> | <span data-ttu-id="e448e-184">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="e448e-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="e448e-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e448e-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e448e-187">부모 AssetFile의 특정 비디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-187">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="e448e-188">자세한 내용은 [VideoTrack 요소](media-services-output-metadata-schema.md#VideoTrack)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="e448e-189"><a name="VideoTrack"></a> VideoTrack 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="e448e-190">부모 AssetFile의 특정 비디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-190">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="e448e-191">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e448e-192">특성</span><span class="sxs-lookup"><span data-stu-id="e448e-192">Attributes</span></span>
| <span data-ttu-id="e448e-193">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-193">Name</span></span> | <span data-ttu-id="e448e-194">형식</span><span class="sxs-lookup"><span data-stu-id="e448e-194">Type</span></span> | <span data-ttu-id="e448e-195">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e448e-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="e448e-196">**Id**</span></span><br/><br/> <span data-ttu-id="e448e-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-198">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-198">Required</span></span> |<span data-ttu-id="e448e-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-199">**xs:int**</span></span> |<span data-ttu-id="e448e-200">이 비디오 트랙의 0 기준 인덱스입니다. **참고:** 반드시 MP4 파일에 사용되는 TrackID일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="e448e-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="e448e-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="e448e-202">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-202">Required</span></span> |<span data-ttu-id="e448e-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-203">**xs:string**</span></span> |<span data-ttu-id="e448e-204">비디오 코덱 FourCC 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="e448e-205">**프로필**</span><span class="sxs-lookup"><span data-stu-id="e448e-205">**Profile**</span></span> |<span data-ttu-id="e448e-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-206">**xs:string**</span></span> |<span data-ttu-id="e448e-207">H264 프로파일입니다(H264 코덱에만 적용).</span><span class="sxs-lookup"><span data-stu-id="e448e-207">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="e448e-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="e448e-208">**Level**</span></span> |<span data-ttu-id="e448e-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-209">**xs:string**</span></span> |<span data-ttu-id="e448e-210">H264 수준입니다(H264 코덱에만 적용).</span><span class="sxs-lookup"><span data-stu-id="e448e-210">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="e448e-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="e448e-211">**Width**</span></span><br/><br/> <span data-ttu-id="e448e-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-213">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-213">Required</span></span> |<span data-ttu-id="e448e-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-214">**xs:int**</span></span> |<span data-ttu-id="e448e-215">인코딩된 비디오 너비(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="e448e-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="e448e-216">**Height**</span></span><br/><br/> <span data-ttu-id="e448e-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-218">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-218">Required</span></span> |<span data-ttu-id="e448e-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-219">**xs:int**</span></span> |<span data-ttu-id="e448e-220">인코딩된 비디오 높이(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="e448e-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="e448e-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="e448e-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-223">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-223">Required</span></span> |<span data-ttu-id="e448e-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="e448e-224">**xs:double**</span></span> |<span data-ttu-id="e448e-225">비디오 디스플레이 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="e448e-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="e448e-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="e448e-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-228">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-228">Required</span></span> |<span data-ttu-id="e448e-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="e448e-229">**xs:double**</span></span> |<span data-ttu-id="e448e-230">비디오 디스플레이 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="e448e-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="e448e-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="e448e-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-233">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-233">Required</span></span> |<span data-ttu-id="e448e-234">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="e448e-234">**xs:decimal**</span></span> |<span data-ttu-id="e448e-235">.3f 형식으로 측정된 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="e448e-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="e448e-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="e448e-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-238">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-238">Required</span></span> |<span data-ttu-id="e448e-239">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="e448e-239">**xs:decimal**</span></span> |<span data-ttu-id="e448e-240">.3f 형식으로 기본 설정된 대상 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="e448e-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="e448e-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="e448e-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-243">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-243">Required</span></span> |<span data-ttu-id="e448e-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-244">**xs:int**</span></span> |<span data-ttu-id="e448e-245">AssetFile에서 계산되는 평균 비디오 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="e448e-246">기본 스트림 페이로드만 계산되며, 패키징 오버헤드는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="e448e-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="e448e-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="e448e-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-249">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-249">Required</span></span> |<span data-ttu-id="e448e-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-250">**xs:int**</span></span> |<span data-ttu-id="e448e-251">인코딩 기본 설정을 통해 요청된 대로 이 비디오 트랙의 대상 평균 비트 전송률(Kbps)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="e448e-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="e448e-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="e448e-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-253">minInclusive ="0"</span></span> |<span data-ttu-id="e448e-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-254">**xs:int**</span></span> |<span data-ttu-id="e448e-255">이 비디오 트랙의 최대 GOP 평균 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="e448e-256"><a name="AudioTracks "></a> AudioTracks 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="e448e-257">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="e448e-258">이 요소는 이러한 모든 오디오 트랙의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-258">This is the collection of all those audio tracks.</span></span>  

<span data-ttu-id="e448e-259">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="e448e-260">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-260">Child elements</span></span>
| <span data-ttu-id="e448e-261">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-261">Name</span></span> | <span data-ttu-id="e448e-262">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="e448e-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="e448e-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="e448e-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="e448e-265">부모 AssetFile의 특정 오디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-265">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="e448e-266">자세한 내용은 [AudioTrack 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="e448e-267"><a name="AudioTrack "></a> AudioTrack 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="e448e-268">부모 AssetFile의 특정 오디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-268">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="e448e-269">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e448e-270">특성</span><span class="sxs-lookup"><span data-stu-id="e448e-270">Attributes</span></span>
| <span data-ttu-id="e448e-271">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-271">Name</span></span> | <span data-ttu-id="e448e-272">형식</span><span class="sxs-lookup"><span data-stu-id="e448e-272">Type</span></span> | <span data-ttu-id="e448e-273">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e448e-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="e448e-274">**Id**</span></span><br/><br/> <span data-ttu-id="e448e-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-276">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-276">Required</span></span> |<span data-ttu-id="e448e-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-277">**xs:int**</span></span> |<span data-ttu-id="e448e-278">이 오디오 트랙의 0 기준 인덱스입니다. **참고:** 반드시 MP4 파일에 사용되는 TrackID일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="e448e-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="e448e-279">**Codec**</span></span> |<span data-ttu-id="e448e-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-280">**xs:string**</span></span> |<span data-ttu-id="e448e-281">오디오 트랙 코덱 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-281">Audio track codec string.</span></span> |
| <span data-ttu-id="e448e-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="e448e-282">**EncoderVersion**</span></span> |<span data-ttu-id="e448e-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-283">**xs:string**</span></span> |<span data-ttu-id="e448e-284">EAC3에 필요한 선택적 인코더 버전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="e448e-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="e448e-285">**Channels**</span></span><br/><br/> <span data-ttu-id="e448e-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-287">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-287">Required</span></span> |<span data-ttu-id="e448e-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-288">**xs:int**</span></span> |<span data-ttu-id="e448e-289">오디오 채널 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-289">Number of audio channels.</span></span> |
| <span data-ttu-id="e448e-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="e448e-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="e448e-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-292">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-292">Required</span></span> |<span data-ttu-id="e448e-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-293">**xs:int**</span></span> |<span data-ttu-id="e448e-294">오디오 샘플링 속도(샘플/초 또는 Hz)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="e448e-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="e448e-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="e448e-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-297">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-297">Required</span></span> |<span data-ttu-id="e448e-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-298">**xs:int**</span></span> |<span data-ttu-id="e448e-299">AssetFile에서 계산되는 평균 오디오 비트 전송률(bps)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="e448e-300">기본 스트림 페이로드만 계산되며, 패키징 오버헤드는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="e448e-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="e448e-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="e448e-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="e448e-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="e448e-303">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-303">Required</span></span> |<span data-ttu-id="e448e-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-304">**xs:int**</span></span> |<span data-ttu-id="e448e-305">wFormatTag 형식 샘플당 비트입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-305">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="e448e-306">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-306">Child elements</span></span>
| <span data-ttu-id="e448e-307">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-307">Name</span></span> | <span data-ttu-id="e448e-308">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e448e-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="e448e-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="e448e-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="e448e-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="e448e-311">음량 측정 결과 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-311">Loudness metering result parameters.</span></span> <span data-ttu-id="e448e-312">자세한 내용은 [LoudnessMeteringResultParameters 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e448e-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="e448e-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters 요소</span><span class="sxs-lookup"><span data-stu-id="e448e-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="e448e-314">음량 측정 결과 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="e448e-315">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="e448e-316">특성</span><span class="sxs-lookup"><span data-stu-id="e448e-316">Attributes</span></span>
| <span data-ttu-id="e448e-317">이름</span><span class="sxs-lookup"><span data-stu-id="e448e-317">Name</span></span> | <span data-ttu-id="e448e-318">형식</span><span class="sxs-lookup"><span data-stu-id="e448e-318">Type</span></span> | <span data-ttu-id="e448e-319">설명</span><span class="sxs-lookup"><span data-stu-id="e448e-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e448e-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="e448e-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="e448e-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-321">**xs:string**</span></span> |<span data-ttu-id="e448e-322">**DPLM**(Dolby Professional Loudness Metering) 개발 키트 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="e448e-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="e448e-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="e448e-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="e448e-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="e448e-325">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-325">Required</span></span> |<span data-ttu-id="e448e-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="e448e-326">**xs:int**</span></span> |<span data-ttu-id="e448e-327">DPLM을 통해 생성되며, LoudnessMetering을 설정할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="e448e-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="e448e-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="e448e-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="e448e-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="e448e-330">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-330">Required</span></span> |<span data-ttu-id="e448e-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e448e-331">**xs:float**</span></span> |<span data-ttu-id="e448e-332">통합된 음량입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-332">Integrated loudness</span></span> |
| <span data-ttu-id="e448e-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="e448e-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="e448e-334">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-334">Required</span></span> |<span data-ttu-id="e448e-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-335">**xs:string**</span></span> |<span data-ttu-id="e448e-336">통합된 음량 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="e448e-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="e448e-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="e448e-338">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-338">Required</span></span> |<span data-ttu-id="e448e-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="e448e-339">**xs:string**</span></span> |<span data-ttu-id="e448e-340">게이팅 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-340">Gating identifier</span></span> |
| <span data-ttu-id="e448e-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="e448e-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="e448e-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="e448e-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="e448e-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e448e-343">**xs:float**</span></span> |<span data-ttu-id="e448e-344">프로그램을 통과하는 음성 콘텐츠(%)입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-344">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="e448e-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="e448e-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="e448e-346">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-346">Required</span></span> |<span data-ttu-id="e448e-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e448e-347">**xs:float**</span></span> |<span data-ttu-id="e448e-348">다시 설정되거나 마지막으로 지워진 이후 채널당 샘플 최대 사용 절대값입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="e448e-349">단위는 dBFS입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-349">Units are dBFS.</span></span> |
| <span data-ttu-id="e448e-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="e448e-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="e448e-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="e448e-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="e448e-352">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-352">Required</span></span> |<span data-ttu-id="e448e-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="e448e-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="e448e-354">샘플 최대 사용 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-354">Sample peak unit.</span></span> |
| <span data-ttu-id="e448e-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="e448e-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="e448e-356">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-356">Required</span></span> |<span data-ttu-id="e448e-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="e448e-357">**xs:float**</span></span> |<span data-ttu-id="e448e-358">다시 설정되거나 마지막으로 지워진 이후 채널당 실제 최대 사용 값입니다(ITU-R BS.1770-2 규격).</span><span class="sxs-lookup"><span data-stu-id="e448e-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="e448e-359">단위는 dBTP입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-359">Units are dBTP.</span></span> |
| <span data-ttu-id="e448e-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="e448e-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="e448e-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="e448e-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="e448e-362">필수</span><span class="sxs-lookup"><span data-stu-id="e448e-362">Required</span></span> |<span data-ttu-id="e448e-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="e448e-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="e448e-364">실제 최대 사용 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="e448e-365">스키마 코드</span><span class="sxs-lookup"><span data-stu-id="e448e-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="e448e-366"><a name="xml"></a> XML 예제</span><span class="sxs-lookup"><span data-stu-id="e448e-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="e448e-367">다음은 출력 메타데이터 파일의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e448e-367">The following is an example of the Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="e448e-368">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e448e-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e448e-369">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="e448e-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
