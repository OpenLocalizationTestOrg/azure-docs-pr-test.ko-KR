---
title: "aaaAdd 조건과 워크플로-Azure 논리 앱 시작 | Microsoft Docs"
description: "조건부 논리, 트리거, 동작 및 매개 변수를 추가하여 Azure Logic Apps에서 워크플로가 실행되는 방식을 제어합니다."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a>논리 앱 기능 사용

[이전 항목](../logic-apps/logic-apps-create-a-logic-app.md)에서는 첫 번째 논리 앱을 만들었습니다. toocontrol 논리 앱의 워크플로 논리 앱 toorun에 대 한 서로 다른 경로 지정 하 고 어떻게 너무 배열, 컬렉션 및 일괄 처리에서 데이터를 처리 합니다. 논리 앱 워크플로에 포함될 수 있는 요소는 다음과 같습니다.

* 조건 및 [switch 문](../logic-apps/logic-apps-switch-case.md) - 특정 조건이 충족되는지 여부에 따라 논리 앱에서 다른 동작을 실행하도록 합니다.

* [루프](../logic-apps/logic-apps-loops-and-scopes.md) - 논리 앱에서 단계를 반복적으로 실행하도록 합니다. 예를 들어 **For_each** 루프를 사용할 때 배열에 대해 동작을 반복할 수 있습니다. 또는 **Until** 루프를 사용할 때 조건이 충족될 때까지 동작을 반복할 수 있습니다.

* [범위](../logic-apps/logic-apps-loops-and-scopes.md) 함께 그룹화 할 일련의 동작, 예를 들어 let tooimplement 예외 처리 합니다.

* [인증](../logic-apps/logic-apps-loops-and-scopes.md) hello를 사용 하는 경우 배열의 항목에 대 한 별도 워크플로 시작 하 여 논리 앱을 사용 하면 있습니다 **SplitOn** 명령입니다.

이 항목에서는 논리 앱을 빌드하기 위한 다른 개념에 대해 설명합니다.

* 보기 tooedit 기존 논리 앱 코드
* 워크플로 시작 옵션

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a>조건: 조건 충족 후에만 단계 실행

toohave 데이터 특정 조건을 충족 하는 경우에 단계를 실행 하 여 논리 앱을 특정 필드 또는 값에 대 한 hello 워크플로에서 데이터를 비교 하는 조건을 추가할 수 있습니다.

예를 들어 웹 사이트의 RSS 피드에 있는 게시물에 대해 너무 많은 전자 메일을 보내는 논리 앱이 있다고 가정해 보겠습니다. 조건이 논리 앱 hello 새 게시 하는 경우에 전자 메일을 보내 있도록 속한 tooa 특정 범주를 추가할 수 있습니다.

1. Hello에 [Azure 포털](https://portal.azure.com), 찾기 및 논리 앱 논리 응용 프로그램 디자이너에서 엽니다.

2. 원하는 조건을 toohello 워크플로 위치를 추가 합니다. 

   기존 hello 논리 앱 워크플로 단계 사이 tooadd hello 조건을 hello 포인터 위로 이동 hello 화살표 저장할 tooadd hello 조건. 
   Hello 선택 **더하기 기호** (**+**)를 선택 합니다 **조건 추가**합니다. 예:

   ![조건 toologic 앱 추가](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > 현재 워크플로의 hello 끝 조건을 tooadd를 원하는 경우 논리 앱의 toohello 아래쪽 이동 고 **+ 새 단계**합니다.

3. 이제 hello 조건을 정의 합니다. Tooevaluate, hello 작업 tooperform 및 hello 대상 값 또는 필드 원하는 hello 소스 필드를 지정 합니다. tooyour 조건 필드 tooadd 기존 hello 중에서 선택할 **동적 콘텐츠 목록에 추가**합니다.

   예:

   ![기본 모드에서 조건 편집](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   Hello 완전 한 조건이 다음과 같습니다.

   ![완성된 조건](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > 코드에서 toodefine hello 조건 선택 **고급 모드에서 편집**합니다. 예:
   > 
   > ![코드에서 조건 편집](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. 아래 **IF 예** 및 **IF 아니요**, hello 단계 tooperform hello 조건 충족 여부에 따라 추가 합니다.

   예:

   ![YES 및 NO 경로가 있는 조건](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > Hello에 기존 작업을 끌어올 수 **IF 예** 및 **IF 아니요** 경로입니다.

5. 완료되면 논리 앱을 저장합니다.

이제 hello 게시물에 조건을 충족 하는 경우에 전자 메일 가져오세요.

## <a name="repeat-actions-over-a-list-with-foreach"></a>forEach를 포함한 목록에 작업 반복

forEach 루프 hello 위에 배열 toorepeat 동작을 지정합니다. 배열이 없는 경우 hello 흐름 실패 합니다. 예를 들어 메시지의 배열을 출력 action1 있고 toosend 각 메시지를 원하는 경우 액션의 hello 속성에서이 forEach 문을 포함할 수 있습니다.`forEach : "@action('action1').outputs.messages"`

## <a name="edit-hello-code-definition-for-a-logic-app"></a>논리 앱에 대 한 hello 코드 정의 편집

Hello 논리가 응용 프로그램 디자이너를 사용 하는 있지만 논리 앱 정의 하는 hello 코드를 직접 편집할 수 있습니다.

1. Hello 명령 모음에서 **코드 뷰**합니다.

    전체 편집기가 열리고 편집한 hello 정의 보여 줍니다.

    ![코드 보기](media/logic-apps-use-logic-app-features/codeview.png)

    Hello 텍스트 편집기에서 복사 및 붙여넣기 수의 hello 내에서 작업 수 있습니다 같은 논리 앱 또는 논리 앱 사이입니다. 
    또한 추가 하거나 hello 정의에서 전체 섹션을 제거할 수 있으며 정의 다른 사용자와 공유할 수도 있습니다.

2. toosave 편집 내용을 선택 **저장**합니다.

## <a name="parameters"></a>매개 변수

일부 Logic Apps 기능은 매개 변수와 같은 코드 보기에서만 사용할 수 있습니다. 매개 변수 논리 앱 전반에서 쉽게 tooreuse 값을 만듭니다. 예를 들어 여러 작업에서 사용할 메일 주소가 있는 경우 해당 전자 메일 주소를 매개 변수로 정의해야 합니다.

매개 변수는 가능성이 toochange을 너무 많이 있는지 값을 추출 하는 데 유용 합니다. 다양 한 환경에서 toooverride 매개 변수를 할 때 특히 유용 합니다. 환경에 따라 toooverride 매개 변수를 확인 하려면 어떻게 toolearn [논리 앱 정의 작성](../logic-apps/logic-apps-author-definitions.md) 및 [REST API 문서](https://docs.microsoft.com/rest/api/logic)합니다.

이 예에서는 어떻게 tooupdate 기존 논리 앱 hello 쿼리 용어에 대 한 매개 변수를 사용할 수 있도록 합니다.

1. 코드 뷰에서 찾을 hello `parameters : {}` 개체를 추가할는 `currentFeedUrl` 개체:

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. Toohello 이동 `When_a_feed-item_is_published` 작업, 찾기 hello `queries` 섹션 및 hello 쿼리 값을 바꿉니다.`"feedUrl": "#@{parameters('currentFeedUrl')}"` 

    toojoin 둘 이상의 문자열 hello를 사용할 수도 있습니다 `concat` 함수입니다. 
    예를 들어 `"@concat('#',parameters('currentFeedUrl'))"` works hello 위의 hello와 동일 합니다.

3.  완료하면 **저장**을 선택합니다. 

    Hello 웹 사이트의 RSS hello 통해 다른 URL을 전달 하 여 피드를 변경할 수 이제 `currentFeedURL` 개체입니다.

에 대 한 자세한 내용은 [어떻게 tooauthor 논리 앱 정의](../logic-apps/logic-apps-author-definitions.md)합니다.

## <a name="start-logic-app-workflows"></a>논리 앱 워크플로 시작

논리 앱에 정의 된 hello 워크플로 시작 하기 위한 다른 옵션이 있습니다. 항상 hello에 대 한 요청 시 워크플로 시작 [Azure 포털]합니다.

### <a name="recurrence-triggers"></a>되풀이 트리거

되풀이 트리거는 지정한 간격마다 실행됩니다. Hello 트리거에 조건부 논리, hello 트리거 hello 워크플로 toorun 필요한 지 여부를 결정 합니다. 트리거를 반환 하 여 hello 워크플로가 실행 되는 나타냅니다는 `200` 상태 코드입니다. Hello 워크플로 toorun 필요 하지 않습니다, hello 트리거 반환는 `202` 상태 코드입니다.

### <a name="callback-using-rest-apis"></a>REST API를 사용한 콜백

워크플로 toostart 서비스 논리 앱 끝점을 호출할 수 있습니다. 이러한 종류의 논리가 응용 프로그램 요청 선택 toostart **지금 실행** hello 명령 모음에서 합니다. [논리 앱 끝점을 트리거로 호출하여 워크플로 시작](../logic-apps/logic-apps-http-endpoint.md)을 참조하세요. 

<!-- Shared links -->
[Azure 포털]: https://portal.azure.com

## <a name="next-steps"></a>다음 단계

* [Switch 문](../logic-apps/logic-apps-switch-case.md) 
* [루프, 범위 및 분할](../logic-apps/logic-apps-loops-and-scopes.md)
* [작성자 논리 앱 정의](../logic-apps/logic-apps-author-definitions.md)