---
title: "Azure 포털 hello aaaConfigure 콘텐츠 키 권한 부여 정책을 사용 하 여 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 콘텐츠 키에 대 한 권한 부여 정책."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>콘텐츠 키 인증 정책 구성
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>개요
Microsoft Azure 미디어 서비스 사용 하면 toodeliver MPEG DASH, 부드러운 스트리밍 및 HTTP 라이브 스트리밍 (HLS) 스트림에서 보호 된 암호화 표준 AES (고급) (128 비트 암호화 키 사용) 또는 [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS 있습니다 toodeliver DASH 스트림을 Widevine DRM을 사용 하 여 암호화를 통해 수도 있습니다. PlayReady 및 Widevine 모두 hello 일반 암호화 (ISO/IEC 23001-7 CENC) 사양 당 암호화 됩니다.

또한 미디어 서비스 제공는 **키/라이선스 배달 서비스** 있는 클라이언트에서 AES 키를 가져올 수 또는 PlayReady/Widevine 라이선스 tooplay 암호화 된 콘텐츠를 환영 합니다.

이 항목에서는 toouse Azure 포털 tooconfigure hello 콘텐츠 키 인증 정책을 hello 하는 방법을 보여 줍니다. hello 키를 나중에 사용할 수 toodynamically 콘텐츠를 암호화 합니다. 현재 수 암호화 하는 hello 스트리밍 형식 다음 참고: HLS, MPEG DASH, 부드러운 스트리밍 및 합니다. 점진적 다운로드를 암호화할 수 없습니다.

플레이어 toobe 동적 암호화를 설정 하는 스트림을 요청 하면 미디어 서비스 사용 하 여 구성 하는 hello 키 toodynamically AES 또는 DRM 암호화를 사용 하 여 콘텐츠를 암호화 합니다. toodecrypt hello 스트림 hello 플레이어 hello 키 배달 서비스에서 hello 키를 요청 합니다. hello 사용자가 아닌지 toodecide 권한이 tooget hello 키, hello 서비스 hello 키에 대해 지정한 hello 권한 부여 정책을 평가 합니다.

Toohave 여러 콘텐츠 키를 계획 하거나 toospecify 경우는 **키/라이선스 배달 서비스** hello 미디어 서비스 키 배달 서비스 이외의 URL 미디어 서비스.NET SDK 또는 REST Api를 사용 합니다.

[미디어 서비스 .NET SDK를 사용하여 콘텐츠 키 권한 부여 정책 구성](media-services-dotnet-configure-content-key-auth-policy.md)

[미디어 서비스 REST API를 사용하여 콘텐츠 키 권한 부여 정책 구성](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>다음과 같은 몇 가지 고려 사항이 적용됩니다.
* AMS 계정이 만들어질 때 한 **기본** 스트리밍 끝점에 hello tooyour 계정 추가 됩니다 **Stopped** 상태입니다. 동적 패키징 및 동적 암호화, 하려면 스트리밍 끝점, 콘텐츠 및 take 있다는 이점이 스트리밍 toostart hello에 대 한 toobe **실행** 상태입니다. 
* 사용자의 자산은 적응 비트 전송률 MP4 또는 적응 비트 전송률 부드러운 스트리밍 파일 집합을 포함해야 합니다. 자세한 내용은 [자산 인코딩](media-services-encode-asset.md)을 참조하세요.
* 키 배달 서비스 hello ContentKeyAuthorizationPolicy 및 관련된 개체 (정책 옵션 및 제한) 15 분 동안 캐시합니다.  ContentKeyAuthorizationPolicy 만들기 및 toouse "토큰" 제한을 지정 합니다. 그런 다음 테스트 한 hello 정책을 업데이트 하는 경우 너무 "열" 제한, hello 정책 스위치 toohello "열기" 버전의 hello 정책 하기 전에 약 15 분이 걸립니다.

## <a name="how-to-configure-hello-key-authorization-policy"></a>방법: hello 키 권한 부여 정책 구성
tooconfigure hello 키 인증 정책을 선택 hello **콘텐츠 보호** 페이지.

미디어 서비스는 키를 요청 하는 사용자를 인증 하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책을 점이 **열고**, **토큰**, 또는 **IP** 권한 부여 제한 (**IP** 로 구성할 수 있습니다 REST 또는.NET SDK)입니다.

### <a name="open-restriction"></a>열기 제한
hello **열고** 제한 의미 hello 시스템 키를 요청 하는 hello 키 tooanyone를 제공 합니다. 이 제한은 테스트 목적으로 유용할 수 있습니다.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>토큰 제한
toochoose hello 토큰 제한 정책을, 키를 눌러 hello **토큰** 단추입니다.

hello **토큰** 제한 되는 정책에서 발급 한 토큰 수반 해야는 **보안 토큰 서비스** (STS). 미디어 서비스는 hello에 토큰을 지원 **단순 웹 토큰** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) 형식 및 **JSON 웹 토큰** (JWT) 형식입니다. 자세한 내용은 [JWT 토큰 인증](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)(영문)을 참조하세요.

미디어 서비스는 **보안 토큰 서비스**를 제공하지 않습니다. 사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다. hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다. hello 미디어 서비스 키 배달 서비스는 hello 암호화 키 toohello 클라이언트 반환 hello 토큰은 유효 하 고 hello hello 토큰의 클레임이 일치 hello 콘텐츠 키에 대해 구성 된 경우. 자세한 내용은 참조 [사용 하 여 Azure ACS tooissue 토큰](http://mingfeiy.com/acs-with-key-services)합니다.

Hello를 구성할 때 **토큰** 제한 정책에 대 한 값을 설정 해야 **확인 키**, **발급자** 및 **audience**합니다. hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다. hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다. hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.

### <a name="playready"></a>PlayReady
사용 하 여 콘텐츠를 보호 하는 경우 **PlayReady**이며 다음 중 하나 toospecify 권한 부여 정책에는 hello PlayReady 라이선스 템플릿을 정의 하는 XML 문자열의 hello 작업 해야 합니다. 기본적으로 hello 정책에 따라 설정 됩니다.

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>비영구</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>허용</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate>

Hello를 클릭할 수 있는 **정책 xml을 가져올** 단추 및 toohello 정의 된 XML 스키마를 준수 한 다른 xml [여기](media-services-playready-license-template-overview.md)합니다.

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

