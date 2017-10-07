---
title: "aaaMonitor B2B 트랜잭션 로깅-Azure 논리 앱을 설정 하 고 | Microsoft Docs"
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
ms.openlocfilehash: a6745ebf41aab331020bfec072f5806711d125bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-set-up-diagnostics-logging-for-b2b-communication-in-integration-accounts"></a><span data-ttu-id="52382-103">통합 계정에서 B2B 통신에 대한 진단 로깅 모니터링 및 설정</span><span class="sxs-lookup"><span data-stu-id="52382-103">Monitor and set up diagnostics logging for B2B communication in integration accounts</span></span>

<span data-ttu-id="52382-104">통합 계정을 통해 실행 중인 두 비즈니스 프로세스 또는 응용 프로그램 간의 B2B 통신을 설정한 후 해당 엔터티는 서로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52382-104">After you set up B2B communication between two running business processes or applications through your integration account, those entities can exchange messages with each other.</span></span> <span data-ttu-id="52382-105">tooconfirm이이 통신 예상 대로 작동 하는지, AS2, X12에 대 한 모니터링을 설정할 수 그리고 hello 통해 통합 계정에 대 한 진단 로깅을 함께 EDIFACT 메시지 [Azure 로그 분석](../log-analytics/log-analytics-overview.md) 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-105">tooconfirm this communication works as expected, you can set up monitoring for AS2, X12, and EDIFACT messages, along with diagnostics logging for your integration account through hello [Azure Log Analytics](../log-analytics/log-analytics-overview.md) service.</span></span> <span data-ttu-id="52382-106">[OMS(Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md)의 이 서비스는 해당 가용성 및 성능을 유지할 수 있도록 클라우드 및 온-프레미스 환경을 모니터링하고 런타임 세부 정보 및 보다 풍부한 디버깅에 대한 이벤트를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-106">This service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) monitors your cloud and on-premises environments, helping you maintain their availability and performance, and also collects runtime details and events for richer debugging.</span></span> <span data-ttu-id="52382-107">또한 Azure Storage 및 Azure Event Hub와 같은 [다른 서비스와 함께 진단 데이터를 사용](#extend-diagnostic-data)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52382-107">You can also [use your diagnostic data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span>

## <a name="requirements"></a><span data-ttu-id="52382-108">요구 사항</span><span class="sxs-lookup"><span data-stu-id="52382-108">Requirements</span></span>

* <span data-ttu-id="52382-109">진단 로깅과 함께 설정된 논리 앱.</span><span class="sxs-lookup"><span data-stu-id="52382-109">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="52382-110">자세한 내용은 [어떻게 해당 논리 앱에 대 한 로깅을 tooset](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-110">Learn [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

  > [!NOTE]
  > <span data-ttu-id="52382-111">이 요구 사항은 충족, 수 있게 hello에 대 한 작업 영역 [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-111">After you've met this requirement, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="52382-112">사용 해야 통합 계정에 대 한 로깅을 설정 하는 경우 동일한 OMS 작업 영역을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-112">You should use hello same OMS workspace when you set up logging for your integration account.</span></span> <span data-ttu-id="52382-113">OMS 작업 영역에 없을 경우에 대해 배울 [어떻게 toocreate OMS 작업 영역](../log-analytics/log-analytics-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-113">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

* <span data-ttu-id="52382-114">통합 계정 tooyour 논리 앱 연결 된입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-114">An integration account that's linked tooyour logic app.</span></span> <span data-ttu-id="52382-115">자세한 내용은 [toocreate 통합 링크 tooyour 논리 앱 계정을 어떻게](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-115">Learn [how toocreate an integration account with a link tooyour logic app](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span></span>

## <a name="turn-on-diagnostics-logging-for-your-integration-account"></a><span data-ttu-id="52382-116">통합 계정에 대한 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="52382-116">Turn on diagnostics logging for your integration account</span></span>

<span data-ttu-id="52382-117">통합 계정에서 직접 로깅을 설정할 수 있습니다 또는 [hello Azure 모니터 서비스를 통해](#azure-monitor-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-117">You can turn on logging either directly from your integration account or [through hello Azure Monitor service](#azure-monitor-service).</span></span> <span data-ttu-id="52382-118">Azure Monitor는 인프라 수준의 데이터와 함께 기본 모니터링을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-118">Azure Monitor provides basic monitoring with infrastructure-level data.</span></span> <span data-ttu-id="52382-119">[Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="52382-119">Learn more about [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md).</span></span>

### <a name="turn-on-diagnostics-logging-directly-from-your-integration-account"></a><span data-ttu-id="52382-120">통합 계정에서 직접 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="52382-120">Turn on diagnostics logging directly from your integration account</span></span>

1. <span data-ttu-id="52382-121">Hello에 [Azure 포털](https://portal.azure.com)찾아 통합 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-121">In hello [Azure portal](https://portal.azure.com), find and select your integration account.</span></span> <span data-ttu-id="52382-122">**모니터링** 아래에서 다음과 같이 **진단 로그**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-122">Under **Monitoring**, choose **Diagnostics logs** as shown here:</span></span>

   ![통합 계정을 찾고 선택하고 "진단 로그"를 선택합니다.](media/logic-apps-monitor-b2b-message/integration-account-diagnostics.png)

2. <span data-ttu-id="52382-124">통합 계정을 선택한 후 다음 값에는 hello 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52382-124">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="52382-125">이러한 값이 올바르면 **진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-125">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="52382-126">그렇지 않으면 hello 원하는 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-126">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="52382-127">아래 **구독**, 선택 hello 통합 계정에 사용할 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="52382-127">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="52382-128">아래 **리소스 그룹**선택, 통합 계정으로 사용 하는 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-128">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="52382-129">**리소스 종류** 아래에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-129">Under **Resource type**, select **Integration accounts**.</span></span> 
   4. <span data-ttu-id="52382-130">**리소스** 아래에서 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-130">Under **Resource**, select your integration account.</span></span> 
   5. <span data-ttu-id="52382-131">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-131">Choose **Turn on diagnostics**.</span></span>

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="52382-133">**진단 설정**, **상태** 아래에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-133">Under **Diagnostics settings**, and then **Status**, choose **On**.</span></span>

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="52382-135">표시 된 것 처럼 이제 로깅에 대 한 hello OMS 작업 영역 및 데이터 toouse를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-135">Now select hello OMS workspace and data toouse for logging as shown:</span></span>

   1. <span data-ttu-id="52382-136">선택 **tooLog 분석 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-136">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="52382-137">**Log Analytics** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-137">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="52382-138">아래 **OMS 작업 영역**를 로깅에 대 한 OMS 작업 영역 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-138">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="52382-139">아래 **로그**선택, hello **IntegrationAccountTrackingEvents** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-139">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="52382-140">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-140">Choose **Save**.</span></span>

   ![진단 데이터 tooa 로그를 보낼 수 있도록 로그 분석 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="52382-142">이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-142">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

<a name="azure-monitor-service"></a>

### <a name="turn-on-diagnostics-logging-through-azure-monitor"></a><span data-ttu-id="52382-143">Azure Monitor를 통해 진단 로깅 켜기</span><span class="sxs-lookup"><span data-stu-id="52382-143">Turn on diagnostics logging through Azure Monitor</span></span>

1. <span data-ttu-id="52382-144">Hello에 [Azure 포털](https://portal.azure.com), 주요 Azure 메뉴 hello, 선택 **모니터**, **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-144">In hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **Monitor**, **Diagnostics logs**.</span></span> <span data-ttu-id="52382-145">그런 다음 다음과 같이 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-145">Then select your integration account as shown here:</span></span>

   !["모니터링", "진단 로그"를 선택하고 통합 계정을 선택합니다.](media/logic-apps-monitor-b2b-message/monitor-service-diagnostics-logs.png)

2. <span data-ttu-id="52382-147">통합 계정을 선택한 후 다음 값에는 hello 자동으로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52382-147">After you select your integration account, hello following values are automatically selected.</span></span> <span data-ttu-id="52382-148">이러한 값이 올바르면 **진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-148">If these values are correct, choose **Turn on diagnostics**.</span></span> <span data-ttu-id="52382-149">그렇지 않으면 hello 원하는 값을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-149">Otherwise, select hello values that you want:</span></span>

   1. <span data-ttu-id="52382-150">아래 **구독**, 선택 hello 통합 계정에 사용할 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="52382-150">Under **Subscription**, select hello Azure subscription that you use with your integration account.</span></span>
   2. <span data-ttu-id="52382-151">아래 **리소스 그룹**선택, 통합 계정으로 사용 하는 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-151">Under **Resource group**, select hello resource group that you use with your integration account.</span></span>
   3. <span data-ttu-id="52382-152">**리소스 종류** 아래에서 **통합 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-152">Under **Resource type**, select **Integration accounts**.</span></span>
   4. <span data-ttu-id="52382-153">**리소스** 아래에서 통합 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-153">Under **Resource**, select your integration account.</span></span>
   5. <span data-ttu-id="52382-154">**진단 켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-154">Choose **Turn on diagnostics**.</span></span>

   ![통합 계정에 대한 진단 설정](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account.png)

3. <span data-ttu-id="52382-156">**진단 설정** 아래에서 **켜기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-156">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Azure 진단 켜기](media/logic-apps-monitor-b2b-message/turn-on-diagnostics-integration-account-2.png)

4. <span data-ttu-id="52382-158">표시 된 것 처럼 이제 로깅에 대 한 hello OMS 작업 영역 및 이벤트 범주를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-158">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="52382-159">선택 **tooLog 분석 보내기**합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-159">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="52382-160">**Log Analytics** 아래에서 **구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-160">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="52382-161">아래 **OMS 작업 영역**를 로깅에 대 한 OMS 작업 영역 toouse hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-161">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="52382-162">아래 **로그**선택, hello **IntegrationAccountTrackingEvents** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="52382-162">Under **Log**, select hello **IntegrationAccountTrackingEvents** category.</span></span>
   5. <span data-ttu-id="52382-163">완료하면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-163">When you're done, choose **Save**.</span></span>

   ![진단 데이터 tooa 로그를 보낼 수 있도록 로그 분석 설정](media/logic-apps-monitor-b2b-message/send-diagnostics-data-log-analytics-workspace.png)

5. <span data-ttu-id="52382-165">이제 [OMS에서 B2B 메시지에 대한 추적을 설정](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-165">Now [set up tracking for your B2B messages in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="52382-166">다른 서비스와 함께 진단 데이터를 사용하는 방법 및 위치 확장</span><span class="sxs-lookup"><span data-stu-id="52382-166">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="52382-167">Azure Log Analytics와 마찬가지로 다른 Azure 서비스와 함께 논리 앱의 진단 데이터를 사용하는 방법을 다음과 같이 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52382-167">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="52382-168">Azure Storage에 Azure 진단 로그 보관</span><span class="sxs-lookup"><span data-stu-id="52382-168">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="52382-169">Azure 진단 로그 tooAzure 스트림 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="52382-169">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="52382-170">그런 다음 [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) 및 [Power BI](../log-analytics/log-analytics-powerbi.md)와 같은 다른 서비스의 원격 분석 및 분석을 사용하여 실시간으로 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52382-170">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="52382-171">예:</span><span class="sxs-lookup"><span data-stu-id="52382-171">For example:</span></span>

* [<span data-ttu-id="52382-172">이벤트 허브 tooStream 분석에서에서 스트림 데이터</span><span class="sxs-lookup"><span data-stu-id="52382-172">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="52382-173">Stream Analytics를 사용하여 스트리밍 데이터 분석 및 Power BI에서 실시간 분석 대시보드 만들기</span><span class="sxs-lookup"><span data-stu-id="52382-173">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="52382-174">Hello 원하는 옵션을 설정에 따라, 다음 사항을 확인 하면 첫 번째 [Azure 저장소 계정 만들기](../storage/common/storage-create-storage-account.md) 또는 [Azure 이벤트 허브 만들기](../event-hubs/event-hubs-create.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-174">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="52382-175">Toosend 진단 데이터에 대 한 hello 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-175">Then select hello options for where you want toosend diagnostic data:</span></span>

![데이터는 저장소 계정 또는 이벤트 허브를 tooAzure 보내기](./media/logic-apps-monitor-b2b-message/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="52382-177">보존 기간 toouse 저장소 계정을 선택 하는 경우에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52382-177">Retention periods apply only when you choose toouse a storage account.</span></span>

## <a name="supported-tracking-schemas"></a><span data-ttu-id="52382-178">지원되는 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="52382-178">Supported tracking schemas</span></span>

<span data-ttu-id="52382-179">Azure는 사용자 지정 유형을 hello 점을 제외 하 고 스키마를 해결 했습니다. 스키마 형식 추적을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="52382-179">Azure supports these tracking schema types, which all have fixed schemas except hello Custom type.</span></span>

* [<span data-ttu-id="52382-180">AS2 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="52382-180">AS2 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="52382-181">X12 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="52382-181">X12 tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="52382-182">사용자 지정 추적 스키마</span><span class="sxs-lookup"><span data-stu-id="52382-182">Custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="52382-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="52382-183">Next steps</span></span>

* [<span data-ttu-id="52382-184">OMS에서 B2B 메시지 추적</span><span class="sxs-lookup"><span data-stu-id="52382-184">Track B2B messages in OMS</span></span>](../logic-apps/logic-apps-track-b2b-messages-omsportal.md "OMS에서 B2B 메시지 추적")
* [<span data-ttu-id="52382-185">엔터프라이즈 통합 팩 hello에 대 한 자세한</span><span class="sxs-lookup"><span data-stu-id="52382-185">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")

