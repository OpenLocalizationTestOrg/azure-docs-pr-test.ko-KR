---
title: "aaaMonitor 작업, 이벤트 및 부하 분산 장치에 대 한 카운터 | Microsoft Docs"
description: "Tooenable 이벤트, 경고 하 고 Azure 부하 분산 장치에 대 한 상태 로깅 상태를 검색 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="f811d-103">Azure 부하 분산 장치에 대한 로그 분석</span><span class="sxs-lookup"><span data-stu-id="f811d-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="f811d-104">Azure toomanage에 서로 다른 유형의 로그를 사용할 수 있으며 부하 분산 장치 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="f811d-104">You can use different types of logs in Azure toomanage and troubleshoot load balancers.</span></span> <span data-ttu-id="f811d-105">일부이 로그 hello 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-105">Some of these logs can be accessed through hello portal.</span></span> <span data-ttu-id="f811d-106">Azure Blob Storage에서 모든 로그를 추출하고 다양한 도구(예: Excel 및 PowerBI)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="f811d-107">Hello 다른 유형의 로그 hello 목록 아래에서 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-107">You can learn more about hello different types of logs from hello list below.</span></span>

* <span data-ttu-id="f811d-108">**감사 로그:** 사용할 수 있습니다 [Azure 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) (이전의 작업 로그) tooview 제출 된 tooyour Azure 구독 및 해당 상태는 모든 작업.</span><span class="sxs-lookup"><span data-stu-id="f811d-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) tooview all operations being submitted tooyour Azure subscription(s), and their status.</span></span> <span data-ttu-id="f811d-109">감사 로그는 기본적으로 설정 되어 있고 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-109">Audit logs are enabled by default, and can be viewed in hello Azure portal.</span></span>
* <span data-ttu-id="f811d-110">**경고 이벤트 로그:** 이 로그 tooview 경고 rasied hello 부하 분산 장치에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-110">**Alert event logs:** You can use this log tooview alerts rasied by hello load balancer.</span></span> <span data-ttu-id="f811d-111">hello 부하 분산 장치에 대 한 hello 상태는 5 분 마다 수집 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-111">hello status for hello load balancer is collected every five minutes.</span></span> <span data-ttu-id="f811d-112">이 로그는 부하 분산 장치 경고 이벤트가 발생하는 경우에만 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="f811d-113">**상태 프로브 로그:** hello 상태 프로브 오류 때문에 hello 부하 분산 장치에서 요청을 받지 않는 경우 백 엔드 풀 인스턴스 수와 같은 프로그램 상태 프로브 검색 한이 로그 tooview 문제를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-113">**Health probe logs:** You can use this log tooview problems detected by your health probe, such as hello number of instances in your backend-pool that are not receiving requests from hello load balancer because of health probe failures.</span></span> <span data-ttu-id="f811d-114">이 로그 toowhen 쓰여집니다 hello 상태 프로브 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-114">This log is written toowhen there is a change in hello health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f811d-115">로그 분석은 현재 인터넷 연결 부하 분산 장치에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="f811d-116">로그는 hello 리소스 관리자 배포 모델에서 배포 된 리소스 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-116">Logs are only available for resources deployed in hello Resource Manager deployment model.</span></span> <span data-ttu-id="f811d-117">Hello 클래식 배포 모델의 리소스에 대 한 로그를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-117">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="f811d-118">Hello 배포 모델에 대 한 자세한 내용은 참조 [이해 리소스 관리자 배포 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-118">For more information about hello deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="f811d-119">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="f811d-119">Enable logging</span></span>

<span data-ttu-id="f811d-120">감사 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="f811d-121">Tooenable 이벤트 및 이러한 로그를 통해 사용할 수 있는 hello 데이터 수집 상태 프로브 로깅 toostart 필요.</span><span class="sxs-lookup"><span data-stu-id="f811d-121">You need tooenable event and health probe logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="f811d-122">다음 단계 tooenable 로깅 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-122">Use hello following steps tooenable logging.</span></span>

<span data-ttu-id="f811d-123">로그인 toohello [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-123">Sign-in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f811d-124">부하 분산 장치가 아직 없으면, 계속하기 전에 [부하 분산 장치를 만듭니다](load-balancer-get-started-internet-arm-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="f811d-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="f811d-125">Hello 포털에서 클릭 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-125">In hello portal, click **Browse**.</span></span>
2. <span data-ttu-id="f811d-126">**부하 분산 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-126">Select **Load Balancers**.</span></span>

    ![포털 - 부하 분산 장치](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="f811d-128">기존 부하 분산 장치 >> **모든 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="f811d-129">Hello 오른쪽에 hello 이름 hello 부하 분산 장치 아래에 hello 대화 상자를 스크롤하여 너무**모니터링**, 클릭 **진단**합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-129">On hello right side of hello dialog under hello name of hello load balancer, scroll too**Monitoring**, click **Diagnostics**.</span></span>

    ![포털 - 부하 분산 장치-설정](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="f811d-131">Hello에 **진단** 창 아래에서 **상태**선택, **에**합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-131">In hello **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="f811d-132">**저장소 계정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="f811d-133">**로그** 아래에서 기존 저장소 계정을 선택하거나 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="f811d-134">사용 하 여 hello 슬라이더 toodetermine 기간 (일) 동안의 이벤트 데이터는 hello 이벤트 로그에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-134">Use hello slider toodetermine how many days worth of event data will be stored in hello event logs.</span></span> 
8. <span data-ttu-id="f811d-135">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-135">Click **Save**.</span></span>

    ![포털 - 진단 로그](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="f811d-137">감사 로그에는 별도의 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="f811d-138">사용 하 여 hello 이벤트 및 상태에 대 한 저장소의 프로브 로깅 요금을 부과할 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-138">hello use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="f811d-139">감사 로그</span><span class="sxs-lookup"><span data-stu-id="f811d-139">Audit log</span></span>

<span data-ttu-id="f811d-140">hello 감사 로그는 기본적으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-140">hello audit log is generated by default.</span></span> <span data-ttu-id="f811d-141">hello 로그는 90 일 동안 Azure의 이벤트 로그 저장소에 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-141">hello logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="f811d-142">에 대 한 자세한이 로그 hello 읽어 [ग द ृ 및 감사 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f811d-142">Learn more about these logs by reading hello [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="f811d-143">경고 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="f811d-143">Alert event log</span></span>

<span data-ttu-id="f811d-144">이 로그는 부하 분산 장치별로 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="f811d-145">hello 이벤트는 JSON 형식에 기록 하 고 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-145">hello events are logged in JSON format and stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="f811d-146">hello 다음은 이벤트의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-146">hello following is an example of an event.</span></span>

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

<span data-ttu-id="f811d-147">hello JSON 출력 표시 hello *eventname* hello 부하 분산 장치에 대 한 hello 이유를 설명 하는 속성 경고를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-147">hello JSON output shows hello *eventname* property which will describe hello reason for hello load balancer created an alert.</span></span> <span data-ttu-id="f811d-148">이 경우 생성 된 hello 경고 tooTCP 포트 소모 원본 IP NAT 제한에 의해 발생 한 (SNAT) 때문 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-148">In this case, hello alert generated was due tooTCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="f811d-149">상태 프로브 로그</span><span class="sxs-lookup"><span data-stu-id="f811d-149">Health probe log</span></span>

<span data-ttu-id="f811d-150">이 로그는 위에서 설명한 대로 부하 분산 장치별로 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="f811d-151">hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-151">hello data is stored in hello storage account you specified when you enabled hello logging.</span></span> <span data-ttu-id="f811d-152">' Insights 로그 loadbalancerprobehealthstatus' 라는 컨테이너 만들어지고 hello 같은 데이터가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and hello following data is logged:</span></span>

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

<span data-ttu-id="f811d-153">hello JSON 출력 hello 속성 필드 hello 기본에 대 한 정보 hello 프로브 상태에에서 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-153">hello JSON output shows in hello properties field hello basic information for hello probe health status.</span></span> <span data-ttu-id="f811d-154">hello *dipDownCount* 속성이 hello 백 엔드 toofailed 프로브 응답 인해 네트워크 트래픽을 수신 하지는 hello 총 인스턴스 수가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-154">hello *dipDownCount* property shows hello total number of instances on hello back-end which are not receiving network traffic due toofailed probe responses.</span></span>

## <a name="view-and-analyze-hello-audit-log"></a><span data-ttu-id="f811d-155">보기 및 hello 감사 로그를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-155">View and analyze hello audit log</span></span>

<span data-ttu-id="f811d-156">보고 하 고 hello 메서드를 다음 중 하나를 사용 하 여 감사 로그 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-156">You can view and analyze audit log data using any of hello following methods:</span></span>

* <span data-ttu-id="f811d-157">**Azure 도구:** hello Azure preview 포털 또는 Azure PowerShell을 hello Azure 명령줄 인터페이스 (CLI) hello Azure REST API를 통해 hello 감사 로그에서 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-157">**Azure tools:** Retrieve information from hello audit logs through Azure PowerShell, hello Azure Command Line Interface (CLI), hello Azure REST API, or hello Azure preview portal.</span></span> <span data-ttu-id="f811d-158">각 방법에 대 한 단계별 지침 hello에 자세히 설명 되어 [리소스 관리자와 작업을 감사](../azure-resource-manager/resource-group-audit.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="f811d-158">Step-by-step instructions for each method are detailed in hello [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="f811d-159">**Power BI:** [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="f811d-160">Hello를 사용 하 여 [Power BI 용 Azure Audit Logs 콘텐츠 팩](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), 미리 구성 된 대시보드를 사용 하 여 데이터를 분석할 수 있습니다 또는 요구 사항를 뷰 toosuit에 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-160">Using hello [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views toosuit your requirements.</span></span>

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a><span data-ttu-id="f811d-161">보기 및 상태 프로브 hello와 이벤트 로그를 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-161">View and analyze hello health probe and event log</span></span>

<span data-ttu-id="f811d-162">Tooconnect tooyour 저장소가 필요한 계정 및 이벤트 및 상태 프로브 로그에 대 한 hello JSON 로그 항목을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-162">You need tooconnect tooyour storage account and retrieve hello JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="f811d-163">Hello JSON 파일을 다운로드 한 후 Excel, PowerBI, 또는 기타 데이터 시각화 도구 뷰와 tooCSV 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-163">Once you download hello JSON files, you can convert them tooCSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="f811d-164">Visual Studio 및 C#의 변수 및 상수에 대 한 값 변경의 기본 개념에 잘 알고 있다면 hello를 사용할 수 있습니다 [변환기 도구 로그](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f811d-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f811d-165">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f811d-165">Additional resources</span></span>

* <span data-ttu-id="f811d-166">[Power BI를 사용하여 Azure 감사 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물.</span><span class="sxs-lookup"><span data-stu-id="f811d-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="f811d-167">[Power BI 등에서 Azure 감사 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물.</span><span class="sxs-lookup"><span data-stu-id="f811d-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f811d-168">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f811d-168">Next steps</span></span>

[<span data-ttu-id="f811d-169">부하 분산 장치 프로브 이해</span><span class="sxs-lookup"><span data-stu-id="f811d-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)
