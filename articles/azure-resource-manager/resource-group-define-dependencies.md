---
title: "Azure 리소스에 대한 배포 순서 설정 | Microsoft Docs"
description: "리소스가 올바른 순서대로 배포되도록 배포 중 다른 리소스에 종속된 것으로 리소스를 설정하는 방법에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="840de-103">Azure Resource Manager 템플릿에서 리소스를 배포하는 순서 정의</span><span class="sxs-lookup"><span data-stu-id="840de-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="840de-104">주어진 리소스에 대해 해당 리소스를 배포하기 전에 존재해야 하는 다른 리소스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="840de-105">예를 들어 SQL 데이터베이스를 배포하려면 SQL Server가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="840de-106">하나의 리소스를 다른 리소스에 종속된 것으로 표시하여 이 관계를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="840de-107">종속성은 **dependsOn** 요소를 사용하거나 **reference** 함수를 사용하여 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="840de-108">Resource Manager는 리소스 간의 종속성을 평가한 후 종속된 순서에 따라 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="840de-109">리소스가 서로 종속되어 있지 않은 경우 Resource Manager는 이를 병렬로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="840de-110">동일한 템플릿에 배포되는 리소스에 대한 종속성만 정의하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="840de-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="840de-111">dependsOn</span></span>
<span data-ttu-id="840de-112">템플릿 내에서 dependsOn 요소를 사용하면 하나의 리소스를 하나 이상의 리소스에 종속된 것으로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="840de-113">값은 리소스 이름의 쉼표로 구분된 목록일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="840de-114">다음 예제에서는 부하 분산 장치, 가상 네트워크 및 여러 저장소 계정을 만드는 루프에 종속된 가상 컴퓨터 확장 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="840de-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="840de-115">이러한 다른 리소스는 다음 예제에 표시되어 있지 않지만 템플릿 내 다른 곳에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="840de-116">앞의 예에서 종속성은 **storageLoop**라는 복사 루프를 통해 생성되는 리소스에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="840de-117">예제는 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="840de-118">종속성을 정의할 때 모호성을 피하기 위해 리소스 공급자 네임스페이스 및 리소스 형식을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="840de-119">예를 들어 다른 리소스와 동일한 이름을 가질 수 있는 부하 분산 장치 및 가상 네트워크를 명확히 하려면 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="840de-120">dependsOn을 사용하여 리소스 간의 관계를 매핑하도록 선택할 수 있지만 왜 그렇게 하는지에 대한 이유를 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="840de-121">예를 들어, 리소스가 상호 연결되는 방식을 문서화하려면, dependsOn은 올바른 접근 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="840de-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="840de-122">배포 후 dependsOn 요소에 어떤 리소스가 정의되었는지 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="840de-123">dependsOn을 사용하면 Resource Manager는 종속성이 있는 두 리소스를 병렬로 배포하지 않으므로 배포 시간에 잠재적으로 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="840de-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="840de-124">리소스 간의 관계를 문서화하려면 [리소스 연결](/rest/api/resources/resourcelinks)을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="840de-125">자식 리소스</span><span class="sxs-lookup"><span data-stu-id="840de-125">Child resources</span></span>
<span data-ttu-id="840de-126">resources 속성을 사용하면 정의되는 리소스에 관련된 자식 리소스를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="840de-127">자식 리소스는 5개 수준 깊이까지만 정의할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="840de-128">자식 리소스 및 부모 리소스 간에 암시적 종속성은 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="840de-129">부모 리소스 다음에 자식 리소스를 배포해야 하는 경우 dependsOn 속성을 사용하여 해당 종속성을 확실하게 명시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="840de-130">각 부모 리소스는 특정 리소스 종류만 자식 리소스로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="840de-131">허용되는 리소스 종류는 부모 리소스의 [템플릿 스키마](https://github.com/Azure/azure-resource-manager-schemas)에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="840de-132">자식 리소스 종류의 이름에는 부모 리소스 종류의 이름이 포함됩니다. 예를 들어 **Microsoft.Web/sites/config**와 **Microsoft.Web/sites/extensions**는 둘 다 **Microsoft.Web/sites**의 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="840de-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="840de-133">다음 예제에서는 SQL Server 및 SQL 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="840de-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="840de-134">데이터베이스가 서버의 자식인 경우에도 SQL 데이터베이스와 SQL Server 간에 명시적 종속성이 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="840de-135">reference 함수</span><span class="sxs-lookup"><span data-stu-id="840de-135">reference function</span></span>
<span data-ttu-id="840de-136">[reference 함수](resource-group-template-functions-resource.md#reference) 를 사용하면 식을 다른 JSON 이름 및 값 쌍 또는 런타임 리소스에서 해당 값을 파생시키는 식을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="840de-137">참조 식은 한 리소스가 다른 리소스에 종속되어 있음을 암시적으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="840de-138">일반적인 형식:</span><span class="sxs-lookup"><span data-stu-id="840de-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="840de-139">다음 예제에서 CDN 끝점은 CDN 프로필에 명시적으로 종속되고 웹앱에 암시적으로 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="840de-140">이 요소 또는 dependsOn 요소를 사용하여 종속성을 지정할 수 있지만 같은 종속 리소스에 대해 두 가지를 모두 사용할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="840de-141">가능하면 불필요한 종속성을 추가하지 않도록 암시적 참조를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="840de-142">자세한 내용은 [reference 함수](resource-group-template-functions-resource.md#reference)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="840de-143">종속성 설정 권장 사항</span><span class="sxs-lookup"><span data-stu-id="840de-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="840de-144">설정할 종속성을 결정하는 경우 다음 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="840de-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="840de-145">종속성을 최대한 적게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="840de-146">자식 리소스가 부모 리소스에 종속되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="840de-147">**reference** 함수를 사용하여 속성을 공유해야 하는 리소스 간에 암시적 종속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="840de-148">암시적 종속성을 이미 정의한 경우에는 명시적 종속성(**dependsOn**)을 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="840de-149">이러한 방법은 불필요한 종속성이 포함될 위험을 줄여줍니다.</span><span class="sxs-lookup"><span data-stu-id="840de-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="840de-150">다른 리소스의 기능을 사용하지 않고 리소스를 **만들** 수 없는 경우 종속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="840de-151">리소스가 배포 후에만 상호 작용하는 경우에는 종속성을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="840de-152">종속성을 명시적으로 설정하지 않고 계단식으로 배열되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="840de-153">예를 들어 가상 컴퓨터는 가상 네트워크 인터페이스에 종속되고 가상 네트워크 인터페이스는 가상 네트워크 및 공용 IP 주소에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="840de-154">따라서 가상 컴퓨터는 세 가지 모든 리소스보다 나중에 배포되지만 가상 컴퓨터가 세 가지 모든 리소스에 종속된다고 명시적으로 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="840de-155">이러한 방법은 종속성 순서를 명확히 하고 나중에 템플릿을 쉽게 변경할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="840de-156">배포하기 전에 값을 확인할 수 있으면 종속성 없이 리소스 배포를 시도해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="840de-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="840de-157">예를 들어 구성 값에 다른 리소스의 이름이 필요하면 종속성이 불필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="840de-158">일부 리소스는 다른 리소스의 존재를 확인하기 때문에 이 지침이 항상 해당되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="840de-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="840de-159">오류가 표시되면 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="840de-160">Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="840de-161">순환적 종속성이 존재한다는 오류가 표시되면 템플릿을 평가하여 불필요한 종속성이 있는지, 제거할 수 있는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="840de-162">종속성을 제거하는 것으로 해결되지 않는다면 일부 배포 작업을 순환적 종속성이 있는 리소스 다음에 배포된 자식 리소스로 이동하여 순환적 종속성을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="840de-163">예를 들어 두 개의 가상 컴퓨터를 배포하지만 각 컴퓨터에 서로를 참조하는 속성을 설정해야 한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="840de-164">이런 경우 다음과 같은 순서로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="840de-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="840de-165">vm1</span><span class="sxs-lookup"><span data-stu-id="840de-165">vm1</span></span>
2. <span data-ttu-id="840de-166">vm2</span><span class="sxs-lookup"><span data-stu-id="840de-166">vm2</span></span>
3. <span data-ttu-id="840de-167">vm1의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="840de-168">이 확장은 vm2에서 얻은 값을 vm1에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="840de-169">vm2의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="840de-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="840de-170">이 확장은 vm1에서 얻은 값을 vm2에 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="840de-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="840de-171">배포 순서를 평가하고 종속성 오류를 해결하는 방법에 대한 자세한 내용은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="840de-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="840de-172">Next steps</span></span>
* <span data-ttu-id="840de-173">배포 중 종속성 문제 해결에 대해 알아보려면 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="840de-174">Azure 리소스 관리자 템플릿을 만드는 방법에 대한 자세한 내용은 [템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="840de-175">템플릿에서 사용할 수 있는 함수 목록은 [템플릿 함수](resource-group-template-functions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="840de-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

