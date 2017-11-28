---
title: "스트림 분석에서 쿼리에 대 한 경고를 aaaSet | Microsoft Docs"
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
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="497f8-104">Azure Stream Analytics 작업에 대한 경고 설정</span><span class="sxs-lookup"><span data-stu-id="497f8-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="497f8-105">소개: 모니터 페이지</span><span class="sxs-lookup"><span data-stu-id="497f8-105">Introduction: Monitor page</span></span>
<span data-ttu-id="497f8-106">설정할 수 있습니다 경고 tootrigger 경고 메트릭을 사용자가 지정한 조건에 도달 하면 합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="497f8-107">예를 들어 hello 다음과 같은 조건에 대 한 경고를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="497f8-108">규칙 기준 hello 포털을 통해에 설정할 수 있습니다 또는 구성할 수 있습니다 [프로그래밍 방식으로](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) 작업 로그 데이터에 대해 합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="497f8-109">Hello Azure 포털에서에서 경고를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="497f8-110">Hello Azure 포털에서에서 toocreate에 대 한 경고를 원하는 hello 스트림 분석 작업을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="497f8-111">Hello에 **작업** 블레이드에서 hello 클릭 **모니터링** 섹션.</span><span class="sxs-lookup"><span data-stu-id="497f8-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="497f8-112">Hello에 **메트릭을** 블레이드에서 hello 클릭 **추가 경고** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Azure Portal 설치](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="497f8-114">이름과 설명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="497f8-115">hello 아래에서 경고를 전송 하는 hello 선택기 toodefine hello 조건을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="497f8-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="497f8-116">Hello 경고 이동 해야 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-116">Provide information about where hello alert should go.</span></span>

      ![Azure Streaming Analytics 작업에 대한 경고 설정](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="497f8-118">Hello Azure 포털에에서 경고를 구성 하는 방법에 자세한 세부 정보를 참조 하십시오. [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="497f8-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="497f8-119">도움말 보기</span><span class="sxs-lookup"><span data-stu-id="497f8-119">Get help</span></span>
<span data-ttu-id="497f8-120">추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="497f8-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="497f8-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="497f8-121">Next steps</span></span>
* [<span data-ttu-id="497f8-122">스트림 분석 소개 tooAzure</span><span class="sxs-lookup"><span data-stu-id="497f8-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="497f8-123">Azure Stream Analytics 사용 시작</span><span class="sxs-lookup"><span data-stu-id="497f8-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="497f8-124">Azure  Stream Analytics 작업 규모 지정</span><span class="sxs-lookup"><span data-stu-id="497f8-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="497f8-125">Azure  Stream Analytics 쿼리 언어 참조</span><span class="sxs-lookup"><span data-stu-id="497f8-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="497f8-126">Azure Stream Analytics 관리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="497f8-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

