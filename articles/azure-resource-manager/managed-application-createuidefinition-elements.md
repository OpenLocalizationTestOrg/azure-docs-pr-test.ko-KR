---
title: "관리 되는 응용 프로그램 aaaAzure UI 정의 함수를 만들 | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 UI 정의 생성할 때 hello 함수 toouse 설명"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>CreateUiDefinition 요소
이 문서에서는 hello 스키마와는 CreateUiDefinition의 지원 되는 모든 요소에 대 한 속성을 설명 합니다. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다. 대부분의 요소에 대 한 hello 스키마는 다음과 같습니다.

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| 속성 | 필수 | 설명 |
| -------- | -------- | ----------- |
| name | 예 | 내부 식별자 tooreference 요소의 특정 인스턴스. hello hello 요소 이름의 가장 일반적으로 사용 중인 `outputs`hello의 hello 출력 값 요소는 hello 서식 파일의 매핑된 toohello 매개 변수를 지정 합니다. 사용할 수 있습니다도 toobind hello 출력 값의 요소 toohello `defaultValue` 다른 요소가 있습니다. |
| type | 예 | hello UI toorender hello 요소에 대 한 제어 합니다. 지원되는 형식 목록은 [요소](#elements)를 참조하세요. |
| label | 예 | hello는 hello 요소의 텍스트를 표시 합니다. 일부 요소 형식은 레이블이 여러 개 포함할 hello 값에는 여러 문자열을 포함 하는 개체 일 수 있습니다. |
| defaultValue | 아니요 | hello hello 요소의 기본 값입니다. 일부 요소 형식은 hello 값 개체 일 수 있으므로 복잡 한 기본값을 지원 합니다. |
| toolTip | 아니요 | hello 요소의 hello 도구 설명에 hello 텍스트 toodisplay 합니다. 비슷한 너무`label`, 일부 요소는 여러 도구 설명 문자열을 지원 합니다. Markdown 구문을 사용하여 인라인 링크를 포함할 수 있습니다.
| constraints | 아니요 | Hello 요소의 hello 유효성 검사 동작을 사용 하는 toocustomize 있는 하나 이상의 속성입니다. 제약 조건에 대 한 지원 hello 속성 요소 유형에 따라 달라 집니다. 일부 요소 형식은 hello 유효성 검사 동작을 사용자 지정을 지원 하지 않으며 제약 조건 속성이 있으므로 합니다. |
| options | 아니요 | Hello 요소의 hello 동작을 사용자 지정 하는 추가 속성입니다. 비슷한 너무`constraints`, 지원 되는 hello 속성 요소 유형에 따라 달라 집니다. |
| visible | 아니요 | Hello 요소가 표시 되는지 여부를 나타냅니다. 경우 `true`, hello 요소 및 해당 자식 요소가 표시 됩니다. hello 기본값은 `true`합니다. 사용 하 여 [논리 함수](managed-application-createuidefinition-functions.md#logical-functions) toodynamically이이 속성의이 값을 제어 합니다.

## <a name="elements"></a>요소

설명서 hello 스키마 hello 요소 (일반적으로 관련 유효성 검사 및 지원 되는 사용자 지정) 및 샘플 출력의 hello 동작에 주의 각 요소는 UI 샘플에 대 한 합니다.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
