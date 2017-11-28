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
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="28f6b-103">이름 및 텍스트에 대한 리소스 정책 적용</span><span class="sxs-lookup"><span data-stu-id="28f6b-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="28f6b-104">이 항목에서는 여러 가지 [리소스 정책을](resource-manager-policy.md) tooestablish 이름 지정 및 텍스트 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="28f6b-105">이러한 정책은 리소스 이름 및 태그 값에 대해 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="28f6b-106">와일드 카드로 명명 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="28f6b-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="28f6b-107">hello 다음 예제에서는 사용을 보여 줍니다 hello hello에서 지원 되는 와일드 카드 **같은** 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="28f6b-108">hello 조건 상태 경우 hello 이름이 않습니다 hello에서 언급 한 패턴 일치 (namePrefix\*nameSuffix) 다음 hello 요청을 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="28f6b-109">패턴으로 명명 규칙 설정</span><span class="sxs-lookup"><span data-stu-id="28f6b-109">Set naming convention with pattern</span></span>

<span data-ttu-id="28f6b-110">리소스 이름이 일치 패턴을 사용 하 여 hello 하는지 toospecify 조건과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="28f6b-111">hello 다음 예제와 이름을 toostart `contoso` 하 고 6 개의 추가 문자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="28f6b-112">태그 값에 대한 날짜 패턴 설정</span><span class="sxs-lookup"><span data-stu-id="28f6b-112">Set date pattern for tag value</span></span>

<span data-ttu-id="28f6b-113">두 자리 숫자, 대시, 3 개의 문자, 대시 및 4 자리 숫자로, 사용 날짜 패턴 toorequire:</span><span class="sxs-lookup"><span data-stu-id="28f6b-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="28f6b-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="28f6b-114">Next steps</span></span>
* <span data-ttu-id="28f6b-115">한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="28f6b-116">구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="28f6b-117">hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="28f6b-118">REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="28f6b-119">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="28f6b-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

