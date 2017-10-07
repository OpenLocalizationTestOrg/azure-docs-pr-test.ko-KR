---
제목: aaa "9 Azure Analysis Services 자습서 단원: 계층 만들기 | Microsoft Docs "설명: 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-9-create-hierarchies"></a>단원 9: 계층 구조 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 계층 구조를 만듭니다. 계층 구조는 수준별로 정렬된 열 그룹입니다. 예를 들어 Geography 계층 구조는 Country, State, County 및 City에 대한 하위 수준을 포함할 수 있습니다. 계층 더 쉽게 클라이언트에 대 한 사용자가 toonavigate 보고 클라이언트 응용 프로그램 필드 목록에서 다른 열과에서는 별도로 표시 및 보고서에 포함할 수 있습니다. toolearn 더 참조 [계층](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
toocreate 계층 hello 모델 디자이너에서 사용 하 여 *다이어그램 보기*합니다. 데이터 뷰에서 계층 구조 만들기 및 관리는 지원되지 않습니다.  
  
이 단원에서는 시간 toocomplete 예상: **20 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [8 단원: 큐브 뷰 만들기](../tutorials/aas-lesson-8-create-perspectives.md)합니다.  
  
## <a name="create-hierarchies"></a>계층 구조 만들기  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>toocreate hello DimProduct 테이블의 범주 계층  
  
1.  Hello를 마우스 오른쪽 단추로 클릭 hello 모델 디자이너 (다이어그램 뷰)에서 **DimProduct** 테이블 > **계층 만들기**합니다. 새 계층 hello hello 테이블 창의 맨 아래에 나타납니다. Hello 계층 이름 바꾸기 **범주**합니다.  
  
2.  클릭 하 고 hello 끌어 **ProductCategoryName** 새 열 toohello **범주** 계층 구조입니다.  
  
3.  Hello에 **범주** 계층, 마우스 오른쪽 단추로 클릭 hello **ProductCategoryName** > **이름 바꾸기**, 한 다음 입력 **범주**합니다.  
  
    > [!NOTE]  
    > 계층의 열 이름 바꾸기 hello 테이블의 해당 열은 바뀌지 않습니다. 계층의 열은 hello 열 hello 테이블에 대 한 표현일 뿐입니다.  
  
4.  클릭 하 고 hello 끌어 **ProductSubcategoryName** 열 toohello **범주** 계층 구조입니다. **Subcategory**로 이름을 바꿉니다. 
  
5.  마우스 오른쪽 단추로 클릭 hello **ModelName** 열 > **toohierarchy 추가**를 선택한 후 **범주**합니다. **Model**로 이름을 바꿉니다.

6.  마지막으로 추가 **EnglishProductName** toohello 범주 계층입니다. **Product**로 이름을 바꿉니다.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>hello DimDate 테이블에서 toocreate 계층  
  
1.  Hello에 **DimDate** 테이블, 명명 된 계층 구조를 만들 **달력**합니다.  
  
3.  Hello 다음 순서 대로 열을 추가 합니다.

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Hello에 **DimDate** 테이블을 만들기는 **회계** 계층 구조입니다. 다음 순서 대로 열 hello를 다음과 같습니다.  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Hello에 마지막으로, **DimDate** 테이블을 만들기는 **ProductionCalendar** 계층 구조입니다. 다음 순서 대로 열 hello를 다음과 같습니다.  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>다음 작업
[단원 10: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md) 
  
  
