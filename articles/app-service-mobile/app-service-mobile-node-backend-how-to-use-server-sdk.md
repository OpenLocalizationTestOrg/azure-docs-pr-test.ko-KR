---
title: "Mobile Apps용 Node.js 백 엔드 서버 SDK를 사용하는 방법 | Microsoft Docs"
description: "Azure App Service Mobile Apps용 Node.js 백 엔드 서버 SDK를 사용하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: elamalani
manager: elamalani
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: crdun
ms.openlocfilehash: 336da28bea7de313bced97e447fc6b7b1fb1390d
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2018
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a>Azure Mobile Apps Node.js SDK를 사용하는 방법
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

이 문서에서는 Azure App Service Mobile Apps에서 Node.js 백 엔드로 작업하는 방법을 보여주는 자세한 정보와 예를 제공합니다.

## <a name="Introduction"></a>소개
Azure App Service Mobile Apps는 모바일에 최적화된 데이터 액세스 Web API를 웹 응용 프로그램에 추가하는 기능을 제공합니다.  Azure App Service Mobile Apps SDK는 ASP.NET 및 Node.js 웹 응용 프로그램에 대해 제공됩니다.  SDK는 다음 작업을 제공합니다.

* 데이터 액세스를 위한 테이블 작업(읽기, 삽입, 업데이트, 삭제)
* API 작업 사용자 지정

두 작업은 모두 Facebook, Twitter, Google Microsoft 등과 같은 소셜 ID 공급자 뿐만 아니라 엔터프라이즈 ID에 대한 Azure Active Directory를 포함하는 Azure App Service에서 허용된 모든 ID 공급자에 걸쳐 인증을 제공합니다.

[GitHub의 샘플 디렉터리]에서 각 사용 사례에 대한 샘플을 찾을 수 있습니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
Azure Mobile Apps 노드 SDK는 노드의 최신 LTS 릴리스 이상을 지원합니다.  이 문서를 작성할 당시 최신 LTS 버전은 노드 v4.5.0입니다.  다른 버전의 노드는 작동할 수는 있지만 지원되지 않습니다.

Azure Mobile Apps 노드 SDK는 두 가지 데이터베이스 드라이버를 지원합니다. node-mssql 드라이버는 SQL Azure 및 로컬 SQL Server 인스턴스를 지원합니다.  sqlite3 드라이버는 단일 인스턴스에서만 SQLite 데이터베이스를 지원합니다.

### <a name="howto-cmdline-basicapp"></a>방법: 명령줄을 사용하는 기본 Node.js 백 엔드 만들기
모든 Azure App Service 모바일 앱 Node.js 백 엔드는 ExpressJS 응용 프로그램으로 시작합니다.  ExpressJS는 Node.js에 사용할 수 있는 가장 인기 있는 웹 서비스 프레임워크입니다.  다음과 같이 기본 [Express] 응용 프로그램을 만들 수 있습니다.

1. 명령 창 또는 PowerShell 창에서 프로젝트의 디렉터리를 만듭니다.

        mkdir basicapp
2. npm init를 실행하여 패키지 구조를 초기화합니다.

        cd basicapp
        npm init

    npm init 명령은 프로젝트를 초기화하기 위해 몇 가지 질문을 합니다.  예제 출력을 참조하세요.

    ![Npm init 출력][0]
3. npm 리포지토리에서 Express 및 azure-mobile-apps 라이브러리를 설치합니다.

        npm install --save express azure-mobile-apps
4. app.js 파일을 만들어서 기본 모바일 서버를 구현합니다.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

이 응용 프로그램은 동적 스키마를 사용하여 기본 SQL 데이터 저장소에 대한 인증되지 않은 액세스를 제공하는 단일 끝점(`/tables/TodoItem`)으로 모바일에 최적화된 WebAPI를 만듭니다.  다음의 클라이언트 라이브러리 빠른 시작에 적합합니다.

* [Android 클라이언트 빠른 시작]
* [Apache Cordova 클라이언트 빠른 시작]
* [iOS 클라이언트 빠른 시작]
* [Windows 스토어 클라이언트 빠른 시작]
* [Xamarin.iOS 클라이언트 빠른 시작]
* [Xamarin.Android 클라이언트 빠른 시작]
* [Xamarin.Forms 클라이언트 빠른 시작]

[GitHub의 기본 앱 샘플]에서 이 기본 응용 프로그램에 대한 코드를 찾을 수 있습니다.

### <a name="howto-vs2015-basicapp"></a>방법: Visual Studio 2015를 사용하여 노드 백 엔드 만들기
Visual Studio 2015는 IDE 내에서 Node.js 응용 프로그램 개발하도록 확장이 필요합니다.  시작하려면 [Visual Studio용 Node.js Tools 1.1]을 설치합니다.  Visual Studio용 Node.js Tools가 설치되면 Express 4.x 응용 프로그램을 만듭니다.

1. **새 프로젝트** 대화를 엽니다(**파일** > **새로 만들기** > **프로젝트...**에서).
2. **템플릿** > **JavaScript** > **Node.js**으로 확장합니다.
3. **기본 Azure Node.js Express 4 응용 프로그램**을 선택합니다.
4. 프로젝트 이름을 입력합니다.  *확인*을 클릭합니다.

    ![Visual Studio 2015 새 프로젝트][1]
5. 마우스 오른쪽 단추로 **npm** 노드를 클릭하고 **새 npm 패키지 설치...**를 선택합니다.
6. 첫 번째 Node.js 응용 프로그램을 만드는 데 npm 카탈로그를 새로 고쳐야 할 수 있습니다.  필요한 경우 **새로 고침** 을 클릭합니다.
7. 검색 상자에 *azure-mobile-apps* 를 입력합니다.  **azure-mobile-apps 2.0.0** 패키지를 클릭한 다음 **패키지 설치**를 클릭합니다.

    ![새 npm 패키지 설치][2]
8. **닫기**를 클릭합니다.
9. *app.js* 파일을 열고 Azure Mobile Apps SDK에 대한 지원을 추가합니다.  라이브러리의 맨 아래 6 줄에 필요한 명령문, 다음 코드를 추가 합니다.

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    다른 app.use 문 뒤 약 27줄에 다음 코드를 추가 합니다.

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    파일을 저장합니다.
10. 응용 프로그램을 로컬로 실행하거나(API가 http://localhost:3000 에서 제공됨) Azure에 게시합니다.

### <a name="create-node-backend-portal"></a>방법: Azure 포털을 사용하여 Node.js 백 엔드 만들기
[Azure 포털]에서 바로 모바일 앱 백 엔드를 만들 수 있습니다. 다음 단계를 수행하거나 [모바일 앱 만들기](app-service-mobile-ios-get-started.md) 자습서에 따라 클라이언트 및 서버를 함께 만들 수 있습니다. 자습서는 이러한 지침의 단순화된 버전을 포함하고 있으며 개념 증명 프로젝트에 가장 적합합니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

*시작* 블레이드로 돌아가서 **테이블 API 만들기** 아래에서 **백 엔드 언어**로 **Node.js**를 선택합니다.
“**이렇게 하면 모든 사이트 콘텐츠를 덮어쓴다는 것을 인정합니다.**”라는 상자를 선택하고 **TodoItem 테이블 만들기**를 클릭합니다.

### <a name="download-quickstart"></a>방법: Git를 사용하여 Node.js 백 엔드 빠른 시작 코드 프로젝트 다운로드
포털 **빠른 시작** 블레이드를 사용하여 Node.js 모바일 앱 백 엔드를 만들 때 Node.js 프로젝트가 생성되어 사이트에 배포됩니다. 테이블 및 API를 추가하고 포털에서 Node.js 백 엔드에 대한 코드 파일을 편집할 수 있습니다. 또한 다양한 배포 도구를 사용하여 백 엔드 프로젝트를 다운로드할 수 있으므로 테이블 및 API를 추가하거나 수정한 다음 프로젝트를 다시 게시할 수 있습니다. 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요. 다음 절차에서는 Git 리포지토리를 사용하여 빠른 시작 프로젝트 코드를 다운로드합니다.

1. 아직 수행하지 않았다면 Git을 설치합니다. Git를 설치하는 데 필요한 단계는 운영 체제마다 다릅니다. 운영 체제별 배포 및 설치 지침은 [Git 설치](http://git-scm.com/book/en/Getting-Started-Installing-Git) 를 참조하세요.
2. 배포 사용자 이름 및 암호를 기록하여 백 엔드 사이트에 대한 Git 리포지토리를 사용하는 [App Service 앱 리포지토리 사용](../app-service/app-service-deploy-local-git.md#Step3)의 단계를 수행합니다.
3. 모바일 앱 백 엔드에 대한 블레이드에서 **Git 복제 URL** 설정을 적어 둡니다.
4. 다음 예제와 같이 Git 복제 URL을 사용하여 `git clone` 명령을 실행하고, 필요한 경우 암호를 입력합니다.

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. 로컬 디렉터리를 찾습니다. 앞의 예제에서는 /todolist였습니다. 그리고 프로젝트 파일이 다운로드되었는지 확인합니다. `/tables` 디렉터리에서 `todoitem.json` 파일을 찾습니다.  이 파일은 테이블의 사용 권한을 정의합니다.  그리고 같은 디렉터리에서 `todoitem.js` 파일도 찾습니다. 이 파일은 테이블에 대한 CRUD 작업 스크립트를 정의합니다.
6. 프로젝트 파일을 변경한 후에 다음 사이트에 변경 내용을 추가, 커밋, 업로드하려면 다음 명령을 실행합니다.

        $ git commit -m "updated the table script"
        $ git push origin master

    프로젝트에 새 파일을 추가할 때 먼저 `git add .` 명령을 실행해야 합니다.

사이트는 사이트에 새로운 커밋 집합이 푸시될 때마다 다시 게시됩니다.

### <a name="howto-publish-to-azure"></a>방법: Azure에 Node.js 백 엔드 게시
Microsoft Azure는 Azure App Service Mobile Apps Node.js 백 엔드를 Azure 서비스에 게시하기 위한 여러 메커니즘을 제공합니다.  여기에는 원본 제어에 따라 Visual Studio, 명령줄 도구 및 연속 배포 옵션에 통합된 배포 도구의 활용을 포함합니다.  이 항목에 대한 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.

Azure App Service에는 배포하기 전에 검토해야 하는 Node.js 응용 프로그램에 대한 구체적인 조언이 있습니다.

* [노드 버전 지정]
* [노드 모듈 사용]

### <a name="howto-enable-homepage"></a>방법: 응용 프로그램에 대한 홈페이지 사용
대부분의 응용 프로그램은 웹앱 및 모바일 앱의 조합이고 ExpressJS 프레임워크를 사용하면 두 가지 측면을 결합할 수 있습니다.  그러나 때로는 모바일 인터페이스를 구현하려고 할 수 있습니다.  앱 서비스를 실행하도록 하기 위해 방문 페이지를 제공하는 것이 유용합니다.  고유한 홈 페이지에 제공하거나 임시 홈 페이지를 사용할 수 있습니다.  임시 홈 페이지를 사용하려면 다음을 사용하여 Azure Mobile Apps를 인스턴스화합니다.

    var mobile = azureMobileApps({ homePage: true });

로컬로 개발할 때에만 이 옵션을 사용하려면 이 설정을 `azureMobile.js` 파일에 추가합니다.

## <a name="TableOperations"></a>테이블 작업
azure-mobile-apps Node.js 서버 SDK는 Azure SQL Database에 저장된 데이터 테이블을 WebAPI로 노출하는 메커니즘을 제공합니다.  다섯 가지 작업이 제공됩니다.

| 작업 | 설명 |
| --- | --- |
| GET /tables/*tablename* |테이블의 레코드 모두 가져오기 |
| GET /tables/*tablename*/:id |테이블의 특정 레코드 가져오기 |
| POST /tables/*tablename* |테이블에 레코드 만들기 |
| PATCH /tables/*tablename*/:id |테이블의 레코드 업데이트 |
| DELETE /tables/*tablename*/:id |테이블의 레코드 삭제 |

이 WebAPI는 [OData]를 지원하고 테이블 스키마를 확장하여 [오프라인 데이터 동기화]를 지원합니다.

### <a name="howto-dynamicschema"></a>방법: 동적 스키마를 사용하여 테이블 정의
테이블을 사용하기 전에 정의되어야 합니다.  테이블은 정적 스키마(개발자가 스키마 내에서 열을 정의하는 위치) 또는 동적으로(SDK가 들어오는 요청에 따라 스키마를 제어하는 위치) 정의될 수 있습니다. 또한 개발자는 정의에 Javascript 코드를 추가하여 WebAPI의 특정 측면을 제어할 수 있습니다.

모범 사례로 테이블 디렉터리의 Javascript 파일에 각 테이블을 정의한 다음 테이블을 가져오는 tables.import() 메서드를 사용해야 합니다.  basic-app을 확장하면 app.js 파일은 조정됩니다.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

./tables/TodoItem.js에서 테이블을 정의합니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

테이블은 기본적으로 동적 스키마를 사용합니다.  동적 스키마를 전역적으로 해제하려면 앱 설정 **MS_DynamicSchema**를 Azure 포털 내에서 false로 설정합니다.

[GitHub의 할 일 샘플]에서 전체 예제를 찾을 수 있습니다.

### <a name="howto-staticschema"></a>방법: 정적 스키마를 사용하여 테이블 정의
열을 명시적으로 정의하여 WebAPI를 통해 노출할 수 있습니다.  azure-mobile-apps Node.js SDK는 오프라인 데이터 동기화에 필요한 모든 열을 사용자가 제공하는 목록에 자동으로 추가합니다.  예를 들어 빠른 시작 클라이언트 응용 프로그램은 텍스트(문자열) 및 완료(부울)이라는 두 열이 있는 테이블이 필요합니다.  
이 테이블은 다음과 같이 테이블 정의 JavaScript 파일(테이블 디렉터리에 위치)에서 정의할 수 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

또한 정적으로 테이블을 정의하는 경우 tables.initialize() 메서드를 호출하여 시작 시 데이터베이스 스키마를 만들어야 합니다.  데이터베이스가 초기화되기 전에 웹 서비스가 요청을 처리하지 않도록 하기 위해 tables.initialize() 메서드는 [Promise] 를 반환합니다.

### <a name="howto-sqlexpress-setup"></a>방법: 로컬 컴퓨터에서 개발 데이터 저장소로 SQL Express 사용
Azure Mobile Apps 노드 SDK는 상자에서 데이터를 처리 하기 위한 세 가지 옵션을 제공합니다. SDK는 상자에서 데이터를 처리 하기 위한 세 가지 옵션을 제공합니다.

* **메모리** 드라이버를 사용하여 비 영구적 예제 저장소를 제공합니다
* **mssql** 드라이버를 사용하여 개발을 위한 SQL Express 데이터 저장소를 제공합니다.
* **mssql** 드라이버를 사용하여 프로덕션을 위한 Azure SQL Database 데이터 저장소를 제공합니다.

Azure Mobile Apps Node.js SDK는 [mssql Node.js 패키지]를 사용하여 SQL Express 및 SQL Database에 대한 연결을 설정하고 사용합니다.  이 패키지는 SQL Express 인스턴스에서 TCP 연결을 사용해야 합니다.

> [!TIP]
> 메모리 드라이버는 테스트하기 위한 완전한 기능 집합을 제공하지 않습니다.  백 엔드 로컬로 테스트하려는 경우 SQL Express 데이터 저장소 및 mssql 드라이버를 사용하는 것이 좋습니다.
>
>

1. [Microsoft SQL Server 2014 Express]를 다운로드하고 설치합니다.  Tools Edition을 사용하여 SQL Server 2014 Express를 설치하도록 합니다.  64비트를 지원하도록 명시적으로 요구하지 않는 한 32비트 버전이 실행할 때 메모리를 적게 사용합니다.
2. SQL Server 2014 구성 관리자를 실행합니다.

   1. 왼쪽 트리 메뉴에서 **SQL Server 네트워크 구성** 노드를 확장합니다.
   2. **SQLEXPRESS에 대한 프로토콜**을 클릭합니다.
   3. 마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **사용**을 선택합니다.  팝업 대화 상자에서 **확인** 을 클릭합니다.
   4. 마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **속성**을 선택합니다.
   5. **IP 주소** 탭을 클릭합니다.
   6. **IPAll** 노드를 찾습니다.  **TCP 포트** 필드에 **1433**을 입력합니다.

          ![Configure SQL Express for TCP/IP][3]
   7. **확인**을 클릭합니다.  팝업 대화 상자에서 **확인** 을 클릭합니다.
   8. 왼쪽 트리 메뉴에서 **SQL Server 서비스** 를 클릭합니다.
   9. 마우스 오른쪽 단추로 **SQL Server (SQLEXPRESS)**를 클릭하고 **다시 시작**을 선택합니다.
   10. SQL Server 2014 구성 관리자를 닫습니다.
3. SQL Server 2014 Management Studio를 실행하고 로컬 SQL Express 인스턴스에 연결합니다.

   1. 개체 탐색기에서 마우스 오른쪽 단추로 인스턴스를 클릭하고 **속성**
   2. **보안** 페이지를 선택합니다.
   3. **SQL Server 및 Windows 인증 모드** 를 선택하도록 합니다.
   4. **확인**

          ![Configure SQL Express Authentication][4]
   5. **보안** > **로그인** 을 확장합니다.
   6. 마우스 오른쪽 단추로 **로그인**을 클릭하고 **새 로그인...**을 선택합니다.
   7. 로그인 이름을 입력합니다.  **SQL Server 인증**을 선택합니다.  암호를 입력한 다음 동일한 암호를 **암호 확인**에 입력합니다.  암호는 Windows 복잡성 요구 사항을 충족해야 합니다.
   8. **확인**

          ![Add a new user to SQL Express][5]
   9. 새 로그인을 마우스 오른쪽 단추로 클릭하고 **속성**
   10. **서버 역할** 페이지를 선택합니다.
   11. **dbcreator** 서버 역할 옆에 확인란을 선택합니다.
   12. **확인**
   13. SQL Server 2015 Management Studio를 닫습니다.

사용자 이름 및 선택한 암호를 기록하도록 합니다.  특정 데이터베이스 요구 사항에 따라 추가 서버 역할 또는 사용 권한을 할당해야 합니다.

Node.js 응용 프로그램은 이 데이터베이스의 연결 문자열을 읽기 위해 **SQLCONNSTR_MS_TableConnectionString** 환경 변수를 읽습니다.  환경 내에서 이 변수를 설정할 수 있습니다.  예를 들어 이 환경 변수를 설정하려면 PowerShell을 사용할 수 있습니다.

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

TCP/IP 연결을 통해 데이터베이스에 액세스하고 연결에 필요한 사용자 이름 및 암호를 입력합니다.

### <a name="howto-config-localdev"></a>방법: 로컬 개발에 대한 프로젝트 구성
Azure Mobile Apps는 로컬 파일 시스템에서 *azureMobile.js*라는 JavaScript 파일을 읽습니다.  이 파일을 사용하여 프로덕션에서 Azure Mobile Apps SDK를 구성하지 마세요. 대신 [Azure 포털] 내에서 앱 설정을 사용하세요.  *azureMobile.js* 파일은 구성 개체를 내보내야 합니다.  가장 일반적인 설정은 다음과 같습니다.

* 데이터베이스 설정
* 진단 로깅 설정
* 대체 CORS 설정

앞에 나온 데이터베이스 설정을 구현하는 *azureMobile.js* 예제 파일은 다음과 같습니다.

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

*.gitignore* 파일에 *azureMobile.js*를 추가하여(또는 기타 소스 코드 제어 무시 파일) 암호가 클라우드에 저장되지 않도록 합니다.  [Azure 포털]내의 앱 설정에서 프로덕션 설정을 항상 구성합니다.

### <a name="howto-appsettings"></a>방법: 모바일 앱에 대한 앱 설정 구성
*azureMobile.js* 파일에서 대부분의 설정은 [Azure 포털]에서 동일한 앱 설정을 포함합니다.  다음 목록을 사용하여 앱 설정에서 앱을 구성합니다.

| 앱 설정 | *azureMobile.js* 설정 | 설명 | 유효한 값 |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |이름 |앱의 이름 |문자열 |
| **MS_MobileLoggingLevel** |logging.level |로깅할 메시지의 최소 로그 수준 |error, warning, info, verbose, debug, silly |
| **MS_DebugMode** |debug |디버그 모드를 사용 또는 사용하지 않도록 설정 |true, false |
| **MS_TableSchema** |data.schema |SQL 테이블에 대한 기본 스키마 이름 |string(기본값: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |디버그 모드를 사용 또는 사용하지 않도록 설정 |true, false |
| **MS_DisableVersionHeader** |version(undefined로 설정) |X-ZUMO-Server-Version 헤더를 사용하지 않도록 설정 |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |클라이언트 API 버전 검사를 사용하지 않도록 설정 |true, false |

앱 설정을 지정하려면:

1. [Azure 포털] 에 로그인합니다.
2. **모든 리소스** 또는 **App Services**를 선택한 후 모바일 앱의 이름을 클릭합니다.
3. 설정 블레이드가 기본적으로 열립니다. 열리지 않으면 **설정**을 클릭합니다.
4. 일반 메뉴에서 **응용 프로그램 설정** 을 클릭합니다.
5. 앱 설정 섹션으로 스크롤합니다.
6. 앱 설정이 이미 있는 경우 앱 설정 값을 클릭하여 값을 편집합니다.
7. 앱 설정이 존재하지 않는 경우 키 상자에 앱 설정을 입력하고 값 상자에 값을 입력합니다.
8. 완료했으면 **저장**을 클릭합니다.

대부분의 앱은 설정 변경 후 서비스를 다시 시작해야 합니다.

### <a name="howto-use-sqlazure"></a>방법: 프로덕션 데이터 저장소로 SQL Database 사용
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Azure SQL Database를 데이터 저장소로 사용하면 모든 Azure App Service 응용 프로그램 형식에 걸쳐 동일합니다. 아직 수행하지 않은 경우 다음 단계에 따라 모바일 앱 백 엔드를 만드세요.

1. [Azure 포털] 에 로그인합니다.
2. 창의 왼쪽 위에서 **+새로 만들기** 단추 > **웹 + 모바일** > **모바일 앱**을 클릭한 다음 모바일 앱 백 엔드에 대한 이름을 입력합니다.
3. **리소스 그룹** 상자에 앱과 동일한 이름을 입력합니다.
4. 기본 App Service 계획이 선택됩니다.  App Service 계획을 변경하려는 경우 App Service 계획 > **+ 새로 만들기**를 클릭하여 변경합니다.  새 App Service 계획의 이름을 입력하고 적절한 위치를 선택합니다.  가격 책정 계층을 클릭하고 서비스에 대한 적절한 가격 책정 계층을 선택합니다. **무료** 및 **공유** 등의 더 많은 가격 책정 옵션을 보려면 **모두 보기**를 선택합니다.  가격 책정 계층을 선택한 다음 **선택** 단추를 클릭합니다.  **App Service 계획** 블레이드로 돌아가서 **확인**을 클릭합니다.
5. **만들기**를 클릭합니다. 모바일 앱 백 엔드를 프로비저닝하는 데 몇 분 정도 걸릴 수 있습니다.  모바일 앱 백 엔드가 프로비전되면 포털에서 모바일 앱 백 엔드에 대한 **설정** 블레이드가 열립니다.

모바일 앱 백 엔드를 만들면 모바일 앱 백 엔드에 기존 SQL 데이터베이스를 연결하거나 새 SQL 데이터베이스를 만들도록 선택할 수 있습니다.  이 섹션에서 SQL 데이터베이스를 만듭니다.

> [!NOTE]
> 모바일 앱 백 엔드와 동일한 위치에 데이터베이스가 이미 있다면 대신 **기존 데이터베이스 사용** 을 선택한 다음 해당 데이터베이스를 선택할 수 있습니다. 다른 위치에 있는 데이터베이스는 대기 시간이 높기 때문에 권장하지 않습니다.
>
>

1. 새 모바일 앱 백 엔드에서 **설정** > **모바일 앱** > **데이터** > **+추가**를 클릭합니다.
2. **데이터 연결 추가** 블레이드에서 **SQL Database - 필요한 설정 구성** > **새 데이터베이스를 만들기**를 클릭합니다.  **이름** 필드에 새 데이터베이스 이름을 입력합니다.
3. **서버**를 클릭합니다.  **새 서버** 블레이드에서 **서버 이름** 필드에 고유한 서버 이름을 입력하고 적절한 **서버 관리자 로그인** 및 **암호**를 입력합니다.  **Azure 서비스가 서버에 액세스하도록 허용** 이 선택되었는지 확인합니다.  **확인**을 클릭합니다.

    ![Azure SQL Database 만들기][6]
4. **새 데이터베이스** 블레이드에서 **확인**을 클릭합니다.
5. **데이터 연결 추가** 블레이드로 돌아가서 **연결 문자열**을 선택하고 데이터베이스를 만들 때 입력한 로그인 및 암호를 입력합니다.  기존 데이터베이스를 사용하는 경우 해당 데이터베이스에 대한 로그인 자격 증명을 입력합니다.  입력한 다음 **확인**을 클릭합니다.
6. **데이터 연결 추가** 블레이드로 다시 돌아가서 **확인**을 클릭하여 데이터베이스를 만듭니다.

<!--- END OF ALTERNATE INCLUDE -->

데이터베이스를 만드는 데 몇 분 정도 걸릴 수 있습니다.  **알림** 영역을 사용하여 배포의 진행률을 모니터링합니다.  데이터베이스가 성공적으로 배포될 때까지 진행하지 마세요.  성공적으로 배포되면 모바일 백 엔드 앱 설정에서 SQL Database 인스턴스에 대한 연결 문자열이 생성됩니다.  **설정** > **응용 프로그램 설정** > **연결 문자열**에서 각 사용 사례에 대한 샘플을 찾을 수 있습니다.

### <a name="howto-tables-auth"></a>방법: 테이블에 대한 액세스 인증 요구
테이블 끝점을 사용하여 App Service 인증을 사용하려는 경우 [Azure 포털] 에서 우선 App Service 인증을 구성해야 합니다.  Azure App Service에서 인증을 구성하는 데 대한 자세한 내용은 사용하려는 ID 공급자를 위한 구성 가이드를 검토합니다.

* [Azure Active Directory 인증을 구성하는 방법]
* [Facebook 인증을 구성하는 방법]
* [Google 인증을 구성하는 방법]
* [Microsoft 인증을 구성하는 방법]
* [Twitter 인증을 구성하는 방법]

각 테이블에는 테이블에 대한 액세스를 제어하는 데 사용할 수 있는 액세스 속성이 있습니다.  다음 샘플에서는 필요한 인증을 사용하여 정적으로 정의된 테이블을 보여줍니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

액세스 속성은 세 가지 값 중 하나를 사용할 수 있습니다

* *익명* 은 클라이언트 응용 프로그램이 인증 없이 데이터를 읽을 수 있다는 것을 나타냅니다.
* *인증됨* 은 클라이언트 응용 프로그램이 요청을 사용하여 유효한 인증 토큰을 송신해야 함을 나타냅니다.
* *사용 안 함* 은 이 테이블이 현재 사용되지 않음을 나타냅니다.

액세스 속성을 정의하지 않으면 인증되지 않은 액세스가 허용됩니다.

### <a name="howto-tables-getidentity"></a>방법: 테이블을 사용하여 인증 클레임 사용
인증이 설정될 때 요청되는 다양한 클레임을 설정할 수 있습니다.  이러한 클레임은 `context.user` 개체를 통해 정상적으로 사용할 수 없습니다.  그러나 `context.user.getIdentity()` 메서드를 사용하여 검색할 수 있습니다.  `getIdentity()` 메서드는 개체로 확인되는 Promise를 반환합니다.  개체는 인증 방법(facebook, google, twitter, microsoftaccount 또는 aad)을 키로 사용합니다.

예를 들어 Microsoft 계정 인증을 설정하고 메일 주소 클레임을 요청하는 경우 다음 테이블 컨트롤러를 사용하여 레코드에 메일 주소를 추가할 수 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

사용할 수 있는 클레임을 보려면 웹 브라우저를 사용하여 사이트의 `/.auth/me` 끝점을 봅니다.

### <a name="howto-tables-disabled"></a>방법: 특정 테이블 작업에 대한 액세스 사용 안 함
테이블에 나타나는 것 외에도 액세스 속성은 개별 작업을 제어하는 데 사용될 수 있습니다.  네 가지 작업이 있습니다.

* *읽기* 는 테이블의 RESTful 가져오기 작업입니다.
* *삽입* 은 테이블의 RESTful POST 작업입니다.
* *업데이트* 는 테이블의 RESTful PATCH 작업입니다.
* *삭제* 는 테이블의 RESTful DELETE 작업입니다.

예를 들어 읽기 전용 인증되지 않은 테이블을 제공하려 할 수도 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>방법: 테이블 작업에 사용되는 쿼리 조정
테이블 작업에 대한 일반적인 요구 사항은 데이터의 제한된 보기를 제공하는 것입니다.  예를 들어 사용자가 본인의 레코드를 읽거나 업데이트하는 것만 가능하도록 인증된 사용자 ID로 태그가 지정된 테이블을 제공할 수 있습니다.  다음 테이블 정의는 이 기능을 제공합니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

일반적으로 쿼리를 실행하는 작업에는 where 절을 사용하여 조정할 수 있는 쿼리 속성이 있습니다. 쿼리 속성은 데이터 백 엔드가 처리할 수 있는 무언가에 OData 쿼리를 변환하는 데 사용되는 [QueryJS] 개체입니다.  앞의 예처럼 간단한 같음 쿼리의 경우 맵을 사용할 수 있습니다. 또한 특정 SQL 절을 추가할 수 있습니다.

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>방법: 테이블에 일시 삭제 구성
일시 삭제는 레코드를 실제로 삭제하지 않습니다.  대신 삭제된 열을 true로 설정하여 데이터베이스 내에서 삭제된 것으로 표시합니다.  모바일 클라이언트 SDK가 IncludeDeleted()를 사용하지 않는 경우 Azure Mobile Apps SDK는 일시 삭제된 레코드를 결과에서 자동으로 삭제합니다.  일시 삭제에 대한 테이블을 구성하려면 테이블 정의 파일에서 `softDelete` 속성을 설정합니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

WebJob, Azure 함수 또는 사용자 지정 API를 통해 클라이언트 응용 프로그램에서 레코드를 제거하는 메커니즘을 설정해야 합니다.

### <a name="howto-tables-seeding"></a>방법: 데이터를 사용하여 데이터베이스 시드
새 응용 프로그램을 만들 때 데이터가 있는 테이블을 시드할 수 있습니다.  다음과 같이 테이블 정의 JavaScript 파일 내에서 수행될 수 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

데이터의 시드는 Azure Mobile Apps SDK에서 테이블을 만들 때에만 수행됩니다.  테이블이 데이터베이스 내에 이미 있으면 데이터는 테이블에 삽입되지 않습니다.  동적 스키마를 설정한 경우 스키마는 시드된 데이터에서 유추됩니다.

서비스가 실행되기 시작하면 `tables.initialize()` 메서드를 명시적으로 호출하여 테이블을 만드는 것이 좋습니다.

### <a name="Swagger"></a>방법: Swagger 지원 사용
Azure App Service Mobile Apps는 기본 제공 [Swagger]를 지원합니다.  Swagger 지원을 사용하려면 먼저Swagger UI를 종속성으로 설치합니다.

    npm install --save swagger-ui

설치되면 Azure Mobile Apps 생성자에서 Swagger 지원을 사용할 수 있습니다.

    var mobile = azureMobileApps({ swagger: true });

개발 버전에서 Swagger 지원을 사용하려 합니다.  `NODE_ENV` 앱 설정을 활용하여 수행할 수 있습니다.

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

Swagger 끝점은 http://*yoursite*.azurewebsites.net/swagger에 위치합니다.  `/swagger/ui` 끝점을 통해 Swagger UI에 액세스할 수 있습니다.  전체 응용 프로그램에서 인증을 요구하도록 선택하면 Swagger가 오류를 생성합니다.  최상의 결과를 위해 Azure App Service 인증/권한 부여 설정 및 `table.access` 속성을 사용하는 제어 인증에서 인증되지 않은 요청을 허용하도록 선택합니다.

또한 로컬로 개발할 때 Swagger 지원을 원하는 경우 `azureMobile.js` 파일에 Swagger 옵션을 추가할 수 있습니다.

## <a name="a-namepushpush-notifications"></a><a name="push">푸시 알림
Mobile Apps는 수많은 모든 주요 플랫폼의 장치에 대상 푸시 알림을 보낼 수 있도록 Azure Notification Hubs와 통합됩니다. Notification Hubs를 사용하여 iOS, Android 및 Windows 장치에 푸시 알림을 보낼 수 있습니다. Notification Hubs를 통해 수행할 수 있는 모든 것에 대한 자세한 내용은 [Notification Hubs 개요](../notification-hubs/notification-hubs-push-notification-overview.md)를 참조하세요.

### </a><a name="send-push"></a>방법: 푸시 알림 보내기
다음 코드는 등록된 iOS 장치에 브로드캐스트 푸시 알림을 보내기 위해 push 개체를 사용하는 방법을 보여 줍니다.

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

클라이언트에서 템플릿 푸시 등록을 만들면 지원되는 모든 플랫폼의 장치에 템플릿 푸시 메시지를 대신 보낼 수 있습니다. 다음 코드는 템플릿 알림을 보내는 방법을 보여 줍니다.

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <a name="push-user"></a>방법: 태그를 사용하여 인증된 사용자에게 푸시 알림 보내기
인증된 사용자가 푸시 알림에 등록하면 사용자 ID 태그가 등록에 자동으로 추가됩니다. 이 태그를 사용하여 특정 사용자가 등록된 모든 장치에 푸시 알림을 보낼 수 있습니다. 다음 코드는 요청을 만드는 사용자의 SID를 가져오고 해당 사용자에 대한 모든 장치 등록에 템플릿 푸시 알림을 보냅니다.

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.

## <a name="CustomAPI"></a> 사용자 지정 API
### <a name="howto-customapi-basic"></a>방법: 사용자 지정 API 정의
/tables 끝점을 통한 데이터 액세스 API 외에도 Azure Mobile Apps는 사용자 지정 API 범위를 제공할 수 있습니다.  사용자 지정 API는 유사한 방식으로 테이블 정의에 정의되고 인증을 비롯한 동일한 시설에 액세스할 수 있습니다.

사용자 지정 API를 사용하여 App Service 인증을 사용하려는 경우 [Azure 포털] 에서 우선 App Service 인증을 구성해야 합니다.  Azure App Service에서 인증을 구성하는 데 대한 자세한 내용은 사용하려는 ID 공급자를 위한 구성 가이드를 검토합니다.

* [Azure Active Directory 인증을 구성하는 방법]
* [Facebook 인증을 구성하는 방법]
* [Google 인증을 구성하는 방법]
* [Microsoft 인증을 구성하는 방법]
* [Twitter 인증을 구성하는 방법]

사용자 지정 API는 거의 동일한 방식으로 테이블 API로 정의됩니다.

1. **api** 디렉터리 만들기
2. **api** 디렉터리에서 API 정의 JavaScript 파일을 만듭니다.
3. 가져오기 메서드를 사용하여 **API** 디렉터리를 가져옵니다.

다음은 이전에 사용된 기본 앱 샘플에 따른 프로토타입 API 정의입니다.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

*Date.now()* 메서드를 사용하여 서버 날짜를 반환하는 API 예제를 살펴보겠습니다.  다음은 api/date.js 파일입니다.

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

각 매개 변수는 GET, POST, PATCH 또는 DELETE와 같은 RESTful 표준 동사의 하나입니다.  메서드는 필요한 출력을 전송하는 표준 [ExpressJS 미들웨어] 함수입니다.

### <a name="howto-customapi-auth"></a>방법: 사용자 지정 API에 대한 액세스 인증 요구
Azure Mobile Apps SDK는 테이블 끝점 및 사용자 지정 API에 대해 동일한 방식으로 인증을 구현합니다.  이전 섹션에서 개발된 API에 인증을 추가하려면 **access** 속성을 추가합니다.

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

또한 특정 작업에 인증을 지정할 수 있습니다.

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

테이블 끝점에 사용되는 동일한 토큰은 인증을 요구하는 사용자 지정 API에 사용되어야 합니다.

### <a name="howto-customapi-auth"></a>방법: 대용량 파일 업로드 처리
Azure Mobile Apps SDK는 [body-parser middleware](https://github.com/expressjs/body-parser)를 사용하여 제출하는 본문 내용을 허용 및 디코딩합니다.  더 큰 파일 업로드를 허용하도록 body-parser를 미리 구성할 수 있습니다.

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

이 파일은 Base-64로 인코딩된 후 전송됩니다.  이렇게 하면 실제 업로드의 크기가 증가합니다(따라서 고려해야 할 크기도 증가).

### <a name="howto-customapi-sql"></a>방법: 사용자 지정 SQL 문 실행
Azure Mobile Apps SDK를 사용하면 정의된 데이터 공급자에 대해 매개 변수화된 SQL 문을 쉽게 실행할 수 있는 요청 개체를 통해 전체 컨텍스트에 액세스할 수 있습니다.

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>디버깅, 쉬운 테이블 및 간편한 API
### <a name="howto-diagnostic-logs"></a>방법: Azure Mobile Apps의 디버깅, 진단 및 문제 해결
Azure App Service는 Node.js 응용 프로그램에 대한 여러 디버깅 및 문제 해결 기술을 제공합니다.
Node.js 모바일 백 엔드 문제 해결에서 시작하는 다음 문서를 참조하세요.

* [Azure App Service 모니터링]
* [Azure App Service에 진단 로그 사용]
* [Visual Studio에서 Azure App Service 문제 해결]

Node.js 응용 프로그램은 넓은 범위의 진단 로그 도구에 액세스합니다.  내부적으로 Azure Mobile Apps Node.js SDK는 진단 로깅에 [윈스턴] 을 사용합니다.  [Azure 포털]에서 디버그 모드를 사용하거나 **MS_DebugMode** 앱 설정을 true로 설정하여 로깅이 자동으로 활성화합니다. 생성된 로그는 [Azure 포털]의 진단 로그에 표시됩니다.

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>방법: Azure 포털에서 테이블로 간편하게 작업
포털에서 쉬운 테이블을 통해 포털에서 테이블을 만들고 작업할 수 있습니다. 데이터 집합을 CSV 형식의 쉬운 테이블로 업로드할 수 있습니다. Azure Mobile Apps 백 엔드의 시스템 속성 이름과 충돌하는 속성 이름(CSV 데이터 집합)은 사용할 수 없습니다. 시스템 속성 이름은 다음과 같습니다.
* createdAt
* updatedAt
* deleted
* 버전

App Service 편집기를 사용하여 테이블 작업을 편집할 수도 있습니다. 백 엔드 사이트 설정에서 **쉬운 테이블** 을 클릭하면 테이블을 추가, 수정 또는 삭제할 수 있습니다. 테이블의 데이터를 볼 수 있습니다.

![쉬운 테이블 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

다음 명령을 테이블에 대한 명령 모음에서 사용할 수 있습니다.

* **사용 권한 변경** - 작업 테이블에서 읽기, 삽입, 업데이트 및 삭제에 대한 권한을 변경합니다.
  옵션은 익명 액세스를 허용하거나 인증을 요구하거나 작업에 대한 모든 액세스를 사용할 수 없도록 합니다.
* **스크립트 편집** - 테이블에 대한 스크립트 파일은 App Service 편집기에서 열립니다.
* **스키마 관리** - 열을 추가 또는 삭제하거나 테이블 인덱스를 변경합니다.
* **테이블 지우기** - 기존 테이블을 잘라서 모든 데이터 행을 삭제하지만 스키마를 그대로 둡니다.
* **행 삭제** - 데이터의 개별 행을 삭제합니다.
* **스트리밍 로그 보기** - 사이트에 대한 스트리밍 로그 서비스에 연결할 수 있습니다.

### <a name="work-easy-apis"></a>방법: Azure 포털에서 API로 간편하게 작업
포털에서 쉬운 API를 통해 포털에서 사용자 지정 API를 만들고 작업할 수 있습니다. App Service 편집기를 사용하여 API 스크립트를 편집할 수 있습니다.

백 엔드 사이트 설정에서 **쉬운 API** 를 클릭하면 사용자 지정 API 끝점을 추가, 수정 또는 삭제할 수 있습니다.

![쉬운 API 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

포털에서 지정된 HTTP 작업에 대한 액세스 권한을 변경하거나, App Service 편집기에서 API 스크립트 파일을 편집하거나, 스트리밍 로그를 볼 수 있습니다.

### <a name="online-editor"></a>방법: App Service 편집기에서 코드 편집
Azure Portal을 사용하면 로컬 컴퓨터에 프로젝트를 다운로드하지 않고도 App Service 편집기에서 Node.js 백 엔드 스크립트 파일을 편집할 수 있습니다. 온라인 편집기에서 스크립트 파일을 편집하려면

1. 모바일 앱 백 엔드 블레이드에서 **모든 설정** > **쉬운 테이블** 또는 **쉬운 API** 중 하나를 클릭하고 테이블 또는 API를 클릭한 다음 **스크립트 편집**을 클릭합니다. 스크립트 파일은 App Service 편집기에서 열립니다.

    ![App Service 편집기](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. 온라인 편집기에서 코드 파일의 내용을 변경합니다. 변경 내용은 입력할 때 자동으로 저장됩니다.

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android 클라이언트 빠른 시작]: app-service-mobile-android-get-started.md
[Apache Cordova 클라이언트 빠른 시작]: app-service-mobile-cordova-get-started.md
[iOS 클라이언트 빠른 시작]: app-service-mobile-ios-get-started.md
[Xamarin.iOS 클라이언트 빠른 시작]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android 클라이언트 빠른 시작]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms 클라이언트 빠른 시작]: app-service-mobile-xamarin-forms-get-started.md
[Windows 스토어 클라이언트 빠른 시작]: app-service-mobile-windows-store-dotnet-get-started.md
[오프라인 데이터 동기화]: app-service-mobile-offline-data-sync.md
[Azure Active Directory 인증을 구성하는 방법]: ../app-service/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook 인증을 구성하는 방법]: ../app-service/app-service-mobile-how-to-configure-facebook-authentication.md
[Google 인증을 구성하는 방법]: ../app-service/app-service-mobile-how-to-configure-google-authentication.md
[Microsoft 인증을 구성하는 방법]: ../app-service/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter 인증을 구성하는 방법]: ../app-service/app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service 배포 가이드]: ../app-service/app-service-deploy-local-git.md
[Azure App Service 모니터링]: ../app-service/web-sites-monitor.md
[Azure App Service에 진단 로그 사용]: ../app-service/web-sites-enable-diagnostic-log.md
[Visual Studio에서 Azure App Service 문제 해결]: ../app-service/web-sites-dotnet-troubleshoot-visual-studio.md
[노드 버전 지정]: ../nodejs-specify-node-version-azure-apps.md
[노드 모듈 사용]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure 포털]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[GitHub의 기본 앱 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[GitHub의 할 일 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[GitHub의 샘플 디렉터리]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Visual Studio용 Node.js Tools 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js 패키지]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS 미들웨어]: http://expressjs.com/guide/using-middleware.html
[윈스턴]: https://github.com/winstonjs/winston
