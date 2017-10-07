---
제목: aaa "11 Azure Analysis Services 자습서 단원: 역할 만들기 | Microsoft Docs "설명: toocreate 역할에서 Azure Analysis Services tutorial 프로젝트를 hello 하는 방법에 대해 설명 합니다. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-11-create-roles"></a>단원 11: 역할 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 역할을 만듭니다. 역할 제공 모델 데이터베이스 개체 및 데이터 보안 tooonly 액세스를 제한 하 여 해당 사용자 역할 구성원 인 합니다. 각 역할은 단일 사용 권한(없음, 읽기, 읽기 및 프로세스, 프로세스 또는 관리자)으로 정의됩니다. 역할 관리자를 사용하여 모델 작성 중에 역할을 정의할 수 있습니다. 모델을 배포한 후에는 SSMS(SQL Server Management Studio)를 사용하여 역할을 관리할 수 있습니다. toolearn 더 참조 [역할](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular)합니다.
  
> [!NOTE]  
> 역할을 만드는 필요 하지 않은 toocomplete이이 자습서가 있습니다. 기본적으로 현재 로그인 하는 hello 계정 관리자에 대 한 권한이 hello 모델입니다. 그러나 다른 사용자는 보고 클라이언트를 사용 하 여 조직 toobrowse 프로그램에 대 한 사용 권한을 읽기 역할을 하나 이상 만들 하며 해당 사용자가 구성원으로 추가 합니다.  
  
세 가지 역할을 만듭니다.  
  
-   **영업 관리자** –이 역할을 구하려는 toohave 읽기 권한 tooall 모델 개체와 데이터 조직에서 사용자를 포함할 수 있습니다.  
  
-   **Sales Analyst US** –이 역할 toobe 수 toobrowse 데이터만 사용 하도록 하려는 조직에서 사용자를 포함할 수 있습니다 toosales hello 미국에에서 관련 됩니다. DAX 수식 toodefine를 사용 하면이 역할에 대 한 *행 필터*, 미국 hello에 대 한 멤버 toobrowse 데이터 제한 합니다.  
  
-   **관리자** –이 역할은 hello model 데이터베이스에서 무제한 액세스 및 사용 권한 tooperform 관리 작업을 허용 toohave 관리자 권한을 사용 하도록 하려는 사용자를 포함할 수 있습니다.  
  
조직의 Windows 사용자 및 그룹 계정은 고유 하므로 특정 조직 toomembers에서 계정을 추가할 수 있습니다. 그러나이 자습서에서는 수 또한 hello 멤버 비워 두면 됩니다. 나중에 12 단원 각 역할의 hello 효과 테스트할: Excel에서 분석 합니다.  
  
이 단원에서는 시간 toocomplete 예상: **15 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [10 단원: 파티션 만들기](../tutorials/aas-lesson-10-create-partitions.md)합니다.  
  
## <a name="create-roles"></a>역할 만들기  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate Sales Manager 사용자 역할  
  
1.  테이블 형식 모델 탐색기에서 **역할** > **역할**을 마우스 오른쪽 단추로 클릭합니다.  
  
2.  역할 관리자에서 **새로 만들기**를 클릭합니다.  
  
3.  Hello 새 역할을 클릭 한 다음 hello **이름** 열을 너무 hello 역할 이름 바꾸기**판매 관리자**합니다.  
  
4.  Hello에 **사용 권한을** 열에서 hello 드롭다운 목록에서를 클릭 한 다음 hello 선택 **읽기** 권한. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다. Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate Sales Analyst US 사용자 역할  
  
1.  역할 관리자에서 **새로 만들기**를 클릭합니다.    
  
2.  너무 hello 역할 이름 바꾸기**Sales Analyst US**합니다.  
  
3.  이 역할에 **읽기** 권한을 부여합니다.  
  
4.  Hello 행 필터 탭을 클릭 하 고 hello에 대 한 다음 **DimGeography** 다음 수식을 형식 hello hello DAX 필터 열에만 테이블:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    행 필터 수식은 tooa 부울 (TRUE/FALSE) 값을 확인 해야 합니다. 이 수식을 사용 하 여 행만 hello Country Region Code 값 "미국" 되는지 표시 toohello 사용자 지정 됩니다.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다. Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate 관리자 사용자 역할  
  
1.  **새로 만들기**를 클릭합니다.  
  
2.  너무 hello 역할 이름 바꾸기**관리자**합니다.  
  
3.  이 역할에 **관리자** 권한을 부여합니다.  
  
4.  선택 사항: hello 클릭 **멤버** 탭을 클릭 한 다음 **추가**합니다. Hello에 **사용자 또는 그룹 선택** 대화 상자 hello Windows 사용자 또는 그룹을 입력 tooinclude hello 역할에 사용자 조직에서 원하는 합니다. 
  
  
## <a name="whats-next"></a>다음 작업
[단원 12: Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)

  
  
