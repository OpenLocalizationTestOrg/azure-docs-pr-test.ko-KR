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
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="2529e-103">리소스 정책 toonetwork 리소스 적용</span><span class="sxs-lookup"><span data-stu-id="2529e-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="2529e-104">이 문서에는 예가 나와 [리소스 정책](resource-manager-policy.md) tooAzure 가상 네트워크 게이트웨이 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="2529e-105">이 정책은 조직에 배포된 게이트웨이의 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="2529e-106">허용된 가상 네트워크 게이트웨이 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="2529e-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="2529e-107">hello 정책에 따라 가상 네트워크 게이트웨이에 대 한 어떤 Sku를 배포할 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2529e-108">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2529e-108">Next steps</span></span>
* <span data-ttu-id="2529e-109">한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="2529e-110">구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="2529e-111">hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2529e-112">REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="2529e-113">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="2529e-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

