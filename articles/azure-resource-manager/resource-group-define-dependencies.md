---
title: "Azure 리소스에 대 한 배포 순서 aaaSet | Microsoft Docs"
description: "설명 hello 올바른 순서로 tooset 하나의 리소스 배포 tooensure 리소스 중 다른 리소스에 종속으로 배포 되는 방법입니다."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="b93c7-103">Azure 리소스 관리자 템플릿의 리소스를 배포 하기 위한 hello 순서 정의</span><span class="sxs-lookup"><span data-stu-id="b93c7-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="b93c7-104">지정된 된 리소스에 대 한 hello 리소스를 배포 하기 전에 있어야 하는 다른 리소스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="b93c7-105">예를 들어 SQL server toodeploy SQL 데이터베이스를 시도 하기 전에 존재 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="b93c7-106">다른 리소스에이 관계 hello에 종속으로 한 리소스를 표시 하 여 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="b93c7-107">Hello로 종속성 정의 **dependsOn** 요소 또는 hello를 사용 하 여 **참조** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="b93c7-108">리소스 관리자 리소스 간의 종속성을 hello 평가 하 고 종속 순서에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="b93c7-109">리소스가 서로 종속되어 있지 않은 경우 Resource Manager는 이를 병렬로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="b93c7-110">Hello에 배포 되는 리소스에 대 한 toodefine 종속성만 하면 같은 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="b93c7-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="b93c7-111">dependsOn</span></span>
<span data-ttu-id="b93c7-112">서식 파일에 내 hello dependsOn 요소 활성화 하면 toodefine 하나의 리소스 하나 이상의 리소스에 의존 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="b93c7-113">값은 리소스 이름의 쉼표로 구분된 목록일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="b93c7-114">hello 다음 예제에서는 부하 분산 장치, 가상 네트워크 및 저장소 계정을 여러 개 만드는 루프에 의존 하는 가상 컴퓨터 크기 집합</span><span class="sxs-lookup"><span data-stu-id="b93c7-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="b93c7-115">이러한 다른 리소스는 다음 예제를 hello에 표시 되지 않습니다 되지만 tooexist hello 서식 파일의 다른 위치에서 필요한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="b93c7-116">앞 예제는 hello, 종속성 라는 복사 루프를 통해 만들어진 hello 리소스에 포함 되어 **storageLoop**합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="b93c7-117">예제는 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b93c7-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="b93c7-118">종속성을 정의할 때는 hello 리소스 공급자 네임 스페이스 및 리소스 유형을 tooavoid 모호성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="b93c7-119">부하 분산 장치 및 hello 다른 리소스를 사용 하 여 hello 다음 동일한 이름을 가질 수 있는 가상 네트워크 형식 tooclarify 예를 들어:</span><span class="sxs-lookup"><span data-stu-id="b93c7-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="b93c7-120">저장할된 toouse dependsOn toomap 관계 수 있습니다 프로그램 리소스 간의 중요 한 toounderstand 하 고 이유는.</span><span class="sxs-lookup"><span data-stu-id="b93c7-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="b93c7-121">예를 들어, 리소스는 연결 되는 방식 toodocument dependsOn 않습니다 hello 적합 한 접근 방식을.</span><span class="sxs-lookup"><span data-stu-id="b93c7-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="b93c7-122">배포 후 리소스 hello dependsOn 요소에 정의 된 쿼리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="b93c7-123">dependsOn을 사용하면 Resource Manager는 종속성이 있는 두 리소스를 병렬로 배포하지 않으므로 배포 시간에 잠재적으로 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="b93c7-124">toodocument 관계 리소스를 대신 사용 하 여 [리소스를 연결](/rest/api/resources/resourcelinks)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="b93c7-125">자식 리소스</span><span class="sxs-lookup"><span data-stu-id="b93c7-125">Child resources</span></span>
<span data-ttu-id="b93c7-126">hello 리소스 속성 정의 하 고 관련된 toohello 리소스 toospecify 자식 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="b93c7-127">자식 리소스는 5개 수준 깊이까지만 정의할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="b93c7-128">암시적 종속성이 없어서 toonote hello 부모 리소스와 자식 리소스 간에 만들어진 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="b93c7-129">자식 리소스 toobe hello 부모 리소스 후 배포 된 hello 필요, 해당 종속성 hello dependsOn 속성으로 명시적 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="b93c7-130">각 부모 리소스는 특정 리소스 종류만 자식 리소스로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="b93c7-131">리소스 종류 hello에 지정 된 hello 허용 [템플릿 스키마](https://github.com/Azure/azure-resource-manager-schemas) hello 부모 리소스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="b93c7-132">자식 리소스 종류의 hello 이름 같은 hello 부모 리소스 종류의 hello 이름이 포함 됩니다 **Microsoft.Web/sites/config** 및 **Microsoft.Web/sites/extensions** hello 의자식리소스가두 **Microsoft.Web/sites**합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="b93c7-133">다음 예제는 hello SQL server와 SQL 데이터베이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="b93c7-134">Hello 데이터베이스 hello 서버의 자식인 경우에 명시적 종속성 hello SQL 데이터베이스와 SQL server에 정의 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="b93c7-135">reference 함수</span><span class="sxs-lookup"><span data-stu-id="b93c7-135">reference function</span></span>
<span data-ttu-id="b93c7-136">hello [함수를 참조](resource-group-template-functions-resource.md#reference) 식 tooderive 다른 JSON 이름 및 값 쌍 이나 런타임 리소스에서 해당 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="b93c7-137">참조 식은 한 리소스가 다른 리소스에 종속되어 있음을 암시적으로 선언합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="b93c7-138">hello 일반 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="b93c7-139">다음 예제는 hello에서 CDN 끝점 hello CDN 프로필을 명시적으로 의존 하 고 암시적으로 웹 응용 프로그램에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="b93c7-140">이 요소 또는 hello dependsOn 요소 toospecify 종속성을 사용할 수 있지만 hello에 대 한 불필요 toouse 모두 같은 종속 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="b93c7-141">가능 하면 불필요 한 종속성을 추가 하는 암시적 참조 tooavoid를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="b93c7-142">toolearn 더 참조 [함수를 참조](resource-group-template-functions-resource.md#reference)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="b93c7-143">종속성 설정 권장 사항</span><span class="sxs-lookup"><span data-stu-id="b93c7-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="b93c7-144">어떤 종속성 tooset를 결정할 때는 hello 지침을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="b93c7-145">종속성을 최대한 적게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="b93c7-146">자식 리소스가 부모 리소스에 종속되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="b93c7-147">사용 하 여 hello **참조** tooshare 속성을 필요로 하는 리소스 간의 암시적 종속성 tooset 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="b93c7-148">암시적 종속성을 이미 정의한 경우에는 명시적 종속성(**dependsOn**)을 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="b93c7-149">이 방법의 불필요 한 종속 hello 위험을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="b93c7-150">다른 리소스의 기능을 사용하지 않고 리소스를 **만들** 수 없는 경우 종속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="b93c7-151">배포 후에 hello 리소스만 상호 작용 하는 경우에 종속성을 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b93c7-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="b93c7-152">종속성을 명시적으로 설정하지 않고 계단식으로 배열되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="b93c7-153">예를 들어 가상 컴퓨터가 가상 네트워크 인터페이스에 따라 달라 집니다 및 hello 가상 네트워크 인터페이스를 가상 네트워크와 공용 IP 주소에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="b93c7-154">따라서 hello 가상 컴퓨터가 배포 된 모든 세 가지 리소스 있지만 모든 세 가지 리소스에 종속으로 hello 가상 컴퓨터를 명시적으로 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="b93c7-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="b93c7-155">이 방법은 hello 종속성 순서를 명확히 고 보다 쉽게 toochange hello 템플릿 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="b93c7-156">값을 확인할 수 없는 배포 하기 전에 한 종속성 없이 hello 리소스를 배포 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b93c7-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="b93c7-157">예를 들어 구성 값 hello 이름 다른 리소스의 경우, 종속성이 필요 하지 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="b93c7-158">이 설명서는 일부 리소스가 있는지 확인 합니다. hello hello 다른 리소스 때문에 항상 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="b93c7-159">오류가 표시되면 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="b93c7-160">Resource Manager는 템플릿의 유효성을 검사하는 동안 순환적 종속성을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="b93c7-161">순환 종속성이 존재 한다는 오류가 나타나면 템플릿 toosee 있는지 여부를 평가할 종속성은 필요 하지 않으며 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="b93c7-162">종속성 제거 작동 하지 않는 경우에 일부 배포 작업 후 hello 순환 종속성을 포함 하는 hello 리소스가 배포 되는 자식 리소스를 이동 하 여 순환 종속성을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="b93c7-163">예를 들어, 두 가상 컴퓨터를 배포 하는 하지만 다른 toohello 참조 하는 각 항목에 속성을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="b93c7-164">순서에 따라 hello에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="b93c7-165">vm1</span><span class="sxs-lookup"><span data-stu-id="b93c7-165">vm1</span></span>
2. <span data-ttu-id="b93c7-166">vm2</span><span class="sxs-lookup"><span data-stu-id="b93c7-166">vm2</span></span>
3. <span data-ttu-id="b93c7-167">vm1의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="b93c7-168">hello 확장 v m 2에서 가져오는 v m 1의 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="b93c7-169">vm2의 확장은 vm1 및 vm2에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="b93c7-170">hello 확장 v m 1에서 가져오는 v m 2에 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="b93c7-171">Hello 배포 순서를 평가 하 고 종속성 오류를 해결 하는 방법에 대 한 정보를 참조 하십시오. [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b93c7-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b93c7-172">Next steps</span></span>
* <span data-ttu-id="b93c7-173">배포 하는 동안 종속성 문제를 해결 하는 방법에 대 한 toolearn 참조 [Azure 리소스 관리자와 일반적인 Azure 배포 오류 문제 해결](resource-manager-common-deployment-errors.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b93c7-174">Azure 리소스 관리자 템플릿을 만드는 방법에 대해 toolearn 참조 [템플릿을 작성](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="b93c7-175">목록이 hello 서식 파일에 사용할 수 있는 함수에 대 한 참조 [템플릿 함수](resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b93c7-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

