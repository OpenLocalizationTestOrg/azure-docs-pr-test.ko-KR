---
title: "명명 규칙에 대 한 리소스 정책을 aaaAzure | Microsoft Docs"
description: "리소스 명명 규칙에 대한 Azure Resource Manager 정책을 설명합니다."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>이름 및 텍스트에 대한 리소스 정책 적용
이 항목에서는 여러 가지 [리소스 정책을](resource-manager-policy.md) tooestablish 이름 지정 및 텍스트 규칙을 적용할 수 있습니다. 이러한 정책은 리소스 이름 및 태그 값에 대해 일관성을 보장합니다. 

## <a name="set-naming-convention-with-wildcard"></a>와일드 카드로 명명 규칙 설정
hello 다음 예제에서는 사용을 보여 줍니다 hello hello에서 지원 되는 와일드 카드 **같은** 조건입니다. hello 조건 상태 경우 hello 이름이 않습니다 hello에서 언급 한 패턴 일치 (namePrefix\*nameSuffix) 다음 hello 요청을 거부 합니다.

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>패턴으로 명명 규칙 설정

리소스 이름이 일치 패턴을 사용 하 여 hello 하는지 toospecify 조건과 일치 합니다. hello 다음 예제와 이름을 toostart `contoso` 하 고 6 개의 추가 문자를 포함 합니다.

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>태그 값에 대한 날짜 패턴 설정

두 자리 숫자, 대시, 3 개의 문자, 대시 및 4 자리 숫자로, 사용 날짜 패턴 toorequire:

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>다음 단계
* 한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다. 구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다. hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다. REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다. 
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

