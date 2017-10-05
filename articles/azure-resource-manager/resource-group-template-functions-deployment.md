---
title: "Azure Resource Manager 템플릿 함수 - 배포 | Microsoft Docs"
description: "Azure Resource Manager 템플릿에서 배포 정보를 검색하는 데 사용할 수 있는 함수에 대해 설명합니다."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="6ead4-103">Azure Resource Manager 템플릿용 배포 함수</span><span class="sxs-lookup"><span data-stu-id="6ead4-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="6ead4-104">Resource Manager는 템플릿의 섹션에서 값을 가져오고 배포와 관련된 값을 가져오기 위한 다음 함수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="6ead4-105">deployment</span><span class="sxs-lookup"><span data-stu-id="6ead4-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="6ead4-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6ead4-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="6ead4-107">variables</span><span class="sxs-lookup"><span data-stu-id="6ead4-107">variables</span></span>](#variables)

<span data-ttu-id="6ead4-108">리소스, 리소스 그룹 또는 구독에서 값을 가져오려면 [리소스 함수](resource-group-template-functions-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead4-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="6ead4-109">배포</span><span class="sxs-lookup"><span data-stu-id="6ead4-109">deployment</span></span>
`deployment()`

<span data-ttu-id="6ead4-110">현재 배포 작업에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="6ead4-111">반환 값</span><span class="sxs-lookup"><span data-stu-id="6ead4-111">Return value</span></span>

<span data-ttu-id="6ead4-112">이 함수는 배포하는 동안 전달되는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="6ead4-113">반환된 개체의 속성은 배포 개체가 링크로 전달되는지 아니면 인라인 개체로 전달되는지에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="6ead4-114">배포 개체가 로컬 파일을 가리키기 위해 Azure PowerShell의 **-TemplateFile** 매개 변수를 사용할 때와 같이 인라인으로 전달되는 경우 개체는 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="6ead4-115">개체가 원격 개체를 가리키기 위해 **-TemplateUri** 매개 변수를 사용할 때와 같이 링크로 전달되는 경우 개체는 다음 형식으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="6ead4-116">설명</span><span class="sxs-lookup"><span data-stu-id="6ead4-116">Remarks</span></span>

<span data-ttu-id="6ead4-117">deployment()를 사용하여 부모 템플릿의 URI를 기반으로 하는 다른 템플릿에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="6ead4-118">예</span><span class="sxs-lookup"><span data-stu-id="6ead4-118">Example</span></span>

<span data-ttu-id="6ead4-119">다음 예제에서는 배포 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-119">The following example returns the deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="6ead4-120">앞의 예제에서는 다음 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-120">The preceding example returns the following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="6ead4-121">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6ead4-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="6ead4-122">매개 변수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-122">Returns a parameter value.</span></span> <span data-ttu-id="6ead4-123">템플릿의 매개 변수 섹션에서 지정된 매개 변수 이름을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="6ead4-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6ead4-124">Parameters</span></span>

| <span data-ttu-id="6ead4-125">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-125">Parameter</span></span> | <span data-ttu-id="6ead4-126">필수</span><span class="sxs-lookup"><span data-stu-id="6ead4-126">Required</span></span> | <span data-ttu-id="6ead4-127">형식</span><span class="sxs-lookup"><span data-stu-id="6ead4-127">Type</span></span> | <span data-ttu-id="6ead4-128">설명</span><span class="sxs-lookup"><span data-stu-id="6ead4-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6ead4-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="6ead4-129">parameterName</span></span> |<span data-ttu-id="6ead4-130">예</span><span class="sxs-lookup"><span data-stu-id="6ead4-130">Yes</span></span> |<span data-ttu-id="6ead4-131">string</span><span class="sxs-lookup"><span data-stu-id="6ead4-131">string</span></span> |<span data-ttu-id="6ead4-132">반환할 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6ead4-133">반환 값</span><span class="sxs-lookup"><span data-stu-id="6ead4-133">Return value</span></span>

<span data-ttu-id="6ead4-134">지정한 매개 변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="6ead4-135">설명</span><span class="sxs-lookup"><span data-stu-id="6ead4-135">Remarks</span></span>

<span data-ttu-id="6ead4-136">일반적으로 매개 변수를 사용하여 리소스 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="6ead4-137">다음 예제에서는 웹 사이트의 이름을 배포 중에 전달된 매개 변수 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="6ead4-138">예</span><span class="sxs-lookup"><span data-stu-id="6ead4-138">Example</span></span>

<span data-ttu-id="6ead4-139">다음 예에서는 매개 변수 함수의 간소화된 사용을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-139">The following example shows a simplified use of the parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="6ead4-140">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6ead4-141">이름</span><span class="sxs-lookup"><span data-stu-id="6ead4-141">Name</span></span> | <span data-ttu-id="6ead4-142">형식</span><span class="sxs-lookup"><span data-stu-id="6ead4-142">Type</span></span> | <span data-ttu-id="6ead4-143">값</span><span class="sxs-lookup"><span data-stu-id="6ead4-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6ead4-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6ead4-144">stringOutput</span></span> | <span data-ttu-id="6ead4-145">문자열</span><span class="sxs-lookup"><span data-stu-id="6ead4-145">String</span></span> | <span data-ttu-id="6ead4-146">옵션 1</span><span class="sxs-lookup"><span data-stu-id="6ead4-146">option 1</span></span> |
| <span data-ttu-id="6ead4-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="6ead4-147">intOutput</span></span> | <span data-ttu-id="6ead4-148">int</span><span class="sxs-lookup"><span data-stu-id="6ead4-148">Int</span></span> | <span data-ttu-id="6ead4-149">1</span><span class="sxs-lookup"><span data-stu-id="6ead4-149">1</span></span> |
| <span data-ttu-id="6ead4-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6ead4-150">objectOutput</span></span> | <span data-ttu-id="6ead4-151">Object</span><span class="sxs-lookup"><span data-stu-id="6ead4-151">Object</span></span> | <span data-ttu-id="6ead4-152">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="6ead4-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="6ead4-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6ead4-153">arrayOutput</span></span> | <span data-ttu-id="6ead4-154">배열</span><span class="sxs-lookup"><span data-stu-id="6ead4-154">Array</span></span> | <span data-ttu-id="6ead4-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="6ead4-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="6ead4-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="6ead4-156">crossOutput</span></span> | <span data-ttu-id="6ead4-157">문자열</span><span class="sxs-lookup"><span data-stu-id="6ead4-157">String</span></span> | <span data-ttu-id="6ead4-158">옵션 1</span><span class="sxs-lookup"><span data-stu-id="6ead4-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="6ead4-159">variables</span><span class="sxs-lookup"><span data-stu-id="6ead4-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="6ead4-160">변수의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-160">Returns the value of variable.</span></span> <span data-ttu-id="6ead4-161">템플릿의 변수 섹션에서 지정된 변수 이름을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="6ead4-162">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6ead4-162">Parameters</span></span>

| <span data-ttu-id="6ead4-163">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-163">Parameter</span></span> | <span data-ttu-id="6ead4-164">필수</span><span class="sxs-lookup"><span data-stu-id="6ead4-164">Required</span></span> | <span data-ttu-id="6ead4-165">형식</span><span class="sxs-lookup"><span data-stu-id="6ead4-165">Type</span></span> | <span data-ttu-id="6ead4-166">설명</span><span class="sxs-lookup"><span data-stu-id="6ead4-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6ead4-167">variableName</span><span class="sxs-lookup"><span data-stu-id="6ead4-167">variableName</span></span> |<span data-ttu-id="6ead4-168">예</span><span class="sxs-lookup"><span data-stu-id="6ead4-168">Yes</span></span> |<span data-ttu-id="6ead4-169">String</span><span class="sxs-lookup"><span data-stu-id="6ead4-169">String</span></span> |<span data-ttu-id="6ead4-170">반환할 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6ead4-171">반환 값</span><span class="sxs-lookup"><span data-stu-id="6ead4-171">Return value</span></span>

<span data-ttu-id="6ead4-172">지정한 변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="6ead4-173">설명</span><span class="sxs-lookup"><span data-stu-id="6ead4-173">Remarks</span></span>

<span data-ttu-id="6ead4-174">일반적으로 복잡한 값을 한 번만 구성하여 템플릿을 간소화하기 위해 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="6ead4-175">다음 예제에서는 저장소 계정에 대한 고유한 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-175">The following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="6ead4-176">예</span><span class="sxs-lookup"><span data-stu-id="6ead4-176">Example</span></span>

<span data-ttu-id="6ead4-177">예제 템플릿은 각기 다른 변수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-177">The example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="6ead4-178">기본 값을 사용한 이전 예제의 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6ead4-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="6ead4-179">이름</span><span class="sxs-lookup"><span data-stu-id="6ead4-179">Name</span></span> | <span data-ttu-id="6ead4-180">형식</span><span class="sxs-lookup"><span data-stu-id="6ead4-180">Type</span></span> | <span data-ttu-id="6ead4-181">값</span><span class="sxs-lookup"><span data-stu-id="6ead4-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6ead4-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="6ead4-182">exampleOutput1</span></span> | <span data-ttu-id="6ead4-183">문자열</span><span class="sxs-lookup"><span data-stu-id="6ead4-183">String</span></span> | <span data-ttu-id="6ead4-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="6ead4-184">myVariable</span></span> |
| <span data-ttu-id="6ead4-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="6ead4-185">exampleOutput2</span></span> | <span data-ttu-id="6ead4-186">배열</span><span class="sxs-lookup"><span data-stu-id="6ead4-186">Array</span></span> | <span data-ttu-id="6ead4-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="6ead4-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="6ead4-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="6ead4-188">exampleOutput3</span></span> | <span data-ttu-id="6ead4-189">문자열</span><span class="sxs-lookup"><span data-stu-id="6ead4-189">String</span></span> | <span data-ttu-id="6ead4-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="6ead4-190">myVariable</span></span> |
| <span data-ttu-id="6ead4-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="6ead4-191">exampleOutput4</span></span> |  <span data-ttu-id="6ead4-192">Object</span><span class="sxs-lookup"><span data-stu-id="6ead4-192">Object</span></span> | <span data-ttu-id="6ead4-193">{“property1”: “value1”, “property2”: “value2”}</span><span class="sxs-lookup"><span data-stu-id="6ead4-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ead4-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ead4-194">Next steps</span></span>
* <span data-ttu-id="6ead4-195">Azure Resource Manager 템플릿의 섹션에 대한 설명은 [Azure Resource Manager 템플릿 작성](resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead4-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6ead4-196">여러 템플릿을 병합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead4-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6ead4-197">리소스 유형을 만들 때 지정된 횟수만큼 반복하려면 [Azure 리소스 관리자에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead4-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="6ead4-198">만든 템플릿을 배포하는 방법을 보려면 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ead4-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

