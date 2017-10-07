---
title: "관리 되는 응용 프로그램 파일 업로드 UI 요소 aaaAzure | Microsoft Docs"
description: "Azure 관리 되는 응용 프로그램에 대 한 hello Microsoft.Common.FileUpload UI 요소를 설명합니다."
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Microsoft.Common.FileUpload UI 요소
하나 이상의 사용자 toospecify를 허용 하는 컨트롤 tooupload 파일. [Azure 관리되는 응용 프로그램을 만드는](managed-application-publishing.md) 경우 이 요소를 사용합니다.

## <a name="ui-sample"></a>UI 샘플
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>스키마
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>설명
- `constraints.accept`hello 형식의 hello 브라우저의 파일 대화 상자에 표시 되는 파일을 지정 합니다. Hello 참조 [HTML5 사양](http://www.w3.org/TR/html5/forms.html#attr-input-accept) 에 대 한 값을 허용 합니다. hello 기본값은 **null**합니다.
- 경우 `options.multiple` 너무 설정**true**, hello 사용자가 tooselect 이상의 hello 브라우저의 파일 대화 상자에서 파일 수입니다. hello 기본값은 **false**합니다.
- 이 요소에서의 hello 값에 따라 두 가지 모드에서 업로드 파일 지원 `options.uploadMode`합니다. 경우 **파일** 지정 hello 출력 blob로 hello 파일의 hello 내용을 포함 합니다. 경우 **url** 지정 되지 않으면 hello 파일이 업로드 된 tooa 임시 위치가 고 hello 출력 hello blob의 hello URL을 포함 합니다. 임시 Blob은 24시간 후에 제거됩니다. hello 기본값은 **파일**합니다.
- 값을 hello `options.openMode` hello 파일을 읽는 방법을 결정 합니다. 예상된 toobe 일반 텍스트 hello 파일을 사용 하는 경우 지정 **텍스트**, 그렇지 않으면, 지정 **이진**합니다. hello 기본값은 **텍스트**합니다.
- 경우 `options.uploadMode` 너무 설정**파일** 및 `options.openMode` 너무 설정**이진**, hello 출력은 base64 인코딩된 합니다.
- `options.encoding`hello 파일을 읽을 때 인코딩 toouse hello를 지정 합니다. hello 기본값은 **u t F-8**, 사용 되 고 경우에만 `options.openMode` 너무 설정**텍스트**합니다.

## <a name="sample-output"></a>샘플 출력
Options.multiple가 false이 고 options.uploadMode은 파일을 하는 경우 JSON 문자열로 hello 파일의 내용을 hello 포함 출력:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Options.multiple 참인 and'options.uploadMode 파일인 경우 출력 JSON 배열로 hello hello 파일 내용에 포함 된:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

options.multiple이 false이고 options.uploadMode가 url이면 출력에 URL이 JSON 문자열로 포함됩니다.

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

options.multiple이 true이고 options.uploadMode가 url이면 출력에 URL 목록이 JSON 배열로 포함됩니다.
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

CreateUiDefinition을 테스트할 때 일부 브라우저 (예: Google Chrome) hello 브라우저 콘솔에서 hello Microsoft.Common.FileUpload 요소에 의해 생성 된 Url을 자릅니다. Tooright 클릭 개별 링크 toocopy hello 전체 Url을 할 수 있습니다.


## <a name="next-steps"></a>다음 단계
* 소개 toomanaged 응용 프로그램에 대 한 참조 [Azure 관리 되는 응용 프로그램 개요](managed-application-overview.md)합니다.
* 소개 toocreating UI 정의 대 한 참조 [CreateUiDefinition 시작](managed-application-createuidefinition-overview.md)합니다.
* UI 요소의 공용 속성에 대한 설명은 [CreateUiDefinition 요소](managed-application-createuidefinition-elements.md)를 참조하세요.
