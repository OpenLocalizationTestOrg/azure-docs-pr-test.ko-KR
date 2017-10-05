---
title: "Log Analytics의 Azure Networking Analytics 솔루션 | Microsoft Docs"
description: "Log Analytics의 Azure Networking Analytics 솔루션을 사용하여 Azure 네트워크 보안 그룹 로그와 Azure Application Gateway 로그를 검토할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 06b67322b3812a668a515ecc357171ede1d85441
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="b2ff4-103">Log Analytics의 Azure 네트워킹 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="b2ff4-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="b2ff4-104">Log Analytics는 네트워크를 모니터링하기 위해 다음과 같은 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="b2ff4-105">NPM(네트워크 성능 모니터)</span><span class="sxs-lookup"><span data-stu-id="b2ff4-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="b2ff4-106">네트워크 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="b2ff4-106">Monitor the health of your network</span></span>
* <span data-ttu-id="b2ff4-107">검토할 Azure Application Gateway 분석</span><span class="sxs-lookup"><span data-stu-id="b2ff4-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="b2ff4-108">Azure Application Gateway 로그</span><span class="sxs-lookup"><span data-stu-id="b2ff4-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="b2ff4-109">Azure Application Gateway 메트릭</span><span class="sxs-lookup"><span data-stu-id="b2ff4-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="b2ff4-110">Azure 네트워크 보안 그룹 분석</span><span class="sxs-lookup"><span data-stu-id="b2ff4-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="b2ff4-111">Azure 네트워크 보안 그룹 로그</span><span class="sxs-lookup"><span data-stu-id="b2ff4-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="b2ff4-112">NPM(네트워크 성능 모니터)</span><span class="sxs-lookup"><span data-stu-id="b2ff4-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="b2ff4-113">[네트워크 성능 모니터](log-analytics-network-performance-monitor.md) 관리 솔루션은 네트워크의 상태, 가용성 및 연결 가능성을 모니터링하는 네트워크 모니터링 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="b2ff4-114">다음 항목 간의 연결을 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-114">It is used to monitor connectivity between:</span></span>

* <span data-ttu-id="b2ff4-115">공용 클라우드 및 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="b2ff4-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="b2ff4-116">데이터 센터 및 사용자 위치(지점)</span><span class="sxs-lookup"><span data-stu-id="b2ff4-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="b2ff4-117">다중 계층 응용 프로그램의 다양한 계층을 호스팅하는 서브넷</span><span class="sxs-lookup"><span data-stu-id="b2ff4-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="b2ff4-118">자세한 내용은 [네트워크 성능 모니터](log-analytics-network-performance-monitor.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="b2ff4-119">Azure Application Gateway 및 네트워크 보안 그룹 분석</span><span class="sxs-lookup"><span data-stu-id="b2ff4-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="b2ff4-120">솔루션을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="b2ff4-120">To use the solutions:</span></span>
1. <span data-ttu-id="b2ff4-121">Log Analytics에 관리 솔루션을 추가하고</span><span class="sxs-lookup"><span data-stu-id="b2ff4-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="b2ff4-122">Log Analytics 작업 영역에 대한 진단을 지시하는 진단을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="b2ff4-123">Azure Blob Storage에 로그를 작성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="b2ff4-124">Application Gateway 및 네트워킹 보안 그룹 중 하나 또는 둘 다에 대해 진단 및 해당 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="b2ff4-125">특정 리소스 유형에 진단 로깅을 사용하도록 설정하지 않고 솔루션을 설치하면 해당 리소스의 대시보드 블레이드가 비어 있고 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="b2ff4-126">2017년 1월 Application Gateway 및 네트워크 보안 그룹에서 Log Analytics로 로그를 보내도록 지원하는 방법이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="b2ff4-127">**Azure Networking Analytics(사용되지 않음)** 솔루션을 표시하는 경우 수행해야 할 단계는 [이전 Networking Analytics 솔루션에서 마이그레이션](#migrating-from-the-old-networking-analytics-solution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="b2ff4-128">Azure 네트워킹 데이터 수집 세부 정보 검토</span><span class="sxs-lookup"><span data-stu-id="b2ff4-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="b2ff4-129">Azure Application Gateway 분석 및 네트워크 보안 그룹 분석 관리 솔루션은 Azure Application Gateway 및 네트워크 보안 그룹에서 직접 진단 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="b2ff4-130">Azure Blob Storage에 로그를 작성할 필요가 없으며 데이터를 수집하는 데 에이전트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="b2ff4-131">다음 표에서는 Azure Application Gateway 분석 및 네트워크 보안 그룹 분석에서 데이터가 수집되는 방법에 대한 데이터 수집 방법 및 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="b2ff4-132">플랫폼</span><span class="sxs-lookup"><span data-stu-id="b2ff4-132">Platform</span></span> | <span data-ttu-id="b2ff4-133">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="b2ff4-133">Direct agent</span></span> | <span data-ttu-id="b2ff4-134">Systems Center Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="b2ff4-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="b2ff4-135">Azure</span><span class="sxs-lookup"><span data-stu-id="b2ff4-135">Azure</span></span> | <span data-ttu-id="b2ff4-136">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="b2ff4-136">Operations Manager required?</span></span> | <span data-ttu-id="b2ff4-137">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="b2ff4-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="b2ff4-138">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="b2ff4-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b2ff4-139">Azure</span><span class="sxs-lookup"><span data-stu-id="b2ff4-139">Azure</span></span> |  |  |<span data-ttu-id="b2ff4-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b2ff4-140">&#8226;</span></span> |  |  |<span data-ttu-id="b2ff4-141">기록될 때</span><span class="sxs-lookup"><span data-stu-id="b2ff4-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="b2ff4-142">Log Analytics의 Azure Application Gateway 분석 솔루션</span><span class="sxs-lookup"><span data-stu-id="b2ff4-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure Application Gateway 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="b2ff4-144">Application Gateway에는 다음 로그가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-144">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="b2ff4-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="b2ff4-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="b2ff4-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="b2ff4-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="b2ff4-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="b2ff4-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="b2ff4-148">Application Gateway에는 다음 메트릭이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-148">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="b2ff4-149">5분 처리량</span><span class="sxs-lookup"><span data-stu-id="b2ff4-149">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="b2ff4-150">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b2ff4-150">Install and configure the solution</span></span>
<span data-ttu-id="b2ff4-151">다음 지침을 사용하여 Azure Application Gateway 분석 솔루션을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-151">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="b2ff4-152">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Azure Application Gateway 분석 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-152">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="b2ff4-153">모니터링할 [Application Gateway](../application-gateway/application-gateway-diagnostics.md)에 대해 진단 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-153">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="b2ff4-154">포털에서 Azure Application Gateway 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="b2ff4-154">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="b2ff4-155">Azure Portal에서 모니터링할 Application Gateway 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-155">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="b2ff4-156">*진단 로그*를 선택하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-156">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="b2ff4-158">*진단 사용*을 클릭하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-158">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="b2ff4-160">진단을 사용하려면 *상태*에서 *켜기*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-160">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="b2ff4-161">*Log Analytics로 보내기* 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-161">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="b2ff4-162">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="b2ff4-163">수집할 각 로그 유형에 대해 **로그** 아래의 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-163">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="b2ff4-164">*저장*을 클릭하여 Log Analytics로의 진단 로깅을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-164">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="b2ff4-165">PowerShell을 사용하여 Azure 네트워크 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="b2ff4-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="b2ff4-166">다음 PowerShell 스크립트는 응용 프로그램 게이트웨이에 진단 로깅을 사용하도록 설정하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-166">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="b2ff4-167">Azure Application Gateway 분석 사용</span><span class="sxs-lookup"><span data-stu-id="b2ff4-167">Use Azure Application Gateway analytics</span></span>
![Azure Application Gateway 분석 타일 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="b2ff4-169">[개요]에서 **Azure Application Gateway 분석** 타일을 클릭한 후 로그 요약을 확인한 후 다음 범주에 대한 세부 정보를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-169">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="b2ff4-170">Application Gateway 액세스 로그</span><span class="sxs-lookup"><span data-stu-id="b2ff4-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="b2ff4-171">Application Gateway 액세스 로그에 대한 클라이언트 및 서버 오류</span><span class="sxs-lookup"><span data-stu-id="b2ff4-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="b2ff4-172">각 Application Gateway의 시간당 요청</span><span class="sxs-lookup"><span data-stu-id="b2ff4-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="b2ff4-173">각 Application Gateway의 시간당 실패한 요청</span><span class="sxs-lookup"><span data-stu-id="b2ff4-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="b2ff4-174">Application Gateway에 대한 사용자 에이전트별 오류</span><span class="sxs-lookup"><span data-stu-id="b2ff4-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="b2ff4-175">Application Gateway 성능 </span><span class="sxs-lookup"><span data-stu-id="b2ff4-175">Application Gateway performance</span></span>
  * <span data-ttu-id="b2ff4-176">Application Gateway에 대한 호스트 상태</span><span class="sxs-lookup"><span data-stu-id="b2ff4-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="b2ff4-177">Application Gateway 실패한 요청에 대해 최대값 및 95번째 백분위수</span><span class="sxs-lookup"><span data-stu-id="b2ff4-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="b2ff4-180">**Azure Application Gateway 분석** 대시보드의 블레이드 중 하나에서 요약 정보를 검토한 다음 하나를 클릭하여 로그 검색 페이지에서 해당 항목에 대한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-180">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="b2ff4-181">로그 검색 페이지에서, 시간별 결과, 자세한 결과 및 로그 검색 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-181">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="b2ff4-182">패싯으로 필터링하여 결과 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-182">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="b2ff4-183">Log Analytics의 Azure 네트워크 보안 그룹 분석 솔루션</span><span class="sxs-lookup"><span data-stu-id="b2ff4-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Azure 네트워크 보안 그룹 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="b2ff4-185">네트워크 보안 그룹에는 다음 로그가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-185">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="b2ff4-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="b2ff4-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="b2ff4-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="b2ff4-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="b2ff4-188">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="b2ff4-188">Install and configure the solution</span></span>
<span data-ttu-id="b2ff4-189">다음 지침을 사용하여 Azure Networking Analytics 솔루션을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-189">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="b2ff4-190">[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Azure 네트워크 보안 그룹 분석 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-190">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="b2ff4-191">모니터링할 [네트워크 보안 그룹](../virtual-network/virtual-network-nsg-manage-log.md) 리소스에 대해 진단 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-191">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="b2ff4-192">포털에서 Azure 네트워크 보안 그룹 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="b2ff4-192">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="b2ff4-193">Azure Portal에서 모니터링할 네트워크 보안 그룹 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-193">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="b2ff4-194">*진단 로그*를 선택하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-194">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="b2ff4-196">*진단 사용*을 클릭하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-196">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="b2ff4-198">진단을 사용하려면 *상태*에서 *켜기*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-198">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="b2ff4-199">*Log Analytics로 보내기* 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-199">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="b2ff4-200">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="b2ff4-201">수집할 각 로그 유형에 대해 **로그** 아래의 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-201">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="b2ff4-202">*저장*을 클릭하여 Log Analytics로의 진단 로깅을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-202">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="b2ff4-203">PowerShell을 사용하여 Azure 네트워크 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="b2ff4-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="b2ff4-204">다음 PowerShell 스크립트는 네트워크 보안 그룹에 진단 로깅을 사용하도록 설정하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-204">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="b2ff4-205">Azure 네트워크 보안 그룹 분석 사용</span><span class="sxs-lookup"><span data-stu-id="b2ff4-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="b2ff4-206">[개요]에서 **Azure 네트워크 보안 그룹 분석** 타일을 클릭한 후 로그 요약을 확인한 후 다음 범주에 대한 세부 정보를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-206">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="b2ff4-207">네트워크 보안 그룹 차단 흐름</span><span class="sxs-lookup"><span data-stu-id="b2ff4-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="b2ff4-208">차단된 흐름이 있는 네트워크 보안 그룹 규칙</span><span class="sxs-lookup"><span data-stu-id="b2ff4-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="b2ff4-209">차단된 흐름이 있는 MAC 주소 </span><span class="sxs-lookup"><span data-stu-id="b2ff4-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="b2ff4-210">네트워크 보안 그룹 허용 흐름</span><span class="sxs-lookup"><span data-stu-id="b2ff4-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="b2ff4-211">허용된 흐름이 있는 네트워크 보안 그룹 규칙</span><span class="sxs-lookup"><span data-stu-id="b2ff4-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="b2ff4-212">허용된 흐름이 있는 MAC 주소 </span><span class="sxs-lookup"><span data-stu-id="b2ff4-212">MAC addresses with allowed flows</span></span>

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="b2ff4-215">**Azure 네트워크 보안 그룹 분석** 대시보드의 블레이드 중 하나에서 요약 정보를 검토한 다음 하나를 클릭하여 로그 검색 페이지에서 해당 항목에 대한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-215">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>

<span data-ttu-id="b2ff4-216">로그 검색 페이지에서, 시간별 결과, 자세한 결과 및 로그 검색 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-216">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="b2ff4-217">패싯으로 필터링하여 결과 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-217">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="b2ff4-218">이전 Networking Analytics 솔루션에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b2ff4-218">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="b2ff4-219">2017년 1월 Azure Application Gateway 및 Azure 네트워크 보안 그룹에서 Log Analytics로 로그를 보내도록 지원하는 방법이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-219">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="b2ff4-220">이러한 변경은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-220">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="b2ff4-221">저장소 계정을 사용할 필요 없이 Log Analytics에 로그 직접 기록</span><span class="sxs-lookup"><span data-stu-id="b2ff4-221">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="b2ff4-222">Log Analytics에서 사용할 수 있는 로그가 생성된 이후의 대기 시간 감소</span><span class="sxs-lookup"><span data-stu-id="b2ff4-222">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="b2ff4-223">구성 단계 감소</span><span class="sxs-lookup"><span data-stu-id="b2ff4-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="b2ff4-224">모든 유형의 Azure 진단을 위한 공통 형식</span><span class="sxs-lookup"><span data-stu-id="b2ff4-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="b2ff4-225">업데이트된 솔루션을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-225">To use the updated solutions:</span></span>

1. <span data-ttu-id="b2ff4-226">[Azure Application Gateway에서 Log Analytics로 직접 보내도록 진단을 구성합니다](#enable-azure-application-gateway-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="b2ff4-226">[Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="b2ff4-227">[Azure 네트워크 보안 그룹에서 Log Analytics로 직접 보내도록 진단을 구성합니다](#enable-azure-network-security-group-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="b2ff4-227">[Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal)</span></span>
2. <span data-ttu-id="b2ff4-228">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 *Azure Application Gateway 분석* 및 *Azure 네트워크 보안 그룹 분석* 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-228">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="b2ff4-229">새 데이터 형식을 사용하도록 저장된 쿼리, 대시보드 또는 경고를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-229">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="b2ff4-230">형식은 AzureDiagnostics로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-230">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="b2ff4-231">ResourceType을 사용하여 Azure 네트워킹 로그로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-231">You can use the ResourceType to filter to Azure networking logs.</span></span>

    | <span data-ttu-id="b2ff4-232">다음 위치 대신</span><span class="sxs-lookup"><span data-stu-id="b2ff4-232">Instead of:</span></span> | <span data-ttu-id="b2ff4-233">사용:</span><span class="sxs-lookup"><span data-stu-id="b2ff4-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="b2ff4-234">이름에 \_s, \_d 또는 \_g 접미사가 있는 필드의 경우 첫 번째 문자를 소문자로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-234">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="b2ff4-235">이름에 \_o 접미사가 있는 모든 필드의 경우 데이터는 중첩된 필드 이름에 기반하여 개별 필드로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-235">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="b2ff4-236">*Azure Networking Analytics(사용되지 않음)* 솔루션을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-236">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="b2ff4-237">PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="b2ff4-238">변경 전에 수집된 데이터는 새 솔루션에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-238">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="b2ff4-239">이전 형식 및 필드 이름을 사용하여 이 데이터를 계속 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-239">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b2ff4-240">문제 해결</span><span class="sxs-lookup"><span data-stu-id="b2ff4-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="b2ff4-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b2ff4-241">Next steps</span></span>
* <span data-ttu-id="b2ff4-242">[Log Analytics의 로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 Azure 진단 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b2ff4-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>
