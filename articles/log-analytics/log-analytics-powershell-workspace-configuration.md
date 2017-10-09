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
# <a name="manage-log-analytics-using-powershell"></a>PowerShell을 사용하여 Log Analytics 관리
Hello를 사용할 수 있습니다 [로그 분석 PowerShell cmdlet](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform 명령줄에서 또는 스크립트의 일부로 로그 분석에 대 한 다양 한 기능입니다.  PowerShell로 수행할 수 있는 하는 hello 작업의 예입니다.

* 작업 영역 만들기
* 솔루션 추가 또는 제거
* 저장된 검색 가져오기 및 내보내기
* 컴퓨터 그룹 만들기
* Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정
* Linux 및 Windows 컴퓨터에서 성능 카운터 수집
* Linux 컴퓨터의 syslog에서 이벤트 수집 
* Windows 이벤트 로그에서 이벤트 수집
* 사용자 지정 이벤트 로그 수집
* Hello 로그 분석 에이전트 tooan Azure 가상 컴퓨터를 추가 합니다.
* Azure 진단을 사용 하 여 수집 된 로그 분석 tooindex 데이터 구성

이 문서에서는 PowerShell에서 수행할 수 있는 hello 함수 중 일부를 보여 주는 두 개의 코드 예제를 제공 합니다.  Toohello 참조할 수 있습니다 [로그 분석 PowerShell cmdlet 참조](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 다른 함수에 대 한 합니다.

> [!NOTE]
> 로그 분석이 이전에 hello cmdlet에 사용 되는 hello 이름을이 Operational Insights는 호출 합니다.
> 
> 

## <a name="prerequisites"></a>필수 조건
이 예제에서는 버전 2.3.0 또는 hello AzureRm.OperationalInsights 모듈의 나중에 작동합니다.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Log Analytics 작업 영역 만들기 및 구성
hello 다음 스크립트 예제에서는 하는 방법:

1. 작업 영역 만들기
2. 목록 hello 사용 가능한 솔루션
3. 추가 솔루션 toohello 작업 영역
4. 저장된 검색 가져오기
5. 저장된 검색 내보내기
6. 컴퓨터 그룹 만들기
7. Hello Windows 에이전트가 설치 된 컴퓨터에서 IIS 로그의 컬렉션을 사용 하도록 설정
8. Linux 컴퓨터에서 논리 디스크 성능 카운터 수집(사용된 Inode 비율, 사용 가능한 MB, 사용된 공간 비율, 초당 디스크 전송, 초당 디스크 읽기, 초당 디스크 쓰기)
9. Linux 컴퓨터에서 syslog 이벤트 수집
10. Windows 컴퓨터에서 hello 응용 프로그램 이벤트 로그에서에서 오류 및 경고 이벤트를 수집 합니다.
11. Windows 컴퓨터에서 사용 가능한 메모리(MB) 성능 카운터 수집
12. 사용자 지정 로그 수집 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>로그 분석 tooindex Azure 진단 구성
Azure 리소스를 에이전트 없는 모니터링 hello 리소스 toohave Azure 진단을 사용 하도록 설정 하 고 구성 되어 toowrite tooa 로그 분석 작업 영역을 필요 합니다. 이 방법은 데이터를 보내는 tooLog 분석 직접 tooa 저장소 계정 작성 된 데이터 toobe 필요 하지 않습니다. 지원되는 리소스는 다음과 같습니다.

| 리소스 종류 | 로그 | 메트릭 |
| --- | --- | --- |
| 응용 프로그램 게이트웨이    | 예 | 예 |
| 자동화 계정     | 예 | |
| 배치 계정          | 예 | 예 |
| Data Lake Analytics     | 예 | | 
| Data Lake Store         | 예 | |
| 탄력적인 SQL 풀        |     | 예 |
| 이벤트 허브 네임스페이스     |     | 예 |
| IoT Hub                |     | 예 |
| 키 자격 증명 모음               | 예 | |
| Load Balancer          | 예 | |
| Logic Apps              | 예 | 예 |
| 네트워크 보안 그룹 | 예 | |
| Redis 캐시             |     | 예 |
| Search 서비스         | 예 | 예 |
| 서비스 버스 네임스페이스   |     | 예 |
| SQL(v12)               |     | 예 |
| 웹 사이트               |     | 예 |
| 웹 서버 팜        |     | 예 |

너무 hello 사용 가능한 메트릭 hello 세부 정보를 참조[지원 되는 Azure 모니터로 메트릭](../monitoring-and-diagnostics/monitoring-supported-metrics.md)합니다.

너무 hello hello 사용 가능한 로그의 세부 정보를 참조[진단 로그에 대 한 서비스 및 스키마 지원](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md)합니다.

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Hello 앞에 서로 다른 구독에 있는 리소스의 cmdlet toocollect 로그를 사용할 수 있습니다. hello cmdlet 없으므로 수 toowork 구독에서 제공 하는 중 로그를 만드는 두 hello 리소스의 hello id 및 hello 작업 영역 hello 로그 전송 됩니다.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>로그 분석 tooindex 저장소에서 Azure 진단 구성
toocollect 로그 데이터의 경우 클래식 클라우드 서비스 또는 서비스 패브릭 클러스터의 실행 중인 인스턴스 내에서 toofirst 쓰기 hello 데이터 tooAzure 저장소가 필요 합니다. 로그 분석은 다음 hello 저장소 계정에서 toocollect hello 로그를 구성 합니다. 지원되는 리소스는 다음과 같습니다.

* 기존 Cloud Services(웹 및 작업자 역할)
* Service Fabric 클러스터

hello 방법을 예제와 다음에:

1. Hello 기존 저장소 계정 및 로그 분석은 데이터를 색인 위치 나열
2. 저장소 계정에서 구성 tooread 만들기
3. 추가 위치에서 구성 tooindex 데이터를 새로 만들어진 hello를 업데이트 합니다.
4. 새로 만든 hello 구성 삭제

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

Hello 앞에 다른 구독의 저장소 계정에서 스크립트 toocollect 로그를 사용할 수 있습니다. hello 스크립트에서는 수 toowork 구독 전반에 걸쳐 이므로 hello 저장소 계정 리소스 id 및 해당 액세스 키를 제공 하는입니다. Hello 액세스 키를 변경 하면 tooupdate hello 저장소 통찰력 toohave hello 새 키가 필요 합니다.


## <a name="next-steps"></a>다음 단계
* [Log Analytics PowerShell Cmdlet 검토](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) 를 참조하세요.

