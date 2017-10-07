---
title: "Azure 논리 앱에서 다른 작업에 대해 aaaSwitch 문을 | Microsoft Docs"
description: "Switch 문을 사용 하 여 식 값에 따라 논리 앱의 동작이 서로 다른 tooperform 선택"
services: logic-apps
keywords: "Switch 문"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Switch 문으로 Logic Apps에서 다양한 작업 수행

워크플로 제작할 때 개체 또는 식의 hello 값에 따라 tootake 서로 다른 작업 종종 있어야 합니다. 예를 들어 hello 상태 코드는 HTTP 요청에 따라 다르게 하 여 논리 앱 toobehave 또는 전자 메일에서 선택한 옵션을 사용할 수 있습니다.

Switch 문 tooimplement 이러한 시나리오를 사용할 수 있습니다. 논리 앱에서 식이나 토큰을 계산 하 고 hello로 hello 사례 선택 수 값 tooexecute hello 동일한 작업을 지정 합니다. 하나의 사례 hello switch 문의 일치 해야 합니다.

> [!TIP]
> 모든 프로그래밍 언어와 마찬가지로 Switch 문도 같음 연산자만을 지원합니다. 다른 관계형 연산자(예: “초과”)가 필요한 경우 조건문을 사용합니다.
> tooensure 결정적 실행 동작의 경우 동적 토큰 또는 식 대신 고유 하 고 정적 값을 포함 해야 합니다.

## <a name="prerequisites"></a>필수 조건

- 활성 Azure 구독. 활성 Azure 구독이 없는 경우 시작하기 전에 [무료 계정을 만들거나](https://azure.microsoft.com/free/) [무료로 Logic Apps](https://tryappservice.azure.com/)을 사용해 보세요.
- [Logic Apps에 대한 기본 지식](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Switch 문 tooyour 워크플로 추가

switch 문의 작동 원리 tooshow,이 예제 모니터 파일 업로드 tooDropbox 되었는지 논리 앱을 만듭니다. Hello 논리 앱 전자 메일 tooan 승인자에 게 보내는 hello 새 파일을 업로드 하는 경우 여부 tootransfer 파일 tooSharePoint 해당 합니다. hello 앱 승인자가 선택 되어 hello는 hello 값에 따라 다른 작업을 수행 하는 switch 문을 사용 합니다.

1. 논리 앱을 만들고 **Dropbox - 파일을 만들 경우** 트리거를 선택합니다.

   ![Dropbox - 파일을 만들 경우 트리거 사용](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Hello 트리거 아래에서이 작업을 추가: **Outlook.com-전자 메일을 보내기 승인**

   > [!TIP]
   > 또한 Logic Apps는 Office 365 Outlook 계정에서 승인 전자 메일을 보내는 시나리오를 지원합니다.

   - 기존 연결 되지 않은 경우 메시지가 toocreate 하나입니다.
   - Hello 필수 필드를 입력 합니다. 예를 들어 아래 **를**, hello 승인자 전자 메일을 보내기 위한 hello 전자 메일 주소를 지정 합니다.
   - **사용자 옵션**에서 `Approve, Reject`을 입력합니다.

   ![연결 구성](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Switch 문을 추가합니다.

   - **+ 새 단계** > **... 추가 정보** > **Switch 사례 추가**를 선택합니다. 
   - 이제 tooselect hello 동작 tooperform hello에 따라 원하는 `SelectedOptions` hello에서 출력 *승인 전자 메일을 보낼* 동작 합니다. 
   Hello에서이 필드를 찾을 수 있습니다 **동적 콘텐츠를 추가할** 선택기입니다.
   - 사용 하 여 *사례 1* hello 승인자를 선택 했을 때 toohandle `Approve`합니다.
     - 승인 되 면 hello 원래 파일 tooSharePoint 온라인 hello로 복사 [ **SharePoint Online-파일을 만들** 동작](../connectors/connectors-create-api-sharepointonline.md)합니다.
     - 새 파일을 SharePoint에서 사용할 수 있는 hello 사례 toonotify 사용자에서 다른 작업을 추가 합니다.
   - 사용자가을 선택할 때 다른 사례 toohandle 추가 `Reject`합니다.
     - 거부 되 면 hello 파일 거부 되 고 추가 조치가 필요 하지 않습니다 다른 승인자에 게 알리는 알림 전자 메일을 보냅니다.
   - `SelectedOptions`hello 삭제할 수 있습니다. 되므로 두 개의 옵션을 제공 **기본** 경우 비어 있습니다.

   ![Switch 문](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Switch 문 또한 toohello 기본적인 경우 대/소문자를 하나 이상 필요합니다.

4. Hello switch 문의 한 후이 작업을 추가 하 여 hello 원래 업로드 한 파일 tooDropbox 삭제할: **Dropbox-파일 삭제**

5. 논리 앱을 저장합니다. 파일 tooDropbox 업로드 하 여 응용 프로그램을 테스트 합니다. 곧 승인 전자 메일을 받게 됩니다. 옵션을 선택 하 고 hello 동작을 관찰 합니다.

   > [!TIP]
   > 방법에 대해 너무 확인[논리 앱 모니터링](logic-apps-monitor-your-logic-apps.md)합니다.

## <a name="understand-hello-code-behind-switch-statements"></a>Switch 문 뒤에 있는 hello 코드 이해

Switch 문을 사용 하 여 논리 앱을 성공적으로 만든 hello switch 문의 뒤 hello 코드 정의에서 살펴보겠습니다.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`hello hello switch 문의 가독성을 높이기 위해 이름을 바꿀 수 있는 이름이입니다. 
* `"type": "Switch"`hello 동작은 switch 문을 나타냅니다. 
* `"expression"`이 예에서 hello 승인자 선택한 옵션이 며 hello 정의 나중에 선언 된 각 사례에 대해 평가 됩니다. 
* `"cases"`은 임의의 사례 수를 포함할 수 있습니다. 각 사례에 대해 `"Case *"` hello hello 소문자 가독성을 높이기 위해 이름을 바꿀 수 있습니다를 기본 이름입니다. 
`"case"`비교를 위해 사용 되는 스위치 식 hello 지속적이 고 고유한 값 이어야 하며 hello case 레이블을 지정 합니다. Hello switch 식에서 작업 하는 경우 필드 hello 사례 중 일치 하는 `"default"` 실행 됩니다.

## <a name="get-help"></a>도움말 보기

tooask 질문과 대답 질문 참조를 수행 하는 다른 Azure 논리 앱 사용자가 방문 hello [Azure 논리 앱 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)합니다.

Azure 논리 앱 및 커넥터 향상, 투표 하거나 hello에서 아이디어 제출 toohelp [Azure 논리 앱 사용자 의견 사이트](http://aka.ms/logicapps-wish)합니다.

## <a name="next-steps"></a>다음 단계

- 너무 방법에 대해 알아봅니다[조건 추가](logic-apps-use-logic-app-features.md)
- [오류 및 예외 처리](logic-apps-exception-handling.md)에 대해 알아봅니다.
- [워크플로 언어 기능](logic-apps-author-definitions.md)을 자세히 살펴봅니다.