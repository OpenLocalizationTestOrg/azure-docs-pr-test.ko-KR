---
title: "태그에 대 한 리소스 정책을 aaaAzure | Microsoft Docs"
description: "리소스에서 태그를 관리하기 위한 리소스 정책의 예제 제공"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>태그에 대한 리소스 정책 적용

이 항목에서는 일반적인 정책 규칙 tooensure 일관성 있게 사용 태그의 리소스에 적용할 수 있습니다.

태그 정책 tooa 리소스 그룹이 나 기존 리소스를 사용 하 여 구독에 적용 해도 hello 정책 toothose 리소스 소급 적용 되지 않습니다. 해당 리소스에 대해 tooenforce hello 정책 기존 리소스는 업데이트 toohello를 트리거합니다. 이 문서는 업데이트를 트리거하기 위해 PowerShell 예제를 포함합니다.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>리소스 그룹의 모든 리소스에 태그/값이 있는지 확인

일반적으로 리소스 그룹의 모든 리소스에 특정 태그 및 값이 있어야 합니다. 이 요구 사항은 부서별로 필요한 tootrack 비용은 경우가 많습니다. hello 다음 조건이 충족 되어야 합니다.

* hello 필요한 태그 및 값 추가 toonew 하며 hello 태그 되지 않은 리소스를 업데이트 합니다.
* hello 필수 태그 및 모든 기존 리소스에서 값을 제거할 수 없습니다.

두 개의 기본 제공 정책 tooa 리소스 그룹을 적용 하 여 요구이 사항을 충족할 수 있습니다.

| ID | 설명 |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Hello 사용자가 지정 되지 않은 경우 필요한 태그 및 값이 기본값으로 적용 됩니다. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | 필수 태그와 해당 값을 적용합니다. |

### <a name="powershell"></a>PowerShell

PowerShell 스크립트 뒤 hello hello 두 가지 기본 제공 정책 정의 tooa 리소스 그룹에 할당 합니다. Hello 스크립트를 실행 하기 전에 모든 필수 태그 toohello 리소스 그룹을 할당 합니다. Hello 리소스 그룹의 각 태그는 hello 그룹에 hello 리소스가 필요 합니다. 구독에서 tooassign tooall 리소스 그룹 hello를 제공 하지 않으면 `-Name` hello 리소스 그룹을 가져올 때 매개 변수입니다.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Hello 정책을 할당 한 후 기존 리소스 tooenforce hello 태그 정책을 추가 하는 업데이트 tooall를 트리거할 수 있습니다. hello 다음 스크립트를 유지 hello 리소스에 존재 하는 다른 태그:

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>리소스 유형에 대한 태그 요구
다음 예제는 hello toonest 논리 연산자 toorequire 응용 프로그램 (이 경우 저장소 계정)에 지정 된 리소스 형식에 대 한 태그 하는 방법을 보여 줍니다.

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>태그 요구
hello 다음 정책을 요청 거부 (모든 값을 적용할 수 있습니다.) "costCenter" 키를 포함 하는 태그 되지 않은:

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>다음 단계
* 한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다. 구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.
* 소개 tooresource 정책에 대 한 참조 [리소스 정책 개요](resource-manager-policy.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

