---
title: "진단 로깅 및 메트릭 aaaAzure SQL 데이터베이스 | Microsoft Docs"
description: "Azure SQL 데이터베이스 리소스 toostore 리소스 사용, 연결 및 쿼리 실행 통계를 구성 하는 방법을 알아봅니다."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="3d30f-103">Azure SQL Database 메트릭 및 진단 로깅</span><span class="sxs-lookup"><span data-stu-id="3d30f-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="3d30f-104">Azure SQL Database는 쉬운 모니터링을 위해 메트릭 및 진단 로그를 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="3d30f-105">Azure SQL 데이터베이스 toostore 리소스 사용량, 작업자 및 세션 및 Azure 이러한 리소스 중 하나에 대 한 연결을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="3d30f-106">**Azure Storage**: 작은 가격으로 방대한 양의 원격 분석을 보관하는 경우</span><span class="sxs-lookup"><span data-stu-id="3d30f-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="3d30f-107">**Azure Event Hub**: 사용자 지정 모니터링 솔루션 또는 핫 파이프라인과 Azure SQL Database 원격 분석을 통합하는 경우</span><span class="sxs-lookup"><span data-stu-id="3d30f-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="3d30f-108">**Azure 로그 분석**:에 대 한 보고, 경고 및 완화 기능을 사용 하 여 솔루션을 모니터링 하는 hello 초기</span><span class="sxs-lookup"><span data-stu-id="3d30f-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![아키텍처](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="3d30f-110">로깅 사용</span><span class="sxs-lookup"><span data-stu-id="3d30f-110">Enable logging</span></span>

<span data-ttu-id="3d30f-111">메트릭 및 진단 로깅은 기본적으로 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="3d30f-112">사용 하도록 설정 하 고 메트릭 및 hello 메서드를 다음 중 하나를 사용 하 여 진단 로깅을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="3d30f-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3d30f-113">Azure portal</span></span>
- <span data-ttu-id="3d30f-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d30f-114">PowerShell</span></span>
- <span data-ttu-id="3d30f-115">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3d30f-115">Azure CLI</span></span>
- <span data-ttu-id="3d30f-116">REST API</span><span class="sxs-lookup"><span data-stu-id="3d30f-116">REST API</span></span> 
- <span data-ttu-id="3d30f-117">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3d30f-117">Resource Manager template</span></span>

<span data-ttu-id="3d30f-118">메트릭 및 진단 로깅을 사용 하도록 설정 하면 선택한 데이터 수집 되는 Azure 리소스 toospecify hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="3d30f-119">사용 가능한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-119">Options available:</span></span>
- <span data-ttu-id="3d30f-120">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="3d30f-120">Log analytics</span></span>
- <span data-ttu-id="3d30f-121">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="3d30f-121">Event Hub</span></span>
- <span data-ttu-id="3d30f-122">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="3d30f-122">Azure Storage</span></span> 

<span data-ttu-id="3d30f-123">새 Azure 리소스를 프로비전하거나 기존 리소스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="3d30f-124">Hello 저장소 리소스를 선택한 후 필요한 toospecify 어떤 데이터 toocollect 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="3d30f-125">사용 가능한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-125">Options available include:</span></span>

- <span data-ttu-id="3d30f-126">**[1분 메트릭](sql-database-metrics-diag-logging.md#1-minute-metrics)** - DTU 백분율, DTU 제한, CPU 백분율, 실제 데이터 읽기 백분율, 로그 쓰기 백분율, 성공/실패/방화벽 연결에 의해 차단됨, 세션 백분율, 작업자 백분율, 저장소, 저장소 백분율, XTP 저장소 백분율을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="3d30f-127">이벤트 허브 또는 AzureStorage 계정을 지정 하면 선택 된 시간 동안 삭제 됩니다 보다 오래 된 데이터 보존 정책 toospecify를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="3d30f-128">로그 분석을 지정 하면 hello 보존 정책 hello 선택한 가격 책정 계층에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="3d30f-129">자세한 내용은 [Log Analytics 가격 책정](https://azure.microsoft.com/pricing/details/log-analytics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d30f-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="3d30f-130">두 hello를 읽는 것이 좋습니다 [Microsoft Azure에서 메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md) 및 [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain 이해만 방법이 아닌 문서 hello 하지만 tooenable 로깅 메트릭 및 로그 범주 hello에서 다양 한 Azure 서비스를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3d30f-131">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3d30f-131">Azure portal</span></span>

<span data-ttu-id="3d30f-132">tooenable 메트릭 및 hello Azure 포털에서에서 진단 로그 컬렉션 tooyour Azure SQL 데이터베이스 또는 탄력적 풀 페이지를 탐색 한 다음 클릭 **진단 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![hello Azure 포털을 사용 하도록 설정](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="3d30f-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d30f-134">PowerShell</span></span>

<span data-ttu-id="3d30f-135">tooenable 메트릭 및 진단 로깅 hello 명령 다음 사용 하 여 PowerShell을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="3d30f-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="3d30f-136">저장소 계정에 진단 로그의 tooenable 저장소에는이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="3d30f-137">hello 저장소 계정 ID는 hello 저장소 계정 toowhich toosend hello를 원하는 로그 hello 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="3d30f-138">이 명령을 사용 하 여 진단 로그 tooan 이벤트 허브의 tooenable 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="3d30f-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="3d30f-139">hello 서비스 버스 규칙 ID는이 형식은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="3d30f-140">tooenable 보내는 진단 로그 tooa 로그 분석 작업 영역에서이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="3d30f-141">다음 명령을 hello를 사용 하 여 로그 분석 작업 영역의 hello 리소스 id를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="3d30f-142">이러한 매개 변수 tooenable 여러 출력 옵션 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="3d30f-143">CLI</span><span class="sxs-lookup"><span data-stu-id="3d30f-143">CLI</span></span>

<span data-ttu-id="3d30f-144">tooenable 메트릭 및 진단 로깅을 사용 하 여 Azure CLI, 다음 명령을 사용 하 여 hello hello:</span><span class="sxs-lookup"><span data-stu-id="3d30f-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="3d30f-145">저장소 계정에 진단 로그의 tooenable 저장소에는이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="3d30f-146">hello 저장소 계정 ID는 hello 저장소 계정 toowhich toosend hello를 원하는 로그 hello 리소스 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="3d30f-147">이 명령을 사용 하 여 진단 로그 tooan 이벤트 허브의 tooenable 스트리밍:</span><span class="sxs-lookup"><span data-stu-id="3d30f-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="3d30f-148">hello 서비스 버스 규칙 ID는이 형식은 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="3d30f-149">tooenable 보내는 진단 로그 tooa 로그 분석 작업 영역에서이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="3d30f-150">이러한 매개 변수 tooenable 여러 출력 옵션 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="3d30f-151">REST API</span><span class="sxs-lookup"><span data-stu-id="3d30f-151">REST API</span></span>

<span data-ttu-id="3d30f-152">너무 방법에 대 한 읽기[hello Azure 모니터 REST API를 사용 하 여 진단 설정을 변경](https://msdn.microsoft.com/library/azure/dn931931.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="3d30f-153">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="3d30f-153">Resource Manager template</span></span>

<span data-ttu-id="3d30f-154">너무 방법에 대 한 읽기[리소스 관리자 템플릿을 사용 하 여 리소스를 만들 때 진단 설정을 사용 하도록 설정](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="3d30f-155">Log Analytics에 스트림</span><span class="sxs-lookup"><span data-stu-id="3d30f-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="3d30f-156">Azure SQL 데이터베이스 메트릭 및 진단 로그 hello 포털 또는 Azure PowerShell cmdlet, Azure CLI 또는 Azure 모니터 REST를 통해 진단 설정의 로그 분석을 사용 하 여 hello 기본 제공 "Send tooLog 분석" 옵션을 사용 하 여 로그 분석에 스트리밍할 수 있습니다. API입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="3d30f-157">설치 개요</span><span class="sxs-lookup"><span data-stu-id="3d30f-157">Installation overview</span></span>

<span data-ttu-id="3d30f-158">Log Analytics를 사용하여 Azure SQL Database를 간편하게 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="3d30f-159">세 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-159">Three steps are required:</span></span>

1.  <span data-ttu-id="3d30f-160">Log Analytics 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d30f-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="3d30f-161">로그 분석을 생성 하는 hello에 데이터베이스 toorecord 메트릭 및 진단 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="3d30f-162">Log Analytics의 갤러리에서 **Azure SQL 분석** 솔루션 설치</span><span class="sxs-lookup"><span data-stu-id="3d30f-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="3d30f-163">Log Analytics 리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="3d30f-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="3d30f-164">클릭 **새로** hello 왼쪽 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="3d30f-165">**모니터링 + 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="3d30f-166">**Log Analytics**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="3d30f-167">필요한 추가 정보를 hello와 hello 로그 분석 양식을 입력: 작업 영역 이름, 구독, 리소스 그룹, 위치 및 가격 책정 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="3d30f-169">데이터베이스 toorecord 메트릭 및 진단 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="3d30f-170">hello 데이터베이스 메트릭을 기록 하는 위치는 가장 쉬운 방법은 tooconfigure hello Azure 포털을 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="3d30f-171">에 Azure 포털 hello tooyour Azure SQL 데이터베이스 리소스를 이동 하 고 클릭 **진단 설정을**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="3d30f-172">갤러리에서 hello Azure SQL 분석 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="3d30f-173">로그 분석 리소스 hello는 만든 후에 데이터 흐름에 Azure SQL 분석 솔루션을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="3d30f-174">Hello를 통해 이렇게 **솔루션 갤러리** hello 측면 메뉴 및 hello OMS 홈 페이지에서 찾을 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="3d30f-175">Hello 갤러리에서 찾아 클릭 **Azure SQL 분석** 솔루션과 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![모니터링 솔루션](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="3d30f-177">OMS 홈 페이지에 **Azure SQL 분석**이라는 새 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="3d30f-178">이 타일을 선택 하면 hello Azure SQL 분석 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="3d30f-179">Azure SQL Analytics 솔루션 사용</span><span class="sxs-lookup"><span data-stu-id="3d30f-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="3d30f-180">Azure SQL 분석은 Azure SQL 데이터베이스 리소스의 hello 계층을 통해 toonavigate 수 있는 계층적 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="3d30f-181">하면 toodo도 모니터링 하지만 높은 수준의 tooscope 수 있습니다.이 기능에서는 리소스의 오른쪽에 모니터링 toojust hello 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="3d30f-182">대시보드는 hello hello 선택한 리소스에서 다양 한 리소스 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="3d30f-183">예를 들어 선택한 구독에 대 한 나타나면 hello 모든 서버, 탄력적 풀 및 toohello 속하는 데이터베이스 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="3d30f-184">또한 탄력적 풀 및 데이터베이스에 대 한 해당 리소스의 hello 리소스 사용 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="3d30f-185">여기에는 DTU, CPU, IO, 로그, 세션, 작업자, 연결 및 저장소(GB)에 대한 차트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="3d30f-186">Azure 이벤트 허브에 스트림</span><span class="sxs-lookup"><span data-stu-id="3d30f-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="3d30f-187">Azure SQL 데이터베이스 메트릭 및 진단 로그를 hello 포털에 만들거나 Azure PowerShell Cmdlet, Azure CLI 또는 Azure 모니터 REST를 통해 진단 설정에 서비스 버스 규칙 Id를 사용 하 여 hello 기본 제공 "스트림 tooan 이벤트 허브" 옵션을 사용 하 여 이벤트 허브에 스트리밍할 수 있습니다. API입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="3d30f-188">메트릭 및 이벤트 허브에서 진단 로그 toodo 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="3d30f-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="3d30f-189">이벤트 허브에 스트림 되는 선택한 hello 데이터 고급 모니터링 시나리오는 한 단계 더 가깝기 때문 tooenabling 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="3d30f-190">이벤트 허브는 이벤트 파이프라인에 대 한 "프런트 도어" hello 역할 하며 전환 하 여 이벤트 허브로 데이터 수집 되 면 및 모든 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용 하 여 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="3d30f-191">이벤트 허브 이벤트 소비자 일정에 따라 hello 이벤트에 액세스할 수 있도록 이러한 이벤트의 hello 소비에서 이벤트 스트림 hello 생산을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="3d30f-192">이벤트 허브에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d30f-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="3d30f-193">[Azure Event Hubs란](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="3d30f-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="3d30f-194">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="3d30f-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="3d30f-195">다음 몇 가지 방법으로 hello 스트리밍 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="3d30f-196">서비스 상태를 보려면 "실행 부하 과다 경로" 데이터 tooPowerBI-를 사용 하 여 이벤트 허브, 스트림 분석 및 PowerBI을 스트리밍하여 변환 하 거의 실시간으로 메트릭 및 진단 데이터에 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="3d30f-197">이벤트 허브를 tooset 스트림 분석을 사용 하 여 데이터를 처리 하 고 출력을 출력으로 PowerBI를 사용 하는 방법에 대 한 개요를 참조 하십시오. [Stream Analytics 및 Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="3d30f-198">스트림 로그 toothird 파티 로깅 및 원격 분석 스트림을 – 스트리밍 있습니다를 사용 하 여 이벤트 허브에서에서 확인할 수 있습니다 메트릭 및 진단 로그 toodifferent 제 3 자 모니터링 및 로그 분석 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="3d30f-199">진단 로그 수집 건물 하나, 확장성이 높은 hello 게시-구독에 대해 생각 방금 이벤트 허브의 특성 tooflexibly 수 있습니다. 또는 사용자가 작성 한 원격 분석 플랫폼을 이미 있는 경우 사용자 지정 원격 분석 및 로깅 플랫폼-빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="3d30f-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="3d30f-200">참조 [세계적인 규모 원격 분석 플랫폼에서 Dan Rosanova 가이드 toousing 이벤트 허브](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="3d30f-201">Azure Storage에 스트림</span><span class="sxs-lookup"><span data-stu-id="3d30f-201">Stream into Azure Storage</span></span>

<span data-ttu-id="3d30f-202">Azure SQL 데이터베이스 메트릭 및 진단 로그 hello Azure 포털 또는 Azure PowerShell Cmdlet, Azure CLI 또는 Azure를 통해 진단 설정에서 Azure 저장소를 사용 하 여 hello 기본 제공 "보관 tooa 저장소 계정" 옵션을 사용 하 여 Azure 저장소에 저장할 수 있습니다. 모니터 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="3d30f-203">메트릭 및 hello 저장소 계정에 진단 로그의 스키마</span><span class="sxs-lookup"><span data-stu-id="3d30f-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="3d30f-204">메트릭 및 진단 로그 컬렉션을 설정 하면 저장소 컨테이너 hello 첫 번째 데이터 행을 사용할 때 선택한 hello 저장소 계정에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="3d30f-205">이러한 blob의 hello 구조는.</span><span class="sxs-lookup"><span data-stu-id="3d30f-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="3d30f-206">또는 더 간단하게 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="3d30f-207">예를 들어 1분 메트릭에 대한 Blob 이름은 다음과 같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="3d30f-208">Hello 탄력적 풀에서에서 toorecord hello 데이터를 원하는 경우에 blob 이름은 약간 다른입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="3d30f-209">Azure Storage에서 메트릭 및 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="3d30f-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="3d30f-210">[Azure Storage에서 메트릭 및 진단 로그 다운로드](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d30f-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="3d30f-211">1분 메트릭</span><span class="sxs-lookup"><span data-stu-id="3d30f-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="3d30f-212">**리소스**</span><span class="sxs-lookup"><span data-stu-id="3d30f-212">**Resource**</span></span>|<span data-ttu-id="3d30f-213">**metrics**</span><span class="sxs-lookup"><span data-stu-id="3d30f-213">**Metrics**</span></span>|
|<span data-ttu-id="3d30f-214">데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3d30f-214">Database</span></span>|<span data-ttu-id="3d30f-215">DTU 백분율, 사용된 DTU, DTU 제한, CPU 백분율, 실제 데이터 읽기 백분율, 로그 쓰기 백분율, 성공/실패/방화벽 연결에 의해 차단됨, 세션 백분율, 작업자 백분율, 저장소, 저장소 백분율, XTP 저장소 백분율, 교착 상태를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="3d30f-216">탄력적 풀</span><span class="sxs-lookup"><span data-stu-id="3d30f-216">Elastic pool</span></span>|<span data-ttu-id="3d30f-217">eDTU 백분율, 사용된 eDTU, eDTU 제한, CPU 백분율, 실제 데이터 읽기 백분율, 로그 쓰기 백분율, 세션 백분율, 작업자 백분율, 저장소, 저장소 백분율, 저장소 용량 한도, XTP 저장소 백분율을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3d30f-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d30f-218">Next steps</span></span>

- <span data-ttu-id="3d30f-219">두 hello 읽기 [Microsoft Azure에서 메트릭 개요](../monitoring-and-diagnostics/monitoring-overview-metrics.md) 및 [개요의 Azure 진단 로그](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain만 방법이 아닌 로깅, tooenable 하지만 메트릭 hello 및 로그 범주 이해 항목 hello에서 지 원하는 다양 한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3d30f-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="3d30f-220">이벤트 허브에 대 한 이러한 문서 toolearn을 읽어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="3d30f-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="3d30f-221">[Azure Event Hubs란](../event-hubs/event-hubs-what-is-event-hubs.md)?</span><span class="sxs-lookup"><span data-stu-id="3d30f-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="3d30f-222">이벤트 허브 시작</span><span class="sxs-lookup"><span data-stu-id="3d30f-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="3d30f-223">[Azure Storage에서 메트릭 및 진단 로그 다운로드](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d30f-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
