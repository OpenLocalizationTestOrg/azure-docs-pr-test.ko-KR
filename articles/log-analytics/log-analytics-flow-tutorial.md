---
title: "Azure 로그 분석을 aaaAutomate Microsoft 흐름에 따라 처리"
description: "Microsoft Flow를 사용 하는 방법에 대해 알아봅니다 tooquickly hello Azure 로그 분석 커넥터를 사용 하 여 반복 가능한 프로세스를 자동화 합니다."
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Microsoft flow hello 커넥터와 함께 로그 분석 프로세스를 자동화 합니다.
[Microsoft Flow](https://ms.flow.microsoft.com) 수백 가지 작업을 사용 하 여 다양 한 서비스에 대 한 자동화 된 toocreate 워크플로가 있습니다. 출력 한 동작을 서로 다른 서비스 간의 toocreate 통합 있도록 입력된 tooanother로 사용할 수 있습니다.  Microsoft flow hello Azure 로그 분석 커넥터를 사용 하면 로그 분석에서 로그 검색에서 검색 된 데이터를 포함 하는 toobuild 워크플로가 있습니다.

예를 들어 Microsoft Flow toouse 로그 분석 데이터를 사용 하 여 Office 365에서 전자 메일 알림을에서 Visual Studio Team Services에서 버그를 만들 하거나 Slack 메시지를 게시할 수 있습니다.  메일이나 트윗이 수신될 때와 같이 연결된 서비스의 일부 작업 또는 단순 일정에서 워크플로를 트리거할 수 있습니다.  


> [!NOTE]
> Microsoft flow hello Azure 로그 분석 커넥터 작업 영역 업그레이드 toobe toohello 새 로그 분석 쿼리 언어를 필요합니다. Hello 새 언어에 대 한 자세한 정보를 hello 프로시저 tooupgrade 작업 영역을 가져올 수 [Azure 로그 분석 작업 영역 toonew 로그 검색을 업그레이드](log-analytics-log-search-upgrade.md)합니다.  

이 문서의 hello 자습서에서는 전자 메일, 예로, Microsoft Flow의 로그 분석을 사용 하는 방법을 자동으로 전송 하는 흐름 toocreate 로그 분석 로그 검색 결과 hello 하는 방법을 보여 줍니다. 


## <a name="step-1-create-a-flow"></a>1단계: 흐름 만들기
1. 역시 로그인[Microsoft Flow](http://flow.microsoft.com)를 선택 하 고 **내 흐름**합니다.
2. **+빈 페이지에서 만들기**를 클릭합니다.

## <a name="step-2-create-a-trigger-for-your-flow"></a>2단계: 흐름에 대한 트리거 만들기
1. **다양한 커넥터 및 트리거 검색**을 클릭합니다.
2. 형식 **일정** hello 검색 상자에 있습니다.
3. **일정**을 선택한 다음, **일정 - 되풀이**를 선택합니다.
4. Hello에 **주파수** 상자 선택 **일** 및 hello **간격** 상자에 입력 **1**합니다.<br><br>![Microsoft Flow 트리거 대화 상자](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>3단계: Log Analytics 작업 추가
1. **+새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.
2. **Log Analytics**를 검색합니다.
3. **Azure Log Analytics - 쿼리 실행 및 결과 시각화**를 클릭합니다.<br><br>![Log Analytics 쿼리 실행 창](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>Hello 로그 분석 작업을 구성 하는 4 단계:

1. Hello 구독 ID, 리소스 그룹 및 작업 영역 이름을 포함 하 여 작업 영역에 대 한 hello 세부 정보를 지정 합니다.
2. 로그 분석 쿼리 toohello 다음 hello 추가 **쿼리** 창.  이는 예제 쿼리일 뿐, 데이터를 반환하는 다른 항목으로 바꿀 수 있습니다.
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. 선택 **HTML 표** hello에 대 한 **차트 종류**합니다.<br><br>![Log Analytics 작업](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>5 단계: hello 흐름 toosend 전자 메일 구성

1. **새 단계**를 클릭한 다음 **+작업 추가**를 클릭합니다.
2. **Office 365 Outlook**을 검색합니다.
3. **Office 365 Outlook - 이메일 보내기**를 클릭합니다.<br><br>![Office 365 Outlook 선택 창](media/log-analytics-flow-tutorial/flow04.png)

4. Hello에 받는 사람의 hello 전자 메일 주소를 지정 **를** 창과 hello 전자 메일의 제목을 **주체**합니다.
5. Hello에서 아무 곳 이나 클릭 **본문** 상자입니다.  이전 작업의 값이 포함된 **동적 콘텐츠** 창이 열립니다.  
6. **본문**을 선택합니다.  이 hello 쿼리 결과를 hello hello 로그 분석 작업입니다.
6. **고급 옵션 표시**를 클릭합니다.
7. Hello에 **은 HTML** 상자 **예**합니다.<br><br>![Office 365 전자 메일 구성 창](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>6단계: 흐름 저장 및 테스트
1. Hello에 **흐름 이름** 상자, 프로그램 흐름에 대 한 이름을 추가 하 고 클릭 **흐름을 만드는**합니다.<br><br>![흐름 저장](media/log-analytics-flow-tutorial/flow06.png)
2. hello 흐름 이제 만들어지고 지정한 hello 일정 인 일 후에 실행 됩니다. 
3. tooimmediately 테스트 hello 흐름 클릭 **지금 실행** 차례로 **흐름 실행**합니다.<br><br>![흐름 실행](media/log-analytics-flow-tutorial/flow07.png)
3. Hello 흐름 완료 되 면 사용자가 지정한 hello 수신자의 hello 메일을 확인 하세요.  본문 비슷한 toohello 다음으로 메일을 받아야 합니다.<br><br>![샘플 메일](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>다음 단계

- [Log Analytics의 로그 검색](log-analytics-log-search-new.md)에 대해 자세히 알아보세요.
- [Microsoft Flow](https://ms.flow.microsoft.com)에 대해 자세히 알아봅니다.



