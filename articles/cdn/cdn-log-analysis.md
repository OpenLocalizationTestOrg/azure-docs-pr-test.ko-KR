---
title: "Azure CDN에 대 한 aaaLog 분석 | Microsoft Docs"
description: "고객은 Azure CDN에 대한 Log Analytics를 사용하도록 설정할 수 있습니다."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="2bfd4-103">Azure CDN에 대한 진단 로그</span><span class="sxs-lookup"><span data-stu-id="2bfd4-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="2bfd4-104">응용 프로그램에 대해 CDN을 활성화 한 다음 됩니다 가능성이 toomonitor hello CDN 사용, 배달의 hello 상태를 확인을 잠재적인 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-104">After enabling CDN for your application, you will likely want toomonitor hello CDN usage, check hello health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="2bfd4-105">Azure CDN에서는 [CDN 핵심 분석](cdn-analyze-usage-patterns.md) 및 [진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)에 이러한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="2bfd4-106">CDN 핵심 분석</span><span class="sxs-lookup"><span data-stu-id="2bfd4-106">CDN Core Analytics</span></span>
<span data-ttu-id="2bfd4-107">Verizon 표준 또는 프리미엄 프로필과 현재 Azure CDN 사용자로 이미 있는 수 tooview 코어 분석 hello 보조 포털 hello hello Azure 포털에서에서 "관리" 옵션을 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able tooview core analytics in hello supplemental portal accessible via hello "Manage" option from hello Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="2bfd4-108">Azure 진단 로그</span><span class="sxs-lookup"><span data-stu-id="2bfd4-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="2bfd4-109">이 새로운 기능의 Azure를 통해 이제 핵심 분석을 보고 다음을 포함한 하나 이상의 대상에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="2bfd4-110">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="2bfd4-110">Azure Storage account</span></span>
 - <span data-ttu-id="2bfd4-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2bfd4-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="2bfd4-112">OMS Log Analytics 리포지토리</span><span class="sxs-lookup"><span data-stu-id="2bfd4-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="2bfd4-113">이 기능은 tooVerizon (Standard 및 Premium) 및 (표준) Akamai CDN 프로필에 속한 모든 CDN 끝점에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-113">This feature is available for all CDN endpoints belonging tooVerizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="2bfd4-114">진단 로그를 사용 하면 프로그램 CDN 끝점 tooa의 다양 한 원본에서 기본 사용 현황 메트릭 tooexport 사용자 지정 된 방식으로 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-114">Diagnostics logs allow you tooexport basic usage metrics from your CDN endpoint tooa variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="2bfd4-115">수행할 수는 예를 들어 다음 데이터 내보내기의 유형을 hello:</span><span class="sxs-lookup"><span data-stu-id="2bfd4-115">For example, you can do hello following types of data export:</span></span>

- <span data-ttu-id="2bfd4-116">데이터 tooblob 저장소 내보내기, tooCSV, 내보내기 및 그래프를 생성 합니다. excel에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-116">Export data tooblob storage, export tooCSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="2bfd4-117">Tooevent 허브 데이터를 내보내고 다른 azure 서비스의 데이터로 상관 관계를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-117">Export data tooevent hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="2bfd4-118">OMS 작업 영역에서 데이터 toolog 보기 및 분석 데이터 내보내기</span><span class="sxs-lookup"><span data-stu-id="2bfd4-118">Export data toolog analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="2bfd4-119">hello 다음 그림은 데이터에 대 한 일반적인 CDN 코어 분석 뷰.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-119">hello following figure shows a typical CDN Core Analytics view into data.</span></span>

![포털 - 진단 로그](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="2bfd4-121">*그림 1 - CDN 핵심 분석 뷰*</span><span class="sxs-lookup"><span data-stu-id="2bfd4-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="2bfd4-122">연습을 수행 하는 hello hello 스키마의 hello 코어 분석 데이터를 hello 기능을 사용 하 고 toovarious 대상에 게 배달 하 고, 이러한 대상에서 사용에 관련 된 단계를 거칩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-122">hello following walkthrough goes through hello schema of hello core analytics data, steps involved in enabling hello feature and delivering them toovarious destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="2bfd4-123">Azure Portal에서 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2bfd4-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="2bfd4-124">hello 진단 로그는 되어 **오프** 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-124">hello diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="2bfd4-125">CDN 코어 분석을 tooenable 로깅 아래 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-125">Follow hello steps below tooenable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="2bfd4-126">Toohello 로그인 [Azure 포털](http://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-126">Sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2bfd4-127">워크플로에 대해 아직 CDN을 사용하도록 설정하지 않은 경우 계속하기 전에 [Azure CDN을 사용](cdn-create-new-endpoint.md)하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="2bfd4-128">Hello 포털에서 이동 너무**CDN 프로필**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-128">In hello portal, navigate too**CDN profile**.</span></span>
2. <span data-ttu-id="2bfd4-129">CDN 프로필을 선택 하 고 원하는 tooenable hello CDN 끝점을 선택 **진단 로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-129">Select a CDN profile, then select hello CDN endpoint that you want tooenable **Diagnostics Logs**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="2bfd4-131">너무 이동**진단 로그** 아래 블레이드 **모니터링** 섹션에서 다음도 hello 상태 변경**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-131">Go too**Diagnostics Logs** blade Under **Monitoring** section, then change hello status too**On**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="2bfd4-133">Azure Storage에서 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2bfd4-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="2bfd4-134">toouse Azure 저장소 toostore hello 로그 선택 **tooa 저장소 계정 보관**, 보존 (일)를 선택 하 고 클릭 **CoreAnalytics** 아래 **로그**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-134">toouse Azure Storage toostore hello logs, select **Archive tooa storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![포털 - 진단 로그](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="2bfd4-136">*그림 2 - Azure Storage로 로깅*</span><span class="sxs-lookup"><span data-stu-id="2bfd4-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="2bfd4-137">OMS Log Analytics로 로깅</span><span class="sxs-lookup"><span data-stu-id="2bfd4-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="2bfd4-138">toouse OMS 로그 분석 toostore hello 로그는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-138">toouse OMS Log Analytics toostore hello logs, follow these steps:</span></span>

1. <span data-ttu-id="2bfd4-139">Hello에서 **진단 로그** 아래 블레이드 **모니터링**선택, **tooLog 분석 보내기** 에서</span><span class="sxs-lookup"><span data-stu-id="2bfd4-139">From hello **Diagnostics Logs** blade Under **Monitoring**, select **Send tooLog Analytics** from</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="2bfd4-141">구성을 클릭 하 여 hello 로그 분석 로깅을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-141">Configure hello Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="2bfd4-142">이렇게 하면 tooa 대화 이전 작업 영역을 선택 하거나 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-142">This takes you tooa dialog where you can select a previous workspace or create a new one.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="2bfd4-144">**새 작업 영역 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-144">Click **Create New Workspace**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="2bfd4-146">그런 다음 새 작업 영역 이름, 기존 구독, 리소스 그룹(새로운 또는 기존), 위치 및 가격 책정 계층을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="2bfd4-147">이 구성 tooyour 대시보드에 고정 hello 선택할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-147">You have hello option of pinning this configuration tooyour dashboard.</span></span> <span data-ttu-id="2bfd4-148">확인 toocomplete hello 구성을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-148">Click OK toocomplete hello configuration.</span></span>

    <span data-ttu-id="2bfd4-149">그러면 OMS 작업 영역 및 리소스 그룹 이름과 함께 작업 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="2bfd4-150">이름은 고유해야 하며 문자, 숫자 및 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="2bfd4-151">공백 및 밑줄은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-151">Spaces and underscores are not allowed.</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="2bfd4-153">다음 작업 영역을 만든 및 구성 화면 로깅 tooyour 반환될지 말하는 짧은 메시지를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-153">You next get a short message saying that your workspace has been created and you are returned tooyour logging configuration screen.</span></span> <span data-ttu-id="2bfd4-154">로그 분석 작업 영역의 hello 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-154">You can confirm hello name of your Log Analytics workspace.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="2bfd4-156">Hello 로그 분석 구성을 설정한 되 면 CDN 로깅에 대 한 hello CoreAnalytics 상자도 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-156">Once you have set up hello Log Analytics configuration, make sure you also check hello CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="2bfd4-157">원하는 대로 tooyour 내용이 없으면 클릭 hello **저장** hello hello 구성 대화 상자 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-157">If everything is tooyour liking, click hello **Save** button at hello top of hello configuration dialog.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="2bfd4-159">hello **저장** 단추는 더 이상 활성 및 해당 hello/끄기 단추는 이제 ON, 하지만 자주색 아닌 파란색입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-159">hello **Save** button is no longer active and that hello ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="2bfd4-160">새 OMS 작업 영역 toosee을 원하는 경우 이동 tooyour Azure 포털의 대시보드를 hello 로그 분석 작업 영역 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-160">If you want toosee your new OMS workspace, go tooyour Azure portal Dashboard, click hello name of your Log Analytics workspace.</span></span> <span data-ttu-id="2bfd4-161">작업 영역을 다음 표시 됩니다 (있는지 OMS 작업 영역 hello 왼쪽에 강조 표시 되어 있는지 확인).</span><span class="sxs-lookup"><span data-stu-id="2bfd4-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on hello left).</span></span> <span data-ttu-id="2bfd4-162">Hello OMS 포털 타일 toosee hello OMS 리포지토리에 작업 영역 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-162">Click on hello OMS Portal tile toosee your workspace in hello OMS repository.</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="2bfd4-164">OMS 리포지토리는 준비 toolog 데이터.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-164">Your OMS repository is now ready toolog data.</span></span> <span data-ttu-id="2bfd4-165">순서로 tooconsume 해당 데이터를 사용 해야 합니다는 [OMS 솔루션](#consuming-oms-log-analytics-data),이 문서의 뒷부분에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-165">In order tooconsume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="2bfd4-166">로그 데이터 지연에 대한 자세한 내용은 [여기](#log-data-delays)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="2bfd4-167">PowerShell을 통해 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="2bfd4-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="2bfd4-168">다음은 방법을 통해 tooenable 및 get 진단 로그 hello Azure PowerShell Cmdlet의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-168">Below is an example on how tooenable and get Diagnostic Logs via hello Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="2bfd4-169">저장소 계정에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="2bfd4-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="2bfd4-170">먼저 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="2bfd4-171">tooEnable 진단 로그는 저장소 계정에이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-171">tooEnable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="2bfd4-172">tooEnable 진단 로그는 OMS 작업 영역에서에이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-172">tooEnable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="2bfd4-173">Azure Storage에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="2bfd4-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="2bfd4-174">이 섹션에서는 hello CDN 코어 분석의 hello 스키마 설명, 샘플 코드 toodownload hello tooa CSV 파일의 로그는 Azure 저장소 계정 내에서 구성 된 이러한 및 제공 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-174">This section describes hello schema of hello CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code toodownload hello logs in tooa CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="2bfd4-175">Microsoft Azure Storage 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="2bfd4-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="2bfd4-176">Hello Azure 저장소 계정에서에서 hello 코어 분석 데이터에 액세스 하기 전에 먼저 저장소 계정에 도구 tooaccess hello 내용을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-176">Before you can access hello core analytics data from hello Azure Storage Account, you first need a tool tooaccess hello contents in a storage account.</span></span> <span data-ttu-id="2bfd4-177">Hello 시장에서 사용할 수 있는 여러 도구가 있습니다, hello Microsoft Azure 저장소 탐색기는 hello 하나 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-177">While there are several tools available in hello market, hello one that we recommend is hello Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="2bfd4-178">Hello 도구를 다운로드할 수 [여기](http://storageexplorer.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-178">You can download hello tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="2bfd4-179">Hello 소프트웨어 다운로드 및 설치 구성 후 toouse hello 대상 toohello CDN 진단 로그로 구성 된 동일한 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-179">After downloading and installing hello software, configure it toouse hello same Azure Storage Account that was configured as a destination toohello CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="2bfd4-180">**Microsoft Azure Storage 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="2bfd4-181">Hello 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="2bfd4-181">Locate hello storage account</span></span>
3.  <span data-ttu-id="2bfd4-182">Toohello 이동 **"Blob 컨테이너"** 노드 아래의이 저장소 계정 및 hello 노드 확장</span><span class="sxs-lookup"><span data-stu-id="2bfd4-182">Go toohello **“Blob Containers”** node under this storage account and expand hello node</span></span>
4.  <span data-ttu-id="2bfd4-183">라는 선택 hello 컨테이너 **"insights 로그 coreanalytics"** 두 번 클릭 하 고</span><span class="sxs-lookup"><span data-stu-id="2bfd4-183">Select hello container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="2bfd4-184">표시 위로 hello 오른쪽 창에서 hello로 먼저 시작 수준으로 다음과 같은 결과 **"resourceId ="**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-184">Results show up on hello right-hand pane starting with hello first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="2bfd4-185">계속 hello 파일 표시 될 때까지 모든 hello 방법을 클릭 **PT1H.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-185">Continue clicking all hello way until you see hello file **PT1H.json**.</span></span> <span data-ttu-id="2bfd4-186">Hello 다음 hello 경로 대 한 설명에 대 한 참고를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-186">See hello following note for explanation of hello path.</span></span>
6.  <span data-ttu-id="2bfd4-187">각 blob **PT1H.json** 나타내는 특정 CDN 끝점 또는 해당 사용자 지정 도메인에 대 한 시간에 대 한 분석 로그 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-187">Each blob **PT1H.json** represents hello analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="2bfd4-188">이 JSON 파일의 hello 내용의 hello 스키마 hello 코어 분석 로그의 hello 섹션 스키마에서 설명</span><span class="sxs-lookup"><span data-stu-id="2bfd4-188">hello schema of hello contents of this JSON file is described in hello section Schema of hello Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="2bfd4-189">**Blob 경로 형식**</span><span class="sxs-lookup"><span data-stu-id="2bfd4-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="2bfd4-190">핵심 분석 로그에는 1시간마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="2bfd4-191">1시간 동안의 모든 데이터는 수집된 후 단일 Azure Blob 내에 JSON 페이로드로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="2bfd4-192">hello 경로 toothis Azure Blob는 계층 구조 처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-192">hello path toothis Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="2bfd4-193">Hello 저장소 탐색기 도구 해석 하기 때문에 '/'를 디렉터리 구분 기호로 이므로 편의 위해 hello 계층을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-193">This is because hello Storage explorer tool interprets '/' as a directory separator and shows hello hierarchy for convenience.</span></span> <span data-ttu-id="2bfd4-194">실제로, 전체 경로 hello hello blob 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-194">Actually, hello whole path just represents hello blob name.</span></span> <span data-ttu-id="2bfd4-195">이 hello blob의 이름은 hello 명명 규칙</span><span class="sxs-lookup"><span data-stu-id="2bfd4-195">This name of hello blob follows hello following naming convention</span></span> 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="2bfd4-196">**필드 설명:**</span><span class="sxs-lookup"><span data-stu-id="2bfd4-196">**Description of fields:**</span></span>

|<span data-ttu-id="2bfd4-197">값</span><span class="sxs-lookup"><span data-stu-id="2bfd4-197">value</span></span>|<span data-ttu-id="2bfd4-198">description</span><span class="sxs-lookup"><span data-stu-id="2bfd4-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="2bfd4-199">구독 ID</span><span class="sxs-lookup"><span data-stu-id="2bfd4-199">Subscription ID</span></span>    |<span data-ttu-id="2bfd4-200">Azure 구독 hello의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-200">ID of hello Azure Subscription.</span></span> <span data-ttu-id="2bfd4-201">Hello Guid 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-201">This is in hello Guid format.</span></span>|
|<span data-ttu-id="2bfd4-202">리소스</span><span class="sxs-lookup"><span data-stu-id="2bfd4-202">Resource</span></span> |<span data-ttu-id="2bfd4-203">그룹 이름 hello 리소스 그룹 toowhich hello CDN 리소스의 이름에 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-203">Group Name   Name of hello resource group toowhich hello CDN resources belong.</span></span>|
|<span data-ttu-id="2bfd4-204">프로필 이름</span><span class="sxs-lookup"><span data-stu-id="2bfd4-204">Profile Name</span></span> |<span data-ttu-id="2bfd4-205">Hello CDN 프로필의 이름</span><span class="sxs-lookup"><span data-stu-id="2bfd4-205">Name of hello CDN Profile</span></span>|
|<span data-ttu-id="2bfd4-206">끝점 이름</span><span class="sxs-lookup"><span data-stu-id="2bfd4-206">Endpoint Name</span></span> |<span data-ttu-id="2bfd4-207">Hello CDN 끝점의 이름</span><span class="sxs-lookup"><span data-stu-id="2bfd4-207">Name of hello CDN Endpoint</span></span>|
|<span data-ttu-id="2bfd4-208">Year</span><span class="sxs-lookup"><span data-stu-id="2bfd4-208">Year</span></span>|  <span data-ttu-id="2bfd4-209">예를 들어 2017 hello 연도의 4 자릿수로 표시</span><span class="sxs-lookup"><span data-stu-id="2bfd4-209">4-digit representation of hello year for example, 2017</span></span>|
|<span data-ttu-id="2bfd4-210">월</span><span class="sxs-lookup"><span data-stu-id="2bfd4-210">Month</span></span>| <span data-ttu-id="2bfd4-211">hello 월 수의 2 자리 표현입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-211">2-digit representation of hello month number.</span></span> <span data-ttu-id="2bfd4-212">01=1월 ... 12=12월</span><span class="sxs-lookup"><span data-stu-id="2bfd4-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="2bfd4-213">일</span><span class="sxs-lookup"><span data-stu-id="2bfd4-213">Day</span></span>|   <span data-ttu-id="2bfd4-214">hello hello 월간 일자 2 자릿수로 표시</span><span class="sxs-lookup"><span data-stu-id="2bfd4-214">2 digit representation of hello day of hello month</span></span>|
|<span data-ttu-id="2bfd4-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2bfd4-215">PT1H.json</span></span>| <span data-ttu-id="2bfd4-216">Hello 분석 데이터가 저장 되는 실제 JSON 파일</span><span class="sxs-lookup"><span data-stu-id="2bfd4-216">Actual JSON file where hello analytics data is stored</span></span>|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a><span data-ttu-id="2bfd4-217">Hello 코어 분석 데이터 tooa CSV 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="2bfd4-217">Exporting hello Core Analytics Data tooa CSV File</span></span>

<span data-ttu-id="2bfd4-218">toomake 쉽게 tooaccess hello 코어 분석을 제공 하는 it tooeasily 사용된 될 수 있는 쉼표로 구분 된 플랫 파일 형식으로 hello JSON 파일을 다운로드할 수 있는 도구에 대 한 샘플 코드 차트 또는 다른 집계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-218">toomake it easy tooaccess hello Core Analytics, we provide a sample code for a tool, which allows downloading hello JSON files into a flat comma-separated file format, which can be used tooeasily create charts or other aggregations.</span></span>

<span data-ttu-id="2bfd4-219">Hello 도구를 사용 하는 방법을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-219">Here is how you can use hello tool:</span></span>

1.  <span data-ttu-id="2bfd4-220">Hello github 링크를 방문: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span><span class="sxs-lookup"><span data-stu-id="2bfd4-220">Visit hello github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="2bfd4-221">Hello 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="2bfd4-221">Download hello code</span></span>
3.  <span data-ttu-id="2bfd4-222">Toocompile 지침에 따라 및 구성</span><span class="sxs-lookup"><span data-stu-id="2bfd4-222">Follow instructions toocompile and configure</span></span>
4.  <span data-ttu-id="2bfd4-223">Hello 도구 실행</span><span class="sxs-lookup"><span data-stu-id="2bfd4-223">Run hello tool</span></span>
5.  <span data-ttu-id="2bfd4-224">결과 CSV 파일 간단한 플랫 계층의 hello 분석 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-224">Resulting CSV file shows hello analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="2bfd4-225">OMS Log Analytics 리포지토리에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="2bfd4-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="2bfd4-226">로그 분석은에 OMS Operations Management Suite ()의 가용성과 성능을 클라우드 및 온-프레미스 환경 toomaintain 프로그램을 모니터링 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments toomaintain their availability and performance.</span></span> <span data-ttu-id="2bfd4-227">여러 소스에서 리소스를 클라우드 및 온-프레미스 환경에서와 다른 모니터링 도구 tooprovide 분석에 의해 생성 된 데이터를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools tooprovide analysis across multiple sources.</span></span> 

<span data-ttu-id="2bfd4-228">toouse 로그 분석을 수행 해야 [로깅을 사용 하도록 설정](#enable-logging-with-azure-storage) toohello Azure OMS 로그 분석 저장소가이 문서의 앞부분에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-228">toouse Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) toohello Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-hello-oms-repository"></a><span data-ttu-id="2bfd4-229">OMS 리포지토리에 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="2bfd4-229">Using hello OMS Repository</span></span>

 <span data-ttu-id="2bfd4-230">다이어그램을 다음 hello hello 입력의 hello 아키텍처 및 hello 저장소의 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-230">hello following diagram shows hello architecture of hello inputs and outputs of hello repository:</span></span>

![OMS Log Analytics 리포지토리](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="2bfd4-232">*그림 3 - Log Analytics 리포지토리*</span><span class="sxs-lookup"><span data-stu-id="2bfd4-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="2bfd4-233">관리 솔루션을 사용 하 여 여러 가지 방법으로 hello 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-233">You can display hello data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="2bfd4-234">Hello에서 관리 솔루션을 가져올 수 있습니다 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-234">You can obtain Management Solutions from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="2bfd4-235">Hello를 클릭 하 여 Azure marketplace의 관리 솔루션을 설치할 수 있습니다 **지금 사용해 보세요** 각 솔루션의 hello 맨 아래에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-235">You can install management solutions from Azure marketplace by clicking hello **Get it now** link at hello bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="2bfd4-236">OMS CDN 관리 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="2bfd4-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="2bfd4-237">이러한 단계 tooadd 관리 솔루션을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-237">Follow these steps tooadd a Management Solution:</span></span>

1.   <span data-ttu-id="2bfd4-238">아직 그렇게 수행 하지 않은, toohello Azure 구독을 사용 하 여 Azure 포털 로그인을 tooyour 대시보드를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-238">If you haven't already done so, sign in toohello Azure portal using your Azure subscription and go tooyour Dashboard.</span></span>
    <span data-ttu-id="2bfd4-239">![Azure 대시보드](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="2bfd4-240">Hello에 **새로** 아래 블레이드 **마켓플레이스**선택, **모니터링 + 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-240">In hello **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![마켓플레이스](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="2bfd4-242">Hello에 **모니터링 + 관리** 블레이드에서 클릭 **스크롤하게**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-242">In hello **Monitoring + management** blade, click **See all**.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="2bfd4-244">Hello 검색 상자에 CDN에 대 한 검색입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-244">Search for CDN in hello search box.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="2bfd4-246">**Azure CDN 핵심 분석**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="2bfd4-248">클릭 한 후 **만들기**, 됩니다 toocreate 새로운 OMS 작업 영역을 요청 하거나 기존 집합을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-248">After clicking **Create**, you will be asked toocreate a new OMS workspace or use an existing one.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="2bfd4-250">전에 만든 hello 작업 영역을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-250">Select hello workspace you created before.</span></span> <span data-ttu-id="2bfd4-251">다음 자동화 계정을 tooadd를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-251">You then need tooadd an automation account.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="2bfd4-253">hello 다음 화면 표시를 작성 해야 하는 hello 자동화 계정 폼 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-253">hello following screen shows hello automation account form you must fill out.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="2bfd4-255">준비 tooadd는 hello 자동화 계정을 만든 후 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-255">Once you have created hello automation account, you are ready tooadd your solution.</span></span> <span data-ttu-id="2bfd4-256">Hello 클릭 **만들기** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-256">Click hello **Create** button.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="2bfd4-258">솔루션에 이제 tooyour 작업 영역을 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-258">Your solution has now been added tooyour workspace.</span></span> <span data-ttu-id="2bfd4-259">Azure 포털의 대시보드 tooyour를 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-259">Go back tooyour Azure portal Dashboard.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="2bfd4-261">Toogo tooyour 작업 영역을 만든 hello 로그 분석 작업 영역을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-261">Click hello Log Analytics workspace you created toogo tooyour workspace.</span></span> 

11. <span data-ttu-id="2bfd4-262">Hello 클릭 **OMS 포털** toosee hello OMS 포털에서 새 솔루션 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-262">Click hello **OMS Portal** tile toosee your new solution in hello OMS portal.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="2bfd4-264">OMS 포털은 이제 다음 화면 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-264">Your OMS portal should now look like hello following screen:</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="2bfd4-266">중 하나를 클릭 hello 타일 toosee 여러 뷰 데이터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-266">Click one of hello tiles toosee several views into your data.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="2bfd4-268">왼쪽 스크롤할 수 또는 오른쪽 toosee 추가로 hello 데이터로 개별 보기를 나타내는 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-268">You can scroll left or right toosee further tiles representing individual views into hello data.</span></span> 

    <span data-ttu-id="2bfd4-269">Hello 타일 중 하나를 클릭 하 여 데이터에 대 한 자세한 내용은 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-269">Clicking one of hello tiles gives you more details about your data.</span></span>

     ![모두 표시](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="2bfd4-271">제품 및 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="2bfd4-271">Offers and pricing tiers</span></span>

<span data-ttu-id="2bfd4-272">[여기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)에서 OMS 관리 솔루션에 대한 제품 및 가격 책정 계층을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="2bfd4-273">뷰 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2bfd4-273">Customizing views</span></span>

<span data-ttu-id="2bfd4-274">Hello 보기 hello를 사용 하 여 데이터를 사용자 지정할 수 **뷰 디자이너**합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-274">You can customize hello view into your data by using hello **View Designer**.</span></span> <span data-ttu-id="2bfd4-275">Tooyour OMS 작업 영역을 이동 하 고 hello를 클릭 하 여 설계를 시작 **뷰 디자이너** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-275">Go tooyour OMS workspace and begin designing by clicking hello **View Designer** tile.</span></span>

![뷰 디자이너](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="2bfd4-277">있습니다 수 끌어서의 차트 종류 hello 왼쪽에서 놓은 tooanalyze hello 왼쪽에 원하는 hello 데이터 세부 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-277">You can drag and drop types of charts from hello left and fill in hello data details you want tooanalyze on hello left.</span></span>

![뷰 디자이너](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="2bfd4-279">로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="2bfd4-279">Log data delays</span></span>

<span data-ttu-id="2bfd4-280">Verizon 로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="2bfd4-280">Verizon log data delays</span></span> | <span data-ttu-id="2bfd4-281">Akamai 로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="2bfd4-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="2bfd4-282">Verizon 로그 데이터가 1 시간 지연 되 고 too2 시간 toostart 끝점 전파가 완료 된 후 표시를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-282">Verizon log data is 1 hour delayed, and take up too2 hours toostart appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="2bfd4-283">Akamai 로그 데이터는 지연 24 시간 및 24 시간 넘게 만들어진 경우 나타나는 too2 시간 toostart 차지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-283">Akamai log data is 24 hours delayed, and takes up too2 hours toostart appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="2bfd4-284">최근에 만든 경우 hello 로그 toostart 표시에 대 한 too25 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-284">If it was recently created, it can take up too25 hours for hello logs toostart appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="2bfd4-285">CDN 핵심 분석에 대한 진단 로그 유형</span><span class="sxs-lookup"><span data-stu-id="2bfd4-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="2bfd4-286">현재 HTTP 응답 통계 및 hello CDN Pop/가장자리에서에서 본 송신 통계를 표시 하는 메트릭을 포함 하는 핵심 분석 로그만을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from hello CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="2bfd4-287">핵심 분석 메트릭 정보</span><span class="sxs-lookup"><span data-stu-id="2bfd4-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="2bfd4-288">다음 표에서 hello hello 코어 분석 로그에서 사용할 수 있는 메트릭 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-288">hello following table shows a list of metrics available in hello Core Analytics logs.</span></span> <span data-ttu-id="2bfd4-289">모든 공급자의 모든 메트릭을 사용할 수 있는 것은 아니지만 이러한 차이는 미미합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="2bfd4-290">다음 표도 hello 지정된 된 메트릭이 공급자에서 사용할 수 있는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-290">hello following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="2bfd4-291">때문에 해당 CDN 끝점에 트래픽을 있는 사용할 수 있는 hello 메트릭이 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-291">Please note that hello metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="2bfd4-292">메트릭</span><span class="sxs-lookup"><span data-stu-id="2bfd4-292">Metric</span></span>                     | <span data-ttu-id="2bfd4-293">설명</span><span class="sxs-lookup"><span data-stu-id="2bfd4-293">Description</span></span>   | <span data-ttu-id="2bfd4-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="2bfd4-294">Verizon</span></span>  | <span data-ttu-id="2bfd4-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="2bfd4-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="2bfd4-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="2bfd4-296">RequestCountTotal</span></span>         |<span data-ttu-id="2bfd4-297">이 기간 동안의 요청 적중의 총 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-297">Total number of request hits during this period</span></span>| <span data-ttu-id="2bfd4-298">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-298">Yes</span></span>  |<span data-ttu-id="2bfd4-299">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-299">Yes</span></span>   |
| <span data-ttu-id="2bfd4-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="2bfd4-301">2xx HTTP 코드(예: 200, 202)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="2bfd4-302">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-302">Yes</span></span>  |<span data-ttu-id="2bfd4-303">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-303">Yes</span></span>   |
| <span data-ttu-id="2bfd4-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="2bfd4-305">3xx HTTP 코드(예: 300, 302)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="2bfd4-306">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-306">Yes</span></span>  |<span data-ttu-id="2bfd4-307">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-307">Yes</span></span>   |
| <span data-ttu-id="2bfd4-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="2bfd4-309">4xx HTTP 코드(예: 400, 404)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="2bfd4-310">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-310">Yes</span></span>   |<span data-ttu-id="2bfd4-311">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-311">Yes</span></span>   |
| <span data-ttu-id="2bfd4-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="2bfd4-313">5xx HTTP 코드(예: 500, 504)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="2bfd4-314">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-314">Yes</span></span>  |<span data-ttu-id="2bfd4-315">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-315">Yes</span></span>   |
| <span data-ttu-id="2bfd4-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="2bfd4-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="2bfd4-317">다른 모든 HTTP 코드의 수(2xx-5xx 이외)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="2bfd4-318">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-318">Yes</span></span>  |<span data-ttu-id="2bfd4-319">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-319">Yes</span></span>   |
| <span data-ttu-id="2bfd4-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="2bfd4-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="2bfd4-321">200 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="2bfd4-322">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-322">No</span></span>   |<span data-ttu-id="2bfd4-323">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-323">Yes</span></span>   |
| <span data-ttu-id="2bfd4-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="2bfd4-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="2bfd4-325">206 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="2bfd4-326">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-326">No</span></span>   |<span data-ttu-id="2bfd4-327">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-327">Yes</span></span>   |
| <span data-ttu-id="2bfd4-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="2bfd4-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="2bfd4-329">302 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="2bfd4-330">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-330">No</span></span>   |<span data-ttu-id="2bfd4-331">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-331">Yes</span></span>   |
| <span data-ttu-id="2bfd4-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="2bfd4-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="2bfd4-333">304 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="2bfd4-334">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-334">No</span></span>   |<span data-ttu-id="2bfd4-335">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-335">Yes</span></span>   |
| <span data-ttu-id="2bfd4-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="2bfd4-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="2bfd4-337">404 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="2bfd4-338">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-338">No</span></span>   |<span data-ttu-id="2bfd4-339">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-339">Yes</span></span>   |
| <span data-ttu-id="2bfd4-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="2bfd4-340">RequestCountCacheHit</span></span> |<span data-ttu-id="2bfd4-341">캐시 적중을 발생한 모든 요청의 수.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="2bfd4-342">이 hello 자산 hello POP toohello 클라이언트에서 직접 처리 된 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-342">This means hello asset was served directly from hello POP toohello Client.</span></span>               | <span data-ttu-id="2bfd4-343">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-343">Yes</span></span>  |<span data-ttu-id="2bfd4-344">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-344">No</span></span>   |
| <span data-ttu-id="2bfd4-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="2bfd4-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="2bfd4-346">캐시 누락을 발생한 모든 요청의 수.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="2bfd4-347">즉 hello 자산 hello POP 가장 가까운 toohello 클라이언트에서 찾을 수 없습니다 하며 따라서 hello 원본에서에서 검색 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-347">This means hello asset was not found on hello POP closest toohello client, and therefore was retrieved from hello Origin.</span></span>              |<span data-ttu-id="2bfd4-348">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-348">Yes</span></span>   | <span data-ttu-id="2bfd4-349">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-349">No</span></span>  |
| <span data-ttu-id="2bfd4-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="2bfd4-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="2bfd4-351">모든의 개수를 hello 가장자리에 tooa 사용자 구성 인해 캐시에 저장할 수 없습니다 tooan 자산을 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-351">Count of all requests tooan asset that are prevented from being cached due tooa user configuration on hello edge.</span></span>              |<span data-ttu-id="2bfd4-352">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-352">Yes</span></span>   | <span data-ttu-id="2bfd4-353">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-353">No</span></span>  |
| <span data-ttu-id="2bfd4-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="2bfd4-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="2bfd4-355">모든의 개수를 hello 자산의 캐시 제어 하 여 캐시에 저장할 수 없습니다 tooassets를 요청 하 고 있는지 것 캐시 되어서는 안 POP 또는 hello HTTP 클라이언트에서 표시 하는 헤더가 만료</span><span class="sxs-lookup"><span data-stu-id="2bfd4-355">Count of all requests tooassets that are prevented from being cached by hello asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                |<span data-ttu-id="2bfd4-356">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-356">Yes</span></span>   |<span data-ttu-id="2bfd4-357">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-357">No</span></span>   |
| <span data-ttu-id="2bfd4-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="2bfd4-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="2bfd4-359">위에 포함되지 않는 캐시 상태를 갖는 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="2bfd4-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="2bfd4-360">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-360">Yes</span></span>   | <span data-ttu-id="2bfd4-361">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-361">No</span></span>  |
| <span data-ttu-id="2bfd4-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="2bfd4-362">EgressTotal</span></span> | <span data-ttu-id="2bfd4-363">아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="2bfd4-364">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-364">Yes</span></span>   |<span data-ttu-id="2bfd4-365">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-365">Yes</span></span>   |
| <span data-ttu-id="2bfd4-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="2bfd4-367">2xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송*(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="2bfd4-368">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-368">Yes</span></span>   |<span data-ttu-id="2bfd4-369">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-369">No</span></span>   |
| <span data-ttu-id="2bfd4-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="2bfd4-371">3xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="2bfd4-372">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-372">Yes</span></span>   |<span data-ttu-id="2bfd4-373">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-373">No</span></span>   |
| <span data-ttu-id="2bfd4-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="2bfd4-375">4xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="2bfd4-376">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-376">Yes</span></span>   | <span data-ttu-id="2bfd4-377">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-377">No</span></span>  |
| <span data-ttu-id="2bfd4-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="2bfd4-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="2bfd4-379">5xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="2bfd4-380">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-380">Yes</span></span>   |  <span data-ttu-id="2bfd4-381">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-381">No</span></span> |
| <span data-ttu-id="2bfd4-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="2bfd4-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="2bfd4-383">다른 HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="2bfd4-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="2bfd4-384">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-384">Yes</span></span>   |<span data-ttu-id="2bfd4-385">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-385">No</span></span>   |
| <span data-ttu-id="2bfd4-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="2bfd4-386">EgressCacheHit</span></span> |  <span data-ttu-id="2bfd4-387">아웃 바운드 데이터 전송 전송 된 응답에 대 한 hello CDN 캐시에서 직접의 hello CDN Pop/가장자리</span><span class="sxs-lookup"><span data-stu-id="2bfd4-387">Outbound data transfer for responses that were delivered directly from hello CDN cache on hello CDN POPs/Edges</span></span>  |<span data-ttu-id="2bfd4-388">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-388">Yes</span></span>   |  <span data-ttu-id="2bfd4-389">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-389">No</span></span> |
| <span data-ttu-id="2bfd4-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="2bfd4-390">EgressCacheMiss</span></span> | <span data-ttu-id="2bfd4-391">가장 근접 한 POP 서버 hello에서 발견 되 고 hello 원본 서버에서 검색 된 응답에 대 한 아웃 바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="2bfd4-391">Outbound data transfer for responses that were not found on hello nearest POP server, and retrieved from hello origin server</span></span>              |<span data-ttu-id="2bfd4-392">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-392">Yes</span></span>   |  <span data-ttu-id="2bfd4-393">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-393">No</span></span> |
| <span data-ttu-id="2bfd4-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="2bfd4-394">EgressCacheNoCache</span></span> | <span data-ttu-id="2bfd4-395">hello 가장자리에 tooa 사용자 구성 인해 캐시에 저장할 수 없는 자산에 대 한 아웃 바운드 데이터 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-395">Outbound data transfer for assets that are prevented from being cached due tooa user configuration on hello edge.</span></span>                |<span data-ttu-id="2bfd4-396">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-396">Yes</span></span>   |<span data-ttu-id="2bfd4-397">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-397">No</span></span>   |
| <span data-ttu-id="2bfd4-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="2bfd4-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="2bfd4-399">hello 자산의 캐시 제어 및/또는 Expires 헤더는 해당 캐시 되어서는 안 POP에 또는 hello HTTP 클라이언트를 나타내는 캐시에 저장할 수 없는 자산에 대 한 아웃 바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="2bfd4-399">Outbound data transfer for assets that are prevented from being cached by hello asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by hello HTTP client</span></span>                    |<span data-ttu-id="2bfd4-400">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-400">Yes</span></span>   | <span data-ttu-id="2bfd4-401">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-401">No</span></span>  |
| <span data-ttu-id="2bfd4-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="2bfd4-402">EgressCacheOthers</span></span> |  <span data-ttu-id="2bfd4-403">다른 캐시 시나리오에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="2bfd4-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="2bfd4-404">예</span><span class="sxs-lookup"><span data-stu-id="2bfd4-404">Yes</span></span>   | <span data-ttu-id="2bfd4-405">아니요</span><span class="sxs-lookup"><span data-stu-id="2bfd4-405">No</span></span>  |

<span data-ttu-id="2bfd4-406">* 아웃 바운드 데이터 전송 참조 tootraffic CDN POP 서버 toohello 클라이언트에서 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-406">*Outbound data transfer refers tootraffic delivered from CDN POP servers toohello client.</span></span>


### <a name="schema-of-hello-core-analytics-logs"></a><span data-ttu-id="2bfd4-407">Hello 코어 분석 로그의 스키마</span><span class="sxs-lookup"><span data-stu-id="2bfd4-407">Schema of hello Core Analytics Logs</span></span> 

<span data-ttu-id="2bfd4-408">모든 로그는 JSON 형식에 저장 하 고 각 항목에 아래의 스키마 hello 다음 문자열 필드:</span><span class="sxs-lookup"><span data-stu-id="2bfd4-408">All logs are stored in JSON format and each entry has string fields following hello below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

<span data-ttu-id="2bfd4-409">여기서 hello 'time를' hello 통계 보고 hello 시간 경계의 hello 시작 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-409">Where hello ‘time’ represents hello start time of hello hour boundary for which hello statistics is reported.</span></span> <span data-ttu-id="2bfd4-410">CDN 공급자가 메트릭을 지원하지 않을 경우 double 또는 정수 값 대신 null 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="2bfd4-411">Null 값이 메트릭 hello 없음을 나타내고 0은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-411">This null value indicates hello absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="2bfd4-412">이러한 메트릭 hello 끝점에서 구성 된 도메인당 하나의 집합 생깁니다 참고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-412">Also note that there will be one set of these metrics per domain configured on hello endpoint.</span></span>

<span data-ttu-id="2bfd4-413">예제 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2bfd4-413">Example properties below:</span></span>

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a><span data-ttu-id="2bfd4-414">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="2bfd4-414">Additional resources</span></span>

* [<span data-ttu-id="2bfd4-415">Azure 진단 로그</span><span class="sxs-lookup"><span data-stu-id="2bfd4-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="2bfd4-416">Azure CDN 보조 포털을 통한 핵심 분석</span><span class="sxs-lookup"><span data-stu-id="2bfd4-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="2bfd4-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="2bfd4-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="2bfd4-418">Azure Log Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="2bfd4-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







