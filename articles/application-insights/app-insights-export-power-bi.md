---
title: "Application Insights에서 aaaExport tooPower BI | Microsoft Docs"
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
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="b8b10-103">Application Insights에서 Power BI 공급</span><span class="sxs-lookup"><span data-stu-id="b8b10-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="b8b10-104">[Power BI](http://www.powerbi.com/)는 데이터를 분석하는 데 도움을 주고 통찰력을 공유하는 비즈니스 분석 도구 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="b8b10-105">모든 장치에서 풍부한 대시보드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="b8b10-106">[Azure Application Insights](app-insights-overview.md)의 Analytics 쿼리를 포함하여 다양한 원본의 데이터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="b8b10-107">Application Insights 데이터 tooPower BI 내보내기의 권장된 하는 세 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="b8b10-108">개별적으로 또는 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-108">You can use them separately or together.</span></span>

* <span data-ttu-id="b8b10-109">[**Power BI 어댑터**](#power-pi-adapter) - 앱에서 원격 분석의 전체 대시보드를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="b8b10-110">hello 일련의 차트 미리 정의 되어 있지만 다른 소스에서 직접 쿼리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="b8b10-111">[**분석 쿼리를 내보내기** ](#export-analytics-queries) -작성할 원하는 쿼리 분석을 사용 하 여 BI tooPower 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="b8b10-112">이 쿼리를 다른 데이터와 함께 대시보드에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="b8b10-113">[**연속 내보내기 및 스트림 분석** ](app-insights-export-stream-analytics.md) -를 더 많은 작업 tooset이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="b8b10-114">오랜 시간 동안 tookeep 데이터 원하는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="b8b10-115">그렇지 않으면 hello 다른 메서드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="b8b10-116">Power BI 어댑터</span><span class="sxs-lookup"><span data-stu-id="b8b10-116">Power BI adapter</span></span>
<span data-ttu-id="b8b10-117">이 방법은 원격 분석의 전체 대시보드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="b8b10-118">hello 초기 데이터 집합을 미리 정의 되어 있지만 더 많은 데이터 tooit를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="b8b10-119">Hello 어댑터를 가져옵니다</span><span class="sxs-lookup"><span data-stu-id="b8b10-119">Get hello adapter</span></span>
1. <span data-ttu-id="b8b10-120">역시 로그인[Power BI](https://app.powerbi.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="b8b10-121">**데이터 가져오기**, **Services**, **Application Insights**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="b8b10-123">Application Insights 리소스의 hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Application Insights 데이터 원본에서 가져오기](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="b8b10-125">가져온 hello 데이터 toobe에 대 일 분 정도 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Power BI 어댑터](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="b8b10-127">다른 원본 및 분석 쿼리 hello Application Insights 차트를 결합 hello 대시보드를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="b8b10-128">추가 차트를 가져올 수 있는 시각화 갤러리가 있으며, 각 차트에는 설정할 수 있는 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="b8b10-129">Hello 초기 가져오기, hello 대시보드 및 보고서 hello 후 tooupdate를 매일 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="b8b10-130">Hello 데이터 집합에 대해 hello 새로 고침 일정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="b8b10-131">Analytics 쿼리 내보내기</span><span class="sxs-lookup"><span data-stu-id="b8b10-131">Export Analytics queries</span></span>
<span data-ttu-id="b8b10-132">이 경로 toowrite 수 있습니다. 모든 분석 원하는 쿼리 한 다음 해당 tooa Power BI 대시보드를 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="b8b10-133">(Hello 어댑터에서 만드는 toohello 대시보드에 추가할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b8b10-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="b8b10-134">한 번: Power BI Desktop을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="b8b10-135">tooimport Application Insights 쿼리, Power BI의 데스크톱 버전 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="b8b10-136">하지만 다음 게시할 수 있습니다 toohello 웹 또는 tooyour Power BI 클라우드 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="b8b10-137">[Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="b8b10-138">Analytics 쿼리 내보내기</span><span class="sxs-lookup"><span data-stu-id="b8b10-138">Export an Analytics query</span></span>
1. <span data-ttu-id="b8b10-139">[Analytics 열기 및 쿼리 작성](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="b8b10-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="b8b10-140">테스트 하 고 hello 쿼리를 구체화 하 여 hello 결과에 만족 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="b8b10-141">**실행 올바르게 분석 하기 전에 내보낼 hello 쿼리 있는지 확인 합니다.**</span><span class="sxs-lookup"><span data-stu-id="b8b10-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="b8b10-142">Hello에 **내보내기** 메뉴 선택 **Power BI (M)**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="b8b10-143">Hello 텍스트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-143">Save hello text file.</span></span>
   
    ![Power BI 쿼리 내보내기](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="b8b10-145">Power BI Desktop select에서 **데이터 가져오기, 빈 쿼리** 다음 hello에서 쿼리 편집기에서 및 **보기** 선택 **고급 쿼리 편집기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="b8b10-146">붙여넣기 hello 내보낸 스크립트를 M 언어 hello 고급 쿼리 편집기.</span><span class="sxs-lookup"><span data-stu-id="b8b10-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![고급 쿼리 편집기](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="b8b10-148">Tooprovide 자격 증명 tooallow Power BI tooaccess Azure 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="b8b10-149">Microsoft 계정으로 '조직 계정' toosign를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Application Insights 쿼리 tooenable Power BI toorun Azure 자격 증명 제공](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="b8b10-151">(Tooverify hello 자격 증명이 필요한 경우 명령을 사용 하 여 hello 데이터 원본 설정 메뉴 hello 쿼리 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="b8b10-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="b8b10-152">주의 toospecify hello Power BI에 대 한 사용자 자격 증명과 다를 수 있는 Azure에 사용할 자격 증명 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b8b10-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="b8b10-153">쿼리에 대 한 시각화를 선택 하 고 x 축, y 및 차원 분할에 대 한 hello 필드를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![시각화 선택](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="b8b10-155">보고서 tooyour Power BI 클라우드 작업 영역을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="b8b10-156">여기에서 다른 웹 페이지에 동기화된 버전을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![시각화 선택](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="b8b10-158">간격에 따라 hello 보고서를 수동으로 새로 고침 또는 hello 옵션 페이지에서 예약 된 새로 고침을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b8b10-159">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b8b10-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="b8b10-160">401 또는 403 권한 없음</span><span class="sxs-lookup"><span data-stu-id="b8b10-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="b8b10-161">업데이트되지 않은 토큰을 새로 고치는 경우 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="b8b10-162">에 이러한 단계 tooensure를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b8b10-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="b8b10-163">액세스 권한이 refershing hello 자격 증명이 작동 하지 않는 경우 지원 티켓을 개시 하세요.</span><span class="sxs-lookup"><span data-stu-id="b8b10-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="b8b10-164">Hello Azure 포털에 로그인 하 고 hello 리소스에 액세스할 수 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="b8b10-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="b8b10-165">대시보드 hello에 대 한 toorefresh hello 자격 증명을 시도 하십시오</span><span class="sxs-lookup"><span data-stu-id="b8b10-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="b8b10-166">502 잘못된 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="b8b10-166">502 Bad Gateway</span></span>
<span data-ttu-id="b8b10-167">일반적으로 너무 많은 데이터를 반환하는 분석 쿼리가 원인입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="b8b10-168">더 작은 시간 범위를 사용 하는 것이 좋습니다 또는 hello를 사용 하 여 [전](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) 또는 [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) 함수만 해당 [프로젝트](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello 필요한 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="b8b10-169">Hello 사용을 고려해 야 hello 분석 쿼리에서에서 들어오는 hello 데이터 집합을 줄여 요구 사항을 충족 하지 않는 경우 [API](https://dev.applicationinsights.io/documentation/overview) toopull 더 큰 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="b8b10-170">다음은 방법 tooconvert hello M 쿼리 내보내기 toouse hello API에 대 한 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="b8b10-171">[API 키](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID) 만들기</span><span class="sxs-lookup"><span data-stu-id="b8b10-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="b8b10-172">업데이트 hello 대체 하 여 분석에서 내보낸 Power BI M 스크립트 hello ARM AI API URL (아래 예제 참조)</span><span class="sxs-lookup"><span data-stu-id="b8b10-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="b8b10-173">대체 **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="b8b10-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="b8b10-174">**https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="b8b10-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="b8b10-175">마지막으로, 자격 증명 toobasic를 업데이트 하 고 API 키를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="b8b10-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="b8b10-176">**기존 스크립트**</span><span class="sxs-lookup"><span data-stu-id="b8b10-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="b8b10-177">**업데이트된 스크립트**</span><span class="sxs-lookup"><span data-stu-id="b8b10-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="b8b10-178">샘플링 정보</span><span class="sxs-lookup"><span data-stu-id="b8b10-178">About sampling</span></span>
<span data-ttu-id="b8b10-179">응용 프로그램에서 많은 양의 데이터를 하는 경우 hello 적응 샘플링 기능 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="b8b10-180">hello 수동으로 설정 하면 샘플링 hello SDK 또는 수집 중에 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="b8b10-181">샘플링에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8b10-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="b8b10-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b8b10-182">Next steps</span></span>
* [<span data-ttu-id="b8b10-183">Power BI - 알아보기</span><span class="sxs-lookup"><span data-stu-id="b8b10-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="b8b10-184">Analytics 자습서</span><span class="sxs-lookup"><span data-stu-id="b8b10-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

