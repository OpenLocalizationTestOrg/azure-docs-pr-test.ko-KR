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
# <a name="playing-your-content-with-existing-players"></a>기존 플레이어를 사용하여 콘텐츠 재생
Azure Media Services는 부드러운 스트리밍, HTTP 라이브 스트리밍 및 Mpeg-dash와 같은 여러 인기 있는 스트리밍 형식을 지원합니다. 이 항목에서는 사용할 수 있는 tootest 스트림을 tooexisting 플레이어입니다.

### <a name="hello-azure-portal-media-services-content-player"></a>hello Azure 포털 미디어 서비스 콘텐츠 플레이어
hello **Azure** 포털 콘텐츠 플레이어를 제공 합니다. 사용할 수 있는 tootest 비디오.

Hello 클릭 필요한 비디오 (가 있는지 확인 [게시](media-services-portal-publish.md)) hello 클릭 **재생** hello hello 포털 맨 아래에 단추입니다.

다음과 같은 몇 가지 고려 사항이 적용됩니다.

* hello **미디어 서비스 콘텐츠 플레이어** hello 기본 스트리밍 끝점에서에서 재생 합니다. Tooplay 기본값이 아닌 스트리밍 끝점에서 다른 플레이어를 사용 합니다. 예를 들어 [Azure 미디어 플레이어](http://amsplayer.azurewebsites.net/azuremediaplayer.html)를 사용합니다.

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Azure 미디어 플레이어
사용 하 여 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback hello 다음 형식 중 하나에서 콘텐츠 (지우기 또는 protected):

* 부드러운 스트리밍
* MPEG DASH
* HLS
* 프로그레시브 MP4

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>AES 암호화 토큰
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Silverlight 플레이어
#### <a name="monitoring"></a>모니터링
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady 토큰
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>DASH 플레이어
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>기타
tootest HLS Url을 사용할 수도 있습니다.

* **Safari** 또는
* **3ivx HLS 플레이어** 

## <a name="developing-video-players"></a>비디오 플레이어 개발
고유한 플레이어 참조 하는 toodevelop 방법에 대 한 내용은 [비디오 플레이어 개발](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
