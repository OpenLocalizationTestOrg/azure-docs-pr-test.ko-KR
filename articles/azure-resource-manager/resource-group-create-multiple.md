---
title: "Azure 리소스의 여러 인스턴스 배포 | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿에서 복사 작업 및 배열을 사용하여 여러 번 반복하는 방법을 설명합니다."
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
ms.openlocfilehash: ed8e3081d2b2e07938d7cf3aa5f95f6dde81bc66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a><span data-ttu-id="4f718-103">Azure Resource Manager 템플릿에서 리소스 또는 속성의 여러 인스턴스 배포</span><span class="sxs-lookup"><span data-stu-id="4f718-103">Deploy multiple instances of a resource or property in Azure Resource Manager templates</span></span>
<span data-ttu-id="4f718-104">이 항목에서는 Azure Resource Manager 템플릿에서 반복하여 리소스의 여러 인스턴스 또는 리소스에 있는 속성의 여러 인스턴스를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-104">This topic shows you how to iterate in your Azure Resource Manager template to create multiple instances of a resource, or multiple instances of a property on a resource.</span></span>

<span data-ttu-id="4f718-105">리소스 배포 여부를 지정할 수 있는 논리를 템플릿에 추가해야 하는 경우 [조건부로 리소스 배포](#conditionally-deploy-resource)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-105">If you need to add logic to your template that enables you to specify whether a resource is deployed, see [Conditionally deploy resource](#conditionally-deploy-resource).</span></span>

## <a name="resource-iteration"></a><span data-ttu-id="4f718-106">리소스 반복</span><span class="sxs-lookup"><span data-stu-id="4f718-106">Resource iteration</span></span>
<span data-ttu-id="4f718-107">리소스 종류의 여러 인스턴스를 만들려면 리소스 종류에 `copy` 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-107">To create multiple instances of a resource type, add a `copy` element to the resource type.</span></span> <span data-ttu-id="4f718-108">copy 요소에서 이 루프의 반복 횟수와 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-108">In the copy element, you specify the number of iterations and a name for this loop.</span></span> <span data-ttu-id="4f718-109">count 값은 양의 정수여야 하며 800을 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-109">The count value must be a positive integer and cannot exceed 800.</span></span> <span data-ttu-id="4f718-110">Resource Manager는 병렬로 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-110">Resource Manager creates the resources in parallel.</span></span> <span data-ttu-id="4f718-111">따라서 생성되는 순서는 정해져 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-111">Therefore, the order in which they are created is not guaranteed.</span></span> <span data-ttu-id="4f718-112">시퀀스에서 반복된 리소스를 만들려면 [직렬 복사](#serial-copy)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-112">To create iterated resources in sequence, see [Serial copy](#serial-copy).</span></span> 

<span data-ttu-id="4f718-113">다음 형식으로 리소스를 여러 번 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-113">The resource to create multiple times takes the following format:</span></span>

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

<span data-ttu-id="4f718-114">각 리소스의 이름에는 `copyIndex()` 함수가 포함되어 있으며 이 함수는 루프에서 현재 반복을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-114">Notice that the name of each resource includes the `copyIndex()` function, which returns the current iteration in the loop.</span></span> <span data-ttu-id="4f718-115">`copyIndex()`는 0부터 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-115">`copyIndex()` is zero-based.</span></span> <span data-ttu-id="4f718-116">따라서 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-116">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex())]",
```

<span data-ttu-id="4f718-117">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-117">Creates these names:</span></span>

* <span data-ttu-id="4f718-118">storage0</span><span class="sxs-lookup"><span data-stu-id="4f718-118">storage0</span></span>
* <span data-ttu-id="4f718-119">storage1</span><span class="sxs-lookup"><span data-stu-id="4f718-119">storage1</span></span>
* <span data-ttu-id="4f718-120">storage2</span><span class="sxs-lookup"><span data-stu-id="4f718-120">storage2.</span></span>

<span data-ttu-id="4f718-121">인덱스 값을 오프셋하려면 copyIndex() 함수에 값을 전달하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-121">To offset the index value, you can pass a value in the copyIndex() function.</span></span> <span data-ttu-id="4f718-122">수행할 반복 수는 복사 요소에서 지정되지만 copyIndex의 값이 지정된 값 만큼 오프셋됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-122">The number of iterations to perform is still specified in the copy element, but the value of copyIndex is offset by the specified value.</span></span> <span data-ttu-id="4f718-123">따라서 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-123">So, the following example:</span></span>

```json
"name": "[concat('storage', copyIndex(1))]",
```

<span data-ttu-id="4f718-124">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-124">Creates these names:</span></span>

* <span data-ttu-id="4f718-125">storage1</span><span class="sxs-lookup"><span data-stu-id="4f718-125">storage1</span></span>
* <span data-ttu-id="4f718-126">storage2</span><span class="sxs-lookup"><span data-stu-id="4f718-126">storage2</span></span>
* <span data-ttu-id="4f718-127">storage3</span><span class="sxs-lookup"><span data-stu-id="4f718-127">storage3</span></span>

<span data-ttu-id="4f718-128">복사 작업은 배열의 각 요소를 반복할 수 있으므로 배열을 사용할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-128">The copy operation is helpful when working with arrays because you can iterate through each element in the array.</span></span> <span data-ttu-id="4f718-129">배열의 `length` 함수를 사용하여 반복 횟수를 지정하고, `copyIndex`를 사용하여 배열의 현재 인덱스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-129">Use the `length` function on the array to specify the count for iterations, and `copyIndex` to retrieve the current index in the array.</span></span> <span data-ttu-id="4f718-130">따라서 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-130">So, the following example:</span></span>

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

<span data-ttu-id="4f718-131">다음과 같은 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-131">Creates these names:</span></span>

* <span data-ttu-id="4f718-132">storagecontoso</span><span class="sxs-lookup"><span data-stu-id="4f718-132">storagecontoso</span></span>
* <span data-ttu-id="4f718-133">storagefabrikam</span><span class="sxs-lookup"><span data-stu-id="4f718-133">storagefabrikam</span></span>
* <span data-ttu-id="4f718-134">storagecoho</span><span class="sxs-lookup"><span data-stu-id="4f718-134">storagecoho</span></span>

## <a name="serial-copy"></a><span data-ttu-id="4f718-135">직렬 복사</span><span class="sxs-lookup"><span data-stu-id="4f718-135">Serial copy</span></span>

<span data-ttu-id="4f718-136">복사 요소를 사용하여 리소스 형식의 여러 인스턴스를 만드는 경우 Resource Manager는 기본적으로 동시에 해당 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-136">When you use the copy element to create multiple instances of a resource type, Resource Manager, by default, deploys those instances in parallel.</span></span> <span data-ttu-id="4f718-137">그러나 그 결과로 리소스가 배포되도록 지정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-137">However, you may want to specify that the resources are deployed in sequence.</span></span> <span data-ttu-id="4f718-138">예를 들어 프로덕션 환경을 업데이트할 때 특정 수를 한 번에 업데이트하도록 업데이트를 늦추려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-138">For example, when updating a production environment, you may want to stagger the updates so only a certain number are updated at any one time.</span></span>

<span data-ttu-id="4f718-139">Resource Manager는 순차적으로 여러 인스턴스를 배포할 수 있는 복사 요소의 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-139">Resource Manager provides properties on the copy element that enable you to serially deploy multiple instances.</span></span> <span data-ttu-id="4f718-140">복사 요소에서 `mode`를 **직렬**로 설정하고 `batchSize`를 한 번에 배포할 인스턴스 수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-140">In the copy element, set `mode` to **serial** and `batchSize` to the number of instances to deploy at a time.</span></span> <span data-ttu-id="4f718-141">Resource Manager는 직렬 모드에서 루프에 이전 인스턴스의 종속성을 만듭니다. 따라서 이전 일괄 처리가 완료될 때까지 하나의 일괄 처리를 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-141">With serial mode, Resource Manager creates a dependency on earlier instances in the loop, so it does not start one batch until the previous batch completes.</span></span>

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

<span data-ttu-id="4f718-142">모드 속성은 기본 값인 **병렬**을 수용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-142">The mode property also accepts **parallel**, which is the default value.</span></span>

<span data-ttu-id="4f718-143">실제 리소스를 만들지 않고 직렬 복사본을 테스트하려면 다음 템플릿을 사용하여 비어 있는 중첩된 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-143">To test serial copy without creating actual resources, use the following template that deploys empty nested templates:</span></span>

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

<span data-ttu-id="4f718-144">배포 기록에서 중첩된 배포가 순서대로 처리되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-144">In the deployment history, notice that the nested deployments are processed in sequence.</span></span>

![직렬 배포](./media/resource-group-create-multiple/serial-copy.png)

<span data-ttu-id="4f718-146">보다 현실적인 시나리오의 경우 다음 예제에서는 중첩된 템플릿을 사용하는 Linux VM 하나당 두 개의 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-146">For a more realistic scenario, the following example deploys two instances at a time of a Linux VM from a nested template:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for the Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for the Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for the Public IP used to access the Virtual Machine."
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
                "description": "The Ubuntu version for the VM. This will pick a fully patched image of this given Ubuntu version."
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

## <a name="property-iteration"></a><span data-ttu-id="4f718-147">속성 반복</span><span class="sxs-lookup"><span data-stu-id="4f718-147">Property iteration</span></span>

<span data-ttu-id="4f718-148">리소스의 속성에 대해 여러 값을 만들려면 속성 요소에서 `copy` 배열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-148">To create multiple values for a property on a resource, add a `copy` array in the properties element.</span></span> <span data-ttu-id="4f718-149">이 배열에는 개체가 포함되어 있으며 각 개체에는 다음 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-149">This array contains objects, and each object has the following properties:</span></span>

* <span data-ttu-id="4f718-150">name - 여러 값을 만들 속성의 이름</span><span class="sxs-lookup"><span data-stu-id="4f718-150">name - the name of the property to create multiple values for</span></span>
* <span data-ttu-id="4f718-151">count - 만들 값 수</span><span class="sxs-lookup"><span data-stu-id="4f718-151">count - the number of values to create</span></span>
* <span data-ttu-id="4f718-152">input - 속성에 할당할 값이 포함된 개체</span><span class="sxs-lookup"><span data-stu-id="4f718-152">input - an object that contains the values to assign to the property</span></span>  

<span data-ttu-id="4f718-153">다음 예제는 가상 컴퓨터에서 `copy`를 dataDisks 속성에 적용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-153">The following example shows how to apply `copy` to the dataDisks property on a virtual machine:</span></span>

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

<span data-ttu-id="4f718-154">속성 반복 내에서 `copyIndex`를 사용하는 경우 반복의 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-154">Notice that when using `copyIndex` inside a property iteration, you must provide the name of the iteration.</span></span> <span data-ttu-id="4f718-155">리소스 반복과 함께 사용할 경우 이름을 제공할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-155">You do not have to provide the name when used with resource iteration.</span></span>

<span data-ttu-id="4f718-156">Resource Manager는 배포 중 `copy` 배열을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-156">Resource Manager expands the `copy` array during deployment.</span></span> <span data-ttu-id="4f718-157">배열 이름은 속성의 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-157">The name of the array becomes the name of the property.</span></span> <span data-ttu-id="4f718-158">입력 값은 개체 속성이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-158">The input values become the object properties.</span></span> <span data-ttu-id="4f718-159">배포된 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-159">The deployed template becomes:</span></span>

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

<span data-ttu-id="4f718-160">리소스 및 속성 반복을 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-160">You can use resource and property iteration together.</span></span> <span data-ttu-id="4f718-161">이름별로 속성 반복을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-161">Reference the property iteration by name.</span></span>

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

<span data-ttu-id="4f718-162">리소스마다 하나의 copy 요소만 속성에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-162">You can only include one copy element in the properties for each resource.</span></span> <span data-ttu-id="4f718-163">둘 이상의 속성에 대해 반복 루프를 지정하려면 복사 배열에서 여러 개체를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-163">To specify an iteration loop for more than one property, define multiple objects in the copy array.</span></span> <span data-ttu-id="4f718-164">각 개체는 개별적으로 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-164">Each object is iterated separately.</span></span> <span data-ttu-id="4f718-165">예를 들어 부하 분산 장치에서 `frontendIPConfigurations` 속성 및 `loadBalancingRules` 속성 모두에 대해 여러 인스턴스를 만들려면 단일 copy 요소에서 두 개체를 모두 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-165">For example, to create multiple instances of both the `frontendIPConfigurations` property and the `loadBalancingRules` property on a load balancer, define both objects in a single copy element:</span></span> 

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

## <a name="depend-on-resources-in-a-loop"></a><span data-ttu-id="4f718-166">루프의 리소스에 따라 달라짐</span><span class="sxs-lookup"><span data-stu-id="4f718-166">Depend on resources in a loop</span></span>
<span data-ttu-id="4f718-167">`dependsOn` 요소를 사용하여 어떤 리소스를 다른 리소스 다음에 배포하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-167">You specify that a resource is deployed after another resource by using the `dependsOn` element.</span></span> <span data-ttu-id="4f718-168">루프의 리소스 컬렉션에 따라 달라지는 리소스를 배포하려면 dependsOn 요소에 복사 루프의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-168">To deploy a resource that depends on the collection of resources in a loop, provide the name of the copy loop in the dependsOn element.</span></span> <span data-ttu-id="4f718-169">다음 예제에서는 가상 컴퓨터를 배포하기 전에 저장소 계정 3개를 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-169">The following example shows how to deploy three storage accounts before deploying the Virtual Machine.</span></span> <span data-ttu-id="4f718-170">전체 가상 컴퓨터 정의는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-170">The full Virtual Machine definition is not shown.</span></span> <span data-ttu-id="4f718-171">참고로 copy 요소의 name은 `storagecopy`로 설정되고 가상 컴퓨터에 대한 dependsOn 요소도 `storagecopy`로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-171">Notice that the copy element has name set to `storagecopy` and the dependsOn element for the Virtual Machines is also set to `storagecopy`.</span></span>

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

## <a name="create-multiple-instances-of-a-child-resource"></a><span data-ttu-id="4f718-172">자식 리소스의 여러 인스턴스 만들기</span><span class="sxs-lookup"><span data-stu-id="4f718-172">Create multiple instances of a child resource</span></span>
<span data-ttu-id="4f718-173">자식 리소스에 대해 복사 반복을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-173">You cannot use a copy loop for a child resource.</span></span> <span data-ttu-id="4f718-174">일반적으로 다른 리소스 내에 중첩된 것으로 정의된 여러 인스턴스를 만들려면 대신 해당 리소스를 최상위 리소스로 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-174">To create multiple instances of a resource that you typically define as nested within another resource, you must instead create that resource as a top-level resource.</span></span> <span data-ttu-id="4f718-175">형식 및 이름 속성을 통해 부모 리소스와의 관계를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-175">You define the relationship with the parent resource through the type and name properties.</span></span>

<span data-ttu-id="4f718-176">예를 들어, 데이터 집합을 데이터 팩터리 내에 자식 리소스로 정의한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-176">For example, suppose you typically define a dataset as a child resource within a data factory.</span></span>

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

<span data-ttu-id="4f718-177">데이터 집합의 여러 인스턴스를 만들려면 데이터 팩터리의 외부에서 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-177">To create multiple instances of data sets, move it outside of the data factory.</span></span> <span data-ttu-id="4f718-178">데이터 집합은 데이터 팩터리와 같은 수준에 있어야 하지만 여전히 데이터 팩터리의 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-178">The dataset must be at the same level as the data factory, but it is still a child resource of the data factory.</span></span> <span data-ttu-id="4f718-179">형식 및 이름 속성을 통해 데이터 집합과 데이터 팩터리 간의 관계를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-179">You preserve the relationship between data set and data factory through the type and name properties.</span></span> <span data-ttu-id="4f718-180">템플릿의 해당 위치에서 형식을 더 이상 유추할 수 없으므로 `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}` 형식으로 정규화된 형식을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-180">Since type can no longer be inferred from its position in the template, you must provide the fully qualified type in the format: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.</span></span>

<span data-ttu-id="4f718-181">데이터 팩터리 인스턴스로 부모/자식 관계를 설정하려면 부모 리소스 이름을 포함하는 데이터 집합에 대해 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-181">To establish a parent/child relationship with an instance of the data factory, provide a name for the data set that includes the parent resource name.</span></span> <span data-ttu-id="4f718-182">사용할 형식: `{parent-resource-name}/{child-resource-name}`.</span><span class="sxs-lookup"><span data-stu-id="4f718-182">Use the format: `{parent-resource-name}/{child-resource-name}`.</span></span>  

<span data-ttu-id="4f718-183">다음 예제에서는 구현을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-183">The following example shows the implementation:</span></span>

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

## <a name="conditionally-deploy-resource"></a><span data-ttu-id="4f718-184">조건부 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="4f718-184">Conditionally deploy resource</span></span>

<span data-ttu-id="4f718-185">리소스 배포 여부를 지정하려면 `condition` 요소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-185">To specify whether a resource is deployed, use the `condition` element.</span></span> <span data-ttu-id="4f718-186">이 요소 값은 true 또는 false로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-186">The value for this element resolves to true or false.</span></span> <span data-ttu-id="4f718-187">값이 true이면 리소스가 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-187">When the value is true, the resource is deployed.</span></span> <span data-ttu-id="4f718-188">값이 false이면 리소스가 배포되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-188">When the value is false, the resource is not deployed.</span></span> <span data-ttu-id="4f718-189">예를 들어 새 저장소 계정 배포 여부 또는 기존 저장소 계정 사용 여부를 지정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4f718-189">For example, to specify whether a new storage account is deployed or an existing storage account is used, use:</span></span>

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

<span data-ttu-id="4f718-190">기존 또는 새 리소스 사용 예제는 [신규 또는 기존 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-190">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="4f718-191">암호 또는 SSH 키를 사용하여 가상 컴퓨터를 배포하는 예제는 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-191">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f718-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4f718-192">Next steps</span></span>
* <span data-ttu-id="4f718-193">템플릿 섹션에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-193">If you want to learn about the sections of a template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="4f718-194">템플릿 배포 방법에 대한 자세한 내용은 [Azure 리소스 관리자 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4f718-194">To learn how to deploy your template, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>

