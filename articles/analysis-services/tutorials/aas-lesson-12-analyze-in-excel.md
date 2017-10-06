---
제목: aaa "12 Azure Analysis Services 자습서 단원: Excel에서 분석 | Microsoft Docs "설명: Azure Analysis Services 하는 hello에 toouse Excel에서 분석 방법에 대해 설명 tutorial 프로젝트. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>단원 12: Excel에서 분석

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Excel 기능은 tooopen Microsoft Excel에서에서 분석 hello를 사용 하 여이 단원에서는 자동으로 연결 toohello 모델 작업 영역 만들기 및 자동으로 피벗 테이블 toohello 워크시트를 추가 합니다. 기능은 Excel에서 분석 hello tooprovide 사용 되므로 모델의 쉽고 빠르게 tootest hello 효율성 이전 toodeploying 모델을 설계 합니다. 이 단원에서는 어떠한 데이터 분석도 수행하지 않습니다. 이 단원에서는의 hello 목적은 toofamiliarize hello 모델을 작성, hello 도구와 함께 사용할 수 있습니다 tootest 모델 디자인 합니다.   
  
이 단원에서는 Excel hello에 설치 해야 toocomplete SSDT와 같은 컴퓨터.
  
이 단원에서는 시간 toocomplete 예상: **5 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [11 단원: 역할 만들기](../tutorials/aas-lesson-11-create-roles.md)합니다.  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Hello 기본 및 인터넷 판매 큐브 뷰를 사용 하 여 찾아보기  
이러한 첫 번째 작업에서 모델을 찾으면 프로그램 모든 모델 개체를 포함 하는 두 hello 기본 큐브를 사용 하 여 및 hello Internet Sales 큐브 뷰를 사용 하 여 앞서 있습니다. hello Internet Sales 큐브 뷰는 hello Customer 테이블 개체가 제외 됩니다.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>hello 기본 큐브 뷰를 사용 하 여 toobrowse  
  
1.  Hello 클릭 **모델** 메뉴 > **Excel에서 분석**합니다.  
  
2.  Hello에 **Excel에서 분석** 대화 상자를 클릭 **확인**합니다.  
  
    Excel에서 새 통합 문서가 열립니다. Hello 기본 큐브는 사용 되는 toodefine 보기 가능한 필드와 데이터 원본 연결을 hello 현재 사용자 계정을 사용 하 여 만들어집니다. 피벗 테이블 toohello 워크시트를 자동으로 추가 됩니다.  
  
3.  Excel의 hello **피벗 테이블 필드 목록**, 통지 hello **DimDate** 및 **FactInternetSales** 측정값 그룹에 표시 합니다. hello **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, 및 **FactInternetSales** 해당 열이 있는 테이블도 나타납니다.  
  
4.  Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>hello Internet Sales 큐브 뷰를 사용 하 여 toobrowse  
  
1.  Hello 클릭 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  Hello에 **Excel에서 분석** 대화 상자 **현재 Windows 사용자** 선택 되 면 다음 hello **관점** 드롭 다운 목록 상자에서 **인터넷 판매** , 클릭 하 고 **확인**합니다. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  Excel에서의 **피벗 테이블 필드**, hello DimCustomer 테이블은 hello 필드 목록에서 제외를 확인 합니다.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.  
  
## <a name="browse-by-using-roles"></a>역할을 사용하여 찾아보기  
역할은 테이블 형식 모델의 중요한 부분입니다. 하나 이상의 역할이 없는 toowhich 사용자가을 구성원으로 추가 사용자가 액세스를 업데이트 하 고 모델을 사용 하 여 데이터를 분석할 수 없습니다. 기능은 Excel에서 분석 hello는 하기 위한 방법을 제공 하면 정의한 tootest hello 역할입니다.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>hello Sales Manager 사용자 역할을 사용 하 여 toobrowse  
  
1.  SSDT에서는 hello 클릭 **모델** 메뉴를 차례로 클릭 **Excel에서 분석**합니다.  
  
2.  **지정 hello 사용자 이름 또는 역할 toouse tooconnect toohello 모델**선택, **역할**, hello 드롭다운 목록 상자에서 선택 **판매 관리자**, 를클릭한다음 **정상**합니다.  
  
    Excel에서 새 통합 문서가 열립니다. 피벗 테이블이 자동으로 만들어집니다. hello 피벗 테이블 필드 목록에 새 모델에서 사용 가능한 모든 hello 데이터 필드에 포함 됩니다.  
      
3.  Hello 통합 문서를 저장 하지 않고 Excel을 닫습니다.  
  
## <a name="whats-next"></a>다음 작업
다음 단원 이동 toohello: [13 단원: 배포](../tutorials/aas-lesson-13-deploy.md)합니다.

  
  
  
