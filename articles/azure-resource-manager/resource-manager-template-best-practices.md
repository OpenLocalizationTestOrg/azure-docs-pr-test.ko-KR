---
title: "리소스 관리자 템플릿을 만들기 위한 aaaBest 사례 | Microsoft Docs"
description: "Azure Resource Manager 템플릿 간소화를 위한 지침입니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="092f6-103">Azure Resource Manager 템플릿 생성 모범 사례</span><span class="sxs-lookup"><span data-stu-id="092f6-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="092f6-104">이러한 지침을 사용 하면 신뢰할 수 있는 쉽고 toouse 된 Azure 리소스 관리자 템플릿이 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="092f6-105">hello 지침만 제안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="092f6-106">명시된 경우를 제외하고 필수 사항은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="092f6-107">시나리오 hello 중 하나의 변형 해야 합니다. 다음 접근 방식 또는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="092f6-108">리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-108">Resource names</span></span>
<span data-ttu-id="092f6-109">일반적으로 Resource Manager에서는 세 가지 유형의 리소스 이름으로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="092f6-110">고유해야 하는 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="092f6-111">되지 않는 리소스 이름이 필요 toobe 고유 하지만, 컨텍스트를 기준으로 리소스를 식별 하는 수 있는 이름이 tooprovide 선택.</span><span class="sxs-lookup"><span data-stu-id="092f6-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="092f6-112">일반적일 수 있는 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="092f6-113">리소스 이름 제한에 대한 자세한 내용은 [Azure 리소스에 대한 권장 명명 규칙](../guidance/guidance-naming-conventions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092f6-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="092f6-114">고유한 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-114">Unique resource names</span></span>
<span data-ttu-id="092f6-115">데이터 액세스 끝점이 있는 모든 리소스 유형에 대해 고유한 리소스 이름을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="092f6-116">고유 이름이 필요한 일반적인 리소스 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="092f6-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="092f6-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="092f6-118">Azure App Service의 Web Apps 기능</span><span class="sxs-lookup"><span data-stu-id="092f6-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="092f6-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="092f6-119">SQL Server</span></span>
* <span data-ttu-id="092f6-120">Azure 키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="092f6-120">Azure Key Vault</span></span>
* <span data-ttu-id="092f6-121">Azure Redis 캐시(영문)</span><span class="sxs-lookup"><span data-stu-id="092f6-121">Azure Redis Cache</span></span>
* <span data-ttu-id="092f6-122">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="092f6-122">Azure Batch</span></span>
* <span data-ttu-id="092f6-123">Azure 트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="092f6-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="092f6-124">Azure 검색</span><span class="sxs-lookup"><span data-stu-id="092f6-124">Azure Search</span></span>
* <span data-ttu-id="092f6-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="092f6-125">Azure HDInsight</span></span>

<span data-ttu-id="092f6-126"><sup>1</sup> 저장소 계정 이름은 24자 이내의 소문자여야 하며 하이픈은 포함할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="092f6-127">리소스 이름에 대 한 매개 변수를 지정 하는 경우 hello 리소스를 배포할 때 고유 이름을 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="092f6-128">Hello를 사용 하는 변수를 만들 수는 필요에 따라 [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate 이름을 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="092f6-129">또한 수 원하는 tooadd 접두사 또는 toohello 접미사 **uniqueString** 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="092f6-130">Hello 고유 이름을 수정 하 고 더욱 쉽게 hello 이름에서 hello 리소스 종류를 식별할 수 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="092f6-131">예를 들어 변수 다음 hello를 사용 하 여 저장소 계정에 대 한 고유 이름을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="092f6-132">식별을 위한 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-132">Resource names for identification</span></span>
<span data-ttu-id="092f6-133">일부 리소스 유형은 이름만 toobe 고유 하지 않은 있지만 tooname를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="092f6-134">이러한 리소스 종류에 대 한 hello 리소스 컨텍스트와 hello 리소스 종류 모두 식별 하는 이름을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="092f6-135">리소스 목록에 hello 리소스를 식별 하는 데 도움이 되는 설명이 포함 된 이름을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="092f6-136">다양 한 배포에 대 한 다른 리소스 이름을 toouse 해야 할 경우에 hello 이름에 대 한 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="092f6-137">배포 중 이름에 toopass를 필요 하지 않은 경우에 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="092f6-138">하드 코드된 값을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="092f6-139">일반 리소스 이름</span><span class="sxs-lookup"><span data-stu-id="092f6-139">Generic resource names</span></span>
<span data-ttu-id="092f6-140">주로 다른 리소스를 통해 액세스 하는 리소스 종류에 대 한 hello 템플릿에 하드 코드 하는 제네릭 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="092f6-141">예를 들어 SQL Server에서 방화벽 규칙에 대해 표준 일반 이름을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="092f6-142">매개 변수</span><span class="sxs-lookup"><span data-stu-id="092f6-142">Parameters</span></span>
<span data-ttu-id="092f6-143">hello 다음 정보가 유용할 수 매개 변수를 사용 하 여 작업할 때:</span><span class="sxs-lookup"><span data-stu-id="092f6-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="092f6-144">매개 변수 사용을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-144">Minimize your use of parameters.</span></span> <span data-ttu-id="092f6-145">가능하면 항상, 변수 또는 리터럴 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="092f6-146">다음과 같은 시나리오에 대해서만 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="092f6-147">Tooenvironment (SKU, 크기, 용량)에 따라의 toouse 변형을 지정 하는 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="092f6-148">쉽게 식별 하기 위해 toospecify 되도록 하는 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="092f6-149">값을 사용 하는 자주 toocomplete 다른 작업 (예: 관리자 사용자 이름)입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="092f6-150">비밀(예: 암호)</span><span class="sxs-lookup"><span data-stu-id="092f6-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="092f6-151">hello 숫자나 값 toouse 리소스 종류의 여러 인스턴스를 만들 때의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="092f6-152">매개 변수 이름에 카멜식 대/소문자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="092f6-153">Hello 메타 데이터의 모든 매개 변수에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="092f6-154">매개 변수의 기본값을 정의합니다(암호 및 SSH 키 제외).</span><span class="sxs-lookup"><span data-stu-id="092f6-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="092f6-155">모든 암호(password) 및 비밀(secret)에 대해 **SecureString**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="092f6-156">가능 하면 항상 매개 변수 toospecify 위치를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="092f6-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="092f6-157">대신, hello를 사용 하 여 **위치** hello 리소스 그룹의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="092f6-158">Hello를 사용 하 여 **resourceGroup ().location** 모든 리소스에 대 한 식, hello 서식 파일의 리소스에 배포 된 hello 같은 hello 리소스 그룹 위치:</span><span class="sxs-lookup"><span data-stu-id="092f6-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="092f6-159">제한 된 수의 위치에서는 리소스 종류는 지원 toospecify hello 서식 파일에서 직접 올바른 위치를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="092f6-160">사용 해야 할 경우는 **위치** 매개 변수를 해당 매개 변수 값을 가능한 한 hello에 가능성이 toobe 않은 리소스와 공유 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="092f6-161">이 사용자에 게 tooprovide 위치 정보를 요청 하는 횟수 hello 만큼을 최소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="092f6-162">리소스 종류에 대 한 hello API 버전에 대 한 매개 변수 또는 변수를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="092f6-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="092f6-163">리소스 속성 및 값은 버전 번호에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="092f6-164">코드 편집기의 IntelliSense는 hello API 버전 tooa 매개 변수 또는 변수에 설정 된 경우 hello 올바른 스키마를 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="092f6-165">대신, 하드 코딩 hello hello 서식 파일에서 API 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="092f6-166">variables</span><span class="sxs-lookup"><span data-stu-id="092f6-166">Variables</span></span>
<span data-ttu-id="092f6-167">hello 다음 정보가 유용할 수 변수를 사용 하 여 작업할 때:</span><span class="sxs-lookup"><span data-stu-id="092f6-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="092f6-168">된다고 toouse 두 번 이상 서식 파일의 값에 대 한 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="092f6-169">값을 한 번만 사용 되는 경우 하드 코드 된 값 이면 템플릿을 쉽게 tooread.</span><span class="sxs-lookup"><span data-stu-id="092f6-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="092f6-170">Hello를 사용할 수 없습니다 [참조](resource-group-template-functions-resource.md#reference) 함수 hello에 **변수** hello 서식 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="092f6-171">hello **참조** 함수 hello 리소스의 런타임 상태에서 해당 값을 파생 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="092f6-172">그러나 변수 hello 초기 hello 서식 파일의 구문 분석 하는 동안 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="092f6-173">Hello를 필요로 하는 값을 생성 **참조** hello에서 직접 함수 **리소스** 또는 **출력** hello 서식 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="092f6-174">[리소스 이름](#resource-names)에 설명된 대로 고유해야 하는 리소스 이름에 대한 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="092f6-175">변수를 복잡한 개체로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-175">You can group variables into complex objects.</span></span> <span data-ttu-id="092f6-176">사용 하 여 hello **variable.subentry** tooreference 복잡 한 개체의 값 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="092f6-177">변수 그룹화는 관련 변수를 추적하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="092f6-178">또한 hello 서식 파일의 가독성을 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-178">It also improves readability of hello template.</span></span> <span data-ttu-id="092f6-179">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="092f6-180">복잡한 개체에는 복잡한 개체의 값을 참조하는 식이 포함될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="092f6-181">이 목적을 위해서는 별도의 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="092f6-182">복잡한 개체를 변수로 사용하는 고급 예제를 보려면 [Azure Resource Manager 템플릿에서 상태 공유](best-practices-resource-manager-state.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092f6-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="092f6-183">리소스</span><span class="sxs-lookup"><span data-stu-id="092f6-183">Resources</span></span>
<span data-ttu-id="092f6-184">hello 다음 정보가 유용할 수 리소스를 사용 하 여 작업할 때:</span><span class="sxs-lookup"><span data-stu-id="092f6-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="092f6-185">toohelp 다른 참가자 hello 리소스의 hello 목적을 이해, 지정 **주석** hello 서식 파일의 각 리소스에 대해:</span><span class="sxs-lookup"><span data-stu-id="092f6-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="092f6-186">태그 tooadd 메타 데이터 tooresources를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="092f6-187">리소스에 대 한 메타 데이터 tooadd 정보를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="092f6-188">예를 들어 toorecord 메타 데이터는 리소스에 대 한 청구 정보를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="092f6-189">자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="092f6-190">사용 하는 경우는 *공용 끝점* (예: Azure Blob 저장소 공용 끝점), 템플릿에 *하드 코딩 하지 마십시오* hello 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="092f6-191">사용 하 여 hello **참조** 함수 toodynamically hello 네임 스페이스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="092f6-192">이 접근 방식을 toodeploy hello 템플릿 toodifferent 공용 네임 스페이스 환경 hello 템플릿에서 hello 끝점을 수동으로 변경 하지 않고 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="092f6-193">Hello API 버전 toohello 설정 hello 저장소 계정에 대 한 서식 파일에는 사용 하는 동일한 버전:</span><span class="sxs-lookup"><span data-stu-id="092f6-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="092f6-194">저장소 계정 hello hello에 배포 된 경우 만들고 있는 동일한 템플릿을 않아도 toospecify hello 공급자 네임 스페이스 hello 리소스를 참조 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="092f6-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="092f6-195">다음은 hello 간소화 된 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="092f6-196">다른 값을 서식 파일에 구성 된 toouse 공용 네임 스페이스를 사용 하도록 설정한 경우 이러한 값을 변경 합니다. 동일한 tooreflect hello **참조** 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="092f6-197">예를 들어 hello를 설정할 수 있습니다 **storageUri** hello 가상 컴퓨터 진단 프로필의 속성:</span><span class="sxs-lookup"><span data-stu-id="092f6-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="092f6-198">다른 리소스 그룹에서 기존 저장소 계정을 참조할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="092f6-199">응용 프로그램에서 필요로 하는 경우에 공용 IP 주소 tooa 가상 컴퓨터를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="092f6-200">tooconnect tooa 또는 가상 컴퓨터 (VM) 디버깅을 위한 관리 또는 관리 목적을 위한 인바운드 NAT 규칙, 가상 네트워크 게이트웨이 또는 jumpbox 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="092f6-201">Toovirtual 컴퓨터를 연결 하는 방법에 대 한 자세한 내용은 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="092f6-202">Azure에서 N 계층 아키텍처에 대한 VM 실행</span><span class="sxs-lookup"><span data-stu-id="092f6-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="092f6-203">Azure Resource Manager에서 VM에 대한 WinRM 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="092f6-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="092f6-204">외부 액세스 tooyour VM hello Azure 포털을 사용 하 여 허용</span><span class="sxs-lookup"><span data-stu-id="092f6-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="092f6-205">PowerShell을 사용 하 여 외부 액세스 tooyour VM 허용</span><span class="sxs-lookup"><span data-stu-id="092f6-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="092f6-206">Azure CLI를 사용 하 여 외부 액세스 tooyour Linux VM 수</span><span class="sxs-lookup"><span data-stu-id="092f6-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="092f6-207">hello **domainNameLabel** 공용 IP 주소에 대 한 속성은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="092f6-208">hello **domainNameLabel** 값 3-63 자 사이 여야 하며이 정규식으로 지정 된 hello 규칙을 따릅니다: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="092f6-209">때문에 hello **uniqueString** 함수는 13 자 hello 하는 문자열을 생성 **dnsPrefixString** 매개 변수는 제한 된 too50 문자:</span><span class="sxs-lookup"><span data-stu-id="092f6-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="092f6-210">Hello를 사용 하 여 암호 tooa 사용자 지정 스크립트 확장을 추가 하면 **commandToExecute** hello에 대 한 속성 **protectedSettings** 속성:</span><span class="sxs-lookup"><span data-stu-id="092f6-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="092f6-211">암호는 tooensure tooVMs 매개 변수 및 확장으로 전달 될 때 암호화를 사용 하 여 hello **protectedSettings** hello 관련 확장의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="092f6-212">outputs</span><span class="sxs-lookup"><span data-stu-id="092f6-212">Outputs</span></span>
<span data-ttu-id="092f6-213">서식 파일 toocreate 공용 IP 주소를 사용 하 여는 **출력** hello IP 주소와 hello 정규화 된 도메인 이름 (FQDN)의 세부 정보를 반환 하는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="092f6-214">배포 후 공용 IP 주소와 Fqdn에 대 한 출력 값 tooeasily 검색 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="092f6-215">Hello 리소스를 참조 하는 경우 toocreate를 사용 하 여 hello API 버전을 사용 하기:</span><span class="sxs-lookup"><span data-stu-id="092f6-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="092f6-216">단일 템플릿 또는 중첩된 템플릿</span><span class="sxs-lookup"><span data-stu-id="092f6-216">Single template vs. nested templates</span></span>
<span data-ttu-id="092f6-217">toodeploy 솔루션에 여러 개의 중첩 된 템플릿으로 단일 템플릿 또는 기본 서식 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="092f6-218">중첩된 템플릿은 좀 더 수준 높은 시나리오에서 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="092f6-219">다음 이점을 hello 중첩 된 템플릿 제공을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="092f6-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="092f6-220">솔루션을 대상 구성 요소로 세분화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="092f6-221">중첩된 템플릿은 다른 주 템플릿에서 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="092f6-222">중첩 toouse 서식 파일을 선택 하면 표준화 템플릿 디자인 지침에 따라 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="092f6-223">이러한 지침은 [Azure Resource Manager 템플릿 디자인 패턴](best-practices-resource-manager-design-templates.md)을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="092f6-224">다음 템플릿 hello 있는 디자인을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="092f6-225">**주 템플릿** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="092f6-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="092f6-226">Hello 입력된 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="092f6-227">**공유 리소스 템플릿**.</span><span class="sxs-lookup"><span data-stu-id="092f6-227">**Shared resources template**.</span></span> <span data-ttu-id="092f6-228">사용 하 여 toodeploy 공유 된 다른 모든 리소스를 사용 하는 리소스 (예를 들어 가상 네트워크 및 가용성 집합).</span><span class="sxs-lookup"><span data-stu-id="092f6-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="092f6-229">사용 하 여 hello **dependsOn** 이 템플릿은 다른 템플릿에 하기 전에 배포 된 식 tooensure 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="092f6-230">**선택적 리소스 템플릿**.</span><span class="sxs-lookup"><span data-stu-id="092f6-230">**Optional resources template**.</span></span> <span data-ttu-id="092f6-231">사용 하 여 tooconditionally 매개 변수 (예를 들어 jumpbox)에 따라 리소스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="092f6-232">**멤버 리소스 템플릿**.</span><span class="sxs-lookup"><span data-stu-id="092f6-232">**Member resources template**.</span></span> <span data-ttu-id="092f6-233">응용 프로그램 계층 내의 각 인스턴스 형식은 자체 구성을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="092f6-234">계층 내에서 서로 다른 인스턴스 형식을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="092f6-235">(예를 들어 hello 첫 번째 인스턴스는 클러스터를 만들고 및 인스턴스가 더 toohello 기존 클러스터에 추가 됩니다.) 각 인스턴스 형식에는 고유한 배포 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="092f6-236">**스크립트**.</span><span class="sxs-lookup"><span data-stu-id="092f6-236">**Scripts**.</span></span> <span data-ttu-id="092f6-237">폭 넓게 재사용할 수 있는 스크립트를 각 인스턴스 형식에 적용할 수 있습니다(예: 추가 디스크 초기화 및 포맷).</span><span class="sxs-lookup"><span data-stu-id="092f6-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="092f6-238">특정 사용자 지정 목적을 위해 생성 된 사용자 지정 스크립트는 hello 인스턴스 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![중첩된 템플릿](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="092f6-240">자세한 내용은 [Azure Resource Manager에서 연결된 템플릿 사용](resource-group-linked-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092f6-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="092f6-241">조건에 따라 toonested 템플릿 연결</span><span class="sxs-lookup"><span data-stu-id="092f6-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="092f6-242">매개 변수 tooconditionally 링크 toonested 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="092f6-243">hello 매개 변수를 사용 하면 hello 서식 파일에 대 한 hello URI의 일부가:</span><span class="sxs-lookup"><span data-stu-id="092f6-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="092f6-244">템플릿 형식</span><span class="sxs-lookup"><span data-stu-id="092f6-244">Template format</span></span>
<span data-ttu-id="092f6-245">것이 좋습니다 toopass JSON 유효성 검사기를 통해 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="092f6-246">유효성 검사기를 통해 불필요한 쉼표, 괄호 및 배포 중에 오류를 유발할 수 있는 대괄호를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="092f6-247">자주 사용하는 편집 환경을 위해 [JSONLint](http://jsonlint.com/) 또는 linter 패키지를 사용합니다(Visual Studio Code, Atom, Sublime Text, Visual Studio 등).</span><span class="sxs-lookup"><span data-stu-id="092f6-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="092f6-248">좋습니다 tooformat 이기도 가독성을 높이기 위해, JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="092f6-249">로컬 편집기에 대한 JSON 포맷터 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="092f6-250">키를 눌러 Visual studio에서는 tooformat hello 문서 **Ctrl + K, Ctrl + D**합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="092f6-251">Visual Studio Code에서 **Alt+Shift+F**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="092f6-252">로컬 편집기 hello 문서의 서식을 지정 하지 않습니다, 하는 경우 사용할 수 있습니다는 [온라인 포맷터](https://www.bing.com/search?q=json+formatter)합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="092f6-253">다음 단계</span><span class="sxs-lookup"><span data-stu-id="092f6-253">Next steps</span></span>
* <span data-ttu-id="092f6-254">가상 컴퓨터를 위한 솔루션 설계에 대한 자세한 내용은 [Azure에서 Windows VM 실행](../guidance/guidance-compute-single-vm.md) 및 [Azure에서 Linux VM 실행](../guidance/guidance-compute-single-vm-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092f6-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="092f6-255">저장소 계정 설정에 대한 자세한 내용은 [Azure Storage 성능 및 확장성 검사 목록](../storage/common/storage-performance-checklist.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="092f6-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="092f6-256">toolearn 엔터프라이즈 tooeffectively 리소스 관리자를 사용 하는 방법에 대 한 구독 관리, 참조 [Azure enterprise 스 캐 폴딩: 규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="092f6-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

