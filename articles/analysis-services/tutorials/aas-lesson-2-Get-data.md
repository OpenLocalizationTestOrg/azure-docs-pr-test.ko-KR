---
제목: aaa "2 Azure Analysis Services 자습서 단원: 데이터 가져오기 | Microsoft Docs "설명: 방식에서 데이터 가져오기 및 tooget hello Azure Analysis Services tutorial 프로젝트에 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---

# <a name="lesson-2-get-data"></a>단원 2: 데이터 가져오기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 데이터 가져오기 SSDT tooconnect toohello AdventureWorksDW2014 예제 데이터베이스, 데이터 선택, 미리 보기 및 필터를 사용 하 여 한 다음 모델 작업 영역으로 가져옵니다.  
  
데이터 가져오기를 사용하여 Azure SQL Database, Oracle, Sybase, OData Feed, Teradata, 파일 등 다양한 원본에서 데이터를 가져올 수 있습니다. 파워 쿼리 M 수식을 사용하여 데이터를 쿼리할 수도 있습니다.
  
이 단원에서는 시간 toocomplete 예상: **10 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [1 단원: 새 테이블 형식 모델 프로젝트 만들기](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
## <a name="create-a-connection"></a>연결 만들기  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate 연결 toohello AdventureWorksDW2014 데이터베이스  
  
1.  테이블 형식 모델 탐색기에서 **데이터 원본** > **데이터 원본에서 가져오기**를 마우스 오른쪽 단추로 클릭합니다.  
  
    데이터 가져오기에서 연결 tooa 데이터 소스를 안내해 주는 시작 됩니다. 테이블 형식 모델 탐색기에 표시 되지 않는 경우 **솔루션 탐색기**를 두 번 클릭 **Model.bim** hello 디자이너에서 tooopen hello 모델입니다. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  데이터 가져오기에서 **데이터베이스** > **SQL Server 데이터베이스** > **연결**을 클릭합니다.  
  
3.  Hello에 **SQL Server 데이터베이스** 대화에 **서버**, hello AdventureWorksDW2014 데이터베이스를 설치한 hello 서버 hello 이름을 입력 하 고 클릭 **연결**합니다.  

4.  메시지가 표시 되 면 Analysis Services를 가져오고 데이터를 처리할 때 tooconnect toohello 데이터 원본을 사용 하 여 toospecify hello 자격 증명이 필요 tooenter 자격 증명입니다. **가장 모드**에서 **계정 가장**을 선택한 다음 자격 증명을 입력하고 **연결**을 클릭합니다. 계정을 사용 하면 hello 암호 만료 되지 않는 것이 좋습니다.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Windows 사용자 계정 및 암호를 사용 하 여 hello 연결 tooa 데이터 원본의 가장 안전한 방법을 제공 합니다.
  
5.  탐색 창의 hello 선택 **AdventureWorksDW2014** 데이터베이스를 선택한 다음 클릭 **확인**합니다. Hello 연결 toohello 데이터베이스를 만듭니다. 
  
6.  탐색 창에서 선택 hello 다음 표는 hello에 대 한 확인란: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales**합니다.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
확인을 클릭하면 쿼리 편집기가 열립니다. Hello 다음 섹션에서 원하는 tooimport hello 데이터만 선택 합니다.

  
## <a name="filter-hello-table-data"></a>Hello 테이블 데이터 필터링  
Hello AdventureWorksDW2014 예제 데이터베이스의 테이블에는 모델에 필요한 tooinclude 없는 데이터를 가집니다. 가능 하면 원하는 toofilter hello 모델에 사용 되는 불필요 한 데이터 toosave 메모리 공간입니다. 하지 가져온 hello 작업 영역 데이터베이스 또는 hello model 데이터베이스에 배포 된 후 되므로 일부 hello 테이블의에서 열을 필터링 합니다. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>toofilter hello 테이블 데이터를 가져오기 전에  
  
1.  쿼리 편집기에서 선택 hello **DimCustomer** 테이블입니다. Hello 데이터 원본 (AdventureWorksDWQ2014 샘플 데이터베이스)에 hello DimCustomer 테이블의 뷰가 표시 됩니다. 
  
2.  **SpanishEducation**, **FrenchEducation**, **SpanishOccupation**, **FrenchOccupation**을 다중 선택(Ctrl + 클릭)한 후 마우스 오른쪽 단추를 클릭한 후 **열 제거**를 클릭합니다. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    없기 때문에 이러한 열에 대 한 hello 값 관련 tooInternet 판매 분석 아닌 없습니다 필요 tooimport 이러한 열입니다. 불필요한 열을 제거하여 모델을 더 작고 효율적으로 만듭니다.  
  
4.  Hello 남아 있는 각 테이블의 열을 다음 hello를 제거 하 여 테이블을 필터링 합니다.  
    
    **DimDate**
    
      |열|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |열|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |열|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |열|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |열|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |열|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Hello 선택한 테이블 및 열 데이터 가져오기  
미리 보기 하 고 불필요 한 데이터를 필터링 했으므로 hello 나머지 않을 hello 데이터를 가져올 수 있습니다. hello 마법사 hello 테이블 데이터를 함께 테이블 간 관계를 가져옵니다. Hello 모델에서 만들어진 새 테이블 및 열 및 필터링 하는 데이터를 가져올 수는 있습니다.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>테이블 및 열 데이터 tooimport hello 선택  
  
1.  선택 항목을 검토합니다. 잘못된 항목이 없으면, **가져오기**를 클릭합니다. hello 데이터 처리 대화 상자에는 hello 상태를 작업 영역 데이터베이스에 사용자 데이터 원본에서 가져올 데이터를 표시 합니다.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  **닫기**를 클릭합니다.  

  
## <a name="save-your-model-project"></a>모델 프로젝트를 저장합니다.  
toofrequently 모델 프로젝트를 저장 합니다.  
  
#### <a name="toosave-hello-model-project"></a>toosave hello 모델 프로젝트  
  
-   **파일** > **모두 저장**을 클릭합니다.  
  
## <a name="whats-next"></a>다음 작업
[단원 3: 날짜 테이블로 표시](../tutorials/aas-lesson-3-mark-as-date-table.md)

  
  
