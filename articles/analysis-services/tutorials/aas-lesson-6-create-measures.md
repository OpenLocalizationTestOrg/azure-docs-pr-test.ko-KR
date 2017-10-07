---
제목: aaa "6 Azure Analysis Services 자습서 단원: 측정값 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트에 측정 하는 방법에 대해 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-6-create-measures"></a>단원 6: 측정값 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 모델에 포함할 측정값 toobe를 만들 수 있습니다. 비슷한 toohello 계산 만든 열, 측정값은 DAX 수식을 사용 하 여 만든 계산입니다. 그러나 계산된 열과 달리 측정값은 사용자가 선택한 *필터*를 기반으로 평가됩니다. 예를 들어 특정 열 이나 슬라이서 toohello 행 레이블 필드 피벗 테이블에 추가 합니다. Hello 필터의 각 셀에 대 한 값이 적용 된 hello 측정값으로 계산 됩니다. 측정값은 숫자 데이터에 대해 거의 모든 테이블 형식 모델 tooperform 동적 계산에서 tooinclude 되도록 하는 강력 하 고 유연한 계산입니다. toolearn 더 참조 [측정값](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular)합니다.
  
hello를 사용 하면 toocreate 측정값 *측정값 표*합니다. 기본적으로 각 테이블에는 빈 측정값 표가 있습니다. 그러나 일반적으로 모든 테이블에 대해 측정값을 만들지 않습니다. 데이터 보기 hello 모델 디자이너에서 테이블 아래 hello 측정값 표가 나타납니다. 표시 / toohide hello 측정값 표는 테이블에 대 한 클릭 hello **테이블** 메뉴를 차례로 클릭 **측정값 표 표시**합니다.  
  
Hello 측정값 표에서 빈 셀을 클릭 하 고 hello 수식 입력줄에 DAX 수식을 입력 하 여 측정값을 만들 수 있습니다. ENTER toocomplete hello 수식 hello 측정값 클릭 후 hello 셀에 나타납니다. 열을 클릭 하 여 표준 집계 함수를 사용 하 여 측정값을 만들 수 있습니다 및 자동 합계 단추 hello 클릭 한 다음 (**∑**) hello 도구 모음입니다. Hello 자동 합계 기능을 이용해 만든 측정값 hello 측정값 표 셀 hello 열 바로 아래에 표시 되지만 이동할 수 있습니다.  
  
이 단원에서는 둘 다 DAX 수식을 입력 hello 수식 입력줄에 고 hello 자동 합계 기능을 사용 하 여 측정값을 만듭니다.  
  
이 단원에서는 시간 toocomplete 예상: **30 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [5 단원: 계산된 열 만들기](../tutorials/aas-lesson-5-create-calculated-columns.md)합니다.  
  
## <a name="create-measures"></a>측정값 만들기  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>toocreate hello DimDate 테이블의 DaysCurrentQuarterToDate 측정값  
  
1.  Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블입니다.  
  
2.  Hello 측정값 표의 hello 왼쪽 위 빈 셀을 클릭 합니다.  
  
3.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    공지 hello 왼쪽 위 셀에는 이제 측정값 이름 포함 **DaysCurrentQuarterToDate**hello 결과 **92**합니다.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    측정값 수식으로 계산 된 열과 달리 hello 측정값 이름, 밑줄 hello 수식 식 뒤에 오는 콜론을 입력할 수 있습니다.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>toocreate hello DimDate 테이블의 DaysInCurrentQuarter 측정값  
  
1.  Hello로 **DimDate** hello 측정값 표의 hello 모델 디자이너에서 계속 활성 상태 테이블을 hello 만든 hello 측정값 아래의 빈 셀을 클릭 합니다.  
  
2.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    이 이전 기간의 불완전 한 기간과 hello 사이의 비교 비율을 만들 때는 hello 수식은 경과 된 hello 기간의 hello 비율을 계산 하 고 toohello 이전 기간의 hello에는 동일한 비율을 비교 해야 합니다. 이 경우 [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] 제공 hello 비율 hello 현재 기간 경과 합니다.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate hello FactInternetSales 테이블의 한 InternetDistinctCountSalesOrder 측정값  
  
1.  Hello 클릭 **FactInternetSales** 테이블입니다.   
  
2.  Hello 클릭 **SalesOrderNumber** 열 머리글입니다.  
  
3.  Hello 도구 모음에서 hello 아래쪽 화살표 다음 toohello 자동 합계 (**∑**) 단추를 선택한 다음 선택 **DistinctCount**합니다.  
  
    hello 자동 합계 기능은 DistinctCount 표준 집계 수식을 hello를 사용 하 여 hello 선택한 열에 대 한 측정값을 자동으로 만듭니다.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Hello 측정값 표의 hello 새 측정값을 클릭 한 다음 hello **속성** 창, **측정값 이름**, 너무 hello 측정값 이름을 바꿀**InternetDistinctCountSalesOrder**합니다. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>hello FactInternetSales 테이블에서 추가 측정이 toocreate  
  
1.  Hello 자동 합계 기능을 사용 하 여 만들고 hello 다음 측정값 이름을 지정 합니다.  

    |열|측정값 이름|자동 합계(∑)|수식|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|개수|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|합계|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|합계|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|합계|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|합계|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|합계|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|합계|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|합계|=SUM([Freight])|  
  
2.  클릭 하 여 hello 측정값 표의 및 hello 수식 입력줄을 사용 하 여 빈 셀, 만들고 hello 다음 이름을 순서 대로 측정 합니다.  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Hello FactInternetSales 테이블에 대해 만든 측정값 매출, 비용, 이익률 hello 사용자가 선택한 필터로 필터링 된 항목 등 중요 한 재무 데이터를 사용 하는 tooanalyze 수 있습니다.  
  
## <a name="whats-next"></a>다음 작업
[단원 7: 핵심 성과 지표 만들기](../tutorials/aas-lesson-7-create-key-performance-indicators.md)  

  
