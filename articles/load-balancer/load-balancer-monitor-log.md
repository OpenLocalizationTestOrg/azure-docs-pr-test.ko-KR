---
title: "부하 분산 장치에 대한 작업, 이벤트 및 카운터 모니터링 | Microsoft Docs"
description: "Azure 부하 분산 장치에 대한 경고 이벤트 및 상태 프로브 상태 로깅을 사용하도록 설정하는 방법에 대해 알아보기"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 638ecd5e02889bd8cb6e7429dfcec335feaac4a3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="2b215-103">Azure 부하 분산 장치에 대한 로그 분석</span><span class="sxs-lookup"><span data-stu-id="2b215-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="2b215-104">Azure에서 부하 분산 장치를 관리하고 문제를 해결하는 데 다양한 유형의 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="2b215-105">이러한 로그 중 일부는 포털을 통해 액세스할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="2b215-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="2b215-106">Azure Blob Storage에서 모든 로그를 추출하고 다양한 도구(예: Excel 및 PowerBI)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="2b215-107">아래 목록에서 다른 종류의 로그에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="2b215-108">**감사 로그:** [Azure 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) (이전의 작업 로그)를 사용하여 Azure 구독에 제출된 모든 작업과 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="2b215-109">감사 로그는 기본적으로 사용하도록 설정되며 Azure 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="2b215-110">**경고 이벤트 로그:** 이 로그를 사용하여 부하 분산 장치에서 발생한 경고를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="2b215-111">부하 분산 장치에 대한 상태는 5분 마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="2b215-112">이 로그는 부하 분산 장치 경고 이벤트가 발생하는 경우에만 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="2b215-113">**상태 프로브 로그:** 상태 프로브 오류 때문에 부하 분산 장치에서 요청을 받지 않는 백 엔드 풀에 있는 인스턴스의 수와 같은 상태 프로브에서 발견한 문제를 보기 위해 이 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="2b215-114">상태 프로브 상태가 변경되는 경우에 이 로그가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b215-115">로그 분석은 현재 인터넷 연결 부하 분산 장치에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="2b215-116">로그는 리소스 관리자 배포 모델에 배포된 리소스에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="2b215-117">클래식 배포 모델에서 리소스에 대한 로그를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="2b215-118">배포 모델에 대한 자세한 내용은 [리소스 관리자 배포 및 클래식 배포 이해](../azure-resource-manager/resource-manager-deployment-model.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b215-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="2b215-119">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="2b215-119">Enable logging</span></span>

<span data-ttu-id="2b215-120">감사 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="2b215-121">이러한 로그를 통해 사용 가능한 데이터 수집을 시작하려면 이벤트 및 상태 프로브 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="2b215-122">로깅을 사용하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="2b215-123">[Azure 포털](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2b215-124">부하 분산 장치가 아직 없으면, 계속하기 전에 [부하 분산 장치를 만듭니다](load-balancer-get-started-internet-arm-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="2b215-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="2b215-125">포털에서 **찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="2b215-126">**부하 분산 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-126">Select **Load Balancers**.</span></span>

    ![포털 - 부하 분산 장치](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="2b215-128">기존 부하 분산 장치 >> **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="2b215-129">대화 상자 오른쪽의 부하 분산 장치 이름 아래에서 **모니터링**으로 스크롤하여 **진단**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![포털 - 부하 분산 장치-설정](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="2b215-131">**진단** 창의 **상태** 아래에서 **설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="2b215-132">**저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="2b215-133">**로그** 아래에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="2b215-134">슬라이더를 사용하여 이벤트 로그에 저장된 이벤트 데이터를 유지할 날짜 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="2b215-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-135">Click **Save**.</span></span>

    ![포털 - 진단 로그](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="2b215-137">감사 로그에는 별도의 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="2b215-138">이벤트 및 상태 프로브 로깅에 대한 저장소를 사용할 경우 서비스 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="2b215-139">감사 로그</span><span class="sxs-lookup"><span data-stu-id="2b215-139">Audit log</span></span>

<span data-ttu-id="2b215-140">감사 로그는 기본적으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-140">The audit log is generated by default.</span></span> <span data-ttu-id="2b215-141">이 로그는 Azure의 이벤트 로그 저장소에 90일 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="2b215-142">[이벤트 및 감사 로그 보기](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서를 읽어 이러한 로그에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="2b215-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="2b215-143">경고 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="2b215-143">Alert event log</span></span>

<span data-ttu-id="2b215-144">이 로그는 부하 분산 장치별로 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="2b215-145">이벤트는 JSON 형식으로 로깅되며, 로깅을 사용하도록 설정할 때 지정한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="2b215-146">다음은 이벤트의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="2b215-147">JSON 출력은 경고가 생성된 부하 분산 장치에 대한 이유를 설명하는 *eventname* 속성을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="2b215-148">이 경우 경고는 원본 IP NAT 제한(SNAT)으로 인해 발생된 TCP 포트 소모로 인해 발생되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="2b215-149">상태 프로브 로그</span><span class="sxs-lookup"><span data-stu-id="2b215-149">Health probe log</span></span>

<span data-ttu-id="2b215-150">이 로그는 위에서 설명한 대로 부하 분산 장치별로 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="2b215-151">데이터는 로깅을 사용하도록 설정할 때 지정된 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="2b215-152">'insights-logs-loadbalancerprobehealthstatus'라는 컨테이너가 생성되고 다음 데이터가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="2b215-153">속성 필드의 JSON 출력은 상태 프로브 상태에 대한 기본 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="2b215-154">*dipDownCount* 속성은 실패한 프로브 응답으로 인해 네트워크 트래픽을 수신하지 않은 백 엔드의 총 인스턴스 수를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="2b215-155">감사 로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="2b215-155">View and analyze the audit log</span></span>

<span data-ttu-id="2b215-156">다음 방법을 사용하여 감사 로그 데이터를 보고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="2b215-157">**Azure 도구:** Azure PowerShell, Azure 명령줄 인터페이스(CLI), Azure REST API 또는 Azure Preview 포털을 통해 감사 로그에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="2b215-158">각 방법에 대한 단계별 지침은 [리소스 관리자로 작업 감사](../azure-resource-manager/resource-group-audit.md) 문서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="2b215-159">**Power BI:** [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="2b215-160">[Power BI에 대한 Azure 감사 로그 콘텐츠 팩](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs)을 사용하여 미리 구성된 대시보드에서 데이터를 분석하거나 요구 사항에 맞게 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="2b215-161">상태 프로브 및 이벤트 로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="2b215-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="2b215-162">저장소 계정에 연결하고 이벤트 및 상태 프로브 로그에 대한 JSON 로그 항목을 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="2b215-163">JSON 파일을 다운로드한 후 CSV로 변환하여 Excel, PowerBI 또는 기타 데이터 시각화 도구에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="2b215-164">Visual Studio 및 C# 상수와 변수의 값 변경에 대한 기본 개념을 잘 알고 있으면 GitHub에서 제공하는 [로그 변환기 도구](https://github.com/Azure-Samples/networking-dotnet-log-converter) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b215-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2b215-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2b215-165">Additional resources</span></span>

* <span data-ttu-id="2b215-166">[Power BI를 사용하여 Azure 감사 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물.</span><span class="sxs-lookup"><span data-stu-id="2b215-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="2b215-167">[Power BI 등에서 Azure 감사 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물.</span><span class="sxs-lookup"><span data-stu-id="2b215-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b215-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b215-168">Next steps</span></span>

[<span data-ttu-id="2b215-169">부하 분산 장치 프로브 이해</span><span class="sxs-lookup"><span data-stu-id="2b215-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
