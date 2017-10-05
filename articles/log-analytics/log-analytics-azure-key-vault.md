---
title: "Log Analytics의 Azure Key Vault 솔루션 | Microsoft Docs"
description: "Log Analytics에서 Azure Key Vault 솔루션을 사용하여 Azure Key Vault 로그를 검토할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 651586e0846ffb22a23e64b73c2cc614980d9b92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="f4515-103">Log Analytics의 Azure Key Vault Analytics 솔루션</span><span class="sxs-lookup"><span data-stu-id="f4515-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Key Vault 기호](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="f4515-105">Log Analytics에서 Azure Key Vault 솔루션을 사용하여 Azure Key Vault AuditEvent 로그를 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="f4515-106">솔루션을 사용하려면 Azure Key Vault 진단 로깅을 사용하도록 설정하고 진단을 Log Analytics 작업 영역으로 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="f4515-107">Azure Blob Storage에 로그를 작성할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="f4515-108">2017년 1월 Key Vault에서 Log Analytics로 로그를 보내도록 지원하는 방법이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="f4515-109">사용 중인 Key Vault 솔루션에서 제목에 *(사용되지 않음)*을 표시하는 경우 수행해야 할 단계는 [이전 Key Vault 솔루션에서 마이그레이션](#migrating-from-the-old-key-vault-solution)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4515-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="f4515-110">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="f4515-110">Install and configure the solution</span></span>
<span data-ttu-id="f4515-111">다음 지침을 사용하여 Azure Key Vault 솔루션을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="f4515-112">[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)에서 또는 [솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Azure Key Vault 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="f4515-113">[포털](#enable-key-vault-diagnostics-in-the-portal) 또는 [PowerShell](#enable-key-vault-diagnostics-using-powershell)을 사용하여 모니터링할 Key Vault 리소스에 대한 진단 로깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="f4515-114">포털에서 Key Vault 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="f4515-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="f4515-115">Azure Portal에서 모니터링할 Key Vault 리소스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="f4515-116">*진단 로그*를 선택하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-116">Select *Diagnostics logs* to open the following page</span></span>

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="f4515-118">*진단 사용*을 클릭하여 다음 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="f4515-120">진단을 사용하려면 *상태*에서 *켜기*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="f4515-121">*Log Analytics로 보내기* 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="f4515-122">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="f4515-123">*AuditEvent* 로그를 사용하도록 설정하려면 [로그] 아래의 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="f4515-124">*저장*을 클릭하여 Log Analytics로의 진단 로깅을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="f4515-125">PowerShell을 사용하여 Key Vault 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="f4515-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="f4515-126">다음 PowerShell 스크립트는 `Set-AzureRmDiagnosticSetting`을 사용하여 Key Vault에 진단 로깅을 사용하도록 설정하는 방법에 대한 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="f4515-127">Azure Key Vault 데이터 수집 상세 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="f4515-128">Azure Key Vault 솔루션은 Key Vault에서 직접 진단 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="f4515-129">Azure Blob Storage에 로그를 작성할 필요가 없으며 데이터를 수집하는 데 에이전트가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="f4515-130">다음 표에서는 데이터 수집 방법 및 Azure Key Vault에 대해 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="f4515-131">플랫폼</span><span class="sxs-lookup"><span data-stu-id="f4515-131">Platform</span></span> | <span data-ttu-id="f4515-132">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="f4515-132">Direct agent</span></span> | <span data-ttu-id="f4515-133">Systems Center Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="f4515-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="f4515-134">Azure</span><span class="sxs-lookup"><span data-stu-id="f4515-134">Azure</span></span> | <span data-ttu-id="f4515-135">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="f4515-135">Operations Manager required?</span></span> | <span data-ttu-id="f4515-136">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="f4515-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="f4515-137">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="f4515-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="f4515-138">Azure</span><span class="sxs-lookup"><span data-stu-id="f4515-138">Azure</span></span> |  |  |<span data-ttu-id="f4515-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="f4515-139">&#8226;</span></span> |  |  | <span data-ttu-id="f4515-140">도착 시</span><span class="sxs-lookup"><span data-stu-id="f4515-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="f4515-141">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="f4515-141">Use Azure Key Vault</span></span>
<span data-ttu-id="f4515-142">[솔루션을 설치](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview)한 후 Log Analytics의 **개요** 페이지에서 **Azure Key Vault** 타일을 클릭하여 Key Vault 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="f4515-144">**개요** 타일을 클릭한 후 로그의 요약을 확인하고 다음 범주에 대한 상세 정보를 파악할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="f4515-145">시간 경과에 따른 모든 Key Vault 작업 크기</span><span class="sxs-lookup"><span data-stu-id="f4515-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="f4515-146">시간 경과에 따른 실패 작업</span><span class="sxs-lookup"><span data-stu-id="f4515-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="f4515-147">작업별 평균 작업 대기 시간</span><span class="sxs-lookup"><span data-stu-id="f4515-147">Average operational latency by operation</span></span>
* <span data-ttu-id="f4515-148">1000ms 이상이 소요되는 작업 수 및 1000ms 이상이 소요되는 작업 목록을 포함한 작업 서비스 품질</span><span class="sxs-lookup"><span data-stu-id="f4515-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="f4515-151">모든 작업에 대한 세부 사항을 보려면</span><span class="sxs-lookup"><span data-stu-id="f4515-151">To view details for any operation</span></span>
1. <span data-ttu-id="f4515-152">**개요** 페이지에서 **Azure Key Vault** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="f4515-153">**Azure Key Vault** 대시보드에서 블레이드 중 하나에서 요약 정보를 검토한 다음 하나를 클릭하여 로그 검색 페이지에서 항목에 대한 세부 정보를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="f4515-154">로그 검색 페이지에서, 시간별 결과, 자세한 결과 및 로그 검색 기록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="f4515-155">패싯으로 필터링하여 결과 범위를 좁힐 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="f4515-156">Log Analytics 레코드</span><span class="sxs-lookup"><span data-stu-id="f4515-156">Log Analytics records</span></span>
<span data-ttu-id="f4515-157">Azure Key Vault 솔루션은 Azure Diagnostics에서 [AuditEvent logs](../key-vault/key-vault-logging.md)에서 수집된 **KeyVaults** 형식의 레코드를 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="f4515-158">이러한 레코드의 속성은 다음 표에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="f4515-159">속성</span><span class="sxs-lookup"><span data-stu-id="f4515-159">Property</span></span> | <span data-ttu-id="f4515-160">설명</span><span class="sxs-lookup"><span data-stu-id="f4515-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f4515-161">형식</span><span class="sxs-lookup"><span data-stu-id="f4515-161">Type</span></span> |<span data-ttu-id="f4515-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="f4515-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="f4515-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="f4515-163">SourceSystem</span></span> |<span data-ttu-id="f4515-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="f4515-164">*Azure*</span></span> |
| <span data-ttu-id="f4515-165">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="f4515-165">CallerIpAddress</span></span> |<span data-ttu-id="f4515-166">요청한 클라이언트의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="f4515-167">Category</span><span class="sxs-lookup"><span data-stu-id="f4515-167">Category</span></span> | <span data-ttu-id="f4515-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="f4515-168">*AuditEvent*</span></span> |
| <span data-ttu-id="f4515-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="f4515-169">CorrelationId</span></span> |<span data-ttu-id="f4515-170">클라이언트가 서비스 쪽(키 자격 증명 모음) 로그를 사용하여 클라이언트 쪽 로그 상관 관계를 지정하도록 전달할 수 있는 선택적 GUID입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="f4515-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="f4515-171">DurationMs</span></span> |<span data-ttu-id="f4515-172">밀리초 단위로 REST API 요청을 처리하는 데 걸린 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="f4515-173">이 시간에는 네트워크 대기 시간이 포함되지 않으므로 클라이언트 쪽에서 측정한 시간이 이 시간과 일치하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="f4515-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="f4515-174">httpStatusCode_d</span></span> |<span data-ttu-id="f4515-175">요청에서 반환한 HTTP 상태 코드(예: *200*)입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="f4515-176">id_s</span><span class="sxs-lookup"><span data-stu-id="f4515-176">id_s</span></span> |<span data-ttu-id="f4515-177">요청의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="f4515-177">Unique ID of the request</span></span> |
| <span data-ttu-id="f4515-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="f4515-178">identity_claim_appid_g</span></span> | <span data-ttu-id="f4515-179">응용 프로그램 id의 GUID</span><span class="sxs-lookup"><span data-stu-id="f4515-179">GUID for the application id</span></span> |
| <span data-ttu-id="f4515-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="f4515-180">OperationName</span></span> |<span data-ttu-id="f4515-181">[Azure Key Vault 로깅](../key-vault/key-vault-logging.md)에 설명된 대로 작업의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="f4515-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="f4515-182">OperationVersion</span></span> |<span data-ttu-id="f4515-183">클라이언트에서 요청한 REST API 버전(예: *2015-06-01*)입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="f4515-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="f4515-184">requestUri_s</span></span> |<span data-ttu-id="f4515-185">요청의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-185">Uri of the request</span></span> |
| <span data-ttu-id="f4515-186">리소스</span><span class="sxs-lookup"><span data-stu-id="f4515-186">Resource</span></span> |<span data-ttu-id="f4515-187">Key Vault의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-187">Name of the key vault</span></span> |
| <span data-ttu-id="f4515-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f4515-188">ResourceGroup</span></span> |<span data-ttu-id="f4515-189">Key Vault의 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="f4515-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="f4515-190">ResourceId</span></span> |<span data-ttu-id="f4515-191">Azure 리소스 관리자 리소스 ID.</span><span class="sxs-lookup"><span data-stu-id="f4515-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="f4515-192">Key Vault 로그의 경우 이는 Key Vault 리소스 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="f4515-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="f4515-193">ResourceProvider</span></span> |<span data-ttu-id="f4515-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="f4515-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="f4515-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="f4515-195">ResourceType</span></span> | <span data-ttu-id="f4515-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="f4515-196">*VAULTS*</span></span> |
| <span data-ttu-id="f4515-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="f4515-197">ResultSignature</span></span> |<span data-ttu-id="f4515-198">HTTP 상태(예: *확인*)</span><span class="sxs-lookup"><span data-stu-id="f4515-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="f4515-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="f4515-199">ResultType</span></span> |<span data-ttu-id="f4515-200">REST API 요청의 결과(예: *성공*)</span><span class="sxs-lookup"><span data-stu-id="f4515-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="f4515-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f4515-201">SubscriptionId</span></span> |<span data-ttu-id="f4515-202">Key Vault를 포함하는 구독의 Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="f4515-203">이전 Key Vault 솔루션에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="f4515-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="f4515-204">2017년 1월 Key Vault에서 Log Analytics로 로그를 보내도록 지원하는 방법이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="f4515-205">이러한 변경은 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="f4515-206">저장소 계정을 사용할 필요 없이 Log Analytics에 로그 직접 기록</span><span class="sxs-lookup"><span data-stu-id="f4515-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="f4515-207">Log Analytics에서 사용할 수 있는 로그가 생성된 이후의 대기 시간 감소</span><span class="sxs-lookup"><span data-stu-id="f4515-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="f4515-208">구성 단계 감소</span><span class="sxs-lookup"><span data-stu-id="f4515-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="f4515-209">모든 유형의 Azure 진단을 위한 공통 형식</span><span class="sxs-lookup"><span data-stu-id="f4515-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="f4515-210">업데이트된 솔루션을 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-210">To use the updated solution:</span></span>

1. <span data-ttu-id="f4515-211">[Key Vault에서 Log Analytics로 직접 보내도록 진단을 구성합니다](#enable-key-vault-diagnostics-in-the-portal).</span><span class="sxs-lookup"><span data-stu-id="f4515-211">[Configure diagnostics to be sent directly to Log Analytics from Key Vault](#enable-key-vault-diagnostics-in-the-portal)</span></span>  
2. <span data-ttu-id="f4515-212">[솔루션 갤러리에서 Log Analytics 솔루션 추가](log-analytics-add-solutions.md)에서 설명한 프로세스를 사용하여 Azure Key Vault 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="f4515-213">새 데이터 형식을 사용하도록 저장된 쿼리, 대시보드 또는 경고를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="f4515-214">KeyVaults에서 AzureDiagnostics로 형식을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="f4515-215">ResourceType을 사용하여 Key Vault 로그로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="f4515-216">`Type=KeyVaults` 대신 `Type=AzureDiagnostics ResourceType=VAULTS`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="f4515-217">필드: (필드 이름은 대/소문자를 구분함)</span><span class="sxs-lookup"><span data-stu-id="f4515-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="f4515-218">이름에 \_s, \_d 또는 \_g 접미사가 있는 필드의 경우 첫 번째 문자를 소문자로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="f4515-219">이름에 \_o 접미사가 있는 모든 필드의 경우 데이터는 중첩된 필드 이름에 기반하여 개별 필드로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="f4515-220">예를 들어 호출자의 UPN은 `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s` 필드에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="f4515-221">CallerIpAddress 필드를 CallerIPAddress로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="f4515-222">RemoteIPCountry 필드는 더 이상 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="f4515-223">*Key Vault 분석(사용되지 않음)* 솔루션을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="f4515-224">PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="f4515-225">변경 전에 수집된 데이터는 새 솔루션에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="f4515-226">이전 형식 및 필드 이름을 사용하여 이 데이터를 계속 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f4515-227">문제 해결</span><span class="sxs-lookup"><span data-stu-id="f4515-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="f4515-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f4515-228">Next steps</span></span>
* <span data-ttu-id="f4515-229">[Log Analytics의 로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 Azure Key Vault 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f4515-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
