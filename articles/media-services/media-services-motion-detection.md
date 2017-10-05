---
title: "Azure 미디어 분석으로 동작 검색 | Microsoft 문서"
description: "Azure 미디어 동작 탐지기 MP(미디어 프로세서)를 사용하여 길고 특별하지 않은 동영상 중에서 원하는 섹션을 효율적으로 식별합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="a9eb2-103">Azure 미디어 검색으로 동작 검색</span><span class="sxs-lookup"><span data-stu-id="a9eb2-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="a9eb2-104">개요</span><span class="sxs-lookup"><span data-stu-id="a9eb2-104">Overview</span></span>
<span data-ttu-id="a9eb2-105">**Azure 미디어 동작 탐지기** 의 MP(미디어 프로세서)를 사용하여 길고 특별하지 않은 동영상 중에서 원하는 섹션을 효율적으로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="a9eb2-106">동작 검색은 고정된 카메라 장면에서 동작이 발생한 동영상 섹션을 식별하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="a9eb2-107">이벤트가 발생한 경계 영역 및 타임스탬프가 있는 메타데이터를 포함하는 JSON 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="a9eb2-108">보안 동영상 피드를 대상으로 하는 이 기술은 동작을 관련 이벤트와 그림자 및 조명 변화와 같은 가양성으로 분류할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="a9eb2-109">이를 통해 수많은 관련 없는 이벤트로 인해 스팸 처리되지 않고 카메라 피드로부터 보안 경고를 생성할 수 있으며, 아주 긴 감시 동영상으로부터 필요한 순간을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="a9eb2-110">**Azure 미디어 동작 탐지기** MP는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="a9eb2-111">이 항목은 **Azure 미디어 동작 탐지기**에 대한 세부 정보 및 .NET용 Media Services SDK와 함께 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="a9eb2-112">동작 검색기 입력 파일</span><span class="sxs-lookup"><span data-stu-id="a9eb2-112">Motion Detector input files</span></span>
<span data-ttu-id="a9eb2-113">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-113">Video files.</span></span> <span data-ttu-id="a9eb2-114">현재 MP4, MOV 및 WMV 형식이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="a9eb2-115">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="a9eb2-115">Task configuration (preset)</span></span>
<span data-ttu-id="a9eb2-116">**Azure 미디어 동작 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="a9eb2-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a9eb2-117">Parameters</span></span>
<span data-ttu-id="a9eb2-118">다음 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-118">You can use the following parameters:</span></span>

| <span data-ttu-id="a9eb2-119">이름</span><span class="sxs-lookup"><span data-stu-id="a9eb2-119">Name</span></span> | <span data-ttu-id="a9eb2-120">옵션</span><span class="sxs-lookup"><span data-stu-id="a9eb2-120">Options</span></span> | <span data-ttu-id="a9eb2-121">설명</span><span class="sxs-lookup"><span data-stu-id="a9eb2-121">Description</span></span> | <span data-ttu-id="a9eb2-122">기본값</span><span class="sxs-lookup"><span data-stu-id="a9eb2-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9eb2-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="a9eb2-123">sensitivityLevel</span></span> |<span data-ttu-id="a9eb2-124">문자열:'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="a9eb2-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="a9eb2-125">동작이 보고되는 민감도 수준을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="a9eb2-126">가양성의 양을 조정할 때 이 값을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="a9eb2-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="a9eb2-127">'medium'</span></span> |
| <span data-ttu-id="a9eb2-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="a9eb2-128">frameSamplingValue</span></span> |<span data-ttu-id="a9eb2-129">양의 정수</span><span class="sxs-lookup"><span data-stu-id="a9eb2-129">Positive integer</span></span> |<span data-ttu-id="a9eb2-130">알고리즘이 실행되는 빈도를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="a9eb2-131">1은 프레임마다, 2는 두 번째 프레임마다 등을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="a9eb2-132">1</span><span class="sxs-lookup"><span data-stu-id="a9eb2-132">1</span></span> |
| <span data-ttu-id="a9eb2-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="a9eb2-133">detectLightChange</span></span> |<span data-ttu-id="a9eb2-134">부울:'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="a9eb2-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="a9eb2-135">결과에 간단한 변경 내용이 보고되는지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="a9eb2-136">'False'</span><span class="sxs-lookup"><span data-stu-id="a9eb2-136">'False'</span></span> |
| <span data-ttu-id="a9eb2-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="a9eb2-137">mergeTimeThreshold</span></span> |<span data-ttu-id="a9eb2-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="a9eb2-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="a9eb2-139">예: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="a9eb2-139">Example: 00:00:03</span></span> |<span data-ttu-id="a9eb2-140">두 개의 이벤트가 결합되어 1로 보고되는 동작 이벤트 간의 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="a9eb2-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="a9eb2-141">00:00:00</span></span> |
| <span data-ttu-id="a9eb2-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="a9eb2-142">detectionZones</span></span> |<span data-ttu-id="a9eb2-143">검색 영역 배열:</span><span class="sxs-lookup"><span data-stu-id="a9eb2-143">An array of detection zones:</span></span><br/><span data-ttu-id="a9eb2-144">- 검색 영역은 3개 이상의 지점 배열</span><span class="sxs-lookup"><span data-stu-id="a9eb2-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="a9eb2-145">- 지점은 0부터 1까지의 x 및 y 좌표입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="a9eb2-146">사용할 다각형의 검색 영역 목록을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="a9eb2-147">결과는 영역과 함께 ID로 보고되며 첫 번째 항목은 'id':0입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="a9eb2-148">전체 프레임에 걸쳐 있는 단일 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="a9eb2-149">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="a9eb2-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="a9eb2-150">동작 검색기 출력 파일</span><span class="sxs-lookup"><span data-stu-id="a9eb2-150">Motion Detector output files</span></span>
<span data-ttu-id="a9eb2-151">동작 검색 작업은 동작 경고 및 동영상 내에서의 해당 범주를 설명하는 출력 자산으로 JSON 파일을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="a9eb2-152">파일에는 동영상에서 검색된 동작 시간 및 기간에 대한 정보가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="a9eb2-153">동작 탐지기 API는 고정된 배경의 동영상에 움직이는 개체가 있는 경우 표시기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="a9eb2-154">동작 탐지기는 조명 및 그림자 변화와 같은 가양성을 줄이기 위해 학습됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="a9eb2-155">현재 알고리즘의 한계로 야간 투시 동영상, 반투명 개체 및 작은 개체가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="a9eb2-156"><a id="output_elements"></a>출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="a9eb2-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="a9eb2-157">최신 릴리스에서는 출력 JSON 형식이 변경되었으며 일부 고객에게는 큰 변화로 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="a9eb2-158">다음 표는 출력 JSON 파일의 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="a9eb2-159">요소</span><span class="sxs-lookup"><span data-stu-id="a9eb2-159">Element</span></span> | <span data-ttu-id="a9eb2-160">설명</span><span class="sxs-lookup"><span data-stu-id="a9eb2-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9eb2-161">버전</span><span class="sxs-lookup"><span data-stu-id="a9eb2-161">Version</span></span> |<span data-ttu-id="a9eb2-162">동영상 API의 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="a9eb2-163">현재 버전은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-163">The current version is 2.</span></span> |
| <span data-ttu-id="a9eb2-164">시간 간격</span><span class="sxs-lookup"><span data-stu-id="a9eb2-164">Timescale</span></span> |<span data-ttu-id="a9eb2-165">동영상의 초당 "틱"입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="a9eb2-166">Offset</span><span class="sxs-lookup"><span data-stu-id="a9eb2-166">Offset</span></span> |<span data-ttu-id="a9eb2-167">"틱" 단위의 타임스탬프에 대한 시간 오프셋입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="a9eb2-168">동영상 API 버전 1.0에서는 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="a9eb2-169">향후 지원하는 시나리오에서는 이 값이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="a9eb2-170">프레임 속도</span><span class="sxs-lookup"><span data-stu-id="a9eb2-170">Framerate</span></span> |<span data-ttu-id="a9eb2-171">동영상의 초당 프레임 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="a9eb2-172">너비, 높이</span><span class="sxs-lookup"><span data-stu-id="a9eb2-172">Width, Height</span></span> |<span data-ttu-id="a9eb2-173">픽셀 단위의 동영상 너비와 높이를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="a9eb2-174">시작</span><span class="sxs-lookup"><span data-stu-id="a9eb2-174">Start</span></span> |<span data-ttu-id="a9eb2-175">"틱" 단위의 시작 타임스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="a9eb2-176">기간</span><span class="sxs-lookup"><span data-stu-id="a9eb2-176">Duration</span></span> |<span data-ttu-id="a9eb2-177">"틱" 단위의 이벤트 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="a9eb2-178">간격</span><span class="sxs-lookup"><span data-stu-id="a9eb2-178">Interval</span></span> |<span data-ttu-id="a9eb2-179">"틱" 단위의 이벤트에 있는 각 항목의 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="a9eb2-180">이벤트</span><span class="sxs-lookup"><span data-stu-id="a9eb2-180">Events</span></span> |<span data-ttu-id="a9eb2-181">각 이벤트 조각에는 해당 기간 내에 검색된 동작이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="a9eb2-182">형식</span><span class="sxs-lookup"><span data-stu-id="a9eb2-182">Type</span></span> |<span data-ttu-id="a9eb2-183">현재 버전에서 이 값은 일반 동작에 대해 항상 '2'입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="a9eb2-184">이 레이블은 향후 버전에서 동영상 API에 동작 분류에 대한 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="a9eb2-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="a9eb2-185">RegionID</span></span> |<span data-ttu-id="a9eb2-186">위에서 설명했듯이 이 버전에서 이 값은 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="a9eb2-187">이 레이블은 향후 버전에서 동영상 API에 다양한 영역에서 동작을 찾는 유연성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="a9eb2-188">영역</span><span class="sxs-lookup"><span data-stu-id="a9eb2-188">Regions</span></span> |<span data-ttu-id="a9eb2-189">동작에 관심이 있는 동영상 영역을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="a9eb2-190">-"id"는 지역 영역을 나타내는데, 이 버전에는 ID 0밖에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="a9eb2-191">-"type"은 동작에 대한 중요한 영역 모양을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="a9eb2-192">현재 "rectangle" 및 "polygon"이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="a9eb2-193">"rectangle"이 지정된 경우 영역은 X, Y, 너비 및 높이 치수를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="a9eb2-194">X 및 Y 좌표는 0.0 ~ 1.0의 정규화된 배율 단위로 영역의 왼쪽 상단 XY 좌표를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="a9eb2-195">너비와 높이는 0.0 ~ 1.0의 정규화된 배율 단위로 영역의 크기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="a9eb2-196">현재 버전에서, X, Y, 너비 및 높이는 0, 0 및 1, 1로 항상 고정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="a9eb2-197">"polygon"이 지정된 경우 영역은 지점 단위의 치수를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="a9eb2-198">조각</span><span class="sxs-lookup"><span data-stu-id="a9eb2-198">Fragments</span></span> |<span data-ttu-id="a9eb2-199">메타데이터는 조각이라고 하는 다른 세그먼트로 청크 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="a9eb2-200">각 조각에는 시작, 기간, 간격 번호 및 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="a9eb2-201">이벤트가 없는 조각은 해당 시작 시간 및 기간 동안에 검색된 동작이 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="a9eb2-202">대괄호 []</span><span class="sxs-lookup"><span data-stu-id="a9eb2-202">Brackets []</span></span> |<span data-ttu-id="a9eb2-203">각 대괄호는 이벤트에서 하나의 간격을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="a9eb2-204">해당 간격에 대한 빈 대괄호는 검색된 동작이 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="a9eb2-205">위치</span><span class="sxs-lookup"><span data-stu-id="a9eb2-205">locations</span></span> |<span data-ttu-id="a9eb2-206">이벤트 아래의 이 새 항목은 동작이 발생한 위치를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="a9eb2-207">검색 영역보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="a9eb2-208">다음은 JSON 출력 예입니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="a9eb2-209">제한 사항</span><span class="sxs-lookup"><span data-stu-id="a9eb2-209">Limitations</span></span>
* <span data-ttu-id="a9eb2-210">지원되는 입력 동영상 형식에는 MP4, MOV 및 WMV가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="a9eb2-211">동작 검색은 고정 배경 동영상에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="a9eb2-212">알고리즘은 조명 변화, 그림자와 같은 거짓 경보를 줄이는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="a9eb2-213">일부 동작은 기술적인 문제(예: 야간 투시 동영상, 반투명 개체 및 작은 개체)로 인해 검색되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="a9eb2-214">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="a9eb2-214">.NET sample code</span></span>

<span data-ttu-id="a9eb2-215">다음 프로그램은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-215">The following program shows how to:</span></span>

1. <span data-ttu-id="a9eb2-216">자산을 만들고 미디어 파일을 자산에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="a9eb2-217">다음 json 사전 설정을 포함하는 구성 파일을 기반으로 비디오 동작 탐지 태스크가 포함된 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="a9eb2-218">출력 JSON 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a9eb2-219">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="a9eb2-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a9eb2-220">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="a9eb2-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a9eb2-221">예제</span><span class="sxs-lookup"><span data-stu-id="a9eb2-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="a9eb2-222">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="a9eb2-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9eb2-223">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a9eb2-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="a9eb2-224">관련 링크</span><span class="sxs-lookup"><span data-stu-id="a9eb2-224">Related links</span></span>
[<span data-ttu-id="a9eb2-225">Azure 미디어 서비스 동작 탐지기 블로그</span><span class="sxs-lookup"><span data-stu-id="a9eb2-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="a9eb2-226">Azure 미디어 서비스 분석 개요</span><span class="sxs-lookup"><span data-stu-id="a9eb2-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="a9eb2-227">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="a9eb2-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

