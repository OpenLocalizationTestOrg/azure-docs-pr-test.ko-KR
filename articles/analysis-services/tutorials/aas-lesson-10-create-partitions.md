---
제목: aaa "10 Azure Analysis Services 자습서 단원: 파티션 만들기 | Microsoft Docs "설명: toocreate hello Azure Analysis Services tutorial 프로젝트에서 분할 하는 방법에 대해 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-10-create-partitions"></a>단원 10: 파티션 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 처리 (새로 고침된) 다른 파티션과 별개로 될 수 있는 더 작은 논리적 부분으로 파티션을 toodivide hello FactInternetSales 테이블을 만듭니다. 기본적으로 모델에 포함할 모든 테이블에는 모든 hello 테이블의 열과 행을 포함 하는 파티션이 하나 있습니다. Hello FactInternetSales 테이블에 대 한 연도별; toodivide hello 데이터 원합니다 각 5 년 hello 테이블에 대해 하나의 파티션을 합니다. 그러면 각 파티션은 독립적으로 처리할 수 있습니다. toolearn 더 참조 [파티션을](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular)합니다. 
  
이 단원에서는 시간 toocomplete 예상: **15 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [9 단원: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)합니다.  
  
## <a name="create-partitions"></a>파티션 만들기  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>hello FactInternetSales 테이블에서 파티션의 toocreate  
  
1.  테이블 형식 모델 탐색기에서 **테이블**를 확장하고 **FactInternetSales** > **파티션**을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  파티션 관리자에서 클릭 **복사**를 바꾼 다음 hello 이름이 너무**FactInternetSales2010**합니다.
  
    하려고 하기 때문에 파티션 tooinclude hello는 행만 hello 연도 2010에 대 한 특정 기간 내 hello 쿼리 식을 수정 해야 합니다.
  
4.  클릭 **디자인** tooopen 쿼리 편집기와 hello 클릭 **FactInternetSales2010** 쿼리 합니다.

5.  미리 보기에서 아래쪽 화살표를 hello hello 클릭 **OrderDate** 열 머리글을 클릭 한 다음 **날짜/시간 필터** > **사이의**합니다.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Hello 행 필터 대화 상자에서에서 **인 경우 행 표시: OrderDate**, 둡니다 **이후 또는 같음**, hello 날짜 필드에 입력 한 다음 **1/1/2010**합니다. Hello 둡니다 **및** 연산자를 선택 하면 다음 선택 **앞**, hello 날짜 필드에 입력 한 다음 **2011/1/1**, 클릭 하 고 **확인**합니다.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    쿼리 편집기의 적용 단계에서 필터링된 행이라는 다른 단계가 표시됩니다. 이 필터는 2010에서 tooselect만 주문 날짜입니다.

8.  **가져오기**를 클릭합니다.

    파티션 관리자는 이제 식에 추가 행 필터링 절 hello 쿼리를 확인 합니다.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    이 문은이 파티션에 hello OrderDate는 hello에서 2010 년 hello 필터링 된 rows 절에 지정 된 대로 행의 hello 데이터만 포함 하도록 지정 합니다.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>2011 년 hello에 대 한 파티션 toocreate  
  
1.  Hello 파티션 목록에서 클릭 hello **FactInternetSales2010** 작성 한을 분할 하 고 클릭 **복사**합니다.  Hello 파티션 이름에도 변경**FactInternetSales2011**합니다. 

    쿼리 편집기 toocreate 새 필터링 된 행 절 toouse가 필요가 없습니다. 2010에 대 한 hello 쿼리의 복사본을 만들 때 toodo 가장 필요한 것 이므로 2011 용 hello 쿼리에서 코드를 약간만 변경 합니다.
  
2.  **쿼리 식**, 순서로 파티션 tooinclude이에 대 한 hello에 대 한 행만 2011 연도, 사용 된 hello 행 필터링 절에서 hello 연도 대체 **2011** 및 **2012**에서 위와 같은:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>2012, 2013 및 2014에 대 한 toocreate 파티션.  
  
- 2012, 2013 및 2014 년 hello 년 hello 행 필터링 절 tooinclude만 행에 해당 연도 대 한 변경에 대 한 파티션을 만들면 그 hello 이전 단계를 따릅니다. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Hello FactInternetSales 파티션을 삭제합니다
각 연도 대 한 파티션을가지고 hello FactInternetSales 파티션을;을 삭제할 수 있습니다. 파티션을 처리할 때 모든 프로세스를 선택할 때 겹침을 방지 합니다.

#### <a name="toodelete-hello-factinternetsales-partition"></a>toodelete hello FactInternetSales 파티션
-  Hello FactInternetSales 파티션을 클릭 한 다음 클릭 **삭제**합니다.



## <a name="process-partitions"></a>파티션 처리  
파티션 관리자에서 확인 hello **마지막 처리** 이러한 파티션을 처리 하지 않은 표시를 생성 하는 hello 새 파티션 각각에 대 한 열입니다. 파티션을 만들 때 해당 파티션을에서 파티션 처리 또는 테이블 처리 작업 toorefresh hello 데이터를 실행 해야 합니다.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess hello FactInternetSales 파티션  
  
1.  클릭 **확인** tooclose 파티션 관리자입니다.  
  
2.  Hello 클릭 **FactInternetSales** 테이블을 클릭 hello **모델** 메뉴 > **프로세스** > **파티션 처리**합니다.  
  
3.  Hello 파티션 처리 대화 상자에서 확인 **모드** 너무 설정**기본값 처리**합니다.  
  
4.  Hello에 hello 확인란을 선택 **프로세스** 생성 하 고 클릭 한 다음 각 5 hello에 대 한 열 파티션 **확인**합니다.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    가장 자격 증명을 묻는 hello Windows 사용자 이름 및 2 단원에서에서 지정한 암호를 입력 합니다.  
  
    hello **데이터 처리** 대화 상자가 나타나고 각 파티션에 대 한 처리 정보가 표시 됩니다. 파티션마다 서로 다른 행 수가 전송된 것을 알 수 있습니다. 각 파티션은 hello hello SQL 문의 WHERE 절에에서 지정 된 hello 연도 대 한 행만 포함 합니다. 처리가 완료 되 면 계속 진행 하 고 hello 데이터 처리 대화 상자를 닫습니다.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>다음 작업
다음 단원 이동 toohello: [11 단원: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)합니다. 
