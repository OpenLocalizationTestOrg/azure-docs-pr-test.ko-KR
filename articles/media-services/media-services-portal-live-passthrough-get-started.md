---
title: "hello Azure 포털을 사용 하 여 온-프레미스 인코더를 사용 하 여 aaaLive 스트림을 | Microsoft Docs"
description: "이 자습서에서는 hello 통과 배달에 대해 구성 하는 채널을 만드는 과정을 안내 합니다."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a><span data-ttu-id="b9d8f-103">어떻게를 통해 라이브 스트리밍 tooperform 온-프레미스 인코더 hello Azure 포털을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b9d8f-103">How tooperform live streaming with on-premises encoders using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9d8f-104">포털</span><span class="sxs-lookup"><span data-stu-id="b9d8f-104">Portal</span></span>](media-services-portal-live-passthrough-get-started.md)
> * [<span data-ttu-id="b9d8f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="b9d8f-105">.NET</span></span>](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [<span data-ttu-id="b9d8f-106">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="b9d8f-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

<span data-ttu-id="b9d8f-107">이 자습서에서는 Azure 포털 toocreate hello를 사용 하 여 hello 단계는 **채널** 하도록 구성 되어 있는 통과 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-107">This tutorial walks you through hello steps of using hello Azure portal toocreate a **Channel** that is configured for a pass-through delivery.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b9d8f-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="b9d8f-108">Prerequisites</span></span>
<span data-ttu-id="b9d8f-109">hello 다음은 필요한 toocomplete hello 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-109">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="b9d8f-110">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-110">An Azure account.</span></span> <span data-ttu-id="b9d8f-111">자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-111">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="b9d8f-112">Media Services 계정.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-112">A Media Services account.</span></span> <span data-ttu-id="b9d8f-113">미디어 서비스 계정 toocreate 참조 [어떻게 tooCreate Media Services 계정을](media-services-portal-create-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-113">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="b9d8f-114">웹캠.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-114">A webcam.</span></span> <span data-ttu-id="b9d8f-115">예를 들어, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm)</span><span class="sxs-lookup"><span data-stu-id="b9d8f-115">For example, [Telestream Wirecast encoder](http://www.telestream.net/wirecast/overview.htm).</span></span>

<span data-ttu-id="b9d8f-116">다음 문서 tooreview hello이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-116">It is highly recommended tooreview hello following articles:</span></span>

* [<span data-ttu-id="b9d8f-117">Azure 미디어 서비스 RTMP 지원 및 라이브 인코더</span><span class="sxs-lookup"><span data-stu-id="b9d8f-117">Azure Media Services RTMP Support and Live Encoders</span></span>](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [<span data-ttu-id="b9d8f-118">Azure 미디어 서비스를 사용하는 라이브 스트리밍 개요</span><span class="sxs-lookup"><span data-stu-id="b9d8f-118">Overview of Live Steaming using Azure Media Services</span></span>](media-services-manage-channels-overview.md)
* [<span data-ttu-id="b9d8f-119">다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍</span><span class="sxs-lookup"><span data-stu-id="b9d8f-119">Live streaming with on-premises encoders that create multi-bitrate streams</span></span>](media-services-live-streaming-with-onprem-encoders.md)

## <span data-ttu-id="b9d8f-120"><a id="scenario"></a>일반적인 라이브 스트리밍 시나리오</span><span class="sxs-lookup"><span data-stu-id="b9d8f-120"><a id="scenario"></a>Common live streaming scenario</span></span>
<span data-ttu-id="b9d8f-121">hello 다음 단계에서는 일반적인 라이브 스트리밍 응용 프로그램을 만드는 통과 배달에 대해 구성 된 채널을 사용 하는 것과 관련 된 작업.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-121">hello following steps describe tasks involved in creating common live streaming applications that use channels that are configured for pass-through delivery.</span></span> <span data-ttu-id="b9d8f-122">이 자습서에서는 어떻게 toocreate 통과 채널 및 라이브 이벤트 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-122">This tutorial shows how toocreate and manage a pass-through channel and live events.</span></span>

>[!NOTE]
><span data-ttu-id="b9d8f-123">스트리밍 끝점 toostream 콘텐츠 원하는 hello hello에 있는지 확인 **실행** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-123">Make sure hello streaming endpoint from which you want toostream content is in hello **Running** state.</span></span> 
    
1. <span data-ttu-id="b9d8f-124">비디오 카메라 tooa 컴퓨터에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-124">Connect a video camera tooa computer.</span></span> <span data-ttu-id="b9d8f-125">다중 비트 전송률 RTMP 또는 조각화된 MP4 스트림을 출력하는 온-프레미스 라이브 인코더를 실행 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-125">Launch and configure an on-premises live encoder that outputs a multi-bitrate RTMP or Fragmented MP4 stream.</span></span> <span data-ttu-id="b9d8f-126">자세한 내용은 [Azure 미디어 서비스 RTMP 지원 및 라이브 인코더](http://go.microsoft.com/fwlink/?LinkId=532824)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-126">For more information, see [Azure Media Services RTMP Support and Live Encoders](http://go.microsoft.com/fwlink/?LinkId=532824).</span></span>
   
    <span data-ttu-id="b9d8f-127">이 단계는 채널을 만든 후에도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-127">This step could also be performed after you create your Channel.</span></span>
2. <span data-ttu-id="b9d8f-128">통과 채널을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-128">Create and start a pass-through Channel.</span></span>
3. <span data-ttu-id="b9d8f-129">검색 hello 채널 수집 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-129">Retrieve hello Channel ingest URL.</span></span> 
   
    <span data-ttu-id="b9d8f-130">hello 수집 URL hello 라이브 인코더 toosend hello 스트림 toohello 채널에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-130">hello ingest URL is used by hello live encoder toosend hello stream toohello Channel.</span></span>
4. <span data-ttu-id="b9d8f-131">Hello 채널 미리 보기 URL을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-131">Retrieve hello Channel preview URL.</span></span> 
   
    <span data-ttu-id="b9d8f-132">이 URL tooverify 채널이 라이브 스트림을 hello을 수신 하 고 제대로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-132">Use this URL tooverify that your channel is properly receiving hello live stream.</span></span>
5. <span data-ttu-id="b9d8f-133">라이브 이벤트/프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-133">Create a live event/program.</span></span> 
   
    <span data-ttu-id="b9d8f-134">Azure 포털을 hello를 사용 하 여, 하는 경우 라이브 이벤트를 만들면 자산도 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-134">When using hello Azure portal, creating a live event also creates an asset.</span></span> 

6. <span data-ttu-id="b9d8f-135">스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트/프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-135">Start hello event/program when you are ready toostart streaming and archiving.</span></span>
7. <span data-ttu-id="b9d8f-136">필요에 따라 hello 라이브 인코더에 신호를 받은 toostart 광고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-136">Optionally, hello live encoder can be signaled toostart an advertisement.</span></span> <span data-ttu-id="b9d8f-137">hello 광고 hello 출력 스트림에 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-137">hello advertisement is inserted in hello output stream.</span></span>
8. <span data-ttu-id="b9d8f-138">Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 이벤트/프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-138">Stop hello event/program whenever you want toostop streaming and archiving hello event.</span></span>
9. <span data-ttu-id="b9d8f-139">Hello 이벤트/프로그램을 삭제 합니다 (및 필요에 따라 hello 자산을 삭제) 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-139">Delete hello event/program (and optionally delete hello asset).</span></span>     

> [!IMPORTANT]
> <span data-ttu-id="b9d8f-140">검토 하십시오 [다중 비트 전송률 스트림을 만들 수 있는 온-프레미스 인코더를 통해 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md) toolearn 개념 및 고려 사항에 대 한 온-프레미스 인코더 및 통과 채널 toolive 스트리밍 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-140">Please review [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md) toolearn about concepts and considerations related toolive streaming with on-premises encoders and pass-through channels.</span></span>
> 
> 

## <a name="tooview-notifications-and-errors"></a><span data-ttu-id="b9d8f-141">tooview 알림 및 오류</span><span class="sxs-lookup"><span data-stu-id="b9d8f-141">tooview notifications and errors</span></span>
<span data-ttu-id="b9d8f-142">Tooview 알림을 발생 한 오류로 인해 hello 하 여 Azure 포털을 hello 알림 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-142">If you want tooview notifications and errors produced by hello Azure portal, click on hello Notification icon.</span></span>

![알림](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a><span data-ttu-id="b9d8f-144">통과 채널 및 이벤트 만들기 및 시작</span><span class="sxs-lookup"><span data-stu-id="b9d8f-144">Create and start pass-through channels and events</span></span>
<span data-ttu-id="b9d8f-145">채널은 toocontrol hello 게시 및 저장 라이브 스트림의 세그먼트의 수 있는 이벤트/프로그램와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-145">A channel is associated with events/programs that enable you toocontrol hello publishing and storage of segments in a live stream.</span></span> <span data-ttu-id="b9d8f-146">채널은 이벤트를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-146">Channels manage events.</span></span> 

<span data-ttu-id="b9d8f-147">시간을 기록 하는 hello 콘텐츠 tooretain hello 프로그램에 대 한 hello 설정 하 여 hello 수를 지정할 수 **보관 창** 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-147">You can specify hello number of hours you want tooretain hello recorded content for hello program by setting hello **Archive Window** length.</span></span> <span data-ttu-id="b9d8f-148">이 값은 최소 5 분 tooa 최대 25 시간에서에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-148">This value can be set from a minimum of 5 minutes tooa maximum of 25 hours.</span></span> <span data-ttu-id="b9d8f-149">보관 창 길이는 클라이언트 hello 현재 라이브 위치에서 시간에 다시 검색할 수 있는 시간을 최대한 hello 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-149">Archive window length also dictates hello maximum amount of time clients can seek back in time from hello current live position.</span></span> <span data-ttu-id="b9d8f-150">이벤트 hello 지정 된 시간 동안, 실행할 수는 있지만 hello 창 길이 보다 늦는 콘텐츠 계속 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-150">Events can run over hello specified amount of time, but content that falls behind hello window length is continuously discarded.</span></span> <span data-ttu-id="b9d8f-151">또한이 속성의이 값이 시간 hello 클라이언트 매니페스트가 증가할 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-151">This value of this property also determines how long hello client manifests can grow.</span></span>

<span data-ttu-id="b9d8f-152">각 이벤트는 자산에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-152">Each event is associated with an asset.</span></span> <span data-ttu-id="b9d8f-153">toopublish hello 이벤트 hello 연결 된 자산에 대 한 OnDemand 로케이터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-153">toopublish hello event, you must create an OnDemand locator for hello associated asset.</span></span> <span data-ttu-id="b9d8f-154">이 로케이터 toobuild tooyour 클라이언트를 제공할 수 있는 스트리밍 URL을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-154">Having this locator enables you toobuild a streaming URL that you can provide tooyour clients.</span></span>

<span data-ttu-id="b9d8f-155">채널에서는 toothree hello 여러 보관 본을 만들 수 있도록 이벤트 동시에 실행 가능한 최대 지원 같은 들어오는 스트림을 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-155">A channel supports up toothree concurrently running events so you can create multiple archives of hello same incoming stream.</span></span> <span data-ttu-id="b9d8f-156">이렇게 하면 필요에 따라 이벤트의 다른 부분 toopublish 및 보관 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-156">This allows you toopublish and archive different parts of an event as needed.</span></span> <span data-ttu-id="b9d8f-157">예를 들어 비즈니스 요구 사항 tooarchive 6 시간의 프로그램에서 나 toobroadcast만 마지막 10 분입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-157">For example, your business requirement is tooarchive 6 hours of a program, but toobroadcast only last 10 minutes.</span></span> <span data-ttu-id="b9d8f-158">tooaccomplish이, 두 개의 동시 실행 프로그램을 toocreate 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-158">tooaccomplish this, you need toocreate two concurrently running programs.</span></span> <span data-ttu-id="b9d8f-159">한 프로그램 tooarchive 6 시간의 이벤트 hello 설정 되어 있지만 hello 프로그램 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-159">One program is set tooarchive 6 hours of hello event but hello program is not published.</span></span> <span data-ttu-id="b9d8f-160">hello 다른 프로그램은 집합 tooarchive 10 분 동안 되며이 프로그램이 게시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-160">hello other program is set tooarchive for 10 minutes and this program is published.</span></span>

<span data-ttu-id="b9d8f-161">기존 라이브 이벤트를 다시 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-161">You should not reuse existing live events.</span></span> <span data-ttu-id="b9d8f-162">대신, 각 이벤트에 대해 새 이벤트를 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-162">Instead, create and start a new event for each event.</span></span>

<span data-ttu-id="b9d8f-163">스트리밍 및 보관 준비 toostart 있을 때는 hello 이벤트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-163">Start hello event when you are ready toostart streaming and archiving.</span></span> <span data-ttu-id="b9d8f-164">Toostop 스트리밍 및 보관 hello 이벤트 원할 때마다 hello 프로그램을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-164">Stop hello program whenever you want toostop streaming and archiving hello event.</span></span> 

<span data-ttu-id="b9d8f-165">toodelete 보관 된 콘텐츠 중지 되어 hello 이벤트를 삭제 하 고 hello 관련된 자산을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-165">toodelete archived content, stop and delete hello event and then delete hello associated asset.</span></span> <span data-ttu-id="b9d8f-166">이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-166">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="b9d8f-167">중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-167">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span>

<span data-ttu-id="b9d8f-168">수행 tooretain hello 보관 된 콘텐츠, 하지만 스트리밍에 사용할 수 없는, hello 스트리밍 로케이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-168">If you do want tooretain hello archived content, but not have it available for streaming, delete hello streaming locator.</span></span>

### <a name="toouse-hello-portal-toocreate-a-channel"></a><span data-ttu-id="b9d8f-169">toouse hello 포털 toocreate 채널</span><span class="sxs-lookup"><span data-stu-id="b9d8f-169">toouse hello portal toocreate a channel</span></span>
<span data-ttu-id="b9d8f-170">이 섹션에서는 어떻게 toouse hello **빠른 생성** 옵션 toocreate 채널을 통과 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-170">This section shows how toouse hello **Quick Create** option toocreate a pass-through channel.</span></span>

<span data-ttu-id="b9d8f-171">통과 채널에 대한 자세한 내용은 [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-171">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

1. <span data-ttu-id="b9d8f-172">Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-172">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b9d8f-173">Hello에 **설정** 창 클릭 **라이브 스트리밍**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-173">In hello **Settings** window, click **Live streaming**.</span></span> 
   
    ![시작](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    <span data-ttu-id="b9d8f-175">hello **라이브 스트리밍을** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-175">hello **Live streaming** window appears.</span></span>
3. <span data-ttu-id="b9d8f-176">클릭 **빠른 생성** toocreate RTMP hello로 통과 채널 수집 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-176">Click **Quick Create** toocreate a pass-through channel with hello RTMP ingest protocol.</span></span>
   
    <span data-ttu-id="b9d8f-177">hello **새 채널 만들기** 창이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-177">hello **CREATE A NEW CHANNEL** window appears.</span></span>
4. <span data-ttu-id="b9d8f-178">이름을 hello 새 채널을 지정 하 고 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-178">Give hello new channel a name and click **Create**.</span></span> 
   
    <span data-ttu-id="b9d8f-179">그러면 생성 통과 채널 hello RTMP 수집 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-179">This creates a pass-through channel with hello RTMP ingest protocol.</span></span>

## <a name="create-events"></a><span data-ttu-id="b9d8f-180">이벤트 생성</span><span class="sxs-lookup"><span data-stu-id="b9d8f-180">Create events</span></span>
1. <span data-ttu-id="b9d8f-181">원하는 tooadd 이벤트 채널 toowhich를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-181">Select a channel toowhich you want tooadd an event.</span></span>
2. <span data-ttu-id="b9d8f-182">**라이브 이벤트** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-182">Press **Live Event** button.</span></span>

![행사](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a><span data-ttu-id="b9d8f-184">수집 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="b9d8f-184">Get ingest URLs</span></span>
<span data-ttu-id="b9d8f-185">가져올 수 있습니다 hello 채널을 만든 후 수집 toohello 라이브 인코더 제공할 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-185">Once hello channel is created, you can get ingest URLs that you will provide toohello live encoder.</span></span> <span data-ttu-id="b9d8f-186">hello 인코더에서 이러한 Url tooinput 라이브 스트림을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-186">hello encoder uses these URLs tooinput a live stream.</span></span>

![생성일](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a><span data-ttu-id="b9d8f-188">조사식 hello 이벤트</span><span class="sxs-lookup"><span data-stu-id="b9d8f-188">Watch hello event</span></span>
<span data-ttu-id="b9d8f-189">toowatch hello 이벤트 클릭 **조사식** 스트리밍 URL Azure 포털 또는 복사 hello hello와 원하는 플레이어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-189">toowatch hello event, click **Watch** in hello Azure portal or copy hello streaming URL and use a player of your choice.</span></span> 

![생성일](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

<span data-ttu-id="b9d8f-191">라이브 이벤트는 자동으로 중지 될 때 변환 된 tooon 주문형 콘텐츠를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-191">Live event automatically get converted tooon-demand content when stopped.</span></span>

## <a name="clean-up"></a><span data-ttu-id="b9d8f-192">정리</span><span class="sxs-lookup"><span data-stu-id="b9d8f-192">Clean up</span></span>
<span data-ttu-id="b9d8f-193">통과 채널에 대한 자세한 내용은 [다중 비트 전송률 스트림을 만드는 온-프레미스 인코더를 사용한 라이브 스트리밍](media-services-live-streaming-with-onprem-encoders.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-193">For more details about pass-through channels, see [Live streaming with on-premises encoders that create multi-bitrate streams](media-services-live-streaming-with-onprem-encoders.md).</span></span>

* <span data-ttu-id="b9d8f-194">모든 이벤트/hello 채널에서 프로그램을 중지 하는 경우에 채널을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-194">A channel can be stopped only when all events/programs on hello channel have been stopped.</span></span>  <span data-ttu-id="b9d8f-195">Hello 채널 중지 되 고 나면 비용이 발생 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-195">Once hello Channel is stopped, it does not incur any charges.</span></span> <span data-ttu-id="b9d8f-196">Toostart 필요한 경우 다시 것은 hello 동일 수집 URL tooreconfigure 인코더 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-196">When you need toostart it again, it will have hello same ingest URL so you won't need tooreconfigure your encoder.</span></span>
* <span data-ttu-id="b9d8f-197">Hello 채널에서 모든 라이브 이벤트를 삭제 하는 경우에 채널을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-197">A channel can be deleted only when all live events on hello channel have been deleted.</span></span>

## <a name="view-archived-content"></a><span data-ttu-id="b9d8f-198">보관된 콘텐츠 보기</span><span class="sxs-lookup"><span data-stu-id="b9d8f-198">View archived content</span></span>
<span data-ttu-id="b9d8f-199">중지 하 고 hello 이벤트를 삭제 한 후에 사용자가 hello는 사용 될 수 toostream 보관 된 콘텐츠를 주문형 비디오로에 대 한 hello 자산을 삭제 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-199">Even after you stop and delete hello event, hello users would be able toostream your archived content as a video on demand, for as long as you do not delete hello asset.</span></span> <span data-ttu-id="b9d8f-200">이벤트에 의해 사용 되는 경우 자산을 삭제할 수 없습니다. hello 이벤트를 먼저 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-200">An asset cannot be deleted if it is used by an event; hello event must be deleted first.</span></span> 

<span data-ttu-id="b9d8f-201">toomanage 자산, 선택 **설정** 클릭 **자산**합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-201">toomanage your assets, select **Setting** and click **Assets**.</span></span>

![자산](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a><span data-ttu-id="b9d8f-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b9d8f-203">Next step</span></span>
<span data-ttu-id="b9d8f-204">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="b9d8f-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b9d8f-205">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b9d8f-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

