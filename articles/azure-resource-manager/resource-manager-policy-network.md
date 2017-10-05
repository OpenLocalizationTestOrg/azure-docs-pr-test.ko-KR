---
title: "네트워크 리소스에 대한 Azure 리소스 정책 | Microsoft Docs"
description: "네트워크 리소스 배포를 관리하기 위한 Azure Resource Manager 정책을 설명합니다."
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
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="cf103-103">네트워크 리소스에 리소스 정책 적용</span><span class="sxs-lookup"><span data-stu-id="cf103-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="cf103-104">이 문서에서는 Azure 가상 네트워크 게이트웨이에 적용할 수 있는 [리소스 정책](resource-manager-policy.md) 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cf103-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="cf103-105">이 정책은 조직에 배포된 게이트웨이의 일관성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="cf103-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="cf103-106">허용된 가상 네트워크 게이트웨이 SKU 정의</span><span class="sxs-lookup"><span data-stu-id="cf103-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="cf103-107">다음 정책은 가상 네트워크 게이트웨이에 대해 배포할 수 있는 SKU를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="cf103-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cf103-108">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cf103-108">Next steps</span></span>
* <span data-ttu-id="cf103-109">앞의 예제와 표시된 바와 같이 정책 규칙을 정의한 후에는 정책 정의를 만들고 범위에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf103-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="cf103-110">범위는 구독, 리소스 그룹 또는 리소스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf103-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="cf103-111">포털을 통해 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf103-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="cf103-112">REST API, PowerShell 또는 Azure CLI를 통해 정책을 할당하려면 [스크립트를 통해 정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf103-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="cf103-113">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf103-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

