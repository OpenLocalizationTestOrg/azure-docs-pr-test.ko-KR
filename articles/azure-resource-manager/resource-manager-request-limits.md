---
title: "리소스 관리자 요청 제한 aaaAzure | Microsoft Docs"
description: "구독 제한에 도달 하면 Azure 리소스 관리자와 조정 toouse 요청 하는 방식에 대해 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Resource Manager 요청 제한
각 구독 및 테 넌 트에 대 한 리소스 관리자 제한 요청 too15, 000 시간당 읽고 요청 too1, 시간당 200을 씁니다. 이러한 제한이 적용 tooeach Azure 리소스 관리자 인스턴스가; 모든 Azure 지역에서 여러 인스턴스가 있는 및 Azure 리소스 관리자는 배포 된 tooall Azure 지역입니다.  따라서 사용자 요청이 일반적으로 서로 다른 여러 인스턴스에서 서비스되므로 실제 한도는 위에 나열된 것보다 훨씬 높습니다.

응용 프로그램 또는 스크립트는 이러한 한도 도달 해야 toothrottle 요청 합니다. 이 항목에서는 남은 toodetermine hello 요청 hello 제한에 도달 하기 전에 보유 하는 방식과 toorespond hello 제한에 도달 하면 합니다.

Hello 제한에 도달 하면 hello HTTP 상태 코드 수신 **429 너무 많은 요청**합니다.

요청 수가 hello은 범위 지정 된 tooeither 구독 또는 테 넌 트입니다. 여러 개 있는 경우 구독에서 요청을 수행 하는 동시 응용 프로그램 hello 요청 해당 응용 프로그램을 함께 추가 됩니다 toodetermine hello 나머지 요청 수입니다.

범위가 지정 된 구독 요청은 hello 관련 구독에 hello 리소스 그룹을 검색 하는 등를 구독 id를 전달 하는 것입니다. 테넌트에 범위가 지정된 요청은 올바른 Azure 위치 검색 등과 같은 구독 ID를 포함하지 않습니다.

## <a name="remaining-requests"></a>나머지 요청
응답 헤더를 검사 하 여 hello 나머지 요청 수를 확인할 수 있습니다. 각 요청 hello 나머지 읽기 및 쓰기 요청 수에 대 한 값을 포함합니다. hello 다음 표에서 hello 응답 헤더 값을 검사할 수 있습니다.

| 응답 헤더 | 설명 |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |구독에 범위가 지정된 나머지 읽기 |
| x-ms-ratelimit-remaining-subscription-writes |구독에 범위가 지정된 나머지 쓰기 |
| x-ms-ratelimit-remaining-tenant-reads |테넌트에 범위가 지정된 나머지 읽기 |
| x-ms-ratelimit-remaining-tenant-writes |테넌트에 범위가 지정된 나머지 쓰기 |
| x-ms-ratelimit-remaining-subscription-resource-requests |구독에 범위가 지정된 나머지 리소스 종류 요청.<br /><br />서비스는 hello 기본 제한을 재정의 한 경우에이 헤더 값이 반환 됩니다. 리소스 관리자는 hello 구독 읽기 또는 쓰기 대신이 값을 추가합니다. |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |구독에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.<br /><br />서비스는 hello 기본 제한을 재정의 한 경우에이 헤더 값이 반환 됩니다. 이 값 hello 다양 한 나머지 컬렉션 요청 (목록 리소스)를 제공 합니다. |
| x-ms-ratelimit-remaining-tenant-resource-requests |테넌트에 범위가 지정된 나머지 리소스 종류 요청.<br /><br />테 넌 트 수준에서 요청에 대 한이 헤더에만 추가 됩니다 및 경우 서비스에만 hello 기본 제한을 재정의 합니다. 리소스 관리자는 hello 테 넌 트 읽기 또는 쓰기 대신이 값을 추가합니다. |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |테넌트에 범위가 지정된 나머지 리소스 종류 컬렉션 요청.<br /><br />테 넌 트 수준에서 요청에 대 한이 헤더에만 추가 됩니다 및 경우 서비스에만 hello 기본 제한을 재정의 합니다. |

## <a name="retrieving-hello-header-values"></a>Hello 헤더 값 검색
코드 또는 스크립트에서 이러한 헤더 값을 검색하는 것은 임의의 헤더 값을 검색하는 것과 같습니다. 

예를 들어 **C#**에서 hello 헤더 값을 검색 한 **HttpWebResponse** 라는 개체 **응답** 코드 다음 hello로:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

**PowerShell**을 Invoke-webrequest 작업에서 hello 헤더 값을 검색 합니다.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

하거나, 디버깅에 대 한 요청 toosee hello 남은 hello를 제공할 수 있습니다 사용할 경우 **-디버그** 에 매개 변수 여 **PowerShell** cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

hello 다음 응답 값을 포함 하 여 여러 개의 값을 반환 합니다.

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

**Azure CLI**를 사용 하 여 hello 헤더 값을 검색할 hello 더 자세한 옵션입니다.

```azurecli
azure group list -vv --json
```

hello 다음 개체를 포함 하 여 여러 개의 값을 반환 합니다.

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>다음 요청을 보낼 때까지 대기
리소스 관리자 hello hello 요청 제한에 도달 하는 경우 반환 **429** HTTP 상태 코드와 **Retry-after** hello 헤더의 값입니다. hello **Retry-after** hello 다음 요청을 보내기 전에 응용 프로그램 대기 해야 하는 시간 (초) (또는 절전 모드) hello 수를 지정 하는 값입니다. Hello 다시 시도 값 경과 하기 전에 요청을 보내는 사용자 요청이 처리 되지 않습니다 및 새 다시 시도 값이 반환 됩니다.

## <a name="next-steps"></a>다음 단계

* 제한 및 할당량에 대한 자세한 내용은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.
* 비동기 REST 요청을 처리 하는 방법에 대 한 toolearn 참조 [Azure 비동기 작업을 추적](resource-manager-async-operations.md)합니다.
