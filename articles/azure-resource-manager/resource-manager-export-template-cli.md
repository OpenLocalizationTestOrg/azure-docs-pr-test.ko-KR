---
title: "Azure CLI를 사용하여 Resource Manager 템플릿 내보내기 | Microsoft Docs"
description: "Azure Resource Manager 및 Azure CLI를 사용하여 리소스 그룹에서 템플릿을 내보냅니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="2edf2-103">Azure CLI를 사용하여 Azure Resource Manager 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="2edf2-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="2edf2-104">Resource Manager를 사용하면 구독의 기존 리소스에서 Resource Manager 템플릿을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="2edf2-105">생성된 템플릿을 사용하여 템플릿 구문에 대해 알아보거나 필요에 따라 솔루션 재배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="2edf2-106">템플릿을 내보내려면 다음과 같은 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="2edf2-107">배포에 사용된 실제 템플릿을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="2edf2-108">내보낸 템플릿은 원본 템플릿에 나타난 대로 모든 매개 변수 및 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="2edf2-109">이 방법은 템플릿을 검색해야 할 때 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="2edf2-110">리소스 그룹의 현재 상태를 나타내는 템플릿을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="2edf2-111">내보낸 템플릿은 배포에 사용된 템플릿에 기초하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="2edf2-112">대신 리소스 그룹의 스냅숏인 템플릿을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="2edf2-113">내보낸 템플릿에는 하드 코드된 값이 많으며 일반적으로 정의된 경우와 같이 매개 변수가 많이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="2edf2-114">이 방법은 리소스 그룹을 수정한 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="2edf2-115">이제 리소스 그룹을 템플릿으로 캡처해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="2edf2-116">이 항목에서는 두 가지 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="2edf2-117">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="2edf2-117">Deploy a solution</span></span>

<span data-ttu-id="2edf2-118">템플릿을 내보내기 위한 두 가지 방법을 확인하려면 먼저 구독에 솔루션을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="2edf2-119">내보내려는 구독에 리소스 그룹이 이미 있는 경우 이 솔루션을 배포할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="2edf2-120">그러나 이 문서의 나머지 부분에서 이 솔루션에 대한 템플릿이 언급됩니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="2edf2-121">예제 스크립트는 저장소 계정을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="2edf2-122">배포 기록에서 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="2edf2-122">Save template from deployment history</span></span>

<span data-ttu-id="2edf2-123">[az group deployment export](/cli/azure/group/deployment#export) 명령을 사용하여 배포 기록에서 템플릿을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="2edf2-124">다음 예제에서는 이전에 배포하는 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="2edf2-125">템플릿을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-125">It returns the template.</span></span> <span data-ttu-id="2edf2-126">JSON을 복사하고 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="2edf2-127">배포에 사용한 정확한 템플릿인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="2edf2-128">매개 변수 및 변수는 GitHub의 템플릿과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="2edf2-129">이 템플릿을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="2edf2-130">리소스 그룹을 템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="2edf2-130">Export resource group as template</span></span>

<span data-ttu-id="2edf2-131">배포 기록에서 템플릿을 검색하지 않고 [az group export](/cli/azure/group#export) 명령을 사용하여 리소스 그룹의 현재 상태를 나타내는 템플릿을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="2edf2-132">이 명령은 리소스 그룹을 많이 변경했으며 모든 변경 내용을 나타내는 기존 템플릿이 없는 경우에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="2edf2-133">템플릿을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-133">It returns the template.</span></span> <span data-ttu-id="2edf2-134">JSON을 복사하고 파일로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="2edf2-135">GitHub의 템플릿과는 다른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="2edf2-136">매개 변수는 다르고 변수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-136">It has different parameters and no variables.</span></span> <span data-ttu-id="2edf2-137">저장소 SKU 및 위치는 값으로 하드 코드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="2edf2-138">다음 예제에서는 내보낸 템플릿을 보여 주지만 템플릿은 약간 다른 매개 변수 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="2edf2-139">이 템플릿을 다시 배포할 수 있지만 저장소 계정에 대한 고유한 이름을 추측해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="2edf2-140">매개 변수의 이름은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="2edf2-141">내보낸 템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2edf2-141">Customize exported template</span></span>

<span data-ttu-id="2edf2-142">이 템플릿을 수정하여 좀 더 사용하기 쉽고 유연하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="2edf2-143">더 많은 위치를 허용하려면 리소스 그룹으로 동일한 위치를 사용하도록 위치 속성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="2edf2-144">저장소 계정에 대한 고유한 이름을 추측하지 않으려면 저장소 계정 이름에 대한 매개 변수를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="2edf2-145">저장소 이름 접미사에 대한 매개 변수와 저장소 SKU를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="2edf2-146">uniqueString 함수를 사용하여 저장소 계정 이름을 생성하는 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="2edf2-147">저장소 계정의 이름을 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="2edf2-148">SKU를 매개 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="2edf2-149">템플릿은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-149">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="2edf2-150">수정된 템플릿을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2edf2-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2edf2-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2edf2-151">Next steps</span></span>
* <span data-ttu-id="2edf2-152">포털을 사용하여 템플릿을 내보내는 방법에 대한 자세한 내용은 [기존 리소스에서 Azure Resource Manager 템플릿 내보내기](resource-manager-export-template.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2edf2-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="2edf2-153">템플릿에서 매개 변수를 정의하려면 [템플릿 작성](resource-group-authoring-templates.md#parameters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2edf2-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2edf2-154">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2edf2-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>