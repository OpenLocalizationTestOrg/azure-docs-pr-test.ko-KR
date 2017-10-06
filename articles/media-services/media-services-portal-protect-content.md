---
title: "aaaConfiguring 콘텐츠 보호 정책을 사용 하 여 hello Azure 포털 | Microsoft Docs"
description: "이 문서에서는 방법을 toouse hello Azure 포털 tooconfigure 콘텐츠 보호 정책 보여줍니다. hello 표시 방법을 문서도 tooenable 자산에 대 한 동적 암호화."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 콘텐츠 보호 정책 구성
> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. 자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
> 
> 

## <a name="overview"></a>개요
Microsoft Azure 미디어 서비스 AMS ()를 사용 하면 toosecure 하면 미디어를 저장, 처리 및 배달을 통해 컴퓨터를 벗어나 hello 시간. 미디어 서비스에서는 toodeliver 내용을 동적으로 AES로 암호화 된 고급 암호화 표준 () (128 비트 암호화 키 사용), PlayReady 및/또는 Widevine DRM 및 Apple FairPlay를 사용 하 여 일반 암호화 (CENC). 

AMS DRM 라이선스 배달용 서비스를 제공 하 고 AES 키 tooauthorized 클라이언트를 취소 합니다. hello Azure 포털을 통해 있습니다 하나 toocreate **권한 부여 정책 키/라이선스** 모든 유형의 암호화 합니다.

이 문서에서는 tooconfigure hello Azure 포털을 사용 하 여 보호 정책을 콘텐츠 하는 방법을 보여줍니다. hello 표시 방법을 문서도 tooapply 동적 암호화 tooyour 자산입니다.


> [!NOTE]
> Hello 정책 hello Azure 클래식 포털 toocreate 보호 정책을 사용 하는 경우 hello에 나타나지 않을 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 그러나 오래 된 모든 hello 정책을 여전히 존재 합니다. 검사할 수 있습니다 Azure 미디어 서비스.NET SDK 또는 hello hello를 사용 하 여 [미디어 서비스 탐색기 Azure](https://github.com/Azure/Azure-Media-Services-Explorer/releases) 도구 (toosee hello 정책 hello 자산에 대해 마우스 오른쪽 단추로 클릭-> 디스플레이 탭 콘텐츠 키에 대해-> (F4) 정보 키를 누르거나 hello). 
> 
> 새 정책을 사용 하 여 자산 tooencrypt 하려는 경우 Azure 포털 hello로 구성 저장을 클릭 한 동적 암호화를 다시 적용 합니다. 
> 
> 

## <a name="start-configuring-content-protection"></a>콘텐츠 보호 구성 시작
콘텐츠 보호, 글로벌 tooyour AMS 계정 구성 toouse hello 포털 toostart 다음 hello지 않습니다.

1. Hello에 [Azure 포털](https://portal.azure.com/)를 Azure 미디어 서비스 계정을 선택 합니다.
2. **설정** > **Content Protection**을 선택합니다.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>키/라이선스 권한 부여 정책
AMS는 키 또는 라이선스를 요청하는 사용자를 인증하는 여러 방법을 지원합니다. hello 콘텐츠 키 인증 정책은 구성 하 고 클라이언트 hello 키/라이선스 toobe delived toohello 클라이언트 하려면에서 충족 해야 합니다. hello 콘텐츠 키 인증 정책이 있을 수 하나 이상의 권한 부여 제한을: **열고** 또는 **토큰** 제한 합니다.

hello Azure 포털을 통해 있습니다 하나 toocreate **권한 부여 정책 키/라이선스** 모든 유형의 암호화 합니다.

### <a name="open"></a>열기
개방형 제한 의미 hello 시스템 키를 요청 하는 hello 키 tooanyone를 제공 합니다. 이 제한은 테스트 목적으로 유용할 수 있습니다. 

### <a name="token"></a>위임
보안 토큰 서비스 (STS)에서 발급 한 토큰 hello 토큰 제한 정책은 함께 제공 해야 합니다. 미디어 서비스는 hello 단순 웹 토큰 (SWT) 형식 및 JSON 웹 토큰 (JWT) 형식 토큰을 지원합니다. 미디어 서비스는 보안 토큰 서비스를 제공하지 않습니다. 사용자 지정 STS를 만들거나 Microsoft Azure ACS tooissue 토큰을 활용할 수 있습니다. hello STS 구성된 toocreate 지정 hello로 토큰에 서명 해야 합니다. 키 클레임을 발급 hello 토큰 제한 구성에 지정 합니다. hello 미디어 서비스 키 배달 서비스는 hello 요청한 키 (또는 라이선스) toohello 클라이언트 hello 토큰이 유효한 경우 및 hello 반환 hello 토큰 일치 항목에 구성 된 hello 키 (또는 라이선스)에 대 한 클레임입니다.

토큰 제한 정책 hello를 구성할 때 hello 기본 확인 키, 발급자 및 대상 매개 변수를 지정 해야 합니다. hello hello 기본 확인 키가 포함 되어 hello 토큰이 서명, 발급자 hello 보안 토큰 서비스 hello 토큰을 발급 하는 키입니다. hello 리소스 hello 토큰에 대 한 액세스 권한을 부여 또는 hello audience (범위 라고도 함) hello 토큰의 hello 의도 설명 합니다. hello 미디어 서비스 키 배달 서비스는 hello 토큰의 이러한 값 hello 템플릿에서 hello 값과 일치 하는지 확인 합니다.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>PlayReady 권한 템플릿
Hello PlayReady 권한 서식 파일에 대 한 자세한 내용은 참조 하십시오. [미디어 서비스 PlayReady 라이선스 템플릿 개요](media-services-playready-license-template-overview.md)합니다.

### <a name="non-persistent"></a>영구적
비 영구적인로 라이선스를 구성 하는 경우 hello 플레이어 hello 라이선스를 사용 하는 동안 메모리에 보관만 됩니다.  

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>영구적
영구적으로 hello 라이선스를 구성 하는 경우 영구 저장소에 클라이언트 hello에 저장 됩니다.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Widevine 권한 템플릿
Widevine 권한 템플릿 hello에 대 한 자세한 내용은 참조 하십시오. [Widevine 라이선스 템플릿 개요](media-services-widevine-license-template-overview.md)합니다.

### <a name="basic"></a>Basic
선택 하는 경우 **기본**, 모든 값이 기본값 된 hello 서식 파일 생성 됩니다.

### <a name="advanced"></a>고급
Widevine 구성의 고급 옵션에 대한 자세한 내용은 [이](media-services-widevine-license-template-overview.md) 토픽을 참조하십시오.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>FairPlay 구성
tooenable FairPlay 암호화 hello FairPlay 구성 옵션을 통해 tooprovide hello 앱 인증서 및 응용 프로그램 암호 키 (ASK) 필요. FairPlay 구성 및 요구 사항에 대한 자세한 내용은 [이](media-services-protect-hls-with-fairplay.md) 문서를 참조하십시오.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>동적 암호화 tooyour 자산 적용
tootake 이점은 동적 암호화 해야 tooencode 소스 파일의 적응 비트 전송률 MP4 파일 집합입니다.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>자산 tooencrypt 않겠다고 선택
모든 자산을 선택 하는 toosee **설정** > **자산**합니다.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>AES 또는 DRM으로 암호화
자산에서 **암호화**를 누르면 **AES** 또는 **DRM**의 두 가지 선택 사항이 표시됩니다. 

#### <a name="aes"></a>AES
부드러운 스트리밍, HLS 및 MPEG-DASH의 모든 스트리밍 프로토콜에서 AES 암호화되지 않은 키 암호화를 사용합니다.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Hello DRM 탭을 선택 하면 콘텐츠 보호 정책의 다른 옵션과 함께 제공 됩니다 (있음 구성한 경우 이제) + 스트리밍 프로토콜의 집합입니다.

* **MPEG-DASH를 사용하는 PlayReady 및 Widevine** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다.
* **MPEG-DASH를 사용하는 PlayReady 및 Widevine + HLS를 사용하는 FairPlay** - PlayReady 및 Widevine DRM의 MPEG-DASH 스트림을 동적으로 암호화합니다. 또한 FairPlay의 HLS 스트림도 암호화합니다.
* **부드러운 스트리밍, HLS 및 MPEG-DASH만 사용하는 PlayReady** - PlayReady DRM의 부드러운 스트리밍, HLS, MPEG-DASH 스트림을 동적으로 암호화합니다.
* **MPEG-DASH만 사용하는 Widevine** - Widevine DRM의 MPEG-DASH를 동적으로 암호화합니다.
* **HLS만 사용하는 FairPlay** - FairPlay의 HLS 스트림을 동적으로 암호화합니다.

tooenable FairPlay 암호화 hello hello 콘텐츠 보호 설정 블레이드의 FairPlay 구성 옵션을 통해 tooprovide hello 앱 인증서 및 응용 프로그램 암호 키 (ASK) 필요.

![콘텐츠 보호](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Hello 암호화 선택 하면 키를 눌러 **적용**합니다.

>[!NOTE] 
>AES 암호화 safari에서는 HLS tooplay 계획인 경우, 참조 [이 블로그](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/)합니다.

## <a name="next-steps"></a>다음 단계
Media Services 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

