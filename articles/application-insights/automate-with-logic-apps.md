---
title: "aaaAutomate Application Insights Azure 논리 앱을 사용 하 여 처리 합니다."
description: "Hello Application Insights 커넥터 tooyour 논리 앱을 추가 하 여 반복 가능한 프로세스 신속 하 게 자동화할 수 방법을 알아봅니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: bwren
ms.openlocfilehash: 8565aadf0644ffb10da8a0964821901907db2e27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-application-insights-processes-by-using-logic-apps"></a>Logic Apps를 사용하여 Application Insights 프로세스 자동화

반복 실행 hello 동일한 쿼리 원격 분석 데이터 toocheck 프로그램 서비스가 제대로 작동 하는지 여부를 사용자가 직접 하십니까? 다음 주위에 맞게 워크플로 작성 및 찾고 tooautomate 찾기 추세와 비정상 상태에 대해 이러한 쿼리는? 논리 앱에 대 한 hello Azure Application Insights 커넥터 (preview)는이 목적을 위해 hello 오른쪽 도구입니다.

이 통합 덕분에 코드를 전혀 작성하지 않고도 수많은 프로세스를 자동화할 수 있습니다. 논리 앱을 만들 수 있습니다 커넥터 tooquickly hello Application Insights로 모든 Application Insights 프로세스를 자동화 합니다. 

작업을 더 추가할 수도 있습니다. Azure 앱 서비스의 hello 논리 앱 기능을 사용 하면 수백 가지 작업을 사용할 수 있습니다. 예를 들어 논리 앱을 사용하여 이메일 알림을 자동으로 보내거나 Visual Studio Team Services에서 버그를 만들 수 있습니다. 사용할 수도 있습니다 hello 중 사용 가능한 많은 [템플릿](https://docs.microsoft.com/azure/logic-apps/logic-apps-use-logic-app-templates) toohelp hello 논리 앱을 만드는 과정을 속도입니다. 

## <a name="create-a-logic-app-for-application-insights"></a>Application Insights에 대한 논리 앱 만들기

이 자습서에서는 toocreate 분석 autocluster 알고리즘 toogroup hello를 사용 하는 논리 앱 특성 방식을 웹 응용 프로그램에 대 한 hello 데이터에 알아봅니다. hello 흐름 전자 메일, 예로, 사용 하는 방법을 응용 프로그램 통찰력 분석 및 논리 앱 함께 hello 결과 자동으로 보냅니다. 

### <a name="step-1-create-a-logic-app"></a>1단계: 논리 앱 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **새로** 창 선택 **웹 + 모바일**를 선택한 후 **논리 앱**합니다.

    ![새 논리 앱 창](./media/automate-with-logic-apps/logicapp1.png)

### <a name="step-2-create-a-trigger-for-your-logic-app"></a>2단계: 논리 앱에 대한 트리거 만들기
1. Hello에 **논리가 응용 프로그램 디자이너** 창 아래에서 **일반적인 트리거 시작**선택, **되풀이**합니다.

    ![논리 앱 디자이너 창](./media/automate-with-logic-apps/logicapp2.png)

2. Hello에 **주파수** 상자 **일** 선택한 다음 hello **간격** 상자에 입력 합니다 **1**합니다.

    ![논리 앱 디자이너 "되풀이" 창](./media/automate-with-logic-apps/step2b.png)

### <a name="step-3-add-an-application-insights-action"></a>3단계: Application Insights 작업 추가
1. **새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.

2. Hello에 **동작 선택** 검색 상자에서 **Azure Application Insights**합니다.

3. **작업**에서 **Azure Application Insights – Analytics 쿼리 시각화 미리 보기**를 클릭합니다.

    ![논리 앱 디자이너 "작업 선택" 창](./media/automate-with-logic-apps/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>4 단계: tooan Application Insights 리소스를 연결 합니다.

toocomplete이이 단계에서는 리소스에 대 한 응용 프로그램 ID와 API 키가 필요 합니다. Hello 다음 다이어그램에에서 나와 있는 것 처럼 hello Azure 포털에서에서 해당를 검색할 수 있습니다.

![Hello Azure 포털에서에서 응용 프로그램 ID](./media/automate-with-logic-apps/appid.png) 

연결, hello 응용 프로그램 ID 및 hello API 키에 대 한 이름을 제공 합니다.

![논리 앱 디자이너 흐름 연결 창](./media/automate-with-logic-apps/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>5 단계: hello 분석 쿼리 및 차트 종류를 지정 합니다.
다음 예제는 hello, hello 쿼리 hello 마지막 날짜 내 hello 실패 요청을가 선택 하 고 상호 관련 시켜 hello 작업의 일부로 발생 하는 예외입니다. 분석은 hello operation_Id 식별자에 따라 hello 실패 요청을 연관 시킵니다. 그런 다음 hello 쿼리 hello autocluster 알고리즘을 사용 하 여 hello 결과 분할 합니다. 

사용자 고유의 쿼리를 만드는 경우를 정상적으로 작동 하는지 분석에서 tooyour 흐름 추가 하기 전에 확인 합니다.

1. Hello에 **쿼리** 상자 hello 다음 분석 쿼리를 추가 합니다. 

    ```
    requests
    | where timestamp > ago(1d)
    | where success == "False"
    | project name, operation_Id
    | join ( exceptions
        | project problemId, outerMessage, operation_Id
    ) on operation_Id
    | evaluate autocluster()
    ```

2. Hello에 **차트 종류** 상자 **Html 테이블**합니다.

    ![Analytics 쿼리 구성 창](./media/automate-with-logic-apps/flow4.png)

### <a name="step-6-configure-hello-logic-app-toosend-email"></a>6 단계: hello 논리 앱 toosend 전자 메일 구성

1. **새 단계**를 클릭한 다음 **작업 추가**를 선택합니다.

2. Hello 검색 상자에 입력 **Office 365 Outlook**합니다.

3. **Office 365 Outlook - 이메일 보내기**를 클릭합니다.

    ![Office 365 Outlook 선택](./media/automate-with-logic-apps/flow2b.png)

4. Hello에 **전자 메일 보내기** 창에서 다음 hello지 않습니다.

   a. Hello 수신자의 hello 전자 메일 주소를 입력 합니다.

   b. Hello 전자 메일의 제목을 입력 합니다.

   c. Hello에서 아무 곳 이나 클릭 **본문** 상자를 선택한 다음 선택 hello 동적 콘텐츠 메뉴에서 hello 오른쪽에 열리는 **본문**합니다.

   d. **고급 옵션 표시**를 클릭합니다.

      ![Office 365 Outlook 구성](./media/automate-with-logic-apps/flow5.png)

5. 동적 콘텐츠 메뉴 hello에서 수행 hello 다음:

    a. **첨부 파일 이름**을 선택합니다.

    b. **첨부 파일 콘텐츠**를 선택합니다.
    
    c. Hello에 **은 HTML** 상자 **예**합니다.

      ![Office 365 메일 구성 화면](./media/automate-with-logic-apps/flow7.png)

### <a name="step-7-save-and-test-your-logic-app"></a>7단계: 논리 앱 저장 및 테스트
* 클릭 **저장** toosave 변경 내용을 합니다.

Hello 트리거 toorun hello 논리 앱을 기다릴 수 있습니다 또는 선택 하 여 hello 논리 앱을 즉시 실행할 수 있습니다 **실행**합니다.

![논리 앱 만들기 화면](./media/automate-with-logic-apps/step7.png)

논리 앱을 실행할 때 hello 전자 메일 목록에 지정 된 hello 받는 사람이 전자 메일을 다음과 같은 hello 받을:

![논리 앱 이메일 메시지](./media/automate-with-logic-apps/flow9.png)

## <a name="next-steps"></a>다음 단계

- [Analytics 쿼리](app-insights-analytics-using.md) 만들기에 대해 자세히 알아봅니다.
- [Logic Apps](https://docs.microsoft.com/azure/logic-apps/logic-apps-what-are-logic-apps)에 대해 자세히 알아봅니다.



<!--Link references-->





