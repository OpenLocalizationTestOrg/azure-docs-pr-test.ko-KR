---
title: "FMLE 인코더를 구성하여 단일 비트 전송률 라이브 스트림 보내기 | Microsoft 문서"
description: "이 항목에서는 FMLE(Flash Media Live Encoder) 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e831048f34ecf6e89595adc4bfd58b5977e04bdb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-fmle-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="b0d3c-103">FMLE 인코더를 사용하여 단일 비트 전송률 라이브 스트림 보내기</span><span class="sxs-lookup"><span data-stu-id="b0d3c-103">Use the FMLE encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0d3c-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="b0d3c-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="b0d3c-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="b0d3c-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="b0d3c-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="b0d3c-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="b0d3c-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="b0d3c-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="b0d3c-108">이 항목에서는 FMLE [(Flash Media Live Encoder)](http://www.adobe.com/products/flash-media-encoder.html) 인코더를 구성하여 라이브 인코딩에 사용할 수 있는 AMS 채널에 단일 비트 전송률 스트림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-108">This topic shows how to configure the [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="b0d3c-109">자세한 내용은 [Azure 미디어 서비스를 사용하여 라이브 인코딩을 수행할 수 있는 채널 작업](media-services-manage-live-encoder-enabled-channels.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="b0d3c-110">이 자습서에서는 AMSE(Azure 미디어 서비스 탐색기) 도구를 사용하여 AMS(Azure 미디어 서비스)를 관리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="b0d3c-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="b0d3c-112">Mac 또는 Linux에서는 Azure Portal을 사용하여 [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="b0d3c-113">이 자습서에서는 AAC 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="b0d3c-114">그러나 FMLE는 AAC를 기본적으로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="b0d3c-115">MainConcept과 같은 곳에서 AAC 인코딩에 대한 플러그 인( [AAC 플러그 인](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-115">You would need to purchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0d3c-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b0d3c-116">Prerequisites</span></span>
* [<span data-ttu-id="b0d3c-117">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="b0d3c-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="b0d3c-118">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="b0d3c-119">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="b0d3c-120">최신 버전의 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-120">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="b0d3c-121">이 도구를 시작하고 AMS 계정에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-121">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="b0d3c-122">팁</span><span class="sxs-lookup"><span data-stu-id="b0d3c-122">Tips</span></span>
* <span data-ttu-id="b0d3c-123">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="b0d3c-124">대역폭 요구 사항을 결정할 때에 가장 좋은 방법은 스트리밍 비트 전송률을 두 배로 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-124">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="b0d3c-125">이는 필수 요구 사항은 아니지만 네트워크 정체로 인한 영향을 줄이는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-125">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="b0d3c-126">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="b0d3c-127">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="b0d3c-127">Create a channel</span></span>
1. <span data-ttu-id="b0d3c-128">AMSE 도구에서 **라이브** 탭으로 이동하고 채널 영역 안을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-128">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="b0d3c-129">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="b0d3c-129">Select **Create channel…**</span></span> <span data-ttu-id="b0d3c-130">(채널 만들기...)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-130">from the menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="b0d3c-132">채널 이름을 지정합니다. 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-132">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="b0d3c-133">[채널 설정]에서 [Live Encoding] 옵션에 대해 **표준**을 선택하고, [입력 프로토콜]을 **RTMP**.로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-133">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="b0d3c-134">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="b0d3c-135">**새 채널 지금 시작** 이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-135">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="b0d3c-136">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="b0d3c-138">채널을 시작하는 데 20분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-138">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="b0d3c-139">채널을 시작하는 동안 [인코더 구성](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp)을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-139">While the channel is starting you can [configure the encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0d3c-140">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="b0d3c-141">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="b0d3c-142"><a id=configure_fmle_rtmp></a>FMLE 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="b0d3c-142"><a id=configure_fmle_rtmp></a>Configure the FMLE encoder</span></span>
<span data-ttu-id="b0d3c-143">이 자습서에서는 다음 출력 설정이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-143">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="b0d3c-144">이 섹션의 나머지 부분에서 구성 단계를 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-144">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="b0d3c-145">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="b0d3c-145">**Video**:</span></span>

* <span data-ttu-id="b0d3c-146">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="b0d3c-146">Codec: H.264</span></span>
* <span data-ttu-id="b0d3c-147">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="b0d3c-148">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="b0d3c-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="b0d3c-149">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="b0d3c-150">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="b0d3c-150">Frame Rate: 30</span></span>

<span data-ttu-id="b0d3c-151">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="b0d3c-151">**Audio**:</span></span>

* <span data-ttu-id="b0d3c-152">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="b0d3c-153">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="b0d3c-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="b0d3c-154">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="b0d3c-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="b0d3c-155">구성 단계</span><span class="sxs-lookup"><span data-stu-id="b0d3c-155">Configuration steps</span></span>
1. <span data-ttu-id="b0d3c-156">사용 중인 컴퓨터에 대한 FMLE(Flash Media Live Encoder)의 인터페이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-156">Navigate to the Flash Media Live Encoder’s (FMLE) interface on the machine being used.</span></span>

    <span data-ttu-id="b0d3c-157">이 인터페이스는 기본 설정 페이지 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-157">The interface is one main page of settings.</span></span> <span data-ttu-id="b0d3c-158">FMLE를 사용하여 스트리밍 시작하려면 다음 권장 설정에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-158">Please take note of the following recommended settings to get started with streaming using FMLE.</span></span>

   * <span data-ttu-id="b0d3c-159">형식: H.264 프레임 속도: 30.00</span><span class="sxs-lookup"><span data-stu-id="b0d3c-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="b0d3c-160">입력 크기: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="b0d3c-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="b0d3c-161">비트 전송률: 5,000kbps(네트워크 제한 사항에 따라 조정 가능)</span><span class="sxs-lookup"><span data-stu-id="b0d3c-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="b0d3c-163">인터레이스된 원본을 사용하는 경우 "디인터레이스" 옵션에 확인 표시를 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-163">When using interlaced sources, please checkmark the “Deinterlace” option</span></span>
2. <span data-ttu-id="b0d3c-164">형식 옆에 있는 렌치 아이콘을 선택합니다. 이러한 추가 설정은 다음과 같이 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-164">Select the wrench icon next to Format, these additional settings should be:</span></span>

   * <span data-ttu-id="b0d3c-165">프로필: 기본</span><span class="sxs-lookup"><span data-stu-id="b0d3c-165">Profile: Main</span></span>
   * <span data-ttu-id="b0d3c-166">수준: 4.0</span><span class="sxs-lookup"><span data-stu-id="b0d3c-166">Level: 4.0</span></span>
   * <span data-ttu-id="b0d3c-167">키 프레임 빈도: 2초</span><span class="sxs-lookup"><span data-stu-id="b0d3c-167">Keyframe Frequency: 2 seconds</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="b0d3c-169">다음의 중요한 오디오 설정을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-169">Set the following important audio setting:</span></span>

   * <span data-ttu-id="b0d3c-170">형식: AAC</span><span class="sxs-lookup"><span data-stu-id="b0d3c-170">Format: AAC</span></span>
   * <span data-ttu-id="b0d3c-171">샘플 속도: 44,100hz</span><span class="sxs-lookup"><span data-stu-id="b0d3c-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="b0d3c-172">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="b0d3c-172">Bitrate: 192 Kbps</span></span>

     ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="b0d3c-174">FMLE의 **RTMP 끝점**에 할당하기 위해 채널의 입력 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-174">Get the channel's input URL in order to assign it to the FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="b0d3c-175">AMSE 도구로 다시 이동하여 채널 완료 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-175">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="b0d3c-176">상태가 **시작 중**에서 **실행 중**으로 변경되었으면 입력 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-176">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="b0d3c-177">채널이 실행 중일 때 채널 이름을 마우스 오른쪽 단추로 클릭하고 아래로 이동하여 **입력 URL을 클립보드로 복사**를 가리킨 다음 **기본 입력 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-177">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="b0d3c-179">출력 섹션의 **FMS URL** 필드에 이 정보를 붙여 넣고 스트림 이름을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-179">Paste this information in the **FMS URL** field of the output section, and assign a stream name.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="b0d3c-181">추가 중복의 경우 보조 입력 URL을 사용하여 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-181">For extra redundancy, repeat these steps with the Secondary Input URL.</span></span>
6. <span data-ttu-id="b0d3c-182">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0d3c-183">**연결**을 클릭하기 전에 채널이 준비되었는지 **반드시** 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-183">Before you click **Connect**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="b0d3c-184">또한 15분을 초과할 때까지 입력 기여 피드 없이 채널을 준비 상태로 그대로 두지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-184">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="b0d3c-185">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="b0d3c-185">Test playback</span></span>

<span data-ttu-id="b0d3c-186">AMSE 도구로 이동하고 테스트할 채널을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-186">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="b0d3c-187">메뉴에서 **미리 보기 재생**을 가리키고 **Azure Media Player 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-187">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="b0d3c-188">스트림이 플레이어에 나타나면 인코더가 AMS에 연결되도록 제대로 구성된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-188">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="b0d3c-189">오류가 수신되면 채널을 다시 설정해서 인코더 설정을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-189">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="b0d3c-190">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-190">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="b0d3c-191">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="b0d3c-191">Create a program</span></span>
1. <span data-ttu-id="b0d3c-192">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="b0d3c-193">AMSE 도구의 **라이브** 탭에서 프로그램 영역 안을 마우스 오른쪽 단추로 클릭하고 **새 프로그램 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-193">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="b0d3c-195">프로그램 이름을 지정하고 필요한 경우 **보관 창 길이** (기본값은 4시간)를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-195">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="b0d3c-196">또한 저장소 위치를 지정하거나 기본값을 그대로 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-196">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="b0d3c-197">**지금 프로그램 시작** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-197">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="b0d3c-198">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="b0d3c-199">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="b0d3c-200">프로그램이 실행되고 있으면 프로그램을 마우스 오른쪽 단추로 클릭하고 **프로그램 재생**으로 이동한 다음 **Azure Media Player 사용**을 선택하여 재생을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-200">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="b0d3c-201">확인되었으면 프로그램을 마우스 오른쪽 단추로 다시 클릭하고 **출력 URL을 클립보드로 복사**를 선택하거나 메뉴의 **프로그램 정보 및 설정** 옵션에서 이 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-201">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="b0d3c-202">이제 스트림을 플레이어에 포함하거나 실시간 보기를 위해 대상 그룹에게 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-202">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="b0d3c-203">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b0d3c-203">Troubleshooting</span></span>
<span data-ttu-id="b0d3c-204">참고 자료를 보려면 [문제 해결](media-services-troubleshooting-live-streaming.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b0d3c-204">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b0d3c-205">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b0d3c-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b0d3c-206">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b0d3c-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
