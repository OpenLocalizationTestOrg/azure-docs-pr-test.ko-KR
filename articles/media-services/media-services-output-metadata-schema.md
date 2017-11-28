---
title: "미디어 서비스 출력 메타 데이터 스키마 aaaAzure | Microsoft Docs"
description: "hello 항목에서는 Azure 미디어 서비스 출력 메타 데이터 스키마에 대 한 개요를 제공 합니다."
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
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="12143-103">출력 메타데이터</span><span class="sxs-lookup"><span data-stu-id="12143-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="12143-104">개요</span><span class="sxs-lookup"><span data-stu-id="12143-104">Overview</span></span>
<span data-ttu-id="12143-105">인코딩 작업은 입력된 자산 (또는 자산)와 연결 하려는 tooperform 몇 가지 인코딩 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="12143-106">예를 들어, MP4 파일 tooH.264 MP4 적응 비트 전송률 인코딩 설정; 미리 보기 만들기 오버레이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="12143-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="12143-107">태스크가 완료되는 즉시 출력 자산이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="12143-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="12143-108">hello 출력 자산은 비디오, 오디오, 미리 보기 포함, 등 hello 출력 자산도 hello 출력 자산에 대 한 메타 데이터와 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="12143-109">hello hello 메타 데이터 XML 파일의 이름에 형식에 따라 hello: &lt;source_file_name&gt;_manifest.xml (예: BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="12143-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="12143-110">Tooexamine hello 메타 데이터 파일을 원하는 경우 만들 수 있습니다는 **SAS** 로케이터 및 다운로드 hello 파일 tooyour 로컬 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="12143-111">이 항목에서는 hello 요소 및 hello XML 스키마 형식의 hello 출력 메타 데이터가 있는에 설명 (&lt;source_file_name&gt;_manifest.xml) 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="12143-112">Hello 입력된 자산 관련 메타 데이터가 포함 된 hello 파일에 대 한 정보를 참조 하십시오. [입력 메타 데이터](media-services-input-metadata-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="12143-113">Hello 완전 한 스키마 코드 및이 항목의 hello 끝에 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="12143-114"><a name="AssetFiles "></a> AssetFiles 루트 요소</span><span class="sxs-lookup"><span data-stu-id="12143-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="12143-115">Hello 인코딩 작업의 AssetFile 항목의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="12143-116">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-116">Child elements</span></span>
| <span data-ttu-id="12143-117">이름</span><span class="sxs-lookup"><span data-stu-id="12143-117">Name</span></span> | <span data-ttu-id="12143-118">설명</span><span class="sxs-lookup"><span data-stu-id="12143-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="12143-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="12143-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="12143-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="12143-121">[AssetFile 요소](media-services-output-metadata-schema.md) hello AssetFiles 컬렉션의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="12143-122"><a name="AssetFile "></a> AssetFile 요소</span><span class="sxs-lookup"><span data-stu-id="12143-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="12143-123">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="12143-124">특성</span><span class="sxs-lookup"><span data-stu-id="12143-124">Attributes</span></span>
| <span data-ttu-id="12143-125">이름</span><span class="sxs-lookup"><span data-stu-id="12143-125">Name</span></span> | <span data-ttu-id="12143-126">형식</span><span class="sxs-lookup"><span data-stu-id="12143-126">Type</span></span> | <span data-ttu-id="12143-127">설명</span><span class="sxs-lookup"><span data-stu-id="12143-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12143-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="12143-128">**Name**</span></span><br/><br/> <span data-ttu-id="12143-129">필수</span><span class="sxs-lookup"><span data-stu-id="12143-129">Required</span></span> |<span data-ttu-id="12143-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-130">**xs:string**</span></span> |<span data-ttu-id="12143-131">hello 미디어 자산 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-131">hello media asset file name.</span></span> |
| <span data-ttu-id="12143-132">**크기**</span><span class="sxs-lookup"><span data-stu-id="12143-132">**Size**</span></span><br/><br/> <span data-ttu-id="12143-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-134">필수</span><span class="sxs-lookup"><span data-stu-id="12143-134">Required</span></span> |<span data-ttu-id="12143-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="12143-135">**xs:long**</span></span> |<span data-ttu-id="12143-136">바이트 단위로 hello 자산 파일의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="12143-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="12143-137">**Duration**</span></span><br/><br/> <span data-ttu-id="12143-138">필수</span><span class="sxs-lookup"><span data-stu-id="12143-138">Required</span></span> |<span data-ttu-id="12143-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="12143-139">**xs:duration**</span></span> |<span data-ttu-id="12143-140">콘텐츠 재생 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="12143-141">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-141">Child elements</span></span>
| <span data-ttu-id="12143-142">이름</span><span class="sxs-lookup"><span data-stu-id="12143-142">Name</span></span> | <span data-ttu-id="12143-143">설명</span><span class="sxs-lookup"><span data-stu-id="12143-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="12143-144">**Sources**</span></span> |<span data-ttu-id="12143-145">입력/원본 미디어 파일의 처리 된 컬렉션의 순서로 tooproduce이이 AssetFile 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="12143-146">자세한 내용은 [Source 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="12143-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="12143-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="12143-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="12143-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="12143-149">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="12143-150">모든 비디오 트랙의 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="12143-151">자세한 내용은 [VideoTracks 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="12143-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="12143-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="12143-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="12143-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="12143-154">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="12143-155">모든 오디오 트랙의 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="12143-156">자세한 내용은 [AudioTracks 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="12143-157"><a name="Sources "></a> Sources 요소</span><span class="sxs-lookup"><span data-stu-id="12143-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="12143-158">입력/원본 미디어 파일의 처리 된 컬렉션의 순서로 tooproduce이이 AssetFile 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="12143-159">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="12143-160">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-160">Child elements</span></span>
| <span data-ttu-id="12143-161">이름</span><span class="sxs-lookup"><span data-stu-id="12143-161">Name</span></span> | <span data-ttu-id="12143-162">설명</span><span class="sxs-lookup"><span data-stu-id="12143-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-163">**원본**</span><span class="sxs-lookup"><span data-stu-id="12143-163">**Source**</span></span><br/><br/> <span data-ttu-id="12143-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="12143-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="12143-165">이 자산을 생성할 때 사용되는 입력/원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="12143-166">자세한 내용은 [Source 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="12143-167"><a name="Source "></a> Source 요소</span><span class="sxs-lookup"><span data-stu-id="12143-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="12143-168">이 자산을 생성할 때 사용되는 입력/원본 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="12143-169">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="12143-170">특성</span><span class="sxs-lookup"><span data-stu-id="12143-170">Attributes</span></span>
| <span data-ttu-id="12143-171">이름</span><span class="sxs-lookup"><span data-stu-id="12143-171">Name</span></span> | <span data-ttu-id="12143-172">형식</span><span class="sxs-lookup"><span data-stu-id="12143-172">Type</span></span> | <span data-ttu-id="12143-173">설명</span><span class="sxs-lookup"><span data-stu-id="12143-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12143-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="12143-174">**Name**</span></span><br/><br/> <span data-ttu-id="12143-175">필수</span><span class="sxs-lookup"><span data-stu-id="12143-175">Required</span></span> |<span data-ttu-id="12143-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-176">**xs:string**</span></span> |<span data-ttu-id="12143-177">입력 원본 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-177">Input source file name.</span></span> |

## <span data-ttu-id="12143-178"><a name="VideoTracks "></a> VideoTracks 요소</span><span class="sxs-lookup"><span data-stu-id="12143-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="12143-179">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 비디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="12143-180">모든 비디오 트랙의 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="12143-181">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="12143-182">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-182">Child elements</span></span>
| <span data-ttu-id="12143-183">이름</span><span class="sxs-lookup"><span data-stu-id="12143-183">Name</span></span> | <span data-ttu-id="12143-184">설명</span><span class="sxs-lookup"><span data-stu-id="12143-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="12143-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="12143-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="12143-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="12143-187">Hello 부모 AssetFile의에서 특정 비디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="12143-188">자세한 내용은 [VideoTrack 요소](media-services-output-metadata-schema.md#VideoTrack)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="12143-189"><a name="VideoTrack"></a> VideoTrack 요소</span><span class="sxs-lookup"><span data-stu-id="12143-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="12143-190">Hello 부모 AssetFile의에서 특정 비디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="12143-191">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="12143-192">특성</span><span class="sxs-lookup"><span data-stu-id="12143-192">Attributes</span></span>
| <span data-ttu-id="12143-193">이름</span><span class="sxs-lookup"><span data-stu-id="12143-193">Name</span></span> | <span data-ttu-id="12143-194">형식</span><span class="sxs-lookup"><span data-stu-id="12143-194">Type</span></span> | <span data-ttu-id="12143-195">설명</span><span class="sxs-lookup"><span data-stu-id="12143-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12143-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="12143-196">**Id**</span></span><br/><br/> <span data-ttu-id="12143-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-198">필수</span><span class="sxs-lookup"><span data-stu-id="12143-198">Required</span></span> |<span data-ttu-id="12143-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-199">**xs:int**</span></span> |<span data-ttu-id="12143-200">이 비디오 트랙의 0 기준 인덱스입니다. **참고:** 반드시 hello MP4 파일에서 사용 되는 TrackID은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="12143-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="12143-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="12143-202">필수</span><span class="sxs-lookup"><span data-stu-id="12143-202">Required</span></span> |<span data-ttu-id="12143-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-203">**xs:string**</span></span> |<span data-ttu-id="12143-204">비디오 코덱 FourCC 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="12143-205">**프로필**</span><span class="sxs-lookup"><span data-stu-id="12143-205">**Profile**</span></span> |<span data-ttu-id="12143-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-206">**xs:string**</span></span> |<span data-ttu-id="12143-207">H264 프로필입니다 (적용 가능한 tooH264 코덱만)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="12143-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="12143-208">**Level**</span></span> |<span data-ttu-id="12143-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-209">**xs:string**</span></span> |<span data-ttu-id="12143-210">H264 수준입니다 (적용 가능한 tooH264 코덱만)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="12143-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="12143-211">**Width**</span></span><br/><br/> <span data-ttu-id="12143-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-213">필수</span><span class="sxs-lookup"><span data-stu-id="12143-213">Required</span></span> |<span data-ttu-id="12143-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-214">**xs:int**</span></span> |<span data-ttu-id="12143-215">인코딩된 비디오 너비(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="12143-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="12143-216">**Height**</span></span><br/><br/> <span data-ttu-id="12143-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-218">필수</span><span class="sxs-lookup"><span data-stu-id="12143-218">Required</span></span> |<span data-ttu-id="12143-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-219">**xs:int**</span></span> |<span data-ttu-id="12143-220">인코딩된 비디오 높이(픽셀)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="12143-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="12143-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="12143-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-223">필수</span><span class="sxs-lookup"><span data-stu-id="12143-223">Required</span></span> |<span data-ttu-id="12143-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="12143-224">**xs:double**</span></span> |<span data-ttu-id="12143-225">비디오 디스플레이 가로 세로 비율의 분자입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="12143-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="12143-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="12143-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-228">필수</span><span class="sxs-lookup"><span data-stu-id="12143-228">Required</span></span> |<span data-ttu-id="12143-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="12143-229">**xs:double**</span></span> |<span data-ttu-id="12143-230">비디오 디스플레이 가로 세로 비율의 분모입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="12143-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="12143-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="12143-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-233">필수</span><span class="sxs-lookup"><span data-stu-id="12143-233">Required</span></span> |<span data-ttu-id="12143-234">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="12143-234">**xs:decimal**</span></span> |<span data-ttu-id="12143-235">.3f 형식으로 측정된 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="12143-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="12143-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="12143-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-238">필수</span><span class="sxs-lookup"><span data-stu-id="12143-238">Required</span></span> |<span data-ttu-id="12143-239">**xs: decimal**</span><span class="sxs-lookup"><span data-stu-id="12143-239">**xs:decimal**</span></span> |<span data-ttu-id="12143-240">.3f 형식으로 기본 설정된 대상 비디오 프레임 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="12143-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="12143-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="12143-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-243">필수</span><span class="sxs-lookup"><span data-stu-id="12143-243">Required</span></span> |<span data-ttu-id="12143-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-244">**xs:int**</span></span> |<span data-ttu-id="12143-245">Hello AssetFile에서에서 계산 된 대로 k b / 초 단위의 평균 비디오 비트 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="12143-246">Hello 기본 스트림 페이로드만 계산 하 고 hello 패키징 오버 헤드는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="12143-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="12143-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="12143-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-249">필수</span><span class="sxs-lookup"><span data-stu-id="12143-249">Required</span></span> |<span data-ttu-id="12143-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-250">**xs:int**</span></span> |<span data-ttu-id="12143-251">이 비디오 트랙에 대 한 평균 비트 전송률 초당 킬로 비트의 hello 인코딩 사전 설정을 통해 요청에 따라 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="12143-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="12143-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="12143-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-253">minInclusive ="0"</span></span> |<span data-ttu-id="12143-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-254">**xs:int**</span></span> |<span data-ttu-id="12143-255">이 비디오 트랙의 최대 GOP 평균 비트 전송률(Kb/초)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="12143-256"><a name="AudioTracks "></a> AudioTracks 요소</span><span class="sxs-lookup"><span data-stu-id="12143-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="12143-257">각각의 실제 AssetFile에는 적절한 컨테이너 형식으로 인터리빙된 0개 이상의 오디오 트랙이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="12143-258">모든 오디오 트랙의 hello 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="12143-259">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="12143-260">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-260">Child elements</span></span>
| <span data-ttu-id="12143-261">이름</span><span class="sxs-lookup"><span data-stu-id="12143-261">Name</span></span> | <span data-ttu-id="12143-262">설명</span><span class="sxs-lookup"><span data-stu-id="12143-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="12143-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="12143-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="12143-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="12143-265">Hello 부모 AssetFile의에서 특정 오디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="12143-266">자세한 내용은 [AudioTrack 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="12143-267"><a name="AudioTrack "></a> AudioTrack 요소</span><span class="sxs-lookup"><span data-stu-id="12143-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="12143-268">Hello 부모 AssetFile의에서 특정 오디오 트랙입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="12143-269">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="12143-270">특성</span><span class="sxs-lookup"><span data-stu-id="12143-270">Attributes</span></span>
| <span data-ttu-id="12143-271">이름</span><span class="sxs-lookup"><span data-stu-id="12143-271">Name</span></span> | <span data-ttu-id="12143-272">형식</span><span class="sxs-lookup"><span data-stu-id="12143-272">Type</span></span> | <span data-ttu-id="12143-273">설명</span><span class="sxs-lookup"><span data-stu-id="12143-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12143-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="12143-274">**Id**</span></span><br/><br/> <span data-ttu-id="12143-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-276">필수</span><span class="sxs-lookup"><span data-stu-id="12143-276">Required</span></span> |<span data-ttu-id="12143-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-277">**xs:int**</span></span> |<span data-ttu-id="12143-278">이 오디오 트랙의 0 기준 인덱스입니다. **참고:** 반드시 hello MP4 파일에서 사용 되는 TrackID은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="12143-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="12143-279">**Codec**</span></span> |<span data-ttu-id="12143-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-280">**xs:string**</span></span> |<span data-ttu-id="12143-281">오디오 트랙 코덱 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-281">Audio track codec string.</span></span> |
| <span data-ttu-id="12143-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="12143-282">**EncoderVersion**</span></span> |<span data-ttu-id="12143-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-283">**xs:string**</span></span> |<span data-ttu-id="12143-284">EAC3에 필요한 선택적 인코더 버전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="12143-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="12143-285">**Channels**</span></span><br/><br/> <span data-ttu-id="12143-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-287">필수</span><span class="sxs-lookup"><span data-stu-id="12143-287">Required</span></span> |<span data-ttu-id="12143-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-288">**xs:int**</span></span> |<span data-ttu-id="12143-289">오디오 채널 수입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-289">Number of audio channels.</span></span> |
| <span data-ttu-id="12143-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="12143-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="12143-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-292">필수</span><span class="sxs-lookup"><span data-stu-id="12143-292">Required</span></span> |<span data-ttu-id="12143-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-293">**xs:int**</span></span> |<span data-ttu-id="12143-294">오디오 샘플링 속도(샘플/초 또는 Hz)입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="12143-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="12143-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="12143-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-297">필수</span><span class="sxs-lookup"><span data-stu-id="12143-297">Required</span></span> |<span data-ttu-id="12143-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-298">**xs:int**</span></span> |<span data-ttu-id="12143-299">Hello AssetFile에서에서 계산 되는 초당 비트 단위의 평균 오디오 비트 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="12143-300">Hello 기본 스트림 페이로드만 계산 하 고 hello 패키징 오버 헤드는 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="12143-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="12143-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="12143-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="12143-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="12143-303">필수</span><span class="sxs-lookup"><span data-stu-id="12143-303">Required</span></span> |<span data-ttu-id="12143-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-304">**xs:int**</span></span> |<span data-ttu-id="12143-305">Hello wFormatTag 형식에 대 한 샘플당 비트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="12143-306">자식 요소</span><span class="sxs-lookup"><span data-stu-id="12143-306">Child elements</span></span>
| <span data-ttu-id="12143-307">이름</span><span class="sxs-lookup"><span data-stu-id="12143-307">Name</span></span> | <span data-ttu-id="12143-308">설명</span><span class="sxs-lookup"><span data-stu-id="12143-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="12143-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="12143-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="12143-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="12143-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="12143-311">음량 측정 결과 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-311">Loudness metering result parameters.</span></span> <span data-ttu-id="12143-312">자세한 내용은 [LoudnessMeteringResultParameters 요소](media-services-output-metadata-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="12143-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="12143-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters 요소</span><span class="sxs-lookup"><span data-stu-id="12143-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="12143-314">음량 측정 결과 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="12143-315">[XML 예제](media-services-output-metadata-schema.md#xml)에서 XML 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12143-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="12143-316">특성</span><span class="sxs-lookup"><span data-stu-id="12143-316">Attributes</span></span>
| <span data-ttu-id="12143-317">이름</span><span class="sxs-lookup"><span data-stu-id="12143-317">Name</span></span> | <span data-ttu-id="12143-318">형식</span><span class="sxs-lookup"><span data-stu-id="12143-318">Type</span></span> | <span data-ttu-id="12143-319">설명</span><span class="sxs-lookup"><span data-stu-id="12143-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12143-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="12143-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="12143-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-321">**xs:string**</span></span> |<span data-ttu-id="12143-322">**DPLM**(Dolby Professional Loudness Metering) 개발 키트 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="12143-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="12143-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="12143-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="12143-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="12143-325">필수</span><span class="sxs-lookup"><span data-stu-id="12143-325">Required</span></span> |<span data-ttu-id="12143-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="12143-326">**xs:int**</span></span> |<span data-ttu-id="12143-327">DPLM을 통해 생성되며, LoudnessMetering을 설정할 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="12143-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="12143-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="12143-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="12143-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="12143-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="12143-330">필수</span><span class="sxs-lookup"><span data-stu-id="12143-330">Required</span></span> |<span data-ttu-id="12143-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="12143-331">**xs:float**</span></span> |<span data-ttu-id="12143-332">통합된 음량입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-332">Integrated loudness</span></span> |
| <span data-ttu-id="12143-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="12143-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="12143-334">필수</span><span class="sxs-lookup"><span data-stu-id="12143-334">Required</span></span> |<span data-ttu-id="12143-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-335">**xs:string**</span></span> |<span data-ttu-id="12143-336">통합된 음량 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="12143-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="12143-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="12143-338">필수</span><span class="sxs-lookup"><span data-stu-id="12143-338">Required</span></span> |<span data-ttu-id="12143-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="12143-339">**xs:string**</span></span> |<span data-ttu-id="12143-340">게이팅 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-340">Gating identifier</span></span> |
| <span data-ttu-id="12143-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="12143-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="12143-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="12143-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="12143-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="12143-343">**xs:float**</span></span> |<span data-ttu-id="12143-344">백분율 hello 프로그램을 통해 음성 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="12143-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="12143-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="12143-346">필수</span><span class="sxs-lookup"><span data-stu-id="12143-346">Required</span></span> |<span data-ttu-id="12143-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="12143-347">**xs:float**</span></span> |<span data-ttu-id="12143-348">다시 설정되거나 마지막으로 지워진 이후 채널당 샘플 최대 사용 절대값입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="12143-349">단위는 dBFS입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-349">Units are dBFS.</span></span> |
| <span data-ttu-id="12143-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="12143-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="12143-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="12143-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="12143-352">필수</span><span class="sxs-lookup"><span data-stu-id="12143-352">Required</span></span> |<span data-ttu-id="12143-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="12143-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="12143-354">샘플 최대 사용 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-354">Sample peak unit.</span></span> |
| <span data-ttu-id="12143-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="12143-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="12143-356">필수</span><span class="sxs-lookup"><span data-stu-id="12143-356">Required</span></span> |<span data-ttu-id="12143-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="12143-357">**xs:float**</span></span> |<span data-ttu-id="12143-358">다시 설정되거나 마지막으로 지워진 이후 채널당 실제 최대 사용 값입니다(ITU-R BS.1770-2 규격).</span><span class="sxs-lookup"><span data-stu-id="12143-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="12143-359">단위는 dBTP입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-359">Units are dBTP.</span></span> |
| <span data-ttu-id="12143-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="12143-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="12143-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="12143-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="12143-362">필수</span><span class="sxs-lookup"><span data-stu-id="12143-362">Required</span></span> |<span data-ttu-id="12143-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="12143-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="12143-364">실제 최대 사용 단위입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="12143-365">스키마 코드</span><span class="sxs-lookup"><span data-stu-id="12143-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
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
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
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
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
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
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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



## <span data-ttu-id="12143-366"><a name="xml"></a> XML 예제</span><span class="sxs-lookup"><span data-stu-id="12143-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="12143-367">hello 다음은 hello 출력 메타 데이터 파일의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="12143-367">hello following is an example of hello Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="12143-368">다음 단계</span><span class="sxs-lookup"><span data-stu-id="12143-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="12143-369">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="12143-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
