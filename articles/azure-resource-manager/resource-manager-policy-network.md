---
title: "네트워크 리소스에 대 한 리소스 정책을 aaaAzure | Microsoft Docs"
description: "네트워크 리소스의 hello 배포 관리를 위한 Azure 리소스 관리자 정책을 설명 합니다."
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
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a>리소스 정책 toonetwork 리소스 적용
이 문서에는 예가 나와 [리소스 정책](resource-manager-policy.md) tooAzure 가상 네트워크 게이트웨이 적용할 수 있습니다. 이 정책은 조직에 배포된 게이트웨이의 일관성을 보장합니다. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>허용된 가상 네트워크 게이트웨이 SKU 정의

hello 정책에 따라 가상 네트워크 게이트웨이에 대 한 어떤 Sku를 배포할 수를 제한 합니다.

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
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

## <a name="next-steps"></a>다음 단계
* 한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다. 구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다. 
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

