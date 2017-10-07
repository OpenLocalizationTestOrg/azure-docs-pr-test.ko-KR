---
title: "Azure CLI aaaExport 리소스 관리자 템플릿을 | Microsoft Docs"
description: "Azure 리소스 관리자 및 Azure CLI tooexport 리소스 그룹에서 서식 파일을 사용 합니다."
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
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="65875-103">Azure CLI를 사용하여 Azure Resource Manager 템플릿 내보내기</span><span class="sxs-lookup"><span data-stu-id="65875-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="65875-104">리소스 관리자 구독에 기존 리소스에서 리소스 관리자 템플릿을 tooexport가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="65875-105">필요에 따라 솔루션의 hello 템플릿 구문 또는 tooautomate hello 재배포에 대 한 해당 생성 된 템플릿 toolearn를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="65875-106">중요 한 toonote 된다고 두 가지 방법으로 tooexport 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="65875-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="65875-107">배포에 사용한 hello 실제 서식 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="65875-108">hello 내보낸된 템플릿에 hello 원본 서식 파일에 표시 된 그대로 hello 매개 변수 및 변수를 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65875-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="65875-109">이 방법은 tooretrieve 서식 파일을 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="65875-110">Hello hello 리소스 그룹의 현재 상태를 나타내는 서식 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="65875-111">hello에서 내보낸된 템플릿 배포에 사용 된 파일 따르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="65875-112">대신, 템플릿에 hello 리소스 그룹의 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="65875-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="65875-113">hello에서 내보낸된 템플릿에 하드 코드 된 값이 많은 및 일반적으로 정의할 때와 하지 못할 수의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="65875-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="65875-114">이 방법은 hello 리소스 그룹을 수정한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="65875-115">이제 템플릿으로 toocapture hello 리소스 그룹이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="65875-116">이 항목에서는 두 가지 방법을 모두 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="65875-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="65875-117">솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="65875-117">Deploy a solution</span></span>

<span data-ttu-id="65875-118">템플릿을 내보내는 대 한 두 tooillustrate 가까워지면, 솔루션 tooyour 구독을 배포 하 여 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="65875-119">원하는 tooexport 구독에 리소스 그룹이 이미 있는 경우 않아도 toodeploy이이 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="65875-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="65875-120">그러나이 문서의 나머지 부분에서는 hello toohello 서식 파일을이 솔루션에 대 한 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="65875-121">hello 예제 스크립트는 저장소 계정을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="65875-122">배포 기록에서 템플릿 저장</span><span class="sxs-lookup"><span data-stu-id="65875-122">Save template from deployment history</span></span>

<span data-ttu-id="65875-123">Hello를 사용 하 여 배포 기록에서 서식 파일을 검색할 수 있습니다 [az 그룹 배포 내보내기](/cli/azure/group/deployment#export) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65875-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="65875-124">다음 예에서는 이전에 배포 하는 저장 hello 템플릿을 hello:</span><span class="sxs-lookup"><span data-stu-id="65875-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="65875-125">Hello 서식 파일을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-125">It returns hello template.</span></span> <span data-ttu-id="65875-126">JSON, hello 복사한 파일로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="65875-127">Hello 정확한 템플릿 배포에 사용 되는 점에 주목 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="65875-128">hello 매개 변수 및 변수 GitHub에서 hello 템플릿을 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="65875-129">이 템플릿을 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="65875-130">리소스 그룹을 템플릿으로 내보내기</span><span class="sxs-lookup"><span data-stu-id="65875-130">Export resource group as template</span></span>

<span data-ttu-id="65875-131">Hello 배포 기록에서 서식 파일을 검색 하지 않고 hello를 사용 하 여 hello 리소스 그룹의 현재 상태를 나타내는 서식 파일을 검색할 수 있습니다 [az 그룹 내보내기](/cli/azure/group#export) 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="65875-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="65875-132">많은 변경 내용을 tooyour 리소스 그룹을 변경한 있고 기존 템플릿이 hello 변경 내용을 모두를 나타내는 경우에이 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="65875-133">Hello 서식 파일을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-133">It returns hello template.</span></span> <span data-ttu-id="65875-134">JSON, hello 복사한 파일로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="65875-135">GitHub의 hello 템플릿보다 다른 인지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="65875-136">매개 변수는 다르고 변수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="65875-136">It has different parameters and no variables.</span></span> <span data-ttu-id="65875-137">hello 저장소 SKU와 위치는 하드 코드 된 toovalues 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="65875-138">hello 다음 예제에서는 hello 내보낸된 템플릿 되었지만 서식 파일에는 약간 다른 매개 변수 이름:</span><span class="sxs-lookup"><span data-stu-id="65875-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="65875-139">이 서식 파일을 다시 배포할 수 있습니다. 그러나 hello 저장소 계정의 고유한 이름을 추측 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="65875-140">매개 변수의 이름을 hello는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="65875-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="65875-141">내보낸 템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="65875-141">Customize exported template</span></span>

<span data-ttu-id="65875-142">이 템플릿 toomake 수정할 수 있습니다 것 보다 쉽게 toouse 보다 유연 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="65875-143">자세한 위치 변경 hello 위치 속성 toouse tooallow hello 같은 hello 리소스 그룹 위치:</span><span class="sxs-lookup"><span data-stu-id="65875-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="65875-144">tooavoid tooguess hello 저장소 계정 이름에 대 한 remove hello 매개 변수, 저장소 계정에 대 한 unique 이름을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="65875-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="65875-145">저장소 이름 접미사에 대한 매개 변수와 저장소 SKU를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="65875-146">Hello uniqueString 함수로 hello 저장소 계정 이름을 생성 하는 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="65875-147">Hello 저장소 계정 toohello 변수의 hello 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="65875-148">Hello SKU toohello 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="65875-149">템플릿은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="65875-149">Your template now looks like:</span></span>

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

<span data-ttu-id="65875-150">Hello 수정 된 서식 파일을 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65875-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="65875-151">Next steps</span></span>
* <span data-ttu-id="65875-152">Hello 포털 tooexport 서식 파일을 사용 하는 방법에 대 한 정보를 참조 하십시오. [기존 리소스에서 Azure 리소스 관리자 템플릿 내보내기](resource-manager-export-template.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="65875-153">서식 파일에서 toodefine 매개 변수를 참조 [템플릿을 작성](resource-group-authoring-templates.md#parameters)합니다.</span><span class="sxs-lookup"><span data-stu-id="65875-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="65875-154">일반적인 배포 오류를 해결하는 방법은 [Azure Resource Manager를 사용한 일반적인 Azure 배포 오류 해결](resource-manager-common-deployment-errors.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="65875-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>