---
title: "자습서: 복사 마법사를 사용하여 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure 데이터 팩터리 파이프라인 복사 활동으로 사용 하 여 만들면 hello Data Factory에서 지 원하는 복사 마법사"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>자습서: 데이터 팩터리 복사 마법사를 사용하여 복사 작업이 있는 파이프라인 만들기
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)

이 자습서에서는 어떻게 toouse hello **복사 마법사** toocopy 데이터를 Azure blob 저장소 tooan Azure SQL 데이터베이스입니다. 

Azure Data Factory hello **복사 마법사** 있습니다 tooquickly 지원 되는 원본 데이터 저장소 지원 tooa 대상 데이터 저장소에서 데이터를 복사 하는 데이터 파이프라인을 만듭니다. 따라서 데이터 이동 시나리오에 대 한 첫 번째 단계 toocreate 샘플 파이프라인으로 hello 마법사를 사용 하는 것이 좋습니다. 원본 및 대상으로 지원되는 데이터 저장소의 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.  

이 자습서에서는 어떻게 toocreate Azure 데이터 팩터리에 시작 hello 복사 마법사는 일련의 데이터 수집/이동 시나리오에 대 한 단계 tooprovide 정보를 이동 합니다. Hello 마법사의 단계를 완료 하면 hello 마법사 파이프라인 Azure blob 저장소 tooan Azure SQL 데이터베이스의 복사 작업 toocopy 데이터로 자동으로 만듭니다. 복사 활동에 대한 자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
Hello에 나온 필수 조건을 완료 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 이 자습서를 수행 하기 전에 문서입니다.

## <a name="create-data-factory"></a>데이터 팩터리 만들기
이 단계를 사용 하 여 Azure 포털 toocreate 라는 Azure 데이터 팩터리에 hello **ADFTutorialDataFactory**합니다.

1. 로그 너무[Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **+ 새로 만들기** hello 왼쪽 위 모퉁이에서 클릭 **데이터 + 분석**를 클릭 하 고 **Data Factory**합니다. 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. Hello에 **새 데이터 팩터리** 블레이드:
   
   1. 입력 **ADFTutorialDataFactory** hello에 대 한 **이름**합니다.
       hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. Hello 오류가 나타나면: `Data factory name “ADFTutorialDataFactory” is not available`을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFTutorialDataFactoryYYYYMMDD)을 변경 하 고 다시 만들어 보십시오. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Azure **구독**을 선택합니다.
   3. 리소스 그룹에 대 한 단계를 수행 하는 hello 중 하나를 수행 합니다. 
      
      - 선택 **기존 항목 사용** tooselect 기존 리소스 그룹입니다.
      - 선택 **새로 만들기** tooenter 리소스 그룹에 대 한 이름입니다.
          
        이 자습서에서는 hello 단계 중 일부를 가정 hello 이름을 사용 합니다: **ADFTutorialResourceGroup** hello 리소스 그룹에 대 한 합니다. 리소스 그룹에 대 한 toolearn 참조 [toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-overview.md)합니다.
   4. 선택 된 **위치** hello 데이터 팩토리에 대 한 합니다.
   5. 선택 **Pin toodashboard** hello hello 블레이드 맨 아래에 있는 확인란 합니다.  
   6. **만들기**를 클릭합니다.
      
       ![새 데이터 팩터리 블레이드](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. Hello 참조 hello 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 블레이드:
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>복사 마법사 시작
1. Hello Data Factory 블레이드에서 클릭 **[미리 보기] 데이터 복사** toolaunch hello **복사 마법사**합니다. 
   
   > [!NOTE]
   > 해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 사용 안 함/취소 **타사 쿠키를 차단 하 고 사이트 데이터** hello 브라우저 설정 (또는) 유지 하지만 사용 하도록 설정에서 설정 하 고 예외를 만들  **login.microsoftonline.com** 및 hello 마법사를 다시 시작 해 보십시오.
2. Hello에 **속성** 페이지:
   
   1. **태스크 이름**에 **CopyFromBlobToAzureSql**을 입력합니다.
   2. **설명** 을 입력합니다(선택 사항).
   3. 변경 hello **시작 날짜 시간이** 및 hello **종료 날짜 시간** hello 종료 날짜는 tootoday를 설정 하 고 toofive 일 전인 날짜 시작 되도록 합니다.  
   4. **다음**을 누릅니다.  
      
      ![복사 도구 - 속성 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. Hello에 **소스 데이터 저장소** 페이지 **Azure Blob 저장소** 바둑판식으로 배열입니다. 이 페이지 toospecify hello 원본 데이터 저장소를 사용 하 여 hello 복사 작업에 대 한 합니다. 
   
    ![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. Hello에 **hello Azure Blob 저장소 계정을 지정** 페이지:
   
   1. **연결된 서비스 이름**에 **AzureStorageLinkedService**를 입력합니다.
   2. **계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.
   3. Azure **구독**을 선택합니다.  
   4. 선택 된 **Azure 저장소 계정** hello에서 목록은 Azure 저장소 계정 선택 hello 구독에서 사용할 수 있습니다. 선택할 수도 있습니다 tooenter 저장소 계정 설정을 수동으로 선택 하 여 **수동으로 입력** hello에 대 한 옵션 **계정 선택 방법을**, 클릭 하 고 **다음**합니다. 
      
      ![도구에 복사-hello Azure Blob 저장소 계정을 지정 합니다.](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. **선택 hello 입력된 파일이 나 폴더** 페이지:
   
   1. **adftutorial**(폴더)을 두 번 클릭합니다.
   2. **emp.txt**를 선택하고 **선택**을 클릭합니다.
      
      ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. Hello에 **선택 hello 입력된 파일이 나 폴더** 페이지 **다음**합니다. **이진 복사**를 선택하지 않습니다. 
   
    ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. Hello에 **파일 형식 설정** hello 구분 기호 및 hello 파일을 구문 분석 하 여 hello 마법사에 의해 자동으로 감지 있는 hello 스키마 참조 페이지입니다. 또한 hello 복사 마법사 toostop 자동 검색할 또는 toooverride hello 구분 기호를 수동으로 입력할 수 있습니다. 클릭 **다음** hello 구분 기호를 검토 하 고 데이터를 미리 봅니다. 
   
    ![복사 도구 - 파일 형식 설정](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. Hello 대상 데이터 페이지를 저장, 선택 **Azure SQL 데이터베이스**를 클릭 하 고 **다음**합니다.
   
    ![복사 도구 - 대상 저장소 선택](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. **지정 hello Azure SQL 데이터베이스** 페이지:
   
   1. 입력 **AzureSqlLinkedService** hello에 대 한 **연결 이름** 필드입니다.
   2. **서버/데이터베이스 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.
   3. Azure **구독**을 선택합니다.  
   4. **서버 이름** 및 **데이터베이스**를 선택합니다.
   5. **사용자 이름** 및 **암호**를 입력합니다.
   6. **다음**을 누릅니다.  
      
      ![복사 도구 - Azure SQL Database 지정](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. Hello에 **테이블 매핑** 페이지에서 **emp** hello에 대 한 **대상** hello 드롭 다운 목록에서 필드를 클릭 **아래쪽 화살표** (선택 사항) toosee hello 스키마 및 toopreview hello 데이터입니다.
    
     ![복사 도구 - 테이블 매핑](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. Hello에 **스키마 매핑** 페이지 **다음**합니다.
    
    ![복사 도구 - 스키마 매핑](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. Hello에 **성능 설정** 페이지 **다음**합니다. 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Hello에 대 한 정보를 검토 **요약** 페이지를 클릭 하 여 **마침**합니다. hello 마법사 (여기서 hello 복사 마법사를 실행)에서 hello data factory에 두 개의 연결 된 서비스, 두 개의 데이터 집합 (입력 및 출력) 및 하나의 파이프라인을 만듭니다. 
    
    ![복사 도구 - 성능 설정](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>응용 프로그램 모니터링 및 관리 시작
1. Hello에 **배포** 페이지에서 hello 링크 클릭: `Click here toomonitor copy pipeline`합니다.
   
   ![복사 도구 - 배포 성공 페이지](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. 응용 프로그램을 모니터링 하는 hello 웹 브라우저에서 별도 탭에서 시작 됩니다.   
   
   ![모니터링 앱](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. 시간 조각의 toosee hello 최신 상태를 클릭 **새로 고침** hello 단추 **활동 창** hello 맨 아래에는 목록입니다. 5 개 활동 windows hello 파이프라인에 대 한 시작 및 종료 시간 사이의 5 일 동안 표시 됩니다. hello 목록이 자동으로 새로 고쳐진 하지, 다음과 같은 행위는 하므로 필요 tooclick 새로 고침 몇 번 모든 hello 활동 windows hello 준비 상태에서를 보기 전에 합니다. 
4. Hello 목록에서 활동을 선택 합니다. Hello에 대 한 hello 세부 사항을 볼 **활동 창 탐색기** hello 오른쪽에 있습니다.

    ![활동 창 세부 정보](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    즉, 이러한 날짜에 대 한 hello 매일 출력 조각만 생성 이미 녹색에서 11, 12, 13, 14 및 15 hello 날짜는 확인 합니다. 또한이 색 구분 hello 파이프라인에서 참조 하 고 hello 다이어그램 보기에서 출력 데이터 집합을 hello 합니다. Hello 이전 단계에서 고 해당 데이터베이스 두 슬라이스 이미 생성 된 파일, 한 조각 현재 처리 중인 hello 다른 두 대기 중인 toobe 처리 (hello 색 구분에 따라). 

    이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

데이터 저장소에 대 한 hello 복사 마법사에서 볼 수 있는 필드/속성에 대 한 자세한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다. 
