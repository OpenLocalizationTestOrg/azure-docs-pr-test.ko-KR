---
title: "Application Gateway에 대한 액세스 로그, 성능 로그, 백 엔드 상태 및 메트릭 모니터링 | Microsoft Docs"
description: "Application Gateway에 대한 액세스 및 성능 로그를 사용하고 관리하는 방법을 알아봅니다"
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
ms.openlocfilehash: 12c252340b82aba5ee69b12db83353750782e7c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a><span data-ttu-id="7c39b-103">Application Gateway에 대한 백 엔드 상태, 진단 로그 및 메트릭</span><span class="sxs-lookup"><span data-stu-id="7c39b-103">Back-end health, diagnostic logs, and metrics for Application Gateway</span></span>

<span data-ttu-id="7c39b-104">Azure Application Gateway를 사용하여 다음과 같은 방법으로 리소스를 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-104">By using Azure Application Gateway, you can monitor resources in the following ways:</span></span>

* <span data-ttu-id="7c39b-105">[백 엔드 상태](#back-end-health) - Application Gateway는 Azure Portal과 PowerShell을 통해 백 엔드 풀에 있는 서버의 상태를 모니터링하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-105">[Back-end health](#back-end-health): Application Gateway provides the capability to monitor the health of the servers in the back-end pools through the Azure portal and through PowerShell.</span></span> <span data-ttu-id="7c39b-106">또한 성능 진단 로그를 통해 백 엔드 풀의 상태도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-106">You can also find the health of the back-end pools through the performance diagnostic logs.</span></span>

* <span data-ttu-id="7c39b-107">[로그](#diagnostic-logs) - 로그를 사용하면 모니터링하기 위해 리소스에서 성능, 액세스 및 기타 데이터를 저장하거나 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-107">[Logs](#diagnostic-logs): Logs allow for performance, access, and other data to be saved or consumed from a resource for monitoring purposes.</span></span>

* <span data-ttu-id="7c39b-108">[메트릭](#metrics) - Application Gateway에는 현재 메트릭이 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-108">[Metrics](#metrics): Application Gateway currently has one metric.</span></span> <span data-ttu-id="7c39b-109">이 메트릭은 응용 프로그램 게이트웨이의 처리량을 초당 바이트 수로 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-109">This metric measures the throughput of the application gateway in bytes per second.</span></span>

## <a name="back-end-health"></a><span data-ttu-id="7c39b-110">백 엔드 상태</span><span class="sxs-lookup"><span data-stu-id="7c39b-110">Back-end health</span></span>

<span data-ttu-id="7c39b-111">Application Gateway는 포털, PowerShell 및 CLI(명령줄 인터페이스)를 통해 백 엔드 풀의 개별 멤버에 대한 상태를 모니터링하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-111">Application Gateway provides the capability to monitor the health of individual members of the back-end pools through the portal, PowerShell, and the command-line interface (CLI).</span></span> <span data-ttu-id="7c39b-112">또한 성능 진단 로그를 통해 백 엔드 풀에 대해 집계된 상태 요약도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-112">You can also find an aggregated health summary of back-end pools through the performance diagnostic logs.</span></span> 

<span data-ttu-id="7c39b-113">백 엔드 상태 보고서는 백 엔드 인스턴스에 대한 Application Gateway 상태 프로브의 결과를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-113">The back-end health report reflects the output of the Application Gateway health probe to the back-end instances.</span></span> <span data-ttu-id="7c39b-114">프로브가 성공하고 백 엔드에서 트래픽을 받을 수 있으면 정상 상태로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-114">When probing is successful and the back end can receive traffic, it's considered healthy.</span></span> <span data-ttu-id="7c39b-115">그렇지 않으면 비정상 상태로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-115">Otherwise, it's considered unhealthy.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c39b-116">Application Gateway 서브넷에 NSG(네트워크 보안 그룹)가 있는 경우 인바운드 트래픽을 위해 Application Gateway 서브넷에서 65503-65534 포트 범위를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-116">If there is a network security group (NSG) on an Application Gateway subnet, open port ranges 65503-65534 on the Application Gateway subnet for inbound traffic.</span></span> <span data-ttu-id="7c39b-117">백 엔드 상태 API가 제대로 작동하는 데 이러한 포트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-117">These ports are required for the back-end health API to work.</span></span>


### <a name="view-back-end-health-through-the-portal"></a><span data-ttu-id="7c39b-118">포털을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="7c39b-118">View back-end health through the portal</span></span>

<span data-ttu-id="7c39b-119">포털에서는 백 엔드 상태를 자동으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-119">In the portal, back-end health is provided automatically.</span></span> <span data-ttu-id="7c39b-120">기존 응용 프로그램 게이트웨이에서 **모니터링** > **백 엔드 상태**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-120">In an existing application gateway, select **Monitoring** > **Backend health**.</span></span> 

<span data-ttu-id="7c39b-121">NIC, IP 또는 FQDN과 관계 없이 백 엔드 풀의 각 멤버가 이 페이지에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-121">Each member in the back-end pool is listed on this page (whether it's a NIC, IP, or FQDN).</span></span> <span data-ttu-id="7c39b-122">백 엔드 풀 이름, 포트, 백 엔드 HTTP 설정 이름 및 상태도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-122">Back-end pool name, port, back-end HTTP settings name, and health status are shown.</span></span> <span data-ttu-id="7c39b-123">상태의 유효한 값은 **정상**, **비정상** 및 **알 수 없음**입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-123">Valid values for health status are **Healthy**, **Unhealthy**, and **Unknown**.</span></span>

> [!NOTE]
> <span data-ttu-id="7c39b-124">백 엔드 상태가 **알 수 없음**이면 백 엔드에 대한 액세스가 가상 네트워크의 NSG 규칙, UDR(사용자 정의 경로) 또는 사용자 지정 DNS에 의해 차단되지 않도록 합니다 .</span><span class="sxs-lookup"><span data-stu-id="7c39b-124">If you see a back-end health status of **Unknown**, ensure that access to the back end is not blocked by an NSG rule, a user-defined route (UDR), or a custom DNS in the virtual network.</span></span>

![백 엔드 상태][10]

### <a name="view-back-end-health-through-powershell"></a><span data-ttu-id="7c39b-126">PowerShell을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="7c39b-126">View back-end health through PowerShell</span></span>

<span data-ttu-id="7c39b-127">다음 PowerShell 코드에서는 `Get-AzureRmApplicationGatewayBackendHealth` cmdlet을 사용하여 백 엔드 상태를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-127">The following PowerShell code shows how to view back-end health by using the `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:</span></span>

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a><span data-ttu-id="7c39b-128">Azure CLI 2.0을 통해 백 엔드 상태 보기</span><span class="sxs-lookup"><span data-stu-id="7c39b-128">View back-end health through Azure CLI 2.0</span></span>

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a><span data-ttu-id="7c39b-129">결과</span><span class="sxs-lookup"><span data-stu-id="7c39b-129">Results</span></span>

<span data-ttu-id="7c39b-130">다음은 응답의 예제를 보여 주는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-130">The following snippet shows an example of the response:</span></span>

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

## <span data-ttu-id="7c39b-131"><a name="diagnostic-logging"></a>진단 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-131"><a name="diagnostic-logging"></a>Diagnostic logs</span></span>

<span data-ttu-id="7c39b-132">Azure에서 다양한 유형의 로그를 사용하여 Application Gateway를 관리하고 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-132">You can use different types of logs in Azure to manage and troubleshoot application gateways.</span></span> <span data-ttu-id="7c39b-133">이러한 로그 중 일부는 포털을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-133">You can access some of these logs through the portal.</span></span> <span data-ttu-id="7c39b-134">모든 로그는 Azure Blob 저장소에서 추출하고 다양한 도구(예: [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md),Excel 및 Power BI)에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-134">All logs can be extracted from Azure Blob storage and viewed in different tools, such as [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel, and Power BI.</span></span> <span data-ttu-id="7c39b-135">다음 목록에서 다른 종류의 로그에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-135">You can learn more about the different types of logs from the following list:</span></span>

* <span data-ttu-id="7c39b-136">**활동 로그** - [Azure 활동 로그](../monitoring-and-diagnostics/insights-debugging-with-events.md)(이전의 작업 로그 및 감사 로그)를 사용하여 Azure 구독에 제출된 모든 작업과 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-136">**Activity log**: You can use [Azure activity logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as operational logs and audit logs) to view all operations that are submitted to your Azure subscription, and their status.</span></span> <span data-ttu-id="7c39b-137">활동 로그 항목은 기본적으로 수집되고 Azure Portal에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-137">Activity log entries are collected by default, and you can view them in the Azure portal.</span></span>
* <span data-ttu-id="7c39b-138">**액세스 로그** - 이 로그를 사용하여 Application Gateway 액세스 패턴을 확인하고 호출자의 IP, 요청된 URL, 응답 대기 시간, 반환 코드, 입/출력 바이트 수 등 중요한 정보를 분석할 수 있습니다. 액세스 로그는 300초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-138">**Access log**: You can use this log to view Application Gateway access patterns and analyze important information, including the caller's IP, requested URL, response latency, return code, and bytes in and out. An access log is collected every 300 seconds.</span></span> <span data-ttu-id="7c39b-139">이 로그에는 Application Gateway 인스턴스당 하나의 레코드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-139">This log contains one record per instance of Application Gateway.</span></span> <span data-ttu-id="7c39b-140">Application Gateway 인스턴스는 'instanceId' 속성으로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-140">The Application Gateway instance can be identified by the instanceId property.</span></span>
* <span data-ttu-id="7c39b-141">**성능 로그** - 이 로그를 사용하여 Application Gateway 인스턴스를 수행하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-141">**Performance log**: You can use this log to view how Application Gateway instances are performing.</span></span> <span data-ttu-id="7c39b-142">이 로그는 인스턴스 단위로 처리된 총 요청 수, 처리량(바이트), 실패한 요청 수, 정상 및 비정상 백 엔드 인스턴스 수 등의 성능 정보를 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-142">This log captures performance information for each instance, including total requests served, throughput in bytes, total requests served, failed request count, and healthy and unhealthy back-end instance count.</span></span> <span data-ttu-id="7c39b-143">성능 로그는 60초마다 수집됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-143">A performance log is collected every 60 seconds.</span></span>
* <span data-ttu-id="7c39b-144">**방화벽 로그** - 이 로그를 사용하면 웹 응용 프로그램 방화벽으로 구성된 응용 프로그램 게이트웨이의 검색 모드 또는 방지 모드를 통해 로깅된 요청을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-144">**Firewall log**: You can use this log to view the requests that are logged through either detection or prevention mode of an application gateway that is configured with the web application firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="7c39b-145">로그는 Azure Resource Manager 배포 모델에 배포된 리소스에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-145">Logs are available only for resources deployed in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="7c39b-146">클래식 배포 모델에서 리소스에 대한 로그를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-146">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="7c39b-147">두 모델에 대해 더 잘 이해하려면 [리소스 관리자 배포 및 클래식 배포 이해](../azure-resource-manager/resource-manager-deployment-model.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c39b-147">For a better understanding of the two models, see the [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="7c39b-148">로그 저장에는 세 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-148">You have three options for storing your logs:</span></span>

* <span data-ttu-id="7c39b-149">**저장소 계정** - 로그를 장기간 저장하고 필요할 때 검토하는 경우에 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-149">**Storage account**: Storage accounts are best used for logs when logs are stored for a longer duration and reviewed when needed.</span></span>
* <span data-ttu-id="7c39b-150">**이벤트 허브** - 다른 SEIM(보안 정보 및 이벤트 관리) 도구와 통합하여 리소스에 대한 알림을 얻을 수 있는 좋은 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-150">**Event hubs**: Event hubs are a great option for integrating with other security information and event management (SEIM) tools to get alerts on your resources.</span></span>
* <span data-ttu-id="7c39b-151">**Log Analytics** - 일반적으로 응용 프로그램을 실시간 모니터링하거나 추세를 파악하는 데 가장 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-151">**Log Analytics**: Log Analytics is best used for general real-time monitoring of your application or looking at trends.</span></span>

### <a name="enable-logging-through-powershell"></a><span data-ttu-id="7c39b-152">PowerShell을 통한 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="7c39b-152">Enable logging through PowerShell</span></span>

<span data-ttu-id="7c39b-153">활동 로깅은 모든 Resource Manager 리소스에 대해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-153">Activity logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="7c39b-154">이러한 로그를 통해 사용 가능한 데이터 수집을 시작하려면 액세스 및 성능 로깅을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-154">You must enable access and performance logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="7c39b-155">로깅을 사용하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-155">To enable logging, use the following steps:</span></span>

1. <span data-ttu-id="7c39b-156">로그 데이터를 저장할 저장소 계정의 리소스 ID를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-156">Note your storage account's resource ID, where the log data is stored.</span></span> <span data-ttu-id="7c39b-157">이 값의 형식은 /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름\>/providers/Microsoft.Storage/storageAccounts/\<저장소 계정 이름\>입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-157">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Storage/storageAccounts/\<storage account name\>.</span></span> <span data-ttu-id="7c39b-158">구독의 모든 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-158">You can use any storage account in your subscription.</span></span> <span data-ttu-id="7c39b-159">Azure Portal을 사용하여 이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-159">You can use the Azure portal to find this information.</span></span>

    ![포털: 저장소 계정의 리소스 ID](./media/application-gateway-diagnostics/diagnostics1.png)

2. <span data-ttu-id="7c39b-161">로깅을 사용할 Application Gateway의 리소스 ID를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-161">Note your application gateway's resource ID for which logging is enabled.</span></span> <span data-ttu-id="7c39b-162">이 값은 형식은 /subscriptions/\<subscriptionId\>/resourceGroups/\<리소스 그룹 이름\>/providers/Microsoft.Network/applicationGateways/\<응용 프로그램 게이트웨이 이름\>입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-162">This value is of the form: /subscriptions/\<subscriptionId\>/resourceGroups/\<resource group name\>/providers/Microsoft.Network/applicationGateways/\<application gateway name\>.</span></span> <span data-ttu-id="7c39b-163">포털을 사용하여 이 정보를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-163">You can use the portal to find this information.</span></span>

    ![포털: 응용 프로그램 게이트웨이의 리소스 ID](./media/application-gateway-diagnostics/diagnostics2.png)

3. <span data-ttu-id="7c39b-165">다음 PowerShell cmdlet을 사용하여 진단 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-165">Enable diagnostic logging by using the following PowerShell cmdlet:</span></span>

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
><span data-ttu-id="7c39b-166">활동 로그에는 별도의 저장소 계정이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-166">Activity logs do not require a separate storage account.</span></span> <span data-ttu-id="7c39b-167">액세스 및 성능 로깅에 저장소를 사용할 경우 서비스 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-167">The use of storage for access and performance logging incurs service charges.</span></span>

### <a name="enable-logging-through-the-azure-portal"></a><span data-ttu-id="7c39b-168">Azure Portal을 통한 로깅 사용</span><span class="sxs-lookup"><span data-stu-id="7c39b-168">Enable logging through the Azure portal</span></span>

1. <span data-ttu-id="7c39b-169">Azure Portal에서 리소스를 찾고 **진단 로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-169">In the Azure portal, find your resource and click **Diagnostic logs**.</span></span>

   <span data-ttu-id="7c39b-170">Application Gateway의 경우 다음 세 가지 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-170">For Application Gateway, three logs are available:</span></span>

   * <span data-ttu-id="7c39b-171">액세스 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-171">Access log</span></span>
   * <span data-ttu-id="7c39b-172">성능 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-172">Performance log</span></span>
   * <span data-ttu-id="7c39b-173">방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-173">Firewall log</span></span>

2. <span data-ttu-id="7c39b-174">데이터 수집을 시작하려면 **진단 켜기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-174">To start collecting data, click **Turn on diagnostics**.</span></span>

   ![진단 켜기][1]

3. <span data-ttu-id="7c39b-176">**진단 설정** 블레이드에서는 진단 로그에 대한 설정을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-176">The **Diagnostics settings** blade provides the settings for the diagnostic logs.</span></span> <span data-ttu-id="7c39b-177">이 예제에서 Log Analytics는 로그를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-177">In this example, Log Analytics stores the logs.</span></span> <span data-ttu-id="7c39b-178">**Log Analytics**에서 **구성**을 클릭하여 작업 영역을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-178">Click **Configure** under **Log Analytics** to configure your workspace.</span></span> <span data-ttu-id="7c39b-179">또한 이벤트 허브 및 저장소 계정을 사용하여 진단 로그를 저장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-179">You can also use event hubs and a storage account to save the diagnostic logs.</span></span>

   ![구성 프로세스 시작][2]

4. <span data-ttu-id="7c39b-181">기존 OMS(Operations Management Suite) 작업 영역을 선택하거나 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-181">Choose an existing Operations Management Suite (OMS) workspace or create a new one.</span></span> <span data-ttu-id="7c39b-182">이 예제에서는 기존 작업 영역을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-182">This example uses an existing one.</span></span>

   ![OMS 작업 영역에 대한 옵션][3]

5. <span data-ttu-id="7c39b-184">설정을 확인하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-184">Confirm the settings and click **Save**.</span></span>

   ![선택 항목이 있는 진단 설정 블레이드][4]

### <a name="activity-log"></a><span data-ttu-id="7c39b-186">활동 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-186">Activity log</span></span>

<span data-ttu-id="7c39b-187">Azure에서는 기본적으로 활동 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-187">Azure generates the activity log by default.</span></span> <span data-ttu-id="7c39b-188">이러한 로그는 Azure 이벤트 로그 저장소에 90일 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-188">The logs are preserved for 90 days in the Azure event logs store.</span></span> <span data-ttu-id="7c39b-189">[이벤트 및 활동 로그 보기](../monitoring-and-diagnostics/insights-debugging-with-events.md) 문서를 참조하여 이러한 로그에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="7c39b-189">Learn more about these logs by reading the [View events and activity log](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

### <a name="access-log"></a><span data-ttu-id="7c39b-190">액세스 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-190">Access log</span></span>

<span data-ttu-id="7c39b-191">이전 단계에서 설명한 대로 액세스 로그는 각 Application Gateway 인스턴스에서 이러한 로그를 사용하도록 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-191">The access log is generated only if you've enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="7c39b-192">데이터는 로깅을 사용하도록 설정할 때 지정한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-192">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="7c39b-193">Application Gateway의 액세스는 각각 다음 예제와 같이 JSON 형식으로 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-193">Each access of Application Gateway is logged in JSON format, as shown in the following example:</span></span>


|<span data-ttu-id="7c39b-194">값</span><span class="sxs-lookup"><span data-stu-id="7c39b-194">Value</span></span>  |<span data-ttu-id="7c39b-195">설명</span><span class="sxs-lookup"><span data-stu-id="7c39b-195">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7c39b-196">instanceId</span><span class="sxs-lookup"><span data-stu-id="7c39b-196">instanceId</span></span>     | <span data-ttu-id="7c39b-197">요청을 처리한 Application Gateway 인스턴스</span><span class="sxs-lookup"><span data-stu-id="7c39b-197">Application Gateway instance that served the request.</span></span>        |
|<span data-ttu-id="7c39b-198">clientIP</span><span class="sxs-lookup"><span data-stu-id="7c39b-198">clientIP</span></span>     | <span data-ttu-id="7c39b-199">요청에 대한 원래 IP</span><span class="sxs-lookup"><span data-stu-id="7c39b-199">Originating IP for the request.</span></span>        |
|<span data-ttu-id="7c39b-200">clientPort</span><span class="sxs-lookup"><span data-stu-id="7c39b-200">clientPort</span></span>     | <span data-ttu-id="7c39b-201">요청에 대한 원래 포트</span><span class="sxs-lookup"><span data-stu-id="7c39b-201">Originating port for the request.</span></span>       |
|<span data-ttu-id="7c39b-202">httpMethod</span><span class="sxs-lookup"><span data-stu-id="7c39b-202">httpMethod</span></span>     | <span data-ttu-id="7c39b-203">요청에서 사용된 HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="7c39b-203">HTTP method used by the request.</span></span>       |
|<span data-ttu-id="7c39b-204">requestUri</span><span class="sxs-lookup"><span data-stu-id="7c39b-204">requestUri</span></span>     | <span data-ttu-id="7c39b-205">받은 요청의 URI</span><span class="sxs-lookup"><span data-stu-id="7c39b-205">URI of the received request.</span></span>        |
|<span data-ttu-id="7c39b-206">RequestQuery</span><span class="sxs-lookup"><span data-stu-id="7c39b-206">RequestQuery</span></span>     | <span data-ttu-id="7c39b-207">**Server-Routed**: 요청을 보낸 백 엔드 풀 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-207">**Server-Routed**: Back-end pool instance that was sent the request.</span></span> </br> <span data-ttu-id="7c39b-208">**X-AzureApplicationGateway-LOG-ID**: 요청에 사용된 상관 관계 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-208">**X-AzureApplicationGateway-LOG-ID**: Correlation ID used for the request.</span></span> <span data-ttu-id="7c39b-209">백 엔드 서버에서 트래픽 문제를 해결하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-209">It can be used to troubleshoot traffic issues on the back-end servers.</span></span> </br><span data-ttu-id="7c39b-210">**SERVER-STATUS**: Application Gateway에서 백 엔드로부터 받은 HTTP 응답 코드</span><span class="sxs-lookup"><span data-stu-id="7c39b-210">**SERVER-STATUS**: HTTP response code that Application Gateway received from the back end.</span></span>       |
|<span data-ttu-id="7c39b-211">UserAgent</span><span class="sxs-lookup"><span data-stu-id="7c39b-211">UserAgent</span></span>     | <span data-ttu-id="7c39b-212">HTTP 요청 헤더의 사용자 에이전트</span><span class="sxs-lookup"><span data-stu-id="7c39b-212">User agent from the HTTP request header.</span></span>        |
|<span data-ttu-id="7c39b-213">httpStatus</span><span class="sxs-lookup"><span data-stu-id="7c39b-213">httpStatus</span></span>     | <span data-ttu-id="7c39b-214">Application Gateway에서 클라이언트로 반환한 HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="7c39b-214">HTTP status code returned to the client from Application Gateway.</span></span>       |
|<span data-ttu-id="7c39b-215">httpVersion</span><span class="sxs-lookup"><span data-stu-id="7c39b-215">httpVersion</span></span>     | <span data-ttu-id="7c39b-216">요청의 HTTP 버전</span><span class="sxs-lookup"><span data-stu-id="7c39b-216">HTTP version of the request.</span></span>        |
|<span data-ttu-id="7c39b-217">receivedBytes</span><span class="sxs-lookup"><span data-stu-id="7c39b-217">receivedBytes</span></span>     | <span data-ttu-id="7c39b-218">받은 패킷의 크기(바이트)</span><span class="sxs-lookup"><span data-stu-id="7c39b-218">Size of packet received, in bytes.</span></span>        |
|<span data-ttu-id="7c39b-219">sentBytes</span><span class="sxs-lookup"><span data-stu-id="7c39b-219">sentBytes</span></span>| <span data-ttu-id="7c39b-220">보낸 패킷의 크기(바이트)</span><span class="sxs-lookup"><span data-stu-id="7c39b-220">Size of packet sent, in bytes.</span></span>|
|<span data-ttu-id="7c39b-221">timeTaken</span><span class="sxs-lookup"><span data-stu-id="7c39b-221">timeTaken</span></span>| <span data-ttu-id="7c39b-222">요청을 처리하고 응답을 보내는 데 걸리는 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-222">Length of time (in milliseconds) that it takes for a request to be processed and its response to be sent.</span></span> <span data-ttu-id="7c39b-223">이 값은 Application Gateway에서 HTTP 요청의 첫 번째 바이트를 받은 시점부터 응답 보내기 작업을 완료하는 시점까지의 간격으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-223">This is calculated as the interval from the time when Application Gateway receives the first byte of an HTTP request to the time when the response send operation finishes.</span></span> <span data-ttu-id="7c39b-224">걸린 시간(Time-Taken) 필드에는 대개 요청 및 응답 패킷이 네트워크를 통해 이동하는 시간이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-224">It's important to note that the Time-Taken field usually includes the time that the request and response packets are traveling over the network.</span></span> |
|<span data-ttu-id="7c39b-225">sslEnabled</span><span class="sxs-lookup"><span data-stu-id="7c39b-225">sslEnabled</span></span>| <span data-ttu-id="7c39b-226">백 엔드 풀에 대한 통신에서 SSL이 사용되었는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-226">Whether communication to the back-end pools used SSL.</span></span> <span data-ttu-id="7c39b-227">유효한 값은 on과 off입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-227">Valid values are on and off.</span></span>|
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

### <a name="performance-log"></a><span data-ttu-id="7c39b-228">성능 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-228">Performance log</span></span>

<span data-ttu-id="7c39b-229">이전 단계에서 설명한 대로 성능 로그는 각 Application Gateway 인스턴스에서 이러한 로그를 사용하도록 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-229">The performance log is generated only if you have enabled it on each Application Gateway instance, as detailed in the preceding steps.</span></span> <span data-ttu-id="7c39b-230">데이터는 로깅을 사용하도록 설정할 때 지정한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-230">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="7c39b-231">성능 로그 데이터는 1분 간격으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-231">The performance log data is generated in 1-minute intervals.</span></span> <span data-ttu-id="7c39b-232">다음 데이터가 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-232">The following data is logged:</span></span>


|<span data-ttu-id="7c39b-233">값</span><span class="sxs-lookup"><span data-stu-id="7c39b-233">Value</span></span>  |<span data-ttu-id="7c39b-234">설명</span><span class="sxs-lookup"><span data-stu-id="7c39b-234">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7c39b-235">instanceId</span><span class="sxs-lookup"><span data-stu-id="7c39b-235">instanceId</span></span>     |  <span data-ttu-id="7c39b-236">성능 데이터가 생성되는 Application Gateway 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-236">Application Gateway instance for which performance data is being generated.</span></span> <span data-ttu-id="7c39b-237">다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-237">For a multiple-instance application gateway, there is one row per instance.</span></span>        |
|<span data-ttu-id="7c39b-238">healthyHostCount</span><span class="sxs-lookup"><span data-stu-id="7c39b-238">healthyHostCount</span></span>     | <span data-ttu-id="7c39b-239">백 엔드 풀의 정상 호스트 수</span><span class="sxs-lookup"><span data-stu-id="7c39b-239">Number of healthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="7c39b-240">unHealthyHostCount</span><span class="sxs-lookup"><span data-stu-id="7c39b-240">unHealthyHostCount</span></span>     | <span data-ttu-id="7c39b-241">백 엔드 풀의 비정상 호스트 수</span><span class="sxs-lookup"><span data-stu-id="7c39b-241">Number of unhealthy hosts in the back-end pool.</span></span>        |
|<span data-ttu-id="7c39b-242">requestCount</span><span class="sxs-lookup"><span data-stu-id="7c39b-242">requestCount</span></span>     | <span data-ttu-id="7c39b-243">처리된 요청 수</span><span class="sxs-lookup"><span data-stu-id="7c39b-243">Number of requests served.</span></span>        |
|<span data-ttu-id="7c39b-244">latency</span><span class="sxs-lookup"><span data-stu-id="7c39b-244">latency</span></span> | <span data-ttu-id="7c39b-245">인스턴스와 요청을 처리하는 백 엔드 사이의 요청 대기 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="7c39b-245">Latency (in milliseconds) of requests from the instance to the back end that serves the requests.</span></span> |
|<span data-ttu-id="7c39b-246">failedRequestCount</span><span class="sxs-lookup"><span data-stu-id="7c39b-246">failedRequestCount</span></span>| <span data-ttu-id="7c39b-247">실패한 요청 수</span><span class="sxs-lookup"><span data-stu-id="7c39b-247">Number of failed requests.</span></span>|
|<span data-ttu-id="7c39b-248">throughput</span><span class="sxs-lookup"><span data-stu-id="7c39b-248">throughput</span></span>| <span data-ttu-id="7c39b-249">마지막 로그 이후의 평균 처리량(초당 바이트 수로 측정됨)</span><span class="sxs-lookup"><span data-stu-id="7c39b-249">Average throughput since the last log, measured in bytes per second.</span></span>|

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
> <span data-ttu-id="7c39b-250">대기 시간은 HTTP 요청의 첫 번째 바이트를 받은 시간부터 HTTP 응답의 마지막 바이트를 보낸 시간까지 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-250">Latency is calculated from the time when the first byte of the HTTP request is received to the time when the last byte of the HTTP response is sent.</span></span> <span data-ttu-id="7c39b-251">즉 Application Gateway 처리 시간, 백 엔드로의 네트워크 사용 시간 및 백 엔드에서 요청을 처리하는 데 걸린 시간의 합계입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-251">It's the sum of the Application Gateway processing time plus the network cost to the back end, plus the time that the back end takes to process the request.</span></span>

### <a name="firewall-log"></a><span data-ttu-id="7c39b-252">방화벽 로그</span><span class="sxs-lookup"><span data-stu-id="7c39b-252">Firewall log</span></span>

<span data-ttu-id="7c39b-253">이전 단계에서 설명한 대로 방화벽 로그는 각 응용 프로그램 게이트웨이에서 이러한 로그를 사용하도록 설정한 경우에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-253">The firewall log is generated only if you have enabled it for each application gateway, as detailed in the preceding steps.</span></span> <span data-ttu-id="7c39b-254">또한 이 로그를 사용하려면 응용 프로그램 게이트웨이에서 웹 응용 프로그램 방화벽을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-254">This log also requires that the web application firewall is configured on an application gateway.</span></span> <span data-ttu-id="7c39b-255">데이터는 로깅을 사용하도록 설정할 때 지정한 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-255">The data is stored in the storage account that you specified when you enabled the logging.</span></span> <span data-ttu-id="7c39b-256">다음 데이터가 로깅됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-256">The following data is logged:</span></span>


|<span data-ttu-id="7c39b-257">값</span><span class="sxs-lookup"><span data-stu-id="7c39b-257">Value</span></span>  |<span data-ttu-id="7c39b-258">설명</span><span class="sxs-lookup"><span data-stu-id="7c39b-258">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="7c39b-259">instanceId</span><span class="sxs-lookup"><span data-stu-id="7c39b-259">instanceId</span></span>     | <span data-ttu-id="7c39b-260">방화벽 데이터가 생성되는 Application Gateway 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-260">Application Gateway instance for which firewall data is being generated.</span></span> <span data-ttu-id="7c39b-261">다중 인스턴스 응용 프로그램 게이트웨이의 경우 인스턴스마다 하나의 행이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-261">For a multiple-instance application gateway, there is one row per instance.</span></span>         |
|<span data-ttu-id="7c39b-262">clientIp</span><span class="sxs-lookup"><span data-stu-id="7c39b-262">clientIp</span></span>     |   <span data-ttu-id="7c39b-263">요청에 대한 원래 IP</span><span class="sxs-lookup"><span data-stu-id="7c39b-263">Originating IP for the request.</span></span>      |
|<span data-ttu-id="7c39b-264">clientPort</span><span class="sxs-lookup"><span data-stu-id="7c39b-264">clientPort</span></span>     |  <span data-ttu-id="7c39b-265">요청에 대한 원래 포트</span><span class="sxs-lookup"><span data-stu-id="7c39b-265">Originating port for the request.</span></span>       |
|<span data-ttu-id="7c39b-266">requestUri</span><span class="sxs-lookup"><span data-stu-id="7c39b-266">requestUri</span></span>     | <span data-ttu-id="7c39b-267">받은 요청의 URL</span><span class="sxs-lookup"><span data-stu-id="7c39b-267">URL of the received request.</span></span>       |
|<span data-ttu-id="7c39b-268">ruleSetType</span><span class="sxs-lookup"><span data-stu-id="7c39b-268">ruleSetType</span></span>     | <span data-ttu-id="7c39b-269">규칙 집합 유형이며,</span><span class="sxs-lookup"><span data-stu-id="7c39b-269">Rule set type.</span></span> <span data-ttu-id="7c39b-270">사용 가능한 값은 OWASP입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-270">The available value is OWASP.</span></span>        |
|<span data-ttu-id="7c39b-271">ruleSetVersion</span><span class="sxs-lookup"><span data-stu-id="7c39b-271">ruleSetVersion</span></span>     | <span data-ttu-id="7c39b-272">사용된 규칙 집합 버전이며,</span><span class="sxs-lookup"><span data-stu-id="7c39b-272">Rule set version used.</span></span> <span data-ttu-id="7c39b-273">사용 가능한 값은 2.2.9 및 3.0입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-273">Available values are 2.2.9 and 3.0.</span></span>     |
|<span data-ttu-id="7c39b-274">ruleId</span><span class="sxs-lookup"><span data-stu-id="7c39b-274">ruleId</span></span>     | <span data-ttu-id="7c39b-275">트리거 이벤트의 규칙 ID</span><span class="sxs-lookup"><span data-stu-id="7c39b-275">Rule ID of the triggering event.</span></span>        |
|<span data-ttu-id="7c39b-276">Message</span><span class="sxs-lookup"><span data-stu-id="7c39b-276">message</span></span>     | <span data-ttu-id="7c39b-277">사용자에게 친숙한 트리거 이벤트에 대한 메시지이며,</span><span class="sxs-lookup"><span data-stu-id="7c39b-277">User-friendly message for the triggering event.</span></span> <span data-ttu-id="7c39b-278">자세한 내용은 세부 정보 섹션에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-278">More details are provided in the details section.</span></span>        |
|<span data-ttu-id="7c39b-279">action</span><span class="sxs-lookup"><span data-stu-id="7c39b-279">action</span></span>     |  <span data-ttu-id="7c39b-280">요청에서 수행되는 동작이며,</span><span class="sxs-lookup"><span data-stu-id="7c39b-280">Action taken on the request.</span></span> <span data-ttu-id="7c39b-281">사용할 수 있는 값은 Blocked 및 Allowed입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-281">Available values are Blocked and Allowed.</span></span>      |
|<span data-ttu-id="7c39b-282">site</span><span class="sxs-lookup"><span data-stu-id="7c39b-282">site</span></span>     | <span data-ttu-id="7c39b-283">로그를 생성한 사이트이며,</span><span class="sxs-lookup"><span data-stu-id="7c39b-283">Site for which the log was generated.</span></span> <span data-ttu-id="7c39b-284">현재 규칙이 전역이므로 Global만 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-284">Currently, only Global is listed because rules are global.</span></span>|
|<span data-ttu-id="7c39b-285">세부 정보</span><span class="sxs-lookup"><span data-stu-id="7c39b-285">details</span></span>     | <span data-ttu-id="7c39b-286">트리거 이벤트의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="7c39b-286">Details of the triggering event.</span></span>        |
|<span data-ttu-id="7c39b-287">details.message</span><span class="sxs-lookup"><span data-stu-id="7c39b-287">details.message</span></span>     | <span data-ttu-id="7c39b-288">규칙에 대한 설명</span><span class="sxs-lookup"><span data-stu-id="7c39b-288">Description of the rule.</span></span>        |
|<span data-ttu-id="7c39b-289">details.data</span><span class="sxs-lookup"><span data-stu-id="7c39b-289">details.data</span></span>     | <span data-ttu-id="7c39b-290">규칙과 일치하는 요청 내 특정 데이터</span><span class="sxs-lookup"><span data-stu-id="7c39b-290">Specific data found in request that matched the rule.</span></span>         |
|<span data-ttu-id="7c39b-291">details.file</span><span class="sxs-lookup"><span data-stu-id="7c39b-291">details.file</span></span>     | <span data-ttu-id="7c39b-292">규칙이 포함된 구성 파일</span><span class="sxs-lookup"><span data-stu-id="7c39b-292">Configuration file that contained the rule.</span></span>        |
|<span data-ttu-id="7c39b-293">details.line</span><span class="sxs-lookup"><span data-stu-id="7c39b-293">details.line</span></span>     | <span data-ttu-id="7c39b-294">이벤트를 트리거한 구성 파일의 줄 번호</span><span class="sxs-lookup"><span data-stu-id="7c39b-294">Line number in the configuration file that triggered the event.</span></span>       |

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

### <a name="view-and-analyze-the-activity-log"></a><span data-ttu-id="7c39b-295">활동 로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="7c39b-295">View and analyze the activity log</span></span>

<span data-ttu-id="7c39b-296">다음 방법 중 하나를 사용하여 활동 로그 데이터를 확인하고 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-296">You can view and analyze activity log data by using any of the following methods:</span></span>

* <span data-ttu-id="7c39b-297">**Azure 도구** - Azure PowerShell, Azure CLI, Azure REST API 또는 Azure Portal을 통해 활동 로그에서 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-297">**Azure tools**: Retrieve information from the activity log through Azure PowerShell, the Azure CLI, the Azure REST API, or the Azure portal.</span></span> <span data-ttu-id="7c39b-298">각 방법에 대한 단계별 지침은 [Resource Manager의 활동 작업](../azure-resource-manager/resource-group-audit.md) 문서에 자세히 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-298">Step-by-step instructions for each method are detailed in the [Activity operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="7c39b-299">**Power BI** - [Power BI](https://powerbi.microsoft.com/pricing) 계정이 아직 없는 경우 무료로 사용해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-299">**Power BI**: If you don't already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="7c39b-300">[Power BI용 Azure Activity Logs 콘텐츠 팩](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/)을 사용하여 미리 구성된 대시보드를 그대로 사용하거나 사용자 지정하여 데이터를 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-300">By using the [Azure Activity Logs content pack for Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), you can analyze your data with preconfigured dashboards that you can use as is or customize.</span></span>

### <a name="view-and-analyze-the-access-performance-and-firewall-logs"></a><span data-ttu-id="7c39b-301">액세스, 성능 및 방화벽 로그 보기 및 분석</span><span class="sxs-lookup"><span data-stu-id="7c39b-301">View and analyze the access, performance, and firewall logs</span></span>

<span data-ttu-id="7c39b-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)는 Blob 저장소 계정에서 카운터 및 이벤트 로그 파일을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-302">Azure [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md) can collect the counter and event log files from your Blob storage account.</span></span> <span data-ttu-id="7c39b-303">여기에는 로그를 분석하는 시각화 및 강력한 검색 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-303">It includes visualizations and powerful search capabilities to analyze your logs.</span></span>

<span data-ttu-id="7c39b-304">저장소 계정에 연결하고 액세스 및 성능 로그에 대한 JSON 로그 항목을 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-304">You can also connect to your storage account and retrieve the JSON log entries for access and performance logs.</span></span> <span data-ttu-id="7c39b-305">JSON 파일을 다운로드한 후 CSV로 변환하여 Excel, Power BI 또는 기타 데이터 시각화 도구에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-305">After you download the JSON files, you can convert them to CSV and view them in Excel, Power BI, or any other data-visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="7c39b-306">Visual Studio를 익숙하게 사용할 수 있고 C#에서 상수 및 변수에 대한 값 변경에 대한 기본 개념이 있는 경우 GitHub에서 제공하는 [로그 변환기 도구](https://github.com/Azure-Samples/networking-dotnet-log-converter)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-306">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>
> 
> 

## <a name="metrics"></a><span data-ttu-id="7c39b-307">메트릭</span><span class="sxs-lookup"><span data-stu-id="7c39b-307">Metrics</span></span>

<span data-ttu-id="7c39b-308">메트릭은 포털에서 성능 카운터를 볼 수 있는 특정 Azure 리소스에 대한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-308">Metrics are a feature for certain Azure resources where you can view performance counters in the portal.</span></span> <span data-ttu-id="7c39b-309">Application Gateway의 경우 현재 메트릭 하나만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-309">For Application Gateway, one metric is available now.</span></span> <span data-ttu-id="7c39b-310">이 메트릭은 처리량이며 포털에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-310">This metric is throughput, and you can see it in the portal.</span></span> <span data-ttu-id="7c39b-311">응용 프로그램 게이트웨이를 찾아 **메트릭**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-311">Browse to an application gateway and click **Metrics**.</span></span> <span data-ttu-id="7c39b-312">값을 보려면 **사용 가능한 메트릭** 섹션에서 처리량을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-312">To view the values, select throughput in the **Available metrics** section.</span></span> <span data-ttu-id="7c39b-313">다음 이미지에서는 여러 시간 범위의 데이터를 표시하는 데 사용할 수 있는 필터가 있는 예를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-313">In the following image, you can see an example with the filters that you can use to display the data in different time ranges.</span></span>

![필터가 있는 메트릭 보기][5]

<span data-ttu-id="7c39b-315">현재 지원되는 메트릭 목록을 보려면 [Azure Monitor에서 지원되는 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c39b-315">To see a current list of metrics, see [Supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

### <a name="alert-rules"></a><span data-ttu-id="7c39b-316">경고 규칙</span><span class="sxs-lookup"><span data-stu-id="7c39b-316">Alert rules</span></span>

<span data-ttu-id="7c39b-317">리소스에 대한 메트릭을 기반으로 하는 경고 규칙을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-317">You can start alert rules based on metrics for a resource.</span></span> <span data-ttu-id="7c39b-318">예를 들어 응용 프로그램 게이트웨이의 처리량이 지정된 기간 동안 임계값보다 높거나 낮거나 같을 때 경고에서 웹후크를 호출하거나 관리자에게 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-318">For example, an alert can call a webhook or email an administrator if the throughput of the application gateway is above, below, or at a threshold for a specified period.</span></span>

<span data-ttu-id="7c39b-319">다음 예제에서는 처리량이 임계값을 위반하면 관리자에게 전자 메일을 보내는 경고 규칙을 만드는 과정을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-319">The following example walks you through creating an alert rule that sends an email to an administrator after throughput breaches a threshold:</span></span>

1. <span data-ttu-id="7c39b-320">**메트릭 경고 추가**를 클릭하여 **규칙 추가** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-320">Click **Add metric alert** to open the **Add rule** blade.</span></span> <span data-ttu-id="7c39b-321">또한 메트릭 블레이드에서 이 블레이드에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-321">You can also reach this blade from the metrics blade.</span></span>

   !["메트릭 경고 추가" 단추][6]

2. <span data-ttu-id="7c39b-323">**규칙 추가** 블레이드에서 이름, 조건 및 알림 섹션을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-323">On the **Add rule** blade, fill out the name, condition, and notify sections, and click **OK**.</span></span>

   * <span data-ttu-id="7c39b-324">**조건** 선택기에서 **보다 큼**, **보다 크거나 같음**, **보다 작음**, **보다 작거나 같음**의 네 가지 값 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-324">In the **Condition** selector, select one of the four values: **Greater than**, **Greater than or equal**, **Less than**, or **Less than or equal to**.</span></span>

   * <span data-ttu-id="7c39b-325">**기간** 선택기에서 5분에서 6시간 사이의 기간까지 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-325">In the **Period** selector, select a period from 5 minutes to 6 hours.</span></span>

   * <span data-ttu-id="7c39b-326">**전자 메일 소유자, 참가자 및 읽기 권한자**를 선택하면 해당 리소스에 액세스할 수 있는 사용자에 따라 동적으로 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-326">If you select **Email owners, contributors, and readers**, the email can be dynamic based on the users who have access to that resource.</span></span> <span data-ttu-id="7c39b-327">그렇지 않으면 **추가 관리자 전자 메일** 상자에서 쉼표로 구분된 사용자 목록을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-327">Otherwise, you can provide a comma-separated list of users in the **Additional administrator email(s)** box.</span></span>

   ![규칙 추가 블레이드][7]

<span data-ttu-id="7c39b-329">임계값을 위반하면 다음 이미지와 비슷한 전자 메일이 도착합니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-329">If the threshold is breached, an email that's similar to the one in the following image arrives:</span></span>

![위반된 임계값에 대한 전자 메일][8]

<span data-ttu-id="7c39b-331">메트릭 경고를 만들면 경고 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-331">A list of alerts appears after you create a metric alert.</span></span> <span data-ttu-id="7c39b-332">모든 경고 규칙에 대한 개요도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c39b-332">It provides an overview of all the alert rules.</span></span>

![경고 및 규칙 목록][9]

<span data-ttu-id="7c39b-334">경고 알림에 대한 자세한 내용은 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c39b-334">To learn more about alert notifications, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="7c39b-335">웹후크에 대한 자세한 내용 및 경고와 함께 웹후크를 사용하는 방법을 알아보려면 [Azure 메트릭 경고에 대한 웹후크 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c39b-335">To understand more about webhooks and how you can use them with alerts, visit [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c39b-336">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7c39b-336">Next steps</span></span>

* <span data-ttu-id="7c39b-337">[Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)를 사용하여 카운터 및 이벤트 로그 시각화</span><span class="sxs-lookup"><span data-stu-id="7c39b-337">Visualize counter and event logs by using [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>
* <span data-ttu-id="7c39b-338">[Power BI를 사용하여 Azure 활동 로그 시각화](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="7c39b-338">[Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="7c39b-339">[Power BI 등에서 Azure 활동 로그 보기 및 분석](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) 블로그 게시물</span><span class="sxs-lookup"><span data-stu-id="7c39b-339">[View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

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
