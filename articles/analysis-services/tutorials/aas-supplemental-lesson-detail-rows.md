---
제목: aaa "Azure Analysis Services tutorial 추가 단원: 정보 행 | Microsoft Docs "설명: toocreate 세부 행 식에는 Azure Analysis Services 자습서 hello 하는 방법에 대해 설명 합니다.
서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>추가 단원 - 세부 정보 행

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 추가 단원에서는 DAX 편집기 toodefine hello는 사용자 지정 세부 행 식을 사용 합니다. 세부 정보 행 식 최종 사용자에 게 hello 집계 결과 측정값에 대 한 자세한 정보를 제공 하는 측정값에 속성입니다. 
  
이 단원에서는 시간 toocomplete 예상: **10 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다. 이 추가 단원 hello 작업을 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다.  
  
## <a name="what-do-we-need-toosolve"></a>수행할 작업 toosolve 필요?
세부 정보 행 식을 추가 하기 전에 InternetTotalSales 측정값의 hello 세부 정보에 살펴보겠습니다.

1.  SSDT에서는 hello 클릭 **모델** 메뉴 > **Excel에서 분석** tooopen Excel 빈 피벗 테이블을 만듭니다.
  
2.  **피벗 테이블 필드**, hello 추가 **InternetTotalSales** 너무 hello FactInternetSales 테이블에서 측정**값**, **CalendarYear**hello DimDate 테이블에서 너무**열**, 및 **EnglishCountryRegionName** 너무**행**합니다. 이 피벗 테이블 이제 목록에 집계 된 결과 영역 및 연도별 hello InternetTotalSales 측정값에서 있습니다. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Hello 피벗 테이블에서 지역 이름과 1 년에 대 한 집계 값을 두 번 클릭 합니다. 여기에서는 두 번 클릭 hello 값 오스트레일리아 및 hello에 대 한 2014 년입니다. 데이터가 포함된 새 시트가 열리지만 유용한 데이터가 아닙니다.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
여기 toosee toohello 기여 하는 데이터의 열과 행을 포함 하는 테이블 처럼 사람이 무엇 InternetTotalSales 측정값의 결과 집계 합니다. toodo을, hello 측정값의 속성으로 정보 행 식을 추가할 수 있습니다.

## <a name="add-a-detail-rows-expression"></a>세부 정보 행 식 추가

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate 세부 행 식 
  
1. SSDT에서는 hello FactInternetSales 테이블의 측정값 표 클릭 hello **InternetTotalSales** 측정값입니다. 

2. **속성** > **세부 행 식**, hello 편집기 단추 tooopen hello DAX 편집기를 클릭 합니다.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. DAX 편집기에서 다음 식은 hello를 입력 합니다.

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    이 식 이름, 열를 지정 하 고 사용자가 피벗 테이블 또는 보고서에는 집계 된 결과 두 번 클릭할 경우 hello FactInternetSales 테이블과 관련된 테이블에서 측정값 결과가 반환 됩니다.

4. 다시 Excel, 3 단계에서에서 만든 hello 시트 삭제 한 후 집계 값을 두 번 클릭 합니다. 이 이번에 hello 측정값에 대해 정의 된 세부 행 식 속성을 새 시트가 열립니다 훨씬 더 유용한 데이터가 포함 된 합니다.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. 모델을 다시 배포합니다.

  
## <a name="see-also"></a>참고 항목  
[SELECTCOLUMNS 함수(DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[추가 단원 - 동적 보안](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[추가 단원 - 불규칙한 계층 구조](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
