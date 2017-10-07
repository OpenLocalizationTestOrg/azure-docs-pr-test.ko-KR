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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Azure PowerShell을 사용하여 Azure Data Lake Analytics 시작
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

어떻게 toouse Azure PowerShell toocreate Azure Data Lake 분석 계정 제출 고 U-SQL 작업 실행에 대해 알아봅니다. 데이터 레이크 분석에 대한 자세한 내용은 [Azure 데이터 레이크 분석 개요](data-lake-analytics-overview.md)를 참조하세요.

## <a name="prerequisites"></a>필수 조건

이 자습서를 시작 하기 전에 다음 정보는 hello가 있어야 합니다.

* **Azure 데이터 레이크 분석 계정**. [Data Lake Analytics 시작](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal)을 참조하세요.
* **Azure PowerShell이 포함된 워크스테이션**. 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인

이 자습서에서는 Azure PowerShell을 사용하는 것에 이미 익숙하다고 가정합니다. 특히, 해야 tooknow 어떻게 toolog tooAzure에 있습니다. Hello 참조 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) 도움이 필요 합니다.

구독 이름 사용 하 여 toolog:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Hello 구독 이름 대신에 구독 id toolog를 사용할 수 있습니다.

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

성공 하면 hello이이 명령의 출력을 텍스트 다음 hello 같습니다.

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Hello 자습서 준비

이 자습서에서는 PowerShell 조각 hello 이러한 변수 toostore이이 정보를 사용합니다.

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Data Lake Analytics 계정에 대한 정보 가져오기

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>U-SQL 작업 제출

PowerShell 변수 toohold hello U-SQL 스크립트를 만듭니다.

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

Hello 스크립트를 제출 합니다.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Hello 스크립트를 파일로 저장 한 다음 명령을 hello로 제출할 수 있습니다.

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


특정 작업의 hello 상태를 가져옵니다. Hello 작업이 완료 되어 표시 될 때까지이 cmdlet을 사용 하 여 계속 합니다.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

작업이 완료 될 때까지 Get AdlAnalyticsJob를 반복 호출을 하는 대신 hello 대기 AdlJob cmdlet을 사용할 수 있습니다.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Hello 출력 파일을 다운로드 합니다.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>참고 항목
* toosee hello 같은 다른 도구를 사용 하 여 자습서 hello hello 페이지 위쪽에 hello 탭 선택기를 클릭 합니다.
* toolearn U SQL 참조 [Azure 데이터 레이크 분석 U-SQL 언어 시작](data-lake-analytics-u-sql-get-started.md)합니다.
* 관리 작업을 보려면 [Azure Portal을 사용하여 Azure Data Lake Analytics 관리](data-lake-analytics-manage-use-portal.md)를 참조하세요.
