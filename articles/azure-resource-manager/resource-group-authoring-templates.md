---
title: "Azure Resource Manager 템플릿 구조 및 구문 | Microsoft Docs"
description: "선언적 JSON 구문을 사용하여 Azure Resource Manager 템플릿의 구조 및 속성을 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: dc9b64062d7f68c83aa090eec96744819a5ca423
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-the-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="3042e-103">Azure Resource Manager 템플릿의 구조 및 구문 이해</span><span class="sxs-lookup"><span data-stu-id="3042e-103">Understand the structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="3042e-104">이 항목에서는 Azure Resource Manager 템플릿의 구조에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-104">This topic describes the structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="3042e-105">여기서는 템플릿의 다른 섹션 및 해당 섹션에서 사용할 수 있는 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-105">It presents the different sections of a template and the properties that are available in those sections.</span></span> <span data-ttu-id="3042e-106">템플릿은 배포에 대한 값을 생성하는 데 사용할 수 있는 식과 JSON으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="3042e-107">템플릿 만들기에 관한 단계별 연습은 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="3042e-108">템플릿 형식</span><span class="sxs-lookup"><span data-stu-id="3042e-108">Template format</span></span>
<span data-ttu-id="3042e-109">가장 간단한 구조의 템플릿에 포함되는 요소는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-109">In its simplest structure, a template contains the following elements:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| <span data-ttu-id="3042e-110">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3042e-110">Element name</span></span> | <span data-ttu-id="3042e-111">필수</span><span class="sxs-lookup"><span data-stu-id="3042e-111">Required</span></span> | <span data-ttu-id="3042e-112">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3042e-113">$schema</span><span class="sxs-lookup"><span data-stu-id="3042e-113">$schema</span></span> |<span data-ttu-id="3042e-114">예</span><span class="sxs-lookup"><span data-stu-id="3042e-114">Yes</span></span> |<span data-ttu-id="3042e-115">템플릿 언어의 버전을 설명하는 JSON 스키마 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-115">Location of the JSON schema file that describes the version of the template language.</span></span> <span data-ttu-id="3042e-116">위 예제에서 보여 주는 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-116">Use the URL shown in the preceding example.</span></span> |
| <span data-ttu-id="3042e-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="3042e-117">contentVersion</span></span> |<span data-ttu-id="3042e-118">예</span><span class="sxs-lookup"><span data-stu-id="3042e-118">Yes</span></span> |<span data-ttu-id="3042e-119">템플릿의 버전입니다(예: 1.0.0.0).</span><span class="sxs-lookup"><span data-stu-id="3042e-119">Version of the template (such as 1.0.0.0).</span></span> <span data-ttu-id="3042e-120">이 요소에 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-120">You can provide any value for this element.</span></span> <span data-ttu-id="3042e-121">템플릿을 사용하여 리소스를 배포할 때 이 값을 사용하면 정확한 템플릿이 사용되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-121">When deploying resources using the template, this value can be used to make sure that the right template is being used.</span></span> |
| <span data-ttu-id="3042e-122">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3042e-122">parameters</span></span> |<span data-ttu-id="3042e-123">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-123">No</span></span> |<span data-ttu-id="3042e-124">배포를 실행하여 리소스 배포를 사용자 지정할 때 제공되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-124">Values that are provided when deployment is executed to customize resource deployment.</span></span> |
| <span data-ttu-id="3042e-125">variables</span><span class="sxs-lookup"><span data-stu-id="3042e-125">variables</span></span> |<span data-ttu-id="3042e-126">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-126">No</span></span> |<span data-ttu-id="3042e-127">템플릿에서 템플릿 언어 식을 단순화하는 JSON 조각으로 사용되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-127">Values that are used as JSON fragments in the template to simplify template language expressions.</span></span> |
| <span data-ttu-id="3042e-128">리소스</span><span class="sxs-lookup"><span data-stu-id="3042e-128">resources</span></span> |<span data-ttu-id="3042e-129">예</span><span class="sxs-lookup"><span data-stu-id="3042e-129">Yes</span></span> |<span data-ttu-id="3042e-130">리소스 그룹에 배포 또는 업데이트되는 리소스 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="3042e-131">outputs</span><span class="sxs-lookup"><span data-stu-id="3042e-131">outputs</span></span> |<span data-ttu-id="3042e-132">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-132">No</span></span> |<span data-ttu-id="3042e-133">배포 후 반환되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="3042e-134">각 요소에는 사용자가 설정할 수 있는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-134">Each element contains properties you can set.</span></span> <span data-ttu-id="3042e-135">다음 예제에서는 템플릿에 대한 전체 구문이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-135">The following example contains the full syntax for a template:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-the parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

<span data-ttu-id="3042e-136">템플릿의 섹션에 대해서는 이 항목의 뒷부분에서 더 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-136">We examine the sections of the template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="3042e-137">식 및 함수</span><span class="sxs-lookup"><span data-stu-id="3042e-137">Expressions and functions</span></span>
<span data-ttu-id="3042e-138">템플릿의 기본 구문은 JSON이지만,</span><span class="sxs-lookup"><span data-stu-id="3042e-138">The basic syntax of the template is JSON.</span></span> <span data-ttu-id="3042e-139">식 및 함수를 사용하면 템플릿에서 사용할 수 있는 JSON 값을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-139">However, expressions and functions extend the JSON values available within the template.</span></span>  <span data-ttu-id="3042e-140">식은 JSON 문자열 리터럴 내에서 작성되며, 첫 번째 및 마지막 문자가 각각 대괄호 `[` 및 `]`입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-140">Expressions are written within JSON string literals whose first and last characters are the brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="3042e-141">식의 값은 템플릿을 배포할 때 평가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-141">The value of the expression is evaluated when the template is deployed.</span></span> <span data-ttu-id="3042e-142">문자열 리터럴로 작성되지만 식의 평가 결과는 실제 식에 따라 다른 JSON 형식(예: 배열 또는 정수)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-142">While written as a string literal, the result of evaluating the expression can be of a different JSON type, such as an array or integer, depending on the actual expression.</span></span>  <span data-ttu-id="3042e-143">리터럴 문자열을 대괄호 `[`로 시작하되, 식으로 해석되지 않게 하려면 문자 `[[`로 시작하도록 추가 대괄호를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-143">To have a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket to start the string with `[[`.</span></span>

<span data-ttu-id="3042e-144">일반적으로 배포를 구성하기 위한 작업을 수행하는 함수를 식과 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-144">Typically, you use expressions with functions to perform operations for configuring the deployment.</span></span> <span data-ttu-id="3042e-145">JavaScript에서와 마찬가지로 함수 호출은 `functionName(arg1,arg2,arg3)`과 같이 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="3042e-146">점과 [인덱스] 연산자를 사용하여 속성을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-146">You reference properties by using the dot and [index] operators.</span></span>

<span data-ttu-id="3042e-147">다음 예제에서는 값을 생성할 때 여러 함수를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-147">The following example shows how to use several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="3042e-148">템플릿 함수의 전체 목록을 보려면 [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-148">For the full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="3042e-149">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3042e-149">Parameters</span></span>
<span data-ttu-id="3042e-150">템플릿의 매개 변수 섹션에서는 리소스를 배포할 때 입력할 수 있는 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-150">In the parameters section of the template, you specify which values you can input when deploying the resources.</span></span> <span data-ttu-id="3042e-151">이러한 매개 변수 값을 사용하여 개발, 테스트 및 프로덕션 등의 특정 환경에 맞게 조정되는 값을 제공함으로써 배포를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-151">These parameter values enable you to customize the deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="3042e-152">템플릿에서 매개 변수를 제공할 필요는 없지만 매개 변수가 없으면 템플릿이 항상 이름, 위치 및 속성이 같은 동일한 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-152">You do not have to provide parameters in your template, but without parameters your template would always deploy the same resources with the same names, locations, and properties.</span></span>

<span data-ttu-id="3042e-153">다음과 같은 구조를 사용하여 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-153">You define parameters with the following structure:</span></span>

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-the parameter>" 
        }
    }
}
```

| <span data-ttu-id="3042e-154">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3042e-154">Element name</span></span> | <span data-ttu-id="3042e-155">필수</span><span class="sxs-lookup"><span data-stu-id="3042e-155">Required</span></span> | <span data-ttu-id="3042e-156">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3042e-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="3042e-157">parameterName</span></span> |<span data-ttu-id="3042e-158">예</span><span class="sxs-lookup"><span data-stu-id="3042e-158">Yes</span></span> |<span data-ttu-id="3042e-159">매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-159">Name of the parameter.</span></span> <span data-ttu-id="3042e-160">유효한 JavaScript 식별자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="3042e-161">type</span><span class="sxs-lookup"><span data-stu-id="3042e-161">type</span></span> |<span data-ttu-id="3042e-162">예</span><span class="sxs-lookup"><span data-stu-id="3042e-162">Yes</span></span> |<span data-ttu-id="3042e-163">매개 변수 값의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-163">Type of the parameter value.</span></span> <span data-ttu-id="3042e-164">이 테이블 다음에 나오는 허용된 유형 목록을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-164">See the list of allowed types after this table.</span></span> |
| <span data-ttu-id="3042e-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="3042e-165">defaultValue</span></span> |<span data-ttu-id="3042e-166">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-166">No</span></span> |<span data-ttu-id="3042e-167">매개 변수 값을 제공하지 않는 경우 매개 변수의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-167">Default value for the parameter, if no value is provided for the parameter.</span></span> |
| <span data-ttu-id="3042e-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="3042e-168">allowedValues</span></span> |<span data-ttu-id="3042e-169">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-169">No</span></span> |<span data-ttu-id="3042e-170">올바른 값을 제공하도록 매개 변수에 대해 허용되는 값의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-170">Array of allowed values for the parameter to make sure that the right value is provided.</span></span> |
| <span data-ttu-id="3042e-171">minValue</span><span class="sxs-lookup"><span data-stu-id="3042e-171">minValue</span></span> |<span data-ttu-id="3042e-172">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-172">No</span></span> |<span data-ttu-id="3042e-173">Int 형식 매개 변수의 최소값이며, 이 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-173">The minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="3042e-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="3042e-174">maxValue</span></span> |<span data-ttu-id="3042e-175">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-175">No</span></span> |<span data-ttu-id="3042e-176">Int 형식 매개 변수의 최대값이며, 이 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-176">The maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="3042e-177">minLength</span><span class="sxs-lookup"><span data-stu-id="3042e-177">minLength</span></span> |<span data-ttu-id="3042e-178">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-178">No</span></span> |<span data-ttu-id="3042e-179">string, secureString 및 array 형식 매개 변수의 최소 길이이며, 이 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-179">The minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="3042e-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="3042e-180">maxLength</span></span> |<span data-ttu-id="3042e-181">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-181">No</span></span> |<span data-ttu-id="3042e-182">string, secureString 및 array 형식 매개 변수의 최대 길이이며, 이 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-182">The maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="3042e-183">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-183">description</span></span> |<span data-ttu-id="3042e-184">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-184">No</span></span> |<span data-ttu-id="3042e-185">포털에서 사용자에게 표시되는 매개 변수의 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-185">Description of the parameter that is displayed to users through the portal.</span></span> |

<span data-ttu-id="3042e-186">허용되는 유형 및 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-186">The allowed types and values are:</span></span>

* <span data-ttu-id="3042e-187">**string**</span><span class="sxs-lookup"><span data-stu-id="3042e-187">**string**</span></span>
* <span data-ttu-id="3042e-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="3042e-188">**secureString**</span></span>
* <span data-ttu-id="3042e-189">**int**</span><span class="sxs-lookup"><span data-stu-id="3042e-189">**int**</span></span>
* <span data-ttu-id="3042e-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="3042e-190">**bool**</span></span>
* <span data-ttu-id="3042e-191">**object**</span><span class="sxs-lookup"><span data-stu-id="3042e-191">**object**</span></span> 
* <span data-ttu-id="3042e-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="3042e-192">**secureObject**</span></span>
* <span data-ttu-id="3042e-193">**array**</span><span class="sxs-lookup"><span data-stu-id="3042e-193">**array**</span></span>

<span data-ttu-id="3042e-194">매개 변수를 선택적으로 지정하려면 defaultValue를 제공합니다(빈 문자열 가능).</span><span class="sxs-lookup"><span data-stu-id="3042e-194">To specify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="3042e-195">템플릿에 템플릿을 배포하는 명령의 매개 변수와 일치하는 매개 변수 이름을 지정하면 제공하는 값에 대한 모호성이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-195">If you specify a parameter name in your template that matches a parameter in the command to deploy the template, there is potential ambiguity about the values you provide.</span></span> <span data-ttu-id="3042e-196">Resource Manager는 템플릿 매개 변수에 **FromTemplate**이라는 후위를 추가하여 이러한 혼동을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-196">Resource Manager resolves this confusion by adding the postfix **FromTemplate** to the template parameter.</span></span> <span data-ttu-id="3042e-197">예를 들어 템플릿에 **ResourceGroupName**이라는 매개 변수가 포함되면, [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet의 **ResourceGroupName** 매개 변수와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="3042e-198">배포하는 동안 **ResourceGroupNameFromTemplate**에 대한 값을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-198">During deployment, you are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="3042e-199">일반적으로 배포 작업에 사용되는 매개 변수와 동일한 이름을 가진 매개 변수를 명명하지 않음으로써 이러한 혼동이 발생하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-199">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="3042e-200">모든 암호와 키, 기타 비밀은 **secureString** 유형을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-200">All passwords, keys, and other secrets should use the **secureString** type.</span></span> <span data-ttu-id="3042e-201">JSON 개체에 중요한 데이터를 전달하는 경우 **secureObject** 유형을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-201">If you pass sensitive data in a JSON object, use the **secureObject** type.</span></span> <span data-ttu-id="3042e-202">리소스 배포 후에는 secureString 또는 secureObject 형식의 템플릿 매개 변수를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="3042e-203">예를 들어 배포 기록의 다음 항목은 secureString 및 secureObject가 아닌 문자열과 개체에 대한 값을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-203">For example, the following entry in the deployment history shows the value for a string and object but not for secureString and secureObject.</span></span>
>
> ![배포 값 표시](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="3042e-205">다음 예제에서는 매개 변수를 정의하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-205">The following example shows how to define parameters:</span></span>

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

<span data-ttu-id="3042e-206">배포 중에 매개 변수 값을 입력하는 방법은 [Azure Resource Manager 템플릿을 사용하여 응용 프로그램 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-206">For how to input the parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="3042e-207">variables</span><span class="sxs-lookup"><span data-stu-id="3042e-207">Variables</span></span>
<span data-ttu-id="3042e-208">변수 섹션에서 템플릿을 통해 사용할 수 있는 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-208">In the variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="3042e-209">변수를 정의할 필요는 없지만 종종 변수를 통해 복잡한 식을 줄이면 템플릿이 단순화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-209">You do not need to define variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="3042e-210">다음과 같은 구조를 사용하여 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-210">You define variables with the following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="3042e-211">다음 예제에서는 두 매개 변수 값에서 생성된 변수를 정의하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-211">The following example shows how to define a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="3042e-212">다음 예제에서는 복합 JSON 유형인 변수와 다른 변수에서 생성된 변수를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-212">The next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a><span data-ttu-id="3042e-213">리소스</span><span class="sxs-lookup"><span data-stu-id="3042e-213">Resources</span></span>
<span data-ttu-id="3042e-214">리소스 섹션에서 배포되거나 업데이트되는 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-214">In the resources section, you define the resources that are deployed or updated.</span></span> <span data-ttu-id="3042e-215">여기서는 올바른 값을 제공하기 위해 배포하는 유형을 이해해야 하기 때문에 템플릿이 더 복잡해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-215">This section can get complicated because you must understand the types you are deploying to provide the right values.</span></span> <span data-ttu-id="3042e-216">사용자가 설정해야 하는 리소스 특정 값(apiVersion, 형식 및 속성)의 경우 [Azure Resource Manager 템플릿에서 리소스 정의](/azure/templates/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-216">For the resource-specific values (apiVersion, type, and properties) that you need to set, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="3042e-217">다음과 같은 구조를 사용하여 리소스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-217">You define resources with the following structure:</span></span>

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| <span data-ttu-id="3042e-218">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3042e-218">Element name</span></span> | <span data-ttu-id="3042e-219">필수</span><span class="sxs-lookup"><span data-stu-id="3042e-219">Required</span></span> | <span data-ttu-id="3042e-220">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3042e-221">condition</span><span class="sxs-lookup"><span data-stu-id="3042e-221">condition</span></span> | <span data-ttu-id="3042e-222">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-222">No</span></span> | <span data-ttu-id="3042e-223">리소스 배포 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-223">Boolean value that indicates whether the resource is deployed.</span></span> |
| <span data-ttu-id="3042e-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3042e-224">apiVersion</span></span> |<span data-ttu-id="3042e-225">예</span><span class="sxs-lookup"><span data-stu-id="3042e-225">Yes</span></span> |<span data-ttu-id="3042e-226">리소스를 만들 때 사용하는 REST API의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-226">Version of the REST API to use for creating the resource.</span></span> |
| <span data-ttu-id="3042e-227">type</span><span class="sxs-lookup"><span data-stu-id="3042e-227">type</span></span> |<span data-ttu-id="3042e-228">예</span><span class="sxs-lookup"><span data-stu-id="3042e-228">Yes</span></span> |<span data-ttu-id="3042e-229">리소스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-229">Type of the resource.</span></span> <span data-ttu-id="3042e-230">이 값은 리소스 공급자의 네임스페이스와 리소스 형식을 조합한 값입니다(예: **Microsoft.Storage/storageAccounts**).</span><span class="sxs-lookup"><span data-stu-id="3042e-230">This value is a combination of the namespace of the resource provider and the resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="3042e-231">name</span><span class="sxs-lookup"><span data-stu-id="3042e-231">name</span></span> |<span data-ttu-id="3042e-232">예</span><span class="sxs-lookup"><span data-stu-id="3042e-232">Yes</span></span> |<span data-ttu-id="3042e-233">리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-233">Name of the resource.</span></span> <span data-ttu-id="3042e-234">이 이름은 RFC3986에 정의된 URI 구성 요소 제한을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-234">The name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="3042e-235">또한 리소스 이름을 외부에 노출하는 Azure 서비스는 다른 ID를 스푸핑하려는 시도가 아님을 확인하기 위해 이름의 유효성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-235">In addition, Azure services that expose the resource name to outside parties validate the name to make sure it is not an attempt to spoof another identity.</span></span> |
| <span data-ttu-id="3042e-236">location</span><span class="sxs-lookup"><span data-stu-id="3042e-236">location</span></span> |<span data-ttu-id="3042e-237">다름</span><span class="sxs-lookup"><span data-stu-id="3042e-237">Varies</span></span> |<span data-ttu-id="3042e-238">제공된 리소스의 지역적 위치를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-238">Supported geo-locations of the provided resource.</span></span> <span data-ttu-id="3042e-239">사용 가능한 위치 중 하나를 선택할 수 있지만 대개는 사용자에게 가까운 하나를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-239">You can select any of the available locations, but typically it makes sense to pick one that is close to your users.</span></span> <span data-ttu-id="3042e-240">일반적으로 동일한 지역에서 서로 상호 작용하도록 리소스를 배치하는 것도 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-240">Usually, it also makes sense to place resources that interact with each other in the same region.</span></span> <span data-ttu-id="3042e-241">대부분의 리소스 종류에는 위치가 필요하지만 일부 종류(예: 역할 할당)에는 위치가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="3042e-242">[Azure Resource Manager 템플릿에서 리소스 위치 설정](resource-manager-template-location.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="3042e-243">tags</span><span class="sxs-lookup"><span data-stu-id="3042e-243">tags</span></span> |<span data-ttu-id="3042e-244">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-244">No</span></span> |<span data-ttu-id="3042e-245">리소스와 연결된 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-245">Tags that are associated with the resource.</span></span> <span data-ttu-id="3042e-246">[Azure Resource Manager 템플릿에서 리소스에 태그 지정](resource-manager-template-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="3042e-247">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-247">comments</span></span> |<span data-ttu-id="3042e-248">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-248">No</span></span> |<span data-ttu-id="3042e-249">템플릿에서 리소스를 문서화하는 내용에 대한 참고</span><span class="sxs-lookup"><span data-stu-id="3042e-249">Your notes for documenting the resources in your template</span></span> |
| <span data-ttu-id="3042e-250">복사</span><span class="sxs-lookup"><span data-stu-id="3042e-250">copy</span></span> |<span data-ttu-id="3042e-251">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-251">No</span></span> |<span data-ttu-id="3042e-252">인스턴스가 둘 이상 필요한 경우 만드는 리소스의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-252">If more than one instance is needed, the number of resources to create.</span></span> <span data-ttu-id="3042e-253">기본 모드는 병렬입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-253">The default mode is parallel.</span></span> <span data-ttu-id="3042e-254">일부 리소스를 동시에 배포하지 않으려면 직렬 모드를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-254">Specify serial mode when you do not want all or the resources to deploy at the same time.</span></span> <span data-ttu-id="3042e-255">자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="3042e-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="3042e-256">dependsOn</span></span> |<span data-ttu-id="3042e-257">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-257">No</span></span> |<span data-ttu-id="3042e-258">이 리소스를 배포하기 전에 배포해야 하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="3042e-259">Resource Manager는 리소스 간의 종속성을 평가한 후 올바른 순서에 따라 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-259">Resource Manager evaluates the dependencies between resources and deploys them in the correct order.</span></span> <span data-ttu-id="3042e-260">리소스는 서로 종속되지 않을 경우 병렬로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="3042e-261">이 값은 리소스 이름 또는 리소스 고유 식별자의 쉼표로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-261">The value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="3042e-262">이 템플릿에 배포된 리소스만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="3042e-263">이 템플릿에 정의되지 않은 리소스는 이미 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="3042e-264">불필요한 종속성은 배포 속도를 느리게 만들고 순환 종속성을 만들기 때문에 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="3042e-265">종속성 설정에 대한 지침은 [Azure Resource Manager 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="3042e-266">properties</span><span class="sxs-lookup"><span data-stu-id="3042e-266">properties</span></span> |<span data-ttu-id="3042e-267">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-267">No</span></span> |<span data-ttu-id="3042e-268">리소스별 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="3042e-269">속성의 값은 리소스를 만들기 위해 REST API 작업(PUT 메서드)에 대한 요청 본문에 제공하는 값과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-269">The values for the properties are the same as the values you provide in the request body for the REST API operation (PUT method) to create the resource.</span></span> <span data-ttu-id="3042e-270">복사 배열을 지정하여 속성의 여러 인스턴스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-270">You can also specify a copy array to create multiple instances of a property.</span></span> <span data-ttu-id="3042e-271">자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="3042e-272">리소스</span><span class="sxs-lookup"><span data-stu-id="3042e-272">resources</span></span> |<span data-ttu-id="3042e-273">아니요</span><span class="sxs-lookup"><span data-stu-id="3042e-273">No</span></span> |<span data-ttu-id="3042e-274">정의 중인 리소스에 종속되는 하위 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-274">Child resources that depend on the resource being defined.</span></span> <span data-ttu-id="3042e-275">부모 리소스의 스키마에서 허용되는 리소스 유형만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-275">Only provide resource types that are permitted by the schema of the parent resource.</span></span> <span data-ttu-id="3042e-276">자식 리소스의 정규화된 유형에는 부모 리소스 유형이 포함됩니다(예: **Microsoft.Web/sites/extensions**).</span><span class="sxs-lookup"><span data-stu-id="3042e-276">The fully qualified type of the child resource includes the parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="3042e-277">부모 리소스에 대한 종속성은 암시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-277">Dependency on the parent resource is not implied.</span></span> <span data-ttu-id="3042e-278">해당 종속성을 명시적으로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="3042e-279">리소스 섹션에는 배포할 리소스의 배열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-279">The resources section contains an array of the resources to deploy.</span></span> <span data-ttu-id="3042e-280">각 리소스 내에서 자식 리소스의 배열도 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="3042e-281">따라서 리소스 섹션에는 다음과 같은 구조가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-281">Therefore, your resources section could have a structure like:</span></span>

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

<span data-ttu-id="3042e-282">자식 리소스를 정의하는 방법에 대한 자세한 내용은 [Resource Manager 템플릿에서 자식 리소스에 대한 이름 및 형식 설정](resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="3042e-283">**condition** 요소는 리소스 배포 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-283">The **condition** element specifies whether the resource is deployed.</span></span> <span data-ttu-id="3042e-284">이 요소 값은 true 또는 false로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-284">The value for this element resolves to true or false.</span></span> <span data-ttu-id="3042e-285">예를 들어 새 저장소 계정 배포 여부를 지정하려면 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-285">For example, to specify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="3042e-286">기존 또는 새 리소스 사용 예제는 [신규 또는 기존 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="3042e-287">가상 컴퓨터를 암호로 배포할지 SSH 키로 배포할지 지정하려면 템플릿에서 두 버전의 가상 컴퓨터를 정의하고 **condition**을 사용하여 사용을 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-287">To specify whether a virtual machine is deployed with a password or SSH key, define two versions of the virtual machine in your template and use **condition** to differentiate usage.</span></span> <span data-ttu-id="3042e-288">배포할 시나리오를 지정하는 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-288">Pass a parameter that specifies which scenario to deploy.</span></span>

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

<span data-ttu-id="3042e-289">암호 또는 SSH 키를 사용하여 가상 컴퓨터를 배포하는 예제는 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-289">For an example of using a password or SSH key to deploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="3042e-290">출력</span><span class="sxs-lookup"><span data-stu-id="3042e-290">Outputs</span></span>
<span data-ttu-id="3042e-291">Outputs 섹션에서, 배포에서 반환되는 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-291">In the Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="3042e-292">예를 들어, 배포된 리소스에 액세스하기 위한 URI를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-292">For example, you could return the URI to access a deployed resource.</span></span>

<span data-ttu-id="3042e-293">다음 예제에서는 출력 정의의 구조를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-293">The following example shows the structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="3042e-294">요소 이름</span><span class="sxs-lookup"><span data-stu-id="3042e-294">Element name</span></span> | <span data-ttu-id="3042e-295">필수</span><span class="sxs-lookup"><span data-stu-id="3042e-295">Required</span></span> | <span data-ttu-id="3042e-296">설명</span><span class="sxs-lookup"><span data-stu-id="3042e-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3042e-297">outputName</span><span class="sxs-lookup"><span data-stu-id="3042e-297">outputName</span></span> |<span data-ttu-id="3042e-298">예</span><span class="sxs-lookup"><span data-stu-id="3042e-298">Yes</span></span> |<span data-ttu-id="3042e-299">출력 값의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-299">Name of the output value.</span></span> <span data-ttu-id="3042e-300">유효한 JavaScript 식별자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="3042e-301">type</span><span class="sxs-lookup"><span data-stu-id="3042e-301">type</span></span> |<span data-ttu-id="3042e-302">예</span><span class="sxs-lookup"><span data-stu-id="3042e-302">Yes</span></span> |<span data-ttu-id="3042e-303">출력 값의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-303">Type of the output value.</span></span> <span data-ttu-id="3042e-304">출력 값은 템플릿 입력 매개 변수와 동일한 유형을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-304">Output values support the same types as template input parameters.</span></span> |
| <span data-ttu-id="3042e-305">value</span><span class="sxs-lookup"><span data-stu-id="3042e-305">value</span></span> |<span data-ttu-id="3042e-306">예</span><span class="sxs-lookup"><span data-stu-id="3042e-306">Yes</span></span> |<span data-ttu-id="3042e-307">출력 값으로 계산되어 반환되는 템플릿 언어 식입니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="3042e-308">다음 예제에서는 Outputs 섹션에서 반환되는 값을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-308">The following example shows a value that is returned in the Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="3042e-309">출력 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿에서 상태 공유](best-practices-resource-manager-state.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="3042e-310">템플릿 제한</span><span class="sxs-lookup"><span data-stu-id="3042e-310">Template limits</span></span>

<span data-ttu-id="3042e-311">템플릿의 크기는 1MB로, 각 매개 변수 파일의 크기는 64KB로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-311">Limit the size of your template to 1 MB, and each parameter file to 64 KB.</span></span> <span data-ttu-id="3042e-312">1MB의 제한은 반복적인 리소스 정의로 확장된 후 템플릿의 마지막 상태와 변수 및 매개변수 값에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-312">The 1-MB limit applies to the final state of the template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="3042e-313">또한 다음으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-313">You are also limited to:</span></span>

* <span data-ttu-id="3042e-314">매개 변수 256개</span><span class="sxs-lookup"><span data-stu-id="3042e-314">256 parameters</span></span>
* <span data-ttu-id="3042e-315">변수 256개</span><span class="sxs-lookup"><span data-stu-id="3042e-315">256 variables</span></span>
* <span data-ttu-id="3042e-316">리소스 800개(인쇄 매수 포함)</span><span class="sxs-lookup"><span data-stu-id="3042e-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="3042e-317">출력 값 64개</span><span class="sxs-lookup"><span data-stu-id="3042e-317">64 output values</span></span>
* <span data-ttu-id="3042e-318">템플릿 식의 문자 24,576자</span><span class="sxs-lookup"><span data-stu-id="3042e-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="3042e-319">중첩된 템플릿을 사용하여 일부 템플릿 제한을 초과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="3042e-320">자세한 내용은 [Azure 리소스를 배포할 때 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="3042e-321">매개 변수, 변수 또는 출력의 수를 줄이려면 개체에 여러 값을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-321">To reduce the number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="3042e-322">자세한 내용은 [매개 변수로 개체 사용](resource-manager-objects-as-parameters.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3042e-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3042e-323">Next steps</span></span>
* <span data-ttu-id="3042e-324">다양한 유형의 솔루션에 대한 전체 템플릿을 보려면 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-324">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="3042e-325">템플릿 내에서 사용할 수 있는 함수에 대한 자세한 내용은 [Azure Resource Manager 템플릿 함수](resource-group-template-functions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-325">For details about the functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="3042e-326">배포 중 여러 템플릿을 결합하려면 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-326">To combine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="3042e-327">다른 리소스 그룹 내에 있는 리소스를 사용해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-327">You may need to use resources that exist within a different resource group.</span></span> <span data-ttu-id="3042e-328">이 시나리오에서는 일반적으로 여러 리소스 그룹에서 공유하는 저장소 계정 또는 가상 네트워크에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="3042e-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="3042e-329">자세한 내용은 [resourceId 함수](resource-group-template-functions-resource.md#resourceid)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3042e-329">For more information, see the [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
