---
title: "논리 앱에서 aaaAdd hello 쿼리 작업 | Microsoft Docs"
description: "필터 배열 처럼 동작을 수행 하는 것에 대 한 hello 쿼리 작업의 개요입니다."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a>Hello 쿼리 작업 시작
Hello 쿼리 작업을 사용 하 여 일괄 처리 및 배열 tooaccomplish 워크플로를 사용 하 여 사용할 수 있습니다.

* 데이터베이스에서 모든 높은 우선순위 레코드에 대한 작업을 만듭니다.
* 전자 메일에 대한 모든 PDF 첨부 파일을 Azure Blob에 저장합니다.

tooget hello 쿼리 동작을 사용 하 여 논리 앱에서 시작 참조 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다.

## <a name="use-hello-query-action"></a>Hello 쿼리 동작을 사용 하 여
동작은 논리 앱에 정의 된 hello 워크플로 통해 수행 되는 작업입니다. [작업에 대해 자세히 알아봅니다.](connectors-overview.md)  

hello 쿼리 작업에는 현재 hello 디자이너에서 제공 되는 hello 필터 배열 이라는 한 번의 작업을 있습니다. 이 배열 tooquery 있으며 필터링 된 결과 집합을 반환 합니다.

논리 앱에서 이를 추가하는 방법은 다음과 같습니다.

1. 선택 hello **새 단계** 단추입니다.
2. **작업 추가**를 선택합니다.
3. Hello 동작 검색 상자에 입력 **필터** toolist hello **필터 배열** 동작 합니다.
   
    ![Hello 쿼리 작업을 선택](./media/connectors-native-query/using-action-1.png)
4. 배열 toofilter를 선택 합니다. (hello 다음 스크린샷은 Twitter 검색에서 결과의 hello 배열입니다.)
5. 각 항목에 조건이 tooevaluate를 만듭니다. (다음 스크린샷 hello 100 개가 넘는 후속 작업이 사용자 로부터 트 윗을 필터링 합니다.)
   
    ![전체 hello 쿼리 작업](./media/connectors-native-query/using-action-2.png)
   
    hello 작업 hello 필터 요구 사항을 충족 하는 결과만 포함 하는 새 배열을 출력 합니다.
6. Hello 도구 모음 toosave와 여 논리 앱에서 모두 저장 hello 왼쪽 위 모퉁이 클릭 하 고 게시 (활성화).

## <a name="query-action"></a>쿼리 작업
이 커넥터가 지 원하는 hello 동작에 대 한 hello 세부 정보는 다음과 같습니다. hello 커넥터에 작업을 사용할 수 있습니다.

| 동작 | 설명 |
| --- | --- |
| 배열 필터링 |배열에 있는 각 항목에 대 한 조건을 평가 하 고 hello 결과 반환 합니다. |

## <a name="action-details"></a>작업 세부 정보
hello 쿼리 작업은 작업을 사용할 함께 제공 됩니다. hello 다음 표에서 필요한 hello 및 hello 작업과 hello 동작을 사용 하 여 연관 된 hello 해당 하는 출력 정보에 대 한 선택적 입력된 필드.

### <a name="filter-array"></a>배열 필터링
hello 다음은 아웃 바운드 HTTP 요청을 낮추는 hello 동작에 대 한 입력된 필드입니다.
*는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 원본* |from |hello 배열 toofilter |
| 조건* |여기서, |각 항목에 대 한 hello 조건 tooevaluate |

<br>

### <a name="output-details"></a>출력 세부 정보
hello 다음은 hello HTTP 응답에 대 한 정보를 출력 합니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 필터링된 배열 |array |각 필터링된 결과에 대한 개체를 포함하는 배열 |

## <a name="next-steps"></a>다음 단계
이제 hello 플랫폼을 사용해 및 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)합니다. 탐색할 수 확인 하 여 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.

