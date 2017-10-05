---
title: "Stream Analytics에서 작업 및 서비스 로그를 사용한 디버그 | Microsoft Docs"
description: "Stream Analytics 작업 로그 사용 방법"
keywords: "서비스 로그"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: c95d240ebef6a84228eb98db70002792fcfbdea6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="bcabf-104">서비스 및 작업 로그를 사용하여 Stream Analytics 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="bcabf-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="bcabf-105">모든 Azure 서비스는 관리 작업과 관련된 세부 정보를 기록하는 작업 로깅 메시지를 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-105">All Azure services supply operational logging messages to users to record details related to management operations.</span></span> <span data-ttu-id="bcabf-106">Azure Stream Analytics에서 이 정보는 작업 상태, 작업 진행률 및 오류 메시지를 보고 시작부터 출력 처리까지 시간에 따른 작업 진행 상황을 추적하는 등 디버깅 목적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages to track the progress of a job over time, from start to processing to output.</span></span>

## <a name="find-operation-logs-in-the-azure-management-portal"></a><span data-ttu-id="bcabf-107">Azure 관리 포털에서 작업 로그 찾기</span><span class="sxs-lookup"><span data-stu-id="bcabf-107">Find operation logs in the Azure Management portal</span></span>
<span data-ttu-id="bcabf-108">작업 로그는 다음 두 가지 방법으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="bcabf-109">Stream Analytics 작업의 대시보드</span><span class="sxs-lookup"><span data-stu-id="bcabf-109">Dashboard of the Stream Analytics job</span></span>  
* <span data-ttu-id="bcabf-110">Azure 클래식 포털의 관리 서비스</span><span class="sxs-lookup"><span data-stu-id="bcabf-110">Management Services in the Azure Classic portal</span></span>  

## <a name="dashboard-of-the-stream-analytics-job"></a><span data-ttu-id="bcabf-111">Stream Analytics 작업의 대시보드</span><span class="sxs-lookup"><span data-stu-id="bcabf-111">Dashboard of the Stream Analytics job</span></span>
<span data-ttu-id="bcabf-112">Stream Analytics 작업의 해당 로그에 대한 링크는 작업의 대시보드 탭에 표시됩니다. 이 링크를 클릭하면 해당 특정 작업에 대한 최신 로그를 표시하는 방식으로 필터가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-112">A link to the corresponding logs of a Stream Analytics job is displayed on the job’s Dashboard tab. If you click on that link, it will set the filters in a way that it shows latest logs for that specific job.</span></span>

  ![관리 서비스 로그 선택](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="bcabf-114">관리 서비스</span><span class="sxs-lookup"><span data-stu-id="bcabf-114">Management Services</span></span>
<span data-ttu-id="bcabf-115">Azure 클래식 포털에서 Stream Analytics 및 기타 서비스에 대한 작업 로그를 수동으로 이동하는 방법:</span><span class="sxs-lookup"><span data-stu-id="bcabf-115">To manually navigate to the Operation Logs for Stream Analytics and other services in the Azure Classic portal:</span></span>

1. <span data-ttu-id="bcabf-116">**Azure 클래식 포털** 에서 [관리 서비스](https://manage.windowsazure.com)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-116">Click on **Management Services** in the [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bcabf-117">**유형**으로 **Stream Analytics**을 선택하고 **서비스 이름**으로 작업 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-117">Select **Stream Analytics** for **Type** and the name of the job for **Service Name**.</span></span>  
   
   ![Stream Analytics 선택](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-the-azure-portal"></a><span data-ttu-id="bcabf-119">Azure Portal에서 감사 로그 찾기</span><span class="sxs-lookup"><span data-stu-id="bcabf-119">Find audit logs in the Azure portal</span></span>
<span data-ttu-id="bcabf-120">Azure Portal에서 Stream Analytics 작업에 대한 작업 로그를 찾으려면, **찾아보기**를 클릭하여 **감사 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-120">To find operational logs for your Stream Analytics job in the Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Azure Portal 선택 Stream Analytics](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-122">그러면 구독의 모든 리소스에 대해 지난 7일 동안의 이벤트를 보여 주는 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-122">This will open a blade showing events from the last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="bcabf-123">**필터** 명령을 클릭하여 유형 또는 시간 프레임 지정 이벤트를 보도록 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-123">You can filter to see events of a specify type or time frame by clicking the **Filter** command.</span></span>

  ![Azure Portal 선택 Stream Analytics](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="bcabf-125">로그 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="bcabf-125">Get log details</span></span>
<span data-ttu-id="bcabf-126">시간 범위 및 상태를 기준으로 필터링하여 작업 로그를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-126">You can filter by Time Range and Status to view the logs for your job.</span></span>

<span data-ttu-id="bcabf-127">Azure 관리 포털에서 창의 맨 아래에 있는 **세부 정보** 단추를 클릭하여 선택한 이벤트에 대한 세부 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-127">In the Azure Management portal, click on the **Details** button at the bottom of the window to view more details about a selected event.</span></span> 

  ![세부 정보 선택](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-129">Azure Portal에서 로그 항목을 클릭하여 그 안의 자세한 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-129">In the Azure portal, click on a log entry to see the detailed events inside it.</span></span>

  ![Azure Portal 선택 세부 정보](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-131">거기에서 해당 이벤트를 클릭하면 **세부 정보** 블레이드를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-131">From there, you can open the **Detail** blade by clicking on the event.</span></span>

  ![Azure Portal 선택 세부 정보](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="bcabf-133">실패한 작업 디버그</span><span class="sxs-lookup"><span data-stu-id="bcabf-133">Debug a failed job</span></span>
<span data-ttu-id="bcabf-134">Azure 관리 포털에서 검색 아이콘을 클릭하고 '실패'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-134">In the Azure Management portal, click on the Search icon and type ‘failed’.</span></span> <span data-ttu-id="bcabf-135">오류가 있는 모든 로그의 결과가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-135">This gives a result of all logs with failures.</span></span> 

  ![실패한 작업 디버그](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-137">Azure Portal에서 메시지 수준을 필터링하여 **위험** 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-137">In the Azure portal, you can filter by level of message to view **Critical** events.</span></span>

  ![Azure Portal 디버그](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-139">오류 중 하나를 선택하고 **세부 정보** 를 클릭하면 오류에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-139">You can select any one of the failures, and click on the **Details** for more information on the error.</span></span>  <span data-ttu-id="bcabf-140">일부 오류 메시지는 문제를 완화시키는 방법에 대한 정보도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bcabf-140">Some error messages also provide information about how to mitigate the issue.</span></span> 

  ![작업 세부 정보](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="bcabf-142">[지원](https://azure.microsoft.com/support/options/)에 문의하거나 [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 통해 팀에 정보를 제공해야 하는 경우 작업 세부 정보, 특히 **상관관계 ID**를 적어 두세요.</span><span class="sxs-lookup"><span data-stu-id="bcabf-142">In case you need to contact [Support](https://azure.microsoft.com/support/options/) or provide information to the team via the [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note the Operation Details, specifically the **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="bcabf-143">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="bcabf-143">Get help</span></span>
<span data-ttu-id="bcabf-144">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bcabf-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcabf-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bcabf-145">Next steps</span></span>
* [<span data-ttu-id="bcabf-146">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="bcabf-146">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bcabf-147">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="bcabf-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bcabf-148">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="bcabf-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bcabf-149">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="bcabf-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bcabf-150">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="bcabf-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

