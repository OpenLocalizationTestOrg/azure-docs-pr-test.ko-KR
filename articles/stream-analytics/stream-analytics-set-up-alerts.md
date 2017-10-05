---
title: "Stream Analytics에서 쿼리에 대한 경고 설정 | Microsoft Docs"
description: "Stream Analytics 경고 이해"
keywords: "경고 설정"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 75b1b256eea7295f5a464996e2f34ae301c715fd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="27d38-104">Azure Stream Analytics 작업에 대한 경고 설정</span><span class="sxs-lookup"><span data-stu-id="27d38-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="27d38-105">소개: 모니터 페이지</span><span class="sxs-lookup"><span data-stu-id="27d38-105">Introduction: Monitor page</span></span>
<span data-ttu-id="27d38-106">메트릭이 지정한 조건에 도달하면 경고를 트리거하도록 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-106">You can set up alerts to trigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="27d38-107">예를 들어 다음과 같은 조건에 대한 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-107">For example, you might set up an alert for a condition like the following:</span></span>

`If there are zero input events in the last 5 minutes, send email notification to sa-admin@example.com`

<span data-ttu-id="27d38-108">포털을 통해 메트릭에 대한 규칙을 설정하거나 [프로그래밍 방식](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a)으로 작업 로그 데이터에 대한 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-108">Rules can be set up on metrics through the portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-the-azure-portal"></a><span data-ttu-id="27d38-109">Azure Portal에서 경고 설정</span><span class="sxs-lookup"><span data-stu-id="27d38-109">Set up alerts in the Azure portal</span></span>
1. <span data-ttu-id="27d38-110">Azure Portal에서 경고를 만들려는 Stream Analytics 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-110">In the Azure portal, open the Stream Analytics job you want to create an alert for.</span></span> 

2. <span data-ttu-id="27d38-111">**작업** 블레이드에서 **모니터링** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-111">In the **Job** blade, click the **Monitoring** section.</span></span>  

3. <span data-ttu-id="27d38-112">**메트릭** 블레이드에서 **경고 추가** 명령을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-112">In the **Metric** blade, click the **Add alert** command.</span></span>

      ![Azure Portal 설치](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="27d38-114">이름과 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="27d38-115">경고가 전송될 조건을 정의하는 데 선택기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-115">Use the selectors to define the condition under which the alert will be sent.</span></span>

6. <span data-ttu-id="27d38-116">경고를 전달할 위치에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27d38-116">Provide information about where the alert should go.</span></span>

      ![Azure Streaming Analytics 작업에 대한 경고 설정](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="27d38-118">Azure Portal에서 경고를 구성에 대한 자세한 내용은 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27d38-118">For more detail on configuring alerts in the Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="27d38-119">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="27d38-119">Get help</span></span>
<span data-ttu-id="27d38-120">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="27d38-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="27d38-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27d38-121">Next steps</span></span>
* [<span data-ttu-id="27d38-122">Azure Stream Analytics 소개</span><span class="sxs-lookup"><span data-stu-id="27d38-122">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="27d38-123">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="27d38-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="27d38-124">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="27d38-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="27d38-125">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="27d38-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="27d38-126">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="27d38-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

