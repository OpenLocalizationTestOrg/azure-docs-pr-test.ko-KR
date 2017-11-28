---
title: "Azure 확장 집합 템플릿에서 기존 가상 네트워크 참조 | Microsoft Docs"
description: "가상 a tooadd tooan 기존 Azure 가상 컴퓨터 크기 집합 서식 파일을 네트워크 방법에 대해 알아봅니다"
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
ms.date: 06/27/2017
ms.author: negat
ms.openlocfilehash: c3034b577e17abc4643dc26d7c38ad643fa26322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-reference-tooan-existing-virtual-network-in-an-azure-scale-set-template"></a><span data-ttu-id="98161-103">Azure 확장 집합 템플릿에서 참조 tooan 기존 가상 네트워크 추가</span><span class="sxs-lookup"><span data-stu-id="98161-103">Add reference tooan existing virtual network in an Azure scale set template</span></span>

<span data-ttu-id="98161-104">이 문서에서는 어떻게 toomodify hello [실행 가능한 최소 소수 자릿수 템플릿을 설정](./virtual-machine-scale-sets-mvss-start.md) toodeploy 새로 만드는 대신 기존 가상 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98161-104">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toodeploy into an existing virtual network instead of creating a new one.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="98161-105">Hello 템플릿 정의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-105">Change hello template definition</span></span>

<span data-ttu-id="98161-106">이 실행 가능한 최소 소수 자릿수 집합 템플릿을 볼 수 있습니다 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), hello에 크기 집합을 기존 가상 네트워크로 배포 하기 위한 우리의 서식 파일을 볼 수 있습니다 및 [여기](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-106">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello scale set into an existing virtual network can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/existing-vnet/azuredeploy.json).</span></span> <span data-ttu-id="98161-107">이 서식 파일 사용 diff toocreate hello를 검토해 보겠습니다 (`git diff minimum-viable-scale-set existing-vnet`) 하나씩:</span><span class="sxs-lookup"><span data-stu-id="98161-107">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="98161-108">먼저 `subnetId` 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-108">First, we add a `subnetId` parameter.</span></span> <span data-ttu-id="98161-109">이 문자열 hello 크기 집합 tooidentify hello에 대 한 미리 작성된 된 서브넷에 가상 컴퓨터 toodeploy 허용 hello 눈금 집합 구성에 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98161-109">This string will be passed into hello scale set configuration, allowing hello scale set tooidentify hello pre-created subnet toodeploy virtual machines into.</span></span> <span data-ttu-id="98161-110">이 문자열 hello 형식 이어야 합니다: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-110">This string must be of hello form: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<virtual-network-name>/subnets/<subnet-name>`.</span></span> <span data-ttu-id="98161-111">Toodeploy hello 눈금을 기존 가상 네트워크 이름의 설정 하는 예를 들어, `myvnet`, 서브넷 `mysubnet`, 리소스 그룹 `myrg`, 구독 및 `00000000-0000-0000-0000-000000000000`, hello subnetId 것: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-111">For instance, toodeploy hello scale set into an existing virtual network with name `myvnet`, subnet `mysubnet`, resource group `myrg`, and subscription `00000000-0000-0000-0000-000000000000`, hello subnetId would be: `/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myrg/providers/Microsoft.Network/virtualNetworks/myvnet/subnets/mysubnet`.</span></span>

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "subnetId": {
+      "type": "string"
     }
   },
```

<span data-ttu-id="98161-112">Hello 가상 네트워크 리소스 hello에서 삭제할 수는 다음으로, `resources` 배열, 기존 가상 네트워크를 사용 하는 고 toodeploy 새 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="98161-112">Next, we can delete hello virtual network resource from hello `resources` array, since we are using an existing virtual network and don't need toodeploy a new one.</span></span>

```diff
   "variables": {},
   "resources": [
-    {
-      "type": "Microsoft.Network/virtualNetworks",
-      "name": "myVnet",
-      "location": "[resourceGroup().location]",
-      "apiVersion": "2016-12-01",
-      "properties": {
-        "addressSpace": {
-          "addressPrefixes": [
-            "10.0.0.0/16"
-          ]
-        },
-        "subnets": [
-          {
-            "name": "mySubnet",
-            "properties": {
-              "addressPrefix": "10.0.0.0/16"
-            }
-          }
-        ]
-      }
-    },
```

<span data-ttu-id="98161-113">가상 네트워크 hello 이미 hello 서식 파일을 배포 하기 전에 hello 눈금에서 dependsOn 절 toohello 가상 네트워크를 설정 없습니다 필요 toospecify 이므로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-113">hello virtual network already exists before hello template is deployed, so there is no need toospecify a dependsOn clause from hello scale set toohello virtual network.</span></span> <span data-ttu-id="98161-114">따라서 다음 줄들을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="98161-114">Thus, we delete these lines:</span></span>

```diff
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "location": "[resourceGroup().location]",
       "apiVersion": "2016-04-30-preview",
-      "dependsOn": [
-        "Microsoft.Network/virtualNetworks/myVnet"
-      ],
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
```

<span data-ttu-id="98161-115">Hello에 마지막으로 전달 `subnetId` hello 사용자가 설정한 매개 변수 (사용 하는 대신 `resourceId` 은 어떤 hello 최소 실행 가능한 소수 자릿수 템플릿을 설정 하는 동일한 배포는 hello에 vnet의 tooget hello id)입니다.</span><span class="sxs-lookup"><span data-stu-id="98161-115">Finally, we pass in hello `subnetId` parameter set by hello user (instead of using `resourceId` tooget hello id of a vnet in hello same deployment, which is what hello minimum viable scale set template does).</span></span>

```diff
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
-                          "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
+                          "id": "[parameters('subnetId')]"
                         }
                       }
                     }
```




## <a name="next-steps"></a><span data-ttu-id="98161-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="98161-116">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
