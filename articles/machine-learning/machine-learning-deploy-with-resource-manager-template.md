---
title: "Azure Resource Manager를 사용하여 Machine Learning 작업 영역 배포 | Microsoft Docs"
description: "Azure Resource Manager 템플릿을 사용하여 Azure 기계 학습에 대한 작업 영역을 배포하는 방법"
services: machine-learning
documentationcenter: 
author: ahgyger
manager: haining
editor: garye
ms.assetid: 4955ac4d-ff99-4908-aa27-69b6bfcc8e85
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/15/2017
ms.author: ahgyger
ms.openlocfilehash: 9e37780428b0867da63987ec4f7f843a8abeb907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="d22fb-103">Azure Resource Manager를 사용하여 기계 학습 작업 영역 배포</span><span class="sxs-lookup"><span data-stu-id="d22fb-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="d22fb-104">소개</span><span class="sxs-lookup"><span data-stu-id="d22fb-104">Introduction</span></span>
<span data-ttu-id="d22fb-105">Azure Resource Manager 배포 템플릿을 사용하면 유효성 검사와 상호 연결된 구성 요소를 배포하고 메커니즘을 다시 시도하는 확장성 있는 방법을 제공하여 시간을 절약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way to deploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="d22fb-106">Azure 기계 학습 작업 영역을 설정하려면 예를 들어 먼저 Azure 저장소 계정을 구성한 다음 작업 영역을 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-106">To set up Azure Machine Learning Workspaces, for example, you need to first configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="d22fb-107">수백 개의 작업 영역에 대해 이 작업을 수동으로 수행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="d22fb-108">쉬운 대안은 Azure Resource Manager 템플릿을 사용하여 Azure 기계 학습 작업 영역 및 모든 종속성을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-108">An easier alternative is to use an Azure Resource Manager template to deploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="d22fb-109">이 문서는 이 과정을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="d22fb-110">Azure Resource Manager에 대한 개요는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d22fb-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="d22fb-111">단계별: 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="d22fb-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="d22fb-112">Azure 리소스 그룹을 만든 다음 리소스 관리자 템플릿을 사용하여 새 Azure 저장소 계정 및 새 Azure 기계 학습 작업 영역을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="d22fb-113">배포가 완료되면 생성된 작업 영역에 대한 중요한 정보를 인쇄합니다(기본 키, workspaceID 및 작업 영역에 대한 URL).</span><span class="sxs-lookup"><span data-stu-id="d22fb-113">Once the deployment is complete, we will print out important information about the workspaces that were created (the primary key, the workspaceID, and the URL to the workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="d22fb-114">Azure Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="d22fb-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="d22fb-115">기계 학습 작업 영역은 연결된 데이터 집합을 저장하려면 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-115">A Machine Learning Workspace requires an Azure storage account to store the dataset linked to it.</span></span>
<span data-ttu-id="d22fb-116">다음 템플릿은 리소스 그룹의 이름을 사용하여 저장소 계정 이름 및 작업 영역 이름을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-116">The following template uses the name of the resource group to generate the storage account name and the workspace name.</span></span>  <span data-ttu-id="d22fb-117">또한 작업 영역을 만들 때 속성으로 저장소 계정 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-117">It also uses the storage account name as a property when creating the workspace.</span></span>

```
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "variables": {
        "namePrefix": "[resourceGroup().name]",
        "location": "[resourceGroup().location]",
        "mlVersion": "2016-04-01",
        "stgVersion": "2015-06-15",
        "storageAccountName": "[concat(variables('namePrefix'),'stg')]",
        "mlWorkspaceName": "[concat(variables('namePrefix'),'mlwk')]",
        "mlResourceId": "[resourceId('Microsoft.MachineLearning/workspaces', variables('mlWorkspaceName'))]",
        "stgResourceId": "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
        "storageAccountType": "Standard_LRS"
    },
    "resources": [
        {
            "apiVersion": "[variables('stgVersion')]",
            "name": "[variables('storageAccountName')]",
            "type": "Microsoft.Storage/storageAccounts",
            "location": "[variables('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "apiVersion": "[variables('mlVersion')]",
            "type": "Microsoft.MachineLearning/workspaces",
            "name": "[variables('mlWorkspaceName')]",
            "location": "[variables('location')]",
            "dependsOn": ["[variables('stgResourceId')]"],
            "properties": {
                "UserStorageAccountId": "[variables('stgResourceId')]"
            }
        }
    ],
    "outputs": {
        "mlWorkspaceObject": {"type": "object", "value": "[reference(variables('mlResourceId'), variables('mlVersion'))]"},
        "mlWorkspaceToken": {"type": "string", "value": "[listWorkspaceKeys(variables('mlResourceId'), variables('mlVersion')).primaryToken]"},
        "mlWorkspaceWorkspaceID": {"type": "string", "value": "[reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId]"},
        "mlWorkspaceWorkspaceLink": {"type": "string", "value": "[concat('https://studio.azureml.net/Home/ViewWorkspace/', reference(variables('mlResourceId'), variables('mlVersion')).WorkspaceId)]"}
    }
}

```
<span data-ttu-id="d22fb-118">c:\temp\ 아래에 mlworkspace.json 파일로 이 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-the-resource-group-based-on-the-template"></a><span data-ttu-id="d22fb-119">템플릿을 기반으로 리소스 그룹 배포</span><span class="sxs-lookup"><span data-stu-id="d22fb-119">Deploy the resource group, based on the template</span></span>
* <span data-ttu-id="d22fb-120">PowerShell 열기</span><span class="sxs-lookup"><span data-stu-id="d22fb-120">Open PowerShell</span></span>
* <span data-ttu-id="d22fb-121">Azure Resource Manager 및 Azure 서비스 관리에 대한 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="d22fb-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install the Azure Resource Manager modules from the PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install the Azure Service Management modules from the PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="d22fb-122">이러한 단계는 나머지 단계를 완료하는 데 필요한 모듈을 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-122">These steps download and install the modules necessary to complete the remaining steps.</span></span> <span data-ttu-id="d22fb-123">PowerShell 명령을 실행하는 환경에서 한 번만 수행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-123">This only needs to be done once in the environment where you are executing the PowerShell commands.</span></span>   

* <span data-ttu-id="d22fb-124">Azure에 대한 인증</span><span class="sxs-lookup"><span data-stu-id="d22fb-124">Authenticate to Azure</span></span>  

```
# Authenticate (enter your credentials in the pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="d22fb-125">이 단계는 각 세션에 대해 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-125">This step needs to be repeated for each session.</span></span> <span data-ttu-id="d22fb-126">인증되면 구독 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure 계정][1]

<span data-ttu-id="d22fb-128">이제 Azure에 대한 액세스가 있으므로 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-128">Now that we have access to Azure, we can create the resource group.</span></span>

* <span data-ttu-id="d22fb-129">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="d22fb-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="d22fb-130">리소스 그룹이 올바르게 프로비전되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-130">Verify that the resource group is correctly provisioned.</span></span> <span data-ttu-id="d22fb-131">**ProvisioningState** 는 "Succeeded"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="d22fb-132">리소스 그룹 이름은 저장소 계정 이름을 생성하는 템플릿에 의해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-132">The resource group name is used by the template to generate the storage account name.</span></span> <span data-ttu-id="d22fb-133">저장소 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-133">The storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![리소스 그룹][2]

* <span data-ttu-id="d22fb-135">리소스 그룹 배포를 사용하여 새 기계 학습 작업 영역을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-135">Using the resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is the location of the JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="d22fb-136">배포가 완료되면 배포한 작업 영역의 속성에 액세스하는 것은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-136">Once the deployment is completed, it is straightforward to access properties of the workspace you deployed.</span></span> <span data-ttu-id="d22fb-137">예를 들어 기본 키 토큰에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-137">For example, you can access the Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="d22fb-138">기존 작업 영역의 토큰을 검색하는 또 다른 방법은 Invoke-AzureRmResourceAction 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-138">Another way to retrieve tokens of existing workspace is to use the Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="d22fb-139">예를 들어 모든 작업 영역의 기본 및 보조 토큰을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-139">For example, you can list the primary and secondary tokens of all workspaces.</span></span>

```  
# List the primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="d22fb-140">작업 영역이 프로비전되면 [Azure 기계 학습에 대한 PowerShell 모듈](http://aka.ms/amlps)을 사용하여 많은 Azure 기계 학습 스튜디오 작업을 자동화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-140">After the workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using the [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d22fb-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d22fb-141">Next Steps</span></span>
* <span data-ttu-id="d22fb-142">[Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="d22fb-143">[Azure 빠른 시작 템플릿 리포지토리](https://github.com/Azure/azure-quickstart-templates)를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-143">Have a look at the [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="d22fb-144">[Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)에 대한 이 동영상을 시청합니다.</span><span class="sxs-lookup"><span data-stu-id="d22fb-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
