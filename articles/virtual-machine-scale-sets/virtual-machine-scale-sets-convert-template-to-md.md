---
title: "Azure Resource Manager 확장 집합 템플릿을 변환하여 관리되는 디스크 사용 | Microsoft Docs"
description: "확장 집합 템플릿을 변환하여 관리되는 디스크 확장 집합 템플릿을 사용합니다."
keywords: "가상 컴퓨터 확장 집합"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: bc8c377a-8c3f-45b8-8b2d-acc2d6d0b1e8
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/18/2017
ms.author: negat
ms.openlocfilehash: 2f5cb85703888c5056611d466f508547ee72e44b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-a-scale-set-template-to-a-managed-disk-scale-set-template"></a><span data-ttu-id="210bf-104">확장 집합 템플릿을 변환하여 관리되는 디스크 확장 집합 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="210bf-104">Convert a scale set template to a managed disk scale set template</span></span>

<span data-ttu-id="210bf-105">확장 집합을 만드는 데 관리되는 디스크를 사용하지 않고 Resource Manager 템플릿을 사용하는 고객은 관리되는 디스크를 사용하도록 수정하려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-105">Customers with a Resource Manager template for creating a scale set not using managed disk may wish to modify it to use managed disk.</span></span> <span data-ttu-id="210bf-106">이 문서에서는 샘플 Resource Manager 템플릿용 커뮤니티 중심 리포지토리 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates)에서 끌어오기 요청을 예로 사용하여 이를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-106">This article shows how to do this, using as an example a pull request from the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates), a community-driven repo for sample Resource Manager templates.</span></span> <span data-ttu-id="210bf-107">전체 끌어오기 요청은 [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998)에서 찾을 수 있으며 diff의 관련 부분은 설명과 함께 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-107">The full pull request can be seen here: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), and the relevant parts of the diff are below, along with explanations:</span></span>

## <a name="making-the-os-disks-managed"></a><span data-ttu-id="210bf-108">관리되는 OS 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="210bf-108">Making the OS disks managed</span></span>

<span data-ttu-id="210bf-109">아래 diff에서 저장소 계정 및 디스크 속성에 관련된 몇 가지 변수를 제거한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-109">In the diff below, we can see that we have removed several variables related to storage account and disk properties.</span></span> <span data-ttu-id="210bf-110">저장소 계정 유형은 더 이상 필요하지 않지만(Standard_LRS가 기본값) 원하는 경우 여전히 지정할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-110">Storage account type is no longer necessary (Standard_LRS is the default), but we could still specify it if we wished to.</span></span> <span data-ttu-id="210bf-111">Standard_LRS 및 Premium_LRS는 관리되는 디스크로만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-111">Only Standard_LRS and Premium_LRS are supported with managed disk.</span></span> <span data-ttu-id="210bf-112">새 저장소 계정 접미사, 고유 문자열 배열 및 sa 수는 저장소 계정 이름을 생성하는 기존 템플릿에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-112">New storage account suffix, unique string array, and sa count were used in the old template to generate storage account names.</span></span> <span data-ttu-id="210bf-113">관리되는 디스크는 고객을 대신하여 저장소 계정을 자동으로 만들기 때문에 이러한 변수는 새 템플릿에 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-113">These variables are no longer necessary in the new template because managed disk automatically creates storage accounts on the customer's behalf.</span></span> <span data-ttu-id="210bf-114">마찬가지로 관리되는 디스크는 기본 저장소 Blob 컨테이너 및 디스크의 이름을 자동으로 지정하므로 vhd 컨테이너 이름 및 os 디스크 이름은 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-114">Similarly, vhd container name and os disk name are no longer necessary because managed disk automatically names the underlying storage blob containers and disks.</span></span>

```diff
   "variables": {
-    "storageAccountType": "Standard_LRS",
     "namingInfix": "[toLower(substring(concat(parameters('vmssName'), uniqueString(resourceGroup().id)), 0, 9))]",
     "longNamingInfix": "[toLower(parameters('vmssName'))]",
-    "newStorageAccountSuffix": "[concat(variables('namingInfix'), 'sa')]",
-    "uniqueStringArray": [
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '0')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '1')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '2')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '3')))]",
-      "[concat(uniqueString(concat(resourceGroup().id, variables('newStorageAccountSuffix'), '4')))]"
-    ],
-    "saCount": "[length(variables('uniqueStringArray'))]",
-    "vhdContainerName": "[concat(variables('namingInfix'), 'vhd')]",
-    "osDiskName": "[concat(variables('namingInfix'), 'osdisk')]",
     "addressPrefix": "10.0.0.0/16",
     "subnetPrefix": "10.0.0.0/24",
     "virtualNetworkName": "[concat(variables('namingInfix'), 'vnet')]",
```


<span data-ttu-id="210bf-115">아래 diff에서 계산 api 버전을 확장 집합이 지원되는 관리되는 디스크에 필요한 가장 오래된 버전인 2016-04-30-미리 보기로 업데이트한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-115">In the diff below, we can see that we updated the compute api version to 2016-04-30-preview, which is the earliest required version for managed disk support with scale sets.</span></span> <span data-ttu-id="210bf-116">원하는 경우 기존 구문을 사용하여 새 api 버전에서 관리되지 않는 디스크를 여전히 사용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-116">Note that we could still use unmanaged disks in the new api version with the old syntax if desired.</span></span> <span data-ttu-id="210bf-117">즉, 계산 api 버전만을 업데이트하고 다른 내용을 변경하지 않는 경우 템플릿은 이전처럼 계속해서 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-117">In other words, if we only update the compute api version and don't change anything else, the template should continue to work as before.</span></span>

```diff
@@ -86,7 +74,7 @@
       "version": "latest"
     },
     "imageReference": "[variables('osType')]",
-    "computeApiVersion": "2016-03-30",
+    "computeApiVersion": "2016-04-30-preview",
     "networkApiVersion": "2016-03-30",
     "storageApiVersion": "2015-06-15"
   },
```

<span data-ttu-id="210bf-118">아래 diff에서 저장소 계정 리소스를 리소스 배열에서 완전히 제거하고 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-118">In the diff below, we can see that we are removing the storage account resource from the resources array completely.</span></span> <span data-ttu-id="210bf-119">관리되는 디스크는 대신해서 이를 자동으로 만들기 때문에 저장소 계정 리소스는 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-119">We no longer need them since managed disk creates them automatically on our behalf.</span></span>

```diff
@@ -113,19 +101,6 @@
       }
     },
-    {
-      "type": "Microsoft.Storage/storageAccounts",
-      "name": "[concat(variables('uniqueStringArray')[copyIndex()], variables('newStorageAccountSuffix'))]",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "[variables('storageApiVersion')]",
-      "copy": {
-        "name": "storageLoop",
-        "count": "[variables('saCount')]"
-      },
-      "properties": {
-        "accountType": "[variables('storageAccountType')]"
-      }
-    },
     {
       "type": "Microsoft.Network/publicIPAddresses",
       "name": "[variables('publicIPAddressName')]",
       "location": "[resourceGroup().location]",
```

<span data-ttu-id="210bf-120">아래 diff에서 확장 집합에서 저장소 계정을 만들고 있던 루프까지를 참조하는 절에 따라 제거하고 있는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-120">In the diff below, we can see that we are removing the depends on clause referring from the scale set to the loop that was creating storage accounts.</span></span> <span data-ttu-id="210bf-121">기존 템플릿에서 확장 집합이 만들기를 시작하기 전에 저장소 계정이 만들어졌던 것을 보장했지만 이 절은 관리되는 디스크에서 더 이상 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-121">In the old template, this was ensuring that the storage accounts were created before the scale set began creation, but this clause is no longer necessary with managed disk.</span></span> <span data-ttu-id="210bf-122">또한 vhd 컨테이너 속성 및 os 디스크 이름 속성은 관리되는 디스크에 의해 내부에서 자동으로 처리되므로 해당 속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-122">We also remove the vhd containers property, and the os disk name property as these properties are automatically handled under the hood by managed disk.</span></span> <span data-ttu-id="210bf-123">원하는 경우 프리미엄 OS 디스크를 원하면 "osDisk" 구성에 `"managedDisk": { "storageAccountType": "Premium_LRS" }`를 추가할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-123">If we wished, we could add `"managedDisk": { "storageAccountType": "Premium_LRS" }` in the "osDisk" configuration if we wanted premium OS disks.</span></span> <span data-ttu-id="210bf-124">VM sku의 대문자 또는 소문자 ‘s’를 사용하는 VM만 프리미엄 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-124">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

```diff
@@ -183,7 +158,6 @@
       "location": "[resourceGroup().location]",
       "apiVersion": "[variables('computeApiVersion')]",
       "dependsOn": [
-        "storageLoop",
         "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
         "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
       ],
@@ -200,16 +174,8 @@
         "virtualMachineProfile": {
           "storageProfile": {
             "osDisk": {
-              "vhdContainers": [
-                "[concat('https://', variables('uniqueStringArray')[0], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[1], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[2], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[3], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]",
-                "[concat('https://', variables('uniqueStringArray')[4], variables('newStorageAccountSuffix'), '.blob.core.windows.net/', variables('vhdContainerName'))]"
-              ],
-              "name": "[variables('osDiskName')]",
             },
             "imageReference": "[variables('imageReference')]"
           },

```

<span data-ttu-id="210bf-125">확장 집합 구성에는 관리되거나 관리되지 않는 디스크를 사용할 것인지에 대한 명시적 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-125">There is no explicit property in the scale set configuration for whether to use managed or unmanaged disk.</span></span> <span data-ttu-id="210bf-126">확장 집합은 저장소 프로필에 있는 속성에 따라 사용할 것을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-126">The scale set knows which to use based on the properties that are present in the storage profile.</span></span> <span data-ttu-id="210bf-127">따라서 올바른 속성이 확장 집합의 저장소 프로필에 있도록 템플릿을 수정하는 경우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-127">Thus, it is important when modifying the template to ensure that the right properties are in the storage profile of the scale set.</span></span>


## <a name="data-disks"></a><span data-ttu-id="210bf-128">데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="210bf-128">Data disks</span></span>

<span data-ttu-id="210bf-129">위의 변경 내용으로 확장 집합은 OS 디스크에 관리되는 디스크를 사용하지만 데이터 디스크의 경우는 어떻습니까?</span><span class="sxs-lookup"><span data-stu-id="210bf-129">With the changes above, the scale set uses managed disks for the OS disk, but what about data disks?</span></span> <span data-ttu-id="210bf-130">데이터 디스크를 추가하려면 "osDisk"와 같은 수준인 "storageProfile" 아래에 "dataDisks" 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-130">To add data disks, add the "dataDisks" property under "storageProfile" at the same level as "osDisk".</span></span> <span data-ttu-id="210bf-131">속성의 값은 다음 예제와 같이 개체의 JSON 목록이며 각각에는 "lun"(VM에서 데이터 디스크마다 고유해야 함), "createOption"("empty"는 현재 지원되는 유일한 옵션임) 및 "diskSizeGB"(기가바이트 단위의 디스크 크기, 0보다 크고 1024보다 작아야 함) 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-131">The value of the property is a JSON list of objects, each of which has properties "lun" (which must be unique per data disk on a VM), "createOption" ("empty" is currently the only supported option), and "diskSizeGB" (the size of the disk in gigabytes; must be greater than 0 and less than 1024) as in the following example:</span></span> 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

<span data-ttu-id="210bf-132">이 배열에 `n`개의 디스크를 지정하는 경우 확장 집합의 각 VM은 `n`개의 데이터 디스크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-132">If you specify `n` disks in this array, each VM in the scale set gets `n` data disks.</span></span> <span data-ttu-id="210bf-133">그러나 이러한 데이터 디스크는 원시 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-133">Do note, however, that these data disks are raw devices.</span></span> <span data-ttu-id="210bf-134">포맷되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-134">They are not formatted.</span></span> <span data-ttu-id="210bf-135">사용하기 전에 디스크를 연결, 파티션 및 포맷하는 고객에게 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-135">It is up to the customer to attach, paritition, and format the disks before using them.</span></span> <span data-ttu-id="210bf-136">필요에 따라 각 데이터 디스크 개체에 `"managedDisk": { "storageAccountType": "Premium_LRS" }`를 지정하여 프리미엄 데이터 디스크가 되어야 하도록 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-136">Optionally, we could also specify `"managedDisk": { "storageAccountType": "Premium_LRS" }` in each data disk object to specify that it should be a premium data disk.</span></span> <span data-ttu-id="210bf-137">VM sku의 대문자 또는 소문자 ‘s’를 사용하는 VM만 프리미엄 디스크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="210bf-137">Only VMs with an uppercase or lowercase 's' in the VM sku can use premium disks.</span></span>

<span data-ttu-id="210bf-138">확장 집합으로 데이터 디스크 사용에 대한 자세한 내용은 [이 문서](./virtual-machine-scale-sets-attached-disks.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="210bf-138">To learn more about using data disks with scale sets, see [this article](./virtual-machine-scale-sets-attached-disks.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="210bf-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="210bf-139">Next steps</span></span>
<span data-ttu-id="210bf-140">확장 집합을 사용하는 예제 리소스 관리자 템플릿은 [Azure 빠른 시작 템플릿 github 리포지토리](https://github.com/Azure/azure-quickstart-templates)에서 "vmss"를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="210bf-140">For example Resource Manager templates using scale sets, search for "vmss" in the [Azure Quickstart Templates github repo](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="210bf-141">일반적인 정보는 [확장 집합에 대한 주 방문 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="210bf-141">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>

