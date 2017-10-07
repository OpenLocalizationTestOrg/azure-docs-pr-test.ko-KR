---
title: "Azure Active Directory B2C: 응용 프로그램 등록 | Microsoft Docs"
description: "어떻게 tooregister 응용 프로그램을 Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: 응용 프로그램 등록

이 Quickstart를 통해 몇 분 이내에 Microsoft Azure Active Directory(Azure AD) B2C 테넌트에서 응용 프로그램을 등록할 수 있습니다. 완료 되 면 hello Azure B2C 테 넌 트에 사용 하기 위해 응용 프로그램 등록 됩니다.

## <a name="prerequisites"></a>필수 조건

toobuild 소비자를 등록 및 로그인을 허용 하는 응용 프로그램을 먼저 tooregister hello 응용 프로그램을 Azure Active Directory B2C 테 넌 트에 있습니다. 에 설명 된 hello 단계를 사용 하 여 자신의 테 넌 트 가져오기 [Azure AD B2C 테 넌 트 만들기](active-directory-b2c-get-started.md)합니다.

Hello에서 hello Azure 포털에서에서 Azure AD B2C hello 블레이드에서 만든 응용 프로그램을 관리 해야 동일한 위치입니다. PowerShell 또는 다른 포털을 사용 하 여 hello B2C 응용 프로그램을 편집 하는 경우 지원 되지 않는 되며 Azure AD B2C 작동 하지 않습니다. Hello에 대 한 자세한 내용을 보려면 [응용 프로그램 오류가 발생 한](#faulted-apps) 섹션. 

## <a name="navigate-toob2c-settings"></a>TooB2C 설정 이동

Toohello 로그인 [Azure 포털](https://portal.azure.com/) 대로 hello hello B2C 테 넌 트의 전역 관리자 여야 합니다. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

등록 하는 hello 응용 프로그램 종류에 따라 다음 단계를 선택 합니다.

* [웹 응용 프로그램 등록](#register-a-web-app)
* [웹 API 등록](#register-a-web-api)
* [모바일 또는 네이티브 앱 등록](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>웹앱 등록

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

웹 응용 프로그램이 Azure AD B2C에서 보호하는 웹 API를 호출하는 경우 다음 단계를 수행하세요.
   1. Toohello 이동 하 여 응용 프로그램 암호를 만들 **키** hello를 클릭 하 고 블레이드 **키 생성** 단추입니다. Hello 기록 **응용 프로그램 키는** 값입니다. 응용 프로그램의 코드에서 hello 응용 프로그램으로 hello 값을 사용합니다.
   2. **API 액세스**를 클릭하고 **추가**를 클릭한 다음 웹 API와 범위(사용 권한)를 선택합니다.

> [!NOTE]
> **응용 프로그램 비밀**은 중요한 보안 자격 증명이며 적절하게 보호해야 합니다.
> 

[너무 점프**다음 단계**](#next-steps)

## <a name="register-a-web-api"></a>웹 API 등록

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

클릭 **범위 게시** tooadd 더 필요에 따라 범위입니다. 기본적으로 hello "user_impersonation" 범위 정의 됩니다. 범위가 user_impersonation hello hello 로그인 한 사용자를 대신 하 여 다른 응용 프로그램 hello 기능 tooaccess이이 api를 제공합니다. 원하는 경우에 범위가 user_impersonation hello를 제거할 수 있습니다.

[너무 점프**다음 단계**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>모바일 또는 네이티브 응용 프로그램 등록

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[너무 점프**다음 단계**](#next-steps)

## <a name="limitations"></a>제한 사항

### <a name="choosing-a-web-app-or-api-reply-url"></a>웹앱 또는 API 회신 URL 선택

현재 응용 프로그램에 등록 된 Azure AD B2C는 회신 URL 값 집합이 제한 tooa 제한 합니다. 웹 앱 및 서비스에 대 한 URL 구성표 hello로 시작 해야 하는 회신 hello `https`, 모든 회신 URL 값 단일 DNS 도메인을 공유 해야 합니다. 예를 들어 다음 회신 URL 중 하나가 있는 웹앱은 등록할 수 없습니다.

`https://login-east.contoso.com`

`https://login-west.contoso.com`

hello 등록 시스템 hello hello 기존 회신 URL toohello DNS 이름 추가 하는 hello 회신 URL의 전체 DNS 이름과 비교 합니다. hello 요청 tooadd hello DNS 이름에는 hello 다음 조건 중 하나에 해당 하는 경우 실패 합니다.

* hello 새 회신 URL의 hello 전체 DNS 이름에는 hello 기존 회신 URL의 DNS 이름을 hello 일치 하지 않습니다.
* hello 새 회신 URL의 hello 전체 DNS 이름 hello 기존 회신 URL의 하위 도메인이 아닌 경우

예를 들어 경우 hello 응용 프로그램에이 회신 URL:

`https://login.contoso.com`

다음과 같이 tooit를 추가할 수 있습니다.

`https://login.contoso.com/new`

이 경우 hello DNS 이름과 정확히 일치합니다. 또는 다음을 수행할 수 있습니다.

`https://new.login.contoso.com`

이 경우 login.contoso.com의 tooa DNS 하위 도메인을 참조 하 합니다. Toohave 로그인 east.contoso.com과 west.contoso.com 로그인 Url 회신으로 되어 있는 앱을 원하는 경우에이 순서 대로 해당 회신 Url을 추가 해야:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Hello 첫 번째 회신 URL의 하위 도메인에 있기 때문에 마지막 두 개의 hello를 추가할 수 있습니다 contoso.com입니다.

### <a name="choosing-a-native-app-redirect-uri"></a>네이티브 앱 리디렉션 URI 선택

모바일/네이티브 응용 프로그램에 대한 리디렉션 URI를 선택하는 경우 두 가지 중요한 고려 사항이 있습니다.

* **고유**: hello 체계 hello 리디렉션 URI의 모든 응용 프로그램에 대 한 고유 해야 합니다. 예제 (com.onmicrosoft.contoso.appname://redirect/path) hello 구성표로 com.onmicrosoft.contoso.appname를 사용합니다. 이 패턴을 따르는 것이 좋습니다. 두 개의 응용 프로그램 hello를 공유 하는 경우 동일한 구성표 hello "앱을 선택" 대화 상자가 사용자에 게 표시 합니다. Hello 사용자가 잘못 선택 하면, hello 로그인 실패 합니다.
* **전체**: 리디렉션 URI에는 체계 및 경로가 있어야 합니다. hello 경로 hello 도메인 (예를 들어 //contoso/ 작동 및 //contoso 실패) 한 후 하나 이상의 앞에 슬래시를 포함 해야 합니다.

Hello에 밑줄이 리디렉션 uri와 같은 특수 문자가 없는 있는지 확인 하십시오.

### <a name="faulted-apps"></a>오류가 발생한 앱

B2C 응용 프로그램은 다음에서 편집할 수 없습니다.

* [Azure 클래식 포털](https://manage.windowsazure.com/) 및 [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/)과 같은 다른 응용 프로그램 관리 포털.
* Graph API 또는 PowerShell 사용

위에서 설명한 것 처럼 hello B2C 응용 프로그램을 편집 하 고 tooedit Azure 포털에서 Azure AD B2C hello 기능 블레이드에서 다시 hello, 오류가 발생 한 앱 되며 응용 프로그램을 Azure AD B2C 사용할 수 없습니다. Toodelete hello 응용 프로그램이 있어야 하 고 다시 만드십시오.

toodelete hello 앱 이동 toohello [응용 프로그램 등록 포털](https://apps.dev.microsoft.com/) hello 응용 프로그램을 삭제 합니다. Hello 응용 프로그램 toobe 표시에 대 한 순서, hello 응용 프로그램의 toobe hello 소유자 (및 hello 테 넌 트의 관리자 뿐 아니라) 해야합니다.

## <a name="next-steps"></a>다음 단계

이제는 응용 프로그램에 등록 된 Azure AD B2C 했으므로 중 하나를 완료할 수 있습니다 [우리의 빠른 시작 자습서](active-directory-b2c-overview.md#get-started) tooget 작동 하 고 실행 합니다.

> [!div class="nextstepaction"]
> [등록, 로그인 및 암호 재설정으로 ASP.NET 웹앱 만들기](active-directory-b2c-devquickstarts-web-dotnet-susi.md)