---
title: "B2B 트랜잭션 모니터링 및 로깅 설정 - Azure Logic Apps | Microsoft Docs"
description: "AS2, X12 및 EDIFACT 메시지 모니터링, 통합 계정에 대한 진단 로깅 시작"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f717dae9a70a96944b623f22b90cf8c5a943f382
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="94214-103">통합 계정에서 B2B 통신에 대한 진단 로깅 모니터링 및 설정</span><span class="sxs-lookup"><span data-stu-id="94214-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="94214-104">통합 계정을 통해 실행 중인 두 비즈니스 프로세스 또는 응용 프로그램 간의 B2B 통신을 설정한 후 해당 엔터티는 서로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="94214-105">이 통신이 예상대로 작동하는지 확인하기 위해 [Azure Log Analytics](../log-analytics/log-analytics-overview.md) 서비스를 통해 통합 계정에 대한 진단 로깅과 함께 AS2, X12 및 EDIFACT 메시지에 대한 모니터링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-105">To confirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through the [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="94214-106">[OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)의 이 서비스는 해당 가용성 및 성능을 유지할 수 있도록 클라우드 및 온-프레미스 환경을 모니터링하고 런타임 세부 정보 및 보다 풍부한 디버깅에 대한 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="94214-107">또한 Azure Storage 및 Azure Event Hub와 같은 [다른 서비스와 함께 진단 데이터를 사용](#extend-diagnostic-data)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="94214-108">요구 사항</span><span class="sxs-lookup"><span data-stu-id="94214-108">Requirements</span></span>

* <span data-ttu-id="94214-109">진단 로깅과 함께 설정된 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="94214-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="94214-110">[해당 논리 앱에 대한 로깅을 설정하는 방법](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94214-110">Learn [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="94214-111">이 요구 사항을 충족한 후 [OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)에 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-111">After you've met this requirement, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="94214-112">통합 계정에 대한 로깅을 설정할 때와 동일한 OMS 작업 영역을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-112">You should use the same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="94214-113">OMS 작업 영역이 없는 경우 [OMS 작업 영역을 만드는 방법](../log-analytics/log-analytics-get-started.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94214-113">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="94214-114">논리 앱에 연결된 통합 계정.</span><span class="sxs-lookup"><span data-stu-id="94214-114">An integration account that's linked to your logic app.</span></span> <span data-ttu-id="94214-115">[논리 앱에 대한 링크와 함께 통합 계정을 만드는 방법](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94214-115">Learn [how to create an integration account with a link to your logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="94214-116">통합 계정에 대한 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="94214-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="94214-117">통합 계정에서 직접 또는 [Azure Monitor 서비스를 통해](#azure-monitor-service) 로깅을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-117">You can turn on logging either directly from your integration account or [through the Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="94214-118">Azure Monitor는 인프라 수준의 데이터와 함께 기본 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="94214-119">[Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94214-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="94214-120">통합 계정에서 직접 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="94214-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="94214-121">[Azure Portal](https://portal.azure.com)에서 통합 계정을 찾고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-121">In the [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="94214-122">**모니터링** 아래에서 다음과 같이 **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![통합 계정을 찾고 선택하고 "진단 로그"를 선택합니다.](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="94214-124">통합 계정을 선택하면 다음 값이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="94214-124">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="94214-125">이러한 값이 올바르면 **진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="94214-126">그렇지 않은 경우 원하는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-126">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="94214-127">**구독** 아래에서 통합 계정과 함께 사용하는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-127">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="94214-128">**리소스 그룹** 아래에서 통합 계정과 함께 사용하는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-128">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="94214-129">**리소스 종류** 아래에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="94214-130">**리소스** 아래에서 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="94214-131">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-131">Choose **Turn on diagnostics**.</span></span>

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="94214-133">**진단 설정**, **상태** 아래에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="94214-135">이제 표시된 것처럼 로깅에 사용할 OMS 작업 영역 및 데이터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-135">Now select the OMS workspace and data to use for logging as shown:</span></span>

   1. <span data-ttu-id="94214-136">**Log Analytics에 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-136">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="94214-137">**Log Analytics** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="94214-138">**OMS 작업 영역** 아래에서 로깅에 사용할 OMS 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-138">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="94214-139">**로그** 아래에서 **IntegrationAccountTrackingEvents** 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-139">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="94214-140">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-140">Choose **Save**.</span></span>

   ![로그에 진단 데이터를 보낼 수 있도록 Log Analytics 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="94214-142">이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="94214-143">Azure Monitor를 통해 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="94214-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="94214-144">[Azure Portal](https://portal.azure.com)의 주요 Azure 메뉴에서 **모니터링**, **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-144">In the [Azure portal](https://portal.azure.com), on the main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="94214-145">그런 다음 다음과 같이 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-145">Then select your integration account as shown here:</span></span>

   !["모니터링", "진단 로그"를 선택하고 통합 계정을 선택합니다.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="94214-147">통합 계정을 선택하면 다음 값이 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="94214-147">After you select your integration account, the following values are automatically selected.</span></span> <span data-ttu-id="94214-148">이러한 값이 올바르면 **진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="94214-149">그렇지 않은 경우 원하는 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-149">Otherwise, select the values that you want:</span></span>

   1. <span data-ttu-id="94214-150">**구독** 아래에서 통합 계정과 함께 사용하는 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-150">Under **Subscription**, select the Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="94214-151">**리소스 그룹** 아래에서 통합 계정과 함께 사용하는 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-151">Under **Resource group**, select the resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="94214-152">**리소스 종류** 아래에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="94214-153">**리소스** 아래에서 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="94214-154">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-154">Choose **Turn on diagnostics**.</span></span>

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="94214-156">**진단 설정** 아래에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="94214-158">이제 표시된 것처럼 로깅에 대한 OMS 작업 영역 및 이벤트 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-158">Now select the OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="94214-159">**Log Analytics에 보내기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-159">Select **Send to Log Analytics**.</span></span> 
   2. <span data-ttu-id="94214-160">**Log Analytics** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="94214-161">**OMS 작업 영역** 아래에서 로깅에 사용할 OMS 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-161">Under **OMS Workspaces**, select the OMS workspace to use for logging.</span></span>
   4. <span data-ttu-id="94214-162">**로그** 아래에서 **IntegrationAccountTrackingEvents** 범주를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-162">Under **Log**, select the **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="94214-163">완료하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-163">When you're done, choose **Save**.</span></span>

   ![로그에 진단 데이터를 보낼 수 있도록 Log Analytics 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="94214-165">이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="94214-166">다른 서비스와 함께 진단 데이터를 사용하는 방법 및 위치 확장</span><span class="sxs-lookup"><span data-stu-id="94214-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="94214-167">Azure Log Analytics와 마찬가지로 다른 Azure 서비스와 함께 논리 앱의 진단 데이터를 사용하는 방법을 다음과 같이 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="94214-168">Azure Storage에 Azure 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="94214-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="94214-169">Azure Event Hub로 Azure 진단 로그 스트림</span><span class="sxs-lookup"><span data-stu-id="94214-169">Stream Azure Diagnostics Logs to Azure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="94214-170">그런 다음 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 및 [Power BI](../log-analytics/log-analytics-powerbi.md)와 같은 다른 서비스의 원격 분석 및 분석을 사용하여 실시간으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94214-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="94214-171">예:</span><span class="sxs-lookup"><span data-stu-id="94214-171">For example:</span></span>

* [<span data-ttu-id="94214-172">Event Hub에서 Stream Analytics로 데이터 스트림</span><span class="sxs-lookup"><span data-stu-id="94214-172">Stream data from Event Hubs to Stream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="94214-173">Stream Analytics를 사용하여 스트리밍 데이터 분석 및 Power BI에서 실시간 분석 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="94214-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="94214-174">설정하려는 옵션에 따라 먼저 [Azure 저장소 계정을 만들](../storage/common/storage-create-storage-account.md)거나 [Azure 이벤트 허브를 만들](../event-hubs/event-hubs-create.md)어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-174">Based on the options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="94214-175">그런 다음 진단 데이터를 전송하려는 위치에 대한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-175">Then select the options for where you want to send diagnostic data:</span></span>

![Azure 저장소 계정 또는 이벤트 허브로 데이터 보내기](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="94214-177">보존 기간은 저장소 계정을 사용하도록 선택한 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="94214-177">Retention periods apply only when you choose to use a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="94214-178">지원되는 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="94214-178">Supported tracking schemas</span></span>

<span data-ttu-id="94214-179">Azure는 이러한 추적 스키마 형식을 지원하며 사용자 지정 유형을 제외한 고정된 스키마를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="94214-179">Azure supports these tracking schema types, which all have fixed schemas except the Custom type.</span></span>

* [<span data-ttu-id="94214-180">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="94214-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="94214-181">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="94214-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="94214-182">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="94214-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="94214-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="94214-183">Next steps</span></span>

* [<span data-ttu-id="94214-184">OMS에서 B2B 메시지 추적</span><span class="sxs-lookup"><span data-stu-id="94214-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "OMS에서 B2B 메시지 추적")
* [<span data-ttu-id="94214-185">엔터프라이즈 통합 팩에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="94214-185">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대해 알아보기")

