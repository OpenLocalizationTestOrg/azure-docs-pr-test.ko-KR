---
title: "aaaDeploy Azure 리소스를 여러 개 | Microsoft Docs"
description: "복사 작업 및 Azure 리소스 관리자 템플릿 tooiterate 배열은 여러 번 사용할 리소스를 배포 하는 경우."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="236f6-103">Azure Resource Manager 템플릿에서 리소스 또는 속성의 여러 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="236f6-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="236f6-104">표시 하는이 항목에서 Azure 리소스 관리자 템플릿 toocreate tooiterate, 리소스의 여러 인스턴스 또는 여러 개 리소스에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-104">This topic shows you how tooiterate in your Azure Resource Manager template toocreate multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="236f6-105">리소스 배포 되었는지 여부를 참조 toospecify를 사용 하는 tooadd 논리 tooyour 템플릿을 필요한 경우 [조건에 따라 리소스를 배포](#conditionally-deploy-resource)합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-105">If you need tooadd logic tooyour template that enables you toospecify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="236f6-106">리소스 반복</span><span class="sxs-lookup"><span data-stu-id="236f6-106">Resource iteration</span></span>
<span data-ttu-id="236f6-107">toocreate 리소스 종류의 여러 인스턴스 추가 `copy` 요소 toohello 리소스 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-107">toocreate multiple instances of a resource type, add a `copy` element toohello resource type.</span></span> <span data-ttu-id="236f6-108">Hello copy 요소에서 hello 수가 반복 및이 루프에 대 한 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-108">In hello copy element, you specify hello number of iterations and a name for this loop.</span></span> <span data-ttu-id="236f6-109">hello 개수 값 양의 정수 여야 하 고 800을 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-109">hello count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="236f6-110">리소스 관리자 병렬로 hello 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-110">Resource Manager creates hello resources in parallel.</span></span> <span data-ttu-id="236f6-111">따라서 생성 되는 hello 순서는 보장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-111">Therefore, hello order in which they are created is not guaranteed.</span></span> <span data-ttu-id="236f6-112">순서 대로 반복 toocreate 리소스 참조 [직렬 복사](#serial-copy)합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-112">toocreate iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="236f6-113">hello 리소스 toocreate 여러 번 형식에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-113">hello resource toocreate multiple times takes hello following format:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

<span data-ttu-id="236f6-114">해당 hello 확인 hello를 포함 하는 각 리소스의 이름 `copyIndex()` hello 루프에서 hello 현재 반복을 반환 하는 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-114">Notice that hello name of each resource includes hello `copyIndex()` function, which returns hello current iteration in hello loop.</span></span> <span data-ttu-id="236f6-115">`copyIndex()`는 0부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="236f6-116">다음 예에서는, hello:</span><span class="sxs-lookup"><span data-stu-id="236f6-116">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="236f6-117">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-117">Creates these names:</span></span>

* <span data-ttu-id="236f6-118">storage0</span><span class="sxs-lookup"><span data-stu-id="236f6-118">storage0</span></span>
* <span data-ttu-id="236f6-119">storage1</span><span class="sxs-lookup"><span data-stu-id="236f6-119">storage1</span></span>
* <span data-ttu-id="236f6-120">storage2</span><span class="sxs-lookup"><span data-stu-id="236f6-120">storage2.</span></span>

<span data-ttu-id="236f6-121">toooffset hello 인덱스 값을 hello copyIndex() 함수에 값을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-121">toooffset hello index value, you can pass a value in hello copyIndex() function.</span></span> <span data-ttu-id="236f6-122">hello 반복 tooperform 수가 지정 되어 hello copy 요소에서 있지만 copyIndex hello 값은 지정 된 hello 오프셋 값입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-122">hello number of iterations tooperform is still specified in hello copy element, but hello value of copyIndex is offset by hello specified value.</span></span> <span data-ttu-id="236f6-123">다음 예에서는, hello:</span><span class="sxs-lookup"><span data-stu-id="236f6-123">So, hello following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="236f6-124">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-124">Creates these names:</span></span>

* <span data-ttu-id="236f6-125">storage1</span><span class="sxs-lookup"><span data-stu-id="236f6-125">storage1</span></span>
* <span data-ttu-id="236f6-126">storage2</span><span class="sxs-lookup"><span data-stu-id="236f6-126">storage2</span></span>
* <span data-ttu-id="236f6-127">storage3</span><span class="sxs-lookup"><span data-stu-id="236f6-127">storage3</span></span>

<span data-ttu-id="236f6-128">hello 복사 작업이 hello 배열의 각 요소를 반복할 수 때문에 배열에서 작업할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-128">hello copy operation is helpful when working with arrays because you can iterate through each element in hello array.</span></span> <span data-ttu-id="236f6-129">사용 하 여 hello `length` , 반복에 대 한 hello 배열 toospecify hello 수에는 함수 및 `copyIndex` tooretrieve hello 현재 hello 배열의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-129">Use hello `length` function on hello array toospecify hello count for iterations, and `copyIndex` tooretrieve hello current index in hello array.</span></span> <span data-ttu-id="236f6-130">다음 예에서는, hello:</span><span class="sxs-lookup"><span data-stu-id="236f6-130">So, hello following example:</span></span>

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

<span data-ttu-id="236f6-131">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-131">Creates these names:</span></span>

* <span data-ttu-id="236f6-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="236f6-132">storagecontoso</span></span>
* <span data-ttu-id="236f6-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="236f6-133">storagefabrikam</span></span>
* <span data-ttu-id="236f6-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="236f6-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="236f6-135">직렬 복사</span><span class="sxs-lookup"><span data-stu-id="236f6-135">Serial copy</span></span>

<span data-ttu-id="236f6-136">복사 요소 toocreate hello를 사용 하는 경우 리소스 종류, 리소스 관리자 기본적으로의 여러 인스턴스는 동시에 이러한 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-136">When you use hello copy element toocreate multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="236f6-137">그러나, 순서 대로 리소스를 배포 하는 hello toospecify를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-137">However, you may want toospecify that hello resources are deployed in sequence.</span></span> <span data-ttu-id="236f6-138">예를 들어 프로덕션 환경으로 업데이트할 때 좋습니다 toostagger hello 업데이트에 특정 수를 한 번에 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-138">For example, when updating a production environment, you may want toostagger hello updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="236f6-139">리소스 관리자 여러 인스턴스를 배포 하는 hello copy 요소에서 tooserially 있습니다 사용할 수 있는 속성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-139">Resource Manager provides properties on hello copy element that enable you tooserially deploy multiple instances.</span></span> <span data-ttu-id="236f6-140">Hello copy 요소에서 설정 `mode` 너무**직렬** 및 `batchSize` toohello 수가 한 번에 인스턴스 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-140">In hello copy element, set `mode` too**serial** and `batchSize` toohello number of instances toodeploy at a time.</span></span> <span data-ttu-id="236f6-141">직렬 모드에서는 리소스 관리자 hello 이전 일괄 처리가 완료 될 때까지 하나의 일괄 처리 시작 되지 않으면 하므로 hello 루프에 있는 이전 인스턴스에 종속성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-141">With serial mode, Resource Manager creates a dependency on earlier instances in hello loop, so it does not start one batch until hello previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="236f6-142">hello 모드 속성 받기도 **병렬**, hello 기본값은입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-142">hello mode property also accepts **parallel**, which is hello default value.</span></span>

<span data-ttu-id="236f6-143">tootest 직렬 복사본 실제 리소스를 만들지 않고 다음 빈 중첩 된 서식 파일을 배포 하는 템플릿에 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="236f6-143">tootest serial copy without creating actual resources, use hello following template that deploys empty nested templates:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

<span data-ttu-id="236f6-144">Hello 배포 기록에 중첩된 배포 hello 순서 대로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-144">In hello deployment history, notice that hello nested deployments are processed in sequence.</span></span>

![직렬 배포](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="236f6-146">보다 실제적인 시나리오에 대 한 hello 다음 예에서는 중첩 된 템플릿에서 Linux VM의 한 번에 두 개의 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-146">For a more realistic scenario, hello following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a><span data-ttu-id="236f6-147">속성 반복</span><span class="sxs-lookup"><span data-stu-id="236f6-147">Property iteration</span></span>

<span data-ttu-id="236f6-148">toocreate 리소스에 대 한 속성에 대 한 여러 값 추가 `copy` hello 속성 요소에 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-148">toocreate multiple values for a property on a resource, add a `copy` array in hello properties element.</span></span> <span data-ttu-id="236f6-149">이 배열에 개체를 포함 하 고 각 개체에는 다음과 같은 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="236f6-149">This array contains objects, and each object has hello following properties:</span></span>

* <span data-ttu-id="236f6-150">이름-hello 이름에 대 한 여러 값의 hello 속성 toocreate</span><span class="sxs-lookup"><span data-stu-id="236f6-150">name - hello name of hello property toocreate multiple values for</span></span>
* <span data-ttu-id="236f6-151">-값 toocreate hello 수를 계산</span><span class="sxs-lookup"><span data-stu-id="236f6-151">count - hello number of values toocreate</span></span>
* <span data-ttu-id="236f6-152">입력-hello 값 tooassign toohello 속성을 포함 하는 개체</span><span class="sxs-lookup"><span data-stu-id="236f6-152">input - an object that contains hello values tooassign toohello property</span></span>  

<span data-ttu-id="236f6-153">hello 방법을 예제와 다음 tooapply `copy` 가상 컴퓨터에서 toohello dataDisks 속성:</span><span class="sxs-lookup"><span data-stu-id="236f6-153">hello following example shows how tooapply `copy` toohello dataDisks property on a virtual machine:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="236f6-154">사용 하는 경우 다음에 유의 `copyIndex` 속성 반복 내 hello 반복 hello 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-154">Notice that when using `copyIndex` inside a property iteration, you must provide hello name of hello iteration.</span></span> <span data-ttu-id="236f6-155">리소스 반복와 함께 사용할 경우 tooprovide hello 이름이 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-155">You do not have tooprovide hello name when used with resource iteration.</span></span>

<span data-ttu-id="236f6-156">리소스 관리자 확장 hello `copy` 배포 하는 동안 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-156">Resource Manager expands hello `copy` array during deployment.</span></span> <span data-ttu-id="236f6-157">hello 배열 hello 이름에는 hello 속성의 hello 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-157">hello name of hello array becomes hello name of hello property.</span></span> <span data-ttu-id="236f6-158">hello 입력된 값은 hello 개체 속성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-158">hello input values become hello object properties.</span></span> <span data-ttu-id="236f6-159">배포 된 hello 템플릿이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-159">hello deployed template becomes:</span></span>

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

<span data-ttu-id="236f6-160">리소스 및 속성 반복을 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="236f6-161">참조 hello 속성 이름으로 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-161">Reference hello property iteration by name.</span></span>

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

<span data-ttu-id="236f6-162">각 리소스에 대 한 hello 속성에만 하나의 copy 요소를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-162">You can only include one copy element in hello properties for each resource.</span></span> <span data-ttu-id="236f6-163">toospecify 둘 이상의 속성에 대 한 반복 루프는 hello 복사 배열에 있는 여러 개체를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-163">toospecify an iteration loop for more than one property, define multiple objects in hello copy array.</span></span> <span data-ttu-id="236f6-164">각 개체는 개별적으로 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-164">Each object is iterated separately.</span></span> <span data-ttu-id="236f6-165">예를 들어 toocreate 두 hello의 여러 인스턴스 `frontendIPConfigurations` 속성과 hello `loadBalancingRules` 단일 copy 요소에서 두 개체를 정의 하는 부하 분산 장치 속성:</span><span class="sxs-lookup"><span data-stu-id="236f6-165">For example, toocreate multiple instances of both hello `frontendIPConfigurations` property and hello `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="236f6-166">루프의 리소스에 따라 달라짐</span><span class="sxs-lookup"><span data-stu-id="236f6-166">Depend on resources in a loop</span></span>
<span data-ttu-id="236f6-167">리소스 hello를 사용 하 여 다른 리소스 후 배포 된 지정 `dependsOn` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-167">You specify that a resource is deployed after another resource by using hello `dependsOn` element.</span></span> <span data-ttu-id="236f6-168">toodeploy 루프에서 리소스의 hello 컬렉션에 종속 된 리소스에는 hello dependsOn 요소에 hello 복사 루프의 hello 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-168">toodeploy a resource that depends on hello collection of resources in a loop, provide hello name of hello copy loop in hello dependsOn element.</span></span> <span data-ttu-id="236f6-169">다음 예제는 hello toodeploy 배포 하기 전에 3 개의 저장소 계정을 가상 컴퓨터를 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-169">hello following example shows how toodeploy three storage accounts before deploying hello Virtual Machine.</span></span> <span data-ttu-id="236f6-170">전체 가상 컴퓨터 정의 hello 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-170">hello full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="236f6-171">해당 hello copy 요소 설정 이름이 너무 공지`storagecopy` hello 가상 컴퓨터에 대 한 hello dependsOn 요소 너무 설정`storagecopy`합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-171">Notice that hello copy element has name set too`storagecopy` and hello dependsOn element for hello Virtual Machines is also set too`storagecopy`.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="236f6-172">자식 리소스의 여러 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="236f6-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="236f6-173">자식 리소스에 대해 복사 반복을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="236f6-174">toocreate 다른 리소스 내에 중첩 된으로 일반적으로 정의 하는 리소스의 여러 인스턴스를 대신 만들어야 해당 리소스를 최상위 리소스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-174">toocreate multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="236f6-175">Hello 유형 및 이름 속성을 통해 hello 부모 리소스와 hello 관계를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-175">You define hello relationship with hello parent resource through hello type and name properties.</span></span>

<span data-ttu-id="236f6-176">예를 들어, 데이터 집합을 데이터 팩터리 내에 자식 리소스로 정의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

<span data-ttu-id="236f6-177">toocreate 데이터 집합의 여러 인스턴스를 이동 hello 데이터 팩터리 외부에서.</span><span class="sxs-lookup"><span data-stu-id="236f6-177">toocreate multiple instances of data sets, move it outside of hello data factory.</span></span> <span data-ttu-id="236f6-178">hello dataset hello hello 데이터 팩터리로 동일한 수준에 있어야 하지만 hello 데이터 팩터리의 자식 리소스 여전히 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-178">hello dataset must be at hello same level as hello data factory, but it is still a child resource of hello data factory.</span></span> <span data-ttu-id="236f6-179">데이터 집합 및 hello 유형 및 이름 속성을 통해 데이터 팩터리 간의 hello 관계를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-179">You preserve hello relationship between data set and data factory through hello type and name properties.</span></span> <span data-ttu-id="236f6-180">Hello 형식으로 정규화 된 hello 형식을 제공 해야 hello 서식 파일에서 해당 위치에서 형식을 유추할 수 없습니다, 이후: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-180">Since type can no longer be inferred from its position in hello template, you must provide hello fully qualified type in hello format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="236f6-181">tooestablish hello 데이터 팩터리의 인스턴스로 부모/자식 관계는 hello 부모 리소스 이름을 포함 하는 hello 데이터 집합에 대 한 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-181">tooestablish a parent/child relationship with an instance of hello data factory, provide a name for hello data set that includes hello parent resource name.</span></span> <span data-ttu-id="236f6-182">형식을 사용 하 여 hello: `{parent-resource-name}/{child-resource-name}`합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-182">Use hello format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="236f6-183">hello 다음 예제는 hello 구현.</span><span class="sxs-lookup"><span data-stu-id="236f6-183">hello following example shows hello implementation:</span></span>

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="236f6-184">조건부 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="236f6-184">Conditionally deploy resource</span></span>

<span data-ttu-id="236f6-185">toospecify 리소스 배포 여부를 사용 하 여 hello `condition` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-185">toospecify whether a resource is deployed, use hello `condition` element.</span></span> <span data-ttu-id="236f6-186">이 요소에 대 한 hello 값 tootrue 또는 false를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-186">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="236f6-187">Hello 값이 true 이면 hello 리소스 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-187">When hello value is true, hello resource is deployed.</span></span> <span data-ttu-id="236f6-188">Hello 값이 false 이면 hello 리소스 배포 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-188">When hello value is false, hello resource is not deployed.</span></span> <span data-ttu-id="236f6-189">예를 들어 toospecify 사용 하는지 여부를 새 저장소 계정을 배포 되었거나 기존 저장소 계정을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-189">For example, toospecify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

<span data-ttu-id="236f6-190">기존 또는 새 리소스 사용 예제는 [신규 또는 기존 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="236f6-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="236f6-191">암호 또는 SSH 키 toodeploy 가상 컴퓨터를 사용 하 여 예제를 보려면 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-191">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="236f6-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="236f6-192">Next steps</span></span>
* <span data-ttu-id="236f6-193">서식 파일의 섹션 hello에 대 한 toolearn 참조 [Azure 리소스 관리자 템플릿 제작](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-193">If you want toolearn about hello sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="236f6-194">toolearn 어떻게 toodeploy 서식 파일에 참조 [Azure 리소스 관리자 템플릿을 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="236f6-194">toolearn how toodeploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

