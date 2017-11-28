---
title: "응용 프로그램 게이트웨이에 대 한 로그, 성능 로그, 백 엔드 상태 및 메트릭을 aaaMonitor에 액세스 | Microsoft Docs"
description: "자세한 내용은 방법 tooenable에 응용 프로그램 게이트웨이 액세스 로그와 성능 로그 및 관리"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="96c90-103">Application Gateway에 대한 백 엔드 상태, 진단 로그 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="96c90-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="96c90-104">Azure 응용 프로그램 게이트웨이 사용 하 여 hello 같은 방법으로 다음의 리소스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-104">By using Azure Application Gateway, you can monitor resources in hello following ways:</span></span>

* <span data-ttu-id="96c90-105">[백 엔드 상태](#back-end-health): 응용 프로그램 게이트웨이 백 엔드 풀 hello Azure 포털을 통해 및 PowerShell을 통해 hello에 대 한 hello 서버 hello 기능 toomonitor hello 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-105">[Back-end health](#back-end-health): Application Gateway provides hello capability toomonitor hello health of hello servers in hello back-end pools through hello Azure portal and through PowerShell.</span></span> <span data-ttu-id="96c90-106">Hello 성능 진단 로그를 통해 hello 백 엔드 풀의 hello 상태를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-106">You can also find hello health of hello back-end pools through hello performance diagnostic logs.</span></span>

* <span data-ttu-id="96c90-107">[로그](#diagnostic-logs): 액세스, 성능, 로그를 사용 하 고 다른 데이터 toobe 저장 하거나 모니터링을 위해 리소스에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data toobe saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="96c90-108">[메트릭](#metrics) - Application Gateway에는 현재 메트릭이 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="96c90-109">이 메트릭은 초당 바이트 수의 응용 프로그램 게이트웨이 hello hello 처리량을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-109">This metric measures hello throughput of hello application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="96c90-110">백 엔드 상태</span><span class="sxs-lookup"><span data-stu-id="96c90-110">Back-end health</span></span>

<span data-ttu-id="96c90-111">응용 프로그램 게이트웨이 hello 기능 toomonitor hello hello 포털, PowerShell 및 hello CLI (명령줄 인터페이스)를 통해 hello 백 엔드 풀의 개별 멤버의 상태를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-111">Application Gateway provides hello capability toomonitor hello health of individual members of hello back-end pools through hello portal, PowerShell, and hello command-line interface (CLI).</span></span> <span data-ttu-id="96c90-112">집계 된 상태를 찾을 수도 있습니다 hello 성능 진단 로그를 통해 백 엔드 풀의 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-112">You can also find an aggregated health summary of back-end pools through hello performance diagnostic logs.</span></span> 

<span data-ttu-id="96c90-113">hello 백 엔드 상태 보고서의 hello 응용 프로그램 게이트웨이 상태 프로브 toohello 백 엔드 인스턴스 hello 출력에 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-113">hello back-end health report reflects hello output of hello Application Gateway health probe toohello back-end instances.</span></span> <span data-ttu-id="96c90-114">검색이 성공 하 고 다시 hello 끝 트래픽을 수신할 수 경우 정상인 상태로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-114">When probing is successful and hello back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="96c90-115">그렇지 않으면 비정상 상태로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96c90-116">응용 프로그램 게이트웨이 서브넷에 NSG ()는 네트워크 보안 그룹이 있는 경우 인바운드 트래픽의 hello 응용 프로그램 게이트웨이 서브넷에 65503 65534 포트 범위를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on hello Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="96c90-117">이러한 포트는 hello 백 엔드 상태 API toowork 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-117">These ports are required for hello back-end health API toowork.</span></span>


### <a name="view-back-end-health-through-hello-portal"></a><span data-ttu-id="96c90-118">Hello 포털을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="96c90-118">View back-end health through hello portal</span></span>

<span data-ttu-id="96c90-119">Hello 포털에서 백 엔드 상태는 자동으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-119">In hello portal, back-end health is provided automatically.</span></span> <span data-ttu-id="96c90-120">기존 응용 프로그램 게이트웨이에서 **모니터링** > **백 엔드 상태**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="96c90-121">Hello 백 엔드 풀의 각 멤버는 (인지 NIC, IP 또는 FQDN)이이 페이지에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-121">Each member in hello back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="96c90-122">백 엔드 풀 이름, 포트, 백 엔드 HTTP 설정 이름 및 상태도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="96c90-123">상태의 유효한 값은 **정상**, **비정상** 및 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="96c90-124">백 엔드의 상태를 표시 하는 경우 **알 수 없는**, 해당 액세스 toohello 백 엔드 NSG 규칙, 사용자 정의 경로 (UDR) 또는 hello 가상 네트워크에 있는 사용자 지정 DNS에 의해 차단 되지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-124">If you see a back-end health status of **Unknown**, ensure that access toohello back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in hello virtual network.</span></span>

![백 엔드 상태][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="96c90-126">PowerShell을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="96c90-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="96c90-127">다음 PowerShell 코드 hello tooview 백 엔드 상태를 사용 하 여 hello 하는 방법을 보여 줍니다. `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="96c90-127">hello following PowerShell code shows how tooview back-end health by using hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="96c90-128">Azure CLI 2.0을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="96c90-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="96c90-129">결과</span><span class="sxs-lookup"><span data-stu-id="96c90-129">Results</span></span>

<span data-ttu-id="96c90-130">다음 코드 조각 hello hello 응답의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-130">hello following snippet shows an example of hello response:</span></span>

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <span data-ttu-id="96c90-131"><a name="diagnostic-logging"></a>진단 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="96c90-132">Azure toomanage에 서로 다른 유형의 로그를 사용할 수 있으며 응용 프로그램 게이트웨이 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="96c90-132">You can use different types of logs in Azure toomanage and troubleshoot application gateways.</span></span> <span data-ttu-id="96c90-133">일부이 로그 hello 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-133">You can access some of these logs through hello portal.</span></span> <span data-ttu-id="96c90-134">모든 로그는 Azure Blob 저장소에서 추출하고 다양한 도구(예: [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md),Excel 및 Power BI)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="96c90-135">Hello 통한 여러 유형의 로그 hello 목록 다음에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-135">You can learn more about hello different types of logs from hello following list:</span></span>

* <span data-ttu-id="96c90-136">**활동 로그**: 사용할 수 있습니다 [Azure 활동 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md) (이전의 작업 로그 및 감사 로그) tooview 중인 모든 작업이 tooyour Azure 구독 및 해당 상태를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) tooview all operations that are submitted tooyour Azure subscription, and their status.</span></span> <span data-ttu-id="96c90-137">기본적으로 활동 로그 항목을 수집 하 고 hello Azure 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-137">Activity log entries are collected by default, and you can view them in hello Azure portal.</span></span>
* <span data-ttu-id="96c90-138">**액세스 로그**:이 로그 tooview 응용 프로그램 게이트웨이 액세스 패턴을 사용 하 고 중요 한 정보, 포함 하 여 hello 호출자의 IP, 요청된 URL, 응답 대기 시간, 반환 코드 및 바이트를 축소 및 분석할 수 있습니다. 액세스 로그는 300초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-138">**Access log**: You can use this log tooview Application Gateway access patterns and analyze important information, including hello caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="96c90-139">이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="96c90-140">hello instanceId 속성에 의해 hello 응용 프로그램 게이트웨이 인스턴스를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-140">hello Application Gateway instance can be identified by hello instanceId property.</span></span>
* <span data-ttu-id="96c90-141">**성능 로그**:이 로그 tooview 응용 프로그램 게이트웨이 인스턴스가 수행 하는 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-141">**Performance log**: You can use this log tooview how Application Gateway instances are performing.</span></span> <span data-ttu-id="96c90-142">이 로그는 인스턴스 단위로 처리된 총 요청 수, 처리량(바이트), 실패한 요청 수, 정상 및 비정상 백 엔드 인스턴스 수 등의 성능 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="96c90-143">성능 로그는 60초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="96c90-144">**방화벽 로그**: 감지 하거나 방지 모드의 웹 응용 프로그램 방화벽 hello로 구성 된 응용 프로그램 게이트웨이 통해 로깅되는이 로그 tooview hello 요청을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-144">**Firewall log**: You can use this log tooview hello requests that are logged through either detection or prevention mode of an application gateway that is configured with hello web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="96c90-145">로그는 hello Azure 리소스 관리자 배포 모델에서 배포 된 리소스에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-145">Logs are available only for resources deployed in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="96c90-146">Hello 클래식 배포 모델의 리소스에 대 한 로그를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-146">You cannot use logs for resources in hello classic deployment model.</span></span> <span data-ttu-id="96c90-147">더 잘 이해 hello 두 모델의를 참조 hello [이해 리소스 관리자 배포 및 클래식 배포](../azure-resource-manager/resource-manager-deployment-model.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="96c90-147">For a better understanding of hello two models, see hello [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="96c90-148">로그 저장에는 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="96c90-149">**저장소 계정** - 로그를 장기간 저장하고 필요할 때 검토하는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="96c90-150">**이벤트 허브**: (SEIM)의 이벤트 관리 도구 리소스에 tooget 경고 및 이벤트 허브는 기타 보안 정보를 통합 하기 위한 유용한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools tooget alerts on your resources.</span></span>
* <span data-ttu-id="96c90-151">**Log Analytics** - 일반적으로 응용 프로그램을 실시간 모니터링하거나 추세를 파악하는 데 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="96c90-152">PowerShell을 통한 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="96c90-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="96c90-153">활동 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="96c90-154">액세스 및 이러한 로그를 통해 사용할 수 있는 hello 데이터 수집 성능 로깅 toostart 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-154">You must enable access and performance logging toostart collecting hello data available through those logs.</span></span> <span data-ttu-id="96c90-155">tooenable 로깅에 사용 하 여 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-155">tooenable logging, use hello following steps:</span></span>

1. <span data-ttu-id="96c90-156">Note hello 로그 데이터가 저장 되는 저장소 계정의 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-156">Note your storage account's resource ID, where hello log data is stored.</span></span> <span data-ttu-id="96c90-157">이 값은 hello 폼의: /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름은\>/providers/Microsoft.Storage/storageAccounts/\<저장소계정이름\>.</span><span class="sxs-lookup"><span data-stu-id="96c90-157">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="96c90-158">구독의 모든 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="96c90-159">Azure 포털 toofind hello이이 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-159">You can use hello Azure portal toofind this information.</span></span>

    ![포털: 저장소 계정의 리소스 ID](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="96c90-161">로깅을 사용할 Application Gateway의 리소스 ID를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="96c90-162">이 값은 hello 폼의: /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름은\>/providers/Microsoft.Network/applicationGateways/\<응용 프로그램 게이트웨이 이름\>합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-162">This value is of hello form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="96c90-163">Hello 포털 toofind이이 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-163">You can use hello portal toofind this information.</span></span>

    ![포털: 응용 프로그램 게이트웨이의 리소스 ID](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="96c90-165">Hello 다음 PowerShell cmdlet을 사용 하 여 진단 로깅 사용:</span><span class="sxs-lookup"><span data-stu-id="96c90-165">Enable diagnostic logging by using hello following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="96c90-166">활동 로그에는 별도의 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="96c90-167">저장소 액세스 및 성능 로깅에 대 한 hello 사용할 서비스 요금이 부과 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-167">hello use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-hello-azure-portal"></a><span data-ttu-id="96c90-168">Azure 포털을 통해 hello 로깅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="96c90-168">Enable logging through hello Azure portal</span></span>

1. <span data-ttu-id="96c90-169">에 Azure 포털 hello, 리소스를 찾 및 클릭 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-169">In hello Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="96c90-170">Application Gateway의 경우 다음 세 가지 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="96c90-171">액세스 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-171">Access log</span></span>
   * <span data-ttu-id="96c90-172">성능 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-172">Performance log</span></span>
   * <span data-ttu-id="96c90-173">방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-173">Firewall log</span></span>

2. <span data-ttu-id="96c90-174">데이터를 수집 하는 toostart 클릭 **진단을 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-174">toostart collecting data, click **Turn on diagnostics**.</span></span>

   ![진단 켜기][1]

3. <span data-ttu-id="96c90-176">hello **진단 설정을** 블레이드는 hello 설정을 hello에 대 한 진단 로그를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-176">hello **Diagnostics settings** blade provides hello settings for hello diagnostic logs.</span></span> <span data-ttu-id="96c90-177">이 예제에서는 로그 분석 hello 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-177">In this example, Log Analytics stores hello logs.</span></span> <span data-ttu-id="96c90-178">클릭 **구성** 아래 **로그 분석** tooconfigure 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-178">Click **Configure** under **Log Analytics** tooconfigure your workspace.</span></span> <span data-ttu-id="96c90-179">이벤트 허브 및는 저장소 계정 toosave hello 진단 로그를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-179">You can also use event hubs and a storage account toosave hello diagnostic logs.</span></span>

   ![Hello 구성 프로세스를 시작합니다.][2]

4. <span data-ttu-id="96c90-181">기존 OMS(Operations Management Suite) 작업 영역을 선택하거나 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="96c90-182">이 예제에서는 기존 작업 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-182">This example uses an existing one.</span></span>

   ![OMS 작업 영역에 대한 옵션][3]

5. <span data-ttu-id="96c90-184">Hello 설정을 확인 하 고 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-184">Confirm hello settings and click **Save**.</span></span>

   ![선택 항목이 있는 진단 설정 블레이드][4]

### <a name="activity-log"></a><span data-ttu-id="96c90-186">활동 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-186">Activity log</span></span>

<span data-ttu-id="96c90-187">Azure는 기본적으로 hello 활동 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-187">Azure generates hello activity log by default.</span></span> <span data-ttu-id="96c90-188">hello 로그 hello 이벤트 로그를 Azure 저장소에서 90 일 동안 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-188">hello logs are preserved for 90 days in hello Azure event logs store.</span></span> <span data-ttu-id="96c90-189">에 대 한 자세한이 로그 hello 읽어 [이벤트 및 활동 로그 보기](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="96c90-189">Learn more about these logs by reading hello [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="96c90-190">액세스 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-190">Access log</span></span>

<span data-ttu-id="96c90-191">각 응용 프로그램 게이트웨이 인스턴스에서 hello 이전 단계에에서 설명 된 대로 활성화 한 경우에 hello 액세스 로그가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-191">hello access log is generated only if you've enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="96c90-192">hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-192">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="96c90-193">각 응용 프로그램 게이트웨이 액세스 hello 다음 예제에에서 나와 있는 것 처럼 JSON 형식으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-193">Each access of Application Gateway is logged in JSON format, as shown in hello following example:</span></span>


|<span data-ttu-id="96c90-194">값</span><span class="sxs-lookup"><span data-stu-id="96c90-194">Value</span></span>  |<span data-ttu-id="96c90-195">설명</span><span class="sxs-lookup"><span data-stu-id="96c90-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="96c90-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="96c90-196">instanceId</span></span>     | <span data-ttu-id="96c90-197">응용 프로그램 게이트웨이 인스턴스는 서비스 제공된 하는 hello 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-197">Application Gateway instance that served hello request.</span></span>        |
|<span data-ttu-id="96c90-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="96c90-198">clientIP</span></span>     | <span data-ttu-id="96c90-199">Hello 요청에 대 한 원래 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-199">Originating IP for hello request.</span></span>        |
|<span data-ttu-id="96c90-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="96c90-200">clientPort</span></span>     | <span data-ttu-id="96c90-201">Hello 요청에 대 한 포트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-201">Originating port for hello request.</span></span>       |
|<span data-ttu-id="96c90-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="96c90-202">httpMethod</span></span>     | <span data-ttu-id="96c90-203">Hello 요청에 의해 사용 되는 HTTP 메서드.</span><span class="sxs-lookup"><span data-stu-id="96c90-203">HTTP method used by hello request.</span></span>       |
|<span data-ttu-id="96c90-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="96c90-204">requestUri</span></span>     | <span data-ttu-id="96c90-205">Hello의 URI는 요청을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-205">URI of hello received request.</span></span>        |
|<span data-ttu-id="96c90-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="96c90-206">RequestQuery</span></span>     | <span data-ttu-id="96c90-207">**서버 라우팅됩니다**: hello 요청 보낸 백 엔드 풀 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="96c90-207">**Server-Routed**: Back-end pool instance that was sent hello request.</span></span> </br> <span data-ttu-id="96c90-208">**AzureApplicationGateway 로그 ID X**: hello 요청에 사용 되는 상관 관계 ID.</span><span class="sxs-lookup"><span data-stu-id="96c90-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for hello request.</span></span> <span data-ttu-id="96c90-209">Hello 백 엔드 서버에 사용 되는 tootroubleshoot 트래픽 문제 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-209">It can be used tootroubleshoot traffic issues on hello back-end servers.</span></span> </br><span data-ttu-id="96c90-210">**서버 상태**: 응용 프로그램 게이트웨이 백 엔드 hello에서에서 받은 HTTP 응답 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from hello back end.</span></span>       |
|<span data-ttu-id="96c90-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="96c90-211">UserAgent</span></span>     | <span data-ttu-id="96c90-212">Hello HTTP 요청 헤더에서 사용자 에이전트입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-212">User agent from hello HTTP request header.</span></span>        |
|<span data-ttu-id="96c90-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="96c90-213">httpStatus</span></span>     | <span data-ttu-id="96c90-214">HTTP 상태 코드는 응용 프로그램 게이트웨이에서 toohello 클라이언트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-214">HTTP status code returned toohello client from Application Gateway.</span></span>       |
|<span data-ttu-id="96c90-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="96c90-215">httpVersion</span></span>     | <span data-ttu-id="96c90-216">Hello 요청의 HTTP 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-216">HTTP version of hello request.</span></span>        |
|<span data-ttu-id="96c90-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="96c90-217">receivedBytes</span></span>     | <span data-ttu-id="96c90-218">받은 패킷의 크기(바이트)</span><span class="sxs-lookup"><span data-stu-id="96c90-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="96c90-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="96c90-219">sentBytes</span></span>| <span data-ttu-id="96c90-220">보낸 패킷의 크기(바이트)</span><span class="sxs-lookup"><span data-stu-id="96c90-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="96c90-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="96c90-221">timeTaken</span></span>| <span data-ttu-id="96c90-222">처리 요청 toobe 및 해당 응답 toobe 전송 하는 데 걸리는 시간 (밀리초)의 길이입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-222">Length of time (in milliseconds) that it takes for a request toobe processed and its response toobe sent.</span></span> <span data-ttu-id="96c90-223">이 응용 프로그램 게이트웨이 hello 응답 송신 작업이 완료 되는 HTTP 요청 toohello 시간의 hello 첫 번째 바이트를 수신 하는 경우 hello 시간부터 hello 간격으로 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-223">This is calculated as hello interval from hello time when Application Gateway receives hello first byte of an HTTP request toohello time when hello response send operation finishes.</span></span> <span data-ttu-id="96c90-224">일반적으로 필드 Time-taken hello toonote hello 요청 및 응답 패킷을 hello 네트워크를 통해 이동 하는 hello 시간을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-224">It's important toonote that hello Time-Taken field usually includes hello time that hello request and response packets are traveling over hello network.</span></span> |
|<span data-ttu-id="96c90-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="96c90-225">sslEnabled</span></span>| <span data-ttu-id="96c90-226">통신 toohello 백 엔드 풀 SSL 사용 여부.</span><span class="sxs-lookup"><span data-stu-id="96c90-226">Whether communication toohello back-end pools used SSL.</span></span> <span data-ttu-id="96c90-227">유효한 값은 on과 off입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-227">Valid values are on and off.</span></span>|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a><span data-ttu-id="96c90-228">성능 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-228">Performance log</span></span>

<span data-ttu-id="96c90-229">hello 성능 로그가 hello 이전 단계에에서 설명 된 대로 각 응용 프로그램 게이트웨이 인스턴스에서 사용 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-229">hello performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in hello preceding steps.</span></span> <span data-ttu-id="96c90-230">hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-230">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="96c90-231">hello 성능 로그 데이터는 1 분 간격으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-231">hello performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="96c90-232">hello 같은 데이터가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-232">hello following data is logged:</span></span>


|<span data-ttu-id="96c90-233">값</span><span class="sxs-lookup"><span data-stu-id="96c90-233">Value</span></span>  |<span data-ttu-id="96c90-234">설명</span><span class="sxs-lookup"><span data-stu-id="96c90-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="96c90-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="96c90-235">instanceId</span></span>     |  <span data-ttu-id="96c90-236">성능 데이터가 생성되는 Application Gateway 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="96c90-237">다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="96c90-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="96c90-238">healthyHostCount</span></span>     | <span data-ttu-id="96c90-239">Hello 백 엔드 풀에서 정상 호스트의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-239">Number of healthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="96c90-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="96c90-240">unHealthyHostCount</span></span>     | <span data-ttu-id="96c90-241">Hello 백 엔드 풀에서 비정상 호스트의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-241">Number of unhealthy hosts in hello back-end pool.</span></span>        |
|<span data-ttu-id="96c90-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="96c90-242">requestCount</span></span>     | <span data-ttu-id="96c90-243">처리된 요청 수</span><span class="sxs-lookup"><span data-stu-id="96c90-243">Number of requests served.</span></span>        |
|<span data-ttu-id="96c90-244">latency</span><span class="sxs-lookup"><span data-stu-id="96c90-244">latency</span></span> | <span data-ttu-id="96c90-245">대기 시간 (밀리초) hello 인스턴스 toohello에서 보낸 요청의 백 엔드 hello 요청을 수용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-245">Latency (in milliseconds) of requests from hello instance toohello back end that serves hello requests.</span></span> |
|<span data-ttu-id="96c90-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="96c90-246">failedRequestCount</span></span>| <span data-ttu-id="96c90-247">실패한 요청 수</span><span class="sxs-lookup"><span data-stu-id="96c90-247">Number of failed requests.</span></span>|
|<span data-ttu-id="96c90-248">throughput</span><span class="sxs-lookup"><span data-stu-id="96c90-248">throughput</span></span>| <span data-ttu-id="96c90-249">바이트 수 / 초 단위로 측정 된 hello 마지막 로그 이후 평균 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-249">Average throughput since hello last log, measured in bytes per second.</span></span>|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> <span data-ttu-id="96c90-250">Hello HTTP 요청의 첫 번째 바이트 hello hello HTTP 응답의 마지막 바이트 hello 전송 된 때 받은 toohello 시간은 언제 인가요 hello 시간에서 대기 시간이 계산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-250">Latency is calculated from hello time when hello first byte of hello HTTP request is received toohello time when hello last byte of hello HTTP response is sent.</span></span> <span data-ttu-id="96c90-251">hello 총 hello 응용 프로그램 게이트웨이 처리 시간 및 hello 네트워크 비용 toohello 다시 종료, 백 엔드는 tooprocess hello 요청 hello hello 시간 plus입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-251">It's hello sum of hello Application Gateway processing time plus hello network cost toohello back end, plus hello time that hello back end takes tooprocess hello request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="96c90-252">방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-252">Firewall log</span></span>

<span data-ttu-id="96c90-253">방화벽 로그 hello hello 이전 단계에에서 설명 된 대로 각 응용 프로그램 게이트웨이를 사용 하는 경우에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-253">hello firewall log is generated only if you have enabled it for each application gateway, as detailed in hello preceding steps.</span></span> <span data-ttu-id="96c90-254">이 로그는 hello 웹 응용 프로그램 방화벽 응용 프로그램 게이트웨이에 구성 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-254">This log also requires that hello web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="96c90-255">hello 데이터 hello 로깅을 사용 하는 경우 지정한 hello 저장소 계정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-255">hello data is stored in hello storage account that you specified when you enabled hello logging.</span></span> <span data-ttu-id="96c90-256">hello 같은 데이터가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-256">hello following data is logged:</span></span>


|<span data-ttu-id="96c90-257">값</span><span class="sxs-lookup"><span data-stu-id="96c90-257">Value</span></span>  |<span data-ttu-id="96c90-258">설명</span><span class="sxs-lookup"><span data-stu-id="96c90-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="96c90-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="96c90-259">instanceId</span></span>     | <span data-ttu-id="96c90-260">방화벽 데이터가 생성되는 Application Gateway 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="96c90-261">다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="96c90-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="96c90-262">clientIp</span></span>     |   <span data-ttu-id="96c90-263">Hello 요청에 대 한 원래 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-263">Originating IP for hello request.</span></span>      |
|<span data-ttu-id="96c90-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="96c90-264">clientPort</span></span>     |  <span data-ttu-id="96c90-265">Hello 요청에 대 한 포트를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-265">Originating port for hello request.</span></span>       |
|<span data-ttu-id="96c90-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="96c90-266">requestUri</span></span>     | <span data-ttu-id="96c90-267">Hello의 URL 요청을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-267">URL of hello received request.</span></span>       |
|<span data-ttu-id="96c90-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="96c90-268">ruleSetType</span></span>     | <span data-ttu-id="96c90-269">규칙 집합 유형이며,</span><span class="sxs-lookup"><span data-stu-id="96c90-269">Rule set type.</span></span> <span data-ttu-id="96c90-270">hello 사용 가능한 값은 OWASP입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-270">hello available value is OWASP.</span></span>        |
|<span data-ttu-id="96c90-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="96c90-271">ruleSetVersion</span></span>     | <span data-ttu-id="96c90-272">사용된 규칙 집합 버전이며,</span><span class="sxs-lookup"><span data-stu-id="96c90-272">Rule set version used.</span></span> <span data-ttu-id="96c90-273">사용 가능한 값은 2.2.9 및 3.0입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="96c90-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="96c90-274">ruleId</span></span>     | <span data-ttu-id="96c90-275">이벤트를 트리거하는 hello의 규칙 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-275">Rule ID of hello triggering event.</span></span>        |
|<span data-ttu-id="96c90-276">Message</span><span class="sxs-lookup"><span data-stu-id="96c90-276">message</span></span>     | <span data-ttu-id="96c90-277">이벤트를 트리거하는 hello에 대 한 친숙 한 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-277">User-friendly message for hello triggering event.</span></span> <span data-ttu-id="96c90-278">자세한 내용은 hello 세부 정보 섹션에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-278">More details are provided in hello details section.</span></span>        |
|<span data-ttu-id="96c90-279">action</span><span class="sxs-lookup"><span data-stu-id="96c90-279">action</span></span>     |  <span data-ttu-id="96c90-280">Hello 요청에서 수행한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-280">Action taken on hello request.</span></span> <span data-ttu-id="96c90-281">사용할 수 있는 값은 Blocked 및 Allowed입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="96c90-282">site</span><span class="sxs-lookup"><span data-stu-id="96c90-282">site</span></span>     | <span data-ttu-id="96c90-283">사이트는 hello에 대 한 로그를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-283">Site for which hello log was generated.</span></span> <span data-ttu-id="96c90-284">현재 규칙이 전역이므로 Global만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="96c90-285">세부 정보</span><span class="sxs-lookup"><span data-stu-id="96c90-285">details</span></span>     | <span data-ttu-id="96c90-286">이벤트를 트리거하는 hello의 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-286">Details of hello triggering event.</span></span>        |
|<span data-ttu-id="96c90-287">details.message</span><span class="sxs-lookup"><span data-stu-id="96c90-287">details.message</span></span>     | <span data-ttu-id="96c90-288">Hello 규칙의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-288">Description of hello rule.</span></span>        |
|<span data-ttu-id="96c90-289">details.data</span><span class="sxs-lookup"><span data-stu-id="96c90-289">details.data</span></span>     | <span data-ttu-id="96c90-290">특정 데이터는 일치 하는 hello 규칙을 요청에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-290">Specific data found in request that matched hello rule.</span></span>         |
|<span data-ttu-id="96c90-291">details.file</span><span class="sxs-lookup"><span data-stu-id="96c90-291">details.file</span></span>     | <span data-ttu-id="96c90-292">Hello 규칙을 포함 하는 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-292">Configuration file that contained hello rule.</span></span>        |
|<span data-ttu-id="96c90-293">details.line</span><span class="sxs-lookup"><span data-stu-id="96c90-293">details.line</span></span>     | <span data-ttu-id="96c90-294">Hello 이벤트를 트리거한 hello 구성 파일에 줄 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-294">Line number in hello configuration file that triggered hello event.</span></span>       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

### <a name="view-and-analyze-hello-activity-log"></a><span data-ttu-id="96c90-295">보기 및 분석 hello 활동 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-295">View and analyze hello activity log</span></span>

<span data-ttu-id="96c90-296">볼 수 있고 hello 메서드를 다음 중 하나를 사용 하 여 활동 로그 데이터를 분석할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-296">You can view and analyze activity log data by using any of hello following methods:</span></span>

* <span data-ttu-id="96c90-297">**Azure tools**: hello Azure 포털 또는 Azure PowerShell을 hello Azure CLI, hello Azure REST API를 통해 hello 활동 로그에서 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-297">**Azure tools**: Retrieve information from hello activity log through Azure PowerShell, hello Azure CLI, hello Azure REST API, or hello Azure portal.</span></span> <span data-ttu-id="96c90-298">각 방법에 대 한 단계별 지침 hello에 자세히 설명 되어 [활동 작업 리소스 관리자와](../azure-resource-manager/resource-group-audit.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="96c90-298">Step-by-step instructions for each method are detailed in hello [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="96c90-299">**Power BI** - [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="96c90-300">Hello를 사용 하 여 [Azure 활동 로그 콘텐츠 팩 Power BI에 대 한](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), 하거나 사용자 지정할 방법으로 사용할 수 있는 미리 구성 된 대시보드를 사용 하 여 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-300">By using hello [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a><span data-ttu-id="96c90-301">보기 및 분석 hello 액세스, 성능 및 방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="96c90-301">View and analyze hello access, performance, and firewall logs</span></span>

<span data-ttu-id="96c90-302">Azure [로그 분석](../log-analytics/log-analytics-azure-networking-analytics.md) Blob 저장소 계정에서 hello 카운터 및 이벤트 로그 파일을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect hello counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="96c90-303">포함 시각화 및 강력한 검색 기능 tooanalyze 로그 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-303">It includes visualizations and powerful search capabilities tooanalyze your logs.</span></span>

<span data-ttu-id="96c90-304">Tooyour 저장소 계정을 연결 하 고 액세스 및 성능 로그에 대 한 hello JSON 로그 항목을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-304">You can also connect tooyour storage account and retrieve hello JSON log entries for access and performance logs.</span></span> <span data-ttu-id="96c90-305">Hello JSON 파일을 다운로드 한 후 tooCSV 변환 하 고 Excel, Power BI 또는 다른 데이터 시각화 도구에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-305">After you download hello JSON files, you can convert them tooCSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="96c90-306">Visual Studio 및 C#의 변수 및 상수에 대 한 값 변경의 기본 개념에 잘 알고 있다면 hello를 사용할 수 있습니다 [변환기 도구 로그](https://github.com/Azure-Samples/networking-dotnet-log-converter) GitHub에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use hello [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="96c90-307">메트릭</span><span class="sxs-lookup"><span data-stu-id="96c90-307">Metrics</span></span>

<span data-ttu-id="96c90-308">메트릭은 hello 포털에서 성능 카운터를 볼 수 있는 특정 Azure 리소스에 대 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-308">Metrics are a feature for certain Azure resources where you can view performance counters in hello portal.</span></span> <span data-ttu-id="96c90-309">Application Gateway의 경우 현재 메트릭 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="96c90-310">이 메트릭은 처리량, 이며 hello 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-310">This metric is throughput, and you can see it in hello portal.</span></span> <span data-ttu-id="96c90-311">Tooan 응용 프로그램 게이트웨이 찾아 클릭 **메트릭**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-311">Browse tooan application gateway and click **Metrics**.</span></span> <span data-ttu-id="96c90-312">tooview hello 값, 선택 hello 처리량 **사용 가능한 메트릭** 섹션.</span><span class="sxs-lookup"><span data-stu-id="96c90-312">tooview hello values, select throughput in hello **Available metrics** section.</span></span> <span data-ttu-id="96c90-313">다음 이미지는 hello, 다른 시간 범위에서 toodisplay hello 데이터를 사용할 수 있는 hello 필터 인 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-313">In hello following image, you can see an example with hello filters that you can use toodisplay hello data in different time ranges.</span></span>

![필터가 있는 메트릭 보기][5]

<span data-ttu-id="96c90-315">toosee 메트릭, 현재 목록을 참조 [지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-315">toosee a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="96c90-316">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="96c90-316">Alert rules</span></span>

<span data-ttu-id="96c90-317">리소스에 대한 메트릭을 기반으로 하는 경고 규칙을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="96c90-318">예를 들어 경고는 webhook을 호출 하거나 hello 응용 프로그램 게이트웨이의 hello 처리량 위, 아래 또는 임계값에 대 한 경우 지정된 된 기간 동안 관리자가 전자 메일로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-318">For example, an alert can call a webhook or email an administrator if hello throughput of hello application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="96c90-319">다음 예제는 hello 임계값 a 처리량 위반 후 tooan 관리자 전자 메일을 보내는 경고 규칙을 만드는 과정을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-319">hello following example walks you through creating an alert rule that sends an email tooan administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="96c90-320">클릭 **추가 메트릭 경고** tooopen hello **규칙 추가** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-320">Click **Add metric alert** tooopen hello **Add rule** blade.</span></span> <span data-ttu-id="96c90-321">이 블레이드 hello 메트릭 블레이드에서 에서도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-321">You can also reach this blade from hello metrics blade.</span></span>

   !["메트릭 경고 추가" 단추][6]

2. <span data-ttu-id="96c90-323">Hello에 **규칙 추가** 블레이드에서 hello 이름, 조건, 작성 및 섹션을 알리고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-323">On hello **Add rule** blade, fill out hello name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="96c90-324">Hello에 **조건** 선택기, 4 hello 값 중 하나를 선택: **보다 큰**, **보다 크거나 같은**, **미만**, 또는  **보다 작거나**합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-324">In hello **Condition** selector, select one of hello four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="96c90-325">Hello에 **기간** 선택기에 선택 5에서 기간 too6 시간을 분입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-325">In hello **Period** selector, select a period from 5 minutes too6 hours.</span></span>

   * <span data-ttu-id="96c90-326">선택 하는 경우 **소유자, 참가자 및 독자를 전자 메일로 보내기**, hello 전자 메일 수 동적 toothat 리소스 액세스 권한이 있는 hello 사용자를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-326">If you select **Email owners, contributors, and readers**, hello email can be dynamic based on hello users who have access toothat resource.</span></span> <span data-ttu-id="96c90-327">Hello에 있는 사용자의 쉼표로 구분 된 목록을 제공할 수는 그렇지 않은 경우 **추가 관리자 email(s)** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-327">Otherwise, you can provide a comma-separated list of users in hello **Additional administrator email(s)** box.</span></span>

   ![규칙 추가 블레이드][7]

<span data-ttu-id="96c90-329">Hello 임계값 위반 되 면 다음 이미지는 hello에 비슷한 toohello 하나는 전자 메일 도착 하면:</span><span class="sxs-lookup"><span data-stu-id="96c90-329">If hello threshold is breached, an email that's similar toohello one in hello following image arrives:</span></span>

![위반된 임계값에 대한 전자 메일][8]

<span data-ttu-id="96c90-331">메트릭 경고를 만들면 경고 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="96c90-332">모든 hello 경고 규칙에 대 한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-332">It provides an overview of all hello alert rules.</span></span>

![경고 및 규칙 목록][9]

<span data-ttu-id="96c90-334">경고 알림에 대해 더 toolearn 참조 [경고 알림의 받을](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-334">toolearn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="96c90-335">webhook 및 경고에를 사용 하는 방법에 대해 자세히 toounderstand 방문 [Azure 메트릭 경고에는 webhook 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="96c90-335">toounderstand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96c90-336">다음 단계</span><span class="sxs-lookup"><span data-stu-id="96c90-336">Next steps</span></span>

* <span data-ttu-id="96c90-337">[Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)를 사용하여 카운터 및 이벤트 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="96c90-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="96c90-338">[Power BI를 사용하여 Azure 활동 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="96c90-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="96c90-339">[Power BI 등에서 Azure 활동 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="96c90-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
