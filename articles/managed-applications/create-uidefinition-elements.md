---
title: "Azure Managed Application UI 정의 만들기 함수 | Microsoft Docs"
description: "Azure Managed Applications에 대한 UI 정의를 생성할 때 사용하는 함수에 대해 설명합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 23e407bf93bc51116ca45339bffcb801d69290f0
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition 요소
이 문서에서는 CreateUiDefinition에 지원되는 모든 요소에 대한 스키마와 속성에 대해 설명합니다. [Azure 관리되는 응용 프로그램을 만드는](publish-service-catalog-app.md) 경우 이 요소를 사용합니다. 대부분의 요소에 대한 스키마는 다음과 같습니다.

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit the [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```

| 속성 | 필수 | 설명 |
| -------- | -------- | ----------- |
| name | 예 | 요소의 특정 인스턴스를 참조하는 내부 식별자입니다. 요소 이름의 가장 일반적인 사용법은 `outputs`에 있으며, 지정된 요소의 출력 값이 템플릿의 매개 변수에 매핑됩니다. 또한 요소의 출력 값을 다른 요소의 `defaultValue`에 바인딩하는 데 사용할 수 있습니다. |
| type | 예 | 요소에 대해 렌더링할 UI 컨트롤입니다. 지원되는 형식 목록은 [요소](#elements)를 참조하세요. |
| label | 예 | 요소의 표시 텍스트입니다. 일부 요소 형식에는 여러 개의 레이블이 포함되므로 값은 여러 문자열을 포함하는 개체가 될 수 있습니다. |
| defaultValue | 아니요 | 요소의 기본값입니다. 일부 요소 형식에서 복잡한 기본값을 지원하므로 이 값은 개체가 될 수 있습니다. |
| toolTip | 아니요 | 요소의 도구 설명에 표시할 텍스트입니다. `label`과 마찬가지로 일부 요소에서 여러 개의 도구 설명 문자열을 지원합니다. Markdown 구문을 사용하여 인라인 링크를 포함할 수 있습니다.
| constraints | 아니요 | 요소의 유효성 검사 동작을 사용자 지정하는 데 사용되는 하나 이상의 속성입니다. 제약 조건에 지원되는 속성은 요소 형식에 따라 다릅니다. 일부 요소 형식에서는 유효성 검사 동작의 사용자 지정을 지원하지 않으므로 제약 조건 속성이 없습니다. |
| options | 아니요 | 요소의 동작을 사용자 지정하는 추가 속성입니다. `constraints`과 마찬가지로 지원되는 속성은 요소 형식에 따라 다릅니다. |
| visible | 아니요 | 요소가 표시되는지 여부를 나타냅니다. `true`이면 요소 및 적용 가능한 자식 요소가 표시됩니다. 기본값은 `true`입니다. [논리 함수](create-uidefinition-functions.md#logical-functions)를 사용하여 이 속성의 값을 동적으로 제어합니다.

## <a name="elements"></a>요소

각 요소에 대한 설명서에는 UI 샘플, 스키마, 요소의 동작에 대한 설명(일반적으로 유효성 검사 및 지원되는 사용자 지정과 관련됨) 및 샘플 출력이 포함되어 있습니다.

- [Microsoft.Common.DropDown](microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](microsoft-common-section.md)
- [Microsoft.Common.TextBox](microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>다음 단계
* 관리되는 응용 프로그램에 대한 소개는 [Azure Managed Application 개요](overview.md)를 참조하세요.
* UI 정의 만들기에 대한 소개는 [CreateUiDefinition 시작](create-uidefinition-overview.md)을 참조하세요.
