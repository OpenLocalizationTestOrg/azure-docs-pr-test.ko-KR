---
title: "Azure 리소스 관리자 범위로 aaaConvert 설정 템플릿 toouse 관리 되는 디스크 | Microsoft Docs"
description: "눈금 집합 템플릿 tooa 관리 되는 디스크 크기 조정 집합 서식 파일의 변환 합니다."
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
ms.openlocfilehash: 66c2217647e57ed2cfa39660c0175710ae2e63be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-scale-set-template-tooa-managed-disk-scale-set-template"></a>눈금 집합 템플릿 tooa 관리 되는 디스크 크기 조정 설정 서식 파일의 변환

크기는 관리 되는 디스크를 사용 하지 집합을 만들기 위한 리소스 관리자 템플릿 사용 하 여 고객 toomodify 것이 좋을 것 toouse 디스크를 관리 합니다. 이 문서에서는 어떻게 toodo를 사용 하 여이 예를 들어 hello에서 끌어오기 요청을 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates), 리소스 관리자 템플릿 샘플에 대 한 커뮤니티 기반 리 포 합니다. hello 전체 끌어오기 요청이 여기에 표시 될 수 있습니다: [https://github.com/Azure/azure-quickstart-templates/pull/2998](https://github.com/Azure/azure-quickstart-templates/pull/2998), 되며 hello 차이의 관련 부분 hello 아래 설명과 함께:

## <a name="making-hello-os-disks-managed"></a>관리 되는 hello OS 디스크 만들기

Hello diff 아래, 몇 가지 변수 관련된 toostorage 계정 및 디스크 속성 제거는 알 수 있습니다. 저장소 계정 유형은 필요 하지 않습니다 (Standard_LRS는 hello 기본값)에서는 여전히 지정 하기 위해 경우 수 없습니다. Standard_LRS 및 Premium_LRS는 관리되는 디스크로만 지원됩니다. 새 저장소 계정 접미사, 고유 문자열 배열 및 sa 수는 hello 이전 템플릿 toogenerate 저장소 계정 이름에 사용 되었습니다. 이러한 변수는 관리 되는 디스크 hello 고객의를 대신 하 여 저장소 계정을 자동으로 만들기 때문에 더 이상 hello 새 서식 파일에 필요 합니다. 마찬가지로, vhd 컨테이너 이름 및 os 디스크 이름은 더 이상 필요 하므로 저장소 blob 컨테이너를 원본으로 사용 하는 hello 및 디스크에 자동으로 관리 되는 디스크 이름을 합니다.

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


에서는 아래 hello diff 참조 hello로 업데이트 되었습니다을 계산할 수 api 버전 too2016-04-30-미리 보기, hello 가장 먼저 필요한 버전 크기 집합을 사용 하 여 관리 되는 디스크 지원 합니다. 에서는 사용할 수 있다는 여전히 관리 되지 않는 디스크 hello hello 오래 된 구문 사용 하 여 새 api 버전에 필요한 경우 note 합니다. 즉,만 업데이트 하는 경우 hello api 버전을 계산 하 고 어떤 항목도 변경 하지 않습니다, 그리고 hello 템플릿 앞으로 toowork 계속 해야 합니다.

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

Hello diff 아래, 있는지 제거 hello 저장소 계정 리소스 hello 리소스 배열에서 완전히 알 수 있습니다. 관리되는 디스크는 대신해서 이를 자동으로 만들기 때문에 저장소 계정 리소스는 더 이상 필요하지 않습니다.

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

에서는 아래 hello diff 수 참조 hello 제거 하는 것에 비례 저장소 계정 만들기가 하는 hello 눈금 집합 toohello 루프에서 참조 하는 절. Hello 이전 템플릿을 hello 크기 집합 만들기를 시작 하지만이 절은 더 이상 필요 없으며 관리 되는 디스크 전에 hello 저장소 계정이 생성 된 확인 된이입니다. 또한 hello vhd 컨테이너 속성을 제거 하 고 관리 되는 디스크에 의해 hello 내부적 이러한 속성은 자동으로 처리 하는 대로 os 디스크 이름 속성을 hello 합니다. 추가할 수 있으면 म 싶 었 거 나, `"managedDisk": { "storageAccountType": "Premium_LRS" }` hello "osDisk" 구성 프리미엄 OS 디스크 려 하는 경우에 합니다. Vm을 대문자 또는 소문자의 ' hello VM sku 프리미엄 디스크를 사용할 수 있습니다.

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

Hello 눈금 toouse 관리 여부 또는 관리 되지 않는 디스크에 대 한 구성 설정에에서 명시적 속성이 없습니다. hello 크기 집합 hello 저장소 프로필에 있는 hello 속성에 따라 어떤 toouse를 알고 있습니다. 즉, 중요 한 hello 템플릿 tooensure hello 크기 집합의 hello 저장소 프로필에 있는 hello 권한 속성을 수정 하는 경우.


## <a name="data-disks"></a>데이터 디스크

위의 hello 변화를 통해 hello 눈금 집합 사용 하 여 관리 하는 디스크 hello 운영 체제에 대 한 디스크에 데이터 디스크에 대 한 제공 하기는 하지만? tooadd 데이터 디스크 "osDisk"로 수준 동일 hello에 "storageProfile" hello "dataDisks" 속성을 추가 합니다. hello hello 속성의 값은 JSON 목록 개체의 속성 "lun" (VM에 데이터 디스크 마다 고유 해야 함)에 각각 "createOption" ("empty"는 현재 hello 지원 되는 옵션에만), 및 "diskSizeGB" ((기가바이트)에서 hello 디스크의 크기를 hello 여야 합니다. 0 보다 크고 1024 미만의) hello 다음 예제 에서처럼에서: 

```
"dataDisks": [
  {
    "lun": "1",
    "createOption": "empty",
    "diskSizeGB": "1023"
  }
]
```

지정 하는 경우 `n` 이 배열에 있는 디스크 hello 규모에 맞게 각 VM 집합 가져옵니다 `n` 데이터 디스크가 있습니다. 그러나 이러한 데이터 디스크는 원시 장치입니다. 포맷되지 않습니다. 사용 하기 전에 이러한 toohello 고객 tooattach, paritition, 및 형식 hello 디스크를 됩니다. 필요에 따라 우리 지정할 수도 `"managedDisk": { "storageAccountType": "Premium_LRS" }` 데이터 디스크를 프리미엄 되도록 각 데이터 디스크 개체 toospecify에 있습니다. Vm을 대문자 또는 소문자의 ' hello VM sku 프리미엄 디스크를 사용할 수 있습니다.

크기 집합에 데이터 디스크 사용에 대 한 더 toolearn 참조 [이 여기서](./virtual-machine-scale-sets-attached-disks.md)합니다.


## <a name="next-steps"></a>다음 단계
Hello에 크기 집합을 사용 하 여 리소스 관리자 템플릿을 "vmss"에 대 한 예를 들어 검색 [Azure 빠른 시작 템플릿 github 리포지토리](https://github.com/Azure/azure-quickstart-templates)합니다.

일반 정보에 대 한 체크 아웃 hello [크기 집합에 대 한 기본 방문 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)합니다.

