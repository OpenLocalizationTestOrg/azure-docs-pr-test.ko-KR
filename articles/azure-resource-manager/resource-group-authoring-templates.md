---
title: "aaaAzure 리소스 관리자 템플릿 구조와 구문을 | Microsoft Docs"
description: "선언적 JSON 구문을 사용 하 여 Azure 리소스 관리자 템플릿의 hello 구조와 속성을 설명 합니다."
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
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a><span data-ttu-id="648d3-103">Hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해합니다</span><span class="sxs-lookup"><span data-stu-id="648d3-103">Understand hello structure and syntax of Azure Resource Manager templates</span></span>
<span data-ttu-id="648d3-104">이 항목에서는 Azure Resource Manager 템플릿의 hello 구조를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-104">This topic describes hello structure of an Azure Resource Manager template.</span></span> <span data-ttu-id="648d3-105">해당 섹션에서 사용할 수 있는 템플릿과 hello 속성의 여러 다른 섹션 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-105">It presents hello different sections of a template and hello properties that are available in those sections.</span></span> <span data-ttu-id="648d3-106">JSON 및 배포에 대 한 tooconstruct 값을 사용할 수 있는 식의 hello 템플릿은 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="648d3-107">템플릿 만들기에 관한 단계별 연습은 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-107">For a step-by-step tutorial on creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

## <a name="template-format"></a><span data-ttu-id="648d3-108">템플릿 형식</span><span class="sxs-lookup"><span data-stu-id="648d3-108">Template format</span></span>
<span data-ttu-id="648d3-109">가장 간단한 구조로 서식 파일 요소 다음 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-109">In its simplest structure, a template contains hello following elements:</span></span>

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

| <span data-ttu-id="648d3-110">요소 이름</span><span class="sxs-lookup"><span data-stu-id="648d3-110">Element name</span></span> | <span data-ttu-id="648d3-111">필수</span><span class="sxs-lookup"><span data-stu-id="648d3-111">Required</span></span> | <span data-ttu-id="648d3-112">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-112">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="648d3-113">$schema</span><span class="sxs-lookup"><span data-stu-id="648d3-113">$schema</span></span> |<span data-ttu-id="648d3-114">예</span><span class="sxs-lookup"><span data-stu-id="648d3-114">Yes</span></span> |<span data-ttu-id="648d3-115">Hello 버전의 hello 템플릿 언어를 설명 하는 hello JSON 스키마 파일의 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-115">Location of hello JSON schema file that describes hello version of hello template language.</span></span> <span data-ttu-id="648d3-116">Hello에에서 표시 된 URL 앞 예제는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-116">Use hello URL shown in hello preceding example.</span></span> |
| <span data-ttu-id="648d3-117">contentVersion</span><span class="sxs-lookup"><span data-stu-id="648d3-117">contentVersion</span></span> |<span data-ttu-id="648d3-118">예</span><span class="sxs-lookup"><span data-stu-id="648d3-118">Yes</span></span> |<span data-ttu-id="648d3-119">Hello 템플릿 (예: 1.0.0.0)의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-119">Version of hello template (such as 1.0.0.0).</span></span> <span data-ttu-id="648d3-120">이 요소에 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-120">You can provide any value for this element.</span></span> <span data-ttu-id="648d3-121">Hello 서식 파일을 사용 하 여 리소스를 배포 하는 경우이 값에 사용 되는 toomake hello 오른쪽 템플릿을 사용 되 고 있는지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-121">When deploying resources using hello template, this value can be used toomake sure that hello right template is being used.</span></span> |
| <span data-ttu-id="648d3-122">매개 변수</span><span class="sxs-lookup"><span data-stu-id="648d3-122">parameters</span></span> |<span data-ttu-id="648d3-123">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-123">No</span></span> |<span data-ttu-id="648d3-124">배포 되 면 제공 되는 값 toocustomize 리소스 배포를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-124">Values that are provided when deployment is executed toocustomize resource deployment.</span></span> |
| <span data-ttu-id="648d3-125">variables</span><span class="sxs-lookup"><span data-stu-id="648d3-125">variables</span></span> |<span data-ttu-id="648d3-126">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-126">No</span></span> |<span data-ttu-id="648d3-127">Hello 템플릿 toosimplify 템플릿 언어 식에 JSON 조각을으로 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-127">Values that are used as JSON fragments in hello template toosimplify template language expressions.</span></span> |
| <span data-ttu-id="648d3-128">리소스</span><span class="sxs-lookup"><span data-stu-id="648d3-128">resources</span></span> |<span data-ttu-id="648d3-129">예</span><span class="sxs-lookup"><span data-stu-id="648d3-129">Yes</span></span> |<span data-ttu-id="648d3-130">리소스 그룹에 배포 또는 업데이트되는 리소스 종류입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-130">Resource types that are deployed or updated in a resource group.</span></span> |
| <span data-ttu-id="648d3-131">outputs</span><span class="sxs-lookup"><span data-stu-id="648d3-131">outputs</span></span> |<span data-ttu-id="648d3-132">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-132">No</span></span> |<span data-ttu-id="648d3-133">배포 후 반환되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-133">Values that are returned after deployment.</span></span> |

<span data-ttu-id="648d3-134">각 요소에는 사용자가 설정할 수 있는 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-134">Each element contains properties you can set.</span></span> <span data-ttu-id="648d3-135">다음 예제는 hello hello 템플릿에 대 한 전체 구문이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-135">hello following example contains hello full syntax for a template:</span></span>

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
                "description": "<description-of-hello parameter>" 
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

<span data-ttu-id="648d3-136">이 항목의 뒷부분에 자세히 hello 템플릿의 hello 섹션을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-136">We examine hello sections of hello template in greater detail later in this topic.</span></span>

## <a name="expressions-and-functions"></a><span data-ttu-id="648d3-137">식 및 함수</span><span class="sxs-lookup"><span data-stu-id="648d3-137">Expressions and functions</span></span>
<span data-ttu-id="648d3-138">hello 기본 hello 서식 파일의 구문은 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-138">hello basic syntax of hello template is JSON.</span></span> <span data-ttu-id="648d3-139">그러나 식과 함수 hello 템플릿 내에서 사용할 수 있는 hello JSON 값을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-139">However, expressions and functions extend hello JSON values available within hello template.</span></span>  <span data-ttu-id="648d3-140">식이 작성 JSON 문자열 리터럴 내에서 해당 첫 번째 및 마지막 문자는 hello 대괄호: `[` 및 `]`각각.</span><span class="sxs-lookup"><span data-stu-id="648d3-140">Expressions are written within JSON string literals whose first and last characters are hello brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="648d3-141">hello 식의 hello 값 hello 템플릿이 배포 될 때 평가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-141">hello value of hello expression is evaluated when hello template is deployed.</span></span> <span data-ttu-id="648d3-142">문자열 리터럴로 작성 하는 동안 다른 JSON 형식의 배열 또는 정수 hello 실제 식에 따라 같은 hello 식의 계산 결과 hello 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-142">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array or integer, depending on hello actual expression.</span></span>  <span data-ttu-id="648d3-143">리터럴 문자열에 대괄호로 시작 하는 toohave `[`, 식으로 해석 하 게을 제외한 추가 대괄호 toostart hello 문자열을 추가 `[[`합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-143">toohave a literal string start with a bracket `[`, but not have it interpreted as an expression, add an extra bracket toostart hello string with `[[`.</span></span>

<span data-ttu-id="648d3-144">일반적으로 식을 함수 tooperform 작업 hello 배포를 구성 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-144">Typically, you use expressions with functions tooperform operations for configuring hello deployment.</span></span> <span data-ttu-id="648d3-145">JavaScript에서와 마찬가지로 함수 호출은 `functionName(arg1,arg2,arg3)`과 같이 형식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-145">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="648d3-146">Hello 점 및 [index] 연산자를 사용 하 여 속성을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-146">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="648d3-147">다음 예제는 hello를 생성할 때 동작 하는 여러 toouse 값 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-147">hello following example shows how toouse several functions when constructing values:</span></span>

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

<span data-ttu-id="648d3-148">Hello 전체 목록은 템플릿 함수를 참조 하십시오. [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-148">For hello full list of template functions, see [Azure Resource Manager template functions](resource-group-template-functions.md).</span></span> 

## <a name="parameters"></a><span data-ttu-id="648d3-149">매개 변수</span><span class="sxs-lookup"><span data-stu-id="648d3-149">Parameters</span></span>
<span data-ttu-id="648d3-150">Hello hello 서식 파일의 매개 변수 섹션, 배포 하는 경우를 입력할 수 있는 값 hello 리소스 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-150">In hello parameters section of hello template, you specify which values you can input when deploying hello resources.</span></span> <span data-ttu-id="648d3-151">이러한 매개 변수 값 (예: 개발, 테스트 및 프로덕션) 환경에 맞는 값을 제공 하 여 toocustomize hello 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-151">These parameter values enable you toocustomize hello deployment by providing values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="648d3-152">템플릿에 tooprovide 매개 변수가 필요는 없지만 매개 변수 없이 서식 파일에는 항상 배포 hello와 같은 리소스 hello 동일한 이름, 위치 및 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-152">You do not have tooprovide parameters in your template, but without parameters your template would always deploy hello same resources with hello same names, locations, and properties.</span></span>

<span data-ttu-id="648d3-153">구조를 다음 hello로 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-153">You define parameters with hello following structure:</span></span>

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
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| <span data-ttu-id="648d3-154">요소 이름</span><span class="sxs-lookup"><span data-stu-id="648d3-154">Element name</span></span> | <span data-ttu-id="648d3-155">필수</span><span class="sxs-lookup"><span data-stu-id="648d3-155">Required</span></span> | <span data-ttu-id="648d3-156">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-156">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="648d3-157">parameterName</span><span class="sxs-lookup"><span data-stu-id="648d3-157">parameterName</span></span> |<span data-ttu-id="648d3-158">예</span><span class="sxs-lookup"><span data-stu-id="648d3-158">Yes</span></span> |<span data-ttu-id="648d3-159">Hello 매개 변수의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-159">Name of hello parameter.</span></span> <span data-ttu-id="648d3-160">유효한 JavaScript 식별자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-160">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="648d3-161">type</span><span class="sxs-lookup"><span data-stu-id="648d3-161">type</span></span> |<span data-ttu-id="648d3-162">예</span><span class="sxs-lookup"><span data-stu-id="648d3-162">Yes</span></span> |<span data-ttu-id="648d3-163">Hello 매개 변수 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-163">Type of hello parameter value.</span></span> <span data-ttu-id="648d3-164">이 표 다음 허용된 유형 목록을 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="648d3-164">See hello list of allowed types after this table.</span></span> |
| <span data-ttu-id="648d3-165">defaultValue</span><span class="sxs-lookup"><span data-stu-id="648d3-165">defaultValue</span></span> |<span data-ttu-id="648d3-166">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-166">No</span></span> |<span data-ttu-id="648d3-167">Hello 매개 변수를 값이 없는 hello 매개 변수에 대해 제공 하는 경우에 대 한 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-167">Default value for hello parameter, if no value is provided for hello parameter.</span></span> |
| <span data-ttu-id="648d3-168">allowedValues</span><span class="sxs-lookup"><span data-stu-id="648d3-168">allowedValues</span></span> |<span data-ttu-id="648d3-169">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-169">No</span></span> |<span data-ttu-id="648d3-170">Hello 매개 변수 toomake hello 오른쪽 값을 제공 하 고 있는지에 대 한 허용 되는 값의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-170">Array of allowed values for hello parameter toomake sure that hello right value is provided.</span></span> |
| <span data-ttu-id="648d3-171">minValue</span><span class="sxs-lookup"><span data-stu-id="648d3-171">minValue</span></span> |<span data-ttu-id="648d3-172">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-172">No</span></span> |<span data-ttu-id="648d3-173">int 형식 매개 변수에 대 한 최소값을 hello로이 값은 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-173">hello minimum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="648d3-174">maxValue</span><span class="sxs-lookup"><span data-stu-id="648d3-174">maxValue</span></span> |<span data-ttu-id="648d3-175">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-175">No</span></span> |<span data-ttu-id="648d3-176">int 형식 매개 변수에 대해 hello 최대 값이이 값은 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-176">hello maximum value for int type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="648d3-177">minLength</span><span class="sxs-lookup"><span data-stu-id="648d3-177">minLength</span></span> |<span data-ttu-id="648d3-178">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-178">No</span></span> |<span data-ttu-id="648d3-179">hello 문자열과 secureString, 형식 매개 변수 배열에 대 한 최소 길이,이 값은 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-179">hello minimum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="648d3-180">maxLength</span><span class="sxs-lookup"><span data-stu-id="648d3-180">maxLength</span></span> |<span data-ttu-id="648d3-181">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-181">No</span></span> |<span data-ttu-id="648d3-182">hello 문자열과 secureString, 형식 매개 변수 배열에 대 한 최대 길이이 값은 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-182">hello maximum length for string, secureString, and array type parameters, this value is inclusive.</span></span> |
| <span data-ttu-id="648d3-183">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-183">description</span></span> |<span data-ttu-id="648d3-184">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-184">No</span></span> |<span data-ttu-id="648d3-185">Hello 포털을 통해 toousers를 표시 하는 설명은 hello 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-185">Description of hello parameter that is displayed toousers through hello portal.</span></span> |

<span data-ttu-id="648d3-186">hello 허용된 유형 및 값은:</span><span class="sxs-lookup"><span data-stu-id="648d3-186">hello allowed types and values are:</span></span>

* <span data-ttu-id="648d3-187">**string**</span><span class="sxs-lookup"><span data-stu-id="648d3-187">**string**</span></span>
* <span data-ttu-id="648d3-188">**secureString**</span><span class="sxs-lookup"><span data-stu-id="648d3-188">**secureString**</span></span>
* <span data-ttu-id="648d3-189">**int**</span><span class="sxs-lookup"><span data-stu-id="648d3-189">**int**</span></span>
* <span data-ttu-id="648d3-190">**bool**</span><span class="sxs-lookup"><span data-stu-id="648d3-190">**bool**</span></span>
* <span data-ttu-id="648d3-191">**object**</span><span class="sxs-lookup"><span data-stu-id="648d3-191">**object**</span></span> 
* <span data-ttu-id="648d3-192">**secureObject**</span><span class="sxs-lookup"><span data-stu-id="648d3-192">**secureObject**</span></span>
* <span data-ttu-id="648d3-193">**array**</span><span class="sxs-lookup"><span data-stu-id="648d3-193">**array**</span></span>

<span data-ttu-id="648d3-194">선택적으로 매개 변수 toospecify defaultValue (빈 문자열일 수 있음)를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-194">toospecify a parameter as optional, provide a defaultValue (can be an empty string).</span></span> 

<span data-ttu-id="648d3-195">Hello 명령 toodeploy hello 서식 파일의 매개 변수와 일치 하는 서식 파일에서 매개 변수 이름을 지정 하면 사용자가 제공한 hello 값에 대 한 잠재적 모호성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-195">If you specify a parameter name in your template that matches a parameter in hello command toodeploy hello template, there is potential ambiguity about hello values you provide.</span></span> <span data-ttu-id="648d3-196">리소스 관리자는 hello 접미사를 추가 하 여 이러한 혼동을 해결 **FromTemplate** toohello 템플릿 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-196">Resource Manager resolves this confusion by adding hello postfix **FromTemplate** toohello template parameter.</span></span> <span data-ttu-id="648d3-197">예를 들어, 명명 된 매개 변수를 포함 하는 경우 **ResourceGroupName** hello와 충돌 템플릿에 **ResourceGroupName** hello에 대 한 매개 변수 [ 새 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="648d3-197">For example, if you include a parameter named **ResourceGroupName** in your template, it conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="648d3-198">배포 하는 동안는 tooprovide 입력 정보 요청된에 대 한 값 **ResourceGroupNameFromTemplate**합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-198">During deployment, you are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="648d3-199">일반적으로 이러한 혼동 하지 배포 작업에 사용 되는 매개 변수로 이름과 같은 이름을 hello로 매개 변수 이름을 지정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="648d3-199">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

> [!NOTE]
> <span data-ttu-id="648d3-200">모든 암호, 키 및 기타 암호 hello를 사용 해야 **secureString** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-200">All passwords, keys, and other secrets should use hello **secureString** type.</span></span> <span data-ttu-id="648d3-201">Hello를 사용 하 여 JSON 개체에 중요 한 데이터를 전달 하는 경우 **secureObject** 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-201">If you pass sensitive data in a JSON object, use hello **secureObject** type.</span></span> <span data-ttu-id="648d3-202">리소스 배포 후에는 secureString 또는 secureObject 형식의 템플릿 매개 변수를 읽을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-202">Template parameters with secureString or secureObject types cannot be read after resource deployment.</span></span> 
> 
> <span data-ttu-id="648d3-203">예를 들어 hello hello 배포 기록의 다음 항목 hello 값을 표시 문자열 및 개체에 대 한 있지만 secureString 및 secureObject 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-203">For example, hello following entry in hello deployment history shows hello value for a string and object but not for secureString and secureObject.</span></span>
>
> ![배포 값 표시](./media/resource-group-authoring-templates/show-parameters.png)  
>

<span data-ttu-id="648d3-205">hello 방법을 예제와 다음 toodefine 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="648d3-205">hello following example shows how toodefine parameters:</span></span>

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

<span data-ttu-id="648d3-206">방법을 배포 하는 동안 tooinput hello 매개 변수 값, 참조 [Azure 리소스 관리자 템플릿 사용 하 여 응용 프로그램 배포](resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-206">For how tooinput hello parameter values during deployment, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span> 

## <a name="variables"></a><span data-ttu-id="648d3-207">variables</span><span class="sxs-lookup"><span data-stu-id="648d3-207">Variables</span></span>
<span data-ttu-id="648d3-208">Hello 변수 섹션에서 서식 파일에 전체에서 사용할 수 있는 값을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-208">In hello variables section, you construct values that can be used throughout your template.</span></span> <span data-ttu-id="648d3-209">Toodefine 변수 필요는 없지만 종종 서식 파일에는 복잡 한 식을 줄여서 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-209">You do not need toodefine variables, but they often simplify your template by reducing complex expressions.</span></span>

<span data-ttu-id="648d3-210">구조를 다음 hello로 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-210">You define variables with hello following structure:</span></span>

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

<span data-ttu-id="648d3-211">hello 방법을 예제와 다음 두 개의 매개 변수 값에서 생성 된 변수 toodefine:</span><span class="sxs-lookup"><span data-stu-id="648d3-211">hello following example shows how toodefine a variable that is constructed from two parameter values:</span></span>

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

<span data-ttu-id="648d3-212">hello 다음 예제에서는 다른 변수에서 생성 되는 변수 및 변수는 복합 JSON 유형를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-212">hello next example shows a variable that is a complex JSON type, and variables that are constructed from other variables:</span></span>

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

## <a name="resources"></a><span data-ttu-id="648d3-213">리소스</span><span class="sxs-lookup"><span data-stu-id="648d3-213">Resources</span></span>
<span data-ttu-id="648d3-214">Hello 리소스 섹션에 배포 또는 업데이트할지 여부를 지정 하는 hello 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-214">In hello resources section, you define hello resources that are deployed or updated.</span></span> <span data-ttu-id="648d3-215">이 섹션 hello 형식 이해 해야 하기 때문에 복잡 해질 수 있습니다 tooprovide hello 오른쪽 값을 배포 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-215">This section can get complicated because you must understand hello types you are deploying tooprovide hello right values.</span></span> <span data-ttu-id="648d3-216">Hello 리소스별 값 (apiVersion, 유형 및 속성) tooset 해야 하는, 참조 [Azure 리소스 관리자 템플릿을에 리소스를 정의](/azure/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-216">For hello resource-specific values (apiVersion, type, and properties) that you need tooset, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span> 

<span data-ttu-id="648d3-217">구조를 다음 hello로 리소스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-217">You define resources with hello following structure:</span></span>

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

| <span data-ttu-id="648d3-218">요소 이름</span><span class="sxs-lookup"><span data-stu-id="648d3-218">Element name</span></span> | <span data-ttu-id="648d3-219">필수</span><span class="sxs-lookup"><span data-stu-id="648d3-219">Required</span></span> | <span data-ttu-id="648d3-220">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-220">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="648d3-221">condition</span><span class="sxs-lookup"><span data-stu-id="648d3-221">condition</span></span> | <span data-ttu-id="648d3-222">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-222">No</span></span> | <span data-ttu-id="648d3-223">Hello 리소스 배포 되는지 여부를 나타내는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-223">Boolean value that indicates whether hello resource is deployed.</span></span> |
| <span data-ttu-id="648d3-224">apiVersion</span><span class="sxs-lookup"><span data-stu-id="648d3-224">apiVersion</span></span> |<span data-ttu-id="648d3-225">예</span><span class="sxs-lookup"><span data-stu-id="648d3-225">Yes</span></span> |<span data-ttu-id="648d3-226">Hello 리소스를 만들기 위한 REST API toouse hello의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-226">Version of hello REST API toouse for creating hello resource.</span></span> |
| <span data-ttu-id="648d3-227">type</span><span class="sxs-lookup"><span data-stu-id="648d3-227">type</span></span> |<span data-ttu-id="648d3-228">예</span><span class="sxs-lookup"><span data-stu-id="648d3-228">Yes</span></span> |<span data-ttu-id="648d3-229">Hello 리소스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-229">Type of hello resource.</span></span> <span data-ttu-id="648d3-230">이 값은 hello 리소스 공급자 및 hello 리소스 종류의 hello 네임 스페이스의 조합 (예: **/storageaccounts**).</span><span class="sxs-lookup"><span data-stu-id="648d3-230">This value is a combination of hello namespace of hello resource provider and hello resource type (such as **Microsoft.Storage/storageAccounts**).</span></span> |
| <span data-ttu-id="648d3-231">name</span><span class="sxs-lookup"><span data-stu-id="648d3-231">name</span></span> |<span data-ttu-id="648d3-232">예</span><span class="sxs-lookup"><span data-stu-id="648d3-232">Yes</span></span> |<span data-ttu-id="648d3-233">Hello 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-233">Name of hello resource.</span></span> <span data-ttu-id="648d3-234">hello 이름은 RFC3986에 정의 된 URI 구성 요소 제한을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-234">hello name must follow URI component restrictions defined in RFC3986.</span></span> <span data-ttu-id="648d3-235">Hello 리소스 이름 toooutside 파티를 노출 하는 Azure 서비스 hello 이름 toomake 시도 toospoof 아닌지 유효성 검사는 또한 다른 id입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-235">In addition, Azure services that expose hello resource name toooutside parties validate hello name toomake sure it is not an attempt toospoof another identity.</span></span> |
| <span data-ttu-id="648d3-236">location</span><span class="sxs-lookup"><span data-stu-id="648d3-236">location</span></span> |<span data-ttu-id="648d3-237">다름</span><span class="sxs-lookup"><span data-stu-id="648d3-237">Varies</span></span> |<span data-ttu-id="648d3-238">Hello의 지원 되는 지리적 위치는 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-238">Supported geo-locations of hello provided resource.</span></span> <span data-ttu-id="648d3-239">Hello 사용 가능한 위치 중 하나를 선택할 수 되지만 일반적으로 의미 toopick 닫기 tooyour 사용자가 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-239">You can select any of hello available locations, but typically it makes sense toopick one that is close tooyour users.</span></span> <span data-ttu-id="648d3-240">일반적으로 만드는 것도 좋습니다 서로 상호 작용 hello에 동일한 tooplace 리소스 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-240">Usually, it also makes sense tooplace resources that interact with each other in hello same region.</span></span> <span data-ttu-id="648d3-241">대부분의 리소스 종류에는 위치가 필요하지만 일부 종류(예: 역할 할당)에는 위치가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-241">Most resource types require a location, but some types (such as a role assignment) do not require a location.</span></span> <span data-ttu-id="648d3-242">[Azure Resource Manager 템플릿에서 리소스 위치 설정](resource-manager-template-location.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-242">See [Set resource location in Azure Resource Manager templates](resource-manager-template-location.md).</span></span> |
| <span data-ttu-id="648d3-243">tags</span><span class="sxs-lookup"><span data-stu-id="648d3-243">tags</span></span> |<span data-ttu-id="648d3-244">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-244">No</span></span> |<span data-ttu-id="648d3-245">Hello 리소스와 연결 된 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-245">Tags that are associated with hello resource.</span></span> <span data-ttu-id="648d3-246">[Azure Resource Manager 템플릿에서 리소스에 태그 지정](resource-manager-template-tags.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-246">See [Tag resources in Azure Resource Manager templates](resource-manager-template-tags.md).</span></span> |
| <span data-ttu-id="648d3-247">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-247">comments</span></span> |<span data-ttu-id="648d3-248">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-248">No</span></span> |<span data-ttu-id="648d3-249">에 대 한 서식 파일에 hello 리소스 설명서 노트</span><span class="sxs-lookup"><span data-stu-id="648d3-249">Your notes for documenting hello resources in your template</span></span> |
| <span data-ttu-id="648d3-250">복사</span><span class="sxs-lookup"><span data-stu-id="648d3-250">copy</span></span> |<span data-ttu-id="648d3-251">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-251">No</span></span> |<span data-ttu-id="648d3-252">둘 이상의 인스턴스가 필요한 경우 hello toocreate 리소스의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-252">If more than one instance is needed, hello number of resources toocreate.</span></span> <span data-ttu-id="648d3-253">hello 기본 모드는 병렬입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-253">hello default mode is parallel.</span></span> <span data-ttu-id="648d3-254">일부 또는 hello에 대 한 리소스 toodeploy hello 하지 않는 경우 직렬 모드를 지정 합니다. 같은 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-254">Specify serial mode when you do not want all or hello resources toodeploy at hello same time.</span></span> <span data-ttu-id="648d3-255">자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-255">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="648d3-256">dependsOn</span><span class="sxs-lookup"><span data-stu-id="648d3-256">dependsOn</span></span> |<span data-ttu-id="648d3-257">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-257">No</span></span> |<span data-ttu-id="648d3-258">이 리소스를 배포하기 전에 배포해야 하는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-258">Resources that must be deployed before this resource is deployed.</span></span> <span data-ttu-id="648d3-259">리소스 관리자 리소스 간의 종속성을 hello 평가 하 고 hello 올바른 순서에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-259">Resource Manager evaluates hello dependencies between resources and deploys them in hello correct order.</span></span> <span data-ttu-id="648d3-260">리소스는 서로 종속되지 않을 경우 병렬로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-260">When resources are not dependent on each other, they are deployed in parallel.</span></span> <span data-ttu-id="648d3-261">hello 값 목록이 될 수 쉼표로 구분 된 리소스의 이름 또는 리소스의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-261">hello value can be a comma-separated list of a resource names or resource unique identifiers.</span></span> <span data-ttu-id="648d3-262">이 템플릿에 배포된 리소스만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-262">Only list resources that are deployed in this template.</span></span> <span data-ttu-id="648d3-263">이 템플릿에 정의되지 않은 리소스는 이미 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-263">Resources that are not defined in this template must already exist.</span></span> <span data-ttu-id="648d3-264">불필요한 종속성은 배포 속도를 느리게 만들고 순환 종속성을 만들기 때문에 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-264">Avoid adding unnecessary dependencies as they can slow your deployment and create circular dependencies.</span></span> <span data-ttu-id="648d3-265">종속성 설정에 대한 지침은 [Azure Resource Manager 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-265">For guidance on setting dependencies, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span> |
| <span data-ttu-id="648d3-266">properties</span><span class="sxs-lookup"><span data-stu-id="648d3-266">properties</span></span> |<span data-ttu-id="648d3-267">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-267">No</span></span> |<span data-ttu-id="648d3-268">리소스별 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-268">Resource-specific configuration settings.</span></span> <span data-ttu-id="648d3-269">hello 속성에 대 한 hello 값은 hello REST API 작업 (PUT 메서드) toocreate hello 리소스에 대 한 hello 요청 본문에 제공 하는 hello 값으로 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-269">hello values for hello properties are hello same as hello values you provide in hello request body for hello REST API operation (PUT method) toocreate hello resource.</span></span> <span data-ttu-id="648d3-270">또한 속성의 여러 인스턴스 복사본 배열 toocreate를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-270">You can also specify a copy array toocreate multiple instances of a property.</span></span> <span data-ttu-id="648d3-271">자세한 내용은 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-271">For more information, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span> |
| <span data-ttu-id="648d3-272">리소스</span><span class="sxs-lookup"><span data-stu-id="648d3-272">resources</span></span> |<span data-ttu-id="648d3-273">아니요</span><span class="sxs-lookup"><span data-stu-id="648d3-273">No</span></span> |<span data-ttu-id="648d3-274">정의 중인 hello 리소스에 종속 된 자식 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-274">Child resources that depend on hello resource being defined.</span></span> <span data-ttu-id="648d3-275">만 hello 부모 리소스의 hello 스키마에서 허용 하는 리소스 종류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-275">Only provide resource types that are permitted by hello schema of hello parent resource.</span></span> <span data-ttu-id="648d3-276">hello hello 자식 리소스의 정규화 된 형식 hello 부모 리소스 종류와 같은 포함 **Microsoft.Web/sites/extensions**합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-276">hello fully qualified type of hello child resource includes hello parent resource type, such as **Microsoft.Web/sites/extensions**.</span></span> <span data-ttu-id="648d3-277">Hello 부모 리소스에 대 한 종속성이 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-277">Dependency on hello parent resource is not implied.</span></span> <span data-ttu-id="648d3-278">해당 종속성을 명시적으로 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-278">You must explicitly define that dependency.</span></span> |

<span data-ttu-id="648d3-279">hello 리소스 섹션에는 hello 리소스 toodeploy 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-279">hello resources section contains an array of hello resources toodeploy.</span></span> <span data-ttu-id="648d3-280">각 리소스 내에서 자식 리소스의 배열도 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-280">Within each resource, you can also define an array of child resources.</span></span> <span data-ttu-id="648d3-281">따라서 리소스 섹션에는 다음과 같은 구조가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-281">Therefore, your resources section could have a structure like:</span></span>

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

<span data-ttu-id="648d3-282">자식 리소스를 정의하는 방법에 대한 자세한 내용은 [Resource Manager 템플릿에서 자식 리소스에 대한 이름 및 형식 설정](resource-manager-template-child-resource.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-282">For more information about defining child resources, see [Set name and type for child resource in Resource Manager template](resource-manager-template-child-resource.md).</span></span>

<span data-ttu-id="648d3-283">hello **조건** 요소 hello 리소스 배포 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-283">hello **condition** element specifies whether hello resource is deployed.</span></span> <span data-ttu-id="648d3-284">이 요소에 대 한 hello 값 tootrue 또는 false를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-284">hello value for this element resolves tootrue or false.</span></span> <span data-ttu-id="648d3-285">예를 들어 toospecify 새 저장소 계정에 배포 하는지 여부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-285">For example, toospecify whether a new storage account is deployed, use:</span></span>

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

<span data-ttu-id="648d3-286">기존 또는 새 리소스 사용 예제는 [신규 또는 기존 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-286">For an example of using a new or existing resource, see [New or existing condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).</span></span>

<span data-ttu-id="648d3-287">toospecify 정의할 수 있는지 여부를 암호 또는 SSH 키로는 가상 컴퓨터가 배포 된 두 가지 버전의 hello 가상 컴퓨터 템플릿을를 사용 하 여 **조건** toodifferentiate 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-287">toospecify whether a virtual machine is deployed with a password or SSH key, define two versions of hello virtual machine in your template and use **condition** toodifferentiate usage.</span></span> <span data-ttu-id="648d3-288">어떤 시나리오 toodeploy를 지정 하는 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-288">Pass a parameter that specifies which scenario toodeploy.</span></span>

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

<span data-ttu-id="648d3-289">암호 또는 SSH 키 toodeploy 가상 컴퓨터를 사용 하 여 예제를 보려면 [사용자 이름 또는 SSH 조건 템플릿](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-289">For an example of using a password or SSH key toodeploy virtual machine, see [Username or SSH condition template](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).</span></span>

## <a name="outputs"></a><span data-ttu-id="648d3-290">outputs</span><span class="sxs-lookup"><span data-stu-id="648d3-290">Outputs</span></span>
<span data-ttu-id="648d3-291">Hello 출력 섹션의 배포에서 반환 된 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-291">In hello Outputs section, you specify values that are returned from deployment.</span></span> <span data-ttu-id="648d3-292">예를 들어 배포 된 리소스 URI tooaccess hello를 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-292">For example, you could return hello URI tooaccess a deployed resource.</span></span>

<span data-ttu-id="648d3-293">hello 다음 예제에서는 구조를 보여 줍니다 hello 출력 정의:</span><span class="sxs-lookup"><span data-stu-id="648d3-293">hello following example shows hello structure of an output definition:</span></span>

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| <span data-ttu-id="648d3-294">요소 이름</span><span class="sxs-lookup"><span data-stu-id="648d3-294">Element name</span></span> | <span data-ttu-id="648d3-295">필수</span><span class="sxs-lookup"><span data-stu-id="648d3-295">Required</span></span> | <span data-ttu-id="648d3-296">설명</span><span class="sxs-lookup"><span data-stu-id="648d3-296">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="648d3-297">outputName</span><span class="sxs-lookup"><span data-stu-id="648d3-297">outputName</span></span> |<span data-ttu-id="648d3-298">예</span><span class="sxs-lookup"><span data-stu-id="648d3-298">Yes</span></span> |<span data-ttu-id="648d3-299">Hello 출력 값의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-299">Name of hello output value.</span></span> <span data-ttu-id="648d3-300">유효한 JavaScript 식별자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-300">Must be a valid JavaScript identifier.</span></span> |
| <span data-ttu-id="648d3-301">type</span><span class="sxs-lookup"><span data-stu-id="648d3-301">type</span></span> |<span data-ttu-id="648d3-302">예</span><span class="sxs-lookup"><span data-stu-id="648d3-302">Yes</span></span> |<span data-ttu-id="648d3-303">Hello 출력 값의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-303">Type of hello output value.</span></span> <span data-ttu-id="648d3-304">출력 값에는 동일한 형식 템플릿 입력된 매개 변수로 hello를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-304">Output values support hello same types as template input parameters.</span></span> |
| <span data-ttu-id="648d3-305">값</span><span class="sxs-lookup"><span data-stu-id="648d3-305">value</span></span> |<span data-ttu-id="648d3-306">예</span><span class="sxs-lookup"><span data-stu-id="648d3-306">Yes</span></span> |<span data-ttu-id="648d3-307">출력 값으로 계산되어 반환되는 템플릿 언어 식입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-307">Template language expression that is evaluated and returned as output value.</span></span> |

<span data-ttu-id="648d3-308">hello 다음 예제에서는 hello 출력 섹션에서 반환 되는 값</span><span class="sxs-lookup"><span data-stu-id="648d3-308">hello following example shows a value that is returned in hello Outputs section.</span></span>

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

<span data-ttu-id="648d3-309">출력 작업에 대한 자세한 내용은 [Azure Resource Manager 템플릿에서 상태 공유](best-practices-resource-manager-state.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-309">For more information about working with output, see [Sharing state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="template-limits"></a><span data-ttu-id="648d3-310">템플릿 제한</span><span class="sxs-lookup"><span data-stu-id="648d3-310">Template limits</span></span>

<span data-ttu-id="648d3-311">Hello 크기 제한의 템플릿 too1 MB 이며 각 매개 변수에 파일 too64 (KB)입니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-311">Limit hello size of your template too1 MB, and each parameter file too64 KB.</span></span> <span data-ttu-id="648d3-312">hello 1MB 제한을 반복 리소스 정 및 변수 및 매개 변수를 사용 하 여 확장 된 후 toohello hello 서식 파일의 최종 상태를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-312">hello 1-MB limit applies toohello final state of hello template after it has been expanded with iterative resource definitions, and values for variables and parameters.</span></span> 

<span data-ttu-id="648d3-313">또한 다음으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-313">You are also limited to:</span></span>

* <span data-ttu-id="648d3-314">매개 변수 256개</span><span class="sxs-lookup"><span data-stu-id="648d3-314">256 parameters</span></span>
* <span data-ttu-id="648d3-315">변수 256개</span><span class="sxs-lookup"><span data-stu-id="648d3-315">256 variables</span></span>
* <span data-ttu-id="648d3-316">리소스 800개(인쇄 매수 포함)</span><span class="sxs-lookup"><span data-stu-id="648d3-316">800 resources (including copy count)</span></span>
* <span data-ttu-id="648d3-317">출력 값 64개</span><span class="sxs-lookup"><span data-stu-id="648d3-317">64 output values</span></span>
* <span data-ttu-id="648d3-318">템플릿 식의 문자 24,576자</span><span class="sxs-lookup"><span data-stu-id="648d3-318">24,576 characters in a template expression</span></span>

<span data-ttu-id="648d3-319">중첩된 템플릿을 사용하여 일부 템플릿 제한을 초과할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-319">You can exceed some template limits by using a nested template.</span></span> <span data-ttu-id="648d3-320">자세한 내용은 [Azure 리소스를 배포할 때 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-320">For more information, see [Using linked templates when deploying Azure resources](resource-group-linked-templates.md).</span></span> <span data-ttu-id="648d3-321">tooreduce hello 수의 매개 변수, 변수 또는 출력을 개체에 여러 값을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-321">tooreduce hello number of parameters, variables, or outputs, you can combine several values into an object.</span></span> <span data-ttu-id="648d3-322">자세한 내용은 [매개 변수로 개체 사용](resource-manager-objects-as-parameters.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="648d3-322">For more information, see [Objects as parameters](resource-manager-objects-as-parameters.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="648d3-323">다음 단계</span><span class="sxs-lookup"><span data-stu-id="648d3-323">Next steps</span></span>
* <span data-ttu-id="648d3-324">다양 한 유형의 솔루션에 대 한 전체 템플릿을 tooview 참조 hello [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-324">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
* <span data-ttu-id="648d3-325">템플릿 내에서 사용 가능한 hello 함수에 대 한 세부 정보를 참조 하십시오. [Azure 리소스 관리자 템플릿 함수](resource-group-template-functions.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-325">For details about hello functions you can use from within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md).</span></span>
* <span data-ttu-id="648d3-326">toocombine 여러 템플릿을 배포 하는 동안 참조 [Azure 리소스 관리자와 연결 된 템플릿을 사용 하 여](resource-group-linked-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-326">toocombine multiple templates during deployment, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="648d3-327">다른 리소스 그룹 내에 있는 toouse 리소스를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-327">You may need toouse resources that exist within a different resource group.</span></span> <span data-ttu-id="648d3-328">이 시나리오에서는 일반적으로 여러 리소스 그룹에서 공유하는 저장소 계정 또는 가상 네트워크에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-328">This scenario is common when working with storage accounts or virtual networks that are shared across multiple resource groups.</span></span> <span data-ttu-id="648d3-329">자세한 내용은 참조 hello [resourceId 함수](resource-group-template-functions-resource.md#resourceid)합니다.</span><span class="sxs-lookup"><span data-stu-id="648d3-329">For more information, see hello [resourceId function](resource-group-template-functions-resource.md#resourceid).</span></span>
