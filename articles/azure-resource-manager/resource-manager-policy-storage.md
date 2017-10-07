---
title: "저장소 계정에 대 한 리소스 정책을 aaaAzure | Microsoft Docs"
description: "저장소 계정의 hello 배포 관리를 위한 Azure 리소스 관리자 정책을 설명 합니다."
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>리소스 정책 toostorage 계정을 적용 합니다.
이 항목에서는 여러 가지 [리소스 정책을](resource-manager-policy.md) tooAzure 저장소 계정에 적용할 수 있습니다. 이러한 정책은 조직에 배포 된 hello 저장소 계정에 대 한 일관성을 보장 합니다. 

## <a name="define-permitted-storage-account-types"></a>허용되는 저장소 계정 유형 정의

hello 다음과 같은 정책 제한는 [저장소 계정 유형을](../storage/common/storage-redundancy.md) 배포할 수 있습니다.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Sku를 허용 하는 hello을 적용 하기 위한 매개 변수가 있는 유사한 정책 규칙은 기본 제공 정책 정의로 제공 됩니다. hello 기본 제공 정책에의 리소스 ID hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`합니다. 

## <a name="define-permitted-access-tier"></a>허용되는 액세스 계층 정의

hello 다음 정책을 hello의 유형을 지정 [액세스 계층](../storage/blobs/storage-blob-storage-tiers.md) 저장소 계정에 대해 지정할 수 있습니다.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>암호화를 사용하도록 설정해야 함

hello 다음 정책에 따라 모든 저장소 계정 tooenable [저장소 서비스 암호화](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

이 정책 규칙의 hello 리소스 ID와 기본 제공 된 정책 정의로 제공 됩니다. `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`합니다.

## <a name="next-steps"></a>다음 단계
* 한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다. 구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다. 
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

