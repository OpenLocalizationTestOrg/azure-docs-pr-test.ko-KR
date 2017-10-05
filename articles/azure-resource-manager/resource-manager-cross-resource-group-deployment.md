---
title: "여러 리소스 그룹에 Azure 리소스 배포 | Microsoft Docs"
description: "배포 중에 둘 이상의 Azure 리소스 그룹을 대상으로 지정하는 방법을 보여 줍니다."
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
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="8d402-103">둘 이상의 리소스 그룹에 Azure 리소스 배포</span><span class="sxs-lookup"><span data-stu-id="8d402-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="8d402-104">일반적으로 단일 리소스 그룹에 템플릿의 모든 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="8d402-105">그러나 일단의 리소스를 함께 배포하고 다른 리소스 그룹에 배치하려는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="8d402-106">예를 들어 Azure Site Recovery의 백업 가상 컴퓨터를 별도의 리소스 그룹과 위치에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="8d402-107">Resource Manager를 사용하면 중첩된 템플릿을 사용하여 부모 템플릿에 사용된 리소스 그룹과 다른 리소스 그룹을 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="8d402-108">리소스 그룹은 응용 프로그램 및 해당 리소스 컬렉션에 대한 수명 주기 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="8d402-109">템플릿 외부에서 리소스 그룹을 만들고 배포 중에 대상으로 지정할 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="8d402-110">리소스 그룹에 대한 소개는 [Azure Resource Manager 개요](resource-group-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d402-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="8d402-111">예제 템플릿</span><span class="sxs-lookup"><span data-stu-id="8d402-111">Example template</span></span>

<span data-ttu-id="8d402-112">다른 리소스를 대상으로 지정하려면 배포 중에 중첩되거나 연결된 템플릿을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="8d402-113">`Microsoft.Resources/deployments` 리소스 형식은 중첩된 배포에 다른 리소스 그룹을 지정할 수 있는 `resourceGroup` 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="8d402-114">모든 리소스 그룹은 배포를 실행하기 전에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="8d402-115">다음 예제에서는 배포 중에 지정한 리소스 그룹 및 `crossResourceGroupDeployment`이라는 리소스 그룹에 각각 하나씩 두 개의 저장소 계정을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="8d402-116">`resourceGroup`을 존재하지 않는 리소스 그룹의 이름으로 설정하면 배포에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="8d402-117">`resourceGroup` 값을 제공하지 않으면 Resource Manager에서 부모 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="8d402-118">템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="8d402-118">Deploy the template</span></span>

<span data-ttu-id="8d402-119">예제 템플릿을 배포하려면 포털, Azure PowerShell 또는 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="8d402-120">Azure PowerShell 또는 Azure CLI의 경우 2017년 5월 이후의 릴리스를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="8d402-121">예제에서는 템플릿을 **crossrgdeployment.json**이라는 이름의 파일로 로컬로 저장한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="8d402-122">PowerShell의 경우:</span><span class="sxs-lookup"><span data-stu-id="8d402-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="8d402-123">Azure CLI의 경우:</span><span class="sxs-lookup"><span data-stu-id="8d402-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="8d402-124">배포가 완료되면 두 개의 리소스 그룹이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="8d402-125">각 리소스 그룹에는 저장소 계정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="8d402-126">resourceGroup() 함수 사용</span><span class="sxs-lookup"><span data-stu-id="8d402-126">Use resourceGroup() function</span></span>

<span data-ttu-id="8d402-127">교차 리소스 그룹 배포를 위해 [resouceGroup() 함수](resource-group-template-functions-resource.md#resourcegroup)는 중첩 템플릿 지정 방식에 따라 다르게 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="8d402-128">하나의 템플릿을 다른 템플릿 내에 포함하는 경우 중첩 템플릿의 resouceGroup()가 부모 리소스 그룹으로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="8d402-129">포함된 템플릿은 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="8d402-130">별도의 템플릿에 연결하는 경우 연결된 템플릿의 resouceGroup()가 중첩된 리소스 그룹으로 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="8d402-131">연결된 템플릿은 다음 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d402-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8d402-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8d402-132">Next steps</span></span>

* <span data-ttu-id="8d402-133">템플릿에서 매개 변수를 정의하는 방법을 이해하려면 [Azure Resource Manager 템플릿의 구조 및 구문 이해](resource-group-authoring-templates.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d402-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8d402-134">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d402-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="8d402-135">SAS 토큰이 필요한 템플릿을 배포하는 데 관한 내용은 [SAS 토큰으로 개인 템플릿 배포](resource-manager-powershell-sas-token.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d402-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
