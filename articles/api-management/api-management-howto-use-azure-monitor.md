---
title: "aaaMonitor Azure 모니터를 사용 하 여 API 관리 | Microsoft Docs"
description: "Azure 모니터를 사용 하 여 Azure API 관리 toomonitor을 서비스 하는 방법에 대해 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="7a4a3-103">Azure Monitor를 사용하여 API Management 모니터링</span><span class="sxs-lookup"><span data-stu-id="7a4a3-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="7a4a3-104">Azure Monitor는 모든 Azure 리소스 모니터링을 위한 단일 소스를 제공하는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="7a4a3-105">Azure 모니터를 사용 시각화, 쿼리, 경로, 보관 하 고 수 hello 메트릭 및 API 관리와 같은 Azure 리소스에서 오는 로그 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on hello metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="7a4a3-106">비디오 표시 방법을 따르는 hello toomonitor Azure 모니터를 사용 하 여 API 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-106">hello following video shows how toomonitor API Management using Azure Monitor.</span></span> <span data-ttu-id="7a4a3-107">Azure Monitor에 대한 자세한 내용은 [Azure Monitor 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="7a4a3-108">메트릭</span><span class="sxs-lookup"><span data-stu-id="7a4a3-108">Metrics</span></span>
<span data-ttu-id="7a4a3-109">API 관리에는 현재 5 개의 메트릭을 내보내는 이며 tooadd hello 향후에 더 많은 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-109">API Management currently emits five metrics and we plan tooadd more in hello future.</span></span> <span data-ttu-id="7a4a3-110">이러한 메트릭을 내보내지는 1 분 마다 근처 hello 상태 및 Api의 상태에 대 한 실시간 가시성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-110">These metrics are emitted every minute, giving you near real-time visibility into hello state and health of your APIs.</span></span> <span data-ttu-id="7a4a3-111">다음은 hello 메트릭에 대 한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-111">Following is a summary of hello metrics:</span></span>
* <span data-ttu-id="7a4a3-112">게이트웨이 요청 합계: hello 기간에는 요청을 API hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-112">Total Gateway Requests: hello number of API requests in hello period.</span></span> 
* <span data-ttu-id="7a4a3-113">304, 등 307 301 (예: 200) 보다 작은 대상 성공 HTTP 응답 코드를 받은 API 요청의 성공 게이트웨이 요청: hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-113">Successful Gateway Requests: hello number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="7a4a3-114">실패 한 요청 수 게이트웨이: hello API 요청 수를 잘못 된 HTTP 응답 코드 400 및 500 보다 큰 모든 항목을 포함 하 여 받은입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-114">Failed Gateway Requests: hello number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="7a4a3-115">받은 HTTP 응답 코드 401, 403, 및 429를 포함 하 여 API 요청 인증 되지 않은 게이트웨이 요청 수: hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-115">Unauthorized Gateway Requests: hello number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="7a4a3-116">API 요청 받은 HTTP 응답 코드의 앞에 범주 (예를 들어 418) hello tooany에 속하지 않는 다른 게이트웨이 요청: hello 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-116">Other Gateway Requests: hello number of API requests that received HTTP response codes that do not belong tooany of hello preceding categories (for example, 418).</span></span>

<span data-ttu-id="7a4a3-117">API Management 서비스에서 메트릭에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 메트릭에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="7a4a3-118">API 관리 서비스에서 tooview 메트릭:</span><span class="sxs-lookup"><span data-stu-id="7a4a3-118">tooview metrics in your API Management service:</span></span>
1. <span data-ttu-id="7a4a3-119">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-119">Open hello Azure portal.</span></span>
2. <span data-ttu-id="7a4a3-120">Tooyour API 관리 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-120">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="7a4a3-121">**메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-121">Click **Metrics**.</span></span>

![메트릭 블레이드][metrics-blade]

<span data-ttu-id="7a4a3-123">방법에 대 한 자세한 정보에 대 한 메트릭, toouse 참조 [메트릭 개요]합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-123">For more information about how toouse Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="7a4a3-124">활동 로그</span><span class="sxs-lookup"><span data-stu-id="7a4a3-124">Activity Logs</span></span>
<span data-ttu-id="7a4a3-125">활동 로그 API 관리 서비스에서 수행 된 hello 작업에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-125">Activity logs provide insight into hello operations that were performed on your API Management services.</span></span> <span data-ttu-id="7a4a3-126">이전에는 이러한 로그를 "감사 로그" 또는 "작업 로그"라고도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="7a4a3-127">작업 로그를 사용 하 여 hello 확인할 수 있습니다 "부분, who, 시기 및" 모든 쓰기 작업 (PUT, POST, DELETE) API 관리 서비스에 대해 수행에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-127">Using activity logs, you can determine hello "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="7a4a3-128">읽기 (GET) 작업이 나에서 수행 된 작업 활동 로그를 포함 하지 않는 hello 클래식 게시자 포털 또는 관리 Api를 원래 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-128">Activity logs do not include read (GET) operations or operations performed in hello classic Publisher Portal or using hello original Management APIs.</span></span>

<span data-ttu-id="7a4a3-129">API Management 서비스에서 활동 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="7a4a3-130">API 관리 서비스에서 tooview 활동 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-130">tooview activity logs in your API Management service:</span></span>
1. <span data-ttu-id="7a4a3-131">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-131">Open hello Azure portal.</span></span>
2. <span data-ttu-id="7a4a3-132">Tooyour API 관리 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-132">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="7a4a3-133">**활동 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-133">Click **Activity log**.</span></span>

![활동 로그 블레이드][activity-logs-blade]

<span data-ttu-id="7a4a3-135">방법에 대 한 자세한 내용은 toouse 메트릭 참조 [활동 로그 개요]합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-135">For more information about how toouse Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="7a4a3-136">경고</span><span class="sxs-lookup"><span data-stu-id="7a4a3-136">Alerts</span></span>
<span data-ttu-id="7a4a3-137">메트릭 및 활동 로그를 기반으로 하는 tooreceive 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-137">You can configure tooreceive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="7a4a3-138">Azure 모니터 표시할 때을 다음 경고 toodo hello tooconfigure가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-138">Azure Monitor allows you tooconfigure an alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="7a4a3-139">전자 메일 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="7a4a3-139">Send an email notification</span></span>
* <span data-ttu-id="7a4a3-140">웹후크 호출</span><span class="sxs-lookup"><span data-stu-id="7a4a3-140">Call a webhook</span></span>
* <span data-ttu-id="7a4a3-141">Azure 논리 앱 호출</span><span class="sxs-lookup"><span data-stu-id="7a4a3-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="7a4a3-142">API Management 서비스 또는 Azure Monitor에서 경고 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="7a4a3-143">tooconfigure API 관리에서 해당:</span><span class="sxs-lookup"><span data-stu-id="7a4a3-143">tooconfigure them in API Management:</span></span> 
1. <span data-ttu-id="7a4a3-144">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-144">Open hello Azure portal.</span></span>
2. <span data-ttu-id="7a4a3-145">Tooyour API 관리 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-145">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="7a4a3-146">**경고 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-146">Click **Alert rules**.</span></span>

![경고 규칙 블레이드][alert-rules-blade]

<span data-ttu-id="7a4a3-148">경고 사용에 대한 자세한 내용은 [경고 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="7a4a3-149">진단 로그</span><span class="sxs-lookup"><span data-stu-id="7a4a3-149">Diagnostic Logs</span></span>
<span data-ttu-id="7a4a3-150">진단 로그는 감사 뿐만 아니라 문제 해결에 중요한 작업 및 오류에 대한 풍부한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="7a4a3-151">진단 로그는 활동 로그와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="7a4a3-152">작업 로그는 Azure 리소스에서 수행 된 hello 작업에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-152">Activity logs provide insights into hello operations that were performed on your Azure resources.</span></span> <span data-ttu-id="7a4a3-153">진단 로그는 리소스 자체에서 수행하는 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="7a4a3-154">API 관리에는 현재 진단을 제공 hello 구조를 다음 있는 각 항목에 개별 API에 대 한 로그 (매시간 일괄 처리) 요청:</span><span class="sxs-lookup"><span data-stu-id="7a4a3-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having hello following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="7a4a3-155">API Management 서비스에서 진단 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="7a4a3-156">API 관리 서비스에서 진단 로그 tooview:</span><span class="sxs-lookup"><span data-stu-id="7a4a3-156">tooview diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="7a4a3-157">Azure 포털 hello를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-157">Open hello Azure portal.</span></span>
2. <span data-ttu-id="7a4a3-158">Tooyour API 관리 서비스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-158">Go tooyour API Management service.</span></span>
3. <span data-ttu-id="7a4a3-159">**진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-159">Click **Diagnostic log**.</span></span>

![진단 로그 블레이드][diagnostic-logs-blade]

<span data-ttu-id="7a4a3-161">방법에 대 한 자세한 정보에 대 한 메트릭, toouse 참조 [진단 로그의 개요]합니다.</span><span class="sxs-lookup"><span data-stu-id="7a4a3-161">For more information about how toouse Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="7a4a3-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a4a3-162">Next Step</span></span>

* <span data-ttu-id="7a4a3-163">[Azure Monitor 시작]</span><span class="sxs-lookup"><span data-stu-id="7a4a3-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="7a4a3-164">[메트릭 개요]</span><span class="sxs-lookup"><span data-stu-id="7a4a3-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="7a4a3-165">[활동 로그 개요]</span><span class="sxs-lookup"><span data-stu-id="7a4a3-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="7a4a3-166">[진단 로그의 개요]</span><span class="sxs-lookup"><span data-stu-id="7a4a3-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="7a4a3-167">[경고 개요]</span><span class="sxs-lookup"><span data-stu-id="7a4a3-167">[Overview of Alerts]</span></span>

[Azure Monitor 시작]: ../monitoring-and-diagnostics/monitoring-get-started.md
[메트릭 개요]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[활동 로그 개요]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[진단 로그의 개요]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[경고 개요]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
