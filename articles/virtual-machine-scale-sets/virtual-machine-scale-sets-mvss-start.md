---
title: "가상 컴퓨터 크기에 대 한 aaaLearn 템플릿을 설정할 | Microsoft Docs"
description: "최소 실행 가능한 소수 자릿수 toocreate 가상 컴퓨터 크기 집합에 대 한 템플릿을 설정에 대해 알아봅니다"
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
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Virtual Machine Scale Sets 템플릿에 대해 알아보기
[Azure 리소스 관리자 템플릿](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) 은 훌륭한 방법 toodeploy 관련된 리소스의 그룹입니다. 이 자습서 시리즈 표시 하 고 최소 실행 가능한 소수 자릿수 toocreate 템플릿을 설정 하는 방법 toomodify이 서식 파일 toosuit 다양 한 시나리오입니다. 모든 예제는 [GitHub 리포지토리](https://github.com/gatneil/mvss)에서 가져온 것입니다. 

이 서식 파일은 의도 한 toobe 단순 합니다. 눈금의 완전 한 예제에 대 한 템플릿 설정, hello 참조 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) hello 문자열이 포함 된 폴더에 대 한 검색 `vmss`합니다.

"다음 단계" 섹션 toosee toohello을 어떻게 건너뛸 수 이미 템플릿 만들기에 대해 잘 알고 있다면 toomodify이 서식이 파일입니다.

## <a name="review-hello-template"></a>검토 hello 템플릿

GitHub를 사용 하 여 tooreview 우리의 최소 실행 가능한 크기 집합 템플릿을 [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json)합니다.

이 자습서에서는 hello diff 살펴보겠습니다 (`git diff master minimum-viable-scale-set`) toocreate hello 최소 실행 가능한 크기 집합 템플릿 하나씩 있습니다.

## <a name="define-schema-and-contentversion"></a>$schema 및 contentVersion 정의
첫째, 정의 `$schema` 및 `contentVersion` hello 서식 파일에 있습니다. hello `$schema` 요소 hello 버전의 hello 템플릿 언어를 정의 하 고 Visual Studio 구문 강조 표시와 비슷한 유효성 검사 기능에 사용 됩니다. hello `contentVersion` 요소가 Azure에서 사용 되지 않습니다. 대신, 수 hello 템플릿 버전을 추적할 수 있습니다.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>매개 변수 정의
다음으로 두 개의 매개 변수인 `adminUsername` 및 `adminPassword`를 정의합니다. 매개 변수는 배포의 hello 시 지정 하는 값입니다. hello `adminUsername` 매개 변수는 단순히는 `string` 형식 때문에 `adminPassword` 는 암호로 형식 지정에서는 `securestring`합니다. 이상에서는 이러한 매개 변수 hello 배율 구성 설정에 전달 됩니다.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>변수 정의
또한 리소스 관리자 템플릿을 사용 하 hello 서식 파일의 뒷부분에 나오는 사용 되는 변수 toobe 정의할 수 있습니다. 예에서 사용 하는 hello JSON 개체를 빈 두었으며 하므로 모든 변수를 사용 하지 않습니다.

```json
  "variables": {},
```

## <a name="define-resources"></a>리소스 정의
다음은 hello 템플릿의 리소스 섹션 hello입니다. 실제로 수행할 동작을 정의 여기서 toodeploy 합니다. `parameters` 및 `variables`(JSON 개체)과 달리 `resources`는 JSON 개체의 JSON 목록입니다.

```json
   "resources": [
```

모든 리소스에는 `type`, `name`, `apiVersion` 및 `location` 속성이 필요합니다. 이 예제의 첫 번째 리소스는 `Microsft.Network/virtualNetwork` 형식이고 이름은 `myVnet`이며 apiVersion은 `2016-03-30`입니다. (리소스 유형에 대 한 toofind hello 최신 API 버전 참조 hello [Azure REST API 설명서](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>위치 지정
hello 가상 네트워크에 대 한 toospecify hello 위치를 사용 하 여 한 [리소스 관리자 템플릿 함수](../azure-resource-manager/resource-group-template-functions.md)합니다. 이 함수는 `"[<template-function>]"`처럼 따옴표와 대괄호로 묶어야 합니다. 이 경우 hello 사용 `resourceGroup` 함수입니다. 인수를 사용 하 고이 배포를 배포 하 고 hello 리소스 그룹에 대 한 메타 데이터와 JSON 개체를 반환 합니다. hello 리소스 그룹 배포의 hello 시 hello 사용자에 의해 설정 됩니다. 에서는 다음이 JSON 개체의 인덱스 `.location` hello JSON 개체에서 tooget hello 위치입니다.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>가상 네트워크 속성 지정
각 리소스 관리자 리소스에는 자체 `properties` 구성 toohello 특정 리소스에 대 한 섹션. 이 경우 해당 hello 가상 네트워크 hello 개인 IP 주소 범위를 사용 하는 서브넷 1 개 있어야 합니다. 지정 म `10.0.0.0/16`합니다. 확장 집합은 항상 하나의 서브넷에 포함되며 여러 서브넷에 걸쳐 있을 수 없습니다.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>dependsOn 목록 추가
또한 toohello 필요한 `type`, `name`, `apiVersion`, 및 `location` 속성, 각 리소스를 선택적 가질 수 있습니다 `dependsOn` 문자열의 목록입니다. 이 목록은 이 리소스를 배포하기 전에 이 배포의 다른 리소스가 완료해야 하는 것을 지정합니다.

이 경우 hello 이전 예제에서 가상 네트워크의 hello hello 목록의 요소가 하나 뿐입니다. 이 종속성 hello 크기 집합 필요 hello 네트워크 tooexist Vm을 만들기 전에 때문에 지정 합니다. 이러한 방식으로 hello 크기 집합 hello 네트워크 속성에 지정 된 이전 hello IP 주소 범위에서 이러한 Vm 개인 IP 주소를 제공할 수 있습니다. hello hello dependsOn 목록의 각 문자열의 형식이 `<type>/<name>`합니다. 사용 하 여 hello 동일 `type` 및 `name` hello 가상 네트워크 리소스 정의에서 이전에 사용 합니다.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>확장 집합 속성 지정
크기 집합은 hello Vm 크기 집합 hello에에서 사용자 지정 하기 위한 많은 속성이 있습니다. 이러한 속성 목록은 전체 참조 hello [크기 REST API 설명서 집합](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set)합니다. 이 자습서에서는 일반적으로 사용되는 몇 가지 속성만 설정합니다.
### <a name="supply-vm-size-and-capacity"></a>VM 크기 및 용량 제공
hello 눈금 VM toocreate ("sku 이름")의 크기 및 이러한 개수 Vm toocreate ("sku 용량") 요구 tooknow를 설정합니다. 어떤 VM 크기를 사용할 수 있는 toosee hello 참조 [VM 크기 설명서](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes)합니다.

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>업데이트 유형 선택
hello 크기 집합에는 또한 toohandle hello 크기 집합에 업데이트 하는 방식 tooknow가 필요 합니다. 현재 `Manual` 및 `Automatic`의 두 가지 옵션이 있습니다. Hello 두 hello 차이에 대 한 자세한 내용은 hello 설명서를 참조 [배율 설정 하는 tooupgrade 방법을](./virtual-machine-scale-sets-upgrade-scale-set.md)합니다.

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>VM 운영 체제 선택
hello 크기 조정 요구 tooknow 어떤 운영 체제 tooput hello Vm에서 설정합니다. 여기에서 완전히 패치 Ubuntu LTS 16.04 이미지로 hello Vm 만듭니다.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>computerNamePrefix 지정
hello 크기 집합 여러 Vm을 배포합니다. 각각의 VM 이름을 지정하는 대신 `computerNamePrefix`를 지정합니다. hello 크기 집합 추가 인덱스 toohello 접두사 각 VM에 대 한 VM 이름 hello 형식으로 되어 있으므로 `<computerNamePrefix>_<auto-generated-index>`합니다.

다음 코드 조각 hello, hello 크기 집합의 모든 Vm에 대 한 hello 매개 변수를 하기 전에 tooset hello 관리자 사용자 이름 및 암호 사용 합니다. Hello로 수행 `parameters` 템플릿 함수입니다. 이 함수는 매개 변수 toorefer tooand 해당 매개 변수에 대해 hello 값을 출력을 지정 하는 문자열에 사용 합니다.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>VM 네트워크 구성 지정
마지막으로, hello 크기 집합의 hello Vm에 대 한 toospecify hello 네트워크 구성을 해야 합니다. 이 경우 앞에서 만든 hello 서브넷의 toospecify hello ID만 필요 합니다. 이 hello 크기 집합 tooput hello 네트워크 인터페이스가이 서브넷의 값을 알려줍니다.

Hello hello를 사용 하 여 hello 서브넷을 포함 하는 가상 네트워크의 hello ID를 얻을 수 `resourceId` 템플릿 함수입니다. 이 함수는 hello 유형 및 리소스의 이름을 사용 하 고 반환 hello 해당 리소스의 정규화 된 식별자입니다. 이 ID는 hello 형식은 같습니다.`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

그러나 hello 가상 네트워크의 hello 식별자 충분 하지 않습니다. 크기 집합 Vm에 있어야 hello hello 특정 서브넷을 지정 해야 합니다. toodo이를 연결할 `/subnets/mySubnet` hello 가상 네트워크의 toohello ID입니다. hello 결과 hello 서브넷의 정규화 된 hello ID입니다. 이 연결은 hello로 수행 `concat` 일련의 문자열에서 사용 하 고 해당 연결을 반환 하는 함수입니다.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>다음 단계

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
