---
title: "NewTek TriCaster 인코더를 구성하여 단일 비트 전송률 라이브 스트림 보내기 | Microsoft 문서"
description: "이 항목에서는 Tricaster 라이브 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="28367-103">NewTek TriCaster 인코더를 사용하여 단일 비트 전송률 라이브 스트림 보내기</span><span class="sxs-lookup"><span data-stu-id="28367-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28367-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="28367-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="28367-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="28367-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="28367-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="28367-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="28367-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="28367-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="28367-108">이 항목에서는 [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) 라이브 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28367-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="28367-109">자세한 내용은 [Azure 미디어 서비스를 사용하여 라이브 인코딩을 수행할 수 있는 채널 작업](media-services-manage-live-encoder-enabled-channels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28367-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="28367-110">이 자습서에서는 AMSE(Azure 미디어 서비스 탐색기) 도구를 사용하여 AMS(Azure 미디어 서비스)를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="28367-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="28367-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="28367-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="28367-112">Mac 또는 Linux에서는 Azure Portal을 사용하여 [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28367-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="28367-113">기여 피드에서 라이브 인코딩에 사용할 수 있는 AMS 채널에 보내기 위해 Tricaster를 사용할 때 피드 간에 빠르게 잘라내기, 슬레이트 간 전환과 같은 Tricaster의 특정 기능을 사용하는 경우 라이브 이벤트에 비디오/오디오 결함이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="28367-114">AMS 팀에서 이러한 문제를 해결하기 위해 노력하고 있으며 그때까지 이러한 기능을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="28367-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="28367-115">Prerequisites</span></span>
* [<span data-ttu-id="28367-116">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="28367-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="28367-117">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="28367-118">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="28367-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="28367-119">최신 버전의 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="28367-120">이 도구를 시작하고 AMS 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="28367-121">팁</span><span class="sxs-lookup"><span data-stu-id="28367-121">Tips</span></span>
* <span data-ttu-id="28367-122">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="28367-123">대역폭 요구 사항을 결정할 때에 가장 좋은 방법은 스트리밍 비트 전송률을 두 배로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="28367-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="28367-124">이는 필수 요구 사항은 아니지만 네트워크 정체로 인한 영향을 줄이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="28367-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="28367-125">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="28367-126">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="28367-126">Create a channel</span></span>
1. <span data-ttu-id="28367-127">AMSE 도구에서 **라이브** 탭으로 이동하고 채널 영역 안을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="28367-128">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="28367-128">Select **Create channel…**</span></span> <span data-ttu-id="28367-129">(채널 만들기...)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-129">from the menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="28367-131">채널 이름을 지정합니다. 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="28367-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="28367-132">[채널 설정]에서 [Live Encoding] 옵션에 대해 **표준**을 선택하고, [입력 프로토콜]을 **RTMP**.로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="28367-133">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="28367-134">**새 채널 지금 시작** 이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="28367-135">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="28367-137">채널을 시작하는 데 20분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="28367-138">채널을 시작하는 동안 [인코더 구성](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28367-139">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="28367-140">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28367-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="28367-141"><a id=configure_tricaster_rtmp></a>NewTek TriCaster 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="28367-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="28367-142">이 자습서에서는 다음 출력 설정이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="28367-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="28367-143">이 섹션의 나머지 부분에서 구성 단계를 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="28367-144">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="28367-144">**Video**:</span></span>

* <span data-ttu-id="28367-145">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="28367-145">Codec: H.264</span></span>
* <span data-ttu-id="28367-146">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="28367-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="28367-147">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="28367-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="28367-148">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="28367-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="28367-149">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="28367-149">Frame Rate: 30</span></span>

<span data-ttu-id="28367-150">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="28367-150">**Audio**:</span></span>

* <span data-ttu-id="28367-151">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="28367-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="28367-152">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="28367-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="28367-153">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="28367-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="28367-154">구성 단계</span><span class="sxs-lookup"><span data-stu-id="28367-154">Configuration steps</span></span>
1. <span data-ttu-id="28367-155">사용 중인 비디오 입력 원본에 따라 새 **NewTek TriCaster** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28367-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="28367-156">해당 프로젝트 내에 있는 경우 **스트림** 단추를 찾고 그 옆의 기어 아이콘을 클릭하여 스트림 구성 메뉴에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="28367-158">메뉴가 열려 있으면 연결 제목 아래에서 **새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="28367-159">연결 형식에 대한 메시지가 표시되면 **Adobe Flash**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="28367-161">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-161">Click **OK**.</span></span>
5. <span data-ttu-id="28367-162">이제 **스트리밍 프로필** 아래에서 드롭다운 화살표를 클릭하고 **찾아보기**로 이동하여 FMLE 프로필을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="28367-164">구성한 FMLE 프로필이 저장된 위치로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="28367-165">선택한 다음 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="28367-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="28367-166">프로필이 업로드되면 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="28367-167">Tricaster **RTMP 끝점**에 할당하기 위해 채널의 입력 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="28367-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="28367-168">AMSE 도구로 다시 이동하여 채널 완료 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="28367-169">상태가 **시작 중**에서 **실행 중**으로 변경되었으면 입력 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="28367-170">채널이 실행 중일 때 채널 이름을 마우스 오른쪽 단추로 클릭하고 아래로 이동하여 **입력 URL을 클립보드로 복사**를 가리킨 다음 **기본 입력 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="28367-172">Tricaster 프로젝트 내의 **플래시 서버** 아래의 **위치** 필드에서 이 정보를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="28367-173">또한 **스트림 ID** 필드에 스트림 이름을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="28367-174">또한 스트림 정보가 FMLE 프로필에 추가된 경우 **설정 가져오기**를 클릭하고 저장된 FMLE 프로필로 이동한 다음 **확인**을 클릭하여 이 섹션으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="28367-175">관련 Flash Server(플래시 서버) 필드는 FMLE의 정보로 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="28367-177">완료되면 화면 아래쪽에 있는 **확인** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="28367-178">비디오 및 오디오를 Tricaster에 입력할 준비가 되면 **스트림** 단추를 클릭하여 AMS로 스트리밍을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="28367-180">**스트림**을 클릭하기 전에 채널이 준비되었는지 **반드시** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="28367-181">또한 15분을 초과할 때까지 입력 기여 피드 없이 채널을 준비 상태로 그대로 두지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="28367-182">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="28367-182">Test playback</span></span>
<span data-ttu-id="28367-183">AMSE 도구로 이동하고 테스트할 채널을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="28367-184">메뉴에서 **미리 보기 재생**을 가리키고 **Azure Media Player 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="28367-185">스트림이 플레이어에 나타나면 인코더가 AMS에 연결되도록 제대로 구성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="28367-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="28367-186">오류가 수신되면 채널을 다시 설정해서 인코더 설정을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="28367-187">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28367-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="28367-188">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="28367-188">Create a program</span></span>
1. <span data-ttu-id="28367-189">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="28367-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="28367-190">AMSE 도구의 **라이브** 탭에서 프로그램 영역 안을 마우스 오른쪽 단추로 클릭하고 **새 프로그램 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="28367-192">프로그램 이름을 지정하고 필요한 경우 **보관 창 길이** (기본값은 4시간)를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="28367-193">또한 저장소 위치를 지정하거나 기본값을 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="28367-194">**지금 프로그램 시작** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="28367-195">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="28367-196">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="28367-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="28367-197">프로그램이 실행되고 있으면 프로그램을 마우스 오른쪽 단추로 클릭하고 **프로그램 재생**으로 이동한 다음 **Azure Media Player 사용**을 선택하여 재생을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="28367-198">확인되었으면 프로그램을 마우스 오른쪽 단추로 다시 클릭하고 **출력 URL을 클립보드로 복사**를 선택하거나 메뉴의 **프로그램 정보 및 설정** 옵션에서 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="28367-199">이제 스트림을 플레이어에 포함하거나 실시간 보기를 위해 대상 그룹에게 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="28367-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="28367-200">문제 해결</span><span class="sxs-lookup"><span data-stu-id="28367-200">Troubleshooting</span></span>
<span data-ttu-id="28367-201">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="28367-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="28367-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28367-202">Next step</span></span>
<span data-ttu-id="28367-203">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="28367-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="28367-204">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="28367-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
