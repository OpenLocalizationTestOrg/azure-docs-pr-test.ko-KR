---
title: "Application Insights에서 Power BI로 내보내기 | Microsoft Docs"
description: "분석 쿼리를 Power BI에서 표시할 수 있습니다."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="55130-103">Application Insights에서 Power BI 공급</span><span class="sxs-lookup"><span data-stu-id="55130-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="55130-104">[Power BI](http://www.powerbi.com/)는 데이터를 분석하는 데 도움을 주고 통찰력을 공유하는 비즈니스 분석 도구 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="55130-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="55130-105">모든 장치에서 풍부한 대시보드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="55130-106">[Azure Application Insights](app-insights-overview.md)의 Analytics 쿼리를 포함하여 다양한 원본의 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="55130-107">Power BI에 Application Insights 데이터를 내보내는 세 가지 권장 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="55130-108">개별적으로 또는 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-108">You can use them separately or together.</span></span>

* <span data-ttu-id="55130-109">[**Power BI 어댑터**](#power-pi-adapter) - 앱에서 원격 분석의 전체 대시보드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="55130-110">일련의 차트가 미리 정의되어 있으나, 다른 원본에서 직접 쿼리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="55130-111">[**Analytics 쿼리 내보내기**](#export-analytics-queries) - Analytics를 사용하여 원하는 쿼리를 작성하고 Power BI로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="55130-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="55130-112">이 쿼리를 다른 데이터와 함께 대시보드에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="55130-113">[**연속 내보내기 및 Stream Analytics**](app-insights-export-stream-analytics.md) - 여기에서는 추가 작업을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="55130-114">데이터를 오랜 기간 유지하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="55130-115">그렇지 않은 경우에는 다른 방법이 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="55130-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="55130-116">Power BI 어댑터</span><span class="sxs-lookup"><span data-stu-id="55130-116">Power BI adapter</span></span>
<span data-ttu-id="55130-117">이 방법은 원격 분석의 전체 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55130-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="55130-118">초기 데이터 집합은 미리 정의되어 있으나, 더 많은 데이터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="55130-119">어댑터 가져오기</span><span class="sxs-lookup"><span data-stu-id="55130-119">Get the adapter</span></span>
1. <span data-ttu-id="55130-120">[Power BI](https://app.powerbi.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="55130-121">**데이터 가져오기**, **Services**, **Application Insights**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="55130-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="55130-123">Application Insights 리소스의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="55130-125">데이터를 가져오는 데1, 2분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="55130-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Power BI 어댑터](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="55130-127">Application Insights 차트를 다른 원본의 차트 및 Analytics 쿼리와 결합하여 대시보드를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="55130-128">추가 차트를 가져올 수 있는 시각화 갤러리가 있으며, 각 차트에는 설정할 수 있는 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="55130-129">초기 가져오기 후에는 대시보드와 보고서가 지속적으로 매일 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="55130-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="55130-130">데이터 집합에 대한 새로 고침 일정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="55130-131">Analytics 쿼리 내보내기</span><span class="sxs-lookup"><span data-stu-id="55130-131">Export Analytics queries</span></span>
<span data-ttu-id="55130-132">이 경로를 사용하면 원하는 모든 Analytics 쿼리를 작성한 다음, Power BI 대시보드로 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="55130-133">(어댑터에서 만든 대시보드를 추가할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="55130-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="55130-134">한 번: Power BI Desktop을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="55130-135">Application Insights 쿼리를 가져오려면 데스크톱 버전의 Power BI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="55130-136">하지만 또 웹이나 사용자의 Power BI 클라우드 작업 영역으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="55130-137">[Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="55130-138">Analytics 쿼리 내보내기</span><span class="sxs-lookup"><span data-stu-id="55130-138">Export an Analytics query</span></span>
1. <span data-ttu-id="55130-139">[Analytics 열기 및 쿼리 작성](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="55130-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="55130-140">결과에 만족할 때까지 쿼리를 테스트하고 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="55130-141">**내보내기 전에 Analytics에서 쿼리가 제대로 실행되는지 확인합니다.**</span><span class="sxs-lookup"><span data-stu-id="55130-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="55130-142">**내보내기** 메뉴에서 **Power BI(M)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="55130-143">텍스트 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-143">Save the text file.</span></span>
   
    ![Power BI 쿼리 내보내기](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="55130-145">Power BI Desktop에서 **데이터 가져오기, 빈 쿼리**를 선택한 다음, 쿼리 편집기에서 **보기** 아래에 있는 **고급 쿼리 편집기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="55130-146">내보낸 M 언어 스크립트를 고급 쿼리 편집기에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![고급 쿼리 편집기](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="55130-148">Power BI가 Azure에 액세스할 수 있도록 자격 증명을 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="55130-149">'조직 계정'을 사용하여 Microsoft 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Application Insights 쿼리를 실행하려면 Power BI를 사용하도록 설정하는 Azure 자격 증명을 제공합니다.](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="55130-151">(자격 증명을 확인해야 하는 경우 쿼리 편집기에서 데이터 원본 설정 메뉴 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="55130-152">Azure에 사용할 자격 증명은 Power BI용 자격 증명과 다를 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="55130-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="55130-153">쿼리에 대한 시각화를 선택하고 x축, y축 및 차원 분할에 대한 필드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![시각화 선택](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="55130-155">Power BI 클라우드 작업 영역에 보고서를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="55130-156">여기에서 다른 웹 페이지에 동기화된 버전을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![시각화 선택](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="55130-158">간격을 두고 보고서를 수동으로 새로 고치거나 옵션 페이지에서 예약된 새로 고침을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="55130-159">문제 해결</span><span class="sxs-lookup"><span data-stu-id="55130-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="55130-160">401 또는 403 권한 없음</span><span class="sxs-lookup"><span data-stu-id="55130-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="55130-161">업데이트되지 않은 토큰을 새로 고치는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="55130-162">여전히 액세스 권한이 있는지 확인하려면 다음 단계를 시도하십시오.</span><span class="sxs-lookup"><span data-stu-id="55130-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="55130-163">액세스 권한이 있고 자격 증명 새로 고침이 작동하지 않는 경우 지원 티켓을 여세요.</span><span class="sxs-lookup"><span data-stu-id="55130-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="55130-164">Azure Portal에 로그인하고 리소스에 액세스할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="55130-165">대시보드에 대한 자격 증명 새로 고침을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="55130-166">502 잘못된 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="55130-166">502 Bad Gateway</span></span>
<span data-ttu-id="55130-167">일반적으로 너무 많은 데이터를 반환하는 분석 쿼리가 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="55130-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="55130-168">더 작은 시간 범위를 사용하거나 [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) 또는 [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) 함수를 사용하여 시도해야 합니다(필요한 필드인 [프로젝트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator)만 해당).</span><span class="sxs-lookup"><span data-stu-id="55130-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="55130-169">분석 쿼리에서 들어오는 데이터 집합 감소가 요구 사항을 충족하지 않는 경우 더 큰 데이터 집합을 가져오도록 [API](https://dev.applicationinsights.io/documentation/overview) 사용을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="55130-170">M 쿼리 내보내기를 변환하여 API를 사용하는 방법에 대한 지침은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="55130-171">[API 키](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID) 만들기</span><span class="sxs-lookup"><span data-stu-id="55130-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="55130-172">ARM URL을 AI API로 대체하여 분석에서 내보낸 Power BI M 스크립트를 업데이트합니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="55130-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="55130-173">대체 **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="55130-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="55130-174">**https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="55130-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="55130-175">마지막으로 자격 증명을 기본으로 업데이트하고 API 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="55130-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="55130-176">**기존 스크립트**</span><span class="sxs-lookup"><span data-stu-id="55130-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="55130-177">**업데이트된 스크립트**</span><span class="sxs-lookup"><span data-stu-id="55130-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="55130-178">샘플링 정보</span><span class="sxs-lookup"><span data-stu-id="55130-178">About sampling</span></span>
<span data-ttu-id="55130-179">응용 프로그램에서 많은 양의 데이터를 전송하는 경우 적응 샘플링 기능이 작동하여 원격 분석의 백분율만 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55130-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="55130-180">이는 SDK 또는 수집에서 샘플링을 수동으로 설정한 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="55130-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="55130-181">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="55130-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="55130-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55130-182">Next steps</span></span>
* [<span data-ttu-id="55130-183">Power BI - 알아보기</span><span class="sxs-lookup"><span data-stu-id="55130-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="55130-184">Analytics 자습서</span><span class="sxs-lookup"><span data-stu-id="55130-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

