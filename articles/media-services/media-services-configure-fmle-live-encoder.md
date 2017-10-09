---
title: "aaaConfigure hello FMLE 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello 플래시 미디어 라이브 인코더 (FMLE) 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다."
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
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="afda0-103">Hello FMLE 인코더 toosend 단일 비트 전송률 라이브 스트림을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="afda0-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="afda0-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="afda0-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="afda0-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="afda0-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="afda0-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="afda0-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="afda0-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="afda0-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="afda0-108">이 항목에서는 방법을 tooconfigure hello [Media 라이브 인코더 플래시](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) 인코더 toosend 단일 비트 전송률 스트림 라이브 인코딩을 tooAMS 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="afda0-109">자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="afda0-110">이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="afda0-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="afda0-112">Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="afda0-113">이 자습서에서는 AAC 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="afda0-114">그러나 FMLE는 AAC를 기본적으로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="afda0-115">해야 toopurchase AAC 인코딩에 대 한 플러그 인에서와 같이 MainConcept: [AAC 플러그 인](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="afda0-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afda0-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="afda0-116">Prerequisites</span></span>
* [<span data-ttu-id="afda0-117">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="afda0-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="afda0-118">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="afda0-119">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="afda0-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="afda0-120">최신 버전의 hello hello 설치 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="afda0-121">Hello 도구를 시작 하 고 tooyour AMS 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="afda0-122">팁</span><span class="sxs-lookup"><span data-stu-id="afda0-122">Tips</span></span>
* <span data-ttu-id="afda0-123">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="afda0-124">바람직한 방법은 대역폭 요구 사항을 결정할 때는 toodouble hello 비트 전송률 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="afda0-125">필수 요구 사항이 없을 때 네트워크 정체가 발생 hello 영향을 완화 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="afda0-126">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="afda0-127">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="afda0-127">Create a channel</span></span>
1. <span data-ttu-id="afda0-128">Hello AMSE 도구에서 toohello 이동 **Live** 탭을 hello 채널 영역 내에서 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="afda0-129">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="afda0-129">Select **Create channel…**</span></span> <span data-ttu-id="afda0-130">hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="afda0-132">채널 이름을 지정 hello 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="afda0-133">채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="afda0-134">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="afda0-135">있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="afda0-136">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="afda0-138">hello 채널 toostart 20 분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="afda0-139">Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp)합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afda0-140">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="afda0-141">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afda0-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="afda0-142"><a id=configure_fmle_rtmp></a>Hello FMLE 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="afda0-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="afda0-143">이 자습서 hello에 다음 출력 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="afda0-144">이 섹션의 hello 나머지 구성 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="afda0-145">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="afda0-145">**Video**:</span></span>

* <span data-ttu-id="afda0-146">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="afda0-146">Codec: H.264</span></span>
* <span data-ttu-id="afda0-147">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="afda0-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="afda0-148">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="afda0-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="afda0-149">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="afda0-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="afda0-150">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="afda0-150">Frame Rate: 30</span></span>

<span data-ttu-id="afda0-151">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="afda0-151">**Audio**:</span></span>

* <span data-ttu-id="afda0-152">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="afda0-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="afda0-153">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="afda0-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="afda0-154">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="afda0-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="afda0-155">구성 단계</span><span class="sxs-lookup"><span data-stu-id="afda0-155">Configuration steps</span></span>
1. <span data-ttu-id="afda0-156">Toohello 플래시 미디어 라이브 인코더의 (FMLE)에 사용 되는 hello 컴퓨터에 대 한 인터페이스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="afda0-157">hello 인터페이스는 설정의 기본 페이지 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="afda0-158">권장 하는 hello 다음의 참고 설정 tooget FMLE를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="afda0-159">형식: H.264 프레임 속도: 30.00</span><span class="sxs-lookup"><span data-stu-id="afda0-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="afda0-160">입력 크기: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="afda0-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="afda0-161">비트 전송률: 5,000kbps(네트워크 제한 사항에 따라 조정 가능)</span><span class="sxs-lookup"><span data-stu-id="afda0-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="afda0-163">사용 하 여 소스 인터레이스된 경우 확인 표시가 hello "" 디인터레이스 옵션 하세요.</span><span class="sxs-lookup"><span data-stu-id="afda0-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="afda0-164">선택 hello 렌치 아이콘 다음 tooFormat, 이러한 추가 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="afda0-165">프로필: 기본</span><span class="sxs-lookup"><span data-stu-id="afda0-165">Profile: Main</span></span>
   * <span data-ttu-id="afda0-166">수준: 4.0</span><span class="sxs-lookup"><span data-stu-id="afda0-166">Level: 4.0</span></span>
   * <span data-ttu-id="afda0-167">키 프레임 빈도: 2초</span><span class="sxs-lookup"><span data-stu-id="afda0-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="afda0-169">중요 한 오디오 설정에 따라 hello를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="afda0-170">형식: AAC</span><span class="sxs-lookup"><span data-stu-id="afda0-170">Format: AAC</span></span>
   * <span data-ttu-id="afda0-171">샘플 속도: 44,100hz</span><span class="sxs-lookup"><span data-stu-id="afda0-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="afda0-172">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="afda0-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="afda0-174">순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello FMLE의 **RTMP 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="afda0-175">뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="afda0-176">hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="afda0-177">Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="afda0-179">Hello에이 정보를 붙여넣습니다 **FMS URL** 필드 hello 출력 섹션과 스트림 이름 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="afda0-181">추가 중복성을 위해 hello 보조 입력 URL로 다음이 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="afda0-182">**연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afda0-183">클릭 하기 전에 **연결**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="afda0-184">또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="afda0-185">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="afda0-185">Test playback</span></span>

<span data-ttu-id="afda0-186">Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="afda0-187">Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="afda0-188">Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="afda0-189">오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="afda0-190">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="afda0-191">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="afda0-191">Create a program</span></span>
1. <span data-ttu-id="afda0-192">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="afda0-193">Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="afda0-195">Hello 프로그램 이름을 지정 하 고 필요한 경우 조정 hello **보관 창 길이** (기본값 too4 시간 어떤).</span><span class="sxs-lookup"><span data-stu-id="afda0-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="afda0-196">저장소 위치를 지정 하거나 hello 기본값으로 그대로 둡니다 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="afda0-197">Hello 확인 **시작 hello 프로그램 이제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="afda0-198">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="afda0-199">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="afda0-200">Hello 프로그램이 실행 되 면 hello 프로그램 마우스 오른쪽 단추로 클릭 하 고 너무 탐색 하 여 재생을 확인**재생 hello 프로그램이** 다음를 선택 하 고 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="afda0-201">확인 하 고 나면 hello 프로그램을 다시 클릭 마우스 오른쪽 단추로 선택한 **hello 출력 URL tooClipboard 복사** (hello에서이 정보를 검색 하거나 **프로그램 정보 및 설정을** hello 메뉴에서 옵션).</span><span class="sxs-lookup"><span data-stu-id="afda0-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="afda0-202">분산된 tooan 대상 그룹에 대 한 라이브 보기 또는 hello 스트림 준비 toobe는 플레이어에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="afda0-203">문제 해결</span><span class="sxs-lookup"><span data-stu-id="afda0-203">Troubleshooting</span></span>
<span data-ttu-id="afda0-204">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="afda0-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="afda0-205">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="afda0-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="afda0-206">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="afda0-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
