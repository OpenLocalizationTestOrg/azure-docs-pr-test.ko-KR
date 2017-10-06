---
제목: aaa "Azure Analysis Services 자습서 단원인 13: 배포 | Microsoft Docs "설명: toodeploy hello 자습서 tooAzure Analysis Services 프로젝트 하는 방법에 대해 설명 합니다.
서비스: 분석 서비스 documentationcenter: ' 작성자: minewiskan 관리자: erikre 편집기: ' 태그: '

ms.assetid: ms.service: 분석 서비스 ms.devlang: NA ms.topic: get 시작 문서 ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend
---
# <a name="lesson-13-deploy"></a>단원 13: 배포

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

이 단원에서는 배포 속성 구성 Azure Analysis Services 서버 toodeploy tooand hello 모델의 이름을 지정 합니다. 그런 다음 hello 모델 toothat 인스턴스를 배포합니다. 모델 배포 된 후 사용자가 보고 클라이언트 응용 프로그램을 사용 하 여 tooit를 연결할 수 있습니다. toolearn 더 참조 [tooAzure Analysis Services 배포](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy)합니다.  
  
이 단원에서는 시간 toocomplete 예상: **5 분**  
  
## <a name="prerequisites"></a>필수 조건  
이 항목은 테이블 형식 모델링 자습서에 포함되며 순서대로 완료해야 합니다. 이 단원에서는 hello 작업을 수행 하기 전에 완료 해야 hello 이전 단원: [12 단원: Excel에서 분석](../tutorials/aas-lesson-12-analyze-in-excel.md)합니다.  

> [!IMPORTANT]  
> 있어야 [관리자 권한을](../analysis-services-server-admins.md) on hello 원격 Analysis Services 서버 순서로 toodeploy tooit 합니다.  

> [!IMPORTANT]  
> 온-프레미스 SQL Server에 hello AdventureWorksDW2014 예제 데이터베이스를 설치 하 고 모델 tooan Azure Analysis Services 서버를 배포 하는 경우는 [온-프레미스 데이터 게이트웨이](../analysis-services-gateway.md) 가 필요 합니다.
  
## <a name="deploy-hello-model"></a>Hello 모델 배포  
  
#### <a name="tooconfigure-deployment-properties"></a>tooconfigure 배포 속성  

  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트를 마우스 클릭 **속성**합니다.  
  
2.  Hello에 **AW Internet Sales 속성 페이지** 대화 상자의 **배포 서버**, hello에 **서버** 속성 hello 전체 서버를 입력 합니다.  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  Hello에 **데이터베이스** 속성을 입력 **Adventure Works Internet Sales**합니다.  
  
4.  Hello에 **모델 이름** 속성을 입력 **Adventure Works Internet Sales Model**합니다.  
  
5.  선택 내용을 확인한 다음 **확인**을 클릭합니다.  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a>toodeploy hello Adventure Works Internet Sales
  
1.  **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트 > **빌드**합니다.  

2.  마우스 오른쪽 단추로 클릭 hello **AW Internet Sales** 프로젝트 > **배포**합니다.

    다음과 같은 행위는 tooAzure Analysis Services를 배포할 때는 증명된 tooenter 사용자 계정 이어야 합니다. 조직의 계정 및 암호를 입력합니다(예: nancy@adventureworks.com). 이 계정은 hello 서버에서 관리자 여야 합니다.
  
    hello 배포 대화 상자가 표시 되 고 hello 메타 데이터의 배포 상태 hello 및 hello 모델에 포함 된 각 테이블에 표시 됩니다.  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. 배포가 성공적으로 완료되면 진행하고 **닫기**를 클릭합니다.  
  
## <a name="conclusion"></a>결론  
축하합니다. 첫 번째 Analysis Services 테이블 형식 모델의 작성 및 배포가 완료되었습니다. 이 자습서에서는 도움이 hello 테이블 형식 모델을 만드는 가장 일반적인 작업을 완료 하는 과정을 안내 합니다. Adventure Works Internet Sales 모델을 배포 했으므로, SQL Server Management Studio toomanage hello 모델을 사용할 수 있습니다. 처리 스크립트와 백업 계획을 만듭니다. 사용자가 Microsoft Excel 또는 Power BI와 같은 보고 클라이언트 응용 프로그램을 사용 하 여 toohello 모델을 연결할 이제 수 있습니다.  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>다음 작업
[Power BI Desktop으로 연결](../analysis-services-connect-pbi.md)   
[추가 단원 - 동적 보안](../tutorials/aas-supplemental-lesson-dynamic-security.md)   
[추가 단원 - 세부 정보 행](../tutorials/aas-supplemental-lesson-detail-rows.md)   
[추가 단원 - 불규칙한 계층 구조](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
