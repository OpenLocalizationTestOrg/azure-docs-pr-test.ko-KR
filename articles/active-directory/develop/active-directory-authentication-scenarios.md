---
title: "Azure AD에 대 한 시나리오 aaaAuthentication | Microsoft Docs"
description: "Hello 5 가장 일반적인 인증 시나리오에 대 한 Azure Active Directory (AAD)의 개요"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Azure AD의 인증 시나리오
Azure Active Directory (Azure AD) 제공 하 여 identity 서비스를 지 원하는 산업 표준 OAuth 2.0 및 OpenID Connect와 같은 오픈 소스 라이브러리 toohelp 다양 한 플랫폼에 대 한 프로토콜에 대 한 개발자를 위한 인증을 간소화 신속 하 게 코딩을 시작 합니다. 이 문서는 데 도움이 됩니다 다양 한 Azure AD 시나리오에서는 hello 및 안내해 tooget 시작 하는 방법을 파악 해야 합니다. Hello 다음 섹션으로 구분 됩니다.

* [Azure AD 인증의 기본 사항](#basics-of-authentication-in-azure-ad)
* [Azure AD 보안 토큰의 클레임](#claims-in-azure-ad-security-tokens)
* [Azure AD 응용 프로그램 등록의 기본 사항](#basics-of-registering-an-application-in-azure-ad)
* [응용 프로그램 종류 및 시나리오](#application-types-and-scenarios)
  
  * [웹 브라우저 tooWeb 응용 프로그램](#web-browser-to-web-application)
  * [SPA(단일 페이지 응용 프로그램)](#single-page-application-spa)
  * [네이티브 응용 프로그램 tooWeb API](#native-application-to-web-api)
  * [웹 응용 프로그램 tooWeb API](#web-application-to-web-api)
  * [디먼 또는 서버 응용 프로그램 tooWeb API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Azure AD 인증의 기본 사항
Azure AD 인증의 기본 개념을 잘 모른다면 이 섹션을 읽어 보세요. 그렇지 않으면 할 수 있습니다 tooskip 아래로 너무[응용 프로그램 유형과 시나리오](#application-types-and-scenarios)합니다.

Id가 필요한 hello 가장 기본적인 시나리오를 생각해 봅시다: tooauthenticate tooa 웹 응용 프로그램에는 사용자 웹 브라우저에 필요 합니다. 이 시나리오는 hello에 더 자세히 설명 [tooWeb 웹 브라우저 응용 프로그램](#web-browser-to-web-application) 는 유용한 구역의 하지만 hello Azure AD의 기능 및 hello 시나리오의 작동 방식을 개념화 지점 tooillustrate를 시작 합니다. 이 시나리오에 대 한 다이어그램을 다음 hello를 고려 합니다.

![로그온 tooweb 응용 프로그램의 개요](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

위의 다이어그램에 주의 hello,으로 다음은 필요한 다양 한 구성 요소에 대 한 tooknow:

* Azure AD는 hello id 공급자를 사용자와 조직의 디렉터리에 존재 하는 응용 프로그램의 hello id를 확인 하 고 궁극적으로 해당 사용자와 응용 프로그램의 인증 성공 시 보안 토큰을 발행 하는 일을 담당 합니다.
* Toooutsource 인증 tooAzure AD가 응용 프로그램을 등록 하 고 고유 하 게 식별 hello 앱 hello 디렉터리에 Azure AD에 등록 되어야 합니다.
* 개발자가 인증을 사용할 수 hello 오픈 소스 Azure AD 인증 라이브러리 toomake 쉽게 hello 프로토콜 세부 정보를 처리 하 여 합니다. 자세한 내용은 [Azure Active Directory 인증 라이브러리](active-directory-authentication-libraries.md) 를 참조하세요.

• 사용자가 한 번 인증 되었는지, hello 응용 프로그램 보안 토큰 tooensure hello 사용자의 유효성을 검사 해야 hello 의도 파티에 대 한 인증에 성공 했습니다. 개발자는 JSON 웹 토큰 (JWT) 또는 SAML 2.0을 포함 하 여 Azure AD에서 모든 토큰의 인증 라이브러리 toohandle 유효성 검사를 제공 하는 hello를 사용할 수 있습니다. 수동으로 tooperform 유효성 검사를 하려는 경우 참조 hello [JWT 토큰 처리기](https://msdn.microsoft.com/library/dn205065.aspx) 설명서입니다.

> [!IMPORTANT]
> Azure AD는 공개 키 암호화 toosign 토큰을 사용 하 고 유효한 지 확인 합니다. 참조 [중요 한 정보에 대 한 서명 키 롤오버 Azure AD에서](active-directory-signing-key-rollover.md) 대 한 자세한 내용은 hello 필수 논리가 응용 프로그램 tooensure의 hello 최신 키를 가진 업데이트 항상 됩니다.
> 
> 

• hello 요청 흐름과 hello 인증 프로세스에 대 한 응답은 OAuth 2.0, OpenID Connect 등 사용 된 hello 인증 프로토콜에 의해 결정 됩니다 Ws-federation 또는 SAML 2.0. 이러한 프로토콜이 hello에 보다 자세히 설명 되어 [Azure Active Directory 인증 프로토콜](active-directory-authentication-protocols.md) 항목 및 아래 hello 섹션.

> [!NOTE]
> Azure AD에서는 OAuth 2.0 hello 지원 및 Jwt로 대표 되는 전달자 토큰을 포함 하 여 전달자 토큰을 광범위 하 게 하는 OpenID Connect 표준을 사용 합니다. 전달자 토큰은 보호 된 리소스를 부여 "전달자" 액세스 tooa hello 하는 경량 보안 토큰입니다. 이 전반에 "bearer" hello hello 토큰을 제공할 수 있는 당사자입니다. 파티 먼저 Azure AD tooreceive hello bearer 토큰으로 인증 hello 필요한 단계는 전송 및 저장에서 toosecure hello 토큰을 따르지 않은 경우, 있지만 차단 하 고 의도 하지 않은 당사자에서 사용 하는 수 있습니다. 일부 보안 토큰에는 권한 없는 당사자가 사용하는 것을 방지하는 기본 제공 메커니즘이 있지만, 전달자 토큰에는 이러한 메커니즘이 없으므로 전송 계층 보안(HTTPS)과 같은 보안 채널에서 전달자 토큰을 전송해야 합니다. 전달자 토큰 지우기 hello에 전송 되기 매뉴얼에 hello 중간 공격 악의적인 당사자 tooacquire hello 토큰에서 사용할 수 있습니다 하 고 사용 하 여 무단된 액세스 tooa 보호 된 리소스에 대 한 합니다. hello 저장 하거나 나중에 사용 하기 위해 전달자 토큰을 캐시 하는 경우 동일한 보안 원칙이 적용 됩니다. 항상 응용 프로그램이 안전한 방식으로 전달자 토큰을 전송하고 저장하도록 합니다. 전달자 토큰의 보안 고려 사항을 자세히 알아보려면 [RFC 6750 Section 5](http://tools.ietf.org/html/rfc6750)를 참조하세요.
> 
> 

이제의 toounderstand 아래 hello 섹션을 참조 하는 hello 기본 한 개요 방법을 Azure AD에서 작동 하는 프로 비전을 hello 일반적인 시나리오는 Azure AD를 지원 합니다.

## <a name="claims-in-azure-ad-security-tokens"></a>Azure AD 보안 토큰의 클레임
보안 토큰을 Azure AD에서 발급 한 인증 된 hello 주제에 대 한 정보 어설션 또는 클레임을 포함 합니다. 이러한 클레임은 다양 한 작업에 대 한 hello 응용 프로그램에서 사용할 수 있습니다. 예를 들어 사용된 toovalidate hello 토큰 이어야, 식별 hello 주체의 디렉터리 테 넌 트, 사용자 정보를 표시, hello 주체의 권한 부여를 결정 하 고 수 등입니다. 지정된 된 보안 토큰에 있는 hello 클레임은 토큰의 hello 형식, 사용 된 자격 증명 tooauthenticate hello 사용자 및 hello 응용 프로그램 구성의 hello 형식에 따라 달라 집니다. Azure AD에서 나오는 클레임의 각 유형에 대 한 간략 한 설명은 hello 테이블 아래에 제공 됩니다. 자세한 내용은 참조 너무[지원 되는 토큰 및 클레임 유형](active-directory-token-and-claims.md)합니다.

| 클레임 | 설명 |
| --- | --- |
| 응용 프로그램 UI |Hello 토큰을 사용 하는 hello 응용 프로그램을 식별 합니다. |
| 대상 |Hello 받는 사람 리소스를 식별에 대 한 hello 토큰을 사용 합니다. |
| 응용 프로그램 인증 컨텍스트 클래스 참조 |Hello 클라이언트 인증된 (공용 클라이언트 및 기밀 클라이언트)를가 하는 방법을 나타냅니다. |
| 인증 인스턴트 |레코드에는 날짜 및 시간 hello 인증 hello 합니다. |
| 인증 방법 |Hello 토큰의 주체 hello 인증 된 방법을 나타냅니다 (암호, 인증서 등). |
| 이름 |Azure AD의 집합으로 hello 사용자의 지정 된 이름 hello를 제공합니다. |
| 그룹 |Hello 사용자가 멤버인 개체 Id의 Azure AD 그룹에 포함 되어 있습니다. |
| ID 공급자 |Hello 토큰의 hello 주체를 인증 하는 레코드 hello id 공급자입니다. |
| 발급 시간 |레코드 hello는 hello에 토큰이 발급 된 시간, 자주 토큰 새로 고침에 사용 됩니다. |
| 발급자 |Hello 내보낸 STS를으로 hello 토큰 hello Azure AD 테 넌 트를 식별 합니다. |
| 성 |설정 hello surname hello 사용자의 Azure AD에서 제공 합니다. |
| 이름 |Hello 토큰의 hello 주체를 식별 하는 사람이 읽을 수 있는 값을 제공 합니다. |
| 개체 ID |Azure AD에서 주체의 hello는 변경할 수 없는 고유 식별자를 포함합니다. |
| 역할 |친숙 한 이름이 포함 된 해당 hello 사용자가 부여한 Azure AD 응용 프로그램 역할입니다. |
| 범위 |Hello 사용 권한을 부여한 toohello 클라이언트 응용 프로그램을 나타냅니다. |
| 제목 |토큰 정보를 어설션하는 hello에 대 한 hello 보안 주체를 나타냅니다. |
| 테넌트 ID |Hello 디렉터리 테 넌 트의 hello 토큰을 발급 하는 변경할 수 없는 고유 식별자를 포함 합니다. |
| 토큰 수명 |Hello 유효한 시간 간격을 토큰을 정의 합니다. |
| 사용자 계정 이름 |Hello hello 주체의 사용자 계정 이름에 포함 되어 있습니다. |
| 버전 |Hello 토큰의 hello 버전 번호를 포함합니다. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Azure AD 응용 프로그램 등록의 기본 사항
모든 아웃소싱하는 응용 프로그램 인증 tooAzure AD 디렉터리에 등록 되어야 합니다. 이 단계에서는 hello URL을 포함 하 여 응용 프로그램에 대 한 Azure AD에 알리는, hello URL toosend 회신 hello URI tooidentify 인증 후 응용 프로그램 등에입니다. 이러한 정보가 필요한 주된 이유는 다음과 같습니다.

* Azure AD는 로그온 하거나 토큰을 교환할 처리할 때 좌표 toocommunicate hello 응용 프로그램과 함께 필요 합니다. Hello 다음을 확인할 수 있습니다.
  
  * 응용 프로그램에 대 한 응용 프로그램 ID URI: hello 식별자입니다. 이 값에는 응용 프로그램 hello 호출자가 토큰을 인증 tooindicate 하는 동안 AD tooAzure 전송 됩니다. 또한이 값 hello 응용 프로그램 hello 대상 의도 한 것을 알 수 있도록 hello 토큰에 포함 됩니다.
  * 회신 URL 및 리디렉션 URI:, 웹 API 또는 웹 응용 프로그램의 hello 경우 hello 회신 URL은 Azure AD가 인증에 성공 하면 토큰을 포함 하 여 hello 인증 응답을 전송할 hello 위치 toowhich 합니다. 네이티브 응용 프로그램의 경우 hello hello 리디렉션 URI는 고유 식별자 toowhich Azure AD에서 OAuth 2.0 요청에 hello 사용자-에이전트를 리디렉션할는 합니다.
  * 응용 프로그램 ID: hello 응용 프로그램 등록 될 때 Azure AD에서 생성 된 응용 프로그램에 대 한 ID를 hello 합니다. 인증 코드나 토큰을 요청할 때 hello 응용 프로그램 ID와 키 tooAzure AD를 인증 하는 동안 전송 됩니다.
  * AD tooAzure toocall 웹 API에 인증할 때 응용 프로그램 ID와 함께 전송 되는 키: hello 키입니다.
* Azure AD 요구 tooensure hello 응용 프로그램에 디렉터리 데이터를 다른 응용 프로그램을 조직에 필요한 사용 권한이 tooaccess hello 하 고

Azure AD를 사용하여 개발 및 통합할 수 있는 두 가지 범주의 응용 프로그램이 있다는 것을 이해하면 프로비저닝이 더 분명해집니다.

* 단일 테넌트 응용 프로그램: 단일 테넌트 응용 프로그램은 단일 조직에서 사용하기 위한 것입니다. 일반적으로 엔터프라이즈 개발자가 작성한 LoB(기간 업무) 응용 프로그램이 이에 해당합니다. 단일 테 넌 트 응용 프로그램만 toobe 한 디렉터리의 사용자가 액세스 하며 결과적으로, 특정 디렉터리에서 사용자를 프로 비전 toobe만 필요 합니다. 이러한 응용 프로그램은 일반적으로 개발자 hello 조직에 등록 됩니다.
* 다중 테넌트 응용 프로그램: 다중 테넌트 응용 프로그램은 하나의 조직뿐만 아니라 다수의 조직에서 사용하기 위한 것입니다. 일반적으로 ISV(Independent Software Vendor)가 작성한 SaaS(Software-as-a-Service) 응용 프로그램이 이에 해당합니다. 다중 테 넌 트 응용 프로그램은 사용자 또는 관리자 동의 tooregister 필요한 위치에 사용 될, 각 디렉터리에 사용자를 프로 비전 toobe 필요 하 합니다. 응용 프로그램 hello 디렉터리에 등록 되었습니다. 그 액세스 toohello Graph API 또는 다른 웹 API이 동의 프로세스 시작 됩니다. 사용자 또는 다른 조직에서 관리자 toouse hello 응용 프로그램 등록을 hello 응용 프로그램에 필요한 hello 사용 권한을 표시 하는 대화 상자가 표시 됩니다. hello 사용자 또는 관리자 동의 toohello 응용 프로그램을 응용 프로그램 액세스 toohello hello 수 있도록 데이터를 지정 하 고 마지막으로 레지스터 hello 해당 디렉터리에서 응용 프로그램 수 있습니다. 자세한 내용은 참조 [hello 동의 프레임 워크 개요](active-directory-integrating-applications.md#overview-of-the-consent-framework)합니다.

단일 테넌트 응용 프로그램 대신 다중 테넌트 응용 프로그램을 개발할 때 고려할 몇 가지 추가 사항이 있습니다. 예를 들어 여러 디렉터리의 응용 프로그램 사용 가능한 toousers를 만들 때는 필요 메커니즘 toodetermine 더에 테 넌 트입니다. 단일 테 넌 트 응용 프로그램 하기만 toolook 자체 디렉터리에 사용자가 다중 테 넌 트 응용 프로그램이 Azure AD에서 tooidentify 모든 hello 디렉터리에서 특정 사용자를 필요로 동안 있습니다. tooaccomplish이이 작업을 Azure AD는 모든 다중 테 넌 트 응용 프로그램 로그인 요청을 테 넌 트 별 끝점 대신에 지시할 수 있는 공용 인증 끝점을 제공 합니다. 이 끝점 중인 https://login.microsoftonline.com/common 모든 디렉터리에 대 한 Azure AD 테 넌 트 별 끝점 https://login.microsoftonline.com/contoso.onmicrosoft.com 일 수 있습니다. hello 일반 끝점이 특히 중요 한 tooconsider 때 필요 하므로 hello 필수 논리가 toohandle 여러 테 넌 트에 로그인, 로그 아웃 및 토큰 유효성 검사 하는 동안 응용 프로그램을 개발 합니다.

현재 단일 테 넌 트 응용 프로그램을 개발 하는 경우 있지만 toomake 원하는 것 toomany 사용할 수 있는 조직에서는 쉽게 수행할 수 있습니다 변경 toohello 응용 프로그램 및 해당 구성에서 Azure AD toomake 것 수 있는 다중 테 넌입니다. 또한 Azure AD에서는 hello 동일한 서명 키의 모든 디렉터리에서 모든 토큰에 대 한 여부를 제공 하는 단일 테 넌 트 또는 다중 테 넌 트 응용 프로그램에 인증 합니다.

이 문서에 나온 각 시나리오에는 해당 프로비저닝 요구 사항을 설명하는 하위 섹션이 나옵니다. Azure AD에서 응용 프로그램을 프로 비전 하는 방법에 대 한 자세한 내용은 단일 및 다중 테 넌 트 응용 프로그램 간의 차이점을 hello, 참조 및 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md) 자세한 정보에 대 한 합니다. 계속 Azure AD에서 toounderstand hello 일반적인 응용 프로그램 시나리오를 진행 하십시오.

## <a name="application-types-and-scenarios"></a>응용 프로그램 종류 및 시나리오
각각이 문서에서 설명 하는 hello 시나리오의 다양 한 언어 및 플랫폼을 사용 하 여 개발할 수 있습니다. 모두에서 사용할 수 있는 전체 코드 샘플에서 지원 우리의 [코드 샘플 안내](active-directory-code-samples.md), 또는 hello 해당에서 직접 [샘플 GitHub 리포지토리에](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory)합니다. 또한 응용 프로그램에 종단 간 시나리오의 특정 부분이나 세그먼트가 필요한 경우 대부분 해당 기능을 개별적으로 추가할 수 있습니다. 예를 들어 web API를 호출 하는 네이티브 응용 프로그램의 경우도 hello 웹 API를 호출 하는 웹 응용 프로그램을 쉽게 추가할 수 있습니다. hello 다음 다이어그램에서는 이러한 시나리오 및 응용 프로그램 유형, 방식과 다양 한 구성 요소를 추가할 수 있습니다.

![응용 프로그램 종류 및 시나리오](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

다음은 Azure AD에서 지 원하는 hello 5 개의 기본 응용 프로그램 시나리오입니다.

* [웹 브라우저 tooWeb 응용 프로그램](#web-browser-to-web-application): 사용자는 Azure AD로 보호 되는 tooa 웹 응용 프로그램에서 toosign 있어야 합니다.
* [단일 페이지 응용 프로그램 (SPA)](#single-page-application-spa): 사용자는 Azure AD로 보호 되는 tooa 단일 페이지 응용 프로그램에서 toosign 있어야 합니다.
* [네이티브 응용 프로그램 tooWeb API](#native-application-to-web-api): 네이티브 응용 프로그램에서 실행 되는 휴대폰, 태블릿 또는 PC 요구 tooauthenticate 사용자 tooget 리소스 web API에서에서 Azure AD로 보호 되는 합니다.
* [웹 응용 프로그램 tooWeb API](#web-application-to-web-api): 웹 응용 프로그램 웹 Azure AD에서 보호 하는 API에서에서 tooget 리소스가 필요 합니다.
* [디먼 또는 서버 응용 프로그램 tooWeb API](#daemon-or-server-application-to-web-api): 디먼 응용 프로그램 또는 서버 응용 프로그램 웹 사용자 인터페이스 없이 웹 Azure AD에서 보호 하는 API에서에서 tooget 리소스가 필요 합니다.

### <a name="web-browser-tooweb-application"></a>웹 브라우저 tooWeb 응용 프로그램
이 섹션에서는 웹 브라우저 tooa 웹 응용 프로그램의 사용자를 인증 하는 응용 프로그램에 설명 합니다. 이 시나리오에서는 웹 응용 프로그램 hello 지시 hello 사용자의 브라우저 toosign tooAzure AD에서에서 해당 합니다. Azure AD 보안 토큰에 hello 사용자에 대 한 클레임을 포함 하는 hello 사용자의 브라우저를 통해 로그인 응답을 반환 합니다. 이 시나리오에서는 로그온 지원 hello Ws-federation, SAML 2.0 및 OpenID Connect 프로토콜을 사용 하 여 합니다.

#### <a name="diagram"></a>다이어그램
![브라우저 tooweb 응용 프로그램에 대 한 인증 흐름](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>프로토콜 흐름 설명
1. 때 사용자 hello 응용 프로그램 방문에 toosign을 리디렉션됩니다 로그인 요청 toohello 인증 끝점을 통해 Azure AD에서.
2. hello 사용자가 hello 로그인 페이지에 로그인 합니다.
3. 인증이 성공 하는 경우 Azure AD 인증 토큰을 만들고 hello Azure 포털에에서 구성 된는 로그인 응답 toohello 응용 프로그램의 회신 URL을 반환 합니다. 프로덕션 응용 프로그램의 경우 이 회신 URL은 HTTPS여야 합니다. 토큰을 반환 하는 hello hello 응용 프로그램 toovalidate hello 토큰에서 필요로 하는 hello 사용자와 Azure AD에 대 한 클레임을 포함 합니다.
4. hello 응용 프로그램 공개 서명 키 및 발급자 정보를 사용할 수 있는 hello 페더레이션 메타 데이터 문서에서 Azure AD에 대 한 사용 하 여 hello 토큰을 확인 합니다. Hello 응용 프로그램에 hello 토큰 유효성을 검사 한 후 Azure AD는 hello 사용자와 새 세션을 시작 합니다. 이 세션 만료 될 때까지 hello 사용자 tooaccess hello 응용 프로그램을 허용 합니다.

#### <a name="code-samples"></a>코드 샘플
웹 브라우저 tooWeb 응용 프로그램 시나리오에 대 한 hello 코드 샘플을 참조 하세요. 자주 확인-hello 항상 새로운 샘플이 추가 합니다. [웹 브라우저 응용 프로그램 tooWeb](active-directory-code-samples.md#web-browser-to-web-application)합니다.

#### <a name="registering"></a>등록
* 단일 테 넌 트: 조직에 대 한 응용 프로그램을 작성 하는 경우 등록 해야 회사의 디렉터리에 hello Azure 포털을 사용 하 여 합니다.
* 다중 테 넌 트: 조직 외부 사용자가 사용할 수 있는 응용 프로그램을 작성 하는 경우 것 회사 디렉터리에 등록 해야 하지만 또한 hello 응용 프로그램을 사용할 각 조직의 디렉터리에 등록 되어야 합니다. toomake가 디렉터리에서 사용할 수 있는 응용 프로그램을 tooconsent tooyour 응용 프로그램 수 있게 해 주는 고객에 대 한 등록 프로세스를 포함할 수 있습니다. 응용 프로그램에 로그인 할 때 hello 권한 hello 응용 프로그램을 필요한 하 고 다음 옵션 tooconsent hello 보여 주는 대화 상자가 표시 됩니다. Hello 관리자 hello 필요한 사용 권한에 따라 다른 조직의 수 있습니다 toogive 동의 필요 합니다. Hello 사용자 또는 관리자가 동의한 경우 hello 응용 프로그램은 해당 디렉터리에 등록 합니다. 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)을 참조하세요.

#### <a name="token-expiration"></a>토큰 만료
Azure AD에서 발급 하는 hello 토큰의 hello 수명이 만료 될 경우 hello 사용자의 세션이 만료 합니다. 원한다면 비활성 기간을 기준으로 사용자를 로그아웃시키는 등, 응용 프로그램이 세션 만료 시간을 단축할 수 있습니다. Hello 세션이 만료 되 면 hello 사용자의 증명된 toosign 다시 됩니다.

### <a name="single-page-application-spa"></a>SPA(단일 페이지 응용 프로그램)
이 섹션에서는 Azure AD를 사용 하는 단일 페이지 응용 프로그램에 대 한 인증 설명 고 hello OAuth 2.0 암시적 권한 부여의 웹 API 백 엔드 toosecure 합니다. 단일 페이지 응용 프로그램은 일반적으로 서버에서 실행 되는 웹 API 백 엔드로 hello 브라우저에서 실행 되는 JavaScript 프레젠테이션 계층 (프런트 엔드)으로 구성 하 고 구현 hello 응용 프로그램의 비즈니스 논리입니다. hello 암시적 권한 부여 및 응용 프로그램 시나리오에 적합 한지 결정 하는 도움말에 대해 자세히 toolearn 참조 [이해 hello OAuth2 암시적 부여 흐름이 Azure Active Directory에서](active-directory-dev-understanding-oauth2-implicit-grant.md)합니다.

이 시나리오에서는 hello 사용자가 로그인 할 때 JavaScript 프런트 엔드 사용 하 여 hello 됩니다. [Active Directory 인증 라이브러리 (ADAL javascript. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) hello 암시적 권한 부여 tooobtain ID 토큰 (id_token) Azure AD에서 합니다. hello 토큰이 캐시 되 한 hello 클라이언트 다시 연결 toohello 요청 hello bearer 토큰으로 tooits 웹 API 백 엔드 hello OWIN 미들웨어를 사용 하 여 보호 되는 호출을 수행 하는 경우. 

#### <a name="diagram"></a>다이어그램
![단일 페이지 응용 프로그램 다이어그램](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>프로토콜 흐름 설명
1. hello 사용자 toohello 웹 응용 프로그램을 탐색합니다.
2. hello 응용 프로그램 hello JavaScript 프런트 엔드 (프레젠테이션 계층) toohello 브라우저를 반환합니다.
3. hello 사용자를 로그인으로 로그인의 로그인 링크를 클릭 하 여 예를 들어 시작 합니다. hello 브라우저 GET toohello Azure AD 권한 부여 끝점 toorequest ID 토큰을 보냅니다. 이 요청 hello 응용 프로그램 ID와 회신 URL hello 쿼리 매개 변수를 포함합니다.
4. Azure AD는 hello hello Azure 포털에에서 구성 된 회신 URL을 등록 하는 hello에 대 한 회신 URL을 확인 합니다.
5. hello 사용자가 hello 로그인 페이지에 로그인 합니다.
6. 인증이 성공 하는 경우 Azure AD ID 토큰을 만들고는 URL 조각 (#) toohello 응용 프로그램의 회신 URL로 반환 합니다. 프로덕션 응용 프로그램의 경우 이 회신 URL은 HTTPS여야 합니다. 토큰을 반환 하는 hello hello 응용 프로그램 toovalidate hello 토큰에서 필요로 하는 hello 사용자와 Azure AD에 대 한 클레임을 포함 합니다.
7. hello hello 브라우저에서 실행 되는 JavaScript 클라이언트 코드가 toohello 응용 프로그램의 웹 API 백 엔드 호출 보안에 대 한 응답 toouse hello에서에서 hello 토큰을 추출 합니다.
8. hello 브라우저 호출 hello 응용 프로그램의 웹 API 백 hello 인증 헤더에 액세스 토큰 hello 끝나야 합니다.

#### <a name="code-samples"></a>코드 샘플
단일 페이지 응용 프로그램 (SPA) 시나리오에 대 한 hello 코드 샘플을 참조 하세요. 있는지 toocheck 다시를 자주-수 새로운 샘플이 추가 모든 hello 시간입니다. [SPA(단일 페이지 응용 프로그램)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>등록
* 단일 테 넌 트: 조직에 대 한 응용 프로그램을 작성 하는 경우 등록 해야 회사의 디렉터리에 hello Azure 포털을 사용 하 여 합니다.
* 다중 테 넌 트: 조직 외부 사용자가 사용할 수 있는 응용 프로그램을 작성 하는 경우 것 회사 디렉터리에 등록 해야 하지만 또한 hello 응용 프로그램을 사용할 각 조직의 디렉터리에 등록 되어야 합니다. toomake가 디렉터리에서 사용할 수 있는 응용 프로그램을 tooconsent tooyour 응용 프로그램 수 있게 해 주는 고객에 대 한 등록 프로세스를 포함할 수 있습니다. 응용 프로그램에 로그인 할 때 hello 권한 hello 응용 프로그램을 필요한 하 고 다음 옵션 tooconsent hello 보여 주는 대화 상자가 표시 됩니다. Hello 관리자 hello 필요한 사용 권한에 따라 다른 조직의 수 있습니다 toogive 동의 필요 합니다. Hello 사용자 또는 관리자가 동의한 경우 hello 응용 프로그램은 해당 디렉터리에 등록 합니다. 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)을 참조하세요.

Hello 응용 프로그램을 등록 한 후 구성 된 toouse OAuth 2.0 Implicit Grant 프로토콜 이어야 합니다. 기본적으로 이 프로토콜은 응용 프로그램에 대해 사용하지 않도록 설정되어 있습니다. 응용 프로그램에 대 한 OAuth2 Implicit Grant 프로토콜 tooenable hello hello Azure 포털에서에서 해당 응용 프로그램 매니페스트를 편집 하 고 "oauth2AllowImplicitFlow" 값 tootrue hello를 설정 합니다. 자세한 지침은 [단일 페이지 응용 프로그램에 OAuth 2.0 암시적 허용 사용](active-directory-integrating-applications.md)을 참조하세요.

#### <a name="token-expiration"></a>토큰 만료
ADAL.js toomanage 인증을 사용 하 여 Azure AD에는 만료 된 토큰으로 hello 응용 프로그램에서 호출할 수 있는 추가 웹 API 리소스에 대 한 토큰을 가져오는 여러 가지 기능에서 활용 합니다. Hello 사용자 Azure AD에 성공적으로 인증 hello 브라우저와 Azure AD 간의 hello 사용자에 대 한 쿠키로 보호 된 세션이 설정 됩니다. 것이 중요 한 toonote hello 사용자와 Azure AD 간의 및 not between hello 사용자와 hello 서버에서 실행 되는 hello 웹 응용 프로그램 hello 세션 존재 합니다. 토큰 만료 되 면 ADAL.js toosilently 다른 토큰을 가져올이 세션을 사용 합니다. 숨겨진된 iFrame toosend를 사용 하 여이 작업을 수행 하 고 hello OAuth Implicit Grant 프로토콜을 사용 하 여 hello 요청을 수신 합니다. ADAL.js 동일한이 메커니즘을 사용할 수 있습니다 toosilently API 리소스 hello 응용 프로그램 호출 이러한 리소스 지원 크로스-원본 자원 공유 (CORS)으로 등록 된를 hello 사용자의 디렉터리에 다른 웹에 대 한 Azure AD에서 액세스 토큰을 가져올 및 동의는 hello 사용자가 로그인 하는 동안 제공 되었습니다.

### <a name="native-application-tooweb-api"></a>네이티브 응용 프로그램 tooWeb API
이 섹션에서는 사용자를 대신하여 웹 API를 호출하는 네이티브 응용 프로그램에 대해 설명합니다. 이 시나리오는 기반으로 공용 클라이언트 hello OAuth 2.0 인증 코드 권한 유형을 hello의 섹션 4.1에에서 설명 된 대로 [OAuth 2.0 사양](http://tools.ietf.org/html/rfc6749)합니다. hello 네이티브 응용 프로그램은 hello OAuth 2.0 프로토콜을 사용 하 여 hello 사용자에 대 한 액세스 토큰을 획득 합니다. 이 액세스 토큰 hello 요청 toohello 웹 API에 hello 사용자 권한을 부여 hello 필요한 리소스를 반환 하는 다음 전송 됩니다.

#### <a name="diagram"></a>다이어그램
![네이티브 응용 프로그램 tooWeb API 다이어그램](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>TooAPI 네이티브 응용 프로그램에 대 한 인증 흐름
#### <a name="description-of-protocol-flow"></a>프로토콜 흐름 설명
Hello AD 인증 라이브러리를 사용 하는 경우 대부분의 hello 프로토콜 세부 정보 아래에 설명 된 hello 브라우저 팝업, 토큰 캐싱 및 새로 고침 토큰 처리 등을 처리 됩니다.

1. Hello 네이티브 응용 프로그램은 브라우저 팝업을 사용 하 여 Azure AD에 요청 toohello 권한 부여 끝점을 만듭니다. 이 요청 hello Azure 포털 및 hello 웹 API에 대 한 hello 응용 프로그램 ID URI에 표시 된 대로 응용 프로그램 ID hello 및 hello 리디렉션 hello 네이티브 응용 프로그램의 URI 포함 합니다. 증명된 toosign 다시는 hello 사용자가 아직 로그인 하는 경우
2. Azure AD는 hello 사용자를 인증합니다. 다중 테 넌 트 응용 프로그램 동의 필요한 toouse hello 응용 프로그램을 아직 수행 하지 않은 이러한 경우 hello 사용자가 필요한 tooconsent을 됩니다. 동의한 후 및 인증 성공 시 Azure AD는 인증 코드 응답 백 toohello 클라이언트 응용 프로그램의 리디렉션 URI를 발급 합니다.
3. Azure AD는 인증 코드 응답을 다시 발급 하면 toohello 리디렉션 URI, 클라이언트 응용 프로그램 중지 브라우저 상호 작용 및 추출 hello에서에서 인증 코드 응답 hello hello 합니다. 이 인증 코드를 사용 하 여 hello 권한 부여 코드를 포함 하는 요청 tooAzure AD의 토큰 끝점을 전송 하는 hello 클라이언트 응용 프로그램, 클라이언트 응용 프로그램 (응용 프로그램 ID 및 리디렉션 URI) hello 고 원하는 리소스 (응용 프로그램 ID hello에 대 한 세부 정보 URI hello 웹 API에 대 한)입니다.
4. hello 권한 부여 코드와 hello 클라이언트 응용 프로그램 및 web API에 대 한 정보는 Azure AD에 의해 유효성이 검사 됩니다. 유효성 검사가 성공하면 Azure AD는 JWT 액세스 토큰과 JWT 새로 고침 토큰 등 두 가지 토큰을 반환합니다. Azure AD에서 자신의 표시 이름 및 테 넌 트 ID와 같은 hello 사용자에 대 한 기본 정보를 반환 하는 또한
5. HTTPS를 통해 클라이언트 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.
6. Hello 액세스 토큰이 만료 되 면 hello 클라이언트 응용 프로그램 hello 사용자 필요한 tooauthenticate 다시 나타내는 오류가 나타납니다. Hello 응용 프로그램에 유효한 새로 고침 토큰을 사용 하는 tooacquire 확인 하지 않고 새 액세스 토큰에서 사용자 toosign 안녕 수 있습니다. Hello 새로 고침 토큰이 만료 되 면 hello 진행 되는 toointeractively 다시 한 번 hello 사용자를 인증 합니다.

> [!NOTE]
> 새로 고침 토큰 hello Azure AD에서 발급 될 수 있습니다 사용된 tooaccess 여러 리소스가 있습니다. 예를 들어 권한 toocall 두 웹 Api에 있는 클라이언트 응용 프로그램이 있는 경우 hello 새로 고침 토큰이 사용 되는 tooget 액세스 토큰 toohello 다른 웹 API도 수 있습니다.
> 
> 

#### <a name="code-samples"></a>코드 샘플
네이티브 응용 프로그램 tooWeb API 시나리오에 대 한 hello 코드 샘플을 참조 하세요. 자주 확인-hello 항상 새로운 샘플이 추가 합니다. [네이티브 응용 프로그램 tooWeb API](active-directory-code-samples.md#native-application-to-web-api)합니다.

#### <a name="registering"></a>등록
* 단일 테 넌 트: 네이티브 응용 프로그램 둘 다 hello 및 hello에 hello web API를 등록 해야 Azure AD에서 동일한 디렉터리입니다. hello web API 구성된 tooexpose tooits 리소스에 사용 되는 toolimit hello 네이티브 응용 프로그램의 액세스는 권한 집합이 될 수 있습니다. hello 그러면 클라이언트 응용 프로그램 hello Azure 포털의에서 hello "tooOther 응용 프로그램 사용 권한" 드롭다운 메뉴에서 원하는 hello 사용 권한을 선택합니다.
* 다중 테 넌 트: 먼저 hello 네이티브 응용 프로그램에만 등록 hello 개발자 또는 게시자의 디렉터리입니다. 둘째, hello 네이티브 응용 프로그램은 구성 된 tooindicate hello toobe 기능 필요한 사용 권한을 합니다. 동의 toohello 응용 프로그램을 사용할 수 있는 tootheir 조직 하므로 하면이 관리자 사용자 또는 관리자 hello 대상 디렉터리에 필요한 사용 권한이 목록은이 대화 상자에서 표시 됩니다. 일부 응용 프로그램 hello 조직의 모든 사용자에 동의할 수 있는 사용자 수준 권한이 필요 합니다. 다른 응용 프로그램에 동의할 수 없습니다 hello 조직에 있는 사용자는 관리자 수준 사용 권한이 필요 합니다. 디렉터리 관리자만이 수준의 권한이 필요한 동의 tooapplications를 제공할 수 있습니다. Hello 사용자 또는 관리자가 동의한 경우만 hello web API가 디렉터리에 등록 됩니다. 자세한 내용은 [Azure Active Directory와 응용 프로그램 통합](active-directory-integrating-applications.md)을 참조하세요.

#### <a name="token-expiration"></a>토큰 만료
Hello 네이티브 응용 프로그램에서 JWT 액세스 토큰의 권한 부여 코드 tooget를 사용 하는 경우 JWT 새로 고침 토큰도 수신 합니다. Hello 새로 고침 토큰 사용된 toore 수 hello 액세스 토큰이 만료 되 면-않고도 toosign 다시 hello 사용자를 인증 합니다. 이 새로 고침 토큰은 사용 되는 tooauthenticate hello 사용자, 발생 하는 새 액세스에서 토큰 및 새로 고침 한 후 토큰입니다.

### <a name="web-application-tooweb-api"></a>웹 응용 프로그램 tooWeb API
이 섹션에서는 web API 로부터 리소스 tooget 하는 웹 응용 프로그램을 설명 합니다. 이 시나리오에는 웹 응용 프로그램 hello 하는 두 개의 id 유형을 수 tooauthenticate를 사용 하 여 있고 hello web API를 호출할: 응용 프로그램 id 또는 위임 된 사용자 id입니다.

*응용 프로그램 id:* OAuth 2.0 클라이언트 자격 증명 hello 응용 프로그램 및 액세스 hello tooauthenticate 부여이 시나리오에서는 웹 API입니다. 응용 프로그램 id를 hello 웹 API는 hello 웹 응용 프로그램 호출 하 고 검색할 수 있습니다를 사용 하는 경우 hello로 web API 받지 않습니다 hello 사용자에 대 한 정보. Hello 응용 프로그램 hello 사용자에 대 한 정보를 받으면 hello 응용 프로그램 프로토콜을 통해 보내집니다 및 Azure AD에서 서명 되지 않은 합니다. hello web API hello 웹 응용 프로그램 hello 사용자를 인증 신뢰 합니다. 이런 이유로, 이 패턴을 신뢰할 수 있는 하위 시스템이라고 합니다.

*위임된 사용자 ID:* 기밀 클라이언트에서 OpenID Connect 및 OAuth 2.0 인증 코드 권한 등 두 가지 방법으로 시나리오를 완수할 수 있습니다. hello 웹 응용 프로그램 사용자 hello toohello web API 해당 hello 사용자 성공적으로 인증 toohello 웹 응용 프로그램의 변수를 증명 하 고 hello 웹 응용 프로그램을 수 tooobtain 위임 된 사용자 identity toocall hello web API에 대 한 액세스 토큰을 가져옵니다. 이 액세스 토큰 hello 요청 toohello web API에는 hello 사용자 권한을 부여 하 고 원하는 hello 리소스 반환에 전송 됩니다.

#### <a name="diagram"></a>다이어그램
![웹 응용 프로그램 API tooWeb 다이어그램](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>프로토콜 흐름 설명
둘 다 hello 응용 프로그램 id와 위임 된 사용자 id 유형을 hello 흐름 아래에서 설명 합니다. hello 둘 간의 주요 차이점은 hello 위임 된 사용자 id hello 사용자 로그인 하 고 수 전에 얻을 toohello 웹 API 액세스 권한 부여 코드 획득 먼저 해야 합니다.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>OAuth 2.0 클라이언트 자격 증명 권한을 사용한 응용 프로그램 ID
1. Hello 웹 응용 프로그램에서 tooAzure AD 사용자가 로그인 (hello 참조 [tooWeb 웹 브라우저 응용 프로그램](#web-browser-to-web-application) 위에).
2. hello 웹 응용 프로그램 toohello 웹 API를 인증 하 고 원하는 hello 리소스를 검색할 수 있도록 tooacquire 액세스 토큰이 필요 합니다. Hello 자격 증명, 응용 프로그램 ID 및 web API의 응용 프로그램 ID URI를 제공 하는 요청 tooAzure AD의 토큰 끝점을 만듭니다.
3. Azure AD hello 응용 프로그램을 인증 하 고는 사용 되는 toocall hello 웹 API JWT 액세스 토큰을 반환 합니다.
4. HTTPS를 통해 웹 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.

##### <a name="delegated-user-identity-with-openid-connect"></a>OpenID Connect를 사용한 위임된 사용자 ID
1. 사용자가 Azure AD를 사용 하 여 tooa 웹 응용 프로그램에 로그인 (hello 참조 [tooWeb 웹 브라우저 응용 프로그램](#web-browser-to-web-application) 위의 섹션). Hello 웹 응용 프로그램의 hello 사용자가 하지 아직 동의한 tooallowing hello 웹 응용 프로그램 toocall hello 웹 API를 대신 하는 경우 hello 사용자 tooconsent이 필요 합니다. hello 응용 프로그램, 필요한 hello 사용 권한을 나타내고 hello 디렉터리의 일반 사용자 수 tooconsent 관리자 수준 사용 권한이 이러한 경우 되지 않습니다. 이 동의 프로세스 hello 응용 프로그램에는 hello 필요한 권한을 이미 있을 것 처럼 toomulti 테 넌 트 응용 프로그램을 하지 단일 테 넌 트 응용 프로그램에만 적용 됩니다. Hello 사용자가 로그인 할 때, hello 웹 응용 프로그램 hello 사용자 인증 코드에 대 한 정보와 함께 ID 토큰을 받았습니다.
2. Hello 웹 응용 프로그램이 보내는 hello 권한 부여 코드를 포함 하는 요청 tooAzure AD의 토큰 끝점, hello 클라이언트 응용 프로그램 (응용 프로그램 ID 및 리디렉션 URI) 및 hello에 대 한 세부 정보 원하는 리소스 (Azure AD에서 발급 하는 hello 인증 코드를 사용 하 여 응용 프로그램 ID URI hello 웹 API에 대 한).
3. hello 권한 부여 코드와 hello 웹 응용 프로그램 및 web API에 대 한 정보는 Azure AD에 의해 유효성이 검사 됩니다. 유효성 검사가 성공하면 Azure AD는 JWT 액세스 토큰과 JWT 새로 고침 토큰 등 두 가지 토큰을 반환합니다.
4. HTTPS를 통해 웹 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>OAuth 2.0 인증 코드 권한을 사용한 위임된 사용자 ID
1. 사용자 인증 메커니즘이 Azure AD와 별개인 tooa 웹 응용 프로그램에 이미 로그인 했습니다.
2. hello 웹 응용 프로그램, 인증, hello 응용 프로그램 ID를 제공 하는 hello 브라우저 tooAzure AD의 권한 부여 끝점을 통해 요청을 실행 하므로, 액세스 토큰이 tooacquire 코드 및 필요 후 hello 웹 응용 프로그램에 대 한 리디렉션 URI 성공 인증입니다. hello 사용자 tooAzure AD에에서 로그인합니다.
3. Hello 웹 응용 프로그램의 hello 사용자가 하지 아직 동의한 tooallowing hello 웹 응용 프로그램 toocall hello 웹 API를 대신 하는 경우 hello 사용자 tooconsent이 필요 합니다. hello 응용 프로그램, 필요한 hello 사용 권한을 나타내고 hello 디렉터리의 일반 사용자 수 tooconsent 관리자 수준 사용 권한이 이러한 경우 되지 않습니다. 이러한 용도로 tooboth 단일 및 다중 테 넌 트 응용 프로그램을 적용합니다.  Hello 단일 테 넌 트의 경우에서 관리자가 사용자 대신 관리자 동의 tooconsent를 수행할 수 있습니다.  이렇게 hello를 사용 하 여 `Grant Permissions` hello 단추 [Azure 포털](https://portal.azure.com)합니다. 
4. Hello 사용자가 동의 hello 웹 응용 프로그램 tooacquire 액세스 토큰이 필요 함을 hello 인증 코드를 수신 합니다.
5. Hello 웹 응용 프로그램이 보내는 hello 권한 부여 코드를 포함 하는 요청 tooAzure AD의 토큰 끝점, hello 클라이언트 응용 프로그램 (응용 프로그램 ID 및 리디렉션 URI) 및 hello에 대 한 세부 정보 원하는 리소스 (Azure AD에서 발급 하는 hello 인증 코드를 사용 하 여 응용 프로그램 ID URI hello 웹 API에 대 한).
6. hello 권한 부여 코드와 hello 웹 응용 프로그램 및 web API에 대 한 정보는 Azure AD에 의해 유효성이 검사 됩니다. 유효성 검사가 성공하면 Azure AD는 JWT 액세스 토큰과 JWT 새로 고침 토큰 등 두 가지 토큰을 반환합니다.
7. HTTPS를 통해 웹 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.

#### <a name="code-samples"></a>코드 샘플
웹 응용 프로그램 tooWeb API 시나리오에 대 한 hello 코드 샘플을 참조 하세요. 자주 확인-hello 항상 새로운 샘플이 추가 합니다. 웹 [응용 프로그램 tooWeb API](active-directory-code-samples.md#web-application-to-web-api)합니다.

#### <a name="registering"></a>등록
* 단일 테 넌 트: hello 응용 프로그램 id와 위임 된 사용자 id의 경우 모두 hello 웹 응용 프로그램 및 hello에 hello web API를 등록 해야 Azure AD에서 동일한 디렉터리입니다. hello web API 구성된 tooexpose tooits 리소스에 사용 되는 toolimit hello 웹 응용 프로그램의 액세스는 권한 집합이 될 수 있습니다. 위임 된 사용자 id 유형을 사용 중인 경우 hello Azure 포털의에서 hello "tooOther 응용 프로그램 사용 권한" 드롭다운 메뉴에서 원하는 hello 권한을 tooselect hello 웹 응용 프로그램에 필요 합니다. Hello 응용 프로그램 id 유형을 사용 중인 경우에이 단계가 필요 하지 않습니다.
* 첫째, 다중 테 넌 트: hello 웹 응용 프로그램 구성 된 tooindicate hello toobe 기능 필요한 사용 권한을 되었습니다. 동의 toohello 응용 프로그램을 사용할 수 있는 tootheir 조직 하므로 하면이 관리자 사용자 또는 관리자 hello 대상 디렉터리에 필요한 사용 권한이 목록은이 대화 상자에서 표시 됩니다. 일부 응용 프로그램 hello 조직의 모든 사용자에 동의할 수 있는 사용자 수준 권한이 필요 합니다. 다른 응용 프로그램에 동의할 수 없습니다 hello 조직에 있는 사용자는 관리자 수준 사용 권한이 필요 합니다. 디렉터리 관리자만이 수준의 권한이 필요한 동의 tooapplications를 제공할 수 있습니다. Hello 사용자 또는 관리자 동의 hello 웹 응용 프로그램 및 hello web API 하는 경우는 모두 해당 디렉터리에 등록 합니다.

#### <a name="token-expiration"></a>토큰 만료
해당 권한 부여 코드 tooget JWT 액세스 토큰을 사용 하는 hello 웹 응용 프로그램 경우 JWT 새로 고침 토큰도 수신 합니다. Hello 새로 고침 토큰 사용된 toore 수 hello 액세스 토큰이 만료 되 면-않고도 toosign 다시 hello 사용자를 인증 합니다. 이 새로 고침 토큰은 사용 되는 tooauthenticate hello 사용자, 발생 하는 새 액세스에서 토큰 및 새로 고침 한 후 토큰입니다.

### <a name="daemon-or-server-application-tooweb-api"></a>디먼 또는 서버 응용 프로그램 tooWeb API
이 섹션에서는 web API에서에서 tooget 리소스를 필요로 하는 디먼 또는 서버 응용 프로그램을 설명 합니다. 두 가지 하위 시나리오 toothis 섹션에 적용 되: toocall OAuth 2.0 클라이언트 자격 증명 권한 유형을; 기반 웹 API를 필요로 하는 디먼으로 한 서버 하는 응용 프로그램 (예: web API) toocall OAuth 2.0 On-Behalf-Of 초안 사양을 기반 웹 API를 합니다.

Hello 시나리오에 대 한 디먼 응용 프로그램이 웹 API toocall 필요한 경우에 중요 한 toounderstand 몇 가지 사항입니다. 첫째, 사용자 상호 작용 hello 응용 프로그램 toohave 자체 id를 요구 하는 디먼 응용 프로그램으로 수는 없습니다. 디먼 응용 프로그램의 예는 일괄 처리 작업 또는 hello 백그라운드에서 실행 되는 운영 체제 서비스입니다. 이 유형의 응용 프로그램의 응용 프로그램 id를 사용 하 여 해당 응용 프로그램 ID, 자격 증명 (암호 또는 인증서) 및 응용 프로그램 ID URI tooAzure 광고를 제공 함으로써 액세스 토큰을 요청 합니다. 인증을 완료 한 후 hello 데몬 사용 되는 toocall hello web API가 Azure AD에서 액세스 토큰을 받습니다.

Hello 시나리오에 대 한 서버 응용 프로그램 toocall web API에 필요한 경우에 유용한 toouse 예 있습니다. 사용자가 인증 하는 네이티브 응용 프로그램에이 네이티브 응용 프로그램이 필요한 웹 API toocall 한다고 가정 합니다. Azure AD는 JWT 액세스 토큰 toocall hello web API를 발급합니다. Hello web API는 toocall 다른 다운스트림 web API를 필요한 hello에 대신-흐름 toodelegate hello 사용자 id를 사용 하 여 있고 toohello 두 번째 계층 web API를 인증 합니다.

#### <a name="diagram"></a>다이어그램
![디먼 또는 서버 응용 프로그램 API tooWeb 다이어그램](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>프로토콜 흐름 설명
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>OAuth 2.0 클라이언트 자격 증명 권한을 사용한 응용 프로그램 ID
1. 첫째, hello 서버 응용 프로그램에 대화형 로그온 대화 상자와 같은 사용자 상호 작용 없이 자체적으로 Azure AD와 tooauthenticate가 필요합니다. Hello 자격 증명, 응용 프로그램 ID 및 응용 프로그램 ID URI를 제공 하는 요청 tooAzure AD의 토큰 끝점을 만듭니다.
2. Azure AD hello 응용 프로그램을 인증 하 고는 사용 되는 toocall hello 웹 API JWT 액세스 토큰을 반환 합니다.
3. HTTPS를 통해 웹 응용 프로그램 hello hello 요청 toohello web API의 hello 권한 부여 헤더에 JWT 액세스 토큰 tooadd hello "Bearer" 라는 지정 JWT 문자열을 반환 하는 hello를 사용 합니다. hello web API 다음 hello JWT 토큰을 확인 하 고 원하는 리소스를 반환 hello 유효성 검사가 성공 하면 키를 누릅니다.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>OAuth 2.0 대리 초안 사양을 사용한 위임된 사용자 ID
아래에서 설명 하는 hello 흐름 (예: 네이티브 응용 프로그램), 다른 응용 프로그램에는 사용자가 인증 된 사용자 id에 사용 되는 tooacquire 액세스 토큰 toohello 첫 번째 계층 web API 되었습니다 되었다고 가정 합니다.

1. hello 네이티브 응용 프로그램 hello 액세스 토큰 toohello 첫 번째 계층 web을 API를 보냅니다.
2. hello 첫 번째 계층 web API hello 사용자의 액세스 토큰 뿐만 아니라 해당 응용 프로그램 ID 및 자격 증명을 제공 하는 요청 tooAzure AD의 토큰 끝점을 보냅니다. 또한 hello 요청이 함께 보내집니다는 hello를 나타내는 매개 변수 on_behalf_of 웹 API를 새로운 요청 토큰을 hello 원래 사용자 대신 toocall 다운스트림 web API입니다.
3. Azure AD 확인 하는 hello 첫 번째 계층 web API 사용 권한을 tooaccess hello 두 번째 계층 web API에 hello 요청의 유효성을 검사 JWT 액세스 토큰 및 JWT 새로 고침 토큰 toohello 첫 번째 계층 web API를 반환 합니다.
4. HTTPS를 통해 hello 첫 번째 계층 web API 호출 hello 요청에 hello 인증 헤더에 토큰 문자열 hello를 추가 하 여 두 번째 계층 web API를 hello 합니다. hello 첫 번째 계층 web API hello 액세스 토큰 및 새로 고침 토큰이 유효한 지으로 toocall hello 두 번째 계층 web API를 계속 수 있습니다.

#### <a name="code-samples"></a>코드 샘플
디먼 또는 서버 응용 프로그램 API tooWeb 시나리오에 대 한 hello 코드 샘플을 참조 하세요. 자주 확인-hello 항상 새로운 샘플이 추가 합니다. [서버 또는 데몬 응용 프로그램 tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>등록
* 단일 테 넌 트: hello 응용 프로그램 id와 위임 된 사용자 id의 경우 모두 hello 디먼 또는 서버 응용 프로그램에에서 등록 해야 hello Azure AD에서 동일한 디렉터리입니다. hello web API 구성된 tooexpose 사용된 toolimit hello 디먼 또는 서버의 tooits 리소스 액세스 권한 집합이 될 수 있습니다. 위임 된 사용자 id 유형을 사용 중인 경우 hello Azure 포털의에서 hello "tooOther 응용 프로그램 사용 권한" 드롭다운 메뉴에서 원하는 hello 권한을 tooselect hello 서버 응용 프로그램에 필요 합니다. Hello 응용 프로그램 id 유형을 사용 중인 경우에이 단계가 필요 하지 않습니다.
* 첫째, 다중 테 넌 트: hello 디먼 또는 서버 응용 프로그램 구성 된 tooindicate hello toobe 기능 필요한 사용 권한을 되었습니다. 동의 toohello 응용 프로그램을 사용할 수 있는 tootheir 조직 하므로 하면이 관리자 사용자 또는 관리자 hello 대상 디렉터리에 필요한 사용 권한이 목록은이 대화 상자에서 표시 됩니다. 일부 응용 프로그램 hello 조직의 모든 사용자에 동의할 수 있는 사용자 수준 권한이 필요 합니다. 다른 응용 프로그램에 동의할 수 없습니다 hello 조직에 있는 사용자는 관리자 수준 사용 권한이 필요 합니다. 디렉터리 관리자만이 수준의 권한이 필요한 동의 tooapplications를 제공할 수 있습니다. Hello 사용자 또는 관리자가 동의한 경우 모두 hello 웹 Api는 해당 디렉터리에 등록 합니다.

#### <a name="token-expiration"></a>토큰 만료
해당 권한 부여 코드 tooget JWT 액세스 토큰을 사용 하는 hello 첫 번째 응용 프로그램 경우 JWT 새로 고침 토큰도 수신 합니다. Hello 새로 고침 토큰 사용된 toore 수 hello 액세스 토큰이 만료 되 면-자격 증명을 확인 하지 않고 hello 사용자를 인증 합니다. 이 새로 고침 토큰은 사용 되는 tooauthenticate hello 사용자, 발생 하는 새 액세스에서 토큰 및 새로 고침 한 후 토큰입니다.

## <a name="see-also"></a>참고 항목
[Azure Active Directory 개발자 가이드](active-directory-developers-guide.md)

[Azure Active Directory 코드 샘플](active-directory-code-samples.md)

[Azure AD의 서명 키 롤오버에 대한 중요한 정보](active-directory-signing-key-rollover.md)

[Azure AD의 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)

