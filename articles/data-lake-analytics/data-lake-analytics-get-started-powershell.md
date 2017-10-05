---
title: "Azure PowerShell을 사용하여 Azure Data Lake Analytics 시작 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Data Lake Analytics 계정을 만들고, U-SQL을 사용하여 Data Lake Analytics 작업을 만들고, 작업을 제출하는 방법에 대해 알아봅니다. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: 4f73e27c733edae658d1ea3bdabe48076328279b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="09d40-103">Azure PowerShell을 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="09d40-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="09d40-104">Azure PowerShell을 사용하여 Azure Data Lake Analytics 계정을 만든 다음 U-SQL 작업을 제출하고 실행하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-104">Learn how to use Azure PowerShell to create Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="09d40-105">데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09d40-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="09d40-106">Prerequisites</span></span>

<span data-ttu-id="09d40-107">이 자습서를 시작하기 전에 다음 정보가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-107">Before you begin this tutorial, you must have the following information:</span></span>

* <span data-ttu-id="09d40-108">**Azure 데이터 레이크 분석 계정**.</span><span class="sxs-lookup"><span data-stu-id="09d40-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="09d40-109">[Data Lake Analytics 시작](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="09d40-110">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="09d40-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="09d40-111">[Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-111">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="09d40-112">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="09d40-112">Log in to Azure</span></span>

<span data-ttu-id="09d40-113">이 자습서에서는 Azure PowerShell을 사용하는 것에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="09d40-114">특히, Azure에 로그인하는 방법을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-114">In particular, you need to know how to log in to Azure.</span></span> <span data-ttu-id="09d40-115">도움이 필요한 경우 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-115">See the [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="09d40-116">구독 이름을 사용하여 로그인하려면</span><span class="sxs-lookup"><span data-stu-id="09d40-116">To log in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="09d40-117">구독 이름 대신 구독 ID를 사용하여 로그인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-117">Instead of the subscription name, you can also use a subscription id to log in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="09d40-118">성공하면 이 명령의 출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-118">If  successful, the output of this command looks like the following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-the-tutorial"></a><span data-ttu-id="09d40-119">자습서 준비</span><span class="sxs-lookup"><span data-stu-id="09d40-119">Preparing for the tutorial</span></span>

<span data-ttu-id="09d40-120">이 자습서의 PowerShell 코드 조각은 이러한 변수를 사용하여 이 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-120">The PowerShell snippets in this tutorial use these variables to store this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="09d40-121">Data Lake Analytics 계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="09d40-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="09d40-122">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="09d40-122">Submit a U-SQL job</span></span>

<span data-ttu-id="09d40-123">U-SQL 스크립트를 보유할 PowerShell 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-123">Create a PowerShell variable to hold the U-SQL script.</span></span>

```
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="09d40-124">스크립트를 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-124">Submit the script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="09d40-125">또는 스크립트를 파일로 저장한 후 다음 명령으로 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-125">Alternatively, you could save the script as a file and submit with the following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="09d40-126">특정 작업의 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-126">Get the status of a specific job.</span></span> <span data-ttu-id="09d40-127">작업이 완료되는 것으로 표시될 때까지 이 cmdlet을 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-127">Keep using this cmdlet until you see the job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="09d40-128">작업이 완료될 때까지 Get-AdlAnalyticsJob을 호출하지 않고 Wait-AdlJob cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use the Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="09d40-129">출력 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-129">Download the output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="09d40-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="09d40-130">See also</span></span>
* <span data-ttu-id="09d40-131">다른 도구를 사용하여 같은 자습서를 보려면 페이지 맨 위의 탭 선택기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09d40-131">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="09d40-132">U-SQL을 알아보려면 [Azure Data Lake Analytics U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-132">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="09d40-133">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09d40-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
