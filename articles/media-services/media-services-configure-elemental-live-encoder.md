---
title: "Elemental Live 인코더를 구성하여 단일 비트 전송률 라이브 스트림 보내기 | Microsoft 문서"
description: "이 항목에서는 Elemental 라이브 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다."
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="ed33c-103">Elemental 라이브 인코더를 사용하여 단일 비트 전송률 라이브 스트림 보내기</span><span class="sxs-lookup"><span data-stu-id="ed33c-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ed33c-104">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="ed33c-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="ed33c-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="ed33c-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="ed33c-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="ed33c-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="ed33c-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="ed33c-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="ed33c-108">이 항목에서는 [Elemental 라이브](http://www.elementaltechnologies.com/products/elemental-live) 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="ed33c-109">자세한 내용은 [Azure 미디어 서비스를 사용하여 라이브 인코딩을 수행할 수 있는 채널 작업](media-services-manage-live-encoder-enabled-channels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="ed33c-110">이 자습서에서는 AMSE(Azure 미디어 서비스 탐색기) 도구를 사용하여 AMS(Azure 미디어 서비스)를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="ed33c-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="ed33c-112">Mac 또는 Linux에서는 Azure Portal을 사용하여 [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed33c-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ed33c-113">Prerequisites</span></span>
* <span data-ttu-id="ed33c-114">라이브 이벤트를 만들려면 Elemental 라이브 웹 인터페이스 사용에 대한 실무 지식이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="ed33c-115">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="ed33c-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="ed33c-116">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="ed33c-117">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="ed33c-118">최신 버전의 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="ed33c-119">이 도구를 시작하고 AMS 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="ed33c-120">팁</span><span class="sxs-lookup"><span data-stu-id="ed33c-120">Tips</span></span>
* <span data-ttu-id="ed33c-121">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="ed33c-122">대역폭 요구 사항을 결정할 때에 가장 좋은 방법은 스트리밍 비트 전송률을 두 배로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="ed33c-123">이는 필수 요구 사항은 아니지만 네트워크 정체로 인한 영향을 줄이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="ed33c-124">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="ed33c-125">RTP 수집을 사용한 Elemental 라이브</span><span class="sxs-lookup"><span data-stu-id="ed33c-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="ed33c-126">이 섹션에서는 RTP를 통해 단일 비트 전송률 라이브 스트림을 전송하는 Elemental 라이브 인코더를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="ed33c-127">자세한 내용은 [RTP를 통한 MPEG-TS 스트림](media-services-manage-live-encoder-enabled-channels.md#channel)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="ed33c-128">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="ed33c-128">Create a channel</span></span>

1. <span data-ttu-id="ed33c-129">AMSE 도구에서 **라이브** 탭으로 이동하고 채널 영역 안을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="ed33c-130">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="ed33c-130">Select **Create channel…**</span></span> <span data-ttu-id="ed33c-131">(채널 만들기...)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-131">from the menu.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="ed33c-133">채널 이름을 지정합니다. 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="ed33c-134">[채널 설정]에서 [Live Encoding] 옵션에 대해 **표준**을 선택하고, [입력 프로토콜]을 **RTP(MPEG-TS)**.로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="ed33c-135">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="ed33c-136">**새 채널 지금 시작** 이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="ed33c-137">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-137">Click **Create Channel**.</span></span>

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="ed33c-139">채널을 시작하는 데 20분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="ed33c-140">채널을 시작하는 동안 [인코더 구성](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed33c-141">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="ed33c-142">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="ed33c-143"><a id=configure_elemental_rtp></a>Elemental 라이브 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="ed33c-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="ed33c-144">이 자습서에서는 다음 출력 설정이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="ed33c-145">이 섹션의 나머지 부분에서 구성 단계를 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="ed33c-146">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="ed33c-146">**Video**:</span></span>

* <span data-ttu-id="ed33c-147">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="ed33c-147">Codec: H.264</span></span>
* <span data-ttu-id="ed33c-148">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="ed33c-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="ed33c-149">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="ed33c-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="ed33c-150">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="ed33c-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="ed33c-151">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="ed33c-151">Frame Rate: 30</span></span>

<span data-ttu-id="ed33c-152">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="ed33c-152">**Audio**:</span></span>

* <span data-ttu-id="ed33c-153">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="ed33c-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="ed33c-154">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="ed33c-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="ed33c-155">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="ed33c-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="ed33c-156">구성 단계</span><span class="sxs-lookup"><span data-stu-id="ed33c-156">Configuration steps</span></span>
1. <span data-ttu-id="ed33c-157">**Elemental Live** 웹 인터페이스로 이동하고 **UDP/TS** 스트리밍을 위한 인코더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="ed33c-158">새 이벤트가 만들어지면 출력 그룹까지 아래로 스크롤하고 **UDP/TS** 출력 그룹을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="ed33c-159">**새 스트림을**을 선택한 다음 **출력 추가**를 클릭하여 새 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="ed33c-161">스트림 오류가 발생한 경우 Elemental 이벤트에서 인코더를 다시 연결할 수 있도록 하는 "시스템 시계"로 설정하는 시간 코드를 갖는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="ed33c-162">이제 출력이 만들어졌으므로 **스트림 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="ed33c-163">이제 출력 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="ed33c-164">방금 만든 "스트림 1"까지 아래로 스크롤하고 왼쪽의 **비디오** 탭을 클릭하고 **고급** 설정 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="ed33c-166">Elemental 라이브는 사용 가능한 다양한 범위의 사용자 지정이 있지만 AMS에 스트리밍을 시작하는데 다음 설정이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="ed33c-167">해상도: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="ed33c-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="ed33c-168">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="ed33c-168">Framerate: 30</span></span>
   * <span data-ttu-id="ed33c-169">GOP 크기: 60프레임</span><span class="sxs-lookup"><span data-stu-id="ed33c-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="ed33c-170">인터레이스 모드: Progressive</span><span class="sxs-lookup"><span data-stu-id="ed33c-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="ed33c-171">비트 전송률: 5,000,000bit/s(네트워크 제한 사항에 따라 조정 가능)</span><span class="sxs-lookup"><span data-stu-id="ed33c-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="ed33c-173">채널의 입력 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="ed33c-174">AMSE 도구로 다시 이동하여 채널 완료 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="ed33c-175">상태가 **시작 중**에서 **실행 중**으로 변경되었으면 입력 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="ed33c-176">채널이 실행 중일 때 채널 이름을 마우스 오른쪽 단추로 클릭하고 아래로 이동하여 **입력 URL을 클립보드로 복사**를 가리킨 다음 **기본 입력 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="ed33c-178">Elemental의 **기본 대상** 필드에 해당 정보를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="ed33c-179">다른 모든 설정은 기본값으로 남아 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-179">All other settings can remain the default.</span></span>

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="ed33c-181">추가 중복의 경우 UDP/TS 스트리밍에 대한 별도 "출력" 탭을 만들어서 보조 입력 URL로 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="ed33c-182">**만들기**(새 이벤트를 만든 경우) 또는 **업데이트**(기존 이벤트를 편집하는 경우)를 클릭한 다음 인코더를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed33c-183">Elemental Live 웹 인터페이스에서 **시작**을 클릭하기 전에 채널이 준비되었는지 **반드시** 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="ed33c-184">또한 15분을 초과할 때까지 이벤트 없이 채널을 준비 상태로 그대로 두지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="ed33c-185">스트림을 30초 동안 실행한 후 AMSE 도구 및 테스트 재생으로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="ed33c-186">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="ed33c-186">Test playback</span></span>

<span data-ttu-id="ed33c-187">AMSE 도구로 이동하고 테스트할 채널을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="ed33c-188">메뉴에서 **미리 보기 재생**을 가리키고 **Azure Media Player 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="ed33c-189">스트림이 플레이어에 나타나면 인코더가 AMS에 연결되도록 제대로 구성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="ed33c-190">오류가 수신되면 채널을 다시 설정해서 인코더 설정을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="ed33c-191">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="ed33c-192">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ed33c-192">Create a program</span></span>
1. <span data-ttu-id="ed33c-193">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="ed33c-194">AMSE 도구의 **라이브** 탭에서 프로그램 영역 안을 마우스 오른쪽 단추로 클릭하고 **새 프로그램 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="ed33c-196">프로그램 이름을 지정하고 필요한 경우 **보관 창 길이** (기본값은 4시간)를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="ed33c-197">또한 저장소 위치를 지정하거나 기본값을 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="ed33c-198">**지금 프로그램 시작** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="ed33c-199">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="ed33c-200">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="ed33c-201">프로그램이 실행되고 있으면 프로그램을 마우스 오른쪽 단추로 클릭하고 **프로그램 재생**으로 이동한 다음 **Azure Media Player 사용**을 선택하여 재생을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="ed33c-202">확인되었으면 프로그램을 마우스 오른쪽 단추로 다시 클릭하고 **출력 URL을 클립보드로 복사**를 선택하거나 메뉴의 **프로그램 정보 및 설정** 옵션에서 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="ed33c-203">이제 스트림을 플레이어에 포함하거나 실시간 보기를 위해 대상 그룹에게 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ed33c-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="ed33c-204">문제 해결</span><span class="sxs-lookup"><span data-stu-id="ed33c-204">Troubleshooting</span></span>
<span data-ttu-id="ed33c-205">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ed33c-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="ed33c-206">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="ed33c-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ed33c-207">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="ed33c-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
