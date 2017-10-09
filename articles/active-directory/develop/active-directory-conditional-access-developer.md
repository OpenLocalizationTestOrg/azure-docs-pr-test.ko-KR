---
title: "Azure Active Directory 조건부 액세스에 대 한 지침 aaaDeveloper | Microsoft Docs"
description: "Azure AD 조건부 액세스를 위한 개발자 지침 및 시나리오"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Azure Active Directory 조건부 액세스를 위한 개발자 지침

Azure Active Directory (AD) 여러 가지 방법으로 toosecure 앱 제공 및 서비스를 보호 합니다.  이러한 고유한 기능 중 하나가 조건부 액세스입니다.  조건부 액세스를 사용 하면 개발자와 다양 한 방법으로 포함 하 여 엔터프라이즈 고객 tooprotect 서비스:

* Multi-Factor Authentication
* 등록 된 장치 tooaccess 특정 서비스 Intune만 허용
* 사용자 위치 및 IP 범위 제한

조건부 액세스의 hello 완전 한 기능에 자세한 내용은 참조 [hello Azure 클래식 포털에서에서 조건부 액세스](../active-directory-conditional-access.md)합니다. 

이 문서에서는 어떤 조건부 액세스 권한을 통해 toodevelopers 앱 빌드 Azure AD에 대 한 집중 합니다.  [단일](active-directory-integrating-applications.md) 및 [다중 테넌트](active-directory-devhowto-multi-tenant-overview.md) 앱과 [일반 인증 패턴](active-directory-authentication-scenarios.md)에 대한 지식이 있다고 가정합니다.

통해 대 한 사용 권한이 적용 되는 조건부 액세스 정책이 있을 수 있습니다는 리소스에 액세스할 hello 영향으로 시작 해 봅니다.  또한 hello Microsoft Graph에 액세스 하 고 Api 호출 hello에 영향을 줄 hello에-를 대신 하 여-의 흐름에서 조건부 액세스의 웹 응용 프로그램을 탐색 합니다.

## <a name="how-does-conditional-access-impact-an-app"></a>조건부 액세스가 앱에 어떤 영향을 주나요?

### <a name="app-topologies-impacted"></a>영향을 받는 앱 토폴로지

가장 일반적인 경우에 조건부 액세스는 응용 프로그램의 동작은 변경 되지 않습니다 또는 hello 개발자의 변경 내용이 필요 합니다.  일부 경우에만 요청는 서비스에 대 한 토큰을 자동으로 또는 간접적으로 응용 프로그램 응용 프로그램 필요 코드가 toohandle 조건부 액세스 "문제"를 변경 합니다.  이것은 대화형 로그인 요청을 수행하는 것처럼 간단할 수도 있습니다. 

특히 hello 다음과 같은 시나리오 사용 하려면 코드 toohandle 조건부 액세스 "문제": 

* Hello Microsoft Graph에 액세스 하는 앱
* Hello에-를 대신 하 여-의 흐름을 수행 하는 앱
* 여러 서비스/리소스에 액세스하는 앱
* ADAL.js를 사용하는 단일 페이지 앱

조건부 액세스 정책이 적용된 toohello 앱 수 있지만 수도 있습니다 적용된 tooa 웹 API 앱에 액세스 합니다. 어떻게 tooconfigure 조건부 액세스 정책을 참조 하세요에 대해 더 알아봅니다을 toolearn [Azure Active Directory 조건부 액세스 시작](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules)합니다.

Hello 시나리오에 따라 기업 고객 적용 하 고 언제 든 지 조건부 액세스 정책을 제거할 수 있습니다.  작동을 위해 사용자 응용 프로그램 toocontinue 새 정책이 적용 된 경우 순서로 tooimplement hello "챌린지" 처리를 해야 합니다. 다음 예제는 hello 챌린지 처리를 보여 줍니다. 

### <a name="conditional-access-examples"></a>조건부 액세스 예제

다른 상태 그대로 작동 하는 반면 일부 시나리오에서 코드 변경 내용을 toohandle 조건부 액세스를 해야 합니다.  다음은 hello 차이에 대 한 일부 정보를 제공 하는 조건부 액세스 toodo 다단계 인증을 사용 하는 몇 가지 시나리오입니다.

* 단일 테넌트 iOS 앱을 빌드 중이고 조건부 액세스 정책을 적용합니다.  hello 앱 사용자가 로그인 하 고 tooan API 액세스를 요청 하지 않습니다.  Hello 사용자가 로그인 hello 정책을 자동으로 호출 하며 hello 사용자 tooperform multi-factor authentication (MFA). 
* 여러 다른 서비스 hello Microsoft Graph tooaccess Exchange를 사용 하는 다중 테 넌 트 웹 앱 작성.  이 앱을 채택하는 기업 고객은 SharePoint Online에서 정책을 설정합니다.  MS 그래프에 대 한 토큰을 요청 하는 hello 웹 앱, 모든 Microsoft 서비스에 정책이 적용 됩니다 (특히 그래프를 통해 액세스할 수 있는 서비스).  이 최종 사용자에게 MFA에 대한 메시지가 표시됩니다. Hello 경우에서 hello 최종 사용자가 유효한 토큰으로 로그인, "클레임"challenge toohello 웹 응용 프로그램에 반환 됩니다.  
* 중간 계층 서비스 tooaccess hello Microsoft Graph를 사용 하는 네이티브 앱 작성.  이 앱을 사용 하 여 hello 회사 기업 고객은 정책 tooExchange을 온라인에 적용 됩니다.  최종 사용자가 로그인 하면 hello 네이티브 응용 프로그램 액세스 toohello 중간 계층을 요청 하 고 hello 토큰을 보냅니다.  hello 중간 계층에서 대신-흐름 toorequest 액세스 toohello MS 그래프를 수행합니다.  이 시점에서 클레임 "챌린지" toohello 중간 계층을 표시 됩니다. hello 중간 계층 hello 챌린지 백 toohello 수 네이티브 앱을 toocomply hello 조건부 액세스 정책 사용 하 여 필요한 보냅니다.

### <a name="complying-with-a-conditional-access-policy"></a>조건부 액세스 정책 준수

여러 가지 서로 다른 응용 프로그램 토폴로지에 대 한 조건부 액세스 정책은 hello 세션을 설정할 때 평가 됩니다.  앱 및 서비스의 hello 세분성에서 작동 하는 조건부 액세스 정책,으로 호출 됩니다는 hello 지점 따라 크게 달라 집니다 hello 시나리오에 tooaccomplish 만들려고 합니다.

앱이 tooaccess 조건부 액세스 정책 사용 하 여 서비스를 조건부 액세스 챌린지를 발생할 합니다.  이러한 문제를 인코딩하는 hello `claims` 응답 Azure AD에서 제공 되는지, 아니면 Microsoft Graph hello는 매개 변수입니다.  이 챌린지 매개 변수의 예는 다음과 같습니다. 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

개발자가 이러한 문제 걸리고 새 요청 tooAzure AD에 추가할 수 있습니다.  이 상태를 전달 hello 조건부 액세스 정책 사용 하 여 모든 작업 필요한 toocomply를 hello 최종 사용자 tooperform 묻습니다. 다음 시나리오는 hello, hello 오류 및 tooextract 매개 변수를 hello 하는 방법의 세부 사항에 설명 합니다. 

## <a name="scenarios"></a>시나리오

### <a name="prerequisites"></a>필수 조건

Azure AD 조건부 액세스는 [Azure AD Premium](../active-directory-whatis.md#choose-an-edition)에 포함된 기능입니다.  자세한 라이선스 hello에 대 한 요구 사항에 대 한 내용은 [허가 되지 않은 사용 현황 보고서](../active-directory-conditional-access-unlicensed-usage-report.md)합니다.  개발자 hello 참여 하 여 [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), 무료 구독 toohello Azure AD Premium을 포함 하는 Enterprise Mobility Suite를 포함 하는 합니다.

### <a name="considerations-for-specific-scenarios"></a>특정 시나리오에 대한 고려 사항

다음 정보에만 hello 이러한 조건부 액세스 시나리오에 적용 됩니다.

* Hello Microsoft Graph에 액세스 하는 앱
* Hello에-를 대신 하 여-의 흐름을 수행 하는 앱
* 여러 서비스/리소스에 액세스하는 앱
* ADAL.js를 사용하는 단일 페이지 앱

Hello 다음 섹션에서 살펴보겠습니다 공통으로 시나리오에는 더 복잡 합니다.  hello 핵심 원칙은 운영는 조건부 액세스 정책은 Microsoft Graph hello를 통해 액세스 하는 경우가 아니면 적용 조건부 액세스 정책이 적용 된 hello 서비스에 대 한 hello 타임 hello 토큰을 요청에 평가 됩니다.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Hello Microsoft Graph에 액세스 하는 시나리오: 응용 프로그램

이 시나리오에서는 살펴보기 hello 경우 웹 응용 프로그램 액세스 toohello Microsoft Graph를 요청 합니다. 이 경우 hello 조건부 액세스 정책은 tooSharePoint, Exchange, 또는 Microsoft Graph hello 통해 작업으로 액세스 하는 몇 가지 다른 서비스도 할당할 수 없습니다.  이 예제에서는 Sharepoint Online에 조건부 액세스 정책이 있다고 가정해 보겠습니다.

![Hello Microsoft Graph 흐름 다이어그램에 액세스 하는 응용 프로그램](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

먼저 hello 앱 권한 부여 toohello 조건부 액세스 없는 다운스트림 작업에 액세스 해야 하는 Microsoft 그래프를 요청 합니다.  정책을 호출 하지 않고 hello 요청이 성공 하 고 hello 앱 Microsoft Graph 용 토큰을 받습니다.  이 시점에서 hello 앱 hello 끝점 요청에 대 한 전달자 요청에서 hello 액세스 토큰을 사용할 수 있습니다. 이제 hello 앱은 예를 들어 Microsoft Graph의 Sharepoint Online 끝점 tooaccess가 필요합니다.`https://graph.microsoft.com/v1.0/me/mySite`

hello 앱 새 토큰을 발급 하지 않고 hello 새 요청을 수행할 수 있도록 Microsoft Graph hello에 대 한 유효한 토큰에 이미 있습니다. 이 요청이 실패 하 고 클레임 과제는 hello와 HTTP 403 금지 형식의 Microsoft Graph에서 발급 한 ```WWW-Authenticate``` 챌린지입니다.
Hello 응답의 예는 다음과 같습니다. 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

hello 클레임 과제는 hello 내 ```WWW-Authenticate``` hello 다음 요청에 대 한 구문 분석 된 tooextract hello 클레임 매개 변수로 사용할 수 있는 헤더입니다.  추가 된 toohello 새 요청 되 면 Azure AD 로그인 hello 사용자 및 hello 앱에는 이제 hello 조건부 액세스 정책을 준수 하는 경우 tooevaluate hello 조건부 액세스 정책을 알고 있습니다.  Sharepoint Online hello 요청 toohello 반복 끝점 성공 합니다.

Toohandle hello 챌린지를 요구 하는 방법을 보여 주는 코드 샘플에 대 한 참조 toohello [.NET 데스크톱 코드 샘플](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) ADAL.NET 또는 hello에 대 한 [에-를 대신 하 여-의 코드 샘플](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) ADAL.NET에 대 한 합니다.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Hello에-를 대신 하 여-의 흐름을 수행 하는 시나리오: 응용 프로그램

이 시나리오에서는 네이티브 응용 프로그램 웹 서비스/API를 호출 하는 hello 사례를 통해 안내 합니다.  이 서비스는 차례로 ["를 대신 하 여-" 흐름 hello](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall 다운스트림 서비스입니다.  경우에는에서는 조건부 액세스 정책 toohello 다운스트림 서비스 (Web API 2) 적용 하 고 서버/디먼 응용 프로그램 보다는 네이티브 응용 프로그램을 사용 하는 합니다. 

![Hello에-를 대신 하 여-의 흐름 다이어그램을 수행 하는 응용 프로그램](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

Web API 1 hello 다운스트림 API를 항상 적중 수 대로 hello 초기 토큰 요청 웹 API 1에 대 한 다단계 인증에 대 한 hello 최종 사용자를 표시 하지 않습니다.  Web API 2에 대 한 토큰에-를 대신 하 여-의 hello 사용자 toorequest를 시도 하는 Web API 1, 되 면 hello 사용자가 다단계 인증을 사용 하 여 로그인 하지 이후 hello 요청이 실패 합니다.

Azure AD는 몇 가지 흥미로운 데이터가 포함된 HTTP 응답을 반환합니다. 

> [!NOTE]
> 이 인스턴스가 다단계 인증 오류 설명, 표시 되지만 다양 한 범위의 `interaction_required` 가능한와 관련 된 tooconditional 액세스 합니다.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

이 웹 API 1에 hello 오류를 catch `error=interaction_required`, 백 hello 보내고 `claims` 챌린지 toohello 데스크톱 응용 프로그램입니다.  Hello를 데스크톱 응용 프로그램을 새 만들 수 해당 시점에 `acquireToken()` 호출 및 hello 추가 `claims`추가 쿼리 문자열 매개 변수로 챌린지입니다.  이 새 요청 hello 사용자 toodo 다단계 인증이 필요 하 고이 새 토큰 백 tooWeb API 1 및 전체 hello에-를 대신 하 여-의 흐름을 보냅니다.

이 시나리오에서는 아웃 tootry 참조 우리의 [.NET 코드 샘플](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca)합니다.  Toopass Web API 1 toohello 네이티브 응용 프로그램에서 다시 클레임 챌린지 hello 하 고 hello 클라이언트 응용 프로그램 안에 새 요청을 생성 하는 방법을 보여 줍니다. 

### <a name="scenario-app-accessing-multiple-services"></a>시나리오: 여러 서비스에 액세스하는 앱

이 시나리오에서는 할당 된 조건부 액세스 정책이 있고이 중 한 hello 경우 웹 응용 프로그램 두 서비스를 액세스 하는 연습입니다.  사용자 응용 프로그램 논리에 따라 응용 프로그램 액세스 tooboth 웹 서비스 필요 하지 않는 경로 있을 수 있습니다.  이 시나리오에서는 토큰을 요청 하는 hello 순서 hello 최종 사용자 환경에서 중요 한 역할을 재생 합니다.

웹 서비스 A와 B가 있고 웹 서비스 B에 조건부 액세스 정책이 적용되었다고 가정해 보겠습니다.  두 서비스에 대 한 승인 해야 하는 hello 대화형 초기 인증 요청을 하는 동안 hello 조건부 액세스 정책은 모든 경우에에서 필요 하지 않습니다.  Hello 앱 웹 서비스 B에 대 한 토큰을 요청 하는 경우 hello 정책 호출 되 고 웹 서비스 A에 대 한 후속 요청에도 다음과 같이 성공 하는 것입니다.

![여러 서비스 흐름에 액세스하는 앱 다이어그램](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

또는 처음 hello 앱 웹 서비스 A에 대 한 토큰을 요청을 하는 경우 hello 최종 사용자 hello 조건부 액세스 정책을 호출 하지 않습니다.  이 통해 hello 앱 개발자 toocontrol hello 최종 사용자 환경을 고쳐지지 hello 조건부 액세스 정책 toobe 모든 경우에에서 호출 됩니다. hello 까다로운 사례는 hello 앱 이후에 B. 웹 서비스에 대 한 토큰을 요청 하는 경우 이 시점에서 hello 최종 사용자는 hello 조건부 액세스 정책 사용 하 여 toocomply가 필요합니다.  Hello 앱 잠그려고 할 때이 너무`acquireToken`, hello 다음 오류가 (다이어그램을 다음 hello에 그림 참조)를 생성할 수 있습니다. 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![새 토큰을 요청하는 여러 서비스에 액세스하는 앱](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Hello 앱 hello ADAL 라이브러리를 사용 하는 오류 tooacquire hello 토큰을 대화형으로 다시 시도 항상 됩니다.  이 대화형 요청 발생 hello 최종 사용자에 hello 기회 toocomply hello 조건부 액세스와 함께 포함 됩니다.  표시 되지 않으면 true hello 요청은 한 `AcquireTokenSilentAsync` 또는 `PromptBehavior.Never` hello 앱 tooperform는 대화형이 필요한 경우 ```AcquireToken``` hello 정책과 toogive hello 최종 사용 hello 기회 toocomply를 요청 합니다. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>시나리오: ADAL.js를 사용하는 SPA(단일 페이지 앱)

이 시나리오에서는 단일 페이지 응용 프로그램 (SPA)이 발생 한 경우 hello 경우 진행, ADAL.js toocall를 사용 하 여 조건부 액세스 웹 API를 보호 합니다.  이 간단한 아키텍처는 아니지만 toobe 조건부 액세스 관련 한 개발 때 적용 해야 하는 몇 가지 갖는 했습니다.

ADAL.js에는 토큰을 얻기 위핸 몇 가지 함수가 있습니다(예: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)` 및 `acquireTokenRedirect(…)`). 

* `login()`은 대화형 로그인 요청을 통해 ID 토큰을 가져오지만 조건부 액세스 보호되는 Web API를 비롯한 모든 서비스에 대한 액세스 토큰을 가져오지는 않습니다  
* `acquireToken(…)`그런 다음 수 사용된 toosilently 토큰을 가져올 수 액세스 의미 UI 어떠한 경우에는 표시 되지 않습니다.  
* `acquireTokenPopup(…)`및 `acquireTokenRedirect(…)` 모두 사용 되는 toointeractively 로그인 UI를 항상 표시를 의미 하는 리소스에 대 한 토큰을 요청 됩니다.

응용 프로그램 액세스 토큰 toocall 웹 API를 필요한 때 프로젝트는 `acquireToken(…)`합니다.  Hello 토큰 세션은 만료 또는 조건부 액세스 정책 사용 하 여 toocomply 필요 하는 경우 다음 hello *acquireToken* 실패 함수를 사용 하 여 응용 프로그램 hello `acquireTokenPopup()` 또는 `acquireTokenRedirect()`합니다.

![ADAL 흐름을 사용하는 단일 페이지 앱 다이어그램](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

이제 조건부 액세스 시나리오에 대한 예를 살펴보겠습니다.  방금 hello 최종 사용자는 hello 사이트 착륙 하 고 세션 없는 경우.  `login()` 호출을 수행하면 다단계 인증 없이 ID 토큰을 가져옵니다.  다음 hello 사용자 hello 앱 toorequest 데이터 웹 API에서 필요로 하는 단추를 누르면 됩니다.  hello 앱 toodo 시도 `acquireToken()` hello 사용자 multi-factor authentication에 아직 수행 하지 않았습니다 고 hello 조건부 액세스 정책 사용 하 여 toocomply 필요 하지만 호출에 실패 합니다.

Azure AD에서 뒤로 hello 다음 HTTP 응답을 보냅니다. 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

앱 요구 toocatch hello `error=interaction_required`합니다.  hello 응용 프로그램 다음 하나를 사용할 수 `acquireTokenPopup()` 또는 `acquireTokenRedirect()` 에 동일한 hello 리소스입니다.  hello 사용자가 multi-factor authentication 강제 toodo입니다. Hello 앱 새 발급 hello 사용자 hello 다단계 인증을 완료 한 후 hello에 대 한 액세스 토큰 요청 된 리소스입니다.

이 시나리오에서는 아웃 tootry 참조 우리의 [JS SPA에-를 대신 하 여-의 코드 샘플](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca)합니다.  이 코드 예제는 hello 조건부 액세스 정책 및 web API 이전에 등록 JS SPA toodemonstrate이이 시나리오를 사용 합니다. Tooproperly 핸들 hello 클레임의 인증 및 웹 API에 대 한 사용할 수 있는 액세스 토큰을 가져오는 방법을 보여 줍니다. 체크 아웃 hello 또는 일반 [Angular.js 코드 샘플](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) 각도 SPA에 대 한 지침


## <a name="see-also"></a>참고 항목

* hello 기능에 대해 자세히 toolearn 참조 [Azure AD에서 조건부 액세스](../active-directory-conditional-access.md)합니다.
* 더 많은 Azure AD 샘플 코드를 보려면 [샘플의 Github 리포지토리](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory)를 참조하세요. 
* Hello ADAL SDK 및 액세스 hello 참조 설명서에 대 한 자세한 내용은 참조 하십시오. [라이브러리 가이드](active-directory-authentication-libraries.md)합니다.
* 다중 테 넌 트 시나리오에 대해 자세히 toolearn 참조 [어떻게 toosign hello 다중 테 넌 트 패턴을 사용 하 여 사용자의](active-directory-devhowto-multi-tenant-overview.md)합니다.
