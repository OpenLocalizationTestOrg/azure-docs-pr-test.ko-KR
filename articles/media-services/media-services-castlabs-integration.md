---
title: "aaaUsing castLabs toodeliver Widevine 라이선스 tooAzure 미디어 서비스 | Microsoft Docs"
description: "이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다. 미디어 서비스 PlayReady 라이선스 서버에서 가져온 hello PlayReady 라이선스 및 Widevine 라이선스 castLabs 라이선스 서버에 의해 전달 됩니다."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>CastLabs toodeliver Widevine 라이선스 tooAzure 미디어 서비스를 사용 하 여
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>개요
이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다. Widevine 라이선스에서 제공 하 고 hello PlayReady 라이선스 미디어 서비스 PlayReady 라이선스 서버에서 가져오는데 **castLabs** 라이선스 서버.

보호 된 콘텐츠 스트리밍 tooplayback CENC (PlayReady 및/또는 Widevine), 여는 데 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다. 자세한 내용은 [AMP 문서](http://amp.azure.net/libs/amp/latest/docs/) 를 참조하십시오.

다음 다이어그램 hello 높은 수준의 Azure 미디어 서비스 및 castLabs 통합 아키텍처를 보여 줍니다.

![통합](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>일반적인 시스템 설정
* 미디어 콘텐츠는 AMS에 저장됩니다.
* 콘텐츠 키의 키 ID는 castLabs 및 AMS에 저장됩니다.
* castLabs 및 AMS에는 모두 내장된 토큰 인증이 있습니다. 다음 섹션 hello 인증 토큰에 설명 합니다. 
* Hello 콘텐츠가 동적으로 암호화 된 클라이언트 toostream hello 비디오를 요청 하면 **일반 암호화** (CENC) 및 스트리밍 및 DASH AMS tooSmooth 하 여 동적으로 패키지 합니다. HLS 스트리밍 프로토콜에 대한 PlayReady M2TS 기본 스트림 암호화를 전달할 수도 있습니다.
* PlayReady 라이선스는 AMS 라이선스 서버에서 검색되고 Widevine 라이선스는 castLabs 라이선스 서버에서 검색됩니다. 
* 미디어 플레이어는 어떤 라이선스 toofetch hello 클라이언트 플랫폼 기능에 따라 자동으로 결정 합니다. 

## <a name="authentication-token-generation-for-getting-a-license"></a>라이선스를 가져오기 위한 인증 토큰 생성
CastLabs 및 AMS 둘 다 사용 하는 토큰 형식을 tooauthorize 라이선스 JWT (JSON 웹 토큰)를 지원합니다. 

### <a name="jwt-token-in-ams"></a>AMS의 JWT 토큰
다음 표에서 hello AMS에서 JWT 토큰을 설명 합니다. 

| 발급자 | 발급자 문자열 hello에서 선택한 서비스 STS (보안 토큰) |
| --- | --- |
| 대상 |STS를 사용 하는 hello에서 대상 그룹 문자열 |
| 클레임 |클레임 집합 |
| NotBefore |Hello 토큰의 유효성을 검사를 시작 합니다. |
| 만료 |Hello 토큰의 끝 유효성 |
| SigningCredentials |라이선스 서버 및 STS를 castLabs PlayReady 라이선스 서버 간에 공유 되는 hello 키 대칭 또는 비대칭 키 수 있습니다. |

### <a name="jwt-token-in-castlabs"></a>castLabs의 JWT 토큰
다음 표에서 hello castLabs에서 JWT 토큰을 설명 합니다. 

| 이름 | 설명 |
| --- | --- |
| optData |사용자에 대한 정보가 포함된 JSON 문자열. |
| crt |JSON 문자열 대 한 정보가 들어 hello 자산, 라이선스 정보 및 재생 권한을 합니다. |
| iat |hello epoch의 현재 datetime입니다. |
| jti |(모든 토큰 수 번만 사용할 hello castLabs 시스템에서)이이 토큰에 대 한 고유 식별자입니다. |

## <a name="sample-solution-set-up"></a>샘플 솔루션 설정
hello [샘플 솔루션](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) 두 개의 프로젝트로 구성 됩니다.

* PlayReady 및 Widevine 모두에 대해 이미 수집 된 자산에 사용 되는 tooset DRM 제한 될 수 있는 콘솔 앱입니다.
* 토큰을 배포하는 웹 응용 프로그램. STS의 간소화된 버전으로 볼 수 있습니다.

toouse hello 콘솔 응용 프로그램:

1. Hello app.config toosetup AMS 자격 증명, castLabs 자격 증명, STS 구성 및 공유 키를 변경 합니다.
2. AMS에 자산을 업로드합니다.
3. Get hello UUID hello에서 자산을 업로드 하 고 hello Program.cs 파일의 선을 32를 변경 합니다.
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Hello castLabs 시스템 (hello Program.cs 파일의 선을 44) hello 자산에는 AssetId를 사용 하십시오.
   
   에 대 한 AssetId 설정 해야 **castLabs**; toobe 고유한 영숫자 문자열 필요 합니다.
5. Hello 프로그램을 실행 합니다.

toouse hello 웹 응용 프로그램 (STS):

1. 변경 hello web.config toosetup castlabs merchant ID, STS 구성 hello 및 hello 공유 키.
2. TooAzure 웹 사이트를 배포 합니다.
3. Toohello 웹 사이트를 이동 합니다.

## <a name="playing-back-a-video"></a>비디오 재생
hello를 사용할 수 있습니다, tooplayback (PlayReady 및/또는 Widevine) 일반 암호화를 사용 하 여 암호화 된 비디오 [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다. Hello 콘솔 응용 프로그램을 실행할 때 hello 콘텐츠 키 ID 및 URL 매니페스트 hello 표시 됩니다.

1. 새 탭을 열고 STS를 시작합니다(http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid]).
2. 너무 이동[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)합니다.
3. 스트리밍 URL hello에 붙여 넣습니다.
4. Hello 클릭 **고급 옵션** 확인란을 선택 합니다.
5. Hello에 **보호** 드롭다운에서 PlayReady 및/또는 Widevine 선택 합니다.
6. Hello 토큰 텍스트 상자에 STS에서 가져온 hello 토큰을 붙여 넣습니다. 
   
   hello castLab 라이선스 서버는 hello 않아도 "전달자 =" hello 토큰 앞에 접두사입니다. 따라서 하는 hello 토큰을 제출 하기 전에 제거 하세요.
7. Hello 플레이어를 업데이트 합니다.
8. hello 비디오를 수행 해야 합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

