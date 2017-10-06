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
# <a name="add-a-custom-image-tooan-azure-scale-set-template"></a>사용자 지정 이미지 tooan Azure 크기 조정 설정 템플릿 추가

이 문서에서는 어떻게 toomodify hello [실행 가능한 최소 소수 자릿수 템플릿을 설정](./virtual-machine-scale-sets-mvss-start.md) 사용자 지정 이미지에서 toodeploy 합니다.

## <a name="change-hello-template-definition"></a>Hello 템플릿 정의 변경 합니다.

이 실행 가능한 최소 소수 자릿수 집합 템플릿을 볼 수 있습니다 [여기](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), hello에 크기 집합에서 사용자 지정 이미지를 배포 하기 위한 우리의 서식 파일을 볼 수 있습니다 및 [여기](https://raw.githubusercontent.com/gatneil/mvss/custom-image/azuredeploy.json)합니다. 이 서식 파일 사용 diff toocreate hello를 검토해 보겠습니다 (`git diff minimum-viable-scale-set custom-image`) 하나씩:

### <a name="creating-a-managed-disk-image"></a>Managed Disk 이미지 만들기

사용자 지정 Managed Disk 이미지가 이미 있는 경우(`Microsoft.Compute/images` 형식 리소스) 이 섹션을 건너뛰어도 됩니다.

먼저, 추가 `sourceImageVhdUri` hello URI toohello 일반화 된 Azure 저장소 blob에에서 사용자 지정 이미지 toodeploy hello를 포함 하는 매개 변수입니다.


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

다음으로, 리소스 유형 추가 `Microsoft.Compute/images`이며 hello 관리 되는 디스크 이미지를 일반화 하는 hello blob URI에 있는에 따라 `sourceImageVhdUri`합니다. 이 이미지 hello에 있어야 합니다.이 사용 하는 hello 크기 집합으로 같은 지역입니다. Hello 이미지의 hello 속성, hello 운영 체제 유형, hello blob의 hello 위치 지정 (hello에서 `sourceImageVhdUri` 매개 변수), 및 hello 저장소 계정 유형:

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

Hello에 크기 집합 리소스에 추가 `dependsOn` toohello 사용자 지정 이미지 toomake hello 크기 집합에 해당 이미지에서 toodeploy 하려고 시도 하기 전에 hello 이미지 생성 되어 있는지를 참조 하는 절:

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

### <a name="changing-scale-set-properties-toouse-hello-managed-disk-image"></a>배율 변경 속성 toouse hello 관리 되는 디스크 이미지를 설정

Hello에 `imageReference` hello 눈금의 설정 `storageProfile`, hello hello 게시자, 제품, sku 및 플랫폼 이미지의 버전을 지정 하는 대신 지정 `id` 의 hello `Microsoft.Compute/images` 리소스:

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

이 예제에서는 사용 하 여 hello `resourceId` 동일 hello에서 hello 이미지의 함수 tooget hello 리소스 ID 만든 서식 파일입니다. 관리 되는 디스크 이미지 hello을 미리 만든 경우 대신 해당 이미지의 hello id를 제공 해야 합니다. 이 id는 hello 양식의 여야 합니다: `/subscriptions/<subscription-id>resourceGroups/<resource-group-name>/providers/Microsoft.Compute/images/<image-name>`합니다.


## <a name="next-steps"></a>다음 단계

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
