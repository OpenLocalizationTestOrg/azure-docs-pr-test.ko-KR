---
title: "Azure 미디어 분석 OCR로 텍스트 디지털화 | Microsoft Docs"
description: "Azure 미디어 분석 OCR(광학 문자 인식)을 사용하면 비디오 파일의 텍스트 콘텐츠를 편집 및 검색 가능한 디지털 텍스트로 변환할 수 있습니다.  이 방법을 사용하면 미디어의 비디오 신호에서 의미 있는 메타데이터를 자동으로 추출할 수 있습니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 43f5b3a9bbec243e668c79702045094fcfedbdda
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-media-analytics-to-convert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="27af2-104">Azure 미디어 분석을 사용하여 비디오 파일의 텍스트 콘텐츠를 디지털 텍스트로 변환</span><span class="sxs-lookup"><span data-stu-id="27af2-104">Use Azure Media Analytics to convert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="27af2-105">개요</span><span class="sxs-lookup"><span data-stu-id="27af2-105">Overview</span></span>
<span data-ttu-id="27af2-106">비디오 파일에서 텍스트 콘텐츠를 추출하고 편집 및 검색 가능한 디지털 텍스트를 생성해야 할 경우 Azure 미디어 분석 OCR(광학 문자 인식)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-106">If you need to extract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="27af2-107">이 Azure 미디어 프로세서는 비디오 파일의 텍스트 콘텐츠를 검색하고 사용할 수 있는 텍스트 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="27af2-108">OCR을 사용하면 미디어의 비디오 신호에서 의미 있는 메타데이터를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-108">OCR enables you to automate the extraction of meaningful metadata from the video signal of your media.</span></span>

<span data-ttu-id="27af2-109">검색 엔진과 함께 사용할 경우 텍스트에 따라 미디어를 쉽게 인덱싱하고 콘텐츠 검색 기능을 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance the discoverability of your content.</span></span> <span data-ttu-id="27af2-110">이러한 방식은 비디오 녹화 또는 슬라이드 쇼 프레젠테이션의 화면 캡처와 같이 텍스트가 풍부한 비디오에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="27af2-111">Azure OCR 미디어 프로세서는 디지털 텍스트에 맞게 최적화됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-111">The Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="27af2-112">**Azure 미디어 OCR** 미디어 프로세서는 현재 미리 보기로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-112">The **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="27af2-113">이 토픽은 **Azure Media OCR** 에 대한 세부 정보 및 .NET용 Media Services SDK와 함께 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-113">This topic gives details about  **Azure Media OCR** and shows how to use it with Media Services SDK for .NET.</span></span> <span data-ttu-id="27af2-114">추가 정보 및 예제에 대해서는 [이 블로그](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27af2-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="27af2-115">OCR 입력 파일</span><span class="sxs-lookup"><span data-stu-id="27af2-115">OCR input files</span></span>
<span data-ttu-id="27af2-116">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-116">Video files.</span></span> <span data-ttu-id="27af2-117">현재 MP4, MOV 및 WMV 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-117">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="27af2-118">작업 구성</span><span class="sxs-lookup"><span data-stu-id="27af2-118">Task configuration</span></span>
<span data-ttu-id="27af2-119">작업 구성(사전 설정)</span><span class="sxs-lookup"><span data-stu-id="27af2-119">Task configuration (preset).</span></span> <span data-ttu-id="27af2-120">**Azure 미디어 OCR**로 작업을 만들 때에는 JSON 또는 XML을 사용하여 구성 사전 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="27af2-121">OCR 엔진은 높이/너비의 유효한 입력으로 최소 40픽셀에서 최대 32000픽셀의 이미지 영역만 차지합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-121">The OCR engine only takes an image region with minimum 40 pixels to maximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="27af2-122">특성 설명</span><span class="sxs-lookup"><span data-stu-id="27af2-122">Attribute descriptions</span></span>
| <span data-ttu-id="27af2-123">특성 이름</span><span class="sxs-lookup"><span data-stu-id="27af2-123">Attribute name</span></span> | <span data-ttu-id="27af2-124">설명</span><span class="sxs-lookup"><span data-stu-id="27af2-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="27af2-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="27af2-125">AdvancedOutput</span></span>| <span data-ttu-id="27af2-126">AdvancedOutput을 true로 설정하면 JSON 출력에는 모든 단일 단어(구 및 지역 외에)에 대해 위치 데이터가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-126">If you set AdvancedOutput to true, the JSON output will contain positional data for every single word (in addition to phrases and regions).</span></span> <span data-ttu-id="27af2-127">이러한 세부 정보를 표시하지 않으려면 flag를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-127">If you do not want to see these details, set the flag to false.</span></span> <span data-ttu-id="27af2-128">기본값은 False입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-128">The default value is false.</span></span> <span data-ttu-id="27af2-129">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27af2-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="27af2-130">language</span><span class="sxs-lookup"><span data-stu-id="27af2-130">Language</span></span> |<span data-ttu-id="27af2-131">(선택 사항) 검색할 텍스트의 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-131">(optional) describes the language of text for which to look.</span></span> <span data-ttu-id="27af2-132">AutoDetect(기본값), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German, Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-132">One of the following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="27af2-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="27af2-133">TextOrientation</span></span> |<span data-ttu-id="27af2-134">(선택 사항) 검색할 텍스트의 방향에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-134">(optional) describes the orientation of text for which to look.</span></span>  <span data-ttu-id="27af2-135">"Left"는 모든 문자의 위쪽이 왼쪽을 향함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-135">"Left" means that the top of all letters are pointed towards the left.</span></span>  <span data-ttu-id="27af2-136">기본 텍스트(예: 책에서 사용되는 텍스트)를 "위쪽" 방향으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="27af2-137">AutoDetect(기본값), Up, Right, Down, Left 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-137">One of the following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="27af2-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="27af2-138">TimeInterval</span></span> |<span data-ttu-id="27af2-139">(선택 사항) 샘플링 속도를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-139">(optional) describes the sampling rate.</span></span>  <span data-ttu-id="27af2-140">기본값은 1/2초 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="27af2-141">JSON 형식 – HH:mm:ss.SSS(기본값 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="27af2-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="27af2-142">XML 형식 – W3C XSD 기간 기본 형식(기본 PT0.5)</span><span class="sxs-lookup"><span data-stu-id="27af2-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="27af2-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="27af2-143">DetectRegions</span></span> |<span data-ttu-id="27af2-144">(선택 사항) 텍스트를 검색할 비디오 프레임 내의 영역을 지정하는 DetectRegion 개체의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-144">(optional) An array of DetectRegion objects specifying regions within the video frame in which to detect text.</span></span><br/><span data-ttu-id="27af2-145">DetectRegion 개체는 다음 4개 정수 값으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-145">A DetectRegion object is made of the following four integer values:</span></span><br/><span data-ttu-id="27af2-146">Left - 왼쪽 여백에서 픽셀</span><span class="sxs-lookup"><span data-stu-id="27af2-146">Left – pixels from the left-margin</span></span><br/><span data-ttu-id="27af2-147">Top - 위쪽 여백에서 픽셀</span><span class="sxs-lookup"><span data-stu-id="27af2-147">Top – pixels from the top-margin</span></span><br/><span data-ttu-id="27af2-148">Width – 영역 너비(픽셀)</span><span class="sxs-lookup"><span data-stu-id="27af2-148">Width – width of the region in pixels</span></span><br/><span data-ttu-id="27af2-149">Height – 영역 높이(픽셀)</span><span class="sxs-lookup"><span data-stu-id="27af2-149">Height – height of the region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="27af2-150">JSON 사전 설정 예제</span><span class="sxs-lookup"><span data-stu-id="27af2-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="27af2-151">XML 사전 설정 예제</span><span class="sxs-lookup"><span data-stu-id="27af2-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="27af2-152">OCR 출력 파일</span><span class="sxs-lookup"><span data-stu-id="27af2-152">OCR output files</span></span>
<span data-ttu-id="27af2-153">OCR 미디어 프로세서의 출력은 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-153">The output of the OCR media processor is a JSON file.</span></span>

### <a name="elements-of-the-output-json-file"></a><span data-ttu-id="27af2-154">출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="27af2-154">Elements of the output JSON file</span></span>
<span data-ttu-id="27af2-155">비디오 OCR 출력은 비디오에서 찾을 수 있는 문자에 대한 시분할 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-155">The Video OCR output provides time-segmented data on the characters found in your video.</span></span>  <span data-ttu-id="27af2-156">분석하려는 정확한 단어 쪽을 향하는 방향 또는 언어와 같은 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-156">You can use attributes such as language or orientation to hone-in on exactly the words that you are interested in analyzing.</span></span> 

<span data-ttu-id="27af2-157">출력은 다음 특성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-157">The output contains the following attributes:</span></span>

| <span data-ttu-id="27af2-158">요소</span><span class="sxs-lookup"><span data-stu-id="27af2-158">Element</span></span> | <span data-ttu-id="27af2-159">설명</span><span class="sxs-lookup"><span data-stu-id="27af2-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="27af2-160">시간 간격</span><span class="sxs-lookup"><span data-stu-id="27af2-160">Timescale</span></span> |<span data-ttu-id="27af2-161">동영상의 초당 "틱"</span><span class="sxs-lookup"><span data-stu-id="27af2-161">"ticks" per second of the video</span></span> |
| <span data-ttu-id="27af2-162">Offset</span><span class="sxs-lookup"><span data-stu-id="27af2-162">Offset</span></span> |<span data-ttu-id="27af2-163">타임스탬프의 시간 오프셋</span><span class="sxs-lookup"><span data-stu-id="27af2-163">time offset for timestamps.</span></span> <span data-ttu-id="27af2-164">동영상 API 버전 1.0에서는 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="27af2-165">프레임 속도</span><span class="sxs-lookup"><span data-stu-id="27af2-165">Framerate</span></span> |<span data-ttu-id="27af2-166">동영상의 초당 프레임 수</span><span class="sxs-lookup"><span data-stu-id="27af2-166">Frames per second of the video</span></span> |
| <span data-ttu-id="27af2-167">width</span><span class="sxs-lookup"><span data-stu-id="27af2-167">width</span></span> |<span data-ttu-id="27af2-168">픽셀 단위의 동영상 너비</span><span class="sxs-lookup"><span data-stu-id="27af2-168">width of the video in pixels</span></span> |
| <span data-ttu-id="27af2-169">height</span><span class="sxs-lookup"><span data-stu-id="27af2-169">height</span></span> |<span data-ttu-id="27af2-170">픽셀 단위의 동영상 높이</span><span class="sxs-lookup"><span data-stu-id="27af2-170">height of the video in pixels</span></span> |
| <span data-ttu-id="27af2-171">조각</span><span class="sxs-lookup"><span data-stu-id="27af2-171">Fragments</span></span> |<span data-ttu-id="27af2-172">메타데이터가 청크되는 시간 기반 비디오 청크 배열</span><span class="sxs-lookup"><span data-stu-id="27af2-172">array of time-based chunks of video into which the metadata is chunked</span></span> |
| <span data-ttu-id="27af2-173">start</span><span class="sxs-lookup"><span data-stu-id="27af2-173">start</span></span> |<span data-ttu-id="27af2-174">"틱" 단위의 조각 시작 시간</span><span class="sxs-lookup"><span data-stu-id="27af2-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="27af2-175">duration</span><span class="sxs-lookup"><span data-stu-id="27af2-175">duration</span></span> |<span data-ttu-id="27af2-176">"틱" 단위의 조각 길이</span><span class="sxs-lookup"><span data-stu-id="27af2-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="27af2-177">interval</span><span class="sxs-lookup"><span data-stu-id="27af2-177">interval</span></span> |<span data-ttu-id="27af2-178">지정된 조각 내의 각 이벤트 간격</span><span class="sxs-lookup"><span data-stu-id="27af2-178">interval of each event within the given fragment</span></span> |
| <span data-ttu-id="27af2-179">events</span><span class="sxs-lookup"><span data-stu-id="27af2-179">events</span></span> |<span data-ttu-id="27af2-180">영역을 포함하는 배열</span><span class="sxs-lookup"><span data-stu-id="27af2-180">array containing regions</span></span> |
| <span data-ttu-id="27af2-181">region</span><span class="sxs-lookup"><span data-stu-id="27af2-181">region</span></span> |<span data-ttu-id="27af2-182">검색된 단어 또는 구를 나타내는 개체</span><span class="sxs-lookup"><span data-stu-id="27af2-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="27af2-183">언어</span><span class="sxs-lookup"><span data-stu-id="27af2-183">language</span></span> |<span data-ttu-id="27af2-184">지역 내에서 검색된 텍스트의 언어</span><span class="sxs-lookup"><span data-stu-id="27af2-184">language of the text detected within a region</span></span> |
| <span data-ttu-id="27af2-185">orientation</span><span class="sxs-lookup"><span data-stu-id="27af2-185">orientation</span></span> |<span data-ttu-id="27af2-186">지역 내에서 검색된 텍스트의 방향</span><span class="sxs-lookup"><span data-stu-id="27af2-186">orientation of the text detected within a region</span></span> |
| <span data-ttu-id="27af2-187">lines</span><span class="sxs-lookup"><span data-stu-id="27af2-187">lines</span></span> |<span data-ttu-id="27af2-188">지역 내에서 검색된 텍스트의 줄 배열</span><span class="sxs-lookup"><span data-stu-id="27af2-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="27af2-189">텍스트</span><span class="sxs-lookup"><span data-stu-id="27af2-189">text</span></span> |<span data-ttu-id="27af2-190">실제 텍스트</span><span class="sxs-lookup"><span data-stu-id="27af2-190">the actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="27af2-191">JSON 출력 예제</span><span class="sxs-lookup"><span data-stu-id="27af2-191">JSON output example</span></span>
<span data-ttu-id="27af2-192">다음 출력 예제는 일반 동영상 정보 및 몇 가지 동영상 조각을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-192">The following output example contains the general video information and several video fragments.</span></span> <span data-ttu-id="27af2-193">모든 이벤트 조각에는 OCR MP에 의해 언어 및 텍스트 방향에 따라 검색되는 모든 영역이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-193">In every video fragment, it contains every region which is detected by OCR MP with the language and its text orientation.</span></span> <span data-ttu-id="27af2-194">또한 이러한 영역에는 이 영역의 모든 단어 줄과 이 줄에 포함된 줄의 텍스트, 줄의 위치 및 모든 단어 정보(단어 내용, 위치 및 신뢰도)가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-194">The region also contains every word line in this region with the line’s text, the line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="27af2-195">다음 예제에서는 줄 내에 주석을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-195">The following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // the time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // the detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including the text and the position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="27af2-196">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="27af2-196">.NET sample code</span></span>

<span data-ttu-id="27af2-197">다음 프로그램은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-197">The following program shows how to:</span></span>

1. <span data-ttu-id="27af2-198">자산을 만들고 미디어 파일을 자산에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-198">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="27af2-199">OCR 구성/사전 설정 파일을 사용하여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="27af2-200">출력 JSON 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-200">Download the output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="27af2-201">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="27af2-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="27af2-202">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="27af2-202">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="27af2-203">예제</span><span class="sxs-lookup"><span data-stu-id="27af2-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
    {
        class Program
        {
            // Read values from the App.config file.
            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run the OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference to Azure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

            static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
            {
                var processor = _context.MediaProcessors
                    .Where(p => p.Name == mediaProcessorName)
                    .ToList()
                    .OrderBy(p => new Version(p.Version))
                    .LastOrDefault();

                if (processor == null)
                    throw new ArgumentException(string.Format("Unknown media processor",
                                                               mediaProcessorName));

                return processor;
            }

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }

        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="27af2-204">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="27af2-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="27af2-205">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="27af2-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="27af2-206">관련 링크</span><span class="sxs-lookup"><span data-stu-id="27af2-206">Related links</span></span>
[<span data-ttu-id="27af2-207">Azure 미디어 서비스 분석 개요</span><span class="sxs-lookup"><span data-stu-id="27af2-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

