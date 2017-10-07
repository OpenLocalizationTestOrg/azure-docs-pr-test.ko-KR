---
title: "앱 서비스에서 지 원하는 aaaCORS | Microsoft Docs"
description: "Azure Azure 앱 서비스의 CORS toouse를 지 원하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>CORS를 사용하여 JavaScript에서 API 앱 사용
앱 서비스 제공에 대 한 기본 제공 지원 [교차 원본 자원 공유 (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), tooAPIs API 앱에서 호스트 되는 호출 JavaScript 클라이언트 toomake 도메인 간 할 수 있게 합니다. 앱 서비스 API에는 모든 코드를 작성 하지 않고도 CORS 액세스 tooyour API를 구성할 수 있습니다.

이 문서에는 다음과 같은 두 섹션이 포함되어 있습니다.

* hello [어떻게 tooconfigure CORS](#corsconfig) 섹션에서는 일반적인 방법에 설명 모든 API 앱, 웹 응용 프로그램 또는 모바일 앱에 대 한 CORS tooconfigure 합니다. 응용 프로그램 서비스,.NET, Node.js, Java 등에서 지원 되는 tooall 프레임 워크 똑같이 합니다. 
* Hello로 시작 [hello.NET 시작 하기 자습서를 계속](#tutorialstart) 섹션 hello 문서는 CORS 지원에서 수행한 작업에 구축 하 여 보여 주는 자습서 [hello 첫 번째 API 앱 시작된 자습서 ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>어떻게 tooconfigure Azure 앱 서비스의 CORS
Hello Azure 포털에서에서 또는 사용 하 여 CORS를 구성할 수 있습니다 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 도구입니다.

#### <a name="configure-cors-in-hello-azure-portal"></a>Hello Azure 포털에서에서 CORS를 구성 합니다.
1. 브라우저에서 toohello 이동 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **응용 프로그램 서비스**, 다음 API 앱의 hello 이름을 클릭 하 고 있습니다.
   
    ![포털에서 API 앱 선택](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Hello에 **설정** hello toohello 오른쪽에 열리는 블레이드 **API 앱** 블레이드, 찾기 hello **API** 섹션을 선택한 다음 클릭 **CORS**합니다.
   
   ![설정 블레이드에서 CORS 선택](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Hello 텍스트 상자에 hello tooallow JavaScript 호출 toocome에서 원하는 Url 또는 URL을 입력 합니다.

    예를 들어 todolistangular 명명 된 JavaScript 응용 프로그램 tooa 웹 앱을 배포한 경우 "https://todolistangular.azurewebsites.net"를 입력 합니다. 대신 모든 원본 도메인이 허용 되는 별표 (*) toospecify를 입력할 수 있습니다.


1. **Save**를 클릭합니다.
   
   ![저장을 클릭합니다.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   클릭 한 후 **저장**, hello API 앱에는 JavaScript 수락할 호출 hello에서 Url을 지정 합니다.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Azure 리소스 관리자 도구를 사용하여 CORS 구성
사용 하 여 API 앱에 대 한 CORS를 구성할 수도 있습니다 [Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) 와 같은 명령줄 도구에서 [Azure PowerShell](/powershell/azureps-cmdlets-docs) 및 hello [Azure CLI](../cli-install-nodejs.md)합니다. 

Hello CORS 속성을 설정 하는 Azure 리소스 관리자 템플릿의 예제를 열고 hello [이 자습서에서는 샘플 응용 프로그램에 대 한 hello 리포지토리에 azuredeploy.json 파일](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json)합니다. 다음 예제는 hello 같은 hello 템플릿의 hello 섹션을 찾습니다.

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Hello.NET-시작 자습서를 계속합니다.
Hello Node.js 또는 Java 시작 시리즈 API 앱에 대 한를 따르는 경우 완료 된 hello 시작된 시리즈 시작 해야 합니다. Toohello 건너뛸 [다음 단계](#next-steps) 추가 API 앱에 대 한 학습을 위한 toofind 제안을 섹션.

hello이 문서의 나머지 부분에서는 연속 된 hello.NET 시작 시리즈 및 성공적으로 완료 했다고 가정 [hello 첫 번째 자습서](app-service-api-dotnet-get-started.md)합니다.

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Hello ToDoListAngular 프로젝트 tooa 새 웹 응용 프로그램 배포
[hello 첫 번째 자습서](app-service-api-dotnet-get-started.md), 중간 계층 API 앱 및 데이터 계층 API 앱을 생성 합니다. 이 자습서는 단일 페이지 응용 프로그램 (SPA) 웹 응용 프로그램 호출 hello 중간 계층 API 앱을 만듭니다. Hello SPA toowork hello 중간 계층 API 앱에서 CORS tooenable를 구조가 있습니다. 

Hello에 [ToDoList 샘플 응용 프로그램](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular 프로젝트는 hello 중간 계층 ToDoListAPI 웹 API 프로젝트를 호출 하는 간단한 AngularJS 클라이언트입니다. hello에서 JavaScript 코드를 hello *app/scripts/todoListSvc.js* hello AngularJS HTTP 공급자를 사용 하 여 hello API를 호출 하는 파일입니다. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Hello ToDoListAngular 프로젝트에 대 한 새 웹 앱 만들기
hello 프로시저 toocreate 새 앱 서비스 웹 앱 및 프로젝트 배포 tooit는 언급 했 듯이 대 한 유사한 toowhat [만들고 hello이이 시리즈의 첫 번째 자습서에서 API 앱을 배포](app-service-api-dotnet-get-started.md#createapiapp)합니다. hello 차이점은 해당 hello 앱 형식에만 **웹 앱** 대신 **API 앱**합니다.  Hello 대화의 스크린 샷을 참조 하십시오. 

1. **솔루션 탐색기**hello ToDoListAngular 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.
2. Hello에 **프로필** hello 탭 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.
3. Hello에 **앱 서비스** 대화 상자를 클릭 **새로**합니다.
4. Hello에 **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자에 입력 한 **웹 앱 이름은** hello에 고유 *azurewebsites.net* 도메인입니다. 
5. Azure hello 선택 **구독** toowork와 원하는 합니다.
6. Hello에 **리소스 그룹** 드롭 다운 목록에서 선택 hello 앞에서 만든 동일한 리소스 그룹입니다.
7. Hello에 **앱 서비스 계획** 드롭 다운 목록에서 선택 hello 앞에서 만든 동일한 계획 합니다. 
8. **만들기**를 클릭합니다.
   
    Visual Studio hello 웹 응용 프로그램, 게시 프로필을 만드는 만들고 표시 hello **연결** hello 단계의 **웹 게시** 마법사.
   
    **게시** 를 아직 클릭하지 마십시오. Hello 섹션 뒤, hello 새 웹 응용 프로그램 toocall hello 중간 계층 API 앱을 앱 서비스에서 실행 되 고 구성 합니다. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>웹 앱 설정의 hello 중간 계층 URL 설정
1. Toohello 이동 [Azure 포털](https://portal.azure.com/)를 이동한 후 toohello **웹 응용 프로그램** 블레이드 toohost hello TodoListAngular (프런트 엔드) 프로젝트를 만든 hello 웹 앱에 대 한 합니다.
2. **설정 > 응용 프로그램 설정**을 클릭합니다.
3. Hello에 **앱 설정** 섹션에서 hello 다음 추가 키 / 값:
   
   | 키 | 값 | 예 |
   | --- | --- | --- |
   | toDoListAPIURL |https://{중간 계층 API 앱 이름}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. **Save**를 클릭합니다.
   
    Azure의 hello 코드가 실행 되 면이 값 재정의 hello에 있는 hello localhost URL *Web.config* 파일입니다. 
   
    값을 설정 하는 hello 가져오는 hello 코드는 *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    코드 hello *todoListSvc.js* hello 설정을 사용 하 여:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Hello ToDoListAngular 웹 프로젝트 toohello 새 웹 응용 프로그램 배포
* Hello에 Visual Studio에서 **연결** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **게시**합니다.
  
   Visual Studio는 hello ToDoListAngular 프로젝트 toohello 새 웹 앱을 배포 하 고 브라우저 toohello hello 웹 앱의 URL을 엽니다. 

### <a name="test-hello-application-without-cors-enabled"></a>CORS를 사용 하도록 설정 하지 않고 hello 응용 프로그램을 테스트 합니다.
1. 브라우저 개발자 도구에서에서 hello 콘솔 창을 엽니다.
2. Hello AngularJS UI를 표시 하는 hello 브라우저 창에서 클릭 hello **tooDo 목록** 링크 합니다.
   
    JavaScript 코드 hello toocall hello 중간 계층 API 앱 하지만 hello 프런트 엔드 끝 hello 다시 아닌 다른 도메인에서 실행 중인 hello 호출이 실패 합니다. hello 브라우저의 개발자 도구 콘솔 창에 크로스-원본 오류 메시지를 표시 합니다.
   
    ![교차 원본 오류 메시지](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>CORS hello 중간 계층 API 앱에 대 한 구성
이 섹션에서는 hello 중간 계층 ToDoListAPI API 앱에 대 한 Azure의 hello CORS 설정을 구성할 수 있습니다. 이 설정을 hello 중간 계층 응용 프로그램 tooreceive JavaScript에서에서 API 호출 hello ToDoListAngular 프로젝트에 대해 만든 hello 웹 앱을 통해 있습니다.

1. 브라우저에서 toohello 이동 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **응용 프로그램 서비스**, 다음 hello ToDoListAPI (중간 계층) API 앱을 클릭 합니다.
   
    ![포털에서 API 앱 선택](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Hello에 **설정** hello toohello 오른쪽에 열리는 블레이드 **API 앱** 블레이드, 찾기 hello **API** 섹션을 선택한 다음 클릭 **CORS**합니다.
   
   ![포털에서 CORS 선택](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Hello 텍스트 상자에 hello ToDoListAngular (프런트 엔드) 웹 앱에 대 한 hello URL을 입력 합니다. Todolistangular0121 라는 hello ToDoListAngular 프로젝트 tooa 웹 앱을 배포한 경우 예를 들어 hello URL에서 호출을 허용 `https://todolistangular0121.azurewebsites.net`합니다.
   
   대신 모든 원본 도메인이 허용 되는 별표 (*) toospecify를 입력할 수 있습니다.
5. **Save**를 클릭합니다.
   
   ![저장을 클릭합니다.](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   클릭 한 후 **저장**, hello API 앱에는 JavaScript 수락할 호출 hello에서 URL을 지정 합니다. 이 스크린 샷 hello ToDoListAPI0223 API 앱은 hello ToDoListAngular 웹 앱에서 JavaScript 클라이언트 호출을 수락 합니다.

### <a name="test-hello-application-with-cors-enabled"></a>CORS를 사용 하도록 설정 된 hello 응용 프로그램을 테스트 합니다.
* 브라우저 toohello hello 웹 앱의 HTTPS URL을 엽니다. 
  
    이 시간 hello 응용 프로그램을 사용 하 여 보고, 추가, 편집 및 할 일 항목을 삭제할 수 있습니다. 
  
    ![샘플 응용 프로그램의 tooDo 목록 페이지](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>앱 서비스 CORS와 Web API CORS
웹 API 프로젝트 hello를 설치할 수 있습니다 [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) API 수락할 수 있는 도메인에서 호출 된 JavaScript 코드에서 NuGet 패키지 toospecify 합니다.

Web API CORS 지원은 앱 서비스 CORS 지원보다 유연성이 뛰어납니다. 예를 들어 코드에서 다른 작업 메서드에 대해 다른 허용된 원본을 지정할 수 있는 반면 앱 서비스 CORS의 경우 모든 API 앱의 메서드에 대해 허용된 원본 집합을 지정합니다.

> [!NOTE]
> Toouse 마세요 Web API CORS와 하나의 API 앱에 응용 프로그램 서비스 CORS 합니다. 앱 서비스 CORS가 우선적으로 적용되며 Web API CORS는 아무 효과가 없습니다. 예를 들어, 앱 서비스에서 하나의 원본 도메인을 사용 하도록 설정 하 고 웹 API 코드에서 모든 원본 도메인을 사용 하도록 설정 하는 경우 Azure API 앱 에서만 수락 Azure에서 지정 된 hello 도메인에서 호출 합니다.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>어떻게 tooenable CORS 웹 API 코드에서
단계를 수행 하는 hello Web API CORS 지원을 사용 하도록 설정 하는 것에 대 한 hello 프로세스를 요약 합니다. 자세한 내용은 [ASP.NET Web API 2에서 크로스-원본 리소스 요청 사용](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)을 참조하세요.

1. 웹 API 프로젝트에 설치 hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet 패키지 합니다.
2. 포함 한 `config.EnableCors()` hello 코드 줄 **등록** hello 방식의 **경우 WebApiConfig** hello 다음 예제와 같이 클래스를 합니다. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. 프로그램 Web API 컨트롤러에 추가 `using` hello에 대 한 문을 `System.Web.Http.Cors` 네임 스페이스, hello 추가 `EnableCors` toohello 컨트롤러 클래스 또는 tooindividual 작업 메서드에 특성입니다. 다음 예제는 hello, CORS 지원 toohello 전체 컨트롤러를 적용 합니다.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>API 앱으로 Azure API 관리 사용
API 앱과 Azure API 관리를 사용 하는 경우 hello API 앱에서 CORS 대신 API 관리에서 구성 합니다. 자세한 내용은 다음 리소스는 hello 참조:

* [Azure API 관리 개요(비디오: CORS는 12:10부터 시작)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [도메인 정책 간 API 관리](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>문제 해결
다음은 이 자습서를 수행하는 동안 문제가 발생하는 경우에 사용할 몇 가지 문제 해결 방법입니다.

* 최신 버전의 hello hello를 사용 하는 확인 [Azure SDK for Visual Studio 2015에 대 한.NET](http://go.microsoft.com/fwlink/?linkid=518003)합니다.
* 입력 했는지 확인 `https` 에 CORS 설정을 hello을 만들고 사용 하는 경우 `https` toorun hello에 대 한 프런트 엔드 웹 응용 프로그램입니다.
* Hello 프런트 엔드 웹 응용 프로그램 아니라 hello 중간 계층 API 앱에서 CORS 설정을 hello를 입력 했는지 확인 합니다.
* 응용 프로그램 코드 및 Azure 앱 서비스의 CORS를 구성한 경우 note 응용 프로그램 코드에서 수행할 무엇이 든 hello 응용 프로그램 서비스 CORS 설정을 재정의 합니다. 

문제 해결을 간소화 하는 Visual Studio 기능에 대해 자세히 toolearn 참조 [Visual Studio에서 문제 해결 Azure 앱 서비스 앱](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)합니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 앱 서비스 CORS tooenable 클라이언트 JavaScript 코드 다른 도메인에 있는 API를 호출할 수 있도록 지 원하는 방법을 살펴보았습니다. toolearn hello 읽기 API 앱에 대 한 자세한 [소개 tooauthentication 앱 서비스에서](../app-service/app-service-authentication-overview.md), toohello 넘어갑니다 [API 앱에 대 한 사용자 인증](app-service-api-dotnet-user-principal-auth.md) 자습서입니다.

