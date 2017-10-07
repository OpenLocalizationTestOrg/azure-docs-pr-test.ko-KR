---
title: "Azure 미디어 분석을 aaaDetect 동작 | Microsoft Docs"
description: "hello Azure 미디어 동작 탐지기 미디어 프로세서 (MP) 사용 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="403ba-103">Azure 미디어 검색으로 동작 검색</span><span class="sxs-lookup"><span data-stu-id="403ba-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="403ba-104">개요</span><span class="sxs-lookup"><span data-stu-id="403ba-104">Overview</span></span>
<span data-ttu-id="403ba-105">hello **Azure 미디어 동작 탐지기** 미디어 프로세서 (MP) 사용 하도록 설정 하면 tooefficiently 그렇지 않으면 길고 정상적인 비디오 내에서 필요한 섹션을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="403ba-106">동작 감지 동작 발생 hello 비디오의 정적 카메라 장면 tooidentify 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="403ba-107">타임 스탬프 및 hello hello 이벤트가 발생 하는 영역 경계와 메타 데이터를 포함 하는 JSON 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="403ba-108">이 기술은 보안 비디오 피드를 겨냥 수 toocategorize 동작 관련 이벤트 및 거짓 긍정 그림자 조명 변경 등으로입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="403ba-109">이렇게 하면 있습니다 카메라 피드에서 toogenerate 보안 경고 수 tooextract 시간이 매우 긴 거리 내 감시 비디오에서 관심 있는 하면서 무한 관련이 없는 이벤트로 스팸 메일 되지 않고.</span><span class="sxs-lookup"><span data-stu-id="403ba-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="403ba-110">hello **Azure 미디어 동작 탐지기** MP는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="403ba-111">이 항목에 대 한 세부 정보를 제공 **Azure 미디어 동작 탐지기** 표시 방법을 toouse Media Services SDK for.NET으로</span><span class="sxs-lookup"><span data-stu-id="403ba-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="403ba-112">동작 검색기 입력 파일</span><span class="sxs-lookup"><span data-stu-id="403ba-112">Motion Detector input files</span></span>
<span data-ttu-id="403ba-113">동영상 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-113">Video files.</span></span> <span data-ttu-id="403ba-114">현재 형식에 따라 hello 지원 됩니다: MP4, MOV, 및 WMV입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="403ba-115">작업 구성(기본 설정)</span><span class="sxs-lookup"><span data-stu-id="403ba-115">Task configuration (preset)</span></span>
<span data-ttu-id="403ba-116">**Azure 미디어 동작 탐지기**로 작업을 만들 때에는 구성 기본 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="403ba-117">매개 변수</span><span class="sxs-lookup"><span data-stu-id="403ba-117">Parameters</span></span>
<span data-ttu-id="403ba-118">Hello 매개 변수 뒤에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="403ba-119">이름</span><span class="sxs-lookup"><span data-stu-id="403ba-119">Name</span></span> | <span data-ttu-id="403ba-120">옵션</span><span class="sxs-lookup"><span data-stu-id="403ba-120">Options</span></span> | <span data-ttu-id="403ba-121">설명</span><span class="sxs-lookup"><span data-stu-id="403ba-121">Description</span></span> | <span data-ttu-id="403ba-122">기본값</span><span class="sxs-lookup"><span data-stu-id="403ba-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="403ba-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="403ba-123">sensitivityLevel</span></span> |<span data-ttu-id="403ba-124">문자열:'low', 'medium', 'high'</span><span class="sxs-lookup"><span data-stu-id="403ba-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="403ba-125">보고 되는 동작에 수준 hello 민감도 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="403ba-126">거짓 긍정이 tooadjust 시간을 조정 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="403ba-127">'medium'</span><span class="sxs-lookup"><span data-stu-id="403ba-127">'medium'</span></span> |
| <span data-ttu-id="403ba-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="403ba-128">frameSamplingValue</span></span> |<span data-ttu-id="403ba-129">양의 정수</span><span class="sxs-lookup"><span data-stu-id="403ba-129">Positive integer</span></span> |<span data-ttu-id="403ba-130">어떤 알고리즘 실행에 hello 주파수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="403ba-131">1은 프레임마다, 2는 두 번째 프레임마다 등을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="403ba-132">1</span><span class="sxs-lookup"><span data-stu-id="403ba-132">1</span></span> |
| <span data-ttu-id="403ba-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="403ba-133">detectLightChange</span></span> |<span data-ttu-id="403ba-134">부울:'true', 'false'</span><span class="sxs-lookup"><span data-stu-id="403ba-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="403ba-135">Hello 결과에 밝은 변경 내용을 보고 있는지 여부를 설정합니다</span><span class="sxs-lookup"><span data-stu-id="403ba-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="403ba-136">'False'</span><span class="sxs-lookup"><span data-stu-id="403ba-136">'False'</span></span> |
| <span data-ttu-id="403ba-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="403ba-137">mergeTimeThreshold</span></span> |<span data-ttu-id="403ba-138">Xs-time: Hh:mm:ss</span><span class="sxs-lookup"><span data-stu-id="403ba-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="403ba-139">예: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="403ba-139">Example: 00:00:03</span></span> |<span data-ttu-id="403ba-140">동작 이벤트 2 이벤트가 결합 및 1로 보고 하려는 hello 시간 창을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="403ba-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="403ba-141">00:00:00</span></span> |
| <span data-ttu-id="403ba-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="403ba-142">detectionZones</span></span> |<span data-ttu-id="403ba-143">검색 영역 배열:</span><span class="sxs-lookup"><span data-stu-id="403ba-143">An array of detection zones:</span></span><br/><span data-ttu-id="403ba-144">- 검색 영역은 3개 이상의 지점 배열</span><span class="sxs-lookup"><span data-stu-id="403ba-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="403ba-145">-점은 x 및 y 좌표 0 too1에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="403ba-146">사용 되는 다각형 검색 영역 toobe hello 목록에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="403ba-147">첫 번째 되 고 'id' hello로 한 ID로 결과 hello 영역으로 보고 됩니다: 0</span><span class="sxs-lookup"><span data-stu-id="403ba-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="403ba-148">단일 5d; 영역 hello 전체 프레임에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="403ba-149">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="403ba-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="403ba-150">동작 검색기 출력 파일</span><span class="sxs-lookup"><span data-stu-id="403ba-150">Motion Detector output files</span></span>
<span data-ttu-id="403ba-151">동작 검색 작업은 hello 동작 경고와 hello 비디오 내에서 해당 범주를 설명 하는 hello 출력 자산에는 JSON 파일을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="403ba-152">hello 파일에는 hello 시간과 기간, hello 비디오에서 검색 하는 동작에 대 한 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="403ba-153">동작에서 개체는 고정된 백그라운드에서 비디오 (예: 한 거리 내 감시 비디오) 되 면 hello 모션 탐지기 API 표시기를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="403ba-154">hello 동작 탐지기는 학습 된 tooreduce 거짓 경보 조명 섀도 변경 등입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="403ba-155">Hello 알고리즘의 현재 제한 사항 밤 비전 비디오, 반투명 개체 및 작은 개체를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="403ba-156"><a id="output_elements"></a>Hello 출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="403ba-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="403ba-157">Hello 최신 릴리스에서 hello JSON 출력 형식 변경 되었으며이 일부 고객에 대 한 주요 변경 내용를 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="403ba-158">hello 다음 설명 hello 출력 JSON 파일의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="403ba-159">요소</span><span class="sxs-lookup"><span data-stu-id="403ba-159">Element</span></span> | <span data-ttu-id="403ba-160">설명</span><span class="sxs-lookup"><span data-stu-id="403ba-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="403ba-161">버전</span><span class="sxs-lookup"><span data-stu-id="403ba-161">Version</span></span> |<span data-ttu-id="403ba-162">이 hello 비디오 API의 toohello 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="403ba-163">hello 현재 버전은 2입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-163">hello current version is 2.</span></span> |
| <span data-ttu-id="403ba-164">시간 간격</span><span class="sxs-lookup"><span data-stu-id="403ba-164">Timescale</span></span> |<span data-ttu-id="403ba-165">"틱" hello 비디오의 초 당 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="403ba-166">Offset</span><span class="sxs-lookup"><span data-stu-id="403ba-166">Offset</span></span> |<span data-ttu-id="403ba-167">"틱"의 타임 스탬프에 대 한 hello 시간 오프셋입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="403ba-168">동영상 API 버전 1.0에서는 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="403ba-169">향후 지원하는 시나리오에서는 이 값이 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="403ba-170">프레임 속도</span><span class="sxs-lookup"><span data-stu-id="403ba-170">Framerate</span></span> |<span data-ttu-id="403ba-171">Hello 비디오의 초당 프레임 수입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="403ba-172">너비, 높이</span><span class="sxs-lookup"><span data-stu-id="403ba-172">Width, Height</span></span> |<span data-ttu-id="403ba-173">픽셀 단위로 비디오 hello의 toohello 너비와 높이 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="403ba-174">시작</span><span class="sxs-lookup"><span data-stu-id="403ba-174">Start</span></span> |<span data-ttu-id="403ba-175">hello "틱"의 타임 스탬프를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="403ba-176">기간</span><span class="sxs-lookup"><span data-stu-id="403ba-176">Duration</span></span> |<span data-ttu-id="403ba-177">"틱" hello 이벤트의 hello 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="403ba-178">간격</span><span class="sxs-lookup"><span data-stu-id="403ba-178">Interval</span></span> |<span data-ttu-id="403ba-179">hello 이벤트 "틱"에 있는 각 항목의 hello 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="403ba-180">이벤트</span><span class="sxs-lookup"><span data-stu-id="403ba-180">Events</span></span> |<span data-ttu-id="403ba-181">각 이벤트 조각 해당 기간 내에서 검색 하는 hello 동작을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="403ba-182">형식</span><span class="sxs-lookup"><span data-stu-id="403ba-182">Type</span></span> |<span data-ttu-id="403ba-183">Hello 현재 버전에서는 이것이 항상 일반 동작에 대 한 ' 2'입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="403ba-184">이 레이블은 이후 버전에서 비디오 Api hello 유연성 toocategorize 동작을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="403ba-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="403ba-185">RegionID</span></span> |<span data-ttu-id="403ba-186">위에서 설명했듯이 이 버전에서 이 값은 항상 0입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="403ba-187">이 레이블은 이후 버전에서는 다양 한 지역에 비디오 API hello 유연성 toofind 동작을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="403ba-188">영역</span><span class="sxs-lookup"><span data-stu-id="403ba-188">Regions</span></span> |<span data-ttu-id="403ba-189">동작에 대 한 관심이 비디오에서 toohello 영역을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="403ba-190">-"id" hello 영역 영역을 나타내는 –이 버전에는 하나의 ID가 0입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="403ba-191">-"type" 동작에 대 한 중요 한 hello 영역의 hello 셰이프를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="403ba-192">현재 "rectangle" 및 "polygon"이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="403ba-193">"사각형"를 지정한 경우 hello 영역 차원이 x, Y, 너비 및 높이입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="403ba-194">hello X 및 Y 좌표 0.0 too1.0의 정규화 된 소수에 hello 영역의 hello 왼쪽 위 XY 좌표를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="403ba-195">hello 너비와 높이 0.0 too1.0의 정규화 된 소수에 hello 영역의 hello 크기를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="403ba-196">Hello 현재 버전, X, Y, 너비 및 높이 0, 0 및 1, 1로 고정 항상 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="403ba-197">"다각형"를 지정한 경우에 hello 지역은 포인트에서 차원이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="403ba-198">조각</span><span class="sxs-lookup"><span data-stu-id="403ba-198">Fragments</span></span> |<span data-ttu-id="403ba-199">hello 메타 데이터를 조각 이라고 하는 서로 다른 세그먼트에 청크 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="403ba-200">각 조각에는 시작, 기간, 간격 번호 및 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="403ba-201">이벤트가 없는 조각은 해당 시작 시간 및 기간 동안에 검색된 동작이 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="403ba-202">대괄호 []</span><span class="sxs-lookup"><span data-stu-id="403ba-202">Brackets []</span></span> |<span data-ttu-id="403ba-203">각 괄호 hello 이벤트에서 하나의 간격을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="403ba-204">해당 간격에 대한 빈 대괄호는 검색된 동작이 없음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="403ba-205">위치</span><span class="sxs-lookup"><span data-stu-id="403ba-205">locations</span></span> |<span data-ttu-id="403ba-206">이벤트에서이 새 항목 hello 동작 발생 한 hello 위치를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="403ba-207">Hello 검색 영역 보다 더 구체적입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="403ba-208">hello 다음은 JSON의 출력 예</span><span class="sxs-lookup"><span data-stu-id="403ba-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="403ba-209">제한 사항</span><span class="sxs-lookup"><span data-stu-id="403ba-209">Limitations</span></span>
* <span data-ttu-id="403ba-210">입력된 비디오 형식을 지원 hello MP4, MOV, 및 WMV 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="403ba-211">동작 검색은 고정 배경 동영상에 최적화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="403ba-212">hello 알고리즘 조명 변경 내용, 그림자 등에 등 거짓 경보를 단축에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="403ba-213">Tootechnical 과제; 인해 일부 동작을 검색할 수 없습니다. 예를 들어 밤 비전 비디오, 반투명 개체 및 작은 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="403ba-214">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="403ba-214">.NET sample code</span></span>

<span data-ttu-id="403ba-215">hello 다음 프로그램 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="403ba-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="403ba-216">자산 만들기 hello 자산 미디어 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="403ba-217">다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 비디오 동작 검색 작업으로 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="403ba-218">Hello 출력 JSON 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="403ba-219">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="403ba-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="403ba-220">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="403ba-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="403ba-221">예제</span><span class="sxs-lookup"><span data-stu-id="403ba-221">Example</span></span>


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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="403ba-222">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="403ba-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="403ba-223">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="403ba-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="403ba-224">관련 링크</span><span class="sxs-lookup"><span data-stu-id="403ba-224">Related links</span></span>
[<span data-ttu-id="403ba-225">Azure 미디어 서비스 동작 탐지기 블로그</span><span class="sxs-lookup"><span data-stu-id="403ba-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="403ba-226">Azure 미디어 서비스 분석 개요</span><span class="sxs-lookup"><span data-stu-id="403ba-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="403ba-227">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="403ba-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

