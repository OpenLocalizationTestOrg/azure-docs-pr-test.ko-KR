---
title: "Microsoft 흐름에 따라 aaaAutomate Azure Application Insights 처리"
description: "Microsoft Flow를 사용 하는 방법에 대해 알아봅니다 tooquickly hello Application Insights 커넥터를 사용 하 여 반복 가능한 프로세스를 자동화 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: bwren
ms.openlocfilehash: b34488a6b8b8b0a6add960a67f1426cbbbc13552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-azure-application-insights-processes-with-hello-connector-for-microsoft-flow"></a>Microsoft flow hello 커넥터와 함께 Azure Application Insights 프로세스를 자동화 합니다.

프로그램 서비스가 제대로 작동 하 여 원격 분석 데이터 toocheck에서 hello 동일한 쿼리를 반복 해 서 실행 직접 하십니까? 다음 주위에 맞게 워크플로 작성 및 찾고 tooautomate 찾기 추세와 비정상 상태에 대해 이러한 쿼리는? Microsoft flow hello Azure Application Insights 커넥터 (preview)는 이러한 용도로 hello 오른쪽 도구입니다.

이 통합 덕분에 이제 코드 한 줄 작성하지 않고도 수많은 프로세스를 자동화할 수 있습니다. Application Insights 동작을 사용 하 여 흐름을 만드는 후 hello 흐름은 자동으로 응용 프로그램 통찰력 분석 쿼리를 실행 합니다. 

작업을 더 추가할 수도 있습니다. Microsoft Flow는 수백 개의 작업을 사용할 수 있게 해줍니다. 예를 들어 Microsoft Flow tooautomatically 송신 전자 메일 알림을 사용 하거나 Visual Studio Team Services에서 버그를 만들 수 있습니다. 사용할 수도 있습니다 hello 중 많은 [템플릿](https://ms.flow.microsoft.com/en-us/connectors/shared_applicationinsights/?slug=azure-application-insights) Microsoft flow hello 커넥터에 대해 사용할 수 있습니다. 이러한 템플릿은 프로세스 속도를 높일 hello 흐름을 만드는 중입니다. 

<!--hello Application Insights connector also works with [Azure Power Apps](https://powerapps.microsoft.com/en-us/) and [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/?v=17.23h). --> 

## <a name="create-a-flow-for-application-insights"></a>Application Insights 흐름 만들기

이 자습서에서는 toocreate hello 분석 자동 클러스터 알고리즘 toogroup을 사용 하는 흐름 특성 방식을 웹 응용 프로그램에 대 한 hello 데이터가 배웁니다. hello 흐름 전자 메일, 예로, 사용 하는 방법을 Microsoft Flow 및 응용 프로그램 통찰력 분석 함께 hello 결과 자동으로 보냅니다. 

### <a name="step-1-create-a-flow"></a>1단계: 흐름 만들기
1. 역시 로그인[Microsoft Flow](http://flow.microsoft.com)를 선택한 후 **내 흐름**합니다.
2. **빈 곳에서 흐름 만들기**를 클릭합니다.

### <a name="step-2-create-a-trigger-for-your-flow"></a>2단계: 흐름에 대한 트리거 만들기
1. **일정**을 선택한 다음, **일정 - 되풀이**를 선택합니다.
2. Hello에 **주파수** 상자 **일**, 및 hello **간격** 상자에 입력 **1**합니다.

    ![Microsoft Flow 트리거 대화 상자](./media/app-insights-automate-with-flow/flow1.png)


### <a name="step-3-add-an-application-insights-action"></a>3단계: Application Insights 작업 추가
1. **새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.
2. **Azure Application Insights**를 검색합니다.
3. **Azure Application Insights – Analytics 쿼리 시각화 미리 보기**를 클릭합니다.

    ![Analytics 쿼리 실행 창](./media/app-insights-automate-with-flow/flow2.png)

### <a name="step-4-connect-tooan-application-insights-resource"></a>4 단계: tooan Application Insights 리소스를 연결 합니다.

toocomplete이이 단계에서는 리소스에 대 한 응용 프로그램 ID와 API 키가 필요 합니다. Hello 다음 다이어그램에에서 나와 있는 것 처럼 hello Azure 포털에서에서 해당를 검색할 수 있습니다.

![Hello Azure 포털에서에서 응용 프로그램 ID](./media/app-insights-automate-with-flow/appid.png) 

- Hello 응용 프로그램 ID와 API 키와 함께 사용자의 연결에 대 한 이름을 제공 합니다.

    ![Microsoft Flow 연결 창](./media/app-insights-automate-with-flow/flow3.png)

### <a name="step-5-specify-hello-analytics-query-and-chart-type"></a>5 단계: hello 분석 쿼리 및 차트 종류를 지정 합니다.
다음 쿼리 예에서는 마지막 날 hello 내에서 실패 하는 hello 요청을 선택 하 상호 관련 시켜 hello 작업의 일부로 발생 하는 예외입니다. 분석은 hello operation_Id 식별자에 따라 상관 관계를 지정 합니다. 그런 다음 hello 쿼리 hello autocluster 알고리즘을 사용 하 여 hello 결과 분할 합니다. 

사용자 고유의 쿼리를 만드는 경우를 정상적으로 작동 하는지 분석에서 tooyour 흐름 추가 하기 전에 확인 합니다.

- Hello 다음 분석 쿼리를 추가 하 고 hello HTML 테이블 차트 종류를 선택 합니다. 

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
    
    ![Analytics 쿼리 구성 창](./media/app-insights-automate-with-flow/flow4.png)

### <a name="step-6-configure-hello-flow-toosend-email"></a>6 단계: hello 흐름 toosend 전자 메일 구성

1. **새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.
2. **Office 365 Outlook**을 검색합니다.
3. **Office 365 Outlook – 메일 보내기**를 클릭합니다.

    ![Office 365 Outlook 선택 창](./media/app-insights-automate-with-flow/flow2b.png)

4. Hello에 **전자 메일 보내기** 창에서 다음 hello지 않습니다.

   a. Hello 수신자의 hello 전자 메일 주소를 입력 합니다.

   b. Hello 전자 메일의 제목을 입력 합니다.

   c. Hello에서 아무 곳 이나 클릭 **본문** 상자를 선택한 다음 선택 hello 동적 콘텐츠 메뉴에서 hello 오른쪽에 열리는 **본문**합니다.

   d. **고급 옵션 표시**를 클릭합니다.

    ![Office 365 Outlook 구성](./media/app-insights-automate-with-flow/flow5.png)

5. 동적 콘텐츠 메뉴 hello에서 수행 hello 다음:

    a. **첨부 파일 이름**을 선택합니다.

    b. **첨부 파일 콘텐츠**를 선택합니다.
    
    c. Hello에 **은 HTML** 상자 **예**합니다.

    ![Office 365 메일 구성 창](./media/app-insights-automate-with-flow/flow7.png)

### <a name="step-7-save-and-test-your-flow"></a>7단계: 흐름 저장 및 테스트
- Hello에 **흐름 이름** 상자, 프로그램 흐름에 대 한 이름을 추가 하 고 클릭 **흐름을 만드는**합니다.

    ![흐름 만들기 창](./media/app-insights-automate-with-flow/flow8.png)

이 작업 트리거 toorun hello에 대 한 대기 수 또는 hello 흐름으로 즉시 실행할 수 있습니다 [필요에 따라 실행 중인 hello 트리거](https://flow.microsoft.com/blog/run-now-and-six-more-services/)합니다.

Hello 흐름 실행 되 면 hello hello 전자 메일 목록에 지정 된 받는 사람은 hello 다음 처럼 보이는 전자 메일 메시지:

![샘플 메일](./media/app-insights-automate-with-flow/flow9.png)


## <a name="next-steps"></a>다음 단계

- [Analytics 쿼리](app-insights-analytics-using.md) 만들기에 대해 자세히 알아봅니다.
- [Microsoft Flow](https://ms.flow.microsoft.com)에 대해 자세히 알아봅니다.



<!--Link references-->





