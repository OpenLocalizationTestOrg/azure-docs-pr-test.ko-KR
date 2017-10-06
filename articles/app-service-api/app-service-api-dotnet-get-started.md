---
title: "API 앱 및 앱 서비스에서 ASP.NET을 시작 하는 aaaGet | Microsoft Docs"
description: "Toocreate, 배포 하 고 Visual Studio 2015를 사용 하 여 Azure 앱 서비스의 ASP.NET API 앱을 사용 하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a>Azure 앱 서비스에서 API 앱, ASP.NET 및 Swagger 시작
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

이 hello 먼저 일련의 어떻게 toouse 기능 Azure 응용 프로그램의 서비스를 보여 주는 자습서는 개발 및 호스팅 Api는 RESTful 데 유용 합니다.  이 자습서에는 Swagger 형식인 API 메타데이터에 대한 지원을 다룹니다.

다음 내용을 배웁니다.

* 어떻게 toocreate 배포 [API 앱](app-service-api-apps-why-best-platform.md) Visual Studio 2015에 내장 된 도구를 사용 하 여 Azure 앱 서비스의 합니다.
* Hello를 사용 하 여 tooautomate API 검색 Swashbuckle NuGet 패키지로 방법 toodynamically API Swagger 메타 데이터를 생성 합니다.
* 어떻게 toouse API Swagger 메타 데이터 tooautomatically API 앱에 대 한 클라이언트 코드를 생성 합니다.

## <a name="sample-application-overview"></a>샘플 응용 프로그램 개요
이 자습서에서는 간단한 할 일 모음 샘플 응용 프로그램으로 작업합니다. hello 응용 프로그램에 단일 페이지 응용 프로그램 (SPA) 프런트 엔드, ASP.NET Web API 중간 계층 및 ASP.NET Web API 데이터 계층입니다.

![API 앱 샘플 응용 프로그램 다이어그램](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

다음은 hello의 스크린 샷을 [AngularJS](https://angularjs.org/) 프런트 엔드 합니다.

![API 앱 샘플 응용 프로그램 toodo 목록](./media/app-service-api-dotnet-get-started/todospa.png)

Visual Studio 솔루션 hello 세 개의 프로젝트가 포함 되어 있습니다.

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* **ToDoListAngular** -hello 프런트 엔드: hello 중간 계층을 호출 하는 AngularJS SPA 합니다.
* **ToDoListAPI** -hello 중간 계층: hello 데이터 계층에 할 일 항목 tooperform CRUD 작업을 호출 하는 ASP.NET Web API 프로젝트입니다.
* **ToDoListDataAPI** -hello 데이터 계층: 할 일 항목에 대 한 CRUD 작업을 수행 하는 ASP.NET Web API 프로젝트입니다.

hello 3 계층 아키텍처 API 앱을 사용 하 여 구현할 수 있고은 여기서 데모 목적 으로만 사용 하는 많은 아키텍처 중 하나입니다. 각 계층의 hello 코드는 하기만 하면 가능한 toodemonstrate API 앱 기능입니다. 예를 들어 hello 데이터 계층 지 속성 메커니즘으로 데이터베이스 대신 서버 메모리를 사용합니다.

이 자습서를 완료를 두 개의 웹 API 프로젝트 hello 및 hello 클라우드에서 응용 프로그램 서비스 API 앱에서 실행 해야 합니다.

hello 시리즈의 다음 자습서 hello hello SPA 프런트 엔드 toohello 클라우드를 배포합니다.

## <a name="prerequisites"></a>필수 조건
* ASP.NET Web API-hello 자습서 지침은 방법에 대 한 기본적인 지식이 있다고 가정 asp.net toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio에서.
* Azure 계정 - [무료로 Azure 계정을 열거나](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.
  
    Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)합니다. 여기서 **신용 카드와 약정 없이**App Service에서 수명이 짧은 스타터 앱을 즉시 만들 수 있습니다.
* Visual Studio 2015 hello로 [Azure SDK for.NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK에서 Visual Studio 2015 자동으로 설치 아직 없는 경우.
  
  * Visual Studio에서 도움말 -> Microsoft Visual Studio를 클릭하고 "Azure App Service 도구 v2.9.1" 이상을 설치해야 합니다.
    
    ![Azure 앱 도구 버전](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > Hello SDK 종속성의 개수를 이미 있는 컴퓨터에 따라 설치 hello SDK에는 몇 분 tooa 30 분 이상에서 시간이 오래 걸릴 수 있습니다.
    > 
    > 

## <a name="download-hello-sample-application"></a>Hello 샘플 응용 프로그램 다운로드
1. Hello 다운로드 [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) 저장소입니다.
   
    Hello를 클릭할 수 있는 **zip 파일 다운로드** 로컬 컴퓨터의 hello 리포지토리 단추 또는 복제 합니다.
2. Visual Studio 2015 또는 2013에서 hello ToDoList 솔루션을 엽니다.
   
   1. 각 솔루션 tootrust 필요 합니다.
         ![보안 경고](./media/app-service-api-dotnet-get-started/securitywarning.png)
3. Hello 솔루션 (CTRL + SHIFT + B) toorestore hello NuGet 패키지를 빌드하십시오.
   
    배포 하기 전에 작업에서 toosee hello 응용 프로그램을 하려는 경우 로컬로 실행할 수 있습니다. ToDoListDataAPI 시작 프로젝트 및 실행된 hello 솔루션 인지 확인 합니다. 브라우저에서 toosee HTTP 403 오류를 하시면 됩니다.

## <a name="use-swagger-api-metadata-and-ui"></a>Swagger API 메타데이터 및 UI 사용
Azure 앱 서비스에서는 기본적으로 [Swagger](http://swagger.io/) 2.0 API 메타데이터를 지원합니다. 각 API 앱 Swagger JSON 형식의 hello API에 대 한 메타 데이터를 반환 하는 URL 끝점을 지정할 수 있습니다. hello 해당 끝점에서 반환 된 메타 데이터 수 toogenerate 클라이언트 코드를 사용 합니다.

Hello를 사용 하 여 ASP.NET Web API 프로젝트 Swagger 메타 데이터를 동적으로 생성할 수 [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 패키지 합니다. hello Swashbuckle NuGet 패키지는 다운로드 한 hello ToDoListDataAPI 및 ToDoListAPI 프로젝트에 이미 설치 되어 있습니다.

Hello 자습서의이 섹션에서는 생성 된 hello Swagger 2.0 메타 데이터를 보면을 hello Swagger 메타 데이터를 기반으로 하는 UI 테스트 하십시오.

1. Hello ToDoListDataAPI 프로젝트 설정 (**하지** hello ToDoListAPI 프로젝트) hello 시작 프로젝트로 합니다.
   
    ![ToDoDataAPI를 시작 프로젝트로 설정](./media/app-service-api-dotnet-get-started/startupproject.png)
2. F5 키를 누르거나 클릭 **디버그 > 디버깅 시작** toorun hello 프로젝트를 디버그 모드에서.
   
    hello 브라우저가 열리고 hello HTTP 403 오류 페이지를 보여 줍니다.
3. 브라우저 주소 표시줄에서 추가 `swagger/docs/v1` toohello 끝날 hello 선과 다음 리턴 키를 누릅니다. (URL이 hello `http://localhost:45914/swagger/docs/v1`.)
   
    Hello API에 대 한 Swashbuckle tooreturn Swagger 2.0 JSON 메타 데이터에서 사용 하는 hello 기본 URL입니다.
   
    Internet Explorer를 사용 하 여 hello 묻는 toodownload는 *v1.json* 파일입니다.
   
    ![IE에서 JSON 메타데이터 다운로드](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    Chrome, Firefox 또는 가장자리를 사용 하는 hello 브라우저 hello 브라우저 창에서 JSON hello를 표시 합니다. 다른 브라우저 JSON를 다르게 처리 하 고 브라우저 창의 hello 예제 처럼 정확 하 게 나타나지 않을 수 있습니다.
   
    ![Chrome에서 JSON 메타데이터](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    hello에 대 한 hello 정의 된 hello 다음 샘플은 hello API에 대 한 hello Swagger 메타 데이터의 첫 번째 섹션 hello 메서드를 가져옵니다. 이 메타 데이터는 어떤 드라이브 hello Swagger UI 단계에 따라 hello에서 사용 하 고 hello 자습서 tooautomatically의 이후 섹션에서는 클라이언트 코드를 생성 합니다.
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. Hello 브라우저를 닫고 Visual Studio의 디버깅을 중지 합니다.
5. Hello ToDoListDataAPI에서에서 프로젝트를 **솔루션 탐색기**개방형 hello *App_Start\SwaggerConfig.cs* 파일을 다음 스크롤 tooline 174 한 hello 코드 다음 주석 처리를 제거 합니다.
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    hello *SwaggerConfig.cs* 파일이 프로젝트에서 hello Swashbuckle 패키지를 설치할 때 만들어집니다. hello 파일에는 다양 한 방법으로 tooconfigure Swashbuckle 제공합니다.
   
    hello 코드 사용 hello hello 다음에서 사용 하는 Swagger UI 단계를 제거 했습니다. Hello API 응용 프로그램 프로젝트 템플릿을 사용 하 여 웹 API 프로젝트를 만들면이 코드 주석 처리 되어 기본적으로 보안 조치로 합니다.
6. Hello 프로젝트를 다시 실행 합니다.
7. 브라우저 주소 표시줄에서 추가 `swagger` toohello 끝날 hello 선과 다음 리턴 키를 누릅니다. (URL이 hello `http://localhost:45914/swagger`.)
8. Hello Swagger UI 페이지가 나타나면 클릭 **ToDoList** toosee hello 메서드를 사용할 수 있습니다.
   
    ![Swagger UI 사용 가능한 메서드](./media/app-service-api-dotnet-get-started/methods.png)
9. Hello를 처음 클릭 **가져오기** hello 목록에서 단추입니다.
10. Hello에 **매개 변수** 섹션에서 hello의 hello 값으로 별표를 입력 `owner` 매개 변수를 클릭 한 다음 **기능 직접 사용해**합니다.
    
    이후의 자습서에서 인증을 추가 하면 hello 중간 계층 hello 실제 사용자 ID toohello 데이터 계층을 제공 합니다. 지금은 모든 작업은 서로 별표 해당 소유자 ID로 인증을 사용 하지 않고 hello 응용 프로그램을 실행 하는 동안 합니다.
    
    ![Swagger UI 사용해 보기](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    hello Swagger UI hello ToDoList Get 메서드를 호출 하 고 hello 응답 코드 및 JSON 결과 표시 합니다.
    
    ![Swagger UI 사용해 보기 결과](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. 클릭 **Post**, 아래의 hello 상자를 클릭 하 고 **모델 스키마**합니다.
    
    상자를 클릭 하면 hello 모델 스키마 prefills hello 입력 Post 메서드 hello에 대 한 hello 매개 변수 값을 지정할 수 있습니다. (Internet Explorer에서 작동 하지 않는 경우 다른 브라우저를 사용 하거나 hello 다음 단계에서 수동으로 hello 매개 변수 값을 입력 합니다.)  
    
    ![Swagger UI 사용해 보기 게시물](./media/app-service-api-dotnet-get-started/post.png)
12. Hello에 대 한 JSON 변경 hello `todo` 매개 변수 입력 상자를 다음과 같이 다음 예에서는, hello 또는 사용자 고유의 설명 텍스트를 대체 합니다.
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. **Try it out**을 클릭합니다.
    
    hello ToDoList API에서 HTTP 204 응답 코드가 성공을 나타내는 반환 합니다.
14. Hello를 처음 클릭 **가져오기** 단추를 클릭 한 다음 hello 페이지의 해당 섹션에 hello 클릭 **기능 직접 사용해** 단추입니다.
    
    이제 Get 메서드 응답 hello hello 새 toodo 항목을 포함합니다.
15. 선택 사항: Put, Delete, hello를 시도 하십시오. 하 고 ID 메서드에서 가져옵니다.
16. Hello 브라우저를 닫고 Visual Studio의 디버깅을 중지 합니다.

Swashbuckle은 모든 ASP.NET Web API 프로젝트에서 작동합니다. Tooadd Swagger 메타 데이터 생성 tooan 기존 프로젝트를 사용 하도록 하려는 경우 방금 hello Swashbuckle 패키지를 설치 합니다.

> [!NOTE]
> Swagger 메타데이터에는 각 API 작업에 대한 고유 ID가 있습니다. 기본적으로 Swashbuckle은 Web API 컨트롤러 메서드에 대한 중복 Swagger 작업 ID를 생성할 수 있습니다. 컨트롤러에 오버로드된 HTTP 메서드가 있는 경우 이러한 동작이 발생합니다(예: `Get()` 및 `Get(id)`). Toohandle 오버 로드 하는 방법에 대 한 정보를 참조 하십시오. [Swashbuckle 사용자 지정에서 생성 된 API 정의](app-service-api-dotnet-swashbuckle-customize.md)합니다. Visual Studio에서 Web API 프로젝트를 만들면 hello Azure API 앱 템플릿을 사용 하 여 고유한 작업 Id를 생성 하는 코드를 자동으로 추가 toohello *SwaggerConfig.cs* 파일입니다.  
> 
> 

## <a id="createapiapp"></a>Azure에서 API 앱 만들기 및 코드 tooit 배포
Hello Visual Studio에 통합 된 Azure 도구를 사용 하면이 섹션에서는 **웹 게시** Azure에서 새로운 API toocreate 앱 마법사. 그런 다음 hello ToDoListDataAPI 프로젝트 toohello 새 API 앱을 배포 하 고 hello Swagger UI를 실행 하 여 hello API를 호출 합니다.

1. **솔루션 탐색기**hello ToDoListDataAPI 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.
   
    ![Visual Studio에서 게시 클릭](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. Hello에 **프로필** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.
   
   ![웹 게시에서 Azure 앱 서비스 클릭](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. 있습니다 아직 수행 하지 않은, 경우 tooyour Azure 계정에에서 서명 하거나 만료 된 하는 경우 자격 증명을 새로 고칩니다.
4. Hello 앱 서비스 대화 상자에서 Azure hello 선택 **구독** toouse을 차례로 클릭 **새로**합니다.
   
    ![앱 서비스 대화 상자에서 새로 만들기 클릭](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    hello **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자가 나타납니다.
   
    설치 Swashbuckle 지정 된 웹 API 프로젝트를 배포 하기 때문에 Visual Studio API 앱 toocreate 한다고 가정 합니다. 이 hello로 표시 **API 앱 이름** 제목 및 여 hello 팩트는 hello **변경 유형을** 드롭다운 목록이 너무 설정 되어**API 앱**합니다.
   
    ![앱 서비스 대화 상자에서 앱 형식](./media/app-service-api-dotnet-get-started/apptype.png)
5. 입력 한 **API 앱 이름** hello에 고유 *azurewebsites.net* 도메인입니다. Visual Studio에서는 제안 된 hello 기본 이름을 사용할 수 있습니다.
   
    다른 사용자가 이미 사용 하는 이름을 입력 하는 경우 빨간색 느낌표가 toohello 바로 볼 수 있습니다.
   
    hello hello API 앱의 URL을 됩니다 `{API app name}.azurewebsites.net`합니다.
6. Hello에 **리소스 그룹** 드롭 다운 클릭 **새로**를 선택한 다음 원하는 경우 "ToDoListGroup" 또는 다른 이름을 입력 합니다.
   
    리소스 그룹은 API 앱, 데이터베이스, VM 등 Azure 리소스의 컬렉션입니다.    이 자습서를 사용 하면 쉽게 toodelete hello 자습서에 대해 만드는 Azure 리소스를 hello 모두 한 번에 때문 최상의 toocreate 새 리소스 그룹입니다.
   
    이 상자에서 기존 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 선택하거나 구독의 기존 리소스 그룹과 다른 이름을 입력하여 새 리소스 그룹을 만들 수 있습니다.
7. Hello 클릭 **새로** 단추 다음 toohello **앱 서비스 계획** 드롭 다운 합니다.
   
    hello 스크린 샷 샘플 값을 보여 줍니다 **API 앱 이름**, **구독**, 및 **리소스 그룹** -값이 달라 집니다.
   
    ![앱 서비스 만들기 대화 상자](./media/app-service-api-dotnet-get-started/createas.png)
   
    단계를 수행 하는 hello hello 새 리소스 그룹에 대 한 앱 서비스 계획을 만듭니다. 앱 서비스 계획에서 API 앱에서 실행 되는 hello 계산 리소스를 지정 합니다. 예를 들어 hello 무료 계층을 선택 하면 일부 유료 계층에 대 한 전용된 Vm에서 실행 하는 동안 공유 Vm에서 API 앱 실행 됩니다. 앱 서비스 계획에 대한 자세한 내용은 [앱 서비스 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.
8. Hello에 **앱 서비스 계획 구성** 대화 상자에서 원하는 경우 "ToDoListPlan" 또는 다른 이름을 입력 합니다.
9. Hello에 **위치** 드롭 다운 목록에서 가장 가까운 tooyou hello 위치 선택 합니다.
   
    이 설정은 앱이 실행되는 Azure 데이터 센터를 지정합니다. 위치 닫기 tooyou toominimize 선택 [대기 시간](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090)합니다.
10. Hello에 **크기** 드롭 다운 클릭 **무료**합니다.
    
    이 자습서에 대 한 hello 무료 가격 책정 계층에 충분 한 성능을 제공 합니다.
11. Hello에 **앱 서비스 계획 구성** 대화 상자를 클릭 하 여 **확인**합니다.
    
    ![앱 서비스 계획 구성에서 확인 클릭](./media/app-service-api-dotnet-get-started/configasp.png)
12. Hello에 **응용 프로그램 서비스 만들기** 대화 상자를 클릭 **만들기**합니다.
    
    ![앱 서비스 만들기 대화 상자에서 만들기 클릭](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    Visual Studio hello API 앱 및 모든 hello API 앱에 대 한 hello 필요한 설정을 포함 하는 게시 프로필을 만듭니다. Hello를 엽니다 **웹 게시** 마법사를 사용 하 여 toodeploy hello 프로젝트.
    
    hello **웹 게시** hello에 마법사가 열립니다. **연결** 탭 (아래 그림 참조).
    
    Hello에 **연결** 탭 hello **서버** 및 **사이트 이름** 지점 tooyour API 앱을 설정 합니다. hello **사용자 이름** 및 **암호** 배포 하는 자격 증명이 Azure 만들어 드립니다. 배포 후 Visual Studio는 브라우저 toohello 열립니다 **대상 URL** (즉 hello 유일한 목적은 **대상 URL**).  
13. **다음**을 누릅니다.
    
    ![웹 게시의 연결 탭에서 다음 클릭](./media/app-service-api-dotnet-get-started/connnext.png)
    
    다음 탭 hello는 hello **설정을** 탭 (아래 그림 참조). 빌드 구성 탭 toodeploy hello에 대 한 디버그 빌드를 변경할 수 여기 [원격 디버깅](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)합니다. hello 탭에서는 여러 **파일 게시 옵션**:
    
    * 대상에 있는 추가적인 파일을 제거합니다.
    * 게시 중 미리 컴파일합니다.
    * Hello App_Data 폴더에서 파일 제외
    
    이 자습서의 경우 이런 것들이 필요하지 않습니다. 옵션을 통해 수행하는 작업에 대한 자세한 설명은 [Visual Studio의 One-Click 게시를 사용하여 웹 프로젝트 배포 방법](https://msdn.microsoft.com/library/dd465337.aspx)을 참조하세요.
14. **다음**을 누릅니다.
    
    ![웹 게시의 설정 탭에서 다음 클릭](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    그런 다음는 hello **미리 보기** 수 파일 toobe 프로젝트 toohello API 앱에서 복사 하려는 영업 기회 toosee 제공 (아래 그림 참조)을 탭 합니다. Tooearlier에 배포한 프로젝트 tooan API 앱을 배포할 때 변경 된 파일만 복사 됩니다. Toosee 복사 될 작업의 목록을 원하는 경우 클릭할 수 있는 hello **미리 보기 시작** 단추입니다.
15. **게시**를 클릭합니다.
    
    ![웹 게시의 미리 보기 탭에서 게시 클릭](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    Visual Studio hello ToDoListDataAPI 프로젝트 toohello 새 API 앱을 배포합니다. hello **출력** 창 로그 성공적으로 배포 하 고 hello API 앱의 브라우저 창 열고 toohello URL에 "성공적으로 만들어진된" 페이지가 나타납니다.
    
    ![출력 창 성공적인 배포](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![새 API 앱을 성공적으로 만들었습니다 페이지](./media/app-service-api-dotnet-get-started/appcreated.png)
16. Hello 브라우저의 주소 표시줄에 "swagger" toohello URL을 추가 하 고 enter 키를 누릅니다. (URL이 hello `http://{apiappname}.azurewebsites.net/swagger`.)
    
    hello 브라우저 hello 클라우드에서 실행 되는 이전에 본 것과 동일한 Swagger UI 하지만 이제 hello를 표시 합니다. Get 메서드 hello 및 뒤로 toohello 기본 2 할 일 항목 되 고 있는지 확인할 해보세요. hello 로컬 컴퓨터의 메모리에에서에 이전에 만든 hello 변경 내용이 저장 됩니다.
17. 열기 hello [Azure 포털](https://portal.azure.com/)합니다.
    
    hello Azure 포털에는 API 앱 같은 Azure 리소스 관리에 대 한 웹 인터페이스입니다.
18. **더 많은 서비스 > App Services**를 클릭합니다.
    
    ![앱 서비스 찾아보기](./media/app-service-api-dotnet-get-started/browseas.png)
19. Hello에 **응용 프로그램 서비스** 블레이드를 찾아 새 API 앱을 클릭 합니다. (Azure 포털 hello toohello 오른쪽 열리는 창 라고 *블레이드*.)
    
    ![앱 서비스 블레이드](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    두 블레이드가 열립니다. 하나의 블레이드 hello API 앱에 대해 간략하게 않았으며 하나에 긴 보고 변경할 수 있는 설정 목록이 됩니다.
20. Hello에 **설정** 블레이드, 찾기 hello **API** 섹션 및 클릭 **API 정의**합니다.
    
    ![설정 블레이드에서 API 정의](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    hello **API 정의** 블레이드를 사용 하면 JSON 형식의 Swagger 2.0 메타 데이터를 반환 하는 hello URL을 지정 합니다. 기본 Swashbuckle 생성 된 메타 데이터가 이전에 본 hello API 앱에 대 한 hello API 정의 URL toohello 기본값 설정 Visual Studio hello API 앱을 만들 때 URL 더하기 `/swagger/docs/v1`합니다.
    
    ![API 정의 URL](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    에 API 앱 toogenerate 클라이언트 코드를 선택 하면 Visual Studio이이 URL에서 hello 메타 데이터를 검색 합니다.

## <a id="codegen"></a>Hello 데이터 계층에 대 한 클라이언트 코드 생성
Swagger Azure API 앱에 통합 hello 장점 중 하나에 자동 코드 생성입니다. 생성 된 클라이언트 클래스는 API 앱을 호출 하는 보다 쉽게 toowrite 코드를 만듭니다.

hello ToDoListAPI 프로젝트에 이미 생성 된 hello 클라이언트 코드 있지만 hello 단계에서 삭제 및 toosee toodo hello 코드 생성 방법을 다시 생성 합니다.

1. Visual Studio에서 **솔루션 탐색기**hello ToDoListAPI에서에서 프로젝트를 hello 삭제, *ToDoListDataAPI* 폴더입니다. **주의: hello ToDoListDataAPI 프로젝트가 아닌 hello 폴더만 삭제 합니다.**
   
    ![생성된 클라이언트 코드 삭제](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    이 폴더는 hello 코드 생성 프로세스를 통해 toogo에 대 한 참여를 사용 하 여 생성 되었습니다.
2. Hello ToDoListAPI 프로젝트를 마우스 오른쪽 단추로 누른 **추가 > REST API 클라이언트**합니다.
   
    ![Visual Studio에서 REST API 클라이언트 추가](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. Hello에 **REST API 클라이언트 추가** 대화 상자를 클릭 **Swagger URL**, 클릭 하 고 **Azure 자산 선택**합니다.
   
    ![Azure 자산 선택](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. Hello에 **앱 서비스** 대화 상자에서이 자습서에 사용할 hello 리소스 그룹을 확장 하 고 API 앱 선택한 다음 **확인**합니다.
   
    ![코드 생성을 위한 API 앱 선택](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    Toohello이 반환 되 면 다음에 유의 **REST API 클라이언트 추가** 대화 상자에서 hello 텍스트 상자가 채워져 hello API 정의 사용 하 여 hello 포털의 앞부분에 표시 된 URL 값입니다.
   
    ![API 정의 URL](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > 코드 생성에는 다른 방법으로 tooget 메타 데이터에는 찾아보기 대화 상자로 hello 통하지 않고 직접 tooenter hello URL입니다. 또는 tooAzure를 배포 하기 전에 toogenerate 클라이언트 코드를 원하는 경우을 수 있습니다 hello 웹 API 프로젝트를 로컬로 실행, hello 파일을 저장 hello Swagger JSON 파일을 제공 하는 toohello URL 이동 hello를 사용 하 여 **기존Swagger메타데이터파일선택**옵션입니다.
   > 
   > 
5. Hello에 **REST API 클라이언트 추가** 대화 상자를 클릭 **확인**합니다.
   
    Visual Studio hello API 앱의 이름을 딴 폴더를 만들고 클라이언트 클래스를 생성 합니다.
   
    ![생성된 클라이언트에 대한 코드 파일](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. Hello ToDoListAPI 프로젝트를 열고 *Controllers\ToDoListController.cs* hello 생성 된 클라이언트를 사용 하 여 hello API를 호출 하는 40 줄 toosee hello 코드입니다.
   
    호출에 Get 메서드가 hello 및 다음 코드 조각 hello hello 코드 hello 클라이언트 개체를 인스턴스화하고 하는 방법을 보여 줍니다.
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    hello 생성자 매개 변수는 hello에서 hello 끝점 URL을 가져옵니다 `toDoListDataAPIURL` 앱 설정 합니다. Hello Web.config 파일에서 해당 값은 집합 toohello hello 응용 프로그램을 로컬로 실행할 수 있도록 로컬 IIS Express URL의 hello API 프로젝트입니다. Hello 생성자 매개 변수를 생략 하면 hello 기본 끝점은 hello 코드를 생성 하는 hello URL입니다.
7. 클라이언트 클래스를 기반으로 API 앱 이름입니다; 다른 이름으로 생성 됩니다. hello 코드 변경 *Controllers\ToDoListController.cs* hello 형식 이름이 일치 프로젝트에서 생성 된 어떤 수 있도록 합니다. 예를 들어 API 앱을 ToDoListDataAPI071316이라고 명명한 경우 이 코드를
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

toothis:

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a>API 앱 toohost hello 중간 계층 만들기
앞서 있습니다 [hello 데이터 계층 API 앱을 만들고 코드 tooit 배포한](#createapiapp)합니다.  Hello를 수행 하는 이제 hello 중간 계층 API 앱에 대해 동일한 절차입니다.

1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello 중간 계층 ToDoListAPI (하지 hello 데이터 계층 ToDoListDataAPI), 프로젝트 및 클릭 **게시**합니다.
   
    ![Visual Studio에서 게시 클릭](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. Hello에 **프로필** hello 탭 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.
3. Hello에 **앱 서비스** 대화 상자를 클릭 **새로**합니다.
4. Hello에 **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자에서 기본값을 사용한 hello **API 앱 이름** hello에서 고유한 이름을 입력 하거나  *azurewebsites.net* 도메인입니다.
5. Azure hello 선택 **구독** 사용 되 고 있습니다.
6. Hello에 **리소스 그룹** 드롭다운 목록에서 선택 hello 앞에서 만든 동일한 리소스 그룹입니다.
7. Hello에 **앱 서비스 계획** 드롭다운 목록에서 선택 hello 앞에서 만든 동일한 계획 합니다. Toothat 값을 기본값이 지정 됩니다.
8. **만들기**를 클릭합니다.
   
    Visual Studio hello API 앱에 대 한 게시 프로필을 만듭니다 만들고를 hello 표시 **연결** hello 단계의 **웹 게시** 마법사.
9. Hello에 **연결** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **게시**합니다.
   
   Visual Studio는 hello ToDoListAPI 프로젝트 toohello 새 API 앱을 배포 하 고 브라우저 toohello hello API 앱의 URL을 엽니다. "만들었습니다" hello 페이지가 나타납니다.

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a>Hello 중간 계층 toocall hello 데이터 계층 구성
이제 hello 중간 계층 API 앱을 호출 하면 toocall hello 데이터 계층 hello Web.config 파일에 여전히 있는 hello localhost URL을 사용 하 여 시도 합니다. 이 섹션의 hello 중간 계층 API 앱에는 환경 설정에 hello 데이터 계층 API 앱 URL을 입력합니다. Hello hello 중간 계층 API 앱의 코드를 검색 하는 hello 데이터 계층 URL 설정, hello Web.config 파일에 무엇이 hello 환경 설정을 재정의 합니다.

1. Toohello 이동 [Azure 포털](https://portal.azure.com/)를 이동한 후 toohello **API 앱** 블레이드 toohost hello TodoListAPI (중간 계층) 프로젝트를 만든 hello API 앱에 대 한 합니다.
2. API 앱 hello **설정** 블레이드에서 클릭 **응용 프로그램 설정**합니다.
3. API 앱 hello **응용 프로그램 설정** 블레이드에서 toohello 아래로 스크롤하여 **앱 설정** 섹션 및 hello 다음 추가 키와 값입니다. hello 값 hello 첫 번째 API이이 자습서에는 게시 된 앱의 URL을 hello 됩니다.
   
   | **키** | toDoListDataAPIURL |
   | --- | --- |
   | **값** |https://{데이터 계층 API 앱 이름}.azurewebsites.net |
   | **예제** |https://todolistdataapi.azurewebsites.net |
4. **Save**를 클릭합니다.
   
    ![앱 설정에서 저장 클릭](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    Azure의 hello 코드가 실행 되 면이 값은 이제 hello Web.config 파일에 있는 hello localhost URL을 덮어씁니다.

## <a name="test"></a>테스트
1. 브라우저 창에서 hello 새 중간 계층 위에서 만든 ToDoListAPI에 대 한 API 앱의 toohello URL를 찾습니다. Hello 포털에서 API hello 응용 프로그램의 주 블레이드에서 hello URL을 클릭 하 여 있습니다 얻을 수 있습니다.
2. Hello 브라우저의 주소 표시줄에 "swagger" toohello URL을 추가 하 고 enter 키를 누릅니다. (URL이 hello `http://{apiappname}.azurewebsites.net/swagger`.)
   
    hello 브라우저 표시 hello 했 듯이 ToDoListDataAPI에 대 한 하지만 이제는 동일한 Swagger UI `owner` hello 중간 계층 API 앱 사용자에 대 한 해당 값 toohello 데이터 계층 API 응용 프로그램에서 보내고 있으므로 hello 가져오기 작업에 대 한 필수 필드가 아닙니다. (Hello 중간 계층 hello에 대 한 실제 사용자 Id를 송신할 때 인증 자습서 hello 수행, `owner` 매개 변수; 이제 것은 하드 코딩 별표.)
3. Get 메서드 hello 및 hello 중간 계층 API 앱 hello 다른 메서드 toovalidate 성공적으로 호출 하는 hello 데이터 계층 응용 프로그램 API 사용해 봅니다.
   
    ![Swagger UI 가져오기 메서드](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a>문제 해결
다음은 이 자습서를 수행하는 동안 문제가 발생하는 경우에 사용할 몇 가지 문제 해결 방법입니다.

* 최신 버전의 hello hello를 사용 하는 확인 [Azure SDK for.NET](http://go.microsoft.com/fwlink/?linkid=518003)합니다.
* Hello 프로젝트 이름은 두 가지 비슷한 (ToDoListAPI, ToDoListDataAPI)입니다. 작업은 프로젝트와 작업 하는 hello 지침에 설명 된 대로 표시 되지 않는, hello 올바른 프로젝트를 열면 해야 합니다.
* 방화벽을 통해 toodeploy tooAzure 앱 서비스 시도 회사 네트워크에는 경우에 포트 443 및 8172 웹 배포에 대 한 열려 있는지 확인 합니다. 이러한 포트를 열 수 없으면 다른 배포 방법을 사용할 수 있습니다.  참조 [프로그램 응용 프로그램 tooAzure 앱 서비스 배포](../app-service-web/web-sites-deploy.md)합니다.
* "경로 이름은 고유 해야" 오류 발생-얻을 수 있습니다 이러한 실수로 hello 잘못 된 프로젝트 tooan API 앱을 배포 하 고 올바른 하나의 tooit hello를 나중에 배포 하는 경우. toocorrect이를 재배포 hello 올바른 프로젝트 toohello API 앱 및 hello **설정** hello 탭 **웹 게시** 마법사 선택 **대상에서추가파일제거**.

Azure 앱 서비스에서 실행 되는 ASP.NET API 앱을 사용 하는 다음 문제 해결을 간소화 하는 Visual Studio 기능에 대 한 자세한 toolearn을 할 수 있습니다. 로깅, 원격 디버깅 등에 대한 정보는 [Visual Studio에서 Azure App Service 앱 문제 해결](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Toodeploy 기존 웹 API 프로젝트 tooAPI 응용 프로그램, API 앱에 대 한 클라이언트 코드를 생성 하 고.NET 클라이언트에서 API 앱을 사용 방법을 살펴보았습니다. 이 시리즈의 다음 자습서 hello 너무 방법을 보여 줍니다[JavaScript 클라이언트에서 CORS tooconsume API 앱을 사용 하 여](app-service-api-cors-consume-javascript.md)합니다.

클라이언트 코드 생성에 대 한 자세한 내용은 참조 hello [Azure/AutoRest](https://github.com/azure/autorest) GitHub.com에 리포지토리 합니다. 에 대 한 도움말 hello 생성 된 클라이언트를 사용 하 여 문제를 열고는 [hello AutoRest 리포지토리에 문제](https://github.com/azure/autorest/issues)합니다.

Hello를 사용 하 여 처음부터 toocreate 새 API 앱 프로젝트를 원하는 경우 **Azure API 앱** 템플릿.

![Visual Studio에서 API 앱 템플릿](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

hello **Azure API 앱** 프로젝트 템플릿에 해당 toochoosing hello **빈** ASP.NET 4.5.2 템플릿을 hello 확인란 tooadd 웹 API 지원를 클릭 하 고 hello Swashbuckle NuGet 패키지를 설치 합니다. 또한 hello 템플릿은 중복 Swagger 작업 Id의 몇 가지 Swashbuckle 구성 코드 설계 tooprevent hello 만들기를 추가합니다. API 앱 프로젝트를 만든 후 배포할 수 있습니다 tooan API 앱 hello 동일한 방식으로이 자습서에서 본 것입니다.

