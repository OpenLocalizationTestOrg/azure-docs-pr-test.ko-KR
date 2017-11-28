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
# <a name="apply-resource-policies-toostorage-accounts"></a><span data-ttu-id="6cbb5-103">리소스 정책 toostorage 계정을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-103">Apply resource policies toostorage accounts</span></span>
<span data-ttu-id="6cbb5-104">이 항목에서는 여러 가지 [리소스 정책을](resource-manager-policy.md) tooAzure 저장소 계정에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooAzure storage accounts.</span></span> <span data-ttu-id="6cbb5-105">이러한 정책은 조직에 배포 된 hello 저장소 계정에 대 한 일관성을 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-105">These policies ensure consistency for hello storage accounts deployed in your organization.</span></span> 

## <a name="define-permitted-storage-account-types"></a><span data-ttu-id="6cbb5-106">허용되는 저장소 계정 유형 정의</span><span class="sxs-lookup"><span data-stu-id="6cbb5-106">Define permitted storage account types</span></span>

<span data-ttu-id="6cbb5-107">hello 다음과 같은 정책 제한는 [저장소 계정 유형을](../storage/common/storage-redundancy.md) 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-107">hello following policy restricts which [storage account types](../storage/common/storage-redundancy.md) can be deployed:</span></span>

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

<span data-ttu-id="6cbb5-108">Sku를 허용 하는 hello을 적용 하기 위한 매개 변수가 있는 유사한 정책 규칙은 기본 제공 정책 정의로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-108">A similar policy rule with a parameter for accepting hello allowed SKUs is available as a built-in policy definition.</span></span> <span data-ttu-id="6cbb5-109">hello 기본 제공 정책에의 리소스 ID hello `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-109">hello built-in policy has hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`.</span></span> 

## <a name="define-permitted-access-tier"></a><span data-ttu-id="6cbb5-110">허용되는 액세스 계층 정의</span><span class="sxs-lookup"><span data-stu-id="6cbb5-110">Define permitted access tier</span></span>

<span data-ttu-id="6cbb5-111">hello 다음 정책을 hello의 유형을 지정 [액세스 계층](../storage/blobs/storage-blob-storage-tiers.md) 저장소 계정에 대해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-111">hello following policy specifies hello type of [access tier](../storage/blobs/storage-blob-storage-tiers.md) that can be specified for storage accounts:</span></span>

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

## <a name="ensure-encryption-is-enabled"></a><span data-ttu-id="6cbb5-112">암호화를 사용하도록 설정해야 함</span><span class="sxs-lookup"><span data-stu-id="6cbb5-112">Ensure encryption is enabled</span></span>

<span data-ttu-id="6cbb5-113">hello 다음 정책에 따라 모든 저장소 계정 tooenable [저장소 서비스 암호화](../storage/common/storage-service-encryption.md):</span><span class="sxs-lookup"><span data-stu-id="6cbb5-113">hello following policy requires all storage accounts tooenable [Storage service encryption](../storage/common/storage-service-encryption.md):</span></span>

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

<span data-ttu-id="6cbb5-114">이 정책 규칙의 hello 리소스 ID와 기본 제공 된 정책 정의로 제공 됩니다. `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-114">This policy rule is also available as a built-in policy definition with hello resource ID of `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cbb5-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6cbb5-115">Next steps</span></span>
* <span data-ttu-id="6cbb5-116">한 정책 규칙 (에서처럼 앞 예제는 hello)를 정의한 후 toocreate hello 정책 정의 필요 하 고 tooa 범위 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-116">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="6cbb5-117">구독, 리소스 그룹 또는 리소스 hello 범위 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-117">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="6cbb5-118">hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-118">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="6cbb5-119">REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-119">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="6cbb5-120">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6cbb5-120">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

