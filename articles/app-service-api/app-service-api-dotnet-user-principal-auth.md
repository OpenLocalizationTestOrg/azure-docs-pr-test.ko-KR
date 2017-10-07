---
title: "Azure 앱 서비스에서 API 앱에 대 한 인증 aaaUser | Microsoft Docs"
description: "Azure 앱 서비스에서 허용 하 여 API 앱 tooprotect만 tooauthenticated 사용자를 액세스 하는 방법을 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Azure 앱 서비스의 API 앱에 대한 사용자 인증
## <a name="overview"></a>개요
이 문서에서는 tooprotect Azure API 앱 하도록 하는 인증 된 사용자만 호출할 수 방법을 보여 줍니다. hello 문서 가정 hello 읽기 [Azure 앱 서비스 인증 개요](../app-service/app-service-authentication-overview.md)합니다.

다음 내용을 배웁니다.

* 어떻게 tooconfigure Azure Active Directory (Azure AD)에 대 한 세부 정보와 함께 인증 공급자입니다.
* 사용 하 여 보호 되는 API 앱 tooconsume hello 어떻게 [Active Directory 인증 라이브러리 (ADAL) javascript](https://github.com/AzureAD/azure-activedirectory-library-for-js)합니다.

hello 문서에는 두 개의 섹션이 포함 됩니다.

* hello [어떻게 Azure 앱 서비스에서 사용자 인증 tooconfigure](#authconfig) 섹션에서는 일반적인 방법에 설명 tooconfigure 사용자 인증 API 앱에 대 한.NET을 포함 하는 응용 프로그램 서비스에서 지 원하는 tooall 프레임 워크를 동일 하 게 적용 Node.js, 및 Java 합니다.
* Hello로 시작 [hello.NET API 앱 자습서를 계속](#tutorialstart) 섹션에서.net 예제 응용 프로그램을 구성 하는 과정 백업할 엔드와 AngularJS 프런트 엔드를 사용자에 대 한 Azure Active Directory를 사용 하도록 문서 안내선 hello 인증입니다. 

## <a id="authconfig"></a>어떻게 Azure 앱 서비스의 tooconfigure 사용자 인증
이 섹션에서는 tooany API 앱에 적용 되는 일반적인 지침을 제공 합니다. 너무 단계 특정 toohello tooDo 목록.NET 예제 응용 프로그램을 이동[hello.NET 시작 하기 자습서를 계속](#tutorialstart)합니다.

1. Hello에 [Azure 포털](https://portal.azure.com/), toohello 이동 **설정** tooprotect, 찾기 hello hello API 앱의 블레이드에서 **기능** 섹션을 선택한 다음 클릭  **인증 / 권한 부여**합니다.
   
    ![Azure 포털 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **에**합니다.
3. Hello에서 hello 옵션 중 하나를 선택 **요청이 인증 되지 않은 경우 동작 tootake** 드롭 다운 목록입니다.
   
   * API 앱 인증 된 호출 tooreach만 하려는 경우 hello 중 하나를 선택 **사용 하 여 로그인...**  옵션입니다. 이 옵션에서 실행 되는 코드를 작성 하지 않고도 tooprotect hello API 앱을 사용 합니다.
   * 모든 호출이 tooreach API 앱을 하려는 경우 선택 **요청 허용 동작이 없습니다**합니다. 이 옵션은 인증 되지 않은 toodirect 호출자 tooa 다양 한 인증 공급자를 사용할 수 있습니다. 이 옵션을 toowrite 코드 toohandle 권한 부여를 해야합니다.
     
     자세한 내용은 [Azure 앱 서비스의 API 앱에 대한 인증 및 권한 부여](app-service-api-authentication.md#multiple-protection-options)를 참조하세요.
4. Hello를 하나 이상 선택 **인증 공급자**합니다.
   
    hello 이미지는 Azure AD에서 인증 하는 모든 호출자에 게 toobe를 필요로 하는 선택 항목을 표시 합니다.
   
    ![Azure 포털 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    인증 공급자를 선택 하면 hello 포털 해당 공급자에 대 한 구성 블레이드를 표시 합니다. 
   
    Tooconfigure 인증 공급자 구성 블레이드 hello 하는 방법을 설명 하는 자세한 지침을 참조 하십시오. [어떻게 tooconfigure 앱 서비스 응용 프로그램 toouse Azure Active Directory 로그인](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)합니다. (hello 링크 Azure AD에 대 한 문서 tooan 까지일 hello 문서 자체 tooarticles hello에 대 한 다른 인증 공급자를 연결 하는 탭을 포함 합니다.)
5. 클릭 하 여 hello 인증 공급자 구성 블레이드를 마치면 **확인**합니다.
6. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **저장**합니다.

이 도구를 실행 하는 경우 앱 서비스 hello API 앱에 도달 하기 전에 모든 API 호출을 인증 합니다. hello 인증 서비스 작업을 hello.NET, Node.js, Java 등을 앱 서비스 지 원하는 모든 언어에 대해 동일 합니다. 

toomake 인증 API 호출, hello 호출자 HTTP 요청의 인증 헤더 hello에에서 hello 인증 공급자의 OAuth 2.0 전달자 토큰을 포함 합니다. hello 인증 공급자 SDK를 사용 하 여 hello 토큰을 받을 수 있습니다.

## <a id="tutorialstart"></a>Hello.NET API 앱 자습서를 계속합니다.
API 앱에 대 한 hello Node.js 또는 Java 자습서를 따르는 경우 건너뛸 toohello 다음 기사 [서비스 API 앱에 대 한 사용자 인증](app-service-api-dotnet-service-principal-auth.md)합니다. 

API 앱에 대 한 hello.NET 자습서 시리즈는 다음과 같습니다. hello에서 지시한 대로 hello 샘플 응용 프로그램을 이미 배포 했어야 하는 경우 [첫 번째](app-service-api-dotnet-get-started.md) 및 [두 번째](app-service-api-cors-consume-javascript.md) 자습서, toohello 건너뛸 [설정 앱 서비스 및 Azure AD에서 인증](#azureauth) 섹션.

Hello 첫 번째 및 두 번째 자습서 수행 하지 않고이 자습서 toofollow 않으려면 tooget 자동화 된 프로세스 toodeploy hello 샘플 응용 프로그램을 사용 하 여 시작 하는 방법에 대해 설명 된 단계를 따라 hello지 않습니다.

> [!NOTE]
> hello 다음 단계 수 있게 해 동일한 시작 지점을 한 가지 예외로 첫 두 자습서 hello 않은 마치 toohello: Visual Studio는 웹 응용 프로그램 또는 각 프로젝트에 배포 됩니다 API 앱을 이미 알고 되지 않습니다. 즉,이 자습서에서 설명 하는 정확한 지침을 가질 수 없습니다 방법을 toodeploy toohello 오른쪽 대상으로 합니다. 모두에 직접 toodo hello 배포 단계 하는 방법을 파악 합니다. 그렇지 않은 경우 hello에서 더 나은 toofollow hello 자습서 시리즈 [첫 번째 자습서](app-service-api-dotnet-get-started.md) 이 toostart 보다 배포 프로세스를 자동화 합니다.
> 
> 

1. 모든 hello hello에 나열 된 필수 구성 요소가 갖도록 [첫 번째 자습서](app-service-api-dotnet-get-started.md)합니다. 나열 된 추가 toohello 필수 조건, 이러한 인증 자습서 앱 서비스 웹 앱 및 Visual Studio에서 API 앱에 대해 작업 하는 Azure 포털 hello를 가정 합니다.
2. Hello 클릭 **tooAzure 배포** hello 단추 [tooDo 목록 샘플 리포지토리 추가 정보 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy hello API 앱 및 hello에 대 한 웹 앱입니다. 만들어진 hello Azure 리소스 그룹의 하므로 기록해이 이후 toolook 웹 앱 및 API 앱 이름은 사용할 수 있습니다.
3. 다운로드 또는 복제 hello [tooDo 목록 샘플 리포지토리](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) tooget hello 코드를 Visual Studio에서 로컬로으로 작업 하겠습니다.

## <a id="azureauth"></a> 앱 서비스와 Azure AD에서 인증 설정
Hello 응용 프로그램 사용자를 인증할 수 필요 없이 Azure 앱 서비스에서 실행 해야 합니다. 이 섹션에서는 hello 다음 작업을 수행 하 여 인증을 추가 합니다.

* Hello API 중간 계층 응용 프로그램을 호출 하는 것에 대 한 앱 서비스 toorequire Azure Active Directory (Azure AD) 인증을 구성 합니다.
* Azure AD 응용 프로그램을 만듭니다.
* 로그온 toohello AngularJS 프런트 엔드 후 hello Azure AD 응용 프로그램 toosend hello 전달자 토큰을 구성 합니다. 

다음 hello 자습서 방향 하는 동안 문제를 실행 하는 경우 참조 hello [문제 해결](#troubleshooting) hello 자습서의 hello 끝 섹션. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Hello 중간 계층 API 앱에 대 한 인증 구성
1. Hello에 [Azure 포털](https://portal.azure.com/), toohello 이동 **설정** hello ToDoListAPI 프로젝트에 대해 만든 hello API 앱의 블레이드에서 hello 찾습니다 **기능** 섹션, 한 다음 클릭 **인증 / 권한 부여**합니다.
   
    ![Azure 포털 인증/권한 부여](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **에**합니다.
3. Hello에 **요청이 인증 되지 않은 경우 동작 tootake** 드롭 다운 목록 **Azure Active Directory로 로그인**합니다.
   
    이 옵션을 사용 하면 unauathenticated 요청이 없는 hello API 앱에 도달 합니다. 
4. **인증 공급자** 아래에서 **Azure Active Directory**를 클릭합니다.
   
    ![Azure 포털 인증/권한 부여 블레이드](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Hello에 **Azure Active Directory 설정** 블레이드에서 클릭 **Express**
   
    ![Azure 포털 인증/권한 부여 Express 옵션](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Hello로 **Express** 옵션을 응용 프로그램 서비스 자동으로 만들 수는 Azure AD 응용 프로그램에서 Azure AD [테 넌 트](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant)합니다. 
   
    않아도 toocreate 테 넌 트 마다 Azure 계정이 자동으로 하나에 있기 때문에 있습니다.
6. 아래 **관리 모드**, 클릭 **새 AD 앱 만들기** 아직 선택 되지 않은 경우 hello에 있는 hello 값 **앱 만들기** 입력란;이 AAD를 조회 합니다 hello Azure 클래식 포털 나중에 응용 프로그램입니다.
   
    ![Azure 포털 Azure AD 설정](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure는 hello Azure AD 테 넌 트에 표시 된 이름으로 Azure AD 응용을 프로그램 자동으로 만듭니다. 기본적으로 hello Azure AD 응용 프로그램 이름은 hello API 응용 프로그램으로 hello 동일 합니다. 원하는 경우 다른 이름을 입력합니다.
7. **확인**을 클릭합니다.
8. Hello에 **인증 / 권한 부여** 블레이드에서 클릭 **저장**합니다.
   
    ![저장을 클릭합니다.](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

이제 Azure AD 테 넌 트의 사용자만 hello API 앱을 호출할 수 있습니다.

### <a name="optional-test-hello-api-app"></a>선택 사항: hello API 앱 테스트
1. 브라우저에서 toohello 앱의 URL을 hello API 이동: hello에 **API 앱** 아래 hello 링크를 클릭 하는 hello Azure 포털에서에서 블레이드 **URL**합니다.  
   
    사용자는 리디렉션된 tooa 로그인 화면 인증 되지 않은 요청이 tooreach hello API 앱 허용 되지 않습니다.
   
    브라우저에 "만들었습니다" toohello 페이지 되 면 hello 브라우저 이미 기록 될 수 있습니다에-경우에 InPrivate 또는 Incognito 창을 열고 toohello API 앱의 URL로 이동 합니다.
2. Azure AD의 사용자에 대한 자격 증명으로 로그온합니다.
   
    에 로그온 하는 hello "만들었습니다" 페이지 hello 브라우저에 나타납니다.
3. 닫기 hello 브라우저입니다.

### <a name="configure-hello-azure-ad-application"></a>Hello Azure AD 응용 프로그램 구성
Azure AD 인증을 구성하면 앱 서비스가 사용자에 대한 Azure AD 응용 프로그램을 만듭니다. 기본적으로 hello 새 Azure AD 응용 프로그램 구성 된 tooprovide hello 전달자 토큰 toohello API 앱의 URL을 했습니다. 이 섹션에서는 hello Azure AD 응용 프로그램 tooprovide hello 전달자 토큰 toohello AngularJS 프런트 엔드 직접 toohello 중간 계층 API 앱 대신 구성 합니다. hello AngularJS 프런트 엔드 hello API 앱을 호출할 때 hello 토큰 toohello API 앱을 보내집니다.

> [!NOTE]
> 이 자습서에서는 단일 Azure AD를 사용 가능한 한 단순하게 tookeep hello 프로세스 hello 프런트 엔드와 hello 중간 계층 API 앱에 대 한 응용 프로그램입니다. 두 번째 방법은 toouse 두 개의 Azure AD 응용 프로그램입니다. 이 경우 toogive hello 프런트 엔드 Azure AD 응용 프로그램 사용 권한 toocall hello 중간 계층의 Azure AD 응용 프로그램을 해야 했습니다. 이렇게 다중 응용 프로그램을 보다 상세하게 제어할 권한이 tooeach 계층 하면 합니다.
> 
> 

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 너무 이동**Azure Active Directory**합니다.
   
   필요한 특정 Azure Active Directory 설정을 액세스할 tooare hello 현재 Azure 포털에서 아직 사용할 수 있기 때문에 toouse hello 클래식 포털을 해야 합니다.
2. Hello에 **디렉터리** 탭에서 AAD 테 넌 트를 클릭 합니다.
   
   ![클래식 포털에서 Azure AD](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. 클릭 **응용 프로그램 > 회사가 보유 한 응용 프로그램**, 다음 hello 확인 표시를 클릭 합니다.
   
   또한 toorefresh hello 페이지 toosee hello 새 응용 프로그램을 할 수 있습니다.
4. 응용 프로그램의 hello 목록에서의 Azure API 앱에 대 한 인증을 사용 하는 경우 한 만든 하나 hello hello 이름을 클릭 합니다.
   
   ![Azure AD 응용 프로그램 탭](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. **Configure**를 클릭합니다.
   
   ![Azure AD 구성 탭](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. 설정 **로그온 URL** 후행 슬래시가 없는지 AngularJS 웹 응용 프로그램에 대 한 toohello URL입니다.
   
   예: https://todolistangular.azurewebsites.net
   
   ![로그온 URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. 설정 **회신 URL** 후행 슬래시가 없는지 웹 응용 프로그램에 대 한 toohello URL입니다.
   
   예: https://todolistsangular.azurewebsites.net
8. **저장**을 클릭합니다.
   
   ![회신 URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Hello hello 페이지의 아래쪽에 있는 클릭 **관리 매니페스트 > 다운로드 매니페스트**합니다.
   
   ![매니페스트 다운로드](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. 편집할 수 있는 hello 파일 tooa 위치를 다운로드 합니다.
11. 다운로드 한 hello 매니페스트 파일에서 hello에 대 한 검색 `oauth2AllowImplicitFlow` 속성입니다. 이 속성의 값을 hello 변경 `false` 너무`true`, hello 파일을 저장 합니다.
    
    이 설정은 JavaScript 단일 페이지 응용 프로그램에서 액세스를 위해 필요합니다. Hello Oauth 2.0 전달자 토큰 toobe를 hello URL 조각에 반환 된 수 있습니다.
12. 클릭 **관리 매니페스트 > 업로드 매니페스트**, 및 업로드 hello 파일 hello 앞 단계에서에서 업데이트 합니다.
    
    ![매니페스트 업로드](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. 복사 hello **클라이언트 ID** 값 및에서 나중에 가져올 수 위치를 저장 합니다.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Hello ToDoListAngular 프로젝트 toouse 인증 구성
이 섹션에 JS tooacquire Azure AD에서 사용자 로그온 hello에 대 한 전달자 토큰에 대 한 Active Directory 인증 라이브러리 (ADAL)를 사용 하도록 hello AngularJS 프런트 엔드를 변경 합니다. hello 코드는 hello 다음 다이어그램에에서 나와 있는 것 처럼 hello 토큰 toohello 중간 계층 전송 된 HTTP 요청에 포함 됩니다. 

![사용자 인증 다이어그램](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Hello 변경 toofiles hello ToDoListAngular 프로젝트에서 다음을 확인 합니다.

1. 열기 hello *index.cshtml* 파일입니다.
2. JS 스크립트에 대 한 Active Directory 인증 라이브러리 (ADAL) hello를 참조 하는 hello 줄 주석 처리를 제거 합니다.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. 열기 hello *app/scripts/app.js* 파일입니다.
4. Hello 코드 블록의 주석 없이"인증" 용으로 표시 및 hello 코드 블록을 표시 "와 인증"에 대 한 주석 처리를 제거 합니다.
   
    이 변경은 hello ADAL JS 인증 공급자를 참조 하 고 구성 값 tooit를 제공 합니다. 단계를 수행 하는 hello API 앱 및 Azure AD 응용 프로그램에 대 한 hello 구성 값을 설정 합니다.
5. Hello를 설정 하는 hello 코드에서 `endpoints` hello ToDoListAPI 프로젝트에 대해 생성 하 고 설정 하는 hello API 앱의 변수, 설정 hello API URL toohello URL hello Azure AD 응용 프로그램 ID toohello 클라이언트 ID hello Azure 클래식 포털에서에서 복사 합니다.
   
    다음 예제와 비슷한 toohello hello 코드가 되었습니다.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. 너무 hello 호출`adalProvider.init`설정, `tenant` tooyour 테 넌 트 이름 및 `clientId` hello 이전 단계에서 사용한 toosame 값입니다.
   
    다음 예제와 비슷한 toohello hello 코드가 되었습니다.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    이러한 변경 너무`app.js` hello 호출 하는 코드와 API를 호출 하는 hello hello 동일한 Azure AD 응용 프로그램에는 지정 합니다.
7. 열기 hello *app/scripts/homeCtrl.js* 파일입니다.
8. Hello 코드 블록의 주석 없이"인증" 용으로 표시 및 hello 코드 블록을 표시 "와 인증"에 대 한 주석 처리를 제거 합니다.
9. 열기 hello *app/scripts/indexCtrl.js* 파일입니다.
10. Hello 코드 블록의 주석 없이"인증" 용으로 표시 및 hello 코드 블록을 표시 "와 인증"에 대 한 주석 처리를 제거 합니다.

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Hello ToDoListAngular 프로젝트 tooAzure 배포
1. **솔루션 탐색기**hello ToDoListAngular 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.
2. **게시**를 클릭합니다.
   
    Visual Studio hello 프로젝트를 배포 하 고 브라우저 toohello 웹 앱의 기본 URL을 엽니다. 이 정상 시도 toogo tooa 웹 API 기본 URL에 대 한 브라우저에서 403 오류 페이지를 표시 됩니다.
   
    해야 toomake 변경 toohello 중간 계층 API 앱 hello 응용 프로그램을 테스트 합니다.
3. 닫기 hello 브라우저입니다.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Hello ToDoListAPI 프로젝트 toouse 인증 구성
현재 프로젝트 보냅니다 ToDoListAPI hello "*" hello로 `owner` 값 tooToDoListDataAPI 합니다. 이 섹션의 hello 코드 toosend hello ID hello 로그온 한 사용자의 변경할 수 있습니다.

Hello hello ToDoListAPI 프로젝트의 변경 내용을 다음을 확인 합니다.

1. 열기 hello *Controllers/ToDoListController.cs* 파일, 및에서 설정 하는 각 작업 메서드에 hello 줄의 주석 처리 제거 `owner` toohello Azure AD `NameIdentifier` 클레임 값입니다. 예:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **중요 한**: hello의 코드를 주석 처리를 제거 하지 않는 `ToDoListDataAPI` 메서드가 작업입니다 나중에 서비스 사용자 인증 자습서 hello에 대 한 합니다.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Hello ToDoListAPI 프로젝트 tooAzure 배포
1. **솔루션 탐색기**hello ToDoListAPI 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.
2. **게시**를 클릭합니다.
   
    Visual Studio hello 프로젝트를 배포 하 고 브라우저 toohello API 앱의 기본 URL을 엽니다.
3. 닫기 hello 브라우저입니다.

### <a name="test-hello-application"></a>Hello 응용 프로그램 테스트
1. Hello 웹 앱의 URL을 toohello 이동 **HTTP가 아닌 HTTPS를 사용 하 여**합니다.
2. Hello 클릭 **tooDo 목록** 탭 합니다.
   
    증명된 toolog 됩니다.
3. AAD 테 넌 트에 사용자의 hello 자격 증명으로 로그인 합니다.
4. hello **tooDo 목록** 페이지가 나타납니다.
   
   ![tooDo 목록 페이지](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   지금까지는 모두 소유자 "*"에 대한 것이기 때문에 할 일 항목이 표시되지 않습니다. 이제 hello 중간 계층이 hello 로그인 한 사용자에 대 한 항목을 요청 none 아직을 만들지 않았습니다.
5. Hello 응용 프로그램이 작동 하는 새 할 일 항목 tooverify를 추가 합니다.
6. 다른 브라우저 창에서 hello ToDoListDataAPI API 앱에 대 한 UI Swagger URL toohello 이동를 클릭 **ToDoList > 가져오기**합니다. Hello에 대 한 별표를 입력 `owner` 매개 변수를 클릭 한 다음 **기능 직접 사용해**합니다.
   
   hello 응답 hello 새 할 일 항목 hello 소유자 속성에서 hello 실제 Azure AD 사용자 ID를 갖도록 표시 됩니다.
   
   ![JSON 응답에서 소유자 ID](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>처음부터 hello 프로젝트 빌드
hello를 사용 하 여 hello 두 웹 API 프로젝트가 만들어진 **Azure API 앱** 프로젝트 템플릿 및 hello 기본 값 컨트롤러와 ToDoList 컨트롤러 교체 합니다. 

방법에 대 한 정보는 너무 Web API 2 백 엔드에서 AngularJS 단일 페이지 응용 프로그램을 만들기, 참조 [손에에 랩: 빌드는 단일 페이지 응용 프로그램 (SPA) ASP.NET Web API와 Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs)합니다. 방법에 대 한 정보에 대 한 Azure AD 인증 코드 tooadd hello 다음 리소스를 참조 하세요.:

* [Azure AD를 사용하여 AngularJS 단일 페이지 앱 보안 유지](../active-directory/active-directory-devquickstarts-angular.md)
* [ADAL JS v1 소개](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>문제 해결
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* ToDoListAPI(중간 계층) 및 ToDoListDataAPI(데이터 계층)를 혼동하지 않아야 합니다. 예를 들어 인증 toohello 중간 계층 API 앱을 하지 hello 데이터 계층 추가 되었는지 확인 합니다. 
* 올바른지 확인 (ToDoListAPI, 하지 ToDoListDataAPI) hello AngularJS 소스 코드 참조 hello 중간 계층 API 응용 프로그램 URL 및 hello Azure AD 클라이언트 id입니다. 

## <a name="next-steps"></a>다음 단계
이 자습서에서는 toouse API 앱에 대 한 앱 서비스 인증 및 방법을 사용 하 여 API 앱 hello를 toocall ADAL JS 라이브러리 hello 방법을 배웠습니다. 다음 자습서 hello 알아봅니다 너무 어떻게[서비스 간 시나리오에 대 한 보안 액세스 tooyour API 앱](app-service-api-dotnet-service-principal-auth.md)합니다.

