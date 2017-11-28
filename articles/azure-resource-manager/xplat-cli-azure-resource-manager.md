---
title: "hello Azure CLI를 사용 하 여 aaaManage 리소스 | Microsoft Docs"
description: "Hello Azure 명령줄 인터페이스 (CLI) toomanage Azure를 사용 하 여 리소스 및 그룹"
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
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a><span data-ttu-id="45efd-103">Hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="45efd-103">Use hello Azure CLI toomanage Azure resources and resource groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45efd-104">포털</span><span class="sxs-lookup"><span data-stu-id="45efd-104">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="45efd-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="45efd-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="45efd-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="45efd-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="45efd-107">REST API</span><span class="sxs-lookup"><span data-stu-id="45efd-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="45efd-108">hello Azure CLI (명령줄 인터페이스 Azure)는 하나는 여러 도구 중 toodeploy를 사용 하 여 고 리소스 관리자와 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-108">hello Azure Command-Line Interface (Azure CLI) is one of several tools you can use toodeploy and manage resources with Resource Manager.</span></span> <span data-ttu-id="45efd-109">이 문서에서는 일반적인 방법으로 toomanage Azure 소개 리소스 및 리소스 그룹을 사용 하 여 리소스 관리자 모드에서 Azure CLI hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-109">This article introduces common ways toomanage Azure resources and resource groups by using hello Azure CLI in Resource Manager mode.</span></span> <span data-ttu-id="45efd-110">Hello CLI toodeploy 리소스를 사용 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](resource-group-template-deploy-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-110">For information about using hello CLI toodeploy resources, see [Deploy resources with Resource Manager templates and Azure CLI](resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="45efd-111">Azure 리소스 및 리소스 관리자에 대 한 배경 방문 hello [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-111">For background about Azure resources and Resource Manager, visit hello [Azure Resource Manager Overview](resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="45efd-112">toomanage Azure hello Azure CLI를 사용 하 여 리소스를 필요한 너무[hello Azure CLI 설치](../cli-install-nodejs.md), 및 [tooAzure 로그인](../xplat-cli-connect.md) hello를 사용 하 여 `azure login` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-112">toomanage Azure resources with hello Azure CLI, you need too[install hello Azure CLI](../cli-install-nodejs.md), and [log in tooAzure](../xplat-cli-connect.md) by using hello `azure login` command.</span></span> <span data-ttu-id="45efd-113">CLI는 리소스 관리자 모드에서 확인 되었는지 hello (실행 `azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="45efd-113">Make sure hello CLI is in Resource Manager mode (run `azure config mode arm`).</span></span> <span data-ttu-id="45efd-114">다음과 같은이 작업을 수행 하는 경우 준비 toogo 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-114">If you've done these things, you're ready toogo.</span></span>
> 
> 

## <a name="get-resource-groups-and-resources"></a><span data-ttu-id="45efd-115">리소스 그룹 및 리소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="45efd-115">Get resource groups and resources</span></span>
### <a name="resource-groups"></a><span data-ttu-id="45efd-116">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="45efd-116">Resource groups</span></span>
<span data-ttu-id="45efd-117">tooget 구독 및 해당 위치에 있는 모든 리소스 그룹의 목록에는이 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-117">tooget a list of all resource groups in your subscription and their locations, run this command.</span></span>

    azure group list


### <a name="resources"></a><span data-ttu-id="45efd-118">리소스</span><span class="sxs-lookup"><span data-stu-id="45efd-118">Resources</span></span>
 <span data-ttu-id="45efd-119">toolist와 같은 그룹의 모든 리소스 이름을 *testRG*, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="45efd-119">toolist all resources in a group, such as one with name *testRG*, use hello following command:</span></span>

    azure resource list testRG

<span data-ttu-id="45efd-120">명명 된 VM과 같은 hello 그룹 내에서 개별 리소스 tooview *MyUbuntuVM*를 hello 다음과 같은 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="45efd-120">tooview an individual resource within hello group, such as a VM named *MyUbuntuVM*, use a command like hello following:</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="45efd-121">공지 hello **Microsoft.Compute/virtualMachines** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-121">Notice hello **Microsoft.Compute/virtualMachines** parameter.</span></span> <span data-ttu-id="45efd-122">이 매개 변수에서 정보를 요청 하는 hello 리소스의 hello 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-122">This parameter indicates hello type of hello resource you are requesting information on.</span></span>

> [!NOTE]
> <span data-ttu-id="45efd-123">Hello를 사용 하는 경우 **azure 리소스** hello 이외의 명령을 **목록** hello hello 리소스의 hello API 버전 지정 해야 합니다. 명령을 **-o** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-123">When using hello **azure resource** commands other than hello **list** command, you must specify hello API version of hello resource with hello **-o** parameter.</span></span> <span data-ttu-id="45efd-124">Hello API 버전에 대 한 잘 모를 경우 hello 템플릿 파일을 참조 하 고 hello 리소스에 대 한 hello apiVersion 필드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-124">If you're unsure about hello API version, consult hello template file and find hello apiVersion field for hello resource.</span></span> <span data-ttu-id="45efd-125">Resource Manager의 API 버전에 대한 자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45efd-125">For more about API versions in Resource Manager, see [Resource providers and types](resource-manager-supported-services.md).</span></span>
> 
> 

<span data-ttu-id="45efd-126">경우 리소스에 대해 세부 정보를 보는 것이 유용한 toouse hello `--json` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-126">When viewing details on a resource, it is often useful toouse hello `--json` parameter.</span></span> <span data-ttu-id="45efd-127">이 매개 변수 되므로 일부 값은 중첩 된 구조 또는 컬렉션 보다 읽기 쉬운 hello 출력을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-127">This parameter makes hello output more readable, because some values are nested structures, or collections.</span></span> <span data-ttu-id="45efd-128">hello 다음 예제에서는 hello의 hello 결과 반환 **표시** JSON 문서 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-128">hello following example demonstrates returning hello results of hello **show** command as a JSON document.</span></span>

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> <span data-ttu-id="45efd-129">원하는 경우 hello를 사용 하 여 JSON 데이터 toofile hello 저장 &gt; 문자 toodirect hello 출력 tooa 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-129">If you want, save hello JSON data toofile by using hello &gt; character toodirect hello output tooa file.</span></span> <span data-ttu-id="45efd-130">예:</span><span class="sxs-lookup"><span data-stu-id="45efd-130">For example:</span></span>
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a><span data-ttu-id="45efd-131">태그</span><span class="sxs-lookup"><span data-stu-id="45efd-131">Tags</span></span>
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a><span data-ttu-id="45efd-132">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="45efd-132">Manage resources</span></span>
<span data-ttu-id="45efd-133">저장소 계정 tooa 리소스 그룹을 같은 리소스 tooadd 비슷한 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-133">tooadd a resource such as a storage account tooa resource group, run a command similar to:</span></span>

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

<span data-ttu-id="45efd-134">또한이 toospecifying hello 리소스의 API 버전을 hello로 hello **-o** 매개 변수를 사용 하 여 hello **-p** 와 모든 필수 매개 변수 toopass JSON 형식 문자열 또는 추가 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-134">In addition toospecifying hello API version of hello resource with hello **-o** parameter, use hello **-p** parameter toopass a JSON-formatted string with any required or additional properties.</span></span>

<span data-ttu-id="45efd-135">가상 컴퓨터 리소스와 같은 기존 리소스 toodelete hello 다음과 같은 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-135">toodelete an existing resource such as a virtual machine resource, use a command like hello following:</span></span>

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

<span data-ttu-id="45efd-136">toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 **azure 리소스 이동** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-136">toomove existing resources tooanother resource group or subscription, use hello **azure resource move** command.</span></span> <span data-ttu-id="45efd-137">hello 방법을 예제와 다음 toomove Redis Cache tooa 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-137">hello following example shows how toomove a Redis Cache tooa new resource group.</span></span> <span data-ttu-id="45efd-138">Hello에 **-i** 매개 변수를 toomove hello 리소스 id의 쉼표로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-138">In hello **-i** parameter, provide a comma-separated list of hello resource id's toomove.</span></span>

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a><span data-ttu-id="45efd-139">컨트롤 액세스 tooresources</span><span class="sxs-lookup"><span data-stu-id="45efd-139">Control access tooresources</span></span>
<span data-ttu-id="45efd-140">Azure CLI toocreate hello를 사용 하 고 정책 toocontrol tooAzure 리소스 액세스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-140">You can use hello Azure CLI toocreate and manage policies toocontrol access tooAzure resources.</span></span> <span data-ttu-id="45efd-141">정책 정 및 할당 정책 tooresources 대 한 배경 정보를 참조 하십시오. [정책 toomanage 리소스를 사용 하 고 액세스 제어](resource-manager-policy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-141">For background about policy definitions and assigning policies tooresources, see [Use policy toomanage resources and control access](resource-manager-policy.md).</span></span>

<span data-ttu-id="45efd-142">예를 들어 hello 정책 toodeny 다음 여기서 위치는 하지 West US 또는 북 중미 모든 요청을 정의 하 고 toohello 정책 정의 파일 policy.json 저장:</span><span class="sxs-lookup"><span data-stu-id="45efd-142">For example, define hello following policy toodeny all requests where location is not West US or North Central US, and save it toohello policy definition file policy.json:</span></span>

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

<span data-ttu-id="45efd-143">그러고 나 서 hello **정책 정의 만들기** 명령:</span><span class="sxs-lookup"><span data-stu-id="45efd-143">Then run hello **policy definition create** command:</span></span>

    azure policy definition create MyPolicy -p c:\temp\policy.json

<span data-ttu-id="45efd-144">이 명령은 유사한 toohello 다음을 출력을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-144">This command shows output similar toohello following:</span></span>

    + <span data-ttu-id="45efd-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span><span class="sxs-lookup"><span data-stu-id="45efd-145">Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy</span></span>

    <span data-ttu-id="45efd-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span><span class="sxs-lookup"><span data-stu-id="45efd-146">data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny</span></span>

 <span data-ttu-id="45efd-147">정책 범위의 hello 사용 하 여 hello tooassign **PolicyDefinitionId** hello 이전 명령에서 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-147">tooassign a policy at hello scope you want, use hello **PolicyDefinitionId** returned from hello previous command.</span></span> <span data-ttu-id="45efd-148">다음 예제는 hello,이 범위 hello 구독 하지만 tooresource 그룹이 나 개별 리소스 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-148">In hello following example, this scope is hello subscription, but you can scope tooresource groups or individual resources:</span></span>

    <span data-ttu-id="45efd-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span><span class="sxs-lookup"><span data-stu-id="45efd-149">azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/</span></span>

<span data-ttu-id="45efd-150">가져오기, 변경 또는 hello를 사용 하 여 정책 정의 제거 **정책 정의 표시**, **정책 정의 집합**, 및 **정책 정의 삭제** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-150">You can get, change, or remove policy definitions by using hello **policy definition show**, **policy definition set**, and **policy definition delete** commands.</span></span>

<span data-ttu-id="45efd-151">마찬가지로, 또는 얻을 수 있습니다, 변경, 정책 할당 hello를 사용 하 여 제거 **정책 할당 표시**, **정책 할당 집합**, 및 **정책 할당을 삭제** 명령 .</span><span class="sxs-lookup"><span data-stu-id="45efd-151">Similarly, you can get, change, or remove policy assignments by using hello **policy assignment show**, **policy assignment set**, and **policy assignment delete** commands.</span></span>

## <a name="export-a-resource-group-as-a-template"></a><span data-ttu-id="45efd-152">리소스 그룹을 템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="45efd-152">Export a resource group as a template</span></span>
<span data-ttu-id="45efd-153">기존 리소스 그룹에 대 한 hello 리소스 그룹에 대 한 hello 리소스 관리자 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-153">For an existing resource group, you can view hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="45efd-154">내보내는 hello 서식 파일에는 두 가지 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-154">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="45efd-155">모든 hello 인프라 hello 서식 파일에 정의 되어 있기 때문에 쉽게 hello 솔루션의 향후 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-155">You can easily automate future deployments of hello solution because all hello infrastructure is defined in hello template.</span></span>
2. <span data-ttu-id="45efd-156">템플릿 구문에 잘 알고 hello 솔루션을 나타내는 JSON 보고 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-156">You can become familiar with template syntax by looking at hello JSON that represents your solution.</span></span>

<span data-ttu-id="45efd-157">Hello Azure CLI를 사용 하 여 hello 리소스 그룹의 현재 상태를 나타내는 템플릿 내보내기 하거나 특정 배포에 사용 된 hello 템플릿을 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-157">Using hello Azure CLI, you can either export a template that represents hello current state of your resource group, or download hello template that was used for a particular deployment.</span></span>

* <span data-ttu-id="45efd-158">**리소스 그룹에 대 한 hello 템플릿 내보내기** -이 변경 내용 tooa 리소스 그룹에서 항목과 필요한 tooretrieve hello 현재 상태로의 JSON 표현을 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-158">**Export hello template for a resource group** - This is helpful when you made changes tooa resource group, and need tooretrieve hello JSON representation of its current state.</span></span> <span data-ttu-id="45efd-159">그러나 생성 된 템플릿 hello 최소한 매개 변수 및 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-159">However, hello generated template contains only a minimal number of parameters and no variables.</span></span> <span data-ttu-id="45efd-160">대부분의 hello 값 hello 템플릿에 하드 코드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-160">Most of hello values in hello template are hard-coded.</span></span> <span data-ttu-id="45efd-161">Hello 생성 된 서식 파일을 배포 하기 전에 수도 있습니다 tooconvert hello 값 중 매개 변수를 다양 한 환경에 대 한 hello 배포를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-161">Before deploying hello generated template, you may wish tooconvert more of hello values into parameters so you can customize hello deployment for different environments.</span></span>
  
    <span data-ttu-id="45efd-162">리소스 그룹 tooa 로컬 디렉터리를 hello 실행에 대 한 tooexport hello 템플릿을 `azure group export` hello 다음 예제와 같이 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-162">tooexport hello template for a resource group tooa local directory, run hello `azure group export` command as shown in hello following example.</span></span> <span data-ttu-id="45efd-163">(운영 체제 환경에 맞게 적합한 로컬 디렉터리로 대체)</span><span class="sxs-lookup"><span data-stu-id="45efd-163">(Substitute a local directory appropriate for your operating system environment.)</span></span>
  
        azure group export testRG ~/azure/templates/
* <span data-ttu-id="45efd-164">**특정 배포에 대 한 hello 템플릿을 다운로드** -tooview hello 실제 서식 파일을 사용 하는 toodeploy 리소스 했습니다 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-164">**Download hello template for a particular deployment** -- This is helpful when you need tooview hello actual template that was used toodeploy resources.</span></span> <span data-ttu-id="45efd-165">모든 매개 변수 및 변수 hello 원래 배포에 대해 정의 된 hello 서식 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-165">hello template includes all parameters and variables defined for hello original deployment.</span></span> <span data-ttu-id="45efd-166">그러나 시도 하면 조직의 누군가가 hello 정의 외부에서 변경 내용 toohello 리소스 그룹 hello 서식 파일에서이 템플릿을 hello hello 리소스 그룹의 현재 상태를 나타내지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-166">However, if someone in your organization made changes toohello resource group outside of hello definition in hello template, this template doesn't represent hello current state of hello resource group.</span></span>
  
    <span data-ttu-id="45efd-167">특정 배포 tooa 로컬 디렉터리 hello 실행에 사용 되는 toodownload hello 템플릿입니다 `azure group deployment template download` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-167">toodownload hello template used for a particular deployment tooa local directory, run hello `azure group deployment template download` command.</span></span> <span data-ttu-id="45efd-168">예:</span><span class="sxs-lookup"><span data-stu-id="45efd-168">For example:</span></span>
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> <span data-ttu-id="45efd-169">템플릿 내보내기는 미리 보기 버전이며, 템플릿 내보내기를 지원하지 않는 리소스 유형도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-169">Template export is in preview, and not all resource types currently support exporting a template.</span></span> <span data-ttu-id="45efd-170">Tooexport 서식 파일을 시도할 때 일부 리소스를 내보내지 못했습니다 되었다는 오류가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-170">When attempting tooexport a template, you may see an error that states some resources were not exported.</span></span> <span data-ttu-id="45efd-171">필요한 경우 템플릿을 다운로드한 후 템플릿에서 이러한 리소스를 수동으로 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-171">If needed, manually define these resources in your template after downloading it.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="45efd-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="45efd-172">Next steps</span></span>
* <span data-ttu-id="45efd-173">배포 작업의 세부 정보 tooget hello Azure CLI를 사용 하 여 배포 오류 문제를 해결 하 고, 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-173">tooget details of deployment operations and troubleshoot deployment errors with hello Azure CLI, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="45efd-174">응용 프로그램 또는 스크립트 tooaccess 리소스를 toouse hello CLI tooset 참조 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](resource-group-authenticate-service-principal-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-174">If you want toouse hello CLI tooset up an application or script tooaccess resources, see [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md).</span></span>
* <span data-ttu-id="45efd-175">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45efd-175">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

