---
title: "논리 앱에서 쿼리 작업 추가 | Microsoft Docs"
description: "배열 필터링과 같은 작업을 수행하기 위한 쿼리 작업의 개요입니다."
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a>쿼리 작업 시작
쿼리 작업을 사용하면 배치 및 배열을 통해 다음을 수행하는 워크플로를 완료할 수 있습니다.

* 데이터베이스에서 모든 높은 우선순위 레코드에 대한 작업을 만듭니다.
* 전자 메일에 대한 모든 PDF 첨부 파일을 Azure Blob에 저장합니다.

논리 앱에서 쿼리 작업 사용을 시작하려면 [논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)를 참조하세요.

## <a name="use-the-query-action"></a>쿼리 작업 사용
작업은 논리 앱에 정의된 워크플로에 의해 수행되는 작업입니다. [작업에 대해 자세히 알아봅니다](connectors-overview.md).  

쿼리 작업에는 디자이너에 표시되는 배열 필터링이라는 작업 한 개가 있습니다. 이를 통해 배열을 쿼리하고 필터링된 결과 집합을 반환할 수 있습니다.

논리 앱에서 이를 추가하는 방법은 다음과 같습니다.

1. **새 단계** 단추를 선택합니다.
2. **작업 추가**를 선택합니다.
3. 작업 검색 상자에 **filter**를 입력하여 **배열 필터링** 작업을 나열합니다.
   
    ![쿼리 작업 선택](./media/connectors-native-query/using-action-1.png)
4. 필터링할 배열을 선택합니다. (다음 스크린샷은 Twitter 검색에서 결과의 배열을 표시합니다.)
5. 각 항목에 대해 평가할 조건을 만듭니다. (다음 스크린샷은 폴로워가 100명 이상인 사용자로부터 오는 트윗을 필터링합니다.)
   
    ![쿼리 작업 완료](./media/connectors-native-query/using-action-2.png)
   
    이 작업은 필터 요구 사항을 충족하는 결과만 포함하는 새 배열을 출력합니다.
6. 도구 모음의 왼쪽 위 모서리를 클릭하여 저장하면 논리 앱이 저장하고 게시합니다(활성화).

## <a name="query-action"></a>쿼리 작업
여기에는 이 커넥터가 지원하는 작업에 대한 세부 정보가 나와 있습니다. 커넥터에는 한 개의 가능한 작업이 있습니다.

| 작업 | 설명 |
| --- | --- |
| 배열 필터링 |배열에 있는 각 항목에 대한 조건을 평가하고 결과를 반환 |

## <a name="action-details"></a>작업 세부 정보
쿼리 작업은 한 개의 가능한 작업을 제공합니다. 다음 표에서는 작업의 필수 및 선택적 입력 필드와 함께 작업 사용과 연관된 해당 출력 세부 정보를 설명합니다.

### <a name="filter-array"></a>배열 필터링
HTTP 아웃바운드 요청을 하는 작업에 대한 입력 필드는 다음과 같습니다.
*는 필수 필드임을 의미합니다.

| 표시 이름 | 속성 이름 | 설명 |
| --- | --- | --- |
| 원본* |from |필터링할 배열 |
| 조건* |여기서, |각 항목에 대해 평가할 조건 |

<br>

### <a name="output-details"></a>출력 세부 정보
HTTP 요청에 대한 출력 세부 정보는 다음과 같습니다.

| 속성 이름 | 데이터 형식 | 설명 |
| --- | --- | --- |
| 필터링된 배열 |array |각 필터링된 결과에 대한 개체를 포함하는 배열 |

## <a name="next-steps"></a>다음 단계
이제 플랫폼을 사용해 보고 [논리 앱을 만듭니다](../logic-apps/logic-apps-create-a-logic-app.md). [API 목록](apis-list.md)에서 논리 앱의 사용 가능한 다른 커넥터를 확인할 수 있습니다.

