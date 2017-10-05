---
title: "태그에 대한 Azure 리소스 정책 | Microsoft Docs"
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
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="a1fcb-103">태그에 대한 리소스 정책 적용</span><span class="sxs-lookup"><span data-stu-id="a1fcb-103">Apply resource policies for tags</span></span>

<span data-ttu-id="a1fcb-104">이 항목에서는 리소스에서 태그의 일관된 사용을 확인하는 데 적용할 수 있는 일반적인 정책 규칙을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="a1fcb-105">기존 리소스를 사용하는 리소스 그룹 또는 구독에 태그 정책을 적용하면 해당 리소스에 정책을 소급 적용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="a1fcb-106">해당 리소스에 대한 정책을 적용하려면 기존 리소스에 대한 업데이트를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="a1fcb-107">이 문서는 업데이트를 트리거하기 위해 PowerShell 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="a1fcb-108">리소스 그룹의 모든 리소스에 태그/값이 있는지 확인</span><span class="sxs-lookup"><span data-stu-id="a1fcb-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="a1fcb-109">일반적으로 리소스 그룹의 모든 리소스에 특정 태그 및 값이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="a1fcb-110">이 요구 사항은 부서별로 비용을 추적하는 데 종종 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="a1fcb-111">다음 조건이 충족되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-111">The following conditions must be met:</span></span>

* <span data-ttu-id="a1fcb-112">필수 태그 및 값은 태그가 없는 신규 및 업데이트된 리소스에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="a1fcb-113">기존 리소스에서 필수 태그 및 값을 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="a1fcb-114">두 가지 기본 제공 정책을 리소스 그룹에 적용하여 이 요구 사항을 달성합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="a1fcb-115">ID</span><span class="sxs-lookup"><span data-stu-id="a1fcb-115">ID</span></span> | <span data-ttu-id="a1fcb-116">설명</span><span class="sxs-lookup"><span data-stu-id="a1fcb-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="a1fcb-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="a1fcb-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="a1fcb-118">사용자가 지정하지 않으면 필수 태그와 해당 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="a1fcb-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="a1fcb-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="a1fcb-120">필수 태그와 해당 값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="a1fcb-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1fcb-121">PowerShell</span></span>

<span data-ttu-id="a1fcb-122">다음 PowerShell 스크립트는 리소스 그룹에 두 가지 기본 제공 정책 정의를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="a1fcb-123">스크립트를 실행하기 전에 리소스 그룹에 모든 필수 태그를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="a1fcb-124">리소스 그룹의 각 태그는 그룹에 있는 리소스에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="a1fcb-125">사용자 구독의 모든 리소스 그룹에 할당하려면 리소스 그룹을 가져올 때 `-Name` 매개 변수를 제공하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

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

<span data-ttu-id="a1fcb-126">정책을 할당한 후에는 모든 기존 리소스에 업데이트를 트리거하여 추가한 태그 정책을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="a1fcb-127">다음 스크립트는 리소스에 존재하는 다른 태그를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-127">The following script retains any other tags that existed on the resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="a1fcb-128">리소스 유형에 대한 태그 요구</span><span class="sxs-lookup"><span data-stu-id="a1fcb-128">Require tags for a resource type</span></span>
<span data-ttu-id="a1fcb-129">아래 예제에서는 특정 리소스 유형(이 경우, 저장소 계정)에만 응용 프로그램 태그를 요구하도록 논리 연산자를 중첩하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="a1fcb-130">태그 요구</span><span class="sxs-lookup"><span data-stu-id="a1fcb-130">Require tag</span></span>
<span data-ttu-id="a1fcb-131">아래 정책은 "costCenter" 키(모든 값을 적용할 수 있음)를 포함하고 있는 태그가 없는 요청을 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a1fcb-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1fcb-132">Next steps</span></span>
* <span data-ttu-id="a1fcb-133">앞의 예제와 표시된 바와 같이 정책 규칙을 정의한 후에는 정책 정의를 만들고 범위에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="a1fcb-134">범위는 구독, 리소스 그룹 또는 리소스일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="a1fcb-135">포털을 통해 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="a1fcb-136">REST API, PowerShell 또는 Azure CLI를 통해 정책을 할당하려면 [스크립트를 통해 정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="a1fcb-137">리소스 정책에 대한 소개는 [리소스 정책 개요](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="a1fcb-138">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a1fcb-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

