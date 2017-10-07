---
title: "Azure 앱 서비스에서 API 앱에 대 한 사용자 인증 aaaService | Microsoft Docs"
description: "자세한 내용은 방법 서비스 간 시나리오에 대 한 Azure 앱 서비스의 API tooprotect 응용 프로그램입니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Azure 앱 서비스의 API 앱에 대한 서비스 주체 인증
## <a name="overview"></a>개요
이 문서에서는 설명 어떻게 toouse 앱 서비스 인증에 대 한 *내부* tooAPI 앱에 액세스 합니다. 내부 시나리오 되도록 toobe 사용 될 응용 프로그램 코드에 의해서만 API 앱이 있는 위치입니다. hello 권장 방법은 tooimplement이이 경우 앱 서비스에서 Azure AD toouse tooprotect hello 라고 API 앱. 응용 프로그램 id (서비스 주체) 자격 증명을 제공 하 여 Azure AD에서 얻을 수 있는 전달자 토큰을 사용 하는 보호 된 hello API 앱을 호출 합니다. 대안 toousing Azure AD에 대 한 참조 hello **서비스 간 인증** hello 섹션 [Azure 앱 서비스 인증 개요](../app-service/app-service-authentication-overview.md#service-to-service-authentication)합니다.

이 문서에서는 다음에 대해 알아봅니다.

* 어떻게 toouse tooprotect API 앱을 Azure Active Directory (Azure AD) 인증 되지 않은 액세스 합니다.
* 어떻게 API 앱, 웹 응용 프로그램 또는 Azure AD 서비스 주체 (앱 id) 자격 증명을 사용 하 여 모바일 앱에서 보호 된 API tooconsume 앱. 방법에 대 한 정보에 대 한 논리 앱에서 tooconsume 참조 [논리 앱과 앱 서비스에서 호스팅되는 사용자 지정 API를 사용 하 여](../logic-apps/logic-apps-custom-hosted-api.md)합니다.
* 사용자 로그온 방법가 브라우저에서 toomake 해당 hello API 앱을 보호 합니다를 호출할 수 없습니다.
* 어떻게 toomake 해당 hello API 앱을 보호 합니다만 호출할 수는 특정 Azure AD 서비스 사용자입니다.

hello 문서에는 두 개의 섹션이 포함 됩니다.

* hello [tooconfigure Azure 앱 서비스에서 사용자 인증을 서비스 하는 방법을](#authconfig) 섹션에서는 일반적인 방법에 설명 모든 API 앱 및 tooconsume hello API 앱을 보호 하는 방법에 대 한 tooconfigure 인증 합니다. 이 섹션에서.NET, Node.js, Java 등 응용 프로그램 서비스를 지 원하는 tooall 프레임 워크 똑같이 합니다.
* Hello로 시작 [hello.NET 시작 하기 자습서를 계속](#tutorialstart) 섹션 hello 자습서에서는 응용 프로그램 서비스에서 실행 되는.NET 예제 응용 프로그램에 대 한 "액세스 내부" 시나리오에서 구성 하는 과정입니다. 

## <a id="authconfig"></a>Tooconfigure Azure 앱 서비스에서 사용자 인증을 서비스 하는 방법
이 섹션에서는 tooany API 앱에 적용 되는 일반적인 지침을 제공 합니다. 너무 단계 특정 toohello tooDo 목록.NET 예제 응용 프로그램을 이동[hello.NET API 앱에 대 한 자습서 시리즈 계속](#tutorialstart)합니다.

1. Hello에 [Azure 포털](https://portal.azure.com/), toohello 이동 **설정** tooprotect를 원하고 hello 찾을 hello API 앱의 블레이드에서 **기능** 섹션 및 클릭**인증 / 권한 부여**합니다.
   
    ![Azure 포털에서 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **에**합니다.
3. Hello에 **요청이 인증 되지 않은 경우 동작 tootake** 드롭 다운 목록 **Azure Active Directory로 로그인** 합니다.
4. **인증 공급자**에서 **Azure Active Directory**를 선택합니다.
   
    ![Azure 포털에서 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Hello 구성 **Azure Active Directory 설정** 블레이드 toocreate 새로운 Azure AD 응용 프로그램 또는 이미 있는 경우 기존 Azure AD 응용 프로그램을 사용 하 여 toouse 되도록 합니다.
   
    내부 시나리오는 일반적으로 API 앱을 호출하는 API 앱을 포함합니다. 각 API 앱 또는 하나의 Azure AD 응용 프로그램에 분리된 AD 응용 프로그램을 사용할 수 있습니다.
   
    이 블레이드에서 자세한 지침을 참조 하십시오. [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다.
6. 클릭 하 여 hello 인증 공급자 구성 블레이드를 마치면 **확인**합니다.
7. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **저장**합니다.
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

이 도구를 실행 하는 경우 앱 서비스 hello 구성 된 Azure AD 테 넌 트의 호출자 로부터 요청 허용 합니다. 보호 된 hello API 앱 인증 또는 권한 부여 코드가 필요 합니다. hello 전달자 토큰이 함께 자주 사용 되는 클레임 toohello API 앱에에서 전달 HTTP 헤더 하 고 서비스 사용자와 같은 특정 호출자의 요청은 코드 toovalidate에서 해당 정보를 읽을 수 있습니다.

이 인증 기능이 작동 hello.NET, Node.js, 및 Java와 같은 모든 언어에 대해 동일한 방식으로 해당 앱 서비스 지원 합니다. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Tooconsume hello API 앱을 보호 하는 방법
hello 호출자 API 호출에는 Azure AD 전달자 토큰을 제공 해야 합니다. tooget 서비스 사용자 자격 증명을 사용 하 여 전달자 토큰을 hello 호출자 사용 하 여 Active Directory 인증 라이브러리 (ADAL에 대 한 [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), 또는 [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). 토큰 tooget ADAL 호출 하는 hello 코드 tooADAL hello를 다음 정보를 제공 합니다.

* Azure AD 테 넌 트의 hello 이름입니다.
* hello 클라이언트 ID와 클라이언트 암호 (응용 프로그램 키) hello 호출자와 연관 된 hello Azure AD 응용 프로그램의입니다.
* hello hello와 연결 된 Azure AD 응용 프로그램의 클라이언트 ID hello API 앱을 보호 합니다. (Azure AD에 대 한 응용 프로그램을 하나만 사용 되는 경우이 hello 같은 클라이언트 ID hello 호출자에 대 한 hello 대로.)

이러한 값은 hello의 hello Azure AD 페이지에서 사용할 [Azure 클래식 포털](https://manage.windowsazure.com/)합니다.

Hello 토큰 획득 한 면 hello 호출자에 hello 인증 헤더에 HTTP 요청과 함께 포함 합니다.  앱 서비스는 hello 토큰의 유효성을 검사 하 고 hello 요청 tooreach hello 보호 API 앱을 허용 합니다.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>어떻게 hello에 대 한 사용자의 액세스 tooprotect hello API 앱 동일한 테 넌 트
전달자 토큰 같은 테 넌 트 hello에 대 한 유효한 것으로 간주 되는 hello에 사용자에 대 한 API 앱을 보호 합니다.  서비스 사용자를 호출할 수 있는 tooensure hello API의 보호 된 앱을 hello에 대 한 코드 API 앱 toovalidate hello hello 토큰에서 클레임에 따라 보호 된 추가:

* `appid`hello 호출자와 연관 된 hello Azure AD 응용 프로그램의 클라이언트 ID hello 이어야 합니다. 
* `oid`(`objectidentifier`) hello 호출자의 hello 서비스 보안 주체 ID 여야 합니다. 

앱 서비스는 hello 제공 `objectidentifier` hello X-MS-클라이언트-보안 주체 ID 헤더에는 클레임입니다.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Tooprotect은 브라우저 액세스에서 API 앱 hello 하는 방법
보호 된 hello API 앱에 코드의 클레임 유효성을 검사 하지 않는 하 고 별도 사용 하는 경우 Azure AD 응용 프로그램 hello API 앱을 보호 된 해야 Azure AD 응용 프로그램의 회신 URL은 해당 hello 하지 hello API 응용 프로그램의 기본 URL과 동일 hello 합니다. 회신 URL hello 가리키면 직접 보호 toohello API 앱, hello 동일한 Azure AD 테 넌 트의 사용자 수 toohello API 앱을 찾아보기, 로그온 한 hello API를 성공적으로 호출 합니다.

## <a id="tutorialstart"></a>Hello.NET API 앱에 대 한 자습서 시리즈를 계속합니다.
Hello Node.js 또는 Java 자습서 시리즈 API 앱에 대 한를 따르는 경우 건너뛸 toohello [다음 단계](#next-steps) 섹션. 

이 문서의 나머지 부분에서는 hello hello.NET API 앱에 대 한 자습서 시리즈를 지속 하 고 hello 완료 한 것으로 가정 [사용자 인증 자습서](app-service-api-dotnet-user-principal-auth.md) hello 샘플 응용 프로그램 사용자 인증으로 Azure에서 실행 되 고 사용할 수 있습니다.

## <a name="set-up-authentication-in-azure"></a>Azure에서 인증 설정
이 섹션에서는 구성한 앱 서비스 하므로 HTTP만 요청 tooreach hello 데이터 계층 API 앱을 통해 해당 hello는 hello 할 유효한 Azure AD 전달자 토큰입니다. 

Hello 중간 계층 API 앱 toosend 응용 프로그램 자격 증명 tooAzure AD 구성 hello 섹션 뒤에서 전달자 토큰 돌아갈 및 보낼 hello 전달자 토큰 toohello 데이터 계층 API 앱. 이 프로세스는 hello 다이어그램에 표시 됩니다.

![서비스 인증 다이어그램](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

다음 hello 자습서 방향 하는 동안 문제를 실행 하는 경우 참조 hello [문제 해결](#troubleshooting) hello 자습서의 hello 끝 섹션. 

1. Hello에 [Azure 포털](https://portal.azure.com/), toohello 이동 **설정** hello ToDoListDataAPI (데이터 계층) API 앱에 대해 생성 하 고 클릭 hello API 앱의 블레이드에서 **설정을**합니다.
2. Hello에 **설정** 블레이드, 찾기 hello **기능** 섹션을 선택한 다음 클릭 **인증 / 권한 부여**합니다.
   
    ![Azure 포털에서 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **에**합니다.
4. Hello에 **요청이 인증 되지 않은 경우 동작 tootake** 드롭 다운 목록 **Azure Active Directory로 로그인**합니다.
   
    앱 서비스 tooensure만 요청 reach hello API 앱을 인증 하는 hello 설정입니다. 요청에 유효한 전달자 토큰에 대 한 앱 서비스 hello 토큰 toohello API 앱을 따라 전달 및 자주 사용 되는 클레임 toomake 된 HTTP 헤더 정보를 채웁니다 tooyour 보다 쉽게 사용할 수 있는 코드입니다.
5. **인증 공급자** 아래에서 **Azure Active Directory**를 클릭합니다.
   
    ![Azure 포털에서 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. Hello에 **Azure Active Directory 설정** 블레이드에서 클릭 **Express**합니다.
   
    Hello로 **Express** 옵션 Azure Azure AD에서 AAD 응용 프로그램을 자동으로 만들 수 [테 넌 트](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)합니다. 
   
    않아도 toocreate 테 넌 트 마다 Azure 계정이 자동으로 하나에 있기 때문에 있습니다.
7. **관리 모드**에서 아직 선택하지 않은 경우 **새 AD 앱 만들기**를 클릭합니다.
   
    hello 포털 연결 hello **앱 만들기** 이며 기본값은 입력된 상자입니다. 기본적으로 hello Azure AD 응용 프로그램 이름은 hello API 응용 프로그램으로 hello 동일 합니다. 원하는 경우 다른 이름을 입력합니다.
   
    ![Azure AD 설정](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **참고**:는 대신 단일 Azure AD를 사용할 수 있습니다 호출 API 앱 hello 둘 다 고 hello 보호 API 앱에 대 한 응용 프로그램입니다. 해당 대체 항목을 선택한 경우 필요 없습니다 hello **새 AD 앱 만들기** hello 사용자 인증 자습서의 앞부분에 나오는 Azure AD 응용 프로그램을 이미 만들어졌기 때문에 여기 옵션입니다. 이 자습서에서는 사용할 호출 API 앱 및 hello hello API 앱을 보호 된 Azure AD 응용 프로그램을 분리 합니다.
8. Hello에 hello 값 메모 **앱 만들기** 입력된 상자; 것이 AAD 응용 프로그램에서에서 조회 hello Azure 클래식 포털 나중입니다.
9. **확인**을 클릭합니다.
10. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **저장**합니다.
    
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    앱 서비스와 Azure Active Directory 응용 프로그램을 만듭니다 **로그온 URL** 및 **회신 URL** API 앱 toohello URL을 자동으로 설정 합니다. hello 후자 값에서 AAD 테 넌 트 toolog 프로그램의 사용자와 액세스 hello API 앱 수 있습니다.

### <a name="verify-that-hello-api-app-is-protected"></a>Hello API 앱 보호 되는지 확인
1. 브라우저에서 toohello 앱의 URL을 hello API 이동: hello에 **API 앱** 아래 hello 링크를 클릭 하는 hello Azure 포털에서에서 블레이드 **URL**합니다. 
   
    사용자는 리디렉션된 tooa 로그인 화면 인증 되지 않은 요청이 tooreach hello API 앱 허용 되지 않습니다. 
   
    경우 브라우저가 않습니다 toohello Swagger UI, 브라우저 이미 기록 될 수 있습니다-이 경우 InPrivate 또는 Incognito 창을 열고 toohello UI Swagger URL로 이동 합니다.
2. AAD 테넌트의 사용자 자격 증명으로 로그인합니다.
   
   에 로그온 하는 hello "만들었습니다" 페이지 hello 브라우저에 나타납니다.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Hello ToDoListAPI 프로젝트 tooacquire를 구성 하 고 hello Azure AD 토큰 보내기
이 섹션에서는 다음 작업 hello 수행 있습니다.

* Azure AD 응용 프로그램 자격 증명 tooacquire 토큰을 사용 하는 hello 중간 계층 API 앱에 코드를 추가 하 고 http toohello 데이터 계층 API 응용 프로그램에 요청을 보냅니다.
* Azure AD에서 필요한 hello 자격 증명을 가져옵니다.
* Hello 중간 계층 API 앱에에서 Azure 앱 서비스 런타임 환경 설정에 hello 자격 증명을 입력 합니다. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Hello ToDoListAPI 프로젝트 tooacquire를 구성 하 고 hello Azure AD 토큰 보내기
Visual Studio에서 hello ToDoListAPI 프로젝트의 변경 내용을 따라 hello를 확인 합니다.

1. Hello에서 모든 코드 hello 주석 처리 제거 *ServicePrincipal.cs* 파일입니다.
   
    .NET tooacquire hello Azure AD 전달자 토큰에 ADAL을 사용 하는 hello 코드입니다.  나중에 hello Azure 런타임 환경에서 설정 하는 몇 가지 구성 값을 사용 합니다. Hello 코드는 다음과 같습니다. 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **참고:** 이 코드는 hello 프로젝트에 이미 설치 된.NET NuGet 패키지 (Microsoft.IdentityModel.Clients.ActiveDirectory)에 대 한 ADAL hello 필요 합니다. 처음부터이 프로젝트를 만들 때,이 패키지 tooinstall 있어야 합니다. 이 패키지에서 hello API 앱 새 프로젝트 템플릿이 자동으로 설치 되지 않았습니다.
2. *컨트롤러/ToDoListController*, hello의 hello 코드를 주석 처리 제거 `NewDataAPIClient` hello 토큰 tooHTTP 요청 hello 인증 헤더에 추가 하는 메서드.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Hello ToDoListAPI 프로젝트를 배포 합니다. (Hello 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시 > 게시**.)
   
    Visual Studio hello 프로젝트를 배포 하 고 브라우저 toohello 웹 앱의 기본 URL을 엽니다. 이 정상 시도 toogo tooa 웹 API 기본 URL에 대 한 브라우저에서 403 오류 페이지를 표시 됩니다.
4. 닫기 hello 브라우저입니다.

### <a name="get-azure-ad-configuration-values"></a>Azure AD 구성 값 가져오기
1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 너무 이동**Azure Active Directory**합니다.
2. Hello에 **디렉터리** 탭에서 AAD 테 넌 트를 클릭 합니다.
3. 클릭 **응용 프로그램 > 회사가 보유 한 응용 프로그램**, 다음 hello 확인 표시를 클릭 합니다.
4. 응용 프로그램의 hello 목록의 hello 하나 hello ToDoListDataAPI (데이터 계층) API 앱에 대 한 인증을 사용 하는 경우 한 만든 Azure의 hello 이름을 클릭 합니다.
5. Hello 클릭 **구성** 탭 합니다.
6. 복사 hello **클라이언트 ID** 값 및에서 나중에 가져올 수 있습니다 했지만 위치를 저장 합니다. 
7. Hello Azure 클래식 포털에서에서 돌아가서 toohello 목록이 **회사가 보유 한 응용 프로그램**, hello 중간 계층 ToDoListAPI API 앱 (hello 하지 hello 이전 자습서에서 만든 것에 대해 만든 hello AAD 응용 프로그램을 클릭 하 고 hello이이 자습서에서 만든 것).
8. Hello 클릭 **구성** 탭 합니다.
9. 복사 hello **클라이언트 ID** 값 및에서 나중에 가져올 수 있습니다 했지만 위치를 저장 합니다.
10. 아래 **키**선택, **1 년** hello에서 **기간 선택** 드롭 다운 목록입니다.
11. **Save**를 클릭합니다.
    
     ![앱 키 생성](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Hello 키 값을 복사 하 고에서 나중에 가져올 수 있습니다 했지만 위치를 저장 합니다.
    
     ![새 앱 키 복사](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Hello API 중간 계층 응용 프로그램의 런타임 환경에서 Azure AD 설정 구성
1. Toohello 이동 [Azure 포털](https://portal.azure.com/)를 이동한 후 toohello **API 앱** 블레이드 hello TodoListAPI (중간 계층) 프로젝트를 호스팅하는 hello API 앱에 대 한 합니다.
2. **설정 > 응용 프로그램 설정**을 클릭합니다.
3. Hello에 **앱 설정** 섹션을 따라 hello 키와 값을 추가 합니다.
   
   | **키** | ida:Authority |
   | --- | --- |
   | **값** |https://login.microsoftonline.com/{Azure AD 테넌트 이름} |
   | **예제** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **키** | ida:ClientId |
   | --- | --- |
   | **값** |응용 프로그램 (중간 계층-ToDoListAPI)을 호출 하는 hello의 클라이언트 ID |
   | **예제** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **키** | ida:ClientSecret |
   | --- | --- |
   | **값** |응용 프로그램 (중간 계층-ToDoListAPI)을 호출 하는 hello의 응용 프로그램 키 |
   | **예제** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **키** | ida:Resource |
   | --- | --- |
   | **값** |응용 프로그램을 호출 하는 hello의 클라이언트 ID (데이터 계층-ToDoListDataAPI) |
   | **예제** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **참고**:에 대 한 `ida:Resource`, 응용 프로그램의 호출 hello를 사용 하면 **클라이언트 ID** 아닌 해당 **앱 ID URI**합니다.
   
    `ida:ClientId`및 `ida:Resource` 서로 구분 hello 중간 계층 및 데이터 계층에 대 한 Azure AD applicaations을 사용 중 이므로이 자습서에 대 한 값입니다. 단일 사용 중 이었다 면 hello 호출 hello 및 API 앱에 대 한 Azure AD 응용 프로그램 보호 API 앱, hello 둘 다에 같은 값을 사용 하 여 `ida:ClientId` 및 `ida:Resource`합니다.
   
    hello 코드 hello Azure 런타임 환경과 또는 hello 프로젝트의 Web.config 파일에 저장 될 수 있으므로 ConfigurationManager tooget 이러한 값을 사용 합니다. Azure 앱 서비스에서 ASP.NET 응용 프로그램을 실행하는 동안 환경 설정은 Web.config에서 설정을 자동으로 재정의합니다. 환경 설정을 일반적으로 [보다 안전한 방식으로 toostore 중요 한 정보가 tooa Web.config 파일을 비교](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)합니다.
4. **Save**를 클릭합니다.
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Hello 응용 프로그램 테스트
1. 브라우저에서 toohello hello AngularJS 프런트 엔드 웹 응용 프로그램의 HTTPS URL을 이동 합니다.
2. Hello 클릭 **tooDo 목록** 탭과 Azure AD 테 넌 트의 사용자에 대 한 자격 증명으로 로그인 합니다. 
3. Hello 응용 프로그램이 작동 하는 할 일 항목 tooverify를 추가 합니다.
   
    ![tooDo 목록 페이지](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Hello 응용 프로그램이 예상 대로 작동 하지 않을 경우 모든 hello Azure 포털에에서 입력 한 hello 설정을 두 번 클릭 합니다. 올바른 toobe hello 설정을 모두 없으면 참조 hello [문제 해결](#troubleshooting) 이 자습서의 뒷부분에 나오는 섹션.

## <a name="protect-hello-api-app-from-browser-access"></a>Hello API 앱에서 브라우저 액세스 보호
이 자습서에 대 한 별도 만든 hello ToDoListDataAPI (데이터 계층) API 앱에 대 한 Azure AD 응용 프로그램입니다. 지금까지 살펴본 대로, 앱 서비스는 AAD 응용 프로그램을 만들 때 hello AAD 응용 프로그램에서 브라우저와 로그에는 사용자 toogo toohello API 앱 URL을 사용 하도록 설정 하는 방식으로 구성 합니다. 즉, Azure AD 테 넌 트 뿐 아니라 서비스 사용자는 최종 사용자 수, tooaccess hello API. 

API 앱을 보호 hello에 코드를 작성 하지 않고 tooprevent 브라우저 액세스를 원하는 경우에 hello을 변경할 수 있습니다 **회신 URL** 하 게 구분할 hello API 앱에서 기본 URL의 hello AAD 응용 프로그램입니다. 

### <a name="disable-browser-access"></a>브라우저 액세스 사용 안 함
1. Hello 클래식 포털에서 **구성** TodoListService hello에 대해 만들어진 hello AAD 응용 프로그램에 대 한 탭 hello에 hello 값을 변경 하세요 **회신 URL** 구분 되는 올바른 URL 있지만 하지 hello API 응용 프로그램의 필드 URL입니다.
2. **Save**를 클릭합니다.

### <a name="verify-browser-access-no-longer-works"></a>브라우저 액세스가 더 이상 작동하지 않는지 확인
이전 버전을 이동할 수 있습니다 toohello API 앱 URL을 브라우저에서 개별 사용자의 자격 증명으로 로그온 하 여 확인 합니다. 이 섹션에서 더 이상 가능하지 않은지 확인합니다. 

1. 새 브라우저 창에서 toohello hello API 앱 URL을 다시 이동 합니다.
2. 경우에 로그 라는 toodo 메시지가 표시 되므로.
3. 로그인 성공 하지만 tooan 오류 페이지를 안내 합니다.
   
    Hello AAD 테 넌 트의 사용자가 로그인 하 고 브라우저에서 hello API에 액세스할 수 없는 있도록 hello AAD 응용 프로그램을 구성 했습니다. 여전히 toohello 웹 앱의 URL을 이동 하 할 일 항목을 더 추가 하 여 확인할 수 있는 서비스 보안 주체 토큰을 사용 하 여 hello API 앱에 액세스할 수 있습니다.

## <a name="restrict-access-tooa-particular-service-principal"></a>액세스 tooa 특정 서비스 사용자를 제한 합니다.
사용자에 대 한 토큰을 얻을 수 있는 모든 호출자가 지금 바로 사용 하거나 Azure AD 테 넌 트에 서비스 사용자는 hello TodoListDataAPI (데이터 계층) API 앱을 호출할 수 있습니다. Hello 데이터 계층 API 앱은만 특정 서비스 보안 주체와만 hello TodoListAPI (중간 계층) API 앱에서 호출을 허용 하는지 toomake를 할 수 있습니다. 

이러한 제한 사항은 toovalidate hello 코드를 추가 하 여 추가할 수 있습니다 `appid` 및 `objectidentifier` 들어오는 호출에는 클레임입니다.

이 자습서에 대 한 앱 ID와 컨트롤러 작업에서 직접 서비스 보안 주체 ID의 유효성을 검사 하는 hello 코드를 넣습니다.  옵션은 사용자 지정 toouse `Authorize` 특성 또는 toodo 시작 시퀀스 (예: OWIN 미들웨어)를 사용 하 여이 유효성 검사 합니다. 예를 보려면 hello 후자 참조 [이 샘플 응용 프로그램](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs)합니다. 

다음 변경 내용을 toohello TodoListDataAPI 프로젝트 hello를 확인 합니다.

1. 열기 hello *Controllers/TodoListController.cs* 파일입니다.
2. 설정 하는 hello 줄의 주석 처리 제거 `trustedCallerClientId` 및 `trustedCallerServicePrincipalId`합니다.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Hello CheckCallerId 메서드의에서 hello 코드 주석 처리를 제거 합니다. 이 메서드는 hello 컨트롤러의 모든 동작 메서드에의 hello 시작 될 때 호출 됩니다. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Hello ToDoListDataAPI 프로젝트 tooAzure 앱 서비스를 다시 배포 합니다.
5. Toohello AngularJS 프런트 엔드 웹 응용 프로그램의 HTTPS URL 이동한 hello 홈 페이지에서 클릭 hello 브라우저에서 **tooDo 목록** 탭 합니다.
   
    hello 응용 프로그램은 다시 toohello 종료 호출이 실패 하 고 때문에 작동 하지 않습니다. 새 코드 hello 및 검사 하 고 실제 appid objectidentifier 있지만 hello 올바른 값 toocheck 아직 없는 대 한 합니다. hello 브라우저 개발자 도구 콘솔 보고 해당 hello 서버에서 HTTP 401 오류를 반환 합니다.
   
    ![개발자 도구 콘솔의 오류](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    단계를 수행 하는 hello hello 예상 값을 구성 합니다.
6. Azure AD PowerShell을 사용 하 여 값을 가져올 hello hello 서비스의 주 hello hello TodoListWebApp 프로젝트에 대해 생성 하는 Azure AD 응용 프로그램에 대 한 합니다.
   
    a. 방법에 대 한 Azure PowerShell tooinstall tooyour 구독을 연결 하 고, 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다.
   
    b. 서비스 주체 목록을 tooget 실행 hello `Login-AzureRmAccount` 명령을 클릭 한 다음 hello `Get-AzureRmADServicePrincipal` 명령입니다.
   
    c. Hello objectid hello에 대 한 hello TodoListAPI 응용 프로그램의 서비스 사용자 찾아에서 나중에 복사할 수 있습니다 위치에 저장 합니다.
7. Hello Azure 포털에서에서 hello ToDoListDataAPI 프로젝트를 배포 하는 hello API 앱에 대 한 toohello API 앱 블레이드를 탐색 합니다.
8. **설정 > 응용 프로그램 설정**을 클릭합니다.
9. Hello에 **앱 설정** 섹션을 따라 hello 키와 값을 추가 합니다.
   
   | **키** | todo:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **값** |호출하는 응용 프로그램의 서비스 주체 ID |
   | **예제** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **키** | todo:TrustedCallerClientId |
   | --- | --- |
   | **값** |호출 하는 응용 프로그램-hello TodoListAPI Azure AD 응용 프로그램에서 복사한 클라이언트 ID |
   | **예제** |960adec2-b74a-484a-960adec2-b74a-484a |
10. **Save**를 클릭합니다.
    
     ![저장을 클릭합니다.](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. 브라우저에서 toohello 웹 앱의 URL을 반환 하 고 hello 홈 페이지에서 hello 클릭 **tooDo 목록** 탭 합니다.
    
     이 시간 hello 응용 프로그램 ID 및 서비스 보안 주체 ID hello 신뢰할 수 있는 호출자에 게 앱 hello 예상 값 때문에 예상 대로 작동 합니다.
    
     ![tooDo 목록 페이지](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>처음부터 hello 프로젝트 빌드
hello를 사용 하 여 hello 두 웹 API 프로젝트가 만들어진 **Azure API 앱** 프로젝트 템플릿 및 hello 기본 값 컨트롤러와 ToDoList 컨트롤러 교체 합니다. Hello ToDoListAPI 프로젝트에서 Azure AD 서비스 보안 주체 토큰을 획득에 대 한 hello [Active Directory 인증 라이브러리 (ADAL).NET 용](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet 패키지가 설치 되었습니다.

방법에 대 한 정보는 너무 ToDoListAngular와 같은 웹 API 백 엔드에서 AngularJS 단일 페이지 응용 프로그램을 만들기, 참조 [손에에 랩: 빌드는 단일 페이지 응용 프로그램 (SPA) ASP.NET Web API와 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)합니다. 방법에 대 한 정보에 대 한 Azure AD 인증 코드 tooadd 참조 [보안 AngularJS 단일 페이지 응용 프로그램을 Azure AD와](../active-directory/active-directory-devquickstarts-angular.md)합니다.

## <a name="troubleshooting"></a>문제 해결
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* ToDoListAPI(중간 계층) 및 ToDoListDataAPI(데이터 계층)를 혼동하지 않아야 합니다. 예를 들어이 자습서에서는 추가한 인증 toohello 데이터 계층 API 앱 **hello 응용 프로그램 키는 hello hello 중간 계층 API 앱에 대해 만든 Azure AD 응용 프로그램에서에서 가져와야 합니다. 하지만**합니다.

## <a name="next-steps"></a>다음 단계
이 hello API 앱 일련의에서 hello 마지막 자습서입니다. 

Azure Active Directory에 대 한 자세한 내용은 다음 리소스는 hello를 참조 하세요.

* [Azure AD 개발자 가이드](http://aka.ms/aaddev)
* [Azure AD 시나리오](http://aka.ms/aadscenarios)
* [Azure AD 샘플](http://aka.ms/aadsamples)
  
    hello [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) 샘플은 유사한 toowhat 앱 서비스 인증을 사용 하지 않고이 자습서에 표시 됩니다.

다른 방법에 대 한 내용은 toodeploy Visual Studio 프로젝트 tooAPI 앱 또는 Visual Studio를 사용 하 여 [배포를 자동화](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) 에서 [소스 제어 시스템이](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), 참조 [어떻게 toodeploy는 Azure 앱 서비스 앱](../app-service-web/web-sites-deploy.md)합니다.

