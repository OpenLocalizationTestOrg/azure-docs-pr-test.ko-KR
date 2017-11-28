---
title: "Azure 서식 파일에 자식 리소스 aaaDefine | Microsoft Docs"
description: "리소스 종류 및 Azure 리소스 관리자 템플릿에 자식 리소스에 대 한 이름을 tooset hello 하는 방법을 보여 줍니다."
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="fdd4d-103">Resource Manager 템플릿에서 자식 리소스의 이름 및 유형 설정</span><span class="sxs-lookup"><span data-stu-id="fdd4d-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="fdd4d-104">서식 파일을 만들 때 자주 tooinclude 자식 리소스 관련된 tooa 부모 리소스에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="fdd4d-105">예를 들어 템플릿에 SQL Server 및 데이터베이스가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="fdd4d-106">hello SQL 서버 hello 부모 리소스와 hello 데이터베이스가 hello 자식 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="fdd4d-107">hello hello 자식 리소스 종류의 형식은 다음과 같습니다.`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="fdd4d-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="fdd4d-108">hello hello 자식 리소스 이름의 형식은 다음과 같습니다.`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="fdd4d-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="fdd4d-109">그러나 hello 형식 및 서식 파일의 이름을 따라 다르게 hello 부모 리소스 내에 중첩 되어 있는지 여부 또는 자체적으로 hello 최상위 수준에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="fdd4d-110">이 항목에서는 두 toohandle 접근 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="fdd4d-111">정규화 된 참조 tooa 리소스를 생성할 때는 hello 순서 toocombine hello 형식에서 세그먼트 및 이름이 hello 2의 연결을 단순히 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="fdd4d-112">대신, hello 네임 스페이스 후의 시퀀스를 사용 하 여 *유형/이름이* 구체적인 toomost 특정 쌍:</span><span class="sxs-lookup"><span data-stu-id="fdd4d-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="fdd4d-113">예:</span><span class="sxs-lookup"><span data-stu-id="fdd4d-113">For example:</span></span>

<span data-ttu-id="fdd4d-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`는 올바릅니다. `Microsoft.Compute/virtualMachines/extensions/myVM/myExt`는 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="fdd4d-115">중첩된 자식 리소스</span><span class="sxs-lookup"><span data-stu-id="fdd4d-115">Nested child resource</span></span>
<span data-ttu-id="fdd4d-116">hello 가장 쉬운 방법은 toodefine 자식 리소스는 toonest hello 부모 리소스 내에서.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="fdd4d-117">hello 다음 예제에서는 SQL server에서 내에 중첩 된 SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="fdd4d-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="fdd4d-118">Hello 자식 리소스에 대 한 hello 유형이 설정 되어 너무`databases` 하지만 해당 전체 리소스 형식이 `Microsoft.Sql/servers/databases`합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="fdd4d-119">그러지 않으면 `Microsoft.Sql/servers/` hello 부모 리소스 종류에서 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="fdd4d-120">hello 자식 리소스 이름이 너무 설정`exampledatabase` hello 전체 이름 hello 부모 이름이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="fdd4d-121">그러지 않으면 `exampleserver` hello 부모 리소스에서 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="fdd4d-122">최상위 자식 리소스</span><span class="sxs-lookup"><span data-stu-id="fdd4d-122">Top-level child resource</span></span>
<span data-ttu-id="fdd4d-123">Hello 최상위 수준 hello 자식 리소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="fdd4d-124">Hello 부모 리소스 hello에 배포 되지 않은 경우이 방법을 사용할 수 있습니다 동일한 템플릿이나 toouse를 원하는 경우 `copy` toocreate 여러 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="fdd4d-125">이 방법에서는 hello 전체 리소스 종류를 제공 하 고 hello 자식 리소스 이름에 hello 부모 리소스 이름을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="fdd4d-126">hello 데이터베이스는 hello hello 서식 파일에 동일한 수준에 정의 된 경우에 자식 리소스 toohello 서버.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdd4d-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fdd4d-127">Next steps</span></span>
* <span data-ttu-id="fdd4d-128">방법에 대 한 권장 사항에 대 한 toocreate 템플릿 참조 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](resource-manager-template-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="fdd4d-129">여러 자식 리소스를 만드는 예제는 [Azure Resource Manager 템플릿에서 리소스의 여러 인스턴스 배포](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fdd4d-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
