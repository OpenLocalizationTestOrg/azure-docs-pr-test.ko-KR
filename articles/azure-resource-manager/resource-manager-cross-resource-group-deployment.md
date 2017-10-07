---
title: "Azure 리소스 toomultiple 리소스 그룹 aaaDeploy | Microsoft Docs"
description: "배포 하는 동안 Azure 리소스가 두 개 이상 tootarget 그룹화 하는 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="18668-103">Azure 리소스 toomore 보다 한 리소스 그룹 배포</span><span class="sxs-lookup"><span data-stu-id="18668-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="18668-104">일반적으로 모든 hello 리소스 템플릿 tooa 단일 리소스 그룹에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="18668-105">그러나 함께 toodeploy 리소스 집합을 원하는 하지만 다른 리소스 그룹에 배치 하는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18668-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="18668-106">예를 들어 toodeploy hello 백업 가상 컴퓨터가 Azure Site Recovery tooa 별도 리소스 그룹 및 위치에 대 한 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18668-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="18668-107">리소스 관리자 hello 부모 서식 파일에 사용 되는 hello 리소스 그룹 보다 toouse 중첩 템플릿 tootarget 여러 리소스 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18668-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="18668-108">hello 리소스 그룹에는 hello 응용 프로그램에 대 한 hello 수명 주기 컨테이너 및 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="18668-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="18668-109">Hello 템플릿 외부에서 hello 리소스 그룹을 만들고 배포 중 리소스 그룹 tootarget hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="18668-110">소개 tooresource 그룹에 대 한 참조 [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="18668-111">예제 템플릿</span><span class="sxs-lookup"><span data-stu-id="18668-111">Example template</span></span>

<span data-ttu-id="18668-112">tootarget 다른 리소스를 배포 하는 동안 중첩 또는 연결 된 서식 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="18668-113">hello `Microsoft.Resources/deployments` 리소스 종류 제공는 `resourceGroup` 매개 변수를 사용 toospecify hello에 대 한 다른 리소스 그룹 배포를 중첩 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="18668-114">Hello 배포를 실행 하기 전에 모든 hello 리소스 그룹이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="18668-115">hello 다음 예제에서는 배포 배포 하는 동안 지정 된 hello 리소스 그룹에 각각 하나씩 두 개의 저장소 계정-리소스 그룹에 하나 `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="18668-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="18668-116">설정한 경우 `resourceGroup` 존재 하지 않는 리소스 그룹의 이름을 toohello hello 배포에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="18668-117">에 대 한 값을 제공 하지 않으면 `resourceGroup`, hello 부모 리소스 그룹 리소스 관리자를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="18668-118">Hello 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="18668-118">Deploy hello template</span></span>

<span data-ttu-id="18668-119">toodeploy hello 예제 서식 파일을 hello 포털, Azure PowerShell 또는 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18668-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="18668-120">Azure PowerShell 또는 Azure CLI의 경우 2017년 5월 이후의 릴리스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="18668-121">hello 예제 이라는 파일로 hello 서식 파일을 로컬로 저장 한 가정 **crossrgdeployment.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="18668-122">PowerShell의 경우:</span><span class="sxs-lookup"><span data-stu-id="18668-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="18668-123">Azure CLI의 경우:</span><span class="sxs-lookup"><span data-stu-id="18668-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="18668-124">배포가 완료되면 두 개의 리소스 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="18668-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="18668-125">각 리소스 그룹에는 저장소 계정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18668-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="18668-126">resourceGroup() 함수 사용</span><span class="sxs-lookup"><span data-stu-id="18668-126">Use resourceGroup() function</span></span>

<span data-ttu-id="18668-127">에 대 한 교차 리소스 그룹 배포 hello [resouceGroup() 함수](resource-group-template-functions-resource.md#resourcegroup) hello 중첩 된 서식 파일을 지정 하는 방법에 따라 다르게을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="18668-128">다른 서식 파일에서 한 템플릿을 포함 한 경우 hello 중첩 된 템플릿에서 resouceGroup() toohello 부모 리소스 그룹을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="18668-129">포함 된 템플릿 형식에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="18668-130">Tooa 별도 서식 파일을 연결 하면 연결 된 템플릿의 hello resouceGroup() toohello 중첩된 리소스 그룹을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="18668-131">연결 된 템플릿 형식에 따라 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="18668-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18668-132">Next steps</span></span>

* <span data-ttu-id="18668-133">템플릿에 toodefine 매개 변수를 확인 하려면 어떻게 toounderstand [hello 구조 및 Azure 리소스 관리자 템플릿 구문을 이해](resource-group-authoring-templates.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="18668-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="18668-134">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18668-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="18668-135">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="18668-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
