---
title: "Azure 템플릿에 자식 리소스 정의 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 자식 리소스의 리소스 유형 및 이름을 설정하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="98de4-103">Resource Manager 템플릿에서 자식 리소스의 이름 및 유형 설정</span><span class="sxs-lookup"><span data-stu-id="98de4-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="98de4-104">템플릿을 만들 때는 부모 리소스와 관련된 자식 리소스를 포함해야 하는 경우가 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="98de4-105">예를 들어 템플릿에 SQL Server 및 데이터베이스가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="98de4-106">SQL Server는 부모 리소스이며 데이터베이스는 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="98de4-107">자식 리소스 유형의 형식은 다음과 같습니다. `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="98de4-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="98de4-108">자식 리소스 이름의 형식은 다음과 같습니다. `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="98de4-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="98de4-109">그러나 부모 리소스 내에 중첩되어 있는지, 자체적으로 최상위 수준에 있는지에 따라 템플릿에 종류와 이름을 다르게 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="98de4-110">이 항목에서는 두 가지 방법을 처리하는 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="98de4-111">리소스에 대한 정규화된 참조를 생성할 때 형식과 이름으로 세그먼트를 결합하는 순서는 단순히 두 항목의 연결이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="98de4-112">대신, 네임스페이스 뒤에 구체성이 낮은 순으로 *형식/이름* 쌍의 시퀀스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="98de4-113">예:</span><span class="sxs-lookup"><span data-stu-id="98de4-113">For example:</span></span>

<span data-ttu-id="98de4-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`는 올바릅니다. `Microsoft.Compute/virtualMachines/extensions/myVM/myExt`는 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="98de4-115">중첩된 자식 리소스</span><span class="sxs-lookup"><span data-stu-id="98de4-115">Nested child resource</span></span>
<span data-ttu-id="98de4-116">자식 리소스를 정의하는 가장 쉬운 방법은 부모 리소스 내에 중첩시키는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="98de4-117">다음 예제에서는 SQL Server 내에 중첩된 SQL Database를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="98de4-118">자식 리소스의 유형은 `databases`로 설정되지만 전체 리소스 유형은 `Microsoft.Sql/servers/databases`입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="98de4-119">`Microsoft.Sql/servers/`는 입력하지 않습니다. 부모 리소스 유형에서 유추되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="98de4-120">자식 리소스 이름은 `exampledatabase`로 설정되지만 전체 이름에는 부모 이름이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="98de4-121">`exampleserver`는 입력하지 않습니다. 부모 리소스에서 유추되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="98de4-122">최상위 자식 리소스</span><span class="sxs-lookup"><span data-stu-id="98de4-122">Top-level child resource</span></span>
<span data-ttu-id="98de4-123">최상위 수준에 자식 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="98de4-124">부모 리소스가 동일한 템플릿에 배포되지 않은 경우 `copy`를 사용하여 여러 자식 리소스를 만들려는 경우 이 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="98de4-125">이 방법을 사용하는 경우 전체 리소스 유형을 입력하고 자식 리소스 이름에 부모 리소스 이름을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="98de4-126">데이터베이스는 템플릿의 동일한 수준에 정의되어 있더라도 서버의 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="98de4-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98de4-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98de4-127">Next steps</span></span>
* <span data-ttu-id="98de4-128">템플릿 작성 방법에 대한 권장 사항은 [Azure Resource Manager 템플릿 생성 모범 사례](resource-manager-template-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98de4-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="98de4-129">여러 자식 리소스를 만드는 예제는 [Azure Resource Manager 템플릿에서 리소스의 여러 인스턴스 배포](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="98de4-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
