---
title: "Azure 미디어 분석으로 얼굴 편집 | Microsoft Docs"
description: "이 항목에서는 Azure Media Analytics로 얼굴을 편집하는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 747f3ae1a7484515083c590942de3da22568cd39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="0b596-103">Azure 미디어 분석으로 얼굴 편집</span><span class="sxs-lookup"><span data-stu-id="0b596-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="0b596-104">개요</span><span class="sxs-lookup"><span data-stu-id="0b596-104">Overview</span></span>
<span data-ttu-id="0b596-105">**Azure Media Redactor** 는 클라우드에서 확장성 있는 얼굴 편집 기능을 제공하는 [Azure Media Analytics](media-services-analytics-overview.md) MP(미디어 프로세서)입니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="0b596-106">얼굴 편집을 사용하면 선택한 개인의 얼굴을 흐리게 표시하기 위해 동영상을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="0b596-107">공공 안전과 새 미디어 시나리오를 위해 얼굴 편집 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="0b596-108">짧은 장면이라도 여러 명의 얼굴이 포함된 경우 수동으로 편집하려면 많은 시간이 걸릴 수 있지만 이 서비스를 사용하면 몇 번의 간단한 단계를 통해 얼굴을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="0b596-109">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b596-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="0b596-110">이 항목은 **Azure Media Redactor** 에 대한 세부 정보 및 .NET용 Media Services SDK와 함께 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-110">This topic gives details about **Azure Media Redactor** and shows how to use it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="0b596-111">**Azure Media Redactor** MP는 현재 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-111">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="0b596-112">이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="0b596-113">이 미리 보기는 현재 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="0b596-114">얼굴 편집 모드</span><span class="sxs-lookup"><span data-stu-id="0b596-114">Face redaction modes</span></span>
<span data-ttu-id="0b596-115">얼굴 편집은 동일한 개인이 다른 각도에서도 흐리게 표시될 수 있도록 동영상의 모든 프레임에서 얼굴을 감지하고 앞뒤 시간의 얼굴 개체를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-115">Facial redaction works by detecting faces in every frame of video and tracking the face object both forwards and backwards in time, so that the same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="0b596-116">자동 편집 프로세스는 매우 복잡하여 항상 원하는 결과가 100% 생성되지는 않습니다. 따라서 Media Analytics는 최종 결과를 수정하기 위한 몇 가지 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-116">The automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways to modify the final output.</span></span>

<span data-ttu-id="0b596-117">완전 자동 모드 외에, ID 목록을 통해 검색한 얼굴을 선택/선택 취소할 수 있는 2단계 워크플로가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-117">In addition to a fully automatic mode, there is a two-pass workflow which allows the selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="0b596-118">또한 MP는 프레임별 임의 조정을 위해 JSON 형식의 메타데이터 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-118">Also, to make arbitrary per frame adjustments the MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="0b596-119">이 워크플로는 **분석** 및 **편집** 모드로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="0b596-120">두 모드를 하나의 작업에서 두 작업을 실행하는 단일 단계로 결합할 수 있습니다. 이러한 모드를 **결합된** 모드라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-120">You can combine the two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="0b596-121">결합된 모드</span><span class="sxs-lookup"><span data-stu-id="0b596-121">Combined mode</span></span>
<span data-ttu-id="0b596-122">이 모드는 수동 입력 없이 자동으로 편집된 mp4를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="0b596-123">단계</span><span class="sxs-lookup"><span data-stu-id="0b596-123">Stage</span></span> | <span data-ttu-id="0b596-124">파일 이름</span><span class="sxs-lookup"><span data-stu-id="0b596-124">File Name</span></span> | <span data-ttu-id="0b596-125">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0b596-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b596-126">입력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-126">Input asset</span></span> |<span data-ttu-id="0b596-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0b596-127">foo.bar</span></span> |<span data-ttu-id="0b596-128">WMV, MOV 또는 MP4 형식의 동영상</span><span class="sxs-lookup"><span data-stu-id="0b596-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="0b596-129">입력 구성</span><span class="sxs-lookup"><span data-stu-id="0b596-129">Input config</span></span> |<span data-ttu-id="0b596-130">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="0b596-130">Job configuration preset</span></span> |<span data-ttu-id="0b596-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="0b596-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="0b596-132">출력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-132">Output asset</span></span> |<span data-ttu-id="0b596-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="0b596-133">foo_redacted.mp4</span></span> |<span data-ttu-id="0b596-134">흐리게 표시하기가 적용된 동영상</span><span class="sxs-lookup"><span data-stu-id="0b596-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="0b596-135">입력 예:</span><span class="sxs-lookup"><span data-stu-id="0b596-135">Input example:</span></span>
[<span data-ttu-id="0b596-136">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b596-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="0b596-137">출력 예제:</span><span class="sxs-lookup"><span data-stu-id="0b596-137">Output example:</span></span>
[<span data-ttu-id="0b596-138">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b596-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="0b596-139">분석 모드</span><span class="sxs-lookup"><span data-stu-id="0b596-139">Analyze mode</span></span>
<span data-ttu-id="0b596-140">2단계 워크플로의 **분석** 단계는 동영상 입력을 사용하여 얼굴 위치의 JSON 파일과 검색된 각 얼굴의 jpg 이미지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-140">The **analyze** pass of the two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="0b596-141">단계</span><span class="sxs-lookup"><span data-stu-id="0b596-141">Stage</span></span> | <span data-ttu-id="0b596-142">파일 이름</span><span class="sxs-lookup"><span data-stu-id="0b596-142">File Name</span></span> | <span data-ttu-id="0b596-143">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0b596-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b596-144">입력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-144">Input asset</span></span> |<span data-ttu-id="0b596-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0b596-145">foo.bar</span></span> |<span data-ttu-id="0b596-146">WMV, MPV 또는 MP4 형식의 동영상</span><span class="sxs-lookup"><span data-stu-id="0b596-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="0b596-147">입력 구성</span><span class="sxs-lookup"><span data-stu-id="0b596-147">Input config</span></span> |<span data-ttu-id="0b596-148">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="0b596-148">Job configuration preset</span></span> |<span data-ttu-id="0b596-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="0b596-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="0b596-150">출력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-150">Output asset</span></span> |<span data-ttu-id="0b596-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="0b596-151">foo_annotations.json</span></span> |<span data-ttu-id="0b596-152">얼굴 위치의 주석 데이터(JSON 형식).</span><span class="sxs-lookup"><span data-stu-id="0b596-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="0b596-153">사용자가 흐리게 표시하는 테두리 상자를 수정하기 위해 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-153">This can be edited by the user to modify the blurring bounding boxes.</span></span> <span data-ttu-id="0b596-154">아래 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b596-154">See sample below.</span></span> |
| <span data-ttu-id="0b596-155">출력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-155">Output asset</span></span> |<span data-ttu-id="0b596-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="0b596-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="0b596-157">검색된 각 얼굴을 잘라낸 jpg(숫자는 얼굴의 레이블 ID)</span><span class="sxs-lookup"><span data-stu-id="0b596-157">A cropped jpg of each detected face, where the number indicates the labelId of the face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="0b596-158">출력 예제:</span><span class="sxs-lookup"><span data-stu-id="0b596-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="0b596-159">편집 모드</span><span class="sxs-lookup"><span data-stu-id="0b596-159">Redact mode</span></span>
<span data-ttu-id="0b596-160">워크플로의 두 번째 단계에서는 하나의 자산으로 결합해야 하는 여러 입력을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-160">The second pass of the workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="0b596-161">여기에는 흐리게 표시할 ID 목록, 원본 동영상 및 주석 JSON이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-161">This includes a list of IDs to blur, the original video, and the annotations JSON.</span></span> <span data-ttu-id="0b596-162">이 모드에서는 주석을 사용하여 입력 동영상에 흐리게 표시를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-162">This mode uses the annotations to apply blurring on the input video.</span></span>

<span data-ttu-id="0b596-163">분석 단계의 출력에는 원본 동영상이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-163">The output from the Analyze pass does not include the original video.</span></span> <span data-ttu-id="0b596-164">동영상을 편집 모드 작업의 입력 자산으로 업로드하고 기본 파일로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-164">The video needs to be uploaded into the input asset for the Redact mode task and selected as the primary file.</span></span>

| <span data-ttu-id="0b596-165">단계</span><span class="sxs-lookup"><span data-stu-id="0b596-165">Stage</span></span> | <span data-ttu-id="0b596-166">파일 이름</span><span class="sxs-lookup"><span data-stu-id="0b596-166">File Name</span></span> | <span data-ttu-id="0b596-167">참고 사항</span><span class="sxs-lookup"><span data-stu-id="0b596-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b596-168">입력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-168">Input asset</span></span> |<span data-ttu-id="0b596-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="0b596-169">foo.bar</span></span> |<span data-ttu-id="0b596-170">WMV, MPV 또는 MP4 형식의 동영상.</span><span class="sxs-lookup"><span data-stu-id="0b596-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="0b596-171">1단계와 동일한 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="0b596-172">입력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-172">Input asset</span></span> |<span data-ttu-id="0b596-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="0b596-173">foo_annotations.json</span></span> |<span data-ttu-id="0b596-174">1단계의 주석 메타데이터 파일 및 수정 사항(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="0b596-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="0b596-175">입력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-175">Input asset</span></span> |<span data-ttu-id="0b596-176">foo_IDList.txt(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="0b596-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="0b596-177">줄로 구분된 편집할 얼굴 ID의 새 목록(선택 사항).</span><span class="sxs-lookup"><span data-stu-id="0b596-177">Optional new line separated list of face IDs to redact.</span></span> <span data-ttu-id="0b596-178">지정하지 않으면 모든 얼굴이 흐리게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="0b596-179">입력 구성</span><span class="sxs-lookup"><span data-stu-id="0b596-179">Input config</span></span> |<span data-ttu-id="0b596-180">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="0b596-180">Job configuration preset</span></span> |<span data-ttu-id="0b596-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="0b596-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="0b596-182">출력 자산</span><span class="sxs-lookup"><span data-stu-id="0b596-182">Output asset</span></span> |<span data-ttu-id="0b596-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="0b596-183">foo_redacted.mp4</span></span> |<span data-ttu-id="0b596-184">주석을 기반으로 흐리게 표시하기가 적용된 동영상</span><span class="sxs-lookup"><span data-stu-id="0b596-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="0b596-185">예제 출력</span><span class="sxs-lookup"><span data-stu-id="0b596-185">Example output</span></span>
<span data-ttu-id="0b596-186">IDList에서 하나의 ID가 선택된 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-186">This is the output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="0b596-187">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="0b596-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="0b596-188">예제 foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="0b596-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="0b596-189">흐리게 형식</span><span class="sxs-lookup"><span data-stu-id="0b596-189">Blur types</span></span>

<span data-ttu-id="0b596-190">**결합** 또는 **편집** 모드에는 JSON 입력 구성을 통해 선택할 수 있는 5가지 흐리게 모드가 있습니다(**낮음**, **중간**, **높음**, **디버그** 및 **검정**).</span><span class="sxs-lookup"><span data-stu-id="0b596-190">In the **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via the JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="0b596-191">기본적으로 **중간**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-191">By default **Med** is used.</span></span>

<span data-ttu-id="0b596-192">아래에 흐리게 형식의 샘플을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-192">You can find samples of the blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="0b596-193">예제 JSON:</span><span class="sxs-lookup"><span data-stu-id="0b596-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="0b596-194">낮음</span><span class="sxs-lookup"><span data-stu-id="0b596-194">Low</span></span>

![낮음](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="0b596-196">중간</span><span class="sxs-lookup"><span data-stu-id="0b596-196">Med</span></span>

![중간](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="0b596-198">높음</span><span class="sxs-lookup"><span data-stu-id="0b596-198">High</span></span>

![높음](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="0b596-200">디버그</span><span class="sxs-lookup"><span data-stu-id="0b596-200">Debug</span></span>

![디버그](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="0b596-202">검정</span><span class="sxs-lookup"><span data-stu-id="0b596-202">Black</span></span>

![검정](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-the-output-json-file"></a><span data-ttu-id="0b596-204">출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="0b596-204">Elements of the output JSON file</span></span>

<span data-ttu-id="0b596-205">편집 MP는 한 동영상 프레임 내에서 최대 64명의 얼굴을 검색할 수 있는 고정밀도 얼굴 위치 검색 및 추적을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-205">The Redaction MP provides high precision face location detection and tracking that can detect up to 64 human faces in a video frame.</span></span> <span data-ttu-id="0b596-206">정면이 최상의 결과를 제공하며 측면 또는 작은 얼굴(24x24 픽셀보다 작거나 같음)의 경우에는 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-206">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="0b596-207">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="0b596-207">.NET sample code</span></span>

<span data-ttu-id="0b596-208">다음 프로그램은 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-208">The following program shows how to:</span></span>

1. <span data-ttu-id="0b596-209">자산을 만들고 미디어 파일을 자산에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-209">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="0b596-210">다음 json 기본 설정을 포함하는 구성 파일을 기반으로 얼굴 편집 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-210">Create a job with a face redaction task based on a configuration file that contains the following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="0b596-211">출력 JSON 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-211">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="0b596-212">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="0b596-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="0b596-213">개발 환경을 설정하고 [.NET을 사용한 Media Services 환경](media-services-dotnet-how-to-use.md)에 설명된 대로 연결 정보를 사용하여 app.config 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="0b596-213">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="0b596-214">예제</span><span class="sxs-lookup"><span data-stu-id="0b596-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
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

            // Run the FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download the job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload the input media file to storage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference to Azure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from the specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with the encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify the input asset.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="0b596-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b596-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0b596-216">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="0b596-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="0b596-217">관련 링크</span><span class="sxs-lookup"><span data-stu-id="0b596-217">Related links</span></span>
[<span data-ttu-id="0b596-218">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="0b596-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="0b596-219">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="0b596-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

