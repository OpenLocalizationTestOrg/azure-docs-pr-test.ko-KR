---
title: "로그 분석에서 네트워킹 분석 솔루션 aaaAzure | Microsoft Docs"
description: "Hello 로그 분석 tooreview Azure 네트워크 보안 그룹 로그 및 Azure 응용 프로그램 게이트웨이 로그에서 Azure 네트워킹 분석 솔루션을 사용할 수 있습니다."
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
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="1f95b-103">Log Analytics의 Azure 네트워킹 모니터링 솔루션</span><span class="sxs-lookup"><span data-stu-id="1f95b-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="1f95b-104">로그 분석은 hello 다음 실제 네트워크 모니터링을 위해 솔루션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-104">Log Analytics offers hello following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="1f95b-105">NPM(네트워크 성능 모니터)</span><span class="sxs-lookup"><span data-stu-id="1f95b-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="1f95b-106">네트워크의 hello 상태 모니터</span><span class="sxs-lookup"><span data-stu-id="1f95b-106">Monitor hello health of your network</span></span>
* <span data-ttu-id="1f95b-107">Azure 응용 프로그램 게이트웨이 분석 tooreview</span><span class="sxs-lookup"><span data-stu-id="1f95b-107">Azure Application Gateway analytics tooreview</span></span>
 * <span data-ttu-id="1f95b-108">Azure Application Gateway 로그</span><span class="sxs-lookup"><span data-stu-id="1f95b-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="1f95b-109">Azure Application Gateway 메트릭</span><span class="sxs-lookup"><span data-stu-id="1f95b-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="1f95b-110">Azure 네트워크 보안 그룹 분석 tooreview</span><span class="sxs-lookup"><span data-stu-id="1f95b-110">Azure Network Security Group analytics tooreview</span></span>
 * <span data-ttu-id="1f95b-111">Azure 네트워크 보안 그룹 로그</span><span class="sxs-lookup"><span data-stu-id="1f95b-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="1f95b-112">NPM(네트워크 성능 모니터)</span><span class="sxs-lookup"><span data-stu-id="1f95b-112">Network Performance Monitor (NPM)</span></span>

<span data-ttu-id="1f95b-113">hello [네트워크 성능 모니터](log-analytics-network-performance-monitor.md) 관리 솔루션은 모니터링 솔루션 hello 상태, 가용성 및 네트워크 연결 가능성을 모니터링 하는 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-113">hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors hello health, availability and reachability of networks.</span></span>  <span data-ttu-id="1f95b-114">간의 toomonitor 사용 되는 연결입니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-114">It is used toomonitor connectivity between:</span></span>

* <span data-ttu-id="1f95b-115">공용 클라우드 및 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="1f95b-115">Public cloud and on-premises</span></span>
* <span data-ttu-id="1f95b-116">데이터 센터 및 사용자 위치(지점)</span><span class="sxs-lookup"><span data-stu-id="1f95b-116">Data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="1f95b-117">다중 계층 응용 프로그램의 다양한 계층을 호스팅하는 서브넷</span><span class="sxs-lookup"><span data-stu-id="1f95b-117">Subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="1f95b-118">자세한 내용은 [네트워크 성능 모니터](log-analytics-network-performance-monitor.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1f95b-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="1f95b-119">Azure Application Gateway 및 네트워크 보안 그룹 분석</span><span class="sxs-lookup"><span data-stu-id="1f95b-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="1f95b-120">toouse hello 솔루션:</span><span class="sxs-lookup"><span data-stu-id="1f95b-120">toouse hello solutions:</span></span>
1. <span data-ttu-id="1f95b-121">Hello 관리 솔루션 tooLog 분석을 추가 하 고</span><span class="sxs-lookup"><span data-stu-id="1f95b-121">Add hello management solution tooLog Analytics, and</span></span>
2. <span data-ttu-id="1f95b-122">진단 toodirect hello 진단 tooa 로그 분석 작업 영역을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-122">Enable diagnostics toodirect hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="1f95b-123">필요한 toowrite hello 로그 tooAzure Blob 저장소는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-123">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

<span data-ttu-id="1f95b-124">하나 또는 둘 다 응용 프로그램 게이트웨이 및 네트워크 보안 그룹에 대 한 진단 및 hello 해당 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-124">You can enable diagnostics and hello corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="1f95b-125">특정 리소스 종류에 대 한 진단 로깅을 사용 하지 않는 hello 솔루션을 설치, 해당 리소스에 대 한 hello 대시보드 블레이드 비어 있는 하 고 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-125">If you do not enable diagnostic logging for a particular resource type, but install hello solution, hello dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="1f95b-126">2017 년 1 월 hello 분석 변경 하는 응용 프로그램 게이트웨이 및 네트워크 보안 그룹 tooLog에서 로그를 보내는 방식으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-126">In January 2017, hello supported way of sending logs from Application Gateways and Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="1f95b-127">Hello 표시 되 면 **Azure 네트워킹 분석 (사용 되지 않음)** 솔루션을 너무 참조[hello 이전 네트워킹 분석 솔루션에서 마이그레이션](#migrating-from-the-old-networking-analytics-solution) toofollow 단계에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-127">If you see hello **Azure Networking Analytics (deprecated)** solution, refer too[migrating from hello old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need toofollow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="1f95b-128">Azure 네트워킹 데이터 수집 세부 정보 검토</span><span class="sxs-lookup"><span data-stu-id="1f95b-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="1f95b-129">hello Azure 응용 프로그램 게이트웨이 분석 및 네트워크 보안 그룹을 분석 관리 솔루션 hello Azure 응용 프로그램 게이트웨이 및 네트워크 보안 그룹에서 직접 진단 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-129">hello Azure Application Gateway analytics and hello Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="1f95b-130">필요한 toowrite hello 로그 tooAzure Blob 저장소 않습니다 되며 에이전트가 없습니다. 데이터 수집을 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-130">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="1f95b-131">hello 다음 표에 Azure 응용 프로그램 게이트웨이 분석 워크 로드와 hello 네트워크 보안 그룹을 분석에 대 한 데이터 수집 방법에 대 한 기타 세부 정보 및 데이터 수집 방법과 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-131">hello following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and hello Network Security Group analytics.</span></span>

| <span data-ttu-id="1f95b-132">플랫폼</span><span class="sxs-lookup"><span data-stu-id="1f95b-132">Platform</span></span> | <span data-ttu-id="1f95b-133">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="1f95b-133">Direct agent</span></span> | <span data-ttu-id="1f95b-134">Systems Center Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="1f95b-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="1f95b-135">Azure</span><span class="sxs-lookup"><span data-stu-id="1f95b-135">Azure</span></span> | <span data-ttu-id="1f95b-136">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="1f95b-136">Operations Manager required?</span></span> | <span data-ttu-id="1f95b-137">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="1f95b-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="1f95b-138">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="1f95b-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="1f95b-139">Azure</span><span class="sxs-lookup"><span data-stu-id="1f95b-139">Azure</span></span> |  |  |<span data-ttu-id="1f95b-140">&#8226;</span><span class="sxs-lookup"><span data-stu-id="1f95b-140">&#8226;</span></span> |  |  |<span data-ttu-id="1f95b-141">기록될 때</span><span class="sxs-lookup"><span data-stu-id="1f95b-141">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="1f95b-142">Log Analytics의 Azure Application Gateway 분석 솔루션</span><span class="sxs-lookup"><span data-stu-id="1f95b-142">Azure Application Gateway analytics solution in Log Analytics</span></span>

![Azure Application Gateway 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="1f95b-144">응용 프로그램 게이트웨이 로그 다음 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-144">hello following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="1f95b-145">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="1f95b-145">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="1f95b-146">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="1f95b-146">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="1f95b-147">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="1f95b-147">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="1f95b-148">응용 프로그램 게이트웨이 hello 다음 메트릭을 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-148">hello following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="1f95b-149">5분 처리량</span><span class="sxs-lookup"><span data-stu-id="1f95b-149">5 minute throughput</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="1f95b-150">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="1f95b-150">Install and configure hello solution</span></span>
<span data-ttu-id="1f95b-151">다음 지침 tooinstall hello를 사용 하 고 hello Azure 응용 프로그램 게이트웨이 분석 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-151">Use hello following instructions tooinstall and configure hello Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="1f95b-152">Hello 분석 솔루션에서 Azure 응용 프로그램 게이트웨이 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-152">Enable hello Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="1f95b-153">Hello에 대 한 진단 로깅 사용 [응용 프로그램 게이트웨이](../application-gateway/application-gateway-diagnostics.md) toomonitor 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-153">Enable diagnostics logging for hello [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want toomonitor.</span></span>

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a><span data-ttu-id="1f95b-154">Hello 포털에서 Azure 응용 프로그램 게이트웨이 진단을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="1f95b-154">Enable Azure Application Gateway diagnostics in hello portal</span></span>

1. <span data-ttu-id="1f95b-155">Hello Azure 포털에서에서 응용 프로그램 게이트웨이 리소스 toomonitor toohello 이동</span><span class="sxs-lookup"><span data-stu-id="1f95b-155">In hello Azure portal, navigate toohello Application Gateway resource toomonitor</span></span>
2. <span data-ttu-id="1f95b-156">선택 *진단 로그* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="1f95b-156">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="1f95b-158">클릭 *진단을 설정* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="1f95b-158">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure Application Gateway 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="1f95b-160">진단, tooturn 클릭 *에* 아래 *상태*</span><span class="sxs-lookup"><span data-stu-id="1f95b-160">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="1f95b-161">에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*</span><span class="sxs-lookup"><span data-stu-id="1f95b-161">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="1f95b-162">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-162">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="1f95b-163">Hello 확인란 아래에서 클릭 하 여 **로그** 각 로그 형식 toocollect hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="1f95b-163">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="1f95b-164">클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅</span><span class="sxs-lookup"><span data-stu-id="1f95b-164">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="1f95b-165">PowerShell을 사용하여 Azure 네트워크 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="1f95b-165">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="1f95b-166">PowerShell 스크립트 뒤 hello 방법의 예를 제공 합니다. 응용 프로그램 게이트웨이에 대 한 진단 로깅을 tooenable 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-166">hello following PowerShell script provides an example of how tooenable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="1f95b-167">Azure Application Gateway 분석 사용</span><span class="sxs-lookup"><span data-stu-id="1f95b-167">Use Azure Application Gateway analytics</span></span>
![Azure Application Gateway 분석 타일 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="1f95b-169">Hello를 클릭 한 후 **Azure 응용 프로그램 게이트웨이 분석** 타일 개요 hello에 요약의 로그를 확인 하 고 다음 드릴 수 hello 다음 범주에 대 한 toodetails에서:</span><span class="sxs-lookup"><span data-stu-id="1f95b-169">After you click hello **Azure Application Gateway analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="1f95b-170">Application Gateway 액세스 로그</span><span class="sxs-lookup"><span data-stu-id="1f95b-170">Application Gateway Access logs</span></span>
  * <span data-ttu-id="1f95b-171">Application Gateway 액세스 로그에 대한 클라이언트 및 서버 오류</span><span class="sxs-lookup"><span data-stu-id="1f95b-171">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="1f95b-172">각 Application Gateway의 시간당 요청</span><span class="sxs-lookup"><span data-stu-id="1f95b-172">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="1f95b-173">각 Application Gateway의 시간당 실패한 요청</span><span class="sxs-lookup"><span data-stu-id="1f95b-173">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="1f95b-174">Application Gateway에 대한 사용자 에이전트별 오류</span><span class="sxs-lookup"><span data-stu-id="1f95b-174">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="1f95b-175">Application Gateway 성능 </span><span class="sxs-lookup"><span data-stu-id="1f95b-175">Application Gateway performance</span></span>
  * <span data-ttu-id="1f95b-176">Application Gateway에 대한 호스트 상태</span><span class="sxs-lookup"><span data-stu-id="1f95b-176">Host health for Application Gateway</span></span>
  * <span data-ttu-id="1f95b-177">Application Gateway 실패한 요청에 대해 최대값 및 95번째 백분위수</span><span class="sxs-lookup"><span data-stu-id="1f95b-177">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure Application Gateway 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="1f95b-180">Hello에 **Azure 응용 프로그램 게이트웨이 분석** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-180">On hello **Azure Application Gateway analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="1f95b-181">Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-181">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="1f95b-182">패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-182">You can also filter by facets toonarrow hello results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="1f95b-183">Log Analytics의 Azure 네트워크 보안 그룹 분석 솔루션</span><span class="sxs-lookup"><span data-stu-id="1f95b-183">Azure Network Security Group analytics solution in Log Analytics</span></span>

![Azure 네트워크 보안 그룹 분석 기호](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

<span data-ttu-id="1f95b-185">다음 로그 hello 네트워크 보안 그룹에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-185">hello following logs are supported for network security groups:</span></span>

* <span data-ttu-id="1f95b-186">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="1f95b-186">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="1f95b-187">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="1f95b-187">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-hello-solution"></a><span data-ttu-id="1f95b-188">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="1f95b-188">Install and configure hello solution</span></span>
<span data-ttu-id="1f95b-189">다음 지침 tooinstall hello를 사용 하 여 하 고 hello Azure 네트워킹 분석 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-189">Use hello following instructions tooinstall and configure hello Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="1f95b-190">Hello 분석 솔루션에서 Azure 네트워크 보안 그룹을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-190">Enable hello Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="1f95b-191">Hello에 대 한 진단 로깅 사용 [네트워크 보안 그룹](../virtual-network/virtual-network-nsg-manage-log.md) toomonitor 원하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-191">Enable diagnostics logging for hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want toomonitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a><span data-ttu-id="1f95b-192">Hello 포털에서 Azure 네트워크 보안 그룹 진단 사용</span><span class="sxs-lookup"><span data-stu-id="1f95b-192">Enable Azure network security group diagnostics in hello portal</span></span>

1. <span data-ttu-id="1f95b-193">Hello Azure 포털에서에서 네트워크 보안 그룹 리소스 toomonitor toohello 이동</span><span class="sxs-lookup"><span data-stu-id="1f95b-193">In hello Azure portal, navigate toohello Network Security Group resource toomonitor</span></span>
2. <span data-ttu-id="1f95b-194">선택 *진단 로그* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="1f95b-194">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="1f95b-196">클릭 *진단을 설정* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="1f95b-196">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure 네트워크 보안 그룹 리소스 이미지](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="1f95b-198">진단, tooturn 클릭 *에* 아래 *상태*</span><span class="sxs-lookup"><span data-stu-id="1f95b-198">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="1f95b-199">에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*</span><span class="sxs-lookup"><span data-stu-id="1f95b-199">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="1f95b-200">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-200">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="1f95b-201">Hello 확인란 아래에서 클릭 하 여 **로그** 각 로그 형식 toocollect hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="1f95b-201">Click hello checkbox under **Log** for each of hello log types toocollect</span></span>
8. <span data-ttu-id="1f95b-202">클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅</span><span class="sxs-lookup"><span data-stu-id="1f95b-202">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="1f95b-203">PowerShell을 사용하여 Azure 네트워크 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="1f95b-203">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="1f95b-204">방법의 예를 제공 하는 PowerShell 스크립트 뒤 hello tooenable 네트워크 보안 그룹에 진단 로깅</span><span class="sxs-lookup"><span data-stu-id="1f95b-204">hello following PowerShell script provides an example of how tooenable diagnostic logging for network security groups</span></span>
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="1f95b-205">Azure 네트워크 보안 그룹 분석 사용</span><span class="sxs-lookup"><span data-stu-id="1f95b-205">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="1f95b-206">Hello를 클릭 한 후 **Azure 네트워크 보안 그룹 분석** 타일 개요 hello에 요약의 로그를 확인 하 고 다음 드릴 수 hello 다음 범주에 대 한 toodetails에서:</span><span class="sxs-lookup"><span data-stu-id="1f95b-206">After you click hello **Azure Network Security Group analytics** tile on hello Overview, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="1f95b-207">네트워크 보안 그룹 차단 흐름</span><span class="sxs-lookup"><span data-stu-id="1f95b-207">Network security group blocked flows</span></span>
  * <span data-ttu-id="1f95b-208">차단된 흐름이 있는 네트워크 보안 그룹 규칙</span><span class="sxs-lookup"><span data-stu-id="1f95b-208">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="1f95b-209">차단된 흐름이 있는 MAC 주소 </span><span class="sxs-lookup"><span data-stu-id="1f95b-209">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="1f95b-210">네트워크 보안 그룹 허용 흐름</span><span class="sxs-lookup"><span data-stu-id="1f95b-210">Network security group allowed flows</span></span>
  * <span data-ttu-id="1f95b-211">허용된 흐름이 있는 네트워크 보안 그룹 규칙</span><span class="sxs-lookup"><span data-stu-id="1f95b-211">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="1f95b-212">허용된 흐름이 있는 MAC 주소 </span><span class="sxs-lookup"><span data-stu-id="1f95b-212">MAC addresses with allowed flows</span></span>

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 네트워크 보안 그룹 분석 대시보드 이미지](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="1f95b-215">Hello에 **Azure 네트워크 보안 그룹을 분석** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-215">On hello **Azure Network Security Group analytics** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information on hello log search page.</span></span>

<span data-ttu-id="1f95b-216">Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-216">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="1f95b-217">패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-217">You can also filter by facets toonarrow hello results.</span></span>

## <a name="migrating-from-hello-old-networking-analytics-solution"></a><span data-ttu-id="1f95b-218">Hello 이전 네트워킹 분석 솔루션에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1f95b-218">Migrating from hello old Networking Analytics solution</span></span>
<span data-ttu-id="1f95b-219">2017 년 1 월 hello 분석 변경 하는 Azure 응용 프로그램 게이트웨이 및 Azure 네트워크 보안 그룹 tooLog에서 로그를 보내는 방식으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-219">In January 2017, hello supported way of sending logs from Azure Application Gateways and Azure Network Security Groups tooLog Analytics changed.</span></span> <span data-ttu-id="1f95b-220">이러한 변경 내용은 다음 장점 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-220">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="1f95b-221">직접 hello 없이 tooLog 분석 필요 toouse 저장소 계정 로그가 기록</span><span class="sxs-lookup"><span data-stu-id="1f95b-221">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="1f95b-222">로그가 hello 시간에서 대기 시간이 짧습니다 생성 toothem 로그 분석에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-222">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="1f95b-223">구성 단계 감소</span><span class="sxs-lookup"><span data-stu-id="1f95b-223">Fewer configuration steps</span></span>
+ <span data-ttu-id="1f95b-224">모든 유형의 Azure 진단을 위한 공통 형식</span><span class="sxs-lookup"><span data-stu-id="1f95b-224">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="1f95b-225">toouse hello 솔루션을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-225">toouse hello updated solutions:</span></span>

1. [<span data-ttu-id="1f95b-226">Azure 응용 프로그램 게이트웨이에서 tooLog 분석을 직접 전송 하는 진단 toobe 구성</span><span class="sxs-lookup"><span data-stu-id="1f95b-226">Configure diagnostics toobe sent directly tooLog Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="1f95b-227">진단 toobe Azure 네트워크 보안 그룹의 직접 tooLog 분석 전송 구성</span><span class="sxs-lookup"><span data-stu-id="1f95b-227">Configure diagnostics toobe sent directly tooLog Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="1f95b-228">Hello를 사용 하도록 설정 *Azure 응용 프로그램 게이트웨이 분석* 및 hello *Azure 네트워크 보안 그룹 분석* hello 프로세스를 사용 하 여 솔루션에 설명 된 [의 추가 로그 분석 솔루션 hello 솔루션 갤러리](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="1f95b-228">Enable hello *Azure Application Gateway Analytics* and hello *Azure Network Security Group Analytics* solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="1f95b-229">모든 저장 된 쿼리, 대시보드, 또는 경고 toouse hello 새 데이터 형식 업데이트</span><span class="sxs-lookup"><span data-stu-id="1f95b-229">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="1f95b-230">형식은 tooAzureDiagnostics 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-230">Type is tooAzureDiagnostics.</span></span> <span data-ttu-id="1f95b-231">Hello ResourceType toofilter tooAzure 네트워킹 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-231">You can use hello ResourceType toofilter tooAzure networking logs.</span></span>

    | <span data-ttu-id="1f95b-232">다음 위치 대신</span><span class="sxs-lookup"><span data-stu-id="1f95b-232">Instead of:</span></span> | <span data-ttu-id="1f95b-233">사용:</span><span class="sxs-lookup"><span data-stu-id="1f95b-233">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + <span data-ttu-id="1f95b-234">접미사가 있는 모든 필드에 대 한 \_s, \_d, 또는 \_g hello 이름 hello 첫 번째 문자 toolower 대/소문자 변경</span><span class="sxs-lookup"><span data-stu-id="1f95b-234">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
   + <span data-ttu-id="1f95b-235">접미사가 있는 모든 필드에 대 한 \_o hello 데이터 이름에는 중첩 된 hello 필드 이름을 기반으로 하는 개별 필드도 나누어집니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-235">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span>
4. <span data-ttu-id="1f95b-236">Hello 제거 *Azure 네트워킹 분석 (사용 되지 않음)* 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-236">Remove hello *Azure Networking Analytics (Deprecated)* solution.</span></span>
  + <span data-ttu-id="1f95b-237">PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-237">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span>

<span data-ttu-id="1f95b-238">데이터는 수집 전에 hello 변경이 hello 새 솔루션에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-238">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="1f95b-239">기존 형식 및 필드 이름을 hello 사용 하 여이 데이터에 대 한 tooquery를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-239">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1f95b-240">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1f95b-240">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="1f95b-241">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f95b-241">Next steps</span></span>
* <span data-ttu-id="1f95b-242">사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Azure 진단 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f95b-242">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure diagnostics data.</span></span>
