---
title: "aaaDeploy 리소스 tooAzure | Microsoft Docs"
description: "Azure PowerShell 또는 Azure CLI toodeploy 리소스 tooAzure를 사용 합니다. hello 리소스는 리소스 관리자 서식 파일에 정의 됩니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="03f06-104">리소스 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="03f06-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="03f06-105">이 항목에서는 방법을 toodeploy 리소스 tooyour Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="03f06-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="03f06-106">Azure PowerShell 또는 Azure CLI toodeploy 솔루션에 대 한 hello 인프라를 정의 하는 리소스 관리자 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="03f06-107">소개 tooconcepts 리소스 관리자의를 참조 하십시오. [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="03f06-108">배포 단계</span><span class="sxs-lookup"><span data-stu-id="03f06-108">Steps for deployment</span></span>

<span data-ttu-id="03f06-109">이 항목에서는 hello를 배포 하는 [예제 저장소 템플릿](#example-storage-template) 이 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="03f06-110">다른 서식 파일을 사용할 수 있지만 hello 매개 변수를 전달 하면이 항목에 표시 된 항목 보다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="03f06-111">서식 파일을 만든 후 서식 파일을 배포 하기 위한 일반 단계 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="03f06-112">Tooyour 계정에 로그인</span><span class="sxs-lookup"><span data-stu-id="03f06-112">Log in tooyour account</span></span>
2. <span data-ttu-id="03f06-113">Hello 구독 toouse (여러 구독이 있는 toouse 이름이 아닌 hello 기본 구독 하려는 경우에 필요)를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="03f06-114">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="03f06-114">Create a resource group</span></span>
4. <span data-ttu-id="03f06-115">Hello 템플릿을 배포합니다</span><span class="sxs-lookup"><span data-stu-id="03f06-115">Deploy hello template</span></span>
5. <span data-ttu-id="03f06-116">배포 상태 확인</span><span class="sxs-lookup"><span data-stu-id="03f06-116">Check your deployment status</span></span>

<span data-ttu-id="03f06-117">hello 다음 섹션에서는 보여 어떻게 tooperform 된 단계와 [PowerShell](#powershell) 또는 [Azure CLI](#azure-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="03f06-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="03f06-118">PowerShell</span></span>

1. <span data-ttu-id="03f06-119">Azure PowerShell tooinstall 참조 [Azure PowerShell cmdlet과 함께 시작](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="03f06-120">tooquickly 배포 시작 하기, hello 다음 cmdlet을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="03f06-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="03f06-121">hello `Set-AzureRmContext` cmdlet은 기본 구독 이외의 toouse 구독 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="03f06-122">toosee 모든 구독 및 Id를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="03f06-123">hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="03f06-124">배포가 완료되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="03f06-125">리소스 그룹 및 저장소 계정이 되었던 toosee tooyour 구독을 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="03f06-126">템플릿을 배포할 때 템플릿 매개 변수를 PowerShell 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="03f06-127">hello 앞의 예제 포함 되지 않았습니다 템플릿 매개 변수를 hello hello 서식 파일의 기본값을 사용 하므로.</span><span class="sxs-lookup"><span data-stu-id="03f06-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="03f06-128">toodeploy 다른 저장소 계정을 한 hello 저장소 이름 접두사와 SKU hello 저장소 계정 사용에 대 한 매개 변수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="03f06-129">이제 리소스 그룹에 두 개의 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="03f06-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="03f06-130">Azure CLI</span></span>

1. <span data-ttu-id="03f06-131">Azure CLI tooinstall 참조 [Azure CLI 2.0 설치](/cli/azure/install-az-cli2)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="03f06-132">tooquickly 배포 시작 하기, hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="03f06-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="03f06-133">hello `az account set` 명령을 기본 구독 이외의 toouse 구독 하려는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="03f06-134">toosee 모든 구독 및 Id를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="03f06-135">hello 배포는 몇 분 toocomplete를 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="03f06-136">배포가 완료되면 다음과 비슷한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="03f06-137">리소스 그룹 및 저장소 계정이 되었던 toosee tooyour 구독을 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="03f06-138">템플릿을 배포할 때 템플릿 매개 변수를 PowerShell 매개 변수로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="03f06-139">hello 앞의 예제 포함 되지 않았습니다 템플릿 매개 변수를 hello hello 서식 파일의 기본값을 사용 하므로.</span><span class="sxs-lookup"><span data-stu-id="03f06-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="03f06-140">toodeploy 다른 저장소 계정을 한 hello 저장소 이름 접두사와 SKU hello 저장소 계정 사용에 대 한 매개 변수 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="03f06-141">이제 리소스 그룹에 두 개의 저장소 계정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="03f06-142">예제 저장소 템플릿</span><span class="sxs-lookup"><span data-stu-id="03f06-142">Example storage template</span></span>

<span data-ttu-id="03f06-143">다음 예제에서는 서식 파일 toodeploy 저장소 계정 tooyour 구독은 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="03f06-144">다음 단계</span><span class="sxs-lookup"><span data-stu-id="03f06-144">Next steps</span></span>

* <span data-ttu-id="03f06-145">PowerShell toodeploy 템플릿을 사용 하는 방법에 대 한 자세한 내용은 참조 [리소스 관리자 템플릿 및 Azure PowerShell을 사용 하 여 리소스를 배포](/azure/azure-resource-manager/resource-group-template-deploy)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="03f06-146">Azure CLI toodeploy 템플릿을 사용 하는 방법에 대 한 자세한 내용은 참조 [리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](/azure/azure-resource-manager/resource-group-template-deploy-cli)합니다.</span><span class="sxs-lookup"><span data-stu-id="03f06-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



