---
제목: aaa "Azure Analysis Services 자습서 단원 4: 관계 만들기 | Microsoft Docs "설명: 방법을에서 toocreate 관계 hello Azure Analysis Services tutorial 프로젝트에 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-4-create-relationships"></a>단원 4: 관계 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 데이터를 가져올 때 자동으로 생성 된 hello 관계 확인 및 서로 다른 테이블 간에 새 관계를 추가 합니다. 관계는 hello 테이블의 데이터는 해야 상관 관계를 설정 하는 두 테이블 간의 연결입니다. 예를 들어 hello DimProduct 테이블과 DimProductSubcategory 테이블 hello 관계가 각 제품 하위 범주 tooa 속함을 hello 팩트를 기반 합니다. toolearn 더 참조 [관계](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular)합니다.
  
이 단원에서는 시간 toocomplete 예상: **10 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [3 단원: 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)합니다. 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>기존 관계 검토 및 새 관계 추가  
데이터 가져오기를 사용 하 여 데이터를 가져올 때 hello AdventureWorksDW2014 데이터베이스에서 7 개의 테이블을 가져왔습니다. 일반적으로 관계형 원본에서 데이터를 가져올 때 기존 관계 없는 hello 데이터와 함께 자동으로 가져옵니다. 그러나 모델 작성을 진행하기 전에 테이블 간의 관계가 적절히 생성되었는지 확인해야 합니다. 이 자습서에서는 3가지 새로운 관계를 추가합니다.  
  
#### <a name="tooreview-existing-relationships"></a>tooreview 기존 관계  
  
1.  Hello 클릭 **모델** 메뉴 > **모델 뷰** > **다이어그램 보기**합니다.  

    hello 모델 디자이너에에서 표시 됩니다 줄 사이 사용 하 여 가져온 모든 hello 테이블을 표시 하는 그래픽 형식 다이어그램 보기. 테이블 사이의 hello 줄 hello 데이터를 가져올 때 자동으로 생성 된 hello 관계를 나타냅니다.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Hello 모델 디자이너의 오른쪽 아래 모서리 hello에에서 미니 맵 컨트롤을 사용 하 여 hello 테이블을 가능한 한 많은 포함 됩니다. 또한 클릭 하 고 곧 제공 될 테이블을 함께 취합 또는 특정 순서 대로 놓습니다 테이블 toodifferent 위치를 끌면 수 있습니다. 테이블 이동 hello 이미 hello 테이블 관계에는 영향을 주지 않습니다. tooview 특정 테이블의 모든 hello 열 클릭 하 고 테이블 가장자리 tooexpand을 끌어 하거나 축소 합니다.  
  
2.  Hello 사이의 실선 hello 클릭 **DimCustomer** 테이블과 hello **DimGeography** 테이블입니다. 이러한 두 테이블 사이의 실선 hello를 보여 줍니다이 관계는 활성 상태 이면 즉, DAX 수식을 계산할 때 기본적으로 사용 됩니다.  
  
    공지 hello **GeographyKey** 열 hello에 **DimCustomer** 테이블과 hello **GeographyKey** 열 hello에 **DimGeography** 테이블 이제 모두 각각 상자 내에 표시 합니다. 이러한 열은 hello 관계에 사용 됩니다. hello 관계의 속성 항목에 표시 됨 hello **속성** 창.  
  
    > [!TIP]  
    > 또한 toousing hello 다이어그램 뷰에서 모델 디자이너, hello 관계 관리 대화 상자 tooshow hello 모든 테이블 간의 관계는 테이블 형식으로 사용할 수도 있습니다. 테이블 형식 모델 탐색기에서 **관계** > **관계 관리**를 마우스 오른쪽 단추로 클릭합니다.
  
3.  관계를 따라 hello 때 생성 되었는지 확인 hello AdventureWorksDW 데이터베이스에서 가져온 각 hello 테이블:  
  
    |Active|테이블|관련된 조회 테이블|  
    |----------|---------|------------------------|  
    |예|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |예|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |예|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |예|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |예|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Hello 관계 중 누락 된 경우 다음 표는 hello 모델에 포함 되어 있는지 확인: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory, 및 FactInternetSales 합니다. 테이블에 동일한 데이터 원본 연결 가져와집니다 hello에서 시간을 구분 하는 경우 해당 테이블 간의 관계는 생성 되지 않으며 수동으로 만들어야 합니다.  

### <a name="take-a-closer-look"></a>자세히 보기
다이어그램 보기에서 화살표는 별표 및 테이블 간의 hello 관계를 보여 주는 hello 줄에서 번호를 확인 합니다.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

hello 화살표는 hello 필터 방향을 나타냅니다. hello 별표가이 테이블은 ' 다 ' 쪽 hello 관계의 카디널리티에 hello 및 hello 한 표시이 테이블은 hello hello 관계의 한 쪽을 표시 합니다. 관계; tooedit 해야 할 경우 예를 들어 hello 관계 필터 방향 나 카디널리티 변경, hello 관계 선 tooopen hello 관계 편집 대화 상자를 두 번 클릭 합니다.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

이러한 기능은 고급 데이터 모델링을 위한 되며이 자습서의 외부 hello 범위. toolearn 더 참조 [양방향 교차 필터에서 Analysis Services 테이블 형식 모델에 대 한](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services)합니다.

경우에 따라 모델 toosupport의 테이블 간에 관계를 추가로 toocreate 특정 비즈니스 논리를 할 수 있습니다. 이 자습서에서는 toocreate 3 개 간에 관계를 추가로 hello FactInternetSales 테이블과 DimDate 테이블 hello 필요합니다.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>테이블 간에 새로운 관계 tooadd  
  
1.  Hello의 hello 모델 디자이너에서 **FactInternetSales** 테이블을 클릭 한 채로 hello **OrderDate** 열에 있으면 드래그 hello 커서 toohello **날짜** hello 의에서열 **DimDate** 테이블을 마우스를 놓습니다.  

    Hello 간에 활성 관계를 만들었음을 보여 주는 실선이 나타납니다 **OrderDate** 열 hello에 **인터넷 판매** 테이블과 hello **날짜** hello의 열 **날짜** 테이블입니다. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > 관계를 만들 때 hello 기본 테이블과 hello 관련된 조회 테이블 간에 hello 카디널리티 및 필터 방향은 자동으로 선택 됩니다.  
  
2.  Hello에 **FactInternetSales** 테이블을 클릭 한 채로 hello **DueDate** 열에 있으면 드래그 hello 커서 toohello **날짜** 열 hello에 **DimDate** 테이블을 마우스를 놓습니다.  
  
    Hello 간에 비활성 관계를 만들었음을 보여 주는 점선이 나타납니다 **DueDate** 열 hello에 **FactInternetSales** 테이블과 hello **날짜** 의 열 hello **DimDate** 테이블입니다. 테이블 간에 여러 관계를 포함할 수 있지만 한 번에 하나의 관계만 활성화될 수 있습니다. 비활성 관계는 사용자 지정 하는 DAX 식에서 활성 tooperform 특별 한 집계 만들 수 있습니다.  
  
3.  마지막으로 관계를 하나 더 만듭니다. Hello에 **FactInternetSales** 테이블을 클릭 한 채로 hello **ShipDate** 열에 있으면 드래그 hello 커서 toohello **날짜** 열 hello에 **DimDate** 테이블을 마우스를 놓습니다.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>다음 작업
[단원 5: 계산된 열 만들기](../tutorials/aas-lesson-5-create-calculated-columns.md)
  
  
  
