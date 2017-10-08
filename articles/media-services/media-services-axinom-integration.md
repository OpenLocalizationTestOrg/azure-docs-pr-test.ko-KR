---
title: "aaaUsing Axinom toodeliver Widevine 라이선스 tooAzure 미디어 서비스 | Microsoft Docs"
description: "이 문서에서는 Azure 미디어 서비스 (AMS) toodeliver PlayReady와 Widevine DRMs AMS 하 여 동적으로 암호화 된 스트림을 사용 하는 방법을 설명 합니다. 미디어 서비스 PlayReady 라이선스 서버에서 가져온 hello PlayReady 라이선스 및 Widevine 라이선스 Axinom 라이선스 서버에 의해 전달 됩니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Axinom toodeliver Widevine 라이선스 tooAzure 미디어 서비스를 사용 하 여
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>개요
Azure 미디어 서비스(AMS)에 Google Widevine 동적 보호가 추가되었습니다(자세한 내용은 [Mingfei의 블로그](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) 참조). 또한 Azure 미디어 플레이어(AMP)에도 Widevine 지원이 추가되었습니다(자세한 내용은 [AMP 문서](http://amp.azure.net/libs/amp/latest/docs/) 참조). 이는 MSE 및 EME가 포함된 현대식 브라우저에 대한 다중 원시 DRM(PlayReady 및 Widevine)를 가진 CENC로 보호되는 DASH 콘텐츠 합리화의 주요 성과입니다.

미디어 서비스.NET SDK 버전 3.5.2 hello 부터는 미디어 서비스 있습니다 tooconfigure Widevine 라이선스 템플릿을 통해 하 고 Widevine 라이선스 가져오기. Widevine 라이선스를 배달 AMS 파트너 toohelp 다음 hello을 사용할 수 있습니다: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/)합니다.

이 문서에서는 toointegrate 및 테스트 Widevine 라이선스 Axinom에서 관리 하는 서버에 방법을 설명 합니다. 구체적으로 다음 사항을 다룹니다.  

* 해당 라이선스 취득 URL이 포함된 다중-DRM(PlayReady 및 Widevine)을 사용하여 동적 일반 암호화 구성;
* 순서 toomeet hello 라이선스 서버 요구 사항;에 JWT 토큰을 생성합니다.
* JWT 토큰 인증으로 라이선스 취득을 처리하는 Azure 미디어 플레이어 앱 개발;

전체 시스템 hello 및 hello 흐름의 콘텐츠 키, 키 ID, 키 시드, JTW 토큰 및 해당 클레임 hello 다이어그램을 다음으로 가장 잘 나타낼 수 있습니다.

![대시 및 CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>콘텐츠 보호
동적 보호 및 키 배달 정책 구성에 대 한 Mingfei의 블로그를 참조 하십시오: [어떻게 Azure 미디어 서비스로 tooconfigure Widevine 패키징](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)합니다.

대시 hello 다음의 두는 것을 스트리밍에 대 한 다중 DRM으로 동적 CENC 보호를 구성할 수 있습니다.

1. 토큰 인증 제한이 포함될 수 있는 MS Edge 및 IE11에 대한 PlayReady 보호. 토큰 제한 정책 hello STS에서 발급 한 보안 토큰 서비스 (), 예: Azure Active Directory; 토큰에 의해 수반 되어야 합니다.
2. Chrome에 대한 Widevine 보호의 경우 다른 STS가 발급한 토큰을 이용한 토큰 인증이 필요할 수 있습니다. 

Azure Active Directory를 Axinom의 Widevine 라이선스 서버에 대한 STS로 사용할 수 없는 이유는 [JWT 토큰 생성](media-services-axinom-integration.md#jwt-token-generation) 을 참조하세요.

### <a name="considerations"></a>고려 사항
1. Axinom 키 배달 서비스를 구성 하기 위한 키 시드 (8888000000000000000000000000000000000000) 및 선택 되거나 생성 된 키 ID toogenerate hello 콘텐츠 키를 지정 하는 hello를 사용 해야 합니다. Axinom 라이선스 서버는 기반으로 하는 콘텐츠 키가 포함 된 모든 라이선스를 발급 하는 hello에 같은 키 초기값으로, 테스트 및 프로덕션에 유효 합니다.
2. 테스트를 위해 hello Widevine 라이선스 취득 URL: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense)합니다. HTTP 및 HTTS 모두 허용됩니다.

## <a name="azure-media-player-preparation"></a>Azure 미디어 플레이어 준비
AMP v1.4.0은 PlayReady와 Widevine DRM 둘 다를 사용하여 동적으로 패키징된 AMS 콘텐츠의 재생을 지원합니다.
Widevine 라이선스 서버 토큰 인증을 요구 하지는 없는 경우 추가 Widevine 여 toodo tootest 대시 콘텐츠 보호 해야 합니다. 예를 들어 hello AMP 팀 제공 단순 [샘플](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html)여기서 가장자리와 PlayReady로 IE11 Widevine와 Chrome에서 작동 볼 수 있습니다.
Axinom에서 제공 하는 hello Widevine 라이선스 서버에는 JWT 토큰 인증이 필요 합니다. hello JWT 토큰에는 HTTP 헤더 "X AxDRM 메시지"를 통해 라이선스 요청과 함께 전송 toobe가 필요 합니다. 이 위해 tooadd hello hello 원본 설정 하기 전에 AMP 호스팅 hello 웹 페이지에서 javascript를 수행 해야 합니다.

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

AMP 코드의 나머지 부분 hello는 AMP 문서 처럼 표준 AMP API [여기](http://amp.azure.net/libs/amp/latest/docs/)합니다.

사용자 지정 권한 부여 헤더는 여전히 AMP 장기 접근법 해제 되는 hello 공식 하기 전에 단기 접근 방식을 설정에 대 한 javascript 위에 해당 hello를 note 합니다.

## <a name="jwt-token-generation"></a>JWT 토큰 생성
테스트용 Axinom Widevine 라이선스 서버에는 JWT 토큰 인증이 필요합니다. 또한 기본 데이터 형식 대신 복잡 한 개체 유형의 hello JWT 토큰의 hello 클레임 중 하나입니다.

아쉽게도 Azure AD는 기본 형식의 JWT 토큰만 발급할 수 있습니다. 마찬가지로,.NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler 및 JwtPayload)만 있습니다 tooinput 복잡 한 개체 유형을 클레임으로 합니다. 그러나 hello 클레임을 여전히 문자열로 serialize 합니다. 따라서 것을 사용할 수 없습니다 두 hello Widevine 라이선스 요청에 대 한 생성 hello JWT 토큰에 대 한 합니다.

이한일은 Sheehan [JWT Nuget 패키지](https://www.nuget.org/packages/JWT) 하겠습니다 toouse이 Nuget 패키지 되므로 충족 hello 요구 합니다.

다음은 hello로 생성 JWT 토큰에 대 한 hello 코드 Axinom Widevine 라이선스 서버에서 필요에 따라 클레임을 테스트에 필요한입니다.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

Axinom Widevine 라이선스 서버

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>고려 사항
1. AMS PlayReady 라이선스 배달 서비스의 경우 인증 토큰 앞에 “Bearer=”가 필요하지만, Axinom Widevine 라이선스 서버는 이를 사용하지 않습니다.
2. hello Axinom 통신 키 서명 키로 사용 됩니다. 하지만 인코딩할 때 일련의 바이트 문자열이 아닌으로 처리 되어야 해당 hello 키는 16 진수 문자열을 note 합니다. 이 hello 메서드 ConvertHexStringToByteArray 여 달성 됩니다.

## <a name="retrieving-key-id"></a>키 ID 검색
JWT 생성을 위한 hello 코드 토큰, 키 ID는 필요한 것을 알 수 있습니다. Hello JWT 토큰 요구 toobe 준비 AMP 플레이어를 로드 하기 전에, 이후 toobe에서 검색 하는 핵심 ID 요구 toogenerate JWT 토큰을 정렬 합니다.

키의 다양 tooget 보유 하는 과정의 id. 예를 들어 키 ID를 콘텐츠 메타데이터와 함께 데이터베이스에 저장할 수 있습니다. 또는 DASH MPD(미디어 프레젠테이션 설명) 파일에서 키 ID를 검색할 수 있습니다. 아래 hello 코드 hello 후자입니다.

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a>요약
Azure 미디어 서비스 콘텐츠 보호와 Azure Media Player에서 지원 Widevine의 가장 최근에 추가 된 수는 tooimplement 대시의 스트리밍 + native-DRM (PlayReady + Widevine) AMS 및 Widevine 라이선스에 모두 PlayReady 라이선스 서비스 사용 Axinom 최신 브라우저를 수행 하는 hello에 대 한 서버:

* Chrome
* Windows 10용 Microsoft Edge
* Windows 8.1 및 Windows 10용 IE 11
* (데스크톱) Firefox 및 Safari (iOS) Mac에서 모두 Silverlight를 통해 지원 되 고 Azure 미디어 플레이어와 같은 URL hello

hello 다음 매개 변수가 필요 hello 미니 솔루션 활용 Axinom Widevine 라이선스 서버에 있습니다. 키를 제외 하 고 ID, hello 나머지 매개 변수 Axinom Widevine 서버 설치에 따라 제공 됩니다.

| 매개 변수 | 사용 방법 |
| --- | --- |
| 통신 키 ID |Com_key_id"hello 클레임" JWT 토큰에서의 값으로 포함 되어야 합니다 (참조 [이](media-services-axinom-integration.md#jwt-token-generation) 섹션). |
| 통신 키 |JWT 토큰의 서명 키 hello 사용 되어야 합니다 (참조 [이](media-services-axinom-integration.md#jwt-token-generation) 섹션). |
| 키 시드 |사용 하 여 콘텐츠 키를 사용 하는 toogenerate 제공 해야 콘텐츠 키 ID (참조 [이](media-services-axinom-integration.md#content-protection) 섹션). |
| Widevine 라이선스 획득 URL |DASH 스트리밍에 대한 자산 배달 정책 구성에 사용해야 합니다([이](media-services-axinom-integration.md#content-protection) 섹션 참조). |
| 콘텐츠 키 ID |JWT 토큰의 권한 메시지 클레임의 hello 값의 일부분으로 포함 되어야 합니다 (참조 [이](media-services-axinom-integration.md#jwt-token-generation) 섹션). |

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>승인
이 문서를 만들 때 제공한 사람 다음 tooacknowledge hello 같은: Axinom의 Kristjan Jõgi, Mingfei Yan 및 Amit Rajput 합니다.

