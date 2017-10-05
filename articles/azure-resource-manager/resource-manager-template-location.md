---
title: "템플릿의 Azure 리소스 위치 | Microsoft Docs"
description: "Azure Resource Manager 템플릿의 리소스에 대한 위치 설정 방법을 보여 줍니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: 73e50a593c41e841dcaf184abb895406ff5001e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="c8003-103">Azure Resource Manager 템플릿에서 리소스 위치 설정</span><span class="sxs-lookup"><span data-stu-id="c8003-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="c8003-104">템플릿을 배포할 때는 각 리소스의 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="c8003-105">이 항목에서는 각 리소스 유형에 대한 구독에서 사용할 수 있는 위치를 확인하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-105">This topic shows how to determine the locations that are available to your subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="c8003-106">지원되는 위치 확인</span><span class="sxs-lookup"><span data-stu-id="c8003-106">Determine supported locations</span></span>

<span data-ttu-id="c8003-107">각 리소스 유형에 대해 지원되는 위치의 전체 목록은 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8003-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="c8003-108">그러나 구독에 해당 목록의 모든 위치에 대한 액세스 권한이 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-108">However, your subscription might not have access to all the locations in that list.</span></span> <span data-ttu-id="c8003-109">구독에서 사용할 수 있는 위치의 사용자 지정된 목록을 보려면 Azure PowerShell 또는 Azure CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-109">To see a customized list of locations that are available to your subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="c8003-110">다음 예제에서는 PowerShell을 사용하여 `Microsoft.Web\sites` 리소스 유형에 대한 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-110">The following example uses PowerShell to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="c8003-111">다음 예제에서는 Azure CLI 2.0을 사용하여 `Microsoft.Web\sites` 리소스 유형에 대한 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-111">The following example uses Azure CLI 2.0 to get the locations for the `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="c8003-112">템플릿에서 위치 설정</span><span class="sxs-lookup"><span data-stu-id="c8003-112">Set location in template</span></span>

<span data-ttu-id="c8003-113">리소스에 대해 지원되는 위치를 확인한 후 템플릿에서 해당 위치를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-113">After determining the supported locations for your resources, you need to set that location in your template.</span></span> <span data-ttu-id="c8003-114">이 값을 설정하는 가장 쉬운 방법은 리소스 유형을 지원하는 위치에 리소스 그룹을 만들고 해당 위치를 `[resourceGroup().location]`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-114">The easiest way to set this value is to create a resource group in a location that supports the resource types, and set each location to `[resourceGroup().location]`.</span></span> <span data-ttu-id="c8003-115">여러 다른 위치의 리소스 그룹에 템플릿을 다시 배포하고 템플릿 또는 매개 변수의 값을 변경하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-115">You can redeploy the template to resource groups in different locations, and not change any values in the template or parameters.</span></span> 

<span data-ttu-id="c8003-116">다음 예제에서는 리소스 그룹과 같은 위치에 배포되는 저장소 계정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-116">The following example shows a storage account that is deployed to the same location as the resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

<span data-ttu-id="c8003-117">템플릿에서 해당 위치를 하드 코드해야 할 경우 지원되는 하위 지역 중 하나의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-117">If you need to hardcode the location in your template, provide the name of one of the supported regions.</span></span> <span data-ttu-id="c8003-118">다음 예제에서는 항상 미국 중북부에 배포되는 저장소 계정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c8003-118">The following example shows a storage account that is always deployed to North Central US:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="c8003-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8003-119">Next steps</span></span>
* <span data-ttu-id="c8003-120">템플릿 작성 방법에 대한 권장 사항은 [Azure Resource Manager 템플릿 생성 모범 사례](resource-manager-template-best-practices.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8003-120">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

