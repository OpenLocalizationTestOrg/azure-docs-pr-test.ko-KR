---
title: "aaaUse PowerShell tooCreate 하 고 로그 분석 작업 영역 구성 | Microsoft Docs"
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
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="eeac0-104">PowerShell을 사용하여 Log Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="eeac0-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="eeac0-105">Hello를 사용할 수 있습니다 [로그 분석 PowerShell cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform 명령줄에서 또는 스크립트의 일부로 로그 분석에 대 한 다양 한 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="eeac0-106">PowerShell로 수행할 수 있는 하는 hello 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="eeac0-107">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="eeac0-107">Create a workspace</span></span>
* <span data-ttu-id="eeac0-108">솔루션 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="eeac0-108">Add or remove a solution</span></span>
* <span data-ttu-id="eeac0-109">저장된 검색 가져오기 및 내보내기</span><span class="sxs-lookup"><span data-stu-id="eeac0-109">Import and export saved searches</span></span>
* <span data-ttu-id="eeac0-110">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="eeac0-110">Create a computer group</span></span>
* <span data-ttu-id="eeac0-111">Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="eeac0-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="eeac0-112">Linux 및 Windows 컴퓨터에서 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="eeac0-113">Linux 컴퓨터의 syslog에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="eeac0-114">Windows 이벤트 로그에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="eeac0-115">사용자 지정 이벤트 로그 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-115">Collect custom event logs</span></span>
* <span data-ttu-id="eeac0-116">Hello 로그 분석 에이전트 tooan Azure 가상 컴퓨터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="eeac0-117">Azure 진단을 사용 하 여 수집 된 로그 분석 tooindex 데이터 구성</span><span class="sxs-lookup"><span data-stu-id="eeac0-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="eeac0-118">이 문서에서는 PowerShell에서 수행할 수 있는 hello 함수 중 일부를 보여 주는 두 개의 코드 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="eeac0-119">Toohello 참조할 수 있습니다 [로그 분석 PowerShell cmdlet 참조](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 다른 함수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="eeac0-120">로그 분석이 이전에 hello cmdlet에 사용 되는 hello 이름을이 Operational Insights는 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="eeac0-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="eeac0-121">Prerequisites</span></span>
<span data-ttu-id="eeac0-122">이 예제에서는 버전 2.3.0 또는 hello AzureRm.OperationalInsights 모듈의 나중에 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="eeac0-123">Log Analytics 작업 영역 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="eeac0-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="eeac0-124">hello 다음 스크립트 예제에서는 하는 방법:</span><span class="sxs-lookup"><span data-stu-id="eeac0-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="eeac0-125">작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="eeac0-125">Create a workspace</span></span>
2. <span data-ttu-id="eeac0-126">목록 hello 사용 가능한 솔루션</span><span class="sxs-lookup"><span data-stu-id="eeac0-126">List hello available solutions</span></span>
3. <span data-ttu-id="eeac0-127">추가 솔루션 toohello 작업 영역</span><span class="sxs-lookup"><span data-stu-id="eeac0-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="eeac0-128">저장된 검색 가져오기</span><span class="sxs-lookup"><span data-stu-id="eeac0-128">Import saved searches</span></span>
5. <span data-ttu-id="eeac0-129">저장된 검색 내보내기</span><span class="sxs-lookup"><span data-stu-id="eeac0-129">Export saved searches</span></span>
6. <span data-ttu-id="eeac0-130">컴퓨터 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="eeac0-130">Create a computer group</span></span>
7. <span data-ttu-id="eeac0-131">Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="eeac0-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="eeac0-132">Linux 컴퓨터에서 논리 디스크 성능 카운터 수집(사용된 Inode 비율, 사용 가능한 MB, 사용된 공간 비율, 초당 디스크 전송, 초당 디스크 읽기, 초당 디스크 쓰기)</span><span class="sxs-lookup"><span data-stu-id="eeac0-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="eeac0-133">Linux 컴퓨터에서 syslog 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="eeac0-134">Windows 컴퓨터에서 hello 응용 프로그램 이벤트 로그에서에서 오류 및 경고 이벤트를 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="eeac0-135">Windows 컴퓨터에서 사용 가능한 메모리(MB) 성능 카운터 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="eeac0-136">사용자 지정 로그 수집</span><span class="sxs-lookup"><span data-stu-id="eeac0-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
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

# Custom Log toocollect
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

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
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

# Create a computer group based on names (up too5000)
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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="eeac0-137">로그 분석 tooindex Azure 진단 구성</span><span class="sxs-lookup"><span data-stu-id="eeac0-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="eeac0-138">Azure 리소스를 에이전트 없는 모니터링 hello 리소스 toohave Azure 진단을 사용 하도록 설정 하 고 구성 되어 toowrite tooa 로그 분석 작업 영역을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="eeac0-139">이 방법은 데이터를 보내는 tooLog 분석 직접 tooa 저장소 계정 작성 된 데이터 toobe 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="eeac0-140">지원되는 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-140">Supported resources include:</span></span>

| <span data-ttu-id="eeac0-141">리소스 종류</span><span class="sxs-lookup"><span data-stu-id="eeac0-141">Resource Type</span></span> | <span data-ttu-id="eeac0-142">로그</span><span class="sxs-lookup"><span data-stu-id="eeac0-142">Logs</span></span> | <span data-ttu-id="eeac0-143">메트릭</span><span class="sxs-lookup"><span data-stu-id="eeac0-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="eeac0-144">응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="eeac0-144">Application Gateways</span></span>    | <span data-ttu-id="eeac0-145">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-145">Yes</span></span> | <span data-ttu-id="eeac0-146">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-146">Yes</span></span> |
| <span data-ttu-id="eeac0-147">자동화 계정</span><span class="sxs-lookup"><span data-stu-id="eeac0-147">Automation accounts</span></span>     | <span data-ttu-id="eeac0-148">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-148">Yes</span></span> | |
| <span data-ttu-id="eeac0-149">배치 계정</span><span class="sxs-lookup"><span data-stu-id="eeac0-149">Batch accounts</span></span>          | <span data-ttu-id="eeac0-150">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-150">Yes</span></span> | <span data-ttu-id="eeac0-151">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-151">Yes</span></span> |
| <span data-ttu-id="eeac0-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="eeac0-152">Data Lake analytics</span></span>     | <span data-ttu-id="eeac0-153">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-153">Yes</span></span> | | 
| <span data-ttu-id="eeac0-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="eeac0-154">Data Lake store</span></span>         | <span data-ttu-id="eeac0-155">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-155">Yes</span></span> | |
| <span data-ttu-id="eeac0-156">탄력적인 SQL 풀</span><span class="sxs-lookup"><span data-stu-id="eeac0-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="eeac0-157">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-157">Yes</span></span> |
| <span data-ttu-id="eeac0-158">이벤트 허브 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="eeac0-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="eeac0-159">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-159">Yes</span></span> |
| <span data-ttu-id="eeac0-160">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="eeac0-160">IoT Hubs</span></span>                |     | <span data-ttu-id="eeac0-161">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-161">Yes</span></span> |
| <span data-ttu-id="eeac0-162">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="eeac0-162">Key Vault</span></span>               | <span data-ttu-id="eeac0-163">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-163">Yes</span></span> | |
| <span data-ttu-id="eeac0-164">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="eeac0-164">Load Balancers</span></span>          | <span data-ttu-id="eeac0-165">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-165">Yes</span></span> | |
| <span data-ttu-id="eeac0-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="eeac0-166">Logic Apps</span></span>              | <span data-ttu-id="eeac0-167">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-167">Yes</span></span> | <span data-ttu-id="eeac0-168">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-168">Yes</span></span> |
| <span data-ttu-id="eeac0-169">네트워크 보안 그룹</span><span class="sxs-lookup"><span data-stu-id="eeac0-169">Network Security Groups</span></span> | <span data-ttu-id="eeac0-170">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-170">Yes</span></span> | |
| <span data-ttu-id="eeac0-171">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="eeac0-171">Redis Cache</span></span>             |     | <span data-ttu-id="eeac0-172">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-172">Yes</span></span> |
| <span data-ttu-id="eeac0-173">Search 서비스</span><span class="sxs-lookup"><span data-stu-id="eeac0-173">Search services</span></span>         | <span data-ttu-id="eeac0-174">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-174">Yes</span></span> | <span data-ttu-id="eeac0-175">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-175">Yes</span></span> |
| <span data-ttu-id="eeac0-176">서비스 버스 네임스페이스</span><span class="sxs-lookup"><span data-stu-id="eeac0-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="eeac0-177">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-177">Yes</span></span> |
| <span data-ttu-id="eeac0-178">SQL(v12)</span><span class="sxs-lookup"><span data-stu-id="eeac0-178">SQL (v12)</span></span>               |     | <span data-ttu-id="eeac0-179">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-179">Yes</span></span> |
| <span data-ttu-id="eeac0-180">웹 사이트</span><span class="sxs-lookup"><span data-stu-id="eeac0-180">Web Sites</span></span>               |     | <span data-ttu-id="eeac0-181">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-181">Yes</span></span> |
| <span data-ttu-id="eeac0-182">웹 서버 팜</span><span class="sxs-lookup"><span data-stu-id="eeac0-182">Web Server farms</span></span>        |     | <span data-ttu-id="eeac0-183">예</span><span class="sxs-lookup"><span data-stu-id="eeac0-183">Yes</span></span> |

<span data-ttu-id="eeac0-184">너무 hello 사용 가능한 메트릭 hello 세부 정보를 참조[지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="eeac0-185">너무 hello hello 사용 가능한 로그의 세부 정보를 참조[진단 로그에 대 한 서비스 및 스키마 지원](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="eeac0-186">Hello 앞에 서로 다른 구독에 있는 리소스의 cmdlet toocollect 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="eeac0-187">hello cmdlet 없으므로 수 toowork 구독에서 제공 하는 중 로그를 만드는 두 hello 리소스의 hello id 및 hello 작업 영역 hello 로그 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="eeac0-188">로그 분석 tooindex 저장소에서 Azure 진단 구성</span><span class="sxs-lookup"><span data-stu-id="eeac0-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="eeac0-189">toocollect 로그 데이터의 경우 클래식 클라우드 서비스 또는 서비스 패브릭 클러스터의 실행 중인 인스턴스 내에서 toofirst 쓰기 hello 데이터 tooAzure 저장소가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="eeac0-190">로그 분석은 다음 hello 저장소 계정에서 toocollect hello 로그를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="eeac0-191">지원되는 리소스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-191">Supported resources include:</span></span>

* <span data-ttu-id="eeac0-192">기존 Cloud Services(웹 및 작업자 역할)</span><span class="sxs-lookup"><span data-stu-id="eeac0-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="eeac0-193">Service Fabric 클러스터</span><span class="sxs-lookup"><span data-stu-id="eeac0-193">Service fabric clusters</span></span>

<span data-ttu-id="eeac0-194">hello 방법을 예제와 다음에:</span><span class="sxs-lookup"><span data-stu-id="eeac0-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="eeac0-195">Hello 기존 저장소 계정 및 로그 분석은 데이터를 색인 위치 나열</span><span class="sxs-lookup"><span data-stu-id="eeac0-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="eeac0-196">저장소 계정에서 구성 tooread 만들기</span><span class="sxs-lookup"><span data-stu-id="eeac0-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="eeac0-197">추가 위치에서 구성 tooindex 데이터를 새로 만들어진 hello를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="eeac0-198">새로 만든 hello 구성 삭제</span><span class="sxs-lookup"><span data-stu-id="eeac0-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="eeac0-199">Hello 앞에 다른 구독의 저장소 계정에서 스크립트 toocollect 로그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="eeac0-200">hello 스크립트에서는 수 toowork 구독 전반에 걸쳐 이므로 hello 저장소 계정 리소스 id 및 해당 액세스 키를 제공 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="eeac0-201">Hello 액세스 키를 변경 하면 tooupdate hello 저장소 통찰력 toohave hello 새 키가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeac0-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eeac0-202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eeac0-202">Next steps</span></span>
* <span data-ttu-id="eeac0-203">[Log Analytics PowerShell Cmdlet 검토](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eeac0-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

