---
title: "aaaGet 샘플을 시작"
description: "Power BI 포함, SDK tooadd 비즈니스 인텔리전스 응용 프로그램에 대화형 Power BI 보고서를 사용 하 여"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a>Power BI Embedded 시작 샘플

**Microsoft Power BI Embedded**를 사용하면 Power BI 보고서를 웹 또는 모바일 응용 프로그램에 통합할 수 있습니다. 이 문서에서는 합니다 소개 toohello **Power BI 포함** get 시작된 샘플.

본론, 전에는 다음 리소스 toosave hello를 설치할 좋을 것입니다. 너무 hello 샘플 응용 프로그램 및 앱에 Power BI 보고서 통합 때 도움이 됩니다.

* [샘플 작업 영역 웹앱](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API 참조](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet을 통해 사용 가능)
* [JavaScript Report Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Toocreate 하나 이상 실행된 hello Power BI 포함 가져오기 샘플을 시작 및 구성할 수 있습니다, 전에 해야 **작업 영역 컬렉션** Azure 구독에 있습니다. toolearn 어떻게 toocreate는 **작업 영역 컬렉션** hello Azure 포털에서에서 볼 [Power BI embedded 시작](power-bi-embedded-get-started.md)합니다.

## <a name="configure-hello-sample-app"></a>Hello 샘플 응용 프로그램 구성

Visual Studio 개발 환경 tooaccess hello 구성 요소가 필요한 toorun hello 샘플 앱을 설정 하는 과정을 살펴보겠습니다.

1. 다운로드 하 고 hello 압축을 풀면 [Power BI 포함-웹 응용 프로그램에 보고서 통합](http://go.microsoft.com/fwlink/?LinkId=761493) GitHub의 샘플입니다.
2. Visual Studio에서 **PowerBI-embedded.sln** 을 엽니다. Tooexecute hello 야 **업데이트 패키지** hello이이 솔루션에서 사용 되는 순서 tooupdate hello 패키지에서 NuGET 패키지 관리자 콘솔에서 명령을 합니다.
3. Hello 솔루션을 빌드하십시오.
4. Hello 실행 **ProvisionSample** 콘솔 앱입니다. Hello 샘플 콘솔 응용 프로그램에서 작업 영역을 프로 비전 하 고 PBIX 파일을 가져옵니다.
5. 새 tooprovision **작업 영역**, 1, 옵션을 선택 **컬렉션 관리**, 다음 6 옵션을 선택 하 고 **새 작업 영역을 프로 비전**
6. 새 tooimport **보고서**, 2, 옵션을 선택 **관리 보고서**, 선택한 후 옵션 3, **가져오기 PBIX 데스크톱 파일을 작업 영역으로**합니다.

7. **작업 영역 컬렉션** 이름 및 **선택키**를 입력합니다. Hello에서 얻을 수 있습니다 **Azure 포털**합니다. toolearn 방법에 대 한 자세한 tooget 프로그램 **선택 키**, 참조 [Power BI API 액세스 키 보기](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) 에서 Microsoft Power BI embedded 시작 합니다.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. 복사 하 고 새로 만든 hello 저장 **작업 영역 ID** 이 문서의 뒷부분에 나오는 toouse 합니다. Hello 후 **작업 영역 ID** 가 만들어지면를 찾을 수 있습니다 hello **Azure 포털**합니다.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport PBIX 파일을으로 프로그램 **작업 영역**, 옵션을 선택 **6입니다. 기존 작업 영역**에 PBIX Desktop 파일을 가져옵니다. Hello를 다운로드할 수 파일 편리한 PBIX를 설정 하지 않은 경우 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)합니다.
10. 메시지가 표시되면 **데이터 집합**의 식별 이름을 입력합니다.

다음과 같은 응답이 표시됩니다.

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> PBIX 파일에 직접 쿼리 연결을 있으면 옵션 7 tooupdate hello 연결 문자열을 실행 합니다.

이제 Power BI PBIX 보고서를 **작업 영역**에 가져왔습니다. 이제는 방법에 살펴보겠습니다 toorun hello **Power BI 포함** 시작된 샘플 웹 응용 프로그램을 가져옵니다.

## <a name="run-hello-sample-web-app"></a>Hello 샘플 웹 응용 프로그램 실행
웹 앱 샘플 hello로 가져올 보고서를 렌더링 하는 샘플 응용 프로그램은 프로그램 **작업 영역**합니다. 어떻게 tooconfigure hello 웹 앱 샘플은 다음과 같습니다.

1. Hello에 **PowerBI 포함** Visual Studio 솔루션을 오른쪽 클릭 hello **EmbedSample** 웹 응용 프로그램을 선택 하 고 **시작 프로젝트로 설정**합니다.
2. **web.config**, hello에 **EmbedSample** 웹 응용 프로그램을 편집 hello **appSettings**: **AccessKey**,  **WorkspaceCollection** 이름 및 **WorkspaceId**합니다.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Hello 실행 **EmbedSample** 웹 응용 프로그램입니다.

실행 된 hello **EmbedSample** 웹 응용 프로그램에서는 hello 왼쪽된 탐색 패널 있어야는 **보고서** 메뉴. 확장을 가져온 tooview hello 보고서 **보고서**, 보고서를 클릭 합니다. Hello를 가져온 경우 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello 샘플 웹 응용 프로그램은 다음과 같습니다.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

보고서를 클릭 한 후 hello **EmbedSample** 웹 응용 프로그램 같아야이:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Hello 샘플 코드 탐색

hello **Microsoft Power BI Embedded** 샘플 표시 하는 예제 웹 응용 프로그램은 toointegrate **Power BI** 앱에는 보고서입니다. 모델-뷰-컨트롤러 (MVC)을 사용 하 여 패턴 toodemonstrate에 대 한 유용한 정보를 디자인 합니다. 이 섹션에서는 hello 내에서 탐색할 수 있는 hello 샘플 코드의 일부를 요약 **PowerBI 포함** 웹 응용 프로그램 솔루션입니다. hello 모델-뷰-컨트롤러 (MVC) 패턴을 구분 hello 도메인, hello 프레젠테이션 및 세 가지 별도 클래스에 대 한 사용자 입력에 따라 hello 동작의 hello 모델링: 모델, 뷰 및 제어 합니다. MVC에 대해 자세히 toolearn 참조 [ASP.NET에 대 한 자세한 내용은](http://www.asp.net/mvc)합니다.

hello **Microsoft Power BI Embedded** 샘플 코드는 다음과 같이 구분 됩니다. 각 섹션에 hello 파일 이름을 hello PowerBI embedded.sln 솔루션 hello 샘플에서 hello 코드를 쉽게 찾을 수 있도록 합니다.

> [!NOTE]
> 이 섹션은 요약 hello 코드를 작성 하는 방법을 보여 주는 hello 샘플 코드입니다. 전체 tooview hello 샘플, Visual Studio에서 PowerBI embedded.sln hello 솔루션을 로드 하십시오.

### <a name="model"></a>모델

hello 샘플에는 **ReportsViewModel** 및 **ReportViewModel**합니다.

**ReportsViewModel.cs**: 여러 Power BI 보고서를 나타냅니다.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: 하나의 Power BI 보고서를 나타냅니다.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>연결 문자열

형식에 따라 hello hello 연결 문자열 이어야 합니다.

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

일반적인 서버 및 데이터베이스 특성을 사용할 수 없습니다. 예: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>보기

hello **보기** Power BI의 hello 표시를 관리 **보고서** 및 Power BI **보고서**합니다.

**Reports.cshtml**: 반복 **Model.Reports** toocreate는 **ActionLink**합니다. hello **ActionLink** 다음과 같이 구성 됩니다.

| 부 | 설명 |
| --- | --- |
| 제목 |Hello 보고서의 이름입니다. |
| QueryString |링크 toohello 보고서 id입니다. |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

Report.cshtml: hello 설정 **Model.AccessToken**, 람다 식에 대 한 hello 및 **PowerBIReportFor**합니다.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Controller

**DashboardController.cs**: **앱 토큰**을 전달하는 PowerBIClient를 만듭니다. JSON 웹 토큰 (JWT) hello에서 만들어집니다. **서명 키** tooget hello **자격 증명**합니다. hello **자격 증명** 사용된 toocreate의 인스턴스는 **PowerBIClient**합니다. **PowerBIClient** 인스턴스가 작성되면 GetReports() 및 GetReportsAsync()를 호출할 수 있습니다.

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


작업<ActionResult> 보고서(문자열 reportId)

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a>앱에 보고서 통합

있으면는 **보고서**를 사용 하면 프로그램 **IFrame** tooembed hello Power BI **보고서**합니다. 다음은 hello에 powerbi.js에서 코드 조각 **Microsoft Power BI Embedded** 샘플.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>응용 프로그램에 포함된 보고서 필터링

URL 구문을 사용하여 포함된 보고서를 필터링할 수 있습니다. toodo이를 추가 하면 한 **$filter** 쿼리 문자열 매개 변수가 있는 **eq** 연산자 tooyour iFrame src url과 hello 필터를 지정 합니다. Hello 필터 쿼리 구문은 다음과 같습니다.

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName}은(는) 공백이나 특수 문자를 포함할 수 없습니다. hello {fieldValue}에 하나의 범주 값을 허용합니다.  

## <a name="see-also"></a>참고 항목

[일반적인 Microsoft Power BI Embedded 시나리오](power-bi-embedded-scenarios.md)  
[Power BI Embedded에서 인증 및 권한 부여](power-bi-embedded-app-token-flow.md)  
[보고서 포함](power-bi-embedded-embed-report.md)  
[데이터 집합에서 새 보고서 만들기](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Embed 샘플](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
궁금한 점이 더 있나요? [Power BI 커뮤니티 hello를 시도 하십시오.](http://community.powerbi.com/)
