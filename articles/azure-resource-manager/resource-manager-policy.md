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
# <a name="resource-policy-overview"></a><span data-ttu-id="de19f-104">리소스 정책 개요</span><span class="sxs-lookup"><span data-stu-id="de19f-104">Resource policy overview</span></span>
<span data-ttu-id="de19f-105">리소스 정책을 사용 하면 조직의 리소스에 대 한 tooestablish 규칙 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="de19f-106">규칙을 정의하여 비용을 제어하고 리소스를 보다 쉽게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="de19f-107">예를 들어, 특정 유형의 가상 컴퓨터만 허용되게 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="de19f-108">또는 모든 리소스가 특정 태그를 갖도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="de19f-109">정책은 모든 자식 리소스에 의해 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="de19f-110">따라서 정책이 적용 된 tooa 리소스 그룹와 된 경우 해당 리소스 그룹에서 적용 가능한 tooall hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="de19f-111">정책에 대 한 개념 toounderstand 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="de19f-112">hello 정책이 적용 되는 경우 고 어떤 작업 tootake 설명 정책 정의-</span><span class="sxs-lookup"><span data-stu-id="de19f-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="de19f-113">hello 정책 정의 tooa 범위 (구독 또는 리소스 그룹)를 적용 하면 정책 할당-</span><span class="sxs-lookup"><span data-stu-id="de19f-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="de19f-114">이 항목은 정책 정의에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="de19f-115">정책 할당에 대 한 정보를 참조 하십시오. [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md) 또는 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="de19f-116">리소스(PUT 및 PATCH 작업)를 만들고 업데이트할 때 정책이 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="de19f-117">현재 정책 태그, 종류 및 hello Microsoft.Resources/deployments 리소스 종류 등의 위치를 지원 하지 않는 리소스 종류를 평가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="de19f-118">이 지원은 나중에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-118">This support will be added at a future time.</span></span> <span data-ttu-id="de19f-119">tooavoid 이전 버전과 호환성 문제를 명시적으로 형식을 지정 해야 정책을 작성 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="de19f-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="de19f-120">예를 들어 형식을 지정하지 않은 태그 정책이 모든 형식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="de19f-121">이 경우 태그를 지원 하지 않는 중첩 리소스가 템플릿 배포 실패 하 고 hello 배포 리소스 유형이 toopolicy 평가 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="de19f-122">RBAC(역할 기반 액세스 제어)와 어떻게 다르나요?</span><span class="sxs-lookup"><span data-stu-id="de19f-122">How is it different from RBAC?</span></span>
<span data-ttu-id="de19f-123">정책 및 RBAC(역할 기반 액세스 제어) 간에 몇 가지 차이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="de19f-124">RBAC는 다른 범위에 있는 **사용자** 작업에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="de19f-125">예를 들어 toothat 리소스 그룹 변경 내용을 확인할 수 있도록 필요한 hello 범위, 리소스 그룹에 대 한 toohello 참가자 역할을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="de19f-126">정책은 배포하는 동안 **리소스** 속성에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="de19f-127">예를 들어, 정책을 통해 hello 유형의 프로 비전 할 수 있는 리소스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="de19f-128">또는 hello 리소스를 프로비저닝할 수 있는 hello 위치를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="de19f-129">RBAC와는 달리 정책은 기본적으로 허용 및 명시적 거부 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="de19f-130">toouse 정책을 RBAC를 통해 인증 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="de19f-131">구체적으로 사용자 계정에는 다음 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="de19f-132">`Microsoft.Authorization/policydefinitions/write`사용 권한 toodefine 정책</span><span class="sxs-lookup"><span data-stu-id="de19f-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="de19f-133">`Microsoft.Authorization/policyassignments/write`사용 권한 tooassign 정책</span><span class="sxs-lookup"><span data-stu-id="de19f-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="de19f-134">이러한 사용 권한은 hello에 포함 되지 않은 **참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="de19f-135">기본 제공 정책</span><span class="sxs-lookup"><span data-stu-id="de19f-135">Built-in policies</span></span>

<span data-ttu-id="de19f-136">Hello 수를 줄일 수 있는 몇 가지 기본 제공 된 정책 정의 제공 하는 azure toodefine 정책의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="de19f-137">정책 정의를 계속 하기 전에 기본 제공 된 정책에서 이미 필요한 hello 정의 제공 하는지 여부를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="de19f-138">hello 기본 제공 정책 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="de19f-139">허용되는 위치</span><span class="sxs-lookup"><span data-stu-id="de19f-139">Allowed locations</span></span>
* <span data-ttu-id="de19f-140">허용되는 리소스 유형</span><span class="sxs-lookup"><span data-stu-id="de19f-140">Allowed resource types</span></span>
* <span data-ttu-id="de19f-141">허용되는 저장소 계정 SKU</span><span class="sxs-lookup"><span data-stu-id="de19f-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="de19f-142">허용되는 가상 컴퓨터 SKU</span><span class="sxs-lookup"><span data-stu-id="de19f-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="de19f-143">태그 및 기본값 적용</span><span class="sxs-lookup"><span data-stu-id="de19f-143">Apply tag and default value</span></span>
* <span data-ttu-id="de19f-144">태그 및 값 적용</span><span class="sxs-lookup"><span data-stu-id="de19f-144">Enforce tag and value</span></span>
* <span data-ttu-id="de19f-145">허용되지 않는 리소스 종류</span><span class="sxs-lookup"><span data-stu-id="de19f-145">Not allowed resource types</span></span>
* <span data-ttu-id="de19f-146">SQL Server 버전 12.0 필요</span><span class="sxs-lookup"><span data-stu-id="de19f-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="de19f-147">저장소 계정 암호화 필요</span><span class="sxs-lookup"><span data-stu-id="de19f-147">Require storage account encryption</span></span>

<span data-ttu-id="de19f-148">Hello 통해 이러한 정책 중 하나를 지정할 수 있습니다 [포털](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), 또는 [Azure CLI](resource-manager-policy-create-assign.md#azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="de19f-149">정책 정의 구조</span><span class="sxs-lookup"><span data-stu-id="de19f-149">Policy definition structure</span></span>
<span data-ttu-id="de19f-150">JSON toocreate 정책 정의 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="de19f-151">hello 정책 정의 대 한 요소가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="de19f-152">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de19f-152">parameters</span></span>
* <span data-ttu-id="de19f-153">표시 이름</span><span class="sxs-lookup"><span data-stu-id="de19f-153">display name</span></span>
* <span data-ttu-id="de19f-154">description</span><span class="sxs-lookup"><span data-stu-id="de19f-154">description</span></span>
* <span data-ttu-id="de19f-155">정책 규칙</span><span class="sxs-lookup"><span data-stu-id="de19f-155">policy rule</span></span>
  * <span data-ttu-id="de19f-156">논리 평가</span><span class="sxs-lookup"><span data-stu-id="de19f-156">logical evaluation</span></span>
  * <span data-ttu-id="de19f-157">영향</span><span class="sxs-lookup"><span data-stu-id="de19f-157">effect</span></span>

<span data-ttu-id="de19f-158">다음 예제는 hello 리소스가 배포 되는 위치를 제한 하는 정책을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-158">hello following example shows a policy that limits where resources are deployed:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="de19f-159">매개 변수</span><span class="sxs-lookup"><span data-stu-id="de19f-159">Parameters</span></span>
<span data-ttu-id="de19f-160">매개 변수를 사용 하 여 정책 정의의 hello 수를 줄여서 정책 관리를 간소화 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="de19f-161">리소스 속성 (예: hello 위치 리소스를 배포할 수 있는 제한)에 대 한 정책을 정의 하 고 hello 정의에 매개 변수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="de19f-162">그런 다음 다시 사용할 있습니다 다양 한 시나리오에 대 한 정책 정의 다른 값 (예: 하나의 집합 구독에 대 한 위치 지정)를에서 전달 하 여 때 hello 정책을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="de19f-163">정책 정의 만들 때 매개 변수를 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-163">You declare parameters when you create policy definitions.</span></span>

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

<span data-ttu-id="de19f-164">hello 형식의 매개 변수는 문자열 또는 배열 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="de19f-165">hello 메타 데이터 속성은 Azure 포털 toodisplay 사용자에 게 친숙 정보와 같은 도구에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="de19f-166">Hello 정책 규칙 구문 다음 hello로 매개 변수를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="de19f-167">표시 이름 및 설명</span><span class="sxs-lookup"><span data-stu-id="de19f-167">Display name and description</span></span>

<span data-ttu-id="de19f-168">Hello를 사용 하 여 **displayName** 및 **설명** tooidentify hello 정책 정의 및 사용 하는 경우에 대 한 컨텍스트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="de19f-169">정책 규칙</span><span class="sxs-lookup"><span data-stu-id="de19f-169">Policy rule</span></span>

<span data-ttu-id="de19f-170">hello 정책 규칙 이루어져 **경우** 및 **다음** 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="de19f-171">Hello에 **경우** 블록 hello 정책 적용 되는 시점을 지정 하는 하나 이상의 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="de19f-172">논리 연산자 toothese 조건을 적용할 수 있습니다 tooprecisely 정책에 대 한 hello 시나리오를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="de19f-173">Hello에 **다음** 블록 하면 hello 나타나는 hello 효과 정의 **경우** 조건이 충족 되는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="de19f-174">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="de19f-174">Logical operators</span></span>
<span data-ttu-id="de19f-175">지원 되는 hello 논리 연산자는:</span><span class="sxs-lookup"><span data-stu-id="de19f-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="de19f-176">hello **하지** 구문 hello 조건의 hello 결과 반전 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="de19f-177">hello **allOf** 구문 (유사한 toohello 논리 **및** 작업) 모든 조건 toobe true 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="de19f-178">hello **anyOf** 구문 (유사한 toohello 논리 **또는** 작업) 하나 이상의 조건 toobe true 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="de19f-179">논리 연산자를 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-179">You can nest logical operators.</span></span> <span data-ttu-id="de19f-180">다음 예제와 hello는 **하지** 내에 중첩 된 작업은 **allOf** 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="de19f-181">조건</span><span class="sxs-lookup"><span data-stu-id="de19f-181">Conditions</span></span>
<span data-ttu-id="de19f-182">hello i o n 여부는 **필드** 특정 기준을 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="de19f-183">지원 되는 hello 조건이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="de19f-184">Hello를 사용 하는 경우 **같은** 조건 hello 값에 와일드 카드 (*)를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="de19f-185">Hello를 사용 하는 경우 **일치** 조건의 경우 제공 `#` toorepresent \d `?` 는 문자, 및 기타 toorepresent 실제 문자를 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="de19f-186">관련 예제는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de19f-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="de19f-187">필드</span><span class="sxs-lookup"><span data-stu-id="de19f-187">Fields</span></span>
<span data-ttu-id="de19f-188">조건은 필드를 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="de19f-189">필드 hello 리소스 요청 페이로드에서 속성을 나타내는 hello 리소스의 즉 사용 되는 toodescribe hello 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="de19f-190">다음 필드는 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="de19f-191">속성 별칭 - 목록은 [별칭](#aliases)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de19f-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="de19f-192">결과</span><span class="sxs-lookup"><span data-stu-id="de19f-192">Effect</span></span>
<span data-ttu-id="de19f-193">정책은 `deny`, `audit` 및 `append`이라는 세 가지 종류의 효과를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="de19f-194">**거부** hello 감사 로그에서 이벤트를 생성 하 고 hello 요청 실패</span><span class="sxs-lookup"><span data-stu-id="de19f-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="de19f-195">**감사** 감사 로그에 경고 이벤트를 생성 하지만 hello 요청에 실패 하지 않습니다</span><span class="sxs-lookup"><span data-stu-id="de19f-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="de19f-196">**추가** 필드 toohello 요청의 hello 정의 집합에 추가</span><span class="sxs-lookup"><span data-stu-id="de19f-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="de19f-197">에 대 한 **추가**, hello 다음 세부 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="de19f-198">문자열 또는 JSON 형식 개체 hello 값일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="de19f-199">Aliases</span><span class="sxs-lookup"><span data-stu-id="de19f-199">Aliases</span></span>

<span data-ttu-id="de19f-200">리소스 종류에 대 한 속성 별칭 tooaccess 특정 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="de19f-201">별칭을 사용 하면 리소스에는 속성에 허용 되는 값 또는 조건이 무엇 toorestrict 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="de19f-202">각 별칭 toopaths가 주어진된 리소스 종류에 대해 다른 API 버전에 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="de19f-203">정책 평가 도중 hello 정책 엔진은 해당 API 버전에 대 한 hello 속성 경로를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="de19f-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="de19f-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="de19f-205">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-205">Alias</span></span> | <span data-ttu-id="de19f-206">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="de19f-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="de19f-208">설정 여부 hello 비 ssl Redis 서버 포트 (6379)은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="de19f-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="de19f-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="de19f-210">프리미엄 캐시 클러스터에 만든 분할 영역 toobe hello 수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="de19f-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="de19f-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="de19f-212">Hello Redis 캐시 toodeploy hello 크기를 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="de19f-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="de19f-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="de19f-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="de19f-214">Hello SKU 제품군 toouse를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="de19f-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="de19f-216">Redis Cache toodeploy hello 형식을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="de19f-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="de19f-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="de19f-218">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-218">Alias</span></span> | <span data-ttu-id="de19f-219">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="de19f-221">Hello 이름 hello 가격 책정 계층으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="de19f-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="de19f-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="de19f-223">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-223">Alias</span></span> | <span data-ttu-id="de19f-224">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="de19f-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="de19f-226">Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="de19f-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="de19f-228">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="de19f-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="de19f-230">Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="de19f-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="de19f-232">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="de19f-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="de19f-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="de19f-234">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-234">Alias</span></span> | <span data-ttu-id="de19f-235">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="de19f-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="de19f-237">Hello 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 식별자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="de19f-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="de19f-239">Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="de19f-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="de19f-241">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="de19f-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="de19f-243">Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="de19f-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="de19f-245">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="de19f-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="de19f-247">Hello 이미지 또는 디스크 사용이 허가 된 온-프레미스 인지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="de19f-248">이 값은 hello Windows Server 운영 체제에 포함 된 이미지에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="de19f-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="de19f-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="de19f-250">Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="de19f-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="de19f-252">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="de19f-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="de19f-254">Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="de19f-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="de19f-256">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="de19f-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="de19f-258">Hello vhd URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="de19f-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="de19f-260">Hello 가상 컴퓨터의 hello 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="de19f-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="de19f-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="de19f-262">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-262">Alias</span></span> | <span data-ttu-id="de19f-263">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="de19f-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="de19f-265">Hello hello 확장의 게시자 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="de19f-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="de19f-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="de19f-267">확장의 hello 유형을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="de19f-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="de19f-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="de19f-269">Hello hello 확장 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="de19f-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="de19f-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="de19f-271">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-271">Alias</span></span> | <span data-ttu-id="de19f-272">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="de19f-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="de19f-274">Hello 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 식별자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="de19f-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="de19f-276">Hello 플랫폼 이미지 또는 마켓플레이스 이미지의 집합 hello 제공 toocreate hello 가상 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="de19f-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="de19f-278">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 게시자를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="de19f-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="de19f-280">Hello hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 SKU를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="de19f-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="de19f-282">Hello 플랫폼 이미지 또는 마켓플레이스에서 사용 되는 이미지 toocreate hello 가상 컴퓨터의 hello 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="de19f-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="de19f-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="de19f-284">Hello 이미지 또는 디스크 사용이 허가 된 온-프레미스 인지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="de19f-285">이 값은 hello Windows Server 운영 체제에 포함 된 이미지에만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="de19f-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="de19f-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="de19f-287">Hello 크기 집합의 모든 hello 가상 컴퓨터에 대 한 hello 컴퓨터 이름 접두사를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="de19f-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="de19f-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="de19f-289">사용자 이미지에 대 한 hello blob URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="de19f-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="de19f-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="de19f-291">Hello 크기 집합에 대 한 운영 체제 디스크를 사용 하는 toostore 있는 hello 컨테이너 Url을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="de19f-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="de19f-293">크기 집합의 가상 컴퓨터의 hello 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="de19f-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="de19f-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="de19f-295">크기 집합의 가상 컴퓨터의 hello 계층을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="de19f-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="de19f-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="de19f-297">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-297">Alias</span></span> | <span data-ttu-id="de19f-298">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="de19f-300">Hello 게이트웨이의 hello 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="de19f-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="de19f-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="de19f-302">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-302">Alias</span></span> | <span data-ttu-id="de19f-303">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="de19f-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="de19f-305">이 가상 네트워크 게이트웨이의 hello 유형을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="de19f-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="de19f-307">Hello 게이트웨이 SKU 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="de19f-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="de19f-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="de19f-309">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-309">Alias</span></span> | <span data-ttu-id="de19f-310">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="de19f-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="de19f-312">Hello 버전의 hello 서버를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="de19f-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="de19f-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="de19f-314">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-314">Alias</span></span> | <span data-ttu-id="de19f-315">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="de19f-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="de19f-317">Hello hello 데이터베이스 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="de19f-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="de19f-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="de19f-319">Hello 탄력적인 풀 hello 데이터베이스의 hello 이름이 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="de19f-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="de19f-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="de19f-321">Hello 구성 된 서비스 수준 목표의 ID hello 데이터베이스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="de19f-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="de19f-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="de19f-323">구성 된 hello hello 데이터베이스의 서비스 수준 목표의 hello 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="de19f-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="de19f-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="de19f-325">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-325">Alias</span></span> | <span data-ttu-id="de19f-326">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="de19f-327">servers/elasticpools</span></span> | <span data-ttu-id="de19f-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="de19f-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="de19f-329">집합 hello 총 hello 데이터베이스 탄력적 풀에 대 한 DTU를 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="de19f-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="de19f-330">servers/elasticpools</span></span> | <span data-ttu-id="de19f-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="de19f-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="de19f-332">Hello 탄력적 풀의 hello 버전을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="de19f-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="de19f-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="de19f-334">Alias</span><span class="sxs-lookup"><span data-stu-id="de19f-334">Alias</span></span> | <span data-ttu-id="de19f-335">설명</span><span class="sxs-lookup"><span data-stu-id="de19f-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="de19f-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="de19f-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="de19f-337">청구에 사용 되는 집합 hello 액세스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="de19f-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="de19f-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="de19f-339">Hello SKU 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="de19f-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="de19f-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="de19f-341">Hello 서비스는 hello blob 저장소 서비스에 저장 된 hello 데이터를 암호화 하는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="de19f-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="de19f-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="de19f-343">Hello 서비스는 hello 파일 저장소 서비스에 저장 된 hello 데이터를 암호화 하는지 여부를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="de19f-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="de19f-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="de19f-345">Hello SKU 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="de19f-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="de19f-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="de19f-347">Tooallow만 https 트래픽 toostorage 서비스를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="de19f-348">정책 예제</span><span class="sxs-lookup"><span data-stu-id="de19f-348">Policy examples</span></span>

<span data-ttu-id="de19f-349">다음 항목 hello 정책 예가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="de19f-350">태그 정책의 예제는 [태그에 리소스 정책 적용](resource-manager-policy-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de19f-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="de19f-351">이름 지정 및 텍스트 패턴의 예는 [이름 및 텍스트에 대한 리소스 정책 적용](resource-manager-policy-naming-convention.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="de19f-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="de19f-352">정책 저장소의 예 참조 [리소스 정책 toostorage 계정 적용](resource-manager-policy-storage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="de19f-353">가상 컴퓨터 정책의 예 참조 [리소스 정책 tooLinux Vm 적용](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) 및 [리소스 정책 tooWindows Vm 적용](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="de19f-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="de19f-354">다음 단계</span><span class="sxs-lookup"><span data-stu-id="de19f-354">Next steps</span></span>
* <span data-ttu-id="de19f-355">정책 규칙을 정의한 후 tooa 범위를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="de19f-356">hello 포털을 통해 tooassign 정책 참조 [사용 하 여 Azure 포털 tooassign 리소스 정책을 관리 하 고](resource-manager-policy-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="de19f-357">REST API, PowerShell 또는 Azure CLI를 통해 tooassign 정책을 참조 [지정 하 고 스크립트를 통해 정책을 관리할](resource-manager-policy-create-assign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="de19f-358">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="de19f-359">에 hello 정책 스키마를 게시 [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="de19f-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

