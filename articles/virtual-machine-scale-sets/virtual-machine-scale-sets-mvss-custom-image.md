---
title: "Azure 확장 집합 템플릿에서 사용자 지정 이미지 참조 | Microsoft Docs"
description: "어떻게 tooadd 사용자 지정 이미지 tooan 기존 Azure 가상 컴퓨터 크기 집합 서식 파일에 알아봅니다"
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
ms.openlocfilehash: 6a17d989e44d241b460238c0106350c3ef038e56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a><span data-ttu-id="c744d-103">사용자 지정 이미지 tooan Azure 크기 조정 설정 템플릿 추가</span><span class="sxs-lookup"><span data-stu-id="c744d-103">Add a custom image tooan Azure scale set template</span></span>

<span data-ttu-id="c744d-104">이 문서에서는 어떻게 toomodify hello [실행 가능한 최소 소수 자릿수 템플릿을 설정](./virtual-machine-scale-sets-mvss-start.md) 사용자 지정 이미지에서 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy from custom image.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="c744d-105">Hello 템플릿 정의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-105">Change hello template definition</span></span>

<span data-ttu-id="c744d-106">이 실행 가능한 최소 소수 자릿수 집합 템플릿을 볼 수 있습니다 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), hello에 크기 집합에서 사용자 지정 이미지를 배포 하기 위한 우리의 서식 파일을 볼 수 있습니다 및 [여기](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set from a custom image can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json).</span></span> <span data-ttu-id="c744d-107">이 서식 파일 사용 diff toocreate hello를 검토해 보겠습니다 (`git diff minimum-viable-scale-set custom-image`) 하나씩:</span><span class="sxs-lookup"><span data-stu-id="c744d-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set custom-image`) piece by piece:</span></span>

### <a name="creating-a-managed-disk-image"></a><span data-ttu-id="c744d-108">Managed Disk 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="c744d-108">Creating a managed disk image</span></span>

<span data-ttu-id="c744d-109">사용자 지정 Managed Disk 이미지가 이미 있는 경우(`Microsoft.Compute/images` 형식 리소스) 이 섹션을 건너뛰어도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-109">If you already have a custom managed disk image (a resource of type `Microsoft.Compute/images`), then you can skip this section.</span></span>

<span data-ttu-id="c744d-110">먼저, 추가 `sourceImageVhdUri` hello URI toohello 일반화 된 Azure 저장소 blob에에서 사용자 지정 이미지 toodeploy hello를 포함 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-110">First, we add a `sourceImageVhdUri` parameter, which is hello URI toohello generalized blob in Azure Storage that contains hello custom image toodeploy from.</span></span>


```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "sourceImageVhdUri": {
+      "type": "string",
+      "metadata": {
+        "description": "hello source of hello generalized blob containing hello custom image"
+      }
     }
   },
   "variables": {},
```

<span data-ttu-id="c744d-111">다음으로, 리소스 유형 추가 `Microsoft.Compute/images`이며 hello 관리 되는 디스크 이미지를 일반화 하는 hello blob URI에 있는에 따라 `sourceImageVhdUri`합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-111">Next, we add a resource of type `Microsoft.Compute/images`, which is hello managed disk image based on hello generalized blob located at URI `sourceImageVhdUri`.</span></span> <span data-ttu-id="c744d-112">이 이미지 hello에 있어야 합니다.이 사용 하는 hello 크기 집합으로 같은 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-112">This image must be in hello same region as hello scale set that uses it.</span></span> <span data-ttu-id="c744d-113">Hello 이미지의 hello 속성, hello 운영 체제 유형, hello blob의 hello 위치 지정 (hello에서 `sourceImageVhdUri` 매개 변수), 및 hello 저장소 계정 유형:</span><span class="sxs-lookup"><span data-stu-id="c744d-113">In hello properties of hello image, we specify hello OS type, hello location of hello blob (from hello `sourceImageVhdUri` parameter), and hello storage account type:</span></span>

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

<span data-ttu-id="c744d-114">Hello에 크기 집합 리소스에 추가 `dependsOn` toohello 사용자 지정 이미지 toomake hello 크기 집합에 해당 이미지에서 toodeploy 하려고 시도 하기 전에 hello 이미지 생성 되어 있는지를 참조 하는 절:</span><span class="sxs-lookup"><span data-stu-id="c744d-114">In hello scale set resource, we add a `dependsOn` clause referring toohello custom image toomake sure hello image gets created before hello scale set tries toodeploy from that image:</span></span>

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a><span data-ttu-id="c744d-115">배율 변경 속성 toouse hello 관리 되는 디스크 이미지를 설정</span><span class="sxs-lookup"><span data-stu-id="c744d-115">Changing scale set properties toouse hello managed disk image</span></span>

<span data-ttu-id="c744d-116">Hello에 `imageReference` hello 눈금의 설정 `storageProfile`, hello hello 게시자, 제품, sku 및 플랫폼 이미지의 버전을 지정 하는 대신 지정 `id` 의 hello `Microsoft.Compute/images` 리소스:</span><span class="sxs-lookup"><span data-stu-id="c744d-116">In hello `imageReference` of hello scale set `storageProfile`, instead of specifying hello publisher, offer, sku, and version of a platform image, we specify hello `id` of hello `Microsoft.Compute/images` resource:</span></span>

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

<span data-ttu-id="c744d-117">이 예제에서는 사용 하 여 hello `resourceId` 동일 hello에서 hello 이미지의 함수 tooget hello 리소스 ID 만든 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-117">In this example, we use hello `resourceId` function tooget hello resource ID of hello image created in hello same template.</span></span> <span data-ttu-id="c744d-118">관리 되는 디스크 이미지 hello을 미리 만든 경우 대신 해당 이미지의 hello id를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-118">If you have created hello managed disk image beforehand, you should provide hello id of that image instead.</span></span> <span data-ttu-id="c744d-119">이 id는 hello 양식의 여야 합니다: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="c744d-119">This id must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c744d-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c744d-120">Next Steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
