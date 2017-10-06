---
title: "모든 Azure AD 사용자를 로그인 할 수 있는 앱 aaaHow toobuild | Microsoft Docs"
description: "모든 Azure Active Directory 테넌트로부터 사용자를 로그인할 수 있게 하는 응용 프로그램(또는 다중 테넌트 응용 프로그램으로 알려짐)을 빌드하기 위한 단계별 지침."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>어떻게 사용 하 여 모든 Azure AD (Active Directory) 사용자의 toosign hello 다중 테 넌 트 응용 프로그램 패턴
소프트웨어 서비스 응용 프로그램 toomany로 조직을 제공 하면 응용 프로그램 tooaccept에서에서 로그인 한 Azure AD 테 넌 트를 구성할 수 있습니다.  Azure AD에서는 이를 두고 다중 테넌트 응용 프로그램을 만드는 것이라고 합니다.  모든 Azure AD 테 넌 트의 사용자가 후 tooyour 응용 프로그램에 수 toosign 됩니다 toouse 자신의 계정으로 응용 프로그램을 승인 합니다.  

기존 응용 프로그램에 자체 계정 시스템이 있거나 다른 클라우드 공급자에서 비롯된 다른 종류의 로그인을 지원하는 경우 테넌트의 Azure AD 로그인을 간단하게 추가할 수 있습니다. 앱을 등록하고 OAuth2, OpenID Connect 또는 SAML을 통해 로그인 코드를 추가하고 응용 프로그램에 "Microsoft를 사용하여 로그인" 단추를 배치합니다. 다음 응용 프로그램 브랜딩에 관한 자세한 단추 toolearn hello를 클릭 합니다.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

이 문서에서는 사용자가 Azure AD에 대한 단일 테넌트 응용 프로그램을 빌드하는 것에 이미 익숙하다고 가정합니다.  H e a d toohello 수 없다면 백업 [개발자 가이드 홈 페이지] [ AAD-Dev-Guide] 우리의 빠른 시작 중 하나를 시도 하 고!

응용 프로그램을 Azure AD 다중 테 넌 트 앱에는 네 가지 간단한 단계만 거치면 tooconvert:

1. 응용 프로그램 등록 toobe 다중 테 넌 트를 업데이트 합니다.
2. 프로그램 코드 toosend 요청 toohello 함께 사용할 수 업데이트 끝점 
3. 코드 toohandle 여러 발급자 값 업데이트
4. 사용자 및 관리자 동의를 이해하고 적절한 코드 변경을 합니다.

각 단계를 자세히 살펴보겠습니다. 너무 바로 이동할 수도 있습니다[이 다중 테 넌 트 예제이 목록은][AAD-Samples-MT]합니다.

## <a name="update-registration-toobe-multi-tenant"></a>등록 toobe 다중 테 넌 트를 업데이트 합니다.
기본적으로 Azure AD에서 웹앱/API 등록은 단일 테넌트입니다.  Hello "다중 테 넌 트" 스위치 hello에 응용 프로그램 등록의 hello 속성 페이지에 검색 하 여 다중 테 넌 트 등록을 만들 수 [Azure 포털] [ AZURE-portal] 너무 "Yes" 설정 합니다.

또한 참고, 다중 테 넌 트 응용 프로그램 설정 하기 전에 Azure AD에서는 hello hello 응용 프로그램 toobe 전역적으로 고유의 앱 ID URI입니다. 앱 ID URI hello hello 방법으로 응용 프로그램은 프로토콜 메시지에 멤버 중 하나입니다.  단일 테 넌 트 응용 프로그램은 해당 테 넌 트 내에서 고유 hello 앱 ID URI toobe 충분 합니다.  다중 테 넌 트 응용 프로그램에 대 한 전역적으로 고유 해야 Azure AD는 모든 테 넌 트 간에 hello 응용 프로그램을 찾을 수 있도록 합니다.  Hello 앱 ID URI toohave hello Azure AD 테 넌 트의 확인 된 도메인을 일치 하는 호스트 이름을 요구 하 여 전역 고유성이 적용 됩니다.  예를 들어 테 넌 트의 hello 이름에서 경우 contoso.onmicrosoft.com 유효한 앱 ID URI 것 `https://contoso.onmicrosoft.com/myapp`합니다.  테넌트가 확인된 도메인 `contoso.com`를 가진 경우, 유효한 앱 ID URI은 또한 `https://contoso.com/myapp`이 됩니다.  다중 테 넌 트로 응용 프로그램을 설정 하면 hello 앱 ID URI는이 패턴을 따르지 않는 경우 실패 합니다.

기본 클라이언트 등록은 기본적으로 다중 테넌트입니다.  모든 작업 toomake 네이티브 클라이언트 응용 프로그램 등록 다중 테 넌 트 tootake을 필요 하지 않습니다.

## <a name="update-your-code-toosend-requests-toocommon"></a>프로그램 코드 toosend 요청 너무/공통 업데이트
단일 테 넌 트 응용 프로그램에서 로그인 요청 toohello 테 넌 트의 로그인 끝점으로 전송 됩니다. 예를 들어 contoso.onmicrosoft.com에 대 한 hello 끝점이 합니다.

    https://login.microsoftonline.com/contoso.onmicrosoft.com

요청 전송 tooa 테 넌 트의 끝점에서 해당 테 넌 트에 해당 테 넌 트 tooapplications 사용자 (또는 게스트)에 서명할 수 있습니다.  다중 테 넌 트 응용 프로그램을 hello 응용 프로그램 인식 하지 들겠지만 tooa 테 넌 트의 끝점을 보낼 수 없습니다, 어떤 테 넌 트 hello 사용자가 요청 합니다.  대신 요청에는 모든 Azure AD 테 넌 트 간에 멀티플렉싱 tooan 끝점을 전송 됩니다.

    https://login.microsoftonline.com/common

Azure AD hello에 대 한 요청을 받을 때 공용 끝점 hello 사용자가 로그인 하 고 테 넌 트 hello 사용자를 검색 하는 경우에 나타나는 결과에서 / 합니다.  hello 모든 Azure AD에서 지 원하는 hello 인증 프로토콜 함께 작동 하는 일반 끝점이 /: OpenID Connect, OAuth 2.0, SAML 2.0 및 WS-페더레이션 합니다.

hello 로그인 응답 toohello 그런 다음 응용 프로그램 hello 사용자를 나타내는 토큰을 포함 합니다.  hello 토큰에서 발급자 값 hello에서 어떤 테 넌 트 hello 사용자가을 응용 프로그램에 지시 합니다.  Hello에서 응답이 반환/경우 일반 끝점이 hello 토큰에서 발급자 값 hello toohello 사용자의 테 넌 트에 해당 됩니다.  중요 한 toonote hello/일반 끝점이 테 넌 트가 아닙니다 아니며 발급자에 방금 멀티플렉서 합니다.  함께 사용할 수를 사용할 때 응용 프로그램 toovalidate 토큰에 hello 논리 필요 업데이트 toobe tootake이을 고려 합니다. 

앞에서 언급 한, 다중 테 넌 트 응용 프로그램 사용자에 대 한 일관 된 로그인 환경을 제공 해야,으로 다음 hello 브랜딩 지침 Azure AD 응용 프로그램입니다. 다음 응용 프로그램 브랜딩에 관한 자세한 단추 toolearn hello를 클릭 합니다.

[![Sign in button][AAD-Sign-In]][AAD-App-Branding]

Hello 함께 사용할 수의 hello 사용에 살펴보겠습니다 끝점과 자세히 코드 구현 합니다.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>코드 toohandle 여러 발급자 값 업데이트
웹 응용 프로그램 및 웹 API는 Azure AD에서 토큰을 받아 유효성을 검사합니다.  

> [!NOTE]
> 따라서 toosend 것을 요청 하 고 Azure AD에서 토큰을 수신 하는 네이티브 클라이언트 응용 프로그램, 하는 유효성 검사 tooAPIs 합니다.  네이티브 응용 프로그램은 토큰의 유효성을 검사하지 않으며 그것을 불투명한 것으로 처리해야 합니다.
> 
> 

응용 프로그램이 Azure AD에서 수신한 토큰의 유효성을 검사하는 방법을 살펴보겠습니다.  단일 테넌트 응용 프로그램은 일반적으로 다음과 같은 끝점 값을 취합니다.

    https://login.microsoftonline.com/contoso.onmicrosoft.com

고 tooconstruct 같은 (이 경우, OpenID Connect)에서 메타 데이터 URL을 사용 합니다.

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

두 toodownload 중요 한 정보가 사용 되는 toovalidate 토큰 있는: hello 테 넌 트의 서명 키 및 발급자 값입니다.  각 Azure AD 테 넌 트는 hello 폼의 고유한 발급자 값:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

여기서 hello GUID 값이 hello 테 넌 트의 테 넌 트 id hello hello 이름 바꾸기 스레드로부터 안전한 버전입니다.  Hello 앞에 대 한 메타 데이터 링크를 클릭할 경우 `contoso.onmicrosoft.com`, hello 문서에서 발급자 값이 볼 수 있습니다.

단일 테 넌 트 응용 프로그램 토큰의 유효성을 검사, 서명 hello 메타 데이터 문서에서 키 hello에 대 한 hello 토큰의 hello 서명을 확인 합니다. 이렇게 하면 해당 toomake 있는지 hello 발급자 값 hello 토큰 일치 hello 하나 hello 메타 데이터 문서에서 찾을 수 있습니다.

Hello 이후/공통 끝점 tooa 테 넌 트와 일치 하지 않으면 같고, 실제 값 대신 템플릿 기반 URL에 일반적인/hello 발급자 값에 대 한 hello 메타 데이터를 검사 하는 경우 발급자에 없습니다.

    https://sts.windows.net/{tenantid}/

따라서 다중 테 넌 트 응용 프로그램 수 없는 토큰 유효성을 검사 hello로 hello 메타 데이터에 hello 발급자 값과 비교 하 여 `issuer` hello 토큰에는 값입니다.  다중 테 넌 트 응용 프로그램 논리 toodecide 어떤 발급자 값이 유효한 및를 하지에 필요한 ID 부분의 hello 발급자 값 hello 테 넌 트에 따라 합니다.  

예를 들어, 다중 테 넌 트 응용 프로그램의 서비스에 대 한 등록 특정 테 넌 트 로부터 로그인만 허용, 다음 해야 확인 고 hello 발급자 값 또는 hello `tid` 클레임 값의 목록에 해당 테 넌 트 인지 토큰 toomake hello에 구독자입니다.  다중 테 넌 트 응용 프로그램만 개인 다루는 및 테 넌 트에 따라 모든 액세스 결정을 확인 하지 않습니다, 다음 무시 해도 hello 발급자 값 모두 합니다.

Hello에 다중 테 넌 트 예제 hello에에서 [관련 콘텐츠](#related-content) 이 문서에서 발급자 유효성 검사의 hello 끝 섹션은 사용할 수 없는 tooenable에 모든 Azure AD 테 넌 트 toosign 합니다.

이제 toomulti 테 넌 트 응용 프로그램에 로그인 하는 사용자에 대 한 hello 사용자 환경에 살펴보겠습니다.

## <a name="understanding-user-and-admin-consent"></a>사용자 및 관리자 동의 이해하기
Azure AD에서 tooan 응용 프로그램에서 사용자 toosign, hello 사용자의 테 넌 트의 hello 응용 프로그램을 나타내야 합니다.  이렇게 하면 hello 조직 toodo 등 자신의 테 넌 트의 사용자 toohello 응용 프로그램에 로그인 할 때 고유 정책을 적용 합니다.  단일 테 넌 트 응용 프로그램의 경우이 등록은 간단 합니다. hello에 hello 응용 프로그램을 등록할 때 발생 하는 하나 hello에 그 [Azure 포털][AZURE-portal]합니다.

다중 테 넌 트 응용 프로그램에 대 한 hello 응용 프로그램에 대 한 초기 등록 hello hello 개발자가 사용 되는 hello Azure AD 테 넌 트에 거주 하 고 있습니다.  다른 테 넌 트의 사용자가 처음으로 hello에 대 한 toohello 응용 로그인 하도록 Azure AD에 hello 응용 프로그램에서 요청한 tooconsent toohello 권한과 요청 합니다.  동의 될 경우 hello 응용 프로그램에 대 한 표현을 호출는 *서비스 사용자* 에서 만든, 사용자의 테 넌 트 hello 및 로그인 계속할 수 있습니다. 한 위임은 hello 사용자의 동의 toohello 응용 프로그램을 기록 하는 hello 디렉터리에 만들어집니다. 참조 [응용 프로그램 개체 및 서비스 주체 개체] [ AAD-App-SP-Objects] hello 응용 프로그램의 응용 프로그램과 ServicePrincipal 개체와 다른 tooeach 관계에 대 한 자세한 내용은 합니다.

![동의 toosingle 계층 응용 프로그램][Consent-Single-Tier] 

이 승인 환경이 hello 응용 프로그램에서 요청한 hello 권한과에 의해 결정 됩니다.  Azure AD에서는 응용 프로그램 전용과 위임이란 두 유형의 사용 권한을 지원합니다.

* 위임 된 권한 hello 작업 hello 사용자의 하위 집합에 대 한 로그인된 한 사용자 수와 마찬가지로 응용 프로그램 hello 기능 tooact를 부여 합니다.  예를 들어 사용자의 일정에는 응용 프로그램 hello 위임 된 권한 tooread hello를 부여할 수 있습니다.
* Hello 응용 프로그램의 toohello id는 응용 프로그램 전용 사용 권한 직접 부여 됩니다.  예를 들어 toohello 응용 프로그램에 서명한에 관계 없이 테 넌 트의 사용자는 응용 프로그램 hello 응용 프로그램 전용 권한 tooread hello 목록을 부여할 수 있습니다.

일부 사용 권한이 다른 테 넌 트 관리자 동의 해야 하는 동안 승인된 tooby 일반 사용자를 수 있습니다. 

### <a name="admin-consent"></a>관리자 동의
응용 프로그램 전용 권한은 테넌트 관리자의 동의를 항상 필요로 합니다.  응용 프로그램에 응용 프로그램 전용 권한을 요청 하는 경우 사용자가 toohello 응용 프로그램에서 toosign hello 사용자 수 tooconsent가 아니면 없다는 오류 메시지가 표시 됩니다.

위임된 특정 권한은 또한 테넌트 관리자의 동의를 필요로 합니다.  예를 들어 hello 기능 toowrite 백 tooAzure AD hello 사용자 로그인으로 테 넌 트 관리자의 동의가 필요 합니다.  응용 프로그램 전용 사용 권한과 마찬가지로 일반 사용자가이 toosign tooan 응용 프로그램에 관리자의 승인이 필요한 위임 된 권한을 요청 하는 응용 프로그램 오류가 발생 합니다.  사용 권한 필요 여부 관리 동의가 hello 리소스를 게시 하는 hello 개발자가 결정 되며, hello 리소스에 대 한 hello 설명서에서 찾을 수 있습니다.  Tootopics hello에 대 한 hello Azure AD Graph API 및 Microsoft Graph API는 hello 사용할 수 있는 권한을 설명 하는 링크 [관련 콘텐츠](#related-content) 이 문서의 섹션.

응용 프로그램에 관리 동의가 필요한 사용 권한에 사용, 예: 단추 또는 링크 admin 님 안녕하세요 hello 작업을 시작할 수 있는 제스처 toohave를 해야 합니다.  응용 프로그램에서이 작업은 일반적인 OAuth2/OpenID Connect 권한 부여 요청을 하지만 hello 포함 된 hello 요청 `prompt=admin_consent` 쿼리 문자열 매개 변수입니다.  Admin 님 안녕하세요가 동의 하 고 hello 서비스 사용자는 hello 고객의 테 넌 트에서 만든을 후속 로그인 요청 불필요 hello `prompt=admin_consent` 매개 변수입니다. 관리자에 게 hello 요청한 사용 권한은 허용 하기로 결정 했습니다, 이후 해당 위치 다음부터 동의 hello 테 넌 트의 사용자를 입력 합니다.

hello `prompt=admin_consent` 매개 변수 관리 동의가 필요 하지 않은 사용 권한을 요청 하는 응용 프로그램에서 사용할 수도 있습니다. 이 작업은 수행 hello 응용 프로그램 경험을 해야 하는 경우 여기서 테 넌 트 admin 님 안녕하세요 "등록"에 해당 지점에서 동의 시간과 다른 사용자가 입력 하나입니다.

하는 경우 응용 프로그램 관리 동의가 필요 하 고 관리자에 있지만 hello 서명 `prompt=admin_consent` 매개 변수는 전송 되지 않습니다, admin 님 안녕하세요 toohello 응용 프로그램 타고 성공적으로 **해당 사용자 계정에 대해서만**합니다.  일반 사용자 여전히 됩니다에 수 toosign 및 동의 toohello 응용 프로그램.  Toogive hello 테 넌 트 관리자 hello 기능 tooexplore 다른 사용자가 액세스를 허용 하기 전에 응용 프로그램을 지정할 경우에 유용 합니다.

테 넌 트 관리자는 일반 사용자 tooconsent tooapplications에 대 한 hello 기능을 해제할 수 있습니다.  이 기능을 비활성화 한 경우 관리 동의가 항상 hello 응용 프로그램 toobe hello 테 넌 트의 설정에 대 한 필요 합니다.  Tootest 일반 사용자가 동의 하면 응용 프로그램에 사용 하지 않도록 설정 하려는 경우에서 찾을 수 있습니다 hello 구성 스위치 hello Azure AD 테 넌 트 구성 섹션의 hello [Azure 포털][AZURE-portal]합니다.

> [!NOTE]
> 일부 응용 프로그램 원하는 경험 여기에서 일반 사용자 수 tooconsent을 처음에 하 고 이후 hello 응용 프로그램 관리자에 게 요청 하는 사용 권한과 관리 동의가 필요 사용 될 수 있습니다.  에 없는 경우 없는 방식으로 toodo이와 단일 응용 프로그램을 등록 하는 Azure AD 오늘  예정 된 Azure AD hello v2 끝점 사용 하면 응용 프로그램 런타임 시 toorequest 사용 권한을 대신이 시나리오를 가능 하 게 등록 시.  자세한 내용은 참조 hello [Azure AD 응용 프로그램 모델 v2 개발자 가이드][AAD-V2-Dev-Guide]합니다.
> 
> 

### <a name="consent-and-multi-tier-applications"></a>동의 및 다중 계층 응용 프로그램
응용 프로그램은 여러 계층을 가질 수 있으며, 각 계층은 Azure AD에서 자체 등록에 의해 표현될 수 있습니다.  예를 들어, 웹 API를 호출하는 네이티브 응용 프로그램 또는 웹 API를 호출하는 웹 응용 프로그램.  두이 경우 모두 hello 클라이언트 (예: 네이티브 응용 프로그램 또는 웹 응용 프로그램) 권한 toocall hello 리소스 (web API)를 요청합니다.  Hello 클라이언트 toobe 고객의 테 넌 트에 성공적으로 승인에 대 한 사용 권한을 요청 하는 모든 리소스 toowhich hello 고객의 테 넌 트에 이미 있어야 합니다.  이 조건이 충족 되지 않으면 Azure AD 리소스 hello 하는 오류를 가장 먼저 추가 해야 반환 됩니다.

**단일 테넌트의 여러 계층**

논리 응용 프로그램이 예를 들어 별도의 클라이언트와 리소스와 같은 두 개 이상의 응용 프로그램 등록으로 구성되어 있다면 이것이 문제일 수 있습니다.  어떻게 할까요 hello 리소스 hello 고객 테 넌 트에 첫 번째?  한 번에 승인할 리소스 toobe 및 azure AD 클라이언트를 사용 하 여이 사례를 다룹니다. hello hello hello 클라이언트와 hello 동의 페이지에서 리소스에서 요청한 hello 권한과의 총 합계 표시 됩니다.  tooenable이이 동작을 hello 리소스의 응용 프로그램 등록으로 hello 클라이언트 앱 ID를 포함 해야 합니다는 `knownClientApplications` 의 응용 프로그램 매니페스트에 합니다.  예:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Hello 리소스를 통해이 속성을 업데이트할 수 [응용 프로그램 매니페스트에서][AAD-App-Manifest]합니다. 다중 계층 네이티브 클라이언트 hello에 웹 API 샘플 호출에서이 확인할 [관련 콘텐츠](#related-content) hello이이 문서의 뒷부분에 나오는 섹션. hello 다음 다이어그램에서는 간략하게 동의 단일 테 넌 트에 등록 하는 다중 계층 응용 프로그램에 대 한:

![동의 toomulti 계층 알려진된 클라이언트 응용 프로그램][Consent-Multi-Tier-Known-Client] 

**다중 테넌트의 여러 계층**

비슷한 경우 hello 다양 한 계층 응용 프로그램의 다른 테 넌 트에 등록 된 경우 발생 합니다.  예를 들어 hello Office 365 Exchange Online API를 호출 하는 네이티브 클라이언트 응용 프로그램을 구축 hello 대/소문자를 것이 좋습니다.  toodevelop hello 네이티브 응용 프로그램에서는, 및 이후 고객의 테 넌 트의 네이티브 응용 프로그램 toorun hello에 대 한 서비스 사용자를 Exchange Online hello 있어야 합니다.  이 경우 hello 개발자와 고객 구입 해야 Exchange Online에 대 한 테 넌 트에서 만든 hello 서비스 보안 주체 toobe 합니다.  

Microsoft 이외의 조직으로 작성 된 API의 hello 대/소문자를 hello API의 hello 개발자가 자신의 고객의 테 넌 트에 고객 tooconsent hello 응용 프로그램에 대 한 tooprovide 방식으로 제공 되어야 합니다. hello 등록 웹 클라이언트 tooimplement으로도 사용할 수 있도록 hello 3rd 파티 개발자 toobuild hello API에 대 한 디자인은 하는 것이 좋습니다.

1. Hello에 따라 이전 섹션에서는 tooensure hello API 구현 hello 다중 테 넌 트 응용 프로그램 등록/코드 요구 사항
2. 또한 역할/tooexposing hello API의 범위 확인 hello 등록 hello에 포함 됩니다. "에 로그인 및 사용자 프로필 읽기" Azure AD 권한 (기본적으로 제공 됨)
3. 로그인-에/등록 페이지 hello 웹 클라이언트에서 다음 hello 구현 [관리 동의가](#admin-consent) 이전에 설명한 지침 
4. Hello 사용자가 toohello 응용 프로그램을 승인 되 면 hello 서비스 보안 주체와 동의 위임 링크에 테 넌 트 만들어지며 hello 네이티브 응용 프로그램 API hello에 대 한 토큰을 가져올 수 있습니다.

다이어그램을 다음 hello 다른 테 넌 트에 등록 하는 다중 계층 응용 프로그램에 대 한 동의 대 한 개요를 제공 합니다.

![동의 toomulti 계층 다자간 응용 프로그램][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>동의 취소
사용자와 관리자가 언제 든 지 동의 tooyour 응용 프로그램을 취소할 수 있습니다.

* 사용자가 revoke 액세스 tooindividual 응용 프로그램에서 제거 하 여 자신의 [액세스 패널 응용 프로그램] [ AAD-Access-Panel] 목록입니다.
* 관리자의 hello hello Azure AD 관리 섹션을 사용 하 여 Azure AD에서 제거 하 여 액세스 tooapplications 해지 [Azure 포털][AZURE-portal]합니다.

관리자가 테 넌 트의 모든 사용자에 대 한 tooan 응용 프로그램을 승인 하는 경우 사용자가 액세스를 개별적으로 취소할 수 없습니다.  관리자에 게 액세스를 취소할 수 있습니다 및 hello 전체 응용 프로그램에 대해서만 합니다.

### <a name="consent-and-protocol-support"></a>동의 및 프로토콜 지원
동의 hello OAuth, OpenID Connect를 통해 Azure AD에서 지원, Ws-federation 및 SAML 프로토콜입니다.  hello Ws-federation 및 SAML 프로토콜 지원 하지 않는 hello `prompt=admin_consent` 관리 동의가 OAuth 및 OpenID Connect를 통해 가능만 이므로 매개 변수입니다.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>다중 테넌트 응용 프로그램및 액세스 토큰 캐시
다중 테 넌 트 응용 프로그램 액세스 토큰 toocall Azure AD로 보호 되는 Api를 가져올 수 있습니다.  다중 테 넌 트 응용 프로그램을 Active Directory 인증 라이브러리 (ADAL) hello를 사용 하는 경우 발생 하는 일반적인 오류 tooinitially 함께 사용할 수를 사용 하 여 사용자에 대 한 토큰 요청, 응답을 받는 설정한 다음도 함께 사용할 수를 사용 하 여 같은 사용자에 대 한 후속 토큰을 요청 합니다.  이후 Azure AD에서 hello 응답 하지는 테 넌 트에서 / 공통, ADAL hello 테 넌 트의 것으로 hello 토큰을 캐시 합니다. 후속 hello/공통 너무 tooget hello 사용자 누락 hello 캐시 항목 및 hello 사용자에 대 한 액세스 토큰에서 증명된 toosign를 다시 호출 합니다.  tooavoid 누락 하는 hello 캐시는 이미 로그인된 한 사용자에 대 한 확인 되었는지 후속 호출은 toohello 테 넌 트의 끝점을 이루어집니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 방법에 대해 배웠습니다 toobuild 모든 Azure Active Directory 테 넌 트에서 사용자를 로그인 할 수 있는 응용 프로그램입니다. 앱과 Azure Active Directory 간에 Single Sign-on 사용 하도록 설정한 후 사용자 응용 프로그램 tooaccess Office 365와 같은 Microsoft 리소스에 의해 노출 된 Api를 업데이트할 수 있습니다. 따라서를 제공할 수 있습니다는 개인화 된 환경을 응용 프로그램의 예를 들어 toohello 사용자에 게 자신의 프로필 사진 또는 다음 일정 약속의 컨텍스트 정보를 표시 합니다. API 만들기에 대해 자세히 toolearn tooAzure Active Directory를 호출 하 고 Exchange, SharePoint, OneDrive, OneNote, Planner, Excel 등, Office 365 서비스 방문: [Microsoft Graph API][MSFT-Graph-overview]합니다.


## <a name="related-content"></a>관련 콘텐츠
* [다중 테넌트 응용 프로그램 샘플][AAD-Samples-MT]
* [응용 프로그램에 대한 브랜딩 지침][AAD-App-Branding]
* [Azure AD 개발자 가이드][AAD-Dev-Guide]
* [응용 프로그램 개체 및 서비스 주체 개체][AAD-App-SP-Objects]
* [Azure Active Directory와 응용 프로그램 통합][AAD-Integrating-Apps]
* [Hello 동의 프레임 워크 개요][AAD-Consent-Overview]
* [Microsoft Graph API 권한 범위][MSFT-Graph-permision-scopes](영문)
* [Azure AD Graph API 권한 범위][AAD-Graph-Perm-Scopes]

다음 설명 섹션 tooprovide 피드백 hello를 사용 하 고 구체화 하 고 콘텐츠를 셰이핑 하는 데 도움이 하십시오.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














