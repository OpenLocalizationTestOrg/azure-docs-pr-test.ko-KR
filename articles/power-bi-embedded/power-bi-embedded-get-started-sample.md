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
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="7fdae-103">Power BI Embedded 시작 샘플</span><span class="sxs-lookup"><span data-stu-id="7fdae-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="7fdae-104">**Microsoft Power BI Embedded**를 사용하면 Power BI 보고서를 웹 또는 모바일 응용 프로그램에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="7fdae-105">이 문서에서는 합니다 소개 toohello **Power BI 포함** get 시작된 샘플.</span><span class="sxs-lookup"><span data-stu-id="7fdae-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="7fdae-106">본론, 전에는 다음 리소스 toosave hello를 설치할 좋을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="7fdae-107">너무 hello 샘플 응용 프로그램 및 앱에 Power BI 보고서 통합 때 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="7fdae-108">샘플 작업 영역 웹앱</span><span class="sxs-lookup"><span data-stu-id="7fdae-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="7fdae-109">Power BI Embedded API 참조</span><span class="sxs-lookup"><span data-stu-id="7fdae-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="7fdae-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet을 통해 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="7fdae-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="7fdae-111">JavaScript Report Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="7fdae-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="7fdae-112">Toocreate 하나 이상 실행된 hello Power BI 포함 가져오기 샘플을 시작 및 구성할 수 있습니다, 전에 해야 **작업 영역 컬렉션** Azure 구독에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="7fdae-113">toolearn 어떻게 toocreate는 **작업 영역 컬렉션** hello Azure 포털에서에서 볼 [Power BI embedded 시작](power-bi-embedded-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="7fdae-114">Hello 샘플 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="7fdae-114">Configure hello sample app</span></span>

<span data-ttu-id="7fdae-115">Visual Studio 개발 환경 tooaccess hello 구성 요소가 필요한 toorun hello 샘플 앱을 설정 하는 과정을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="7fdae-116">다운로드 하 고 hello 압축을 풀면 [Power BI 포함-웹 응용 프로그램에 보고서 통합](http://go.microsoft.com/fwlink/?LinkId=761493) GitHub의 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="7fdae-117">Visual Studio에서 **PowerBI-embedded.sln** 을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="7fdae-118">Tooexecute hello 야 **업데이트 패키지** hello이이 솔루션에서 사용 되는 순서 tooupdate hello 패키지에서 NuGET 패키지 관리자 콘솔에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="7fdae-119">Hello 솔루션을 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="7fdae-119">Build hello solution.</span></span>
4. <span data-ttu-id="7fdae-120">Hello 실행 **ProvisionSample** 콘솔 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="7fdae-121">Hello 샘플 콘솔 응용 프로그램에서 작업 영역을 프로 비전 하 고 PBIX 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="7fdae-122">새 tooprovision **작업 영역**, 1, 옵션을 선택 **컬렉션 관리**, 다음 6 옵션을 선택 하 고 **새 작업 영역을 프로 비전**</span><span class="sxs-lookup"><span data-stu-id="7fdae-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="7fdae-123">새 tooimport **보고서**, 2, 옵션을 선택 **관리 보고서**, 선택한 후 옵션 3, **가져오기 PBIX 데스크톱 파일을 작업 영역으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="7fdae-124">**작업 영역 컬렉션** 이름 및 **선택키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="7fdae-125">Hello에서 얻을 수 있습니다 **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="7fdae-126">toolearn 방법에 대 한 자세한 tooget 프로그램 **선택 키**, 참조 [Power BI API 액세스 키 보기](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) 에서 Microsoft Power BI embedded 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="7fdae-127">복사 하 고 새로 만든 hello 저장 **작업 영역 ID** 이 문서의 뒷부분에 나오는 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="7fdae-128">Hello 후 **작업 영역 ID** 가 만들어지면를 찾을 수 있습니다 hello **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="7fdae-129">tooimport PBIX 파일을으로 프로그램 **작업 영역**, 옵션을 선택 **6입니다. 기존 작업 영역**에 PBIX Desktop 파일을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="7fdae-130">Hello를 다운로드할 수 파일 편리한 PBIX를 설정 하지 않은 경우 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="7fdae-131">메시지가 표시되면 **데이터 집합**의 식별 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="7fdae-132">다음과 같은 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="7fdae-133">PBIX 파일에 직접 쿼리 연결을 있으면 옵션 7 tooupdate hello 연결 문자열을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="7fdae-134">이제 Power BI PBIX 보고서를 **작업 영역**에 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="7fdae-135">이제는 방법에 살펴보겠습니다 toorun hello **Power BI 포함** 시작된 샘플 웹 응용 프로그램을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="7fdae-136">Hello 샘플 웹 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="7fdae-136">Run hello sample web app</span></span>
<span data-ttu-id="7fdae-137">웹 앱 샘플 hello로 가져올 보고서를 렌더링 하는 샘플 응용 프로그램은 프로그램 **작업 영역**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="7fdae-138">어떻게 tooconfigure hello 웹 앱 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="7fdae-139">Hello에 **PowerBI 포함** Visual Studio 솔루션을 오른쪽 클릭 hello **EmbedSample** 웹 응용 프로그램을 선택 하 고 **시작 프로젝트로 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="7fdae-140">**web.config**, hello에 **EmbedSample** 웹 응용 프로그램을 편집 hello **appSettings**: **AccessKey**,  **WorkspaceCollection** 이름 및 **WorkspaceId**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="7fdae-141">Hello 실행 **EmbedSample** 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="7fdae-142">실행 된 hello **EmbedSample** 웹 응용 프로그램에서는 hello 왼쪽된 탐색 패널 있어야는 **보고서** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="7fdae-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="7fdae-143">확장을 가져온 tooview hello 보고서 **보고서**, 보고서를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="7fdae-144">Hello를 가져온 경우 [소매 분석 샘플 PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello 샘플 웹 응용 프로그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="7fdae-145">보고서를 클릭 한 후 hello **EmbedSample** 웹 응용 프로그램 같아야이:</span><span class="sxs-lookup"><span data-stu-id="7fdae-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="7fdae-146">Hello 샘플 코드 탐색</span><span class="sxs-lookup"><span data-stu-id="7fdae-146">Explore hello sample code</span></span>

<span data-ttu-id="7fdae-147">hello **Microsoft Power BI Embedded** 샘플 표시 하는 예제 웹 응용 프로그램은 toointegrate **Power BI** 앱에는 보고서입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="7fdae-148">모델-뷰-컨트롤러 (MVC)을 사용 하 여 패턴 toodemonstrate에 대 한 유용한 정보를 디자인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="7fdae-149">이 섹션에서는 hello 내에서 탐색할 수 있는 hello 샘플 코드의 일부를 요약 **PowerBI 포함** 웹 응용 프로그램 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="7fdae-150">hello 모델-뷰-컨트롤러 (MVC) 패턴을 구분 hello 도메인, hello 프레젠테이션 및 세 가지 별도 클래스에 대 한 사용자 입력에 따라 hello 동작의 hello 모델링: 모델, 뷰 및 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="7fdae-151">MVC에 대해 자세히 toolearn 참조 [ASP.NET에 대 한 자세한 내용은](http://www.asp.net/mvc)합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="7fdae-152">hello **Microsoft Power BI Embedded** 샘플 코드는 다음과 같이 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="7fdae-153">각 섹션에 hello 파일 이름을 hello PowerBI embedded.sln 솔루션 hello 샘플에서 hello 코드를 쉽게 찾을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7fdae-154">이 섹션은 요약 hello 코드를 작성 하는 방법을 보여 주는 hello 샘플 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="7fdae-155">전체 tooview hello 샘플, Visual Studio에서 PowerBI embedded.sln hello 솔루션을 로드 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7fdae-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="7fdae-156">모델</span><span class="sxs-lookup"><span data-stu-id="7fdae-156">Model</span></span>

<span data-ttu-id="7fdae-157">hello 샘플에는 **ReportsViewModel** 및 **ReportViewModel**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="7fdae-158">**ReportsViewModel.cs**: 여러 Power BI 보고서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="7fdae-159">**ReportViewModel.cs**: 하나의 Power BI 보고서를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="7fdae-160">연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7fdae-160">Connection string</span></span>

<span data-ttu-id="7fdae-161">형식에 따라 hello hello 연결 문자열 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="7fdae-162">일반적인 서버 및 데이터베이스 특성을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="7fdae-163">예: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="7fdae-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="7fdae-164">보기</span><span class="sxs-lookup"><span data-stu-id="7fdae-164">View</span></span>

<span data-ttu-id="7fdae-165">hello **보기** Power BI의 hello 표시를 관리 **보고서** 및 Power BI **보고서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="7fdae-166">**Reports.cshtml**: 반복 **Model.Reports** toocreate는 **ActionLink**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="7fdae-167">hello **ActionLink** 다음과 같이 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="7fdae-168">부</span><span class="sxs-lookup"><span data-stu-id="7fdae-168">Part</span></span> | <span data-ttu-id="7fdae-169">설명</span><span class="sxs-lookup"><span data-stu-id="7fdae-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7fdae-170">제목</span><span class="sxs-lookup"><span data-stu-id="7fdae-170">Title</span></span> |<span data-ttu-id="7fdae-171">Hello 보고서의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-171">Name of hello Report.</span></span> |
| <span data-ttu-id="7fdae-172">QueryString</span><span class="sxs-lookup"><span data-stu-id="7fdae-172">QueryString</span></span> |<span data-ttu-id="7fdae-173">링크 toohello 보고서 id입니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-173">A link toohello Report ID.</span></span> |

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

<span data-ttu-id="7fdae-174">Report.cshtml: hello 설정 **Model.AccessToken**, 람다 식에 대 한 hello 및 **PowerBIReportFor**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="7fdae-175">Controller</span><span class="sxs-lookup"><span data-stu-id="7fdae-175">Controller</span></span>

<span data-ttu-id="7fdae-176">**DashboardController.cs**: **앱 토큰**을 전달하는 PowerBIClient를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="7fdae-177">JSON 웹 토큰 (JWT) hello에서 만들어집니다. **서명 키** tooget hello **자격 증명**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="7fdae-178">hello **자격 증명** 사용된 toocreate의 인스턴스는 **PowerBIClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="7fdae-179">**PowerBIClient** 인스턴스가 작성되면 GetReports() 및 GetReportsAsync()를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="7fdae-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="7fdae-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="7fdae-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="7fdae-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="7fdae-182">작업<ActionResult> 보고서(문자열 reportId)</span><span class="sxs-lookup"><span data-stu-id="7fdae-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="7fdae-183">앱에 보고서 통합</span><span class="sxs-lookup"><span data-stu-id="7fdae-183">Integrate a report into your app</span></span>

<span data-ttu-id="7fdae-184">있으면는 **보고서**를 사용 하면 프로그램 **IFrame** tooembed hello Power BI **보고서**합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="7fdae-185">다음은 hello에 powerbi.js에서 코드 조각 **Microsoft Power BI Embedded** 샘플.</span><span class="sxs-lookup"><span data-stu-id="7fdae-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="7fdae-186">응용 프로그램에 포함된 보고서 필터링</span><span class="sxs-lookup"><span data-stu-id="7fdae-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="7fdae-187">URL 구문을 사용하여 포함된 보고서를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="7fdae-188">toodo이를 추가 하면 한 **$filter** 쿼리 문자열 매개 변수가 있는 **eq** 연산자 tooyour iFrame src url과 hello 필터를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="7fdae-189">Hello 필터 쿼리 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="7fdae-190">{tableName/fieldName}은(는) 공백이나 특수 문자를 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="7fdae-191">hello {fieldValue}에 하나의 범주 값을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="7fdae-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="7fdae-192">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7fdae-192">See also</span></span>

[<span data-ttu-id="7fdae-193">일반적인 Microsoft Power BI Embedded 시나리오</span><span class="sxs-lookup"><span data-stu-id="7fdae-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="7fdae-194">Power BI Embedded에서 인증 및 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7fdae-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="7fdae-195">보고서 포함</span><span class="sxs-lookup"><span data-stu-id="7fdae-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="7fdae-196">데이터 집합에서 새 보고서 만들기</span><span class="sxs-lookup"><span data-stu-id="7fdae-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="7fdae-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7fdae-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="7fdae-198">JavaScript Embed 샘플</span><span class="sxs-lookup"><span data-stu-id="7fdae-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="7fdae-199">궁금한 점이 더 있나요?</span><span class="sxs-lookup"><span data-stu-id="7fdae-199">More questions?</span></span> [<span data-ttu-id="7fdae-200">Power BI 커뮤니티 hello를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7fdae-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
