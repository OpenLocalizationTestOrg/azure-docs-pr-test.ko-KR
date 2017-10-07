---
제목: aaa "Azure Analysis Services 자습서 단원 1: 새 테이블 형식 모델 프로젝트 만들기 | Microsoft Docs "설명: 설명 방법을 toocreate 새 Azure Analysis Services tutorial 프로젝트. 서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 06/01/2017 ms.author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>단원 1: 테이블 형식 모델 프로젝트 만들기

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 SQL Server Data Tools (SSDT) toocreate 새로운 테이블 형식 모델 프로젝트를 사용 하 여 hello 1400 호환성 수준. 새 프로젝트가 만들어지면 데이터를 추가하고 모델을 작성할 수 있습니다. 이 단원에서는 간략 한 소개 toohello 테이블 형식 모델 제작 환경 SSDT에서 제공 합니다.  
  
이 단원에서는 시간 toocomplete 예상: **10 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델 제작 자습서의에서 첫 번째 단원 hello입니다. toocomplete 단원이 toohave 적절 해야 하는 몇 가지 필수 구성 요소가 필요 합니다. toolearn 더 참조 [Azure Analysis Services-Adventure Works 자습서](../tutorials/aas-adventure-works-tutorial.md)합니다.  
  
## <a name="create-a-new-tabular-model-project"></a>새 테이블 형식 모델 프로젝트 만들기  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate 새로운 테이블 형식 모델 프로젝트  
  
1.  Hello에 SSDT에서 **파일** 메뉴를 클릭 하 여 **새로** > **프로젝트**합니다.  
  
2.  Hello에 **새 프로젝트** 대화 상자에서 **설치 됨** > **Business Intelligence** > **AnalysisServices**, 클릭 하 고 **Analysis Services 테이블 형식 프로젝트**합니다.  
  
3.  **이름**, 형식 **AW Internet Sales**, hello 프로젝트 파일의 위치를 지정 합니다.  
  
    기본적으로 **솔루션 이름** hello 프로젝트 이름으로 같은 hello은; 하지만 다른 솔루션 이름을 입력할 수 있습니다.  
  
4.  **확인**을 클릭합니다.  
  
5.  Hello에 **테이블 형식 모델 디자이너** 대화 상자에서 **통합된 작업 영역**합니다.  
  
    hello 작업 영역 모델 제작 중 hello 프로젝트 이름이 hello로는 테이블 형식 모델 데이터베이스를 호스팅합니다. 통합된 작업 영역 의미 SSDT hello 필요 tooinstall 모델 제작에 대 한 별도 Analysis Services 서버 인스턴스를 제거 합니다. 기본 제공 된 인스턴스를 사용 합니다.
      
6.  **호환성 수준**에서 **SQL Server 2017 / Azure Analysis Services(1400)**를 선택합니다.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    SQL Server 2017 / Azure Analysis Services (1400) 보이지 않으면 hello 호환성 수준 목록 상자에서 SQL Server Data Tools의 최신 버전 hello를 사용 하지 않는 합니다. tooget hello 최신 버전 참조 [Install SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)합니다.  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Hello SSDT 테이블 형식 모델 제작 환경 이해  
새 테이블 형식 모델 프로젝트를 만들었으므로 이제는 순간 tooexplore hello 테이블 형식 모델을 제작 환경에 SSDT 보겠습니다.  
  
프로젝트를 만들면 SSDT에서 프로젝트가 열립니다. Hello에 오른쪽 측면에서 **테이블 형식 모델 탐색기**, 모델에 hello 개체의 트리 뷰를 표시 합니다. 데이터를 아직 가져오지 않은, 이후 hello 폴더는 비어 있습니다. 개체를 마우스 오른쪽 단추로 클릭 수 폴더 tooperform 작업, 비슷한 toohello 메뉴 모음입니다. 이 자습서를 실행할 때는 모델 프로젝트에서 서로 다른 개체를 toonavigate hello 테이블 형식 모델 탐색기 사용 합니다.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Hello 클릭 **솔루션 탐색기** 탭 합니다. 여기에 **Model.bim** 파일이 표시됩니다. hello 디자이너 창의 toohello 왼쪽 (hello에 빈 창이 hello Model.bim 탭), 표시 되지 않으면 **솔루션 탐색기**아래 **AW Internet Sales 프로젝트**, hello를 두 번 클릭  **Model.bim** 파일입니다. 모델 프로젝트에 대 한 hello 메타 데이터를 포함 하는 hello Model.bim 파일입니다. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
**Model.bim**을 클릭합니다. Hello에 **속성** 창을 보면 hello 모델 속성을 hello 되며이 중 가장 중요 한 **DirectQuery 모드** 속성입니다. 이 속성 (Off) 메모리 내 모드 또는 DirectQuery 모드 (On) hello 모델을 배포 하는 경우를 지정 합니다. 이 자습서의 경우 메모리 내 모드로 모델을 작성 및 배포합니다.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
모델 프로젝트를 만들 때 특정 모델 속성은 toohello를 자동으로 hello에 지정할 수 있는 데이터 모델링 설정에 따라 **도구** 메뉴 > **옵션** 대화 상자. 데이터 백업, 작업 영역 보존 및 작업 영역 서버 속성 위치와 방법을 hello 작업 영역 데이터베이스 (모델 제작 데이터베이스)를 백업, 메모리에 유지 및 지정 작성 합니다. 필요한 경우 나중에 이러한 설정을 변경할 수 있지만 지금은 이러한 속성을 그대로 둡니다.  

**솔루션 탐색기**에서 **AW Internet Sales**(프로젝트)를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다. hello **AW Internet Sales 속성 페이지** 대화 상자가 나타납니다. 이러한 속성 중 일부는 모델을 배포할 때 나중에 설정합니다.  
  
SSDT를 설치할 때 몇 가지 새 메뉴 항목이 Visual Studio 환경 toohello 추가 되었습니다. Hello 클릭 **모델** 메뉴. 여기에서 있습니다 수 데이터를 가져올 작업 영역 데이터 새로 고침, Excel에서 모델 찾아보기, 큐브 뷰 및 역할을 선택 하는 hello 모델 뷰를 만들고 계산 옵션을 설정 합니다. Hello 클릭 **테이블** 메뉴. 여기에서 관계를 만들고 관리할 수 있으며 날짜 테이블 설정을 지정하고 파티션을 만들며 테이블 속성을 편집할 수 있습니다. Hello를 누르면 **열** 메뉴를 추가 하 고 테이블의 열 삭제, 열을 고정 및 정렬 순서를 지정할 수 있습니다. SSDT는 또한 몇 가지 단추 toohello 모음을 추가합니다. Hello 자동 합계 기능 toocreate 선택한 열에 대 한 표준 집계 측정값을 가장 유용 합니다. 빠른 액세스 toofrequently 기능 및 명령에 사용 되는 다른 도구 모음 단추를 제공 합니다.  
  
일부의 hello 대화 상자 및 다양 한 기능 특정 tooauthoring 테이블 형식 모델에 대 한 위치를 탐색 합니다. 일부 항목은 아직 활성, hello 테이블 형식 모델 제작 환경에 대 한 유용한 정보를 얻을 수 있습니다.  
  

## <a name="whats-next"></a>다음 작업
[단원 2: 데이터 가져오기](../tutorials/aas-lesson-2-get-data.md)

  
  
  
