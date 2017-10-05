---
title: "Azure PowerShell을 사용하여 Azure Data Lake Analytics 관리 | Microsoft Docs"
description: "Data Lake Analytics 계정, 데이터 원본, 작업 및 카탈로그 항목을 관리하는 방법을 알아봅니다. "
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
ms.openlocfilehash: 862e9551f1e129b7bba06651fbae94e337c92dcb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="2653b-103">Azure PowerShell을 사용하여 Azure 데이터 레이크 분석 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="2653b-104">Azure PowerShell을 사용하여 Azure Data Lake Analytics 계정, 데이터 원본, 작업 및 카탈로그 항목을 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2653b-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2653b-105">Prerequisites</span></span>

<span data-ttu-id="2653b-106">Data Lake Analytics 계정을 만들 때는 다음을 알아두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-106">When creating a Data Lake Analytics account, you need to know:</span></span>

* <span data-ttu-id="2653b-107">**구독 ID**: Data Lake Analytics 계정이 상주하는 Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-107">**Subscription ID**: The Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="2653b-108">**리소스 그룹**: Data Lake Analytics 계정이 포함된 Azure 리소스 그룹의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-108">**Resource group**: The name of the Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="2653b-109">**Data Lake Analytics 계정 이름**: 이 계정 이름은 소문자와 숫자만을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-109">**Data Lake Analytics account name**: The account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="2653b-110">**기본 Data Lake Store 계정**: 각 Data Lake Analytics 계정에는 기본 Data Lake Store 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="2653b-111">이러한 계정은 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-111">These accounts must be in the same location.</span></span>
* <span data-ttu-id="2653b-112">**위치**: Data Lake Analytics 계정의 위치입니다(예: "미국 동부 2" 또는 다른 지원되는 위치).</span><span class="sxs-lookup"><span data-stu-id="2653b-112">**Location**: The location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="2653b-113">지원되는 위치는 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/data-lake-analytics/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="2653b-114">이 자습서의 PowerShell 코드 조각은 이러한 변수를 사용하여 이 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-114">The PowerShell snippets in this tutorial use these variables to store this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="2653b-115">로그인</span><span class="sxs-lookup"><span data-stu-id="2653b-115">Log in</span></span>

<span data-ttu-id="2653b-116">구독 ID를 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="2653b-117">구독 이름을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="2653b-118">`Login-AzureRmAccount` cmdlet은 항상 자격 증명을 묻는 메시지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-118">The `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="2653b-119">다음 cmdlet을 사용하면 메시지가 표시되지 않게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-119">You can avoid being prompted by using the following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="2653b-120">계정 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="2653b-121">Data Lake 분석 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2653b-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="2653b-122">사용할 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)이 아직 없는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) to use, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="2653b-123">모든 Data Lake Analytics 계정에는 로그를 저장하는 데 사용할 기본 Data Lake Store 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="2653b-124">기존 계정을 다시 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="2653b-125">리소스 그룹 및 Data Lake Store 계정을 사용할 수 있게 되면 Data Lake Analytics 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="2653b-126">계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-126">Get information about an account</span></span>

<span data-ttu-id="2653b-127">계정에 대한 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="2653b-128">특정 Data Lake Analytics 계정의 존재 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-128">Check the existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="2653b-129">이 cmdlet은 `True` 또는 `False`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-129">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="2653b-130">특정 Data Lake Store 계정이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-130">Check the existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="2653b-131">이 cmdlet은 `True` 또는 `False`를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-131">The cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="2653b-132">계정 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-132">Listing accounts</span></span>

<span data-ttu-id="2653b-133">현재 구독 내의 Data Lake Analytics 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-133">List Data Lake Analytics accounts within the current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="2653b-134">특정 리소스 그룹 내의 Data Lake Analytics 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="2653b-135">방화벽 규칙 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-135">Managing firewall rules</span></span>

<span data-ttu-id="2653b-136">방화벽 규칙을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="2653b-137">방화벽 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="2653b-138">방화벽 규칙을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="2653b-139">방화벽 규칙을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="2653b-140">Azure IP 주소를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="2653b-141">데이터 원본 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-141">Managing data sources</span></span>
<span data-ttu-id="2653b-142">Azure Data Lake Analytics는 현재 다음 데이터 원본을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-142">Azure Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="2653b-143">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="2653b-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="2653b-144">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="2653b-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="2653b-145">Analytics 계정을 만들 때 Data Lake Store 계정이 기본 데이터 원본이 되도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-145">When you create an Analytics account, you must designate a Data Lake Store account to be the default data source.</span></span> <span data-ttu-id="2653b-146">기본 데이터 레이크 저장소 계정은 작업 메타데이터 및 작업 감사 로그를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-146">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="2653b-147">Data Lake Analytics 계정을 만든 후 Data Lake Store 계정 및/또는 Azure 저장소 계정을 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="2653b-148">기본 데이터 레이크 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="2653b-148">Find the default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="2653b-149">`IsDefault` 속성으로 데이터 원본 목록을 필터링하여 기본 Data Lake Store 계정을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-149">You can find the default Data Lake Store account by filtering the list of datasources by the `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="2653b-150">데이터 원본 추가</span><span class="sxs-lookup"><span data-stu-id="2653b-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="2653b-151">데이터 원본 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-151">List data sources</span></span>

```powershell
# List all the data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="2653b-152">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="2653b-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="2653b-153">문자열을 U-SQL 스크립트로 제출</span><span class="sxs-lookup"><span data-stu-id="2653b-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="2653b-154">파일을 U-SQL 스크립트로 제출</span><span class="sxs-lookup"><span data-stu-id="2653b-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="2653b-155">계정에 작업 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-155">List jobs in an account</span></span>

### <a name="list-all-the-jobs-in-the-account"></a><span data-ttu-id="2653b-156">계정에서 모든 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-156">List all the jobs in the account.</span></span> 

<span data-ttu-id="2653b-157">출력은 현재 실행 중인 작업 및 최근에 완료된 해당 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-157">The output includes the currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="2653b-158">특정 수의 작업 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-158">List a specific number of jobs</span></span>

<span data-ttu-id="2653b-159">기본적으로 작업 목록은 제출 시간을 기준으로 정렬됩니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-159">By default the list of jobs is sorted on submit time.</span></span> <span data-ttu-id="2653b-160">따라서 최근에 제출한 작업이 먼저 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-160">So the most recently submitted jobs appear first.</span></span> <span data-ttu-id="2653b-161">기본적으로 ADLA 계정에서는 180일 동안의 작업을 저장하지만 Ge-AdlJob cmdlet은 기본적으로 처음 500개 작업만 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-161">By default, The ADLA account remembers jobs for 180 days, but the Ge-AdlJob  cmdlet by default returns only the first 500.</span></span> <span data-ttu-id="2653b-162">특정 수의 작업을 나열하려면 -Top 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-162">Use -Top parameter to list a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-the-value-of-job-property"></a><span data-ttu-id="2653b-163">작업 속성 값을 기준으로 작업 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-163">List jobs based on the value of job property</span></span>

<span data-ttu-id="2653b-164">`-State` 매개 변수 사용.</span><span class="sxs-lookup"><span data-stu-id="2653b-164">Using the `-State` parameter.</span></span> <span data-ttu-id="2653b-165">이러한 값을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-165">You can combine any of these values:</span></span>

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
# List the running jobs
Get-AdlJob -Account $adla -State Running

# List the jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List the jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="2653b-166">`-Result` 매개 변수를 사용하여 종료된 작업이 성공적으로 완료되었는지 여부를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-166">Use the `-Result` parameter to detect whether ended jobs completed successfully.</span></span> <span data-ttu-id="2653b-167">다음 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-167">It has these values:</span></span>

* <span data-ttu-id="2653b-168">Cancelled</span><span class="sxs-lookup"><span data-stu-id="2653b-168">Cancelled</span></span>
* <span data-ttu-id="2653b-169">실패</span><span class="sxs-lookup"><span data-stu-id="2653b-169">Failed</span></span>
* <span data-ttu-id="2653b-170">없음</span><span class="sxs-lookup"><span data-stu-id="2653b-170">None</span></span>
* <span data-ttu-id="2653b-171">Succeeded</span><span class="sxs-lookup"><span data-stu-id="2653b-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="2653b-172">`-Submitter` 매개 변수를 사용하면 작업을 제출한 사람을 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-172">The `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="2653b-173">`-SubmittedAfter`는 시간 범위로 필터링하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-173">The `-SubmittedAfter` is useful in filtering to a time range.</span></span>


```powershell
# List  jobs submitted in the last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in the last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="2653b-174">작업을 나열하기 위한 일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="2653b-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in the last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within the past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="2653b-175">작업 목록 필터링</span><span class="sxs-lookup"><span data-stu-id="2653b-175">Filtering a list of jobs</span></span>

<span data-ttu-id="2653b-176">현재 PowerShell 세션에 작업 목록이 있으면,</span><span class="sxs-lookup"><span data-stu-id="2653b-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="2653b-177">일반 PowerShell cmdlet을 사용하여 목록을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-177">You can use normal PowerShell cmdlets to filter the list.</span></span>

<span data-ttu-id="2653b-178">지난 24시간 동안에 제출된 작업으로 작업 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-178">Filter a list of jobs to the jobs submitted in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="2653b-179">지난 24시간 동안에 종료된 작업으로 작업 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-179">Filter a list of jobs to the jobs that ended in the last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="2653b-180">실행이 시작된 작업으로 작업 목록을 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-180">Filter a list of jobs to the jobs that started running.</span></span> <span data-ttu-id="2653b-181">컴파일 시 작업이 실패할 수 있습니다. 따라서 작업은 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="2653b-182">실제로 실행이 시작되었지만 실패로 끝난 실패한 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-182">Let's look at the failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="2653b-183">작업 목록 분석</span><span class="sxs-lookup"><span data-stu-id="2653b-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="2653b-184">`Group-Object` cmdlet을 사용하여 작업 목록을 분석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-184">Use the `Group-Object` cmdlet to analyze a list of jobs.</span></span>

```
# Count the number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count the number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count the number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count the number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="2653b-185">분석을 수행할 때 Job 개체에 속성을 추가하여 필터링과 그룹화를 더 간단하게 만들면 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-185">When performing an analysis, it can be useful to add properties to the Job objects to make filtering and grouping simpler.</span></span> <span data-ttu-id="2653b-186">다음 코드 조각에서는 계산된 속성으로 JobInfo에 주석을 다는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-186">The following  snippet shows how to annotate a JobInfo with calculated properties.</span></span>

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

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="2653b-187">파이프라인 및 되풀이에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="2653b-188">`Get-AdlJobPipeline` cmdlet을 사용하여 이전에 제출한 작업의 파이프라인 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-188">Use the `Get-AdlJobPipeline` cmdlet to see the pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="2653b-189">`Get-AdlJobRecurrence` cmdlet을 사용하여 이전에 제출한 작업의 되풀이 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-189">Use the `Get-AdlJobRecurrence` cmdlet to see the recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="2653b-190">작업 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="2653b-191">작업 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-191">Get job status</span></span>

<span data-ttu-id="2653b-192">특정 작업의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-192">Get the status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-the-job-outputs"></a><span data-ttu-id="2653b-193">작업 출력 검토</span><span class="sxs-lookup"><span data-stu-id="2653b-193">Examine the job outputs</span></span>

<span data-ttu-id="2653b-194">작업이 종료되면 폴더의 파일을 나열하여 출력 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-194">After the job has ended, check if the output file exists by listing the files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="2653b-195">실행 중인 작업 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="2653b-196">작업 취소</span><span class="sxs-lookup"><span data-stu-id="2653b-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-to-finish"></a><span data-ttu-id="2653b-197">작업이 완료될 때까지 대기</span><span class="sxs-lookup"><span data-stu-id="2653b-197">Wait for a job to finish</span></span>

<span data-ttu-id="2653b-198">작업이 완료될 때까지 `Get-AdlAnalyticsJob`을 반복하는 대신 `Wait-AdlJob` cmdlet을 사용하여 작업이 종료될 때까지 기다릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use the `Wait-AdlJob` cmdlet to wait for the job to end.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="2653b-199">계산 정책 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="2653b-200">기존 계산 정책 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-200">List existing compute policies</span></span>

<span data-ttu-id="2653b-201">`Get-AdlAnalyticsComputePolicy` cmdlet은 Data Lake Analytics 계정에 대한 계산 정책에 대한 정보를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-201">The `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="2653b-202">계산 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="2653b-202">Create a compute policy</span></span>

<span data-ttu-id="2653b-203">`New-AdlAnalyticsComputePolicy` cmdlet은 Data Lake Analytics 계정에 대한 새 계산 정책을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-203">The `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="2653b-204">이 예제에서는 지정된 사용자에게 제공되는 최대 AU를 50으로 설정하고 최소 작업 우선 순위를 250으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-204">This example sets  the maximum AUs available to the specified user to 50, and the minimum job priority to 250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-the-existence-of-a-file"></a><span data-ttu-id="2653b-205">파일의 존재 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-205">Check for the existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="2653b-206">업로드 및 다운로드</span><span class="sxs-lookup"><span data-stu-id="2653b-206">Uploading and downloading</span></span>

<span data-ttu-id="2653b-207">파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="2653b-208">전체 폴더를 재귀적으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="2653b-209">파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="2653b-210">전체 폴더를 재귀적으로 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="2653b-211">업로드 또는 다운로드 프로세스가 중단될 경우 ``-Resume`` 플래그와 함께 해당 cmdlet을 다시 실행하여 프로세스를 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-211">If the upload or download process is interrupted, you can attempt to resume the process by running the cmdlet again with the ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="2653b-212">카탈로그 항목 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-212">Manage catalog items</span></span>

<span data-ttu-id="2653b-213">U-SQL 카탈로그는 U-SQL 스크립트에서 공유할 수 있도록 데이터 및 코드를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-213">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="2653b-214">카탈로그를 사용하면 가능한 가장 높은 성능으로 Azure 데이터 레이크의 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-214">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="2653b-215">자세한 내용은 [U-SQL 카탈로그 사용](data-lake-analytics-use-u-sql-catalog.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2653b-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-the-u-sql-catalog"></a><span data-ttu-id="2653b-216">U-SQL 카탈로그의 항목 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-216">List items in the U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="2653b-217">ADLA 계정에 있는 모든 데이터베이스의 모든 어셈블리를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-217">List all the assemblies in all the databases in an ADLA Account.</span></span>

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

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="2653b-218">카탈로그 항목에 대한 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="2653b-219">카탈로그에 자격 증명 만들기</span><span class="sxs-lookup"><span data-stu-id="2653b-219">Create credentials in a catalog</span></span>

<span data-ttu-id="2653b-220">U-SQL 데이터베이스 내에서 Azure에서 호스트되는 데이터베이스에 대한 자격 증명 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="2653b-221">현재 U-SQL 자격 증명은 PowerShell을 통해 만들 수 있는 유일한 유형의 카탈로그 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-221">Currently, U-SQL credentials are the only type of catalog item that you can create through PowerShell.</span></span>

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

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="2653b-222">ADLA 계정에 대한 기본 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="2653b-223">계정 이름을 지정하는 경우 다음 코드는 계정에 대한 기본 정보를 조회합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-223">Given an account name, the following code looks up basic information about the account</span></span>

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

## <a name="working-with-azure"></a><span data-ttu-id="2653b-224">Azure 작업</span><span class="sxs-lookup"><span data-stu-id="2653b-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="2653b-225">AzureRm 오류에 대한 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="2653b-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="2653b-226">관리자로 실행 중인지 확인</span><span class="sxs-lookup"><span data-stu-id="2653b-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="2653b-227">TenantID 찾기</span><span class="sxs-lookup"><span data-stu-id="2653b-227">Find a TenantID</span></span>

<span data-ttu-id="2653b-228">구독 이름에서</span><span class="sxs-lookup"><span data-stu-id="2653b-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="2653b-229">구독 ID에서</span><span class="sxs-lookup"><span data-stu-id="2653b-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="2653b-230">"contoso.com"과 같은 도메인 주소에서</span><span class="sxs-lookup"><span data-stu-id="2653b-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="2653b-231">모든 구독 및 테넌트 ID 나열</span><span class="sxs-lookup"><span data-stu-id="2653b-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="2653b-232">템플릿을 사용하여 Data Lake Analytics 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="2653b-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="2653b-233">또한 다음 PowerShell 스크립트를 통해 Azure 리소스 그룹 템플릿을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-233">You can also use an Azure Resource Group template using the following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update the JSON template path 

# Log in to Azure
Login-AzureRmAccount -SubscriptionId $subId

# Create the resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create the Data Lake Analytics account with the default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="2653b-234">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](../azure-resource-manager/resource-group-template-deploy.md) 및 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2653b-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="2653b-235">**예제 템플릿**</span><span class="sxs-lookup"><span data-stu-id="2653b-235">**Example template**</span></span>

<span data-ttu-id="2653b-236">다음 텍스트를 `.json` 파일로 저장한 후 이전의 PowerShell 스크립트를 통해 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2653b-236">Save the following text as a `.json` file, and then use the preceding PowerShell script to use the template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Analytics account to create."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "The name of the Data Lake Store account to create."
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

## <a name="next-steps"></a><span data-ttu-id="2653b-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2653b-237">Next steps</span></span>
* [<span data-ttu-id="2653b-238">Microsoft Azure 데이터 레이크 분석 개요</span><span class="sxs-lookup"><span data-stu-id="2653b-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="2653b-239">[Azure Portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)을 사용하여 Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="2653b-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="2653b-240">[Azure Portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)를 사용하여 Azure Data Lake Analytics 관리</span><span class="sxs-lookup"><span data-stu-id="2653b-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
