---
title: "aaaProtect Azure 미디어 서비스를 사용 하 여 콘텐츠 | Microsoft Docs"
description: "이 기사는 미디어 서비스 콘텐츠 보호에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>콘텐츠 보호 개요
Microsoft Azure 미디어 서비스 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간을 수 있습니다. 미디어 서비스에서는 라이브 및 주문형 콘텐츠에 사용 하 여 동적으로 암호화 toodeliver 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 또는 hello 주요 DRMs: Microsoft PlayReady, Google Widevine 및 Apple FairPlay 합니다. 또한 미디어 서비스 AES 키 배달용 서비스를 제공 하 고 DRM (PlayReady, Widevine, 및 FairPlay) tooauthorized 클라이언트 라이선스 키를 누릅니다. 

다음 이미지는 hello AMS 지원 hello 콘텐츠 보호 워크플로 보여 줍니다. 

![PlayReady로 보호](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화 하면 콘텐츠 및 take 장점이 스트리밍 toostart hello toostream 콘텐츠 hello toobe에 들어 있는 스트리밍 끝점 **실행** 상태입니다. 

이 항목에서는 설명 [개념 및 용어](media-services-content-protection-overview.md) 관련 toounderstanding AMS로 내용을 보호 합니다. hello 항목에 포함 되어 [링크](media-services-content-protection-overview.md#common-scenarios) 방법을 tooachieve 콘텐츠 보호 작업을 보여 주는 tootopics 합니다. 

## <a name="dynamic-encryption"></a>동적 암호화
Microsoft Azure 미디어 서비스 사용 하면 콘텐츠 지우기 키 AES 또는 DRM 암호화를 사용 하 여 동적으로 암호화 toodeliver: Microsoft PlayReady, Google Widevine 및 Apple FairPlay 합니다.

현재 다음 스트리밍 형식 hello를 암호화할 수 있습니다: HLS, MPEG DASH, 부드러운 스트리밍 및 합니다. 점진적 다운로드를 암호화할 수 없습니다.

에 대해 원하는 tooencrypt 미디어 서비스 자산, 자산을 사용 하 여 암호화 키 (CommonEncryption 또는 EnvelopeEncryption) tooassociate 필요한 고 hello 키에 대 한 권한 부여 정책을 구성할 수도 있습니다.

Tooconfigure hello 자산의 배달 정책을 해야합니다. Toostream 저장소 암호화 된 자산을 확인 방법을 있는지 toospecify toodeliver 자산 배달 정책을 구성 하 여 것입니다.

미디어 서비스는 지정 된 hello 플레이어에서 스트림을 요청 되 면 키 toodynamically 지우기 키 AES를 사용 하 여 콘텐츠 또는 DRM 암호화를 암호화 합니다. toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다. hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.


## <a name="storage-encryption"></a>저장소 암호화
저장소 암호화 tooencrypt AES 256 비트 암호화를 사용 하 여 로컬로 되어 있지 않은 콘텐츠를 사용 하 고 암호화 된 상태로 저장 된 저장소 tooAzure 업로드 합니다. 자동으로 저장소 암호화로 보호 되는 자산 암호화 되지 않은 하 고 암호화 된 파일 시스템 이전 tooencoding 및 새 출력 자산으로 다시 다시 암호화 필요에 따라 이전 toouploading에 배치 됩니다. 강력한 암호화를 사용 하 여 고품질 입력된 미디어 파일 디스크에 놓으면 toosecure를 원하는 때 저장소 암호화에 대 한 기본 사용 사례 hello 표시 합니다.

순서 toodeliver 저장소 암호화 된 자산을 원하는 toodeliver 콘텐츠 미디어 서비스에서 알 수 있도록 hello 자산의 배달 정책을 구성 해야 합니다. 자산을 스트리밍하기 전에 스트리밍 서버 제거 hello 저장소 암호화 및 스트림을 hello를 사용 하 여 콘텐츠 hello 배달 정책 (예: AES, 일반 암호화 또는 암호화 안 함)를 지정 합니다.

## <a name="common-encryption-cenc"></a>CENC(일반 암호화)
일반 암호화는 PlayReady 또는/및 Widewine으로 콘텐츠를 암호화하는 경우에 사용합니다.

## <a name="using-cbcs-aapl-encryption"></a>cbcs-aapl 암호화 사용
cbcs-aapl은 FairPlay로 콘텐츠를 암호화하는 경우 사용합니다.

## <a name="envelope-encryption"></a>봉투 암호화
원하는 tooprotect 콘텐츠 aes-128 암호화 되지 않은 키와이 옵션을 사용 합니다. 보다 안전한 옵션을 사용 하도록 하려는 경우이 항목에 나열 된 hello DRMs 중 하나를 선택 합니다. 

## <a name="licenses-and-keys-delivery-service"></a>라이선스 및 키 배달 서비스
미디어 서비스는 DRM (PlayReady, Widevine, FairPlay) 라이선스 배달용 서비스를 제공 하 고 AES 키 tooauthorized 클라이언트를 취소 합니다. 사용할 수 있습니다 [Azure 포털 hello](media-services-portal-protect-content.md), REST API 또는 Media Services SDK for.NET 라이선스 및 키에 대 한 권한 부여 및 인증 정책 tooconfigure 합니다.

## <a name="token-restriction"></a>토큰 제한
hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: 열거나 토큰 제한 합니다. 보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다. 미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다. 미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다. 사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다. hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다. hello 미디어 서비스 키 배달 서비스는 hello 요청한 키 (또는 라이선스) toohello 클라이언트 hello 토큰이 유효한 경우 및 hello 반환 hello 토큰 일치 항목에 구성 된 hello 키 (또는 라이선스)에 대 한 클레임입니다.

토큰 제한 정책 hello를 구성할 때 hello 기본 확인 키, 발급자 및 대상 매개 변수를 지정 해야 합니다. hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다. hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다. hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.

## <a name="streaming-urls"></a>스트리밍 URL
Hello 스트리밍 URL에에서는 암호화 태그를 사용 해야 둘 이상의 DRM으로 자산 암호화 된 경우: (형식 ='m3u8-aapl' 암호화 'xxx' =) 합니다.

hello 고려 사항에 따라 적용 됩니다.

* 1개 이하의 암호화 형식만 지정할 수 있습니다.
* 암호화 유형 toobe 한 암호화가 적용 된 toohello 자산만 hello url에 지정 되어 있지 않습니다.
* 암호화 형식은 대/소문자를 구분하지 않습니다.
* hello 다음 암호화 종류를 지정할 수 있습니다.  
  * **cenc**: 일반 암호화(Playready 또는 Widevine)
  * **cbcs-aapl**: Fairplay
  * **cbc**: AES 봉투 암호화

## <a name="common-scenarios"></a>일반적인 시나리오
hello 다음 항목에서는 설명 AMS 키/라이선스 배달 서비스를 사용 하 여 저장소의 tooprotect 콘텐츠 스트리밍 미디어를 동적으로 암호화를 제공 하는 방법

* [AES로 보호](media-services-protect-with-aes128.md) 
* [PlayReady 및/또는 Widevine으로 보호 ](media-services-protect-with-drm.md)
* [Apple FairPlay 및/또는 PlayReady로 보호되는 HLS 콘텐츠 스트림](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>추가 시나리오
* [암호기/스트리밍 서버와 함께 toointegrate Azure PlayReady 라이선스 서비스 어떻게](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server)합니다.
* [CastLabs toodeliver DRM 라이선스 tooAzure 미디어 서비스를 사용 하 여](media-services-castlabs-integration.md)

>[!NOTE]
>외부 DRM 서버(기술)를 사용하고 AMS에서 스트리밍하는 시나리오는 현재 지원되지 않습니다.


## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure 미디어 서비스를 사용하여 AES 동적 암호화로 PlayReady 발표](http://mingfeiy.com/playready)

[Azure 미디어 서비스 PlayReady 라이선스 배달 가격 설명](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Aes toodebug Azure 미디어 서비스에서 스트림으로 암호화 하는 방법](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[JWT 토큰 인증을 참조하세요.](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Azure Active Directory와 Azure 미디어 서비스 OWIN MVC 기반 앱을 Azure Active Directory와 통합하고 JWT 클레임을 기반으로 하는 콘텐츠 키 배달을 제한합니다](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Azure ACS tooissue 토큰을 사용 하 여](http://mingfeiy.com/acs-with-key-services)합니다.

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
