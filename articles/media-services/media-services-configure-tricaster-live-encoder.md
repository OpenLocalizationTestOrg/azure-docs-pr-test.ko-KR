---
title: "aaaConfigure hello NewTek TriCaster 인코더 toosend 단일 비트 전송률 라이브 스트림을 | Microsoft Docs"
description: "이 항목에서는 방법을 tooconfigure hello Tricaster 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널 보여 줍니다."
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
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="a0b6e-103">Hello NewTek TriCaster 인코더 toosend 단일 비트 전송률 라이브 스트림 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a0b6e-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0b6e-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="a0b6e-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="a0b6e-105">Elemental Live</span><span class="sxs-lookup"><span data-stu-id="a0b6e-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="a0b6e-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="a0b6e-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="a0b6e-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="a0b6e-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="a0b6e-108">이 항목에서는 방법을 tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) 라이브 인코더 toosend 라이브 인코딩을 사용 하는 단일 비트 전송률 스트림을 tooAMS 채널입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="a0b6e-109">자세한 내용은 참조 [있는지 Enabled tooPerform 라이브 인코딩하는 Azure 미디어 서비스 채널로 작업](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="a0b6e-110">이 자습서에서는 Azure 미디어 서비스 하는 toomanage 방법을 AMS () Azure 미디어 서비스 탐색기 (AMSE) 도구와 함께 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="a0b6e-111">이 도구는 Windows PC에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="a0b6e-112">Mac 또는 Linux를 사용 하 여 Azure 포털 toocreate hello [채널](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) 및 [프로그램](media-services-portal-creating-live-encoder-enabled-channel.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0b6e-113">에 대 한 기여도 보내기 위한 Tricaster를 사용 하 여 라이브 인코딩을 tooAMS 채널 피드 때에 있을 수 비디오/오디오 결함 라이브 이벤트 Tricaster 신속 하 게 피드, 사이 자르는 또는 슬레이트에서 전환 등의 특정 기능을 사용 하는 경우 .</span><span class="sxs-lookup"><span data-stu-id="a0b6e-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="a0b6e-114">hello AMS 팀은 협력 그때까지 이러한 문제를 수정한 것이 좋지 toouse 이러한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="a0b6e-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a0b6e-115">Prerequisites</span></span>
* [<span data-ttu-id="a0b6e-116">Azure Media Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="a0b6e-117">실행 중인 스트리밍 끝점이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="a0b6e-118">자세한 내용은 [미디어 서비스 계정에서 스트리밍 끝점 관리](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="a0b6e-119">최신 버전의 hello hello 설치 [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="a0b6e-120">Hello 도구를 시작 하 고 tooyour AMS 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="a0b6e-121">팁</span><span class="sxs-lookup"><span data-stu-id="a0b6e-121">Tips</span></span>
* <span data-ttu-id="a0b6e-122">가능하면 하드웨어에 내장된 인터넷 연결을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="a0b6e-123">바람직한 방법은 대역폭 요구 사항을 결정할 때는 toodouble hello 비트 전송률 스트리밍입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="a0b6e-124">필수 요구 사항이 없을 때 네트워크 정체가 발생 hello 영향을 완화 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="a0b6e-125">소프트웨어 기반 인코더를 사용하는 경우 불필요한 프로그램을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="a0b6e-126">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-126">Create a channel</span></span>
1. <span data-ttu-id="a0b6e-127">Hello AMSE 도구에서 toohello 이동 **Live** 탭을 hello 채널 영역 내에서 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="a0b6e-128">메뉴에서 **Create channel...**</span><span class="sxs-lookup"><span data-stu-id="a0b6e-128">Select **Create channel…**</span></span> <span data-ttu-id="a0b6e-129">hello 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-129">from hello menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="a0b6e-131">채널 이름을 지정 hello 설명 필드는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="a0b6e-132">채널 설정에서 선택 **표준** hello 라이브 인코딩을 옵션에 대 한 hello로 입력 프로토콜 설정 너무**RTMP**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="a0b6e-133">다른 모든 설정은 그대로 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="a0b6e-134">있는지 hello 확인 **시작 hello 새 채널 이제** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="a0b6e-135">**채널 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-135">Click **Create Channel**.</span></span>

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="a0b6e-137">hello 채널 toostart 20 분까지 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="a0b6e-138">Hello 채널을 시작 하는 동안 다음을 수행할 수 있습니다 [hello 인코더 구성](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0b6e-139">채널이 준비 상태가 되는 즉시 요금이 청구되기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="a0b6e-140">자세한 내용은 [채널 상태](media-services-manage-live-encoder-enabled-channels.md#states)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="a0b6e-141"><a id=configure_tricaster_rtmp></a>Hello NewTek TriCaster 인코더 구성</span><span class="sxs-lookup"><span data-stu-id="a0b6e-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="a0b6e-142">이 자습서 hello에 다음 출력 설정이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="a0b6e-143">이 섹션의 hello 나머지 구성 단계를 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="a0b6e-144">**비디오**:</span><span class="sxs-lookup"><span data-stu-id="a0b6e-144">**Video**:</span></span>

* <span data-ttu-id="a0b6e-145">코덱: H.264</span><span class="sxs-lookup"><span data-stu-id="a0b6e-145">Codec: H.264</span></span>
* <span data-ttu-id="a0b6e-146">프로필: 높음(수준 4.0)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="a0b6e-147">비트 전송률: 5,000kbps</span><span class="sxs-lookup"><span data-stu-id="a0b6e-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="a0b6e-148">키 프레임: 2초(60초)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="a0b6e-149">프레임 속도: 30</span><span class="sxs-lookup"><span data-stu-id="a0b6e-149">Frame Rate: 30</span></span>

<span data-ttu-id="a0b6e-150">**오디오**:</span><span class="sxs-lookup"><span data-stu-id="a0b6e-150">**Audio**:</span></span>

* <span data-ttu-id="a0b6e-151">코덱: AAC(LC)</span><span class="sxs-lookup"><span data-stu-id="a0b6e-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="a0b6e-152">비트 전송률: 192kbps</span><span class="sxs-lookup"><span data-stu-id="a0b6e-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="a0b6e-153">샘플 속도: 44.1khz</span><span class="sxs-lookup"><span data-stu-id="a0b6e-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="a0b6e-154">구성 단계</span><span class="sxs-lookup"><span data-stu-id="a0b6e-154">Configuration steps</span></span>
1. <span data-ttu-id="a0b6e-155">사용 중인 비디오 입력 원본에 따라 새 **NewTek TriCaster** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="a0b6e-156">한 번 해당 프로젝트 내의 hello 찾을 **스트림** 단추를 클릭 한 hello 기어 아이콘 다음 tooit tooaccess hello 스트림 구성 메뉴를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="a0b6e-158">Hello 메뉴를 연 후 클릭 **새로** hello 연결 제목에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="a0b6e-159">Hello 연결 유형에 대 한 메시지가 나타나면 선택 **Adobe Flash**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="a0b6e-161">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-161">Click **OK**.</span></span>
5. <span data-ttu-id="a0b6e-162">FMLE 프로필 hello 드롭다운 아래 화살표를 클릭 하 여 가져올 수 이제 **스트리밍 프로필** 너무 이동**찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="a0b6e-164">Toowhere 탐색 구성 hello FMLE 프로필을 저장 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="a0b6e-165">선택한 다음 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="a0b6e-166">Hello 프로필 업로드 되 면 toohello 다음 단계를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="a0b6e-167">순서 tooassign에 hello 채널의 입력된 URL을 가져올 것 toohello Tricaster **RTMP 끝점**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="a0b6e-168">뒤로 toohello AMSE 도구를 이동 하 고 hello 채널 완료 상태를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="a0b6e-169">hello 상태가 변경 되 면 **시작** 너무**실행**, hello 입력된 URL을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="a0b6e-170">Hello 채널 실행 중일 때 hello 채널 이름을 마우스 오른쪽 단추로 클릭, toohover 아래로 탐색 **입력 URL 복사 tooclipboard** 선택한 후 **기본 입력 URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="a0b6e-172">Hello에이 정보를 붙여넣습니다 **위치** 아래 **플래시 서버** hello Tricaster 프로젝트 내에서.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="a0b6e-173">Hello에 스트림 이름을 할당할 수도 **스트림 ID** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="a0b6e-174">스트림 정보 toohello FMLE 프로필에 추가한은 가져올 수를 클릭 하 여 toothis 섹션 **설정 가져오기**저장 toohello FMLE 프로필 탐색을 클릭 하 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="a0b6e-175">hello 관련 서버 플래시 필드 FMLE hello 정보로 채워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="a0b6e-177">완료 되 면 클릭 **확인** hello hello 화면 맨 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="a0b6e-178">Tricaster hello에 대 한 비디오 및 오디오 입력 준비 되 면 hello를 클릭 하 여 tooAMS 스트리밍을 시작 **스트림** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="a0b6e-180">클릭 하기 전에 **스트림**, 있습니다 **해야** hello 채널 사용할 준비가 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="a0b6e-181">또한 > 15 분 이상에 대 한 피드 tooleave hello 채널 입력된 기여 하지 않고 준비 상태가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="a0b6e-182">테스트 재생</span><span class="sxs-lookup"><span data-stu-id="a0b6e-182">Test playback</span></span>
<span data-ttu-id="a0b6e-183">Toohello AMSE 도구를 찾아 테스트 hello 채널 toobe 마우스 오른쪽 단추로 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="a0b6e-184">Hello 메뉴에서 위로 마우스를 가져가고 **재생 hello 미리 보기** 선택 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="a0b6e-185">Hello 스트림 hello 플레이어에 있으면 hello 인코더 올바르게 구성 된 tooconnect tooAMS 되었습니다 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="a0b6e-186">오류가 수신 되 면 hello 채널 toobe 재설정 및 인코더 설정을 조정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="a0b6e-187">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="a0b6e-188">프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a0b6e-188">Create a program</span></span>
1. <span data-ttu-id="a0b6e-189">채널 재생이 확인되면 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="a0b6e-190">Hello에서 **Live** hello AMSE 도구에서 탭 hello 프로그램 영역 내에서 마우스 오른쪽 단추로 클릭 하 고 선택 **새 프로그램 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="a0b6e-192">Hello 프로그램 이름을 지정 하 고 필요한 경우 조정 hello **보관 창 길이** (기본값 too4 시간 어떤).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="a0b6e-193">저장소 위치를 지정 하거나 hello 기본값으로 그대로 둡니다 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="a0b6e-194">Hello 확인 **시작 hello 프로그램 이제** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="a0b6e-195">**프로그램 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="a0b6e-196">프로그램 만들기는 채널 만들기보다 시간이 덜 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="a0b6e-197">Hello 프로그램이 실행 되 면 hello 프로그램 마우스 오른쪽 단추로 클릭 하 고 너무 탐색 하 여 재생을 확인**재생 hello 프로그램이** 다음를 선택 하 고 **Azure Media player**합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="a0b6e-198">확인 하 고 나면 hello 프로그램을 다시 클릭 마우스 오른쪽 단추로 선택한 **hello 출력 URL tooClipboard 복사** (hello에서이 정보를 검색 하거나 **프로그램 정보 및 설정을** hello 메뉴에서 옵션).</span><span class="sxs-lookup"><span data-stu-id="a0b6e-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="a0b6e-199">분산된 tooan 대상 그룹에 대 한 라이브 보기 또는 hello 스트림 준비 toobe는 플레이어에 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="a0b6e-200">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a0b6e-200">Troubleshooting</span></span>
<span data-ttu-id="a0b6e-201">Hello를 참조 하십시오 [문제 해결](media-services-troubleshooting-live-streaming.md) 지침에 대 한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="a0b6e-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0b6e-202">Next step</span></span>
<span data-ttu-id="a0b6e-203">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="a0b6e-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a0b6e-204">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="a0b6e-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
