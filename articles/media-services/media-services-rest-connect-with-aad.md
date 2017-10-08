---
title: "Azure AD 인증 tooaccess REST 사용 하 여 Azure 미디어 서비스 API aaaUse | Microsoft Docs"
description: "Azure 미디어 서비스 API를 사용 하 여 Azure Active Directory 인증으로 tooaccess 놓으면 방법을 알아봅니다."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 114f7bdde3a8f5fe6189d712e05b6afdc8a8787a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-hello-azure-media-services-api-with-rest"></a>사용 하 여 Azure AD 인증 tooaccess hello Azure 미디어 서비스 REST API

hello Azure 미디어 서비스 팀은 Azure 미디어 서비스 액세스에 대 한 Azure Active Directory (Azure AD) 인증 지원을 출시 했습니다. 또한 미디어 서비스 액세스에 대 한 계획 toodeprecate Azure 액세스 제어 서비스 인증을 발표 했습니다. 모든 Azure 구독 및 모든 미디어 서비스 계정에 연결 된 tooan Azure AD 테 넌 트 이기 때문에 Azure AD 인증 지원 다양 한 보안 이점을 제공 합니다. 이 변경과 마이그레이션 (hello 미디어 서비스.NET SDK를 사용 하 여 앱에 대 한) 경우에 대 한 참조 hello 다음 블로그 게시물 및 항목:

- [Azure Media Services의 Azure AD 지원 및 Access Control 인증 중단 발표](https://azure.microsoft.com/blog/azure%20media%20service%20aad%20auth%20and%20acs%20deprecation)
- [Azure AD 인증을 사용하여 Azure Media Services API 액세스](media-services-use-aad-auth-to-access-ams-api.md)
- [Microsoft.NET을 사용 하 여 Azure AD 인증 tooaccess Azure 미디어 서비스 API를 사용 하 여](media-services-dotnet-get-started-with-aad.md)
- [Azure 포털 hello를 사용 하 여 Azure AD 인증 시작](media-services-portal-get-started-with-aad.md)

일부 고객 toodevelop hello 제약 조건 뒤에서 미디어 서비스 솔루션을 필요 합니다.

*   Microsoft.NET 또는 C# 프로그래밍 언어를 사용 또는 사용할 수 없는 Windows hello 런타임 환경입니다.
*   Active Directory 인증 라이브러리와 같은 azure AD 라이브러리 hello 프로그래밍 언어에 대해 사용할 수 없거나 런타임 환경에 사용할 수 없습니다.

일부 고객은 Access Control 인증 및 Azure Media Services 액세스 모두에 REST API를 사용하여 응용 프로그램을 개발했습니다. 이러한 고객 후속 Azure 미디어 서비스 액세스와 Azure AD 인증을 위해 실행 하는 방식으로 toouse 유일한 hello REST API를 필요 합니다. Toonot 필요한 hello 미디어 서비스.NET SDK 또는 hello Azure AD 라이브러리에 의존 합니다. 이 문서에서는 솔루션에 대해 설명하고 이 시나리오에 대한 심플 코드를 제공합니다. Hello 코드는 모든 Azure AD에 의존 하지 않고 모든 REST API 호출 하기 때문에 Azure 미디어 서비스 라이브러리 hello 코드 수 쉽게 또는 번역 된 tooany 다른 프로그래밍 언어 여야 합니다.

> [!IMPORTANT]
> 현재 미디어 서비스는 hello Azure 액세스 제어 서비스 인증 모델을 지원합니다. 하지만 Access Control 인증은 2018년 6월 1일부로 사용 중단되었습니다. Toohello Azure AD 인증 모델을 최대한 빨리 마이그레이션하는 것이 좋습니다.


## <a name="design"></a>디자인

이 문서에서는 인증 및 권한 부여 디자인 hello를 사용 합니다.

*  권한 부여 프로토콜: OAuth 2.0. OAuth 2.0은 인증 및 권한 부여 모두에 적용되는 웹 보안 표준입니다. Google, Microsoft, Facebook 및 PayPal에서 지원됩니다. 2012년 10월에 비준되었습니다. Microsoft는 OAuth 2.0 및 OpenID Connect를 지원합니다. 이러한 두 표준은 Azure Active Directory, .NET용 OWIN(Open Web Interface for .NET), Katana 및 Azure AD 라이브러리와 같은 여러 서비스 및 클라이언트 라이브러리에서 지원됩니다.
*  부여 유형: 클라이언트 자격 증명 부여 유형. 클라이언트 자격 증명에는 OAuth 2.0의 hello 4 개의 grant 형식 중 하나입니다. Azure AD Microsoft Graph API 액세스에 주로 사용됩니다.
*  인증 모드: 서비스 주체. hello 다른 인증 모드는 사용자 또는 대화형 인증 합니다.

환경에서는 총 4 개의 응용 프로그램 또는 서비스의가 미디어 서비스 사용을 위한 hello Azure AD 인증 및 권한 부여 흐름에 참여 합니다. hello 응용 프로그램 및 서비스에 hello 흐름 hello 다음 표에 설명 되어 있습니다.

|응용 프로그램 형식 |응용 프로그램 |흐름|
|---|---|---|
|클라이언트 | 고객 앱 또는 솔루션 | 이 응용 프로그램 (실제로 해당 프록시)는 hello Azure 구독 및 hello 미디어 서비스 계정 거주 하는 hello Azure AD 테 넌 트에 등록 됩니다. hello hello 등록 응용 프로그램의 서비스 사용자 다음 부여 된 액세스 제어 (IAM) hello 미디어 서비스 계정의 hello에서 소유자 또는 참가자 역할입니다. hello 서비스 사용자 hello 앱 클라이언트 ID와 클라이언트 암호가 표시 됩니다. |
|IDP(ID 공급자) | IDP로 Azure AD | (클라이언트 ID와 클라이언트 암호가) hello 등록 된 응용 프로그램 서비스 사용자는 hello IDP로 Azure AD에 의해 인증 됩니다. 이 인증은 내부에서 암시적으로 수행됩니다. 클라이언트 자격 증명 흐름에서와 같이 hello 클라이언트는 hello 사용자 대신 인증 됩니다. |
|STS(보안 토큰 서비스)/OAuth 서버 | STS로 Azure AD | 액세스 toohello 중간 계층 리소스에 대 한 STS/OAuth 서버와 Azure AD에서 액세스 토큰 또는 JSON 웹 토큰 (JWT) hello IDP (또는 OAuth 2.0 용어로 OAuth 서버)에 의해 인증 후 발급: 경우에 hello 미디어 서비스 REST API 끝점. |
|리소스 | Media Services REST API | 액세스 토큰을 STS 또는 hello OAuth 서버와 Azure AD에서 발급 하 여 모든 미디어 서비스 REST API 호출 권한이 부여 합니다. |

Hello 샘플 코드를 실행 하 고 JWT 또는 액세스 토큰 캡처 hello JWT hello 특성 뒤에 있습니다.

    aud: "https://rest.media.azure.net",

    iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    iat: 1497146280,

    nbf: 1497146280,
    exp: 1497150180,

    aio: "Y2ZgYDjuy7SptPzO/muf+uRu1B+ZDQA=",

    appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6",

    appidacr: "1",

    idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",

    oid: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    sub: "a938cfcc-d3de-479c-b0dd-d4ffe6f50f7c",

    tid: "72f988bf-86f1-41af-91ab-2d7cd011db47",

Hello 테이블 앞의 서비스 또는 hello JWT 및 hello 네 가지 응용 프로그램의 hello 특성 간의 hello 매핑을 다음과 같습니다.

|응용 프로그램 형식 |응용 프로그램 |JWT 특성 |
|---|---|---|
|클라이언트 |고객 앱 또는 솔루션 |appid: "02ed1e8e-af8b-477e-af3d-7e7219a99ac6". hello 클라이언트 ID는 응용 프로그램의 hello 다음 섹션에서 tooAzure AD를 등록 합니다. |
|IDP(ID 공급자) | IDP로 Azure AD |idp: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/".  hello GUID (microsoft.onmicrosoft.com)를 테 넌 트 hello Microsoft ID입니다. 각 테넌트가 자기만의 ID를 가지고 있습니다. |
|STS(보안 토큰 서비스)/OAuth 서버 |STS로 Azure AD | iss: "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/". hello GUID (microsoft.onmicrosoft.com)를 테 넌 트 hello Microsoft ID입니다. |
|리소스 | Media Services REST API |aud: "https://rest.media.azure.net". hello 받는 사람 또는 hello 액세스 토큰의 대상 그룹입니다. |

## <a name="steps-for-setup"></a>설치 단계

tooregister 및 Azure AD 인증 및 tooobtain hello Azure 미디어 서비스 REST API 끝점을 다음 단계 완료 hello 호출에 대 한 액세스 토큰에 대 한 Azure AD 응용 프로그램 설정:

1.  Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), Azure AD 응용 프로그램 (예를 들어 wzmediaservice) toohello Azure AD 테 넌 트 (예를 들어 microsoft.onmicrosoft.com)을 등록 합니다. 웹앱 또는 원시 앱으로 등록했는지 여부는 중요하지 않습니다. 또한 로그온 URL 및 회신 URL(예를 들어, 둘 다로 http://wzmediaservice.com )을 선택할 수 있습니다.
2. Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), toohello 이동 **구성** 응용 프로그램의 탭 합니다. 참고 hello **클라이언트 ID**합니다. 그런 다음 **키** 아래에서 **클라이언트 키**(클라이언트 암호)를 생성합니다. 

    > [!NOTE] 
    > Hello 클라이언트 암호를 기록해 둡니다. 다시 표시되지 않습니다.
    
3.  Hello에 [Azure 포털](http://ms.portal.azure.com), toohello 미디어 서비스 계정 이동 합니다. 선택 hello **액세스 제어** (IAM) 창. Hello 소유자 또는 참가자 역할 hello 권한이 있는 새 멤버를 추가 합니다. Hello 주체에 대 한 hello 응용 프로그램 이름 (이 예에서는 wzmediaservice)에서 1 단계에서 등록을 검색 합니다.

## <a name="info-toocollect"></a>정보 toocollect

tooprepare 코딩 REST, hello 데이터 포인트 tooinclude hello 코드에서 다음 수집:

*   STS 끝점으로 Azure AD: https://login.microsoftonline.com/microsoft.onmicrosoft.com/oauth2/token. 이 끝점에서 JWT 액세스 토큰이 요청됩니다. 또한 한 IDP로 tooserving, Azure AD도는 STS 역할을 합니다. Azure AD는 리소스 액세스를 위한 JWT(액세스 토큰)를 발급합니다. JWT 토큰은 다양한 클레임을 포함합니다.
*   리소스 또는 대상으로 Azure Media Services REST API: https://rest.media.azure.net.
*   클라이언트 ID: [설치 단계](#steps-for-setup)의 2단계를 참조하세요.
*   클라이언트 암호: [설치 단계](#steps-for-setup)의 2단계를 참조하세요.
*   미디어 서비스 계정 형식에 따라 hello의 REST API 끝점:

    https://[media_service_account_name].restv2.[data_center].media.azure.net/API 

    응용 프로그램의 호출이 수행 되는 모든 미디어 서비스 REST API에 대 한 hello 끝점입니다. 예를 들어, https://willzhanmswjapan.restv2.japanwest.media.azure.net/API.

그런 다음 web.config 또는 app.config 파일을 코드에서 toouse에 이러한 다섯 개의 매개 변수를 넣을 수 있습니다.

## <a name="sample-code"></a>샘플 코드

hello 샘플 코드를 찾을 수 있습니다 [Azure 미디어 서비스 액세스에 대 한 Azure AD 인증: REST API를 통해 둘 다](https://github.com/willzhan/WAMSRESTSoln)합니다.

hello 샘플 코드는 두 부분으로 구성 되어 있습니다.

*   Azure AD 인증 및 권한 부여에 대 한 모든 hello REST API 코드를 있는 DLL 라이브러리 프로젝트입니다. 또한 hello 액세스 토큰으로 REST API 호출 toohello 미디어 서비스 REST API 끝점을 만들기 위한 메서드가 있습니다.
*   Azure AD 인증을 시작하고 다양한 Media Services REST API를 호출하는 콘솔 테스트 클라이언트.

hello 샘플 프로젝트에는 세 가지 기능에 있습니다.

*   Hello REST API를 사용 하 여 hello 클라이언트 자격 증명을 통해 azure AD 인증 권한을 부여 합니다.
*   Hello REST API를 사용 하 여 azure 미디어 서비스 액세스
*   만 사용 하 여 azure 저장소 액세스 (사용 되는 toocreate REST API를 사용 하 여 미디어 서비스 계정)으로 REST API를 hello 합니다.


## <a name="where-is-hello-refresh-token"></a>Hello 새로 고침 토큰은 어디 입니까?

일부 판독기 요청할 수 있습니다: 여기서 hello 새로 고침 토큰은? 여기서 새로 고침을 사용하지 않는 이유

toorefresh 액세스 토큰 새로 고침 토큰의 hello 목적은 않습니다. 대신은 설계 된 toobypass 최종 사용자 인증 또는 사용자 개입 하 고 여전히 이전 토큰이 만료 된 경우 유효한 액세스 토큰을 가져옵니다. 새로 고침 토큰에는 “사용자 다시 로그인 바이패스 토큰”과 같은 표현이 더 적절한 이름일 수 있습니다.

OAuth 2.0 권한 부여 권한 (사용자 이름 및 암호를 사용자를 대신) 흐름 hello를 사용 하는 경우 새로 고침 토큰을 사용 하면 갱신 된 액세스 토큰을 가져오는 요청 사용자 개입 하지 않고 있습니다. 그러나 OAuth 2.0 클라이언트 자격 증명 부여 흐름이이 문서에서 설명 하는 hello에 대 한 hello 클라이언트 자체를 대신 하 여 작동 합니다. 사용자 개입을 전혀 필요 하지 않습니다 주며 hello 권한 부여 서버 너무 필요 하지 않습니다 (및 않습니다) 새로 고침 토큰입니다. Hello를 디버깅 하는 경우 **GetUrlEncodedJWT** 메서드를 경우 갖고 있음을 알게 hello 응답 hello 토큰 끝점에서 액세스 토큰에 있지만 새로 고침 토큰이 없습니다.

## <a name="next-steps"></a>다음 단계

시작 [tooyour 계정에 파일 업로드](media-services-dotnet-upload-files.md)합니다.
