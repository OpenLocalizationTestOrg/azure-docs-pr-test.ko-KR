---
title: "Media Encoder Premium Workflow 형식 및 코덱 | Microsoft 문서"
description: "이 토픽에서는 미디어 인코더 Premium 워크플로 형식 및 코덱에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e18de2adc9aac585d6890dd7b43a54f1a0ca177e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="a3f6a-103">미디어 인코더 Premium 워크플로 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="a3f6a-104">프리미엄 인코더 관련 질문은 mepd@microsoft.com으로 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="a3f6a-105">중국에서는 이 토픽에서 설명하는 미디어 인코더 Premium 워크플로 미디어 프로세서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="a3f6a-106">이 문서에는 **미디어 인코더 Premium 워크플로** 인코더의 공개 미리 보기 버전에서 지원하는 입력 및 출력 파일 형식과 코덱 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="a3f6a-107">미디어 인코더 Premium 워크플로 입력 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="a3f6a-108">미디어 인코더 Premium 워크플로 출력 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="a3f6a-109">**미디어 인코더 Premium 워크플로** 는 [이](#closed_captioning) 섹션에 설명된 선택 캡션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="a3f6a-110"><a id="input_formats"></a>미디어 인코더 Premium 워크플로 입력 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="a3f6a-111">다음 섹션에는 이 미디어 프로세서에서 입력으로 지원되는 코덱 및 파일 형식이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="a3f6a-112">입력 컨테이너/파일 형식</span><span class="sxs-lookup"><span data-stu-id="a3f6a-112">Input Container/File Formats</span></span>
* <span data-ttu-id="a3f6a-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="a3f6a-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="a3f6a-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="a3f6a-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="a3f6a-115">GXF</span><span class="sxs-lookup"><span data-stu-id="a3f6a-115">GXF</span></span>
* <span data-ttu-id="a3f6a-116">MPEG-2 전송 스트림</span><span class="sxs-lookup"><span data-stu-id="a3f6a-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="a3f6a-117">MPEG-2 프로그램 스트림</span><span class="sxs-lookup"><span data-stu-id="a3f6a-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="a3f6a-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="a3f6a-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="a3f6a-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="a3f6a-119">Windows Media/ASF</span></span>
* <span data-ttu-id="a3f6a-120">AVI(압축되지 않은 8비트/10비트)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="a3f6a-121">입력 비디오 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-121">Input Video Codecs</span></span>
* <span data-ttu-id="a3f6a-122">AVC 8비트/10비트, 최대 4:2:2, AVCIntra 포함</span><span class="sxs-lookup"><span data-stu-id="a3f6a-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="a3f6a-123">Avid DNxHD(MXF)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="a3f6a-124">DVCPro/DVCProHD(MXF)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="a3f6a-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="a3f6a-125">JPEG2000</span></span>
* <span data-ttu-id="a3f6a-126">MPEG-2(최대 422 프로필 및 높은 수준, XDCAM, XDCAM HD, XDCAM IMX, CableLabs® 및 D10과 같은 변형 포함)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="a3f6a-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="a3f6a-127">MPEG-1</span></span>
* <span data-ttu-id="a3f6a-128">Windows Media 비디오/VC-1</span><span class="sxs-lookup"><span data-stu-id="a3f6a-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="a3f6a-129">입력 오디오 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-129">Input Audio Codecs</span></span>
* <span data-ttu-id="a3f6a-130">AES(SMPTE 331M 및 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="a3f6a-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="a3f6a-131">Dolby® E</span></span>
* <span data-ttu-id="a3f6a-132">Dolby® Digital(AC3)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="a3f6a-133">AAC(AAC-LC, AAC-HE 및 AAC-HEv2, 최대 5.1)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="a3f6a-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="a3f6a-134">MPEG Layer 2</span></span>
* <span data-ttu-id="a3f6a-135">MP3(MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="a3f6a-136">Windows Media 오디오</span><span class="sxs-lookup"><span data-stu-id="a3f6a-136">Windows Media Audio</span></span>
* <span data-ttu-id="a3f6a-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="a3f6a-137">WAV/PCM</span></span>

## <span data-ttu-id="a3f6a-138"><a id="output_format"></a>미디어 인코더 Premium 워크플로 출력 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="a3f6a-139">다음 섹션에는 이 미디어 프로세서에서 출력으로 지원되는 코덱 및 파일 형식이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="a3f6a-140">출력 컨테이너/파일 형식</span><span class="sxs-lookup"><span data-stu-id="a3f6a-140">Output Container/File Formats</span></span>
* <span data-ttu-id="a3f6a-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="a3f6a-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="a3f6a-142">MXF(OP1a, XDCAM 및 AS02)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="a3f6a-143">DPP(AS11 포함)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-143">DPP (including AS11)</span></span>
* <span data-ttu-id="a3f6a-144">GXF</span><span class="sxs-lookup"><span data-stu-id="a3f6a-144">GXF</span></span>
* <span data-ttu-id="a3f6a-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="a3f6a-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="a3f6a-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="a3f6a-146">Windows Media/ASF</span></span>
* <span data-ttu-id="a3f6a-147">AVI(압축되지 않은 8비트/10비트)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="a3f6a-148">부드러운 스트리밍 파일 형식(PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="a3f6a-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="a3f6a-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="a3f6a-150">출력 비디오 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-150">Output Video Codecs</span></span>
* <span data-ttu-id="a3f6a-151">AVC(H.264, 8비트, 최대 High Profile, 수준 5.2, 4K Ultra HD, AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="a3f6a-152">Avid DNxHD(MXF)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="a3f6a-153">DVCPro/DVCProHD(MXF)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="a3f6a-154">MPEG-2(최대 422 프로필 및 높은 수준, XDCAM, XDCAM HD, XDCAM IMX, CableLabs® 및 D10과 같은 변형 포함)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="a3f6a-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="a3f6a-155">MPEG-1</span></span>
* <span data-ttu-id="a3f6a-156">Windows Media 비디오/VC-1</span><span class="sxs-lookup"><span data-stu-id="a3f6a-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="a3f6a-157">JPEG 축소판 그림 만들기</span><span class="sxs-lookup"><span data-stu-id="a3f6a-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="a3f6a-158">출력 오디오 코덱</span><span class="sxs-lookup"><span data-stu-id="a3f6a-158">Output Audio Codecs</span></span>
* <span data-ttu-id="a3f6a-159">AES(SMPTE 331M 및 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="a3f6a-160">Dolby® Digital(AC3)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="a3f6a-161">Dolby® Digital Plus(E-AC3) 최대 7.1</span><span class="sxs-lookup"><span data-stu-id="a3f6a-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="a3f6a-162">AAC(AAC-LC, AAC-HE 및 AAC-HEv2, 최대 5.1)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="a3f6a-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="a3f6a-163">MPEG Layer 2</span></span>
* <span data-ttu-id="a3f6a-164">MP3(MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="a3f6a-165">Windows Media 오디오</span><span class="sxs-lookup"><span data-stu-id="a3f6a-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="a3f6a-166">Dolby® Digital(AC3)로 인코딩하면 출력은 ISO MP4 파일에만 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="a3f6a-167"><a id="closed_captioning"></a>선택 캡션 지원</span><span class="sxs-lookup"><span data-stu-id="a3f6a-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="a3f6a-168">수집 시 **미디어 인코더 Premium 워크플로** 는 다음을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="a3f6a-169">SCC 파일</span><span class="sxs-lookup"><span data-stu-id="a3f6a-169">SCC files</span></span>
2. <span data-ttu-id="a3f6a-170">SMPTE-TT 파일</span><span class="sxs-lookup"><span data-stu-id="a3f6a-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="a3f6a-171">CEA-608/CEA-708 – 사용자 데이터에 수반됨(H.264 기초 스트림, ATSC/53, SCTE20의 SEI 메시지) 또는 MXF/GXF 파일의 보조 데이터에 수반됨</span><span class="sxs-lookup"><span data-stu-id="a3f6a-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="a3f6a-172">STL 자막 파일</span><span class="sxs-lookup"><span data-stu-id="a3f6a-172">STL subtitle files</span></span>

<span data-ttu-id="a3f6a-173">출력 시 다음 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="a3f6a-174">CEA 608을 CEA 708로 변환</span><span class="sxs-lookup"><span data-stu-id="a3f6a-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="a3f6a-175">CEA-608/CEA-708 통과(H.264 기본 스트림의 SEI 메시지에 포함되거나 MXF 파일의 보조 데이터로 전달됨)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="a3f6a-176">SCC</span><span class="sxs-lookup"><span data-stu-id="a3f6a-176">SCC</span></span>
4. <span data-ttu-id="a3f6a-177">SMPTE 시간 제한 텍스트(SMPTE RP2052당 소스 CEA 608, DFXP 파일 만들기 포함)</span><span class="sxs-lookup"><span data-stu-id="a3f6a-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="a3f6a-178">SRT 자막 파일</span><span class="sxs-lookup"><span data-stu-id="a3f6a-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="a3f6a-179">DVB 자막 스트림</span><span class="sxs-lookup"><span data-stu-id="a3f6a-179">DVB subtitle streams</span></span>

<span data-ttu-id="a3f6a-180">참고: 위의 출력 형식 중 일부는 Azure 미디어 서비스에서 스트리밍을 통해 배달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a3f6a-181">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="a3f6a-181">Known issues</span></span>
<span data-ttu-id="a3f6a-182">입력된 비디오에 자막이 없는 경우, 출력 자산은 빈 TTML 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a3f6a-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="a3f6a-183">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a3f6a-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a3f6a-184">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a3f6a-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

