---
title: "Azure PowerShell 스크립트 샘플 - 템플릿 배포 | Microsoft Docs"
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
ms.openlocfilehash: b7a7dda1da653d084e02e6724d2f0cb5aa76807a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="3b914-103">Azure Resource Manager 템플릿 배포 - PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="3b914-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="3b914-104">이 스크립트에서는 Resource Manager 템플릿을 구독의 리소스 그룹에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-104">This script deploys a Resource Manager template to a resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3b914-105">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="3b914-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template to Azure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #The subscription id where the template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #The resource group where the template will be deployed. Can be the name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try to create a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #The deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path to the template file. Defaults to template.json.
    [string]$TemplateFilePath = "template.json",  

    #Path to the parameters file. Defaults to parameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login to Azure and select subscription
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

# Start the deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="3b914-106">배포 정리</span><span class="sxs-lookup"><span data-stu-id="3b914-106">Clean up deployment</span></span> 

<span data-ttu-id="3b914-107">다음 명령을 실행하여 리소스 그룹과 모든 관련 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-107">Run the following command to remove the resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3b914-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="3b914-108">Script explanation</span></span>

<span data-ttu-id="3b914-109">이 스크립트는 다음 명령을 사용하여 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="3b914-110">테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3b914-111">명령</span><span class="sxs-lookup"><span data-stu-id="3b914-111">Command</span></span> | <span data-ttu-id="3b914-112">참고</span><span class="sxs-lookup"><span data-stu-id="3b914-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b914-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="3b914-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="3b914-114">리소스 유형을 구독에 배포할 수 있도록 리소스 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-114">Registers a resource provider so its resource types can be deployed to your subscription.</span></span>  |
| [<span data-ttu-id="3b914-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b914-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="3b914-116">리소스 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="3b914-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b914-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3b914-118">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3b914-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="3b914-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="3b914-120">리소스 그룹에 Azure 배포를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-120">Adds an Azure deployment to a resource group.</span></span>  |
| [<span data-ttu-id="3b914-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b914-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3b914-122">리소스 그룹 및 포함된 모든 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b914-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="3b914-123">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b914-123">Next steps</span></span>
* <span data-ttu-id="3b914-124">템플릿 배포에 대한 소개는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b914-124">For an introduction to deploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="3b914-125">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b914-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="3b914-126">템플릿에서 매개 변수를 정의하려면 [템플릿 작성](resource-group-authoring-templates.md#parameters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b914-126">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="3b914-127">엔터프라이즈에서 리소스 관리자를 사용하여 구독을 효과적으로 관리할 수 있는 방법에 대한 지침은 [Azure 엔터프라이즈 스캐폴드 - 규범적 구독 거버넌스](resource-manager-subscription-governance.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b914-127">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

