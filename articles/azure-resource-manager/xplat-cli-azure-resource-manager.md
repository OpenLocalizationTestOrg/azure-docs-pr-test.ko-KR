---
title: "Azure CLI를 사용하여 리소스 관리 | Microsoft Docs"
description: "Azure 명령줄 인터페이스 (CLI)를 사용하여 Azure 리소스 및 그룹 관리"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3ad4e68b90979fd7f9d3ddf5278e65e19cb07152
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-cli-to-manage-azure-resources-and-resource-groups"></a><span data-ttu-id="654f5-103">Azure 리소스 및 리소스 그룹 관리를 위해 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="654f5-103">Use the Azure CLI to manage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="654f5-104">포털</span><span class="sxs-lookup"><span data-stu-id="654f5-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="654f5-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="654f5-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="654f5-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="654f5-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="654f5-107">REST API</span><span class="sxs-lookup"><span data-stu-id="654f5-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="654f5-108">Azure 명령줄 인터페이스 (Azure CLI)는 리소스 관리자를 사용하여 리소스를 배포하고 관리하는 데 사용할 수 있는 몇 가지 도구 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-108">The Azure Command-Line Interface (Azure CLI) is one of several tools you can use to deploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="654f5-109">이 문서에서는 리소스 관리자 모드에서 Azure CLI를 사용하여 Azure 리소스 및 리소스 그룹을 관리하는 일반적인 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-109">This article introduces common ways to manage Azure resources and resource groups by using the Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="654f5-110">리소스를 배포하기 위해 CLI를 사용하는 방법에 대한 정보는 [Resource Manager 템플릿 및 Azure CLI를 사용하여 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-110">For information about using the CLI to deploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="654f5-111">Azure 리소스 및 Resource Manager에 대한 기본 지식은 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-111">For background about Azure resources and Resource Manager, visit the [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="654f5-112">Azure CLI를 사용하여 Azure 리소스를 관리하려면 `azure login` 명령을 사용하여 [Azure CLI를 설치](../cli-install-nodejs.md)하고 [Azure에 로그인](../xplat-cli-connect.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-112">To manage Azure resources with the Azure CLI, you need to [install the Azure CLI](../cli-install-nodejs.md), and [log in to Azure](../xplat-cli-connect.md) by using the `azure login` command.</span></span> <span data-ttu-id="654f5-113">CLI가 리소스 관리자 모드에 있는지 확인합니다.(`azure config mode arm`를 실행함)</span><span class="sxs-lookup"><span data-stu-id="654f5-113">Make sure the CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="654f5-114">이러한 작업이 완료되면 사용할 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-114">If you've done these things, you're ready to go.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="654f5-115">리소스 그룹 및 리소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="654f5-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="654f5-116">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="654f5-116">Resource groups</span></span>
<span data-ttu-id="654f5-117">구독 및 해당 위치에서 모든 리소스 그룹 목록을 가져오려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-117">To get a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="654f5-118">리소스</span><span class="sxs-lookup"><span data-stu-id="654f5-118">Resources</span></span>
 <span data-ttu-id="654f5-119">이름이 *testRG*인 리소스 등, 그룹의 모든 리소스를 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-119">To list all resources in a group, such as one with name *testRG*, use the following command:</span></span>

    azure resource list testRG

<span data-ttu-id="654f5-120">이름이 *MyUbuntuVM*인 VM 등, 그룹 내의 개별 리소스를 보려면 다음과 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-120">To view an individual resource within the group, such as a VM named *MyUbuntuVM*, use a command like the following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="654f5-121">**Microsoft.Compute/virtualMachines** 매개 변수에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-121">Notice the **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="654f5-122">이 매개 변수는 정보를 요청하는 대상 리소스의 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-122">This parameter indicates the type of the resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="654f5-123">**list** 명령이 아닌 **azure resource** 명령을 사용할 경우 **-o** 매개 변수를 사용하여 리소스의 API 버전을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-123">When using the **azure resource** commands other than the **list** command, you must specify the API version of the resource with the **-o** parameter.</span></span> <span data-ttu-id="654f5-124">API 버전에 관해 확실하지 않은 경우 템플릿 파일을 참조하여 리소스의 apiVersion 필드를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-124">If you're unsure about the API version, consult the template file and find the apiVersion field for the resource.</span></span> <span data-ttu-id="654f5-125">Resource Manager의 API 버전에 대한 자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="654f5-126">`--json` 매개 변수는 보통 리소스 세부 정보를 볼 때 유용하게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-126">When viewing details on a resource, it is often useful to use the `--json` parameter.</span></span> <span data-ttu-id="654f5-127">일부 값이 중첩된 구조이거나 컬렉션이기 때문에 이 매개 변수를 사용하면 출력을 읽기가 훨씬 수월합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-127">This parameter makes the output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="654f5-128">다음 예제에서는 **show** 명령의 결과를 JSON 문서로 반환하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-128">The following example demonstrates returning the results of the **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="654f5-129">원하는 경우 &gt; 문자를 사용하여 파일에 출력되도록 하여 JSON 데이터를 파일에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-129">If you want, save the JSON data to file by using the &gt; character to direct the output to a file.</span></span> <span data-ttu-id="654f5-130">예:</span><span class="sxs-lookup"><span data-stu-id="654f5-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="654f5-131">태그</span><span class="sxs-lookup"><span data-stu-id="654f5-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="654f5-132">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="654f5-132">Manage resources</span></span>
<span data-ttu-id="654f5-133">리소스 그룹에 저장소 계정과 같은 리소스를 추가하려면 다음과 비슷한 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-133">To add a resource such as a storage account to a resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="654f5-134">**-o** 매개 변수를 사용하여 리소스의 API 버전을 지정하는 외에도 **-p** 매개 변수를 사용하여 JSON 형식 문자열을 필수 또는 추가적인 속성과 함께 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-134">In addition to specifying the API version of the resource with the **-o** parameter, use the **-p** parameter to pass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="654f5-135">가상 컴퓨터 리소스와 같은 기존 리소스를 삭제하려면 다음과 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-135">To delete an existing resource such as a virtual machine resource, use a command like the following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="654f5-136">다른 리소스 그룹 또는 구독에 기존 리소스를 이동하려면 **azure resource move** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-136">To move existing resources to another resource group or subscription, use the **azure resource move** command.</span></span> <span data-ttu-id="654f5-137">다음 예제에서는 Redis Cache를 새 리소스 그룹으로 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-137">The following example shows how to move a Redis Cache to a new resource group.</span></span> <span data-ttu-id="654f5-138">**-i** 매개 변수에서 이동할 리소스 ID를 쉼표로 구분한 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-138">In the **-i** parameter, provide a comma-separated list of the resource id's to move.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-to-resources"></a><span data-ttu-id="654f5-139">리소스에 대한 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="654f5-139">Control access to resources</span></span>
<span data-ttu-id="654f5-140">Azure CLI를 사용하여 Azure 리소스에 대한 액세스를 제어하는 정책을 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-140">You can use the Azure CLI to create and manage policies to control access to Azure resources.</span></span> <span data-ttu-id="654f5-141">정책 정의 및 리소스에 정책 할당에 관한 배경 지식은 [정책을 사용하여 리소스 및 컨트롤 액세스 관리](resource-manager-policy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-141">For background about policy definitions and assigning policies to resources, see [Use policy to manage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="654f5-142">예를 들어, 위치가 미국 서부 또는 미국 북중부가 아닌 모든 요청을 거부하도록 다음 정책을 정의하고 정책 정의 파일인 policy.json에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-142">For example, define the following policy to deny all requests where location is not West US or North Central US, and save it to the policy definition file policy.json:</span></span>

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

<span data-ttu-id="654f5-143">그런 다음 **policy definition create**명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-143">Then run the **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="654f5-144">이 명령은 다음과 유사한 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-144">This command shows output similar to the following:</span></span>

    + <span data-ttu-id="654f5-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="654f5-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="654f5-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="654f5-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="654f5-147">정책을 원하는 범위에 할당하려면 이전 명령에서 반환된 **PolicyDefinitionId**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-147">To assign a policy at the scope you want, use the **PolicyDefinitionId** returned from the previous command.</span></span> <span data-ttu-id="654f5-148">다음 예제에서 이 범위는 해당 구독이지만 리소스 그룹이나 개별 리소스에 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-148">In the following example, this scope is the subscription, but you can scope to resource groups or individual resources:</span></span>

    <span data-ttu-id="654f5-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="654f5-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="654f5-150">**policy definition show**, **policy definition set** 및 **policy definition delete** 명령을 사용하여 정책 정의를 가져오거나, 변경하거나 또는 없앨 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-150">You can get, change, or remove policy definitions by using the **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="654f5-151">마찬가지로, **policy assignment show**, **policy assignment set** 및 **policy assignment delete** 명령을 사용하여 정책 할당을 가져오거나, 변경하거나 또는 없앨 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-151">Similarly, you can get, change, or remove policy assignments by using the **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="654f5-152">리소스 그룹을 템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="654f5-152">Export a resource group as a template</span></span>
<span data-ttu-id="654f5-153">기존 리소스 그룹에 대해 해당 리스소 그룹의 리소스 관리자 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-153">For an existing resource group, you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="654f5-154">템플릿을 내보내면 다음과 같은 두 가지 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-154">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="654f5-155">모든 인프라가 템플릿에 정의되어 있기 때문에 향후 솔루션 배포를 간단하게 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-155">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="654f5-156">솔루션을 나타내는 JSON을 살펴보면서 템플릿 구문에 익숙해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-156">You can become familiar with template syntax by looking at the JSON that represents your solution.</span></span>

<span data-ttu-id="654f5-157">Azure CLI를 사용하여 리소스 그룹의 현재 상태를 나타내는 템플릿을 내보내거나 특정 배포에 사용된 템플릿을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-157">Using the Azure CLI, you can either export a template that represents the current state of your resource group, or download the template that was used for a particular deployment.</span></span>

* <span data-ttu-id="654f5-158">**리소스 그룹에 대한 템플릿 내보내기** - 리소스 그룹을 변경했고 현재 상태의 JSON 표현을 검색해야 하는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-158">**Export the template for a resource group** - This is helpful when you made changes to a resource group, and need to retrieve the JSON representation of its current state.</span></span> <span data-ttu-id="654f5-159">그러나 생성된 템플릿에는 최소한의 매개 변수만 포함되고 변수는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-159">However, the generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="654f5-160">템플릿의 값은 대부분 하드 코드됩니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-160">Most of the values in the template are hard-coded.</span></span> <span data-ttu-id="654f5-161">생성된 템플릿을 배포하기 전에, 다양한 환경에 맞게 배포를 사용자 지정할 수 있도록 더 많은 값을 매개 변수로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-161">Before deploying the generated template, you may wish to convert more of the values into parameters so you can customize the deployment for different environments.</span></span>
  
    <span data-ttu-id="654f5-162">리소스 그룹에 대한 템플릿을 로컬 디렉터리로 내보내려면 다음 예제처럼 `azure group export` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-162">To export the template for a resource group to a local directory, run the `azure group export` command as shown in the following example.</span></span> <span data-ttu-id="654f5-163">(운영 체제 환경에 맞게 적합한 로컬 디렉터리로 대체)</span><span class="sxs-lookup"><span data-stu-id="654f5-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="654f5-164">**특정 배포에 대한 템플릿 다운로드** -- 리소스를 배포하는 데 사용된 실제 템플릿을 살펴보아야 하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-164">**Download the template for a particular deployment** -- This is helpful when you need to view the actual template that was used to deploy resources.</span></span> <span data-ttu-id="654f5-165">이 템플릿에는 원래 배포에 대해 정의된 모든 매개 변수와 변수가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-165">The template includes all parameters and variables defined for the original deployment.</span></span> <span data-ttu-id="654f5-166">그러나 조직 내 다른 사람이 템플릿에 정의된 범위를 넘어서 리소스 그룹을 변경할 경우 이 템플릿은 리소스 그룹의 현재 상태를 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-166">However, if someone in your organization made changes to the resource group outside of the definition in the template, this template doesn't represent the current state of the resource group.</span></span>
  
    <span data-ttu-id="654f5-167">특정 배포에 사용한 템플릿을 로컬 디렉터리에 다운로드하려면 `azure group deployment template download` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-167">To download the template used for a particular deployment to a local directory, run the `azure group deployment template download` command.</span></span> <span data-ttu-id="654f5-168">예:</span><span class="sxs-lookup"><span data-stu-id="654f5-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="654f5-169">템플릿 내보내기는 미리 보기 버전이며, 템플릿 내보내기를 지원하지 않는 리소스 유형도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="654f5-170">템플릿 내보내기를 시도할 때 일부 리소스를 내보내지 못했다는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-170">When attempting to export a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="654f5-171">필요한 경우 템플릿을 다운로드한 후 템플릿에서 이러한 리소스를 수동으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="654f5-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="654f5-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="654f5-172">Next steps</span></span>
* <span data-ttu-id="654f5-173">Azure CLI를 사용하여 배포 작업의 자세한 내용을 보고 배포 오류의 문제를 해결하려면 [배포 작업 보기](resource-manager-deployment-operations.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-173">To get details of deployment operations and troubleshoot deployment errors with the Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="654f5-174">CLI를 사용하여 리소스에 액세스하도록 응용 프로그램이나 스크립트를 설정하려면 [Azure CLI를 사용하여 리소스에 액세스하는 서비스 주체 만들기](resource-group-authenticate-service-principal-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-174">If you want to use the CLI to set up an application or script to access resources, see [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="654f5-175">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="654f5-175">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

