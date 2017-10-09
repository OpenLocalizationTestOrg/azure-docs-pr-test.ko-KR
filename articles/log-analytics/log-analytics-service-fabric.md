---
title: "PowerShell을 사용 하는 Azure 로그 분석 서비스 패브릭 응용 프로그램 aaaAssess | Microsoft Docs"
description: "PowerShell tooassess hello 위험 및 서비스 패브릭 응용 프로그램, 마이크로 서비스, 노드 및 클러스터의 상태를 사용 하 여 로그 분석에서 hello 서비스 패브릭 솔루션을 사용할 수 있습니다."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="8f757-103">PowerShell로 Azure Service Fabric 응용 프로그램 및 마이크로 서비스 평가</span><span class="sxs-lookup"><span data-stu-id="8f757-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f757-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="8f757-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="8f757-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f757-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Service Fabric 기호](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="8f757-107">이 문서에서는 toouse hello 로그 분석 toohelp에서 서비스 패브릭 솔루션을 식별 하 고 서비스 패브릭 클러스터 전체에서 문제를 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="8f757-108">Service Fabric 노드의 수행 방법 및 응용 프로그램 및 마이크로 서비스의 실행 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="8f757-109">서비스 패브릭 솔루션 hello Azure WAD 테이블에서이 데이터를 수집 하 여 서비스 패브릭 Vm에서 Azure 진단 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="8f757-110">다음 로그 분석 서비스 패브릭 프레임 워크 이벤트 다음 hello를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="8f757-111">**Reliable Service 이벤트**</span><span class="sxs-lookup"><span data-stu-id="8f757-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="8f757-112">**행위자 이벤트**</span><span class="sxs-lookup"><span data-stu-id="8f757-112">**Actor Events**</span></span>
- <span data-ttu-id="8f757-113">**작업 이벤트**</span><span class="sxs-lookup"><span data-stu-id="8f757-113">**Operational Events**</span></span>
- <span data-ttu-id="8f757-114">**사용자 지정 ETW 이벤트**</span><span class="sxs-lookup"><span data-stu-id="8f757-114">**Custom ETW events**</span></span>

<span data-ttu-id="8f757-115">hello 서비스 패브릭 솔루션 대시보드 서비스 패브릭 환경에서 주목할 만한 문제 및 관련 이벤트를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="8f757-116">설치 하 고 hello 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="8f757-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="8f757-117">이러한 세 가지 간단한 단계 tooinstall를 수행 하 고 hello 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="8f757-118">Hello를 사용 하 여 toocreate 저장소 계정, 작업 영역을 포함 하 여 모든 클러스터 리소스를 Azure 구독에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="8f757-119">Log Analytics 작업 영역을 만드는 방법에 대한 자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f757-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="8f757-120">로그 분석 toocollect 구성 서비스 패브릭 로그를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f757-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="8f757-121">작업 영역에서 hello 서비스 패브릭 솔루션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="8f757-122">로그 분석 toocollect 구성 서비스 패브릭 로그를 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f757-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="8f757-123">이 섹션에서는 서비스 패브릭 tooconfigure 로그 분석 tooretrieve 기록 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="8f757-124">hello 로그 tooview 수 있도록 분석 및 클러스터 또는 hello 응용 프로그램 및 hello OMS 포털을 사용 하 여 해당 클러스터에서 서비스를 실행 하는 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8f757-125">저장소 테이블에 대 한 hello Azure 진단 확장 tooupload hello 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="8f757-126">로그 분석 찾고 hello 테이블 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="8f757-127">자세한 내용은 참조 [toocollect Azure 진단으로 기록 하는 방법을](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="8f757-128">hello 구성 설정은이 문서의 예제에서는 테이블 해야 하는 hello 저장소의 어떤 hello 이름을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="8f757-129">Hello 다음 단계는 tooconfigure 로그 분석 toocollect 진단 hello 클러스터에 설치 되어 tooa 저장소 계정 로그를 업로드 되 면 이러한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="8f757-130">Hello를 업데이트 **EtwEventSourceProviderConfiguration** hello 섹션인 **template.json** hello hello 구성을 적용 하기 전에 새 EventSources 하 여 업데이트에 대 한 tooadd 항목 파일 실행 **deploy.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="8f757-131">hello 테이블 업로드에 대 한 hello 동일 (ETWEventTable)으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="8f757-132">Hello 시점에서 로그 분석 읽을 수만 응용 프로그램 ETW 이벤트 hello에서 *WADETWEventTable* 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="8f757-133">hello 다음 도구를 사용 하는 tooperform이이 섹션의 hello 작업의 일부:</span><span class="sxs-lookup"><span data-stu-id="8f757-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="8f757-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f757-134">Azure PowerShell</span></span>
* [<span data-ttu-id="8f757-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="8f757-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="8f757-136">로그 분석 작업 영역 tooshow hello 클러스터 로그 구성</span><span class="sxs-lookup"><span data-stu-id="8f757-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="8f757-137">로그 분석 작업 영역을 만든 후 hello hello Azure 저장소 테이블에서 toopull 로그를 작업 영역을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="8f757-138">그런 다음 PowerShell 스크립트 뒤 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="8f757-139">Hello 로그 분석 작업 영역 tooread hello Azure에서에서 구성 하 고 나면 저장소 계정의 테이블 toohello Azure 포털에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="8f757-140">Hello 로그 분석 작업 영역에서 선택 **모든 리소스**합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="8f757-141">저장소 계정 연결 된 로그 toohello 영역의 hello 번호가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="8f757-142">선택 hello **저장소 계정 로그** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="8f757-143">저장소 계정 로그 tooverify 저장소 계정이 연결 된 toohello 올바른 작업 공간 인지의 hello 목록을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Storage 계정 로그](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="8f757-145">Hello 서비스 패브릭 솔루션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8f757-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="8f757-146">다음 스크립트 tooadd hello 솔루션 tooyour 로그 분석 작업 영역 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="8f757-147">Hello에 tooenable hello 서비스 패브릭 솔루션을 원하는 hello 로그 분석 작업 영역에 연관 된 Azure 구독을 사용 하 여 PowerShell에서 hello 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="8f757-148">서비스 패브릭 타일 hello tooyour 로그 분석에 추가 됩니다 hello 솔루션을 사용 하도록 설정한 후 *개요* 페이지.</span><span class="sxs-lookup"><span data-stu-id="8f757-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="8f757-149">hello 페이지 주목할 만한 문제 runAsync 실패와 지난 24 시간 동안 발생 한 hello 취소 등의 뷰를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Service Fabric 타일](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="8f757-151">Service Fabric 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="8f757-151">View Service Fabric events</span></span>
<span data-ttu-id="8f757-152">Hello 클릭 **서비스 패브릭** tooopen hello 서비스 패브릭 대시보드 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="8f757-153">hello 대시보드 뒤에 오는 hello 표에 hello 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="8f757-154">각 열 개수를 비교 하 hello에 대 한 열의 기준을 시간 범위를 지정 하 여 hello 상위 10 개의 이벤트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="8f757-155">클릭 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** 각 열의 또는 hello 열 머리글을 클릭 하 여 hello 오른쪽 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="8f757-156">**Service Fabric 이벤트**</span><span class="sxs-lookup"><span data-stu-id="8f757-156">**Service Fabric event**</span></span> | <span data-ttu-id="8f757-157">**description**</span><span class="sxs-lookup"><span data-stu-id="8f757-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="8f757-158">주목할 만한 문제</span><span class="sxs-lookup"><span data-stu-id="8f757-158">Notable Issues</span></span> | <span data-ttu-id="8f757-159">RunAsyncFailures, RunAsynCancellations 및 노드 다운을 포함하는 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="8f757-160">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="8f757-160">Operational Events</span></span> | <span data-ttu-id="8f757-161">응용 프로그램 업그레이드 및 배포를 포함하는 주목할 만한 작업 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="8f757-162">Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="8f757-162">Reliable Service Events</span></span> | <span data-ttu-id="8f757-163">Runasyncinvocations를 포함하는 주목할 만한 Reliable Service 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="8f757-164">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="8f757-164">Actor Events</span></span> | <span data-ttu-id="8f757-165">마이크로 서비스에서 생성된 주목할 만한 행위자 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="8f757-166">이벤트는 행위자 메서드, 행위자 활성화 및 비활성화 등에 의해 throw된 예외를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="8f757-167">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="8f757-167">Application Events</span></span> | <span data-ttu-id="8f757-168">응용 프로그램으로 생성된 모든 사용자 지정 ETW 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-168">Displays all custom ETW events generated by your applications.</span></span> |

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="8f757-171">hello 다음 표에서 데이터 수집 방법과 서비스 패브릭에 대 한 데이터 수집 방법에 대 한 기타 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="8f757-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="8f757-172">플랫폼</span><span class="sxs-lookup"><span data-stu-id="8f757-172">platform</span></span> | <span data-ttu-id="8f757-173">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="8f757-173">Direct Agent</span></span> | <span data-ttu-id="8f757-174">Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="8f757-174">Operations Manager agent</span></span> | <span data-ttu-id="8f757-175">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="8f757-175">Azure Storage</span></span> | <span data-ttu-id="8f757-176">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="8f757-176">Operations Manager required?</span></span> | <span data-ttu-id="8f757-177">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="8f757-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="8f757-178">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="8f757-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8f757-179">Windows</span><span class="sxs-lookup"><span data-stu-id="8f757-179">Windows</span></span> |  |  | <span data-ttu-id="8f757-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="8f757-180">&#8226;</span></span> |  |  |<span data-ttu-id="8f757-181">10분</span><span class="sxs-lookup"><span data-stu-id="8f757-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="8f757-182">사용 하 여 이벤트의 hello 범위를 변경 **지난 7 일을 기준으로 데이터** hello hello 대시보드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="8f757-183">6 시간 또는 1 일, 지난 7 일 hello 내에서 생성 된 이벤트를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="8f757-184">선택할 수 있습니다 또는 **사용자 지정** toospecify 사용자 지정 날짜 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="8f757-185">Service Fabric 및 Log Analytics 구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8f757-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="8f757-186">필요한 경우 tooverify 로그 분석 구성에 도달 하 여 로그 분석에 없습니다 tooview 이벤트 데이터를 hello 다음 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="8f757-187">Hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="8f757-188">Service Fabric 진단 구성 읽기</span><span class="sxs-lookup"><span data-stu-id="8f757-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="8f757-189">Hello 테이블에 기록 된 데이터를 확인.</span><span class="sxs-lookup"><span data-stu-id="8f757-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="8f757-190">로그 분석 hello 테이블에서 구성 된 tooread 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="8f757-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f757-191">Next steps</span></span>
* <span data-ttu-id="8f757-192">사용 하 여 [로그 분석에서 로그 검색](log-analytics-log-searches.md) tooview 서비스 패브릭 이벤트 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f757-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
