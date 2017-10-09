---
title: "hello Node.js 백 엔드 서버 모바일 앱에 대 한 SDK와 aaaHow toowork | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱에 대 한와 toowork Node.js 백 엔드 서버 SDK hello 하는 방법에 대해 알아봅니다."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>어떻게 toouse hello Azure 모바일 앱 Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

이 문서에서는 상세 정보와 예제를 보여 주는 방법을 Azure 앱 서비스 모바일 앱에서 Node.js 백 엔드와 toowork 합니다.

## <a name="Introduction"></a>소개
Azure 앱 서비스 모바일 앱 hello 기능 tooadd 모바일에 최적화 된 데이터 액세스 Web API tooa 웹 응용 프로그램을 제공합니다.  hello Azure 앱 서비스 모바일 앱 SDK는 ASP.NET 및 Node.js 웹 응용 프로그램에 제공 됩니다.  hello를 SDK hello를 다음 작업을 제공 합니다.

* 데이터 액세스를 위한 테이블 작업(읽기, 삽입, 업데이트, 삭제)
* API 작업 사용자 지정

두 작업은 모두 Facebook, Twitter, Google Microsoft 등과 같은 소셜 ID 공급자 뿐만 아니라 엔터프라이즈 ID에 대한 Azure Active Directory를 포함하는 Azure 앱 서비스에서 허용된 모든 ID 공급자에 걸쳐 인증을 제공합니다.

각각에 대 한 샘플 사례를 사용 하 여 hello에서 찾을 수 있습니다 [GitHub에서 예제 디렉터리]합니다.

## <a name="supported-platforms"></a>지원되는 플랫폼
Azure 모바일 앱 노드 SDK hello hello 현재 LTS 노드의 이상 릴리스를 지원 합니다.  문서를 작성할 당시 hello 최신 LTS 버전이 노드 첫 v4.5.0 합니다.  다른 버전의 노드는 작동할 수는 있지만 지원되지 않습니다.

Azure 모바일 앱 노드 SDK hello 두 데이터베이스 드라이버 지원-hello 노드 mssql 드라이버가 지 원하는 SQL Azure 및 로컬 SQL Server 인스턴스.  hello sqlite3 드라이버 단일 인스턴스에서 SQLite 데이터베이스를 지원합니다.

### <a name="howto-cmdline-basicapp"></a>방법: 명령줄 hello를 사용 하 여 기본 Node.js 백 엔드 만들기
모든 Azure 앱 서비스 모바일 앱 Node.js 백 엔드는 ExpressJS 응용 프로그램으로 시작합니다.  ExpressJS는 hello 가장 인기 있는 웹 서비스 프레임 워크 Node.js에 사용할 수 있습니다.  다음과 같이 기본 [Express] 응용 프로그램을 만들 수 있습니다.

1. 명령 창 또는 PowerShell 창에서 프로젝트의 디렉터리를 만듭니다.

        mkdir basicapp
2. Npm init tooinitialize hello 패키지 구조를 실행 합니다.

        cd basicapp
        npm init

    hello npm init 명령은 질문 tooinitialize hello 프로젝트 집합이 묻습니다.  Hello 예제 출력이 표시 됩니다.

    ![hello npm init 출력][0]
3. Hello npm 리포지토리에서 hello express 및 azure 모바일 앱 라이브러리를 설치 합니다.

        npm install --save express azure-mobile-apps
4. app.js 파일 tooimplement hello 기본 모바일 서버를 만듭니다.

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

이 응용 프로그램을 단일 끝점과 모바일 액세스에 최적화 된 WebAPI를 만듭니다 (`/tables/TodoItem`) 인증 되지 않은 액세스 tooan 동적 스키마를 사용 하 여 SQL 데이터 저장소를 기본 제공 하는 합니다.  다음의 클라이언트 라이브러리 빠른 시작에 적합합니다.

* [Android 클라이언트 빠른 시작]
* [Apache Cordova 클라이언트 빠른 시작]
* [iOS 클라이언트 빠른 시작]
* [Windows 스토어 클라이언트 빠른 시작]
* [Xamarin.iOS 클라이언트 빠른 시작]
* [Xamarin.Android 클라이언트 빠른 시작]
* [Xamarin.Forms 클라이언트 빠른 시작]

Hello에서이 기본 응용 프로그램에 대 한 hello 코드를 찾을 수 [GitHub에 basicapp 샘플]합니다.

### <a name="howto-vs2015-basicapp"></a>방법: Visual Studio 2015를 사용하여 노드 백 엔드 만들기
Visual Studio 2015 hello IDE 내에서 확장 toodevelop Node.js 응용 프로그램을 필요합니다.  toostart, 설치 hello [Visual Studio 용 Node.js 도구 1.1]합니다.  Visual Studio 용 Node.js 도구 hello 설치 되 면 Express 4.x 응용 프로그램을 만듭니다.

1. 열기 hello **새 프로젝트** 대화 (에서 **파일** > **새로** > **프로젝트...** ).
2. **템플릿** > **JavaScript** > **Node.js**으로 확장합니다.
3. 선택 hello **기본 Azure Node.js Express 4 응용 프로그램**합니다.
4. Hello 프로젝트 이름을 입력 합니다.  *확인*을 클릭합니다.

    ![Visual Studio 2015 새 프로젝트][1]
5. 마우스 오른쪽 단추로 클릭 hello **npm** 노드 선택한 **npm 패키지를 새 설치 중...** .
6. 첫 번째 Node.js 응용 프로그램을 만드는 방법에 toorefresh hello npm 카탈로그를 할 수 있습니다.  필요한 경우 **새로 고침** 을 클릭합니다.
7. 입력 *azure 모바일 앱* hello 검색 상자에 있습니다.  Hello 클릭 **azure 모바일 앱 2.0.0** 패키지 하 고, 한 다음 클릭 **패키지 설치**합니다.

    ![새 npm 패키지 설치][2]
8. **닫기**를 클릭합니다.
9. 열기 hello *app.js* 파일 hello Azure 모바일 앱 SDK에 대 한 tooadd 지원 합니다.  Hello 라이브러리의 줄에 6 hello 아래쪽에 문이 필요 hello 코드 다음을 추가 합니다.

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    선에서 약 27 hello 후 다른 app.use 문 코드 다음 hello를 추가 합니다.

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    Hello 파일을 저장 합니다.
10. Hello 응용 프로그램을 로컬 (http://localhost:3000에 배달 API 광고가 hello)를 실행 하거나 tooAzure 게시 합니다.

### <a name="create-node-backend-portal"></a>방법: hello Azure 포털을 사용 하 여 Node.js 백 엔드 만들기
Hello에 대 한 모바일 앱 백 엔드 권한을 만들 수 있습니다 [Azure 포털]합니다. 다음 단계 또는 클라이언트와 서버 hello를 수행 하 여 함께 만들 hello 하거나 따르면 [모바일 앱을 만들](app-service-mobile-ios-get-started.md) 자습서입니다. hello 자습서가이 지침의 단순화 된 버전을 포함 하 고 프로젝트 개념 증명에 가장 적합 합니다.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Hello에 다시 *시작* 블레이드 아래 **API 테이블을 만들**, 선택 **Node.js** 으로 프로그램 **백 엔드 언어**합니다.
Hello 확인란에 대 한 "**는 덮어씁니다 모든 사이트 콘텐츠. 것에 동의**"를 클릭 한 다음 **만들 TodoItem 테이블**합니다.

### <a name="download-quickstart"></a>방법: Git를 사용 하 여 다운로드 hello Node.js 백 엔드 퀵 스타트 코드 프로젝트
Hello 포털을 사용 하 여 Node.js 모바일 앱 백 엔드를 만들면 **퀵 스타트** 블레이드에서 Node.js 프로젝트 및 배포 된 tooyour 사이트에 대해 만들어집니다. 테이블 및 Api 추가 및 hello 포털에서 hello Node.js 백 엔드에 대 한 코드 파일을 편집할 수 있습니다. 다양 한 배포 도구 toodownload hello 백 엔드 프로젝트를 추가 하거나 테이블 및 Api를 수정한 다음 hello 프로젝트를 다시 게시할 수 있습니다 사용할 수도 있습니다. 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요. hello 다음 절차에서는 사용 Git 리포지토리 toodownload hello 퀵 스타트 프로젝트 코드입니다.

1. 아직 수행하지 않았다면 Git을 설치합니다. hello 단계 필요한 tooinstall Git 운영 체제 마다 다릅니다. 운영 체제별 배포 및 설치 지침은 [Git 설치](http://git-scm.com/book/en/Getting-Started-Installing-Git) 를 참조하세요.
2. Hello 단계에 따라 [사용 hello 앱 서비스 앱 저장소](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello 배포 사용자 이름 및 암호의 한 노트 백 엔드 사이트에 Git 리포지토리를 hello 합니다.
3. 모바일 앱 백 엔드에 대 한 hello 블레이드에서 hello 기록해 **Git 복제 URL** 설정 합니다.
4. Hello 실행 `git clone` 다음 예제와 같이 필요한 경우 암호를 입력 hello Git 복제 URL을 사용 하 여 명령을:

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. 앞 예제는 hello에서는 /todolist 인 검색 toolocal 디렉터리 및 프로젝트 파일에 다운로드 했습니다. Hello 찾을 `todoitem.json` hello에 대 한 파일 `/tables` 디렉터리입니다.  이 파일은 테이블의 사용 권한을 정의합니다.  Hello 오류도 찾을 `todoitem.js` hello 동일 파일 hello 테이블에 대 한 CRUD 작업 스크립트를 정의 하는 디렉터리입니다.
6. 변경을 마쳤으면 tooproject 파일을 한 후 명령을 tooadd, 커밋, 다음 변경 내용을 toohello 사이트 업로드를 수행 하는 hello를 실행 합니다.

        $ git commit -m "updated hello table script"
        $ git push origin master

    Tooexecute hello 먼저 새 파일 toohello 프로젝트에 추가 하면 `git add .` 명령입니다.

hello 사이트는 새로운 집합이 커밋 toohello 사이트 푸시됩니다 될 때마다 다시 게시 합니다.

### <a name="howto-publish-to-azure"></a>방법: Node.js 백 엔드 tooAzure 게시
Microsoft Azure hello Azure 서비스를 Azure 앱 서비스 모바일 앱 Node.js 백 엔드를 게시 하기 위한 여러 메커니즘을 제공 합니다.  여기에는 원본 제어에 따라 Visual Studio, 명령줄 도구 및 연속 배포 옵션에 통합된 배포 도구의 활용을 포함합니다.  이 항목에 대한 자세한 내용은 [Azure App Service 배포 가이드]를 참조하세요.

Azure 앱 서비스에는 배포하기 전에 검토해야 하는 Node.js 응용 프로그램에 대한 구체적인 조언이 있습니다.

* 어떻게 너무[hello 노드 버전을 지정 합니다.]
* 어떻게 너무[노드 모듈 사용]

### <a name="howto-enable-homepage"></a>방법: 응용 프로그램에 대한 홈페이지 사용
대부분의 응용 프로그램은 웹 및 모바일 앱의 조합 및 hello ExpressJS 프레임 워크 있습니다 toocombine 두 패싯 합니다.  그러나 경우에 따라 수도 있습니다 tooonly 구현 모바일 인터페이스.  것이 유용한 tooprovide 방문 페이지 tooensure hello 앱 서비스 실행 중입니다.  고유한 홈 페이지에 제공하거나 임시 홈 페이지를 사용할 수 있습니다.  tooenable 임시 홈 페이지를 사용 하 여 hello 다음 tooinstantiate Azure 모바일 앱:

    var mobile = azureMobileApps({ homePage: true });

로컬 개발 하는 경우이 옵션을 사용 하려면,이 설정은 tooyour를 추가할 수 있습니다 `azureMobile.js` 파일입니다.

## <a name="TableOperations"></a>테이블 작업
hello azure 모바일 앱 Node.js 서버 SDK 메커니즘을 제공 tooexpose 데이터 테이블을 WebAPI와 Azure SQL 데이터베이스에 저장 합니다.  다섯 가지 작업이 제공됩니다.

| 작업 | 설명 |
| --- | --- |
| GET /tables/*tablename* |Hello 테이블의 모든 레코드 가져오기 |
| GET /tables/*tablename*/:id |Hello 테이블에서 특정 레코드 가져오기 |
| POST /tables/*tablename* |Hello 테이블의 레코드를 만듭니다. |
| PATCH /tables/*tablename*/:id |Hello 테이블의 레코드 업데이트 |
| DELETE /tables/*tablename*/:id |Hello 테이블에서 레코드 삭제 |

이 WebAPI 지원 [OData] hello 테이블 스키마 toosupport 확장 [오프 라인 데이터 동기화]합니다.

### <a name="howto-dynamicschema"></a>방법: 동적 스키마를 사용하여 테이블 정의
테이블을 사용하기 전에 정의되어야 합니다.  테이블 스키마 (hello 개발자 정의 hello 스키마 내의 hello 열) 정적 또는 동적으로 정의할 수 있습니다 (SDK hello 컨트롤 hello 스키마 들어오는 요청에 따라). 또한 hello 개발자는 Javascript 코드 toohello 정의 추가 하 여 hello WebAPI의 특정 측면을 제어할 수 있습니다.

모범 사례로, hello 테이블 디렉터리에 Javascript 파일에 각 테이블을 정의한 다음 tables.import() 메서드 tooimport hello 테이블을 사용 해야 합니다.  Hello basic 앱을 확장 hello app.js 파일 조정 합니다.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

Hello 테이블에 정의 됩니다. / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

테이블은 기본적으로 동적 스키마를 사용합니다.  동적 스키마 오프 tooturn hello 앱 설정을 전역으로 설정 **MS_DynamicSchema** toofalse hello Azure 포털 내에서.

전체 예제는 hello에서 찾을 수 [GitHub에 todo 샘플]합니다.

### <a name="howto-staticschema"></a>방법: 정적 스키마를 사용하여 테이블 정의
Hello 열 tooexpose hello WebAPI 통해 명시적으로 정의할 수 있습니다.  hello azure 모바일 앱 Node.js SDK 제공 하는 오프 라인 데이터 동기화 toohello 목록에 필요한 모든 추가 열을 자동으로 추가 합니다.  예를 들어 빠른 시작 클라이언트 응용 프로그램은 텍스트(문자열) 및 완료(부울)이라는 두 열이 있는 테이블이 필요합니다.  
hello 테이블 hello 테이블 정의 JavaScript 파일에 (hello 테이블 디렉터리에 위치) 다음과 같이 정의할 수 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

테이블을 정적으로 정의 하는 경우 다음도 호출 해야 hello tables.initialize() 메서드 toocreate hello 데이터베이스 스키마 시작할 때입니다.  hello tables.initialize() 메서드 반환는 [프라미스] hello 웹 서비스는 hello 데이터베이스 초기화 하기 전에 요청을 처리 하지 않는 경우 되도록 합니다.

### <a name="howto-sqlexpress-setup"></a>방법: 로컬 컴퓨터에서 개발 데이터 저장소로 SQL Express 사용
hello Azure 모바일 앱 hello AzureMobile 앱 노드 SDK는 트랜잭션 구성을 위해 hello 초기 데이터 서비스를 제공할: SDK는 hello 초기 데이터를 처리 하기 위한 세 가지 옵션을 제공 합니다.

* 사용 하 여 hello **메모리** 드라이버 tooprovide 비 영구적인 예제 저장소
* 사용 하 여 hello **mssql** 드라이버 tooprovide 개발을 위한 SQL Express 데이터 저장소
* 사용 하 여 hello **mssql** 드라이버 tooprovide Azure SQL 데이터베이스 데이터 저장소를 사용 하 여 프로덕션에

Azure 모바일 앱 Node.js SDK hello hello를 사용 하 여 [mssql Node.js 패키지] tooestablish 연결 tooboth SQL Express 및 SQL 데이터베이스를 사용 합니다.  이 패키지는 SQL Express 인스턴스에서 TCP 연결을 사용해야 합니다.

> [!TIP]
> hello 메모리 드라이버는 완전 한 테스트 하기 위한 기능 집합을 제공 하지 않습니다.  로컬로 백 엔드 tootest을 원할 경우에서는 SQL Express 데이터 저장소의 hello 사용 고 권장 mssql 드라이버 hello 됩니다.
>
>

1. [Microsoft SQL Server 2014 Express]를 다운로드하고 설치합니다.  Hello SQL Server 2014 Express with Tools 버전 설치를 확인 합니다.  64 비트 지원 기능을 명시적으로 요구 하지 않는 한 hello 32 비트 버전 실행 하는 경우 메모리를 적게 사용 합니다.
2. Hello SQL Server 2014 구성 관리자를 실행 합니다.

   1. Hello 확장 **SQL Server 네트워크 구성** hello 왼쪽 트리 메뉴에서 노드.
   2. **SQLEXPRESS에 대한 프로토콜**을 클릭합니다.
   3. 마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **사용**을 선택합니다.  클릭 **확인** hello 팝업 대화 상자에서.
   4. 마우스 오른쪽 단추로 **TCP/IP**를 클릭하고 **속성**을 선택합니다.
   5. Hello 클릭 **IP 주소** 탭 합니다.
   6. Hello **IPAll** 노드.  Hello에 **TCP 포트** 필드에, 입력 **1433**합니다.

          ![Configure SQL Express for TCP/IP][3]
   7. **확인**을 클릭합니다.  클릭 **확인** hello 팝업 대화 상자에서.
   8. 클릭 **SQL Server 서비스** hello 왼쪽 트리 메뉴에 있습니다.
   9. 마우스 오른쪽 단추로 **SQL Server (SQLEXPRESS)**를 클릭하고 **다시 시작**을 선택합니다.
   10. Hello SQL Server 2014 구성 관리자를 닫습니다.
3. Hello SQL Server 2014 Management Studio를 실행 하 고 tooyour 로컬 SQL Express 인스턴스에 연결 합니다.

   1. Hello 개체 탐색기에서에서 인스턴스를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**
   2. 선택 hello **보안** 페이지.
   3. Hello 확인 **SQL Server 및 Windows 인증 모드** 선택
   4. **확인**

          ![Configure SQL Express Authentication][4]
   5. 확장 **보안** > **로그인** hello 개체 탐색기에서
   6. 마우스 오른쪽 단추로 **로그인**을 클릭하고 **새 로그인...**을 선택합니다.
   7. 로그인 이름을 입력합니다.  **SQL Server 인증**을 선택합니다.  암호를 입력 한 다음 hello 입력에 동일한 암호를 **암호 확인**합니다.  hello 암호 Windows 복잡성 요구 사항을 충족 해야 합니다.
   8. **확인**

          ![Add a new user tooSQL Express][5]
   9. 새 로그인을 마우스 오른쪽 단추로 클릭하고 **속성**
   10. 선택 hello **서버 역할** 페이지
   11. Hello 상자 다음 toohello 확인 **dbcreator** 서버 역할
   12. **확인**
   13. Hello SQL Server 2015 Management Studio를 닫습니다.

레코드 hello 사용자 이름 및 암호 선택한 확인 하십시오.  특정 데이터베이스 요구 사항에 따라 tooassign 추가 서버 역할 또는 권한을 할 수 있습니다.

Node.js 응용 프로그램 hello 읽고 hello **SQLCONNSTR_MS_TableConnectionString** 이 데이터베이스에 대 한 연결 문자열 hello에 대 한 환경 변수입니다.  환경 내에서 이 변수를 설정할 수 있습니다.  예를 들어이 환경 변수 PowerShell tooset를 사용할 수 있습니다.

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

TCP/IP 연결을 통해 hello 데이터베이스에 액세스 하 고 hello 연결에 대 한 사용자 이름 및 암호를 제공 합니다.

### <a name="howto-config-localdev"></a>방법: 로컬 개발에 대한 프로젝트 구성
Azure 모바일 앱 이라는 JavaScript 파일을 읽고 *azureMobile.js* hello 로컬 파일 시스템에서 합니다.  프로덕션 환경에서이 파일 tooconfigure hello Azure 모바일 앱 SDK를 사용 하 여-hello 내에서 응용 프로그램 설정을 사용 하지 않는 [Azure 포털] 대신 합니다.  hello *azureMobile.js* 파일 구성 개체를 내보낼 수 있어야 합니다.  hello 가장 일반적인 설정은 다음과 같습니다.

* 데이터베이스 설정
* 진단 로깅 설정
* 대체 CORS 설정

예로 *azureMobile.js* 데이터베이스 설정을 다음과 같이 앞 hello를 구현 하는 파일:

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

추가 하는 것이 좋습니다 *azureMobile.js* tooyour *.gitignore* 파일 (또는 파일을 무시 다른 소스 코드 제어) hello 클라우드에 저장 되지 tooprevent 암호입니다.  항상 hello 내에서 프로덕션 설정을 응용 프로그램 설정에서 구성 [Azure 포털]합니다.

### <a name="howto-appsettings"></a>방법: 모바일 앱에 대한 앱 설정 구성
Hello에 대부분의 설정은 *azureMobile.js* 파일이 hello에 해당 하는 응용 프로그램 설정을 [Azure 포털]합니다.  사용 하 여 hello 다음 tooconfigure 앱 설정에서 응용 프로그램을 나열합니다.

| 앱 설정 | *azureMobile.js* 설정 | 설명 | 유효한 값 |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |name |hello hello 앱 이름 |string |
| **MS_MobileLoggingLevel** |logging.level |메시지 toolog의 최소 로그 수준 |error, warning, info, verbose, debug, silly |
| **MS_DebugMode** |debug |디버그 모드를 사용 또는 사용하지 않도록 설정 |true, false |
| **MS_TableSchema** |data.schema |SQL 테이블에 대한 기본 스키마 이름 |string(기본값: dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |디버그 모드를 사용 또는 사용하지 않도록 설정 |true, false |
| **MS_DisableVersionHeader** |버전 (집합 tooundefined) |Hello X ZUMO-서버 버전 헤더를 사용 하지 않도록 설정 |true, false |
| **MS_SkipVersionCheck** |skipversioncheck |Hello 클라이언트 API 버전 검사를 사용 하지 않도록 설정 |true, false |

tooset 앱 설정:

1. Toohello 로그인 [Azure 포털]합니다.
2. 선택 **모든 리소스** 또는 **응용 프로그램 서비스** 모바일 응용 프로그램의 hello 이름을 클릭 합니다.
3. 기본적으로 hello 설정 블레이드에서가 열립니다. 열리지 않으면 **설정**을 클릭합니다.
4. 클릭 **응용 프로그램 설정** hello 일반 메뉴에 있습니다.
5. 응용 프로그램 설정 섹션 toohello를 스크롤하십시오.
6. 앱 설정에 이미 있는 경우 hello 앱 설정 tooedit hello 값의 hello 값을 클릭 합니다.
7. 응용 프로그램 설정에 없는 경우 hello 키 상자와 hello 값 상자에 hello 값에 hello 응용 프로그램 설정을 입력 합니다.
8. 완료했으면 **저장**을 클릭합니다.

대부분의 앱은 설정 변경 후 서비스를 다시 시작해야 합니다.

### <a name="howto-use-sqlazure"></a>방법: 프로덕션 데이터 저장소로 SQL 데이터베이스 사용
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

Azure SQL 데이터베이스를 데이터 저장소로 사용하면 모든 Azure 앱 서비스 응용 프로그램 형식에 걸쳐 동일합니다. 아직 수행 하지 않은, 이러한 단계 toocreate 모바일 앱 백 엔드를 수행 합니다.

1. Toohello 로그인 [Azure 포털]합니다.
2. Hello 왼쪽 위 hello 창의 hello 클릭에서 **+ 새로 만들기** 단추 > **웹 + 모바일** > **모바일 앱**, 모바일 앱 백 엔드에 대 한 이름을 제공 합니다.
3. Hello에 **리소스 그룹** 상자에 응용 프로그램으로 hello 이름과 같은 이름을 입력 합니다.
4. hello 기본 앱 서비스 계획 선택 되어 있습니다.  앱 서비스 계획 toochange을 원할 경우 후 그렇게 hello 앱 서비스 계획을 클릭 하 여 > **+ 새로 만들기**합니다.  Hello 새 앱 서비스 계획의 이름을 제공 하 고 적절 한 위치를 선택 합니다.  Hello 가격 책정 계층을 클릭 하 고 hello 서비스에 대 한 적절 한 가격대를 선택 합니다. 선택 **모든 보기** 더와 같은 옵션, 가격 책정 tooview **무료** 및 **Shared**합니다.  가격 책정 계층을 선택 하면 클릭 hello **선택** 단추입니다.  Hello에 다시 **앱 서비스 계획** 블레이드에서 클릭 **확인**합니다.
5. **만들기**를 클릭합니다. 모바일 앱 백 엔드를 프로비저닝하는 데 몇 분 정도 걸릴 수 있습니다.  Hello 포털이 열립니다 hello hello 모바일 앱 백 엔드는 프로 비전 되 면 **설정을** 블레이드 hello 모바일 앱 백 엔드에 대 한 합니다.

Hello 모바일 앱 백 엔드를 만든 후 tooeither 선택할 수 있습니다는 기존 SQL 데이터베이스 tooyour 모바일 앱 백 엔드 연결 하거나 새 SQL 데이터베이스를 만들어야 합니다.  이 섹션에서 SQL 데이터베이스를 만듭니다.

> [!NOTE]
> Hello에 데이터베이스를 이미 만든 경우 hello 모바일 앱 백 엔드에서와 동일한 위치를 선택할 수 있습니다 대신 **기존 데이터베이스를 사용 하 여** 한 다음 해당 데이터베이스를 선택 합니다. hello를 사용 하 여 다른 위치에 데이터베이스의 대기 시간이 늘어날 때문에 권장 되지 않습니다.
>
>

1. Hello 새로운 모바일 앱 백 엔드에서 클릭 **설정** > **모바일 앱** > **데이터** > **+ 추가**.
2. Hello에 **데이터 연결 추가** 블레이드에서 클릭 **SQL 데이터베이스-필요한 설정 구성** > **새 데이터베이스를 만들**합니다.  Hello에 hello 새 데이터베이스의 hello 이름을 입력 **이름** 필드입니다.
3. **서버**를 클릭합니다.  Hello에 **새 서버** 블레이드에서 hello에 고유한 서버 이름을 입력 **서버 이름** 필드를 한 번 살펴보고 적절 한 **서버 관리자 로그인** 및 **암호**.  확인 **허용 azure 서비스 tooaccess 서버** 을 선택 합니다.  **확인**을 클릭합니다.

    ![Azure SQL 데이터베이스 만들기][6]
4. Hello에 **새 데이터베이스** 블레이드에서 클릭 **확인**합니다.
5. Hello에 다시 **데이터 연결 추가** 블레이드를 **연결 문자열**, hello 로그인 및 사용자가 제공한 hello 데이터베이스를 만들 때 암호를 입력 합니다.  기존 데이터베이스를 사용 하는 경우 해당 데이터베이스에 대 한 hello 로그인 자격 증명을 제공 합니다.  입력한 다음 **확인**을 클릭합니다.
6. Hello에 다시 **데이터 연결 추가** 블레이드를 다시 클릭 **확인** toocreate hello 데이터베이스입니다.

<!--- END OF ALTERNATE INCLUDE -->

Hello 데이터베이스 만들기에는 몇 분 정도 걸릴 수 있습니다.  사용 하 여 hello **알림** 영역 toomonitor hello 배포의 진행 상황 hello 합니다.  Hello 데이터베이스를 성공적으로 배포 될 때까지 진행 되지 않습니다.  성공적으로 배포 되 면 모바일 백 엔드 응용 프로그램 설정의에서 hello SQL 데이터베이스 인스턴스에 대 한 연결 문자열을 생성 됩니다.  Hello에서이 응용 프로그램 설정을 볼 수 있습니다 **설정** > **응용 프로그램 설정** > **연결 문자열**합니다.

### <a name="howto-tables-auth"></a>방법: 액세스 tootables에 인증 필요
Hello에 응용 프로그램 서비스 인증을 구성 해야 응용 프로그램 서비스 인증 toouse hello 테이블 끝점을 사용 하려는 경우 [Azure 포털] 첫 번째입니다.  Azure 응용 프로그램 서비스에 인증을 구성 하는 방법에 대 한 자세한 내용은 hello id 공급자에 대 한 hello 구성 가이드를 확인 하려는 toouse:

* [어떻게 tooconfigure Azure Active Directory 인증]
* [어떻게 tooconfigure Facebook 인증]
* [어떻게 tooconfigure Google 인증]
* [어떻게 tooconfigure Microsoft 인증]
* [어떻게 tooconfigure Twitter 인증]

각 테이블에 사용 되는 toocontrol access toohello 테이블 일 수 있는 액세스 속성입니다.  다음 예제는 hello 인증 필요로 정적으로 정의 된 테이블을 보여 줍니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

hello 액세스 속성 세 값 중 하나를 사용할 수 있습니다.

* *익명* hello 클라이언트 응용 프로그램 인증 없이 tooread 데이터 허용 됨을 나타냅니다
* *인증 된* hello 클라이언트 응용 프로그램 hello 요청과 함께 유효한 인증 토큰이 송신 해야 함을 나타냅니다
* *사용 안 함* 은 이 테이블이 현재 사용되지 않음을 나타냅니다.

Hello 액세스 속성을 정의 하지 않으면 인증 되지 않은 액세스가 허용 됩니다.

### <a name="howto-tables-getidentity"></a>방법: 테이블을 사용하여 인증 클레임 사용
인증이 설정될 때 요청되는 다양한 클레임을 설정할 수 있습니다.  이러한 클레임이 hello를 통해 일반적으로 제공 되지 않습니다. `context.user` 개체입니다.  그러나 검색할 수 있는 hello를 사용 하 여 `context.user.getIdentity()` 메서드.  hello `getIdentity()` 메서드 tooan 개체를 확인 되는 프라미스를 반환 합니다.  hello 개체는 인증 방법 (facebook, google, twitter, microsoftaccount, 또는 aad)에서 입력 됩니다.

예를 들어 Microsoft 계정 인증 및 요청 hello 전자 메일 주소 클레임을 설정한 경우 다음 테이블 컨트롤러 hello로 hello 전자 메일 주소 toohello 레코드를 추가할 수 있습니다.

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee 어떤 클레임을 사용할 수, 웹 브라우저 tooview hello를 사용 하 여 `/.auth/me` 사이트의 끝점입니다.

### <a name="howto-tables-disabled"></a>방법: 사용 안 함 액세스 toospecific 테이블 작업
Hello 테이블에 추가 tooappearing, hello 액세스 속성 사용된 toocontrol 개별 작업 될 수 있습니다.  네 가지 작업이 있습니다.

* *읽기* 은 hello 테이블에 hello RESTful GET 작업
* *삽입* hello RESTful POST 작업 hello 테이블에는
* *업데이트* hello RESTful PATCH 작업 hello 테이블에는
* *삭제* hello 테이블에서 hello RESTful 삭제 작업은

예, 읽기 전용 인증 되지 않은 테이블 tooprovide를 지정할 수 있습니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>방법: 테이블 작업에 사용 되는 hello 쿼리를 조정 합니다.
테이블 작업에 대 한 일반적인 요구 사항은 tooprovide hello 데이터의 제한 된 보기입니다.  예를 들어 hello로 태그가 지정 된 테이블 에서만 읽을 하거나 사용자 고유의 레코드를 업데이트할 수 있도록 사용자 ID를 인증을 제공할 수 있습니다.  이 기능을 제공 하는 테이블 정의 다음 hello:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

일반적으로 쿼리를 실행하는 작업에는 where 절을 사용하여 조정할 수 있는 쿼리 속성이 있습니다. hello 쿼리 속성은 한 [QueryJS] 되는 개체를 사용 하는 백 엔드 데이터 hello 하는 OData 쿼리 toosomething tooconvert 처리할 수 있습니다.  (예: hello 앞서) 간단 비교의 경우에 대 한 지도 사용할 수 있습니다. 또한 특정 SQL 절을 추가할 수 있습니다.

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>방법: 테이블에 일시 삭제 구성
일시 삭제는 레코드를 실제로 삭제하지 않습니다.  대신 표시에 열 tootrue hello 삭제를 설정 하 여 hello 데이터베이스 내에서 삭제 합니다.  hello Azure 모바일 앱 SDK에서에서 자동으로 제거 일시 삭제 된 레코드 결과 hello 모바일 클라이언트 SDK IncludeDeleted() 사용 하지 않는 경우.  소프트에 대 한 테이블 삭제 tooconfigure hello 설정 `softDelete` hello 테이블 정의 파일에서 속성:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

WebJob, Azure 함수 또는 사용자 지정 API를 통해 클라이언트 응용 프로그램에서 레코드를 제거하는 메커니즘을 설정해야 합니다.

### <a name="howto-tables-seeding"></a>방법: 데이터를 사용하여 데이터베이스 시드
새 응용 프로그램을 만들 때 데이터가 있는 테이블을 tooseed를 지정할 수 있습니다.  이렇게 hello 테이블 정의 JavaScript 파일 내에서 다음과 같이 합니다.

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

데이터 시드 hello 테이블은 hello Azure 모바일 앱 SDK가 작성 하는 경우에 수행 됩니다.  Hello 테이블에 이미 있으면 hello 데이터베이스 내에서 데이터가 없는 hello 테이블에 삽입 됩니다.  동적 스키마를 설정 하는 경우 스키마는 hello 시드 데이터에서 유추 됩니다.

안녕하세요 명시적으로 호출 하는 것이 좋습니다 `tables.initialize()` hello 서비스 실행을 시작할 때 메서드 toocreate hello 테이블입니다.

### <a name="Swagger"></a>방법: Swagger 지원 사용
Azure 앱 서비스 모바일 앱은 기본 제공 [Swagger] 를 지원합니다.  먼저 tooenable Swagger 지원 종속성으로 hello swagger ui를 설치 합니다.

    npm install --save swagger-ui

설치 되 면 hello Azure 모바일 앱 생성자에서 Swagger 지원할 수 있습니다.

    var mobile = azureMobileApps({ swagger: true });

있습니다 수만 원하는 tooenable 개발 버전의 Swagger 지원 합니다.  `NODE_ENV` 앱 설정을 활용하여 수행할 수 있습니다.

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

hello swagger 끝점은에 http://*yoursite*.azurewebsites.net/swagger 합니다.  Hello Swagger UI hello 통해 액세스할 수 있습니다 `/swagger/ui` 끝점입니다.  Swagger 전체 응용 프로그램에서 toorequire 인증을 선택한 경우 오류가 발생 합니다.  최상의 결과 통해 인증 되지 않은 tooallow 요청에서 선택 hello Azure 앱 서비스 인증에에서 권한 부여 설정 후 hello를 사용 하 여 인증을 제어 하는 / `table.access` 속성입니다.

Hello Swagger 옵션 tooyour를 추가할 수도 있습니다 `azureMobile.js` 로컬로 개발할 때만 Swagger 지원을 원하는 경우에 파일입니다.

## <a name="a-namepushpush-notifications"></a><a name="push">푸시 알림
모바일 앱 통합 Azure 알림 허브 tooenable 하면 장치를 대상 toosend 푸시 알림을 toomillions 모든 주요 플랫폼 합니다. 알림 허브를 사용 하 여 푸시를 보낼 수 있습니다 알림 tooiOS, Android 및 Windows 장치입니다. 사용 하 여 수행할 수 있는 모든 작업에 대 한 자세한 toolearn 알림 허브 참조 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)합니다.

### </a><a name="send-push"></a>방법: 푸시 알림 보내기
코드 다음 hello toouse hello 푸시 개체 toosend 브로드캐스트 알림 tooregistered iOS 장치를 강제 하는 방법을 보여 줍니다.

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

Hello 클라이언트에서 템플릿 푸시 등록을 만들어, 지원 되는 모든 플랫폼에서 템플릿 푸시 메시지 toodevices 대신 보낼 수 있습니다. 코드에서 보여 주는 방법을 다음 hello toosend 템플릿 알림:

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>방법: 태그를 사용 하 여 사용자를 인증 하는 송신 푸시 알림을 tooan
인증된 된 사용자 푸시 알림에 등록, 사용자 ID 태그 toohello 등록 자동으로 추가 됩니다. 이 태그를 사용 하 여 푸시 알림 tooall 장치는 특정 사용자가 등록을 보낼 수 있습니다. hello 다음 코드 hello hello 요청을 만드는 사용자의 SID를 가져오고 해당 사용자에 대 한 템플릿 푸시 알림 tooevery 장치 등록을 보냅니다.

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.

## <a name="CustomAPI"></a> 사용자 지정 API
### <a name="howto-customapi-basic"></a>방법: 사용자 지정 API 정의
또한 toohello 데이터 액세스 API hello /tables 끝점을 통해, Azure 모바일 앱에서 사용자 지정 API 검사를 제공할 수 있습니다.  사용자 지정 Api와 비슷한 방식으로 toohello 테이블 정의에 정의 되어 있고 모든 액세스할 수 있습니다 hello 인증을 비롯 한 동일한 기능을 합니다.

Hello에 응용 프로그램 서비스 인증을 구성 해야 toouse 사용자 지정 API를 사용 하는 응용 프로그램 서비스 인증을 원하는 경우 [Azure 포털] 첫 번째입니다.  Azure 응용 프로그램 서비스에 인증을 구성 하는 방법에 대 한 자세한 내용은 hello id 공급자에 대 한 hello 구성 가이드를 확인 하려는 toouse:

* [어떻게 tooconfigure Azure Active Directory 인증]
* [어떻게 tooconfigure Facebook 인증]
* [어떻게 tooconfigure Google 인증]
* [어떻게 tooconfigure Microsoft 인증]
* [어떻게 tooconfigure Twitter 인증]

사용자 지정 Api에서 정의 된 hello 같은 방식으로 테이블 API hello 합니다.

1. **api** 디렉터리 만들기
2. API 정의 JavaScript 파일에는 hello에 만들 **api** 디렉터리입니다.
3. 사용 하 여 hello 가져오기 메서드 tooimport hello **api** 디렉터리입니다.

다음은 이전 사용 되는 hello basic 앱 샘플을 기준으로 hello 프로토타입 api 정의입니다.

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

예를 들어 hello를 사용 하 여 hello 서버 날짜를 반환 하는 API 보겠습니다 *Date.now()* 메서드.  다음은 hello api/date.js 파일입니다.

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

각 매개 변수에 hello 표준 RESTful 동사-GET, POST, PATCH 또는 DELETE 중 하나입니다.  hello 메서드는 표준 [ExpressJS 미들웨어] 를 보내는 데 필요한 hello 출력 함수입니다.

### <a name="howto-customapi-auth"></a>방법: 액세스 tooa 사용자 지정 API에 인증 필요
Hello에서 인증을 구현 하는 azure 모바일 앱 SDK hello 테이블 끝점 및 사용자 지정 Api를 모두에 동일 합니다.  Hello 이전 섹션에서 개발 된 인증 toohello API를 추가 하려면 추가 **액세스** 속성:

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
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

hello hello 테이블 끝점에 사용 되는 동일한 토큰 따라야 인증을 요구 하는 사용자 지정 Api에 대 한 합니다.

### <a name="howto-customapi-auth"></a>방법: 대용량 파일 업로드 처리
Azure 모바일 앱 SDK hello를 사용 하 여 [본문 파서 미들웨어](https://github.com/expressjs/body-parser) tooaccept 등록의 본문 콘텐츠를 디코딩합니다.  본문-파서 tooaccept 더 큰 파일 업로드를 미리 구성할 수 있습니다.

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

hello 파일은 base-64 전송 하기 전에 인코딩 형식입니다.  이 hello 실제 업로드의 hello 크기를 늘리는 (및 따라서 크기를 계산 해야 hello).

### <a name="howto-customapi-sql"></a>방법: 사용자 지정 SQL 문 실행
Azure 모바일 앱 SDK hello 액세스 toohello 허용 tooexecute 있도록 hello 요청 개체를 통해 전체 컨텍스트 SQL 문을 toohello 정의 된 데이터 공급자를 쉽게 parameterized:

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
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
몇 가지 디버깅 및 문제 해결 기술 Node.js 응용 프로그램에 대 한 hello Azure 앱 서비스를 제공 합니다.
Toohello 문서 tooget Node.js 모바일 백 엔드 문제 해결에서 시작 하는 다음을 참조 하십시오.

* [Azure 앱 서비스 모니터링]
* [Azure 앱 서비스에 진단 로그 사용]
* [Visual Studio에서 Azure 앱 서비스 문제 해결]

Node.js 응용 프로그램에 대 한 액세스 권한이 tooa 다양 한 진단 로그 도구입니다.  Azure 모바일 앱 Node.js SDK를 사용 하는 hello 내부적으로 [윈스턴] 진단 로깅에 대 한 합니다.  자동으로 로깅을 hello 설정 하거나 디버그 모드를 사용 하도록 설정 하 여 **MS_DebugMode** hello에 응용 프로그램 설정 tootrue [Azure 포털]합니다. Hello에 hello 진단 로그에에서 생성 된 로그 표시 [Azure 포털]합니다.

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>방법: hello Azure 포털에서에서 쉽게 테이블 작업
Hello 포털에서 쉽게 테이블을 사용 하 여 만들고 hello 포털에서 바로 테이블을 작업할 수 있도록 합니다. 도 hello 응용 프로그램 서비스 편집기를 사용 하 여 테이블 작업을 편집할 수 있습니다.

백 엔드 사이트 설정에서 **쉬운 테이블** 을 클릭하면 테이블을 추가, 수정 또는 삭제할 수 있습니다. Hello 테이블의에서 데이터를 볼 수 있습니다.

![쉬운 테이블 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

hello 다음 명령을 사용 하는 테이블에 대 한 hello 명령 모음에서:

* **사용 권한을 변경** -읽기에 대 한 hello 권한을 수정, 삽입, 업데이트 및 hello 테이블에 대 한 작업을 삭제 합니다.
  옵션은 tooallow 익명 액세스, toorequire 인증 또는 toodisable 모든 toohello 작업에 액세스 합니다.
* **스크립트를 편집** -hello 테이블에 대 한 hello 스크립트 파일은 hello 응용 프로그램 서비스 편집기에서에서 열립니다.
* **스키마 관리** -추가 또는 열 삭제 또는 hello 테이블 인덱스를 변경 합니다.
* **결과 지우기** -기존 테이블을 자릅니다 될 모든 데이터 행을 삭제 하지만 hello 스키마 변경 되지 않습니다.
* **행 삭제** - 데이터의 개별 행을 삭제합니다.
* **스트리밍 로그 보기** -toohello 스트리밍 사이트에 대 한 로그 서비스를 연결 합니다.

### <a name="work-easy-apis"></a>방법: hello Azure 포털에서 쉽게 Api를 사용 합니다.
Hello 포털에서 쉽게 Api를 사용 하 여 만들고 hello 포털에서 사용자 지정 Api 바로 작업할 수 있도록 합니다. 응용 프로그램 서비스 편집기 hello를 사용 하 여 API 스크립트를 편집할 수 있습니다.

백 엔드 사이트 설정에서 **쉬운 API** 를 클릭하면 사용자 지정 API 끝점을 추가, 수정 또는 삭제할 수 있습니다.

![쉬운 API 작업](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

Hello 포털에서 지정된 된 HTTP 동작에 대 한 액세스 권한을 hello 변경 hello API 스크립트 파일이 응용 프로그램 서비스 편집기에서 편집 하거나 hello 스트리밍 로그를 볼 수 있습니다.

### <a name="online-editor"></a>방법: hello 응용 프로그램 서비스 편집기에서에서 코드를 편집
Azure 포털 hello hello 프로젝트 tooyour 로컬 컴퓨터에 다운로드 하지 않고 hello 응용 프로그램 서비스 편집기의에서 Node.js 백 엔드 스크립트 파일을 편집할 수 있습니다. tooedit hello 온라인 편집기에서 스크립트 파일:

1. 모바일 앱 백 엔드 블레이드에서 **모든 설정** > **쉬운 테이블** 또는 **쉬운 API** 중 하나를 클릭하고 테이블 또는 API를 클릭한 다음 **스크립트 편집**을 클릭합니다. hello 스크립트 파일 hello 응용 프로그램 서비스 편집기에서에서 열립니다.

    ![앱 서비스 편집기](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Hello 온라인 편집기에서 변경 내용을 toohello 코드 파일을 확인 합니다. 변경 내용은 입력할 때 자동으로 저장됩니다.

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
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[오프 라인 데이터 동기화]: app-service-mobile-offline-data-sync.md
[어떻게 tooconfigure Azure Active Directory 인증]: app-service-mobile-how-to-configure-active-directory-authentication.md
[어떻게 tooconfigure Facebook 인증]: app-service-mobile-how-to-configure-facebook-authentication.md
[어떻게 tooconfigure Google 인증]: app-service-mobile-how-to-configure-google-authentication.md
[어떻게 tooconfigure Microsoft 인증]: app-service-mobile-how-to-configure-microsoft-authentication.md
[어떻게 tooconfigure Twitter 인증]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service 배포 가이드]: ../app-service-web/web-sites-deploy.md
[Azure 앱 서비스 모니터링]: ../app-service-web/web-sites-monitor.md
[Azure 앱 서비스에 진단 로그 사용]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Visual Studio에서 Azure 앱 서비스 문제 해결]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[hello 노드 버전을 지정 합니다.]: ../nodejs-specify-node-version-azure-apps.md
[노드 모듈 사용]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure 포털]: https://portal.azure.com/
[OData]: http://www.odata.org
[프라미스]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[GitHub에 basicapp 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[GitHub에 todo 샘플]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[GitHub에서 예제 디렉터리]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Visual Studio 용 Node.js 도구 1.1]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js 패키지]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS 미들웨어]: http://expressjs.com/guide/using-middleware.html
[윈스턴]: https://github.com/winstonjs/winston
