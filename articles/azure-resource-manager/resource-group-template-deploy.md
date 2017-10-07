---
title: "PowerShell 및 서식 파일을 사용 하 여 aaaDeploy 리소스 | Microsoft Docs"
description: "리소스 tooAzure toodeploy Azure 리소스 관리자 및 Azure PowerShell을 사용 합니다. hello 리소스는 리소스 관리자 서식 파일에 정의 됩니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="7bf28-104">리소스 관리자 템플릿과 Azure PowerShell로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="7bf28-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="7bf28-105">이 항목에서는 설명 어떻게 리소스 관리자 템플릿 toodeploy와 Azure PowerShell toouse 리소스 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="7bf28-106">발생 Azure 솔루션을 관리 하는 배포의 hello 개념에 익숙하지 않은 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="7bf28-107">hello 리소스 관리자 템플릿 배포를 컴퓨터에 로컬 파일 또는 GitHub와 같은 저장소에 있는 외부 파일 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="7bf28-108">이 문서에 배포 하는 hello 템플릿을 hello에 사용할 수는 [예제 서식 파일](#sample-template) 섹션 또는 as [GitHub의 저장소 계정 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="7bf28-109">로컬 컴퓨터에서 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="7bf28-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="7bf28-110">리소스 tooAzure를 배포할 때 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="7bf28-111">Azure 계정 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="7bf28-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="7bf28-112">배포 된 hello 리소스에 대 한 hello 컨테이너 역할을 하는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="7bf28-113">hello 리소스 그룹의 hello 이름은 영숫자, 마침표, 밑줄, 하이픈 및 괄호에만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="7bf28-114">Too90 문자를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-114">It can be up too90 characters.</span></span> <span data-ttu-id="7bf28-115">마침표로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="7bf28-116">Toohello 리소스 그룹 hello 템플릿을 hello 리소스 toocreate를 정의 하는 배포</span><span class="sxs-lookup"><span data-stu-id="7bf28-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="7bf28-117">템플릿을은 toocustomize hello 배포를 사용 하는 매개 변수를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="7bf28-118">예를 들어 특정 환경(예: 개발, 테스트 및 프로덕션)에 맞게 조정되는 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="7bf28-119">hello 샘플 템플릿은 hello 저장소 계정 SKU에 대 한 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="7bf28-120">다음 예제는 hello 리소스 그룹을 만들고 서식 파일은 로컬 컴퓨터에서 배포.</span><span class="sxs-lookup"><span data-stu-id="7bf28-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="7bf28-121">hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="7bf28-122">완료 되 면 hello 결과 포함 하는 메시지가 표시:</span><span class="sxs-lookup"><span data-stu-id="7bf28-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="7bf28-123">외부 원본에서 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="7bf28-123">Deploy a template from an external source</span></span>

<span data-ttu-id="7bf28-124">로컬 컴퓨터의 리소스 관리자 템플릿을 저장 하는 대신 toostore 경우가 외부 위치에서 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="7bf28-125">원본 제어 리포지토리(예: GitHub)에 템플릿을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="7bf28-126">또는 조직에서 공유 액세스에 대한 Azure Storage 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="7bf28-127">toodeploy 외부 서식 파일을 사용 하 여 hello **TemplateUri** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="7bf28-128">GitHub에서 hello 예제 toodeploy hello 샘플 템플릿에서 URI hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="7bf28-129">hello 앞의 예제에서는 공개적으로 액세스할 수 있는 URI 서식 파일에 중요 한 데이터를 포함 하지 해야 하기 때문에 대부분의 시나리오에 대 한 작동 하는 hello 서식 파일</span><span class="sxs-lookup"><span data-stu-id="7bf28-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="7bf28-130">Toospecify 중요 한 데이터 (예: 관리자 암호) 해야 할 경우 해당 값을 안전한 매개 변수로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="7bf28-131">그러나 하지 않을 경우 서식 파일 toobe 공개적으로 액세스할 수 있는, 개인 저장소 컨테이너에 저장 하 여 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="7bf28-132">SAS(공유 액세스 서명) 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bf28-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="7bf28-133">매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="7bf28-133">Parameter files</span></span>

<span data-ttu-id="7bf28-134">인라인 스크립트에는 값으로 매개 변수를 전달 하는 대신 쉽게 toouse를 hello 매개 변수 값을 포함 하는 JSON 파일 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="7bf28-135">hello 매개 변수 파일 형식에 따라 hello 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-135">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="7bf28-136">Hello 매개 변수 섹션 (storageAccountType) 서식 파일에 정의 된 hello 매개 변수에 일치 하는 매개 변수 이름을 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="7bf28-137">hello 매개 변수 파일 hello 매개 변수의 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="7bf28-138">자동으로이 값은 배포 중 toohello 서식 파일을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="7bf28-139">다양 한 배포 시나리오에 대 한 여러 매개 변수 파일을 만들고 hello 적절 한 매개 변수 파일에 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="7bf28-140">앞 예제는 hello를 복사 하 고 이라는 파일로 저장 `storage.parameters.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="7bf28-141">toopass 로컬 매개 변수 파일을 사용 하 여 hello **TemplateParameterFile** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="7bf28-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="7bf28-142">toopass 외부 매개 변수 파일을 사용 하 여 hello **TemplateParameterUri** 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="7bf28-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="7bf28-143">인라인 매개 변수를 사용할 수 있습니다 및 hello에 로컬 매개 변수 파일 같은 작업을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="7bf28-144">예를 들어 hello 로컬 매개 변수 파일의 일부 값을 지정할 수 있으며 다른 값 인라인을 배포 하는 동안 추가.</span><span class="sxs-lookup"><span data-stu-id="7bf28-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="7bf28-145">Hello 로컬 매개 변수 파일과 인라인 둘 다에 매개 변수의 값을 제공 하는 경우 hello 인라인 값 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="7bf28-146">하지만 외부 매개 변수 파일을 사용하면 인라인 또는 로컬 파일에서 다른 값을 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="7bf28-147">Hello에 매개 변수 파일을 지정할 때 **TemplateParameterUri** 매개 변수, 모든 인라인 매개 변수가 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="7bf28-148">Hello 외부 파일에 있는 모든 매개 변수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="7bf28-149">서식 파일에 hello 매개 변수 파일에 포함할 수 없는 중요 한 값을 포함 하는 경우 해당 값 tooa 키 자격 증명 모음을 추가 하거나 모든 매개 변수 값 인라인을 동적으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="7bf28-150">PowerShell hello 후 위에 서식 파일에서 hello 매개 변수를 제공 hello hello PowerShell 명령에에서 hello 매개 변수 중 하나로 이름과 같은 이름을 가진 매개 변수가 있는 서식 파일의 경우, **FromTemplate**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="7bf28-151">예를 들어 매개 변수 이름 **ResourceGroupName** hello와 사용자 템플릿 충돌에서 **ResourceGroupName** hello에 대 한 매개 변수 [새로 만들기-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bf28-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="7bf28-152">입력 정보 요청된 tooprovide에 대 한 값은 **ResourceGroupNameFromTemplate**합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="7bf28-153">일반적으로 이러한 혼동 하지 배포 작업에 사용 되는 매개 변수로 이름과 같은 이름을 hello로 매개 변수 이름을 지정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7bf28-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="7bf28-154">템플릿 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="7bf28-154">Test a template deployment</span></span>

<span data-ttu-id="7bf28-155">실제로 모든 리소스를 배포 하지 않고 템플릿 및 매개 변수 값에 사용 하 여 tootest [테스트 AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="7bf28-156">오류가 감지 되 면 hello 명령 응답 하지 않고 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="7bf28-157">오류가 검색 되 면 hello 명령은 오류 메시지를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="7bf28-158">예를 들어 toopass hello 저장소 계정 SKU에 대 한 잘못 된 값을 시도 하면 다음 오류가 hello 반환:</span><span class="sxs-lookup"><span data-stu-id="7bf28-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="7bf28-159">서식 파일에 구문 오류가 있으면 hello 명령은 hello 서식 파일을 분석할 수 없습니다 것을 나타내는 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="7bf28-160">hello 메시지 hello 줄 번호 및 구문 분석 오류 hello의 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="7bf28-161">toouse 전체 모드를 사용 하 여 hello `Mode` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="7bf28-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="7bf28-162">샘플 템플릿</span><span class="sxs-lookup"><span data-stu-id="7bf28-162">Sample template</span></span>

<span data-ttu-id="7bf28-163">hello 다음 서식 파일에 사용 됩니다이 항목의 hello 예제.</span><span class="sxs-lookup"><span data-stu-id="7bf28-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="7bf28-164">복사한 후 storage.json이라는 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="7bf28-165">toounderstand 어떻게 toocreate이 서식이 파일 참조 [첫 번째 Azure 리소스 관리자 서식 파일 만들기](resource-manager-create-first-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="7bf28-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7bf28-166">Next steps</span></span>
* <span data-ttu-id="7bf28-167">hello이이 문서의 예제에서는 기본 구독에서 리소스 tooa 리소스 그룹을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="7bf28-168">다른 구독을 toouse 참조 [여러 Azure 구독을 관리](/powershell/azure/manage-subscriptions-azureps)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="7bf28-169">템플릿을 배포하는 전체 샘플 스크립트는 [Resource Manager 템플릿 배포 스크립트](resource-manager-samples-powershell-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bf28-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="7bf28-170">템플릿에 toodefine 매개 변수를 확인 하려면 어떻게 toounderstand [hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="7bf28-171">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bf28-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="7bf28-172">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7bf28-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="7bf28-173">기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7bf28-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

