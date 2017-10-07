---
title: "Azure PowerShell을 사용 하 여 Azure Data Lake 분석 aaaGet 시작 | Microsoft Docs"
description: "Azure PowerShell toocreate Data Lake 분석 계정을 사용 하 고, U SQL을 사용 하 여 데이터 레이크 분석 작업 만들기 하 고 및 hello 작업을 제출 합니다. "
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
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="a92a1-103">Azure PowerShell을 사용하여 Azure Data Lake Analytics 시작</span><span class="sxs-lookup"><span data-stu-id="a92a1-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="a92a1-104">어떻게 toouse Azure PowerShell toocreate Azure Data Lake 분석 계정 제출 고 U-SQL 작업 실행에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="a92a1-105">데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a92a1-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a92a1-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a92a1-106">Prerequisites</span></span>

<span data-ttu-id="a92a1-107">이 자습서를 시작 하기 전에 다음 정보는 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="a92a1-108">**Azure 데이터 레이크 분석 계정**.</span><span class="sxs-lookup"><span data-stu-id="a92a1-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="a92a1-109">[Data Lake Analytics 시작](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a92a1-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="a92a1-110">**Azure PowerShell이 포함된 워크스테이션**.</span><span class="sxs-lookup"><span data-stu-id="a92a1-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="a92a1-111">참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="a92a1-112">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="a92a1-112">Log in tooAzure</span></span>

<span data-ttu-id="a92a1-113">이 자습서에서는 Azure PowerShell을 사용하는 것에 이미 익숙하다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="a92a1-114">특히, 해야 tooknow 어떻게 toolog tooAzure에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="a92a1-115">Hello 참조 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) 도움이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="a92a1-116">구독 이름 사용 하 여 toolog:</span><span class="sxs-lookup"><span data-stu-id="a92a1-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="a92a1-117">Hello 구독 이름 대신에 구독 id toolog를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="a92a1-118">성공 하면 hello이이 명령의 출력을 텍스트 다음 hello 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="a92a1-119">Hello 자습서 준비</span><span class="sxs-lookup"><span data-stu-id="a92a1-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="a92a1-120">이 자습서에서는 PowerShell 조각 hello 이러한 변수 toostore이이 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="a92a1-121">Data Lake Analytics 계정에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="a92a1-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="a92a1-122">U-SQL 작업 제출</span><span class="sxs-lookup"><span data-stu-id="a92a1-122">Submit a U-SQL job</span></span>

<span data-ttu-id="a92a1-123">PowerShell 변수 toohold hello U-SQL 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

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
    too"/data.csv"
    USING Outputters.Csv();

"@
```

<span data-ttu-id="a92a1-124">Hello 스크립트를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="a92a1-125">Hello 스크립트를 파일로 저장 한 다음 명령을 hello로 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="a92a1-126">특정 작업의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-126">Get hello status of a specific job.</span></span> <span data-ttu-id="a92a1-127">Hello 작업이 완료 되어 표시 될 때까지이 cmdlet을 사용 하 여 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="a92a1-128">작업이 완료 될 때까지 Get AdlAnalyticsJob를 반복 호출을 하는 대신 hello 대기 AdlJob cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="a92a1-129">Hello 출력 파일을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="a92a1-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a92a1-130">See also</span></span>
* <span data-ttu-id="a92a1-131">toosee hello 같은 다른 도구를 사용 하 여 자습서 hello hello 페이지 위쪽에 hello 탭 선택기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="a92a1-132">toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a92a1-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="a92a1-133">관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a92a1-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
