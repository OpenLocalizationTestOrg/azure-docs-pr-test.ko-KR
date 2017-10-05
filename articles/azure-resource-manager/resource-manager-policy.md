---
title: "Azure 리소스 정책 | Microsoft Docs"
description: "Azure Resource Manager 정책을 사용하여 배포하는 동안 일관된 리소스 속성을 설정했는지 확인하는 방법에 대해 설명합니다. 구독 또는 리소스 그룹에 정책을 적용할 수 있습니다."
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
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="cc712-104">리소스 정책 개요</span><span class="sxs-lookup"><span data-stu-id="cc712-104">Resource policy overview</span></span>
<span data-ttu-id="cc712-105">리소스 정책을 사용하면 조직에서 리소스에 대한 규칙을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="cc712-106">규칙을 정의하여 비용을 제어하고 리소스를 보다 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="cc712-107">예를 들어, 특정 유형의 가상 컴퓨터만 허용되게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="cc712-108">또는 모든 리소스가 특정 태그를 갖도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="cc712-109">정책은 모든 자식 리소스에 의해 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="cc712-110">이에 따라 리소스 그룹에 정책을 적용하면 해당 리소스 그룹의 모든 리소스에 해당 정책을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="cc712-111">정책에 대해 이해하기 위한 두 가지 개념이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="cc712-112">정책 정의 - 정책이 적용되는 시점 및 수행할 작업을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="cc712-113">정책 할당 - 정책 정의를 범위(구독 또는 리소스 그룹)에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="cc712-114">이 항목은 정책 정의에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="cc712-115">정책 할당에 대한 자세한 내용은 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](resource-manager-policy-portal.md) 또는 [스크립트를 통해 리소스 정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="cc712-116">리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="cc712-117">현재 정책은 태그, 종류 및 위치를 지원하지 않는 리소스 종류(예: Microsoft.Resources/deployments)를 평가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="cc712-118">이 지원은 나중에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-118">This support will be added at a future time.</span></span> <span data-ttu-id="cc712-119">이전 버전과의 호환성 문제를 방지하기 위해 정책을 작성할 때 유형을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="cc712-120">예를 들어 형식을 지정하지 않은 태그 정책이 모든 형식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="cc712-121">여기서 태그를 지원하지 않는 중첩된 리소스가 있고 배포 리소스 형식을 정책 평가에 추가한 경우에는 템플릿 배포에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="cc712-122">RBAC(역할 기반 액세스 제어)와 어떻게 다르나요?</span><span class="sxs-lookup"><span data-stu-id="cc712-122">How is it different from RBAC?</span></span>
<span data-ttu-id="cc712-123">정책 및 RBAC(역할 기반 액세스 제어) 간에 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="cc712-124">RBAC는 다른 범위에 있는 **사용자** 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="cc712-125">예를 들어 사용자가 원하는 범위에서 리소스 그룹에 대한 참가자 역할에 추가됩니다. 따라서 사용자는 해당 리소스 그룹을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="cc712-126">정책은 배포하는 동안 **리소스** 속성에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="cc712-127">예를 들어, 정책을 통해 프로비전 가능한 리소스 유형을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="cc712-128">또는 리소스를 프로비전할 수 있는 위치를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="cc712-129">RBAC와는 달리 정책은 기본적으로 허용 및 명시적 거부 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="cc712-130">사용자는 RBAC를 통해 인증되어야 정책을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="cc712-131">구체적으로 사용자 계정에는 다음 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="cc712-132">정책을 정의할 수 있는 `Microsoft.Authorization/policydefinitions/write` 사용 권한</span><span class="sxs-lookup"><span data-stu-id="cc712-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="cc712-133">정책을 할당할 수 있는 `Microsoft.Authorization/policyassignments/write` 사용 권한</span><span class="sxs-lookup"><span data-stu-id="cc712-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="cc712-134">이러한 사용 권한은 **참가자** 역할에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="cc712-135">기본 제공 정책</span><span class="sxs-lookup"><span data-stu-id="cc712-135">Built-in policies</span></span>

<span data-ttu-id="cc712-136">Azure에서는 일부 기본 제공 정책 정의을 제공하여 정의해야 하는 정책의 수를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="cc712-137">정책 정의를 진행하기 전에 기본 제공 정책에서 필요한 정의를 이미 제공하는지 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="cc712-138">기본 제공 정책은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="cc712-139">허용되는 위치</span><span class="sxs-lookup"><span data-stu-id="cc712-139">Allowed locations</span></span>
* <span data-ttu-id="cc712-140">허용되는 리소스 유형</span><span class="sxs-lookup"><span data-stu-id="cc712-140">Allowed resource types</span></span>
* <span data-ttu-id="cc712-141">허용되는 저장소 계정 SKU</span><span class="sxs-lookup"><span data-stu-id="cc712-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="cc712-142">허용되는 가상 컴퓨터 SKU</span><span class="sxs-lookup"><span data-stu-id="cc712-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="cc712-143">태그 및 기본값 적용</span><span class="sxs-lookup"><span data-stu-id="cc712-143">Apply tag and default value</span></span>
* <span data-ttu-id="cc712-144">태그 및 값 적용</span><span class="sxs-lookup"><span data-stu-id="cc712-144">Enforce tag and value</span></span>
* <span data-ttu-id="cc712-145">허용되지 않는 리소스 종류</span><span class="sxs-lookup"><span data-stu-id="cc712-145">Not allowed resource types</span></span>
* <span data-ttu-id="cc712-146">SQL Server 버전 12.0 필요</span><span class="sxs-lookup"><span data-stu-id="cc712-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="cc712-147">저장소 계정 암호화 필요</span><span class="sxs-lookup"><span data-stu-id="cc712-147">Require storage account encryption</span></span>

<span data-ttu-id="cc712-148">[포털](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell) 또는 [Azure CLI](resource-manager-policy-create-assign.md#azure-cli)를 통해 이러한 정책을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="cc712-149">정책 정의 구조</span><span class="sxs-lookup"><span data-stu-id="cc712-149">Policy definition structure</span></span>
<span data-ttu-id="cc712-150">JSON을 사용하여 정책 정의를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="cc712-151">정책 정의에는 다음 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="cc712-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cc712-152">parameters</span></span>
* <span data-ttu-id="cc712-153">표시 이름</span><span class="sxs-lookup"><span data-stu-id="cc712-153">display name</span></span>
* <span data-ttu-id="cc712-154">description</span><span class="sxs-lookup"><span data-stu-id="cc712-154">description</span></span>
* <span data-ttu-id="cc712-155">정책 규칙</span><span class="sxs-lookup"><span data-stu-id="cc712-155">policy rule</span></span>
  * <span data-ttu-id="cc712-156">논리 평가</span><span class="sxs-lookup"><span data-stu-id="cc712-156">logical evaluation</span></span>
  * <span data-ttu-id="cc712-157">영향</span><span class="sxs-lookup"><span data-stu-id="cc712-157">effect</span></span>

<span data-ttu-id="cc712-158">다음 예제에서는 리소스가 배포되는 위치를 제한하는 정책을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="cc712-159">매개 변수</span><span class="sxs-lookup"><span data-stu-id="cc712-159">Parameters</span></span>
<span data-ttu-id="cc712-160">매개 변수의 사용은 정책 정의의 수를 줄여 정책 관리를 간소화하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="cc712-161">리소스 속성에 대한 정책을 정의하고(예: 리소스를 배포할 수 있는 위치 제한) 정의에 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="cc712-162">그런 다음 정책을 할당할 때 다른 값(예: 구독에 한 가지 일련의 위치 지정)을 전달하여 다양한 시나리오에 대한 정책 정의를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="cc712-163">정책 정의 만들 때 매개 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="cc712-164">매개 변수의 형식은 문자열 또는 배열이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="cc712-165">메타데이터 속성은 Azure Portal과 같은 도구에 사용되어 사용자 친화적 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="cc712-166">정책 규칙에서 다음 구문을 사용하여 매개 변수를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="cc712-167">표시 이름 및 설명</span><span class="sxs-lookup"><span data-stu-id="cc712-167">Display name and description</span></span>

<span data-ttu-id="cc712-168">**displayName** 및 **설명**을 사용하여 정책 정의를 식별하고 사용하는 시기에 대한 컨텍스트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="cc712-169">정책 규칙</span><span class="sxs-lookup"><span data-stu-id="cc712-169">Policy rule</span></span>

<span data-ttu-id="cc712-170">정책 규칙은 **If** 및 **Then** 블록으로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="cc712-171">**If** 블록에서 정책이 적용되는 시점을 지정하는 하나 이상의 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="cc712-172">이러한 조건에 논리 연산자를 적용하여 정책에 대한 시나리오를 정확하게 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="cc712-173">**Then** 블록에서 **If** 조건이 충족된 경우에 발생하는 효과를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="cc712-174">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="cc712-174">Logical operators</span></span>
<span data-ttu-id="cc712-175">지원되는 논리 연산자는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="cc712-176">**not** 구문은 조건의 결과를 반전시킵니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="cc712-177">**allOf** 구문(논리 **And** 작업과 비슷함)은 모든 조건이 true여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="cc712-178">**anyOf** 구문(논리 **Or** 작업과 비슷함)은 하나 이상의 조건이 true여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="cc712-179">논리 연산자를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-179">You can nest logical operators.</span></span> <span data-ttu-id="cc712-180">다음 예제에서는 **allOf** 작업 내에 중첩된 **not** 작업을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="cc712-181">조건</span><span class="sxs-lookup"><span data-stu-id="cc712-181">Conditions</span></span>
<span data-ttu-id="cc712-182">조건은 **field**에서 특정 기준을 충족하는지를 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="cc712-183">지원되는 조건은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="cc712-184">**like** 조건을 사용하는 경우 값에 와일드카드(*)를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="cc712-185">**match** 조건을 사용하는 경우 자릿수 하나를 나타내려면 `#`를, 문자 하나를 나타내려면 `?`를, 해당 실제 문자를 나타내려면 다른 모든 문자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="cc712-186">관련 예제는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="cc712-187">필드</span><span class="sxs-lookup"><span data-stu-id="cc712-187">Fields</span></span>
<span data-ttu-id="cc712-188">조건은 필드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="cc712-189">필드는 리소스의 상태를 설명하는 데 사용되는 리소스 요청 페이로드의 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="cc712-190">다음 필드가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="cc712-191">속성 별칭 - 목록은 [별칭](#aliases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="cc712-192">결과</span><span class="sxs-lookup"><span data-stu-id="cc712-192">Effect</span></span>
<span data-ttu-id="cc712-193">정책은 `deny`, `audit` 및 `append`이라는 세 가지 종류의 효과를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="cc712-194">**거부**는 감사 로그에 이벤트를 생성하고 요청을 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="cc712-195">**감사**는 감사 로그에 경고 이벤트를 생성하지만 요청을 실패하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="cc712-196">**추가**는 정의된 필드 집합을 요청에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="cc712-197">**append**의 경우 아래와 같이 details(세부 정보)를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="cc712-198">값은 문자열 또는 JSON 형식의 개체일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="cc712-199">Aliases</span><span class="sxs-lookup"><span data-stu-id="cc712-199">Aliases</span></span>

<span data-ttu-id="cc712-200">리소스 유형에 대한 특정 속성에 액세스하려면 속성 별칭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="cc712-201">별칭을 사용하면 리소스의 속성에 허용되는 값이나 조건을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="cc712-202">각 별칭은 주어진 리소스 유형에 대해 서로 다른 API 버전의 경로에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="cc712-203">정책 평가 중에 정책 엔진은 해당 API 버전에 대한 속성 경로를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="cc712-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="cc712-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="cc712-205">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-205">Alias</span></span> | <span data-ttu-id="cc712-206">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="cc712-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="cc712-208">비-ssl Redis 서버 포트(6379)가 사용하도록 설정되었는지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="cc712-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="cc712-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="cc712-210">프리미엄 클러스터 캐시에 만들 분할된 데이터베이스 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="cc712-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="cc712-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="cc712-212">배포할 Redis Cache의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="cc712-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="cc712-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="cc712-214">사용할 SKU 제품군을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="cc712-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="cc712-216">배포할 Redis Cache 유형을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="cc712-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="cc712-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="cc712-218">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-218">Alias</span></span> | <span data-ttu-id="cc712-219">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="cc712-221">가격 책정 계층의 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="cc712-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="cc712-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="cc712-223">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-223">Alias</span></span> | <span data-ttu-id="cc712-224">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="cc712-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="cc712-226">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지 제안을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="cc712-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="cc712-228">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 게시자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="cc712-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="cc712-230">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 SKU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="cc712-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="cc712-232">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="cc712-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="cc712-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="cc712-234">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-234">Alias</span></span> | <span data-ttu-id="cc712-235">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="cc712-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="cc712-237">가상 컴퓨터를 만드는 데 사용되는 이미지의 식별자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="cc712-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="cc712-239">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지 제안을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="cc712-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="cc712-241">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 게시자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="cc712-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="cc712-243">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 SKU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="cc712-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="cc712-245">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="cc712-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="cc712-247">온-프레미스로 사용이 허가된 이미지 또는 디스크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="cc712-248">이 값은 Windows Server 운영 체제를 포함하는 이미지에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="cc712-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="cc712-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="cc712-250">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지 제안을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="cc712-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="cc712-252">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 게시자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="cc712-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="cc712-254">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 SKU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="cc712-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="cc712-256">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="cc712-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="cc712-258">Vhd URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="cc712-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="cc712-260">가상 컴퓨터의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="cc712-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="cc712-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="cc712-262">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-262">Alias</span></span> | <span data-ttu-id="cc712-263">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="cc712-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="cc712-265">확장의 게시자 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="cc712-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="cc712-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="cc712-267">확장 유형을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-267">Set the type of extension.</span></span> |
| <span data-ttu-id="cc712-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="cc712-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="cc712-269">확장 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-269">Set the version of the extension.</span></span> |

<span data-ttu-id="cc712-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="cc712-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="cc712-271">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-271">Alias</span></span> | <span data-ttu-id="cc712-272">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="cc712-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="cc712-274">가상 컴퓨터를 만드는 데 사용되는 이미지의 식별자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="cc712-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="cc712-276">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지 제안을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="cc712-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="cc712-278">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 게시자를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="cc712-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="cc712-280">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 SKU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="cc712-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="cc712-282">플랫폼 이미지 또는 가상 컴퓨터를 만드는 데 사용된 Marketplace 이미지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="cc712-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="cc712-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="cc712-284">온-프레미스로 사용이 허가된 이미지 또는 디스크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="cc712-285">이 값은 Windows Server 운영 체제를 포함하는 이미지에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="cc712-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="cc712-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="cc712-287">확장 집합에서 모든 가상 컴퓨터에 대해 컴퓨터 이름 접두사를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="cc712-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="cc712-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="cc712-289">사용자 이미지에 대한 Blob URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="cc712-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="cc712-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="cc712-291">확장 집합에 대한 운영 체제 디스크를 저장하는 데 사용되는 컨테이너 URL을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="cc712-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="cc712-293">확장 집합에서 가상 컴퓨터 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="cc712-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="cc712-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="cc712-295">확장 집합에서 가상 컴퓨터 계층을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="cc712-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="cc712-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="cc712-297">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-297">Alias</span></span> | <span data-ttu-id="cc712-298">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="cc712-300">게이트웨이의 크기를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="cc712-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="cc712-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="cc712-302">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-302">Alias</span></span> | <span data-ttu-id="cc712-303">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="cc712-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="cc712-305">이 가상 네트워크 게이트웨이의 형식을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="cc712-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="cc712-307">게이트웨이 SKU 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="cc712-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="cc712-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="cc712-309">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-309">Alias</span></span> | <span data-ttu-id="cc712-310">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="cc712-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="cc712-312">서버 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-312">Set the version of the server.</span></span> |

<span data-ttu-id="cc712-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="cc712-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="cc712-314">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-314">Alias</span></span> | <span data-ttu-id="cc712-315">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="cc712-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="cc712-317">데이터베이스의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="cc712-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="cc712-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="cc712-319">데이터베이스가 들어 있는 탄력적 풀의 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="cc712-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="cc712-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="cc712-321">데이터베이스의 구성된 서비스 수준 목표 ID를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="cc712-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="cc712-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="cc712-323">데이터베이스의 구성된 서비스 수준 목표의 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="cc712-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="cc712-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="cc712-325">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-325">Alias</span></span> | <span data-ttu-id="cc712-326">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="cc712-327">servers/elasticpools</span></span> | <span data-ttu-id="cc712-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="cc712-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="cc712-329">탄력적 데이터베이스 풀에 대한 총 공유 DTU를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="cc712-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="cc712-330">servers/elasticpools</span></span> | <span data-ttu-id="cc712-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="cc712-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="cc712-332">탄력적 풀의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="cc712-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="cc712-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="cc712-334">Alias</span><span class="sxs-lookup"><span data-stu-id="cc712-334">Alias</span></span> | <span data-ttu-id="cc712-335">설명</span><span class="sxs-lookup"><span data-stu-id="cc712-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="cc712-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="cc712-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="cc712-337">청구에 사용되는 액세스 계층을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="cc712-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="cc712-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="cc712-339">SKU 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-339">Set the SKU name.</span></span> |
| <span data-ttu-id="cc712-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="cc712-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="cc712-341">서비스에서 데이터가 Blob Storage 서비스에 저장될 때 데이터를 암호화할지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="cc712-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="cc712-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="cc712-343">서비스에서 데이터가 File Storage 서비스에 저장될 때 데이터를 암호화할지 여부를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="cc712-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="cc712-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="cc712-345">SKU 이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-345">Set the SKU name.</span></span> |
| <span data-ttu-id="cc712-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="cc712-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="cc712-347">저장소 서비스에 https 트래픽만 허용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="cc712-348">정책 예제</span><span class="sxs-lookup"><span data-stu-id="cc712-348">Policy examples</span></span>

<span data-ttu-id="cc712-349">다음 항목에는 정책 예제가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="cc712-350">태그 정책의 예제는 [태그에 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="cc712-351">이름 지정 및 텍스트 패턴의 예는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="cc712-352">저장소 정책의 예제는 [저장소 계정에 리소스 정책 적용](resource-manager-policy-storage.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="cc712-353">가상 컴퓨터 정책의 예제는 [Linux VM에 리소스 정책 적용](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 및 [Windows VM에 리소스 정책 적용](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc712-354">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc712-354">Next steps</span></span>
* <span data-ttu-id="cc712-355">정책 규칙을 정의한 후에 범위에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="cc712-356">포털을 통해 정책을 할당하려면 [Azure Portal을 사용하여 리소스 정책 할당 및 관리](resource-manager-policy-portal.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="cc712-357">REST API, PowerShell 또는 Azure CLI를 통해 정책을 할당하려면 [스크립트를 통해 정책 할당 및 관리](resource-manager-policy-create-assign.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="cc712-358">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc712-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="cc712-359">정책 스키마는 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)에 게시되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc712-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

