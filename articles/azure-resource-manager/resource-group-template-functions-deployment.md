---
title: "aaaAzure 리소스 관리자 템플릿 함수 배포 | Microsoft Docs"
description: "Hello 함수 toouse는 Azure 리소스 관리자 템플릿 tooretrieve 배포 정보에 설명합니다."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="0808e-103">Azure Resource Manager 템플릿용 배포 함수</span><span class="sxs-lookup"><span data-stu-id="0808e-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="0808e-104">리소스 관리자는 hello 다음 hello 서식 파일의 섹션에서 값 가져오기에 대 한 함수 및 관련된 toohello 배포 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="0808e-105">deployment</span><span class="sxs-lookup"><span data-stu-id="0808e-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="0808e-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0808e-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="0808e-107">variables</span><span class="sxs-lookup"><span data-stu-id="0808e-107">variables</span></span>](#variables)

<span data-ttu-id="0808e-108">리소스, 리소스 그룹 또는 구독에서 tooget 값 참조 [리소스 함수](resource-group-template-functions-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="0808e-109">배포</span><span class="sxs-lookup"><span data-stu-id="0808e-109">deployment</span></span>
`deployment()`

<span data-ttu-id="0808e-110">Hello 현재 배포 작업에 대 한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="0808e-111">반환 값</span><span class="sxs-lookup"><span data-stu-id="0808e-111">Return value</span></span>

<span data-ttu-id="0808e-112">이 함수는 배포 중에 전달 되는 hello 개체를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="0808e-113">개체를 반환 하는 hello에 hello 속성 hello 배포 개체를 전달 했는지 여부 또는 인라인 개체로 링크에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="0808e-114">Hello 배포 전달 경우 인라인와 같은 hello를 사용 하는 경우 **-TemplateFile** 매개 변수 hello Azure PowerShell toopoint tooa 로컬 파일에서 개체의 형식에 따라 hello을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

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

<span data-ttu-id="0808e-115">Hello 개체 때 hello를 사용 하 여 같은 링크로 전달 되 면 **-TemplateUri** 매개 변수 toopoint tooa 원격 개체 형식에 따라 hello에 hello 개체가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="0808e-116">설명</span><span class="sxs-lookup"><span data-stu-id="0808e-116">Remarks</span></span>

<span data-ttu-id="0808e-117">Hello hello 부모 템플릿의 URI에 따라 배포 선정 () toolink tooanother 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="0808e-118">예제</span><span class="sxs-lookup"><span data-stu-id="0808e-118">Example</span></span>

<span data-ttu-id="0808e-119">hello 다음 예제에서는 개체를 반환 hello 배포:</span><span class="sxs-lookup"><span data-stu-id="0808e-119">hello following example returns hello deployment object:</span></span>

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

<span data-ttu-id="0808e-120">hello 위 예제에서는 반환 개체를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="0808e-120">hello preceding example returns hello following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="0808e-121">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0808e-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="0808e-122">매개 변수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-122">Returns a parameter value.</span></span> <span data-ttu-id="0808e-123">지정한 매개 변수 이름이 hello hello 템플릿의 hello 매개 변수 섹션에서 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="0808e-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0808e-124">Parameters</span></span>

| <span data-ttu-id="0808e-125">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-125">Parameter</span></span> | <span data-ttu-id="0808e-126">필수</span><span class="sxs-lookup"><span data-stu-id="0808e-126">Required</span></span> | <span data-ttu-id="0808e-127">형식</span><span class="sxs-lookup"><span data-stu-id="0808e-127">Type</span></span> | <span data-ttu-id="0808e-128">설명</span><span class="sxs-lookup"><span data-stu-id="0808e-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0808e-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="0808e-129">parameterName</span></span> |<span data-ttu-id="0808e-130">예</span><span class="sxs-lookup"><span data-stu-id="0808e-130">Yes</span></span> |<span data-ttu-id="0808e-131">string</span><span class="sxs-lookup"><span data-stu-id="0808e-131">string</span></span> |<span data-ttu-id="0808e-132">hello 매개 변수 tooreturn의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0808e-133">반환 값</span><span class="sxs-lookup"><span data-stu-id="0808e-133">Return value</span></span>

<span data-ttu-id="0808e-134">hello hello 값 매개 변수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="0808e-135">설명</span><span class="sxs-lookup"><span data-stu-id="0808e-135">Remarks</span></span>

<span data-ttu-id="0808e-136">일반적으로 매개 변수 tooset 리소스 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="0808e-137">hello 다음 예제에서는 설정 배포 중에 전달 하는 웹 사이트 toohello 매개 변수 값의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="0808e-138">예제</span><span class="sxs-lookup"><span data-stu-id="0808e-138">Example</span></span>

<span data-ttu-id="0808e-139">hello 다음 예제에서는 hello 매개 변수 함수를 사용 하는 단순화</span><span class="sxs-lookup"><span data-stu-id="0808e-139">hello following example shows a simplified use of hello parameters function.</span></span>

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

<span data-ttu-id="0808e-140">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="0808e-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="0808e-141">이름</span><span class="sxs-lookup"><span data-stu-id="0808e-141">Name</span></span> | <span data-ttu-id="0808e-142">형식</span><span class="sxs-lookup"><span data-stu-id="0808e-142">Type</span></span> | <span data-ttu-id="0808e-143">값</span><span class="sxs-lookup"><span data-stu-id="0808e-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0808e-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="0808e-144">stringOutput</span></span> | <span data-ttu-id="0808e-145">문자열</span><span class="sxs-lookup"><span data-stu-id="0808e-145">String</span></span> | <span data-ttu-id="0808e-146">옵션 1</span><span class="sxs-lookup"><span data-stu-id="0808e-146">option 1</span></span> |
| <span data-ttu-id="0808e-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="0808e-147">intOutput</span></span> | <span data-ttu-id="0808e-148">int</span><span class="sxs-lookup"><span data-stu-id="0808e-148">Int</span></span> | <span data-ttu-id="0808e-149">1</span><span class="sxs-lookup"><span data-stu-id="0808e-149">1</span></span> |
| <span data-ttu-id="0808e-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="0808e-150">objectOutput</span></span> | <span data-ttu-id="0808e-151">Object</span><span class="sxs-lookup"><span data-stu-id="0808e-151">Object</span></span> | <span data-ttu-id="0808e-152">{“one”: “a”, “two”: “b”}</span><span class="sxs-lookup"><span data-stu-id="0808e-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="0808e-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="0808e-153">arrayOutput</span></span> | <span data-ttu-id="0808e-154">배열</span><span class="sxs-lookup"><span data-stu-id="0808e-154">Array</span></span> | <span data-ttu-id="0808e-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="0808e-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="0808e-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="0808e-156">crossOutput</span></span> | <span data-ttu-id="0808e-157">문자열</span><span class="sxs-lookup"><span data-stu-id="0808e-157">String</span></span> | <span data-ttu-id="0808e-158">옵션 1</span><span class="sxs-lookup"><span data-stu-id="0808e-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="0808e-159">variables</span><span class="sxs-lookup"><span data-stu-id="0808e-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="0808e-160">반환 hello 변수의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-160">Returns hello value of variable.</span></span> <span data-ttu-id="0808e-161">지정한 변수 이름이 hello hello 템플릿의 hello 변수 섹션에서 정의 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="0808e-162">매개 변수</span><span class="sxs-lookup"><span data-stu-id="0808e-162">Parameters</span></span>

| <span data-ttu-id="0808e-163">매개 변수를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-163">Parameter</span></span> | <span data-ttu-id="0808e-164">필수</span><span class="sxs-lookup"><span data-stu-id="0808e-164">Required</span></span> | <span data-ttu-id="0808e-165">형식</span><span class="sxs-lookup"><span data-stu-id="0808e-165">Type</span></span> | <span data-ttu-id="0808e-166">설명</span><span class="sxs-lookup"><span data-stu-id="0808e-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0808e-167">variableName</span><span class="sxs-lookup"><span data-stu-id="0808e-167">variableName</span></span> |<span data-ttu-id="0808e-168">예</span><span class="sxs-lookup"><span data-stu-id="0808e-168">Yes</span></span> |<span data-ttu-id="0808e-169">문자열</span><span class="sxs-lookup"><span data-stu-id="0808e-169">String</span></span> |<span data-ttu-id="0808e-170">hello 변수 tooreturn의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0808e-171">반환 값</span><span class="sxs-lookup"><span data-stu-id="0808e-171">Return value</span></span>

<span data-ttu-id="0808e-172">hello 지정 변수의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="0808e-173">설명</span><span class="sxs-lookup"><span data-stu-id="0808e-173">Remarks</span></span>

<span data-ttu-id="0808e-174">일반적으로 사용 하면 변수 toosimplify 서식 파일에 복잡 한 값을 한 번만 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="0808e-175">hello 다음 구성 예제는 저장소 계정에 대 한 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-175">hello following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="0808e-176">예제</span><span class="sxs-lookup"><span data-stu-id="0808e-176">Example</span></span>

<span data-ttu-id="0808e-177">hello 예제 템플릿 각기 다른 변수 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-177">hello example template returns different variable values.</span></span>

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

<span data-ttu-id="0808e-178">hello는 hello 기본값을 사용 하는 예제는 hello 앞에서 출력:</span><span class="sxs-lookup"><span data-stu-id="0808e-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="0808e-179">이름</span><span class="sxs-lookup"><span data-stu-id="0808e-179">Name</span></span> | <span data-ttu-id="0808e-180">형식</span><span class="sxs-lookup"><span data-stu-id="0808e-180">Type</span></span> | <span data-ttu-id="0808e-181">값</span><span class="sxs-lookup"><span data-stu-id="0808e-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0808e-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="0808e-182">exampleOutput1</span></span> | <span data-ttu-id="0808e-183">문자열</span><span class="sxs-lookup"><span data-stu-id="0808e-183">String</span></span> | <span data-ttu-id="0808e-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="0808e-184">myVariable</span></span> |
| <span data-ttu-id="0808e-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="0808e-185">exampleOutput2</span></span> | <span data-ttu-id="0808e-186">배열</span><span class="sxs-lookup"><span data-stu-id="0808e-186">Array</span></span> | <span data-ttu-id="0808e-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="0808e-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="0808e-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="0808e-188">exampleOutput3</span></span> | <span data-ttu-id="0808e-189">문자열</span><span class="sxs-lookup"><span data-stu-id="0808e-189">String</span></span> | <span data-ttu-id="0808e-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="0808e-190">myVariable</span></span> |
| <span data-ttu-id="0808e-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="0808e-191">exampleOutput4</span></span> |  <span data-ttu-id="0808e-192">Object</span><span class="sxs-lookup"><span data-stu-id="0808e-192">Object</span></span> | <span data-ttu-id="0808e-193">{“property1”: “value1”, “property2”: “value2”}</span><span class="sxs-lookup"><span data-stu-id="0808e-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0808e-194">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0808e-194">Next steps</span></span>
* <span data-ttu-id="0808e-195">Azure 리소스 관리자 템플릿의 hello 섹션에 대 한 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0808e-196">toomerge 템플릿이 여러 개 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="0808e-197">지정 된 횟수 만큼 tooiterate 리소스의 종류를 만들 때 참조 [Azure 리소스 관리자 리소스의 여러 인스턴스를 만들](resource-group-create-multiple.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="0808e-198">toosee toodeploy hello 서식 파일을 만든 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0808e-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

