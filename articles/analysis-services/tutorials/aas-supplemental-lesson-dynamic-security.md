---
제목: aaa "Azure Analysis Services tutorial 추가 단원: 동적 보안 | Microsoft Docs "설명: hello Azure Analysis Services 자습서의 행을 사용 하 여 동적 보안 toouse 필터링 하는 방법에 대해 설명 합니다.
서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>추가 단원 - 동적 보안

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 추가 단원에서는 동적 보안을 구현하는 추가 역할을 만듭니다. 동적 보안은 현재 로그온 hello 사용자의 hello 사용자 이름 또는 로그인 id에 따라 행 수준 보안을 제공 합니다. 
  
tooimplement 동적 보안 toohello 모델을 연결 하 고 모델 개체와 데이터를 찾아볼 수 있는 사용자의 hello 사용자 이름이 포함 된 테이블 tooyour 모델을 추가 합니다. 이 자습서를 사용 하 여 만드는 hello 모델은 Adventure Works;의 hello 컨텍스트에서 그러나 toocomplete이 단원, 사용자의 도메인에서 사용자가 포함 된 테이블을 추가 해야 합니다. 추가 된 hello 사용자 이름에 대 한 hello 암호 필요가 없습니다. 사용자의 도메인에서 사용자의 작은 샘플으로는 EmployeeSecurity 테이블 toocreate hello 붙여넣기 기능을 사용 하면 Excel 스프레드시트의 데이터입니다. 실제 시나리오에서 사용자 이름을 포함 하는 hello 테이블 일반적으로 것 실제 데이터베이스에서 테이블을 데이터 소스로 예를 들어는 실제 DimEmployee 테이블입니다.  
  
두 개의 DAX 함수를 사용 하면 tooimplement 동적 보안: [USERNAME 함수 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) 및 [LOOKUPVALUE 함수 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)합니다. 행 필터 수식에 적용된 이러한 함수는 새 역할에 정의됩니다. Hello LOOKUPVALUE 함수를 사용 하 여 hello 수식 hello EmployeeSecurity 테이블의 값을 지정 합니다. hello 수식 값 toohello USERNAME 함수 로그온 hello 사용자의 hello 사용자 이름을 지정 하는 toothis 역할에 속해 있는지를 전달 합니다. hello 사용자 hello 역할 행 필터에 의해 지정 된 데이터만 탐색할 수 있습니다. 이 시나리오에서는 영업 직원이 이들이 속한은 hello 영업 지역에 대 한 인터넷 매출 데이터를 찾아볼 수만 지정 합니다.  
  
이러한 태스크는 고유한 toothis Adventure Works 테이블 형식 모델 시나리오는 tooa 실제 시나리오에 반드시 적용 되지 않습니다으로 식별 됩니다. 각 태스크는 hello 작업의 hello 용도 설명 하는 추가 정보를 포함 합니다.  
  
이 단원에서는 시간 toocomplete 예상: **30 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 추가 단원 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 추가 단원 hello 작업을 수행 하려면 이전 단원을 모두 완료 해야 합니다.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Hello DimSalesTerritory 테이블 toohello AW Internet Sales 테이블 형식 모델 프로젝트를 추가 합니다.  
tooimplement이 Adventure Works 시나리오에 대 한 동적 보안을 두 개의 추가 테이블 tooyour 모델을 추가 해야 합니다. 동일한 AdventureWorksDW 데이터베이스를 hello 하는 hello 첫 번째 테이블에서 dimsalesterritory (Sales Territory)을 추가 합니다. 나중 hello 특정 데이터를 정의 하는 행 필터 toohello SalesTerritory 테이블에 적용 hello 로그온 한 사용자를 찾아볼 수 있습니다.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tooadd hello DimSalesTerritory 테이블  
  
1.  테이블 형식 모델 탐색기의 > **데이터 원본**에서 해당 연결을 마우스 오른쪽 단추로 클릭한 다음 **새 테이블 가져오기**를 클릭합니다.  

    Hello 가장 자격 증명 대화 상자가 나타나면 2 단원에서에서 사용한 hello 가장 자격 증명 입력: 데이터 추가 합니다.
  
2.  탐색 창의 hello 선택 **DimSalesTerritory** 테이블을 마우스 클릭 **확인**합니다.    
  
3.  쿼리 편집기에서 클릭 hello **DimSalesTerritory** 쿼리하고 다음 제거 **SalesTerritoryAlternateKey** 열입니다.  
  
7.  **가져오기**를 클릭합니다.  
  
    새 테이블 hello toohello 모델 작업 영역에 추가 됩니다. 그런 다음 개체 및 hello 원본 DimSalesTerritory 테이블의에서 데이터를 AW Internet Sales Tabular Model으로 가져옵니다.  
  
9. Hello 테이블을 성공적으로 가져온 후 클릭 **닫기**합니다.  

## <a name="add-a-table-with-user-name-data"></a>사용자 이름 데이터가 있는 테이블 추가  
hello AdventureWorksDW 예제 데이터베이스의 DimEmployee 테이블 hello hello AdventureWorks 도메인의 사용자가 포함 합니다. 해당 사용자 이름은 사용자 환경에 존재하지 않습니다. 모델에 조직에서 실제 사용자의 작은 샘플(3개 이상)을 포함하는 테이블을 만들어야 합니다. 그런 다음 멤버 toohello 새 역할로 이러한 사용자를 추가합니다. 사용자의 도메인에서 실제 Windows 사용자 이름이 필요는 없지만 hello 샘플 사용자 이름에 대 한 hello 암호 필요가 없습니다.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd EmployeeSecurity 테이블  
  
1.  Microsoft Excel을 열어 워크시트를 만듭니다.  
  
2.  다음 표를 hello 머리글 행을 포함 하 여 hello 복사한 hello 워크시트에 붙여 넣습니다.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Hello 이름과 조직에 있는 세 개의 사용자의 로그인 id를 가진 hello 이름, 성 및 domain\username을 대체 합니다. Hello 배치 EmployeeId 1 이므로이 사용자가 속한 toomore 보다 한 영업 지역에 대 한 hello 처음 두 행에 같은 사용자입니다. Hello EmployeeId 및 SalesTerritoryId 필드 그대로 둡니다.  
  
4.  Hello 워크시트로 저장 **SampleEmployee**합니다.  
  
5.  Hello 워크시트에서 hello 헤더를 포함 하 여 직원 데이터가 있는 모든 hello 셀을 선택 하 고 hello 선택한 데이터를 마우스 오른쪽 단추로 클릭 **복사**합니다.  
  
6.  SSDT에서는 hello 클릭 **편집** 메뉴를 차례로 클릭 **붙여넣기**합니다.  
  
    붙여넣기가 회색 hello 모델 디자이너 창의 테이블에서 모든 열을 클릭 하 고 다시 시도 하십시오.  
  
7.  Hello에 **붙여넣기 미리 보기** 대화 상자의 **테이블 이름**, 형식 **EmployeeSecurity**합니다.  
  
8.  **붙여 넣은 데이터 toobe**, 모든 hello 사용자 데이터 및 hello SampleEmployee 워크시트에서 머리글 hello 데이터 포함을 확인 합니다.  
  
9. **첫 행을 열 머리글로 사용**이 선택되어 있는지 확인한 후 **확인**을 클릭합니다.  
  
    Hello SampleEmployee 워크시트에서 복사 된 직원 데이터가 있는 EmployeeSecurity 라는 새 테이블이 생성 됩니다.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>FactInternetSales, DimGeography 및 DimSalesTerritory 테이블 간의 관계 만들기  
hello FactInternetSales, DimGeography, 및 DimSalesTerritory 테이블에는 모두 SalesTerritoryId 공통 된 열을 포함 합니다. hello SalesTerritoryId 열 hello DimSalesTerritory 테이블의 각 영업 지역에 대해 다른 Id 사용 하 여 값을 포함합니다.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>FactInternetSales hello, DimGeography, 및 hello DimSalesTerritory 테이블 간의 toocreate 관계  
  
1.  다이어그램 보기에서 hello **DimGeography** 테이블을 클릭 한 채로 hello **SalesTerritoryId** 열에 있으면 드래그 hello 커서 toohello **SalesTerritoryId** hello의 열 **DimSalesTerritory** 테이블을 마우스를 놓습니다.  
  
2.  Hello에 **FactInternetSales** 테이블을 클릭 한 채로 hello **SalesTerritoryId** 열에 있으면 드래그 hello 커서 toohello **SalesTerritoryId** hello 의에서열 **DimSalesTerritory** 테이블을 마우스를 놓습니다.  
  
    공지 hello이이 관계에 대 한 활성 속성은 False, 되지 않음입니다. hello FactInternetSales 테이블에 다른 활성 관계가 이미 있습니다.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>클라이언트 응용 프로그램에서 hello EmployeeSecurity 테이블 숨기기  
이 태스크에서는 숨기면 hello EmployeeSecurity 테이블 지속적으로 업데이트를 클라이언트 응용 프로그램의 필드 목록에 표시 합니다. 테이블을 숨긴다고 해서 안전한 것은 아닙니다. 사용자는 EmployeeSecurity 테이블 데이터를 계속 쿼리할 수 있습니다(알고 있는 경우). toosecure hello EmployeeSecurity 테이블 데이터를 사용자가 tooquery 수 없도록 방지 데이터, 이후 태스크에서 필터를 적용 합니다.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>클라이언트 응용 프로그램에서 toohide hello EmployeeSecurity 테이블  
  
-   다이어그램 뷰에서 hello 모델 디자이너에서 마우스 오른쪽 단추로 클릭 hello **직원** 테이블 머리글을 마우스 클릭 **클라이언트 도구에서 숨기기**합니다.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Sales Employees by Territory(지역별 영업 직원) 사용자 역할 만들기  
이 작업에서는 사용자 역할을 만듭니다. 이 역할 정의 hello DimSalesTerritory 테이블의 어떤 행이 표시 toousers 행 필터를 포함 합니다. hello 필터를 적용 합니다 hello 대 다 관계의 다른 방향 tooall 테이블 관련된 tooDimSalesTerritory 합니다. 도 hello 역할의 구성원 인 모든 사용자가 쿼리할 수 없도록 hello 전체 EmployeeSecurity 테이블의 보안을 유지 하는 필터를 적용 합니다.  
  
> [!NOTE]  
> Sales Employees by Territory 역할이이 단원에서 만드는 hello 멤버 toobrowse (또는 쿼리)만 판매 데이터를 자신이 속한 hello 영업 지역 toowhich 제한 합니다. 사용자는 멤버 toohello Sales Employees by Territory 역할에서 만든 역할의 멤버로 존재 하는 추가 하면 [11 단원: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md), 사용 권한의 조합의 얻을 합니다. 사용자가 여러 역할, hello 사용 권한 및 각 역할에 대해 정의 된 행 필터의 멤버인 경우 누적 됩니다. 즉, hello 사용자 hello 더 큰 권한이 hello 역할 조합으로 결정 합니다.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate Sales Employees by Territory 사용자 역할  
  
1.  SSDT에서는 hello 클릭 **모델** 메뉴를 차례로 클릭 **역할**합니다.  
  
2.  **역할 관리자**에서 **새로 만들기**를 클릭합니다.  
  
    새 역할 hello 사용 권한 없음 toohello 목록을 추가 합니다.  
  
3.  Hello 새 역할을 클릭 한 다음 hello **이름** 열을 너무 hello 역할 이름 바꾸기**Sales Employees by Territory**합니다.  
  
4.  Hello에 **사용 권한을** 열에서 hello 드롭다운 목록에서를 클릭 한 다음 hello 선택 **읽기** 권한.  
  
5.  Hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다.  
  
6.  Hello에 **사용자 또는 그룹 선택** 대화 상자의 **Enter hello 개체인 tooselect**, hello 첫 번째 예제 사용자 이름을 입력 hello EmployeeSecurity 테이블을 만들 때 사용 합니다. 클릭 **이름 확인** tooverify hello 사용자 이름이 올바른지와 클릭 **확인**합니다.  
  
    Hello EmployeeSecurity 테이블을 만들 때 사용한 다른 예제 사용자 이름을 추가 hello이이 단계를 반복 합니다.  
  
7.  Hello 클릭 **행 필터** 탭 합니다.  
  
8.  Hello에 대 한 **EmployeeSecurity** 테이블 hello에 **DAX 필터** 다음 수식을 형식 hello, 열:  
  
    ```
      =FALSE()  
    ```
  
    이 수식은 모든 열 toohello false 부울 조건 확인할 수 있는지를 지정 합니다. Hello EmployeeSecurity 테이블에 대 한 열이 없습니다 hello Sales Employees by Territory 사용자 역할의 멤버가 쿼리할 수 있습니다.  
  
9. Hello에 대 한 **DimSalesTerritory** 테이블, 다음 수식을 형식 hello:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    이 수식에서 LOOKUPVALUE 함수 hello 모든 값이 반환 hello DimEmployeeSecurity [SalesTerritoryId] 열에 대 한 여기서 hello EmployeeSecurity [LoginId]가 hello 동일 현재 로그온 한 Windows 사용자 이름 및 EmployeeSecurity [hello로 SalesTerritoryId] hello DimSalesTerritory [SalesTerritoryId]와 동일 hello 됩니다.  
  
    hello LOOKUPVALUE에서 반환 된 sales territory Id 집합에 있으면 사용 되는 toorestrict hello hello DimSalesTerritory 테이블에에서 표시 되는 행. 여기서 hello hello 행에 대 한 SalesTerritoryID는 hello LOOKUPVALUE 함수에서 반환 된 Id의 hello 집합에 행만 표시 됩니다.  
  
10. 역할 관리자에서 **확인**을 클릭합니다.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Hello Sales Employees by Territory 사용자 역할 테스트  
이 태스크에서는 Excel 기능에서 분석 hello를 사용 하 여 hello Sales Employees by Territory 사용자 역할의 SSDT tootest hello 효율성에서. 하나를 지정 toohello EmployeeSecurity 테이블을 추가한 hello 사용자 이름 및 hello 역할의 구성원으로 합니다. 이 사용자 이름은 Excel 및 hello 모델 간에 만들어진 hello 연결에서 hello 유효 사용자 이름으로 다음 사용 됩니다.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>tootest hello Sales Employees by Territory 사용자 역할  
  
1.  SSDT에서는 hello 클릭 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  Hello에 **Excel에서 분석** 대화 상자의 **지정 hello 사용자 이름 또는 역할 toouse tooconnect toohello 모델**선택, **기타 Windows 사용자**, 클릭하고**찾아보기**합니다.  
  
3.  Hello에 **사용자 또는 그룹 선택** 대화 상자의 **hello 개체 이름 tooselect 입력**hello EmployeeSecurity 테이블에 포함 된 사용자 이름을 입력 한 다음 클릭 **이름 확인**.  
  
4.  클릭 **확인** tooclose hello **사용자 또는 그룹 선택** 대화 상자를 닫은 다음 **확인** tooclose hello **Excel에서 분석** 대화 상자.  
  
    Excel에서 새 통합 문서가 열립니다. 피벗 테이블이 자동으로 만들어집니다. hello 피벗 테이블 필드 목록에 새 모델에서 사용할 수 있는 hello 데이터 필드 대부분 포함 되어 있습니다.  
  
    공지 hello EmployeeSecurity 테이블 hello 피벗 테이블 필드 목록에에서 표시 되지 않습니다. 이전 작업의 클라이언트 도구에서 이 테이블을 숨겼습니다.  
  
5.  Hello에 **필드** 목록에서 **∑ Internet Sales** (측정값) 선택 hello **InternetTotalSales** 측정값입니다. hello 측정값 hello에 입력 된 **값** 필드입니다.  
  
6.  선택 hello **SalesTerritoryId** hello에서 열 **DimSalesTerritory** 테이블입니다. hello 열 hello에 입력 된 **행 레이블** 필드입니다.  
  
    공지 인터넷 판매 수치 hello 하나의 영역 toowhich hello 유효 사용자 이름을 사용한 경우에 표시 속해 있습니다. 다른 열을 선택 하는 경우 City hello DimGeography 테이블에서 같은 행 레이블 필드와만 4 개 도시 hello 영업 지역 toowhich hello 유효 사용자에 속한 표시 됩니다.  
  
    이 사용자는 찾아보기 또는 지역에 속해 하나 hello 이외의 다른 지역에 대 한 모든 인터넷 판매 데이터를 쿼리할 수 없습니다. 이 제한은 hello hello DimSalesTerritory 테이블 hello Sales Employees by Territory 사용자 역할에에서 대해 정의 된 행 필터는 데이터를 보호에 대 한 모든 데이터 때문에 관련 tooother 영업 지역.  
  
## <a name="see-also"></a>참고 항목  
[USERNAME 함수(DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[LOOKUPVALUE 함수(DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[CUSTOMDATA 함수(DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  