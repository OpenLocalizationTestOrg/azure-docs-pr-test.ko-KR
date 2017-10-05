---
title: "Azure Application Insights에서 SQL로 내보내기 | Microsoft Docs"
description: "스트림 분석을 사용하여 Application Insights 데이터를 SQL로 계속 내보냅니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="d9da2-103">연습: 스트림 분석을 사용하여 Application Insights에서 SQL로 내보내기</span><span class="sxs-lookup"><span data-stu-id="d9da2-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="d9da2-104">이 문서에서는 [연속 내보내기][export] 및 [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)을 사용하여 [Azure Application Insights][start]에서 Azure SQL Database로 원격 분석 데이터를 이동하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="d9da2-105">연속 내보내기는 원격 분석 데이터를 JSON 형식으로 Azure 저장소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="d9da2-106">Azure 스트림 분석을 사용하여 JSON 개체를 구문 분석하고 데이터베이스 테이블에 행을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="d9da2-107">보다 일반적으로 말하자면, 연속 내보내기는 앱에서 Application Insights에 보내는 원격 분석을 자체적으로 분석하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="d9da2-108">데이터 집계와 같은 원격 분석을 사용하여 이 코드 샘플이 기타 작업을 수행하도록 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="d9da2-109">모니터링하려는 앱이 이미 있다고 가정하고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="d9da2-110">이 예제에서는 페이지 보기 데이터를 사용하지만, 동일한 패턴을 사용자 지정 이벤트 및 예외와 같은 다른 데이터 형식으로 쉽게 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="d9da2-111">응용 프로그램에 Application Insights 추가</span><span class="sxs-lookup"><span data-stu-id="d9da2-111">Add Application Insights to your application</span></span>
<span data-ttu-id="d9da2-112">시작하기:</span><span class="sxs-lookup"><span data-stu-id="d9da2-112">To get started:</span></span>

1. <span data-ttu-id="d9da2-113">[웹 페이지용 Application Insights를 설치합니다](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="d9da2-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="d9da2-114">(이 예제에서는 클라이언트 브라우저에서 페이지 보기 데이터를 처리하는 데 초점을 두었지만 [Java](app-insights-java-get-started.md) 또는 [ASP.NET](app-insights-asp-net.md) 앱의 서버 쪽에 대한 Application Insights, 프로세스 요청, 종속성 및 기타 서버 원격 분석도 설정할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="d9da2-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="d9da2-115">앱을 게시하고 Application Insights 리소스에 표시되는 원격 분석 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="d9da2-116">Azure에서 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="d9da2-116">Create storage in Azure</span></span>
<span data-ttu-id="d9da2-117">연속 내보내기는 항상 Azure 저장소 계정에 데이터를 출력하므로 저장소를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="d9da2-118">[Azure Portal][portal]에서 구독에 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![Azure 포털에서 새로 만들기, 데이터, 저장소를 선택합니다.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="d9da2-122">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d9da2-122">Create a container</span></span>
   
    ![새 저장소에서 컨테이너를 선택하고 컨테이너 타일, 추가를 차례로 클릭합니다.](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="d9da2-124">저장소 액세스 키 복사</span><span class="sxs-lookup"><span data-stu-id="d9da2-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="d9da2-125">스트림 분석 서비스에 대한 입력을 설정하려면 곧 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![저장소에서 설정, 키를 열고 기본 액세스 키 복사](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="d9da2-127">Azure 저장소로 연속 내보내기 시작</span><span class="sxs-lookup"><span data-stu-id="d9da2-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="d9da2-128">Azure 포털에서 응용 프로그램에 대해 만든 Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![찾아보기, Application Insights, 응용 프로그램 선택](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="d9da2-130">연속 내보내기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-130">Create a continuous export.</span></span>
   
    ![설정, 연속 내보내기, 추가를 차례로 선택](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="d9da2-132">이전에 만든 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-132">Select the storage account you created earlier:</span></span>

    ![내보내기 대상 설정](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="d9da2-134">보려는 이벤트 유형을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-134">Set the event types you want to see:</span></span>

    ![이벤트 유형 선택](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="d9da2-136">일부 데이터가 누적되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-136">Let some data accumulate.</span></span> <span data-ttu-id="d9da2-137">한동안 사용자가 응용 프로그램을 사용하도록 놓아둡니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="d9da2-138">원격 분석이 제공되어 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 통계 차트가, [진단 검색](app-insights-diagnostic-search.md)에서 개별 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="d9da2-139">또한 데이터를 저장소로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="d9da2-140">포털 또는 Visual Studio에서 내보낸 데이터를 검사합니다. 포털에서 **찾아보기**, 저장소 계정을 선택한 다음 **컨테이너**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="d9da2-141">Visual Studio에서 **보기/클라우드 탐색기**를 선택하고 Azure/저장소를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="d9da2-142">이 메뉴 옵션이 없는 경우 Azure SDK를 설치해야 합니다. 새 프로젝트 대화 상자를 열고 Visual C#/클라우드/Microsoft Azure SDK for .NET 가져오기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Visual Studio에서 서버 브라우저, Azure, 저장소 열기](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="d9da2-144">응용 프로그램 이름 및 계측 키에서 파생된 경로 이름의 공통 부분을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="d9da2-145">이벤트는 JSON 형식으로 blob 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="d9da2-146">각 파일에는 하나 이상의 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-146">Each file may contain one or more events.</span></span> <span data-ttu-id="d9da2-147">따라서 이벤트 데이터를 읽고 원하는 필드를 필터링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="d9da2-148">데이터로 온갖 종류의 작업을 수행할 수 있지만, 지금은 스트림 분석을 사용하여 데이터를 SQL 데이터베이스로 이동하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="d9da2-149">이렇게 하면 흥미로운 많은 쿼리를 쉽게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="d9da2-150">Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="d9da2-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="d9da2-151">다시 한 번 [Azure Portal][portal]의 구독에서 시작하여 데이터를 작성할 데이터베이스(및 이미 있는 경우 새 서버)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![새로 만들기, 데이터, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="d9da2-153">데이터베이스 서버에서 Azure 서비스에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-153">Make sure that the database server allows access to Azure services:</span></span>

![찾아보기, 서버, 사용자 서버, 설정, 방화벽, Azure에 대한 액세스 허용](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="d9da2-155">Azure SQL DB에 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="d9da2-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="d9da2-156">기본 관리 도구로 이전 섹션에서 만든 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="d9da2-157">이 연습에서는 SSMS( [SQL Server 관리 도구](https://msdn.microsoft.com/ms174173.aspx) )를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="d9da2-158">새 쿼리를 만들고 다음 T-SQL을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-158">Create a new query, and execute the following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="d9da2-159">이 샘플에서 페이지 보기에서 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="d9da2-160">사용 가능한 다른 데이터를 보려면 JSON 출력을 검사하고 [데이터 모델 내보내기](app-insights-export-data-model.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="d9da2-161">Azure 스트림 분석 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="d9da2-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="d9da2-162">[클래식 Azure 포털](https://manage.windowsazure.com/)에서 Azure 스트림 분석 서비스를 선택하고 새 스트림 분석 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="d9da2-163">새 작업이 만들어지면 해당 세부 정보를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="d9da2-164">Blob 위치 설정</span><span class="sxs-lookup"><span data-stu-id="d9da2-164">Set blob location</span></span>
<span data-ttu-id="d9da2-165">연속 내보내기 Blob에서 입력을 가져오도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="d9da2-166">이제 앞에서 기록해 둔 저장소 계정의 기본 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="d9da2-167">이 키를 저장소 계정 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="d9da2-168">경로 접두사 패턴 설정</span><span class="sxs-lookup"><span data-stu-id="d9da2-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="d9da2-169">날짜 형식을 **YYYY-MM-DD**(**파선** 포함)로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="d9da2-170">경로 접두사 패턴은 스트림 분석이 저장소에서 입력 파일을 찾는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="d9da2-171">연속 내보내기에서 데이터를 저장하는 방법과 일치하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="d9da2-172">다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="d9da2-173">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="d9da2-173">In this example:</span></span>

* <span data-ttu-id="d9da2-174">`webapplication27` 은 Application Insights 리소스의 이름으로, **모두 소문자**입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="d9da2-175">`1234...` 은 **대시를 제거한**Application Insights 리소스의 계측 키입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="d9da2-176">`PageViews` 는 분석하려는 데이터의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="d9da2-177">사용 가능한 형식은 연속 내보내기에 설정한 필터에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="d9da2-178">내보낸 데이터를 검사하여 사용 가능한 다른 형식을 확인하고 [데이터 모델 내보내기](app-insights-export-data-model.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="d9da2-179">`/{date}/{time}` 은 문자로 기록된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="d9da2-180">Application Insights 리소스의 이름 및 iKey를 가져오려면 해당 개요 페이지에서 필수 항목을 열거나 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="d9da2-181">초기 설치 완료</span><span class="sxs-lookup"><span data-stu-id="d9da2-181">Finish initial setup</span></span>
<span data-ttu-id="d9da2-182">직렬화 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-182">Confirm the serialization format:</span></span>

![마법사 확인 후 닫기](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="d9da2-184">마법사를 닫고 설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="d9da2-185">샘플 함수를 사용하여 입력 경로가 올바르게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="d9da2-186">실패한 경우 선택한 샘플 시간 범위에 대한 저장소에 데이터가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="d9da2-187">입력 정의를 편집하고 저장소 계정, 경로 접두사 및 날짜 형식이 올바르게 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="d9da2-188">쿼리 설정</span><span class="sxs-lookup"><span data-stu-id="d9da2-188">Set query</span></span>
<span data-ttu-id="d9da2-189">쿼리 섹션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-189">Open the query section:</span></span>

![스트림 분석에서 쿼리 선택](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="d9da2-191">기본 쿼리를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-191">Replace the default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="d9da2-192">처음 몇 가지 속성은 페이지 보기 데이터에만 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="d9da2-193">다른 원격 분석 유형 내보내기에 다른 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="d9da2-194">[속성 형식 및 값에 대한 자세한 데이터 모델 참조](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="d9da2-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="d9da2-195">데이터베이스에 출력 설정</span><span class="sxs-lookup"><span data-stu-id="d9da2-195">Set up output to database</span></span>
<span data-ttu-id="d9da2-196">SQL을 출력으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-196">Select SQL as the output.</span></span>

![스트림 분석에서 출력 선택](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="d9da2-198">SQL 데이터베이스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-198">Specify the SQL database.</span></span>

![데이터베이스의 세부 정보 채우기](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="d9da2-200">마법사를 닫고 출력이 설정되었다는 알림이 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="d9da2-201">처리 시작</span><span class="sxs-lookup"><span data-stu-id="d9da2-201">Start processing</span></span>
<span data-ttu-id="d9da2-202">작업 모음에서 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-202">Start the job from the action bar:</span></span>

![스트림 분석에서 시작 클릭](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="d9da2-204">지금부터의 데이터를 처리할 것인지 아니면 이전 데이터부터 처리할 것인지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="d9da2-205">후자는 연속 내보내기를 이미 한동안 실행한 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![스트림 분석에서 시작 클릭](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="d9da2-207">몇 분 후에 SQL Server 관리 도구로 돌아가서 데이터 흐름을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="d9da2-208">예를 들어 다음과 같은 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="d9da2-209">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="d9da2-209">Related articles</span></span>
* [<span data-ttu-id="d9da2-210">스트림 분석을 사용하여 PowerBI로 내보내기</span><span class="sxs-lookup"><span data-stu-id="d9da2-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="d9da2-211">속성 형식 및 값에 대한 자세한 데이터 모델 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="d9da2-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="d9da2-212">Application Insights에서 연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="d9da2-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="d9da2-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d9da2-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

