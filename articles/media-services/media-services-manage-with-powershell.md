---
title: "aaaManage PowerShell 사용한 Azure 미디어 서비스 계정"
description: "PowerShell cmdlet과 toomanage Azure 미디어 서비스 계정 하는 방법에 대해 알아봅니다."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>PowerShell을 사용하여 Azure 미디어 서비스 계정 관리
> [!div class="op_single_selector"]
> * [포털](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST (영문)](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe 수 toocreate Azure 미디어 서비스 계정, Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure 무료 평가판</a>을 참조하세요.
> 
> 

## <a name="overview"></a>개요
이 문서 hello Azure 리소스 관리자 framework에서 hello Azure PowerShell cmdlet에 대 한 Azure 미디어 서비스 AMS ()를 나열합니다. hello에 hello cmdlet 존재 **Microsoft.Azure.Commands.Media** 네임 스페이스입니다.

## <a name="versions"></a>버전
**ApiVersion**: "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
미디어 서비스를 만듭니다.

### <a name="syntax"></a>구문
매개 변수 집합: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

매개 변수 집합: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | Name |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

**-Location &lt;String&gt;**

Hello 미디어 서비스의 hello 리소스 위치를 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |2 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-StorageAccountId &lt;String&gt;**

Hello 미디어 서비스와 연결 된 기본 저장소 계정을 지정 합니다.

* 새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.
* hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |3 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| 매개 변수 집합 이름 |StorageAccountIdParamSet |
| Accept Wildcard Characters? |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Hello 미디어 서비스와 연결 된 저장소 계정을 지정 합니다.

* 새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.
* hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.
* 단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |3 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| 매개 변수 집합 이름 |StorageAccountsParamSet |
| Accept Wildcard Characters? |false |

**-Tags &lt;Hashtable&gt;**

Hello 미디어 서비스와 관련 된 hello 태그의 해시 테이블을 지정 합니다.

* 예: @{"tag1"="value1";" tag2 "=: value2"을 (를)

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position? |named |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
미디어 서비스를 만듭니다.

### <a name="syntax"></a>구문
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | Name |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Hello 미디어 서비스와 연결 된 저장소 계정을 지정 합니다.

* 새 저장소 계정 (hello 리소스 관리자 API를 사용 하 여 만든)만 지원 합니다.
* hello 저장소 계정이 있어야 하며가 hello hello 미디어 서비스와 동일한 위치입니다.
* 단 하나의 저장소 계정 만을 기본으로 지정할 수 있습니다.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position? |named |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| 매개 변수 집합 이름 |StorageAccountsParamSet |
| Accept Wildcard Characters? |false |

**-Tags &lt;Hashtable&gt;**

이 미디어 서비스와 관련 된 hello 태그의 해시 테이블을 지정 합니다.

* hello 미디어 서비스와 관련 된 hello 태그 hello 고객이 지정 된 값으로 대체 됩니다.

| Aliases | 없음 |
| --- | --- |
| Required? |false |
| Position? |named |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
미디어 서비스를 제거합니다.

### <a name="syntax"></a>구문
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |2 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |False |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
지정된 이름으로 리소스 그룹 또는 미디어 서비스에 있는 모든 미디어 서비스를 가져옵니다.

### <a name="syntax"></a>구문
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| 매개 변수 집합 이름 |ResourceGroupParameterSet, AccountNameParameterSet |

Accept Wildcard Characters?   false

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| 매개 변수 집합 이름 |AccountNameParameterSet |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
미디어 서비스의 키를 가져옵니다.

### <a name="syntax"></a>구문
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
미디어 서비스의 기본 또는 보조 키를 다시 생성합니다.

### <a name="syntax"></a>구문
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-KeyType &lt;KeyType&gt;**

Hello hello 미디어 서비스 키 유형을 지정합니다.

* 기본 또는 보조

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |2 |
| 기본값 |없음 |
| Accept Pipeline Input? |false |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toothe cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Hello 미디어 서비스와 연결 된 저장소 계정에 대 한 저장소 계정 키를 동기화 합니다.

### <a name="syntax"></a>구문
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>매개 변수
**-ResourceGroupName &lt;String&gt;**

이 미디어 서비스 속한 hello 리소스 그룹 toowhich hello 이름을 지정 합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |0 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-AccountName &lt;String&gt;**

Hello hello 미디어 서비스 이름을 지정합니다.

| Aliases | 없음 |
| --- | --- |
| Required? |true |
| Position? |1 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**-StorageAccountId &lt;String&gt;**

Hello 미디어 서비스와 관련 된 hello 저장소 계정을 지정 합니다.

| Aliases | Id |
| --- | --- |
| Required? |true |
| Position? |2 |
| 기본값 |없음 |
| Accept Pipeline Input? |true(ByPropertyName) |
| Accept Wildcard Characters? |false |

**&lt;CommandParameters&gt;**

이 cmdlet은 공통 매개 변수 hello:-디버그,-ErrorAction,-ErrorVariable,-InformationAction,-InformationVariable,-OutVariable,-OutBuffer,-PipelineVariable,-Verbose,-WarningAction 및-warningvariable을 지원 합니다.

### <a name="inputs"></a>입력
hello 입력된 형식은 toohello cmdlet에 파이프할 수 있음을 hello hello 유형의 개체입니다.

### <a name="outputs"></a>outputs
hello 출력 유형은 cmdlet hello hello 개체 유형의 hello를 내보냅니다.

## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 확인하세요.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

