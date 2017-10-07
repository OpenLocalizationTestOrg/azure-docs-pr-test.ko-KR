---
제목: aaa "Azure Analysis Services tutorial 추가 단원: 비정형 계층 | Microsoft Docs "설명: toofix hello Azure Analysis Services 자습서의 계층 구조를 정렬 하는 방법에 대해 설명 합니다.
서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>추가 단원 - 불규칙한 계층 구조

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 추가 단원에서는 다양한 수준에서 빈 값(멤버)을 포함하는 계층 구조를 피벗할 때 발생하는 일반적인 문제를 해결합니다. 예를 들어, 고위 관리자가 부하 직원으로 부서별 관리자와 비관리자를 포함하는 조직을 들 수 있습니다. 또는 워싱턴 D.C., 바티칸 시티처럼 일부 도시는 상위 시/도가 없는 국가-지역-도시로 구성된 지리적 계층 구조가 있습니다. 계층에 구성원이 비어 있는 경우 종종 toodifferent, 상속 또는 비정형 수준입니다.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Hello 1400 호환성 수준에서 테이블 형식 모델은 추가 **멤버 숨기기** 계층에 대 한 속성입니다. hello **기본** 설정에서는 빈 멤버가 모든 수준에서 한다고 가정 합니다. hello **빈 멤버를 숨기도록** 설정을 추가할 때 hello 계층에서 빈 멤버를 제외 시킵니다. tooa 피벗 테이블 또는 보고서입니다.  
  
이 단원에서는 시간 toocomplete 예상: **20 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함됩니다. 이 추가 단원 hello 작업을 수행 하기 전에 완료 해야 이전 단원을 모두 완료 된 Adventure Works Internet Sales 샘플 모델 프로젝트 수도 있고 합니다. 

Hello AW Internet Sales 프로젝트 hello 자습서의 일부로 만든 모델에 아직 없는 경우 데이터 나 비정형된 계층이 합니다. toocomplete이 추가 단원에서는 먼저 있는 toocreate 몇 가지 추가 테이블을 추가 하 여 문제를 hello, 관계, 계산된 열, 측정값 및 새로운 조직 계층을 만듭니다. 이 부분에는 약 15분 정도 걸립니다. Toosolve를 가져온 후, 단 몇 분 후에 해당 합니다.  

## <a name="add-tables-and-objects"></a>테이블 및 개체 추가
  
### <a name="tooadd-new-tables-tooyour-model"></a>tooadd 새 테이블 tooyour 모델
  
1.  테이블 형식 모델 탐색기에서 **데이터 원본**을 확장한 후 연결을 마우스 오른쪽 단추로 클릭한 다음 > **새 테이블 가져오기**를 클릭합니다.
  
2.  탐색기에서 **DimEmployee** 및 **FactResellerSales**를 클릭하고 **확인**을 클릭합니다.

3.  쿼리 편집기에서 **가져오기**를 클릭합니다.

4.  Hello 다음 만들기 [관계](../tutorials/aas-lesson-4-create-relationships.md):

    | 표 1           | 열       | 필터 방향   | 표 2     | 열      | Active |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | 기본값            | DimDate     | Date        | 예    |
    | FactResellerSales | DueDate      | 기본값            | DimDate     | Date        | 아니요     |
    | FactResellerSales | ShipDateKey  | 기본값            | DimDate     | Date        | 아니요     |
    | FactResellerSales | ProductKey   | 기본값            | DimProduct  | ProductKey  | 예    |
    | FactResellerSales | EmployeeKey  | tooBoth 테이블 | DimEmployee | EmployeeKey | 예    |

5. Hello에 **DimEmployee** 테이블에서 만들 hello 다음 [계산 된 열](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Path** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  Hello에 **DimEmployee** 테이블을 만들기는 [계층](../tutorials/aas-lesson-9-create-hierarchies.md) 라는 **조직**합니다. 다음 순서 대로 열 hello 추가: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**합니다.

7.  Hello에 **FactResellerSales** 테이블에서 만들 hello 다음 [측정값](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  사용 하 여 [Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel 피벗 테이블을 자동으로 만듭니다.

9.  **피벗 테이블 필드**, hello 추가 **조직** hello 계층 **DimEmployee** 너무 테이블**행**, 및 hello **ResellerTotalSales** hello에서 측정값 **FactResellerSales** 너무 테이블**값**합니다.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Hello 피벗 테이블에서에서 볼 수 있습니다, hello 계층 구조는 비정형 않은 행을 표시 합니다. 빈 멤버가 표시된 많은 행이 있습니다.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>hello 숨기기 멤버 속성을 설정 하 여 toofix hello 비정형 계층

1.  **테이블 형식 모델 탐색기**에서 **테이블** > **DimEmployee** > **계층 구조** > **조직**을 확장합니다.

2.  **속성** > **멤버 숨기기**에서 **빈 멤버 숨기기**를 선택합니다. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  Excel에서 다시 hello를 피벗 테이블을 새로 고칩니다. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    이제 훨씬 좋아 보입니다.

## <a name="see-also"></a>참고 항목   
[단원 9: 계층 구조 만들기](../tutorials/aas-lesson-9-create-hierarchies.md)  
[추가 단원 - 동적 보안](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[추가 단원 - 세부 정보 행](../tutorials/aas-supplemental-lesson-detail-rows.md)  