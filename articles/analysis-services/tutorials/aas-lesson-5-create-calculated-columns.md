---
제목: aaa "5 Azure Analysis Services 자습서 단원: 계산된 열 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트의 열을 계산 하는 방법을 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-5-create-calculated-columns"></a>단원 5: 계산된 열 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 계산된 열을 추가하여 모델에서 데이터를 만듭니다. (사용자 정의 열)으로 계산 된 열을 만들 수 있습니다 쿼리 편집기 hello를 사용 하 여 가져올 데이터를 사용할 때 또는 나중에 모델 디자이너 같은 hello 있습니다 여기 합니다. toolearn 더 참조 [계산 된 열](https://docs.microsoft.com/sql/analysis-services/tabular-models/ssas-calculated-columns)합니다.
  
서로 다른 세 테이블에 5개의 새 계산된 열을 만듭니다. hello 단계는 약간 다른 여러 가지 toocreate 열을 보여 주는 각 작업에 대해, 이름을 바꾸고 테이블의 다양 한 위치에 배치 합니다.  

이 단원에서는 먼저 DAX(Data Analysis Expressions)를 사용합니다. DAX는 테이블 형식 모델에 대해 사용자 지정 가능한 수식을 만드는 특별한 언어입니다. 이 자습서에서는 DAX toocreate 계산 열, 측정값 및 역할 필터를 사용합니다. toolearn 더 참조 [테이블 형식 모델에서 DAX](https://docs.microsoft.com/sql/analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular)합니다. 
  
이 단원에서는 시간 toocomplete 예상: **15 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [4 단원: 관계 만들기](../tutorials/aas-lesson-4-create-relationships.md)합니다. 
  
## <a name="create-calculated-columns"></a>계산된 열 만들기  
  
#### <a name="create-a-monthcalendar-calculated-column-in-hello-dimdate-table"></a>Hello DimDate 테이블에서 MonthCalendar 계산된 열 만들기  
  
1.  Hello 클릭 **모델** 메뉴 > **모델 뷰** > **데이터 뷰**합니다.  
  
    계산 된 열 데이터 뷰에서 hello 모델 디자이너를 사용 하 여 만들 수만 있습니다.  
  
2.  Hello 모델 디자이너에서 클릭 hello **DimDate** 테이블 (탭).  
  
3.  마우스 오른쪽 단추로 클릭 hello **CalendarQuarter** 열 머리글을 클릭 한 다음 **열 삽입**합니다.  
  
    이라는 새 열 **계산 열 1** hello 삽입된 toohello 왼쪽은 **Calendar Quarter** 열입니다.  
  
4.  Hello hello 테이블 위의 수식 입력줄에서 다음 DAX 수식을 hello 입력: 자동 완성 사용 하면 입력 열과 테이블의 정규화 된 이름을 hello 및 목록을 사용할 수 있는 함수와 hello 합니다.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    값이 모든 hello 행 hello 계산된 열에 대해 채워집니다. Hello 테이블을 통해 아래로 스크롤할 경우 행이 열에서 각 행에 hello 데이터에 따라 다른 값을 가질 수 볼 수 있습니다.    
  
5.  이 열을 너무 이름 바꾸기**MonthCalendar**합니다. 

    ![aas-lesson5-newcolumn](../tutorials/media/aas-lesson5-newcolumn.png) 
  
hello MonthCalendar 계산된 열에는 월에 대 한 정렬 가능한 이름을 제공합니다.  
  
#### <a name="create-a-dayofweek-calculated-column-in-hello-dimdate-table"></a>Hello DimDate 테이블의 DayOfWeek 계산된 열 만들기  
  
1.  Hello로 **DimDate** 여전히 활성 상태 테이블에서 hello **열** 메뉴를 차례로 클릭 **열 추가**합니다.  
  
2.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Hello 수식 작성을 마쳤으면 ENTER 키를 누릅니다. 새 열 hello toohello hello 테이블의 맨 오른쪽에 추가 됩니다.  
  
3.  너무 hello 열 이름 바꾸기**DayOfWeek**합니다.  
  
4.  Hello 열 머리글을 클릭 한 다음 hello 간의 hello 열을 끌어 **EnglishDayNameOfWeek** 열과 hello **DayNumberOfMonth** 열입니다.  
  
    > [!TIP]  
    > 테이블에서 열을 이동 하면 더 쉽게 toonavigate 있습니다.  
  
hello DayOfWeek 계산된 열에는 hello 요일에 대 한 정렬 가능한 이름을 제공합니다.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-hello-dimproduct-table"></a>Hello DimProduct 테이블에서 ProductSubcategoryName 계산된 열 만들기  
  
  
1.  Hello에 **DimProduct** 테이블, hello 테이블의 맨 오른쪽 toohello 스크롤합니다. 공지 hello 맨 오른쪽 열 이름이 **열 추가** (기울임꼴) hello 열 머리글을 클릭 합니다.  
  
2.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  너무 hello 열 이름 바꾸기**ProductSubcategoryName**합니다.  
  
hello ProductSubcategoryName 계산된 열에 사용 되는 toocreate hello DimProductSubcategory 테이블에 hello EnglishProductSubcategoryName 열에서 데이터를 포함 하는 hello DimProduct 테이블의 계층 구조입니다. 계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다. 계층 구조는 단원 9에서 나중에 만듭니다.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-hello-dimproduct-table"></a>Hello DimProduct 테이블의 ProductCategoryName 계산된 열 만들기  
  
1.  Hello로 **DimProduct** 여전히 활성 상태 테이블에서 hello **열** 메뉴를 차례로 클릭 **열 추가**합니다.  
  
2.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  너무 hello 열 이름 바꾸기**ProductCategoryName**합니다.  
  
hello ProductCategoryName에 대 한 계산 된 열에 사용 되는 toocreate hello DimProductCategory 테이블에 hello EnglishProductCategoryName 열에서 데이터를 포함 하는 hello DimProduct 테이블의 계층 구조입니다. 계층 구조는 둘 이상의 테이블에 걸쳐 있을 수 없습니다.  
  
#### <a name="create-a-margin-calculated-column-in-hello-factinternetsales-table"></a>Hello FactInternetSales 테이블에서 Margin 계산된 열 만들기  
  
1.  Hello 모델 디자이너에서 선택 hello **FactInternetSales** 테이블입니다.  
  
2.  Hello 사이 새 계산된 열 만들기 **SalesAmount** 열과 hello **TaxAmt** 열입니다.  
  
3.  Hello 수식 입력줄에 다음 수식을 hello를 입력 합니다.  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  너무 hello 열 이름 바꾸기**여백**합니다.  
 
      ![aas-lesson5-newmargin](../tutorials/media/aas-lesson5-newmargin.png)
      
    hello Margin 계산된 열은 사용 되는 tooanalyze 매출 이익률을 각 판매 합니다.  
  
## <a name="whats-next"></a>다음 작업
[단원 6: 측정값 만들기](../tutorials/aas-lesson-6-create-measures.md)
  
  
  
