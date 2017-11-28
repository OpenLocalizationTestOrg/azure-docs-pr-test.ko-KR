---
title: "Azure Application Insights에서 tooSQL 내보내기 | Microsoft Docs"
description: "Application Insights 데이터 tooSQL Stream Analytics을 사용 하 여 지속적으로 내보냅니다."
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
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="de929-103">연습: 스트림 분석을 사용 하 여 Application Insights에서 tooSQL 내보내기</span><span class="sxs-lookup"><span data-stu-id="de929-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="de929-104">이 문서에서는 어떻게 toomove에서 원격 분석 데이터 [Azure Application Insights] [ start] 를 사용 하 여 Azure SQL 데이터베이스로 [연속 내보내기가] [ export] 및 [Azure 스트림 분석](https://azure.microsoft.com/services/stream-analytics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="de929-105">연속 내보내기는 원격 분석 데이터를 JSON 형식으로 Azure 저장소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="de929-106">Azure 스트림 분석을 사용 하 여 hello JSON 개체를 구문 분석 알아보고 데이터베이스 테이블의 행을 만들 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="de929-107">(보다 일반적으로 hello 방식으로 toodo은 연속 내보내기가 hello 원격 분석 분석 앱 tooApplication Insights 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="de929-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="de929-108">수를 조정이 코드 샘플 toodo 메커니즘과 된 데이터의 집계 등의 내보낸 hello 원격 분석.)</span><span class="sxs-lookup"><span data-stu-id="de929-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="de929-109">원하는 toomonitor hello 앱이 이미 있는 hello 가정부터 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="de929-110">이 예제에서는 hello 페이지 보기 데이터를 사용 합니다 하지만 hello 동일한 패턴 쉽게 확장할 수 있습니다 사용자 지정 이벤트 및 예외와 같은 tooother 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="de929-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="de929-111">Application Insights tooyour 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="de929-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="de929-112">tooget 시작:</span><span class="sxs-lookup"><span data-stu-id="de929-112">tooget started:</span></span>

1. <span data-ttu-id="de929-113">[웹 페이지용 Application Insights를 설치합니다](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="de929-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="de929-114">(이 예제에서는 집중적으로 살펴봅니다 hello 클라이언트 브라우저에서 페이지 보기 데이터를 처리 하지만의 hello 서버 측에 대 한 Application Insights를도 설정할 수 있습니다 프로그램 [Java](app-insights-java-get-started.md) 또는 [ASP.NET](app-insights-asp-net.md) 응용 프로그램 및 프로세스 요청 종속성 및 기타 서버 원격 분석.)</span><span class="sxs-lookup"><span data-stu-id="de929-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="de929-115">앱을 게시하고 Application Insights 리소스에 표시되는 원격 분석 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="de929-116">Azure에서 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="de929-116">Create storage in Azure</span></span>
<span data-ttu-id="de929-117">연속 내보내기를 먼저 toocreate hello 저장소가 필요 하므로 항상 데이터 tooan Azure 저장소 계정을 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="de929-118">Hello에 구독에서 저장소 계정을 만드는 [Azure 포털][portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![Azure 포털에서 새로 만들기, 데이터, 저장소를 선택합니다.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="de929-122">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="de929-122">Create a container</span></span>
   
    ![Hello 새 저장소를 선택 하세요.를 hello 컨테이너 타일 및 추가 클릭 합니다.](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="de929-124">Hello 저장소 액세스 키를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="de929-125">해야 곧 tooset hello 입력된 toohello 스트림 분석 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Hello 저장소에서 설정, 키를 열고 hello 기본 액세스 키의 복사본](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="de929-127">연속 내보내기를 tooAzure 저장소 시작</span><span class="sxs-lookup"><span data-stu-id="de929-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="de929-128">Hello Azure 포털에서에서 응용 프로그램에 대해 만든 toohello Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![찾아보기, Application Insights, 응용 프로그램 선택](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="de929-130">연속 내보내기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="de929-130">Create a continuous export.</span></span>
   
    ![설정, 연속 내보내기, 추가를 차례로 선택](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="de929-132">이전에 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-132">Select hello storage account you created earlier:</span></span>

    ![Hello 내보내기 대상을 설정합니다](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="de929-134">Toosee 원하는 hello 이벤트 유형을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-134">Set hello event types you want toosee:</span></span>

    ![이벤트 유형 선택](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="de929-136">일부 데이터가 누적되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-136">Let some data accumulate.</span></span> <span data-ttu-id="de929-137">한동안 사용자가 응용 프로그램을 사용하도록 놓아둡니다.</span><span class="sxs-lookup"><span data-stu-id="de929-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="de929-138">원격 분석이 제공되어 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 통계 차트가, [진단 검색](app-insights-diagnostic-search.md)에서 개별 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="de929-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="de929-139">및 또한 hello 데이터는 tooyour 저장소를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="de929-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="de929-140">Hello 포털에서 hello 내보낸 데이터를 검사-선택 **찾아보기**, 저장소 계정을 선택 하 고 다음 **컨테이너** -또는 Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="de929-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="de929-141">Visual Studio에서 **보기/클라우드 탐색기**를 선택하고 Azure/저장소를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="de929-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="de929-142">(Tooinstall hello Azure SDK이 메뉴 옵션에 없을 경우 해야: hello 새 프로젝트 대화 상자를 열고 엽니다 Visual C# / 클라우드 / Microsoft Azure SDK for.NET 가져오기.)</span><span class="sxs-lookup"><span data-stu-id="de929-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Visual Studio에서 서버 브라우저, Azure, 저장소 열기](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="de929-144">Hello 응용 프로그램 이름 및 계측 키에서 파생 된 hello 경로 이름의 hello 공통 부분을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de929-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="de929-145">hello 이벤트는 JSON 형식의 tooblob 파일 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de929-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="de929-146">각 파일에는 하나 이상의 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-146">Each file may contain one or more events.</span></span> <span data-ttu-id="de929-147">따라서 싶습니다 tooread hello 이벤트 데이터와 원하는 hello 필드를 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="de929-148">모든 종류의 hello 데이터로 수행 하는 항목이 없지만 현재 계획으로 오늘 toouse 스트림 분석 toomove hello 데이터 tooa SQL 데이터베이스는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="de929-149">하면 더욱 쉽게 toorun 다양 한 흥미로운 쿼리.</span><span class="sxs-lookup"><span data-stu-id="de929-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="de929-150">Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="de929-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="de929-151">다시 한 번에 구독에서 시작 [Azure 포털][portal], hello 데이터베이스 만들기 (및 새 서버 경우를 제외 하면 이미 하나) toowhich hello 데이터를 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![새로 만들기, 데이터, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="de929-153">Hello 데이터베이스 서버를 tooAzure 서비스 액세스를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-153">Make sure that hello database server allows access tooAzure services:</span></span>

![찾아보기, 서버, 서버, 설정, 방화벽, tooAzure 액세스 허용](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="de929-155">Azure SQL DB에 테이블 만들기</span><span class="sxs-lookup"><span data-stu-id="de929-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="de929-156">기본 설정된 관리 도구와 hello 이전 섹션에서 만든 toohello 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="de929-157">이 연습에서는 SSMS( [SQL Server 관리 도구](https://msdn.microsoft.com/ms174173.aspx) )를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="de929-158">새 쿼리를 만들고 hello 다음 T-SQL을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-158">Create a new query, and execute hello following T-SQL:</span></span>

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

<span data-ttu-id="de929-159">이 샘플에서 페이지 보기에서 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="de929-160">toosee hello 사용할 수 있는 다른 데이터를 검사 하 여 JSON 출력을 hello 확인할 [데이터 모델을 내보낼](app-insights-export-data-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="de929-161">Azure 스트림 분석 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="de929-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="de929-162">Hello에서 [클래식 Azure 포털](https://manage.windowsazure.com/)hello Azure 스트림 분석 서비스를 선택 하 고 새 스트림 분석 작업 만들기:</span><span class="sxs-lookup"><span data-stu-id="de929-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="de929-163">Hello 새 작업을 만든 경우 해당 세부 정보를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="de929-164">Blob 위치 설정</span><span class="sxs-lookup"><span data-stu-id="de929-164">Set blob location</span></span>
<span data-ttu-id="de929-165">연속 내보내기 blob의 tootake 입력으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="de929-166">이제 기본 액세스 키 hello 앞에서 기록해 둔 저장소 계정에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="de929-167">저장소 계정 키 hello로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="de929-168">경로 접두사 패턴 설정</span><span class="sxs-lookup"><span data-stu-id="de929-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="de929-169">너무 있는지 tooset hello 날짜 형식 수**YYYY-월-일** (으로 **대시**).</span><span class="sxs-lookup"><span data-stu-id="de929-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="de929-170">경로 접두사 패턴 hello 스트림 분석 hello 저장소에 hello 입력된 파일을 찾는 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="de929-171">Tooset 필요한 것 연속 내보내기가 toocorrespond toohow hello 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="de929-172">다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="de929-173">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="de929-173">In this example:</span></span>

* <span data-ttu-id="de929-174">`webapplication27`hello Application Insights 리소스의 hello 이름인 **소문자 모두에**합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="de929-175">`1234...`hello Application Insights 리소스의 계측 키 hello **대시 제거 된**합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="de929-176">`PageViews`hello 형식이 tooanalyze 원하는 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="de929-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="de929-177">연속 내보내기에서 설정한 hello 필터에 대 한 hello 사용 가능한 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="de929-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="de929-178">사용 가능한 다른 유형 hello 내보낸된 데이터 toosee hello를 검사 하 고 hello 참조 [데이터 모델을 내보낼](app-insights-export-data-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="de929-179">`/{date}/{time}` 은 문자로 기록된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="de929-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="de929-180">tooget hello 이름 및 Application Insights 리소스를 iKey Essentials의 개요 페이지에서 또는 설정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="de929-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="de929-181">초기 설치 완료</span><span class="sxs-lookup"><span data-stu-id="de929-181">Finish initial setup</span></span>
<span data-ttu-id="de929-182">Hello 직렬화 형식을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-182">Confirm hello serialization format:</span></span>

![마법사 확인 후 닫기](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="de929-184">Hello 마법사를 닫고 설치 프로그램 toocomplete hello에 대 한 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="de929-185">Hello 샘플 함수 toocheck hello 입력된 경로 올바르게 설정 했는지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="de929-186">실패할 경우: hello 샘플 시간 범위 동안 선택한 hello 저장소의 데이터 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="de929-187">Hello 입력된 정의 편집 하 고 hello 저장소 계정에 경로 접두사를 설정 하 고 날짜 형식에 올바르게를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="de929-188">쿼리 설정</span><span class="sxs-lookup"><span data-stu-id="de929-188">Set query</span></span>
<span data-ttu-id="de929-189">Hello 쿼리 섹션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="de929-189">Open hello query section:</span></span>

![스트림 분석에서 쿼리 선택](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="de929-191">Hello 기본 쿼리를를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="de929-191">Replace hello default query with:</span></span>

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

<span data-ttu-id="de929-192">hello 처음 몇 가지 속성은 특정 toopage 뷰 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="de929-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="de929-193">다른 원격 분석 유형 내보내기에 다른 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="de929-194">Hello 참조 [hello 속성 형식 및 값에 대 한 데이터 모델 참조를 자세히 설명 합니다.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="de929-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="de929-195">출력 toodatabase 설정</span><span class="sxs-lookup"><span data-stu-id="de929-195">Set up output toodatabase</span></span>
<span data-ttu-id="de929-196">SQL hello 출력으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-196">Select SQL as hello output.</span></span>

![스트림 분석에서 출력 선택](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="de929-198">Hello SQL 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-198">Specify hello SQL database.</span></span>

![데이터베이스의 hello 세부 사항을 입력합니다](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="de929-200">Hello 마법사를 닫고 hello 출력 설정 되는 알림을 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="de929-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="de929-201">처리 시작</span><span class="sxs-lookup"><span data-stu-id="de929-201">Start processing</span></span>
<span data-ttu-id="de929-202">Hello 작업 모음에서 hello 작업을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-202">Start hello job from hello action bar:</span></span>

![스트림 분석에서 시작 클릭](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="de929-204">Toostart 처리 hello 데이터에서 지금 또는 이전 데이터와 함께 toostart 시작 여부를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de929-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="de929-205">후자의 hello 잠시 동안 이미 실행 되 고 연속 내보내기가 완료 하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![스트림 분석에서 시작 클릭](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="de929-207">몇 분 후 tooSQL 서버 관리 도구 돌아가서 hello 데이터 흐름에 시청 하십시오.</span><span class="sxs-lookup"><span data-stu-id="de929-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="de929-208">예를 들어 다음과 같은 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="de929-209">관련 문서</span><span class="sxs-lookup"><span data-stu-id="de929-209">Related articles</span></span>
* [<span data-ttu-id="de929-210">스트림 분석을 사용 하 여 내보내기 tooPowerBI</span><span class="sxs-lookup"><span data-stu-id="de929-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="de929-211">세부 데이터는 hello 속성 형식 및 값에 대 한 참조를 모델링합니다.</span><span class="sxs-lookup"><span data-stu-id="de929-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="de929-212">Application Insights에서 연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="de929-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="de929-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="de929-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

