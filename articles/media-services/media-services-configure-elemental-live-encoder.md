---
title: "aaaConfigure hello 실세계 라이브 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello 실세계 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="20750-103">단일 비트 전송률 라이브 스트림을 실세계 라이브 인코더 toosend hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="20750-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20750-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="20750-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="20750-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="20750-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="20750-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="20750-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="20750-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="20750-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="20750-108">이 항목에서는 방법을 tooconfigure hello [실세계 라이브](http://www.elementaltechnologies.com/products/elemental-live) 인코더 toosend 단일 비트 전송률 스트림 라이브 인코딩을 tooAMS 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="20750-109">자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="20750-110">이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="20750-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="20750-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="20750-112">Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="20750-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="20750-113">Prerequisites</span></span>
* <span data-ttu-id="20750-114">실세계 라이브 웹 인터페이스 toocreate 라이브 이벤트를 사용 하 여 대 한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="20750-115">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="20750-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="20750-116">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="20750-117">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20750-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="20750-118">최신 버전의 hello hello 설치 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="20750-119">Hello 도구를 시작 하 고 tooyour AMS 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="20750-120">팁</span><span class="sxs-lookup"><span data-stu-id="20750-120">Tips</span></span>
* <span data-ttu-id="20750-121">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="20750-122">바람직한 방법은 대역폭 요구 사항을 결정할 때는 toodouble hello 비트 전송률 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="20750-123">필수 요구 사항이 없을 때 네트워크 정체가 발생 hello 영향을 완화 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20750-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="20750-124">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="20750-125">RTP 수집을 사용한 Elemental 라이브</span><span class="sxs-lookup"><span data-stu-id="20750-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="20750-126">이 섹션에서는 어떻게 tooconfigure hello 실세계 라이브 인코더를 보내는 단일 비트 전송률 라이브 스트림을 RTP를 통한 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="20750-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="20750-127">자세한 내용은 [RTP를 통한 MPEG-TS 스트림](media-services-manage-live-encoder-enabled-channels.md#channel)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20750-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="20750-128">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="20750-128">Create a channel</span></span>

1. <span data-ttu-id="20750-129">Hello AMSE 도구에서 toohello 이동 **Live** 탭을 hello 채널 영역 내에서 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="20750-130">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="20750-130">Select **Create channel…**</span></span> <span data-ttu-id="20750-131">hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-131">from hello menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="20750-133">채널 이름을 지정 hello 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="20750-134">채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTP (MPEG-TS)**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="20750-135">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="20750-136">있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="20750-137">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="20750-139">hello 채널 toostart 20 분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="20750-140">Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp)합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20750-141">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="20750-142">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20750-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="20750-143"><a id=configure_elemental_rtp></a>Hello 실세계 라이브 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="20750-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="20750-144">이 자습서 hello에 다음 출력 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="20750-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="20750-145">이 섹션의 hello 나머지 구성 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="20750-146">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="20750-146">**Video**:</span></span>

* <span data-ttu-id="20750-147">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="20750-147">Codec: H.264</span></span>
* <span data-ttu-id="20750-148">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="20750-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="20750-149">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="20750-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="20750-150">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="20750-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="20750-151">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="20750-151">Frame Rate: 30</span></span>

<span data-ttu-id="20750-152">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="20750-152">**Audio**:</span></span>

* <span data-ttu-id="20750-153">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="20750-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="20750-154">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="20750-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="20750-155">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="20750-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="20750-156">구성 단계</span><span class="sxs-lookup"><span data-stu-id="20750-156">Configuration steps</span></span>
1. <span data-ttu-id="20750-157">Toohello 이동 **실세계 라이브** 인터페이스를 구성 하 고 hello 인코더 설정 **UDP/TS** 스트리밍.</span><span class="sxs-lookup"><span data-stu-id="20750-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="20750-158">새 이벤트를 만든 후 toohello 출력 그룹 아래로 스크롤하여 더하고 hello **UDP/TS** 출력 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="20750-159">**새 스트림을**을 선택한 다음 **출력 추가**를 클릭하여 새 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20750-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="20750-161">해당 hello 실세계 이벤트에도 hello 시간 코드 것이 좋습니다. "시스템 클록" toohelp hello 인코더 스트림 오류의 hello 경우 다시 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="20750-162">이제 hello 출력 만들어지면 클릭 **스트림 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="20750-163">이제 hello 출력 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="20750-164">방금 만든 toohello "스트림 1" 아래로 스크롤하여을 hello 클릭 **비디오** hello 왼쪽에 탭 및 hello 확장 **고급** 설정 섹션.</span><span class="sxs-lookup"><span data-stu-id="20750-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="20750-166">실세계 라이브에 사용할 수 있는 사용자 지정의 다양 한 범위의 있으면 hello 다음 설정이 권장 tooAMS 스트리밍 시작 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="20750-167">해상도: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="20750-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="20750-168">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="20750-168">Framerate: 30</span></span>
   * <span data-ttu-id="20750-169">GOP 크기: 60프레임</span><span class="sxs-lookup"><span data-stu-id="20750-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="20750-170">인터레이스 모드: Progressive</span><span class="sxs-lookup"><span data-stu-id="20750-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="20750-171">비트 전송률: 5,000,000bit/s(네트워크 제한 사항에 따라 조정 가능)</span><span class="sxs-lookup"><span data-stu-id="20750-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="20750-173">Hello 채널의 입력된 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20750-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="20750-174">뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="20750-175">hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="20750-176">Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="20750-178">Hello에이 정보를 붙여넣습니다 **기본 대상** hello Elemental 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="20750-179">다른 모든 설정은 hello 기본 남을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-179">All other settings can remain hello default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="20750-181">추가 중복성을 위해 UDP/TS 스트리밍에 대 한 별도 "Output" 탭을 만들어 hello 보조 입력 URL로 다음이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="20750-182">클릭 **만들기** (새 이벤트가 생성 된) 경우 또는 **업데이트** (기존 이벤트 편집) 하는 경우 후 toostart hello 인코더를 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20750-183">클릭 하기 전에 **시작** hello 실세계 라이브 웹 인터페이스에 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="20750-184">또한 tooleave hello 채널 > 15 분 이상에 대 한 이벤트 없이 준비 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="20750-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="20750-185">Hello 스트림을 30 초 동안 실행 한 후 뒤로 toohello AMSE 도구 및 테스트 재생을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="20750-186">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="20750-186">Test playback</span></span>

<span data-ttu-id="20750-187">Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="20750-188">Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="20750-189">Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="20750-190">오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="20750-191">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="20750-192">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="20750-192">Create a program</span></span>
1. <span data-ttu-id="20750-193">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="20750-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="20750-194">Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="20750-196">Hello 프로그램 이름을 지정 하 고 필요한 경우 조정 hello **보관 창 길이** (기본값 too4 시간 어떤).</span><span class="sxs-lookup"><span data-stu-id="20750-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="20750-197">저장소 위치를 지정 하거나 hello 기본값으로 그대로 둡니다 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="20750-198">Hello 확인 **시작 hello 프로그램 이제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="20750-199">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="20750-200">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="20750-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="20750-201">Hello 프로그램이 실행 되 면 hello 프로그램 마우스 오른쪽 단추로 클릭 하 고 너무 탐색 하 여 재생을 확인**재생 hello 프로그램이** 다음를 선택 하 고 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="20750-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="20750-202">확인 하 고 나면 hello 프로그램을 다시 클릭 마우스 오른쪽 단추로 선택한 **hello 출력 URL tooClipboard 복사** (hello에서이 정보를 검색 하거나 **프로그램 정보 및 설정을** hello 메뉴에서 옵션).</span><span class="sxs-lookup"><span data-stu-id="20750-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="20750-203">분산된 tooan 대상 그룹에 대 한 라이브 보기 또는 hello 스트림 준비 toobe는 플레이어에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="20750-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="20750-204">문제 해결</span><span class="sxs-lookup"><span data-stu-id="20750-204">Troubleshooting</span></span>
<span data-ttu-id="20750-205">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="20750-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="20750-206">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="20750-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="20750-207">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="20750-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
