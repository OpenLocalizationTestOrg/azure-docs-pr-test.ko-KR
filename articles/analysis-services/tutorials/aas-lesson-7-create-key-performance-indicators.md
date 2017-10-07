---
제목: aaa "7 Azure Analysis Services 자습서 단원: 핵심 성과 지표 만들기 | Microsoft Docs "설명: 방법을 toocreate 핵심 성과 지표의 hello Azure Analysis Services tutorial 프로젝트에 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>단원 7: 핵심 성과 지표 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 KPI(핵심 성과 지표)를 만듭니다. Kpi는 정의 된 값의 사용 되는 toogauge 성능을 *자료* 측정값에 대해는 *대상* 측정값으로 또는 절대값으로 정의 된 값입니다. 보고 클라이언트 응용 프로그램을 쉽고 빠르게 toounderstand 비즈니스의 성공 또는 tooidentify 추세의 요약이 Kpi 경영진이 제공할 수 있습니다. toolearn 더 참조 [Kpi](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
이 단원에서는 시간 toocomplete 예상: **15 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [6 단원: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)합니다.   
  
## <a name="create-key-performance-indicators"></a>핵심 성과 지표 만들기  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate InternetCurrentQuarterSalesPerformance KPI  
  
1.  Hello 모델 디자이너에서 클릭 hello **FactInternetSales** 테이블입니다.  
  
2.  Hello 측정값 표에서 빈 셀을 클릭 합니다.  
  
3.  Hello 테이블 위에 hello 수식 입력줄에 다음 수식을 hello를 입력 합니다. 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    이 측정값 hello hello KPI 기본 측정값으로 사용 됩니다.  
  
4.  **InternetCurrentQuarterSalesPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.   
  
5.  Hello KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.1**합니다.  
  
7.  Hello 왼쪽된 (아래쪽) 슬라이더 필드에 입력 **1**, 한 다음 hello 오른쪽 (위쪽) 슬라이더 필드를 입력 **1.07**합니다.  
  
8.  **아이콘 스타일 선택**원 (녹색) 아이콘 유형의 hello 다이아몬드 (빨간색), 삼각형 (노란색)를 선택 합니다.
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > 확장 가능한 알림 hello **설명** hello 가능한 아이콘 스타일 아래에 레이블을 합니다. Hello에 대 한 설명을 사용 하 여 다양 한 KPI 요소 toomake을 클라이언트 응용 프로그램에서 쉽게 식별할 수 있습니다.  
  
9. 클릭 **확인** toocomplete hello KPI입니다.  
  
    Hello 측정값 표의 hello 아이콘 다음 toohello 확인 **InternetCurrentQuarterSalesPerformance** 측정값입니다. 이 아이콘은 이 측정값이 KPI에 대한 기본값으로 제공됨을 나타냅니다.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate InternetCurrentQuarterMarginPerformance KPI  
  
1.  Hello에 대 한 측정값 표에서 hello **FactInternetSales** 테이블에서 빈 셀을 클릭 합니다.  
  
2.  Hello 테이블 위에 hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  **InternetCurrentQuarterMarginPerformance** > **KPI 만들기**를 마우스 오른쪽 단추로 클릭합니다.  
  
4.  Hello KPI 핵심 성과 지표 () 대화 상자에서에 **대상** 선택 **절대값**, 한 다음 입력 **1.25**합니다.   
  
5.  Hello 필드 표시 될 때까지 슬라이드 hello 왼쪽된 (아래쪽) 슬라이더 필드에서 **0.8**, 및 hello 필드 표시 될 때까지 다음 슬라이드 hello 오른쪽 (높음) 슬라이더 필드 **1.03**합니다.  
  
6.  **아이콘 스타일 선택**, hello 다이아몬드 (빨간색), 삼각형 (노란색), 원 (녹색) 아이콘 유형을 선택한 다음 클릭 **확인**합니다.  
  
## <a name="whats-next"></a>다음 작업
[단원 8: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)
  
  
