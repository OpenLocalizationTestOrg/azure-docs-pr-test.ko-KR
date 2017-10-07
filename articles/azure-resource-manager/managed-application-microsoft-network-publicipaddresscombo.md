---
title: "관리 되는 응용 프로그램 PublicIpAddressCombo UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Network.PublicIpAddressCombo UI 요소를 설명합니다."
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Microsoft.Network.PublicIpAddressCombo UI 요소
새 또는 기존 공용 IP 주소를 선택하는 컨트롤 그룹입니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Hello 사용자가 공용 IP 주소에 대 한 ' 없음'를 선택 하는 경우 hello 도메인 이름 레이블 입력란은 숨겨집니다.
- Hello 사용자가 기존 공용 IP 주소를 선택 하는 경우 hello 도메인 이름 레이블 텍스트 상자가 비활성화 됩니다. 해당 값은 hello 도메인 이름 레이블이 hello 선택한 IP 주소입니다.
- hello hello 선택한 위치에 따라 자동으로 도메인 이름 접미사 (예를 들어 westus.cloudapp.azure.com) 업데이트 합니다.

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>설명
- 경우 `constraints.required.domainNameLabel` 너무 설정**true**, hello 사용자가 새 공용 IP 주소를 만들 때 도메인 이름 레이블을 제공 해야 합니다. 레이블이 없는 기존의 공용 IP 주소는 선택할 수 없습니다.
- 경우 `options.hideNone` 너무 설정**true**, 다음 옵션 tooselect hello **None** hello 공용 IP 주소는 숨겨집니다. hello 기본값은 **false**합니다.
- 경우 `options.hideDomainNameLabel` 너무 설정 되어**true**, 다음 hello 텍스트 상자에 도메인 이름 레이블이 숨겨집니다. hello 기본값은 **false**합니다.
- 경우 `options.hideExisting` 가 true 이면 hello 사용자가 기존 공용 IP 주소 수 toochoose가 아닙니다. hello 기본값은 **false**합니다.

## <a name="sample-output"></a>샘플 출력
Hello 사용자가 공용 IP 주소를 선택 하는 경우 hello 다음 예상 출력은:
```json
{
  "newOrExistingOrNone": "none"
}
```

Hello 사용자가 기존 또는 새 IP 주소를 선택 하는 경우 hello 다음 예상 출력은:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- `options.hideNone`을 지정하면 `newOrExistingOrNone`은 항상 **none**을 반환합니다.
- `options.hideDomainNameLabel`을 지정하면 `domainNameLabel`이 선언되지 않습니다.

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
