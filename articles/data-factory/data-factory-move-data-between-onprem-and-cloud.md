---
title: "데이터 관리 게이트웨이 aaaMove 데이터-| Microsoft Docs"
description: "Hello와 온-프레미스 데이터 게이트웨이 toomove 데이터 설정 클라우드입니다. 데이터 toomove Azure Data Factory에서에서 데이터 관리 게이트웨이 사용 합니다."
keywords: "데이터 게이트웨이, 데이터 통합, 데이터 이동, 게이트웨이 자격 증명"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동
이 문서에서는 Data Factory를 사용하여 온-프레미스 데이터 저장소와 클라우드 데이터 저장소 간에 데이터 통합의 개요를 제공합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 및 기타 데이터 팩터리 핵심 개념 문서: [데이터 집합](data-factory-create-datasets.md) 및 [파이프라인](data-factory-create-pipelines.md)합니다.

## <a name="data-management-gateway"></a>데이터 관리 게이트웨이
온-프레미스 데이터 저장소에서 데이터를 이동 하 여 온-프레미스 컴퓨터 tooenable에 데이터 관리 게이트웨이 설치 해야 합니다. hello 게이트웨이 hello hello 데이터 저장소로 또는 다른 컴퓨터에이 hello 게이트웨이 toohello 데이터 저장소에 연결할 수 있는 상태로 동일를 컴퓨터에 설치할 수 있습니다.

> [!IMPORTANT]
> 데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요. 

hello 다음 연습에서는 표시 하는 toocreate 온-프레미스에서 데이터를 이동 하는 파이프라인으로 데이터 팩터리 **SQL Server** 데이터베이스 tooan Azure blob 저장소입니다. Hello 연습의 일부로 설치 하 고 컴퓨터에 hello 데이터 관리 게이트웨이 구성 합니다.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>연습: 온-프레미스 데이터 toocloud 복사
이 연습에서는 다음 단계 hello 수행 있습니다. 

1. 데이터 팩터리를 만듭니다.
2. 데이터 관리 게이트웨이를 만듭니다. 
3. 원본 및 싱크 데이터 저장소에 대한 연결된 서비스를 만듭니다.
4. Toorepresent 입력 데이터 집합을 만들고 데이터를 출력 합니다.
5. 복사 활동 toomove hello 데이터 파이프라인을 만듭니다.

## <a name="prerequisites-for-hello-tutorial"></a>Hello 자습서에 대 한 필수 구성 요소
이 연습을 시작 하기 전에 다음 필수 구성 요소는 hello가 있어야 합니다.

* **Azure 구독**.  구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. Hello 참조 [무료 평가판](http://azure.microsoft.com/pricing/free-trial/) 을 참조 합니다.
* **Azure Storage 계정**. Hello blob 저장소로 사용 하는 **대상/싱크** 이 자습서에서는 데이터를 저장 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계 toocreate 하나에 대 한 문서입니다.
* **SQL Server**. 이 자습서에서는 온-프레미스 SQL Server 데이터베이스를 **원본** 데이터 저장소로 사용합니다. 

## <a name="create-data-factory"></a>데이터 팩터리 만들기
이 단계를 사용 하 여 Azure 데이터 팩터리 인스턴스 이름은 Azure 포털 toocreate hello **ADFTutorialOnPremDF**합니다.

1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. **+ 새로 만들기**, **인텔리전스 + 분석** 및 **데이터 팩터리s**을 차례로 클릭합니다.

   ![새로 만들기->DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. Hello에 **새 데이터 팩터리** 페이지에서 입력 **ADFTutorialOnPremDF** hello 이름에 대 한 합니다.

    ![TooStartboard 추가](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. Hello 오류가 나타나면: **"ADFTutorialOnPremDF" 데이터 팩터리 이름을 사용할 수 없으면**을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFTutorialOnPremDF)을 변경 하 고 다시 만들어 보십시오. 이 자습서의 나머지 단계를 수행하는 동안 ADFTutorialOnPremDF 대신에 이 이름을 사용합니다.
   >
   > hello 데이터 팩터리의 hello 이름으로 등록 될 수는 **DNS** hello 미래에 이름을 지정 하 고 따라서 공개적으로 표시 됩니다.
   >
   >
4. 선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.
5. 기존 **리소스 그룹** 을 선택하거나 리소스 그룹을 만듭니다. Hello 자습서에 대 한 명명 된 리소스 그룹 만들기: **ADFTutorialResourceGroup**합니다.
6. 클릭 **만들기** hello에 **새 데이터 팩터리** 페이지.

   > [!IMPORTANT]
   > toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.
   >
   >
7. Hello 참조 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 페이지:

   ![데이터 팩터리 홈페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>게이트웨이 만들기
1. Hello에 **Data Factory** 페이지 **작성자 및 배포** 타일 toolaunch hello **편집기** hello 데이터 팩토리에 대 한 합니다.

    ![작성 및 배포 타일](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. 데이터 팩터리 편집기 hello 클릭 **중... 더 많은** 도구 모음 hello 되 고 클릭 **새 데이터 게이트웨이**합니다. 단추로 또는 **데이터 게이트웨이** hello 트리 보기와 클릭 **새 데이터 게이트웨이**합니다.

   ![도구 모음의 새 데이터 게이트웨이](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. Hello에 **만들기** 페이지에서 입력 **adftutorialgateway** hello에 대 한 **이름**를 클릭 하 고 **확인**합니다.     

    ![게이트웨이 만들기 페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > 이 연습에서는 하나의 노드만 (온-프레미스 Windows 컴퓨터)으로 hello 논리 게이트웨이 만듭니다. Hello 게이트웨이를 여러 온-프레미스 컴퓨터를 연결 하 여 데이터 관리 게이트웨이 확장할 수 있습니다. 노드에서 동시에 실행할 수 있는 데이터 이동 작업의 수를 늘려 강화할 수 있습니다. 이 기능은 단일 노드가 있는 논리 게이트웨이에서도 사용할 수 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 관리 게이트웨이 확장](data-factory-data-management-gateway-high-availability-scalability.md) 문서를 참조하세요.  
4. Hello에 **구성** 페이지 **이 컴퓨터에 직접 설치**합니다. 이 작업 hello 게이트웨이에 대 한 hello 설치 패키지를 다운로드, 설치, 구성 하 고 hello 컴퓨터에서 hello 게이트웨이 등록 합니다.  

   > [!NOTE]
   > Internet Explorer 또는 Microsoft ClickOnce 호환 웹 브라우저를 사용합니다.
   >
   > Chrome을 사용 하는 경우 이동 toohello [크롬 웹 저장소](https://chrome.google.com/webstore/), "ClickOnce" 키워드를 사용 하 여 검색, hello ClickOnce 확장 중 하나를 선택 하 고 설치 합니다.
   >
   > Firefox (설치 추가 기능에서)에 대 한 마십시오 hello 동일 합니다. 클릭 **열기 메뉴** hello 도구 모음에서 단추 (**세 개의 가로선** hello 오른쪽 위 모서리에)를 클릭 하 여 **추가 기능**, "ClickOnce" 키워드를 사용 하 여 검색, hello 중 하나를 선택 ClickOnce 확장 하 고 설치 합니다.    
   >
   >

    ![게이트웨이 - 구성 페이지](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    이 방법은 가장 쉬운 방법은 (원클릭) toodownload hello, 설치, 구성 및 한 번에 hello 게이트웨이 등록 합니다. Hello 나타나면 **Microsoft 데이터 관리 게이트웨이 구성 관리자** 응용 프로그램이 컴퓨터에 설치 되어 있습니다. 찾을 수 있습니다 hello 실행 **ConfigManager.exe** hello 폴더에서: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared**합니다.

    있습니다 수도 다운로드 하 고이 페이지에 hello 링크를 사용 하 여 게이트웨이 수동으로 설치 하 고 hello에 표시 된 hello 키를 사용 하 여 등록 **새 키** 입력란.

    참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 모든 hello hello 게이트웨이에 대 한 세부 정보에 대 한 문서입니다.

   > [!NOTE]
   > 로컬 컴퓨터 tooinstall hello의 관리자 여야 하 고 hello 데이터 관리 게이트웨이 성공적으로 구성 해야 합니다. 추가 사용자 toohello를 추가할 수 있습니다 **데이터 관리 게이트웨이 사용자** 로컬 Windows 그룹입니다. 이 그룹의 hello 구성원 hello 데이터 관리 게이트웨이 구성 관리자 도구 tooconfigure hello 게이트웨이 사용할 수 있습니다.
   >
   >
5. 몇 분 정도 표시 될 때까지 기다리거나 hello 알림 메시지의 뒤에 표시 될 때까지 기다립니다.

    ![성공적인 게이트웨이 설치](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. 컴퓨터에서 **데이터 관리 게이트웨이 구성 관리자** 응용 프로그램을 시작합니다. Hello에 **검색** 창, 형식 **데이터 관리 게이트웨이** tooaccess이 유틸리티입니다. 찾을 수 있습니다 hello 실행 **ConfigManager.exe** hello 폴더에서: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared**

    ![게이트웨이 구성 관리자](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. `adftutorialgateway is connected toohello cloud service` 메시지를 확인합니다. 상태 표시줄 아래쪽 디스플레이 hello hello **toohello 클라우드 서비스 연결** 와 함께 한 **녹색 확인 표시가**합니다.

    Hello에 **홈** 탭 에서도 할 수 있습니다 다음 작업 hello:

   * **등록** hello hello 등록 단추를 사용 하 여 Azure 포털에서에서 게이트웨이 키가 있는 합니다.
   * **중지** hello 데이터 관리 게이트웨이 호스트 서비스 게이트웨이 컴퓨터에서 실행 합니다.
   * **업데이트를 예약할** toobe hello 하루 중 특정 시간에 설치 합니다.
   * Hello 게이트웨이 보기 **마지막으로 업데이트**합니다.
   * 업데이트 toohello 게이트웨이 설치할 수 있는 시간을 지정 합니다.
8. Toohello 전환 **설정** hello에 지정 된 탭 hello 인증서 **인증서** 섹션은 hello 포털에서 사용자가 지정한 hello 온-프레미스 데이터 저장소에 대 한 자격 증명 사용 되는 tooencrypt/암호 해독 합니다. (선택 사항) 클릭 **변경** toouse 고유의 인증서 대신 합니다. 기본적으로 hello 게이트웨이 hello 데이터 팩터리 서비스에서 자동 생성 된 hello 인증서를 사용 합니다.

    ![게이트웨이 인증서 구성](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    수행할 수 있습니다 hello에 다음 작업 hello **설정을** 탭:

   * 보거나 hello 게이트웨이에서 사용 되는 hello 인증서를 내보냅니다.
   * Hello 게이트웨이에서 사용 되는 hello HTTPS 끝점을 변경 합니다.    
   * HTTP 프록시 toobe hello 게이트웨이에서 사용 되는 설정 합니다.     
9. (선택 사항) Toohello 전환 **진단** 탭에서 확인 hello **자세한 정보 로깅 사용** 옵션이 원하는 tooenable 자세한 로깅을 사용할 수 있는 tootroubleshoot 문제 hello 게이트웨이가 설치 된 경우. hello 로깅 정보에서 확인할 수 있습니다 **이벤트 뷰어** 아래 **Applications and Services Logs** -> **데이터 관리 게이트웨이** 노드.

    ![진단 탭](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Hello 다음 hello에 대 한 작업을 수행할 수 있습니다 **진단** 탭:

   * 사용 하 여 **연결 테스트** hello 게이트웨이 사용 하 여 섹션 tooan 온-프레미스 데이터 원본입니다.
   * 클릭 **로그 보기** toosee hello 데이터 관리 게이트웨이 이벤트 뷰어 창에 로그인 합니다.
   * 클릭 **로그 보내기** tooupload 지난 7 일 tooMicrosoft toofacilitate 문제 해결 과정의 문제에 대 한 로그가 포함 된 zip 파일입니다.
10. Hello에 **진단** 탭 hello **연결 테스트** 섹션에서 **SqlServer** hello 유형의 hello 데이터에 대해 저장, 이름이 hello 데이터베이스 서버의 hello 이름을 입력 데이터베이스 hello 인증 유형을 지정, 사용자 이름 및 암호를 입력 하 고 클릭 **테스트** tootest hello 게이트웨이 toohello 데이터베이스를 연결할 수 있는지 여부.
11. 스위치 toohello 웹 브라우저 및 hello **Azure 포털**, 클릭 **확인** hello에 **구성** 페이지 hello에서 **새 데이터 게이트웨이** 페이지입니다.
12. 표시 되어야 **adftutorialgateway** 아래 **데이터 게이트웨이** hello 왼쪽 hello 트리 뷰에서 합니다.  를 클릭 하면 hello JSON 관련 된 표시 됩니다.

## <a name="create-linked-services"></a>연결된 서비스 만들기
이 단계에서는 두 개의 연결된 서비스인 **AzureStorageLinkedService** 및 **SqlServerLinkedService**를 만듭니다. hello **SqlServerLinkedService** 온-프레미스 SQL Server 데이터베이스 및 hello 연결 **AzureStorageLinkedService** 연결 된 서비스는 Azure blob 저장소 toohello 데이터 팩터리를 연결 합니다. Hello 온-프레미스 SQL Server 데이터베이스 toohello Azure blob 저장소에서 데이터를 복사 하는이 연습의 뒷부분에서 파이프라인을 만듭니다.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>연결 된 서비스 tooan 온-프레미스 SQL Server 데이터베이스 추가
1. Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** hello 도구 모음을 선택 **SQL Server**합니다.

   ![새로운 SQL Server 연결 서비스](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. Hello에 **JSON 편집기** hello 오른쪽에서 다음 단계 hello지 않습니다.

   1. Hello에 대 한 **gatewayName**, 지정 **adftutorialgateway**합니다.    
   2. Hello에 **connectionString**, 다음 단계 hello지 않습니다.    

      1. 에 대 한 **servername**, hello hello SQL Server 데이터베이스를 호스팅하는 hello 서버 이름을 입력 하십시오.
      2. 에 대 한 **databasename**, hello 데이터베이스의 hello 이름을 입력 합니다.
      3. 클릭 **Encrypt** hello 도구 모음에서 단추입니다. Hello 자격 증명 관리자 응용 프로그램이 표시 됩니다.

         ![자격 증명 관리자 응용 프로그램](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. Hello에 **자격 증명 설정** 대화 상자, 인증 유형, 사용자 이름 및 암호를 지정 하 고 클릭 **확인**합니다. Hello 연결 완료 되 면 hello 암호화 된 자격 증명 hello JSON에에서 저장 됩니다 및 hello 대화 상자가 닫힙니다.
      5. 자동으로 닫히지 않은 경우 hello 대화 상자를 시작 및 돌아갈 toohello 탭 hello Azure 포털으로 된 hello 빈 브라우저 탭을 닫습니다.

         Hello 게이트웨이 컴퓨터에서 이러한 자격 증명은 **암호화 된** Data Factory hello 인증서를 사용 하 여 서비스를 소유 합니다. 대신 데이터 관리 게이트웨이 hello와 연결 된 toouse hello 인증서 참조 [자격 증명을 안전 하 게 설정](#set-credentials-and-security)합니다.    
   3. 클릭 **배포** hello 명령 toodeploy hello SQL Server에 연결 된 서비스 모음에 있습니다. Hello 연결 된 서비스 hello 트리 뷰에 표시 됩니다.

      ![Hello 트리 보기에서 SQL Server 연결 된 서비스](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Azure 저장소 계정에 대한 연결된 서비스 추가
1. Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** 명령 모음 hello 되 고 클릭 **Azure 저장소**합니다.
2. Hello hello에 대 한 Azure 저장소 계정 이름을 입력 **계정 이름**합니다.
3. Hello에 대 한 Azure 저장소 계정에 대 한 hello 키 입력 **계정 키**합니다.
4. 클릭 **배포** toodeploy hello **AzureStorageLinkedService**합니다.

## <a name="create-datasets"></a>데이터 집합 만들기
이 단계에서는 사용자 입력 및 출력 만드는 hello 복사 작업에 대 한 입력 및 출력 데이터를 나타내는 데이터 집합 (온-프레미스 SQL Server 데이터베이스 = > Azure blob 저장소). 데이터 집합을 만들기 전에 수행 hello (자세한 단계는 hello 목록 뒤) 단계를 수행 합니다.

* 라는 테이블을 만들어 **emp** 에 연결 된 서비스 toohello 데이터 팩터리로 추가 하는 SQL Server 데이터베이스 hello 및 몇 가지 샘플 항목 hello 테이블에 삽입 합니다.
* 라는 blob 컨테이너 만들기 **adftutorial** hello Azure에서에서 blob 저장소 계정을 연결 된 서비스 toohello 데이터 팩터리로 추가 합니다.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Hello 자습서에 대 한 온-프레미스 SQL Server 준비
1. Hello 온-프레미스 SQL Server를 지정 하는 hello 데이터베이스에 연결 된 서비스 (**SqlServerLinkedService**)를 다음 SQL 스크립트 toocreate hello hello를 사용 하 여 **emp** hello 데이터베이스의 테이블입니다.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. 몇 가지 샘플 hello 테이블에 삽입 합니다.

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기

1. Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은**, 클릭 **새 데이터 집합** 명령 모음 hello 되 고 클릭 **SQL Server 테이블**합니다.
2. Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   포인트 다음 참고 hello:

   * **형식** 너무 설정**SqlServerTable**합니다.
   * **tableName** 너무 설정**emp**합니다.
   * **linkedServiceName** 너무 설정**SqlServerLinkedService** (이 연습의 앞부분에서이 연결 된 서비스를 생성 했습니다.).
   * 다른 Azure 데이터 팩터리 파이프라인에서 생성 되지 않습니다는 입력된 데이터 집합을로 설정 해야 **외부** 너무**true**합니다. Hello 입력된 데이터는 생성 된 외부 toohello Azure 데이터 팩터리 서비스를 나타냅니다. Hello를 사용 하 여 모든 외부 데이터 정책을 지정할 수도 있습니다 **externalData** hello 요소 **정책** 섹션.    

   JSON 속성에 대한 자세한 내용은 [SQL Server 간 데이터 이동 데이터 이동](data-factory-sqlserver-connector.md)을 참조하세요.
3. 클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 있습니다.  

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기

1. Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 집합** 명령 모음 hello 되 고 클릭 **Azure Blob 저장소**합니다.
2. Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   포인트 다음 참고 hello:

   * **형식** 너무 설정**AzureBlob**합니다.
   * **linkedServiceName** 너무 설정**AzureStorageLinkedService** (2 단계에서에서이 연결 된 서비스 만든 했습니다).
   * **folderPath** 너무 설정**adftutorial/outfromonpremdf** outfromonpremdf hello adftutorial 컨테이너에서 hello 폴더입니다. Hello 만들기 **adftutorial** 아직 없는 경우에 컨테이너입니다.
   * hello **가용성** 너무 설정**매시간** (**주파수** 도**시간** 및 **간격** 너무 설정 **1**).  hello 데이터 팩터리 서비스에서는 발생 하는 출력 데이터 조각 1 시간 마다 hello에 **emp** hello Azure SQL 데이터베이스의에서 테이블입니다.

   지정 하지 않는 경우는 **fileName** 에 대 한는 **출력 테이블**, hello에 생성 된 hello 파일 **folderPath** 형식에 따라 hello에 이름이 지정: 데이터.<Guid>합니다. txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** 및 **fileName** hello에 따라 동적으로 **SliceStart** 시간 hello partitionedBy 속성을 사용 하십시오. 다음 예제는 hello에서 folderPath hello SliceStart (처리 되 고 hello 조각의 시작 시간)에서 연도, 월 및 일을 사용 하 고 파일 이름을 hello SliceStart에서에서 시간을 사용 합니다. 예를 들어, 2014에 대 한 조각이 생성 되는 경우-10-20T08:00:00, hello folderName toowikidatagateway/wikisampledataout/2014/10/20 설정 및 hello fileName too08.csv 설정 됩니다.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    JSON 속성에 대한 자세한 내용은 [Azure Blob Storage 간의 데이터 이동](data-factory-azure-blob-connector.md)을 참조하세요.
3. 클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 있습니다. Hello 트리 보기에서 두 hello 데이터 집합에 표시 되는지 확인 합니다.  

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **EmpOnPremSQLTable**을 입력으로, **OutputBlobTable**을 출력으로 사용하는 **복사 작업**을 포함하는 **파이프라인**을 만듭니다.

1. [데이터 팩터리 편집기]에서 **... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다.
2. Hello 오른쪽 창에서 JSON hello를 텍스트 다음 hello로 바꿉니다.    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다.
   >
   >

   포인트 다음 참고 hello:

   * Hello 활동 섹션에는 활동만 인 **형식** 너무 설정**복사**합니다.
   * **입력** hello 활동 너무 설정 되어**EmpOnPremSQLTable** 및 **출력** hello 활동 너무 설정 되어**OutputBlobTable**합니다.
   * Hello에 **typeProperties** 섹션 **SqlSource** hello로 지정 된 **소스 형식** 및 * * BlobSink * * hello로 지정 된 **싱크 유형**.
   * SQL 쿼리 `select * from emp` hello에 대 한 지정 된 **sqlReaderQuery** 속성 **SqlSource**합니다.

   start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예: 2014-10-14T16:32:41Z. hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.

   Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다. toorun hello 파이프라인 무제한으로 지정 **9/9/9999** hello에 대 한 hello 값으로 **끝** 속성입니다.

   Hello hello에 따라 어떤 hello 데이터 조각이 처리 되는 시간 기간을 정의 하는 **가용성** 각 Azure 데이터 팩터리 데이터 집합에 대해 정의 된 속성입니다.

   Hello 예제에서는 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.        
3. 클릭 **배포** hello 명령 모음 toodeploy hello 데이터 집합에 (테이블 데이터 집합이 사각형). Hello 파이프라인 hello 트리 보기 아래에 표시 확인 **파이프라인** 노드.  
4. 이제 클릭 **X** 두 번 tooclose hello 페이지 tooget 뒤로 toohello **Data Factory** hello에 대 한 페이지 **ADFTutorialOnPremDF**합니다.

**축하합니다.** Azure 데이터 팩터리에, 연결 된 서비스, 데이터 집합 및 파이프라인 및 예약 된 hello 파이프라인 성공적으로 만들었습니다.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>다이어그램 보기에서 보기 hello 데이터 팩터리
1. Hello에 **Azure 포털**, 클릭 **다이어그램** hello에 대 한 hello 홈 페이지에서 타일 **ADFTutorialOnPremDF** 데이터 팩터리입니다. :

    ![다이어그램 링크](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. 다음 이미지 hello 다이어그램 비슷한 toohello를 나타나야 합니다.

    ![다이어그램 뷰](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    확대, 축소, 확대/축소 too100%, toofit 확대/축소, 자동으로 위치 파이프라인 및 데이터 집합 및 계보 정보를 표시 합니다 (선택 된 항목의 업스트림 및 다운스트림 항목을 강조 표시).  에 대 한 개체 (입/출력 데이터 집합 또는 파이프라인) toosee 속성을 두 번 수 있습니다.

## <a name="monitor-pipeline"></a>파이프라인 모니터링
이 단계에서 진행 되는 상황에서 Azure 데이터 팩터리에 Azure 포털 toomonitor hello를 사용 합니다. PowerShell cmdlet toomonitor 집합과 파이프라인을 사용할 수도 있습니다. 모니터링에 대한 자세한 내용은 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 서를 참조하세요.

1. Hello 다이어그램에서 두 번 클릭 **EmpOnPremSQLTable**합니다.  

    ![EmpOnPremSQLTable 조각](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. 에 있는 모든 hello 데이터 조각이를 사라졌는지 **준비** hello 지난 hello 파이프라인 기간 (시작 시간 tooend 시간) 중 이므로 상태입니다. Hello 데이터 hello SQL Server 데이터베이스에 삽입 한 모든 hello 시간 거기 때문 이기도 합니다. 조각이 없습니다 hello에 표시 되는지 확인 **문제 조각** hello 아래쪽 섹션. tooview 모든 hello 분할 영역 클릭 **더 참조** hello 조각 hello 목록 맨 아래에 있습니다.
3. Hello에 이제 **데이터 집합** 페이지 **OutputBlobTable**합니다.

    ![OputputBlobTable 조각](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Hello 목록에서 데이터 조각을 아무 것 이나 클릭 하 고 hello 표시 되어야 **데이터 조각을** 페이지. Hello 조각에 대 한 활동을 실행 하는 것이 표시 됩니다. 일반적으로 하나의 작업 실행만 표시됩니다.  

    ![데이터 조각 블레이드](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Hello 조각 hello에 없는 경우 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않은 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다.
5. Hello 클릭 **작업 실행** hello 아래쪽 toosee에 hello 목록에서 **활동 실행 정보**합니다.

   ![작업 실행 세부 정보 페이지](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   사용 되는 tootransfer hello 데이터 처리량, 기간 및 hello 게이트웨이 같은 정보를 볼 수 있습니다.
6. 클릭 **X** tooclose 할 때까지 페이지 hello 모든
7. hello에 대 한 toohello 홈 페이지를 다시 가져오기 **ADFTutorialOnPremDF**합니다.
8. (선택 사항) **파이프라인**, **ADFTutorialOnPremDF**를 차례로 클릭한 다음 입력 데이터 집합(**Consumed**) 또는 출력 데이터 집합(**Produced**)을 드릴스루합니다.
9. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) tooverify blob/파일 각 시간에 대해 생성 됩니다.

   ![Azure Storage 탐색기](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>다음 단계
* 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 모든 hello 데이터 관리 게이트웨이 hello에 대 한 세부 정보에 대 한 문서입니다.
* 참조 [Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn toouse 복사 작업 toomove 데이터를 원본 데이터에서에서 tooa 싱크 데이터 저장소를 저장 하는 방법에 대 한 합니다.
