---
title: "Azure 미디어 분석을 aaaRedact 면 | Microsoft Docs"
description: "이 항목에서는 Azure 미디어 analytics와 tooredact 직면 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="fc05f-103">Azure 미디어 분석으로 얼굴 편집</span><span class="sxs-lookup"><span data-stu-id="fc05f-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="fc05f-104">개요</span><span class="sxs-lookup"><span data-stu-id="fc05f-104">Overview</span></span>
<span data-ttu-id="fc05f-105">**Azure 미디어 Redactor** 는 [Azure 미디어 분석](media-services-analytics-overview.md) hello 클라우드에서 확장 가능한 글꼴 교정에서 제공 하는 미디어 프로세서 (MP).</span><span class="sxs-lookup"><span data-stu-id="fc05f-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="fc05f-106">Face 교정 있습니다 toomodify 선택한 개인의 순서 tooblur 면에서 비디오를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="fc05f-107">공용 안전과 뉴스 미디어 시나리오에서 toouse hello 얼굴 교정 서비스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="fc05f-108">몇 분 정도 여러 글꼴로 포함 된 장면 시간 tooredact 수동으로 필요로 하지만이 서비스 hello 모양을 가진 교정 프로세스는 몇 가지 간단한 단계만 거치면 요구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="fc05f-109">자세한 내용은 [이 블로그](https://azure.microsoft.com/blog/azure-media-redactor/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc05f-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="fc05f-110">이 항목에 대 한 세부 정보를 제공 **Azure 미디어 Redactor** 표시 방법을 toouse Media Services SDK for.NET으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="fc05f-111">hello **Azure 미디어 Redactor** MP는 현재 미리 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="fc05f-112">이 기능은 모든 공용 Azure 지역과 미국 정부 및 중국 데이터 센터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="fc05f-113">이 미리 보기는 현재 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="fc05f-114">얼굴 편집 모드</span><span class="sxs-lookup"><span data-stu-id="fc05f-114">Face redaction modes</span></span>
<span data-ttu-id="fc05f-115">비디오의 모든 프레임에서 얼굴 감지 하 고 hello 얼굴 추적 안 면 교정 works 개체 모두 앞으로 및 뒤로 시간 내에 있도록 hello 동일한 개별 수 수 흐려지는 다른 각도도에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="fc05f-116">hello 교정 자동화 된 프로세스는 매우 복잡 하며 미디어 분석을 제공 toomodify hello 최종 출력 하는 여러 가지 방법으로 이러한 이유로 100%의 원하는 출력을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="fc05f-117">또한 tooa 완전 자동 모드에서는 hello 선택/de-selection Id 목록을 통해 찾은 면 수 있는 2 패스 워크플로입니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="fc05f-118">또한, 프레임 조정 hello MP 당 임의의 toomake JSON 형식의 메타 데이터 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="fc05f-119">이 워크플로는 **분석** 및 **편집** 모드로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="fc05f-120">두 작업 모두 하나의 작업이;에서 실행 되는 단일 패스로 hello 두 가지 모드를 결합할 수 있습니다. 이 모드는 무엇 일까요 **조합**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="fc05f-121">결합된 모드</span><span class="sxs-lookup"><span data-stu-id="fc05f-121">Combined mode</span></span>
<span data-ttu-id="fc05f-122">이 모드는 수동 입력 없이 자동으로 편집된 mp4를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="fc05f-123">단계</span><span class="sxs-lookup"><span data-stu-id="fc05f-123">Stage</span></span> | <span data-ttu-id="fc05f-124">파일 이름</span><span class="sxs-lookup"><span data-stu-id="fc05f-124">File Name</span></span> | <span data-ttu-id="fc05f-125">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fc05f-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc05f-126">입력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-126">Input asset</span></span> |<span data-ttu-id="fc05f-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="fc05f-127">foo.bar</span></span> |<span data-ttu-id="fc05f-128">WMV, MOV 또는 MP4 형식의 동영상</span><span class="sxs-lookup"><span data-stu-id="fc05f-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="fc05f-129">입력 구성</span><span class="sxs-lookup"><span data-stu-id="fc05f-129">Input config</span></span> |<span data-ttu-id="fc05f-130">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="fc05f-130">Job configuration preset</span></span> |<span data-ttu-id="fc05f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="fc05f-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="fc05f-132">출력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-132">Output asset</span></span> |<span data-ttu-id="fc05f-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="fc05f-133">foo_redacted.mp4</span></span> |<span data-ttu-id="fc05f-134">흐리게 표시하기가 적용된 동영상</span><span class="sxs-lookup"><span data-stu-id="fc05f-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="fc05f-135">입력 예:</span><span class="sxs-lookup"><span data-stu-id="fc05f-135">Input example:</span></span>
[<span data-ttu-id="fc05f-136">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="fc05f-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="fc05f-137">출력 예제:</span><span class="sxs-lookup"><span data-stu-id="fc05f-137">Output example:</span></span>
[<span data-ttu-id="fc05f-138">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="fc05f-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="fc05f-139">분석 모드</span><span class="sxs-lookup"><span data-stu-id="fc05f-139">Analyze mode</span></span>
<span data-ttu-id="fc05f-140">hello **분석** 각 개의 jpg 이미지가 얼굴 감지 및 hello 2 패스 워크플로의 패스 비디오 입력을 얼굴 위치의 JSON 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="fc05f-141">단계</span><span class="sxs-lookup"><span data-stu-id="fc05f-141">Stage</span></span> | <span data-ttu-id="fc05f-142">파일 이름</span><span class="sxs-lookup"><span data-stu-id="fc05f-142">File Name</span></span> | <span data-ttu-id="fc05f-143">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fc05f-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc05f-144">입력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-144">Input asset</span></span> |<span data-ttu-id="fc05f-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="fc05f-145">foo.bar</span></span> |<span data-ttu-id="fc05f-146">WMV, MPV 또는 MP4 형식의 동영상</span><span class="sxs-lookup"><span data-stu-id="fc05f-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="fc05f-147">입력 구성</span><span class="sxs-lookup"><span data-stu-id="fc05f-147">Input config</span></span> |<span data-ttu-id="fc05f-148">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="fc05f-148">Job configuration preset</span></span> |<span data-ttu-id="fc05f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="fc05f-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="fc05f-150">출력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-150">Output asset</span></span> |<span data-ttu-id="fc05f-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="fc05f-151">foo_annotations.json</span></span> |<span data-ttu-id="fc05f-152">얼굴 위치의 주석 데이터(JSON 형식).</span><span class="sxs-lookup"><span data-stu-id="fc05f-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="fc05f-153">이 흐리게 하 여 hello 사용자 toomodify hello 경계 상자의 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="fc05f-154">아래 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fc05f-154">See sample below.</span></span> |
| <span data-ttu-id="fc05f-155">출력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-155">Output asset</span></span> |<span data-ttu-id="fc05f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="fc05f-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="fc05f-157">각 자른된 jpg 과제를 여기서 hello 번호 나타냅니다 hello 앞면의 hello labelId를 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="fc05f-158">출력 예제:</span><span class="sxs-lookup"><span data-stu-id="fc05f-158">Output example:</span></span>

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

### <a name="redact-mode"></a><span data-ttu-id="fc05f-159">편집 모드</span><span class="sxs-lookup"><span data-stu-id="fc05f-159">Redact mode</span></span>
<span data-ttu-id="fc05f-160">hello hello 워크플로의 두 번째 단계에서는 단일 자산에 결합 해야 하는 입력 중 더 큰 수 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="fc05f-161">여기에 Id tooblur, hello 원본 비디오 및 JSON hello 주석 목록이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="fc05f-162">이 모드는 hello 입력된 비디오에서 주석 tooapply 흐리게 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="fc05f-163">hello 출력 hello 분석 패스에서는 hello 원본 비디오</span><span class="sxs-lookup"><span data-stu-id="fc05f-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="fc05f-164">비디오 hello toobe hello Redact 모드 작업에 대 한 hello 입력된 자산으로 업로드 하 고 주 파일 hello로 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="fc05f-165">단계</span><span class="sxs-lookup"><span data-stu-id="fc05f-165">Stage</span></span> | <span data-ttu-id="fc05f-166">파일 이름</span><span class="sxs-lookup"><span data-stu-id="fc05f-166">File Name</span></span> | <span data-ttu-id="fc05f-167">참고 사항</span><span class="sxs-lookup"><span data-stu-id="fc05f-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fc05f-168">입력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-168">Input asset</span></span> |<span data-ttu-id="fc05f-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="fc05f-169">foo.bar</span></span> |<span data-ttu-id="fc05f-170">WMV, MPV 또는 MP4 형식의 동영상.</span><span class="sxs-lookup"><span data-stu-id="fc05f-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="fc05f-171">1단계와 동일한 동영상입니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="fc05f-172">입력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-172">Input asset</span></span> |<span data-ttu-id="fc05f-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="fc05f-173">foo_annotations.json</span></span> |<span data-ttu-id="fc05f-174">1단계의 주석 메타데이터 파일 및 수정 사항(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="fc05f-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="fc05f-175">입력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-175">Input asset</span></span> |<span data-ttu-id="fc05f-176">foo_IDList.txt(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="fc05f-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="fc05f-177">(옵션) 새 줄 면 tooredact Id의 목록을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="fc05f-178">지정하지 않으면 모든 얼굴이 흐리게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="fc05f-179">입력 구성</span><span class="sxs-lookup"><span data-stu-id="fc05f-179">Input config</span></span> |<span data-ttu-id="fc05f-180">작업 구성 사전 설정</span><span class="sxs-lookup"><span data-stu-id="fc05f-180">Job configuration preset</span></span> |<span data-ttu-id="fc05f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="fc05f-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="fc05f-182">출력 자산</span><span class="sxs-lookup"><span data-stu-id="fc05f-182">Output asset</span></span> |<span data-ttu-id="fc05f-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="fc05f-183">foo_redacted.mp4</span></span> |<span data-ttu-id="fc05f-184">주석을 기반으로 흐리게 표시하기가 적용된 동영상</span><span class="sxs-lookup"><span data-stu-id="fc05f-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="fc05f-185">예제 출력</span><span class="sxs-lookup"><span data-stu-id="fc05f-185">Example output</span></span>
<span data-ttu-id="fc05f-186">선택한 한 ID 가진 IDList hello 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="fc05f-187">이 동영상을 보세요.</span><span class="sxs-lookup"><span data-stu-id="fc05f-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="fc05f-188">예제 foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="fc05f-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="fc05f-189">흐리게 형식</span><span class="sxs-lookup"><span data-stu-id="fc05f-189">Blur types</span></span>

<span data-ttu-id="fc05f-190">Hello에 **조합** 또는 **Redact** 모드를 가지 5 다른 흐림 효과 모드를 통해 hello JSON 입력된 구성에서 선택할 수 있습니다: **낮은**, **Med**, **높은**, **디버그**, 및 **검정**합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="fc05f-191">기본적으로 **중간**이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-191">By default **Med** is used.</span></span>

<span data-ttu-id="fc05f-192">샘플의 hello 아래의 형식 흐림 효과 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="fc05f-193">예제 JSON:</span><span class="sxs-lookup"><span data-stu-id="fc05f-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="fc05f-194">낮음</span><span class="sxs-lookup"><span data-stu-id="fc05f-194">Low</span></span>

![낮음](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="fc05f-196">중간</span><span class="sxs-lookup"><span data-stu-id="fc05f-196">Med</span></span>

![중간](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="fc05f-198">높음</span><span class="sxs-lookup"><span data-stu-id="fc05f-198">High</span></span>

![높음](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="fc05f-200">디버그</span><span class="sxs-lookup"><span data-stu-id="fc05f-200">Debug</span></span>

![디버그](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="fc05f-202">검정</span><span class="sxs-lookup"><span data-stu-id="fc05f-202">Black</span></span>

![검정](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="fc05f-204">Hello 출력 JSON 파일의 요소</span><span class="sxs-lookup"><span data-stu-id="fc05f-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="fc05f-205">hello 교정 MP 고정밀 얼굴 위치 검색 및 비디오 프레임에 too64 휴먼 면을 검색할 수 있는 추적을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="fc05f-206">전면 제공 하는 동안 측면 및 작은 면 hello 최상의 결과 (미만 또는 too24x24 픽셀 값이) 하는 어려움이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="fc05f-207">.NET 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="fc05f-207">.NET sample code</span></span>

<span data-ttu-id="fc05f-208">hello 다음 프로그램 표시 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="fc05f-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="fc05f-209">자산 만들기 hello 자산 미디어 파일을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="fc05f-210">다음 json 사전 설정을 hello를 포함 하는 구성 파일에 따라 얼굴 교정 작업과 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="fc05f-211">Hello 출력 JSON 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="fc05f-212">Visual Studio 프로젝트 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="fc05f-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="fc05f-213">개발 환경을 설정 하 고에 설명 된 대로 연결 정보를 포함 하는 hello app.config 파일을 채울 [.net 미디어 서비스 개발](media-services-dotnet-how-to-use.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fc05f-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="fc05f-214">예제</span><span class="sxs-lookup"><span data-stu-id="fc05f-214">Example</span></span>

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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="fc05f-215">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fc05f-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fc05f-216">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="fc05f-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="fc05f-217">관련 링크</span><span class="sxs-lookup"><span data-stu-id="fc05f-217">Related links</span></span>
[<span data-ttu-id="fc05f-218">Azure Media Services 분석 개요</span><span class="sxs-lookup"><span data-stu-id="fc05f-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="fc05f-219">Azure 미디어 분석 데모</span><span class="sxs-lookup"><span data-stu-id="fc05f-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

