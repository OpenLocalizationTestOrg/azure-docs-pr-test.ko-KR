---
title: "관리 되는 응용 프로그램 VirtualNetworkCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Network.VirtualNetworkCombo UI 요소를 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Microsoft.Network.VirtualNetworkCombo UI 요소
새 또는 기존 가상 네트워크를 선택하는 컨트롤 그룹입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- Hello 상위 와이어 프레임으로 hello 사용자 하므로 hello 사용자 각 서브넷의 이름 및 주소 접두사를 사용자 지정할 수 새 가상 네트워크를 선택 했습니다. 이 경우 서브넷을 구성하는 것은 선택 사항입니다.
- Hello 아래쪽 와이어 프레임으로 hello 사용자가 기존 가상 네트워크를 선택, 각 서브넷 hello 배포 템플릿에 tooan 기존 서브넷 필요 하므로 hello 사용자를 매핑해야 합니다. 이 경우 서브넷을 구성해야 합니다.

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>설명
- 를 지정 하는 경우 첫 번째 겹치지 않는 주소 접두사 크기 hello `defaultValue.addressPrefixSize` hello 사용자의 구독에서 기존 가상 네트워크에 따라 자동으로 결정 됩니다.
- 에 대 한 기본값을 hello `defaultValue.name` 및 `defaultValue.addressPrefixSize` 은 **null**합니다.
- `constraints.minAddressPrefixSize`를 지정해야 합니다. Hello 지정 된 값이 없는 선택할 수 있는 보다 작은 주소 공간과 기존 가상 네트워크입니다.
- `subnets`를 지정해야 하며, 각 서브넷에 대해 `constraints.minAddressPrefixSize`를 지정해야 합니다.
- 새 가상 네트워크를 만들 때 각 서브넷의 주소 접두사는 기준으로 자동 계산 hello 가상 네트워크의 주소 접두사와 해당 `addressPrefixSize`합니다.
- 기존 가상 네트워크를 사용할 때 각각의 `constraints.minAddressPrefixSize`보다 작은 서브넷은 모두 선택할 수 없습니다. 또한 지정하는 경우 `minAddressCount` 값 이상의 사용 가능한 주소를 포함하지 않는 서브넷은 선택할 수 없습니다.
hello 기본값은 **0**합니다. 사용 가능한 주소 hello tooensure 연속 되는, 지정 **true** 에 대 한 `requireContiguousAddresses`합니다. hello 기본값은 **true**합니다.
- 기존 가상 네트워크에서 서브넷을 만드는 것은 지원되지 않습니다.
- 경우 `options.hideExisting` 은 **true**, hello 사용자는 기존 가상 네트워크를 선택할 수 없습니다. hello 기본값은 **false**합니다.

## <a name="sample-output"></a>샘플 출력
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
