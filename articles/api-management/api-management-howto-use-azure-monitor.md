---
title: "Azure Monitor를 사용하여 API Management 모니터링 | Microsoft Docs"
description: "Azure Monitor를 사용하여 Azure API Management 서비스를 모니터링하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 0f64947755c79739bb6f15325929bd074cfd7210
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="c3f27-103">Azure Monitor를 사용하여 API Management 모니터링</span><span class="sxs-lookup"><span data-stu-id="c3f27-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="c3f27-104">Azure Monitor는 모든 Azure 리소스 모니터링을 위한 단일 소스를 제공하는 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="c3f27-105">Azure Monitor를 통해 API Management와 같은 Azure 리소스의 메트릭과 로그에 대해 시각화, 쿼리, 라우팅, 보관 및 조치를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="c3f27-106">다음 비디오는 Azure Monitor를 사용하여 API Management를 모니터링하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="c3f27-107">Azure Monitor에 대한 자세한 내용은 [Azure Monitor 시작]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f27-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="c3f27-108">메트릭</span><span class="sxs-lookup"><span data-stu-id="c3f27-108">Metrics</span></span>
<span data-ttu-id="c3f27-109">API Management는 현재 5개의 메트릭을 내보내고 향후 더 추가할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="c3f27-110">이러한 메트릭은 1분마다 내보내지므로 거의 실시간으로 API의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="c3f27-111">다음은 메트릭에 대한 요약입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="c3f27-112">총 게이트웨이 요청: 기간 동안의 API 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="c3f27-113">성공적인 게이트웨이 요청: 304, 307 및 301보다 작은(예: 200) 모든 항목을 포함하여 성공적인 HTTP 응답 코드를 수신하는 API 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="c3f27-114">실패한 게이트웨이 요청: 400 및 500보다 큰 모든 항목을 포함하여 잘못된 HTTP 응답 코드를 수신하는 API 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="c3f27-115">허가되지 않은 게이트웨이 요청: 401, 403 및 429를 포함하는 HTTP 응답 코드를 수신하는 API 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="c3f27-116">기타 게이트웨이 요청: 앞의 범주 중 하나에 속하지 않는(예: 418) HTTP 응답 코드를 수신하는 API 요청의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="c3f27-117">API Management 서비스에서 메트릭에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 메트릭에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="c3f27-118">API Management 서비스에서 메트릭을 보려면:</span><span class="sxs-lookup"><span data-stu-id="c3f27-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="c3f27-119">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="c3f27-120">API Management 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="c3f27-121">**메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-121">Click **Metrics**.</span></span>

![메트릭 블레이드][metrics-blade]

<span data-ttu-id="c3f27-123">메트릭을 사용하는 방법에 대한 자세한 내용은 [메트릭 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f27-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="c3f27-124">활동 로그</span><span class="sxs-lookup"><span data-stu-id="c3f27-124">Activity Logs</span></span>
<span data-ttu-id="c3f27-125">활동 로그는 API Management 서비스에서 수행된 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="c3f27-126">이전에는 이러한 로그를 "감사 로그" 또는 "작업 로그"라고도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="c3f27-127">활동 로그를 통해 API Management 서비스에 대한 모든 쓰기 작업(PUT, POST, DELETE)에서 "무엇을, 누가, 언제"를 판단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="c3f27-128">활동 로그는 읽기(GET) 작업 또는 클래식 게시자 포털에서 수행되었거나 원본 Management API를 사용하는 작업을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="c3f27-129">API Management 서비스에서 활동 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="c3f27-130">API Management 서비스에서 활동 로그를 보려면:</span><span class="sxs-lookup"><span data-stu-id="c3f27-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="c3f27-131">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="c3f27-132">API Management 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="c3f27-133">**활동 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-133">Click **Activity log**.</span></span>

![활동 로그 블레이드][activity-logs-blade]

<span data-ttu-id="c3f27-135">메트릭을 사용하는 방법에 대한 자세한 내용은 [활동 로그 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f27-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="c3f27-136">경고</span><span class="sxs-lookup"><span data-stu-id="c3f27-136">Alerts</span></span>
<span data-ttu-id="c3f27-137">메트릭 및 활동 로그를 기반으로 경고를 수신하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="c3f27-138">Azure Monitor를 사용하여 트리거되면 다음을 수행하도록 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="c3f27-139">전자 메일 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c3f27-139">Send an email notification</span></span>
* <span data-ttu-id="c3f27-140">웹후크 호출</span><span class="sxs-lookup"><span data-stu-id="c3f27-140">Call a webhook</span></span>
* <span data-ttu-id="c3f27-141">Azure 논리 앱 호출</span><span class="sxs-lookup"><span data-stu-id="c3f27-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="c3f27-142">API Management 서비스 또는 Azure Monitor에서 경고 규칙을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="c3f27-143">API Management에서 구성하려면:</span><span class="sxs-lookup"><span data-stu-id="c3f27-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="c3f27-144">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="c3f27-145">API Management 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="c3f27-146">**경고 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-146">Click **Alert rules**.</span></span>

![경고 규칙 블레이드][alert-rules-blade]

<span data-ttu-id="c3f27-148">경고 사용에 대한 자세한 내용은 [경고 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f27-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="c3f27-149">진단 로그</span><span class="sxs-lookup"><span data-stu-id="c3f27-149">Diagnostic Logs</span></span>
<span data-ttu-id="c3f27-150">진단 로그는 감사 뿐만 아니라 문제 해결에 중요한 작업 및 오류에 대한 풍부한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="c3f27-151">진단 로그는 활동 로그와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="c3f27-152">활동 로그는 Azure 리소스에서 수행된 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="c3f27-153">진단 로그는 리소스 자체에서 수행하는 작업에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="c3f27-154">API Management는 현재 다음 구조를 갖는 각 항목으로 개별 API 요청에 대한 진단 로그(시간 단위로 일괄 처리됨)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

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

<span data-ttu-id="c3f27-155">API Management 서비스에서 진단 로그에 액세스하거나 Azure Monitor에서 모든 Azure 리소스의 로그에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="c3f27-156">API Management 서비스에서 진단 로그를 보려면:</span><span class="sxs-lookup"><span data-stu-id="c3f27-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="c3f27-157">Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="c3f27-158">API Management 서비스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="c3f27-159">**진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c3f27-159">Click **Diagnostic log**.</span></span>

![진단 로그 블레이드][diagnostic-logs-blade]

<span data-ttu-id="c3f27-161">메트릭을 사용하는 방법에 대한 자세한 내용은 [진단 로그 개요]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c3f27-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="c3f27-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c3f27-162">Next Step</span></span>

* <span data-ttu-id="c3f27-163">[Azure Monitor 시작]</span><span class="sxs-lookup"><span data-stu-id="c3f27-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="c3f27-164">[메트릭 개요]</span><span class="sxs-lookup"><span data-stu-id="c3f27-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="c3f27-165">[활동 로그 개요]</span><span class="sxs-lookup"><span data-stu-id="c3f27-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="c3f27-166">[진단 로그 개요]</span><span class="sxs-lookup"><span data-stu-id="c3f27-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="c3f27-167">[경고 개요]</span><span class="sxs-lookup"><span data-stu-id="c3f27-167">[Overview of Alerts]</span></span>

<span data-ttu-id="c3f27-168">[Azure Monitor 시작]: ../monitoring-and-diagnostics/monitoring-get-started.md</span><span class="sxs-lookup"><span data-stu-id="c3f27-168">[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md</span></span>
<span data-ttu-id="c3f27-169">[메트릭 개요]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span><span class="sxs-lookup"><span data-stu-id="c3f27-169">[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md</span></span>
<span data-ttu-id="c3f27-170">[활동 로그 개요]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span><span class="sxs-lookup"><span data-stu-id="c3f27-170">[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md</span></span>
<span data-ttu-id="c3f27-171">[진단 로그 개요]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span><span class="sxs-lookup"><span data-stu-id="c3f27-171">[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md</span></span>
<span data-ttu-id="c3f27-172">[경고 개요]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span><span class="sxs-lookup"><span data-stu-id="c3f27-172">[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md</span></span>



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
