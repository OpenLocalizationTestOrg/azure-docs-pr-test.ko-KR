---
title: "Azure Automation Runbook에 Azure Resource Manager 템플릿 배포 | Microsoft Docs"
description: "Runbook에서 Azure Storage에 저장된 Azure Resource Manager 템플릿을 배포하는 방법"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: powershell,  runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 07/09/2017
ms.author: eslesar
ms.openlocfilehash: e511eee2f9eac3969b15ad3d45558dc7034f330a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a><span data-ttu-id="ffdd4-104">Azure Automation PowerShell Runbook에 Azure Resource Manager 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="ffdd4-104">Deploy an Azure Resource Manager template in an Azure Automation PowerShell runbook</span></span>

<span data-ttu-id="ffdd4-105">[Azure Resource Management 템플릿](../azure-resource-manager/resource-manager-create-first-template.md)을 사용하여 Azure 리소스를 배포하는 [Azure Automation PowerShell Runbook](automation-first-runbook-textual-powershell.md)을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-105">You can write an [Azure Automation PowerShell runbook](automation-first-runbook-textual-powershell.md) that deploys an Azure resource by using an [Azure Resource Management template](../azure-resource-manager/resource-manager-create-first-template.md).</span></span>

<span data-ttu-id="ffdd4-106">이렇게 하면 Azure 리소스 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-106">By doing this, you can automate deployment of Azure resources.</span></span> <span data-ttu-id="ffdd4-107">Azure Storage와 같은 안전한 중앙 위치에서 Resource Manager 템플릿을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-107">You can maintain your Resource Manager templates in a central,secure location such as Azure Storage.</span></span>

<span data-ttu-id="ffdd4-108">이 항목에서는 [Azure Storage](../storage/common/storage-introduction.md)에 저장된 Resource Manager 템플릿을 사용하여 새 Azure Storage 계정을 배포하는 PowerShell Runbook을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-108">In this topic, we create a PowerShell runbook that uses an Resource Manager template stored in [Azure Storage](../storage/common/storage-introduction.md) to deploy a new Azure Storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffdd4-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ffdd4-109">Prerequisites</span></span>

<span data-ttu-id="ffdd4-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="ffdd4-111">동작합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-111">Azure subscription.</span></span> <span data-ttu-id="ffdd4-112">계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-112">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="ffdd4-113">[자동화 계정](automation-sec-configure-azure-runas-account.md) .</span><span class="sxs-lookup"><span data-stu-id="ffdd4-113">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="ffdd4-114">이 계정은 가상 컴퓨터를 시작하고 중지할 수 있는 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-114">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="ffdd4-115">[Azure Storage 계정](../storage/common/storage-create-storage-account.md) - Resource Manager 템플릿을 저장하는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-115">[Azure Storage account](../storage/common/storage-create-storage-account.md) in which to store the Resource Manager template</span></span>
* <span data-ttu-id="ffdd4-116">로컬 컴퓨터에 설치된 Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-116">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="ffdd4-117">Azure PowerShell을 얻는 방법에 대한 자세한 내용은 [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0)(Azure Powershell 설치 및 구성)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-117">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-resource-manager-template"></a><span data-ttu-id="ffdd4-118">리소스 관리자 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="ffdd4-118">Create the Resource Manager template</span></span>

<span data-ttu-id="ffdd4-119">이 예제에서는 새 Azure Storage 계정을 배포하는 Resource Manager 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-119">For this example, we use an Resource Manager template that deploys a new Azure Storage account.</span></span>

<span data-ttu-id="ffdd4-120">텍스트 편집기에서 다음 텍스트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-120">In a text editor, copy the following text:</span></span>

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

<span data-ttu-id="ffdd4-121">파일을 `TemplateTest.json`(으)로 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-121">Save the file locally as `TemplateTest.json`.</span></span>

## <a name="save-the-resource-manager-template-in-azure-storage"></a><span data-ttu-id="ffdd4-122">Azure Storage에 Resource Manager 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="ffdd4-122">Save the Resource Manager template in Azure Storage</span></span>

<span data-ttu-id="ffdd4-123">이제 PowerShell을 사용하여 Azure Storage 파일 공유를 만들고 `TemplateTest.json` 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-123">Now we use PowerShell to create an Azure Storage file share and upload the `TemplateTest.json` file.</span></span>
<span data-ttu-id="ffdd4-124">Azure Portal에서 파일 공유를 만들고 파일을 업로드하는 방법에 대한 지침은 [Windows에서 Azure File Storage 시작](../storage/files/storage-dotnet-how-to-use-files.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-124">For instructions on how to create a file share and upload a file in the Azure portal, see [Get started with Azure File storage on Windows](../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="ffdd4-125">로컬 컴퓨터에서 PowerShell을 시작하고, 다음 명령을 실행하여 파일 공유를 만들고 Resource Manager 템플릿을 해당 파일 공유에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-125">Launch PowerShell on your local machine, and run the following commands to create a file share and upload the Resource Manager template to that file share.</span></span>

```powershell
# Login to Azure
Login-AzureRmAccount

# Get the access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using the first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add the TemplateTest.json file to the new file share
# "TemplatePath" is the path where you saved the TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-the-powershell-runbook-script"></a><span data-ttu-id="ffdd4-126">PowerShell Runbook 스크립트 만들기</span><span class="sxs-lookup"><span data-stu-id="ffdd4-126">Create the PowerShell runbook script</span></span>

<span data-ttu-id="ffdd4-127">이제 Azure Storage에서 `TemplateTest.json` 파일을 가져오고 템플릿을 배포하여 새 Azure Storage 계정을 만드는 PowerShell 스크립트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-127">Now we create a PowerShell script that gets the `TemplateTest.json` file from Azure Storage and deploys the template to create a new Azure Storage account.</span></span>

<span data-ttu-id="ffdd4-128">텍스트 편집기에서 다음 텍스트를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-128">In a text editor, paste the following text:</span></span>

```powershell
param (
    [Parameter(Mandatory=$true)]
    [string]
    $ResourceGroupName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountName,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageAccountKey,

    [Parameter(Mandatory=$true)]
    [string]
    $StorageFileName
)



# Authenticate to Azure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set the parameter values for the Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy the storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

<span data-ttu-id="ffdd4-129">파일을 `DeployTemplate.ps1`(으)로 로컬에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-129">Save the file locally as `DeployTemplate.ps1`.</span></span>

## <a name="import-and-publish-the-runbook-into-your-azure-automation-account"></a><span data-ttu-id="ffdd4-130">Azure Automation 계정으로 Runbook 가져오기 및 게시</span><span class="sxs-lookup"><span data-stu-id="ffdd4-130">Import and publish the runbook into your Azure Automation account</span></span>

<span data-ttu-id="ffdd4-131">이제 PowerShell을 사용하여 Runbook을 Azure Automation 계정으로 가져온 다음 이 Runbook을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-131">Now we use PowerShell to import the runbook into your Azure Automation account, and then publish the runbook.</span></span>
<span data-ttu-id="ffdd4-132">Azure Portal에서 Runbook을 가져오고 게시하는 방법에 대한 자세한 내용은 [Azure Automation에서 Runbook 만들기 또는 가져오기](automation-creating-importing-runbook.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-132">For information about how to import and publish a runbook in the Azure portal, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md).</span></span>

<span data-ttu-id="ffdd4-133">`DeployTemplate.ps1`을 PowerShell Runbook으로 Automation 계정에 가져오려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-133">To import `DeployTemplate.ps1` into your Automation account as a PowerShell runbook, run the following PowerShell commands:</span></span>

```powershell
# MyPath is the path where you saved DeployTemplate.ps1
# MyResourceGroup is the name of the Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is the name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish the runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-the-runbook"></a><span data-ttu-id="ffdd4-134">Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-134">Start the runbook</span></span>

<span data-ttu-id="ffdd4-135">이제 [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet을 호출하여 Runbook을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-135">Now we start the runbook by calling the [Start-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.</span></span>

<span data-ttu-id="ffdd4-136">Azure Portal에서 Runbook을 시작하는 방법에 대한 자세한 내용은 [Azure Automation에서 Runbook 시작](automation-starting-a-runbook.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-136">For information about how to start a runbook in the Azure portal, see [Starting a runbook in Azure Automation](automation-starting-a-runbook.md).</span></span>

<span data-ttu-id="ffdd4-137">PowerShell 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-137">Run the following commands in the PowerShell console:</span></span>

```powershell
# Set up the parameters for the runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for the Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start the runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

<span data-ttu-id="ffdd4-138">Runbook이 실행되고 `$job.Status`를 실행하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-138">The runbook runs, and you can check its status by running `$job.Status`.</span></span>

<span data-ttu-id="ffdd4-139">Runbook은 Resource Manager 템플릿을 가져와서 새 Azure Storage 계정을 배포하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-139">The runbook gets the Resource Manager template and uses it to deploy a new Azure Storage account.</span></span>
<span data-ttu-id="ffdd4-140">다음 명령을 실행하여 새 저장소 계정을 만들었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-140">You can see that the new storage account was created by running the following command:</span></span>
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a><span data-ttu-id="ffdd4-141">요약</span><span class="sxs-lookup"><span data-stu-id="ffdd4-141">Summary</span></span>

<span data-ttu-id="ffdd4-142">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-142">That's it!</span></span> <span data-ttu-id="ffdd4-143">이제 Azure Automation, Azure Storage 및 Resource Manager 템플릿을 사용하여 모든 Azure 리소스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-143">Now you can use Azure Automation and Azure Storage, and Resource Manager templates to deploy all your Azure resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffdd4-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffdd4-144">Next steps</span></span>

* <span data-ttu-id="ffdd4-145">Resource Manager 템플릿에 대한 자세한 내용은 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-145">To learn more about Resource Manager templates, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="ffdd4-146">Azure Storage를 시작하려면 [Azure Storage 소개](../storage/common/storage-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-146">To get started with Azure Storage, see [Introduction to Azure Storage](../storage/common/storage-introduction.md).</span></span>
* <span data-ttu-id="ffdd4-147">다른 유용한 Azure Automation Runbook을 찾으려면 [Azure Automation용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-147">To find other useful Azure Automation runbooks, see [Runbook and module galleries for Azure Automation](automation-runbook-gallery.md).</span></span>
* <span data-ttu-id="ffdd4-148">다른 유용한 Resource Manager 템플릿을 찾으려면 [Azure 퀵 스타트 템플릿](https://azure.microsoft.com/resources/templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffdd4-148">To find other useful Resource Manager templates, see [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/)</span></span>

