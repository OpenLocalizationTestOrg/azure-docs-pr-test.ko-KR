---
title: "Azure CDN에 대한 Log Analytics | Microsoft Docs"
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
ms.openlocfilehash: 03ff74ae4e40d3f2279caaf4f73e9b4aac6a2ebb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a><span data-ttu-id="e0535-103">Azure CDN에 대한 진단 로그</span><span class="sxs-lookup"><span data-stu-id="e0535-103">Diagnostics Logs for Azure CDN</span></span>

<span data-ttu-id="e0535-104">응용 프로그램에 대해 CDN을 사용하도록 설정한 후에는 CDN 사용을 모니터링하고, 전송 상태를 확인하고, 잠재적인 문제를 해결하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-104">After enabling CDN for your application, you will likely want to monitor the CDN usage, check the health of your delivery, and troubleshoot potential issues.</span></span> <span data-ttu-id="e0535-105">Azure CDN에서는 [CDN 핵심 분석](cdn-analyze-usage-patterns.md) 및 [진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)에 이러한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-105">Azure CDN provides these capabilities with [CDN Core Analytics](cdn-analyze-usage-patterns.md) and [Diagnostic Logs](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)</span></span>

## <a name="cdn-core-analytics"></a><span data-ttu-id="e0535-106">CDN 핵심 분석</span><span class="sxs-lookup"><span data-stu-id="e0535-106">CDN Core Analytics</span></span>
<span data-ttu-id="e0535-107">Verizon 표준 또는 프리미엄 프로필이 있는 현재 Azure CDN 사용자는 Azure Portal의 "관리" 옵션을 통해 액세스할 수 있는 보조 포털에서 이미 핵심 분석 기능을 볼 수 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-107">As a current Azure CDN user with Verizon standard or premium profile, you are already able to view core analytics in the supplemental portal accessible via the "Manage" option from the Azure portal.</span></span> 

## <a name="azure-diagnostic-logs"></a><span data-ttu-id="e0535-108">Azure 진단 로그</span><span class="sxs-lookup"><span data-stu-id="e0535-108">Azure Diagnostic Logs</span></span>

<span data-ttu-id="e0535-109">이 새로운 기능의 Azure를 통해 이제 핵심 분석을 보고 다음을 포함한 하나 이상의 대상에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-109">Azure With this new feature, you can now view core analytics and save them into one or more destinations including:</span></span>

 - <span data-ttu-id="e0535-110">Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="e0535-110">Azure Storage account</span></span>
 - <span data-ttu-id="e0535-111">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e0535-111">Azure Event Hubs</span></span>
 - [<span data-ttu-id="e0535-112">OMS Log Analytics 리포지토리</span><span class="sxs-lookup"><span data-stu-id="e0535-112">OMS Log Analytics repository</span></span>](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 <span data-ttu-id="e0535-113">이 기능은 Verizon(표준 및 프리미엄) 및 Akamai(표준) CDN 프로필에 속하는 모든 CDN 끝점에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-113">This feature is available for all CDN endpoints belonging to Verizon (Standard & Premium) and Akamai (Standard) CDN Profiles.</span></span>

<span data-ttu-id="e0535-114">진단 로그를 사용하면 사용자 지정 방식으로 사용할 수 있도록 CDN 끝점에서 다양한 원본으로 기본 사용 현황 메트릭을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-114">Diagnostics logs allow you to export basic usage metrics from your CDN endpoint to a variety of sources so that you can consume them in a customized way.</span></span> <span data-ttu-id="e0535-115">예를 들어 다음 유형의 데이터 내보내기를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-115">For example, you can do the following types of data export:</span></span>

- <span data-ttu-id="e0535-116">데이터를 Blob Storage로 내보내고, CSV로 내보낸 후 Excel에서 그래프를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-116">Export data to blob storage, export to CSV, and generate graphs in excel.</span></span>
- <span data-ttu-id="e0535-117">데이터를 Event Hubs로 내보내고 다른 Azure 서비스의 데이터와 상관 관계를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-117">Export data to event hubs and correlate with data from other azure services.</span></span>
- <span data-ttu-id="e0535-118">데이터를 Log Analytics로 내보내고, 고유한 OMS 작업 공간에서 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-118">Export data to log analytics and view data in your own OMS work space</span></span>

<span data-ttu-id="e0535-119">다음 그림에서는 데이터에 대한 일반적인 CDN 핵심 분석 뷰를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-119">The following figure shows a typical CDN Core Analytics view into data.</span></span>

![포털 - 진단 로그](./media/cdn-diagnostics-log/01_OMS-workspace.png)

<span data-ttu-id="e0535-121">*그림 1 - CDN 핵심 분석 뷰*</span><span class="sxs-lookup"><span data-stu-id="e0535-121">*Figure 1 - CDN Core Analytics view*</span></span>

<span data-ttu-id="e0535-122">다음 연습에서는 핵심 분석 데이터의 스키마, 기능을 사용하도록 설정한 후 다양한 대상에게 전송하는 단계, 이러한 대상에서 기능을 사용하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-122">The following walkthrough goes through the schema of the core analytics data, steps involved in enabling the feature and delivering them to various destinations, and consuming from these destinations.</span></span>

## <a name="enable-logging-with-azure-portal"></a><span data-ttu-id="e0535-123">Azure Portal에서 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e0535-123">Enable logging with Azure portal</span></span>

> [!NOTE]
> <span data-ttu-id="e0535-124">진단 로그는 기본적으로 **해제**됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-124">The diagnostics logs are turned **off** by default.</span></span> 

<span data-ttu-id="e0535-125">CDN 핵심 분석에서 로깅을 사용하도록 설정하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-125">Follow the steps below to enable logging with CDN Core Analytics:</span></span>

<span data-ttu-id="e0535-126">[Azure Portal](http://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-126">Sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="e0535-127">워크플로에 대해 아직 CDN을 사용하도록 설정하지 않은 경우 계속하기 전에 [Azure CDN을 사용](cdn-create-new-endpoint.md)하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-127">If you don't already have CDN enabled for your workflow, [Enable Azure CDN](cdn-create-new-endpoint.md) before you continue.</span></span>

1. <span data-ttu-id="e0535-128">포털에서 **CDN 프로필**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-128">In the portal, navigate to **CDN profile**.</span></span>
2. <span data-ttu-id="e0535-129">CDN 프로필을 선택한 다음 **진단 로그**를 사용하도록 설정하려는 CDN 끝점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-129">Select a CDN profile, then select the CDN endpoint that you want to enable **Diagnostics Logs**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. <span data-ttu-id="e0535-131">**모니터링** 섹션 아래의 **진단 로그** 블레이드로 이동한 후 상태를 **설정**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-131">Go to **Diagnostics Logs** blade Under **Monitoring** section, then change the status to **On**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a><span data-ttu-id="e0535-133">Azure Storage에서 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e0535-133">Enable logging with Azure Storage</span></span>
    
<span data-ttu-id="e0535-134">Azure Storage를 사용하여 로그를 저장하려면 **저장소 계정에 대한 보관**을 선택하고, 보존 기간을 선택하고, **로그** 아래에서 **CoreAnalytics**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-134">To use Azure Storage to store the logs, select **Archive to a storage account**, select retention days, and click **CoreAnalytics** under **Log**.</span></span>

![포털 - 진단 로그](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

<span data-ttu-id="e0535-136">*그림 2 - Azure Storage로 로깅*</span><span class="sxs-lookup"><span data-stu-id="e0535-136">*Figure 2 - Logging with Azure Storage*</span></span>

### <a name="logging-with-oms-log-analytics"></a><span data-ttu-id="e0535-137">OMS Log Analytics로 로깅</span><span class="sxs-lookup"><span data-stu-id="e0535-137">Logging with OMS Log Analytics</span></span>

<span data-ttu-id="e0535-138">OMS 로그 분석을 사용하여 로그를 저장하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-138">To use OMS Log Analytics to store the logs, follow these steps:</span></span>

1. <span data-ttu-id="e0535-139">**진단 로그** 블레이드의 **모니터링**에서 **Log Analytics에 보내기** 선택</span><span class="sxs-lookup"><span data-stu-id="e0535-139">From the **Diagnostics Logs** blade Under **Monitoring**, select **Send to Log Analytics** from</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. <span data-ttu-id="e0535-141">구성을 클릭하여 Log Analytics 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-141">Configure the Log Analytics logging by clicking on Configure.</span></span> <span data-ttu-id="e0535-142">그러면 이전 작업 영역을 선택하거나 새 작업 영역을 선택할 수 있는 대화 상자로 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-142">This takes you to a dialog where you can select a previous workspace or create a new one.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. <span data-ttu-id="e0535-144">**새 작업 영역 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-144">Click **Create New Workspace**.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/07_Create-new.png)

4. <span data-ttu-id="e0535-146">그런 다음 새 작업 영역 이름, 기존 구독, 리소스 그룹(새로운 또는 기존), 위치 및 가격 책정 계층을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-146">Next you must select a new workspace name, existing subscription, resource group (new or existing), location, and pricing tier.</span></span> <span data-ttu-id="e0535-147">이 구성을 대시보드에 고정하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-147">You have the option of pinning this configuration to your dashboard.</span></span> <span data-ttu-id="e0535-148">확인을 클릭하여 구성을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-148">Click OK to complete the configuration.</span></span>

    <span data-ttu-id="e0535-149">그러면 OMS 작업 영역 및 리소스 그룹 이름과 함께 작업 영역이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-149">Next you should see your workspace with your OMS Workspace and Resource group names.</span></span> <span data-ttu-id="e0535-150">이름은 고유해야 하며 문자, 숫자 및 하이픈만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-150">Names must be unique and can only use letters, numbers, and hyphens.</span></span> <span data-ttu-id="e0535-151">공백 및 밑줄은 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-151">Spaces and underscores are not allowed.</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. <span data-ttu-id="e0535-153">다음으로, 작업 영역이 생성되었으며 로깅 구성 화면으로 되돌아 갔다는 짧은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-153">You next get a short message saying that your workspace has been created and you are returned to your logging configuration screen.</span></span> <span data-ttu-id="e0535-154">Log Analytics 작업 영역의 이름을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-154">You can confirm the name of your Log Analytics workspace.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    <span data-ttu-id="e0535-156">Log Analytics 구성을 설정한 후 CDN 로깅을 위해 CoreAnalytics 상자도 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-156">Once you have set up the Log Analytics configuration, make sure you also check the CoreAnalytics box for CDN logging.</span></span>

6. <span data-ttu-id="e0535-157">원하는 대로 설정이 완료되면 구성 대화 상자의 맨 위에서 **저장** 단추를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-157">If everything is to your liking, click the **Save** button at the top of the configuration dialog.</span></span>

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/10_Save-me.png)

    <span data-ttu-id="e0535-159">**저장** 단추는 더 이상 활성 상태가 아니며 ON/OFF 단추가 현재 ON이지만, 자주색이 아닌 파란색입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-159">The **Save** button is no longer active and that the ON/OFF button is now ON, but blue instead of purple.</span></span>

7. <span data-ttu-id="e0535-160">새 OMS 작업 영역을 보려는 경우 Azure Portal 대시보드로 이동하여 Log Analytics 작업 영역의 이름을 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-160">If you want to see your new OMS workspace, go to your Azure portal Dashboard, click the name of your Log Analytics workspace.</span></span> <span data-ttu-id="e0535-161">그러면 작업 영역이 보입니다(왼쪽의 OMS 작업 영역이 강조 표시되어 있는지 확인).</span><span class="sxs-lookup"><span data-stu-id="e0535-161">Next you will see your workspace (make sure that OMS Workspace is highlighted on the left).</span></span> <span data-ttu-id="e0535-162">OMS 포털 타일을 클릭하여 OMS 리포지토리에서 작업 영역을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-162">Click on the OMS Portal tile to see your workspace in the OMS repository.</span></span> 

    ![포털 - 진단 로그](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    <span data-ttu-id="e0535-164">이제 OMS 리포지토리에 데이터를 기록 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-164">Your OMS repository is now ready to log data.</span></span> <span data-ttu-id="e0535-165">해당 데이터를 사용하려면 이 문서의 후반부에서 다루고 있는 [OMS 솔루션](#consuming-oms-log-analytics-data)을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-165">In order to consume that data, you must use an [OMS Solution](#consuming-oms-log-analytics-data), covered later in this article.</span></span>

<span data-ttu-id="e0535-166">로그 데이터 지연에 대한 자세한 내용은 [여기](#log-data-delays)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-166">For more information about log data delays, go [here](#log-data-delays).</span></span>

## <a name="enable-logging-with-powershell"></a><span data-ttu-id="e0535-167">PowerShell을 통해 로깅을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="e0535-167">Enable logging with PowerShell</span></span>

<span data-ttu-id="e0535-168">다음은 Azure PowerShell Cmdlet을 통해 진단 로그를 사용하도록 설정하고 가져오는 방법을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-168">Below is an example on how to enable and get Diagnostic Logs via the Azure PowerShell Cmdlets.</span></span>

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a><span data-ttu-id="e0535-169">저장소 계정에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="e0535-169">Enabling Diagnostic Logs in a Storage Account</span></span>

<span data-ttu-id="e0535-170">먼저 로그인하고 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-170">First log in and select a subscription:</span></span>

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


<span data-ttu-id="e0535-171">저장소 계정에서 진단 로그를 사용하도록 설정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-171">To Enable Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
<span data-ttu-id="e0535-172">OMS 작업 영역에서 진단 로그를 사용하도록 설정하려면이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-172">To Enable Diagnostics Logs in an OMS workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a><span data-ttu-id="e0535-173">Azure Storage에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="e0535-173">Consuming diagnostics logs from Azure Storage</span></span>
<span data-ttu-id="e0535-174">이 섹션에서는 CDN 핵심 분석의 스키마를 설명하고, Azure Storage 계정 내에서 이러한 분석을 구성하는 방법을 설명하며, 로그를 CSV 파일로 다운로드하기 위한 샘플 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-174">This section describes the schema of the CDN core analytics, how these are organized inside of an Azure Storage Account and provides sample code to download the logs in to a CSV file.</span></span>

### <a name="using-microsoft-azure-storage-explorer"></a><span data-ttu-id="e0535-175">Microsoft Azure Storage 탐색기 사용</span><span class="sxs-lookup"><span data-stu-id="e0535-175">Using Microsoft Azure Storage Explorer</span></span>
<span data-ttu-id="e0535-176">Azure Storage 계정에서 핵심 분석 데이터에 액세스하려면 먼저 저장소 계정의 콘텐츠에 액세스하기 위한 도구가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-176">Before you can access the core analytics data from the Azure Storage Account, you first need a tool to access the contents in a storage account.</span></span> <span data-ttu-id="e0535-177">시중에 여러 도구가 나와 있지만 Microsoft Azure Storage 탐색기가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-177">While there are several tools available in the market, the one that we recommend is the Microsoft Azure Storage Explorer.</span></span> <span data-ttu-id="e0535-178">이 도구는 [여기](http://storageexplorer.com/)서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-178">You can download the tool from [here](http://storageexplorer.com/).</span></span> <span data-ttu-id="e0535-179">이 소프트웨어를 다운로드하여 설치한 후에는 CDN 진단 로그의 대상으로 구성된 동일한 Azure Storage 계정을 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-179">After downloading and installing the software, configure it to use the same Azure Storage Account that was configured as a destination to the CDN Diagnostics Logs.</span></span>

1.  <span data-ttu-id="e0535-180">**Microsoft Azure Storage 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-180">Open **Microsoft Azure Storage Explorer**</span></span>
2.  <span data-ttu-id="e0535-181">저장소 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-181">Locate the storage account</span></span>
3.  <span data-ttu-id="e0535-182">이 저장소 계정 아래의 **"Blob 컨테이너"** 노드로 이동한 후 해당 노드를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-182">Go to the **“Blob Containers”** node under this storage account and expand the node</span></span>
4.  <span data-ttu-id="e0535-183">**“insights-logs-coreanalytics”**라는 컨테이너를 선택하고 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-183">Select the container named **“insights-logs-coreanalytics”** and double-click it</span></span>
5.  <span data-ttu-id="e0535-184">오른쪽 창에 결과가 표시되고 **“resourceId=”**와 같은 첫 번째 수준에서 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-184">Results show up on the right-hand pane starting with the first level, which looks like **“resourceId=”**.</span></span> <span data-ttu-id="e0535-185">**PT1H.json** 파일이 보일 때까지 모든 항목을 계속 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-185">Continue clicking all the way until you see the file **PT1H.json**.</span></span> <span data-ttu-id="e0535-186">경로에 대한 설명은 다음 메모를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-186">See the following note for explanation of the path.</span></span>
6.  <span data-ttu-id="e0535-187">각 blob **PT1H.json**은 특정 CDN 끝점 또는 사용자 지정 도메인에 대해 1시간의 분석 로그를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-187">Each blob **PT1H.json** represents the analytics logs for one hour for a specific CDN endpoint or its custom domain.</span></span>
7.  <span data-ttu-id="e0535-188">이 JSON 파일 내용의 스키마는 핵심 분석 로그의 스키마 섹션에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-188">The schema of the contents of this JSON file is described in the section Schema of the Core Analytics Logs</span></span>


> [!NOTE]
> <span data-ttu-id="e0535-189">**Blob 경로 형식**</span><span class="sxs-lookup"><span data-stu-id="e0535-189">**Blob path format**</span></span>
> 
> <span data-ttu-id="e0535-190">핵심 분석 로그에는 1시간마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-190">Core Analytics logs are generated every hour.</span></span> <span data-ttu-id="e0535-191">1시간 동안의 모든 데이터는 수집된 후 단일 Azure Blob 내에 JSON 페이로드로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-191">All data for an hour are collected and stored inside a single Azure Blob as a JSON payload.</span></span> <span data-ttu-id="e0535-192">이 Azure Blob에 대한 경로는 계층 구조처럼 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-192">The path to this Azure Blob appears as if there is a hierarchical structure.</span></span> <span data-ttu-id="e0535-193">저장소 탐색기 도구는 '/'를 디렉터리 구분 기호로 해석하므로 편의를 위해 계층으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-193">This is because the Storage explorer tool interprets '/' as a directory separator and shows the hierarchy for convenience.</span></span> <span data-ttu-id="e0535-194">실제로는 전체 경로에 blob 이름만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-194">Actually, the whole path just represents the blob name.</span></span> <span data-ttu-id="e0535-195">이 blob 이름은 다음 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-195">This name of the blob follows the following naming convention</span></span>   
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

<span data-ttu-id="e0535-196">**필드 설명:**</span><span class="sxs-lookup"><span data-stu-id="e0535-196">**Description of fields:**</span></span>

|<span data-ttu-id="e0535-197">값</span><span class="sxs-lookup"><span data-stu-id="e0535-197">value</span></span>|<span data-ttu-id="e0535-198">description</span><span class="sxs-lookup"><span data-stu-id="e0535-198">description</span></span>|
|-------|---------|
|<span data-ttu-id="e0535-199">구독 ID</span><span class="sxs-lookup"><span data-stu-id="e0535-199">Subscription ID</span></span>    |<span data-ttu-id="e0535-200">Azure 구독의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-200">ID of the Azure Subscription.</span></span> <span data-ttu-id="e0535-201">이것은 GUID 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-201">This is in the Guid format.</span></span>|
|<span data-ttu-id="e0535-202">리소스</span><span class="sxs-lookup"><span data-stu-id="e0535-202">Resource</span></span> |<span data-ttu-id="e0535-203">그룹 이름   CDN 리소스가 속한 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-203">Group Name   Name of the resource group to which the CDN resources belong.</span></span>|
|<span data-ttu-id="e0535-204">프로필 이름</span><span class="sxs-lookup"><span data-stu-id="e0535-204">Profile Name</span></span> |<span data-ttu-id="e0535-205">CDN 프로필의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-205">Name of the CDN Profile</span></span>|
|<span data-ttu-id="e0535-206">끝점 이름</span><span class="sxs-lookup"><span data-stu-id="e0535-206">Endpoint Name</span></span> |<span data-ttu-id="e0535-207">CDN 끝점의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-207">Name of the CDN Endpoint</span></span>|
|<span data-ttu-id="e0535-208">Year</span><span class="sxs-lookup"><span data-stu-id="e0535-208">Year</span></span>|  <span data-ttu-id="e0535-209">4자리 연도 표시(예: 2017)입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-209">4-digit representation of the year for example, 2017</span></span>|
|<span data-ttu-id="e0535-210">월</span><span class="sxs-lookup"><span data-stu-id="e0535-210">Month</span></span>| <span data-ttu-id="e0535-211">2자리 월 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-211">2-digit representation of the month number.</span></span> <span data-ttu-id="e0535-212">01=1월 ... 12=12월</span><span class="sxs-lookup"><span data-stu-id="e0535-212">01=January ... 12=December</span></span>|
|<span data-ttu-id="e0535-213">일</span><span class="sxs-lookup"><span data-stu-id="e0535-213">Day</span></span>|   <span data-ttu-id="e0535-214">2자리 일 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-214">2 digit representation of the day of the month</span></span>|
|<span data-ttu-id="e0535-215">PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e0535-215">PT1H.json</span></span>| <span data-ttu-id="e0535-216">분석 데이터가 저장되는 실제 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-216">Actual JSON file where the analytics data is stored</span></span>|

### <a name="exporting-the-core-analytics-data-to-a-csv-file"></a><span data-ttu-id="e0535-217">핵심 분석 데이터를 CSV 파일로 내보내기</span><span class="sxs-lookup"><span data-stu-id="e0535-217">Exporting the Core Analytics Data to a CSV File</span></span>

<span data-ttu-id="e0535-218">핵심 분석에 쉽게 액세스할 수 있도록 하기 위해 도구에 샘플 코드를 제공하고 있습니다. 이를 사용하여 JSON 파일을 쉼표로 구분된 일반 파일 형식으로 다운로드한 다음, 쉽게 차트를 만들거나 기타 집계를 수행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-218">To make it easy to access the Core Analytics, we provide a sample code for a tool, which allows downloading the JSON files into a flat comma-separated file format, which can be used to easily create charts or other aggregations.</span></span>

<span data-ttu-id="e0535-219">이 도구를 사용하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-219">Here is how you can use the tool:</span></span>

1.  <span data-ttu-id="e0535-220">Github 링크 [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ) 방문</span><span class="sxs-lookup"><span data-stu-id="e0535-220">Visit the github link: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv ](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )</span></span>
2.  <span data-ttu-id="e0535-221">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="e0535-221">Download the code</span></span>
3.  <span data-ttu-id="e0535-222">지침에 따라 컴파일 및 구성</span><span class="sxs-lookup"><span data-stu-id="e0535-222">Follow instructions to compile and configure</span></span>
4.  <span data-ttu-id="e0535-223">도구 실행</span><span class="sxs-lookup"><span data-stu-id="e0535-223">Run the tool</span></span>
5.  <span data-ttu-id="e0535-224">결과 CSV 파일은 분석 데이터를 간단한 평면 계층으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-224">Resulting CSV file shows the analytics data in a simple flat hierarchy.</span></span>

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a><span data-ttu-id="e0535-225">OMS Log Analytics 리포지토리에서 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="e0535-225">Consuming diagnostics logs from an OMS Log Analytics repository</span></span>
<span data-ttu-id="e0535-226">Log Analytics는 클라우드 및 온-프레미스 환경을 모니터링하여 해당 가용성 및 성능을 유지하는 OMS(Operations Management Suite)의 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-226">Log Analytics is a service in Operations Management Suite (OMS) that monitors your cloud and on-premises environments to maintain their availability and performance.</span></span> <span data-ttu-id="e0535-227">이 서비스는 클라우드 및 온-프레미스 환경에서 리소스에 의해 생성되고 여러 원본에 대한 분석을 제공하는 다른 모니터링 도구에서 생성된 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-227">It collects data generated by resources in your cloud and on-premises environments and from other monitoring tools to provide analysis across multiple sources.</span></span> 

<span data-ttu-id="e0535-228">Log Analytics를 사용하려면 앞서 이 문서에서 논의한 Azure OMS Log Analytics 리포지토리에 대한 [로깅을 사용하도록 설정](#enable-logging-with-azure-storage)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-228">To use Log Analytics, you must [enable logging](#enable-logging-with-azure-storage) to the Azure OMS Log Analytics repository, which is discussed earlier in this article.</span></span>

### <a name="using-the-oms-repository"></a><span data-ttu-id="e0535-229">OMS 리포지토리 사용</span><span class="sxs-lookup"><span data-stu-id="e0535-229">Using the OMS Repository</span></span>

 <span data-ttu-id="e0535-230">다음 다이어그램에서는 리포지토리의 입력 및 출력의 아키텍처를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-230">The following diagram shows the architecture of the inputs and outputs of the repository:</span></span>

![OMS Log Analytics 리포지토리](./media/cdn-diagnostics-log/12_Repo-overview.png)

<span data-ttu-id="e0535-232">*그림 3 - Log Analytics 리포지토리*</span><span class="sxs-lookup"><span data-stu-id="e0535-232">*Figure 3 - Log Analytics Repository*</span></span>

<span data-ttu-id="e0535-233">관리 솔루션을 사용하여 다양한 방법으로 데이터를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-233">You can display the data in a variety of ways by using Management Solutions.</span></span> <span data-ttu-id="e0535-234">[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)에서 관리 솔루션을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-234">You can obtain Management Solutions from the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).</span></span>

<span data-ttu-id="e0535-235">각 솔루션의 맨 아래에서 **지금 신청** 링크를 클릭하여 Azure Marketplace에서 관리 솔루션을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-235">You can install management solutions from Azure marketplace by clicking the **Get it now** link at the bottom of each solution.</span></span>

### <a name="adding-an-oms-cdn-management-solution"></a><span data-ttu-id="e0535-236">OMS CDN 관리 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="e0535-236">Adding an OMS CDN Management Solution</span></span>

<span data-ttu-id="e0535-237">관리 솔루션을 추가하려면 아래 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="e0535-237">Follow these steps to add a Management Solution:</span></span>

1.   <span data-ttu-id="e0535-238">Azure Portal에 아직 로그인하지 않은 경우 Azure 구독을 사용하여 로그인한 후 대시보드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-238">If you haven't already done so, sign in to the Azure portal using your Azure subscription and go to your Dashboard.</span></span>
    <span data-ttu-id="e0535-239">![Azure 대시보드](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="e0535-239">![Azure Dashboard](./media/cdn-diagnostics-log/13_Azure-dashboard.png)</span></span>

2. <span data-ttu-id="e0535-240">**Marketplace** 아래 **새로 만들기** 블레이드에서 **모니터링 + 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-240">In the **New** blade under **Marketplace**, select **Monitoring + management**.</span></span>

    ![마켓플레이스](./media/cdn-diagnostics-log/14_Marketplace.png)

3. <span data-ttu-id="e0535-242">**모니터링 + 관리** 블레이드에서 **모두 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-242">In the **Monitoring + management** blade, click **See all**.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/15_See-all.png)

4.  <span data-ttu-id="e0535-244">검색 상자에서 CDN을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-244">Search for CDN in the search box.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/16_Search-for.png)

5.  <span data-ttu-id="e0535-246">**Azure CDN 핵심 분석**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-246">Select **Azure CDN Core Analytics**.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  <span data-ttu-id="e0535-248">**만들기**를 클릭하면 새 OMS 작업 영역을 만들거나 기존 작업 영역을 사용할지 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-248">After clicking **Create**, you will be asked to create a new OMS workspace or use an existing one.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  <span data-ttu-id="e0535-250">이전에 만든 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-250">Select the workspace you created before.</span></span> <span data-ttu-id="e0535-251">그런 다음 자동화 계정을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-251">You then need to add an automation account.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/19_Add-automation.png)

8. <span data-ttu-id="e0535-253">다음 화면은 사용자가 작성해야 하는 자동화 계정 양식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-253">The following screen shows the automation account form you must fill out.</span></span> 

    ![모두 표시](./media/cdn-diagnostics-log/20_Automation.png)

9. <span data-ttu-id="e0535-255">자동화 계정을 만든 후 솔루션을 추가할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-255">Once you have created the automation account, you are ready to add your solution.</span></span> <span data-ttu-id="e0535-256">**만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-256">Click the **Create** button.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/21_Ready.png)

10. <span data-ttu-id="e0535-258">이제 솔루션이 작업 영역에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-258">Your solution has now been added to your workspace.</span></span> <span data-ttu-id="e0535-259">Azure Portal 대시보드로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-259">Go back to your Azure portal Dashboard.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/22_Dashboard.png)

    <span data-ttu-id="e0535-261">만든 Log Analytics 작업 영역을 클릭하여 작업 영역으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-261">Click the Log Analytics workspace you created to go to your workspace.</span></span> 

11. <span data-ttu-id="e0535-262">**OMS 포털** 타일을 클릭하여 OMS 포털에서 새 솔루션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-262">Click the **OMS Portal** tile to see your new solution in the OMS portal.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/23_workspace.png)

12. <span data-ttu-id="e0535-264">이제 OMS 포털은 다음 화면과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-264">Your OMS portal should now look like the following screen:</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/24_OMS-solution.png)

    <span data-ttu-id="e0535-266">데이터에 대한 여러 뷰를 보려면 타일 중 하나를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-266">Click one of the tiles to see several views into your data.</span></span>

    ![모두 표시](./media/cdn-diagnostics-log/25_Interior-view.png)

    <span data-ttu-id="e0535-268">왼쪽 또는 오른쪽으로 스크롤하여 데이터에 대한 개별 뷰를 나타내는 추가 타일을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-268">You can scroll left or right to see further tiles representing individual views into the data.</span></span> 

    <span data-ttu-id="e0535-269">타일 중 하나를 클릭하면 데이터에 대한 더 자세한 정보가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-269">Clicking one of the tiles gives you more details about your data.</span></span>

     ![모두 표시](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a><span data-ttu-id="e0535-271">제품 및 가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="e0535-271">Offers and pricing tiers</span></span>

<span data-ttu-id="e0535-272">[여기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)에서 OMS 관리 솔루션에 대한 제품 및 가격 책정 계층을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-272">You can see offers and pricing tiers for OMS management solutions [here](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).</span></span>

### <a name="customizing-views"></a><span data-ttu-id="e0535-273">뷰 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="e0535-273">Customizing views</span></span>

<span data-ttu-id="e0535-274">**뷰 디자이너**를 사용하여 데이터에 대한 뷰를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-274">You can customize the view into your data by using the **View Designer**.</span></span> <span data-ttu-id="e0535-275">OMS 작업 영역으로 이동한 후 **뷰 디자이너** 타일을 클릭하여 디자인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-275">Go to your OMS workspace and begin designing by clicking the **View Designer** tile.</span></span>

![뷰 디자이너](./media/cdn-diagnostics-log/27_Designer.png)

<span data-ttu-id="e0535-277">왼쪽에서 차트 유형을 끌어서 놓고 왼쪽에 분석하려는 데이터 세부 정보를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-277">You can drag and drop types of charts from the left and fill in the data details you want to analyze on the left.</span></span>

![뷰 디자이너](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a><span data-ttu-id="e0535-279">로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="e0535-279">Log data delays</span></span>

<span data-ttu-id="e0535-280">Verizon 로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="e0535-280">Verizon log data delays</span></span> | <span data-ttu-id="e0535-281">Akamai 로그 데이터 지연</span><span class="sxs-lookup"><span data-stu-id="e0535-281">Akamai log data delays</span></span>
--- | ---
<span data-ttu-id="e0535-282">Verizon 로그 데이터는 1시간 지연되고, 끝점 전파가 완료된 후 나타날 때까지 최대 2시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-282">Verizon log data is 1 hour delayed, and take up to 2 hours to start appearing after endpoint propagation completion.</span></span> | <span data-ttu-id="e0535-283">Akamai 로그 데이터는 24시간 지연되고, 24시간 이전에 만들어진 경우 나타날 때까지 최대 2시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-283">Akamai log data is 24 hours delayed, and takes up to 2 hours to start appearing if it was created more than 24 hours ago.</span></span> <span data-ttu-id="e0535-284">최근에 만든 경우 로그가 나타날 때까지 최대 25시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-284">If it was recently created, it can take up to 25 hours for the logs to start appearing.</span></span>

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a><span data-ttu-id="e0535-285">CDN 핵심 분석에 대한 진단 로그 유형</span><span class="sxs-lookup"><span data-stu-id="e0535-285">Diagnostic log types for CDN Core Analytics</span></span>

<span data-ttu-id="e0535-286">현재는 CDN POP/Edge에서 볼 수 있는 HTTP 응답 통계 및 송신 통계를 보여 주는 메트릭이 포함된 핵심 분석 로그만 제공하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-286">We currently offer only Core Analytics logs, which contain metrics showing HTTP response statistics and egress statistics as seen from the CDN POPs/edges.</span></span>

### <a name="core-analytics-metrics-details"></a><span data-ttu-id="e0535-287">핵심 분석 메트릭 정보</span><span class="sxs-lookup"><span data-stu-id="e0535-287">Core Analytics Metrics Details</span></span>
<span data-ttu-id="e0535-288">다음 표는 핵심 분석 로그에서 사용할 수 있는 메트릭의 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-288">The following table shows a list of metrics available in the Core Analytics logs.</span></span> <span data-ttu-id="e0535-289">모든 공급자의 모든 메트릭을 사용할 수 있는 것은 아니지만 이러한 차이는 미미합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-289">Not all metrics are available from all providers, although such differences are minimal.</span></span> <span data-ttu-id="e0535-290">아래 표에는 지정된 메트릭을 공급자에서 사용할 수 있는지 여부도 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-290">The following table also shows if a given metric is available from a provider.</span></span> <span data-ttu-id="e0535-291">메트릭은 트래픽이 있는 해당 CDN 끝점에 대해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-291">Please note that the metrics are available for only those CDN endpoints that have traffic on them.</span></span>


|<span data-ttu-id="e0535-292">메트릭</span><span class="sxs-lookup"><span data-stu-id="e0535-292">Metric</span></span>                     | <span data-ttu-id="e0535-293">설명</span><span class="sxs-lookup"><span data-stu-id="e0535-293">Description</span></span>   | <span data-ttu-id="e0535-294">Verizon</span><span class="sxs-lookup"><span data-stu-id="e0535-294">Verizon</span></span>  | <span data-ttu-id="e0535-295">Akamai</span><span class="sxs-lookup"><span data-stu-id="e0535-295">Akamai</span></span> 
|---------------------------|---------------|---|---|
| <span data-ttu-id="e0535-296">RequestCountTotal</span><span class="sxs-lookup"><span data-stu-id="e0535-296">RequestCountTotal</span></span>         |<span data-ttu-id="e0535-297">이 기간 동안의 요청 적중의 총 수</span><span class="sxs-lookup"><span data-stu-id="e0535-297">Total number of request hits during this period</span></span>| <span data-ttu-id="e0535-298">예</span><span class="sxs-lookup"><span data-stu-id="e0535-298">Yes</span></span>  |<span data-ttu-id="e0535-299">예</span><span class="sxs-lookup"><span data-stu-id="e0535-299">Yes</span></span>   |
| <span data-ttu-id="e0535-300">RequestCountHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e0535-300">RequestCountHttpStatus2xx</span></span> |<span data-ttu-id="e0535-301">2xx HTTP 코드(예: 200, 202)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-301">Count of all requests that resulted in a 2xx HTTP code (e.g. 200, 202)</span></span>              | <span data-ttu-id="e0535-302">예</span><span class="sxs-lookup"><span data-stu-id="e0535-302">Yes</span></span>  |<span data-ttu-id="e0535-303">예</span><span class="sxs-lookup"><span data-stu-id="e0535-303">Yes</span></span>   |
| <span data-ttu-id="e0535-304">RequestCountHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e0535-304">RequestCountHttpStatus3xx</span></span> | <span data-ttu-id="e0535-305">3xx HTTP 코드(예: 300, 302)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-305">Count of all requests that resulted in a 3xx HTTP code (e.g. 300, 302)</span></span>              | <span data-ttu-id="e0535-306">예</span><span class="sxs-lookup"><span data-stu-id="e0535-306">Yes</span></span>  |<span data-ttu-id="e0535-307">예</span><span class="sxs-lookup"><span data-stu-id="e0535-307">Yes</span></span>   |
| <span data-ttu-id="e0535-308">RequestCountHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e0535-308">RequestCountHttpStatus4xx</span></span> |<span data-ttu-id="e0535-309">4xx HTTP 코드(예: 400, 404)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-309">Count of all requests that resulted in a 4xx HTTP code (e.g. 400, 404)</span></span>               | <span data-ttu-id="e0535-310">예</span><span class="sxs-lookup"><span data-stu-id="e0535-310">Yes</span></span>   |<span data-ttu-id="e0535-311">예</span><span class="sxs-lookup"><span data-stu-id="e0535-311">Yes</span></span>   |
| <span data-ttu-id="e0535-312">RequestCountHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e0535-312">RequestCountHttpStatus5xx</span></span> | <span data-ttu-id="e0535-313">5xx HTTP 코드(예: 500, 504)를 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-313">Count of all requests that resulted in a 5xx HTTP code (e.g. 500, 504)</span></span>              | <span data-ttu-id="e0535-314">예</span><span class="sxs-lookup"><span data-stu-id="e0535-314">Yes</span></span>  |<span data-ttu-id="e0535-315">예</span><span class="sxs-lookup"><span data-stu-id="e0535-315">Yes</span></span>   |
| <span data-ttu-id="e0535-316">RequestCountHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e0535-316">RequestCountHttpStatusOthers</span></span> |  <span data-ttu-id="e0535-317">다른 모든 HTTP 코드의 수(2xx-5xx 이외)</span><span class="sxs-lookup"><span data-stu-id="e0535-317">Count of all other HTTP codes (outside of 2xx-5xx)</span></span> | <span data-ttu-id="e0535-318">예</span><span class="sxs-lookup"><span data-stu-id="e0535-318">Yes</span></span>  |<span data-ttu-id="e0535-319">예</span><span class="sxs-lookup"><span data-stu-id="e0535-319">Yes</span></span>   |
| <span data-ttu-id="e0535-320">RequestCountHttpStatus200</span><span class="sxs-lookup"><span data-stu-id="e0535-320">RequestCountHttpStatus200</span></span> | <span data-ttu-id="e0535-321">200 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-321">Count of all requests that resulted in a 200 HTTP code response</span></span>              |<span data-ttu-id="e0535-322">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-322">No</span></span>   |<span data-ttu-id="e0535-323">예</span><span class="sxs-lookup"><span data-stu-id="e0535-323">Yes</span></span>   |
| <span data-ttu-id="e0535-324">RequestCountHttpStatus206</span><span class="sxs-lookup"><span data-stu-id="e0535-324">RequestCountHttpStatus206</span></span> | <span data-ttu-id="e0535-325">206 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-325">Count of all requests that resulted in a 206 HTTP code response</span></span>              |<span data-ttu-id="e0535-326">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-326">No</span></span>   |<span data-ttu-id="e0535-327">예</span><span class="sxs-lookup"><span data-stu-id="e0535-327">Yes</span></span>   |
| <span data-ttu-id="e0535-328">RequestCountHttpStatus302</span><span class="sxs-lookup"><span data-stu-id="e0535-328">RequestCountHttpStatus302</span></span> | <span data-ttu-id="e0535-329">302 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-329">Count of all requests that resulted in a 302 HTTP code response</span></span>              |<span data-ttu-id="e0535-330">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-330">No</span></span>   |<span data-ttu-id="e0535-331">예</span><span class="sxs-lookup"><span data-stu-id="e0535-331">Yes</span></span>   |
| <span data-ttu-id="e0535-332">RequestCountHttpStatus304</span><span class="sxs-lookup"><span data-stu-id="e0535-332">RequestCountHttpStatus304</span></span> |  <span data-ttu-id="e0535-333">304 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-333">Count of all requests that resulted in a 304 HTTP code response</span></span>             |<span data-ttu-id="e0535-334">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-334">No</span></span>   |<span data-ttu-id="e0535-335">예</span><span class="sxs-lookup"><span data-stu-id="e0535-335">Yes</span></span>   |
| <span data-ttu-id="e0535-336">RequestCountHttpStatus404</span><span class="sxs-lookup"><span data-stu-id="e0535-336">RequestCountHttpStatus404</span></span> | <span data-ttu-id="e0535-337">404 HTTP 코드 응답을 생성한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-337">Count of all requests that resulted in a 404 HTTP code response</span></span>              |<span data-ttu-id="e0535-338">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-338">No</span></span>   |<span data-ttu-id="e0535-339">예</span><span class="sxs-lookup"><span data-stu-id="e0535-339">Yes</span></span>   |
| <span data-ttu-id="e0535-340">RequestCountCacheHit</span><span class="sxs-lookup"><span data-stu-id="e0535-340">RequestCountCacheHit</span></span> |<span data-ttu-id="e0535-341">캐시 적중을 발생한 모든 요청의 수.</span><span class="sxs-lookup"><span data-stu-id="e0535-341">Count of all requests that resulted in a Cache Hit.</span></span> <span data-ttu-id="e0535-342">자산이 POP에서 클라이언트로 직접 제공되었음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-342">This means the asset was served directly from the POP to the Client.</span></span>               | <span data-ttu-id="e0535-343">예</span><span class="sxs-lookup"><span data-stu-id="e0535-343">Yes</span></span>  |<span data-ttu-id="e0535-344">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-344">No</span></span>   |
| <span data-ttu-id="e0535-345">RequestCountCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e0535-345">RequestCountCacheMiss</span></span> | <span data-ttu-id="e0535-346">캐시 누락을 발생한 모든 요청의 수.</span><span class="sxs-lookup"><span data-stu-id="e0535-346">Count of all requests that resulted in a Cache Miss.</span></span> <span data-ttu-id="e0535-347">자산을 클라이언트에 가장 가까운 POP에서 찾을 수 없으므로 원래 시작점에서 검색되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-347">This means the asset was not found on the POP closest to the client, and therefore was retrieved from the Origin.</span></span>              |<span data-ttu-id="e0535-348">예</span><span class="sxs-lookup"><span data-stu-id="e0535-348">Yes</span></span>   | <span data-ttu-id="e0535-349">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-349">No</span></span>  |
| <span data-ttu-id="e0535-350">RequestCountCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e0535-350">RequestCountCacheNoCache</span></span> | <span data-ttu-id="e0535-351">Edge의 사용자 구성 때문에 캐시되지 못한 자산에 대한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-351">Count of all requests to an asset that are prevented from being cached due to a user configuration on the edge.</span></span>              |<span data-ttu-id="e0535-352">예</span><span class="sxs-lookup"><span data-stu-id="e0535-352">Yes</span></span>   | <span data-ttu-id="e0535-353">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-353">No</span></span>  |
| <span data-ttu-id="e0535-354">RequestCountCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e0535-354">RequestCountCacheUncacheable</span></span> | <span data-ttu-id="e0535-355">자산의 Cache-Control 및 Expires 헤더에 의해 캐시되지 못하여 POP에서 또는 HTTP 클라이언트에 의해 캐시되지 않아야 함을 나타내는 자산에 대한 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-355">Count of all requests to assets that are prevented from being cached by the asset's Cache-Control and Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                |<span data-ttu-id="e0535-356">예</span><span class="sxs-lookup"><span data-stu-id="e0535-356">Yes</span></span>   |<span data-ttu-id="e0535-357">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-357">No</span></span>   |
| <span data-ttu-id="e0535-358">RequestCountCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e0535-358">RequestCountCacheOthers</span></span> | <span data-ttu-id="e0535-359">위에 포함되지 않는 캐시 상태를 갖는 모든 요청의 수</span><span class="sxs-lookup"><span data-stu-id="e0535-359">Count of all requests with cache status not covered by above.</span></span>              |<span data-ttu-id="e0535-360">예</span><span class="sxs-lookup"><span data-stu-id="e0535-360">Yes</span></span>   | <span data-ttu-id="e0535-361">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-361">No</span></span>  |
| <span data-ttu-id="e0535-362">EgressTotal</span><span class="sxs-lookup"><span data-stu-id="e0535-362">EgressTotal</span></span> | <span data-ttu-id="e0535-363">아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-363">Outbound data transfer in GB</span></span>              |<span data-ttu-id="e0535-364">예</span><span class="sxs-lookup"><span data-stu-id="e0535-364">Yes</span></span>   |<span data-ttu-id="e0535-365">예</span><span class="sxs-lookup"><span data-stu-id="e0535-365">Yes</span></span>   |
| <span data-ttu-id="e0535-366">EgressHttpStatus2xx</span><span class="sxs-lookup"><span data-stu-id="e0535-366">EgressHttpStatus2xx</span></span> | <span data-ttu-id="e0535-367">2xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송*(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-367">Outbound data transfer* for responses with 2xx HTTP status codes in GB</span></span>            |<span data-ttu-id="e0535-368">예</span><span class="sxs-lookup"><span data-stu-id="e0535-368">Yes</span></span>   |<span data-ttu-id="e0535-369">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-369">No</span></span>   |
| <span data-ttu-id="e0535-370">EgressHttpStatus3xx</span><span class="sxs-lookup"><span data-stu-id="e0535-370">EgressHttpStatus3xx</span></span> | <span data-ttu-id="e0535-371">3xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-371">Outbound data transfer for responses with 3xx HTTP status codes in GB</span></span>              |<span data-ttu-id="e0535-372">예</span><span class="sxs-lookup"><span data-stu-id="e0535-372">Yes</span></span>   |<span data-ttu-id="e0535-373">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-373">No</span></span>   |
| <span data-ttu-id="e0535-374">EgressHttpStatus4xx</span><span class="sxs-lookup"><span data-stu-id="e0535-374">EgressHttpStatus4xx</span></span> | <span data-ttu-id="e0535-375">4xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-375">Outbound data transfer for responses with 4xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e0535-376">예</span><span class="sxs-lookup"><span data-stu-id="e0535-376">Yes</span></span>   | <span data-ttu-id="e0535-377">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-377">No</span></span>  |
| <span data-ttu-id="e0535-378">EgressHttpStatus5xx</span><span class="sxs-lookup"><span data-stu-id="e0535-378">EgressHttpStatus5xx</span></span> | <span data-ttu-id="e0535-379">5xx HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-379">Outbound data transfer for responses with 5xx HTTP status codes in GB</span></span>               |<span data-ttu-id="e0535-380">예</span><span class="sxs-lookup"><span data-stu-id="e0535-380">Yes</span></span>   |  <span data-ttu-id="e0535-381">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-381">No</span></span> |
| <span data-ttu-id="e0535-382">EgressHttpStatusOthers</span><span class="sxs-lookup"><span data-stu-id="e0535-382">EgressHttpStatusOthers</span></span> | <span data-ttu-id="e0535-383">다른 HTTP 상태 코드를 나타내는 응답에 대한 아웃바운드 데이터 전송(GB)</span><span class="sxs-lookup"><span data-stu-id="e0535-383">Outbound data transfer for responses with other HTTP status codes in GB</span></span>                |<span data-ttu-id="e0535-384">예</span><span class="sxs-lookup"><span data-stu-id="e0535-384">Yes</span></span>   |<span data-ttu-id="e0535-385">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-385">No</span></span>   |
| <span data-ttu-id="e0535-386">EgressCacheHit</span><span class="sxs-lookup"><span data-stu-id="e0535-386">EgressCacheHit</span></span> |  <span data-ttu-id="e0535-387">CDN POP/Edge의 CDN 캐시에서 직접 전달된 응답에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e0535-387">Outbound data transfer for responses that were delivered directly from the CDN cache on the CDN POPs/Edges</span></span>  |<span data-ttu-id="e0535-388">예</span><span class="sxs-lookup"><span data-stu-id="e0535-388">Yes</span></span>   |  <span data-ttu-id="e0535-389">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-389">No</span></span> |
| <span data-ttu-id="e0535-390">EgressCacheMiss</span><span class="sxs-lookup"><span data-stu-id="e0535-390">EgressCacheMiss</span></span> | <span data-ttu-id="e0535-391">가장 가까운 POP 서버에 없으며 원본 서버에서 검색된 응답에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e0535-391">Outbound data transfer for responses that were not found on the nearest POP server, and retrieved from the origin server</span></span>              |<span data-ttu-id="e0535-392">예</span><span class="sxs-lookup"><span data-stu-id="e0535-392">Yes</span></span>   |  <span data-ttu-id="e0535-393">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-393">No</span></span> |
| <span data-ttu-id="e0535-394">EgressCacheNoCache</span><span class="sxs-lookup"><span data-stu-id="e0535-394">EgressCacheNoCache</span></span> | <span data-ttu-id="e0535-395">Edge의 사용자 구성 때문에 캐시되지 못한 자산에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e0535-395">Outbound data transfer for assets that are prevented from being cached due to a user configuration on the edge.</span></span>                |<span data-ttu-id="e0535-396">예</span><span class="sxs-lookup"><span data-stu-id="e0535-396">Yes</span></span>   |<span data-ttu-id="e0535-397">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-397">No</span></span>   |
| <span data-ttu-id="e0535-398">EgressCacheUncacheable</span><span class="sxs-lookup"><span data-stu-id="e0535-398">EgressCacheUncacheable</span></span> | <span data-ttu-id="e0535-399">자산의 Cache-Control 및/또는 Expires 헤더에 의해 캐시되지 못하여 POP에서 또는 HTTP 클라이언트에 의해 캐시되지 않아야 함을 나타내는 자산에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e0535-399">Outbound data transfer for assets that are prevented from being cached by the asset's Cache-Control and/or Expires headers, which indicate that it should not be cached on a POP or by the HTTP client</span></span>                    |<span data-ttu-id="e0535-400">예</span><span class="sxs-lookup"><span data-stu-id="e0535-400">Yes</span></span>   | <span data-ttu-id="e0535-401">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-401">No</span></span>  |
| <span data-ttu-id="e0535-402">EgressCacheOthers</span><span class="sxs-lookup"><span data-stu-id="e0535-402">EgressCacheOthers</span></span> |  <span data-ttu-id="e0535-403">다른 캐시 시나리오에 대한 아웃바운드 데이터 전송</span><span class="sxs-lookup"><span data-stu-id="e0535-403">Outbound data transfers for other cache scenarios.</span></span>             |<span data-ttu-id="e0535-404">예</span><span class="sxs-lookup"><span data-stu-id="e0535-404">Yes</span></span>   | <span data-ttu-id="e0535-405">아니요</span><span class="sxs-lookup"><span data-stu-id="e0535-405">No</span></span>  |

<span data-ttu-id="e0535-406">* 아웃바운드 데이터 전송은 CDN POP 서버에서 클라이언트로 전달되는 트래픽을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-406">*Outbound data transfer refers to traffic delivered from CDN POP servers to the client.</span></span>


### <a name="schema-of-the-core-analytics-logs"></a><span data-ttu-id="e0535-407">핵심 분석 로그의 스키마</span><span class="sxs-lookup"><span data-stu-id="e0535-407">Schema of the Core Analytics Logs</span></span> 

<span data-ttu-id="e0535-408">모든 로그는 JSON 형식으로 저장되며 각 항목에는 아래 스키마의 문자열 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-408">All logs are stored in JSON format and each entry has string fields following the below schema:</span></span>

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of the CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of the domain for which the statistics is reported>",
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

<span data-ttu-id="e0535-409">여기서 'time'은 통계가 보고되는 시간 범위의 시작 시간을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-409">Where the ‘time’ represents the start time of the hour boundary for which the statistics is reported.</span></span> <span data-ttu-id="e0535-410">CDN 공급자가 메트릭을 지원하지 않을 경우 double 또는 정수 값 대신 null 값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-410">When a metric is not supported by a CDN provider, instead of a double or integer value, there will be a null value.</span></span> <span data-ttu-id="e0535-411">이 null 값은 메트릭이 없음을 나타내며 값 0과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-411">This null value indicates the absence of a metric, and this is different from a 0 value.</span></span> <span data-ttu-id="e0535-412">이러한 메트릭 집합은 끝점에 구성된 도메인당 1개만 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-412">Also note that there will be one set of these metrics per domain configured on the endpoint.</span></span>

<span data-ttu-id="e0535-413">예제 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0535-413">Example properties below:</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="e0535-414">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="e0535-414">Additional resources</span></span>

* [<span data-ttu-id="e0535-415">Azure 진단 로그</span><span class="sxs-lookup"><span data-stu-id="e0535-415">Azure Diagnostic logs</span></span>](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [<span data-ttu-id="e0535-416">Azure CDN 보조 포털을 통한 핵심 분석</span><span class="sxs-lookup"><span data-stu-id="e0535-416">Core analytics via Azure CDN supplemental portal</span></span>](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [<span data-ttu-id="e0535-417">Azure OMS Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0535-417">Azure OMS Log Analytics</span></span>](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [<span data-ttu-id="e0535-418">Azure Log Analytics REST API</span><span class="sxs-lookup"><span data-stu-id="e0535-418">Azure Log Analytics REST API</span></span>](https://docs.microsoft.com/en-us/rest/api/loganalytics)







