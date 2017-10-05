---
title: "Azure Cosmos DB 요청 및 저장소 모니터링 | Microsoft Docs"
description: "성능 메트릭(예: 요청 및 서버 오류) 및 사용 메트릭(예: 저장소 사용)에 대해 Azure Cosmos DB 계정을 모니터링하는 방법을 알아봅니다."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: 0ca652d31d6c50124f87916b4486d8279075f106
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a><span data-ttu-id="d9f90-103">Azure Cosmos DB 요청, 사용 및 저장소 모니터링</span><span class="sxs-lookup"><span data-stu-id="d9f90-103">Monitor Azure Cosmos DB requests, usage, and storage</span></span>
<span data-ttu-id="d9f90-104">[Azure Portal](https://portal.azure.com/)에서 Azure Cosmos DB 계정을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-104">You can monitor your Azure Cosmos DB accounts in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d9f90-105">각 Azure Cosmos DB 계정에 대해 성능 메트릭(예: 요청 및 서버 오류) 및 사용 메트릭(예: 저장소 사용)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-105">For each Azure Cosmos DB account, both performance metrics, such as requests and server errors, and usage metrics, such as storage consumption, are available.</span></span>

<span data-ttu-id="d9f90-106">계정 블레이드, 새 메트릭 블레이드 또는 Azure Monitor에서 메트릭을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-106">Metrics can be reviewed on the Account blade, the new Metrics blade, or in Azure Monitor.</span></span>

## <a name="view-performance-metrics-on-the-metrics-blade"></a><span data-ttu-id="d9f90-107">메트릭 블레이드에서 성능 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="d9f90-107">View performance metrics on the Metrics blade</span></span>
1. <span data-ttu-id="d9f90-108">[Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**를 클릭하고, **데이터베이스**로 스크롤한 다음 **Azure Cosmos DB**를 클릭하고 성능 메트릭을 보려는 Azure Cosmos DB 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-108">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="d9f90-109">리소스 메뉴의 **모니터링** 아레에서 **메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-109">In the resource menu, under **Monitoring**, click **Metrics**.</span></span>

<span data-ttu-id="d9f90-110">메트릭 블레이드가 열리고 검토할 컬렉션을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-110">The Metrics blade opens, and you can select the collection to review.</span></span> <span data-ttu-id="d9f90-111">가용성, 요청, 처리량 및 저장소 메트릭을 검토하고 Azure Cosmos DB SLA와 비교할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-111">You can review Availability, Requests, Throughput, and Storage metrics and compare them to the Azure Cosmos DB SLAs.</span></span>

## <a name="view-performance-metrics-by-using-azure-monitoring"></a><span data-ttu-id="d9f90-112">Azure 모니터링을 사용하여 성능 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="d9f90-112">View performance metrics by using Azure Monitoring</span></span>
1. <span data-ttu-id="d9f90-113">[Azure Portal](https://portal.azure.com/)에서 표시줄에 있는 **모니터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-113">In the [Azure portal](https://portal.azure.com/), click **Monitor** on the Jumpbar.</span></span>
2. <span data-ttu-id="d9f90-114">리소스 메뉴에서 **메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-114">In the resource menu, click **Metrics**.</span></span>
3. <span data-ttu-id="d9f90-115">**모니터 - 메트릭** 창의 **리소스 그룹** 드롭다운 메뉴에서 모니터링할 Azure Cosmos DB 계정과 연결된 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-115">In the **Monitor - Metrics** window, in the **esource group** drop-down menu, select the resource group associated with the Azure Cosmos DB account that you'd like to monitor.</span></span> 
4. <span data-ttu-id="d9f90-116">**리소스** 드롭 다운 메뉴에서 모니터링할 데이터베이스 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-116">In the **Resource** drop-down menu, select the database account to monitor.</span></span>
5. <span data-ttu-id="d9f90-117">**사용 가능한 메트릭** 목록에서 표시할 메트릭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-117">In the list of **Available metrics**, select the metrics to display.</span></span> <span data-ttu-id="d9f90-118">다중 선택을 하려면 CTRL 단추를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-118">Use the CTRL button to multi-select.</span></span> 

    <span data-ttu-id="d9f90-119">**그림** 창에서 메트릭이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-119">Your metrics are displayed on in the **Plot** window.</span></span> 

## <a name="view-performance-metrics-on-the-account-blade"></a><span data-ttu-id="d9f90-120">계정 블레이드에서 성능 메트릭 보기</span><span class="sxs-lookup"><span data-stu-id="d9f90-120">View performance metrics on the account blade</span></span>
1. <span data-ttu-id="d9f90-121">[Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**를 클릭하고, **데이터베이스**로 스크롤한 다음 **Azure Cosmos DB**를 클릭하고 성능 메트릭을 보려는 Azure Cosmos DB 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-121">In the [Azure portal](https://portal.azure.com/), click **More Services**, scroll to **Databases**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to view performance metrics.</span></span>
2. <span data-ttu-id="d9f90-122">**모니터링** 렌즈에는 기본적으로 다음 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-122">The **Monitoring** lens displays the following tiles by default:</span></span>
   
   * <span data-ttu-id="d9f90-123">오늘의 총 요청 수</span><span class="sxs-lookup"><span data-stu-id="d9f90-123">Total requests for the current day.</span></span>
   * <span data-ttu-id="d9f90-124">사용된 저장소.</span><span class="sxs-lookup"><span data-stu-id="d9f90-124">Storage used.</span></span>
   
   <span data-ttu-id="d9f90-125">데이터베이스에 데이터가 있는데 테이블에 **데이터를 사용할 수 없음** 이 표시되면 [문제 해결](#troubleshooting) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9f90-125">If your table displays **No data available** and you believe there is data in your database, see the [Troubleshooting](#troubleshooting) section.</span></span>
   
   ![요청 및 저장소 사용량이 표시된 모니터링 렌즈의 스크린샷](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. <span data-ttu-id="d9f90-127">**요청** 또는 **사용 할당량** 타일을 클릭하면 자세한 **메트릭** 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-127">Clicking on the **Requests** or **Usage Quota** tile opens a detailed **Metric** blade.</span></span>
4. <span data-ttu-id="d9f90-128">**메트릭** 블레이드는 선택한 메트릭에 대한 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-128">The **Metric** blade shows you details about the metrics you have selected.</span></span>  <span data-ttu-id="d9f90-129">블레이드 맨 위에는 시간별 요청 그래프가 표시되고 아래에는 정제 및 총 요청의 집계 값을 표시하는 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-129">At the top of the blade is a graph of requests charted hourly, and below that is table that shows aggregation values for throttled and total requests.</span></span>  <span data-ttu-id="d9f90-130">또한 메트릭 블레이드는 현재 메트릭 블레이드에 표시되는 메트릭으로 정의 및 필터링된 경고 목록을 보여 줍니다. 이런 방법으로, 경고가 많은 경우 여기에 표시되는 관련성 높은 경고만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-130">The metric blade also shows the list of alerts which have been defined, filtered to the metrics that appear on the current metric blade (this way, if you have a number of alerts, you'll only see the relevant ones presented here).</span></span>   
   
   ![정제된 요청을 포함하는 메트릭 블레이드의 스크린샷](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-the-portal"></a><span data-ttu-id="d9f90-132">포털에서 성능 메트릭 뷰 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d9f90-132">Customize performance metric views in the portal</span></span>
1. <span data-ttu-id="d9f90-133">특정 차트에서 표시되는 메트릭을 사용자 지정하려면 차트를 클릭하여 **메트릭** 블레이드에서 열고 **차트 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-133">To customize the metrics that display in a particular chart, click the chart to open it in the **Metric** blade, and then click **Edit chart**.</span></span>  
   <span data-ttu-id="d9f90-134">![차트 편집이 강조된 메트릭 블레이드 컨트롤의 스크린샷](./media/monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-134">![Screen shot of the Metric blade controls, with Edit chart highlighted](./media/monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="d9f90-135">**차트 편집** 블레이드는 차트에 표시되는 메트릭과 메트릭의 시간 범위를 수정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-135">On the **Edit Chart** blade, there are options to modify the metrics that display in the chart, as well as their time range.</span></span>  
   <span data-ttu-id="d9f90-136">![차트 편집 블레이드의 스크린샷](./media/monitor-accounts/madocdb4.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-136">![Screen shot of the Edit Chart blade](./media/monitor-accounts/madocdb4.png)</span></span>
3. <span data-ttu-id="d9f90-137">이 부분에 표시되는 메트릭을 변경하려는 경우 사용 가능한 성능 메트릭을 선택/선택 취소한 다음 블레이드의 아래쪽에 있는 **확인** 을 클릭하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-137">To change the metrics displayed in the part, simply select or clear the available performance metrics, and then click **OK** at the bottom of the blade.</span></span>  
4. <span data-ttu-id="d9f90-138">시간 범위를 변경하려면 다른 범위(예: **사용자 지정**)를 선택한 다음 블레이드의 아래쪽에 있는 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-138">To change the time range, choose a different range (for example, **Custom**), and then click **OK** at the bottom of the blade.</span></span>  
   
   ![사용자 지정 시간 범위를 입력하는 방법을 보여 주는 차트 편집 블레이드 시간 범위 파트의 스크린샷](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-the-portal"></a><span data-ttu-id="d9f90-140">포털에서 병렬 차트 만들기</span><span class="sxs-lookup"><span data-stu-id="d9f90-140">Create side-by-side charts in the portal</span></span>
<span data-ttu-id="d9f90-141">Azure 포털에서 병렬 메트릭 차트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-141">The Azure Portal allows you to create side-by-side metric charts.</span></span>  

1. <span data-ttu-id="d9f90-142">먼저 복사할 차트를 마우스 오른쪽 단추로 클릭하고 **사용자 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-142">First, right-click on the chart you want to copy and select **Customize**.</span></span>
   
   ![사용자 지정 옵션이 강조 표시된 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb6.png)
2. <span data-ttu-id="d9f90-144">메뉴에서 **복제**를 클릭하여 파트를 복사한 후 **사용자 지정 완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-144">Click **Clone** on the menu to copy the part and then click **Done customizing**.</span></span>
   
   ![복제 및 사용자 지정 완료 옵션이 강조 표시된 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb7.png)  

<span data-ttu-id="d9f90-146">이제 파트에 표시되는 메트릭 및 시간 범위를 사용자 지정하면서 이 파트를 다른 메트릭 파트로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-146">You may now treat this part as any other metric part, customizing the metrics and time range displayed in the part.</span></span>  <span data-ttu-id="d9f90-147">이렇게 하면 두 가지 다른 메트릭 차트를 동시에 병렬로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-147">By doing this, you can see two different metrics chart side-by-side at the same time.</span></span>  
    ![총 요청 차트 및 지난 1시간의 새로운 총 요청 차트의 스크린샷](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-the-portal"></a><span data-ttu-id="d9f90-149">포털에서 경고 설정</span><span class="sxs-lookup"><span data-stu-id="d9f90-149">Set up alerts in the portal</span></span>
1. <span data-ttu-id="d9f90-150">[Azure Portal](https://portal.azure.com/)에서 **서비스 더 보기**, **Azure Cosmos DB**를 차례로 클릭하고 성능 메트릭 경고를 설정할 Azure Cosmos DB 계정의 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-150">In the [Azure portal](https://portal.azure.com/), click **More Services**, click **Azure Cosmos DB**, and then click the name of the Azure Cosmos DB account for which you would like to setup performance metric alerts.</span></span>
2. <span data-ttu-id="d9f90-151">리소스 메뉴에서 **경고 규칙** 을 클릭하여 경고 규칙 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-151">In the resource menu, click **Alert Rules** to open the Alert rules blade.</span></span>  
   <span data-ttu-id="d9f90-152">![경고 규칙 부분이 선택된 스크린샷](./media/monitor-accounts/madocdb10.5.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-152">![Screen shot of the Alert rules part selected](./media/monitor-accounts/madocdb10.5.png)</span></span>
3. <span data-ttu-id="d9f90-153">**경고 규칙** 블레이드에서 **경고 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-153">In the **Alert rules** blade, click **Add alert**.</span></span>  
   <span data-ttu-id="d9f90-154">![경고 추가 단추가 강조 표시된 경고 규칙 블레이드의 스크린샷](./media/monitor-accounts/madocdb11.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-154">![Screenshot of the Alert Rules blade, with the Add Alert button highlighted](./media/monitor-accounts/madocdb11.png)</span></span>
4. <span data-ttu-id="d9f90-155">**경고 규칙 추가** 블레이드에서 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-155">In the **Add an alert rule** blade, specify:</span></span>
   
   * <span data-ttu-id="d9f90-156">설정 중인 경고 규칙의 이름</span><span class="sxs-lookup"><span data-stu-id="d9f90-156">The name of the alert rule you are setting up.</span></span>
   * <span data-ttu-id="d9f90-157">새 경고 규칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="d9f90-157">A description of the new alert rule.</span></span>
   * <span data-ttu-id="d9f90-158">경고 규칙에 대한 메트릭</span><span class="sxs-lookup"><span data-stu-id="d9f90-158">The metric for the alert rule.</span></span>
   * <span data-ttu-id="d9f90-159">경고가 활성화되는 시기를 결정하는 조건, 임계값 및 기간.</span><span class="sxs-lookup"><span data-stu-id="d9f90-159">The condition, threshold, and period that determine when the alert activates.</span></span> <span data-ttu-id="d9f90-160">예를 들어 서버 오류가 지난 15분 동안 5개보다 많습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-160">For example, a server error count greater than 5 over the last 15 minutes.</span></span>
   * <span data-ttu-id="d9f90-161">경고가 발생할 때 서비스 관리자 및 공동 관리자에게 메일을 보낼지 여부</span><span class="sxs-lookup"><span data-stu-id="d9f90-161">Whether the service administrator and coadministrators are emailed when the alert fires.</span></span>
   * <span data-ttu-id="d9f90-162">경고 알림에 대한 추가 메일 주소</span><span class="sxs-lookup"><span data-stu-id="d9f90-162">Additional email addresses for alert notifications.</span></span>  
     ![경고 규칙 추가 블레이드의 스크린샷](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a><span data-ttu-id="d9f90-164">프로그래밍 방식으로 Azure Cosmos DB 모니터링</span><span class="sxs-lookup"><span data-stu-id="d9f90-164">Monitor Azure Cosmos DB programatically</span></span>
<span data-ttu-id="d9f90-165">포털에서 제공되는 계정 수준 메트릭(예: 계정 저장소 사용 및 총 요청)은 DocumentDB API를 통해 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-165">The account level metrics available in the portal, such as account storage usage and total requests, are not available via the DocumentDB APIs.</span></span> <span data-ttu-id="d9f90-166">그러나 DocumentDB API를 사용하여 컬렉션 수준에서 사용 데이터를 조회할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-166">However, you can retrieve usage data at the collection level by using the DocumentDB APIs.</span></span> <span data-ttu-id="d9f90-167">컬렉션 수준 데이터를 검색하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-167">To retrieve collection level data, do the following:</span></span>

* <span data-ttu-id="d9f90-168">REST API를 사용하려면 [컬렉션에 대해 GET을 수행](https://msdn.microsoft.com/library/mt489073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-168">To use the REST API, [perform a GET on the collection](https://msdn.microsoft.com/library/mt489073.aspx).</span></span> <span data-ttu-id="d9f90-169">컬렉션에 대한 할당량 및 사용량 정보는 응답의 x-ms-resource-quota 및 x-ms-resource-usage 헤더에서 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-169">The quota and usage information for the collection is returned in the x-ms-resource-quota and x-ms-resource-usage headers in the response.</span></span>
* <span data-ttu-id="d9f90-170">.NET SDK를 사용하려면 [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) 메서드를 사용합니다. 이 메서드는 **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage** 등의 여러 사용량 속성이 포함된 [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx)를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-170">To use the .NET SDK, use the [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) method, which returns a [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) that contains a number of usage properties such as **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**, and more.</span></span>

<span data-ttu-id="d9f90-171">추가 메트릭에 액세스하려면 [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="d9f90-171">To access additional metrics, use the [Azure Monitor SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights).</span></span> <span data-ttu-id="d9f90-172">가용 메트릭 정의는 다음을 호출하면 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-172">Available metric definitions can be retrieved by calling:</span></span>

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

<span data-ttu-id="d9f90-173">개별 메트릭을 검색하는 쿼리는 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-173">Queries to retrieve individual metrics use the following format:</span></span>

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

<span data-ttu-id="d9f90-174">자세한 내용은 [Azure Monitor REST API를 통해 리소스 메트릭 검색](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9f90-174">For more information, see [Retrieving Resource Metrics via the Azure Monitor REST API](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/).</span></span> <span data-ttu-id="d9f90-175">"Azure Inights"가 "Azure Monitor"로 이름이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-175">Note that "Azure Inights" was renamed "Azure Monitor".</span></span>  <span data-ttu-id="d9f90-176">이 블로그 항목에서는 이전 이름을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-176">This blog entry refers to the older name.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d9f90-177">문제 해결</span><span class="sxs-lookup"><span data-stu-id="d9f90-177">Troubleshooting</span></span>
<span data-ttu-id="d9f90-178">최근에 데이터를 요청했거나 데이터베이스에 데이터를 추가했는데 모니터링 타일에 **데이터를 사용할 수 없음** 메시지가 표시되면 최근 사용 현황을 반영하도록 이 타일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-178">If your monitoring tiles display the **No data available** message, and you recently made requests or added data to the database, you can edit the tile to reflect the recent usage.</span></span>

### <a name="edit-a-tile-to-refresh-current-data"></a><span data-ttu-id="d9f90-179">현재 데이터를 새로 고치도록 타일 편집</span><span class="sxs-lookup"><span data-stu-id="d9f90-179">Edit a tile to refresh current data</span></span>
1. <span data-ttu-id="d9f90-180">특정 부분에 표시되는 메트릭을 사용자 지정하려면 차트를 클릭하여 **메트릭** 블레이드를 열고 **차트 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-180">To customize the metrics that display in a particular part, click the chart to open the **Metric** blade, and then click **Edit Chart**.</span></span>  
   <span data-ttu-id="d9f90-181">![차트 편집이 강조된 메트릭 블레이드 컨트롤의 스크린샷](./media/monitor-accounts/madocdb3.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-181">![Screen shot of the Metric blade controls, with Edit chart highlighted](./media/monitor-accounts/madocdb3.png)</span></span>
2. <span data-ttu-id="d9f90-182">**차트 편집** 블레이드의 **시간 범위** 섹션에서 **지난 시간**, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-182">On the **Edit Chart** blade, in the **Time Range** section, click **past hour**, and then click **OK**.</span></span>  
   <span data-ttu-id="d9f90-183">![지난 시간이 선택된 차트 편집 블레이드의 스크린샷](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)</span><span class="sxs-lookup"><span data-stu-id="d9f90-183">![Screen shot of the Edit Chart blade with past hour selected](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)</span></span>
3. <span data-ttu-id="d9f90-184">그러면 타일이 새로 고쳐져 최신 데이터 및 사용 현황이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9f90-184">Your tile should now refresh showing your current data and usage.</span></span>  
   ![업데이트된 총 요청 지난 시간 타일의 스크린샷](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a><span data-ttu-id="d9f90-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9f90-186">Next steps</span></span>
<span data-ttu-id="d9f90-187">Azure Cosmos DB 용량 계획에 대한 자세한 내용은 [Azure Cosmos DB Capacity Planner 계산기](https://www.documentdb.com/capacityplanner)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d9f90-187">To learn more about Azure Cosmos DB capacity planning, see the [Azure Cosmos DB capacity planner calculator](https://www.documentdb.com/capacityplanner).</span></span>

