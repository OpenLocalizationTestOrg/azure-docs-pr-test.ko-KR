---
title: "aaaConfigure hello Telestream Wirecast 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello Wirecast 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="f69ec-103">Hello Wirecast 인코더 toosend 단일 비트 전송률 라이브 스트림을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f69ec-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f69ec-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="f69ec-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="f69ec-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="f69ec-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="f69ec-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="f69ec-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="f69ec-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="f69ec-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="f69ec-108">이 항목에서는 방법을 tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="f69ec-109">자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="f69ec-110">이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="f69ec-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="f69ec-112">Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f69ec-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f69ec-113">Prerequisites</span></span>
* [<span data-ttu-id="f69ec-114">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="f69ec-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="f69ec-115">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="f69ec-116">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="f69ec-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="f69ec-117">최신 버전의 hello hello 설치 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="f69ec-118">Hello 도구를 시작 하 고 tooyour AMS 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="f69ec-119">팁</span><span class="sxs-lookup"><span data-stu-id="f69ec-119">Tips</span></span>
* <span data-ttu-id="f69ec-120">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="f69ec-121">바람직한 방법은 대역폭 요구 사항을 결정할 때는 toodouble hello 비트 전송률 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="f69ec-122">필수 요구 사항이 없을 때 네트워크 정체가 발생 hello 영향을 완화 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="f69ec-123">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="f69ec-124">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="f69ec-124">Create a channel</span></span>
1. <span data-ttu-id="f69ec-125">Hello AMSE 도구에서 toohello 이동 **Live** 탭을 hello 채널 영역 내에서 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="f69ec-126">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="f69ec-126">Select **Create channel…**</span></span> <span data-ttu-id="f69ec-127">hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-127">from hello menu.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="f69ec-129">채널 이름을 지정 hello 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="f69ec-130">채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="f69ec-131">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="f69ec-132">있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="f69ec-133">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-133">Click **Create Channel**.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="f69ec-135">hello 채널 toostart 20 분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="f69ec-136">Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp)합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f69ec-137">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="f69ec-138">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f69ec-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="f69ec-139"><a id=configure_wirecast_rtmp></a>Hello Telestream Wirecast 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="f69ec-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="f69ec-140">이 자습서 hello에 다음 출력 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="f69ec-141">이 섹션의 hello 나머지 구성 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="f69ec-142">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="f69ec-142">**Video**:</span></span>

* <span data-ttu-id="f69ec-143">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="f69ec-143">Codec: H.264</span></span>
* <span data-ttu-id="f69ec-144">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="f69ec-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="f69ec-145">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="f69ec-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="f69ec-146">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="f69ec-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="f69ec-147">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="f69ec-147">Frame Rate: 30</span></span>

<span data-ttu-id="f69ec-148">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="f69ec-148">**Audio**:</span></span>

* <span data-ttu-id="f69ec-149">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="f69ec-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="f69ec-150">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="f69ec-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="f69ec-151">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="f69ec-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="f69ec-152">구성 단계</span><span class="sxs-lookup"><span data-stu-id="f69ec-152">Configuration steps</span></span>
1. <span data-ttu-id="f69ec-153">RTMP 스트리밍에 대 한 설정 및을 사용 하는 hello 컴퓨터 있는 것에 hello Telestream Wirecast 응용 프로그램을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="f69ec-154">Hello 출력 toohello 이동 하 여 구성 **출력** 탭을 선택 하 고 **출력 설정...** .</span><span class="sxs-lookup"><span data-stu-id="f69ec-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="f69ec-155">있는지 hello 확인 **출력 대상** 너무 설정**RTMP 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="f69ec-156">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-156">Click **OK**.</span></span>
4. <span data-ttu-id="f69ec-157">Hello 설정 페이지에서 설정 hello **대상** 필드 toobe **Azure 미디어 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="f69ec-158">hello 인코딩 프로필은 너무 미리 선택**Azure H.264 720 p 16:9 (1280x720)**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="f69ec-159">toocustomize 이러한 설정은 선택 hello 기어 아이콘 toohello hello 오른쪽의 드롭다운을 선택한 후 **새 사전 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="f69ec-161">인코더 기본 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-161">Configure encoder presets.</span></span>

    <span data-ttu-id="f69ec-162">이름 hello 미리 설정 하 고 hello 다음 권장 되는 설정에 대 한 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="f69ec-163">**비디오**</span><span class="sxs-lookup"><span data-stu-id="f69ec-163">**Video**</span></span>

   * <span data-ttu-id="f69ec-164">인코더: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="f69ec-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="f69ec-165">초당 프레임 수: 30</span><span class="sxs-lookup"><span data-stu-id="f69ec-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="f69ec-166">평균 비트 전송률: 5000kbps(네트워크 제한 사항에 따라 조정 가능)</span><span class="sxs-lookup"><span data-stu-id="f69ec-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="f69ec-167">프로필: 기본</span><span class="sxs-lookup"><span data-stu-id="f69ec-167">Profile: Main</span></span>
   * <span data-ttu-id="f69ec-168">키 프레임 간격: 60프레임</span><span class="sxs-lookup"><span data-stu-id="f69ec-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="f69ec-169">**오디오**</span><span class="sxs-lookup"><span data-stu-id="f69ec-169">**Audio**</span></span>

   * <span data-ttu-id="f69ec-170">대상 비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="f69ec-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="f69ec-171">샘플 속도: 44.100kHz</span><span class="sxs-lookup"><span data-stu-id="f69ec-171">Sample Rate: 44.100 kHz</span></span>

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="f69ec-173">**저장**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-173">Press **Save**.</span></span>

    <span data-ttu-id="f69ec-174">hello Encoding 필드가 선택할 수 있는 새로 만든 hello 프로필이 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="f69ec-175">새 프로필 hello 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="f69ec-176">순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello Wirecast **RTMP 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="f69ec-177">뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="f69ec-178">hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="f69ec-179">Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="f69ec-181">Wirecast hello에 **출력 설정** 창 hello에이 정보를 붙여넣습니다 **주소** 필드 hello 출력 섹션과 스트림 이름 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="f69ec-183">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-183">Select **OK**.</span></span>
2. <span data-ttu-id="f69ec-184">주 hello에 **Wirecast** 화면에서 비디오 및 오디오 준비에 대 한 입력된 소스를 확인 한 다음 **스트림** hello 왼쪽 위 모서리에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="f69ec-186">클릭 하기 전에 **스트림**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="f69ec-187">또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="f69ec-188">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="f69ec-188">Test playback</span></span>

<span data-ttu-id="f69ec-189">Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="f69ec-190">Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="f69ec-191">Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="f69ec-192">오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="f69ec-193">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="f69ec-194">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="f69ec-194">Create a program</span></span>
1. <span data-ttu-id="f69ec-195">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="f69ec-196">Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="f69ec-198">Hello 프로그램 이름을 지정 하 고 필요한 경우 조정 hello **보관 창 길이** (기본값 too4 시간 어떤).</span><span class="sxs-lookup"><span data-stu-id="f69ec-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="f69ec-199">저장소 위치를 지정 하거나 hello 기본값으로 그대로 둡니다 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="f69ec-200">Hello 확인 **시작 hello 프로그램 이제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="f69ec-201">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="f69ec-202">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="f69ec-203">Hello 프로그램이 실행 되 면 hello 프로그램 마우스 오른쪽 단추로 클릭 하 고 너무 탐색 하 여 재생을 확인**재생 hello 프로그램이** 다음를 선택 하 고 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="f69ec-204">확인 하 고 나면 hello 프로그램을 다시 클릭 마우스 오른쪽 단추로 선택한 **hello 출력 URL tooClipboard 복사** (hello에서이 정보를 검색 하거나 **프로그램 정보 및 설정을** hello 메뉴에서 옵션).</span><span class="sxs-lookup"><span data-stu-id="f69ec-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="f69ec-205">분산된 tooan 대상 그룹에 대 한 라이브 보기 또는 hello 스트림 준비 toobe는 플레이어에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="f69ec-206">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f69ec-206">Troubleshooting</span></span>
<span data-ttu-id="f69ec-207">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="f69ec-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f69ec-208">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="f69ec-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f69ec-209">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="f69ec-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
