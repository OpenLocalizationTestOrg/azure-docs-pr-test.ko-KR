---
title: "기계 학습 작업 영역에서 Azure 리소스 관리자와 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy Azure 리소스 관리자 템플릿을 사용 하 여 Azure 기계 학습 작업 영역"
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
ms.openlocfilehash: 308959825bcbd670f6ce9b6dc381be767f172357
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-machine-learning-workspace-using-azure-resource-manager"></a><span data-ttu-id="b999b-103">Azure Resource Manager를 사용하여 기계 학습 작업 영역 배포</span><span class="sxs-lookup"><span data-stu-id="b999b-103">Deploy Machine Learning Workspace Using Azure Resource Manager</span></span>
## <a name="introduction"></a><span data-ttu-id="b999b-104">소개</span><span class="sxs-lookup"><span data-stu-id="b999b-104">Introduction</span></span>
<span data-ttu-id="b999b-105">배포 템플릿을 저장 하는 Azure 리소스 관리자를 사용 하 여 확장 가능한 방식으로 toodeploy 제공 하 여 시간 상호 연결 된 구성 요소에는 유효성 검사 및 다시 시도 메커니즘.</span><span class="sxs-lookup"><span data-stu-id="b999b-105">Using an Azure Resource Manager deployment template saves you time by giving you a scalable way toodeploy interconnected components with a validation and retry mechanism.</span></span> <span data-ttu-id="b999b-106">Azure 기계 학습 작업 영역을 tooset, 예를 들어 필요한 toofirst는 Azure 저장소 계정을 구성 하 고 다음 작업 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-106">tooset up Azure Machine Learning Workspaces, for example, you need toofirst configure an Azure storage account and then deploy your workspace.</span></span> <span data-ttu-id="b999b-107">수백 개의 작업 영역에 대해 이 작업을 수동으로 수행한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-107">Imagine doing this manually for hundreds of workspaces.</span></span> <span data-ttu-id="b999b-108">쉽게 대신 toouse Azure 리소스 관리자 템플릿 toodeploy Azure 기계 학습 작업 영역 및 모든 해당 모든 종속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-108">An easier alternative is toouse an Azure Resource Manager template toodeploy an Azure Machine Learning Workspace and all its dependencies.</span></span> <span data-ttu-id="b999b-109">이 문서는 이 과정을 단계별로 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-109">This article takes you through this process step-by-step.</span></span> <span data-ttu-id="b999b-110">Azure Resource Manager에 대한 개요는 [Azure Resource Manager 개요](../azure-resource-manager/resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b999b-110">For a great overview of Azure Resource Manager, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="step-by-step-create-a-machine-learning-workspace"></a><span data-ttu-id="b999b-111">단계별: 기계 학습 작업 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="b999b-111">Step-by-step: create a Machine Learning Workspace</span></span>
<span data-ttu-id="b999b-112">Azure 리소스 그룹을 만든 다음 리소스 관리자 템플릿을 사용하여 새 Azure 저장소 계정 및 새 Azure 기계 학습 작업 영역을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-112">We will create an Azure resource group, then deploy a new Azure storage account and a new Azure Machine Learning Workspace using a Resource Manager template.</span></span> <span data-ttu-id="b999b-113">Hello 배포 완료 되 면 (hello 기본 키, hello workspaceID 및 hello URL toohello 작업 영역) 생성 된 hello 작업 영역에 대 한 중요 한 정보를 출력 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-113">Once hello deployment is complete, we will print out important information about hello workspaces that were created (hello primary key, hello workspaceID, and hello URL toohello workspace).</span></span>

### <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="b999b-114">Azure Resource Manager 템플릿 만들기</span><span class="sxs-lookup"><span data-stu-id="b999b-114">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="b999b-115">기계 학습 작업 영역에는 Azure 저장소 계정 toostore hello 연결 된 데이터 집합 tooit이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-115">A Machine Learning Workspace requires an Azure storage account toostore hello dataset linked tooit.</span></span>
<span data-ttu-id="b999b-116">hello 다음 템플릿은 사용 hello 이름 hello 리소스 그룹 toogenerate hello 저장소 계정 이름 및 작업 영역 이름을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-116">hello following template uses hello name of hello resource group toogenerate hello storage account name and hello workspace name.</span></span>  <span data-ttu-id="b999b-117">또한 hello 작업 영역을 만들 때 속성으로 hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-117">It also uses hello storage account name as a property when creating hello workspace.</span></span>

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
<span data-ttu-id="b999b-118">c:\temp\ 아래에 mlworkspace.json 파일로 이 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-118">Save this template as mlworkspace.json file under c:\temp\.</span></span>

### <a name="deploy-hello-resource-group-based-on-hello-template"></a><span data-ttu-id="b999b-119">Hello 템플릿을 기반으로 hello 리소스 그룹 배포</span><span class="sxs-lookup"><span data-stu-id="b999b-119">Deploy hello resource group, based on hello template</span></span>
* <span data-ttu-id="b999b-120">PowerShell 열기</span><span class="sxs-lookup"><span data-stu-id="b999b-120">Open PowerShell</span></span>
* <span data-ttu-id="b999b-121">Azure Resource Manager 및 Azure 서비스 관리에 대한 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="b999b-121">Install modules for Azure Resource Manager and Azure Service Management</span></span>  

```
# Install hello Azure Resource Manager modules from hello PowerShell Gallery (press “A”)
Install-Module AzureRM -Scope CurrentUser

# Install hello Azure Service Management modules from hello PowerShell Gallery (press “A”)
Install-Module Azure -Scope CurrentUser
```

   <span data-ttu-id="b999b-122">다음이 단계를 다운로드 하 고 hello 모듈 필요한 toocomplete hello 나머지 단계를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-122">These steps download and install hello modules necessary toocomplete hello remaining steps.</span></span> <span data-ttu-id="b999b-123">이 toobe hello PowerShell 명령을 실행 하는 hello 환경에서 한 번만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-123">This only needs toobe done once in hello environment where you are executing hello PowerShell commands.</span></span>   

* <span data-ttu-id="b999b-124">TooAzure 인증</span><span class="sxs-lookup"><span data-stu-id="b999b-124">Authenticate tooAzure</span></span>  

```
# Authenticate (enter your credentials in hello pop-up window)
Add-AzureRmAccount
```
<span data-ttu-id="b999b-125">이 단계는 각 세션에 대해 반복 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-125">This step needs toobe repeated for each session.</span></span> <span data-ttu-id="b999b-126">인증되면 구독 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-126">Once authenticated, your subscription information should be displayed.</span></span>

![Azure 계정][1]

<span data-ttu-id="b999b-128">액세스 tooAzure를 만들었으므로 이제 해당 hello 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-128">Now that we have access tooAzure, we can create hello resource group.</span></span>

* <span data-ttu-id="b999b-129">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="b999b-129">Create a resource group</span></span>

```
$rg = New-AzureRmResourceGroup -Name "uniquenamerequired523" -Location "South Central US"
$rg
```

<span data-ttu-id="b999b-130">해당 hello 리소스 그룹 서 올바르게 프로 비전을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-130">Verify that hello resource group is correctly provisioned.</span></span> <span data-ttu-id="b999b-131">**ProvisioningState** 는 "Succeeded"여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-131">**ProvisioningState** should be “Succeeded.”</span></span>
<span data-ttu-id="b999b-132">hello 리소스 그룹 이름은 hello 템플릿 toogenerate hello 저장소 계정 이름으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-132">hello resource group name is used by hello template toogenerate hello storage account name.</span></span> <span data-ttu-id="b999b-133">hello 저장소 계정 이름은 길이가 3 ~ 24 자 사이 여야 하며 숫자 및 소문자만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-133">hello storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

![리소스 그룹][2]

* <span data-ttu-id="b999b-135">Hello 리소스 그룹 배포를 사용 하 여 새 기계 학습 작업 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-135">Using hello resource group deployment, deploy a new Machine Learning Workspace.</span></span>

```
# Create a Resource Group, TemplateFile is hello location of hello JSON template.
$rgd = New-AzureRmResourceGroupDeployment -Name "demo" -TemplateFile "C:\temp\mlworkspace.json" -ResourceGroupName $rg.ResourceGroupName
```

<span data-ttu-id="b999b-136">Hello 배포가 완료 되 면 배포 된 hello 영역의 간단 tooaccess 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-136">Once hello deployment is completed, it is straightforward tooaccess properties of hello workspace you deployed.</span></span> <span data-ttu-id="b999b-137">예를 들어 기본 키 토큰 hello를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-137">For example, you can access hello Primary Key Token.</span></span>

```
# Access Azure ML Workspace Token after its deployment.
$rgd.Outputs.mlWorkspaceToken.Value
```

<span data-ttu-id="b999b-138">기존 작업 영역의 또 다른 방법은 tooretrieve 토큰이 toouse hello Invoke AzureRmResourceAction 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-138">Another way tooretrieve tokens of existing workspace is toouse hello Invoke-AzureRmResourceAction command.</span></span> <span data-ttu-id="b999b-139">예를 들어 hello 기본 및 보조 토큰의 모든 작업 영역을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-139">For example, you can list hello primary and secondary tokens of all workspaces.</span></span>

```  
# List hello primary and secondary tokens of all workspaces
Get-AzureRmResource |? { $_.ResourceType -Like "*MachineLearning/workspaces*"} |% { Invoke-AzureRmResourceAction -ResourceId $_.ResourceId -Action listworkspacekeys -Force}  
```
<span data-ttu-id="b999b-140">Hello를 사용 하 여 여러 Azure 기계 학습 스튜디오 작업을 자동화할 수도 있습니다 hello 작업 영역을 프로 비전 되 면 [Azure 기계 학습에 대 한 PowerShell 모듈](http://aka.ms/amlps)합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-140">After hello workspace is provisioned, you can also automate many Azure Machine Learning Studio tasks using hello [PowerShell Module for Azure Machine Learning](http://aka.ms/amlps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b999b-141">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b999b-141">Next Steps</span></span>
* <span data-ttu-id="b999b-142">[Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-142">Learn more about [authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="b999b-143">Hello 살펴보고 [Azure 빠른 시작 템플릿 리포지토리](https://github.com/Azure/azure-quickstart-templates)합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-143">Have a look at hello [Azure Quickstart Templates Repository](https://github.com/Azure/azure-quickstart-templates).</span></span> 
* <span data-ttu-id="b999b-144">[Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39)에 대한 이 동영상을 시청합니다.</span><span class="sxs-lookup"><span data-stu-id="b999b-144">Watch this video about [Azure Resource Manager](https://channel9.msdn.com/Events/Ignite/2015/C9-39).</span></span> 

<!--Image references-->
[1]: ../media/machine-learning-deploy-with-resource-manager-template/azuresubscription.png
[2]: ../media/machine-learning-deploy-with-resource-manager-template/resourcegroupprovisioning.png


<!--Link references-->
