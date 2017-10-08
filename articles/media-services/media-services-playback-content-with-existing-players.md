---
title: "기존 플레이어 tooplayback 콘텐츠-Azure aaaUse | Microsoft Docs"
description: "이 항목에서는 기존 플레이어를 사용할 수 있는 tooplayback 콘텐츠를 나열 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="b6b41-103">기존 플레이어를 사용하여 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="b6b41-103">Playing your content with existing players</span></span>
<span data-ttu-id="b6b41-104">Azure Media Services는 부드러운 스트리밍, HTTP 라이브 스트리밍 및 Mpeg-dash와 같은 여러 인기 있는 스트리밍 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="b6b41-105">이 항목에서는 사용할 수 있는 tootest 스트림을 tooexisting 플레이어입니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-105">This topic points you tooexisting players that you can use tootest your streams.</span></span>

### <a name="hello-azure-portal-media-services-content-player"></a><span data-ttu-id="b6b41-106">hello Azure 포털 미디어 서비스 콘텐츠 플레이어</span><span class="sxs-lookup"><span data-stu-id="b6b41-106">hello Azure portal Media Services content player</span></span>
<span data-ttu-id="b6b41-107">hello **Azure** 포털 콘텐츠 플레이어를 제공 합니다. 사용할 수 있는 tootest 비디오.</span><span class="sxs-lookup"><span data-stu-id="b6b41-107">hello **Azure** portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="b6b41-108">Hello 클릭 필요한 비디오 (가 있는지 확인 [게시](media-services-portal-publish.md)) hello 클릭 **재생** hello hello 포털 맨 아래에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-108">Click on hello desired video (make sure it was [published](media-services-portal-publish.md)) and click hello **Play** button at hello bottom of hello portal.</span></span>

<span data-ttu-id="b6b41-109">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-109">Some considerations apply:</span></span>

* <span data-ttu-id="b6b41-110">hello **미디어 서비스 콘텐츠 플레이어** hello 기본 스트리밍 끝점에서에서 재생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-110">hello **MEDIA SERVICES CONTENT PLAYER** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="b6b41-111">Tooplay 기본값이 아닌 스트리밍 끝점에서 다른 플레이어를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-111">If you want tooplay from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="b6b41-112">예를 들어 [Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="b6b41-114">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="b6b41-114">Azure Media Player</span></span>
<span data-ttu-id="b6b41-115">사용 하 여 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback hello 다음 형식 중 하나에서 콘텐츠 (지우기 또는 protected):</span><span class="sxs-lookup"><span data-stu-id="b6b41-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback your content (clear or protected) in any of hello following formats:</span></span>

* <span data-ttu-id="b6b41-116">부드러운 스트리밍</span><span class="sxs-lookup"><span data-stu-id="b6b41-116">Smooth Streaming</span></span>
* <span data-ttu-id="b6b41-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="b6b41-117">MPEG DASH</span></span>
* <span data-ttu-id="b6b41-118">HLS</span><span class="sxs-lookup"><span data-stu-id="b6b41-118">HLS</span></span>
* <span data-ttu-id="b6b41-119">프로그레시브 MP4</span><span class="sxs-lookup"><span data-stu-id="b6b41-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="b6b41-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="b6b41-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="b6b41-121">AES 암호화 토큰</span><span class="sxs-lookup"><span data-stu-id="b6b41-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="b6b41-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6b41-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="b6b41-123">Silverlight 플레이어</span><span class="sxs-lookup"><span data-stu-id="b6b41-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="b6b41-124">모니터링</span><span class="sxs-lookup"><span data-stu-id="b6b41-124">Monitoring</span></span>
[<span data-ttu-id="b6b41-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="b6b41-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="b6b41-126">PlayReady 토큰</span><span class="sxs-lookup"><span data-stu-id="b6b41-126">PlayReady with Token</span></span>
[<span data-ttu-id="b6b41-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6b41-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="b6b41-128">DASH 플레이어</span><span class="sxs-lookup"><span data-stu-id="b6b41-128">DASH Players</span></span>
[<span data-ttu-id="b6b41-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="b6b41-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="b6b41-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="b6b41-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="b6b41-131">기타</span><span class="sxs-lookup"><span data-stu-id="b6b41-131">Other</span></span>
<span data-ttu-id="b6b41-132">tootest HLS Url을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b6b41-132">tootest HLS URLs you can also use:</span></span>

* <span data-ttu-id="b6b41-133">**Safari** 또는</span><span class="sxs-lookup"><span data-stu-id="b6b41-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="b6b41-134">**3ivx HLS 플레이어** </span><span class="sxs-lookup"><span data-stu-id="b6b41-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="b6b41-135">비디오 플레이어 개발</span><span class="sxs-lookup"><span data-stu-id="b6b41-135">Developing video players</span></span>
<span data-ttu-id="b6b41-136">고유한 플레이어 참조 하는 toodevelop 방법에 대 한 내용은 [비디오 플레이어 개발](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="b6b41-136">For information about how toodevelop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b6b41-137">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="b6b41-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b6b41-138">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="b6b41-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
