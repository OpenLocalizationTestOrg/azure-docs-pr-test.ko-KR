---
title: "Azure Application Insights에서 Stream Analytics를 사용하여 내보내기 | Microsoft Docs"
description: "Stream Analytics를 사용하면 Application Insights에서 내보내는 데이터를 지속적으로 변환, 필터링 및 라우팅할 수 있습니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="e05f5-103">Stream Analytics를 사용하여 Application Insights에서 내보낸 데이터 처리</span><span class="sxs-lookup"><span data-stu-id="e05f5-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="e05f5-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/)는 [Application Insights에서 내보낸](app-insights-export-telemetry.md) 데이터를 처리하는 위한 이상적인 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="e05f5-105">Stream Analytics는 다양한 원본의 데이터를 가져와서</span><span class="sxs-lookup"><span data-stu-id="e05f5-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="e05f5-106">변환하고 필터링한 다음 다양한 싱크로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="e05f5-107">이 예제에서는 Application Insights에서 데이터를 가져오고, 필드 중 일부에 대해 이름을 바꾸고 처리하며, Power BI로 파이프하는 어댑터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="e05f5-108">[Power BI에서 Application Insights 데이터를 표시하는 데 권장되는 방법](app-insights-export-power-bi.md)이 있으며, 이 방법들은 훨씬 더 효율적이며 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="e05f5-109">여기서 설명하는 경로는 내보낸 데이터를 처리하는 방법을 보여 주기 위한 예로 사용했을 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![SA를 통해 PBI로 내보내기에 대한 블록 다이어그램](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="e05f5-111">Azure에서 저장소 만들기</span><span class="sxs-lookup"><span data-stu-id="e05f5-111">Create storage in Azure</span></span>
<span data-ttu-id="e05f5-112">연속 내보내기는 항상 Azure 저장소 계정에 데이터를 출력하므로 저장소를 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="e05f5-113">[Azure 포털](https://portal.azure.com)에서 구독에 "클래식" 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![Azure 포털에서 새로 만들기, 데이터, 저장소 선택](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="e05f5-115">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e05f5-115">Create a container</span></span>
   
    ![새 저장소에서 컨테이너를 선택하고 컨테이너 타일, 추가를 차례로 클릭합니다.](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="e05f5-117">저장소 액세스 키 복사</span><span class="sxs-lookup"><span data-stu-id="e05f5-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="e05f5-118">스트림 분석 서비스에 대한 입력을 설정하려면 곧 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![저장소에서 설정, 키를 열고 기본 액세스 키 복사](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="e05f5-120">Azure 저장소로 연속 내보내기 시작</span><span class="sxs-lookup"><span data-stu-id="e05f5-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="e05f5-121">[연속 내보내기](app-insights-export-telemetry.md) 는 Application Insights에서 Azure 저장소로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="e05f5-122">Azure 포털에서 응용 프로그램에 대해 만든 Application Insights 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![찾아보기, Application Insights, 응용 프로그램 선택](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="e05f5-124">연속 내보내기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-124">Create a continuous export.</span></span>
   
    ![설정, 연속 내보내기, 추가를 차례로 선택](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="e05f5-126">이전에 만든 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-126">Select the storage account you created earlier:</span></span>

    ![내보내기 대상 설정](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="e05f5-128">보려는 이벤트 유형을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-128">Set the event types you want to see:</span></span>

    ![이벤트 유형 선택](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="e05f5-130">일부 데이터가 누적되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-130">Let some data accumulate.</span></span> <span data-ttu-id="e05f5-131">한동안 사용자가 응용 프로그램을 사용하도록 놓아둡니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="e05f5-132">원격 분석이 제공되어 [메트릭 탐색기](app-insights-metrics-explorer.md)에서 통계 차트가, [진단 검색](app-insights-diagnostic-search.md)에서 개별 이벤트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="e05f5-133">또한 데이터를 저장소로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="e05f5-134">내보낸 데이터를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-134">Inspect the exported data.</span></span> <span data-ttu-id="e05f5-135">Visual Studio에서 **보기/클라우드 탐색기**를 선택하고 Azure/저장소를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="e05f5-136">이 메뉴 옵션이 없는 경우 Azure SDK를 설치해야 합니다. 새 프로젝트 대화 상자를 열고 Visual C#/클라우드/Microsoft Azure SDK for .NET 가져오기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="e05f5-137">응용 프로그램 이름 및 계측 키에서 파생된 경로 이름의 공통 부분을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="e05f5-138">이벤트는 JSON 형식으로 blob 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="e05f5-139">각 파일에는 하나 이상의 이벤트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-139">Each file may contain one or more events.</span></span> <span data-ttu-id="e05f5-140">따라서 이벤트 데이터를 읽고 원하는 필드를 필터링하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="e05f5-141">데이터로 온갖 종류의 작업을 수행할 수 있지만, 지금은 스트림 분석을 사용하여 데이터를 Power BI로 파이프하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="e05f5-142">Azure 스트림 분석 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="e05f5-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="e05f5-143">[클래식 Azure 포털](https://manage.windowsazure.com/)에서 Azure 스트림 분석 서비스를 선택하고 새 스트림 분석 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="e05f5-144">새 작업이 만들어지면 해당 세부 정보를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="e05f5-145">Blob 위치 설정</span><span class="sxs-lookup"><span data-stu-id="e05f5-145">Set blob location</span></span>
<span data-ttu-id="e05f5-146">연속 내보내기 Blob에서 입력을 가져오도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="e05f5-147">이제 앞에서 기록해 둔 저장소 계정의 기본 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="e05f5-148">이 키를 저장소 계정 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="e05f5-149">경로 접두사 패턴 설정</span><span class="sxs-lookup"><span data-stu-id="e05f5-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="e05f5-150">**날짜 형식을 YYYY-MM-DD(파선 포함)로 설정해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="e05f5-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="e05f5-151">전위 패턴은 스트림 분석이 저장소에서 입력 파일을 찾는 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="e05f5-152">연속 내보내기에서 데이터를 저장하는 방법과 일치하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="e05f5-153">다음과 같이 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="e05f5-154">이 예제에서:</span><span class="sxs-lookup"><span data-stu-id="e05f5-154">In this example:</span></span>

* <span data-ttu-id="e05f5-155">`webapplication27` 은 Application Insights 리소스의 이름으로, **모두 소문자**입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="e05f5-156">`1234...` 는 **대시를 생략한**Application Insights 리소스의 계측 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="e05f5-157">`PageViews` 는 분석하려는 데이터의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="e05f5-158">사용 가능한 형식은 연속 내보내기에 설정한 필터에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="e05f5-159">내보낸 데이터를 검사하여 사용 가능한 다른 형식을 확인하고 [데이터 모델 내보내기](app-insights-export-data-model.md)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="e05f5-160">`/{date}/{time}` 은 문자로 기록된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="e05f5-161">저장소를 검사하여 올바른 경로를 가져오는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="e05f5-162">초기 설치 완료</span><span class="sxs-lookup"><span data-stu-id="e05f5-162">Finish initial setup</span></span>
<span data-ttu-id="e05f5-163">직렬화 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-163">Confirm the serialization format:</span></span>

![마법사 확인 후 닫기](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="e05f5-165">마법사를 닫고 설치가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="e05f5-166">샘플 명령을 사용하여 일부 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="e05f5-167">쿼리를 디버그할 테스트 샘플로 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="e05f5-168">출력 설정</span><span class="sxs-lookup"><span data-stu-id="e05f5-168">Set the output</span></span>
<span data-ttu-id="e05f5-169">이제 사용자의 작업을 선택하고 출력을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-169">Now select your job and set the output.</span></span>

![새 채널을 선택하고, 출력, 추가, Power BI를 클릭합니다.](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="e05f5-171">**회사 또는 학교 계정** 을 제공하여 스트림 분석에 Power BI 리소스에 대한 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="e05f5-172">그런 다음 출력 및 대상 Power BI 데이터 집합과 테이블의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![이름 3개를 생성합니다.](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="e05f5-174">쿼리 설정</span><span class="sxs-lookup"><span data-stu-id="e05f5-174">Set the query</span></span>
<span data-ttu-id="e05f5-175">쿼리는 입력에서 출력으로 번역을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-175">The query governs the translation from input to output.</span></span>

![작업을 선택하고 쿼리를 클릭합니다.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="e05f5-178">Test 함수를 사용하여 올바른 출력이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="e05f5-179">입력 페이지에서 얻은 샘플 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="e05f5-180">이벤트 수를 표시하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="e05f5-180">Query to display counts of events</span></span>
<span data-ttu-id="e05f5-181">이 쿼리 붙여넣기:</span><span class="sxs-lookup"><span data-stu-id="e05f5-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="e05f5-182">내보내기 입력은 스트림 입력에 제공된 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="e05f5-183">pbi 출력은 정의한 출력 별칭입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="e05f5-184">이벤트 이름은 중첩된 JSON 배열에 있으므로 [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="e05f5-185">그런 다음 Select는 기간의 해당 이름이 있는 인스턴스의 수의 개수와 함께 이벤트 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="e05f5-186">[Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) 절은 요소를 1분의 기간으로 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="e05f5-187">메트릭 값을 표시하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="e05f5-187">Query to display metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="e05f5-188">이 쿼리는 이벤트 시간과 메트릭 값을 가져오기 위해 메트릭 원격 분석을 드릴합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="e05f5-189">메트릭 값은 배열 내부에 있으므로 OUTER APPLY GetElements 패턴을 사용하여 행을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="e05f5-190">이 경우 "myMetric"은 메트릭 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="e05f5-191">차원 속성의 값을 포함하는 쿼리</span><span class="sxs-lookup"><span data-stu-id="e05f5-191">Query to include values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="e05f5-192">이 쿼리는 차원 배열에 고정된 인덱스의 특정 차원에 상관없이 차원 속성의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="e05f5-193">작업 실행</span><span class="sxs-lookup"><span data-stu-id="e05f5-193">Run the job</span></span>
<span data-ttu-id="e05f5-194">작업을 시작할 과거의 날짜를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-194">You can select a date in the past to start the job from.</span></span> 

![작업을 선택하고 쿼리를 클릭합니다.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="e05f5-197">작업이 실행 중인 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="e05f5-198">Power BI에 결과를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e05f5-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="e05f5-199">[Power BI에서 Application Insights 데이터를 표시하는 데 권장되는 방법](app-insights-export-power-bi.md)이 있으며, 이 방법들은 훨씬 더 효율적이며 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="e05f5-200">여기서 설명하는 경로는 내보낸 데이터를 처리하는 방법을 보여 주기 위한 예로 사용했을 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="e05f5-201">회사 또는 학교 계정을 사용하여 Power BI를 열고 스트림 분석 작업의 출력으로 정의된 데이터 집합 및 테이블을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="e05f5-203">이제 [Power BI](https://powerbi.microsoft.com)의 보고서 및 대시보드에서 이 데이터 집합을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Power BI에서 데이터 집합과 필드를 선택합니다.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="e05f5-205">데이터가 없나요?</span><span class="sxs-lookup"><span data-stu-id="e05f5-205">No data?</span></span>
* <span data-ttu-id="e05f5-206">[날짜 형식](#set-path-prefix-pattern) 을 YYYY-MM-DD(대시 사용)로 정확하게 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="e05f5-207">비디오</span><span class="sxs-lookup"><span data-stu-id="e05f5-207">Video</span></span>
<span data-ttu-id="e05f5-208">Noam Ben Zeev에서는 Stream Analytics를 사용하여 내보낸 데이터를 처리하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e05f5-209">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e05f5-209">Next steps</span></span>
* [<span data-ttu-id="e05f5-210">연속 내보내기</span><span class="sxs-lookup"><span data-stu-id="e05f5-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="e05f5-211">속성 형식 및 값에 대한 자세한 데이터 모델 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="e05f5-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="e05f5-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="e05f5-212">Application Insights</span></span>](app-insights-overview.md)

