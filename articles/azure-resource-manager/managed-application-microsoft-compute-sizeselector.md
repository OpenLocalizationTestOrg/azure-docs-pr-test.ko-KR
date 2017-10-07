---
title: "관리 되는 응용 프로그램 SizeSelector UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Compute.SizeSelector UI 요소를 설명합니다."
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a>Microsoft.Compute.SizeSelector UI 요소
하나 이상의 가상 컴퓨터 인스턴스에 대한 크기를 선택하는 컨트롤입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>설명
- `recommendedSizes`는 하나 이상의 크기를 포함해야 합니다. hello 먼저 hello 기본값으로 사용 되는 크기 것이 좋습니다.
- Hello 선택한 위치에 권장 되는 크기를 사용할 수 없으면 hello 크기를 자동으로 건너뜁니다. 대신, hello 다음 권장된 크기가 사용 됩니다.
- Hello에 지정 되지 않은 모든 크기 `constraints.allowedSizes` 숨겨져 있는 경우에 지정 되지 않은 모든 크기 및 `constraints.excludedSizes` 표시 됩니다.
`constraints.allowedSizes`와 `constraints.excludedSizes`는 모두 선택 사항이지만 동시에 사용할 수는 없습니다. 호출 하 여 hello 목록이 사용 가능한 크기를 확인할 수 있습니다 [구독에 대 한 사용 가능한 가상 컴퓨터 크기 나열](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)합니다.
- `osPlatform`을 지정해야 하며 **Windows** 또는 **Linux**일 수 있습니다. Toodetermine hello 하드웨어 비용 hello 가상 컴퓨터를 사용 하는 합니다.
- `imageReference`은 자사 이미지에 대해 생략되지만, 타사 이미지에 대해서는 제공됩니다. Toodetermine hello 소프트웨어 비용의 hello 가상 컴퓨터를 사용 하는 합니다.
- `count`사용 되는 tooset hello hello 요소에 대 한 적절 한 승수가입니다. **2**와 같은 정적 값 또는 `[steps('step1').vmCount]`와 같은 다른 요소의 동적 값을 지원합니다. hello 기본값은 **1**합니다.

## <a name="sample-output"></a>샘플 출력
```json
"Standard_D1"
```

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
