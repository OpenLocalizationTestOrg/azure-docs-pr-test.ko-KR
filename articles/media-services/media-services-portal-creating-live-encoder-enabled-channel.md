---
title: "aaaHow tooperform 라이브 스트리밍을 toocreate 다중 비트 전송률 스트림을 Azure 미디어 서비스를 사용 하 여 Azure 포털 hello로 | Microsoft Docs"
description: "이 자습서에서는 단일 비트 전송률 라이브 스트림을 수신 하는 채널을 만드는 단계 hello 하 고 hello Azure 포털을 사용 하 여 toomulti 비트 전송률 스트림으로 인코딩합니다."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a><span data-ttu-id="b8e31-103">Azure 포털 hello로 어떻게 스트리밍하 tooperform 라이브 스트리밍을 Azure 미디어 서비스 toocreate 다중 비트 전송률을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b8e31-103">How tooperform live streaming using Azure Media Services toocreate multi-bitrate streams with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8e31-104">포털</span><span class="sxs-lookup"><span data-stu-id="b8e31-104">Portal</span></span>](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="b8e31-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b8e31-105">.NET</span></span>](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [<span data-ttu-id="b8e31-106">REST API</span><span class="sxs-lookup"><span data-stu-id="b8e31-106">REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="b8e31-107">이 자습서에서는 hello 만드는 단계는 **채널** 단일 비트 전송률 라이브 스트림을 수신 하 고 toomulti 비트 전송률 스트림으로 인코딩합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-107">This tutorial walks you through hello steps of creating a **Channel** that receives a single-bitrate live stream and encodes it toomulti-bitrate stream.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e31-108">자세한 개념 정보에 대 한 라이브 인코딩이 관련된 tooChannels 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-108">For more conceptual information related tooChannels that are enabled for live encoding, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
> 
> 

## <a name="common-live-streaming-scenario"></a><span data-ttu-id="b8e31-109">일반적인 라이브 스트리밍 시나리오</span><span class="sxs-lookup"><span data-stu-id="b8e31-109">Common Live Streaming Scenario</span></span>
<span data-ttu-id="b8e31-110">hello 다음은 일반적인 라이브 스트리밍 응용 프로그램 만들기와 관련 된 일반적인 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-110">hello following are general steps involved in creating common live streaming applications.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e31-111">현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-111">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="b8e31-112">오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b8e31-112">Please contact  amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
> 
> 

1. <span data-ttu-id="b8e31-113">비디오 카메라 tooa 컴퓨터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-113">Connect a video camera tooa computer.</span></span> <span data-ttu-id="b8e31-114">시작 하 고 hello 다음 프로토콜 중 하나에 단일 비트 전송률 스트림을 출력 하는 온-프레미스 라이브 인코더 구성: RTMP, 부드러운 스트리밍 또는 RTP (MPEG-TS).</span><span class="sxs-lookup"><span data-stu-id="b8e31-114">Launch and configure an on-premises live encoder that can output a single bitrate stream in one of hello following protocols: RTMP, Smooth Streaming, or RTP (MPEG-TS).</span></span> <span data-ttu-id="b8e31-115">자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e31-115">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="b8e31-116">이 단계는 채널을 만든 후에도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-116">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="b8e31-117">채널을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-117">Create and start a Channel.</span></span> 
3. <span data-ttu-id="b8e31-118">검색 hello 채널 수집 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-118">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="b8e31-119">hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-119">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="b8e31-120">Hello 채널 미리 보기 URL을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-120">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="b8e31-121">이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-121">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="b8e31-122">이벤트/프로그램을 만듭니다(자산도 만들어짐).</span><span class="sxs-lookup"><span data-stu-id="b8e31-122">Create an event/program (that will also create an asset).</span></span> 
6. <span data-ttu-id="b8e31-123">(를 hello 연결 된 자산에 대 한 OnDemand 로케이터 만들기) hello 이벤트를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-123">Publish hello event (that will create an  OnDemand locator for hello associated asset).</span></span>    
7. <span data-ttu-id="b8e31-124">스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-124">Start hello event when you are ready toostart streaming and archiving.</span></span>
8. <span data-ttu-id="b8e31-125">필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-125">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="b8e31-126">hello 광고 hello 출력 스트림에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-126">hello advertisement is inserted in hello output stream.</span></span>
9. <span data-ttu-id="b8e31-127">Hello 이벤트 toostop 스트리밍 및 hello 이벤트를 보관 하려는 경우 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-127">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span>
10. <span data-ttu-id="b8e31-128">Hello 이벤트 삭제 (및 필요에 따라 hello 자산을 삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-128">Delete hello event (and optionally delete hello asset).</span></span>   

## <a name="in-this-tutorial"></a><span data-ttu-id="b8e31-129">자습서 내용</span><span class="sxs-lookup"><span data-stu-id="b8e31-129">In this tutorial</span></span>
<span data-ttu-id="b8e31-130">이 자습서에서는 hello Azure 포털은 작업을 수행 하는 사용 되는 tooaccomplish hello:</span><span class="sxs-lookup"><span data-stu-id="b8e31-130">In this tutorial, hello Azure portal is used tooaccomplish hello following tasks:</span></span> 

1. <span data-ttu-id="b8e31-131">채널을 만드는 즉 사용된 tooperform 라이브 인코딩을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-131">Create a channel that is enabled tooperform live encoding.</span></span>
2. <span data-ttu-id="b8e31-132">Get 순서 toosupply의 수집 URL hello 것 toolive 인코더입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-132">Get hello Ingest URL in order toosupply it toolive encoder.</span></span> <span data-ttu-id="b8e31-133">hello 라이브 인코더는이 URL tooingest hello 스트림을 hello 채널에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-133">hello live encoder will use this URL tooingest hello stream into hello Channel.</span></span>
3. <span data-ttu-id="b8e31-134">이벤트/프로그램(및 자산)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-134">Create an event/program (and an asset).</span></span>
4. <span data-ttu-id="b8e31-135">Hello 자산을 게시 하 고 스트리밍 Url을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-135">Publish hello asset and get streaming URLs.</span></span>  
5. <span data-ttu-id="b8e31-136">콘텐츠를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-136">Play your content.</span></span>
6. <span data-ttu-id="b8e31-137">정리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-137">Cleaning up.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8e31-138">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b8e31-138">Prerequisites</span></span>
<span data-ttu-id="b8e31-139">필요한 toocomplete hello 자습서는 hello 다음과가 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-139">hello following are required toocomplete hello tutorial.</span></span>

* <span data-ttu-id="b8e31-140">toocomplete이이 자습서에서는 Azure 계정이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-140">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="b8e31-141">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-141">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> 
  <span data-ttu-id="b8e31-142">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e31-142">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="b8e31-143">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="b8e31-143">A Media Services account.</span></span> <span data-ttu-id="b8e31-144">미디어 서비스 계정 toocreate 참조 [계정 만들기](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-144">toocreate a Media Services account, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b8e31-145">단일 비트 전송률 라이브 스트림을 보낼 수 있는 웹캠 및 인코더.</span><span class="sxs-lookup"><span data-stu-id="b8e31-145">A webcam and an encoder that can send a single bitrate live stream.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="b8e31-146">채널 만들기</span><span class="sxs-lookup"><span data-stu-id="b8e31-146">Create a channel</span></span>
1. <span data-ttu-id="b8e31-147">Hello에 [Azure 포털](https://portal.azure.com/), 미디어 서비스를 선택 하 고 미디어 서비스 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-147">In hello [Azure portal](https://portal.azure.com/), select Media Services and then click on your Media Services account name.</span></span>
2. <span data-ttu-id="b8e31-148">**라이브 스트리밍**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-148">Select **Live Streaming**.</span></span>
3. <span data-ttu-id="b8e31-149">**사용자 지정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-149">Select **Custom create**.</span></span> <span data-ttu-id="b8e31-150">이 옵션을 통해 Live Encoding에 사용할 수 있는 채널을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-150">This option will let you create a channel that is enabled for live encoding.</span></span>
   
    ![채널 만들기](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. <span data-ttu-id="b8e31-152">**설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-152">Click on **Settings**.</span></span>
   
   1. <span data-ttu-id="b8e31-153">Hello 선택 **라이브 인코딩을** 채널 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-153">Choose hello **Live Encoding** channel type.</span></span> <span data-ttu-id="b8e31-154">이 형식은 라이브 인코딩에 사용 하도록 설정 된 채널 toocreate 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-154">This type specifies that you want toocreate a Channel that is enabled for live encoding.</span></span> <span data-ttu-id="b8e31-155">의미 hello 들어오는 단일 비트 전송률을 스트림 toohello 채널을 전달 하 고 라이브 인코더를 지정 된 설정을 사용 하 여 다중 비트 전송률 스트림으로 인코딩될 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-155">That means hello incoming single bitrate stream is sent toohello Channel and encoded into a multi-bitrate stream using specified live encoder settings.</span></span> <span data-ttu-id="b8e31-156">자세한 내용은 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-156">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span> <span data-ttu-id="b8e31-157">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-157">Click OK.</span></span>
   2. <span data-ttu-id="b8e31-158">채널의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-158">Specify a channel's name.</span></span>
   3. <span data-ttu-id="b8e31-159">Hello hello 화면 맨 아래에 확인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-159">Click OK at hello bottom of hello screen.</span></span>
5. <span data-ttu-id="b8e31-160">선택 hello **수집** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-160">Select hello **Ingest** tab.</span></span>
   
   1. <span data-ttu-id="b8e31-161">이 페이지에서는 스트리밍 프로토콜을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-161">On this page, you can select a streaming protocol.</span></span> <span data-ttu-id="b8e31-162">Hello에 대 한 **라이브 인코딩을** 채널 형식을 유효한 프로토콜 옵션은:</span><span class="sxs-lookup"><span data-stu-id="b8e31-162">For hello **Live Encoding** channel type, valid protocol options are:</span></span>
      
      * <span data-ttu-id="b8e31-163">단일 비트 전송률 조각화된 MP4(부드러운 스트리밍)</span><span class="sxs-lookup"><span data-stu-id="b8e31-163">Single bitrate Fragmented MP4 (Smooth Streaming)</span></span>
      * <span data-ttu-id="b8e31-164">단일 비트 전송률 RTMP</span><span class="sxs-lookup"><span data-stu-id="b8e31-164">Single bitrate RTMP</span></span>
      * <span data-ttu-id="b8e31-165">RTP(MPEG-TS): RTP를 통한 MPEG-2 전송 스트림</span><span class="sxs-lookup"><span data-stu-id="b8e31-165">RTP (MPEG-TS): MPEG-2 Transport Stream over RTP.</span></span>
        
        <span data-ttu-id="b8e31-166">각 프로토콜에 대 한 자세한 내용은 참조 하십시오. [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-166">For detailed explanation about each protocol, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>
        
        <span data-ttu-id="b8e31-167">연결 된 이벤트/프로그램을 실행 하는 또는 hello 채널 하는 동안 hello 프로토콜 옵션을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-167">You cannot change hello protocol option while hello Channel or its associated events/programs are running.</span></span> <span data-ttu-id="b8e31-168">다른 프로토콜을 요청하는 경우 각각의 스트리밍 프로토콜에 대한 개별 채널을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-168">If you require different protocols, you should create separate channels for each streaming protocol.</span></span>  
   2. <span data-ttu-id="b8e31-169">IP 제한이 hello에 적용할 수 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-169">You can apply IP restriction on hello ingest.</span></span> 
      
       <span data-ttu-id="b8e31-170">Hello IP를 정의할 수 있는 주소 tooingest 비디오 toothis 채널을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-170">You can define hello IP addresses that are allowed tooingest a video toothis channel.</span></span> <span data-ttu-id="b8e31-171">허용된 IP 주소는 단일 IP 주소(예: '10.0.0.1'), IP 주소와 CIDR 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1/22'), 또는 IP 주소와 점으로 구분된 10진수 서브넷 마스크를 사용하는 IP 범위(예: '10.0.0.1(255.255.252.0)').</span><span class="sxs-lookup"><span data-stu-id="b8e31-171">Allowed IP addresses can be specified as either a single IP address (e.g. '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (e.g. '10.0.0.1/22'), or an IP range using an IP address and a dotted decimal subnet mask (e.g. '10.0.0.1(255.255.252.0)').</span></span>
      
       <span data-ttu-id="b8e31-172">IP 주소가 지정되지 않고 정의된 규칙이 없는 경우 IP 주소가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-172">If no IP addresses are specified and there is no rule definition then no IP address will be allowed.</span></span> <span data-ttu-id="b8e31-173">tooallow 모든 IP 주소 규칙을 만들고 0.0.0.0/0을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-173">tooallow any IP address, create a rule and set 0.0.0.0/0.</span></span>
6. <span data-ttu-id="b8e31-174">Hello에 **미리 보기** 탭, hello 미리 보기에서 IP 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-174">On hello **Preview** tab, apply IP restriction on hello preview.</span></span>
7. <span data-ttu-id="b8e31-175">Hello에 **인코딩** 탭 hello 인코딩 사전 설정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-175">On hello **Encoding** tab, specify hello encoding preset.</span></span> 
   
    <span data-ttu-id="b8e31-176">현재 시스템만 hello 사전 설정을 선택할 수는 **720p 기본**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-176">Currently, hello only system preset you can select is **Default 720p**.</span></span> <span data-ttu-id="b8e31-177">toospecify 사용자 지정 사전 설정, Microsoft 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-177">toospecify a custom preset, open a Microsoft support ticket.</span></span> <span data-ttu-id="b8e31-178">다음의 hello hello 이름을 입력으로 생성 하는 사전 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-178">Then, enter hello name of hello preset created for you.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8e31-179">현재 채널 시작 hello too30 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-179">Currently, hello Channel start can take up too30 minutes.</span></span> <span data-ttu-id="b8e31-180">채널 재설정 too5 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-180">Channel reset can take up too5 minutes.</span></span>
> 
> 

<span data-ttu-id="b8e31-181">Hello 채널에서을 클릭 하 고 선택할 수 hello 채널을 만든 후 **설정을** 채널 구성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-181">Once you created hello Channel, you can click on hello channel and select **Settings** where you can view your channels configurations.</span></span> 

<span data-ttu-id="b8e31-182">자세한 내용은 참조 [Azure 미디어 서비스 toocreate 다중 비트 전송률 스트림을 사용 하 여 라이브 스트리밍](media-services-manage-live-encoder-enabled-channels.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-182">For more information, see [Live streaming using Azure Media Services toocreate multi-bitrate streams](media-services-manage-live-encoder-enabled-channels.md).</span></span>

## <a name="get-ingest-urls"></a><span data-ttu-id="b8e31-183">수집 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="b8e31-183">Get ingest URLs</span></span>
<span data-ttu-id="b8e31-184">가져올 수 있습니다 hello 채널을 만든 후 수집 toohello 라이브 인코더 제공할 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-184">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="b8e31-185">hello 인코더에서 이러한 Url tooinput 라이브 스트림을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-185">hello encoder uses these URLs tooinput a live stream.</span></span>

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a><span data-ttu-id="b8e31-187">이벤트 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="b8e31-187">Create and manage events</span></span>
### <a name="overview"></a><span data-ttu-id="b8e31-188">개요</span><span class="sxs-lookup"><span data-stu-id="b8e31-188">Overview</span></span>
<span data-ttu-id="b8e31-189">채널은 toocontrol hello 게시 및 저장 라이브 스트림의 세그먼트의 수 있는 이벤트/프로그램와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-189">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="b8e31-190">채널은 이벤트/프로그램을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-190">Channels manage events/programs.</span></span> <span data-ttu-id="b8e31-191">hello 채널과 프로그램 관계는 매우 유사한 tootraditional 미디어 여기서는 채널에 일정 한 콘텐츠 스트림이 하 고 프로그램은 해당 채널의 이벤트 범위가 지정 된 toosome 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-191">hello Channel and Program relationship is very similar tootraditional media where a channel has a constant stream of content and a program is scoped toosome timed event on that channel.</span></span>

<span data-ttu-id="b8e31-192">시간을 기록 하는 hello 콘텐츠 tooretain hello 이벤트에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-192">You can specify hello number of hours you want tooretain hello recorded content for hello event by setting hello **Archive Window** length.</span></span> <span data-ttu-id="b8e31-193">이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-193">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="b8e31-194">보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-194">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="b8e31-195">이벤트 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-195">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="b8e31-196">또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-196">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="b8e31-197">각 이벤트는 자산에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-197">Each event is associated with an Asset.</span></span> <span data-ttu-id="b8e31-198">toopublish hello 이벤트 hello에 대 한 OnDemand 로케이터를 만들어야 합니다 자산에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-198">toopublish hello event you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="b8e31-199">이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-199">Having this locator will enable you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="b8e31-200">채널에서는 toothree hello 여러 보관 본을 만들 수 있도록 이벤트 동시에 실행 가능한 최대 지원 같은 들어오는 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-200">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="b8e31-201">이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-201">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="b8e31-202">예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 이벤트를 있지만 toobroadcast만 마지막 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-202">For example, your business requirement is tooarchive 6 hours of an event, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="b8e31-203">tooaccomplish이를 동시에 실행 가능한 두 개의 toocreate 필요한 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-203">tooaccomplish this, you need toocreate two concurrently running event.</span></span> <span data-ttu-id="b8e31-204">하나의 이벤트 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-204">One event is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="b8e31-205">hello 다른 이벤트 집합 tooarchive 10 분 동안 이며이 프로그램이 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-205">hello other event is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="b8e31-206">새 이벤트에 기존 프로그램을 다시 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-206">You should not reuse existing programs for new events.</span></span> <span data-ttu-id="b8e31-207">대신, 각 이벤트에 대해 새 프로그램을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-207">Instead, create and start a new program for each event.</span></span>

<span data-ttu-id="b8e31-208">스트리밍 및 보관 준비 toostart 있을 때는 행사/프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-208">Start an event/program when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="b8e31-209">Hello 이벤트 toostop 스트리밍 및 hello 이벤트를 보관 하려는 경우 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-209">Stop hello event whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="b8e31-210">toodelete 보관 된 콘텐츠 중지 되어 hello 이벤트를 삭제 하 고 hello 관련된 자산을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-210">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="b8e31-211">Hello 이벤트;에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-211">An asset cannot be deleted if it is used by hello event; hello event must be deleted first.</span></span> 

<span data-ttu-id="b8e31-212">중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b8e31-212">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="b8e31-213">수행 tooretain hello 보관 된 콘텐츠, 하지만 스트리밍에 사용할 수 없는, hello 스트리밍 로케이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-213">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="createstartstop-events"></a><span data-ttu-id="b8e31-214">이벤트 만들기/시작/중지</span><span class="sxs-lookup"><span data-stu-id="b8e31-214">Create/start/stop events</span></span>
<span data-ttu-id="b8e31-215">Hello 스트림 있으면 들어오는 hello 채널 시작할 수 있습니다는 자산, 프로그램 및 스트리밍 로케이터를 만들어 이벤트 스트리밍 hello.</span><span class="sxs-lookup"><span data-stu-id="b8e31-215">Once you have hello stream flowing into hello Channel you can begin hello streaming event by creating an Asset, Program, and Streaming Locator.</span></span> <span data-ttu-id="b8e31-216">Hello 스트림 보관 되 고 사용할 수 있는 tooviewers hello 스트리밍 끝점을 통해 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-216">This will archive hello stream and make it available tooviewers through hello Streaming Endpoint.</span></span> 

>[!NOTE]
><span data-ttu-id="b8e31-217">AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-217">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="b8e31-218">동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-218">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="b8e31-219">두 가지 방법으로 toostart 이벤트 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-219">There are two ways toostart event:</span></span> 

1. <span data-ttu-id="b8e31-220">Hello에서 **채널** 페이지에서 키를 눌러 **라이브 이벤트** tooadd 새 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-220">From hello **Channel** page, press **Live Event** tooadd a new event.</span></span>
   
    <span data-ttu-id="b8e31-221">이벤트 이름, 자산 이름, 보관 창 및 암호화 옵션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-221">Specify: event name, asset name, archive window, and encryption option.</span></span>
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    <span data-ttu-id="b8e31-223">두 었으 면 **이 라이브 이벤트를 지금 게시** 옵션을 선택 hello 이벤트 hello 게시 Url 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-223">If you left **Publish this live event now** checked, hello event hello PUBLISHING URLs will get created.</span></span>
   
    <span data-ttu-id="b8e31-224">누르면 **시작**준비 toostream hello 이벤트 때마다, 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-224">You can press **Start**, whenever you are ready toostream hello event.</span></span>
   
    <span data-ttu-id="b8e31-225">Hello 이벤트를 시작 하면 누르면 **조사식** toostart hello 콘텐츠를 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-225">Once you start hello event, you can press **Watch** toostart playing hello content.</span></span>
2. <span data-ttu-id="b8e31-226">또는 바로 가기 및 키를 눌러를 사용할 수 있습니다 **Go Live** hello 단추 **채널** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b8e31-226">Alternatively, you can use a shortcut and press **Go Live** button on hello **Channel** page.</span></span> <span data-ttu-id="b8e31-227">그러면 기본 자산, 프로그램 및 스트리밍 로케이터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-227">This will create a default Asset, Program, and Streaming Locator.</span></span>
   
    <span data-ttu-id="b8e31-228">hello 이벤트 이름은 **기본** hello 보관 창은 설정 되어 too8 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-228">hello event is named **default** and hello archive window is set too8 hours.</span></span>

<span data-ttu-id="b8e31-229">Hello hello에서 게시 된 이벤트를 볼 수 있습니다 **라이브 이벤트** 페이지.</span><span class="sxs-lookup"><span data-stu-id="b8e31-229">You can watch hello published event from hello **Live event** page.</span></span> 

<span data-ttu-id="b8e31-230">**가동 안 함**을 클릭하면 라이브 이벤트를 모두 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-230">If you click **Off Air**, it will stop all live events.</span></span> 

## <a name="watch-hello-event"></a><span data-ttu-id="b8e31-231">조사식 hello 이벤트</span><span class="sxs-lookup"><span data-stu-id="b8e31-231">Watch hello event</span></span>
<span data-ttu-id="b8e31-232">toowatch hello 이벤트 클릭 **조사식** 스트리밍 URL Azure 포털 또는 복사 hello hello와 원하는 플레이어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-232">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![생성일](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

<span data-ttu-id="b8e31-234">라이브 이벤트는 자동으로 중지 될 때 이벤트 tooon 주문형 콘텐츠를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-234">Live event automatically converts events tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="b8e31-235">정리</span><span class="sxs-lookup"><span data-stu-id="b8e31-235">Clean up</span></span>
<span data-ttu-id="b8e31-236">이벤트 스트리밍 작업을 마쳤으면 tooclean 이전에 프로 비전 하는 hello 리소스를 원하는 절차를 수행 하는 hello를 수행 하세요.</span><span class="sxs-lookup"><span data-stu-id="b8e31-236">If you are done streaming events and want tooclean up hello resources provisioned earlier, follow hello following procedure.</span></span>

* <span data-ttu-id="b8e31-237">Hello 스트림 hello 인코더에서 밀어넣기를 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-237">Stop pushing hello stream from hello encoder.</span></span>
* <span data-ttu-id="b8e31-238">Hello 채널을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-238">Stop hello channel.</span></span> <span data-ttu-id="b8e31-239">Hello 채널 중지 되 고 나면 비용이 발생 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-239">Once hello Channel is stopped, it will not incur any charges.</span></span> <span data-ttu-id="b8e31-240">Toostart 필요한 경우 다시 것은 hello 동일 수집 URL tooreconfigure 인코더 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-240">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="b8e31-241">주문형 스트림으로 라이브 이벤트 toocontinue tooprovide hello 보관 하려는 경우가 아니면 스트리밍 끝점을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-241">You can stop your Streaming Endpoint, unless you want toocontinue tooprovide hello archive of your live event as an on-demand stream.</span></span> <span data-ttu-id="b8e31-242">Hello 채널이 중지 상태인 경우 비용이 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-242">If hello channel is in stopped state, it will not incur any charges.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="b8e31-243">보관된 콘텐츠 보기</span><span class="sxs-lookup"><span data-stu-id="b8e31-243">View archived content</span></span>
<span data-ttu-id="b8e31-244">중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b8e31-244">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="b8e31-245">이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-245">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="b8e31-246">toomanage 자산, 선택 **설정** 클릭 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-246">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![자산](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a><span data-ttu-id="b8e31-248">고려 사항</span><span class="sxs-lookup"><span data-stu-id="b8e31-248">Considerations</span></span>
* <span data-ttu-id="b8e31-249">현재 hello 최대 8 시간은 라이브 이벤트 기간을 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-249">Currently, hello max recommended duration of a live event is 8 hours.</span></span> <span data-ttu-id="b8e31-250">오랜 시간에 대 한 채널 toorun 해야 할 경우 amslived (영문)에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b8e31-250">Please contact amslived at Microsoft.com if you need toorun a Channel for longer periods of time.</span></span>
* <span data-ttu-id="b8e31-251">끝점을 toostream 하려는 콘텐츠 스트리밍 hello hello에 있는지 확인 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-251">Make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>

## <a name="next-step"></a><span data-ttu-id="b8e31-252">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8e31-252">Next step</span></span>
<span data-ttu-id="b8e31-253">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b8e31-253">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b8e31-254">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b8e31-254">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

