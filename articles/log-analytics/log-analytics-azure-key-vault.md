---
title: "로그 분석에서 주요 자격 증명 모음 솔루션 aaaAzure | Microsoft Docs"
description: "로그 분석 tooreview Azure 키 자격 증명 모음 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다."
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
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="4340c-103">Log Analytics의 Azure Key Vault Analytics 솔루션</span><span class="sxs-lookup"><span data-stu-id="4340c-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Key Vault 기호](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="4340c-105">로그 분석 tooreview Azure 키 자격 증명 모음 AuditEvent 로그에서 hello Azure 키 자격 증명 모음 솔루션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-105">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="4340c-106">toouse hello 솔루션을 직접 hello 진단 tooa 로그 분석 작업 영역 및 Azure 키 자격 증명 모음 진단 tooenable 로깅이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-106">toouse hello solution, you need tooenable logging of Azure Key Vault diagnostics and direct hello diagnostics tooa Log Analytics workspace.</span></span> <span data-ttu-id="4340c-107">필요한 toowrite hello 로그 tooAzure Blob 저장소는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-107">It is not necessary toowrite hello logs tooAzure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="4340c-108">2017 년 1 월 hello 분석 변경 하는 주요 자격 증명 모음 tooLog에서 로그를 보내는 방식으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-108">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="4340c-109">Hello 키 자격 증명 모음 솔루션 사용 하는 경우 표시 *(사용 되지 않음)* hello 제목에 참조 너무[hello 이전 키 자격 증명 모음 솔루션에서 마이그레이션](#migrating-from-the-old-key-vault-solution) toofollow 필요한 단계에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-109">If hello Key Vault solution you are using shows *(deprecated)* in hello title, refer too[migrating from hello old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need toofollow.</span></span>
>
>

## <a name="install-and-configure-hello-solution"></a><span data-ttu-id="4340c-110">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="4340c-110">Install and configure hello solution</span></span>
<span data-ttu-id="4340c-111">다음 지침 tooinstall hello를 사용 하 여 하 고 hello Azure 키 자격 증명 모음 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-111">Use hello following instructions tooinstall and configure hello Azure Key Vault solution:</span></span>

1. <span data-ttu-id="4340c-112">솔루션을 hello Azure 키 자격 증명 모음을 사용 하도록 설정 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) 또는에 설명 된 hello 프로세스를 사용 하 여 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-112">Enable hello Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="4340c-113">키 자격 증명 모음 리소스 toomonitor hello에 대 한 로깅, 어느 hello를 사용 하 여 진단을 사용 하도록 설정 [포털](#enable-key-vault-diagnostics-in-the-portal) 또는 [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="4340c-113">Enable diagnostics logging for hello Key Vault resources toomonitor, using either hello [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a><span data-ttu-id="4340c-114">Hello 포털에서 주요 자격 증명 모음 진단을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="4340c-114">Enable Key Vault diagnostics in hello portal</span></span>

1. <span data-ttu-id="4340c-115">Hello Azure 포털에서에서 toohello 주요 자격 증명 모음 리소스 toomonitor 이동</span><span class="sxs-lookup"><span data-stu-id="4340c-115">In hello Azure portal, navigate toohello Key Vault resource toomonitor</span></span>
2. <span data-ttu-id="4340c-116">선택 *진단 로그* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="4340c-116">Select *Diagnostics logs* tooopen hello following page</span></span>

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="4340c-118">클릭 *진단을 설정* tooopen hello 다음 페이지</span><span class="sxs-lookup"><span data-stu-id="4340c-118">Click *Turn on diagnostics* tooopen hello following page</span></span>

   ![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="4340c-120">진단, tooturn 클릭 *에* 아래 *상태*</span><span class="sxs-lookup"><span data-stu-id="4340c-120">tooturn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="4340c-121">에 대 한 hello 확인란 클릭 *tooLog 분석 보내기*</span><span class="sxs-lookup"><span data-stu-id="4340c-121">Click hello checkbox for *Send tooLog Analytics*</span></span>
6. <span data-ttu-id="4340c-122">기존 Log Analytics 작업 영역을 선택하거나 작업 영역을 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="4340c-123">tooenable *AuditEvent* 로그 hello 확인란을 클릭 하 여 로그에서</span><span class="sxs-lookup"><span data-stu-id="4340c-123">tooenable *AuditEvent* logs, click hello checkbox under Log</span></span>
8. <span data-ttu-id="4340c-124">클릭 *저장* 진단 tooLog 분석의 tooenable hello 로깅</span><span class="sxs-lookup"><span data-stu-id="4340c-124">Click *Save* tooenable hello logging of diagnostics tooLog Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="4340c-125">PowerShell을 사용하여 Key Vault 진단 사용 설정</span><span class="sxs-lookup"><span data-stu-id="4340c-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="4340c-126">방법의 예를 제공 하는 PowerShell 스크립트 뒤 hello toouse `Set-AzureRmDiagnosticSetting` tooenable 주요 자격 증명 모음에 진단 로깅:</span><span class="sxs-lookup"><span data-stu-id="4340c-126">hello following PowerShell script provides an example of how toouse `Set-AzureRmDiagnosticSetting` tooenable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="4340c-127">Azure Key Vault 데이터 수집 상세 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="4340c-128">Azure 키 자격 증명 모음 솔루션 hello 주요 자격 증명 모음에서 직접 진단 로그를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-128">Azure Key Vault solution collects diagnostics logs directly from hello Key Vault.</span></span>
<span data-ttu-id="4340c-129">필요한 toowrite hello 로그 tooAzure Blob 저장소 않습니다 되며 에이전트가 없습니다. 데이터 수집을 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-129">It is not necessary toowrite hello logs tooAzure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="4340c-130">hello 다음 표에 Azure 키 자격 증명 모음에 대 한 데이터 수집 방법에 대 한 기타 세부 정보 및 데이터 수집 방법과 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-130">hello following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="4340c-131">플랫폼</span><span class="sxs-lookup"><span data-stu-id="4340c-131">Platform</span></span> | <span data-ttu-id="4340c-132">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="4340c-132">Direct agent</span></span> | <span data-ttu-id="4340c-133">Systems Center Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="4340c-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="4340c-134">Azure</span><span class="sxs-lookup"><span data-stu-id="4340c-134">Azure</span></span> | <span data-ttu-id="4340c-135">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="4340c-135">Operations Manager required?</span></span> | <span data-ttu-id="4340c-136">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="4340c-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="4340c-137">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="4340c-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4340c-138">Azure</span><span class="sxs-lookup"><span data-stu-id="4340c-138">Azure</span></span> |  |  |<span data-ttu-id="4340c-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4340c-139">&#8226;</span></span> |  |  | <span data-ttu-id="4340c-140">도착 시</span><span class="sxs-lookup"><span data-stu-id="4340c-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="4340c-141">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="4340c-141">Use Azure Key Vault</span></span>
<span data-ttu-id="4340c-142">후 [hello 솔루션 설치](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), hello를 클릭 하 여 hello 주요 자격 증명 모음 데이터를 볼 **Azure 키 자격 증명 모음** hello에서 타일 **개요** 로그 분석의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-142">After you [install hello solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view hello Key Vault data by clicking hello **Azure Key Vault** tile from hello **Overview** page of Log Analytics.</span></span>

![Azure Key Vault 타일 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="4340c-144">Hello를 클릭 한 후 **개요** 타일 toodetails hello 다음 범주에 대 한에서 로그와 다음 드릴의 요약을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-144">After you click hello **Overview** tile, you can view summaries of your logs and then drill in toodetails for hello following categories:</span></span>

* <span data-ttu-id="4340c-145">시간 경과에 따른 모든 Key Vault 작업 크기</span><span class="sxs-lookup"><span data-stu-id="4340c-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="4340c-146">시간 경과에 따른 실패 작업</span><span class="sxs-lookup"><span data-stu-id="4340c-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="4340c-147">작업별 평균 작업 대기 시간</span><span class="sxs-lookup"><span data-stu-id="4340c-147">Average operational latency by operation</span></span>
* <span data-ttu-id="4340c-148">1000 밀리초 이상 하는 작업의 목록과 hello 수가 1000 밀리초 이상 하는 작업을 사용 하 여 작업에 대 한 서비스 품질</span><span class="sxs-lookup"><span data-stu-id="4340c-148">Quality of service for operations with hello number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Azure Key Vault 대시보드 이미지](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a><span data-ttu-id="4340c-151">모든 작업에 대 한 tooview 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4340c-151">tooview details for any operation</span></span>
1. <span data-ttu-id="4340c-152">Hello에 **개요** 페이지에서 hello **Azure 키 자격 증명 모음** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-152">On hello **Overview** page, click hello **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="4340c-153">Hello에 **Azure 키 자격 증명 모음** 대시보드를 hello hello 블레이드 중 하나의 요약 정보를 검토 한 다음 하나를 클릭 tooview hello 로그 검색 페이지의 항목에 대 한 정보를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-153">On hello **Azure Key Vault** dashboard, review hello summary information in one of hello blades, and then click one tooview detailed information about it in hello log search page.</span></span>

    <span data-ttu-id="4340c-154">Hello 로그 검색 페이지에서 자세한 결과 시간과 로그 검색 기록을로 결과 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-154">On any of hello log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="4340c-155">패싯 toonarrow hello 결과에서 필터링 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-155">You can also filter by facets toonarrow hello results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="4340c-156">Log Analytics 레코드</span><span class="sxs-lookup"><span data-stu-id="4340c-156">Log Analytics records</span></span>
<span data-ttu-id="4340c-157">형식을 갖는 레코드를 분석 하는 hello Azure 키 자격 증명 모음 솔루션 **KeyVaults** 에서 수집한 [AuditEvent 로그](../key-vault/key-vault-logging.md) Azure 진단에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-157">hello Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="4340c-158">이러한 레코드에 대 한 속성은 다음 표에 hello에:</span><span class="sxs-lookup"><span data-stu-id="4340c-158">Properties for these records are in hello following table:</span></span>  

| <span data-ttu-id="4340c-159">속성</span><span class="sxs-lookup"><span data-stu-id="4340c-159">Property</span></span> | <span data-ttu-id="4340c-160">설명</span><span class="sxs-lookup"><span data-stu-id="4340c-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="4340c-161">형식</span><span class="sxs-lookup"><span data-stu-id="4340c-161">Type</span></span> |<span data-ttu-id="4340c-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="4340c-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="4340c-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4340c-163">SourceSystem</span></span> |<span data-ttu-id="4340c-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="4340c-164">*Azure*</span></span> |
| <span data-ttu-id="4340c-165">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="4340c-165">CallerIpAddress</span></span> |<span data-ttu-id="4340c-166">Hello 요청을 수행한 hello 클라이언트의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="4340c-166">IP address of hello client who made hello request</span></span> |
| <span data-ttu-id="4340c-167">Category</span><span class="sxs-lookup"><span data-stu-id="4340c-167">Category</span></span> | <span data-ttu-id="4340c-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="4340c-168">*AuditEvent*</span></span> |
| <span data-ttu-id="4340c-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="4340c-169">CorrelationId</span></span> |<span data-ttu-id="4340c-170">클라이언트 hello 선택적 GUID가 toocorrelate 서비스 측 (키 자격 증명 모음) 로그를 사용 하 여 클라이언트 쪽 로그를 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-170">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="4340c-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="4340c-171">DurationMs</span></span> |<span data-ttu-id="4340c-172">밀리초 단위로 tooservice hello REST API 요청에 소요 된 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-172">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="4340c-173">이 시간 hello 클라이언트 쪽에서 측정 하는 hello 시간이 이번 일치 하지 않을 수 있으므로 네트워크 대기 시간, 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-173">This time does not include network latency, so hello time that you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="4340c-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="4340c-174">httpStatusCode_d</span></span> |<span data-ttu-id="4340c-175">Hello 요청에서 반환 된 HTTP 상태 코드 (예를 들어 *200*)</span><span class="sxs-lookup"><span data-stu-id="4340c-175">HTTP status code returned by hello request (for example, *200*)</span></span> |
| <span data-ttu-id="4340c-176">id_s</span><span class="sxs-lookup"><span data-stu-id="4340c-176">id_s</span></span> |<span data-ttu-id="4340c-177">Hello 요청의 고유 ID</span><span class="sxs-lookup"><span data-stu-id="4340c-177">Unique ID of hello request</span></span> |
| <span data-ttu-id="4340c-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="4340c-178">identity_claim_appid_g</span></span> | <span data-ttu-id="4340c-179">Hello 응용 프로그램 id에 대 한 GUID</span><span class="sxs-lookup"><span data-stu-id="4340c-179">GUID for hello application id</span></span> |
| <span data-ttu-id="4340c-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="4340c-180">OperationName</span></span> |<span data-ttu-id="4340c-181">에 설명 된 대로 hello 작업의 이름 [Azure 키 자격 증명 모음 로깅](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="4340c-181">Name of hello operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="4340c-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="4340c-182">OperationVersion</span></span> |<span data-ttu-id="4340c-183">Hello 클라이언트에서 요청 된 REST API 버전 (예를 들어 *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="4340c-183">REST API version requested by hello client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="4340c-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="4340c-184">requestUri_s</span></span> |<span data-ttu-id="4340c-185">Hello 요청의 Uri</span><span class="sxs-lookup"><span data-stu-id="4340c-185">Uri of hello request</span></span> |
| <span data-ttu-id="4340c-186">리소스</span><span class="sxs-lookup"><span data-stu-id="4340c-186">Resource</span></span> |<span data-ttu-id="4340c-187">Hello 키 자격 증명 모음의 이름</span><span class="sxs-lookup"><span data-stu-id="4340c-187">Name of hello key vault</span></span> |
| <span data-ttu-id="4340c-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4340c-188">ResourceGroup</span></span> |<span data-ttu-id="4340c-189">Hello 키 자격 증명 모음의 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="4340c-189">Resource group of hello key vault</span></span> |
| <span data-ttu-id="4340c-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="4340c-190">ResourceId</span></span> |<span data-ttu-id="4340c-191">Azure 리소스 관리자 리소스 ID.</span><span class="sxs-lookup"><span data-stu-id="4340c-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="4340c-192">주요 자격 증명 모음 로그의 경우이 hello 주요 자격 증명 모음 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-192">For Key Vault logs, this is hello Key Vault resource ID.</span></span> |
| <span data-ttu-id="4340c-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="4340c-193">ResourceProvider</span></span> |<span data-ttu-id="4340c-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="4340c-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="4340c-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="4340c-195">ResourceType</span></span> | <span data-ttu-id="4340c-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="4340c-196">*VAULTS*</span></span> |
| <span data-ttu-id="4340c-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="4340c-197">ResultSignature</span></span> |<span data-ttu-id="4340c-198">HTTP 상태(예: *확인*)</span><span class="sxs-lookup"><span data-stu-id="4340c-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="4340c-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="4340c-199">ResultType</span></span> |<span data-ttu-id="4340c-200">REST API 요청의 결과(예: *성공*)</span><span class="sxs-lookup"><span data-stu-id="4340c-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="4340c-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4340c-201">SubscriptionId</span></span> |<span data-ttu-id="4340c-202">Hello 주요 자격 증명 모음을 포함 하는 hello 구독의 azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="4340c-202">Azure subscription ID of hello subscription containing hello Key Vault</span></span> |

## <a name="migrating-from-hello-old-key-vault-solution"></a><span data-ttu-id="4340c-203">Hello 이전 키 자격 증명 모음 솔루션에서 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="4340c-203">Migrating from hello old Key Vault solution</span></span>
<span data-ttu-id="4340c-204">2017 년 1 월 hello 분석 변경 하는 주요 자격 증명 모음 tooLog에서 로그를 보내는 방식으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-204">In January 2017, hello supported way of sending logs from Key Vault tooLog Analytics changed.</span></span> <span data-ttu-id="4340c-205">이러한 변경 내용은 다음 장점 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-205">These changes provide hello following advantages:</span></span>
+ <span data-ttu-id="4340c-206">직접 hello 없이 tooLog 분석 필요 toouse 저장소 계정 로그가 기록</span><span class="sxs-lookup"><span data-stu-id="4340c-206">Logs are written directly tooLog Analytics without hello need toouse a storage account</span></span>
+ <span data-ttu-id="4340c-207">로그가 hello 시간에서 대기 시간이 짧습니다 생성 toothem 로그 분석에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-207">Less latency from hello time when logs are generated toothem being available in Log Analytics</span></span>
+ <span data-ttu-id="4340c-208">구성 단계 감소</span><span class="sxs-lookup"><span data-stu-id="4340c-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="4340c-209">모든 유형의 Azure 진단을 위한 공통 형식</span><span class="sxs-lookup"><span data-stu-id="4340c-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="4340c-210">toouse hello 솔루션을 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-210">toouse hello updated solution:</span></span>

1. [<span data-ttu-id="4340c-211">주요 자격 증명 모음에서 tooLog 분석을 직접 전송 하는 진단 toobe 구성</span><span class="sxs-lookup"><span data-stu-id="4340c-211">Configure diagnostics toobe sent directly tooLog Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="4340c-212">에 설명 된 hello 프로세스를 사용 하 여 hello Azure 키 자격 증명 모음 솔루션을 사용 하도록 설정 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="4340c-212">Enable hello Azure Key Vault solution by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="4340c-213">모든 저장 된 쿼리, 대시보드, 또는 경고 toouse hello 새 데이터 형식 업데이트</span><span class="sxs-lookup"><span data-stu-id="4340c-213">Update any saved queries, dashboards, or alerts toouse hello new data type</span></span>
  + <span data-ttu-id="4340c-214">형식이 변경: KeyVaults tooAzureDiagnostics 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-214">Type is change from: KeyVaults tooAzureDiagnostics.</span></span> <span data-ttu-id="4340c-215">Hello ResourceType toofilter tooKey 자격 증명 모음 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-215">You can use hello ResourceType toofilter tooKey Vault Logs.</span></span>
  - <span data-ttu-id="4340c-216">`Type=KeyVaults` 대신 `Type=AzureDiagnostics ResourceType=VAULTS`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-216">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="4340c-217">필드: (필드 이름은 대/소문자를 구분함)</span><span class="sxs-lookup"><span data-stu-id="4340c-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="4340c-218">접미사가 있는 모든 필드에 대 한 \_s, \_d, 또는 \_g hello 이름 hello 첫 번째 문자 toolower 대/소문자 변경</span><span class="sxs-lookup"><span data-stu-id="4340c-218">For any field that has a suffix of \_s, \_d, or \_g in hello name, change hello first character toolower case</span></span>
  - <span data-ttu-id="4340c-219">접미사가 있는 모든 필드에 대 한 \_o hello 데이터 이름에는 중첩 된 hello 필드 이름을 기반으로 하는 개별 필드도 나누어집니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-219">For any field that has a suffix of \_o in name, hello data is split into individual fields based on hello nested field names.</span></span> <span data-ttu-id="4340c-220">Hello hello 호출자의 UPN 필드에 저장 되는 예를 들어`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="4340c-220">For example, hello UPN of hello caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="4340c-221">변경 된 필드 CallerIpAddress tooCallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="4340c-221">Field CallerIpAddress changed tooCallerIPAddress</span></span>
   - <span data-ttu-id="4340c-222">RemoteIPCountry 필드는 더 이상 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="4340c-223">Hello 제거 *키 자격 증명 모음 분석 (사용 되지 않음)* 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-223">Remove hello *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="4340c-224">PowerShell을 사용하는 경우 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="4340c-225">데이터는 수집 전에 hello 변경이 hello 새 솔루션에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-225">Data collected before hello change is not visible in hello new solution.</span></span> <span data-ttu-id="4340c-226">기존 형식 및 필드 이름을 hello 사용 하 여이 데이터에 대 한 tooquery를 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-226">You can continue tooquery for this data using hello old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4340c-227">문제 해결</span><span class="sxs-lookup"><span data-stu-id="4340c-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="4340c-228">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4340c-228">Next steps</span></span>
* <span data-ttu-id="4340c-229">사용 하 여 [로그 분석 검색 로그인](log-analytics-log-searches.md) tooview Azure 키 자격 증명 모음 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4340c-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Azure Key Vault data.</span></span>
