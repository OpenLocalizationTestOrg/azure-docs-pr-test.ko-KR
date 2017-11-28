---
title: "서식 파일에 리소스 위치 aaaAzure | Microsoft Docs"
description: "표시 방법을 tooset Azure Resource Manager 템플릿의 리소스에 대 한 위치"
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
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a><span data-ttu-id="71e77-103">Azure Resource Manager 템플릿에서 리소스 위치 설정</span><span class="sxs-lookup"><span data-stu-id="71e77-103">Set resource location in Azure Resource Manager templates</span></span>
<span data-ttu-id="71e77-104">템플릿을 배포할 때는 각 리소스의 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-104">When deploying a template, you must provide a location for each resource.</span></span> <span data-ttu-id="71e77-105">이 항목에서는 각 리소스에 대 한 사용 가능한 tooyour 구독 않은 toodetermine hello 위치 입력 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-105">This topic shows how toodetermine hello locations that are available tooyour subscription for each resource type.</span></span>

## <a name="determine-supported-locations"></a><span data-ttu-id="71e77-106">지원되는 위치 확인</span><span class="sxs-lookup"><span data-stu-id="71e77-106">Determine supported locations</span></span>

<span data-ttu-id="71e77-107">각 리소스 유형에 대해 지원되는 위치의 전체 목록은 [지역별 사용 가능한 제품](https://azure.microsoft.com/regions/services/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="71e77-107">For a complete list of supported locations for each resource type, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="71e77-108">그러나 구독 액세스 tooall hello 위치 해당 목록에 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-108">However, your subscription might not have access tooall hello locations in that list.</span></span> <span data-ttu-id="71e77-109">사용자 지정된 위치를 사용할 수 있는 tooyour 구독 목록을 toosee Azure PowerShell 또는 Azure CLI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-109">toosee a customized list of locations that are available tooyour subscription, use Azure PowerShell or Azure CLI.</span></span> 

<span data-ttu-id="71e77-110">hello 다음 예제에서는 PowerShell tooget hello 위치 hello에 대 한 `Microsoft.Web\sites` 리소스 종류:</span><span class="sxs-lookup"><span data-stu-id="71e77-110">hello following example uses PowerShell tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="71e77-111">hello 다음 예제에서는 Azure CLI 2.0 tooget hello 위치 hello에 대 한 `Microsoft.Web\sites` 리소스 종류:</span><span class="sxs-lookup"><span data-stu-id="71e77-111">hello following example uses Azure CLI 2.0 tooget hello locations for hello `Microsoft.Web\sites` resource type:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a><span data-ttu-id="71e77-112">템플릿에서 위치 설정</span><span class="sxs-lookup"><span data-stu-id="71e77-112">Set location in template</span></span>

<span data-ttu-id="71e77-113">리소스에 대 한 지원 hello 위치를 결정 했으면 tooset 해당 위치에에서 필요한 서식 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-113">After determining hello supported locations for your resources, you need tooset that location in your template.</span></span> <span data-ttu-id="71e77-114">이 값은 toocreate hello 리소스 종류를 지 원하는 위치에 리소스를 그룹화 하는 가장 쉬운 방법은 tooset hello와 각 위치를 너무 설정`[resourceGroup().location]`합니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-114">hello easiest way tooset this value is toocreate a resource group in a location that supports hello resource types, and set each location too`[resourceGroup().location]`.</span></span> <span data-ttu-id="71e77-115">서로 다른 위치에 템플릿 tooresource 그룹 hello를 다시 배포할 수 있으며 hello 템플릿 또는 매개 변수 값을 변경 하지 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-115">You can redeploy hello template tooresource groups in different locations, and not change any values in hello template or parameters.</span></span> 

<span data-ttu-id="71e77-116">hello 다음 예제에서는 배포 된 toohello 저장소 계정을 같은 hello 리소스 그룹 위치:</span><span class="sxs-lookup"><span data-stu-id="71e77-116">hello following example shows a storage account that is deployed toohello same location as hello resource group:</span></span>

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

<span data-ttu-id="71e77-117">서식 파일에서 toohardcode hello 위치 해야 할 경우 hello 이름 hello 지원 영역 중 하나를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-117">If you need toohardcode hello location in your template, provide hello name of one of hello supported regions.</span></span> <span data-ttu-id="71e77-118">다음 예제는 hello 항상 저장소 계정을 tooNorth 중앙 미국 배포를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-118">hello following example shows a storage account that is always deployed tooNorth Central US:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="71e77-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="71e77-119">Next steps</span></span>
* <span data-ttu-id="71e77-120">방법에 대 한 권장 사항에 대 한 toocreate 템플릿 참조 [Azure 리소스 관리자 템플릿 만들기에 대 한 유용한](resource-manager-template-best-practices.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="71e77-120">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

