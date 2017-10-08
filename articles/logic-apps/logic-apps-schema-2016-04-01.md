---
title: "aaaSchema 2016 년 6 월 1--Azure 논리 앱을 업데이트 | Microsoft Docs"
description: "스키마 버전 2016-06-01로 Azure Logic Apps에 대한 JSON 정의 만들기"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 349d57e8-f62b-4ec6-a92f-a6e0242d6c0e
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/25/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: b0347fbbd692a93b63a2f8b741402a225450b35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---june-1-2016"></a>Azure Logic Apps에 대한 스키마 업데이트 - 2016년 6월 1일

이 새로운 스키마 및 API 버전 Azure 논리 앱에 대 한 논리 앱을 추가 하는 주요 향상 기능이 포함 되어 신뢰할 수 있는 쉽고 toouse:

* [범위](#scopes)를 통해 작업 컬렉션으로 작업을 그룹화 또는 중첩시킬 수 있습니다.
* [조건과 루프](#conditions-loops)는 최고 수준의 작업입니다.
* Hello로 작업을 실행 하는 것에 대 한 더 정확한 순서 `runAfter` 속성, 바꾸기`dependsOn`

논리 앱의 2015 년 8 월 1 일 hello tooupgrade 스키마 toohello 2016 년 6 월 1 일 스키마를 미리 볼 [섹션을 업그레이드 하는 hello](##upgrade-your-schema)합니다.

<a name="scopes"></a>
## <a name="scopes"></a>범위

이 스키마는 작업을 함께 그룹화하거나 작업을 서로 중첩시킬 수 있는 범위를 포함합니다. 예를 들어 조건은 다른 조건을 포함할 수 있습니다. [범위 구문](../logic-apps/logic-apps-loops-and-scopes.md)에 대해 자세히 알아보거나 기본 범위 예제를 검토하세요.

```
{
    "actions": {
        "My_Scope": {
            "type": "scope",
            "actions": {                
                "Http": {
                    "inputs": {
                        "method": "GET",
                        "uri": "http://www.bing.com"
                    },
                    "runAfter": {},
                    "type": "Http"
                }
            }
        }
    }
}
```

<a name="conditions-loops"></a>
## <a name="conditions-and-loops-changes"></a>조건 및 루프 변경

이전 버전의 스키마에서 조건과 루프는 단일 작업과 관련된 매개 변수였습니다. 이 스키마는 이 제한 사항을 해제하므로 조건과 루프가 작업 유형으로 나타납니다. [루프 및 범위](../logic-apps/logic-apps-loops-and-scopes.md)에 대해 자세히 알아보거나 조건 작업에 대한 기본 예제를 검토하세요.

```
{
    "If_trigger_is_some-trigger": {
        "type": "If",
        "expression": "@equals(triggerBody(), 'some-trigger')",
        "runAfter": { },
        "actions": {
            "Http_2": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://www.bing.com"
                },
                "runAfter": {},
                "type": "Http"
            }
        },
        "else": 
        {
            "if_trigger_is_another-trigger": "..."
        }      
    }
}
```

<a name="run-after"></a>
## <a name="runafter-property"></a>'runAfter' 속성

hello `runAfter` 속성 대신 `dependsOn`이전 동작의 hello 상태에 따라 작업에 대 한 hello 실행 순서를 지정 하는 경우 보다 정밀 하 게 제공 합니다.

hello `dependsOn` hello 이전 작업에 성공 했는지 여부에 따라 tooexecute 동작을 건너뛴 또는 실패 했거나, 원하는 횟수에 관계 없이, 속성은 "hello 작업 실행 및 성공 했습니다"와 같습니다. hello `runAfter` 속성은 모든 hello hello 개체 실행 하는 작업 이름을 지정 하는 개체와 이러한 유연성을 제공 합니다. 또한 이 속성은 트리거로 허용 가능한 상태 배열도 정의합니다. 예를 들어 toorun A 단계에 성공 하 고 또한 후 B 단계의 성공 또는 실패 한 후 원하는 경우 구성한이 `runAfter` 속성:

```
{
    "...",
    "runAfter": {
        "A": ["Succeeded"],
        "B": ["Succeeded", "Failed"]
    }
}
```

## <a name="upgrade-your-schema"></a>스키마 업그레이드

몇 가지 단계는 새 스키마에서만 toohello 업그레이드 합니다. hello 업그레이드 프로세스에 포함 되어 hello 업그레이드 스크립트 실행을 새 논리 앱으로 저장 하 고 원하는 경우 hello 이전 논리 앱을 덮어쓸 수 있습니다.

1. Hello Azure 포털에서에서 논리 앱을 엽니다.

2. 너무 이동**개요**합니다. Hello 논리 응용 프로그램 도구 모음에서 선택 **스키마 업데이트**합니다.
   
    ![스키마 업데이트 선택][1]
   
    hello 업그레이드 된 정의 반환 복사 하 고 필요한 경우 리소스 정의에 붙여 넣을 수 있는입니다. 
    그러나 우리 **강력히 권장** 선택한 **다른 이름으로 저장** toomake 모든 연결 참조 hello에 유효한 지 논리 앱을 업그레이드 합니다.

3. Hello 업그레이드 블레이드 도구 모음에서 선택 **다른 이름으로 저장**합니다.

4. Hello 논리 이름 및 상태를 입력 합니다. toodeploy 업그레이드 논리 앱 선택 **만들기**합니다.

5. 업그레이드된 논리 앱이 예상대로 작동하는지 확인합니다.
   
   > [!NOTE]
   > 수동 또는 요청 트리거를 사용 하는 경우 새 논리 앱 hello 콜백 URL이 변경 됩니다. 테스트 hello 새 URL toomake 있는지 hello에 종단 간 환경을 사용할 수 있습니다. toopreserve 이전 Url을 기존 논리 앱을 통해 복제할 수 있습니다.

6. *선택적* toooverwrite hello 새 스키마 버전으로 hello 도구 모음에서 이전 논리 앱 선택 **복제**다음, 너무**스키마 업데이트**합니다. 이 단계는 tookeep 논리 앱의 동일한 리소스 ID 또는 요청 트리거 URL hello 사용할 경우에 필요 합니다.

### <a name="upgrade-tool-notes"></a>업그레이드 도구 정보

#### <a name="mapping-conditions"></a>매핑 조건

업그레이드 하는 hello 정의 hello 도구 범위로 true 및 false 분기 작업을 함께 그룹화에서 최상의 노력을 만듭니다. 디자이너 패턴 hello 특히 `@equals(actions('a').status, 'Skipped')` 로 표시 해야 할는 `else` 동작 합니다. 그러나 인식할 수 없습니다. 패턴을 검색 하는 hello 도구, hello 도구는 hello true와 false 분기가 hello에 대 한 별도 조건을 만들 수 있습니다. 필요에 따라 업그레이드 후 작업을 다시 매핑할 수 있습니다.

#### <a name="foreach-loop-with-condition"></a>조건이 있는 'foreach' 루프

Hello 새 스키마에서의 hello 필터 동작 tooreplicate hello 패턴을 사용할 수 있습니다는 `foreach` 항목당, 조건이 포함 된 루프 있지만 업그레이드 하는 경우이 변경 내용을 자동으로 수행 해야 합니다. hello 조건 hello 조건과 일치 하는 항목의 배열을를 반환 하는 데 foreach 루프 hello 하기 전에 필터 동작을 되며 해당 배열 hello foreach 동작으로 전달 됩니다. 이에 대한 예제는 [루프 및 범위](../logic-apps/logic-apps-loops-and-scopes.md)를 참조하세요.

#### <a name="resource-tags"></a>리소스 태그

를 업그레이드 한 후 업그레이드 hello 워크플로에 대 한 재설정 해야 하므로 리소스 태그가 제거 됩니다.

## <a name="other-changes"></a>기타 변경 내용

### <a name="renamed-manual-trigger-toorequest-trigger"></a>이름이 '수동' 트리거 too'request' 트리거

hello `manual` 트리거 형식이 사용 되지 않으며 너무 이름이 변경 된`request` 형식과 `http`합니다. 이 변경은 hello 종류의 트리거가 hello 패턴은 사용 되는 toobuild 일관성이 만듭니다.

### <a name="new-filter-action"></a>새 '필터' 작업

toofilter tooa 정하여 항목을 새로운 hello 아래로 대형 배열 `filter` 형식을 수용 배열 및 조건을 각 항목에 대 한 hello 조건을 평가 하 고, hello 조건에 일치 항목이 있는 배열을 반환 합니다.

### <a name="restrictions-for-foreach-and-until-actions"></a>'foreach' 및 'until' 작업에 대한 제한 사항

hello `foreach` 및 `until` 루프는 제한 된 tooa 단일 작업입니다.

### <a name="new-trackedproperties-for-actions"></a>작업에 대한 새 'trackedProperties'

작업에서 이제 라는 추가 속성을 포함할 수 `trackedProperties`, 형제 toohello 변수인 `runAfter` 및 `type` 속성입니다. 이 개체에는 hello Azure 진단 원격 분석에서 워크플로의 일부로 내보내집니다 tooinclude 원하는 출력 또는 일부 작업 입력 데이터를 지정 합니다. 예:

```
{                
    "Http": {
        "inputs": {
            "method": "GET",
            "uri": "http://www.bing.com"
        },
        "runAfter": {},
        "type": "Http",
        "trackedProperties": {
            "responseCode": "@action().outputs.statusCode",
            "uri": "@action().inputs.uri"
        }
    }
}
```

## <a name="next-steps"></a>다음 단계
* [논리 앱용 워크플로 정의 만들기](../logic-apps/logic-apps-author-definitions.md)
* [논리 앱용 배포 템플릿 만들기](../logic-apps/logic-apps-create-deploy-template.md)

<!-- Image references -->
[1]: ./media/logic-apps-schema-2016-04-01/upgradeButton.png
