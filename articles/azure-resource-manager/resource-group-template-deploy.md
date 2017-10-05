---
title: "PowerShell 및 템플릿으로 리소스 배포 | Microsoft Docs"
description: "Azure Resource Manager와 Azure PowerShell을 사용하여 Azure에 리소스를 배포합니다. 리소스는 Resource Manager 템플릿에 정의됩니다."
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
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="22ac1-104">리소스 관리자 템플릿과 Azure PowerShell로 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="22ac1-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="22ac1-105">이 항목은 리소스 관리자 템플릿으로 Azure PowerShell을 사용하여 Azure에 리소스를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="22ac1-106">Azure 솔루션 배포 및 관리와 관련된 개념에 익숙하지 않은 경우 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="22ac1-107">배포하는 Resource Manager 템플릿은 컴퓨터의 로컬 파일 또는 GitHub와 같은 저장소에 있는 외부 파일일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="22ac1-108">이 문서에서 배포하는 템플릿은 [샘플 템플릿](#sample-template) 섹션 또는 [GitHub의 저장소 계정 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json)으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="22ac1-109">로컬 컴퓨터에서 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="22ac1-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="22ac1-110">Azure에 리소스를 배포할 때 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="22ac1-111">Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="22ac1-112">배포된 리소스에 대한 컨테이너 역할을 하는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="22ac1-113">리소스 그룹의 이름은 영숫자, 마침표, 밑줄, 하이픈 및 괄호만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="22ac1-114">최대 90자까지 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-114">It can be up to 90 characters.</span></span> <span data-ttu-id="22ac1-115">마침표로 끝날 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="22ac1-116">만들려는 리소스를 정의하는 템플릿을 리소스 그룹에 배포</span><span class="sxs-lookup"><span data-stu-id="22ac1-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="22ac1-117">템플릿에는 템플릿 배포를 사용자 지정할 수 있도록 하는 매개 변수가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="22ac1-118">예를 들어 특정 환경(예: 개발, 테스트 및 프로덕션)에 맞게 조정되는 값을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="22ac1-119">샘플 템플릿은 저장소 계정 SKU에 대한 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="22ac1-120">다음 예제에서는 리소스 그룹을 만들고 로컬 컴퓨터에서 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="22ac1-121">배포가 완료될 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="22ac1-122">완료되면 결과가 포함된 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="22ac1-123">외부 원본에서 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="22ac1-123">Deploy a template from an external source</span></span>

<span data-ttu-id="22ac1-124">로컬 컴퓨터에 Resource Manager 템플릿을 저장하는 대신, 외부 위치에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="22ac1-125">원본 제어 리포지토리(예: GitHub)에 템플릿을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="22ac1-126">또는 조직에서 공유 액세스에 대한 Azure Storage 계정에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="22ac1-127">외부 템플릿을 배포하려면 **TemplateUri** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="22ac1-128">예제의 URI를 사용하여 GitHub에서 샘플 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="22ac1-129">앞의 예제에서는 템플릿에 중요한 데이터가 포함되어 있지 않으므로 대부분의 시나리오에 적합한 이 템플릿에 대해 공개적으로 액세스할 수 있는 URI가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="22ac1-130">중요한 데이터(예: 관리자 암호)를 지정해야 하는 경우 해당 값을 안전한 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="22ac1-131">그러나 템플릿에 공개적으로 액세스할 수 있도록 하지 않으려면 개인 저장소 컨테이너에 저장하여 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="22ac1-132">SAS(공유 액세스 서명) 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="22ac1-133">매개 변수 파일</span><span class="sxs-lookup"><span data-stu-id="22ac1-133">Parameter files</span></span>

<span data-ttu-id="22ac1-134">매개 변수를 스크립트에 인라인 값으로 전달하는 것보다는, 매개 변수 값이 포함된 JSON 파일을 사용하는 것이 더 쉬울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="22ac1-135">매개 변수 파일은 다음과 같은 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="22ac1-136">매개 변수 섹션에는 템플릿에 정의된 매개 변수(storageAccountType)와 일치하는 매개 변수 이름이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="22ac1-137">매개 변수 파일에는 매개 변수의 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="22ac1-138">이 값은 배포 동안 템플릿에 자동으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="22ac1-139">다양한 배포 시나리오를 위해 여러 매개 변수 파일을 만든 후 적절한 매개 변수 파일을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="22ac1-140">앞의 예제를 복사하고 `storage.parameters.json`이라는 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="22ac1-141">로컬 매개 변수 파일을 전달하려면 **TemplateParameterFile** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="22ac1-142">외부 매개 변수 파일을 전달하려면 **TemplateParameterUri** 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="22ac1-143">동일한 배포 작업에서 인라인 매개 변수 및 로컬 매개 변수 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="22ac1-144">예를 들어 로컬 매개 변수 파일에서 일부 값을 지정하고 배포하는 동안 인라인으로 다른 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="22ac1-145">로컬 매개 변수 파일 및 인라인에서 매개 변수에 대한 값을 제공하는 경우 인라인 값이 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="22ac1-146">하지만 외부 매개 변수 파일을 사용하면 인라인 또는 로컬 파일에서 다른 값을 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="22ac1-147">**TemplateParameterUri** 매개 변수에서 매개 변수 파일을 지정하는 경우 모든 인라인 매개 변수는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="22ac1-148">외부 파일에서 모든 매개 변수 값을 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="22ac1-149">템플릿이 매개 변수 파일에 포함할 수 없는 중요한 값을 포함하는 경우 해당 값을 키 자격 증명 모음에 추가하고 동적으로 모든 매개 변수 값을 인라인으로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="22ac1-150">템플릿에 PowerShell 명령의 매개 변수 중 하나와 이름이 같은 매개 변수가 포함되어 있으면 PowerShell에서 접미사가 **FromTemplate**인 템플릿에서 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="22ac1-151">예를 들어 템플릿의 **ResourceGroupName**이라는 매개 변수는 [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet의 **ResourceGroupName** 매개 변수와 충돌합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="22ac1-152">**ResourceGroupNameFromTemplate**에 대한 값을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="22ac1-153">일반적으로 배포 작업에 사용되는 매개 변수와 동일한 이름을 가진 매개 변수를 명명하지 않음으로써 이러한 혼동이 발생하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="22ac1-154">템플릿 배포 테스트</span><span class="sxs-lookup"><span data-stu-id="22ac1-154">Test a template deployment</span></span>

<span data-ttu-id="22ac1-155">리소스를 실제로 배포하지 않고 템플릿과 매개 변수 값을 테스트하려면 [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="22ac1-156">오류가 감지되지 않으면 명령은 응답 없이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="22ac1-157">오류가 감지되면 명령은 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="22ac1-158">예를 들어 저장소 계정 SKU에 대해 잘못된 값을 제공하려고 하면 다음 오류가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="22ac1-159">템플릿에 구문 오류가 있으면 명령은 템플릿을 구문 분석할 수 없다는 오류를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="22ac1-160">메시지는 줄 번호 및 구문 분석 오류의 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="22ac1-161">완료 모드를 사용하려면 `Mode` 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="22ac1-162">샘플 템플릿</span><span class="sxs-lookup"><span data-stu-id="22ac1-162">Sample template</span></span>

<span data-ttu-id="22ac1-163">다음 템플릿은 이 항목의 예제에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="22ac1-164">복사한 후 storage.json이라는 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="22ac1-165">이 템플릿을 만드는 방법을 이해하려면 [첫 번째 Azure Resource Manager 템플릿 만들기](resource-manager-create-first-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="22ac1-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22ac1-166">Next steps</span></span>
* <span data-ttu-id="22ac1-167">이 문서의 예제에서는 리소스를 기본 구독의 리소스 그룹으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="22ac1-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="22ac1-168">다른 구독을 사용하려면 [여러 Azure 구독 관리](/powershell/azure/manage-subscriptions-azureps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="22ac1-169">템플릿을 배포하는 전체 샘플 스크립트는 [Resource Manager 템플릿 배포 스크립트](resource-manager-samples-powershell-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="22ac1-170">템플릿에서 매개 변수를 정의하는 방법을 이해하려면 [Azure Resource Manager 템플릿의 구조 및 구문 이해](resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="22ac1-171">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="22ac1-172">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="22ac1-173">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22ac1-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

