---
title: "PowerShell 스크립트 샘플-aaaAzure 템플릿을 배포 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 배포하는 샘플 스크립트"
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
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a>Azure Resource Manager 템플릿 배포 - PowerShell 스크립트

이 스크립트는 구독에서 리소스 관리자 템플릿 tooa 리소스 그룹을 배포합니다.

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>샘플 스크립트

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a>배포 정리 

실행된 hello 다음 tooremove hello 리소스 그룹 및 모든 리소스를 명령입니다.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate hello 배포한 후에 hello를 사용 합니다. Hello 테이블의 각 항목 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 |
|---|---|
| [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider) | 해당 리소스 종류에는 배포 된 tooyour 구독 될 수 있도록 리소스 공급자를 등록 합니다.  |
| [Get-AzureRmResourceGroup](/powershell/module/azurerm.resources/get-azurermresourcegroup) | 리소스 그룹을 가져옵니다.  |
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | Azure 배포 tooa 리소스 그룹을 추가합니다.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 리소스 그룹 및 포함된 모든 리소스를 제거합니다. |



## <a name="next-steps"></a>다음 단계
* 소개 toodeploying 서식 파일에 대 한 참조 [리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](resource-group-template-deploy.md)합니다.
* SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.
* 서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

