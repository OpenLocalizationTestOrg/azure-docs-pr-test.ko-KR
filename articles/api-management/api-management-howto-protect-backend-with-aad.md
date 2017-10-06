---
title: "Azure Active Directory 및 API 관리 웹 API 백 엔드 aaaProtect | Microsoft Docs"
description: "자세한 내용은 방법 tooprotect을 웹 API 백 엔드 Azure Active Directory 및 API 관리 합니다."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>어떻게 tooprotect을 웹 API 백 엔드 Azure Active Directory 및 API 관리
비디오 표시 방법을 따르는 hello toobuild 웹 API 백 엔드 고 OAuth 2.0 프로토콜을 사용 하 여 Azure Active Directory 및 API 관리를 보호 합니다.  Hello 비디오에서 단계 hello에 대 한 추가 정보 및이 문서 개요를 제공 합니다. 이 24분 비디오에서는 다음을 수행할 수 있는 방법을 보여줍니다.

* Web API 백 엔드 빌드 및 AAD로 보안 유지 - 1시 30분에 시작
* API 관리-7시 10분부터 hello API 가져오기
* Hello 개발자 포털 toocall hello API-9시 09분부터 구성
* 데스크톱 응용 프로그램 toocall hello API-18시 08분에서 시작 구성
* JWT 유효성 검사 정책 toopre 구성-요청 수-20시 47분부터 권한 부여

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Azure AD 디렉터리 만들기
웹 API 있어야 하는 Azure Active Directory를 사용 하 여 백업 toosecure는 AAD 테 넌 트가 있습니다. 이 비디오에서는 **APIMDemo** 라는 테넌트가 사용됩니다. AAD 테 넌 트가 toocreate 로그인 toohello [Azure 클래식 포털](https://manage.windowsazure.com) 클릭 **새로**->**응용 프로그램 서비스**->**Active 디렉터리**->**디렉터리**->**사용자 지정 만들기**합니다. 

![Azure Active Directory][api-management-create-aad-menu]

이 예에서 **APIMDemo**라는 디렉터리는 **DemoAPIM.onmicrosoft.com**이라는 기본 도메인 이름으로 만들어집니다. 이 디렉터리는 hello 비디오 전체에서 사용 됩니다.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Azure Active Directory로 보안이 유지된 Web API 서비스 만들기
이 단계에서는 Web API 백 엔드는 Visual Studio 2013을 사용하여 생성됩니다. Hello 비디오의이 단계 1시 30분부터 시작합니다. Visual Studio에서 toocreate 웹 API 백 엔드 프로젝트 **파일**->**새로**->**프로젝트**, 선택 **ASP.NET 웹 응용 프로그램** hello에서 **웹** 템플릿 목록입니다. 이 비디오 hello 프로젝트 이름은 **APIMAADDemo**합니다. 클릭 **확인** toocreate hello 프로젝트. 

![Visual Studio][api-management-new-web-app]

클릭 **웹 API** hello에서 **템플릿 목록 선택** toocreate 웹 API 프로젝트입니다. Azure Directory 인증 tooconfigure 클릭 **인증 변경**합니다.

![새 프로젝트][api-management-new-project]

클릭 **조직 계정**, hello 지정 **도메인** AAD 테 넌 트의 합니다. 이 예제에서는 hello 도메인은 **DemoAPIM.onmicrosoft.com**. hello에서 디렉터리의 hello 도메인을 가져올 수 있습니다 **도메인** 디렉터리의 탭 합니다.

![도메인][api-management-aad-domains]

Hello에서 원하는 hello 설정을 구성 **인증 변경** 대화 상자와 클릭 **확인**합니다.

![인증 변경][api-management-change-authentication]

클릭할 때 **확인** Visual Studio는 tooregister Azure AD 디렉터리와 응용 프로그램 변수와 Visual Studio에서의 증명된 toosign 될 수 있습니다. 디렉터리에 대한 관리 계정을 사용하여 로그인합니다.

![TooVisual Studio에 로그인][api-management-sign-in-vidual-studio]

tooconfigure Azure 웹 API 검사 hello로이 프로젝트에 대 한 상자 **hello 클라우드의 호스트에에서** 클릭 하 고 **확인**합니다.

![새 프로젝트][api-management-new-project-cloud]

TooAzure에서 증명된 toosign 수 및 다음 hello 웹 응용 프로그램을 구성할 수 있습니다.

![구성][api-management-configure-web-app]

이 예에서는 **APIMAADDemo**라는 새 **App Service 계획**이 지정됩니다.

클릭 **확인** tooconfigure hello 웹 앱을 hello 프로젝트를 만듭니다.

## <a name="add-hello-code-toohello-web-api-project"></a>Hello 코드 toohello 웹 API 프로젝트 추가
hello hello 비디오의 다음 단계는 hello 코드 toohello 웹 API 프로젝트를 추가합니다. 이 단계는 4분 35초에 시작됩니다.

이 예에서 웹 API hello 모델과 컨트롤러를 사용 하 여 기본 계산기 서비스를 구현 합니다. hello 서비스에 대 한 tooadd hello 모델 마우스 오른쪽 단추로 클릭 **모델** 에 **솔루션 탐색기** 선택 **추가**, **클래스**합니다. Hello 클래스 이름을 `CalcInput` 클릭 **추가**합니다.

Hello 다음 추가 `using` 문 toohello 맨 hello `CalcInput.cs` 파일입니다.

```c#
using Newtonsoft.Json;
```

Replace hello 코드 다음 hello를 사용 하 여 클래스를 생성 합니다.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

**솔루션 탐색기**에서 **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 **추가**->**컨트롤러**를 선택합니다. **Web API 2 컨트롤러 - 비어 있음**을 선택하고 **추가**를 클릭합니다. 형식 **CalcController** hello 컨트롤러에 대 한 이름을 지정 하 고 클릭 **추가**합니다.

![컨트롤러 추가][api-management-add-controller]

Hello 다음 추가 `using` 문 toohello 맨 hello `CalcController.cs` 파일입니다.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Replace hello 코드 다음 hello를 사용 하 여 컨트롤러 클래스를 생성 합니다. 이 코드 구현 hello `Add`, `Subtract`, `Multiply`, 및 `Divide` hello 기본 계산기 API의 작업입니다.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

키를 눌러 **F6** toobuild hello 솔루션을 확인 합니다.

## <a name="publish-hello-project-tooazure"></a>Hello 프로젝트 tooAzure 게시
이 단계 hello Visual Studio 프로젝트는 게시 된 tooAzure입니다. 이 단계를 hello 비디오 5시 45분에서 시작 됩니다.

toopublish 프로젝트 tooAzure hello, hello를 마우스 오른쪽 단추로 클릭 **APIMAADDemo** Visual Studio에서 프로젝트를 마우스 선택 **게시**합니다. Hello hello 기본 설정을 유지 **웹 게시** 대화 상자와 클릭 **게시**합니다.

![웹 게시][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Azure AD toohello 백 엔드 서비스 응용 프로그램 사용 권한 부여
Hello 백 엔드 서비스에 대 한 새 응용 프로그램 부분 hello 구성 및 게시 프로세스의 웹 API 프로젝트에 Azure AD 디렉터리에 만들어집니다. Hello 비디오의이 단계에서는 6시 13분부터 권한은 부여 toohello 웹 API 백 엔드 합니다.

![응용 프로그램][api-management-aad-backend-app]

Hello 응용 프로그램 tooconfigure hello 필요한 사용 권한 hello 이름을 클릭 합니다. Toohello 이동 **구성** 탭과 toohello 아래로 스크롤하여 **tooother 응용 프로그램 사용 권한** 섹션. Hello 클릭 **응용 프로그램 사용 권한** 옆에 있는 드롭 다운 **Windows** **Azure Active Directory**에 대 한 hello 확인란 **디렉터리데이터읽기**를 클릭 하 고 **저장**합니다.

![권한 추가][api-management-aad-add-permissions]

> [!NOTE]
> 경우 **Windows** **Azure Active Directory** 가 나타나지 않으면 tooother 응용 프로그램 사용 권한 아래에서 클릭 **응용 프로그램을 추가** hello 목록에서 추가 합니다.
> 
> 

Hello 메모 **앱 Id URI** hello API 관리 개발자 포털에 대 한 Azure AD 응용 프로그램 구성 된 경우 이후 단계에서 사용 하도록 합니다.

![앱 ID URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>가져오기 hello API 관리에 웹 API
Api는 hello Azure 포털을 통해 액세스할 수 있는 hello API 게시자 포털에서 구성 됩니다. tooreach, 클릭 **게시자 포털** API 관리 서비스의 hello 도구 모음에서 합니다. API 관리 서비스 인스턴스를 아직 만들지 않은 경우 참조 [API 관리 서비스 인스턴스를 만들] [ Create an API Management service instance] hello에 [첫 번째 API 관리] [ Manage your first API] 자습서입니다.

![게시자 포털][api-management-management-console]

작업 수 [tooAPIs를 수동으로 추가](api-management-howto-add-operations.md), 가져왔거나 가져올 수 있습니다. 이 비디오에서는 작업을 6분 40초부터 Swagger 형식으로 가져옵니다.

라는 파일을 만들어 `calcapi.json` 와 콘텐츠를 따르고 tooyour 컴퓨터를 저장 합니다. 해당 hello 확인 `host` 특성 tooyour 웹 API 백 엔드를 가리킵니다. 이 예에서는 `"host": "apimaaddemo.azurewebsites.net"` 가 사용됩니다.

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

tooimport hello 계산기 API 클릭 **Api** hello에서 **API 관리** 를 hello 왼쪽, 클릭 한 다음 메뉴 **가져오기 API**합니다.

![API 가져오기 단추][api-management-import-api]

Hello 단계 tooconfigure hello 계산기 API 다음을 수행 합니다.

1. 클릭 **파일에서**, toohello 찾아보기 `calculator.json` 파일을 저장 하 고 hello 클릭 **Swagger** 라디오 단추입니다.
2. 형식 **calc** hello에 **웹 API URL 접미사** 텍스트 상자에 붙여넣습니다.
3. Hello에 클릭 **(선택 사항) 제품** 확인란을 선택한 **스타터**합니다.
4. 클릭 **저장** tooimport hello API입니다.

![새 API 추가][api-management-import-new-api]

가져온 hello API는 hello hello API에 대 한 요약 페이지에에서 표시 됩니다 hello 게시자 포털.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Hello 개발자 포털에서 실패 한 hello API를 호출
이 시점에서 hello API API 관리에 가져온 하지만 없습니다 아직에서 호출할 수 성공적으로 hello 개발자 포털 hello 백 엔드 서비스는 Azure AD 인증으로 보호 되어야 하기 때문에 있습니다. 이 단계를 수행 하는 hello를 사용 하 여 7시 40분에서 시작 하는 hello 비디오에서 보여 줍니다.

클릭 **개발자 포털** hello 게시자 포털의 상단 오른쪽 면 hello에서에서 합니다.

![개발자 포털][api-management-developer-portal-menu]

클릭 **Api** hello 클릭 **계산기** API입니다.

![개발자 포털][api-management-dev-portal-apis]

**사용해 보세요**를 클릭합니다.

![시도][api-management-dev-portal-try-it]

클릭 **보낼** 의 hello 응답 상태를 확인 하 고 **401 권한 없음**합니다.

![보내기][api-management-dev-portal-send-401]

hello 백 엔드 API은 Azure Active Directory로 보호 되어 hello 요청이 인증 되지 않습니다. 성공적으로 hello API를 호출 하기 전에 hello 개발자 포털 구성된 tooauthorize 개발자가 OAuth 2.0을 사용 해야 합니다. 이 프로세스는 hello 다음 섹션에에서 설명 되어 있습니다.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Hello 개발자 포털 AAD 응용 프로그램으로 등록
OAuth 2.0을 사용 하 여 hello 개발자 포털 tooauthorize 개발자 구성 hello 첫 번째 단계는 AAD 응용 프로그램으로 tooregister hello 개발자 포털을 것입니다. 이 8:27 hello 비디오에서에서 시작 하는 보여 줍니다.

이 예에서이 비디오의 hello 첫 번째 단계에서 toohello Azure AD 테 넌 트 탐색 **APIMDemo** toohello 이동 **응용 프로그램** 탭 합니다.

![새 응용 프로그램][api-management-aad-new-application-devportal]

Hello 클릭 **추가** toocreate 새 Azure Active Directory 응용 프로그램 단추 선택한 **조직에서 개발 중인 응용 프로그램 추가**합니다.

![새 응용 프로그램][api-management-new-aad-application-menu]

선택 **웹 응용 프로그램 및/또는 Web API**는 이름을 입력 하 고 hello 다음 화살표를 클릭 합니다. 이 예에서는 **APIMDeveloperPortal** 이 사용됩니다.

![새 응용 프로그램][api-management-aad-new-application-devportal-1]

에 대 한 **로그온 URL** API 관리 서비스의 hello URL을 입력 하 고 추가 `/signin`합니다. 이 예에서는 `https://contoso5.portal.azure-api.net/signin` 가 사용됩니다.

에 대 한 **앱 Id URL** API 관리 서비스의 hello URL을 입력 하 고 몇 가지 고유한 문자를 추가 합니다. 원하는 문자를 사용할 수 있으며 이 예에서는 `https://contoso5.portal.azure-api.net/dp`이(가) 사용됩니다. Hello 필요한 경우 **앱 속성** 됩니다 구성 hello 확인 표시가 toocreate hello 응용 프로그램을 클릭 합니다.

![새 응용 프로그램][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>API 관리 OAuth 2.0 권한 부여 서버 구성
hello 다음 단계는 tooconfigure API 관리에서 OAuth 2.0 권한 부여 서버입니다. 이 단계를 hello 9:43 일에서 시작 비디오에서 보여 줍니다.

클릭 **보안** hello 왼쪽에 hello API 관리 메뉴에서 클릭 **OAuth 2.0**, 클릭 하 고 **추가 권한 부여** 서버입니다.

![권한 부여 서버 추가][api-management-add-authorization-server]

Hello에는 이름 및 선택적 설명을 입력 **이름** 및 **설명** 필드입니다. 이러한 필드는 hello API 관리 서비스 인스턴스 내에서 사용 되는 tooidentify hello OAuth 2.0 권한 부여 서버입니다. 이 예에서 **권한 부여 서버 데모** 가 사용됩니다. 나중에 API에 대 한 인증에 사용 되는 OAuth 2.0 서버 toobe를 지정할 때이 이름을 선택 합니다.

Hello에 대 한 **클라이언트 등록 페이지 URL** 같은 자리 표시자 값을 입력 `http://localhost`합니다.  hello **클라이언트 등록 페이지 URL** toohello 페이지가 사용 하는 지점 toocreate를 사용 하 여를 업데이트 하 고 계정의 사용자 관리를 지 원하는 OAuth 2.0 공급자에 대 한 자신의 계정을 구성할 수 있습니다. 이 예에서 자리 표시자를 사용하도록 사용자는 자신의 계정을 만들거나 구성하지 않습니다.

![권한 부여 서버 추가][api-management-add-authorization-server-1]

그런 다음 **권한 부여 끝점 URL** 및**토큰 끝점 URL**을 지정합니다.

![권한 부여 서버][api-management-add-authorization-server-1a]

Hello에서 이러한 값을 검색할 수 **앱 끝점** hello hello 개발자 포털에 대해 생성 되는 AAD 응용 프로그램의 페이지입니다. tooaccess hello 끝점 이동 toohello **구성** hello AAD 응용 프로그램에 대 한 탭을 클릭 **끝점 보기**합니다.

![응용 프로그램][api-management-aad-devportal-application]

![끝점 보기][api-management-aad-view-endpoints]

복사 hello **OAuth 2.0 권한 부여 끝점** hello에 붙여 넣습니다 **권한 부여 끝점 URL** 텍스트 상자에 붙여넣습니다.

![권한 부여 서버 추가][api-management-add-authorization-server-2]

복사 hello **OAuth 2.0 토큰 끝점** hello에 붙여 넣습니다 **끝점 URL 토큰** 텍스트 상자에 붙여넣습니다.

![권한 부여 서버 추가][api-management-add-authorization-server-2a]

Hello 토큰 끝점에 toopasting 라는 추가 본문 매개 변수를 추가 하는 또한 **리소스** hello 값에 대 한 hello를 사용 하 여 **앱 Id URI** hello hello 백 엔드 서비스는 AAD 응용 프로그램에서 hello Visual Studio 프로젝트를 게시할 때 만들어집니다.

![앱 ID URI][api-management-aad-sso-uri]

다음으로 hello 클라이언트 자격 증명을 지정 합니다. 원하는 hello 리소스에 대 한 자격 증명 hello 이들은 tooaccess,이 경우 개발자 포털을 hello 합니다.

![클라이언트 자격 증명][api-management-client-credentials]

tooget hello **클라이언트 Id**, toohello 이동 **구성** hello hello 개발자 포털 및 복사 hello에 대 한 AAD 응용 프로그램의 탭 **클라이언트 Id**합니다.

tooget hello **클라이언트 암호** hello 클릭 **기간 선택** 드롭 다운 hello **키** 섹션 고 간격을 지정 합니다. 이 예제에서는 1년을 사용합니다.

![클라이언트 ID][api-management-aad-client-id]

클릭 **저장** toosave hello 구성 및 표시 hello 키입니다. 

> [!IMPORTANT]
> 이 키를 기록해 둡니다. Hello Azure Active Directory 구성 창을 닫으면 되 면 hello 키를 다시 표시할 수 없습니다.
> 
> 

Hello 키 toohello 클립보드로 복사, 스위치 백 toohello 게시자 포털 hello에 hello 키를 붙여 **클라이언트 암호** 입력란을 클릭 하 고 **저장**합니다.

![권한 부여 서버 추가][api-management-add-authorization-server-3]

바로 뒤에 따라오는 hello 클라이언트 자격 증명은 인증 코드 부여 합니다. 이 권한 부여 코드를 복사 하 고 스위치 백 tooyour Azure AD 개발자 포털 응용 프로그램 페이지 및 hello 인증 부여 hello에 붙여 **회신 URL** 필드를 클릭 **저장** 다시 합니다.

![회신 URL][api-management-aad-reply-url]

hello 다음 단계는 hello 개발자 포털 AAD 응용 프로그램에 대 한 tooconfigure hello 권한입니다. 클릭 **응용 프로그램 사용 권한** hello 상자를 선택 하 고 **디렉터리 데이터 읽기**합니다. 클릭 **저장** toosave 변경 하 고 클릭이 **응용 프로그램을 추가**합니다.

![권한 추가][api-management-add-devportal-permissions]

Hello 검색 아이콘을 클릭 형식 **APIM** hello에 선택 상자 부터는 **APIMAADDemo**, hello 확인 표시가 toosave를 클릭 합니다.

![권한 추가][api-management-aad-add-app-permissions]

클릭 **위임 된 권한** 에 대 한 **APIMAADDemo** hello 상자를 선택 하 고 **액세스 APIMAADDemo**를 클릭 하 고 **저장**합니다. 이렇게 하면 hello 개발자 포털 응용 프로그램 tooaccess hello 백 엔드 서비스.

![권한 추가][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Hello 계산기 API에 대 한 OAuth 2.0 사용자 권한 부여를 사용 하도록 설정
Hello OAuth 2.0 서버를 구성 하는 이제 API에 대 한 hello 보안 설정에서 지정할 수 있습니다. 이 단계를 hello 14시 30분부터 비디오에서 보여 줍니다.

클릭 **Api** 에서 왼쪽된 메뉴 hello 하 고 클릭 **계산기** tooview 하 고 해당 설정을 구성 합니다.

![계산기 API][api-management-calc-api]

Toohello 이동 **보안** 탭에서 확인 hello **OAuth 2.0** 확인란을 선택 하는 hello 원하는 권한 부여 서버 hello에서 **권한 부여 서버** 드롭 다운 클릭 **저장**합니다.

![계산기 API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Hello 개발자 포털에서 hello 계산기 API를 호출 했습니다.
Hello API에 hello OAuth 2.0 권한 부여가 구성 된 했으므로 hello 개발자 센터에서 해당 작업을 성공적으로 호출할 수 있습니다. 이 단계를 hello 15시 시작 비디오에서 보여 줍니다.

뒤로 toohello 이동 **정수 두 개를 추가** hello 개발자 포털에서 hello 계산기 서비스의 작동 **실습**합니다. 참고 hello hello에 새 항목이 **권한 부여** 방금 추가한 해당 toohello 권한 부여 서버 섹션.

![계산기 API][api-management-calc-authorization-server]

선택 **인증 코드** hello 권한 부여 드롭다운 목록에서에서 나열 하 고 hello 계정 toouse의 hello 자격 증명을 입력 합니다. Hello 계정을 사용 하 여 이미 로그인 한 경우에 사용자에 메시지가 나타나지 않을.

![계산기 API][api-management-devportal-authorization-code]

클릭 **보낼** 및 참고 hello **응답 상태** 의 **200 확인** 및 hello 응답 콘텐츠 hello 연산의 hello 결과입니다.

![계산기 API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>데스크톱 응용 프로그램 toocall hello API를 구성 합니다.
hello hello 비디오의 다음 절차는 16시 30분부터 시작 하 고 간단한 데스크톱 응용 프로그램 toocall hello API를 구성 합니다. hello 첫 번째 단계는 tooregister hello 데스크톱 응용 프로그램에서 Azure AD는 하 고 액세스 toohello 디렉터리와 toohello 백 엔드 서비스를 제공 합니다. 18:25 hello 데스크톱 응용 프로그램 호출 hello 계산기 API에 대 한 작업의 데모가 있습니다.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>JWT 유효성 검사 정책 toopre 구성-요청 권한 부여
hello hello 비디오에서 마지막 절차에서 시작 20시 48분을 표시 하는 toouse hello [JWT의 유효성을 검사](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) 정책 toopre-들어오는 각 요청의 hello 액세스 토큰을 확인 하 여 요청 권한을 부여 합니다. Hello 요청 hello 정책 JWT의 유효성을 검사 하 여 검증 되지 않은 경우 hello 요청 API 관리에 의해 액세스가 차단 되 고 toohello 백 엔드를 따라 전달 되지 않습니다.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

다른 구성 하 고이 정책을 사용 하 여 데모를 보려면을 참조 하십시오. [클라우드 포괄 에피소드 177: 더욱 API 관리 기능](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) too13:50 빨리 감기 및 합니다. Hello 정책 편집기에 구성 된 toosee hello 정책이 too15:00를 빨리 감기 및 too18:50 모두와 사용 하지 않는 hello hello 개발자 포털에서 호출 하는 작업의 데모에 대 한 권한 부여 토큰을 필요로 하는 다음 합니다.

## <a name="next-steps"></a>다음 단계
* API 관리에 대한 추가 [비디오](https://azure.microsoft.com/documentation/videos/index/?services=api-management) 를 확인합니다.
* 다른 방법으로 toosecure에 대 한 백 엔드 서비스에서 참조 [상호 인증서 인증](api-management-howto-mutual-certificates.md)합니다.

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
