---
title: "PowerShell을 사용하여 Log Analytics 작업 영역 만들기 및 구성 | Microsoft Docs"
description: "Log Analytics는 온-프레미스 또는 클라우드 인프라의 서버에서 데이터를 사용합니다. Azure 진단에 의해 생성된 경우에 Azure 저장소에서 컴퓨터 데이터를 수집할 수 있습니다."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="f1481-104">PowerShell을 사용하여 Log Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="f1481-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="f1481-105">[Log Analytics PowerShell cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx)을 사용하여 명령줄에서 또는 스크립트의 일부로 Log Analytics의 다양한 기능을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="f1481-106">PowerShell을 사용하여 수행할 수 있는 작업의 예:</span><span class="sxs-lookup"><span data-stu-id="f1481-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="f1481-107">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="f1481-107">Create a workspace</span></span>
* <span data-ttu-id="f1481-108">솔루션 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="f1481-108">Add or remove a solution</span></span>
* <span data-ttu-id="f1481-109">저장된 검색 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="f1481-109">Import and export saved searches</span></span>
* <span data-ttu-id="f1481-110">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f1481-110">Create a computer group</span></span>
* <span data-ttu-id="f1481-111">Windows 에이전트가 설치된 컴퓨터에서 IIS 로그 수집 활성화</span><span class="sxs-lookup"><span data-stu-id="f1481-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="f1481-112">Linux 및 Windows 컴퓨터에서 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="f1481-113">Linux 컴퓨터의 syslog에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="f1481-114">Windows 이벤트 로그에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="f1481-115">사용자 지정 이벤트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-115">Collect custom event logs</span></span>
* <span data-ttu-id="f1481-116">Azure 가상 컴퓨터에 Log Analytics 에이전트 추가</span><span class="sxs-lookup"><span data-stu-id="f1481-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="f1481-117">Azure 진단을 사용하여 수집된 데이터를 인덱싱하도록 Log Analytics 구성</span><span class="sxs-lookup"><span data-stu-id="f1481-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="f1481-118">이 문서에서는 PowerShell에서 수행할 수 있는 몇 가지 기능을 보여 주는 두 가지 코드 샘플을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="f1481-119">다른 기능에 대해서는 [Log Analytics PowerShell Cmdlet 참조](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="f1481-120">Log Analytics는 이전에 Operational Insights라고 했기 때문에 cmdlet에서는 Operational Insights라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f1481-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f1481-121">Prerequisites</span></span>
<span data-ttu-id="f1481-122">이 예제는 AzureRm.OperationalInsights 모듈 버전 2.3.0 이상에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="f1481-123">Log Analytics 작업 영역 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="f1481-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="f1481-124">다음 스크립트 샘플에서는 다음 작업의 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="f1481-125">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="f1481-125">Create a workspace</span></span>
2. <span data-ttu-id="f1481-126">사용 가능한 솔루션 나열</span><span class="sxs-lookup"><span data-stu-id="f1481-126">List the available solutions</span></span>
3. <span data-ttu-id="f1481-127">작업 영역에 솔루션 추가</span><span class="sxs-lookup"><span data-stu-id="f1481-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="f1481-128">저장된 검색 가져오기</span><span class="sxs-lookup"><span data-stu-id="f1481-128">Import saved searches</span></span>
5. <span data-ttu-id="f1481-129">저장된 검색 내보내기</span><span class="sxs-lookup"><span data-stu-id="f1481-129">Export saved searches</span></span>
6. <span data-ttu-id="f1481-130">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="f1481-130">Create a computer group</span></span>
7. <span data-ttu-id="f1481-131">Windows 에이전트가 설치된 컴퓨터에서 IIS 로그 수집 활성화</span><span class="sxs-lookup"><span data-stu-id="f1481-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="f1481-132">Linux 컴퓨터에서 논리 디스크 성능 카운터 수집(사용된 Inode 비율, 사용 가능한 MB, 사용된 공간 비율, 초당 디스크 전송, 초당 디스크 읽기, 초당 디스크 쓰기)</span><span class="sxs-lookup"><span data-stu-id="f1481-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="f1481-133">Linux 컴퓨터에서 syslog 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="f1481-134">Windows 컴퓨터에서 응용 프로그램 이벤트 로그의 오류 및 경고 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="f1481-135">Windows 컴퓨터에서 사용 가능한 메모리(MB) 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="f1481-136">사용자 지정 로그 수집</span><span class="sxs-lookup"><span data-stu-id="f1481-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log to collect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up to 5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="f1481-137">Azure 진단을 인덱싱하도록 Log Analytics 구성</span><span class="sxs-lookup"><span data-stu-id="f1481-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="f1481-138">에이전트 없이 Azure 리소스를 모니터링할 경우 리소스가 Azure 진단을 사용할 수 있어야 하며 Log Analytics 작업 영역에 쓰도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="f1481-139">이러한 방식은 데이터를 Log Analytics에 바로 보내며 데이터를 저장소 계정에 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="f1481-140">지원되는 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-140">Supported resources include:</span></span>

| <span data-ttu-id="f1481-141">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="f1481-141">Resource Type</span></span> | <span data-ttu-id="f1481-142">로그</span><span class="sxs-lookup"><span data-stu-id="f1481-142">Logs</span></span> | <span data-ttu-id="f1481-143">메트릭</span><span class="sxs-lookup"><span data-stu-id="f1481-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1481-144">응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="f1481-144">Application Gateways</span></span>    | <span data-ttu-id="f1481-145">예</span><span class="sxs-lookup"><span data-stu-id="f1481-145">Yes</span></span> | <span data-ttu-id="f1481-146">예</span><span class="sxs-lookup"><span data-stu-id="f1481-146">Yes</span></span> |
| <span data-ttu-id="f1481-147">자동화 계정</span><span class="sxs-lookup"><span data-stu-id="f1481-147">Automation accounts</span></span>     | <span data-ttu-id="f1481-148">예</span><span class="sxs-lookup"><span data-stu-id="f1481-148">Yes</span></span> | |
| <span data-ttu-id="f1481-149">배치 계정</span><span class="sxs-lookup"><span data-stu-id="f1481-149">Batch accounts</span></span>          | <span data-ttu-id="f1481-150">예</span><span class="sxs-lookup"><span data-stu-id="f1481-150">Yes</span></span> | <span data-ttu-id="f1481-151">예</span><span class="sxs-lookup"><span data-stu-id="f1481-151">Yes</span></span> |
| <span data-ttu-id="f1481-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f1481-152">Data Lake analytics</span></span>     | <span data-ttu-id="f1481-153">예</span><span class="sxs-lookup"><span data-stu-id="f1481-153">Yes</span></span> | | 
| <span data-ttu-id="f1481-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f1481-154">Data Lake store</span></span>         | <span data-ttu-id="f1481-155">예</span><span class="sxs-lookup"><span data-stu-id="f1481-155">Yes</span></span> | |
| <span data-ttu-id="f1481-156">탄력적인 SQL 풀</span><span class="sxs-lookup"><span data-stu-id="f1481-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="f1481-157">예</span><span class="sxs-lookup"><span data-stu-id="f1481-157">Yes</span></span> |
| <span data-ttu-id="f1481-158">이벤트 허브 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="f1481-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="f1481-159">예</span><span class="sxs-lookup"><span data-stu-id="f1481-159">Yes</span></span> |
| <span data-ttu-id="f1481-160">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="f1481-160">IoT Hubs</span></span>                |     | <span data-ttu-id="f1481-161">예</span><span class="sxs-lookup"><span data-stu-id="f1481-161">Yes</span></span> |
| <span data-ttu-id="f1481-162">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="f1481-162">Key Vault</span></span>               | <span data-ttu-id="f1481-163">예</span><span class="sxs-lookup"><span data-stu-id="f1481-163">Yes</span></span> | |
| <span data-ttu-id="f1481-164">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="f1481-164">Load Balancers</span></span>          | <span data-ttu-id="f1481-165">예</span><span class="sxs-lookup"><span data-stu-id="f1481-165">Yes</span></span> | |
| <span data-ttu-id="f1481-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="f1481-166">Logic Apps</span></span>              | <span data-ttu-id="f1481-167">예</span><span class="sxs-lookup"><span data-stu-id="f1481-167">Yes</span></span> | <span data-ttu-id="f1481-168">예</span><span class="sxs-lookup"><span data-stu-id="f1481-168">Yes</span></span> |
| <span data-ttu-id="f1481-169">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="f1481-169">Network Security Groups</span></span> | <span data-ttu-id="f1481-170">예</span><span class="sxs-lookup"><span data-stu-id="f1481-170">Yes</span></span> | |
| <span data-ttu-id="f1481-171">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="f1481-171">Redis Cache</span></span>             |     | <span data-ttu-id="f1481-172">예</span><span class="sxs-lookup"><span data-stu-id="f1481-172">Yes</span></span> |
| <span data-ttu-id="f1481-173">Search 서비스</span><span class="sxs-lookup"><span data-stu-id="f1481-173">Search services</span></span>         | <span data-ttu-id="f1481-174">예</span><span class="sxs-lookup"><span data-stu-id="f1481-174">Yes</span></span> | <span data-ttu-id="f1481-175">예</span><span class="sxs-lookup"><span data-stu-id="f1481-175">Yes</span></span> |
| <span data-ttu-id="f1481-176">서비스 버스 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="f1481-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="f1481-177">예</span><span class="sxs-lookup"><span data-stu-id="f1481-177">Yes</span></span> |
| <span data-ttu-id="f1481-178">SQL(v12)</span><span class="sxs-lookup"><span data-stu-id="f1481-178">SQL (v12)</span></span>               |     | <span data-ttu-id="f1481-179">예</span><span class="sxs-lookup"><span data-stu-id="f1481-179">Yes</span></span> |
| <span data-ttu-id="f1481-180">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="f1481-180">Web Sites</span></span>               |     | <span data-ttu-id="f1481-181">예</span><span class="sxs-lookup"><span data-stu-id="f1481-181">Yes</span></span> |
| <span data-ttu-id="f1481-182">웹 서버 팜</span><span class="sxs-lookup"><span data-stu-id="f1481-182">Web Server farms</span></span>        |     | <span data-ttu-id="f1481-183">예</span><span class="sxs-lookup"><span data-stu-id="f1481-183">Yes</span></span> |

<span data-ttu-id="f1481-184">사용 가능한 메트릭에 대한 자세한 내용은 [Azure Monitor에서 지원되는 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1481-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="f1481-185">사용 가능한 로그에 대한 자세한 내용은 [진단 로그에 지원되는 서비스 및 스키마](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1481-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="f1481-186">위의 cmdlet을 사용하여 다른 구독에 속하는 리소스에서 로그를 수집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="f1481-187">리소스 생성 로그의 ID 및 로그를 보내는 작업 영역의 ID를 모두 제공하기 때문에 cmdlet은 구독 간에 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="f1481-188">저장소에서 Azure 진단을 인덱싱하도록 Log Analytics 구성</span><span class="sxs-lookup"><span data-stu-id="f1481-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="f1481-189">클래식 클라우드 서비스 또는 Service Fabric 클러스터의 실행 중인 인스턴스 내에서 로그 데이터를 수집하려면 먼저 Azure Storage에 데이터를 써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="f1481-190">그런 다음 저장소 계정에서 로그를 수집하도록 Log Analytics를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="f1481-191">지원되는 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-191">Supported resources include:</span></span>

* <span data-ttu-id="f1481-192">기존 Cloud Services(웹 및 작업자 역할)</span><span class="sxs-lookup"><span data-stu-id="f1481-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="f1481-193">Service Fabric 클러스터</span><span class="sxs-lookup"><span data-stu-id="f1481-193">Service fabric clusters</span></span>

<span data-ttu-id="f1481-194">아래 예제는 다음과 같은 작업의 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-194">The following example shows how to:</span></span>

1. <span data-ttu-id="f1481-195">Log Analytics가 다음 출처에서 오는 데이터를 인덱싱하는 기존 저장소 계정 및 위치 나열</span><span class="sxs-lookup"><span data-stu-id="f1481-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="f1481-196">저장소 계정에서 읽을 구성 만들기</span><span class="sxs-lookup"><span data-stu-id="f1481-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="f1481-197">새로 만든 구성을 추가 위치에서 오는 데이터를 인덱싱하도록 업데이트</span><span class="sxs-lookup"><span data-stu-id="f1481-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="f1481-198">새로 만든 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="f1481-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="f1481-199">위의 스크립트를 사용하여 다른 구독에 속하는 저장소 계정에서 로그를 수집할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="f1481-200">저장소 계정 리소스 ID와 해당 액세스 키를 제공하기 때문에 스크립트는 구독 간에 작업이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="f1481-201">액세스 키를 변경할 때 저장소 정보가 새 키를 갖도록 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1481-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f1481-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1481-202">Next steps</span></span>
* <span data-ttu-id="f1481-203">[Log Analytics PowerShell Cmdlet 검토](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1481-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

