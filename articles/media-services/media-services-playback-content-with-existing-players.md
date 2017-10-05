---
title: "기존 플레이어를 사용하여 콘텐츠 재생 - Azure | Microsoft Docs"
description: "이 항목에서는 콘텐츠를 재생하는 데 사용할 수 있는 기존 플레이어를 나열합니다."
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
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="55b29-103">기존 플레이어를 사용하여 콘텐츠 재생</span><span class="sxs-lookup"><span data-stu-id="55b29-103">Playing your content with existing players</span></span>
<span data-ttu-id="55b29-104">Azure Media Services는 부드러운 스트리밍, HTTP 라이브 스트리밍 및 Mpeg-dash와 같은 여러 인기 있는 스트리밍 형식을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="55b29-105">이 항목에는 스트림을 테스트하는 데 사용할 수 있는 기존 플레이어가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="55b29-106">Azure Portal Media Services 콘텐츠 플레이어</span><span class="sxs-lookup"><span data-stu-id="55b29-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="55b29-107">**Azure** 포털에서는 비디오를 테스트하는 데 사용할 수 있는 콘텐츠 플레이어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="55b29-108">원하는 비디오( [게시된](media-services-portal-publish.md)것이어야 함)를 클릭하고 포털 맨 아래에 있는 **재생** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="55b29-109">다음과 같은 몇 가지 고려 사항이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-109">Some considerations apply:</span></span>

* <span data-ttu-id="55b29-110">**MEDIA SERVICES CONTENT PLAYER** 가 기본 스트리밍 끝점에서 재생됩니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="55b29-111">기본이 아닌 스트리밍 끝점에서 재생하려면 다른 플레이어를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="55b29-112">예를 들어 [Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="55b29-114">Azure 미디어 플레이어</span><span class="sxs-lookup"><span data-stu-id="55b29-114">Azure Media Player</span></span>
<span data-ttu-id="55b29-115">[Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html) 를 사용하여 다음 형식 중 하나로 콘텐츠(일반 또는 보호됨)를 재생합니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="55b29-116">부드러운 스트리밍</span><span class="sxs-lookup"><span data-stu-id="55b29-116">Smooth Streaming</span></span>
* <span data-ttu-id="55b29-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="55b29-117">MPEG DASH</span></span>
* <span data-ttu-id="55b29-118">HLS</span><span class="sxs-lookup"><span data-stu-id="55b29-118">HLS</span></span>
* <span data-ttu-id="55b29-119">프로그레시브 MP4</span><span class="sxs-lookup"><span data-stu-id="55b29-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="55b29-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="55b29-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="55b29-121">AES 암호화 토큰</span><span class="sxs-lookup"><span data-stu-id="55b29-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="55b29-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55b29-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="55b29-123">Silverlight 플레이어</span><span class="sxs-lookup"><span data-stu-id="55b29-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="55b29-124">모니터링</span><span class="sxs-lookup"><span data-stu-id="55b29-124">Monitoring</span></span>
[<span data-ttu-id="55b29-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="55b29-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="55b29-126">PlayReady 토큰</span><span class="sxs-lookup"><span data-stu-id="55b29-126">PlayReady with Token</span></span>
[<span data-ttu-id="55b29-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55b29-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="55b29-128">DASH 플레이어</span><span class="sxs-lookup"><span data-stu-id="55b29-128">DASH Players</span></span>
[<span data-ttu-id="55b29-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="55b29-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="55b29-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="55b29-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="55b29-131">기타</span><span class="sxs-lookup"><span data-stu-id="55b29-131">Other</span></span>
<span data-ttu-id="55b29-132">다음을 이용하여 HLS URL을 테스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55b29-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="55b29-133">**Safari** 또는</span><span class="sxs-lookup"><span data-stu-id="55b29-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="55b29-134">**3ivx HLS 플레이어** </span><span class="sxs-lookup"><span data-stu-id="55b29-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="55b29-135">비디오 플레이어 개발</span><span class="sxs-lookup"><span data-stu-id="55b29-135">Developing video players</span></span>
<span data-ttu-id="55b29-136">사용자 고유의 플레이어를 개발하는 방법에 대한 자세한 내용은 [비디오 플레이어 개발](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="55b29-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="55b29-137">미디어 서비스 학습 경로</span><span class="sxs-lookup"><span data-stu-id="55b29-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="55b29-138">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="55b29-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
