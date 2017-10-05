---
title: "Azure 확장 집합 템플릿에서 사용자 지정 이미지 참조 | Microsoft Docs"
description: "기존 Azure Virtual Machine Scale Set 템플릿에 사용자 지정 이미지를 추가하는 방법 알아보기"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/10/2017
ms.author: negat
ms.openlocfilehash: cf52fc9e95267c4bc5c0106aadf626685ddd5c24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-custom-image-to-an-azure-scale-set-template"></a><span data-ttu-id="a2842-103">Azure 확장 집합 템플릿에 사용자 지정 이미지 추가</span><span class="sxs-lookup"><span data-stu-id="a2842-103">Add a custom image to an Azure scale set template</span></span>

<span data-ttu-id="a2842-104">이 문서에서는 사용자 지정 이미지에서 배포할 [실행 가능한 최소 크기 집합 템플릿](./virtual-machine-scale-sets-mvss-start.md)을 수정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-104">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to deploy from custom image.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="a2842-105">템플릿 정의 변경</span><span class="sxs-lookup"><span data-stu-id="a2842-105">Change the template definition</span></span>

<span data-ttu-id="a2842-106">실행 가능한 최소 크기 집합 템플릿은 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)에 있으며, 사용자 지정 이미지에서 크기 집합을 배포하기 위한 템플릿은 [여기](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="a2842-107">이 템플릿(`git diff minimum-viable-scale-set custom-image`)을 하나씩 만드는 데 사용되는 diff에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-107">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="a2842-108">Managed Disk 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="a2842-108">Creating a managed disk image</span></span>

<span data-ttu-id="a2842-109">사용자 지정 Managed Disk 이미지가 이미 있는 경우(`Microsoft.Compute/images` 형식 리소스) 이 섹션을 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="a2842-110">먼저 배포를 시작할 사용자 지정 이미지를 포함하는 Azure Storage의 일반화된 Blob에 대한 URI에 해당하는 `sourceImageVhdUri` 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-110">First, we add a `sourceImageVhdUri` parameter, which is the URI to the generalized blob in Azure Storage that contains the custom image to deploy from.</span></span>


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "The source of the generalized blob containing the custom image"
+      }
     }
   },
   "variables": {},
```

<span data-ttu-id="a2842-111">다음으로 `sourceImageVhdUri` URI에 있는 일반화된 Blob를 기준으로 하는 Managed Disk 이미지에 해당하는 `Microsoft.Compute/images` 형식의 리소스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-111">Next, we add a resource of type `Microsoft.Compute/images`, which is the managed disk image based on the generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="a2842-112">이 이미지는 사용되는 확장 집합과 동일한 하위 지역에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-112">This image must be in the same region as the scale set that uses it.</span></span> <span data-ttu-id="a2842-113">이미지의 속성에서 OS 운영 체제, blob의 위치(`sourceImageVhdUri` 매개 변수) 및 저장소 계정 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-113">In the properties of the image, we specify the OS type, the location of the blob (from the `sourceImageVhdUri` parameter), and the storage account type:</span></span>

```diff
   "resources": [
     {
+      "type": "Microsoft.Compute/images",
+      "apiVersion": "2016-04-30-preview",
+      "name": "myCustomImage",
+      "location": "[resourceGroup().location]",
+      "properties": {
+        "storageProfile": {
+          "osDisk": {
+            "osType": "Linux",
+            "osState": "Generalized",
+            "blobUri": "[parameters('sourceImageVhdUri')]",
+            "storageAccountType": "Standard_LRS"
+          }
+        }
+      }
+    },
+    {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "location": "[resourceGroup().location]",

```

<span data-ttu-id="a2842-114">확장 집합 리소스에서 사용자 지정 이미지를 참조하는 추가 `dependsOn` 절을 추가하여 확장 집합이 해당 이미지에서의 배포를 시도하기 전에 이미지가 만들어지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-114">In the scale set resource, we add a `dependsOn` clause referring to the custom image to make sure the image gets created before the scale set tries to deploy from that image:</span></span>

```diff
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
       "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
+        "Microsoft.Network/virtualNetworks/myVnet",
+        "Microsoft.Compute/images/myCustomImage"
       ],
       "sku": {
         "name": "Standard_A1",

```

### <a name="changing-scale-set-properties-to-use-the-managed-disk-image"></a><span data-ttu-id="a2842-115">Managed Disk 이미지를 사용하도록 확장 집합 속성 설정</span><span class="sxs-lookup"><span data-stu-id="a2842-115">Changing scale set properties to use the managed disk image</span></span>

<span data-ttu-id="a2842-116">확장 집합 `storageProfile`의 `imageReference`에서, 플랫폼 이미지의 게시자, 제품, SKU 및 버전을 지정하는 대신, `Microsoft.Compute/images` 리소스의 `id`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-116">In the `imageReference` of the scale set `storageProfile`, instead of specifying the publisher, offer, sku, and version of a platform image, we specify the `id` of the `Microsoft.Compute/images` resource:</span></span>

```diff
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
-              "publisher": "Canonical",
-              "offer": "UbuntuServer",
-              "sku": "16.04-LTS",
-              "version": "latest"
+              "id": "[resourceId('Microsoft.Compute/images', 'myCustomImage')]"
             }
           },
           "osProfile": {
```

<span data-ttu-id="a2842-117">이 예제에서는 `resourceId` 함수를 사용하여 같은 템플릿에서 만들어진 이미지의 리소스 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-117">In this example, we use the `resourceId` function to get the resource ID of the image created in the same template.</span></span> <span data-ttu-id="a2842-118">Managed Disk 이미지를 미리 만든 경우 대신 해당 이미지의 ID를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-118">If you have created the managed disk image beforehand, you should provide the id of that image instead.</span></span> <span data-ttu-id="a2842-119">이 ID는 `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>` 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2842-119">This id must be of the form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a2842-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a2842-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
