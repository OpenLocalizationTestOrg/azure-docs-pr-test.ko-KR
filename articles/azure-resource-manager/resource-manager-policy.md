---
title: "aaaAzure 리소스 정책 | Microsoft Docs"
description: "배포 하는 동안 toouse Azure 리소스 관리자 정책 tooensure 일관성 있는 리소스 속성 설정 방법을 설명 합니다. Hello 구독 또는 리소스 그룹에 정책은 적용할 수 있습니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>리소스 정책 개요
리소스 정책을 사용 하면 조직의 리소스에 대 한 tooestablish 규칙 수 있습니다. 규칙을 정의하여 비용을 제어하고 리소스를 보다 쉽게 관리할 수 있습니다. 예를 들어, 특정 유형의 가상 컴퓨터만 허용되게 지정할 수 있습니다. 또는 모든 리소스가 특정 태그를 갖도록 요구할 수 있습니다. 정책은 모든 자식 리소스에 의해 상속됩니다. 따라서 정책이 적용 된 tooa 리소스 그룹와 된 경우 해당 리소스 그룹에서 적용 가능한 tooall hello 리소스입니다.

정책에 대 한 개념 toounderstand 두 가지가 있습니다.

* hello 정책이 적용 되는 경우 고 어떤 작업 tootake 설명 정책 정의-
* hello 정책 정의 tooa 범위 (구독 또는 리소스 그룹)를 적용 하면 정책 할당-

이 항목은 정책 정의에 중점을 둡니다. 정책 할당에 대 한 정보를 참조 하십시오. [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md) 또는 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.

리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.

> [!NOTE]
> 현재 정책 태그, 종류 및 hello Microsoft.Resources/deployments 리소스 종류 등의 위치를 지원 하지 않는 리소스 종류를 평가 하지 않습니다. 이 지원은 나중에 추가됩니다. tooavoid 이전 버전과 호환성 문제를 명시적으로 형식을 지정 해야 정책을 작성 하는 경우. 예를 들어 형식을 지정하지 않은 태그 정책이 모든 형식에 적용됩니다. 이 경우 태그를 지원 하지 않는 중첩 리소스가 템플릿 배포 실패 하 고 hello 배포 리소스 유형이 toopolicy 평가 추가 되었습니다. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>RBAC(역할 기반 액세스 제어)와 어떻게 다르나요?
정책 및 RBAC(역할 기반 액세스 제어) 간에 몇 가지 차이점이 있습니다. RBAC는 다른 범위에 있는 **사용자** 작업에 중점을 둡니다. 예를 들어 toothat 리소스 그룹 변경 내용을 확인할 수 있도록 필요한 hello 범위, 리소스 그룹에 대 한 toohello 참가자 역할을 추가 됩니다. 정책은 배포하는 동안 **리소스** 속성에 중점을 둡니다. 예를 들어, 정책을 통해 hello 유형의 프로 비전 할 수 있는 리소스를 제어할 수 있습니다. 또는 hello 리소스를 프로비저닝할 수 있는 hello 위치를 제한할 수 있습니다. RBAC와는 달리 정책은 기본적으로 허용 및 명시적 거부 시스템입니다. 

toouse 정책을 RBAC를 통해 인증 해야 합니다. 구체적으로 사용자 계정에는 다음 권한이 필요합니다.

* `Microsoft.Authorization/policydefinitions/write`사용 권한 toodefine 정책
* `Microsoft.Authorization/policyassignments/write`사용 권한 tooassign 정책 

이러한 사용 권한은 hello에 포함 되지 않은 **참가자** 역할입니다.

## <a name="built-in-policies"></a>기본 제공 정책

Hello 수를 줄일 수 있는 몇 가지 기본 제공 된 정책 정의 제공 하는 azure toodefine 정책의 해야 합니다. 정책 정의를 계속 하기 전에 기본 제공 된 정책에서 이미 필요한 hello 정의 제공 하는지 여부를 고려해 야 합니다. hello 기본 제공 정책 정의 합니다.

* 허용되는 위치
* 허용되는 리소스 유형
* 허용되는 저장소 계정 SKU
* 허용되는 가상 컴퓨터 SKU
* 태그 및 기본값 적용
* 태그 및 값 적용
* 허용되지 않는 리소스 종류
* SQL Server 버전 12.0 필요
* 저장소 계정 암호화 필요

Hello 통해 이러한 정책 중 하나를 지정할 수 있습니다 [포털](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), 또는 [Azure CLI](resource-manager-policy-create-assign.md#azure-cli)합니다.

## <a name="policy-definition-structure"></a>정책 정의 구조
JSON toocreate 정책 정의 사용 합니다. hello 정책 정의 대 한 요소가 포함 되어 있습니다.

* 매개 변수
* 표시 이름
* description
* 정책 규칙
  * 논리 평가
  * 영향

다음 예제는 hello 리소스가 배포 되는 위치를 제한 하는 정책을 보여 줍니다.

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>매개 변수
매개 변수를 사용 하 여 정책 정의의 hello 수를 줄여서 정책 관리를 간소화 하는 데 도움이 됩니다. 리소스 속성 (예: hello 위치 리소스를 배포할 수 있는 제한)에 대 한 정책을 정의 하 고 hello 정의에 매개 변수를 포함 합니다. 그런 다음 다시 사용할 있습니다 다양 한 시나리오에 대 한 정책 정의 다른 값 (예: 하나의 집합 구독에 대 한 위치 지정)를에서 전달 하 여 때 hello 정책을 할당 합니다.

정책 정의 만들 때 매개 변수를 선언합니다.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

hello 형식의 매개 변수는 문자열 또는 배열 될 수 있습니다. hello 메타 데이터 속성은 Azure 포털 toodisplay 사용자에 게 친숙 정보와 같은 도구에 사용 됩니다. 

Hello 정책 규칙 구문 다음 hello로 매개 변수를 참조 합니다. 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>표시 이름 및 설명

Hello를 사용 하 여 **displayName** 및 **설명** tooidentify hello 정책 정의 및 사용 하는 경우에 대 한 컨텍스트를 제공 합니다.

## <a name="policy-rule"></a>정책 규칙

hello 정책 규칙 이루어져 **경우** 및 **다음** 블록입니다. Hello에 **경우** 블록 hello 정책 적용 되는 시점을 지정 하는 하나 이상의 조건을 정의 합니다. 논리 연산자 toothese 조건을 적용할 수 있습니다 tooprecisely 정책에 대 한 hello 시나리오를 정의 합니다. Hello에 **다음** 블록 하면 hello 나타나는 hello 효과 정의 **경우** 조건이 충족 되는지 합니다.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>논리 연산자
지원 되는 hello 논리 연산자는:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

hello **하지** 구문 hello 조건의 hello 결과 반전 합니다. hello **allOf** 구문 (유사한 toohello 논리 **및** 작업) 모든 조건 toobe true 필요 합니다. hello **anyOf** 구문 (유사한 toohello 논리 **또는** 작업) 하나 이상의 조건 toobe true 필요 합니다.

논리 연산자를 중첩할 수 있습니다. 다음 예제와 hello는 **하지** 내에 중첩 된 작업은 **allOf** 작업 합니다. 

```json
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
```

### <a name="conditions"></a>조건
hello i o n 여부는 **필드** 특정 기준을 충족 합니다. 지원 되는 hello 조건이 됩니다.

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Hello를 사용 하는 경우 **같은** 조건 hello 값에 와일드 카드 (*)를 제공할 수 있습니다.

Hello를 사용 하는 경우 **일치** 조건의 경우 제공 `#` toorepresent \d `?` 는 문자, 및 기타 toorepresent 실제 문자를 문자에 대 한 합니다. 관련 예제는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.

### <a name="fields"></a>필드
조건은 필드를 사용하여 구성됩니다. 필드 hello 리소스 요청 페이로드에서 속성을 나타내는 hello 리소스의 즉 사용 되는 toodescribe hello 상태입니다.  

다음 필드는 hello 지원 됩니다.

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* 속성 별칭 - 목록은 [별칭](#aliases)을 참조하세요.

### <a name="effect"></a>결과
정책은 `deny`, `audit` 및 `append`이라는 세 가지 종류의 효과를 지원합니다. 

* **거부** hello 감사 로그에서 이벤트를 생성 하 고 hello 요청 실패
* **감사** 감사 로그에 경고 이벤트를 생성 하지만 hello 요청에 실패 하지 않습니다
* **추가** 필드 toohello 요청의 hello 정의 집합에 추가 

에 대 한 **추가**, hello 다음 세부 정보를 제공 해야 합니다.

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

문자열 또는 JSON 형식 개체 hello 값일 수 있습니다. 

## <a name="aliases"></a>Aliases

리소스 종류에 대 한 속성 별칭 tooaccess 특정 속성을 사용 합니다. 별칭을 사용 하면 리소스에는 속성에 허용 되는 값 또는 조건이 무엇 toorestrict 있습니다. 각 별칭 toopaths가 주어진된 리소스 종류에 대해 다른 API 버전에 매핑합니다. 정책 평가 도중 hello 정책 엔진은 해당 API 버전에 대 한 hello 속성 경로를 가져옵니다.

**Microsoft.Cache/Redis**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | 설정 여부 hello 비 ssl Redis 서버 포트 (6379)은 사용할 수 있습니다. |
| Microsoft.Cache/Redis/shardCount | 프리미엄 캐시 클러스터에 만든 분할 영역 toobe hello 수를 설정 합니다.  |
| Microsoft.Cache/Redis/sku.capacity | Hello Redis 캐시 toodeploy hello 크기를 설정 하십시오.  |
| Microsoft.Cache/Redis/sku.family | Hello SKU 제품군 toouse를 설정 합니다. |
| Microsoft.Cache/Redis/sku.name | Redis Cache toodeploy hello 형식을 설정 합니다. |

**Microsoft.Cdn/profiles**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Hello 이름 hello 가격 책정 계층으로 설정 합니다. |

**Microsoft.Compute/disks**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다. |
| Microsoft.Compute/imagePublisher | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다. |
| Microsoft.Compute/imageSku | Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다. |
| Microsoft.Compute/imageVersion | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다. |


**Microsoft.Compute/virtualMachines**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Compute/imageId | Hello 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 식별자를 설정 합니다. |
| Microsoft.Compute/imageOffer | Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다. |
| Microsoft.Compute/imagePublisher | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다. |
| Microsoft.Compute/imageSku | Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다. |
| Microsoft.Compute/imageVersion | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다. |
| Microsoft.Compute/licenseType | Hello 이미지 또는 디스크 사용이 허가 된 온-프레미스 인지를 설정 합니다. 이 값은 hello Windows Server 운영 체제에 포함 된 이미지에만 사용 됩니다.  |
| Microsoft.Compute/virtualMachines/imageOffer | Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다. |
| Microsoft.Compute/virtualMachines/imagePublisher | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다. |
| Microsoft.Compute/virtualMachines/imageSku | Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다. |
| Microsoft.Compute/virtualMachines/imageVersion | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Hello vhd URI를 설정 합니다. |
| Microsoft.Compute/virtualMachines/sku.name | Hello 가상 컴퓨터의 hello 크기를 설정 합니다. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Hello hello 확장의 게시자 이름을 설정 합니다. |
| Microsoft.Compute/virtualMachines/extensions/type | 확장의 hello 유형을 설정 합니다. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Hello hello 확장 버전을 설정 합니다. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Compute/imageId | Hello 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 식별자를 설정 합니다. |
| Microsoft.Compute/imageOffer | Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다. |
| Microsoft.Compute/imagePublisher | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다. |
| Microsoft.Compute/imageSku | Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다. |
| Microsoft.Compute/imageVersion | Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다. |
| Microsoft.Compute/licenseType | Hello 이미지 또는 디스크 사용이 허가 된 온-프레미스 인지를 설정 합니다. 이 값은 hello Windows Server 운영 체제에 포함 된 이미지에만 사용 됩니다. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Hello 크기 집합의 모든 hello 가상 컴퓨터에 대 한 hello 컴퓨터 이름 접두사를 설정 합니다. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | 사용자 이미지에 대 한 hello blob URI를 설정 합니다. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Hello 크기 집합에 대 한 운영 체제 디스크를 사용 하는 toostore 있는 hello 컨테이너 Url을 설정 합니다. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | 크기 집합의 가상 컴퓨터의 hello 크기를 설정 합니다. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | 크기 집합의 가상 컴퓨터의 hello 계층을 설정 합니다. |
  
**Microsoft.Network/applicationGateways**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Hello 게이트웨이의 hello 크기를 설정 합니다. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | 이 가상 네트워크 게이트웨이의 hello 유형을 설정 합니다. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Hello 게이트웨이 SKU 이름을 설정 합니다. |

**Microsoft.Sql/servers**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Hello 버전의 hello 서버를 설정 합니다. |

**Microsoft.Sql/databases**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Hello hello 데이터베이스 버전을 설정 합니다. |
| Microsoft.Sql/servers/databases/elasticPoolName | Hello 탄력적인 풀 hello 데이터베이스의 hello 이름이 집합입니다. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Hello 구성 된 서비스 수준 목표의 ID hello 데이터베이스를 설정 합니다. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | 구성 된 hello hello 데이터베이스의 서비스 수준 목표의 hello 이름을 설정 합니다.  |

**Microsoft.Sql/elasticpools**

| Alias | 설명 |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | 집합 hello 총 hello 데이터베이스 탄력적 풀에 대 한 DTU를 공유 합니다. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Hello 탄력적 풀의 hello 버전을 설정 합니다. |

**Microsoft.Storage/storageAccounts**

| Alias | 설명 |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | 청구에 사용 되는 집합 hello 액세스 계층입니다. |
| Microsoft.Storage/storageAccounts/accountType | Hello SKU 이름을 설정 합니다. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Hello 서비스는 hello blob 저장소 서비스에 저장 된 hello 데이터를 암호화 하는지 여부를 설정 합니다. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Hello 서비스는 hello 파일 저장소 서비스에 저장 된 hello 데이터를 암호화 하는지 여부를 설정 합니다. |
| Microsoft.Storage/storageAccounts/sku.name | Hello SKU 이름을 설정 합니다. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Tooallow만 https 트래픽 toostorage 서비스를 설정 합니다. |


## <a name="policy-examples"></a>정책 예제

다음 항목 hello 정책 예가 포함 되어 있습니다.

* 태그 정책의 예제는 [태그에 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.
* 이름 지정 및 텍스트 패턴의 예는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.
* 정책 저장소의 예 참조 [리소스 정책 toostorage 계정 적용](resource-manager-policy-storage.md)합니다.
* 가상 컴퓨터 정책의 예 참조 [리소스 정책 tooLinux Vm 적용](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 및 [리소스 정책 tooWindows Vm 적용](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>다음 단계
* 정책 규칙을 정의한 후 tooa 범위를 할당 합니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.
* 에 hello 정책 스키마를 게시 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)합니다. 

