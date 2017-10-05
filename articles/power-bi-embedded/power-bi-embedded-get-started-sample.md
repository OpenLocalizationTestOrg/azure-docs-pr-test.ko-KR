---
title: "샘플 시작"
description: "Power BI Embedded, SDK를 사용하여 대화형 Power BI 보고서를 비즈니스 인텔리전스 응용 프로그램에 추가"
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="eb9cc-103">Power BI Embedded 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="eb9cc-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="eb9cc-104">**Microsoft Power BI Embedded**를 사용하면 Power BI 보고서를 웹 또는 모바일 응용 프로그램에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="eb9cc-105">이 문서에서 **Power BI Embedded** 시작 샘플을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="eb9cc-106">진행하기 전에 다음 리소스를 저장하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="eb9cc-107">이렇게 하면 Power BI 보고서를 샘플 앱 및 사용자 앱에 통합할 때도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="eb9cc-108">샘플 작업 영역 웹앱</span><span class="sxs-lookup"><span data-stu-id="eb9cc-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="eb9cc-109">Power BI Embedded API 참조</span><span class="sxs-lookup"><span data-stu-id="eb9cc-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="eb9cc-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet을 통해 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="eb9cc-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="eb9cc-111">JavaScript Report Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="eb9cc-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="eb9cc-112">Power BI Embedded 시작 샘플을 구성하고 실행하려면 먼저 Azure 구독에 적어도 하나의 **작업 영역 컬렉션** 을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="eb9cc-113">Azure 포털에 **작업 영역 컬렉션** 을 만드는 방법을 알아보려면 [Power BI Embedded 시작](power-bi-embedded-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="eb9cc-114">샘플 앱 구성</span><span class="sxs-lookup"><span data-stu-id="eb9cc-114">Configure the sample app</span></span>

<span data-ttu-id="eb9cc-115">샘플 앱을 실행하는 데 필요한 구성 요소에 액세스할 Visual Studio 개발 환경을 설정하는 방법을 단계적으로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="eb9cc-116">[Power BI Embedded - 보고서를 웹앱으로 통합](http://go.microsoft.com/fwlink/?LinkId=761493) 샘플을 GitHub에서 다운로드하여 압축을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="eb9cc-117">Visual Studio에서 **PowerBI-embedded.sln** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="eb9cc-118">이 솔루션에서 사용되는 패키지를 업데이트하려면 NuGET 패키지 관리자 콘솔에서 **Update-Package** 명령을 실행해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="eb9cc-119">솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-119">Build the solution.</span></span>
4. <span data-ttu-id="eb9cc-120">**ProvisionSample** 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="eb9cc-121">샘플 콘솔 앱에서 작업 영역을 프로비전하고 PBIX 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="eb9cc-122">새 **작업 영역**을 프로비전하려면 옵션 1 **컬렉션 관리**를 선택한 다음 옵션 6 **새 작업 영역 프로비전**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="eb9cc-123">새 **보고서**를 가져오려면 옵션 2 **관리 보고**를 선택한 다음, 옵션 3 **PBIX 데스크톱 파일을 작업 영역에 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="eb9cc-124">**작업 영역 컬렉션** 이름 및 **선택키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="eb9cc-125">**Azure 포털**에서 이러한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="eb9cc-126">**선택키**를 가져오는 방법에 대해 알아보려면 Microsoft Power BI Embedded 시작의 [Power BI API 선택키 보기](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="eb9cc-127">이 문서의 뒷부분에서 사용할 수 있도록 새로 만든 **작업 영역 ID** 를 복사하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="eb9cc-128">**작업 영역 ID**는 **Azure Portal**에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="eb9cc-129">PBIX 파일을 **작업 영역**으로 가져오려면 옵션 **6, 기존 작업 영역**에 PBIX Desktop 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="eb9cc-130">사용할 수 있는 PBIX 파일이 없는 경우 [소매점 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="eb9cc-131">메시지가 표시되면 **데이터 집합**의 식별 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="eb9cc-132">다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="eb9cc-133">PBIX 파일에 직접 쿼리 연결이 포함되어 있는 경우 연결 문자열을 업데이트하도록 옵션 7을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="eb9cc-134">이제 Power BI PBIX 보고서를 **작업 영역**에 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="eb9cc-135">다음으로는 **Power BI Embedded** 시작 샘플 웹앱을 실행하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="eb9cc-136">샘플 웹앱 실행</span><span class="sxs-lookup"><span data-stu-id="eb9cc-136">Run the sample web app</span></span>
<span data-ttu-id="eb9cc-137">웹앱 샘플은 **작업 영역**으로 가져온 보고서를 렌더링하는 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="eb9cc-138">웹앱 샘플을 구성하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="eb9cc-139">**PowerBI-embedded** Visual Studio 솔루션에서 **EmbedSample** 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="eb9cc-140">**web.config**의 **EmbedSample** 웹 응용 프로그램에서 **appSettings**, 즉 **AccessKey**, **WorkspaceCollection** 이름 및 **WorkspaceId**를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="eb9cc-141">**EmbedSample** 웹 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="eb9cc-142">**EmbedSample** 웹 응용 프로그램을 실행하면 왼쪽 탐색 패널에 **보고서** 메뉴가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="eb9cc-143">가져온 보고서를 보려면 **보고서**를 확장하고 보고서를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="eb9cc-144">[소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)를 가져온 경우 샘플 웹앱이 다음과 같이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="eb9cc-145">보고서를 클릭하면 **EmbedSample** 웹 응용 프로그램이 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="eb9cc-146">샘플 코드 탐색</span><span class="sxs-lookup"><span data-stu-id="eb9cc-146">Explore the sample code</span></span>

<span data-ttu-id="eb9cc-147">**Microsoft Power BI Embedded** 샘플은 **Power BI** 보고서를 앱에 통합하는 방법을 보여주는 웹앱의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="eb9cc-148">MVC(Model-View-Controller) 디자인 패턴을 사용하여 모범 사례를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="eb9cc-149">이 섹션에서는 **PowerBI-embedded** 웹앱 솔루션 내에서 탐색할 수 있는 샘플 코드 부분을 중점적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="eb9cc-150">MVC(Model-View-Controller) 패턴은 도메인의 모델링, 프레젠테이션 및 작업을 사용자 입력에 따라 모델, 보기 및 제어의 세 가지 별도 클래스로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="eb9cc-151">MVC에 대한 알아보려면 [ASP.NET에 대해 알아보기](http://www.asp.net/mvc)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="eb9cc-152">**Microsoft Power BI Embedded** 샘플 코드는 다음과 같이 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="eb9cc-153">각 섹션에는 샘플 코드를 쉽게 찾을 수 있도록 PowerBI-embedded.sln 솔루션에 파일 이름이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="eb9cc-154">이 섹션에서는 코드가 작성된 방법을 보여 주는 샘플 코드에 대해 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="eb9cc-155">전체 샘플을 보려면 Visual Studio에서 PowerBI-embedded.sln을 로드하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="eb9cc-156">모델</span><span class="sxs-lookup"><span data-stu-id="eb9cc-156">Model</span></span>

<span data-ttu-id="eb9cc-157">이 샘플에는 **ReportsViewModel** 및 **ReportViewModel**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="eb9cc-158">**ReportsViewModel.cs**: 여러 Power BI 보고서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="eb9cc-159">**ReportViewModel.cs**: 하나의 Power BI 보고서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="eb9cc-160">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="eb9cc-160">Connection string</span></span>

<span data-ttu-id="eb9cc-161">연결 문자열은 다음 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="eb9cc-162">일반적인 서버 및 데이터베이스 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="eb9cc-163">예: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="eb9cc-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="eb9cc-164">보기</span><span class="sxs-lookup"><span data-stu-id="eb9cc-164">View</span></span>

<span data-ttu-id="eb9cc-165">**보기**를 통해 여러 Power BI **보고서** 및 하나의 Power BI **보고서** 표시를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="eb9cc-166">**Reports.cshtml**: **Model.Reports**를 반복하여 **ActionLink**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="eb9cc-167">**ActionLink**는 다음과 같이 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="eb9cc-168">부</span><span class="sxs-lookup"><span data-stu-id="eb9cc-168">Part</span></span> | <span data-ttu-id="eb9cc-169">설명</span><span class="sxs-lookup"><span data-stu-id="eb9cc-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb9cc-170">제목</span><span class="sxs-lookup"><span data-stu-id="eb9cc-170">Title</span></span> |<span data-ttu-id="eb9cc-171">보고서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-171">Name of the Report.</span></span> |
| <span data-ttu-id="eb9cc-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="eb9cc-172">QueryString</span></span> |<span data-ttu-id="eb9cc-173">보고서 ID에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="eb9cc-174">Report.cshtml: **Model.AccessToken** 및 **PowerBIReportFor**에 대한 람다 식을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="eb9cc-175">Controller</span><span class="sxs-lookup"><span data-stu-id="eb9cc-175">Controller</span></span>

<span data-ttu-id="eb9cc-176">**DashboardController.cs**: **앱 토큰**을 전달하는 PowerBIClient를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="eb9cc-177">**자격 증명**을 가져오기 위해 **서명 키**에서 JWT(JSON Web Token)가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="eb9cc-178">**자격 증명**은 **PowerBIClient** 인스턴스를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="eb9cc-179">**PowerBIClient** 인스턴스가 작성되면 GetReports() 및 GetReportsAsync()를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="eb9cc-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="eb9cc-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="eb9cc-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="eb9cc-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="eb9cc-182">작업<ActionResult> 보고서(문자열 reportId)</span><span class="sxs-lookup"><span data-stu-id="eb9cc-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="eb9cc-183">앱에 보고서 통합</span><span class="sxs-lookup"><span data-stu-id="eb9cc-183">Integrate a report into your app</span></span>

<span data-ttu-id="eb9cc-184">**보고서**를 만든 후에는 **IFrame**을 사용하여 Power BI **보고서**를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="eb9cc-185">다음은 **Microsoft Power BI Embedded** 샘플 내 powerbi.js의 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="eb9cc-186">응용 프로그램에 포함된 보고서 필터링</span><span class="sxs-lookup"><span data-stu-id="eb9cc-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="eb9cc-187">URL 구문을 사용하여 포함된 보고서를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="eb9cc-188">이렇게 하려면 지정된 필터를 사용하여 **eq** 연산자가 포함된 **$filter** 쿼리 문자열 매개 변수를 iFrame src url에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="eb9cc-189">필터 쿼리 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="eb9cc-190">{tableName/fieldName}은(는) 공백이나 특수 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="eb9cc-191">{fieldValue}은(는) 단일 범주 값을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="eb9cc-192">참고 항목</span><span class="sxs-lookup"><span data-stu-id="eb9cc-192">See also</span></span>

[<span data-ttu-id="eb9cc-193">일반적인 Microsoft Power BI Embedded 시나리오</span><span class="sxs-lookup"><span data-stu-id="eb9cc-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="eb9cc-194">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="eb9cc-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="eb9cc-195">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="eb9cc-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="eb9cc-196">데이터 집합에서 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="eb9cc-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="eb9cc-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="eb9cc-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="eb9cc-198">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="eb9cc-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="eb9cc-199">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="eb9cc-199">More questions?</span></span> [<span data-ttu-id="eb9cc-200">Power BI 커뮤니티를 이용하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
