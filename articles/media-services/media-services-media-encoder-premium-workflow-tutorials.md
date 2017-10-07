---
title: "aaaAvanced 미디어 인코더 프리미엄 워크플로 자습서"
description: "이 문서 tooperform 고급 미디어 인코더 프리미엄 워크플로 작업 하는 방법을 보여 주는 연습이 포함 되어와 방법을 toocreate의 복잡 한 워크플로 워크플로 디자이너를 사용 합니다."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="7056b-103">고급 미디어 인코더 Premium 워크플로 자습서</span><span class="sxs-lookup"><span data-stu-id="7056b-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="7056b-104">개요</span><span class="sxs-lookup"><span data-stu-id="7056b-104">Overview</span></span>
<span data-ttu-id="7056b-105">이 문서에 보여 주는 연습이 포함 되어 방법을 사용 하는 toocustomize 워크플로 **워크플로 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-105">This document contains walkthroughs that show how toocustomize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="7056b-106">Hello 실제 워크플로 파일을 찾을 수 [여기](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-106">You can find hello actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="7056b-107">목차</span><span class="sxs-lookup"><span data-stu-id="7056b-107">TOC</span></span>
<span data-ttu-id="7056b-108">hello 다음 항목에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-108">hello following topics are covered:</span></span>

* [<span data-ttu-id="7056b-109">단일 비트 전송률 MP4로 MXF 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="7056b-110">새 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="7056b-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="7056b-111">미디어 파일 입력 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-111">Using hello Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="7056b-112">미디어 스트림 검사</span><span class="sxs-lookup"><span data-stu-id="7056b-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="7056b-113">MP4 파일 생성을 위해 비디오 인코더 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="7056b-114">Hello 오디오 스트림 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-114">Encoding hello audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="7056b-115">MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱</span><span class="sxs-lookup"><span data-stu-id="7056b-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="7056b-116">Hello MP4 파일 쓰기</span><span class="sxs-lookup"><span data-stu-id="7056b-116">Writing hello MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="7056b-117">Hello 출력 파일에서 미디어 서비스 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="7056b-117">Creating a Media Services Asset from hello output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="7056b-118">테스트 hello 로컬로 워크플로 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-118">Test hello finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="7056b-119">다중 비트 전송률 MP4로 MXF 인코딩 - 동적 패키징 사용</span><span class="sxs-lookup"><span data-stu-id="7056b-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="7056b-120">하나 이상의 추가 MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="7056b-121">구성 hello 파일 출력 이름</span><span class="sxs-lookup"><span data-stu-id="7056b-121">Configuring hello file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="7056b-122">별도 오디오 트랙 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="7056b-123">Hello를 추가 합니다. ISM SMIL 파일</span><span class="sxs-lookup"><span data-stu-id="7056b-123">Adding hello .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="7056b-124">다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진</span><span class="sxs-lookup"><span data-stu-id="7056b-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="7056b-125">워크플로 개요 tooenhance</span><span class="sxs-lookup"><span data-stu-id="7056b-125">Workflow overview tooenhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="7056b-126">파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="7056b-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="7056b-127">게시에 hello 워크플로 루트 구성 요소 속성</span><span class="sxs-lookup"><span data-stu-id="7056b-127">Publishing component properties onto hello workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="7056b-128">게시된 속성 값을 사용하는 출력 파일 이름 생성</span><span class="sxs-lookup"><span data-stu-id="7056b-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="7056b-129">축소판 그림 toomultibitrate MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-129">Adding thumbnails toomultibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="7056b-130">워크플로 개요 tooadd 미리 보기</span><span class="sxs-lookup"><span data-stu-id="7056b-130">Workflow overview tooadd thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="7056b-131">JPG 인코딩 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="7056b-132">색 공간 변환 처리</span><span class="sxs-lookup"><span data-stu-id="7056b-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="7056b-133">쓰기 hello 미리 보기</span><span class="sxs-lookup"><span data-stu-id="7056b-133">Writing hello thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="7056b-134">워크플로에서 오류 감지</span><span class="sxs-lookup"><span data-stu-id="7056b-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="7056b-135">완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="7056b-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="7056b-136">다중 비트 전송률 MP4 출력의 시간 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="7056b-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="7056b-137">워크플로 개요 toostart 트리밍을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-137">Workflow overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="7056b-138">스트림 트리머 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-138">Using hello Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="7056b-139">완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="7056b-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="7056b-140">스크립트 구성 요소를 hello 소개</span><span class="sxs-lookup"><span data-stu-id="7056b-140">Introducing hello Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="7056b-141">워크플로 내의 스크립팅: Hello World</span><span class="sxs-lookup"><span data-stu-id="7056b-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="7056b-142">다중 비트 전송률 MP4 출력의 프레임 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="7056b-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="7056b-143">조정을 추가 개요 toostart 세부 계획</span><span class="sxs-lookup"><span data-stu-id="7056b-143">Blueprint overview toostart adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="7056b-144">Hello 클립 목록 XML을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-144">Using hello Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="7056b-145">스크립트 구성 요소에서 hello 클립 목록을 수정</span><span class="sxs-lookup"><span data-stu-id="7056b-145">Modifying hello clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="7056b-146">ClippingEnabled 편의 속성 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="7056b-147"><a id="MXF_to_MP4"></a>단일 비트 전송률 MP4로 MXF 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="7056b-148">이 연습에서는 .MXF 입력 파일에서 AAC-HE 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="7056b-149"><a id="MXF_to_MP4_start_new"></a>새 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="7056b-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="7056b-150">워크플로 디자이너를 열고 "파일"-"새 작업 영역"-"청사진 트랜스코딩"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="7056b-151">hello 새 워크플로 요소 3 개 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-151">hello new workflow will show 3 elements:</span></span>

* <span data-ttu-id="7056b-152">기본 원본 파일</span><span class="sxs-lookup"><span data-stu-id="7056b-152">Primary Source File</span></span>
* <span data-ttu-id="7056b-153">클립 목록 XML</span><span class="sxs-lookup"><span data-stu-id="7056b-153">Clip List XML</span></span>
* <span data-ttu-id="7056b-154">출력 파일/자산</span><span class="sxs-lookup"><span data-stu-id="7056b-154">Output File/Asset</span></span>  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="7056b-156">*새 인코딩 워크플로*</span><span class="sxs-lookup"><span data-stu-id="7056b-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="7056b-157"><a id="MXF_to_MP4_with_file_input"></a>미디어 파일 입력 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-157"><a id="MXF_to_MP4_with_file_input"></a>Using hello Media File Input</span></span>
<span data-ttu-id="7056b-158">순서 tooaccept에 쿼리하여 입력된 미디어 파일 하나으로 시작 미디어 파일 입력 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-158">In order tooaccept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="7056b-159">구성 요소 toohello 워크플로 tooadd hello 리포지토리 검색 상자에 검색할 끌어서 hello 디자이너 창에 놓을 hello 원하는 항목 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-159">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span> <span data-ttu-id="7056b-160">미디어 파일 입력 hello에 대 한이 작업을 수행 하 고 hello 미디어 파일 입력에서 hello 기본 소스 파일 구성 요소 toohello 파일 이름 입력된 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-160">Do this for hello Media File Input and connect hello Primary Source File component toohello Filename input pin from hello Media File Input.</span></span>

![연결된 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="7056b-162">*연결된 미디어 파일 입력*</span><span class="sxs-lookup"><span data-stu-id="7056b-162">*Connected Media File Input*</span></span>

<span data-ttu-id="7056b-163">다른 많은 실행 하기 전에 먼저 사용 해야 tooindicate toohello 워크플로 디자이너 어떤 샘플 파일 toouse toodesign 같은 우리의 워크플로와 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-163">Before we can do much else, we'll first need tooindicate toohello workflow designer what sample file we'd like toouse toodesign our workflow with.</span></span> <span data-ttu-id="7056b-164">따라서 toodo hello 디자이너 창 배경을 클릭 하 고 hello 오른쪽 속성 창에서 hello 소스 파일을 기본 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-164">toodo so, click hello designer pane background and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="7056b-165">Hello 폴더 아이콘을 사용 하 여 원하는 선택 hello 파일 tootest hello 워크플로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-165">Click hello folder icon and select hello desired file tootest hello workflow with.</span></span> <span data-ttu-id="7056b-166">이 도구를 실행 하는 즉시 hello 미디어 파일 입력 구성 요소 되며 hello 파일을 검사 검사이 해당 출력 핀 tooreflect hello 파일을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-166">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file it inspected.</span></span>

![채워진 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="7056b-168">*채워진 미디어 파일 입력*</span><span class="sxs-lookup"><span data-stu-id="7056b-168">*Populated Media File Input*</span></span>

<span data-ttu-id="7056b-169">Toowork와 같은 입력 사항으로 지정 하는 동안 알 수 없습니다 아직 hello 인코딩된 출력 위치 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-169">While this specifies with what input we'd like toowork with, it doesn't tell yet where hello encoded output should go to.</span></span> <span data-ttu-id="7056b-170">이제 기본 소스 파일 구성 된 유사한 toohow hello hello 바로 아래의 출력 폴더 변수 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-170">Similar toohow hello Primary Source File was configured, now configure hello Output Folder Variable property, just below it.</span></span>

![구성된 입력 및 출력 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="7056b-172">*구성된 입력 및 출력 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="7056b-173"><a id="MXF_to_MP4_streams"></a>미디어 스트림 검사</span><span class="sxs-lookup"><span data-stu-id="7056b-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="7056b-174">종종 hello 스트림 그렇게 모양을 tooknow hello 워크플로 통해 흐르는 원하는입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-174">Often it's desired tooknow how hello stream looks like that flows through hello workflow.</span></span> <span data-ttu-id="7056b-175">tooinspect hello 워크플로에서 언제 든 지 스트림 출력 또는 입력된 핀 hello 구성 요소 중 하나를 클릭 하기만 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-175">tooinspect a stream at any point in hello workflow, just click an output or input pin on any of hello components.</span></span> <span data-ttu-id="7056b-176">이 경우의 미디어 파일 입력에서 hello 압축 되지 않은 비디오 출력 핀에 클릭 해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="7056b-176">In this case, try clicking on hello Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="7056b-177">대화 상자가 열리고 tooinspect hello에 대 한 아웃 바운드 비디오 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-177">A dialog will open up that allows tooinspect hello outbound video.</span></span>

![검사 hello 압축 되지 않은 비디오 출력 핀](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="7056b-179">*검사 hello 압축 되지 않은 비디오 출력 핀*</span><span class="sxs-lookup"><span data-stu-id="7056b-179">*Inspecting hello Uncompressed Video output pin*</span></span>

<span data-ttu-id="7056b-180">이 경우에 예를 들어 거의 2분인 비디오의 4:2:2 샘플링에서 초 당 24프레임으로 1920x1080 입력을 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="7056b-181"><a id="MXF_to_MP4_file_generation"></a>MP4 파일 생성을 위해 비디오 인코더 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="7056b-182">이제 압축되지 않은 비디오 및 여러 압축되지 않은 오디오 출력 핀을 미디어 파일 입력에 사용할 수 있다는 점을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="7056b-183">순서 tooencode에서 인바운드 비디오 hello, 생성 하기 위한 인코딩 구성 요소-이 경우에 필요 합니다. MP4 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-183">In order tooencode hello inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="7056b-184">tooencode 비디오 스트림 tooH.264 hello, hello toohello 디자이너 화면 AVC 비디오 인코더 구성 요소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-184">tooencode hello video stream tooH.264, add hello AVC Video Encoder component toohello designer surface.</span></span> <span data-ttu-id="7056b-185">이 구성 요소는 압축되지 않은 비디오 스트림을 입력으로 사용하고 AVC 압축된 비디오 스트림을 해당 출력 핀에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="7056b-187">*연결되지 않은 AVC 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="7056b-188">해당 속성 방법을 hello 인코딩 정확 하 게 발생 하는 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-188">Its properties determine how hello encoding exactly happens.</span></span> <span data-ttu-id="7056b-189">일부의 hello에 살펴봅시다 더 중요 한 설정:</span><span class="sxs-lookup"><span data-stu-id="7056b-189">Let's have a look at some of hello more important settings:</span></span>

* <span data-ttu-id="7056b-190">출력 너비와 높이 출력: 이러한 hello 인코딩된 비디오의 hello 해상도 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-190">Output width and Output height: these determine hello resolution of hello encoded video.</span></span> <span data-ttu-id="7056b-191">이 경우에 640x360로 결정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="7056b-192">프레임 속도: hello 소스 프레임 속도 채택 하는 집합 toopassthrough just 됩니다, 경우에 가능한 toooverride 하지만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-192">Frame Rate: when set toopassthrough it will just adopt hello source frame rate, it's possible toooverride this though.</span></span> <span data-ttu-id="7056b-193">이러한 프레임 속도 변환은 동작 보정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="7056b-194">프로필 및 수준: 이러한 hello AVC 프로필과 수준을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-194">Profile and Level: these determine hello AVC profile and level.</span></span> <span data-ttu-id="7056b-195">tooconveniently 자세한 내용을 보려면 hello 다양 한 수준 및 프로필에 대 한 hello AVC 비디오 인코더 구성 요소에 대해 hello 물음표 아이콘을 클릭 한 hello 도움말 페이지에는 각 hello 수준에 대 한 자세한 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-195">tooconveniently get more information about hello different levels and profiles, click hello question mark icon on hello AVC Video Encoder component and hello help page will show more detail about each of hello levels.</span></span> <span data-ttu-id="7056b-196">이 샘플에서는 3.2 (hello 기본값) 수준에서 기본 프로필을 가진 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-196">For our sample, let's go with Main Profile at level 3.2 (hello default).</span></span>
* <span data-ttu-id="7056b-197">전송률 제어 모드 및 비트 전송률(kbps): 이 시나리오에서는 1200kbps에서 상수 비트 전송률(CBR) 출력을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="7056b-198">: 비디오이 형식은 hello hello H.264 스트림으로 작성 되려면 VUI (비디오 유용성 정보)에 대 한 (디코더 tooenhance hello 표시할 하지만 반드시 toocorrectly에서 사용할 수 있는 정보 디코드):</span><span class="sxs-lookup"><span data-stu-id="7056b-198">Video Format: this is about hello VUI (Video Usability Information) that gets written into hello H.264 stream (side information that might be used by a decoder tooenhance hello display but not essential toocorrectly decode):</span></span>
* <span data-ttu-id="7056b-199">NTSC(30fps를 사용하는 미국 또는 일본에 일반적임)</span><span class="sxs-lookup"><span data-stu-id="7056b-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="7056b-200">PAL(25fps를 사용하는 유럽에 일반적임)</span><span class="sxs-lookup"><span data-stu-id="7056b-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="7056b-201">GOP 크기 모드: 여기서는 닫힌 GOP로 키 간격이 2초인 고정된 GOP 크기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="7056b-202">이렇게 하면 동적 패키징 Azure 미디어 서비스를 제공 하는 hello와의 호환성.</span><span class="sxs-lookup"><span data-stu-id="7056b-202">This ensures compatibility with hello dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="7056b-203">toofeed 우리의 AVC 인코더 hello 미디어 파일 입력 구성 요소 toohello 압축 되지 않은 비디오 입력된 핀 hello AVC 인코더에서에서 hello 압축 되지 않은 비디오 출력 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-203">toofeed our AVC encoder, connect hello Uncompressed Video output pin from hello Media File Input component toohello Uncompressed Video input pin from hello AVC encoder.</span></span>

![연결된 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="7056b-205">*연결된 AVC 기본 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="7056b-206"><a id="MXF_to_MP4_audio"></a>Hello 오디오 스트림 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-206"><a id="MXF_to_MP4_audio"></a>Encoding hello audio stream</span></span>
<span data-ttu-id="7056b-207">이 시점에서 인코딩된 비디오에서는 하지만 hello 원래 압축 되지 않은 오디오 스트림 여전히 toobe 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-207">At this point, we have encoded video but hello original uncompressed audio stream still needs toobe compressed.</span></span> <span data-ttu-id="7056b-208">이 대 한 AAC 인코더 (돌비) 구성 요소를 hello 하 여 인코딩을 AAC를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-208">For this we'll go with AAC encoding by hello AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="7056b-209">Toohello 워크플로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-209">Add it toohello workflow.</span></span>

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="7056b-211">*연결되지 않은 AAC 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="7056b-212">이제는 비 호환성: 오디오 스트림을 사용할 수 있는 압축 되지 않은 미디어 파일 입력 가능성이 hello 서로 다른 두 갖습니다 보다 더 많은 동안만 단일 압축 되지 않은 오디오 입력된 핀 hello AAC 인코더에서에서에: 왼쪽 오디오 채널 및 hello에 대 한 hello에 대 한 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from hello AAC Encoder while more than likely hello Media File Input will have two different uncompressed audio stream available: one for hello left audio channel and one for hello right.</span></span> <span data-ttu-id="7056b-213">(서라운드 사운드를 처리하는 경우 6채널입니다.) 되므로 수 toodirectly hello 오디오 hello AAC 오디오 인코더에에 hello 미디어 파일 입력 원본에서 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible toodirectly connect hello audio from hello Media File Input source into hello AAC audio encoder.</span></span> <span data-ttu-id="7056b-214">hello AAC 구성 요소가 예상 이른바 "인터리브" 오디오 스트림을: 둘 다를 포함 하는 단일 스트림을 hello 서로 포함 되어 hello의 왼쪽 및 오른쪽 채널과 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-214">hello AAC component expects a so-called "interleaved" audio stream: a single stream that has both hello left and hello right channels interleaved with each other.</span></span> <span data-ttu-id="7056b-215">소스 미디어 파일에서 알고 있으므로 오디오 트랙 hello 소스 어떤 위치에서 생성할 수 hello 사용 하 여 이러한 인터리브 오디오 스트림을 올바르게 할당 왼쪽 및 오른쪽에 대 한 스피커 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-215">Once we know from our source media file which audio tracks are on what position in hello source, we can generate such interleaved audio stream with hello correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="7056b-216">먼저 하나 toogenerated hello 필요한 소스 오디오 채널에서 인터리빙된 된 스트림을 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-216">First one will want toogenerated an interleaved stream from hello required source audio channels.</span></span> <span data-ttu-id="7056b-217">hello 오디오 스트림 인터리브 구성 요소에이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-217">hello Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="7056b-218">Toohello 워크플로 추가 하 고에 미디어 파일 입력 hello에서 hello 오디오 출력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-218">Add it toohello workflow and connect hello audio outputs from hello Media File Input into it.</span></span>

![연결된 오디오 스트림 인터리버](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="7056b-220">*연결된 오디오 스트림 인터리버*</span><span class="sxs-lookup"><span data-stu-id="7056b-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="7056b-221">이제 인터리빙된 된 오디오 스트림을 했으므로 여전히 지정 하는 대신 tooassign hello 왼쪽 또는 오른쪽 스피커를 배치 하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-221">Now that we have an interleaved audio stream, we still didn't specify where tooassign hello left or right speaker positions to.</span></span> <span data-ttu-id="7056b-222">이 toospecify 순서, hello 스피커 위치 Assigner 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-222">In order toospecify this, we can leverage hello Speaker Position Assigner.</span></span>

![스피커 위치 할당자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="7056b-224">*스피커 위치 할당자 추가*</span><span class="sxs-lookup"><span data-stu-id="7056b-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="7056b-225">채널 "2.0 (L, R)"를 호출 하는 미리 설정 된 hello 및 인코더 사전 설정의 필터는 "Custom"를 통해 사용 하기 위해 스피커 위치 Assigner hello 스테레오 입력된 스트림을 사용 하 여 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-225">Configure hello Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and hello Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="7056b-226">(이 할당 hello 왼쪽된 스피커 위치 toochannel 1 및 2 hello 오른쪽 스피커 위치 toochannel 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-226">(This will assign hello left speaker position toochannel 1 and hello right speaker position toochannel 2.)</span></span>

<span data-ttu-id="7056b-227">Hello AAC 인코더의 hello 스피커 위치 Assigner toohello 입력의 hello 출력에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-227">Connect hello output of hello Speaker Position Assigner toohello input of hello AAC Encoder.</span></span> <span data-ttu-id="7056b-228">그런 다음 hello AAC 인코더 toowork는 "2.0 (L, R)"를 입력으로 스테레오 오디오와 toodeal를 알 수 있도록 채널 미리 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-228">Then, tell hello AAC Encoder toowork with a "2.0 (L,R)" Channel Preset, so it knows toodeal with stereo audio as input.</span></span>

### <span data-ttu-id="7056b-229"><a id="MXF_to_MP4_audio_and_fideo"></a>MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱</span><span class="sxs-lookup"><span data-stu-id="7056b-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="7056b-230">AVC 인코딩된 비디오 스트림 및 AAC 인코딩된 오디오 스트림을 지정하여 둘 모두를 .MP4 컨테이너에 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="7056b-231">단일는 다양 한 스트림 혼합의 hello 프로세스 "멀티플렉싱" (또는 "muxing") 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-231">hello process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="7056b-232">이 경우 hello 오디오 및 일관 된 단일에서 비디오 스트림 hello 인터리빙 하는 것입니다. MP4 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-232">In this case we're interleaving hello audio and hello video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="7056b-233">hello 구성 요소에 대해이 조정 하는 합니다. MP4 컨테이너 ISO mpeg-4 멀티플렉서 hello를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-233">hello component that coordinates this for an .MP4 container is called hello ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="7056b-234">하나의 toohello 디자이너 화면을 추가 하 고 hello AVC 비디오 인코더와 hello AAC 인코더 tooits 입력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-234">Add one toohello designer surface and connect both hello AVC Video Encoder and hello AAC Encoder tooits inputs.</span></span>

![연결된 MPEG4 멀티플렉서](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="7056b-236">*연결된 MPEG4 멀티플렉서*</span><span class="sxs-lookup"><span data-stu-id="7056b-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="7056b-237"><a id="MXF_to_MP4_writing_mp4"></a>Hello MP4 파일 쓰기</span><span class="sxs-lookup"><span data-stu-id="7056b-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing hello MP4 file</span></span>
<span data-ttu-id="7056b-238">출력 파일을 작성할 때는 hello 출력 파일 구성 요소가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-238">When writing an output file, hello File Output component is used.</span></span> <span data-ttu-id="7056b-239">출력 toodisk 작성 되려면 있도록 hello ISO mpeg-4 멀티플렉서의 toohello 출력을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-239">We can connect this toohello output of hello ISO MPEG-4 Multiplexer so that its output gets written toodisk.</span></span> <span data-ttu-id="7056b-240">toodo이 hello 컨테이너 (mpeg-4) 출력 핀 toohello 쓰기 입력된 핀의 hello 파일 출력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-240">toodo this, connect hello Container (MPEG-4) output pin toohello Write input pin of hello File Output.</span></span>

![연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="7056b-242">*연결된 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="7056b-242">*Connected File Output*</span></span>

<span data-ttu-id="7056b-243">사용 되는 hello filename hello 파일 속성 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-243">hello filename that will be used is determined by hello File property.</span></span> <span data-ttu-id="7056b-244">가장 가능성이 높은 하나 tooset 합니다 해당 속성에는 하드 코드 된 tooa 값이 지정 될 수 있지만, 식을 통해 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-244">While that property can be hardcoded tooa given value, most likely one will want tooset it through an expression instead.</span></span>

<span data-ttu-id="7056b-245">toohave hello 워크플로 hello 출력을 자동으로 결정 파일 이름 속성 식에서 hello 단추 다음 toohello 파일 이름을 클릭 합니다 (다음 toohello 폴더 아이콘).</span><span class="sxs-lookup"><span data-stu-id="7056b-245">toohave hello workflow automatically determine hello output File name property from an expression, click hello buton next toohello File name (next toohello folder icon).</span></span> <span data-ttu-id="7056b-246">Hello에서 드롭다운 메뉴를 선택한 다음 "식"을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-246">From hello drop down menu then select "Expression".</span></span> <span data-ttu-id="7056b-247">이 hello 식 편집기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-247">This will bring up hello expression editor.</span></span> <span data-ttu-id="7056b-248">먼저 hello 내용을 hello 편집기의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-248">Clear hello contents of hello editor first.</span></span>

![빈 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="7056b-250">*빈 식 편집기*</span><span class="sxs-lookup"><span data-stu-id="7056b-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="7056b-251">hello 식 편집기를 사용 하면 tooenter 혼합 된 하나 이상의 변수, 리터럴 값입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-251">hello expression editor allows tooenter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="7056b-252">변수는 달러 기호로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="7056b-253">Hello $ 키를 누르면 처럼 사용 가능한 변수를 선택할 드롭다운 상자 hello 편집기에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-253">As you hit hello $ key, hello editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="7056b-254">여기서는 hello 출력 디렉터리 변수와 hello 기본 입력된 파일 이름 변수 사용:</span><span class="sxs-lookup"><span data-stu-id="7056b-254">In our case we'll use a combination of hello output directory variable and hello base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![채워진 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="7056b-256">*채워진 식 편집기*</span><span class="sxs-lookup"><span data-stu-id="7056b-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="7056b-257">Hello 식 편집기에서 값을 제공 해야, toosee 순서로 Azure에서 인코딩 작업의 출력 파일을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="7056b-257">In order toosee see an output file of your encoding job in Azure, you must provide a value in hello expression editor.</span></span>
>
>

<span data-ttu-id="7056b-258">Hello 식 ok를 클릭 하 여 확인 하면 hello 속성 창은 미리 봅니다 toowhat 값 hello 파일 속성 확인을 시점에서.</span><span class="sxs-lookup"><span data-stu-id="7056b-258">When you confirm hello expression by hitting ok, hello property window will preview toowhat value hello File property resolves at this point in time.</span></span>

![파일 식이 출력 dir 확인](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="7056b-260">*파일 식이 출력 dir 확인*</span><span class="sxs-lookup"><span data-stu-id="7056b-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="7056b-261"><a id="MXF_to_MP4_asset_from_output"></a>Hello 출력 파일에서 미디어 서비스 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="7056b-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from hello output file</span></span>
<span data-ttu-id="7056b-262">Tooindicate 여전히 필요 MP4 출력 파일을 쓴 하는 동안이 워크플로 실행 한 결과로 생성 됩니다는 미디어 서비스 자산 출력 toohello이이 파일에 속해 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-262">While we have written an MP4 output file, we still need tooindicate that this file belongs toohello output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="7056b-263">toothis 끝나도 hello 출력 파일/자산 노드 hello 워크플로 캔버스에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-263">toothis end, hello Output File/Asset node on hello workflow canvas is used.</span></span> <span data-ttu-id="7056b-264">이 노드의에 들어오는 모든 파일 부분에서는 hello 결과 Azure 미디어 서비스 자산 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-264">All incoming files into this node will make part of hello resulting Azure Media Services asset.</span></span>

<span data-ttu-id="7056b-265">Hello 출력 파일 구성 요소 toohello 출력 파일/자산 구성 요소 toofinish hello 워크플로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-265">Connect hello File Output component toohello Output File/Asset component toofinish hello workflow.</span></span>

![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="7056b-267">*완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="7056b-267">*Finished Workflow*</span></span>

### <span data-ttu-id="7056b-268"><a id="MXF_to_MP4_test"></a>테스트 hello 로컬로 워크플로 완료 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-268"><a id="MXF_to_MP4_test"></a>Test hello finished workflow locally</span></span>
<span data-ttu-id="7056b-269">tootest hello 워크플로 로컬로 hello 위쪽에 hello 도구 모음에서 hello 재생 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-269">tootest hello workflow locally, hit hello play button in hello toolbar at hello top.</span></span> <span data-ttu-id="7056b-270">Hello 워크플로 실행을 완료 하는 경우 구성 하는 hello 출력 폴더에 생성 된 hello 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-270">When hello workflow finished executing, inspect hello output generated in hello configured output folder.</span></span> <span data-ttu-id="7056b-271">Hello 완료 hello MXF 입력된 소스 파일에서 인코딩된 MP4 출력 파일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-271">You'll see hello finished MP4 output file that was encoded from hello MXF input source file.</span></span>

## <span data-ttu-id="7056b-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>MP4로 MXF 인코딩 - 다중 비트 전송률 동적 패키징 사용</span><span class="sxs-lookup"><span data-stu-id="7056b-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="7056b-273">이 연습에서는 단일 .MXF 입력 파일에서 AAC 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일의 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="7056b-274">때 Azure 미디어 서비스는 서로 다른 비트 전송률 및 해결 toobe 생성 해야 합니다 각 여러 GOP 정렬 MP4 파일에서 제공 하는 동적 패키징 기능 hello와 함께에서 사용 하기 위해 다중 비트 전송률 자산 출력 방법이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-274">When a multi-bitrate asset output is desired for use in combination with hello Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need toobe generated.</span></span> <span data-ttu-id="7056b-275">toodo 따라서 hello [단일 비트 전송률 MP4에 인코딩 MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) 연습 좋은 출발점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-275">toodo so, hello [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![워크플로 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="7056b-277">*워크플로 시작*</span><span class="sxs-lookup"><span data-stu-id="7056b-277">*Starting Workflow*</span></span>

### <span data-ttu-id="7056b-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>하나 이상의 추가 MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="7056b-279">결과 Azure 미디어 서비스 자산의 모든 MP4 파일은 서로 다른 비트 전송률 및 해상도를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="7056b-280">하나 이상의 MP4 출력 파일 toohello 워크플로 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-280">Let's add one or more MP4 output files toohello workflow.</span></span>

<span data-ttu-id="7056b-281">있는지 toomake 동일한 설정을 hello 우리의 비디오 인코더 사용 하 여 만든 모든, 가장 편리 하 게 tooduplicate 이미 기존 AVC 비디오 인코더 hello 및 해상도 비트 전송률의 다른 조합 구성 (추가해보겠습니다 960 x 540 중 하나에서 초당 25 프레임 2,5 Mbps)입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-281">toomake sure we have all our video encoders created with hello same settings, it's most convenient tooduplicate hello already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="7056b-282">tooduplicate hello 기존 인코더 복사본에 붙여 hello 디자이너 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-282">tooduplicate hello existing encoder, copy paste it on hello designer surface.</span></span>

<span data-ttu-id="7056b-283">새 AVC 구성 요소에 미디어 파일 입력 hello hello 압축 되지 않은 비디오 출력 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-283">Connect hello Uncompressed Video output pin of hello Media File Input into our new AVC component.</span></span>

![연결된 두 번째 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="7056b-285">*연결된 두 번째 AVC 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="7056b-286">이제이 새 AVC 인코더 toooutput 960 x 540 2,5로 대 한 hello 구성을 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-286">Now adapt hello configuration for our new AVC encoder toooutput 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="7056b-287">(여기에 해당 속성 "출력 너비", "출력 높이" 및 "비트 전송률(kbps)"을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="7056b-288">지정 된 Azure 미디어 서비스 동적 패키징과 함께 toouse hello 결과 자산 원하는, 스트리밍 끝점 hello 필요한 toobe 정확 하 게 정렬 된 tooeach 다른 방식으로 HLS/조각난 MP4/DASH 조각의 이러한 MP4 파일에서 생성할 수 서로 다른 비트 전송률 간에 전환 하는 클라이언트는 단일 부드러운 연속 비디오 및 오디오 환경이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-288">Given we want toouse hello resulting asset together with Azure Media Services' dynamic packaging, hello streaming endpoint needs toobe capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned tooeach other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="7056b-289">toomake 발생 tooensure 두 AVC 인코더의 hello 속성, hello GOP ("그룹의 사진") 크기를 MP4 파일을 모두 설정 되어이 필요 하 여 변환을 수행할 수 있는 too2 초:</span><span class="sxs-lookup"><span data-stu-id="7056b-289">toomake that happen, we need tooensure that, in hello properties of both AVC encoders hello GOP ("group of pictures") size for both MP4 files is set too2 seconds, which can be done by:</span></span>

* <span data-ttu-id="7056b-290">hello GOP 크기 모드 tooFixed GOP 크기를 설정 하 고</span><span class="sxs-lookup"><span data-stu-id="7056b-290">setting hello GOP Size Mode tooFixed GOP size and</span></span>
* <span data-ttu-id="7056b-291">hello 키 프레임 간격 tootwo (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-291">hello Key Frame Interval tootwo seconds.</span></span>
* <span data-ttu-id="7056b-292">hello GOP IDR 제어 tooClosed GOP tooensure 모든 GOP 대기 중입니다. 종속성 없이 자체에 설정</span><span class="sxs-lookup"><span data-stu-id="7056b-292">also set hello GOP IDR Control tooClosed GOP tooensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="7056b-293">toomake 우리의 워크플로 편리한 toounderstand 너무 hello 첫 번째 AVC 인코더 이름 바꾸기 "AVC 비디오 인코더 640 x 360 1200 kbps" 두 번째 AVC 인코더 hello 및 "AVC 비디오 인코더 960 x 540 2500 kbps"입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-293">toomake our workflow convenient toounderstand, rename hello first AVC encoder too"AVC Video Encoder 640x360 1200kbps" and hello second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="7056b-294">이제 두 번째 ISO MPEG-4 멀티플렉서 및 두 번째 파일 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="7056b-295">Hello 멀티플렉서 toohello 새 AVC 인코더를 연결 하 고 해당 결과 hello 파일 출력으로 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-295">Connect hello multiplexer toohello new AVC encoder and make sure its output is directed into hello File Output.</span></span> <span data-ttu-id="7056b-296">그런 다음 새 hello AAC 오디오 인코더 출력 toohello도 연결 멀티플렉서의 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-296">Then also connect hello AAC audio encoder output toohello new multiplexer's input.</span></span> <span data-ttu-id="7056b-297">hello 파일 출력 차례로 수 연결된 toohello 출력 파일/자산 노드 tooadd 것 toohello 미디어 서비스 자산으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-297">hello File Output in turn can then be connected toohello Output File/Asset node tooadd it toohello Media Services Asset that will be created.</span></span>

![두 번째 Muxer 및 연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="7056b-299">*두 번째 Muxer 및 연결된 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="7056b-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="7056b-300">Azure 미디어 서비스 동적 패키징 사용 호환성을 위해 hello 멀티플렉서의 청크 모드 tooGOP count 또는 기간을 구성 하 고 청크 too1 당 hello Gop를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-300">For compatibility with Azure Media Services dynamic packaging, configure hello multiplexer's Chunk Mode tooGOP count or duration and set hello GOPs per chunk too1.</span></span> <span data-ttu-id="7056b-301">(Hello 기본 이어야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-301">(This should be hello default.)</span></span>

![Muxer 청크 모드](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="7056b-303">*Muxer 청크 모드*</span><span class="sxs-lookup"><span data-stu-id="7056b-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="7056b-304">참고: 수도 있습니다 toorepeat이이 프로세스 다른 비트 전송률 및 해상도 toohave 사용할 조합을 toohello 자산 출력을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-304">Note: you may want toorepeat this process for any other bitrate and resolution combinations you want toohave added toohello asset output.</span></span>

### <span data-ttu-id="7056b-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>구성 hello 파일 출력 이름</span><span class="sxs-lookup"><span data-stu-id="7056b-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring hello file output names</span></span>
<span data-ttu-id="7056b-306">둘 이상의 단일 파일에 추가 된 toohello 출력 자산을 개가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-306">We have more than one single file added toohello output asset.</span></span> <span data-ttu-id="7056b-307">파일 이름의 각 hello에 대 한 출력 파일은 서로 다릅니다 및 미정도 적용 파일 명명 규칙 되므로 것을 알 수 hello 파일 이름에서으로 처리 하는 필요성 toomake 있는지 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-307">This provides a need toomake sure hello filenames for each of hello output files are different from each other and maybe even apply a file-naming convention so it becomes clear from hello file name what you're dealing with.</span></span>

<span data-ttu-id="7056b-308">Hello 디자이너에서 식을 통해 파일 출력 이름 지정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-308">File output naming can be controlled through expressions in hello designer.</span></span> <span data-ttu-id="7056b-309">Hello 출력 파일 구성 요소 중 하나에 대 한 hello 속성 창을 열고 hello 파일 속성에 대 한 hello 식 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-309">Open hello property pane for one of hello File Output components and open hello expression editor for hello File property.</span></span> <span data-ttu-id="7056b-310">다음 식은 hello를 통해 구성 된이 첫 번째 출력 파일 (hello 자습서에서 이동 하는 것에 대 한 참조 [MXF tooa 단일 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span><span class="sxs-lookup"><span data-stu-id="7056b-310">Our first output file was configured through hello following expression (see hello tutorial for going from [MXF tooa single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="7056b-311">즉, 우리의 파일 이름을 두 변수에 의해 결정 됩니다: hello 및를 출력 디렉터리 toowrite에 hello 소스 파일의 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-311">This means that our filename is determined by two variables: hello output directory toowrite in and hello source file base name.</span></span> <span data-ttu-id="7056b-312">hello 전자 hello 워크플로 루트를 속성으로 노출 됩니다 및 후자 hello hello 들어오는 파일에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-312">hello former is exposed as a property on hello workflow root and hello latter is determined by hello incoming file.</span></span> <span data-ttu-id="7056b-313">로컬 테스트;에 대해 사용 하는 것이 hello 출력 디렉터리는 note 이 속성은 Azure 미디어 서비스에서 hello 클라우드 기반 미디어 프로세서에서 hello 워크플로가 실행 될 때 hello 워크플로 엔진에 의해 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-313">Note that hello output directory is what you use for local testing; this property will be overridden by hello workflow engine when hello workflow is executed by hello cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="7056b-314">toogive 두 출력 파일 이름 지정 일관 된 출력을 변경 hello 명명 식을 첫 번째 파일:</span><span class="sxs-lookup"><span data-stu-id="7056b-314">toogive both our output files a consistent output naming, change hello first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7056b-315">및를 두 번째로 hello:</span><span class="sxs-lookup"><span data-stu-id="7056b-315">and hello second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7056b-316">Toomake MP4 출력 파일을 모두 올바르게 생성 되도록 실행 하는 중간 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-316">Execute an intermediate test run toomake sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="7056b-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>별도 오디오 트랙 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="7056b-318">.Ism 파일 toogo MP4 출력 파일 생성 하는 경우 나중에 볼 수 있겠지만, 것도 필요 오디오 전용 MP4 파일을 hello 오디오 트랙으로 우리의 적응 스트리밍에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-318">As we'll see later when we generate an .ism file toogo with our MP4 output files, we will also require a audio-only MP4 file as hello audio track for our adaptive streaming.</span></span> <span data-ttu-id="7056b-319">(ISO-mpeg-4 멀티플렉서) 추가 muxer toohello 워크플로 추가 toocreate이 파일을 연결 하 고 hello AAC 인코더 출력 핀 있는 해당 입력된 핀 트랙 1에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-319">toocreate this file, add an additional muxer toohello workflow (ISO-MPEG-4 Multiplexer) and connect hello AAC encoder's output pin with its input pin for Track 1.</span></span>

![추가된 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="7056b-321">*추가된 오디오 Muxer*</span><span class="sxs-lookup"><span data-stu-id="7056b-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="7056b-322">세 번째 파일 출력 구성 요소 toooutput hello 아웃 바운드 스트림은 hello muxer에서 만들고 hello 파일 명명 식으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-322">Create a third File Output component toooutput hello outbound stream from hello muxer and configure hello file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![파일 출력을 생성하는 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="7056b-324">*파일 출력을 생성하는 오디오 Muxer*</span><span class="sxs-lookup"><span data-stu-id="7056b-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="7056b-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Hello를 추가 합니다. ISM SMIL 파일</span><span class="sxs-lookup"><span data-stu-id="7056b-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding hello .ISM SMIL File</span></span>
<span data-ttu-id="7056b-326">Hello 동적 패키징 toowork 함께 두 MP4 파일 (및 오디오 전용 MP4 hello) 당사의 미디어 서비스 자산에도 필요 매니페스트 파일 ("SMIL" 파일이 라고도: 멀티미디어 Integration 언어 동기화).</span><span class="sxs-lookup"><span data-stu-id="7056b-326">For hello dynamic packaging toowork in combination with both MP4 files (and hello audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="7056b-327">이 파일 MP4 파일을 동적 패키징 및 hello 오디오 스트리밍에 대 한 이러한 tooconsider 중에 사용할 수 있는 tooAzure 미디어 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-327">This file indicates tooAzure Media Services what MP4 files are available for dynamic packaging and which of those tooconsider for hello audio streaming.</span></span> <span data-ttu-id="7056b-328">단일 오디오 스트림이 있는 MP4의 집합에 대한 일반적인 매니페스트 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

<span data-ttu-id="7056b-329">hello 개별 MP4 비디오 파일의 참조 tooeach switch 문 내에서 포함 된 hello.ism 파일 및 오디오 파일 toothose도 하나 이상의 tooan hello 오디오 포함 하는 MP4를 참조 하는 또한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-329">hello .ism file contains within a switch statement, a reference tooeach of hello individual MP4 video files and in addition toothose also one (or more) audio file references tooan MP4 that only contains hello audio.</span></span>

<span data-ttu-id="7056b-330">MP4의의 집합에 대 한 hello 매니페스트 파일을 생성 "AMS 매니페스트 Writer" hello 라는 구성 요소를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-330">Generating hello manifest file for our set of MP4's can be done through a component called hello "AMS Manifest Writer".</span></span> <span data-ttu-id="7056b-331">toouse, hello 화면으로 끌어 및 hello 세 개의 출력 파일 구성 요소 toohello 입력 AMS 매니페스트 기록기에서에서 hello "쓰기 완료" 출력 핀을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-331">toouse it, drag it onto hello surface and connect hello "Write Complete" output pins from hello three File Output components toohello AMS Manifest Writer input.</span></span> <span data-ttu-id="7056b-332">Hello AMS 매니페스트 기록기 toohello 출력 파일/자산의 tooconnect hello 출력 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-332">Then make sure tooconnect hello output of hello AMS Manifest Writer toohello Output File/Asset.</span></span>

<span data-ttu-id="7056b-333">이 다른 파일 출력 구성 요소와 마찬가지로 hello.ism 파일 출력 이름을 하는 식으로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-333">As with our other file output components, configure hello .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="7056b-334">완료 된 워크플로 hello 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-334">Our finished workflow looks like hello below:</span></span>

![완성 된 MXF toomultibitrate MP4 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="7056b-336">*완성 된 MXF toomultibitrate MP4 워크플로*</span><span class="sxs-lookup"><span data-stu-id="7056b-336">*Finished MXF toomultibitrate MP4 workflow*</span></span>

## <span data-ttu-id="7056b-337"><a id="MXF_to__multibitrate_MP4"></a>다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진</span><span class="sxs-lookup"><span data-stu-id="7056b-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="7056b-338">Hello에 [이전 워크플로 연습](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) 어떻게 단일 MXF 입력된 자산으로 변환할 수 출력 자산을 다중 비트 전송률 MP4 파일, 오디오 전용 MP4 파일 매니페스트 파일을 Azure 미디어와 함께에서 사용 하 여 버퍼 오버런 서비스 동적 패키징입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-338">In hello [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="7056b-339">이 연습에서는 어떻게 hello 측면의 일부 향상 및 수 더 편리 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-339">This walkthrough will show how some of hello aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="7056b-340"><a id="MXF_to_multibitrate_MP4_overview"></a>워크플로 개요 tooenhance</span><span class="sxs-lookup"><span data-stu-id="7056b-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview tooenhance</span></span>
![다중 비트 전송률 MP4 워크플로 tooenhance](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="7056b-342">*다중 비트 전송률 MP4 워크플로 tooenhance*</span><span class="sxs-lookup"><span data-stu-id="7056b-342">*Multibitrate MP4 workflow tooenhance*</span></span>

### <span data-ttu-id="7056b-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="7056b-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="7056b-344">Hello 이전 워크플로에서 출력 파일 이름을 생성 hello 기준으로 단순 식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-344">In hello previous workflow we specified a simple expression as hello basis for generating output file names.</span></span> <span data-ttu-id="7056b-345">하지만 일부 중복 있는: hello hello 개별 출력 파일 구성 요소를 모두 지정 된 이러한 식입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-345">We have some duplication though: all of hello hello individual output file components specified such expression.</span></span>

<span data-ttu-id="7056b-346">예를 들어 hello 첫 번째 비디오 파일에 대 한 파일 출력 구성 요소는이 식을 사용 하 여 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-346">For example, our file output component for hello first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="7056b-347">동안 hello 두 번째 출력에 비디오와 같은 식을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-347">While for hello second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="7056b-348">대신 이러한 중복을 제거하고 더 구성 가능하게 된다면 간결하며 오류가 발생할 가능성이 적고 더 편리해질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="7056b-349">다행히을 활용해 서: hello 기능 toocreate 우리의 워크플로 루트에서 사용자 지정 속성을 조합 하 여 hello 디자이너의 식 기능 편의 추가 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-349">Luckily we can: hello designer's expression capabilities in combination with hello ability toocreate custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="7056b-350">Hello 비트 전송률 MP4 파일을 개별 hello에서에서 드라이브 파일 이름 구성 하겠습니다 우리 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-350">Let's assume we'll drive filename configuration from hello bitrates of hello individual MP4 files.</span></span> <span data-ttu-id="7056b-351">이러한 비트 전송률 tooconfigure 하나의 중앙에서 항상 건강 합니다 (에 배치할 hello 그래프의 루트 우리의)에서 위치 액세스 tooconfigure 및 드라이브 파일 이름 생성 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-351">These bitrates we'll aim tooconfigure in one central place (on hello root of our graph), from where they'll be accessed tooconfigure and drive file name generation.</span></span> <span data-ttu-id="7056b-352">toodo이 hello AVC 인코더의 경우와 마찬가지로 모두 hello 루트에서 액세스할 수 있도록 두 AVC 인코더 toohello 루트 우리의 워크플로의 hello 비트 전송률 속성을 게시 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-352">toodo this, we start by publishing hello bitrate property from both AVC encoders toohello root of our workflow, so that it becomes accessible from both hello root as well as from hello AVC encoders.</span></span> <span data-ttu-id="7056b-353">(두 개의 서로 다른 위치에 표시되는 경우에도 기본 값은 하나입니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="7056b-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>게시에 hello 워크플로 루트 구성 요소 속성</span><span class="sxs-lookup"><span data-stu-id="7056b-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto hello workflow root</span></span>
<span data-ttu-id="7056b-355">첫 번째 AVC 인코더 hello를 열고 toohello 비트 전송률 (kbps) 속성이 이동 hello 드롭다운에서 게시를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-355">Open hello first AVC encoder, go toohello Bitrate (kbps) property and from hello dropdown choose Publish.</span></span>

![게시 hello 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="7056b-357">*게시 hello 비트 전송률 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-357">*Publishing hello bitrate property*</span></span>

<span data-ttu-id="7056b-358">Hello 구성 "1 비트 전송률 비디오"의 읽을 수 있는 표시 이름 및 "video1bitrate"의 게시 이름 대화 toopublish toohello 루트 우리의 워크플로 그래프의 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-358">Configure hello publish dialog toopublish toohello root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="7056b-359">"비트 전송률 스트리밍"이라는 사용자 지정 그룹 이름을 구성하고 게시를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![게시 hello 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="7056b-361">*비트 전송률 속성에 게시 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7056b-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="7056b-362">반복 hello hello의 hello 비트 전송률 속성에 대해 동일 AVC 인코더의 두 번째 하 고 이름을 "video2bitrate" "2 비트 전송률 비디오"의 표시 이름으로, "비트 전송률 스트리밍" 사용자 지정 같은 그룹 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-362">Repeat hello same for hello bitrate property of hello second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in hello same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="7056b-363">에서는 이제 hello 워크플로 루트 속성을 검사, 사용자 지정 그룹을 표시 되는 두 개의 게시 속성 hello로를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-363">If we now inspect hello workflow root properties, we'll see our custom group with hello two published properties show up.</span></span> <span data-ttu-id="7056b-364">해당 AVC 인코더 비트 전송률의 hello 값을 반영 하는 둘 다 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-364">Both are reflecting hello value of their respective AVC encoder bitrate.</span></span>

![워크플로 루트에 게시된 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="7056b-366">Tooaccess 코드 또는 식에서 이러한 속성을 원하는 때마다 다음과 같이 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-366">Whenever we want tooaccess these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="7056b-367">hello 루트 바로 아래 구성 요소에서 인라인 코드 로부터: node.getPropertyAsString('.. / video1bitrate', null)</span><span class="sxs-lookup"><span data-stu-id="7056b-367">from inline code from a component right below hello root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="7056b-368">식 내에서: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="7056b-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="7056b-369">우리의 오디오 트랙 비트 전송률에도 게시 하 여 hello "비트 전송률 스트리밍" 그룹을 완료 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-369">Let's complete hello "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="7056b-370">Hello AAC 인코더의 hello 속성 내에서 hello 비트 전송률 설정에 대 한 검색 하 고 hello 드롭다운 다음 tooit에서 게시를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-370">Within hello properties of hello AAC Encoder, search for hello Bitrate setting and select Publish from hello dropdown next tooit.</span></span> <span data-ttu-id="7056b-371">이름이 "audio1bitrate"를 사용 하 여 hello 그래프의 toohello 루트를 게시 하 고 표시 이름 "오디오 1 비트 전송률" "비트 전송률 스트리밍" 사용자 지정 그룹 내에서 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-371">Publish toohello root of hello graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![오디오 비트 전송률에 게시 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="7056b-373">*오디오 비트 전송률에 게시 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7056b-373">*Publishing dialog for audio bitrate*</span></span>

![루트의 결과 비디오 및 오디오 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="7056b-375">*루트의 결과 비디오 및 오디오 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="7056b-376">이러한 세 가지 중 하나를 변경 값도 다시 구성 되며 변경 내용이 hello hello 해당 구성 요소와 연결 된 값 (및에서 게시 된 경우).</span><span class="sxs-lookup"><span data-stu-id="7056b-376">Note that changing any of those three values also re-configures and changes hello values on hello respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="7056b-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>게시된 속성 값을 사용하는 출력 파일 이름 생성</span><span class="sxs-lookup"><span data-stu-id="7056b-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="7056b-378">하드 코딩 하는 대신이 생성 된 파일 이름을 변경할 수 있습니다 이제 각 hello 출력 파일 구성 요소 toorely hello 그래프 루트에 게시 된 뿐 우리 hello 비트 전송률 속성에서이 파일 이름 식입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of hello File Output components toorely on hello bitrate properties we just published on hello graph root.</span></span> <span data-ttu-id="7056b-379">첫 번째 파일 출력을 hello 파일 속성을 찾을 hello 식을 다음과 같이 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-379">Starting with our first file output, find hello File property and edit hello expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="7056b-380">이 식에 다른 매개 변수 hello 액세스 하 고 hello 식 창에서 작업 하는 동안 hello 키보드 hello 달러 기호를 클릭 하 여 입력 한 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-380">hello different parameters in this expression can be accessed and entered by hitting hello dollar sign on hello keyboard while in hello expression window.</span></span> <span data-ttu-id="7056b-381">Hello 사용 가능한 매개 변수 중 하나는 우리의 video1bitrate 속성 이전에 게시입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-381">One of hello available parameters is our video1bitrate property which we published earlier.</span></span>

![식 내에서 매개 변수 액세스](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="7056b-383">*식 내에서 매개 변수 액세스*</span><span class="sxs-lookup"><span data-stu-id="7056b-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="7056b-384">수행의 두 번째 비디오에 대 한 hello 파일 출력에 대 한 동일한 hello:</span><span class="sxs-lookup"><span data-stu-id="7056b-384">Do hello same for hello file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="7056b-385">및 hello 오디오 전용 파일 출력:</span><span class="sxs-lookup"><span data-stu-id="7056b-385">and for hello audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="7056b-386">이제 hello 비디오 또는 오디오 파일 중 하나에 대 한 hello 비트 전송률을 변경 하면 hello 각 인코더 다시 구성 됩니다 및 hello 비트 전송률 기반 파일 이름 규칙은 모두 자동으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-386">If we now change hello bitrate for any of hello video or audio files, hello respective encoder will be reconfigured and hello bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="7056b-387"><a id="thumbnails_to__multibitrate_MP4"></a>축소판 그림 toomultibitrate MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails toomultibitrate MP4 output</span></span>
<span data-ttu-id="7056b-388">생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것을 미리 보기 toohello 출력을 추가 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails toohello output.</span></span>

### <span data-ttu-id="7056b-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>워크플로 개요 tooadd 미리 보기</span><span class="sxs-lookup"><span data-stu-id="7056b-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview tooadd thumbnails to</span></span>
![다중 비트 전송률 MP4 워크플로 toostart](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="7056b-391">*다중 비트 전송률 MP4 워크플로 toostart*</span><span class="sxs-lookup"><span data-stu-id="7056b-391">*Multibitrate MP4 workflow toostart from*</span></span>

### <span data-ttu-id="7056b-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>JPG 인코딩 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="7056b-393">이 축소판 이미지 생성의 hello 핵심 hello JPG Encoder 구성 요소 수 toooutput JPG 파일 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-393">hello heart of our thumbnail generation will be hello JPG Encoder component, able toooutput JPG files.</span></span>

![JPG 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="7056b-395">*JPG 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-395">*JPG Encoder*</span></span>

<span data-ttu-id="7056b-396">그러나 직접 우리의 압축 되지 않은 비디오 스트림 hello JPG 인코더에 미디어 파일 입력 hello에서 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-396">We cannot however directly connect our Uncompressed Video stream from hello Media File Input into hello JPG encoder.</span></span> <span data-ttu-id="7056b-397">대신, toobe 전달 개별 프레임 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-397">Instead, it expects toobe handed individual frames.</span></span> <span data-ttu-id="7056b-398">이 hello 비디오 프레임 게이트 구성 요소를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-398">This, we can do through hello Video Frame Gate component.</span></span>

![연결 프레임 게이트 toohello JPG 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="7056b-400">*연결 프레임 게이트 toohello JPG 인코더*</span><span class="sxs-lookup"><span data-stu-id="7056b-400">*Connecting a frame gate toohello JPG encoder*</span></span>

<span data-ttu-id="7056b-401">게이트 프레임 hello 사용 하면 비디오 프레임 toopass 모든 너무 많은 시간 (초) 또는 프레임 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-401">hello frame gate once every so many seconds or frames allows a video frame toopass.</span></span> <span data-ttu-id="7056b-402">hello 간격 및 hello 이런 있는 오프셋 시간은 hello 속성에서 구성 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-402">hello interval and hello time offset with which this happens is configurable in hello properties.</span></span>

![비디오 프레임 게이트 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="7056b-404">*비디오 프레임 게이트 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="7056b-405">Hello 모드 tooTime (초)을 설정 하 여 미리 보기 1 분 마다 만들기 하 고 간격 too60 hello 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-405">Let's create a thumbnail every minute by setting hello mode tooTime (seconds) and hello Interval too60.</span></span>

### <span data-ttu-id="7056b-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>색 공간 변환 처리</span><span class="sxs-lookup"><span data-stu-id="7056b-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="7056b-407">논리 것 모두 hello 프레임 게이트와 hello 미디어 파일 입력의 압축 되지 않은 비디오 핀 이제 연결 될 수 있습니다, 그리고 우리 대기줄 경고에서는 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-407">While it would seem logical both Uncompressed Video pins of hello frame gate and hello Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![입력 색 공간 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="7056b-409">*입력 색 공간 오류*</span><span class="sxs-lookup"><span data-stu-id="7056b-409">*Input color space error*</span></span>

<span data-ttu-id="7056b-410">즉, 어떤 컬러 정보가 표시 됩니다는 원래 원시 압축 되지 않은 비디오 스트림의 우리의 MXF에서 들어오는 hello 방법은 JPG 인코더에 필요 하지만 어떤 hello에서 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-410">This is because hello way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what hello JPG Encoder is expecting.</span></span> <span data-ttu-id="7056b-411">tooflow 예상은 특히는 소위 "색 공간"의 "RGB" 또는 "회색" 더 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected tooflow in.</span></span> <span data-ttu-id="7056b-412">즉, 해당 hello 비디오 프레임 게이트의 인바운드 비디오 스트림 toohave는 색 공간에 대 한이 먼저 적용 변환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-412">This means that hello Video Frame Gate's inbound video stream will need toohave a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="7056b-413">Hello 워크플로 hello 색 공간 변환기-Intel 끌고 tooour 프레임 게이트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-413">Drag onto hello workflow hello Color Space Converter - Intel and connect it tooour frame gate.</span></span>

![색 공간 변환 연결](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="7056b-415">*색 공간 변환 연결*</span><span class="sxs-lookup"><span data-stu-id="7056b-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="7056b-416">Hello 속성 창에서 hello BGR 24 항목 hello 사전 설정 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-416">In hello properties window, pick hello BGR 24 entry from hello Preset list.</span></span>

### <span data-ttu-id="7056b-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>쓰기 hello 미리 보기</span><span class="sxs-lookup"><span data-stu-id="7056b-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing hello thumbnails</span></span>
<span data-ttu-id="7056b-418">우리의 MP4 비디오에서 다른, hello 파일 하나 이상 JPG 인코더 구성 요소 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-418">Different from our MP4 video's, hello JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="7056b-419">이 순서 toodeal에서 장면 검색 JPG 파일 기록기 구성 요소를 사용할 수 있습니다: 들어오는 hello JPG 미리 보기를 수행 하 고 여러 되 고 그 뒤에 각 파일 이름으로 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-419">In order toodeal with this, a Scene Search JPG File Writer component can be used: it will take hello incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="7056b-420">(일반적으로 hello hello 스트림 hello 축소판 그림의에서 시간 (초) / 단위 수를 나타내는 hello 숫자에서 출발 했습니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-420">(hello number typically indicating hello number of seconds/units in hello stream which hello thumbnail was drawn from.)</span></span>

![장면 검색 JPG 파일 기록기 용 hello 소개](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="7056b-422">*장면 검색 JPG 파일 기록기 용 hello 소개*</span><span class="sxs-lookup"><span data-stu-id="7056b-422">*Introducing hello Scene Search JPG File Writer*</span></span>

<span data-ttu-id="7056b-423">Hello 식을 사용 하 여 hello 출력 폴더 경로 속성 구성: ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="7056b-423">Configure hello Output Folder Path property with hello expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="7056b-424">및 파일 이름 접두사 속성을 hello:</span><span class="sxs-lookup"><span data-stu-id="7056b-424">and hello Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="7056b-425">hello 접두사 hello 축소판 파일은 이름이 지정 되 고 방식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-425">hello prefix will determine how hello thumbnail files are being named.</span></span> <span data-ttu-id="7056b-426">Hello 스트림 내의 위치를 숫자 나타내는 hello 엄지 것은 붙어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-426">They will be suffixed with a number indicating hello thumb's position in hello stream.</span></span>

![장면 검색 JPG 파일 기록기 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="7056b-428">*장면 검색 JPG 파일 기록기 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="7056b-429">Hello 장면 검색 JPG 파일 기록기 용 toohello 출력 파일/자산 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-429">Connect hello Scene Search JPG File Writer toohello Output File/Asset node.</span></span>

### <span data-ttu-id="7056b-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>워크플로에서 오류 감지</span><span class="sxs-lookup"><span data-stu-id="7056b-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="7056b-431">Hello 색 공간 변환기 toohello 원시 압축 되지 않은 비디오 출력의 hello 입력을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-431">Connect hello input of hello color space converter toohello raw uncompressed video output.</span></span> <span data-ttu-id="7056b-432">이제 실행 hello 워크플로에 대 한 로컬 테스트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-432">Now perform a local test run for hello workflow.</span></span> <span data-ttu-id="7056b-433">될 가능성이 높은 hello 워크플로 갑자기 실행을 중지 하 고 오류가 발생 하는 hello 구성 요소에 대해 빨간색 윤곽선으로 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-433">There's a good chance hello workflow will suddenly stop executing and indicate with a red outline on hello component that encountered an error:</span></span>

![색 공간 변환기 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="7056b-435">*색 공간 변환기 오류*</span><span class="sxs-lookup"><span data-stu-id="7056b-435">*Color Space Converter error*</span></span>

<span data-ttu-id="7056b-436">Hello 인코딩 시도가 실패 하는 hello 이유는 무엇 hello의 오른쪽 위 모서리 hello 색 공간 변환기 구성 요소 toosee에서에서 약간 빨간색 hello "E" 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-436">Click hello little red "E" icon in hello top right corner of hello Color Space Converter component toosee what's hello reason hello encoding attempt failed.</span></span>

![색 공간 변환기 오류 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="7056b-438">*색 공간 변환기 오류 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="7056b-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="7056b-439">Hello 들어오는 색 공간 hello 색 공간 변환기에 대 한 표준에 대 한 YUV tooRGB 우리의 요청한 변환 toobe rec601 있는지, 볼 수 있듯이을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-439">It turns out, as you can see, that hello incoming color space standard for hello color space converter has toobe rec601 for our requested conversion of YUV tooRGB.</span></span> <span data-ttu-id="7056b-440">스트림은 rec601을 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="7056b-441">(Rec 601은 디지털 비디오 형태로 인터레이스된 아날로그 비디오 신호를 인코딩하기 위한 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="7056b-442">720 광도 샘플 및 줄 당 360 색차 샘플을 포함하는 활성 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="7056b-443">인코딩 시스템 hello 색 YCbCr 4 라고: 2:2.)</span><span class="sxs-lookup"><span data-stu-id="7056b-443">hello color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="7056b-444">toofix이 म rec601 콘텐츠로 처리할 우리의 스트림의 hello 메타 데이터에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-444">toofix this, we'll indicate on hello metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="7056b-445">toodo 되므로 원시 원본과 hello 색 공간 변환 구성 요소 간의 입력 비디오 데이터 형식 업데이트 프로그램 구성 요소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-445">toodo so we'll use a Video Data Type Updater component, which we'll put in between our raw source and hello color space conversion component.</span></span> <span data-ttu-id="7056b-446">이 데이터 형식 업데이트 프로그램 형식 속성을 특정 비디오 데이터를 수동으로 업데이트 hello 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-446">This data type updater allows for hello manual update of certain video data type properties.</span></span> <span data-ttu-id="7056b-447">Tooindicate는 색 공간 표준 "Rec 601"의 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-447">Configure it tooindicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="7056b-448">이렇게 하면 hello 비디오 데이터 형식 업데이트 프로그램 tootag hello 스트림 hello "Rec 601" 색 공간을 가진 경우 아직 정의 색 공간이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-448">This will cause hello Video Data Type Updater tootag hello stream with hello "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="7056b-449">(하지 파일로 재정의 됩니다 기존 메타 데이터, hello 재정의 확인란을 선택 하지 않으면.)</span><span class="sxs-lookup"><span data-stu-id="7056b-449">(It will not override any existing metadata, unless hello Override checkbox was checked.)</span></span>

![데이터 형식 업데이트 프로그램 hello에 색 공간 표준 업데이트](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="7056b-451">*데이터 형식 업데이트 프로그램 hello에 색 공간 표준 업데이트*</span><span class="sxs-lookup"><span data-stu-id="7056b-451">*Updating Color Space Standard on hello Data Type Updater*</span></span>

### <span data-ttu-id="7056b-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="7056b-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="7056b-453">이제 우리 워크플로 완료 되 면 통과 하는 다른 테스트 실행 toosee 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-453">Now that our our workflow is finished, do another test run toosee it pass.</span></span>

![미리 보기로 다중 mp4 출력에 대해 완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="7056b-455">*미리 보기로 다중 mp4 출력에 대해 완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="7056b-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="7056b-456"><a id="time_based_trim"></a>다중 비트 전송률 MP4 출력의 시간 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="7056b-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7056b-457">생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것 트리밍 hello 소스 비디오 타임 스탬프를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on time-stamps.</span></span>

### <span data-ttu-id="7056b-458"><a id="time_based_trim_start"></a>워크플로 개요 toostart 트리밍을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-458"><a id="time_based_trim_start"></a>Workflow overview toostart adding trimming to</span></span>
![워크플로 tooadd 조정을 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="7056b-460">*워크플로 tooadd 조정을 시작*</span><span class="sxs-lookup"><span data-stu-id="7056b-460">*Starting workflow tooadd trimming to*</span></span>

### <span data-ttu-id="7056b-461"><a id="time_based_trim_use_stream_trimmer"></a>스트림 트리머 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-461"><a id="time_based_trim_use_stream_trimmer"></a>Using hello Stream Trimmer</span></span>
<span data-ttu-id="7056b-462">hello 스트림 트리머 구성 요소는 타이밍 정보 (초, 분,...)를 기준으로 tootrim hello 시작과 끝의 입력된 스트림 있습니다. hello 트리머 프레임 기반 트리밍을 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-462">hello Stream Trimmer component allows tootrim hello beginning and ending of an input stream base on timing information (seconds, minutes, ...). hello trimmer does not support frame-based trimming.</span></span>

![스트림 트리머](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="7056b-464">*스트림 트리머*</span><span class="sxs-lookup"><span data-stu-id="7056b-464">*Stream Trimmer*</span></span>

<span data-ttu-id="7056b-465">Hello AVC 인코더 및 스피커 위치 assigner toohello 미디어 파일 입력을 직접 연결 하는 대신 이러한 hello 스트림 트리머 사이 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-465">Instead of linking hello AVC encoders and speaker position assigner toohello Media File Input directly, we'll put in between those hello stream trimmer.</span></span> <span data-ttu-id="7056b-466">(Hello 비디오 신호 및 hello에 대 한 인터리빙 된 오디오 신호입니다.)</span><span class="sxs-lookup"><span data-stu-id="7056b-466">(One for hello video signal and one for hello interleaved audio signal.)</span></span>

![사이 간 스트림 트리머 배치](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="7056b-468">*사이 간 스트림 트리머 배치*</span><span class="sxs-lookup"><span data-stu-id="7056b-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="7056b-469">비디오 및 오디오 15 초에서 60 초 hello 비디오에서 사이만 처리 합니다 있도록 보겠습니다 hello 트리머를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-469">Let's configure hello trimmer so that we will only process video and audio between 15 seconds and 60 seconds in hello video.</span></span>

<span data-ttu-id="7056b-470">Hello 비디오 스트림 트리머의 toohello 속성 이동한 다음 (15) 시작 시간 및 종료 시간 (60 초) 속성을 모두 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-470">Go toohello properties of hello Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="7056b-471">toomake 두 당사의 오디오 및 비디오 트리머가 항상 구성 된 toohello 동일 앞뒤에 값이 있는지, 해당 toohello 워크플로 루트를 hello 발표 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-471">toomake sure both our audio and video trimmer are always configured toohello same start and end values, we will publish those toohello root of hello workflow.</span></span>

![스트림 트리머에서 시작 시간 속성 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="7056b-473">*스트림 트리머에서 시작 시간 속성 게시*</span><span class="sxs-lookup"><span data-stu-id="7056b-473">*Publish start time property from Stream Trimmer*</span></span>

![시작 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="7056b-475">*시작 시간에 속성 대화 상자 게시*</span><span class="sxs-lookup"><span data-stu-id="7056b-475">*Publish property dialog for start time*</span></span>

![종료 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="7056b-477">*종료 시간에 속성 대화 상자 게시*</span><span class="sxs-lookup"><span data-stu-id="7056b-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="7056b-478">म hello 우리의 워크플로 루트 이제 검사를 하는 경우 두 속성 모두 깔끔하게 표시 되 고 구성 가능한 여기에서.</span><span class="sxs-lookup"><span data-stu-id="7056b-478">If we now inspect hello root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![루트에 사용 가능한 게시된 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="7056b-480">*루트에 사용 가능한 게시된 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-480">*Published properties available on root*</span></span>

<span data-ttu-id="7056b-481">이제 hello 트리밍 속성 hello 오디오 트리머에서 열고 toohello 참조 하는 식으로 모두 시작 및 종료 시간을 구성 워크플로의 hello 루트에 대 한 속성을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-481">Now open hello trimming properties from hello audio trimmer and configure both start and end times with an expression that refers toohello published properties on hello root of our workflow.</span></span>

<span data-ttu-id="7056b-482">Hello에 대 한 오디오 트리밍 시작 시간:</span><span class="sxs-lookup"><span data-stu-id="7056b-482">For hello audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="7056b-483">그리고 종료 시간을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="7056b-484"><a id="time_based_trim_finish"></a>완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="7056b-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="7056b-486">*완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="7056b-486">*Finished Workflow*</span></span>

## <span data-ttu-id="7056b-487"><a id="scripting"></a>스크립트 구성 요소를 hello 소개</span><span class="sxs-lookup"><span data-stu-id="7056b-487"><a id="scripting"></a>Introducing hello Scripted Component</span></span>
<span data-ttu-id="7056b-488">스크립트 구성 요소 워크플로 hello 실행 단계 중 임의의 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-488">Scripted Components can execute arbitrary scripts during hello execution phases of our workflow.</span></span> <span data-ttu-id="7056b-489">실행 될 수 있는 다른 스크립트는 4 개가 각각 특정 한 특성 및 hello 워크플로 수명 주기에서 자신의 위치:</span><span class="sxs-lookup"><span data-stu-id="7056b-489">There are four different scripts that can be executed, each with specific characteristics and their own place in hello workflow life-cycle:</span></span>

* <span data-ttu-id="7056b-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="7056b-490">**commandScript**</span></span>
* <span data-ttu-id="7056b-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="7056b-491">**realizeScript**</span></span>
* <span data-ttu-id="7056b-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="7056b-492">**processInputScript**</span></span>
* <span data-ttu-id="7056b-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="7056b-493">**lifeCycleScript**</span></span>

<span data-ttu-id="7056b-494">스크립트 구성 요소 각 위의 hello에 대 한 자세히가 이동 hello hello 문서화 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-494">hello documentation of hello Scripted Component goes in more detail for each of hello above.</span></span> <span data-ttu-id="7056b-495">[섹션 다음 hello](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** hello 워크플로 시작할 때 스크립트 구성 요소는 사용 되는 tooconstruct hello 신속 하 게 cliplist xml입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-495">In [hello following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** scripting component is used tooconstruct a cliplist xml on hello fly when hello workflow starts.</span></span> <span data-ttu-id="7056b-496">이 스크립트의 수명에 한 번만 수행 됨 hello 구성 요소 설치 하는 동안 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-496">This script is called during hello component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="7056b-497"><a id="scripting_hello_world"></a>워크플로 내의 스크립팅: Hello World</span><span class="sxs-lookup"><span data-stu-id="7056b-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="7056b-498">Hello 디자이너 화면에 스크립트 구성 요소를 끌어 하 고 (예: "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="7056b-498">Drag a Scripted Component onto hello designer surface and rename it (for example, "SetClipListXML").</span></span>

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7056b-500">*스크립팅된 구성 요소 추가*</span><span class="sxs-lookup"><span data-stu-id="7056b-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7056b-501">hello 속성을 검사할 때 스크립트 구성 요소, 다른 스크립트 유형은 나타납니다 hello, 각 구성 가능한 tooa 다른 스크립트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-501">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7056b-503">*스크립팅된 구성 요소 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-503">*Scripted Component properties*</span></span>

<span data-ttu-id="7056b-504">지우기 processInputScript hello 고 realizeScript hello에 대 한 hello 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-504">Clear hello processInputScript and open hello editor for hello realizeScript.</span></span> <span data-ttu-id="7056b-505">이제를 설정 하는 하 고 toostart 스크립트를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-505">Now we're set up and ready toostart scripting.</span></span>

<span data-ttu-id="7056b-506">스크립트 Groovy, Java와의 호환성을 유지 하는 hello Java 플랫폼에 대 한 동적으로 컴파일된 스크립트 언어로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-506">Scripts are written in Groovy, a dynamically compiled scripting language for hello Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="7056b-507">사실 대부분의 Java 코드는 유효한 Groovy 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="7056b-508">우리의 realizeScript의 hello 컨텍스트에서 간단한 hello world 하시면 스크립트를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-508">Let's write a simple hello world groovy script in hello context of our realizeScript.</span></span> <span data-ttu-id="7056b-509">Hello 편집기에서 hello 다음을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-509">Enter hello following in hello editor:</span></span>

    node.log("hello world");

<span data-ttu-id="7056b-510">이제 로컬 테스트 실행을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-510">Now execute a local test run.</span></span> <span data-ttu-id="7056b-511">이 실행 한 후 검사할 (hello 시스템 탭을 통해 구성 요소 스크립팅 hello) hello 로그 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-511">After this run, inspect (through hello System tab on hello Scripted Component) hello Logs property.</span></span>

![Hello World 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="7056b-513">*Hello World 로그 출력*</span><span class="sxs-lookup"><span data-stu-id="7056b-513">*Hello world log output*</span></span>

<span data-ttu-id="7056b-514">hello 로그 메서드를 호출 하는 hello 노드 개체 tooour 현재 "노드" 또는 hello 구성 요소 내에서 스크립팅 하는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-514">hello node object we call hello log method on, refers tooour current "node" or hello component we're scripting within.</span></span> <span data-ttu-id="7056b-515">따라서을 hello 기능 toooutput 로깅 데이터를 hello 시스템을 통해 사용할 수 있는 모든 구성 요소입니다. 이 경우에서는 문자열 리터럴 "hello world" hello를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-515">Every component as such has hello ability toooutput logging data, available through hello system tab. In this case, we output hello string literal "hello world".</span></span> <span data-ttu-id="7056b-516">중요 한 toounderstand 여기에이 증명할 수 toobe hello 스크립트를 실제로에 대 한 정보를 제공 하는 매우 유용한 디버깅 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-516">Important toounderstand here is that this can prove toobe an invaluable debugging tool, providing you with insight on what hello script is actually doing.</span></span>

<span data-ttu-id="7056b-517">스크립팅 우리의 환경 내에서 해야 액세스 tooproperties 다른 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-517">From within our scripting environment, we also have access tooproperties on other components.</span></span> <span data-ttu-id="7056b-518">다음을 실행해보세요.</span><span class="sxs-lookup"><span data-stu-id="7056b-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="7056b-519">이 로그 창 다음 hello를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-519">Our log window will show us hello following:</span></span>

![노드 경로에 액세스하기 위한 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="7056b-521">*노드 경로에 액세스하기 위한 로그 출력*</span><span class="sxs-lookup"><span data-stu-id="7056b-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="7056b-522"><a id="frame_based_trim"></a>다중 비트 전송률 MP4 출력의 프레임 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="7056b-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="7056b-523">생성 하는 워크플로 시작 [입력는 MXF에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), 이제 살펴볼 것 잘라내기의 프레임 수에 비해 hello 원본 비디오에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming hello source video based on frame counts.</span></span>

### <span data-ttu-id="7056b-524"><a id="frame_based_trim_start"></a>조정을 추가 개요 toostart 세부 계획</span><span class="sxs-lookup"><span data-stu-id="7056b-524"><a id="frame_based_trim_start"></a>Blueprint overview toostart adding trimming to</span></span>
![워크플로 toostart 트리밍을 추가 합니다.](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="7056b-526">*워크플로 toostart 트리밍을 추가 합니다.*</span><span class="sxs-lookup"><span data-stu-id="7056b-526">*Workflow toostart adding trimming to*</span></span>

### <span data-ttu-id="7056b-527"><a id="frame_based_trim_clip_list"></a>Hello 클립 목록 XML을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7056b-527"><a id="frame_based_trim_clip_list"></a>Using hello Clip List XML</span></span>
<span data-ttu-id="7056b-528">모든 이전 워크플로 자습서 hello 미디어 파일 입력 구성 요소는 비디오 입력된 원본으로 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-528">In all previous workflow tutorials, we used hello Media File Input component as our video input source.</span></span> <span data-ttu-id="7056b-529">이 특정 시나리오에 대 한 하지만 사용할 예정 hello 클립 목록 원본 구성 요소 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-529">For this specific scenario though, we'll be using hello Clip List Source component instead.</span></span> <span data-ttu-id="7056b-530">참고 hello 되지 않아야이 방식으로 작업;의 기본 설정 hello 클립 목록 소스는 실제 이유 toodo 하므로 경우에 사용 (hello 하는 중 있는 경우 아래에는 hello 클립 목록 지우기 기능을 사용).</span><span class="sxs-lookup"><span data-stu-id="7056b-530">Note that this should not be hello preferred way of working; only use hello Clip List Source when there's a real reason toodo so (like in hello below case, where we're making use of hello clip list trimming capabilities).</span></span>

<span data-ttu-id="7056b-531">당사의 미디어 파일 입력 toohello 클립 목록 소스에서에서 tooswitch hello 디자인 화면으로 끌어오는 hello 클립 목록 원본 구성 요소를 hello 워크플로 디자이너의 hello 클립 목록 XML pin toohello 클립 목록 XML 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-531">tooswitch from our Media File Input toohello Clip List Source, drag hello Clip List Source component onto hello design surface and connect hello Clip List XML pin toohello Clip List XML node of hello workflow designer.</span></span> <span data-ttu-id="7056b-532">이 hello 클립 목록 소스 tooour 입력된 비디오에 따라 출력 핀으로 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-532">This should populate hello Clip List Source with output pins, according tooour input video.</span></span> <span data-ttu-id="7056b-533">이제 hello hello 클립 목록 소스 toohello에서 hello 압축 되지 않은 비디오 및 오디오를 압축 되지 않은 pin을 연결할 각 AVC 인코더 및 오디오 스트림 인터리브 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-533">Now connect hello Uncompressed Video and Uncompressed Audio pins from hello hello Clip List Source toohello respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="7056b-534">이제 hello 미디어 파일 입력을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-534">Now remove hello Media File Input.</span></span>

![미디어 파일 입력 hello 클립 목록 소스 hello로 대체](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="7056b-536">*미디어 파일 입력 hello 클립 목록 소스 hello로 대체*</span><span class="sxs-lookup"><span data-stu-id="7056b-536">*Replaced hello Media File Input with hello Clip List Source*</span></span>

<span data-ttu-id="7056b-537">hello 클립 목록 원본 구성 요소는 입력으로 사용해 "클립 목록 XML"입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-537">hello Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="7056b-538">와 소스 파일 tootest hello를 로컬에 선택이 클립 목록 xml은을 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-538">When selecting hello source file tootest with locally, this clip list xml is auto-populated for you.</span></span>

![자동으로 채워진 클립 목록 XML 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="7056b-540">*자동으로 채워진 클립 목록 XML 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="7056b-541">좀 더 가깝기 때문 toohello xml을 찾고,이 같은 모양을:</span><span class="sxs-lookup"><span data-stu-id="7056b-541">Looking a bit closer toohello xml, this is how it looks like:</span></span>

![클립 목록 대화 상자 편집](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="7056b-543">*클립 목록 대화 상자 편집*</span><span class="sxs-lookup"><span data-stu-id="7056b-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="7056b-544">그러나이 반영 하지 않습니다 hello 클립 목록 xml의 hello 기능.</span><span class="sxs-lookup"><span data-stu-id="7056b-544">This however does not reflect hello capabilities of hello clip list xml.</span></span> <span data-ttu-id="7056b-545">한 가지 옵션은 tooadd hello 비디오 및 오디오 소스, 다음과 같이 모두에서 "트리밍" 요소.</span><span class="sxs-lookup"><span data-stu-id="7056b-545">One option we have is tooadd a "Trim" element under both hello video and audio source, like this:</span></span>

![트림 요소 toohello 클립 목록 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="7056b-547">*트림 요소 toohello 클립 목록 추가*</span><span class="sxs-lookup"><span data-stu-id="7056b-547">*Adding a trim element toohello clip list*</span></span>

<span data-ttu-id="7056b-548">Hello 비디오 위에 다음과 같이 hello 클립 목록 xml을 수정 하 고 로컬 테스트를 실행 하는 경우 나타납니다 잘못 된 hello 비디오에서 10에서 20 초 사이의 잘립니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-548">If you modify hello clip list xml like this above and perform a local test run, you'll see hello video correctly been trimmed between 10 and 20 seconds in hello video.</span></span>

<span data-ttu-id="7056b-549">반대 toowhat이 동일한 cliplist xml hello Azure 미디어 서비스에서 실행 되는 워크플로에서 적용 될 때 효과가 같음 없는 경우 로컬 실행을 할 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-549">Contrary toowhat happens when you do a local run though, this very same cliplist xml would not have hello same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="7056b-550">Azure 프리미엄 인코더가 시작 되 면 hello cliplist xml 입력된 파일 hello 인코딩 hello에 따라 다시 될 때마다 생성 될 때 작업이 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-550">When Azure Premium Encoder starts, hello cliplist xml is generated every time again, based on hello input file hello encoding job was given.</span></span> <span data-ttu-id="7056b-551">즉, hello xml에 대해 수행 하는 변경 내용을 아쉽게도 재정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-551">This means that any changes we do on hello xml would unfortunately be overridden.</span></span>

<span data-ttu-id="7056b-552">toocounter hello cliplist xml 인코딩 작업 시작 될 때 초기화 되 고 다시 생성할 수 것 hello 신속 하 게 취급 워크플로의 hello 시작 후 바로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-552">toocounter hello cliplist xml being wiped when an encoding job is started, we can re-generate it on hello fly just after hello start of our workflow.</span></span> <span data-ttu-id="7056b-553">"스크립팅된 구성 요소"라는 것을 통해 이러한 사용자 지정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="7056b-554">자세한 내용은 참조 [소개 hello 구성 요소 스크립팅](media-services-media-encoder-premium-workflow-tutorials.md#scripting)합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-554">For more information, see [Introducing hello Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="7056b-555">스크립트 구성 요소 hello 디자이너 화면으로 끌어서 너무 이름 바꾸기 "SetClipListXML"입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-555">Drag a Scripted Component onto hello designer surface and rename it too"SetClipListXML".</span></span>

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="7056b-557">*스크립팅된 구성 요소 추가*</span><span class="sxs-lookup"><span data-stu-id="7056b-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="7056b-558">hello 속성을 검사할 때 스크립트 구성 요소, 다른 스크립트 유형은 나타납니다 hello, 각 구성 가능한 tooa 다른 스크립트 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-558">When you inspect hello properties of hello Scripted Component, hello four different script types will be shown, each configurable tooa different script.</span></span>

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="7056b-560">*스크립팅된 구성 요소 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="7056b-561"><a id="frame_based_trim_modify_clip_list"></a>스크립트 구성 요소에서 hello 클립 목록을 수정</span><span class="sxs-lookup"><span data-stu-id="7056b-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying hello clip list from a Scripted Component</span></span>
<span data-ttu-id="7056b-562">Hello cliplist 생성 된 xml을 워크플로 시작 하는 동안 다시 작성할 수 있습니다, 전에 toohave 액세스 toohello cliplist xml 속성 및 내용 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-562">Before we can re-write hello cliplist xml that is generated during workflow startup, we'll need toohave access toohello cliplist xml property and contents.</span></span> <span data-ttu-id="7056b-563">다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![기록된 들어오는 클립 목록](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="7056b-565">*기록된 들어오는 클립 목록*</span><span class="sxs-lookup"><span data-stu-id="7056b-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="7056b-566">먼저 다음 방식으로 toodetermine 해야 tootrim 지점인까지 원하는 하는 시점을 hello 비디오.</span><span class="sxs-lookup"><span data-stu-id="7056b-566">First we need a way toodetermine from which point till which point we want tootrim hello video.</span></span> <span data-ttu-id="7056b-567">toomake hello 워크플로의이 편리한 toohello 간단한 기술 사용자 게시 hello 그래프의 두 가지 속성 toohello 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-567">toomake this convenient toohello less-technical user of hello workflow, publish two properties toohello root of hello graph.</span></span> <span data-ttu-id="7056b-568">toodo이 hello 디자이너 화면을 마우스 오른쪽 단추로 클릭 하 고 "속성 추가"를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-568">toodo this, right click hello designer surface and select "Add Property":</span></span>

* <span data-ttu-id="7056b-569">첫 번째 속성: 형식의 "ClippingTimeStart": "시간 코드"</span><span class="sxs-lookup"><span data-stu-id="7056b-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="7056b-570">두 번째 속성: 형식의 "ClippingTimeEnd": "시간 코드"</span><span class="sxs-lookup"><span data-stu-id="7056b-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![클리핑 시작 시간에 속성 대화 상자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="7056b-572">*클리핑 시작 시간에 속성 대화 상자 추가*</span><span class="sxs-lookup"><span data-stu-id="7056b-572">*Add Property dialog for clipping start time*</span></span>

![워크플로 루트에 게시된 클리핑 시간 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="7056b-574">*워크플로 루트에 게시된 클리핑 시간 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="7056b-575">두 속성 tooa 적합 한 값을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-575">Configure both properties tooa suitable value:</span></span>

![시작 및 끝 속성 클리핑 hello 구성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="7056b-577">*시작 및 끝 속성 클리핑 hello 구성*</span><span class="sxs-lookup"><span data-stu-id="7056b-577">*Configure hello clipping start and end properties*</span></span>

<span data-ttu-id="7056b-578">이제 스크립트 내에서 다음과 같은 두 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![클리핑의 시작 및 종료를 보여주는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="7056b-580">*클리핑의 시작 및 종료를 보여주는 로그 창*</span><span class="sxs-lookup"><span data-stu-id="7056b-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="7056b-581">보겠습니다 간단한 정규식을 사용 하 여 더 편리 toouse 양식으로 hello 시간 코드 문자열을 구문 분석:</span><span class="sxs-lookup"><span data-stu-id="7056b-581">Let's parse hello timecode strings into a more convenient toouse form, using a simple regular expression:</span></span>

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![구문 분석된 시간 코드의 출력이 있는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="7056b-583">*구문 분석된 시간 코드의 출력이 있는 로그 창*</span><span class="sxs-lookup"><span data-stu-id="7056b-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="7056b-584">이 정보를 이제 hello cliplist xml tooreflect hello 시작을 수정할 수 있습니다 및 hello에 대 한 종료 시간 프레임을 정확 하 게 클리핑 hello 동영상의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-584">With this information at hand, we can now modify hello cliplist xml tooreflect hello start and end times for hello desired frame-accurate clipping of hello movie.</span></span>

![스크립트 코드 tooadd 트림 요소](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="7056b-586">*스크립트 코드 tooadd 트림 요소*</span><span class="sxs-lookup"><span data-stu-id="7056b-586">*Script code tooadd trim elements*</span></span>

<span data-ttu-id="7056b-587">이 작업은 일반 문자열 조작 작업을 통해 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="7056b-588">hello 결과 수정 된 클립 목록 xml은 다시 기록 toohello clipListXML 속성 hello 워크플로 루트에 hello "setProperty" 메서드를 통해.</span><span class="sxs-lookup"><span data-stu-id="7056b-588">hello resulting modified clip list xml is written back toohello clipListXML property on hello workflow root through hello "setProperty" method.</span></span> <span data-ttu-id="7056b-589">hello 로그 창 다른 테스트 실행 한 후에 다음 hello 보여주실:</span><span class="sxs-lookup"><span data-stu-id="7056b-589">hello log window after another test run would show us hello following:</span></span>

![Hello 결과 클립 목록 로깅](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="7056b-591">*Hello 결과 클립 목록 로깅*</span><span class="sxs-lookup"><span data-stu-id="7056b-591">*Logging hello resulting clip list*</span></span>

<span data-ttu-id="7056b-592">Hello 비디오 및 오디오 스트림이 자르는 방법을 테스트 실행 toosee를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-592">Do a test-run toosee how hello video and audio streams have been clipped.</span></span> <span data-ttu-id="7056b-593">그러나 Hello 트리밍 지점에 대 한 값이 서로 다른 여러 개 테스트 실행, 작업을 하는 것은 고려 되지 않습니다 수 알 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="7056b-593">As you'll do more than one test-run with different values for hello trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="7056b-594">이 대 한 hello 이유는 해당 hello 디자이너 hello Azure 런타임 달리, 모든 실행 hello cliplist xml를 재정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-594">hello reason for this is that hello designer, unlike hello Azure runtime, does NOT override hello cliplist xml every run.</span></span> <span data-ttu-id="7056b-595">즉,만 hello hello를 설정 하면 처음으로 시작 및 종료 지점에서 않도록 hello xml tootransform, 시간, 우리의 가드 절 hello 모든 다른 (하는 경우 (clipListXML.indexOf ("<trim>")-1 = =)) hello 워크플로 트림 다른 추가 되지 것입니다 요소 한 개가 있는 경우 이미 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-595">This means that only hello very first time you have set hello in and out points, will cause hello xml tootransform, all hello other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent hello workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="7056b-596">toomake 우리의 워크플로 편리한 tootest 로컬로 최상의 우리 트림 요소가 이미 있는 경우를 검사 하는 일부 집 유지 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-596">toomake our workflow convenient tootest locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="7056b-597">이 경우 hello 새 값을 사용 하 여 hello xml을 수정 하 여 계속 하기 전에 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-597">If so, we can remove it before continuing by modifying hello xml with hello new values.</span></span> <span data-ttu-id="7056b-598">실제 xml 개체를 통해이 모델을 구문 분석 하는 것 보다 안전한 toodo는 것 대신 일반 문자열 조작을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-598">Rather than using plain string manipulations, it's probably safer toodo this through real xml object model parsing.</span></span>

<span data-ttu-id="7056b-599">하지만 이러한 코드 추가할 수 있습니다, 전에 tooadd 스크립트의 다양 한 hello에 대 한 import 문 먼저 시작 해야:</span><span class="sxs-lookup"><span data-stu-id="7056b-599">Before we can add such code though, we'll need tooadd a number of import statements at hello start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="7056b-600">그러면 코드를 정리 하는 데 필요한 hello를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-600">After this, we can add hello required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="7056b-601">이 코드는 hello 트림 요소 toohello cliplist xml을 추가 하는 hello 지점 바로 위에 놓입니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-601">This code goes just above hello point at which we add hello trim elements toohello cliplist xml.</span></span>

<span data-ttu-id="7056b-602">이 시점에서 실행 하 고 hello 변경 내용을 계속 적용 하는 동안 원하는 만큼 시간 처럼 워크플로 수정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-602">At this point, we can run and modify our workflow as much as we want while having hello changes applied ever time.</span></span>    

### <span data-ttu-id="7056b-603"><a id="frame_based_trim_clippingenabled_prop"></a>ClippingEnabled 편의 속성 추가</span><span class="sxs-lookup"><span data-stu-id="7056b-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="7056b-604">항상 원하지 트리밍 toohappen, 대로 보겠습니다 마무리 하기만 하면 워크플로 편리 하 게 나타내는 부울 플래그를 추가 하 여 tooenable 트리밍 / 클리핑 원하는 여부.</span><span class="sxs-lookup"><span data-stu-id="7056b-604">As you might not always want trimming toohappen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want tooenable trimming / clipping.</span></span>

<span data-ttu-id="7056b-605">와 마찬가지로 이전에 "부울" 형식의 "ClippingEnabled" 라는 워크플로 중 새 속성 toohello 루트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-605">Just as before, publish a new property toohello root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![클리핑 설정에 게시된 속성 ](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="7056b-607">*클리핑 설정에 게시된 속성*</span><span class="sxs-lookup"><span data-stu-id="7056b-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="7056b-608">간단한 가드 절 아래의 hello와 트리밍 해야 하는 경우를 확인 하 고 클립 목록 수정 toobe 따라서 있어야 하는 경우를 결정 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7056b-608">With hello below simple guard clause, we can check if trimming is required and decide if our clip list as such needs toobe modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="7056b-609"><a id="code"></a>코드 완료</span><span class="sxs-lookup"><span data-stu-id="7056b-609"><a id="code"></a>Complete code</span></span>
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a><span data-ttu-id="7056b-610">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7056b-610">Also see</span></span>
[<span data-ttu-id="7056b-611">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="7056b-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7056b-612">어떻게 tooUse Azure 미디어 서비스에서 프리미엄 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-612">How tooUse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="7056b-613">Azure Media Service로 주문형 콘텐츠 인코딩</span><span class="sxs-lookup"><span data-stu-id="7056b-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="7056b-614">미디어 인코더 Premium 워크플로 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="7056b-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="7056b-615">샘플 워크플로 파일</span><span class="sxs-lookup"><span data-stu-id="7056b-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="7056b-616">Azure 미디어 서비스 탐색기 도구</span><span class="sxs-lookup"><span data-stu-id="7056b-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="7056b-617">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="7056b-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7056b-618">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="7056b-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
