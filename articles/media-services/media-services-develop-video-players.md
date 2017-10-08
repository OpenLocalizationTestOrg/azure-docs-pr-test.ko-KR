---
title: "aaaDevelop 비디오 플레이어 응용 프로그램"
description: "hello 항목 링크 tooPlayer 프레임 워크를 제공 하 고 플러그 인을 사용할 수 있는 toodevelop 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램입니다."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>비디오 플레이어 응용 프로그램 개발
## <a name="overview"></a>개요
Azure 미디어 서비스는 hello 도구 toocreate rich 필요 등 대부분의 플랫폼에 대 한 동적 클라이언트 플레이어 응용 프로그램: iOS 장치, Android 장치, Windows, Windows Phone, Xbox 및 셋톱 상자입니다. 또한이 항목 링크 tooSDKs 및 사용할 수 있는 toodevelop Azure 미디어 서비스에서 스트리밍 미디어를 사용할 수 있는 클라이언트 응용 프로그램 플레이어 프레임 워크를 제공 합니다.

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 
 
## <a name="azure-media-player"></a>Azure 미디어 플레이어
[Azure Media Player](http://aka.ms/ampinfo) 웹 비디오 플레이어 기반 tooplay 백 미디어 콘텐츠 Microsoft Azure 미디어 서비스에서 다양 한 브라우저와 장치입니다. Azure 미디어 플레이어에서 HTML5, 미디어 원본 확장 (MSE) 및 암호화 된 미디어 확장 (EME) tooprovide 다양된 한 적응 스트리밍 환경 등의 업계 표준을 사용합니다. 이러한 표준을 장치 또는 브라우저에서 사용할 수 없는 경우, Azure 미디어 플레이어는 Flash 및 Silverlight를 대체 기술로 사용합니다. 개발자는 hello 재생 기술을 사용에 관계 없이 통합된 JavaScript 인터페이스 tooaccess Api 해야 합니다. 따라서 콘텐츠는 광범위 한 장치 및 추가 작업 없이 브라우저에서 재생 하는 Azure 미디어 서비스 toobe 제공할 수 있습니다.

Microsoft Azure 미디어 서비스 콘텐츠 toobe DASH, 부드러운 스트리밍 처리에 대 한 있으며 tooplay 형식 스트리밍을 HLS 콘텐츠를 백업 합니다. Azure 미디어 플레이어는 고려 이러한 다양 한 형식 및 자동으로 재생 hello hello 플랫폼/브라우저의 기능에 따라 최상의 링크 합니다. Microsoft Azure 미디어 서비스에서 PlayReady 암호화 또는 AES 128 비트 봉투 암호화로 자산의 동적 암호화를 사용할 수 있습니다. 적절하게 구성된 경우 Azure 미디어 플레이어를 사용하여 PlayReady의 및 AES 128 비트 암호화된 콘텐츠를 암호 해독할 수 있습니다. 

자세한 내용은 다음을 참조하세요.

* [Azure 미디어 플레이어](http://aka.ms/ampinfo)
* [Azure 미디어 플레이어 서비스 설명서](http://aka.ms/ampdocs) 
* [Azure 미디어 플레이어 시작 블로그](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Azure 미디어 플레이어에서 최신 hello로 toodate toostay 등록](http://aka.ms/ampsignup)
* [새로운 기능 요청, 아이디어, 사용자 의견 추가](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>플레이어 응용 프로그램을 만들기 위한 다른 도구
또한 다음 Sdk hello를 사용할 수 있습니다.

* [부드러운 스트리밍 클라이언트 SDK](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [부드러운 스트리밍 Windows 스토어 앱](media-services-build-smooth-streaming-apps.md)
* [Microsoft Media Platform: 플레이어 프레임워크](http://playerframework.codeplex.com/) 
* [HTML5 플레이어 프레임워크 설명서](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [OSMF용 Microsoft 부드러운 스트리밍 플러그인](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Microsoft® 부드러운 스트리밍 클라이언트 이식 키트 라이선스](http://aka.ms/sspk) 
* [XBOX 비디오 응용 프로그램 개발](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>광고
Windows 미디어 플랫폼 hello 통해 광고 삽입에 대 한 azure 미디어 서비스에서는: 플레이어 프레임 워크입니다. 광고를 지원하는 플레이어 프레임워크는 Windows 8, Silverlight, Windows Phone 8 및 iOS 장치에 사용할 수 있습니다. 각 플레이어 프레임 워크에는 방법을 보여 주는 샘플 코드가 포함 되어 tooimplement 플레이어 응용 프로그램입니다. 미디어에 삽입할 수 있는 서로 다른 세 종류의 광고가 있습니다.

선형-기본 비디오 hello 일시 중지 하는 전체 프레임 광고

비선형-hello 기본 비디오가 재생 되로 표시 되는 오버레이 광고, 일반적으로 로고나 기타 정적 이미지 hello 플레이어 내에 배치

동반-플레이어 hello 외부에서 표시 되는 광고

Hello 기본 비디오 타임 라인의 한 지점에서 광고를 배치할 수 있습니다. Ad 및 tooplay hello 하는 경우 hello 플레이어 알려야 광고 tooplay 합니다. 이 작업은 표준 XML 기반 파일 집합을 사용하여 수행됩니다. VAST(Video Ad Service Template), VMAP(Digital Video Multiple Ad Playlist), MAST(Media Abstract Sequencing Template) 및 VPAID(Digital Video Player Ad Interface Definition). VAST 파일 어떤 광고 toodisplay를 지정합니다. 시점을 지정 하는 VMAP 파일 tooplay 다양 한 광고 하 고 VAST XML을 포함 합니다. MAST 파일은 또한 VAST XML을 포함할 수 있는 다른 방법은 toosequence 광고입니다. VPAID 파일 hello 비디오 플레이어와 hello 광고 또는 광고 서버 간의 인터페이스를 정의합니다. 자세한 내용은 [광고 삽입](https://msdn.microsoft.com/library/dn387398.aspx)을 참조하세요.

라이브 스트리밍 비디오의 선택 캡션 및 광고 지원에 대한 정보는 [지원되는 선택 캡션 및 광고 삽입 표준](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad)을 참조하세요.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>참고 항목
[DASH.js를 사용하여 HTML5 응용 프로그램에 MPEG-DASH 적응 스트리밍 비디오 포함](media-services-embed-mpeg-dash-in-html5.md)

[GitHub dash.js 리포지토리](https://github.com/Dash-Industry-Forum/dash.js)

