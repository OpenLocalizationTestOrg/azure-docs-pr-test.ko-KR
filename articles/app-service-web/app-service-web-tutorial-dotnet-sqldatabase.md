---
title: "SQL 데이터베이스를 사용 하 여 Azure에 ASP.NET 응용 프로그램 aaaBuild | Microsoft Docs"
description: "자세한 방법을 tooget는 ASP.NET 응용 프로그램 연결 tooa SQL 데이터베이스와 Azure에서 작업 합니다."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>SQL Database를 사용하여 Azure에서 ASP.NET 앱 빌드

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)는 확장성 있는 자체 패치 웹 호스팅 서비스를 제공합니다. 이 자습서에서는 toodeploy 데이터 기반 ASP.NET 웹 앱에 Azure 방법과 너무 연결[Azure SQL 데이터베이스](../sql-database/sql-database-technical-overview.md)합니다. 실행 중인 ASP.NET 앱이 있는 완료 된 경우 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) tooSQL 데이터베이스를 연결 합니다.

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * Azure에서 SQL Database 만들기
> * ASP.NET 응용 프로그램 tooSQL 데이터베이스 연결
> * Hello 앱 tooAzure 배포
> * Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure tooyour 터미널에서 스트림 로그
> * Hello Azure 포털에서에서 hello 응용 프로그램 관리

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서:

* 설치 [Visual Studio 2017](https://www.visualstudio.com/downloads/) 워크 로드를 수행 하는 hello로:
  - **ASP.NET 및 웹 배포**
  - **Azure 개발**

  ![ASP.NET 및 웹 개발 및 Azure 개발(웹 & 클라우드에서)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Hello 샘플 다운로드

[Hello 샘플 프로젝트를 다운로드](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip)합니다.

추출 (압축) hello *sqldb 자습서 master.zip dotnet* 파일입니다.

hello 샘플 프로젝트에는 기본 [ASP.NET MVC](https://www.asp.net/mvc) CRUD (만들기-읽기-업데이트-삭제) 응용 프로그램 사용 하 여 [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)합니다.

### <a name="run-hello-app"></a>Hello 앱 실행

열기 hello *dotnet-sqldb-자습서-마스터/DotNetAppSqlDb.sln* Visual Studio에서 파일입니다. 

형식 `Ctrl+F5` 디버깅 하지 않고 toorun hello 앱입니다. hello 앱은 기본 브라우저에 표시 됩니다. 선택 hello **새로 만들기** 에 연결 하 고 2를 만들어 *할 일* 항목입니다. 

![새 ASP.NET 프로젝트 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

테스트 hello **편집**, **세부 정보**, 및 **삭제** 링크 합니다.

hello 앱 hello 데이터베이스와 데이터베이스 컨텍스트 tooconnect를 사용합니다. Hello 데이터베이스 컨텍스트를이 샘플에서는 명명 된 연결 문자열을 사용 `MyDbConnection`합니다. 연결 문자열 hello hello에 설정 되어 *Web.config* 파일과에 언급 된 hello *Models/MyDatabaseContext.cs* 파일입니다. hello 자습서 tooconnect hello Azure 웹 앱 tooan Azure SQL 데이터베이스의 뒷부분에 나오는 hello 연결 문자열 이름이 사용 됩니다. 

## <a name="publish-tooazure-with-sql-database"></a>SQL 데이터베이스와 tooAzure 게시

Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 하면 **DotNetAppSqlDb** 프로젝트를 마우스 선택 **게시**합니다.

![솔루션 탐색기에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

**Microsoft Azure App Service**를 선택했는지 확인하고 **게시**를 클릭합니다.

![프로젝트 개요 페이지에서 게시](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

게시 열립니다 hello **응용 프로그램 서비스 만들기** 대화 상자에서 만들 모든 해줍니다 hello toorun Azure에서 ASP.NET 웹 앱을 필요한 Azure 리소스입니다.

### <a name="sign-in-tooazure"></a>TooAzure에 로그인

Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 클릭 **계정 추가**, tooyour Azure 구독에에서 로그인 합니다. 이미 Microsoft 계정에 로그인한 경우 계정에 Azure 구독이 있는지 확인합니다. Microsoft 계정 로그인 hello 없는 경우 Azure 구독, tooadd hello에 대 한 올바른 계정을 클릭 합니다.
   
![TooAzure에 로그인](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

로그인 한 후이 대화 상자에 Azure 웹 앱에 필요한 리소스를 모두 hello 준비 toocreate 것입니다.

### <a name="configure-hello-web-app-name"></a>Hello 웹 응용 프로그램 이름 구성

생성 된 hello 웹 응용 프로그램 이름, 유지 하거나 tooanother 고유 이름을 변경할 수 있습니다 (유효한 문자는 `a-z`, `0-9`, 및 `-`). hello 웹 앱 이름은 앱에 대 한 hello 기본 URL의 일부로 사용 됩니다 (`<app_name>.azurewebsites.net`여기서 `<app_name>` 웹 응용 프로그램 이름). 웹 앱 이름은 hello 필요 toobe 고유 Azure에서 모든 앱 간에 합니다. 

![앱 서비스 만들기 대화 상자](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

[!INCLUDE [resource-group](../../includes/resource-group.md)]

다음 너무**리소스 그룹**, 클릭 **새로**합니다.

![다음 tooResource 그룹에서 새로 만들기를 클릭 합니다.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Hello 리소스 그룹 이름 **myResourceGroup**합니다.

> [!NOTE]
> **만들기**는 클릭하지 마세요. 먼저 tooset 이후 단계에서 SQL 데이터베이스를 해야합니다.

### <a name="create-an-app-service-plan"></a>App Service 계획 만들기

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

다음 너무**앱 서비스 계획**, 클릭 **새로**합니다. 

Hello에 **앱 서비스 계획 구성** 대화 상자에서 다음 설정을 hello로 hello 새 앱 서비스 계획을 구성:

![App Service 계획 만들기](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| 설정  | 제안 값 | Blob에 대한 자세한 내용은 |
| ----------------- | ------------ | ----|
|**App Service 계획**| myAppServicePlan | [App Service 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**위치**| 서유럽 | [Azure 지역](https://azure.microsoft.com/regions/) |
|**크기**| 무료 | [가격 책정 계층](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>SQL Server 인스턴스 만들기

먼저 [Azure SQL Database 논리 서버](../sql-database/sql-database-features.md)가 있어야 데이터베이스를 만들 수 있습니다. 논리 서버는 그룹으로 관리되는 데이터베이스 그룹을 포함합니다.

**추가 Azure 서비스 탐색**을 선택합니다.

![웹앱 이름 구성](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

Hello에 **서비스** 탭에서 hello  **+**  아이콘 다음 너무**SQL 데이터베이스**합니다. 

![Hello 서비스 탭 hello + 아이콘을 클릭 다음 tooSQL 데이터베이스입니다.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

Hello에 **SQL 데이터베이스를 구성** 대화 상자를 클릭 하 여 **새로** 다음 너무**SQL Server**합니다. 

고유한 서버 이름이 생성됩니다. 이 이름은 논리 서버에 대 한 hello 기본 URL의 일부로 사용 됩니다 `<server_name>.database.windows.net`합니다. Azure의 모든 논리 서버 인스턴스에서 고유해야 합니다. Hello 서버 이름을 변경할 수 있지만이 자습서에 대 한 hello 생성 된 값을 유지 합니다.

관리자 사용자 이름과 암호를 추가한 다음 **확인**을 선택합니다. 암호 복잡성 요구 사항은 [암호 정책](/sql/relational-databases/security/password-policy)을 참조하세요.

이 사용자 이름과 암호를 기억해 두세요. Toomanage hello 논리 서버를 필요한 나중 인스턴스.

![SQL Server 인스턴스 만들기](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>SQL 데이터베이스 만들기

Hello에 **SQL 데이터베이스를 구성** 대화 상자: 

* 생성 된 hello 기본 유지 **데이터베이스 이름**합니다.
* **연결 문자열 이름**에 *MyDbConnection*을 입력합니다. 이 이름은 hello 연결 문자열에서 참조 되는 같아야 합니다. *Models/MyDatabaseContext.cs*합니다.
* **확인**을 선택합니다.

![SQL Database 구성](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

hello **응용 프로그램 서비스 만들기** 대화 상자에 만든 hello 리소스 표시 합니다. **만들기**를 클릭합니다. 

![만든 hello 리소스](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Hello 마법사 hello Azure 리소스 만들기를 완료 한 후에 ASP.NET 응용 프로그램 tooAzure 게시 합니다. 기본 브라우저 hello URL toohello 배포 응용 프로그램으로 시작 됩니다. 

몇 가지 할 일 항목을 추가합니다.

![Azure 웹앱의 게시된 ASP.NET 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

축하합니다. 데이터 기반 ASP.NET 응용 프로그램이 Azure App Service에서 라이브로 실행되고 있습니다.

## <a name="access-hello-sql-database-locally"></a>로컬로 hello SQL 데이터베이스에 액세스

Visual Studio를 사용 하면 탐색 및 hello에서 쉽게 새 SQL 데이터베이스 관리 **SQL Server 개체 탐색기**합니다.

### <a name="create-a-database-connection"></a>데이터베이스 연결 만들기

Hello에서 **보기** 메뉴 선택 **SQL Server 개체 탐색기**합니다.

Hello 위쪽에 **SQL Server 개체 탐색기**, hello 클릭 **SQL Server 추가** 단추입니다.

### <a name="configure-hello-database-connection"></a>Hello 데이터베이스 연결 구성

Hello에 **연결** 대화 상자에서 hello 확장 **Azure** 노드. 여기서는 Azure의 모든 SQL Database 인스턴스가 나열됩니다.

선택 hello `DotNetAppSqlDb` SQL 데이터베이스입니다. 앞에서 만든 hello 연결 hello 맨 아래에 자동으로 채워집니다.

앞에서 만든 hello 데이터베이스 관리자 암호를 입력 하 고 클릭 **연결**합니다.

![Visual Studio에서 데이터베이스 연결 구성](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>컴퓨터에서 클라이언트 연결 허용

hello **새 방화벽 규칙 만들기** 대화 상자를 열입니다. 기본적으로 SQL Database 인스턴스는 Azure 웹앱과 같은 Azure 서비스의 연결만 허용합니다. tooconnect tooyour 데이터베이스, SQL 데이터베이스 인스턴스의 hello 방화벽 규칙을 만듭니다. hello 방화벽 규칙에는 로컬 컴퓨터의 공용 IP 주소를 hello 허용 됩니다.

hello 대화는 컴퓨터의 공용 IP 주소가 이미 채워집니다.

**내 클라이언트 IP 추가**가 선택되어 있는지 확인하고 **확인**을 클릭합니다. 

![SQL Database 인스턴스에 대한 방화벽 설정](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

연결에 표시 SQL 데이터베이스 인스턴스에 대 한 hello 방화벽 설정을 만들어 Visual Studio 완료 되 면 **SQL Server 개체 탐색기**합니다.

여기에서 수행할 수 있습니다 hello 가장 데이터베이스와 같은 일반적인 작업이 실행된 된 쿼리를 뷰 및 저장된 프로시저를 만듭니다. 

Hello를 마우스 오른쪽 단추로 클릭 `Todoes` 테이블을 선택한 **데이터 보기**합니다. 

![SQL Database 개체 탐색](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Code First 마이그레이션으로 앱 업데이트

Azure의 hello tooupdate Visual Studio의에서 친숙 한 도구 데이터베이스 및 웹 앱을 사용할 수 있습니다. Entity Framework toomake 변경 tooyour 데이터베이스 스키마에서에서 Code First 마이그레이션을 사용 하 여이 단계에서는 tooAzure 게시 하십시오.

Entity Framework Code First 마이그레이션 사용에 대한 자세한 내용은 [MVC 5를 사용하여 Entity Framework 6 Code First 시작](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)을 참조하세요.

### <a name="update-your-data-model"></a>데이터 모델 업데이트

열기 _Models\Todo.cs_ hello 코드 편집기에서. 다음 속성 toohello hello 추가 `ToDo` 클래스:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Code First 마이그레이션을 로컬에서 실행

몇 가지 명령을 toomake 업데이트 tooyour 로컬 데이터베이스를 실행 합니다. 

Hello에서 **도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자** > **패키지 관리자 콘솔**합니다.

Hello 패키지 관리자 콘솔 창에서에서 Code First 마이그레이션을 사용 하도록 설정 합니다.

```PowerShell
Enable-Migrations
```

마이그레이션을 추가합니다.

```PowerShell
Add-Migration AddProperty
```

Hello 로컬 데이터베이스를 업데이트 합니다.

```PowerShell
Update-Database
```

형식 `Ctrl+F5` toorun hello 앱. 테스트 hello 세부 정보를 편집 및 링크를 만듭니다.

Hello 응용 프로그램 오류 없이 로드 됨, Code First 마이그레이션이 성공 했습니다. 그러나 페이지 여전히 찾습니다 hello 응용 프로그램 논리를이 새 속성을 아직 사용 하지 않으므로 동일 합니다. 

### <a name="use-hello-new-property"></a>Hello 새 속성을 사용 하 여

코드 toouse hello에 대 한 일부 변경 `Done` 속성입니다. 이 자습서에서는 간단한 설명을 위해만 거 toochange hello `Index` 및 `Create` 보기 toosee hello 속성을 실행에서 합니다.

_Controllers\TodosController.cs_를 엽니다.

Hello `Create()` 메서드 추가 `Done` hello 속성 목록이 toohello `Bind` 특성입니다. 완료 되 면 프로그램 `Create()` 메서드 시그니처 코드 다음 hello 같습니다.

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

_Views\Todos\Create.cshtml_을 엽니다.

Hello Razor 코드에에서 표시 됩니다는 `<div class="form-group">` 를 사용 하는 요소 `model.Description`, 다음 또 다른 `<div class="form-group">` 를 사용 하는 요소 `model.CreatedDate`합니다. 이러한 두 요소 바로 뒤에 `model.Done`을 사용하는 또 다른 `<div class="form-group">` 요소를 추가합니다.

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

_Views\Todos\Index.cshtml_을 엽니다.

빈 hello에 대 한 검색 `<th></th>` 요소입니다. 이 요소 위에 바로 hello Razor 코드 다음을 추가 합니다.

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Hello `<td>` hello 포함 된 요소 `Html.ActionLink()` 도우미 메서드. 이 요소 위에 바로 hello Razor 코드 다음을 추가 합니다.

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Hello toosee hello 변경 하면 이것이 `Index` 및 `Create` 보기. 

형식 `Ctrl+F5` toorun hello 앱.

이제 할 일 항목을 추가하고 **완료**를 확인할 수 있습니다. 그러면 홈페이지에 완료된 항목으로 표시됩니다. 해당 hello 기억 `Edit` 보기 hello 표시 되지 않는 `Done` hello를 변경 하지 않은 때문에 필드 `Edit` 보기.

### <a name="enable-code-first-migrations-in-azure"></a>Azure에서 Code First 마이그레이션 사용

코드 변경, 데이터베이스 migration을 비롯 한 했으므로 tooyour Azure web app을 게시 하 고 너무 Code First 마이그레이션을 사용 하면 SQL 데이터베이스를 업데이트 합니다.

이전과 마찬가지로 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.

클릭 **설정을** tooopen hello 게시 마법사.

![게시 설정 열기](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

Hello 마법사에서 **다음**합니다.

하는지 확인 한 hello 연결 문자열을 SQL 데이터베이스에 채워진 **MyDatabaseContext (MyDbConnection)**합니다. Tooselect hello 야 **myToDoAppDb** hello 드롭다운에서 데이터베이스. 

**Execute Code First Migrations (runs on application start)**(Code First 마이그레이션 실행(응용 프로그램 시작 시 실행))를 선택한 다음 **저장**을 클릭합니다.

![Azure 웹앱에서 Code First 마이그레이션 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>변경 내용 게시

이제 Azure 웹앱에서 Code First 마이그레이션을 사용하도록 설정했으므로 코드 변경 내용을 게시합니다.

Hello 게시 페이지, 클릭 **게시**합니다.

할 일 항목 추가를 다시 시도하고 **Done**(완료)을 선택합니다. 그러면 홈페이지에 완료된 항목으로 표시되어야 합니다.

![Code First 마이그레이션 후 Azure 웹앱](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

기존의 모든 할 일 항목이 계속 표시됩니다. ASP.NET 응용 프로그램을 다시 게시해도 SQL Database의 기존 데이터가 손실되지 않습니다. Code First 마이그레이션을 hello 데이터 스키마만 변경 되는 또한 기존 데이터를 그대로 둡니다.


## <a name="stream-application-logs"></a>응용 프로그램 로그 스트림

Azure 웹 앱 tooVisual Studio에서 직접 추적 메시지를 스트리밍할 수 있습니다.

_Controllers\TodosController.cs_를 엽니다.

각 동작은 `Trace.WriteLine()` 메서드로 시작됩니다. 이 코드가 tooshow 추가 하면 어떻게 tooadd 추적 메시지 tooyour Azure 웹 앱입니다.

### <a name="open-server-explorer"></a>서버 탐색기 열기

Hello에서 **보기** 메뉴 선택 **서버 탐색기**합니다. **서버 탐색기**에서 Azure 웹앱에 대한 로깅을 구성할 수 있습니다. 

### <a name="enable-log-streaming"></a>로그 스트리밍 사용

**서버 탐색기**에서 **Azure** > **App Service**를 확장합니다.

Hello 확장 **myResourceGroup** hello Azure 웹 앱을 처음 만들 때 만든 리소스 그룹입니다.

Azure 웹앱을 마우스 오른쪽 단추로 클릭하고 **스트리밍 로그 보기**를 선택합니다.

![로그 스트리밍 사용](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

hello 로그 이제 스트리밍되거나 hello에 **출력** 창. 

![출력 창에서 로그 스트리밍](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

그러나 표시 되지 않으면 hello 추적 메시지 중 하나가 아직 합니다. 먼저 선택 하므로 **스트리밍 로그 보기**, Azure 웹 앱 설정 hello 추적 수준이 너무`Error`만 오류 이벤트를 기록 하 (hello로 `Trace.TraceError()` 메서드).

### <a name="change-trace-levels"></a>추적 수준 변경

toochange hello 추적 수준을 toooutput 이동 다른 추적 메시지 다시 너무**서버 탐색기**합니다.

Azure 웹앱을 마우스 오른쪽 단추로 다시 클릭하고 **설정**을 선택합니다.

Hello에 **응용 프로그램 로깅 (파일 시스템)** 드롭다운 **Verbose**합니다. **Save**를 클릭합니다.

![추적 수준 tooVerbose 변경](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> 각 수준에 대해 표시 되는 메시지 유형을 다양 한 추적 수준 toosee를 테스트할 수 있습니다. 예를 들어 hello **정보** 수준에서 만들어진 모든 로그에 포함 됩니다. `Trace.TraceInformation()`, `Trace.TraceWarning()`, 및 `Trace.TraceError()`, 하지만에서 만들어진 로그 하지 `Trace.WriteLine()`합니다.
>
>

브라우저에서 Azure의 hello 할 일 목록 응용 프로그램 주위의 클릭 하십시오. hello 추적 메시지 toohello 스트리밍되거나 이제 **출력** Visual Studio의 창.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>로그 스트리밍 중지

toostop 로그 스트리밍 서비스 hello, hello 클릭 **모니터링을 중지** hello 단추 **출력** 창.

![로그 스트리밍 중지](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Azure Web App 관리

Toohello 이동 [Azure 포털](https://portal.azure.com) 만든 toosee hello 웹 앱입니다. 



Hello 왼쪽된 메뉴에서 클릭 **앱 서비스**, Azure 웹 앱의 hello 이름을 클릭 합니다.

![포털 탐색 tooAzure 웹 응용 프로그램](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

웹앱 페이지에 연결되었습니다. 

기본적으로 hello 포털 표시 hello **개요** 페이지. 이 페이지에서는 앱이 어떻게 작동하고 있는지를 보여 줍니다. 여기에서 찾아보기, 중지, 시작, 다시 시작, 삭제와 같은 기본 관리 작업을 수행할 수 있습니다. hello hello 페이지의 왼쪽에 hello 탭 hello 서로 다른 구성 페이지를 열 수를 표시 합니다. 

![Azure Portal의 App Service 페이지](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>다음 단계

이 자습서에서 학습한 방법은 다음과 같습니다.

> [!div class="checklist"]
> * Azure에서 SQL Database 만들기
> * ASP.NET 응용 프로그램 tooSQL 데이터베이스 연결
> * Hello 앱 tooAzure 배포
> * Hello 데이터 모델을 업데이트 하 고 hello 응용 프로그램을 다시 배포
> * Azure tooyour 터미널에서 스트림 로그
> * Hello Azure 포털에서에서 hello 응용 프로그램 관리

다음 자습서 toolearn toohello 진행 방법을 사용자 지정 DNS toomap toohello 웹 앱의 이름을 합니다.

> [!div class="nextstepaction"]
> [지도 기존 사용자 지정 DNS 이름 tooAzure 웹 응용 프로그램](app-service-web-tutorial-custom-domain.md)
