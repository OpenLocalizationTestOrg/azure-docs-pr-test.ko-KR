---
title: "고급 미디어 인코더 Premium 워크플로 자습서"
description: "이 문서는 미디어 인코더 Premium 워크플로를 사용한 고급 작업을 수행하는 방법 및 워크플로 디자이너르 사용한 복잡한 워크플로를 만드는 방법을 보여주는 연습을 포함합니다."
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
ms.openlocfilehash: 565497bd5a35e3c4d69d29512307cf3ca2364bdd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a><span data-ttu-id="5257c-103">고급 미디어 인코더 Premium 워크플로 자습서</span><span class="sxs-lookup"><span data-stu-id="5257c-103">Advanced Media Encoder Premium Workflow tutorials</span></span>
## <a name="overview"></a><span data-ttu-id="5257c-104">개요</span><span class="sxs-lookup"><span data-stu-id="5257c-104">Overview</span></span>
<span data-ttu-id="5257c-105">이 문서는 **워크플로 디자이너**를 사용하여 워크플로를 사용자 지정하는 방법을 보여주는 연습을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-105">This document contains walkthroughs that show how to customize workflows with  **Workflow Designer**.</span></span> <span data-ttu-id="5257c-106">[여기](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples)서 실제 워크플로 파일을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-106">You can find the actual workflow files [here](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).</span></span>  

## <a name="toc"></a><span data-ttu-id="5257c-107">목차</span><span class="sxs-lookup"><span data-stu-id="5257c-107">TOC</span></span>
<span data-ttu-id="5257c-108">다음 항목이 다루어집니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-108">The following topics are covered:</span></span>

* [<span data-ttu-id="5257c-109">단일 비트 전송률 MP4로 MXF 인코딩</span><span class="sxs-lookup"><span data-stu-id="5257c-109">Encoding MXF into a single bitrate MP4</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [<span data-ttu-id="5257c-110">새 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="5257c-110">Starting a new workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [<span data-ttu-id="5257c-111">미디어 파일 입력 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-111">Using the Media File Input</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [<span data-ttu-id="5257c-112">미디어 스트림 검사</span><span class="sxs-lookup"><span data-stu-id="5257c-112">Inspecting media streams</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [<span data-ttu-id="5257c-113">MP4 파일 생성을 위해 비디오 인코더 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-113">Adding a video encoder for .MP4 file generation</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [<span data-ttu-id="5257c-114">오디오 스트림 인코딩</span><span class="sxs-lookup"><span data-stu-id="5257c-114">Encoding the audio stream</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [<span data-ttu-id="5257c-115">MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱</span><span class="sxs-lookup"><span data-stu-id="5257c-115">Multiplexing Audio and Video streams into an MP4 container</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [<span data-ttu-id="5257c-116">MP4 파일 작성</span><span class="sxs-lookup"><span data-stu-id="5257c-116">Writing the MP4 file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [<span data-ttu-id="5257c-117">출력 파일에서 미디어 서비스 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="5257c-117">Creating a Media Services Asset from the output file</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [<span data-ttu-id="5257c-118">완료된 워크플로 로컬로 테스트</span><span class="sxs-lookup"><span data-stu-id="5257c-118">Test the finished workflow locally</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [<span data-ttu-id="5257c-119">다중 비트 전송률 MP4로 MXF 인코딩 - 동적 패키징 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-119">Encoding MXF into multibitrate MP4s - dynamic packaging enabled</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [<span data-ttu-id="5257c-120">하나 이상의 추가 MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-120">Adding one or more additional MP4 outputs</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [<span data-ttu-id="5257c-121">파일 출력 이름 구성</span><span class="sxs-lookup"><span data-stu-id="5257c-121">Configuring the file output names</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [<span data-ttu-id="5257c-122">별도 오디오 트랙 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-122">Adding a separate Audio Track</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [<span data-ttu-id="5257c-123">.ISM SMIL 파일 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-123">Adding the .ISM SMIL File</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [<span data-ttu-id="5257c-124">다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진</span><span class="sxs-lookup"><span data-stu-id="5257c-124">Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [<span data-ttu-id="5257c-125">강화할 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-125">Workflow overview to enhance</span></span>](#workflow-overview-to-enhance)
  * [<span data-ttu-id="5257c-126">파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="5257c-126">File Naming Conventions</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [<span data-ttu-id="5257c-127">워크플로 루트에 구성 요소 속성 게시</span><span class="sxs-lookup"><span data-stu-id="5257c-127">Publishing component properties onto the workflow root</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [<span data-ttu-id="5257c-128">게시된 속성 값을 사용하는 출력 파일 이름 생성</span><span class="sxs-lookup"><span data-stu-id="5257c-128">Have generated output file names rely on published property values</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [<span data-ttu-id="5257c-129">다중 비트 전송률 MP4 출력에 미리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-129">Adding thumbnails to multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [<span data-ttu-id="5257c-130">미리 보기를 추가하는 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-130">Workflow overview to add thumbnails to</span></span>](#workflow-overview-to-add-thumbnails-to)
  * [<span data-ttu-id="5257c-131">JPG 인코딩 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-131">Adding JPG Encoding</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [<span data-ttu-id="5257c-132">색 공간 변환 처리</span><span class="sxs-lookup"><span data-stu-id="5257c-132">Dealing with Color Space conversion</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [<span data-ttu-id="5257c-133">미리 보기 작성</span><span class="sxs-lookup"><span data-stu-id="5257c-133">Writing the thumbnails</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [<span data-ttu-id="5257c-134">워크플로에서 오류 감지</span><span class="sxs-lookup"><span data-stu-id="5257c-134">Detecting errors in a workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [<span data-ttu-id="5257c-135">완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="5257c-135">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [<span data-ttu-id="5257c-136">다중 비트 전송률 MP4 출력의 시간 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="5257c-136">Time-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [<span data-ttu-id="5257c-137">트리밍을 추가하기 시작하려는 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-137">Workflow overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [<span data-ttu-id="5257c-138">스트림 트리머 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-138">Using the Stream Trimmer</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [<span data-ttu-id="5257c-139">완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="5257c-139">Finished Workflow</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [<span data-ttu-id="5257c-140">스크립팅한 구성 요소 소개</span><span class="sxs-lookup"><span data-stu-id="5257c-140">Introducing the Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [<span data-ttu-id="5257c-141">워크플로 내의 스크립팅: Hello World</span><span class="sxs-lookup"><span data-stu-id="5257c-141">Scripting within a workflow: hello world</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [<span data-ttu-id="5257c-142">다중 비트 전송률 MP4 출력의 프레임 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="5257c-142">Frame-based trimming of multibitrate MP4 output</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [<span data-ttu-id="5257c-143">트리밍을 추가하기 시작하려는 청사진 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-143">Blueprint overview to start adding trimming to</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [<span data-ttu-id="5257c-144">클립 목록 XML 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-144">Using the Clip List XML</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [<span data-ttu-id="5257c-145">스크립팅한 구성 요소에서 클립 목록 수정</span><span class="sxs-lookup"><span data-stu-id="5257c-145">Modifying the clip list from a Scripted Component</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [<span data-ttu-id="5257c-146">ClippingEnabled 편의 속성 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-146">Adding a ClippingEnabled convenience property</span></span>](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <span data-ttu-id="5257c-147"><a id="MXF_to_MP4"></a>단일 비트 전송률 MP4로 MXF 인코딩</span><span class="sxs-lookup"><span data-stu-id="5257c-147"><a id="MXF_to_MP4"></a>Encoding MXF into a single bitrate MP4</span></span>
<span data-ttu-id="5257c-148">이 연습에서는 .MXF 입력 파일에서 AAC-HE 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-148">In this walkthrough we'll create a single bitrate .MP4 file with AAC-HE encoded audio from an .MXF input file.</span></span>

### <span data-ttu-id="5257c-149"><a id="MXF_to_MP4_start_new"></a>새 워크플로 시작</span><span class="sxs-lookup"><span data-stu-id="5257c-149"><a id="MXF_to_MP4_start_new"></a>Starting a new workflow</span></span>
<span data-ttu-id="5257c-150">워크플로 디자이너를 열고 "파일"-"새 작업 영역"-"청사진 트랜스코딩"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-150">Open Workflow Designer and select "File"-"New Workspace"-"Transcode Blueprint"</span></span>

<span data-ttu-id="5257c-151">새 워크플로는 3개 요소를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-151">The new workflow will show 3 elements:</span></span>

* <span data-ttu-id="5257c-152">기본 원본 파일</span><span class="sxs-lookup"><span data-stu-id="5257c-152">Primary Source File</span></span>
* <span data-ttu-id="5257c-153">클립 목록 XML</span><span class="sxs-lookup"><span data-stu-id="5257c-153">Clip List XML</span></span>
* <span data-ttu-id="5257c-154">출력 파일/자산</span><span class="sxs-lookup"><span data-stu-id="5257c-154">Output File/Asset</span></span>  

![새 인코딩 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

<span data-ttu-id="5257c-156">*새 인코딩 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-156">*New Encoding Workflow*</span></span>

### <span data-ttu-id="5257c-157"><a id="MXF_to_MP4_with_file_input"></a>미디어 파일 입력 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-157"><a id="MXF_to_MP4_with_file_input"></a>Using the Media File Input</span></span>
<span data-ttu-id="5257c-158">입력 미디어 파일을 허용하기 위해 미디어 파일 입력 구성 요소를 추가하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-158">In order to accept our input media file, one starts with adding a Media File Input component.</span></span> <span data-ttu-id="5257c-159">워크플로에 구성 요소를 추가하려면 리포지토리 검색 상자에서 구성 요소를 찾고 디자이너 창으로 원하는 항목을 끕니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-159">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span> <span data-ttu-id="5257c-160">미디어 파일 입력에 이 작업을 수행하고 미디어 파일 입력에서 파일 이름 입력 핀에 기본 원본 파일 구성 요소를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-160">Do this for the Media File Input and connect the Primary Source File component to the Filename input pin from the Media File Input.</span></span>

![연결된 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

<span data-ttu-id="5257c-162">*연결된 미디어 파일 입력*</span><span class="sxs-lookup"><span data-stu-id="5257c-162">*Connected Media File Input*</span></span>

<span data-ttu-id="5257c-163">다른 많은 작업을 실행하기 전에 먼저 워크플로 디자이너에 워크플로를 디자인하는 데 사용하려는 샘플 파일을 설명해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-163">Before we can do much else, we'll first need to indicate to the workflow designer what sample file we'd like to use to design our workflow with.</span></span> <span data-ttu-id="5257c-164">이렇게 하려면 디자이너 창 배경을 클릭하고 오른쪽 속성 창에서 기본 원본 파일 속성을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-164">To do so, click the designer pane background and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="5257c-165">폴더 아이콘을 클릭하고 원하는 파일을 선택하여 워크플로를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-165">Click the folder icon and select the desired file to test the workflow with.</span></span> <span data-ttu-id="5257c-166">이 작업이 완료되는 즉시 미디어 파일 입력 구성 요소는 파일을 검사하고 해당 출력 핀을 채워서 검사한 파일을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-166">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file it inspected.</span></span>

![채워진 미디어 파일 입력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

<span data-ttu-id="5257c-168">*채워진 미디어 파일 입력*</span><span class="sxs-lookup"><span data-stu-id="5257c-168">*Populated Media File Input*</span></span>

<span data-ttu-id="5257c-169">작업하려는 입력을 지정하는 반면 인코딩된 출력이 이동해야 하는 위치를 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-169">While this specifies with what input we'd like to work with, it doesn't tell yet where the encoded output should go to.</span></span> <span data-ttu-id="5257c-170">이제 기본 원본 파일의 구성 방법과 유사하게 아래의 출력 폴더 변수 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-170">Similar to how the Primary Source File was configured, now configure the Output Folder Variable property, just below it.</span></span>

![구성된 입력 및 출력 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

<span data-ttu-id="5257c-172">*구성된 입력 및 출력 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-172">*Configured Input and Output properties*</span></span>

### <span data-ttu-id="5257c-173"><a id="MXF_to_MP4_streams"></a>미디어 스트림 검사</span><span class="sxs-lookup"><span data-stu-id="5257c-173"><a id="MXF_to_MP4_streams"></a>Inspecting media streams</span></span>
<span data-ttu-id="5257c-174">종종 워크플로를 통해 흐르는 스트림의 모양을 알고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-174">Often it's desired to know how the stream looks like that flows through the workflow.</span></span> <span data-ttu-id="5257c-175">워크플로의 어떤 시점에서 스트림을 검사하려면 구성 요소에서 출력 또는 입력 핀을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-175">To inspect a stream at any point in the workflow, just click an output or input pin on any of the components.</span></span> <span data-ttu-id="5257c-176">이 경우에 미디어 파일 입력에서 압축되지 않은 비디오 출력 핀을 클릭해봅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-176">In this case, try clicking on the Uncompressed Video output pin from our Media File Input.</span></span> <span data-ttu-id="5257c-177">아웃 바운드 비디오를 검사할 수 있도록 하는 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-177">A dialog will open up that allows to inspect the outbound video.</span></span>

![압축되지 않은 비디오 출력 핀 검사](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

<span data-ttu-id="5257c-179">*압축되지 않은 비디오 출력 핀 검사*</span><span class="sxs-lookup"><span data-stu-id="5257c-179">*Inspecting the Uncompressed Video output pin*</span></span>

<span data-ttu-id="5257c-180">이 경우에 예를 들어 거의 2분인 비디오의 4:2:2 샘플링에서 초 당 24프레임으로 1920x1080 입력을 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-180">In our case, it tells us for example that we're dealing with a 1920x1080 input at 24 frames per second in 4:2:2 sampling for a video of almost 2 minutes.</span></span>

### <span data-ttu-id="5257c-181"><a id="MXF_to_MP4_file_generation"></a>MP4 파일 생성을 위해 비디오 인코더 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-181"><a id="MXF_to_MP4_file_generation"></a>Adding a video encoder for .MP4 file generation</span></span>
<span data-ttu-id="5257c-182">이제 압축되지 않은 비디오 및 여러 압축되지 않은 오디오 출력 핀을 미디어 파일 입력에 사용할 수 있다는 점을 기억합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-182">Note that now, an Uncompressed Video and multiple Uncompressed Audio output pins are available for use on our Media File Input.</span></span> <span data-ttu-id="5257c-183">인바운드 비디오를 인코딩하기 위해 인코딩 구성 요소가 필요하며 이 경우에 .MP4 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-183">In order to encode the inbound video, we need an encoding component - in this case for generating .MP4 files.</span></span>

<span data-ttu-id="5257c-184">비디오 스트림을 H.264로 인코딩하려면 AVC 비디오 인코더 구성 요소를 디자이너 화면에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-184">To encode the video stream to H.264, add the AVC Video Encoder component to the designer surface.</span></span> <span data-ttu-id="5257c-185">이 구성 요소는 압축되지 않은 비디오 스트림을 입력으로 사용하고 AVC 압축된 비디오 스트림을 해당 출력 핀에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-185">This component takes an uncompress video stream as input and delivers an AVC compressed video stream on its output pin.</span></span>

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

<span data-ttu-id="5257c-187">*연결되지 않은 AVC 인코더*</span><span class="sxs-lookup"><span data-stu-id="5257c-187">*Unconnected AVC Encoder*</span></span>

<span data-ttu-id="5257c-188">해당 속성은 인코딩이 정확하게 발생하는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-188">Its properties determine how the encoding exactly happens.</span></span> <span data-ttu-id="5257c-189">몇 가지 중요한 설정을 보도록 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-189">Let's have a look at some of the more important settings:</span></span>

* <span data-ttu-id="5257c-190">출력 너비 및 출력 높이: 인코딩된 비디오의 해상도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-190">Output width and Output height: these determine the resolution of the encoded video.</span></span> <span data-ttu-id="5257c-191">이 경우에 640x360로 결정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-191">In our case let's go with 640x360</span></span>
* <span data-ttu-id="5257c-192">프레임 속도: 통과로 설정하면 원본 프레임 속도를 채택하지만 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-192">Frame Rate: when set to passthrough it will just adopt the source frame rate, it's possible to override this though.</span></span> <span data-ttu-id="5257c-193">이러한 프레임 속도 변환은 동작 보정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-193">Note that such framerate conversion is not motion-compensated.</span></span>
* <span data-ttu-id="5257c-194">프로필 및 수준: AVC 프로필 및 수준을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-194">Profile and Level: these determine the AVC profile and level.</span></span> <span data-ttu-id="5257c-195">다양한 수준 및 프로필에 대한 자세한 정보를 편리하게 가져오려면 AVC 비디오 인코더 구성 요소에서 물음표 아이콘을 클릭하고 도움말 페이지는 각 수준에 대한 자세한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-195">To conveniently get more information about the different levels and profiles, click the question mark icon on the AVC Video Encoder component and the help page will show more detail about each of the levels.</span></span> <span data-ttu-id="5257c-196">이 샘플에서는 3.2(기본값) 수준에서 기본 프로필로  결정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-196">For our sample, let's go with Main Profile at level 3.2 (the default).</span></span>
* <span data-ttu-id="5257c-197">전송률 제어 모드 및 비트 전송률(kbps): 이 시나리오에서는 1200kbps에서 상수 비트 전송률(CBR) 출력을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-197">Rate Control Mode and Bitrate (kbps): in our scenario we opt for a constant bitrate (CBR) output at 1200 kbps</span></span>
* <span data-ttu-id="5257c-198">비디오 형식: H.264 스트림에 작성된 VUI(비디오 유용성 정보)에 대한 것입니다(디코더에서 디스플레이를 향상시키는 데 사용되지만 반드시 올바르게 디코딩하는 데 사용될 필요는 없는 부가 정보).</span><span class="sxs-lookup"><span data-stu-id="5257c-198">Video Format: this is about the VUI (Video Usability Information) that gets written into the H.264 stream (side information that might be used by a decoder to enhance the display but not essential to correctly decode):</span></span>
* <span data-ttu-id="5257c-199">NTSC(30fps를 사용하는 미국 또는 일본에 일반적임)</span><span class="sxs-lookup"><span data-stu-id="5257c-199">NTSC (typical for US or Japan, using 30 fps)</span></span>
* <span data-ttu-id="5257c-200">PAL(25fps를 사용하는 유럽에 일반적임)</span><span class="sxs-lookup"><span data-stu-id="5257c-200">PAL (typical for Europe, using 25 fps)</span></span>
* <span data-ttu-id="5257c-201">GOP 크기 모드: 여기서는 닫힌 GOP로 키 간격이 2초인 고정된 GOP 크기를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-201">GOP Size Mode: we'll configure Fixed GOP Size for our purposes with a Key Interval of 2 seconds with Closed GOPs.</span></span> <span data-ttu-id="5257c-202">이렇게 하면 동적 패키징 Azure 미디어 서비스와 호환성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-202">This ensures compatibility with the dynamic packaging Azure Media Services provides.</span></span>

<span data-ttu-id="5257c-203">AVC 인코더를 공급하려면 미디어 파일 입력 구성 요소에서 AVC 인코더의 압축되지 않은 비디오 입력 핀에 압축되지 않은 비디오 출력 핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-203">To feed our AVC encoder, connect the Uncompressed Video output pin from the Media File Input component to the Uncompressed Video input pin from the AVC encoder.</span></span>

![연결된 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

<span data-ttu-id="5257c-205">*연결된 AVC 기본 인코더*</span><span class="sxs-lookup"><span data-stu-id="5257c-205">*Connected AVC Main encoder*</span></span>

### <span data-ttu-id="5257c-206"><a id="MXF_to_MP4_audio"></a>오디오 스트림 인코딩</span><span class="sxs-lookup"><span data-stu-id="5257c-206"><a id="MXF_to_MP4_audio"></a>Encoding the audio stream</span></span>
<span data-ttu-id="5257c-207">이 시점에서 인코딩된 비디오가 있지만 원래 압축되지 않은 오디오 스트림을 압축해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-207">At this point, we have encoded video but the original uncompressed audio stream still needs to be compressed.</span></span> <span data-ttu-id="5257c-208">이를 위해 AAC 인코더(Dolby) 구성 요소에서 AAC 인코딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-208">For this we'll go with AAC encoding by the AAC Encoder (Dolby) component.</span></span> <span data-ttu-id="5257c-209">워크플로에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-209">Add it to the workflow.</span></span>

![연결되지 않은 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

<span data-ttu-id="5257c-211">*연결되지 않은 AAC 인코더*</span><span class="sxs-lookup"><span data-stu-id="5257c-211">*Unconnected AAC encoder*</span></span>

<span data-ttu-id="5257c-212">비호환성: 미디어 파일 입력에서 두 개의 압축되지 않은 오디오 스트림(왼쪽 오디오 채널 및 오른쪽 오디오 채널에 각각 하나)을 사용할 수 있는 반면 AAC 인코더에 압축되지 않은 단일 오디오 입력 핀이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-212">Now there's an incompatibility: there's only a single uncompressed audio input pin from the AAC Encoder while more than likely the Media File Input will have two different uncompressed audio stream available: one for the left audio channel and one for the right.</span></span> <span data-ttu-id="5257c-213">(서라운드 사운드를 처리하는 경우 6채널입니다.) 따라서 미디어 파일 입력 원본에서 AAC 오디오 인코더에 오디오를 직접 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-213">(If you're dealing with surround sound, that's 6 channels.) So it's not possible to directly connect the audio from the Media File Input source into the AAC audio encoder.</span></span> <span data-ttu-id="5257c-214">AAC 구성 요소는 소위 "인터리브" 오디오 스트림이 필요합니다: 서로 인터리브된 왼쪽 및 오른쪽 채널이 있는 단일 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-214">The AAC component expects a so-called "interleaved" audio stream: a single stream that has both the left and the right channels interleaved with each other.</span></span> <span data-ttu-id="5257c-215">어떤 오디오 트랙이 원본에서 어떤 위치에 있는지 원본 미디어 파일에서 알게 되면 왼쪽 및 오른쪽에 올바르게 할당된 스피커 위치로 이러한 인터리브 오디오 스트림을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-215">Once we know from our source media file which audio tracks are on what position in the source, we can generate such interleaved audio stream with the correctly assigned speaker positions for left and right.</span></span>

<span data-ttu-id="5257c-216">먼저 필요한 원본 오디오 채널에서 인터리브 스트림을 생성하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-216">First one will want to generated an interleaved stream from the required source audio channels.</span></span> <span data-ttu-id="5257c-217">오디오 스트림 인터리브 구성 요소가 이를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-217">The Audio Stream Interleaver component will handle this for us.</span></span> <span data-ttu-id="5257c-218">워크플로에 추가하고 미디어 파일 입력에서 오디오 출력을 여기에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-218">Add it to the workflow and connect the audio outputs from the Media File Input into it.</span></span>

![연결된 오디오 스트림 인터리버](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

<span data-ttu-id="5257c-220">*연결된 오디오 스트림 인터리버*</span><span class="sxs-lookup"><span data-stu-id="5257c-220">*Connected Audio Stream Interleaver*</span></span>

<span data-ttu-id="5257c-221">인터리브 오디오 스트림이 있으므로 왼쪽 또는 오른쪽 스피커 위치를 할당할 위치를 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-221">Now that we have an interleaved audio stream, we still didn't specify where to assign the left or right speaker positions to.</span></span> <span data-ttu-id="5257c-222">이 위치를 지정하기 위해 스피커 위치 할당자를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-222">In order to specify this, we can leverage the Speaker Position Assigner.</span></span>

![스피커 위치 할당자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

<span data-ttu-id="5257c-224">*스피커 위치 할당자 추가*</span><span class="sxs-lookup"><span data-stu-id="5257c-224">*Adding a Speaker Position Assigner*</span></span>

<span data-ttu-id="5257c-225">"사용자 지정"이라는 인코더 사전 설정 필터 및 "2.0 (L,R)"이라는 채널 사전 설정를 통해 스테레오 입력 스트림을 사용하도록 스피커 위치 할당자를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-225">Configure the Speaker Position Assigner for use with a stereo input stream through an Encoder Preset Filter of "Custom" and the Channel Preset called "2.0 (L,R)".</span></span> <span data-ttu-id="5257c-226">(채널1에 왼쪽 스피커 위치를 할당하고 채널2에 오른쪽 스피커 위치를 할당합니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-226">(This will assign the left speaker position to channel 1 and the right speaker position to channel 2.)</span></span>

<span data-ttu-id="5257c-227">AAC 인코더의 입력에 스피커 위치 할당자의 출력을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-227">Connect the output of the Speaker Position Assigner to the input of the AAC Encoder.</span></span> <span data-ttu-id="5257c-228">그런 다음 AAC 인코더가 "2.0 (L,R)" 채널 사전 설정으로 작업하므로 스테레오 오디오를 입력으로 처리하는 방법을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-228">Then, tell the AAC Encoder to work with a "2.0 (L,R)" Channel Preset, so it knows to deal with stereo audio as input.</span></span>

### <span data-ttu-id="5257c-229"><a id="MXF_to_MP4_audio_and_fideo"></a>MP4 컨테이너에 오디오 및 비디오 스트림 멀티플렉싱</span><span class="sxs-lookup"><span data-stu-id="5257c-229"><a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexing Audio and Video streams into an MP4 container</span></span>
<span data-ttu-id="5257c-230">AVC 인코딩된 비디오 스트림 및 AAC 인코딩된 오디오 스트림을 지정하여 둘 모두를 .MP4 컨테이너에 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-230">Given our AVC encoded video stream and our AAC encoded audio stream, we can capture both into an .MP4 container.</span></span> <span data-ttu-id="5257c-231">다양한 스트림을 하나로 혼합하는 프로세스는 "멀티플렉싱"(또는 "muxing")이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-231">The process of mixing different streams into a single one is called "multiplexing" (or "muxing").</span></span> <span data-ttu-id="5257c-232">이 경우에 일관된 단일 .MP4 패키지에서 오디오 및 비디오 스트림을 인터리브합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-232">In this case we're interleaving the audio and the video streams in a single coherent .MP4 package.</span></span> <span data-ttu-id="5257c-233">.MP4 컨테이너에 이 기능을 조정하는 구성 요소는 ISO MPEG-4 멀티플렉서라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-233">The component that coordinates this for an .MP4 container is called the ISO MPEG-4 Multiplexer.</span></span> <span data-ttu-id="5257c-234">이를 디자이너 화면에 추가하고 AVC 비디오 인코더 및 AAC 인코더를 입력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-234">Add one to the designer surface and connect both the AVC Video Encoder and the AAC Encoder to its inputs.</span></span>

![연결된 MPEG4 멀티플렉서](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

<span data-ttu-id="5257c-236">*연결된 MPEG4 멀티플렉서*</span><span class="sxs-lookup"><span data-stu-id="5257c-236">*Connected MPEG4 Multiplexer*</span></span>

### <span data-ttu-id="5257c-237"><a id="MXF_to_MP4_writing_mp4"></a>MP4 파일 작성</span><span class="sxs-lookup"><span data-stu-id="5257c-237"><a id="MXF_to_MP4_writing_mp4"></a>Writing the MP4 file</span></span>
<span data-ttu-id="5257c-238">출력 파일을 작성할 때 파일 출력 구성 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-238">When writing an output file, the File Output component is used.</span></span> <span data-ttu-id="5257c-239">ISO MPEG-4 멀티플렉서의 출력에 연결할 수 있으므로 해당 출력이 디스크에 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-239">We can connect this to the output of the ISO MPEG-4 Multiplexer so that its output gets written to disk.</span></span> <span data-ttu-id="5257c-240">이렇게 하려면 컨테이너(MPEG-4) 출력 핀을 파일 출력의 쓰기 입력 핀에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-240">To do this, connect the Container (MPEG-4) output pin to the Write input pin of the File Output.</span></span>

![연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

<span data-ttu-id="5257c-242">*연결된 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="5257c-242">*Connected File Output*</span></span>

<span data-ttu-id="5257c-243">사용되는 파일 이름은 파일 속성에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-243">The filename that will be used is determined by the File property.</span></span> <span data-ttu-id="5257c-244">해당 속성은 지정된 값에 하드 코딩될 수 있는 반면 대신 식을 통해 설정하려 할 가능성이 가장 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-244">While that property can be hardcoded to a given value, most likely one will want to set it through an expression instead.</span></span>

<span data-ttu-id="5257c-245">워크플로가 식에서 출력 파일 이름 속성을 자동으로 결정하려면 파일 이름 옆에 있는 단추를 클릭합니다(폴더 아이콘 옆에 있음).</span><span class="sxs-lookup"><span data-stu-id="5257c-245">To have the workflow automatically determine the output File name property from an expression, click the buton next to the File name (next to the folder icon).</span></span> <span data-ttu-id="5257c-246">그런 다음 드롭다운 메뉴에서 "식"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-246">From the drop down menu then select "Expression".</span></span> <span data-ttu-id="5257c-247">이렇게 하면 식 편집기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-247">This will bring up the expression editor.</span></span> <span data-ttu-id="5257c-248">편집기의 내용을 먼저 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-248">Clear the contents of the editor first.</span></span>

![빈 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

<span data-ttu-id="5257c-250">*빈 식 편집기*</span><span class="sxs-lookup"><span data-stu-id="5257c-250">*Empty Expression Editor*</span></span>

<span data-ttu-id="5257c-251">식 편집기는 리터럴 값을 입력할 수 있게 하고 이는 하나 이상의 변수와 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-251">The expression editor allows to enter any literal value, mixed with one or more variables.</span></span> <span data-ttu-id="5257c-252">변수는 달러 기호로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-252">Variables start with a dollar sign.</span></span> <span data-ttu-id="5257c-253">$ 키를 누르면 사용 가능한 변수로 선택한 드롭다운 상자가 편집기에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-253">As you hit the $ key, the editor will show a dropdown box with a choice of available variables.</span></span> <span data-ttu-id="5257c-254">이 경우에 출력 디렉터리 변수 및 기본 입력 파일 이름 변수의 조합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-254">In our case we'll use a combination of the output directory variable and the base input file name variable:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![채워진 식 편집기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

<span data-ttu-id="5257c-256">*채워진 식 편집기*</span><span class="sxs-lookup"><span data-stu-id="5257c-256">*Filled out Expression Editor*</span></span>

> [!NOTE]
> <span data-ttu-id="5257c-257">Azure에서 인코딩 작업의 출력 파일을 참조하기 위해 식 편집기에서 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-257">In order to see see an output file of your encoding job in Azure, you must provide a value in the expression editor.</span></span>
>
>

<span data-ttu-id="5257c-258">확인을 눌러 식을 확인하는 경우 속성 창으로 이 시점에서 제 시간에 파일 속성이 확인하는 값을 미리 봅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-258">When you confirm the expression by hitting ok, the property window will preview to what value the File property resolves at this point in time.</span></span>

![파일 식이 출력 dir 확인](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

<span data-ttu-id="5257c-260">*파일 식이 출력 dir 확인*</span><span class="sxs-lookup"><span data-stu-id="5257c-260">*File Expression resolves output dir*</span></span>

### <span data-ttu-id="5257c-261"><a id="MXF_to_MP4_asset_from_output"></a>출력 파일에서 미디어 서비스 자산 만들기</span><span class="sxs-lookup"><span data-stu-id="5257c-261"><a id="MXF_to_MP4_asset_from_output"></a>Creating a Media Services Asset from the output file</span></span>
<span data-ttu-id="5257c-262">MP4 출력 파일을 작성한 반면 미디어 서비스가 이 워크플로를 실행한 결과로 생성한 출력 자산에 이 파일이 속해 있음을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-262">While we have written an MP4 output file, we still need to indicate that this file belongs to the output asset which media services will generate as a result of executing this workflow.</span></span> <span data-ttu-id="5257c-263">이 마지막에 워크플로 캔버스의 출력 파일/자산 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-263">To this end, the Output File/Asset node on the workflow canvas is used.</span></span> <span data-ttu-id="5257c-264">이 노드에 들어오는 파일은 모두 결과적으로 Azure 미디어 서비스 자산의 일부가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-264">All incoming files into this node will make part of the resulting Azure Media Services asset.</span></span>

<span data-ttu-id="5257c-265">출력 파일/자산 구성 요소에 파일 출력 구성 요소를 연결하여 워크플로를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-265">Connect the File Output component to the Output File/Asset component to finish the workflow.</span></span>

![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

<span data-ttu-id="5257c-267">*완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-267">*Finished Workflow*</span></span>

### <span data-ttu-id="5257c-268"><a id="MXF_to_MP4_test"></a>완료된 워크플로 로컬로 테스트</span><span class="sxs-lookup"><span data-stu-id="5257c-268"><a id="MXF_to_MP4_test"></a>Test the finished workflow locally</span></span>
<span data-ttu-id="5257c-269">로컬에서 워크플로를 테스트하려면 맨 위에 있는 도구 모음에서 재생 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-269">To test the workflow locally, hit the play button in the toolbar at the top.</span></span> <span data-ttu-id="5257c-270">워크플로가 실행을 마치면 구성된 출력 폴더에 생성된 출력을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-270">When the workflow finished executing, inspect the output generated in the configured output folder.</span></span> <span data-ttu-id="5257c-271">MXF 입력 원본 파일에서 인코딩된 완료된 MP4 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-271">You'll see the finished MP4 output file that was encoded from the MXF input source file.</span></span>

## <span data-ttu-id="5257c-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>MP4로 MXF 인코딩 - 다중 비트 전송률 동적 패키징 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-272"><a id="MXF_to_MP4_with_dyn_packaging"></a>Encoding MXF into MP4 - multibitrate dynamic packaging enabled</span></span>
<span data-ttu-id="5257c-273">이 연습에서는 단일 .MXF 입력 파일에서 AAC 인코딩 오디오를 사용하여 단일 비트 전송률 MP4 파일의 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-273">In this walkthrough we'll create a set of multiple bitrate MP4 files with AAC encoded audio from a single .MXF input file.</span></span>

<span data-ttu-id="5257c-274">다중 비트 전송률 자산을 Azure 미디어 서비스에서 제공한 동적 패키징 기능과 함께 사용하려면 비트 전송률 및 해상도 각각에 여러 GOP로 정렬된 MP4 파일이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-274">When a multi-bitrate asset output is desired for use in combination with the Dynamic Packaging features offered by Azure Media Services, multiple GOP-aligned MP4 files of each a different bitrate and resolution will need to be generated.</span></span> <span data-ttu-id="5257c-275">이렇게 하려면 [단일 비트 전송률 MP4로 MXF 인코딩](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) 연습으로 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-275">To do so, the [Encoding MXF into a single bitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) walkthrough provides us with a good starting point.</span></span>

![워크플로 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

<span data-ttu-id="5257c-277">*워크플로 시작*</span><span class="sxs-lookup"><span data-stu-id="5257c-277">*Starting Workflow*</span></span>

### <span data-ttu-id="5257c-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>하나 이상의 추가 MP4 출력 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-278"><a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adding one or more additional MP4 outputs</span></span>
<span data-ttu-id="5257c-279">결과 Azure 미디어 서비스 자산의 모든 MP4 파일은 서로 다른 비트 전송률 및 해상도를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-279">Every MP4 file in our resulting Azure Media Services asset will support a different bitrate and resolution.</span></span> <span data-ttu-id="5257c-280">워크플로에 하나 이상의 MP4 출력 파일을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-280">Let's add one or more MP4 output files to the workflow.</span></span>

<span data-ttu-id="5257c-281">동일한 설정을 사용하여 만든 모든 비디오 인코더가 있는지 확인하는 작업은 기존 AVC 비디오 인코더를 복제하고 해상도 및 비트 전송률의 다른 조합을 구성하는 데 가장 편리합니다.(2,5Mbps로 초 당 25프레임에서 960x540를 추가해보겠습니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-281">To make sure we have all our video encoders created with the same settings, it's most convenient to duplicate the already existing AVC Video Encoder and configure another combination of resolution and bitrate (let's add one of 960 x 540 at 25 frames per second at 2,5 Mbps).</span></span> <span data-ttu-id="5257c-282">기존 인코더를 복제하려면 디자이너 화면에 복사하고 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-282">To duplicate the existing encoder, copy paste it on the designer surface.</span></span>

<span data-ttu-id="5257c-283">새 AVC 구성 요소에 미디어 파일 입력의 압축되지 않은 비디오 출력 핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-283">Connect the Uncompressed Video output pin of the Media File Input into our new AVC component.</span></span>

![연결된 두 번째 AVC 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

<span data-ttu-id="5257c-285">*연결된 두 번째 AVC 인코더*</span><span class="sxs-lookup"><span data-stu-id="5257c-285">*Second AVC encoder connected*</span></span>

<span data-ttu-id="5257c-286">이제 2,5Mbps로 960x540를 출력하는 새 AVC 인코더에 대한 구성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-286">Now adapt the configuration for our new AVC encoder to output 960x540 at 2,5 Mbps.</span></span> <span data-ttu-id="5257c-287">(여기에 해당 속성 "출력 너비", "출력 높이" 및 "비트 전송률(kbps)"을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-287">(Use its properties "Output width", "Output height", and "Bitrate (kbps)" for this.)</span></span>

<span data-ttu-id="5257c-288">Azure 미디어 서비스의 동적 패키징과 함께 결과 자산을 사용하려 한다면 스트리밍 끝점은 서로 정확하게 정렬된 MP4 파일 HLS/조각화된 MP4/DASH 조각에서 생성될 수 있어야 합니다. 생성되는 방법도 다른 비트 전송률 간에 전환하는 클라이언트가 부드러운 단일 연속 비디오 및 오디오 환경을 가져오는 방식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-288">Given we want to use the resulting asset together with Azure Media Services' dynamic packaging, the streaming endpoint needs to be capable of generating from these MP4 files HLS/Fragmented MP4/DASH fragments that are exactly aligned to each other in a way that clients that are switching between different bitrates get a single smooth continuous video and audio experience.</span></span> <span data-ttu-id="5257c-289">이렇게 하려면 두 AVC 인코더 GOP("사진의 그룹")의 속성에서 MP4 파일의 크기가 2초로 설정되어 있는지 확인해야 합니다. 이는 다음으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-289">To make that happen, we need to ensure that, in the properties of both AVC encoders the GOP ("group of pictures") size for both MP4 files is set to 2 seconds, which can be done by:</span></span>

* <span data-ttu-id="5257c-290">고정 GOP 크기 모드를 GOP 크기로 설정하고</span><span class="sxs-lookup"><span data-stu-id="5257c-290">setting the GOP Size Mode to Fixed GOP size and</span></span>
* <span data-ttu-id="5257c-291">키 프레임 간격을 2초로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-291">the Key Frame Interval to two seconds.</span></span>
* <span data-ttu-id="5257c-292">또한 GOP IDR 컨트롤을 닫힌 GOP로 설정하여 모든 GOP이 종속성 없이 자체에 대기하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-292">also set the GOP IDR Control to Closed GOP to ensure all GOP's are standing on their own without dependencies</span></span>

<span data-ttu-id="5257c-293">워크플로를 편리하게 이해하려면 첫 번째 AVC 인코더의 이름을 "AVC 비디오 인코더 640x360 1200kbps"로 바꾸고 두 번째 AVC 인코더의 이름을 "AVC 비디오 인코더 960x540 2500kbps"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-293">To make our workflow convenient to understand, rename the first AVC encoder to "AVC Video Encoder 640x360 1200kbps" and the second AVC encoder "AVC Video Encoder 960x540 2500 kbps".</span></span>

<span data-ttu-id="5257c-294">이제 두 번째 ISO MPEG-4 멀티플렉서 및 두 번째 파일 출력을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-294">Now add a second ISO MPEG-4 Multiplexer and a second File Output.</span></span> <span data-ttu-id="5257c-295">새 AVC 인코더에 멀티플렉서를 연결하고 해당 출력이 파일 출력에 전달되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-295">Connect the multiplexer to the new AVC encoder and make sure its output is directed into the File Output.</span></span> <span data-ttu-id="5257c-296">그런 다음 AAC 오디오 인코더 출력을 새 멀티플렉서의 입력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-296">Then also connect the AAC audio encoder output to the new multiplexer's input.</span></span> <span data-ttu-id="5257c-297">그러면 파일 출력은 출력 파일/자산 노드에 연결되어 생성되는 미디어 서비스 자산에 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-297">The File Output in turn can then be connected to the Output File/Asset node to add it to the Media Services Asset that will be created.</span></span>

![두 번째 Muxer 및 연결된 파일 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

<span data-ttu-id="5257c-299">*두 번째 Muxer 및 연결된 파일 출력*</span><span class="sxs-lookup"><span data-stu-id="5257c-299">*Second Muxer and File Output connected*</span></span>

<span data-ttu-id="5257c-300">Azure 미디어 서비스 동적 패키징과 호환성을 위해 멀티플렉서의 청크 모드를 GOP 개수나 기간으로 구성하고 청크 당 GOP를 1로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-300">For compatibility with Azure Media Services dynamic packaging, configure the multiplexer's Chunk Mode to GOP count or duration and set the GOPs per chunk to 1.</span></span> <span data-ttu-id="5257c-301">(기본값이어야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-301">(This should be the default.)</span></span>

![Muxer 청크 모드](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

<span data-ttu-id="5257c-303">*Muxer 청크 모드*</span><span class="sxs-lookup"><span data-stu-id="5257c-303">*Muxer Chunk Modes*</span></span>

<span data-ttu-id="5257c-304">참고: 사용자가 자산 출력에 추가하려는 다른 비트 전송률 및 해상도 조합에 대해 이 프로세스를 반복하고자 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-304">Note: you may want to repeat this process for any other bitrate and resolution combinations you want to have added to the asset output.</span></span>

### <span data-ttu-id="5257c-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>파일 출력 이름 구성</span><span class="sxs-lookup"><span data-stu-id="5257c-305"><a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configuring the file output names</span></span>
<span data-ttu-id="5257c-306">출력 자산에 추가된 둘 이상의 단일 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-306">We have more than one single file added to the output asset.</span></span> <span data-ttu-id="5257c-307">각 출력 파일에 대한 파일 이름이 서로 다르게 만들 필요를 제공하고 어쩌면 파일 명명 규칙을 제공하므로 파일 이름에서 다룰 내용이 명확해집니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-307">This provides a need to make sure the filenames for each of the output files are different from each other and maybe even apply a file-naming convention so it becomes clear from the file name what you're dealing with.</span></span>

<span data-ttu-id="5257c-308">파일 출력 이름 지정은 디자이너에서 식을 통해 제어될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-308">File output naming can be controlled through expressions in the designer.</span></span> <span data-ttu-id="5257c-309">파일 출력 구성 요소 중 하나에 대한 속성 창을 열고 파일 속성에 대한 식 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-309">Open the property pane for one of the File Output components and open the expression editor for the File property.</span></span> <span data-ttu-id="5257c-310">다음 식을 통해 첫 번째 출력 파일을 구성했습니다( [MXF에서 단일 비트 전송률 MP4 출력으로](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)이동하기 위한 자습서를 참조).</span><span class="sxs-lookup"><span data-stu-id="5257c-310">Our first output file was configured through the following expression (see the tutorial for going from [MXF to a single bitrate MP4 output](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

<span data-ttu-id="5257c-311">즉, 작성할 출력 디렉터리 및 원본 파일 기본 이름 등 두 개의 변수로 파일 이름을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-311">This means that our filename is determined by two variables: the output directory to write in and the source file base name.</span></span> <span data-ttu-id="5257c-312">전자는 워크플로 루트에서 속성으로 노출되고 후자는 들어오는 파일에 의해 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-312">The former is exposed as a property on the workflow root and the latter is determined by the incoming file.</span></span> <span data-ttu-id="5257c-313">출력 디렉터리는 로컬 테스트에 사용합니다. 워크플로가 Azure 미디어 서비스에서 클라우드 기반 미디어 프로세서에 의해 실행되는 경우 워크플로 엔진이 이 속성을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-313">Note that the output directory is what you use for local testing; this property will be overridden by the workflow engine when the workflow is executed by the cloud-based media processor in Azure Media Services.</span></span>
<span data-ttu-id="5257c-314">출력 파일 모두에 일관된 출력 명명을 부여하려면 첫 번째 파일 명명 식을 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-314">To give both our output files a consistent output naming, change the first file naming expression to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5257c-315">그리고 두 번째를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-315">and the second to:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5257c-316">중간 테스트 실행을 실행하여 MP4 출력 파일이 모두 제대로 생성되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-316">Execute an intermediate test run to make sure both MP4 output files are properly generated.</span></span>

### <span data-ttu-id="5257c-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>별도 오디오 트랙 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-317"><a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adding a separate Audio Track</span></span>
<span data-ttu-id="5257c-318">나중에 살펴보겠지만 .ism 파일을 생성하여 MP4 출력 파일을 사용하는 경우 적응 스트리밍에 대한 오디오 트랙으로 오디오 전용 MP4 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-318">As we'll see later when we generate an .ism file to go with our MP4 output files, we will also require a audio-only MP4 file as the audio track for our adaptive streaming.</span></span> <span data-ttu-id="5257c-319">이 파일을 만들려면 워크플로(ISO-MPEG-4 멀티플렉서)에 추가 muxer를 추가하고 트랙1에 해당 입력 핀으로 AAC 인코더의 출력 핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-319">To create this file, add an additional muxer to the workflow (ISO-MPEG-4 Multiplexer) and connect the AAC encoder's output pin with its input pin for Track 1.</span></span>

![추가된 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

<span data-ttu-id="5257c-321">*추가된 오디오 Muxer*</span><span class="sxs-lookup"><span data-stu-id="5257c-321">*Audio Muxer Added*</span></span>

<span data-ttu-id="5257c-322">세 번째 출력 파일 구성 요소를 만들어서 muxer에서 아웃바운드 스트림을 출력하고 파일 명명 식을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-322">Create a third File Output component to output the outbound stream from the muxer and configure the file naming expression as:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![파일 출력을 생성하는 오디오 Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

<span data-ttu-id="5257c-324">*파일 출력을 생성하는 오디오 Muxer*</span><span class="sxs-lookup"><span data-stu-id="5257c-324">*Audio Muxer creating File Output*</span></span>

### <span data-ttu-id="5257c-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>.ISM SMIL 파일 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-325"><a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adding the .ISM SMIL File</span></span>
<span data-ttu-id="5257c-326">또한 미디어 서비스 자산에서 MP4 파일 모두(및 오디오 전용 MP4)와 함께 작업하는 동적 패키징의 경우 매니페스트 파일이 필요합니다(또는 "SMIL"(동기화 멀티미디어 통합 언어) 파일이라고도 함).</span><span class="sxs-lookup"><span data-stu-id="5257c-326">For the dynamic packaging to work in combination with both MP4 files (and the audio-only MP4) in our Media Services asset, we also need a manifest file (also called a "SMIL" file: Synchronized Multimedia Integration Language).</span></span> <span data-ttu-id="5257c-327">이 파일은 동적 패키징에 사용 가능하고 오디오 스트리밍에 고려하는 MP4 파일을 Azure 미디어 서비스에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-327">This file indicates to Azure Media Services what MP4 files are available for dynamic packaging and which of those to consider for the audio streaming.</span></span> <span data-ttu-id="5257c-328">단일 오디오 스트림이 있는 MP4의 집합에 대한 일반적인 매니페스트 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-328">A typical manifest file for a set of MP4's with a single audio stream looks like this:</span></span>

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

<span data-ttu-id="5257c-329">.ism 파일은 전환 문 내에서 개별 MP4 비디오 파일 각각에 대한 참조 및 추가로 오디오를 포함하는 MP4에 하나(또는 이상)의 오디오 파일 참조를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-329">The .ism file contains within a switch statement, a reference to each of the individual MP4 video files and in addition to those also one (or more) audio file references to an MP4 that only contains the audio.</span></span>

<span data-ttu-id="5257c-330">MP4의 집합에 매니페스트 파일을 생성하는 작업은 "AMS 매니페스트 기록기"라는 구성 요소를 통해 수행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-330">Generating the manifest file for our set of MP4's can be done through a component called the "AMS Manifest Writer".</span></span> <span data-ttu-id="5257c-331">이를 사용하려면 화면으로 끌어서 세 개의 파일 출력 구성 요소에서 AMS 매니페스트 기록기 입력에 "쓰기 완료" 출력 핀을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-331">To use it, drag it onto the surface and connect the "Write Complete" output pins from the three File Output components to the AMS Manifest Writer input.</span></span> <span data-ttu-id="5257c-332">그런 다음 출력 파일/자산에 AMS 매니페스트 기록기의 출력을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-332">Then make sure to connect the output of the AMS Manifest Writer to the Output File/Asset.</span></span>

<span data-ttu-id="5257c-333">다른 파일 출력 구성 요소와 마찬가지로 .ism 파일 출력 이름을 식으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-333">As with our other file output components, configure the .ism file output name with an expression:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

<span data-ttu-id="5257c-334">완료된 워크플로는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-334">Our finished workflow looks like the below:</span></span>

![다중 비트 전송률 MP4 워크플로에 완료된 MXF](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

<span data-ttu-id="5257c-336">*다중 비트 전송률 MP4 워크플로에 완료된 MXF*</span><span class="sxs-lookup"><span data-stu-id="5257c-336">*Finished MXF to multibitrate MP4 workflow*</span></span>

## <span data-ttu-id="5257c-337"><a id="MXF_to__multibitrate_MP4"></a>다중 비트 전송률 MP4로 MXF 인코딩 - 향상된 청사진</span><span class="sxs-lookup"><span data-stu-id="5257c-337"><a id="MXF_to__multibitrate_MP4"></a>Encoding MXF into multibitrate MP4 - enhanced blueprint</span></span>
<span data-ttu-id="5257c-338">[이전 워크플로 연습](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) 에서 단일 MXF 입력 자산이 어떻게 Azure 미디어 서비스 동적 패키징과 함께 사용할 다중 비트 전송률 MP4 파일, 오디오 전용 MP4 파일, 매니페스트 파일을 가진 출력 자산으로 변환될 수 있는지를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-338">In the [previous workflow walkthrough](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) we've seen how a single MXF input asset can be converted into an output asset with multi-bitrate MP4 files, an audio-only MP4 file and a manifest file for use in conjunction with Azure Media Services dynamic packaging.</span></span>

<span data-ttu-id="5257c-339">이 연습에서는 일부의 측면이 강화되고 더 편리하게 만들어지는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-339">This walkthrough will show how some of the aspects can be enhanced and made more convenient.</span></span>

### <span data-ttu-id="5257c-340"><a id="MXF_to_multibitrate_MP4_overview"></a>강화할 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-340"><a id="MXF_to_multibitrate_MP4_overview"></a>Workflow overview to enhance</span></span>
![강화할 다중 비트 전송률 MP4 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

<span data-ttu-id="5257c-342">*강화할 다중 비트 전송률 MP4 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-342">*Multibitrate MP4 workflow to enhance*</span></span>

### <span data-ttu-id="5257c-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>파일 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="5257c-343"><a id="MXF_to__multibitrate_MP4_file_naming"></a>File Naming Conventions</span></span>
<span data-ttu-id="5257c-344">이전 워크플로에서 출력 파일 이름을 생성하기 위한 기반으로 단일 식을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-344">In the previous workflow we specified a simple expression as the basis for generating output file names.</span></span> <span data-ttu-id="5257c-345">그러나  이러한 식을 지정한 각 개별 출력 파일 구성 요소의 경우 모두 일부 중복이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-345">We have some duplication though: all of the the individual output file components specified such expression.</span></span>

<span data-ttu-id="5257c-346">예를 들어 첫 번째 비디오 파일에 대한 파일 출력 구성 요소는 다음 식으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-346">For example, our file output component for the first video file is configured with this expression:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

<span data-ttu-id="5257c-347">반면 두 번째 출력 비디오의 경우 다음과 같은 식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-347">While for the second output video, we have an expression like:</span></span>

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

<span data-ttu-id="5257c-348">대신 이러한 중복을 제거하고 더 구성 가능하게 된다면 간결하며 오류가 발생할 가능성이 적고 더 편리해질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-348">Wouldn't it be cleaner, less error prone and more convenient if we could remove some of this duplication and make things more configurable instead?</span></span> <span data-ttu-id="5257c-349">다행히 다음과 같은 작업이 가능합니다. 워크플로 루트에서 사용자 지정 속성을 만드는 기능과 함께 디자이너의 식 기능이 편리한 추가 계층을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-349">Luckily we can: the designer's expression capabilities in combination with the ability to create custom properties on our workflow root will give us an added layer of convenience.</span></span>

<span data-ttu-id="5257c-350">개별 MP4 파일의 비트 전송률에서 파일 이름 구성을 가져온다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-350">Let's assume we'll drive filename configuration from the bitrates of the individual MP4 files.</span></span> <span data-ttu-id="5257c-351">(그래프의 루트의) 하나의 중앙 위치에서 구성하려는 이러한 비트 전송률은 해당 위치에서 파일 이름 생성을 구성하고 가져오도록 액세스됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-351">These bitrates we'll aim to configure in one central place (on the root of our graph), from where they'll be accessed to configure and drive file name generation.</span></span> <span data-ttu-id="5257c-352">이렇게 하려면 AVC 인코더 모두에서 워크플로 루트로 비트 전송률 속성을 게시하기 시작하므로 AVC 인코더와 마찬가지로 모두 루트에서도 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-352">To do this, we start by publishing the bitrate property from both AVC encoders to the root of our workflow, so that it becomes accessible from both the root as well as from the AVC encoders.</span></span> <span data-ttu-id="5257c-353">(두 개의 서로 다른 위치에 표시되는 경우에도 기본 값은 하나입니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-353">(Even if displayed in two different spots, there's only one underlying value.)</span></span>

### <span data-ttu-id="5257c-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>워크플로 루트에 구성 요소 속성 게시</span><span class="sxs-lookup"><span data-stu-id="5257c-354"><a id="MXF_to__multibitrate_MP4_publishing"></a>Publishing component properties onto the workflow root</span></span>
<span data-ttu-id="5257c-355">첫 번째 AVC 인코더를 열고 비트 전송률(kbps) 속성으로 이동하여 드롭다운에서 게시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-355">Open the first AVC encoder, go to the Bitrate (kbps) property and from the dropdown choose Publish.</span></span>

![비트 전송률 속성 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

<span data-ttu-id="5257c-357">*비트 전송률 속성 게시*</span><span class="sxs-lookup"><span data-stu-id="5257c-357">*Publishing the bitrate property*</span></span>

<span data-ttu-id="5257c-358">게시 대화 상자를 구성하여 "video1bitrate"라는 게시된 이름 및 "비디오 1 비트 전송률"이라는 읽을 수 있는 표시 이름을 사용하여 워크플로 그래프의 루트에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-358">Configure the publish dialog to publish to the root of our workflow graph, with a published name of "video1bitrate" and a readable display name of "Video 1 Bitrate".</span></span> <span data-ttu-id="5257c-359">"비트 전송률 스트리밍"이라는 사용자 지정 그룹 이름을 구성하고 게시를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-359">Configure a custom group name called "Streaming Bitrates" and hit Publish.</span></span>

![비트 전송률 속성 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

<span data-ttu-id="5257c-361">*비트 전송률 속성에 게시 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5257c-361">*Publishing dialog for bitrate property*</span></span>

<span data-ttu-id="5257c-362">두 번째 AVC 인코더의 비트 전송률 속성에서 동일하게 반복하고 동일한 "비트 전송률 스트리밍" 사용자 지정 그룹에서 "비디오 2 비트 전송률"이라는 표시 이름을 사용하여 "video2bitrate"이라고 명명합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-362">Repeat the same for the bitrate property of the second AVC encoder and name it "video2bitrate" with a display name of "Video 2 Bitrate", in the same custom group "Streaming Bitrates".</span></span>

<span data-ttu-id="5257c-363">이제 워크플로 루트 속성을 검사하면 두 개의 게시된 속성이 있는 사용자 지정 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-363">If we now inspect the workflow root properties, we'll see our custom group with the two published properties show up.</span></span> <span data-ttu-id="5257c-364">둘 모두 해당 AVC 인코더 비트 전송률의 값을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-364">Both are reflecting the value of their respective AVC encoder bitrate.</span></span>

![워크플로 루트에 게시된 비트 전송률 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

<span data-ttu-id="5257c-366">코드 또는 식에서 이러한 속성에 액세스하려는 때마다 다음과 같이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-366">Whenever we want to access these properties from code or from an expression, we can do so like this:</span></span>

* <span data-ttu-id="5257c-367">루트 바로 아래 구성 요소의 인라인 코드에서: node.getPropertyAsString('../video1bitrate',null)</span><span class="sxs-lookup"><span data-stu-id="5257c-367">from inline code from a component right below the root: node.getPropertyAsString('../video1bitrate',null)</span></span>
* <span data-ttu-id="5257c-368">식 내에서: ${ROOT_video1bitrate}</span><span class="sxs-lookup"><span data-stu-id="5257c-368">within an expression: ${ROOT_video1bitrate}</span></span>

<span data-ttu-id="5257c-369">여기에서도 오디오 트랙 비트 전송률을 게시하여 "비트 전송률 스트리밍" 그룹을 완료하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-369">Let's complete the "Streaming Bitrates" group by publishing our audio track bitrate on it as well.</span></span> <span data-ttu-id="5257c-370">AAC 인코더의 속성 내에서 비트 전송률 설정을 검색하고 옆에 있는 드롭다운에서 게시를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-370">Within the properties of the AAC Encoder, search for the Bitrate setting and select Publish from the dropdown next to it.</span></span> <span data-ttu-id="5257c-371">"비트 전송률 스트리밍" 사용자 지정 그룹 내에서 "audio1bitrate"이라는 이름과 "오디오 1 비트 전송률"이라는 표시 이름을 사용하여 그래프의 루트에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-371">Publish to the root of the graph with name "audio1bitrate" and display name "Audio 1 Bitrate" within our custom group "Streaming Bitrates".</span></span>

![오디오 비트 전송률에 게시 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

<span data-ttu-id="5257c-373">*오디오 비트 전송률에 게시 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5257c-373">*Publishing dialog for audio bitrate*</span></span>

![루트의 결과 비디오 및 오디오 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

<span data-ttu-id="5257c-375">*루트의 결과 비디오 및 오디오 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-375">*Resulting video and audio props on root*</span></span>

<span data-ttu-id="5257c-376">또한 세 가지 해당 값의 변경이 연결된 (그리고 게시된) 해당 구성 요소의 값을 다시 구성하고 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-376">Note that changing any of those three values also re-configures and changes the values on the respective components they are linked with (and where published from).</span></span>

### <span data-ttu-id="5257c-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>게시된 속성 값을 사용하는 출력 파일 이름 생성</span><span class="sxs-lookup"><span data-stu-id="5257c-377"><a id="MXF_to__multibitrate_MP4_output_files"></a>Have generated output file names rely on published property values</span></span>
<span data-ttu-id="5257c-378">생성된 파일 이름을 하드 코딩하는 대신 각 그래프 루트에 방금 게시한 비트 전송률 속성을 사용하는 각 출력 파일 구성 요소의 파일 이름 식을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-378">Instead of hardcoding our generated file names, we can now change our filename expression on each of the File Output components to rely on the bitrate properties we just published on the graph root.</span></span> <span data-ttu-id="5257c-379">첫 번째 파일 출력을 시작하고 파일 속성을 찾아서 다음과 같이 식을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-379">Starting with our first file output, find the File property and edit the expression like this:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

<span data-ttu-id="5257c-380">식 창에서 키보드에 달러 기호를 눌러서 이 식의 다른 매개 변수를 액세스하고 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-380">The different parameters in this expression can be accessed and entered by hitting the dollar sign on the keyboard while in the expression window.</span></span> <span data-ttu-id="5257c-381">사용 가능한 매개 변수 중 하나는 이전에 게시한 video1bitrate 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-381">One of the available parameters is our video1bitrate property which we published earlier.</span></span>

![식 내에서 매개 변수 액세스](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

<span data-ttu-id="5257c-383">*식 내에서 매개 변수 액세스*</span><span class="sxs-lookup"><span data-stu-id="5257c-383">*Accessing parameters within an expression*</span></span>

<span data-ttu-id="5257c-384">두 번째 비디오에 대한 파일 출력에 동일한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-384">Do the same for the file output for our second video:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

<span data-ttu-id="5257c-385">그리고 오디오 전용 파일 출력에도 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-385">and for the audio-only file output:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

<span data-ttu-id="5257c-386">이제 비디오 또는 오디오 파일에 대한 비트 전송률을 변경하면 해당하는 인코더를 다시 구성하고 비트 전송률 기반 파일 이름 규칙을 모두 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-386">If we now change the bitrate for any of the video or audio files, the respective encoder will be reconfigured and the bitrate-based file name convention will be honored all automatic.</span></span>

## <span data-ttu-id="5257c-387"><a id="thumbnails_to__multibitrate_MP4"></a>다중 비트 전송률 MP4 출력에 미리 보기 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-387"><a id="thumbnails_to__multibitrate_MP4"></a>Adding thumbnails to multibitrate MP4 output</span></span>
<span data-ttu-id="5257c-388">[MXF 입력에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)을 생성하는 워크플로를 시작하고 이제 출력에 미리 보기의 추가를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-388">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into adding thumbnails to the output.</span></span>

### <span data-ttu-id="5257c-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>미리 보기를 추가하는 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-389"><a id="thumbnails_to__multibitrate_MP4_overview"></a>Workflow overview to add thumbnails to</span></span>
![시작할 다중 비트 전송률 MP4 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

<span data-ttu-id="5257c-391">*시작할 다중 비트 전송률 MP4 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-391">*Multibitrate MP4 workflow to start from*</span></span>

### <span data-ttu-id="5257c-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>JPG 인코딩 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-392"><a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adding JPG Encoding</span></span>
<span data-ttu-id="5257c-393">미리 보기 생성의 핵심은 JPG 파일을 출력할 수 있는 JPG 인코더 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-393">The heart of our thumbnail generation will be the JPG Encoder component, able to output JPG files.</span></span>

![JPG 인코더](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

<span data-ttu-id="5257c-395">*JPG 인코더*</span><span class="sxs-lookup"><span data-stu-id="5257c-395">*JPG Encoder*</span></span>

<span data-ttu-id="5257c-396">그러나 직접 미디어 파일 입력에서 JPG 인코더에 압축되지 않은 비디오 스트림을 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-396">We cannot however directly connect our Uncompressed Video stream from the Media File Input into the JPG encoder.</span></span> <span data-ttu-id="5257c-397">대신 전달된 개별 프레임을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-397">Instead, it expects to be handed individual frames.</span></span> <span data-ttu-id="5257c-398">이는 비디오 프레임 게이트 구성 요소를 통해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-398">This, we can do through the Video Frame Gate component.</span></span>

![JPG 인코더에 프레임 게이트 연결](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

<span data-ttu-id="5257c-400">*JPG 인코더에 프레임 게이트 연결*</span><span class="sxs-lookup"><span data-stu-id="5257c-400">*Connecting a frame gate to the JPG encoder*</span></span>

<span data-ttu-id="5257c-401">프레임 게이트는 여러 초 또는 여러 프레임에 한 번 비디오 프레임을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-401">The frame gate once every so many seconds or frames allows a video frame to pass.</span></span> <span data-ttu-id="5257c-402">발생하는 간격 및 시간 오프셋은 속성에서 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-402">The interval and the time offset with which this happens is configurable in the properties.</span></span>

![비디오 프레임 게이트 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

<span data-ttu-id="5257c-404">*비디오 프레임 게이트 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-404">*Video Frame Gate properties*</span></span>

<span data-ttu-id="5257c-405">모드를 시간(초)으로 설정하고 간격을 60으로 설정하여 매 분 마다 미리 보기를 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-405">Let's create a thumbnail every minute by setting the mode to Time (seconds) and the Interval to 60.</span></span>

### <span data-ttu-id="5257c-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>색 공간 변환 처리</span><span class="sxs-lookup"><span data-stu-id="5257c-406"><a id="thumbnails_to__multibitrate_MP4_color_space"></a>Dealing with Color Space conversion</span></span>
<span data-ttu-id="5257c-407">프레임 게이트 및 미디어 파일 입력의 압축되지 않은 비디오 핀은 모두 연결될 수 있다는 것이 논리적 보이는 반면 그렇게 할 경우 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-407">While it would seem logical both Uncompressed Video pins of the frame gate and the Media File Input can now be connected, we would get a warning if we would do so.</span></span>

![입력 색 공간 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

<span data-ttu-id="5257c-409">*입력 색 공간 오류*</span><span class="sxs-lookup"><span data-stu-id="5257c-409">*Input color space error*</span></span>

<span data-ttu-id="5257c-410">색 정보가 원래 있는 그대로 압축되지 않은 비디오 스트림에서 보여지는 방식 때문에 MXF에서 가져오면 JPG 인코더가 예상하는 것과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-410">This is because the way in which colour information is represented in our original raw uncompressed video stream, coming from our MXF, is different from what the JPG Encoder is expecting.</span></span> <span data-ttu-id="5257c-411">구체적으로 말하면 소위 "RGB" 또는 "회색"의 "색 공간"이 흘러들어 올 것이 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-411">More specifically, a so-called "color space" of "RGB" or "Grayscale" is expected to flow in.</span></span> <span data-ttu-id="5257c-412">즉, 비디오 프레임 게이트의 인바운드 비디오 스트림이 해당 색 공간을 고려하여 적용할 변환이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-412">This means that the Video Frame Gate's inbound video stream will need to have a conversion applied regarding its color space first.</span></span>

<span data-ttu-id="5257c-413">워크플로인 색상 공간 변환기 - Intel에 끌어서 놓고 프레임 게이트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-413">Drag onto the workflow the Color Space Converter - Intel and connect it to our frame gate.</span></span>

![색 공간 변환 연결](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

<span data-ttu-id="5257c-415">*색 공간 변환 연결*</span><span class="sxs-lookup"><span data-stu-id="5257c-415">*Connecting a Color Space Convertor*</span></span>

<span data-ttu-id="5257c-416">속성 창의 사전 설정 목록에서 BGR 24 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-416">In the properties window, pick the BGR 24 entry from the Preset list.</span></span>

### <span data-ttu-id="5257c-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>미리 보기 작성</span><span class="sxs-lookup"><span data-stu-id="5257c-417"><a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Writing the thumbnails</span></span>
<span data-ttu-id="5257c-418">MP4 비디오와 다르게 JPG 인코더 구성 요소는 여러 개의 파일을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-418">Different from our MP4 video's, the JPG Encoder component will output more than one file.</span></span> <span data-ttu-id="5257c-419">이를 처리하기 위해 장면 검색 JPG 파일 기록기 구성 요소를 사용할 수 있습니다. 들어오는 JPG 미리 보기를 사용하고 이를 작성하며 각 파일 이름이 다른 숫자 뒤에 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-419">In order to deal with this, a Scene Search JPG File Writer component can be used: it will take the incoming JPG thumbnails and write them out, each filename being suffixed by a different number.</span></span> <span data-ttu-id="5257c-420">(일반적으로 미리 보기를 그린 스트림에서 초/단위의 수를 나타내는 숫자입니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-420">(The number typically indicating the number of seconds/units in the stream which the thumbnail was drawn from.)</span></span>

![장면 검색 JPG 파일 기록기 소개](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

<span data-ttu-id="5257c-422">*장면 검색 JPG 파일 기록기 소개*</span><span class="sxs-lookup"><span data-stu-id="5257c-422">*Introducing the Scene Search JPG File Writer*</span></span>

<span data-ttu-id="5257c-423">다음 식을 사용하여 출력 폴더 경로 속성을 구성합니다. ${ROOT_outputWriteDirectory}</span><span class="sxs-lookup"><span data-stu-id="5257c-423">Configure the Output Folder Path property with the expression: ${ROOT_outputWriteDirectory}</span></span>

<span data-ttu-id="5257c-424">그리고 다음으로 파일 이름 접두사 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-424">and the Filename Prefix property with:</span></span>

    ${ROOT_sourceFileBaseName}_thumb_

<span data-ttu-id="5257c-425">접두사는 미리 보기 파일이 명명되는 방법을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-425">The prefix will determine how the thumbnail files are being named.</span></span> <span data-ttu-id="5257c-426">스트림에서 미리 보기의 위치를 나타내는 숫자가 뒤에 붙습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-426">They will be suffixed with a number indicating the thumb's position in the stream.</span></span>

![장면 검색 JPG 파일 기록기 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

<span data-ttu-id="5257c-428">*장면 검색 JPG 파일 기록기 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-428">*Scene Search JPG File Writer properties*</span></span>

<span data-ttu-id="5257c-429">출력 파일/자산 노드에 장면 검색 JPG 파일 기록기를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-429">Connect the Scene Search JPG File Writer to the Output File/Asset node.</span></span>

### <span data-ttu-id="5257c-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>워크플로에서 오류 감지</span><span class="sxs-lookup"><span data-stu-id="5257c-430"><a id="thumbnails_to__multibitrate_MP4_errors"></a>Detecting errors in a workflow</span></span>
<span data-ttu-id="5257c-431">색상 공간 변환기의 입력을 그대로 압축되지 않은 비디오 출력에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-431">Connect the input of the color space converter to the raw uncompressed video output.</span></span> <span data-ttu-id="5257c-432">이제 워크플로에 대한 로컬 테스트 실행을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-432">Now perform a local test run for the workflow.</span></span> <span data-ttu-id="5257c-433">워크플로가 갑자기 실행을 중지하고 오류가 발생한 구성 요소에 빨간 윤곽선이 나타날 가능성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-433">There's a good chance the workflow will suddenly stop executing and indicate with a red outline on the component that encountered an error:</span></span>

![색 공간 변환기 오류](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

<span data-ttu-id="5257c-435">*색 공간 변환기 오류*</span><span class="sxs-lookup"><span data-stu-id="5257c-435">*Color Space Converter error*</span></span>

<span data-ttu-id="5257c-436">색 공간 변환기 구성 요소의 오른쪽 상단에 있는 작은 빨간색 "E" 아이콘을 클릭하여 인코딩 시도가 실패한 이유를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-436">Click the little red "E" icon in the top right corner of the Color Space Converter component to see what's the reason the encoding attempt failed.</span></span>

![색 공간 변환기 오류 대화 상자](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

<span data-ttu-id="5257c-438">*색 공간 변환기 오류 대화 상자*</span><span class="sxs-lookup"><span data-stu-id="5257c-438">*Color Space Converter error dialog*</span></span>

<span data-ttu-id="5257c-439">결국 확인할 수 있듯이 색 공간 변환기에 들어오는 색 공간 표준이 요청한 YUV에서 RGB로의 변환에 대해 rec601로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-439">It turns out, as you can see, that the incoming color space standard for the color space converter has to be rec601 for our requested conversion of YUV to RGB.</span></span> <span data-ttu-id="5257c-440">스트림은 rec601을 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-440">Apparently our stream doesn't indicate it's rec601.</span></span> <span data-ttu-id="5257c-441">(Rec 601은 디지털 비디오 형태로 인터레이스된 아날로그 비디오 신호를 인코딩하기 위한 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-441">(Rec 601 is a standard for encoding interlaced analog video signals in digital video form.</span></span> <span data-ttu-id="5257c-442">720 광도 샘플 및 줄 당 360 색차 샘플을 포함하는 활성 영역을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-442">It specifies an active region covering 720 luminance samples and 360 chrominance samples per line.</span></span> <span data-ttu-id="5257c-443">색 인코딩 시스템은 YCbCr 4:2:2라고 알려져 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-443">The color encoding system is known as YCbCr 4:2:2.)</span></span>

<span data-ttu-id="5257c-444">이를 해결하기 위해 rec601 콘텐츠를 다루는 스트림의 메타데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-444">To fix this, we'll indicate on the metadata of our stream that we're dealing with rec601 content.</span></span> <span data-ttu-id="5257c-445">이렇게 하려면 비디오 데이터 형식 업데이트를 구성 요소를 사용하며 이를 원시 원본 및 색 공간 변환 구성 요소 사이에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-445">To do so we'll use a Video Data Type Updater component, which we'll put in between our raw source and the color space conversion component.</span></span> <span data-ttu-id="5257c-446">이 데이터 형식 업데이트 프로그램을 사용하면 특정 비디오 데이터 형식 속성을 수동으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-446">This data type updater allows for the manual update of certain video data type properties.</span></span> <span data-ttu-id="5257c-447">이를 구성하여 색 공간 표준인 "Rec 601"을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-447">Configure it to indicate a Color Space Standard of "Rec 601".</span></span> <span data-ttu-id="5257c-448">이렇게 하면 색 공백이 없는 경우 비디오 데이터 형식 업데이트 프로그램이 "Rec 601" 색 공간을 사용하여 스트림의 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-448">This will cause the Video Data Type Updater to tag the stream with the "Rec 601" color space if there was no color space defined yet.</span></span> <span data-ttu-id="5257c-449">(재정의 확인란을 선택하지 않으면 기존 메타데이터를 재정의하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="5257c-449">(It will not override any existing metadata, unless the Override checkbox was checked.)</span></span>

![데이터 형식 업데이트 프로그램에서 색 공간 표준 업데이트](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

<span data-ttu-id="5257c-451">*데이터 형식 업데이트 프로그램에서 색 공간 표준 업데이트*</span><span class="sxs-lookup"><span data-stu-id="5257c-451">*Updating Color Space Standard on the Data Type Updater*</span></span>

### <span data-ttu-id="5257c-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="5257c-452"><a id="thumbnails_to__multibitrate_MP4_finish"></a>Finished Workflow</span></span>
<span data-ttu-id="5257c-453">이제 워크플로가 완료되면 다른 테스트를 실행하여 통과하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-453">Now that our our workflow is finished, do another test run to see it pass.</span></span>

![미리 보기로 다중 mp4 출력에 대해 완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

<span data-ttu-id="5257c-455">*미리 보기로 다중 mp4 출력에 대해 완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-455">*Finished workflow for multi-mp4 output with thumbnails*</span></span>

## <span data-ttu-id="5257c-456"><a id="time_based_trim"></a>다중 비트 전송률 MP4 출력의 시간 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="5257c-456"><a id="time_based_trim"></a>Time-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5257c-457">[MXF 입력에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)을 생성하는 워크플로를 시작하고 이제 타임 스탬프를 기반으로 하는 원본 비디오의 트리밍을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-457">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on time-stamps.</span></span>

### <span data-ttu-id="5257c-458"><a id="time_based_trim_start"></a>트리밍을 추가하기 시작하려는 워크플로 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-458"><a id="time_based_trim_start"></a>Workflow overview to start adding trimming to</span></span>
![트리밍에 추가할 워크플로 시작](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

<span data-ttu-id="5257c-460">*트리밍에 추가할 워크플로 시작*</span><span class="sxs-lookup"><span data-stu-id="5257c-460">*Starting workflow to add trimming to*</span></span>

### <span data-ttu-id="5257c-461"><a id="time_based_trim_use_stream_trimmer"></a>스트림 트리머 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-461"><a id="time_based_trim_use_stream_trimmer"></a>Using the Stream Trimmer</span></span>
<span data-ttu-id="5257c-462">스트림 트리머 구성 요소를 사용하면 시간 정보(초, 분,...)에 기반하는 입력 스트림의 시작 및 종료를 자를 수 있습니다. 트리머는 프레임 기반 자르기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-462">The Stream Trimmer component allows to trim the beginning and ending of an input stream base on timing information (seconds, minutes, ...). The trimmer does not support frame-based trimming.</span></span>

![스트림 트리머](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

<span data-ttu-id="5257c-464">*스트림 트리머*</span><span class="sxs-lookup"><span data-stu-id="5257c-464">*Stream Trimmer*</span></span>

<span data-ttu-id="5257c-465">AVC 인코더 및 스피커 위치 할당자를 미디어 파일 입력에 직접 연결하는 대신 해당 스트림 트리머 간에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-465">Instead of linking the AVC encoders and speaker position assigner to the Media File Input directly, we'll put in between those the stream trimmer.</span></span> <span data-ttu-id="5257c-466">(비디오 신호 및 인터리브 오디오 신호에 각각 하나.)</span><span class="sxs-lookup"><span data-stu-id="5257c-466">(One for the video signal and one for the interleaved audio signal.)</span></span>

![사이 간 스트림 트리머 배치](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

<span data-ttu-id="5257c-468">*사이 간 스트림 트리머 배치*</span><span class="sxs-lookup"><span data-stu-id="5257c-468">*Put Stream Trimmer in between*</span></span>

<span data-ttu-id="5257c-469">비디오에서 15초에서 60초 사이에 있는 비디오 및 오디오만 처리하도록 트리머를 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-469">Let's configure the trimmer so that we will only process video and audio between 15 seconds and 60 seconds in the video.</span></span>

<span data-ttu-id="5257c-470">비디오 스트림 트리머의 속성으로 이동하고 시작 시간(15초) 및 종료 시간(60초) 속성을 모두 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-470">Go to the properties of the Video Stream Trimmer and configure both Start Time (15s) and End Time (60s) properties.</span></span> <span data-ttu-id="5257c-471">오디오 및 비디오 트리머를 모두 항상 동일한 시작 및 종료 값으로 구성하려면 해당 사항을 워크플로의 루트에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-471">To make sure both our audio and video trimmer are always configured to the same start and end values, we will publish those to the root of the workflow.</span></span>

![스트림 트리머에서 시작 시간 속성 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

<span data-ttu-id="5257c-473">*스트림 트리머에서 시작 시간 속성 게시*</span><span class="sxs-lookup"><span data-stu-id="5257c-473">*Publish start time property from Stream Trimmer*</span></span>

![시작 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

<span data-ttu-id="5257c-475">*시작 시간에 속성 대화 상자 게시*</span><span class="sxs-lookup"><span data-stu-id="5257c-475">*Publish property dialog for start time*</span></span>

![종료 시간에 속성 대화 상자 게시](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

<span data-ttu-id="5257c-477">*종료 시간에 속성 대화 상자 게시*</span><span class="sxs-lookup"><span data-stu-id="5257c-477">*Publish property dialog for end time*</span></span>

<span data-ttu-id="5257c-478">이제 워크플로의 루트를 검사하면 속성이 모두 여기에 깔끔하게 표시되고 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-478">If we now inspect the root of our workflow, both properties will be neatly displayed and configurable from there.</span></span>

![루트에 사용 가능한 게시된 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

<span data-ttu-id="5257c-480">*루트에 사용 가능한 게시된 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-480">*Published properties available on root*</span></span>

<span data-ttu-id="5257c-481">이제 오디오 트리머에서 트리밍 속성을 열고 워크플로의 루트에 게시된 속성을 참조하는 식으로 시작 및 종료 시간을 모두 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-481">Now open the trimming properties from the audio trimmer and configure both start and end times with an expression that refers to the published properties on the root of our workflow.</span></span>

<span data-ttu-id="5257c-482">오디오 트리밍 시작 시간을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-482">For the audio trimming start time:</span></span>

    ${ROOT_TrimmingStartTime}

<span data-ttu-id="5257c-483">그리고 종료 시간을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-483">and for its end time:</span></span>

    ${ROOT_TrimmingEndTime}

### <span data-ttu-id="5257c-484"><a id="time_based_trim_finish"></a>완료된 워크플로</span><span class="sxs-lookup"><span data-stu-id="5257c-484"><a id="time_based_trim_finish"></a>Finished Workflow</span></span>
![완료된 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

<span data-ttu-id="5257c-486">*완료된 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-486">*Finished Workflow*</span></span>

## <span data-ttu-id="5257c-487"><a id="scripting"></a>스크립팅한 구성 요소 소개</span><span class="sxs-lookup"><span data-stu-id="5257c-487"><a id="scripting"></a>Introducing the Scripted Component</span></span>
<span data-ttu-id="5257c-488">스크립팅한 구성 요소는 워크플로의 실행 단계 중 임의의 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-488">Scripted Components can execute arbitrary scripts during the execution phases of our workflow.</span></span> <span data-ttu-id="5257c-489">실행될 수 있는 다른 4개의 스크립트가 있으며 각각 워크플로 수명 주기에서 특정한 특성 및 고유한 위치를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-489">There are four different scripts that can be executed, each with specific characteristics and their own place in the workflow life-cycle:</span></span>

* <span data-ttu-id="5257c-490">**commandScript**</span><span class="sxs-lookup"><span data-stu-id="5257c-490">**commandScript**</span></span>
* <span data-ttu-id="5257c-491">**realizeScript**</span><span class="sxs-lookup"><span data-stu-id="5257c-491">**realizeScript**</span></span>
* <span data-ttu-id="5257c-492">**processInputScript**</span><span class="sxs-lookup"><span data-stu-id="5257c-492">**processInputScript**</span></span>
* <span data-ttu-id="5257c-493">**lifeCycleScript**</span><span class="sxs-lookup"><span data-stu-id="5257c-493">**lifeCycleScript**</span></span>

<span data-ttu-id="5257c-494">스크립팅된 구성 요소의 설명서는 위에서 각각에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-494">The documentation of the Scripted Component goes in more detail for each of the above.</span></span> <span data-ttu-id="5257c-495">[다음 섹션](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)에서 **realizeScript** 스크립트 구성 요소는 워크플로가 시작할 때 즉석에서 cliplist xml을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-495">In [the following section](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), the **realizeScript** scripting component is used to construct a cliplist xml on the fly when the workflow starts.</span></span> <span data-ttu-id="5257c-496">이 스크립트는 구성 요소를 설치하는 동안 호출되며 수명 주기에서 한 번만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-496">This script is called during the component setup, which happens only once in it's lifecycle.</span></span>

### <span data-ttu-id="5257c-497"><a id="scripting_hello_world"></a>워크플로 내의 스크립팅: Hello World</span><span class="sxs-lookup"><span data-stu-id="5257c-497"><a id="scripting_hello_world"></a>Scripting within a workflow: hello world</span></span>
<span data-ttu-id="5257c-498">스크립트 구성 요소를 디자이너 화면으로 끌어오고 이름을 바꿉니다(예: "SetClipListXML").</span><span class="sxs-lookup"><span data-stu-id="5257c-498">Drag a Scripted Component onto the designer surface and rename it (for example, "SetClipListXML").</span></span>

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5257c-500">*스크립팅된 구성 요소 추가*</span><span class="sxs-lookup"><span data-stu-id="5257c-500">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5257c-501">스크립팅된 구성 요소의 속성을 검사할 때 네 개의 스크립트 형식이 표시되고 각각 다른 스크립트로 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-501">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5257c-503">*스크립팅된 구성 요소 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-503">*Scripted Component properties*</span></span>

<span data-ttu-id="5257c-504">processInputScript의 선택을 취소하고 realizeScript에 대한 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-504">Clear the processInputScript and open the editor for the realizeScript.</span></span> <span data-ttu-id="5257c-505">이제 스크립트를 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-505">Now we're set up and ready to start scripting.</span></span>

<span data-ttu-id="5257c-506">스크립트는 Java와의 호환성을 유지하는 Java 플랫폼에 동적으로 컴파일된 스크립트 언어인 Groovy로 작성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-506">Scripts are written in Groovy, a dynamically compiled scripting language for the Java platform that retains compatibility with Java.</span></span> <span data-ttu-id="5257c-507">사실 대부분의 Java 코드는 유효한 Groovy 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-507">Actually, most Java code is valid Groovy code.</span></span>

<span data-ttu-id="5257c-508">realizeScript의 컨텍스트에서 간단한 Hello World Groovy 스크립트를 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-508">Let's write a simple hello world groovy script in the context of our realizeScript.</span></span> <span data-ttu-id="5257c-509">편집기에 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-509">Enter the following in the editor:</span></span>

    node.log("hello world");

<span data-ttu-id="5257c-510">이제 로컬 테스트 실행을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-510">Now execute a local test run.</span></span> <span data-ttu-id="5257c-511">실행한 후에 로그 속성을 검사합니다(스크립팅된 구성 요소의 시스템 탭을 통해).</span><span class="sxs-lookup"><span data-stu-id="5257c-511">After this run, inspect (through the System tab on the Scripted Component) the Logs property.</span></span>

![Hello World 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

<span data-ttu-id="5257c-513">*Hello World 로그 출력*</span><span class="sxs-lookup"><span data-stu-id="5257c-513">*Hello world log output*</span></span>

<span data-ttu-id="5257c-514">로그 메서드를 호출하는 노드 개체는 현재 "노드" 또는 스크립트하는 구성 요소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-514">The node object we call the log method on, refers to our current "node" or the component we're scripting within.</span></span> <span data-ttu-id="5257c-515">이와 같은 모든 구성 요소는 출력 로깅 데이터에 대한 기능을 가지며 시스템 탭을 통해 사용할 수 있습니다. 이 경우에 문자열 리터럴 "Hello World"를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-515">Every component as such has the ability to output logging data, available through the system tab. In this case, we output the string literal "hello world".</span></span> <span data-ttu-id="5257c-516">중요한 것은 스크립트가 실제로 수행하는 작업에 대한 통찰력을 제공하는 중요한 디버깅 도구라는 것을 증명할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-516">Important to understand here is that this can prove to be an invaluable debugging tool, providing you with insight on what the script is actually doing.</span></span>

<span data-ttu-id="5257c-517">또한 스크립트 환경 내에서 다른 구성 요소의 속성에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-517">From within our scripting environment, we also have access to properties on other components.</span></span> <span data-ttu-id="5257c-518">다음을 실행해보세요.</span><span class="sxs-lookup"><span data-stu-id="5257c-518">Try this:</span></span>

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up to other nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

<span data-ttu-id="5257c-519">로그 창은 다음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-519">Our log window will show us the following:</span></span>

![노드 경로에 액세스하기 위한 로그 출력](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

<span data-ttu-id="5257c-521">*노드 경로에 액세스하기 위한 로그 출력*</span><span class="sxs-lookup"><span data-stu-id="5257c-521">*Log output for accessing node paths*</span></span>

## <span data-ttu-id="5257c-522"><a id="frame_based_trim"></a>다중 비트 전송률 MP4 출력의 프레임 기반 트리밍</span><span class="sxs-lookup"><span data-stu-id="5257c-522"><a id="frame_based_trim"></a>Frame-based trimming of multibitrate MP4 output</span></span>
<span data-ttu-id="5257c-523">[MXF 입력에서 다중 비트 전송률 MP4 출력](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)을 생성하는 워크플로를 시작하고 이제 프레임 개수를 기반으로 하는 원본 비디오의 트리밍을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-523">Starting from a workflow that generates [a multibitrate MP4 output from an MXF input](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), we will now be looking into trimming the source video based on frame counts.</span></span>

### <span data-ttu-id="5257c-524"><a id="frame_based_trim_start"></a>트리밍을 추가하기 시작하려는 청사진 개요</span><span class="sxs-lookup"><span data-stu-id="5257c-524"><a id="frame_based_trim_start"></a>Blueprint overview to start adding trimming to</span></span>
![트리밍을 추가하기 시작하려는 워크플로](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

<span data-ttu-id="5257c-526">*트리밍을 추가하기 시작하려는 워크플로*</span><span class="sxs-lookup"><span data-stu-id="5257c-526">*Workflow to start adding trimming to*</span></span>

### <span data-ttu-id="5257c-527"><a id="frame_based_trim_clip_list"></a>클립 목록 XML 사용</span><span class="sxs-lookup"><span data-stu-id="5257c-527"><a id="frame_based_trim_clip_list"></a>Using the Clip List XML</span></span>
<span data-ttu-id="5257c-528">이전의 모든 워크플로 자습서에서 미디어 파일 입력 구성 요소를 비디오 입력 원본으로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-528">In all previous workflow tutorials, we used the Media File Input component as our video input source.</span></span> <span data-ttu-id="5257c-529">하지만 이 특정 시나리오에서 클립 목록 원본 구성 요소를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-529">For this specific scenario though, we'll be using the Clip List Source component instead.</span></span> <span data-ttu-id="5257c-530">선호하는 작업 방법이 아니어야 합니다. 그렇게 해야 하는 실제 이유가 있을 때에만 클립 목록 원본을 사용합니다(아래와 같이 클립 목록 지우기 기능을 사용할 경우).</span><span class="sxs-lookup"><span data-stu-id="5257c-530">Note that this should not be the preferred way of working; only use the Clip List Source when there's a real reason to do so (like in the below case, where we're making use of the clip list trimming capabilities).</span></span>

<span data-ttu-id="5257c-531">미디어 파일 입력에서 클립 목록 원본으로 전환하려면 클립 목록 원본 구성 요소를 디자인 화면으로 끌어서 클립 목록 XML 핀을 워크플로 디자이너의 클립 목록 XML 노드에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-531">To switch from our Media File Input to the Clip List Source, drag the Clip List Source component onto the design surface and connect the Clip List XML pin to the Clip List XML node of the workflow designer.</span></span> <span data-ttu-id="5257c-532">입력 비디오에 따라 출력 핀으로 클립 목록 원본을 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-532">This should populate the Clip List Source with output pins, according to our input video.</span></span> <span data-ttu-id="5257c-533">이제 압축되지 않은 비디오 및 압축되지 않은 오디오 핀을 클립 목록 원본에서 해당 AVC 인코더 및 오디오 스트림 인터리버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-533">Now connect the Uncompressed Video and Uncompressed Audio pins from the the Clip List Source to the respective AVC Encoders and Audio Stream Interleaver.</span></span> <span data-ttu-id="5257c-534">이제 미디어 파일 입력을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-534">Now remove the Media File Input.</span></span>

![클립 목록 원본으로 미디어 파일 입력 바꾸기](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

<span data-ttu-id="5257c-536">*클립 목록 원본으로 미디어 파일 입력 바꾸기*</span><span class="sxs-lookup"><span data-stu-id="5257c-536">*Replaced the Media File Input with the Clip List Source*</span></span>

<span data-ttu-id="5257c-537">클립 목록 원본 구성 요소는 "클립 목록 XML"을 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-537">The Clip List Source component takes as its input a "Clip List XML".</span></span> <span data-ttu-id="5257c-538">로컬로 테스트할 원본 파일을 선택한 경우 이 클립 목록 xml은 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-538">When selecting the source file to test with locally, this clip list xml is auto-populated for you.</span></span>

![자동으로 채워진 클립 목록 XML 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

<span data-ttu-id="5257c-540">*자동으로 채워진 클립 목록 XML 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-540">*Auto-populated Clip List XML property*</span></span>

<span data-ttu-id="5257c-541">xml을 더 자세히 알아보려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-541">Looking a bit closer to the xml, this is how it looks like:</span></span>

![클립 목록 대화 상자 편집](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

<span data-ttu-id="5257c-543">*클립 목록 대화 상자 편집*</span><span class="sxs-lookup"><span data-stu-id="5257c-543">*Edit clip list dialog*</span></span>

<span data-ttu-id="5257c-544">그러나 클립 목록 xml의 기능을 반영하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-544">This however does not reflect the capabilities of the clip list xml.</span></span> <span data-ttu-id="5257c-545">한 가지 옵션은 비디오 및 오디오 원본에 다음과 같이 "트리밍" 요소를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-545">One option we have is to add a "Trim" element under both the video and audio source, like this:</span></span>

![클립 목록에 자르기 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

<span data-ttu-id="5257c-547">*클립 목록에 자르기 요소 추가*</span><span class="sxs-lookup"><span data-stu-id="5257c-547">*Adding a trim element to the clip list*</span></span>

<span data-ttu-id="5257c-548">위와 같이 클립 목록 xml을 수정하고 로컬 테스트 실행을 수행하는 경우 비디오에서 10-20초 사이가 잘린 비디오를 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-548">If you modify the clip list xml like this above and perform a local test run, you'll see the video correctly been trimmed between 10 and 20 seconds in the video.</span></span>

<span data-ttu-id="5257c-549">그러나 로컬로 실행할 때 발생한 것과 달리 동일한 cliplist xml은 Azure 미디어 서비스에서 실행되는 워크플로에 적용될 때 동일한 효과를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-549">Contrary to what happens when you do a local run though, this very same cliplist xml would not have the same effect when applied in a workflow that runs in Azure Media Services.</span></span> <span data-ttu-id="5257c-550">Azure Premium 인코더가 시작되면 cliplist xml은 인코딩 작업에서 지정한 입력 파일에 따라 매번 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-550">When Azure Premium Encoder starts, the cliplist xml is generated every time again, based on the input file the encoding job was given.</span></span> <span data-ttu-id="5257c-551">즉, xml에서 수행하는 변경 내용이 아쉽게도 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-551">This means that any changes we do on the xml would unfortunately be overridden.</span></span>

<span data-ttu-id="5257c-552">인코딩 작업이 시작될 때 cliplist xml의 초기화를 방지하려면 워크플로가 시작된 후에 바로 즉석에서 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-552">To counter the cliplist xml being wiped when an encoding job is started, we can re-generate it on the fly just after the start of our workflow.</span></span> <span data-ttu-id="5257c-553">"스크립팅된 구성 요소"라는 것을 통해 이러한 사용자 지정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-553">Such custom actions can be taken through what is called a "Scripted Component".</span></span> <span data-ttu-id="5257c-554">자세한 내용은 [스크립팅된 구성 요소 소개](media-services-media-encoder-premium-workflow-tutorials.md#scripting)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5257c-554">For more information, see [Introducing the Scripted Component](media-services-media-encoder-premium-workflow-tutorials.md#scripting).</span></span>

<span data-ttu-id="5257c-555">스크립트 구성 요소를 디자이너 화면으로 끌어오고 이름을 "SetClipListXML"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-555">Drag a Scripted Component onto the designer surface and rename it to "SetClipListXML".</span></span>

![스크립팅된 구성 요소 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

<span data-ttu-id="5257c-557">*스크립팅된 구성 요소 추가*</span><span class="sxs-lookup"><span data-stu-id="5257c-557">*Adding a Scripted Component*</span></span>

<span data-ttu-id="5257c-558">스크립팅된 구성 요소의 속성을 검사할 때 네 개의 스크립트 형식이 표시되고 각각 다른 스크립트로 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-558">When you inspect the properties of the Scripted Component, the four different script types will be shown, each configurable to a different script.</span></span>

![스크립팅된 구성 요소 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

<span data-ttu-id="5257c-560">*스크립팅된 구성 요소 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-560">*Scripted Component properties*</span></span>

### <span data-ttu-id="5257c-561"><a id="frame_based_trim_modify_clip_list"></a>스크립팅한 구성 요소에서 클립 목록 수정</span><span class="sxs-lookup"><span data-stu-id="5257c-561"><a id="frame_based_trim_modify_clip_list"></a>Modifying the clip list from a Scripted Component</span></span>
<span data-ttu-id="5257c-562">워크플로가 시작하는 동안 생성되는 cliplist xml을 다시 작성할 수 있기 전에 cliplist xml 속성 및 내용에 액세스할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-562">Before we can re-write the cliplist xml that is generated during workflow startup, we'll need to have access to the cliplist xml property and contents.</span></span> <span data-ttu-id="5257c-563">다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-563">We can do so like this:</span></span>

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![기록된 들어오는 클립 목록](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

<span data-ttu-id="5257c-565">*기록된 들어오는 클립 목록*</span><span class="sxs-lookup"><span data-stu-id="5257c-565">*Incoming clip list being logged*</span></span>

<span data-ttu-id="5257c-566">먼저 어떤 지점에서 어떤 지점까지 비디오를 트리밍하려는지 결정하는 방법이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-566">First we need a way to determine from which point till which point we want to trim the video.</span></span> <span data-ttu-id="5257c-567">워크플로에 덜 숙련된 사용자에게 편리하도록 두 개의 속성을 그래프의 루트에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-567">To make this convenient to the less-technical user of the workflow, publish two properties to the root of the graph.</span></span> <span data-ttu-id="5257c-568">이렇게 하려면 디자이너 화면을 마우스 오른쪽 단추로 클릭하고 "속성 추가"를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-568">To do this, right click the designer surface and select "Add Property":</span></span>

* <span data-ttu-id="5257c-569">첫 번째 속성: 형식의 "ClippingTimeStart": "시간 코드"</span><span class="sxs-lookup"><span data-stu-id="5257c-569">First property: "ClippingTimeStart" of type: "TIMECODE"</span></span>
* <span data-ttu-id="5257c-570">두 번째 속성: 형식의 "ClippingTimeEnd": "시간 코드"</span><span class="sxs-lookup"><span data-stu-id="5257c-570">Second property: "ClippingTimeEnd" of type: "TIMECODE"</span></span>

![클리핑 시작 시간에 속성 대화 상자 추가](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

<span data-ttu-id="5257c-572">*클리핑 시작 시간에 속성 대화 상자 추가*</span><span class="sxs-lookup"><span data-stu-id="5257c-572">*Add Property dialog for clipping start time*</span></span>

![워크플로 루트에 게시된 클리핑 시간 속성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

<span data-ttu-id="5257c-574">*워크플로 루트에 게시된 클리핑 시간 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-574">*Published clipping time props on workflow root*</span></span>

<span data-ttu-id="5257c-575">두 속성을 모두 적절한 값으로 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-575">Configure both properties to a suitable value:</span></span>

![클리핑 시작 및 종료 속성 구성](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

<span data-ttu-id="5257c-577">*클리핑 시작 및 종료 속성 구성*</span><span class="sxs-lookup"><span data-stu-id="5257c-577">*Configure the clipping start and end properties*</span></span>

<span data-ttu-id="5257c-578">이제 스크립트 내에서 다음과 같은 두 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-578">Now, from within our script, we can access both properties, like this:</span></span>

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![클리핑의 시작 및 종료를 보여주는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

<span data-ttu-id="5257c-580">*클리핑의 시작 및 종료를 보여주는 로그 창*</span><span class="sxs-lookup"><span data-stu-id="5257c-580">*Log window showing start and end of clipping*</span></span>

<span data-ttu-id="5257c-581">간단한 정규식을 사용하여 양식을 보다 편리하게 사용하도록 시간 코드 문자열을 구문 분석해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-581">Let's parse the timecode strings into a more convenient to use form, using a simple regular expression:</span></span>

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![구문 분석된 시간 코드의 출력이 있는 로그 창](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

<span data-ttu-id="5257c-583">*구문 분석된 시간 코드의 출력이 있는 로그 창*</span><span class="sxs-lookup"><span data-stu-id="5257c-583">*Log window with output of parsed timecode*</span></span>

<span data-ttu-id="5257c-584">이 정보가 있으므로 이제 cliplist xml를 수정하여 동영상의 원하는 정확한 프레임 클리핑에 대한 시작 및 종료 시간을 반영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-584">With this information at hand, we can now modify the cliplist xml to reflect the start and end times for the desired frame-accurate clipping of the movie.</span></span>

![자르기 요소를 추가하는 스크립트 코드](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

<span data-ttu-id="5257c-586">*자르기 요소를 추가하는 스크립트 코드*</span><span class="sxs-lookup"><span data-stu-id="5257c-586">*Script code to add trim elements*</span></span>

<span data-ttu-id="5257c-587">이 작업은 일반 문자열 조작 작업을 통해 수행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-587">This was done through normal string manipulation operations.</span></span> <span data-ttu-id="5257c-588">결과 수정된 클립 목록 xml은 워크플로 루트에서 "setProperty" 메서드를 통해 clipListXML 속성에 다시 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-588">The resulting modified clip list xml is written back to the clipListXML property on the workflow root through the "setProperty" method.</span></span> <span data-ttu-id="5257c-589">다른 테스트를 실행한 후에 로그 창은 다음을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-589">The log window after another test run would show us the following:</span></span>

![결과 클립 목록 로깅](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

<span data-ttu-id="5257c-591">*결과 클립 목록 로깅*</span><span class="sxs-lookup"><span data-stu-id="5257c-591">*Logging the resulting clip list*</span></span>

<span data-ttu-id="5257c-592">비디오 및 오디오 스트림을 자르는 방법을 보려면 테스트 실행을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-592">Do a test-run to see how the video and audio streams have been clipped.</span></span> <span data-ttu-id="5257c-593">하지만 트리밍 지점에 대한 값이 서로 다른 둘 이상의 테스트를 실행하면 고려하지 않은 점인 있음을 알 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="5257c-593">As you'll do more than one test-run with different values for the trimming points, you'll notice that those will not be taken into account however!</span></span> <span data-ttu-id="5257c-594">이유는 Azure 런타임과 달리 디자이너가 실행할 때 마다 cliplist xml을 재정의하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-594">The reason for this is that the designer, unlike the Azure runtime, does NOT override the cliplist xml every run.</span></span> <span data-ttu-id="5257c-595">즉 시작 지점과 종료 지점을 처음 설정한 때에만 xml을 변환할 수 있고, 다른 모든 시간에는 자르기 요소가 이미 있는 경우 가드 절(if(clipListXML.indexOf("<trim>") == -1))은 워크플로에서 다른 자르기 요소를 추가하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-595">This means that only the very first time you have set the in and out points, will cause the xml to transform, all the other times, our guard clause (if(clipListXML.indexOf("<trim>") == -1)) will prevent the workflow from adding another trim element when there's already one present.</span></span>

<span data-ttu-id="5257c-596">워크플로를 편리하게 로컬로 테스트하려는 가장 좋은 방법은 자르기 요소가 이미 있는지 조사하는 정리 코드를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-596">To make our workflow convenient to test locally, we best add some house-keeping code that inspects if a trim element was already present.</span></span> <span data-ttu-id="5257c-597">그렇다면 새 값으로 xml을 수정하여 계속하기 전에 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-597">If so, we can remove it before continuing by modifying the xml with the new values.</span></span> <span data-ttu-id="5257c-598">일반 문자열 조작을 사용하지 않고 구문 분석하는 실제 xml 개체 모델을 통해이 작업을 수행하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-598">Rather than using plain string manipulations, it's probably safer to do this through real xml object model parsing.</span></span>

<span data-ttu-id="5257c-599">하지만 이러한 코드를 추가할 수 있기 전에 먼저 스크립트의 시작 부분에 여러 개의 가져오기 문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-599">Before we can add such code though, we'll need to add a number of import statements at the start of our script first:</span></span>

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

<span data-ttu-id="5257c-600">그런 다음 필요한 정리 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-600">After this, we can add the required cleaning code:</span></span>

    //for local testing: delete any pre-existing trim elements from the clip list xml by parsing the xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
     //delete the trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

<span data-ttu-id="5257c-601">이 코드는 cliplist xml에 자르기 요소를 추가한 지점 바로 위에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-601">This code goes just above the point at which we add the trim elements to the cliplist xml.</span></span>

<span data-ttu-id="5257c-602">이 시점에서 변경 사항을 적용하는 동안 원하는 만큼 워크플로를 실행하고 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-602">At this point, we can run and modify our workflow as much as we want while having the changes applied ever time.</span></span>    

### <span data-ttu-id="5257c-603"><a id="frame_based_trim_clippingenabled_prop"></a>ClippingEnabled 편의 속성 추가</span><span class="sxs-lookup"><span data-stu-id="5257c-603"><a id="frame_based_trim_clippingenabled_prop"></a>Adding a ClippingEnabled convenience property</span></span>
<span data-ttu-id="5257c-604">항상 트리밍이 발생하기를 원하지 않으면 트리밍/클리핑을 사용할지 여부를 나타내는 편리한 부울 플래그를 추가하여 워크플로를 마무리하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-604">As you might not always want trimming to happen, let's finish off our workflow by adding a convenient boolean flag that indicates whether or not we want to enable trimming / clipping.</span></span>

<span data-ttu-id="5257c-605">이전과 마찬가지로 "부울" 형식의 "ClippingEnabled"라는 워크플로의 루트에 새 속성을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-605">Just as before, publish a new property to the root of our workflow called "ClippingEnabled" of type "BOOLEAN".</span></span>

![클리핑 설정에 게시된 속성 ](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

<span data-ttu-id="5257c-607">*클리핑 설정에 게시된 속성*</span><span class="sxs-lookup"><span data-stu-id="5257c-607">*Published a property for enabling clipping*</span></span>

<span data-ttu-id="5257c-608">간단한 가드 절 아래에서 트리밍해야 하는지를 확인하고 이와 같은 클립 목록을 수정할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5257c-608">With the below simple guard clause, we can check if trimming is required and decide if our clip list as such needs to be modified or not.</span></span>

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <span data-ttu-id="5257c-609"><a id="code"></a>코드 완료</span><span class="sxs-lookup"><span data-stu-id="5257c-609"><a id="code"></a>Complete code</span></span>
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

    //parse the start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse the end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from the clip list xml by parsing the xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find the trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about to delete any existing trim nodes");
    //delete the trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize the modified clip list xml dom into a string:
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

    //add trim elements to cliplist xml
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


## <a name="also-see"></a><span data-ttu-id="5257c-610">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5257c-610">Also see</span></span>
[<span data-ttu-id="5257c-611">Azure 미디어 서비스의 프리미엄 인코딩 소개</span><span class="sxs-lookup"><span data-stu-id="5257c-611">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5257c-612">Azure 미디어 서비스의 프리미엄 인코딩 사용 방법</span><span class="sxs-lookup"><span data-stu-id="5257c-612">How to Use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[<span data-ttu-id="5257c-613">Azure Media Service로 주문형 콘텐츠 인코딩</span><span class="sxs-lookup"><span data-stu-id="5257c-613">Encoding On-Demand Content with Azure Media Service</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

[<span data-ttu-id="5257c-614">미디어 인코더 Premium 워크플로 형식 및 코덱</span><span class="sxs-lookup"><span data-stu-id="5257c-614">Media Encoder Premium Workflow Formats and Codecs</span></span>](media-services-premium-workflow-encoder-formats.md)

[<span data-ttu-id="5257c-615">샘플 워크플로 파일</span><span class="sxs-lookup"><span data-stu-id="5257c-615">Sample workflow files</span></span>](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[<span data-ttu-id="5257c-616">Azure 미디어 서비스 탐색기 도구</span><span class="sxs-lookup"><span data-stu-id="5257c-616">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="5257c-617">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="5257c-617">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5257c-618">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="5257c-618">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
