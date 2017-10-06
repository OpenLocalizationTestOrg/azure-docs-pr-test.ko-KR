---
title: "Azure PowerShell을 사용 하 여 Azure Data Lake 분석 aaaManage | Microsoft Docs"
description: "Toomanage Data Lake 분석 계정, 데이터 원본 작업 하는 방법에 대해 알아봅니다 및 카탈로그 항목입니다. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure 데이터 레이크 분석 관리
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Toomanage Azure Data Lake 분석 계정, 데이터 원본 작업 하는 방법 및 Azure PowerShell을 사용 하 여 카탈로그 항목에 알아봅니다. 

## <a name="prerequisites"></a>필수 조건

Data Lake 분석 계정을 만들 때 tooknow가 필요 합니다.

* **구독 ID**: hello Azure 구독 ID는 Data Lake 분석 계정 상주 합니다.
* **리소스 그룹**: hello 이름 Data Lake 분석 계정이 포함 된 hello Azure 리소스 그룹입니다.
* **Data Lake 분석 계정 이름을**: hello 계정 이름은 소문자와 숫자만 포함 해야 합니다.
* **기본 Data Lake Store 계정**: 각 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 있습니다. 이러한 계정은 hello에 있어야 합니다. 동일한 위치입니다.
* **위치**: hello 위치가 Data Lake 분석 계정 예: "미국 동부 2" 또는 다른 위치를 지원 합니다. 지원되는 위치는 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/data-lake-analytics/)에서 확인할 수 있습니다.

이 자습서에서는 PowerShell 조각 hello 이러한 변수 toostore이이 정보를 사용

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>로그인

구독 ID를 사용하여 로그인합니다.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

구독 이름을 사용하여 로그인합니다.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

hello `Login-AzureRmAccount` cmdlet 항상 자격 증명을 묻습니다. Hello 다음 cmdlet을 사용 하 여 하 라는 메시지가 표시 되 고 방지할 수 있습니다.

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>계정 관리

### <a name="create-a-data-lake-analytics-account"></a>Data Lake 분석 계정 만들기

아직 없는 경우는 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse를 하나 만듭니다. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

모든 Data Lake Analytics 계정에는 로그를 저장하는 데 사용할 기본 Data Lake Store 계정이 필요합니다. 기존 계정을 다시 사용하거나 새 계정을 만들 수 있습니다. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

리소스 그룹 및 Data Lake Store 계정을 사용할 수 있게 되면 Data Lake Analytics 계정을 만듭니다.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>계정에 대한 정보 가져오기

계정에 대한 세부 정보를 가져옵니다.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

특정 Data Lake 분석 계정이 hello 존재 여부를 확인 합니다. hello cmdlet 중 하나를 반환 합니다. `True` 또는 `False`합니다.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

특정 데이터 레이크 저장소 계정이 hello 존재 여부를 확인 합니다. hello cmdlet 중 하나를 반환 합니다. `True` 또는 `False`합니다.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>계정 나열

Hello 현재 구독 내에서 목록 데이터 레이크 분석 계정.

```powershell
Get-AdlAnalyticsAccount
```

특정 리소스 그룹 내의 Data Lake Analytics 계정을 나열합니다.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>방화벽 규칙 관리

방화벽 규칙을 나열합니다.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

방화벽 규칙을 추가합니다.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

방화벽 규칙을 변경합니다.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

방화벽 규칙을 제거합니다.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Azure IP 주소를 허용합니다.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>데이터 원본 관리
현재 azure 데이터 레이크 분석 데이터 원본 hello를 지원 합니다.

* [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md)
* [Azure 저장소](../storage/common/storage-introduction.md)

분석 계정을 만들 때 데이터 레이크 저장소 계정 toobe hello 기본 데이터 소스를 지정 해야 합니다. hello 기본 데이터 레이크 저장소 계정이 사용 됩니다 toostore 작업 메타 데이터 및 작업에 대 한 감사 로그 합니다. Data Lake Analytics 계정을 만든 후 Data Lake Store 계정 및/또는 Azure 저장소 계정을 더 추가할 수 있습니다. 

### <a name="find-hello-default-data-lake-store-account"></a>Hello 기본 데이터 레이크 저장소 계정 찾기

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

데이터 원본 목록이 hello hello 하 여 필터링 하 여 hello 기본 데이터 레이크 저장소 계정을 찾을 수 있습니다 `IsDefault` 속성:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>데이터 원본 추가

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>데이터 원본 나열

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>U-SQL 작업 제출

### <a name="submit-a-string-as-a-u-sql-script"></a>문자열을 U-SQL 스크립트로 제출

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a>파일을 U-SQL 스크립트로 제출

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>계정에 작업 나열

### <a name="list-all-hello-jobs-in-hello-account"></a>Hello 계정에서 모든 hello 작업을 나열 합니다. 

hello 출력 hello 현재 실행 중인 작업 및 최근에 완료 된 이러한 작업을 포함 합니다.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>특정 수의 작업 나열

기본적으로 작업의 hello 목록이 정렬에 전송 되는 시간입니다. Hello 최근에 전송 하도록 작업을 맨 먼저 나타납니다. 기본적으로 180 일에 대 한 작업을 기억 하는 hello ADLA 계정 되지만 기본 리턴으로 hello Ge AdlJob cmdlet에만 첫 번째 500 hello 합니다. 사용 하지 않으려면-상위 매개 변수 toolist 특정 개수의 작업 합니다.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>작업 속성의 hello 값에 따라 작업 나열

Hello를 사용 하 여 `-State` 매개 변수입니다. 이러한 값을 결합할 수 있습니다.

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

사용 하 여 hello `-Result` 매개 변수 toodetect 종료 작업이 성공적으로 완료 합니다. 다음 값을 포함합니다.

* Cancelled
* 실패
* 없음
* Succeeded

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


hello `-Submitter` 매개 변수를 사용 하면 작업을 제출한 사람을 식별 합니다.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

hello `-SubmittedAfter` 는 tooa 시간 범위를 필터링 하는 데 유용 합니다.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>작업을 나열하기 위한 일반적인 시나리오


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a>작업 목록 필터링

현재 PowerShell 세션에 작업 목록이 있으면, 일반 PowerShell cmdlet toofilter hello 목록을 사용할 수 있습니다.

지난 24 시간 동안 hello에 제출 된 작업 toohello 작업 목록 필터

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

지난 24 시간 동안 hello에 종료 된 작업 toohello 작업의 목록 필터링

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

실행이 시작 된 작업 toohello 작업의 목록을 필터링 합니다. 컴파일 시 작업이 실패할 수 있습니다. 따라서 작업은 시작되지 않습니다. 실제로 실행을 시작 하 고 실패 하는 hello 하지 못했습니다 작업을 살펴보겠습니다.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>작업 목록 분석

사용 하 여 hello `Group-Object` cmdlet tooanalyze 작업 목록입니다.

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
분석을 수행할 때 유용한 tooadd 속성 toohello 작업 개체 toomake 필터링 및 그룹화 간단 수 있습니다. 다음 코드 조각 hello와 JobInfo a tooannotate 속성을 계산 하는 방법을 보여 줍니다.

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a>파이프라인 및 되풀이에 대한 정보 가져오기

사용 하 여 hello `Get-AdlJobPipeline` cmdlet toosee hello 파이프라인 정보에는 이전에 작업 제출 합니다.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

사용 하 여 hello `Get-AdlJobRecurrence` cmdlet toosee hello 되풀이 이전에 제출 된 작업에 대 한 정보입니다.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>작업 정보 가져오기

### <a name="get-job-status"></a>작업 상태 가져오기

특정 작업의 hello 상태를 가져옵니다.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Hello 작업 출력을 검사

Hello 작업이 종료 된 후에 폴더의 hello 파일을 나열 하 여 hello 출력 파일이 있는지를 확인 하십시오.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>실행 중인 작업 관리

### <a name="cancel-a-job"></a>작업 취소

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>작업 toofinish 때까지 대기

반복 하는 대신 `Get-AdlAnalyticsJob` hello 작업이 완료 될 때까지 사용할 수 있습니다 `Wait-AdlJob` cmdlet toowait 작업 tooend hello에 대 한 합니다.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>계산 정책 관리

### <a name="list-existing-compute-policies"></a>기존 계산 정책 나열

hello `Get-AdlAnalyticsComputePolicy` cmdlet Data Lake 분석 계정에 대 한 계산 정책에 대 한 정보를 검색 합니다.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>계산 정책 만들기

hello `New-AdlAnalyticsComputePolicy` cmdlet Data Lake 분석 계정에 대 한 새 계산 정책을 만듭니다. 이 예제에서는 집합 hello 최대 AUs 사용 가능한 toohello 사용자 too50 및 hello 최소 작업 우선 순위 too250 지정.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Hello 파일이 있는지 확인 합니다.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>업로드 및 다운로드

파일을 업로드합니다.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

전체 폴더를 재귀적으로 업로드합니다.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

파일을 다운로드합니다.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

전체 폴더를 재귀적으로 다운로드합니다.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Hello 업로드 또는 다운로드 프로세스, hello 사용 하 여 다시 hello cmdlet를 실행 하 여 tooresume hello 프로세스를 시작할 수 있습니다. ``-Resume`` 플래그입니다.

## <a name="manage-catalog-items"></a>카탈로그 항목 관리

hello U-SQL 카탈로그 이므로 toostructure 사용 되는 데이터와 코드 U-SQL 스크립트에서 공유할 수 있습니다. hello 카탈로그에서 Azure 데이터 레이크 데이터 가능한 최고 성능을 hello 수 있습니다. 자세한 내용은 [U-SQL 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.

### <a name="list-items-in-hello-u-sql-catalog"></a>Hello U-SQL 카탈로그에 있는 목록 항목

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

모든 hello ADLA 계정 데이터베이스에서 모든 hello 어셈블리를 나열 합니다.

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a>카탈로그 항목에 대한 세부 정보 가져오기

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>카탈로그에 자격 증명 만들기

U-SQL 데이터베이스 내에서 Azure에서 호스트되는 데이터베이스에 대한 자격 증명 개체를 만듭니다. 현재 U-SQL 자격 증명이 hello 유일한 형식 PowerShell을 통해 만들 수 있는 카탈로그 항목입니다.

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a>ADLA 계정에 대한 기본 정보 가져오기

지정 된 계정 이름, 코드 다음 hello hello 계정에 대 한 기본 정보를 조회

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a>Azure 작업

### <a name="get-details-of-azurerm-errors"></a>AzureRm 오류에 대한 세부 정보 가져오기

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>관리자로 실행 중인지 확인

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>TenantID 찾기

구독 이름에서

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

구독 ID에서

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

"contoso.com"과 같은 도메인 주소에서


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>모든 구독 및 테넌트 ID 나열

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>템플릿을 사용하여 Data Lake Analytics 계정 만들기

또한 PowerShell 스크립트 뒤 hello를 사용 하는 Azure 리소스 그룹 템플릿을 사용할 수 있습니다.

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](../azure-resource-manager/resource-group-template-deploy.md) 및 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.

**예제 템플릿**

Hello 텍스트도 다음 저장 한 `.json` 파일을 선택한 다음 앞에 PowerShell 스크립트 toouse hello 템플릿을 hello를 사용 합니다. 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a>다음 단계
* [Microsoft Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)
* [Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)을 사용하여 Data Lake Analytics 시작
* [Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)를 사용하여 Azure Data Lake Analytics 관리 
