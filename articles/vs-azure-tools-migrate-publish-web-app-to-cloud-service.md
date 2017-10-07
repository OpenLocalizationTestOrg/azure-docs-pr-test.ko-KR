---
title: "Visual Studio에서 Azure 클라우드 서비스 aaaHow tooMigrate 및 웹 응용 프로그램 tooan 게시 | Microsoft Docs"
description: "자세한 내용은 방법 toomigrate 및 Visual Studio를 사용 하 여 웹 응용 프로그램 tooan Azure 클라우드 서비스를 게시 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9394adfd-a645-4664-9354-dd5df08e8c91
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: a2832c37d2ebdbc1e69a307d16b65b1c87e9070c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-migrate-and-publish-a-web-application-tooan-azure-cloud-service-from-visual-studio"></a>방법: 마이그레이션하고 게시할 웹 응용 프로그램 tooan Visual Studio에서 Azure 클라우드 서비스
호스팅 서비스와 Azure의 확장성 tootake 활용 hello, toomigrate 및 웹 응용 프로그램 tooan Azure 클라우드 서비스를 게시할 수 있습니다. 최소한의 변경 tooyour 기존 응용 프로그램과 함께 Azure에서 웹 응용 프로그램을 실행할 수 있습니다.

> [!NOTE]
> 이 항목은 서비스 toocloud 하지 tooweb 사이트 배포에 대 한 합니다. Tooweb 사이트를 배포 하는 방법에 대 한 정보를 참조 하십시오. [Azure 앱 서비스의 웹 앱을 배포](app-service-web/web-sites-deploy.md)합니다.
>
>

Visual C# 및 Visual Basic 모두에 대해 지원 되는 특정 템플릿의 목록은 hello 섹션을 참조 **프로젝트 템플릿 지원** 이 항목의 뒷부분에 나오는 합니다.

우선 Visual Studio에서 Azure용 웹 응용 프로그램을 사용하도록 설정해야 합니다. 다음 그림 hello 배포는 Azure 프로젝트 toouse를 추가 하 여 hello 주요 단계 toopublish 기존 웹 응용을 프로그램 보여 줍니다. 이 프로세스는 hello 필요한 웹 역할 tooyour 솔루션으로 Azure 프로젝트를 추가합니다. Hello의 형식을 기반으로 해야 하는 웹 프로젝트, 어셈블리에 대 한 hello 프로젝트 속성 업데이트 hello 서비스 패키지 배포를 위한 추가 어셈블리가 필요한 경우.

![웹 응용 프로그램 tooMicrosoft Azure 게시](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC748917.png)

> [!NOTE]
> hello **변환**, **tooAzure 클라우드 서비스 프로젝트를 변환** 명령은 솔루션의 hello 웹 프로젝트에 대해서만 표시 됩니다. 예를 들어 hello 명령이 솔루션의 Silverlight 프로젝트에 대해 제공 되지 않습니다.
> 응용 프로그램 tooAzure 게시 또는 서비스 패키지를 만들 때 경고 또는 오류가 발생할 수 있습니다. 이러한 경고와 오류 tooAzure를 배포 하기 전에 문제를 해결할 수 있습니다. 예를 들어 어셈블리 누락에 대한 경고가 표시될 수 있습니다. Tootreat 모든 경고를 오류로 확인 하려면 어떻게 해야 하는 방법에 대 한 자세한 내용은 [Visual Studio에서 Azure 클라우드 서비스 프로젝트 구성](vs-azure-tools-configuring-an-azure-project.md)합니다. 응용 프로그램을 작성, hello 계산 에뮬레이터를 사용 하 여 로컬로 실행 또는 tooAzure 게시 hello 다음 hello에 오류가 표시 될 수 있습니다 **오류 목록** 창: **hello 지정한 경로, 파일 이름 또는 둘 다가 너무 깁니다** . 이 오류는 hello 정규화 된 Azure 프로젝트 이름의 hello 길이가 너무 길기 때문에 발생 합니다. hello 전체 경로 포함 하 여 hello 프로젝트 이름의 hello 길이 146 자 이상 수 없습니다. 예를 들어,이 Silverlight 응용 프로그램에 대해 만들어진 Azure 프로젝트에 대 한 파일 경로 포함 하는 hello 전체 프로젝트 이름: `c:\users\<user name>\documents\visual studio 2015\Projects\SilverlightApplication4\SilverlightApplication4.Web.Azure.ccproj`합니다. 에 더 짧은 경로 tooreduce hello hello 정규화 된 프로젝트 이름의 솔루션 tooa 다른 디렉터리 toomove를 할 수 있습니다.
>
>

toomigrate 및 Visual Studio에서 웹 응용 프로그램 tooAzure 게시, 다음이 단계를 수행 합니다.

## <a name="enable-a-web-application-for-deployment-tooazure"></a>배포 tooAzure에 대 한 웹 응용 프로그램을 사용 하도록 설정
### <a name="tooenable-a-web-application-for-deployment-tooazure"></a>tooenable tooAzure 배포에 대 한 웹 응용 프로그램
1. tooenable 배포 tooAzure, 웹에 대 한 바로 가기 메뉴를 열고 hello에 대 한 웹 응용 프로그램 솔루션에서 프로젝트를 선택 하 고 Azure 배포 프로젝트 추가

    작업을 수행 하는 hello 발생 합니다.

   * Azure 프로젝트 라는 `<name of hello web project>.Azure` toohello 응용 프로그램 솔루션에 추가 됩니다.
   * Hello 웹 프로젝트에 대 한 웹 역할 toothis Azure 프로젝트에 추가 됩니다.
   * hello **로컬 복사** 속성이 tootrue MVC 2, MVC 3, MVC 4 및 Silverlight 비즈니스 응용 프로그램에 필요한 모든 어셈블리에 대 한 설정 되어 있습니다. 이 배포에 사용 되는 이러한 어셈블리 toohello 서비스 패키지를 추가 합니다.

   > [!IMPORTANT]
   > 다른 어셈블리나이 웹 응용 프로그램에 필요한 파일을 하는 경우 이러한 파일에 대 한 hello 속성을 수동으로 설정 해야 합니다. 이러한 속성을 참조 하는 tooset 방법에 대 한 정보에 대 한 섹션 hello **hello 서비스 패키지에에서 파일 포함** 이 문서의 뒷부분에 나오는 합니다.
   >
   > [!NOTE]
   > 특정 웹 프로젝트에 대 한 웹 역할 hello 솔루션에서 Azure 프로젝트에 이미 있는 경우 **변환**, **tooAzure 클라우드 서비스 프로젝트를 변환** 이 웹 프로젝트에 대 한 hello 바로 가기 메뉴에 표시 되지 않으면 .
   >
   >

   웹 응용 프로그램에서 여러 개의 웹 프로젝트가 있고 각 웹 프로젝트에 대해 toocreate 웹 역할을 원하는 경우에 각 웹 프로젝트에 대해이 절차에서는 hello 단계를 수행 해야 합니다. 그러면 각 웹 역할에 대해 별도의 Azure 프로젝트가 생성됩니다. 각 웹 프로젝트는 별도로 게시됩니다. 또는 웹 응용 프로그램에서 다른 웹 역할 tooan 기존 Azure 프로젝트를 수동으로 추가할 수 있습니다. toodo hello에 대 한이 열고 hello 바로 가기 메뉴 **역할** Azure 프로젝트에서 폴더 선택 **추가**, 다음 **솔루션의 웹 역할 프로젝트**, 웹 프로젝트 tooadd hello를 선택 합니다. 역할을 선택한 후 hello **확인** 단추입니다.

## <a name="use-an-azure-sql-database-for-your-application"></a>응용 프로그램에 Azure SQL 데이터베이스 사용
Hello 온-프레미스에 SQL Server 데이터베이스를 사용 하 여 웹 응용 프로그램에 대 한 연결 문자열을 설정한 경우 변경 해야이 연결 문자열 toouse SQL 데이터베이스 인스턴스의 Azure에서 호스팅되는 대신.

> [!IMPORTANT]
> 구독 toouse SQL 데이터베이스를 사용 해야 합니다. Hello에서 구독에 액세스할 경우 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), 구독을 제공 하는 서비스를 확인할 수 있습니다. hello 다음 지침이 적용 해제 toohello [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다. Hello를 사용 하는 경우 [Azure 포털](http://portal.microsoft.com), toohello 다음 절차를 건너뜁니다.
>
>

### <a name="toouse-a-sql-database-instance-in-your-web-role-for-your-connection-string"></a>toouse 연결 문자열에 대 한 웹 역할에서 SQL 데이터베이스 인스턴스
1. toocreate hello의 SQL 데이터베이스 인스턴스에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), hello hello 다음 문서에서에서 다음과 같이: [SQL 데이터베이스 서버 만들기](http://go.microsoft.com/fwlink/?LinkId=225109)합니다.

   > [!NOTE]
   > SQL 데이터베이스 인스턴스에 대 한 hello 방화벽 규칙을 설정할 때 hello를 선택 해야 **이 서버 다른 Azure 서비스 tooaccess 허용** 확인란 합니다.
   >
   >
2. hello hello 다음 문서에서에서 다음 섹션의 hello 단계를 수행 하는 연결 문자열에 대 한 SQL 데이터베이스 toouse 인스턴스가 toocreate: [SQL 데이터베이스 만들기](http://go.microsoft.com/fwlink/?LinkId=225110)합니다.
3. 연결 문자열에 대 한 toocopy hello ADO.NET 연결 문자열 toouse 수행 hello 단계를 수행 하는 hello [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.  

   1. Hello 선택 **데이터베이스** 단추를 사용 했는지 toocreate SQL 데이터베이스의 인스턴스는 hello 구독에 대 한 연 다음 hello 노드.
   2. SQL 데이터베이스의 toodisplay hello 사용 가능한 인스턴스가 선택 hello **SQL 데이터베이스** 노드.
   3. hello 데이터베이스에 대 한 toodisplay hello 속성 hello 데이터베이스를 선택 합니다. hello **속성** 뷰가 표시 됩니다.

      > [!NOTE]
      > 경우 hello **속성** 보기 표시 되지 않으면, 사용 하 여 hello 구분선 tooopen 할 수 있습니다.
      >
      >
   4. hello 줄임표 (...) 단추 다음 tooView toodisplay hello 연결 문자열을 선택 합니다.

      hello **연결 문자열** 대화 상자가 나타납니다.
   5. toocopy hello ADO.NET 연결 문자열 hello 텍스트를 강조 표시 하 고 hello Ctrl + C 키를 선택 합니다.
   6. tooclose hello 대화 상자에서 선택 하는 hello **닫기** 단추입니다.
4. tooreplace hello 연결 SQL 데이터베이스의이 인스턴스는 hello web.config 파일 toouse에서 문자열 hello web.config 파일, hello 기존 연결 문자열 항목을 강조 표시를 열고 hello Ctrl + V 키를 선택 합니다. SQL 데이터베이스 인스턴스 hello에 대 한 ADO.NET 연결 문자열 hello hello 기존 연결 문자열을 대체합니다.
5. Hello 매개 변수를 추가 해야 `MultipleActiveResultSets=True` toohello 연결 문자열입니다. hello 연결 문자열 형식에 따라 hello를 같아야 합니다.

    ```
    connectionString=”Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"
    ```
6. (선택 사항) 다른 방법은 toochanging hello 연결 문자열 직접 hello web.config 파일에서은 tooadd hello 빌드 구성 사용 하는 toocreate 서비스 패키지에 따라 hello web.config 변환 파일 중 하나에 섹션. Hello Web.Debug.Config 파일 또는 hello Web.Release.Config 파일을 엽니다. 이 파일에 다음 단원을 hello를 추가 합니다.

    ```
    XMLCopy<connectionStrings><addname="DefaultConnection"connectionString="Server=tcp:<database_server>.database.windows.net,1433;Database=<database_name>;User ID=<user_name>@<database_server>;Password=<myPassword>;Trusted_Connection=False;Encrypt=True;MultipleActiveResultSets=True"xdt:Transform="SetAttributes"xdt:Locator="Match(name)"/></connectionStrings>
    ```
7. 수정한 hello 파일을 저장 하 고 응용 프로그램을 게시 합니다.

### <a name="toouse-an-instance-of-sql-database-by-using-hello-azure-classic-portal"></a>toouse hello Azure 클래식 포털을 사용 하 여 SQL 데이터베이스 인스턴스
1. Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), hello SQL 데이터베이스 노드를 선택 합니다.

   * Hello toouse SQL 데이터베이스 인스턴스의 나타나면 선택 tooopen 것입니다.
   * 모든 인스턴스를 만들지 않은 경우 hello 적절 한 링크를 선택한 다음 인스턴스를 만듭니다.
2. 를 열고 하거나 데이터베이스 인스턴스를 만든 후 선택 hello **연결 문자열** 링크 합니다.
3. Hello 페이지의 hello 맨 아래에 hello 링크 tooconfigure 방화벽 설정을 선택 하 고 hello 기본값을 적용 또는 해야 하는 hello 값을 구성 합니다.
4. Hello ADO.NET 연결 문자열을 복사, hello 온-프레미스 데이터베이스에 대 한 오래 된 연결 문자열 hello 통해 web.config 파일에 붙여 넣고 있는지 tooadd 수 `MultipleActiveResultSets=True`합니다.

## <a name="publish-a-web-application-tooazure"></a>웹 응용 프로그램 tooAzure 게시
### <a name="toopublish-a-web-application-tooazure"></a>웹 응용 프로그램 tooAzure toopublish
1. tootest hello hello Azure 계산 에뮬레이터를 사용 하 여 hello 로컬 개발 환경에서 응용 프로그램을 Azure hello에 대 한 바로 가기 메뉴를 열고 hello hello 웹 역할에 대 한 프로젝트 및 선택 **시작 프로젝트로 설정**합니다. 그런 다음 **디버그**, **디버깅 시작**(키보드: **F5**)을 선택합니다.

    hello **Azure 디버깅 환경 시작 hello** 대화 상자가 열리고 hello 응용 프로그램이 hello 브라우저에서 시작 합니다. 계산 에뮬레이터 hello에 웹 응용 프로그램의 각 toostart 입력 하는 방법에 대 한 자세한 내용은이 섹션의 hello 표를 참조 하십시오.
2. 응용 프로그램 toopublish tooAzure에 대 한 hello 서비스를 tooset, Microsoft 계정과 Azure 구독이 있어야 합니다. 다음 서비스를 항목 tooset hello에서 단계를 사용 하 여 hello: [toopublish를 준비 하거나 Visual Studio에서 Azure 응용 프로그램 배포](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)합니다.
3. toopublish hello 웹 응용 프로그램 tooAzure hello 웹 프로젝트에 대 한 hello 바로 가기 메뉴를 열고 선택 **tooAzure 게시**합니다.

    hello **Azure 응용 프로그램 게시** 대화 상자가 열리고 Visual Studio hello 배포 프로세스를 시작 합니다. 어떻게 toopublish hello 응용 프로그램에 대 한 자세한 내용은 hello 섹션을 참조 하십시오. **Visual Studio에서 Azure 응용 프로그램을 게시** 에 [hello Azure Tools를 사용 하 여 클라우드 서비스 게시](vs-azure-tools-publishing-a-cloud-service.md)합니다.

   > [!NOTE]
   > 또한 hello Azure 프로젝트에서에서 hello 웹 응용 프로그램을 게시할 수 있습니다. toodo hello Azure 프로젝트에 대 한 hello 바로 가기 메뉴를 열고 선택이 **게시**합니다.
   >
   >
4. toosee hello hello 배포의 진행 상황을 hello를 볼 수 있습니다 **Azure 활동 로그** 창. 이 로그는 hello 배포 프로세스가 시작 될 때 자동으로 표시 됩니다. Hello 활동 로그에서 품목 hello를 확장할 수 tooshow 자세한 정보를 hello 다음 그림에에서 나와 있는 것 처럼:

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)
5. (선택 사항) toocancel hello 배포 프로세스를 hello 활동 로그에서 품목 hello에 대 한 hello 바로 가기 메뉴를 열고 선택한 **취소 및 제거**합니다. Hello 배포 프로세스를 중지 하 고 Azure에서 hello 배포 환경이 삭제 합니다.

   > [!NOTE]
   > 그 뒤에이 배포 환경 된 tooremove 배포 hello를 사용 해야 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
   >
   >
6. (선택 사항) 사용자의 역할 인스턴스가 시작 된 후 Visual Studio 자동으로 표시 hello 배포 환경 hello **Azure 계산** 노드에서 **클라우드 탐색기** 또는 **서버 탐색기**. 여기에서 hello 개별 역할 인스턴스의 hello 상태를 볼 수 있습니다.

    hello 다음 그림과의 hello 역할 인스턴스가 **서버 탐색기** 중일 때 여전히 Initializing 상태인 hello:

    ![VST_DeployComputeNode](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744134.png)
7. 배포 후 응용 프로그램 tooaccess hello 화살표 다음 tooyour 배포 때의 상태를 선택 **완료** hello에 표시 **Azure 활동 로그**합니다. 이 Azure에서 웹 응용 프로그램에 대 한 hello URL이 표시 됩니다. Hello 다음 어떻게 toostart 특정 유형의 Azure에서 웹 응용 프로그램에 대 한 hello 세부 정보에 대 한 표를 참조 하십시오.

    다음 표에서 hello toostart 특정 웹 응용 프로그램에서 Azure 또는 toorun 또는 hello Azure 계산 에뮬레이터를 사용 하 여 로컬로 웹 응용 프로그램을 디버깅 방법에 대 한 hello 세부 정보를 나열 합니다.

   | 웹 응용 프로그램 유형 | 실행/디버그 사용 하 여 로컬로 hello 계산 에뮬레이터 | Azure에서 실행 |
   | --- | --- | --- |
   | ASP.NET 웹 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Hello hello에 표시 되는 URL 하이퍼링크를 선택 **배포** hello에 대 한 탭 **Azure 활동 로그** hello 브라우저에 tooload hello 시작 페이지입니다. |
   | ASP.NET MVC 2 웹 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Hello hello에 표시 되는 URL 하이퍼링크를 선택 **배포** hello에 대 한 탭 **Azure 활동 로그** hello 브라우저에 tooload hello 시작 페이지입니다. |
   | ASP.NET MVC 3 웹 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Hello hello에 표시 되는 URL 하이퍼링크를 선택 **배포** hello에 대 한 탭 **Azure 활동 로그** hello 브라우저에 tooload hello 시작 페이지입니다. |
   | ASP.NET MVC 4 웹 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Hello hello에 표시 되는 URL 하이퍼링크를 선택 **배포** hello에 대 한 탭 **Azure 활동 로그** hello 브라우저에 tooload hello 시작 페이지입니다. |
   | ASP.NET 빈 웹 응용 프로그램 |웹 프로젝트에 대 한 hello 시작 페이지로 설정한 응용 프로그램에서.aspx 페이지를 추가 해야 합니다. Hello 메뉴 모음에서 선택 합니다 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |응용 프로그램에 기본.aspx 페이지가 있는 경우 hello hello에 표시 되는 URL 하이퍼링크를 선택 **배포** hello에 대 한 탭 **Azure 활동 로그** hello 브라우저에서이 페이지가 로드 됩니다. 다른.aspx 페이지가 있는 경우 url에 대 한 형식에 따라 hello를 사용 하 여 toonavigate toothis 특정 페이지가 필요 합니다.`<url for deployment>/<name of page>.aspx` |
   | Silverlight 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Toonavigate toohello 특정 페이지 url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 필요 합니다.`<url for deployment>/<name of page>.aspx` |
   | Silverlight 비즈니스 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Toonavigate toohello 특정 페이지 url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 필요 합니다.`<url for deployment>/<name of page>.aspx` |
   | Silverlight 탐색 응용 프로그램 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Toonavigate toohello 특정 페이지 url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 필요 합니다.`<url for deployment>/<name of page>.aspx` |
   | WCF 서비스 응용 프로그램 |Hello 시작 페이지로 WCF 서비스 프로젝트에 대 한 hello.svc 파일을 설정 해야 합니다. Hello 메뉴 모음에서 선택 합니다 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 대 한 toonavigate toohello svc 파일이 필요:`<url for deployment>/<name of service file>.svc` |
   | WCF 워크플로 서비스 응용 프로그램 |Hello 시작 페이지로 WCF 서비스 프로젝트에 대 한 hello.svc 파일을 설정 해야 합니다. Hello 메뉴 모음에서 선택 합니다 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 대 한 toonavigate toohello svc 파일이 필요:`<url for deployment>/<name of service file>.svc` |
   | ASP.NET 동적 엔터티 |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |Hello 연결 문자열을 업데이트 해야 합니다 (다음 섹션 참조). Url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 대 한 toonavigate toohello 특정 페이지 구성 요소도 필요.`<url for deployment>/<name of page>.aspx` |
   | ASP.NET 동적 데이터 Linq tooSQL |Hello 메뉴 모음에서 **디버그**, **디버깅 시작** (키보드: hello 선택 **F5** 키입니다.). |이 절차의 hello 단계를 수행 해야 합니다: 응용 프로그램에 대 한 SQL Azure 데이터베이스를 사용 하 여 (이 항목의 이전 섹션 참조). Url에 대 한 형식에 따라 hello를 사용 하 여 응용 프로그램에 대 한 toonavigate toohello 특정 페이지 구성 요소도 필요.`<url for deployment>/<name of page>.aspx` |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>ASP.NET 동적 엔터티의 연결 문자열 업데이트
### <a name="tooupdate-a-connection-string-for-aspnet-dynamic-entities"></a>tooUpdate ASP.NET 동적 엔터티에 대 한 연결 문자열
1. toocreate ASP.NET 동적 엔터티 웹 응용 프로그램에서 사용할 수 있는 SQL Azure 데이터베이스에서에서 다음과 같이 hello hello 프로시저 **SQL Azure 데이터베이스를 사용 하 여 응용 프로그램에 대 한** 이 항목의에서 앞부분입니다.
2. Hello 테이블과 필드를 hello에서이 데이터베이스에 필요한 추가 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)합니다.
3. 이 유형의 응용 프로그램에 대 한 연결 문자열 hello hello web.config 파일의 형식에 따라 hello에 있습니다.  

    ```
    <addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```

    업데이트 hello *connectionString* SQL Azure 데이터베이스에 대 한 ADO.NET 연결 문자열 hello로 다음과 같은 값:

    ```
    XMLCopy<addname="tempdbEntities"connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"providerName="System.Data.EntityClient"/>
    ```
4. toohello 연결 문자열 hello 메뉴 모음에서 선택 사항을 hello 변경과 toosave hello web.config 파일 **파일**, **web.config 저장**합니다.

## <a name="supported-project-templates"></a>지원되는 프로젝트 템플릿
웹 응용 프로그램 tooAzure toopublish hello 응용 프로그램에 사용 해야 hello 프로젝트 템플릿 중 하나 C# 또는 Visual Basic을 사용 하 여 hello 테이블 아래에 나열 됩니다.

| 프로젝트 템플릿 그룹 | 프로젝트 템플릿 |
| --- | --- |
| 웹 |ASP.NET 웹 응용 프로그램 |
| 웹 |ASP.NET MVC 2 웹 응용 프로그램 |
| 웹 |ASP.NET MVC 3 웹 응용 프로그램 |
| 웹 |ASP.NET MVC4 웹 응용 프로그램 |
| 웹 |ASP.NET 빈 웹 응용 프로그램 |
| 웹 |ASP.NET MVC 2 빈 웹 응용 프로그램 |
| 웹 |ASP.NET 동적 데이터 엔터티 웹 응용 프로그램 |
| 웹 |ASP.NET 동적 데이터 Linq tooSQL 웹 응용 프로그램 |
| Silverlight |Silverlight 응용 프로그램 |
| Silverlight |Silverlight 비즈니스 응용 프로그램 |
| Silverlight |Silverlight 탐색 응용 프로그램 |
| WCF |WCF 서비스 응용 프로그램 |
| WCF |WCF 워크플로 서비스 응용 프로그램 |
| 워크플로 |WCF 워크플로 서비스 응용 프로그램 |

## <a name="next-steps"></a>다음 단계
게시에 대 한 자세한 내용은 참조 하십시오. [tooPublish를 준비 하거나 Visual Studio에서 Azure 응용 프로그램 배포](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)합니다. 또한 [명명된 인증 자격 증명 설정](vs-azure-tools-setting-up-named-authentication-credentials.md)도 참조하세요.
