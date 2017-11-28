---
title: "PowerShell을 사용하여 Azure Log Analytics로 Service Fabric 응용 프로그램 평가 | Microsoft Docs"
description: "PowerShell을 사용하여 Log Analytics의 Service Fabric 솔루션을 사용하여 Service Fabric 응용 프로그램, 마이크로 서비스, 노드 및 클러스터의 위험과 상태를 평가할 수 있습니다."
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="6c25d-103">PowerShell로 Azure Service Fabric 응용 프로그램 및 마이크로 서비스 평가</span><span class="sxs-lookup"><span data-stu-id="6c25d-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c25d-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="6c25d-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="6c25d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c25d-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Service Fabric 기호](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="6c25d-107">이 문서에서는 Log Analytics에서 Service Fabric 솔루션을 사용하여 Service Fabric 클러스터 간의 문제를 파악 및 해결하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="6c25d-108">Service Fabric 노드의 수행 방법 및 응용 프로그램 및 마이크로 서비스의 실행 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="6c25d-109">Service Fabric 솔루션은 Azure WAD 테이블에서 이 데이터를 수집하여 Service Fabric VM에서 Azure 진단 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="6c25d-110">그런 다음 Log Analytics는 다음 Service Fabric 프레임워크 이벤트를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="6c25d-111">**Reliable Service 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6c25d-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="6c25d-112">**행위자 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6c25d-112">**Actor Events**</span></span>
- <span data-ttu-id="6c25d-113">**작업 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6c25d-113">**Operational Events**</span></span>
- <span data-ttu-id="6c25d-114">**사용자 지정 ETW 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6c25d-114">**Custom ETW events**</span></span>

<span data-ttu-id="6c25d-115">Service Fabric 솔루션 대시보드는 Service Fabric 환경에서 주목할 만한 문제와 관련 이벤트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="6c25d-116">솔루션 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="6c25d-116">Installing and configuring the solution</span></span>
<span data-ttu-id="6c25d-117">다음 세 가지 간단한 단계에 따라 솔루션을 설치 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="6c25d-118">저장소 계정을 비롯하여 모든 클러스터 리소스를 만드는 데 사용한 Azure 구독을 작업 영역과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="6c25d-119">Log Analytics 작업 영역을 만드는 방법에 대한 자세한 내용은 [Log Analytics 시작](log-analytics-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c25d-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="6c25d-120">Service Fabric 로그를 수집하고 보기 위해 Log Analytics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="6c25d-121">작업 영역에서 Service Fabric 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="6c25d-122">Service Fabric 로그를 수집하고 보기 위해 Log Analytics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="6c25d-123">이 섹션에서는 Service Fabric 로그를 검색하도록 Log Analytics를 구성하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="6c25d-124">로그를 통해 OMS 포털을 사용하여 클러스터나 해당 클러스터에서 실행 중인 응용 프로그램 및 서비스의 문제를 보고 분석하며 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6c25d-125">저장소 테이블에 대한 로그를 업로드하도록 Azure 진단 확장을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="6c25d-126">테이블은 Log Analytics에서 찾는 것과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="6c25d-127">자세한 내용은 [Azure 진단을 사용하여 로그를 수집하는 방법](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c25d-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="6c25d-128">이 문서의 구성 설정 예에서는 필요한 저장소 테이블 이름을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="6c25d-129">클러스터에 진단이 설정되었고 로그를 저장소 계정에 업로드하는 중이면 다음 단계는 이러한 로그를 수집하도록 Log Analytics를 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="6c25d-130">**deploy.ps1**을 실행하여 구성 업데이트를 적용하려면 먼저 새 EventSources에 대해 항목을 추가하도록 **template.json** 파일의 **EtwEventSourceProviderConfiguration** 섹션을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="6c25d-131">업로드를 위한 테이블은 (ETWEventTable)과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="6c25d-132">지금은 Log Analytics가 *WADETWEventTable* 테이블에서 응용 프로그램 ETW 이벤트만 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="6c25d-133">다음 도구는 이 문서의 일부 작업을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="6c25d-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c25d-134">Azure PowerShell</span></span>
* [<span data-ttu-id="6c25d-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6c25d-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="6c25d-136">클러스터 로그를 표시하도록 Log Analytics 작업 영역 구성</span><span class="sxs-lookup"><span data-stu-id="6c25d-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="6c25d-137">Log Analytics 작업 영역을 만든 후 Azure 저장소 테이블에서 로그를 끌어오도록 작업 영역을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="6c25d-138">그런 후 다음 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="6c25d-139">저장소 계정의 Azure 테이블에서 읽어 오도록 Log Analytics 작업 영역을 구성한 후에는 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="6c25d-140">**모든 리소스**에서 Log Analytics 작업 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="6c25d-141">작업 영역에 연결된 저장소 계정 로그 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="6c25d-142">**저장소 계정 로그** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="6c25d-143">저장소 계정 로그 목록을 검토하여 저장소 계정이 올바른 작업 영역에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Storage 계정 로그](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="6c25d-145">Service Fabric 솔루션 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6c25d-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="6c25d-146">다음 스크립트를 사용하여 Log Analytics 작업 영역에 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="6c25d-147">Service Fabric 솔루션을 사용하도록 설정할 Log Analytics 작업 영역에 연결된 Azure 구독을 사용하여 PowerShell에서 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="6c25d-148">솔루션을 활성화한 후 Service Fabric 타일이 Log Analytics *개요* 페이지에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="6c25d-149">페이지는 지난 24시간 동안 발생했던 runAsync 오류 및 취소와 같은 주목할 만한 문제의 뷰를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Service Fabric 타일](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="6c25d-151">Service Fabric 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="6c25d-151">View Service Fabric events</span></span>
<span data-ttu-id="6c25d-152">**Service Fabric** 타일을 클릭하여 Service Fabric 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="6c25d-153">대시보드는 뒤에 오는 테이블의 열을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="6c25d-154">각 열은 지정된 시간 범위에 대한 열의 기준과 일치하는 카운트별로 상위 10개의 이벤트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="6c25d-155">각 열의 오른쪽 아래쪽에 있는 **모두 보기**를 클릭하거나 열 제목을 클릭하여 전체 목록을 제공하는 로그 검색을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="6c25d-156">**Service Fabric 이벤트**</span><span class="sxs-lookup"><span data-stu-id="6c25d-156">**Service Fabric event**</span></span> | <span data-ttu-id="6c25d-157">**description**</span><span class="sxs-lookup"><span data-stu-id="6c25d-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="6c25d-158">주목할 만한 문제</span><span class="sxs-lookup"><span data-stu-id="6c25d-158">Notable Issues</span></span> | <span data-ttu-id="6c25d-159">RunAsyncFailures, RunAsynCancellations 및 노드 다운을 포함하는 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="6c25d-160">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="6c25d-160">Operational Events</span></span> | <span data-ttu-id="6c25d-161">응용 프로그램 업그레이드 및 배포를 포함하는 주목할 만한 작업 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="6c25d-162">Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="6c25d-162">Reliable Service Events</span></span> | <span data-ttu-id="6c25d-163">Runasyncinvocations를 포함하는 주목할 만한 Reliable Service 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="6c25d-164">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="6c25d-164">Actor Events</span></span> | <span data-ttu-id="6c25d-165">마이크로 서비스에서 생성된 주목할 만한 행위자 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="6c25d-166">이벤트는 행위자 메서드, 행위자 활성화 및 비활성화 등에 의해 throw된 예외를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="6c25d-167">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="6c25d-167">Application Events</span></span> | <span data-ttu-id="6c25d-168">응용 프로그램으로 생성된 모든 사용자 지정 ETW 이벤트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-168">Displays all custom ETW events generated by your applications.</span></span> |

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="6c25d-171">다음 표에서는 데이터 수집 방법 및 Service Fabric에 대해 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="6c25d-172">플랫폼</span><span class="sxs-lookup"><span data-stu-id="6c25d-172">platform</span></span> | <span data-ttu-id="6c25d-173">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="6c25d-173">Direct Agent</span></span> | <span data-ttu-id="6c25d-174">Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="6c25d-174">Operations Manager agent</span></span> | <span data-ttu-id="6c25d-175">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="6c25d-175">Azure Storage</span></span> | <span data-ttu-id="6c25d-176">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="6c25d-176">Operations Manager required?</span></span> | <span data-ttu-id="6c25d-177">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="6c25d-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="6c25d-178">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="6c25d-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6c25d-179">Windows</span><span class="sxs-lookup"><span data-stu-id="6c25d-179">Windows</span></span> |  |  | <span data-ttu-id="6c25d-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6c25d-180">&#8226;</span></span> |  |  |<span data-ttu-id="6c25d-181">10분</span><span class="sxs-lookup"><span data-stu-id="6c25d-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="6c25d-182">이벤트의 범위를 대시보드 위쪽에 있는 **지난 7일 기준의 데이터**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="6c25d-183">최근 7일, 1일 또는 6시간 내에 생성된 이벤트를 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="6c25d-184">또는 **사용자 지정**을 선택하고 사용자 지정 날짜 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="6c25d-185">Service Fabric 및 Log Analytics 구성 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6c25d-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="6c25d-186">Log Analytics에서 이벤트 데이터를 볼 수 없어 Log Analytics 구성을 확인해야 하는 경우에는 다음 스크립트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="6c25d-187">다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-187">It performs the following actions:</span></span>

1. <span data-ttu-id="6c25d-188">Service Fabric 진단 구성 읽기</span><span class="sxs-lookup"><span data-stu-id="6c25d-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="6c25d-189">테이블에 기록된 데이터 확인</span><span class="sxs-lookup"><span data-stu-id="6c25d-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="6c25d-190">Log Analytics가 테이블에서 읽도록 구성되어 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="6c25d-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="6c25d-191">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c25d-191">Next steps</span></span>
* <span data-ttu-id="6c25d-192">[Log Analytics의 로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 Service Fabric 이벤트 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c25d-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
