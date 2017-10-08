---
title: "Azure 미디어 분석 OCR aaaDigitize 텍스트 | Microsoft Docs"
description: "Azure 미디어 분석 OCR (광학 인식)에 사용할 수 있게 하면 비디오 파일의 텍스트 콘텐츠 tooconvert 검색 가능한 디지털 편집 가능한 텍스트입니다.  이렇게 하면 의미 있는 메타 데이터에서 미디어의 hello 비디오 신호 tooautomate hello 추출 있습니다."
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
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="b762e-104">Azure 미디어 분석 tooconvert 텍스트 콘텐츠를 사용 하 여 디지털 텍스트로 비디오 파일에서</span><span class="sxs-lookup"><span data-stu-id="b762e-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="b762e-105">개요</span><span class="sxs-lookup"><span data-stu-id="b762e-105">Overview</span></span>
<span data-ttu-id="b762e-106">비디오 파일에서 콘텐츠 tooextract 텍스트 필요 하 고 검색 가능한 디지털 텍스트는 편집 가능한를 생성 하는 경우에 Azure 미디어 분석 OCR (광학 인식)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="b762e-107">이 Azure 미디어 프로세서는 비디오 파일의 텍스트 콘텐츠를 검색하고 사용할 수 있는 텍스트 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="b762e-108">OCR 있습니다 tooautomate hello 의미 있는 메타 데이터에서에서 추출을 중인 미디어의 hello 비디오 신호를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="b762e-109">함께에서 함께 사용 하면 검색 엔진 쉽게 텍스트가 미디어 인덱스 및 콘텐츠 hello 검색 기능을 향상 시킬 수 있습니다 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="b762e-110">이러한 방식은 비디오 녹화 또는 슬라이드 쇼 프레젠테이션의 화면 캡처와 같이 텍스트가 풍부한 비디오에서 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="b762e-111">hello Azure OCR 미디어 프로세서 디지털 텍스트에 대해 최적화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="b762e-112">hello **Azure 미디어 OCR** 미디어 프로세서는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="b762e-113">이 항목에 대 한 세부 정보를 제공 **Azure 미디어 OCR** 표시 방법을 toouse Media Services SDK for.NET으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="b762e-114">추가 정보 및 예제에 대해서는 [이 블로그](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b762e-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="b762e-115">OCR 입력 파일</span><span class="sxs-lookup"><span data-stu-id="b762e-115">OCR input files</span></span>
<span data-ttu-id="b762e-116">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-116">Video files.</span></span> <span data-ttu-id="b762e-117">현재 형식에 따라 hello 지원 됩니다: MP4, MOV, 및 WMV입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="b762e-118">작업 구성</span><span class="sxs-lookup"><span data-stu-id="b762e-118">Task configuration</span></span>
<span data-ttu-id="b762e-119">작업 구성(사전 설정)</span><span class="sxs-lookup"><span data-stu-id="b762e-119">Task configuration (preset).</span></span> <span data-ttu-id="b762e-120">**Azure 미디어 OCR**로 작업을 만들 때에는 JSON 또는 XML을 사용하여 구성 사전 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="b762e-121">hello OCR 엔진에만 두 높이/너비에서 유효한 입력으로 최소 40 픽셀 toomaximum 32000 (픽셀) 사용 하 여 프로그램 이미지 영역이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="b762e-122">특성 설명</span><span class="sxs-lookup"><span data-stu-id="b762e-122">Attribute descriptions</span></span>
| <span data-ttu-id="b762e-123">특성 이름</span><span class="sxs-lookup"><span data-stu-id="b762e-123">Attribute name</span></span> | <span data-ttu-id="b762e-124">설명</span><span class="sxs-lookup"><span data-stu-id="b762e-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="b762e-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="b762e-125">AdvancedOutput</span></span>| <span data-ttu-id="b762e-126">AdvancedOutput tootrue로 설정 하면 모든 단일 단어 (추가 toophrases 및 지역)에 대 한 위치 데이터 hello JSON 출력에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="b762e-127">Toosee 하지 않을 경우 이러한 세부 정보 집합 hello toofalse를 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="b762e-128">hello 기본값은 false입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-128">hello default value is false.</span></span> <span data-ttu-id="b762e-129">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b762e-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="b762e-130">언어</span><span class="sxs-lookup"><span data-stu-id="b762e-130">Language</span></span> |<span data-ttu-id="b762e-131">(선택 사항) 어떤 toolook에 대 한 텍스트의 hello 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="b762e-132">Hello 다음 중 하나: 자동 검색 (기본값), 아랍어, ChineseSimplified, ChineseTraditional, 체코어 덴마크어, 네덜란드어, 영어, 핀란드어, 프랑스어, 독일어, 그리스어, 헝가리어, 이탈리아어, 일본어, 한국어, 노르웨이어, 폴란드어, 포르투갈어, 루마니아어, 러시아어, SerbianCyrillic, SerbianLatin, 슬로바키아어, 스페인어, 스웨덴어, 터키어로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="b762e-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="b762e-133">TextOrientation</span></span> |<span data-ttu-id="b762e-134">(선택 사항)는 toolook에 대 한 텍스트의 hello 방향을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="b762e-135">모든 문자 맨 hello "왼쪽된" 의미는 hello 왼쪽 방향으로 리 켰습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="b762e-136">기본 텍스트(예: 책에서 사용되는 텍스트)를 "위쪽" 방향으로 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="b762e-137">Hello 다음 중 하나: 자동 검색 (기본값), 최대, 오른쪽, 아래쪽, 왼쪽 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="b762e-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="b762e-138">TimeInterval</span></span> |<span data-ttu-id="b762e-139">(선택 사항) hello 샘플링 속도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="b762e-140">기본값은 1/2초 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="b762e-141">JSON 형식 – HH:mm:ss.SSS(기본값 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="b762e-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="b762e-142">XML 형식 – W3C XSD 기간 기본 형식(기본 PT0.5)</span><span class="sxs-lookup"><span data-stu-id="b762e-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="b762e-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="b762e-143">DetectRegions</span></span> |<span data-ttu-id="b762e-144">(선택 사항) DetectRegion 개체 배열을 toodetect 텍스트에서 hello 비디오 프레임 내에서 영역을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="b762e-145">DetectRegion 개체는 다음 4 개의 정수 값에는 hello 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="b762e-146">왼쪽-hello 왼쪽 여백에서 픽셀</span><span class="sxs-lookup"><span data-stu-id="b762e-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="b762e-147">Top-hello 위쪽 여백에서 픽셀</span><span class="sxs-lookup"><span data-stu-id="b762e-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="b762e-148">너비-픽셀에 hello 영역의 너비</span><span class="sxs-lookup"><span data-stu-id="b762e-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="b762e-149">높이 – 픽셀에 hello 영역의 높이</span><span class="sxs-lookup"><span data-stu-id="b762e-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="b762e-150">JSON 사전 설정 예제</span><span class="sxs-lookup"><span data-stu-id="b762e-150">JSON preset example</span></span>

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


#### <a name="xml-preset-example"></a><span data-ttu-id="b762e-151">XML 사전 설정 예제</span><span class="sxs-lookup"><span data-stu-id="b762e-151">XML preset example</span></span>
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

## <a name="ocr-output-files"></a><span data-ttu-id="b762e-152">OCR 출력 파일</span><span class="sxs-lookup"><span data-stu-id="b762e-152">OCR output files</span></span>
<span data-ttu-id="b762e-153">hello OCR 미디어 프로세서의 hello 출력은 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="b762e-154">Hello 출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="b762e-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="b762e-155">hello 비디오 OCR 출력 비디오에 문자가 hello에 시간을 세그먼트 데이터를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="b762e-156">분석에 관심이 hello 단어 정확 하 게 언어 또는 toohone에서 방향 등의 특성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="b762e-157">hello 출력 특성에 따라 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="b762e-158">요소</span><span class="sxs-lookup"><span data-stu-id="b762e-158">Element</span></span> | <span data-ttu-id="b762e-159">설명</span><span class="sxs-lookup"><span data-stu-id="b762e-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b762e-160">시간 간격</span><span class="sxs-lookup"><span data-stu-id="b762e-160">Timescale</span></span> |<span data-ttu-id="b762e-161">"틱" hello 비디오의 초 당</span><span class="sxs-lookup"><span data-stu-id="b762e-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="b762e-162">Offset</span><span class="sxs-lookup"><span data-stu-id="b762e-162">Offset</span></span> |<span data-ttu-id="b762e-163">타임스탬프의 시간 오프셋</span><span class="sxs-lookup"><span data-stu-id="b762e-163">time offset for timestamps.</span></span> <span data-ttu-id="b762e-164">동영상 API 버전 1.0에서는 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="b762e-165">프레임 속도</span><span class="sxs-lookup"><span data-stu-id="b762e-165">Framerate</span></span> |<span data-ttu-id="b762e-166">Hello 비디오의 초당 프레임 수</span><span class="sxs-lookup"><span data-stu-id="b762e-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="b762e-167">width</span><span class="sxs-lookup"><span data-stu-id="b762e-167">width</span></span> |<span data-ttu-id="b762e-168">hello 픽셀에서 비디오의 너비</span><span class="sxs-lookup"><span data-stu-id="b762e-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="b762e-169">height</span><span class="sxs-lookup"><span data-stu-id="b762e-169">height</span></span> |<span data-ttu-id="b762e-170">hello 픽셀에서 비디오의 높이</span><span class="sxs-lookup"><span data-stu-id="b762e-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="b762e-171">조각</span><span class="sxs-lookup"><span data-stu-id="b762e-171">Fragments</span></span> |<span data-ttu-id="b762e-172">시간 기반 청크는 hello에 메타 데이터 청크 되는 비디오의 배열</span><span class="sxs-lookup"><span data-stu-id="b762e-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="b762e-173">start</span><span class="sxs-lookup"><span data-stu-id="b762e-173">start</span></span> |<span data-ttu-id="b762e-174">"틱" 단위의 조각 시작 시간</span><span class="sxs-lookup"><span data-stu-id="b762e-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b762e-175">duration</span><span class="sxs-lookup"><span data-stu-id="b762e-175">duration</span></span> |<span data-ttu-id="b762e-176">"틱" 단위의 조각 길이</span><span class="sxs-lookup"><span data-stu-id="b762e-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="b762e-177">interval</span><span class="sxs-lookup"><span data-stu-id="b762e-177">interval</span></span> |<span data-ttu-id="b762e-178">조각을 지정한 hello 내에서 각 이벤트의 간격</span><span class="sxs-lookup"><span data-stu-id="b762e-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="b762e-179">events</span><span class="sxs-lookup"><span data-stu-id="b762e-179">events</span></span> |<span data-ttu-id="b762e-180">영역을 포함하는 배열</span><span class="sxs-lookup"><span data-stu-id="b762e-180">array containing regions</span></span> |
| <span data-ttu-id="b762e-181">region</span><span class="sxs-lookup"><span data-stu-id="b762e-181">region</span></span> |<span data-ttu-id="b762e-182">검색된 단어 또는 구를 나타내는 개체</span><span class="sxs-lookup"><span data-stu-id="b762e-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="b762e-183">언어</span><span class="sxs-lookup"><span data-stu-id="b762e-183">language</span></span> |<span data-ttu-id="b762e-184">hello 텍스트 영역 내에서 검색의 언어</span><span class="sxs-lookup"><span data-stu-id="b762e-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="b762e-185">orientation</span><span class="sxs-lookup"><span data-stu-id="b762e-185">orientation</span></span> |<span data-ttu-id="b762e-186">영역 내에서 검색 하는 hello 텍스트의 방향</span><span class="sxs-lookup"><span data-stu-id="b762e-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="b762e-187">lines</span><span class="sxs-lookup"><span data-stu-id="b762e-187">lines</span></span> |<span data-ttu-id="b762e-188">지역 내에서 검색된 텍스트의 줄 배열</span><span class="sxs-lookup"><span data-stu-id="b762e-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="b762e-189">텍스트</span><span class="sxs-lookup"><span data-stu-id="b762e-189">text</span></span> |<span data-ttu-id="b762e-190">실제 hello 텍스트</span><span class="sxs-lookup"><span data-stu-id="b762e-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="b762e-191">JSON 출력 예제</span><span class="sxs-lookup"><span data-stu-id="b762e-191">JSON output example</span></span>
<span data-ttu-id="b762e-192">hello 다음 출력 예제에서는 hello 일반 비디오 정보와 여러 비디오 조각을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="b762e-193">모든 비디오 조각은 OCR MP hello 언어 및의 텍스트 방향으로 검색 되는 영역 마다 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="b762e-194">hello 영역에는 모든 단어 줄 hello 줄의 텍스트, hello 줄의 위치 및 모든 단어 정보 (word 콘텐츠에, 위치 및 신뢰도)이이 줄에서이 영역에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="b762e-195">hello 다음은 예를 들어, 넣은 몇 가지 설명을 인라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-195">hello following is an example, and I put some comments inline.</span></span>

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
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
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

## <a name="net-sample-code"></a><span data-ttu-id="b762e-196">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="b762e-196">.NET sample code</span></span>

<span data-ttu-id="b762e-197">hello 다음 프로그램 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="b762e-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="b762e-198">자산 만들기 hello 자산 미디어 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="b762e-199">OCR 구성/사전 설정 파일을 사용하여 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="b762e-200">Hello 출력 JSON 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="b762e-201">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="b762e-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="b762e-202">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b762e-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="b762e-203">예제</span><span class="sxs-lookup"><span data-stu-id="b762e-203">Example</span></span>

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
            // Read values from hello App.config file.
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="b762e-204">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b762e-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b762e-205">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b762e-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="b762e-206">관련 링크</span><span class="sxs-lookup"><span data-stu-id="b762e-206">Related links</span></span>
[<span data-ttu-id="b762e-207">Azure 미디어 서비스 분석 개요</span><span class="sxs-lookup"><span data-stu-id="b762e-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

