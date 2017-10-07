---
title: "Azure 자동화 runbook에는 Azure 리소스 관리자 템플릿 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy Azure 리소스 관리자 템플릿을 저장 된 Azure 저장소에는 runbook에서"
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
ms.openlocfilehash: f489a8e8635a48f5a6a2f1a88e1c803f56f01832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-resource-manager-template-in-an-azure-automation-powershell-runbook"></a>Azure Automation PowerShell Runbook에 Azure Resource Manager 템플릿 배포

[Azure Resource Management 템플릿](../azure-resource-manager/resource-manager-create-first-template.md)을 사용하여 Azure 리소스를 배포하는 [Azure Automation PowerShell Runbook](automation-first-runbook-textual-powershell.md)을 작성할 수 있습니다.

이렇게 하면 Azure 리소스 배포를 자동화할 수 있습니다. Azure Storage와 같은 안전한 중앙 위치에서 Resource Manager 템플릿을 유지 관리할 수 있습니다.

이 항목에 저장 하는 리소스 관리자 템플릿을 사용 하는 PowerShell runbook 만듭니다 [Azure 저장소](../storage/common/storage-introduction.md) toodeploy 새 Azure 저장소 계정입니다.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 hello 필요:

* 동작합니다. 계정이 아직 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 <a href="/pricing/free-account/" target="_blank">[무료 계정을 등록](https://azure.microsoft.com/free/)할 수 있습니다.
* [자동화 계정](automation-sec-configure-azure-runas-account.md) toohold runbook hello 및 tooAzure 리소스를 인증 합니다.  이 계정은 권한 toostart 있고 hello 가상 컴퓨터를 중지 해야 합니다.
* [Azure 저장소 계정](../storage/common/storage-create-storage-account.md) 는 toostore hello 리소스 관리자 템플릿에서
* 로컬 컴퓨터에 설치된 Azure Powershell. 참조 [설치 Azure Powershell을 구성 하 고](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) 방법에 대 한 정보에 대 한 Azure PowerShell tooget 합니다.

## <a name="create-hello-resource-manager-template"></a>Hello 리소스 관리자 템플릿 만들기

이 예제에서는 새 Azure Storage 계정을 배포하는 Resource Manager 템플릿을 사용합니다.

텍스트 편집기에서 텍스트 다음 hello를 복사 합니다.

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

으로 hello 파일을 로컬로 저장 `TemplateTest.json`합니다.

## <a name="save-hello-resource-manager-template-in-azure-storage"></a>Hello 리소스 관리자 템플릿을 Azure 저장소에 저장

이제 PowerShell toocreate Azure 저장소 파일 공유를 사용 하 고 hello 업로드 `TemplateTest.json` 파일입니다.
Toocreate 파일을 공유 하 고 hello Azure 포털에서에서 파일을 업로드 하는 방법에 지침은 [Windows에서 Azure 파일 저장소 시작](../storage/files/storage-dotnet-how-to-use-files.md)합니다.

로컬 컴퓨터의 PowerShell을 시작 하 고 hello 명령을 toocreate 파일 공유에 다음을 실행 하 고 hello 리소스 관리자 템플릿 toothat 파일 공유를 업로드 합니다.

```powershell
# Login tooAzure
Login-AzureRmAccount

# Get hello access key for your storage account
$key = Get-AzureRmStorageAccountKey -ResourceGroupName 'MyAzureAccount' -Name 'MyStorageAccount'

# Create an Azure Storage context using hello first access key
$context = New-AzureStorageContext -StorageAccountName 'MyStorageAccount' -StorageAccountKey $key[0].value

# Create a file share named 'resource-templates' in your Azure Storage account
$fileShare = New-AzureStorageShare -Name 'resource-templates' -Context $context

# Add hello TemplateTest.json file toohello new file share
# "TemplatePath" is hello path where you saved hello TemplateTest.json file
$templateFile = 'C:\TemplatePath'
Set-AzureStorageFileContent -ShareName $fileShare.Name -Context $context -Source $templateFile
```

## <a name="create-hello-powershell-runbook-script"></a>Hello PowerShell runbook 스크립트 만들기

Hello를 가져오는 PowerShell 스크립트를 생성 하는 이제 `TemplateTest.json` Azure 저장소에서 파일을 hello 템플릿 toocreate 새 Azure 저장소 계정에 배포 합니다.

텍스트 편집기에서 텍스트 다음 hello를 붙여 넣습니다.

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



# Authenticate tooAzure if running from Azure Automation
$ServicePrincipalConnection = Get-AutomationConnection -Name "AzureRunAsConnection"
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $ServicePrincipalConnection.TenantId `
    -ApplicationId $ServicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $ServicePrincipalConnection.CertificateThumbprint | Write-Verbose

#Set hello parameter values for hello Resource Manager template
$Parameters = @{
    "storageAccountType"="Standard_LRS"
    }

# Create a new context
$Context = New-AzureStorageContext -StorageAccountKey $StorageAccountKey

Get-AzureStorageFileContent -ShareName 'resource-templates' -Context $Context -path 'TemplateTest.json' -Destination 'C:\Temp'

$TemplateFile = Join-Path -Path 'C:\Temp' -ChildPath $StorageFileName

# Deploy hello storage account
New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFile -TemplateParameterObject $Parameters 
``` 

으로 hello 파일을 로컬로 저장 `DeployTemplate.ps1`합니다.

## <a name="import-and-publish-hello-runbook-into-your-azure-automation-account"></a>가져오기 및 Azure 자동화 계정으로 hello runbook을 게시 합니다.

이제 Azure 자동화 계정에 PowerShell tooimport hello runbook을 사용 하 고 hello runbook을 게시 하십시오.
방법에 대 한 내용은 tooimport hello Azure 포털에서에서 runbook을 게시 하 고, 참조 [만들기 또는 Azure 자동화에서 runbook을 가져와](automation-creating-importing-runbook.md)합니다.

tooimport `DeployTemplate.ps1` PowerShell runbook과 자동화 계정에 hello 다음 PowerShell 명령을 실행 합니다.

```powershell
# MyPath is hello path where you saved DeployTemplate.ps1
# MyResourceGroup is hello name of hello Azure ResourceGroup that contains your Azure Automation account
# MyAutomationAccount is hello name of your Automation account
$importParams = @{
    Path = 'C:\MyPath\DeployTemplate.ps1'
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Type = 'PowerShell'
}
Import-AzureRmAutomationRunbook @

# Publish hello runbook
$publishParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
}
Publish-AzureRmAutomationRunbook @publishParams
```

## <a name="start-hello-runbook"></a>Hello runbook 시작

Hello runbook 호출 hello을 시작 하겠습니다. 이제 [시작 AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/start-azurermautomationrunbook?view=azurermps-4.1.0) cmdlet.

Toostart hello Azure 포털에서에서 runbook을 확인 하려면 어떻게 해야 하는 방법에 대 한 내용은 [Azure 자동화에서 runbook 시작](automation-starting-a-runbook.md)합니다.

Hello hello PowerShell 콘솔 명령에에서 따라를 실행 합니다.

```powershell
# Set up hello parameters for hello runbook
$runbookParams = @{
    ResourceGroupName = 'MyResourceGroup'
    StorageAccountName = 'MyStorageAccount'
    StorageAccountKey = $key[0].Value # We got this key earlier
    StorageFileName = 'TemplateTest.json' 
}

# Set up parameters for hello Start-AzureRmAutomationRunbook cmdlet
$startParams = @{
    ResourceGroupName = 'MyResourceGroup'
    AutomationAccountName = 'MyAutomationAccount'
    Name = 'DeployTemplate'
    Parameters = $runbookParams
}

# Start hello runbook
$job = Start-AzureRmAutomationRunbook @startParams
```

hello runbook이 실행 되 고 실행 하 여 해당 상태를 확인할 수 있습니다 `$job.Status`합니다.

hello runbook hello 리소스 관리자 템플릿을 가져오고 toodeploy 새 Azure 저장소 계정을 사용 합니다.
새 저장소 계정을 hello hello 다음 명령을 실행 하 여 만들어졌는지 확인할 수 있습니다.
```powershell
Get-AzureRmStorageAccount
```

## <a name="summary"></a>요약

이것으로 끝입니다. 이제 사용할 수 있습니다 Azure 자동화 및 Azure 저장소 및 리소스 관리자 템플릿 toodeploy 모든 Azure 리소스입니다.

## <a name="next-steps"></a>다음 단계

* 리소스 관리자 템플릿에 대해 자세히 toolearn 참조 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)
* Azure 저장소 시작 tooget 참조 [소개 tooAzure 저장소](../storage/common/storage-introduction.md)합니다.
* toofind 다른 유용한 Azure 자동화 runbook 참조 [Azure 자동화 용 Runbook 및 모듈 갤러리](automation-runbook-gallery.md)합니다.
* toofind 다른 유용한 리소스 관리자 템플릿을 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/resources/templates/)

