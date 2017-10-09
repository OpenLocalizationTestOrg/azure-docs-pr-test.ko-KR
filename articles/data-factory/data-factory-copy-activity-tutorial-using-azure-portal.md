---
title: "자습서: Azure 데이터 팩터리 파이프라인 toocopy 데이터 (Azure 포털) 만들기 | Microsoft Docs"
description: "이 자습서에서는 Azure blob 저장소 tooan Azure SQL 데이터베이스의 복사 작업 toocopy 데이터로 Azure 포털 toocreate Azure 데이터 팩터리 파이프라인을 사용합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fadd840fe9a15cd8831cdb25dccbd10ac42fa161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-portal-toocreate-a-data-factory-pipeline-toocopy-data"></a>자습서:를 사용 하 여 Azure 포털 toocreate 데이터 팩터리 파이프라인 toocopy 데이터 
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [복사 마법사](data-factory-copy-data-wizard-tutorial.md)
> * [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager 템플릿](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

이 문서에서는 설명 어떻게 toouse [Azure 포털](https://portal.azure.com) toocreate 데이터 팩터리 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인을 사용 합니다. 새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.   

이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다. hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다. 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.

파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요. 

> [!NOTE] 
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.

## <a name="prerequisites"></a>필수 조건
Hello에 나온 필수 조건을 완료 [자습서 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 이 자습서를 수행 하기 전에 문서입니다.

## <a name="steps"></a>단계
이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.

1. Azure **데이터 팩터리**를 만듭니다. 이 단계에서는 ADFTutorialDataFactory라는 데이터 팩터리를 만듭니다. 
2. 만들 **연결 된 서비스** hello data factory에 있습니다. 이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다. 
    
    AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

    AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.   
3. 입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.  
    
    hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

    마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.
4. 만들기는 **파이프라인** hello data factory에 있습니다. 이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.   
    
    hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다. 모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다. 지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요. 
5. 모니터 hello 파이프라인입니다. 이 단계에서는 있습니다 **모니터** Azure 포털을 사용 하 여 입력 및 출력 데이터 집합의 조각을 hello 합니다. 

## <a name="create-data-factory"></a>데이터 팩터리 만들기
> [!IMPORTANT]
> 전체 [hello 자습서에 대 한 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아직 수행 하지 않은 경우.   

데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다. 이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.

1. Toohello 로그인 한 후 [Azure 포털](https://portal.azure.com/), 클릭 **새로** hello 왼쪽된 메뉴를 클릭 **데이터 + 분석**를 클릭 하 고 **Data Factory**합니다. 
   
   ![새로 만들기->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. Hello에 **새 데이터 팩터리** 블레이드:
   
   1. 입력 **ADFTutorialDataFactory** hello에 대 한 **이름**합니다. 
      
         ![새 데이터 팩터리 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다. Hello 다음 오류가 표시 되 면 (예를 들어 yournameADFTutorialDataFactory) hello data factory와 다시 만들어 보십시오.의 hello 이름을 변경 합니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![데이터 팩터리 이름을 사용할 수 없음](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Azure 선택 **구독** toocreate hello 데이터 팩터리 원하는 합니다. 
   3. Hello에 대 한 **리소스 그룹**, hello 다음 단계 중 하나를 수행 합니다.
      
      - 선택 **기존 항목 사용**, hello 드롭 다운 목록에서 기존 리소스 그룹을 선택 합니다. 
      - 선택 **새로 만들기**, 리소스 그룹의 hello 이름을 입력 합니다.   
         
          이 자습서에서는 hello 단계 중 일부를 가정 hello 이름을 사용 합니다: **ADFTutorialResourceGroup** hello 리소스 그룹에 대 한 합니다. 리소스 그룹에 대 한 toolearn 참조 [toomanage Azure 리소스 그룹 리소스를 사용 하 여](../azure-resource-manager/resource-group-overview.md)합니다.  
   4. 선택 hello **위치** hello 데이터 팩토리에 대 한 합니다. Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.
   5. 선택 **Pin toodashboard**합니다.     
   6. **만들기**를 클릭합니다.
      
      > [!IMPORTANT]
      > toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.
      > 
      > hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.                
      > 
      > 
3. 표시 상태와 함께 바둑판식으로 배열 하는 hello 다음 hello 대시보드에서: **배포 데이터 팩터리**합니다. 

    ![데이터 팩터리 배포 중 타일](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. Hello 참조 hello 만들기가 완료 되 면 **Data Factory** 블레이드 hello 이미지에 나와 있는 것 처럼 합니다.
   
   ![데이터 팩터리 홈페이지](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>연결된 서비스 만들기
데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다. 이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다. Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다. 

이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.  

AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. 이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.  

### <a name="create-azure-storage-linked-service"></a>Azure 저장소 연결된 서비스 만들기
이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.  

1. Hello에 **Data Factory** 블레이드에서 클릭 **작성자 및 배포** 바둑판식으로 배열입니다.
   
   ![작성 및 배포 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. Hello 참조 **데이터 팩터리 편집기** hello 다음 이미지와 같이: 

    ![데이터 팩터리 편집기](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. Hello 편집기 클릭 **새 데이터 저장소** hello 도구 모음을 선택 하는 단추 **Azure 저장소** hello 드롭 다운 메뉴에서 합니다. Hello 오른쪽 창에서 Azure 저장소 연결 서비스를 만들기 위한 hello JSON 템플릿이 표시 되어야 합니다. 
   
    ![편집기 새 데이터 저장소 단추](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. 대체 `<accountname>` 및 `<accountkey>` hello 계정 이름 및 계정 키 값을 가진 Azure 저장소 계정에 대 한 합니다. 
   
    ![편집기 Blob 저장소 JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. 클릭 **배포** hello 도구 모음입니다. 배포 된 hello 표시 되어야 **AzureStorageLinkedService** hello 트리에 지금를 보고 합니다. 
   
    ![편집기 Blob 저장소 배포](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    연결 된 hello 서비스 정의에 JSON 속성에 대 한 자세한 내용은 참조 [Azure Blob 저장소 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서.

### <a name="create-a-linked-service-for-hello-azure-sql-database"></a>Hello Azure SQL 데이터베이스에 대 한 연결 된 서비스 만들기
이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다. 이 섹션의 hello Azure SQL server 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다. 

1. Hello에 **데이터 팩터리 편집기**, 클릭 **새 데이터 저장소** hello 도구 모음을 선택 하는 단추 **Azure SQL 데이터베이스** hello 드롭 다운 메뉴에서 합니다. Hello 오른쪽 창에 hello Azure SQL 연결 서비스를 만들기 위한 hello JSON 템플릿이 표시 되어야 합니다.
2. `<servername>`, `<databasename>`, `<username>@<servername>` 및 `<password>`를 Azure SQL Server의 이름, 사용자 계정 및 암호로 바꿉니다. 
3. 클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **AzureSqlLinkedService**합니다.
4. 표시 되는지 확인 **AzureSqlLinkedService** 아래 hello 트리 보기에서 **연결 된 서비스**합니다.  

    이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.

## <a name="create-datasets"></a>데이터 집합 만들기
Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다. 이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.

hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다. 

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다. 하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다. 이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다. 

1. Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 더 많은**, 클릭 **새 데이터 집합**를 클릭 하 고 **Azure Blob 저장소** hello 드롭 다운 메뉴에서 합니다. 
   
    ![새 데이터 집합 메뉴](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다. 
   
    ```json
    {
      "name": "InputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    | 속성 | 설명 |
    |:--- |:--- |
    | type | hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다. |
    | linkedServiceName | Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다. |
    | folderPath | Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다. 이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다. | 
    | fileName | 이 속성은 선택 사항입니다. 이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다. 이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다. |
    | format -> type |사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다. |
    | columnDelimiter | hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다. |
    | frequency/interval | hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다. 즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다. Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.  |
    | external | 이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다. 이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다. |

    이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.      
3. 클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **InputDataset** 데이터 집합입니다. Hello 표시 되는지 확인 **InputDataset** hello 트리 보기에서 합니다.

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. hello 출력 SQL 테이블 데이터 집합 (OututDataset)이이 단계에서 만드는 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.

1. Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 더 많은**, 클릭 **새 데이터 집합**를 클릭 하 고 **Azure SQL** hello 드롭 다운 메뉴에서 합니다. 
2. JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다.

    ```json   
    {
      "name": "OutputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     

    hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.

    | 속성 | 설명 |
    |:--- |:--- |
    | type | hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다. |
    | linkedServiceName | Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다. |
    | tableName | 지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다. | 
    | frequency/interval | hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.  |

    세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다. Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.

    이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.
3. 클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **OutputDataset** 데이터 집합입니다. Hello 표시 되는지 확인 **OutputDataset** 아래 hello 트리 보기에서 **데이터 집합**합니다. 

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.

현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다. hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다. 따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다. 

1. Hello에 **편집기** hello Data Factory에 대 한 클릭 **중... 추가**를 클릭하고 **새 파이프라인**을 클릭합니다. 단추로 또는 **파이프라인** hello 트리 뷰 및 클릭 **새 파이프라인**합니다.
2. JSON을 hello 오른쪽 창에서 다음 JSON 코드 조각은 hello 바꿉니다. 

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob tooAzure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    포인트 다음 참고 hello:
   
    - Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다. Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.
    - Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다. 
    - Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. 원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.
    - start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예를 들어 2016-10-14T16:32:41Z입니다. hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다. Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다. toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.
     
    앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.

    파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요. BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요. SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.
3. 클릭 **배포** 도구 모음 toocreate hello 되 고 hello 배포 **ADFTutorialPipeline**합니다. Hello 파이프라인 hello 트리 보기에 표시 되는지 확인 합니다. 
4. Hello, 닫습니다 **편집기** 블레이드를 클릭 하 여 **X**합니다. 클릭 **X** 다시 toosee hello **Data Factory** hello에 대 한 홈 페이지 **ADFTutorialDataFactory**합니다.

**축하합니다.** Azure blob 저장소 tooan Azure SQL 데이터베이스의 파이프라인 toocopy 데이터로 Azure 데이터 팩터리에 성공적으로 만들었습니다. 


## <a name="monitor-pipeline"></a>파이프라인 모니터링
이 단계에서 진행 되는 상황에서 Azure 데이터 팩터리에 Azure 포털 toomonitor hello를 사용 합니다.    

### <a name="monitor-pipeline-using-monitor--manage-app"></a>앱 모니터링 및 관리를 사용하여 파이프라인 모니터링
hello 다음 단계 보여 toomonitor data factory에 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 파이프라인 하는 방법: 

1. 클릭 **모니터링 및 관리** 데이터 팩토리에 대 한 hello 홈 페이지에 바둑판식으로 배열 합니다.
   
    ![타일 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. 별도의 탭에서 **모니터링 및 관리 응용 프로그램**이 표시되어야 합니다. 

    > [!NOTE]
    > 해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 hello 다음 중 하나를 수행: 지우기 hello **타사 쿠키를 차단 하 고 사이트 데이터** 확인란 (또는)에 대 한 예외를 만들려면 **login.microsoftonline.com**, 후 tooopen hello 응용 프로그램을 다시 시도 하십시오.

    ![앱 모니터링 및 관리](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. 변경 hello **시작 시간** 및 **종료 시간** tooinclude (2017-05-11)를 시작 및 종료 시간 (2017-05-12), 파이프라인의 고 클릭 **적용**합니다.     
3. Hello 참조 **활동 창** 파이프라인 시작과 끝 사이의 매시간와 관련 된 hello 가운데 창에서 hello 목록에는 시간입니다. 
4. 선택 활동 창에 대 한 세부 정보 toosee hello hello에서 작업 창을 **활동 창** 목록입니다. 
    ![활동 창 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

    Hello 오른쪽에 작업 창 탐색기에서 해당 hello toohello 현재 UTC 시간 조각이 표시 (오후 8시 12분) 모두 (녹색)으로 처리 합니다. hello 8-오후 9, 9-10 PM, 10-11 오후, 오후 11-오전 12 시 분할 영역을 아직 처리 되지 않습니다.

    hello **시도** hello hello 데이터 조각에 대 한 실행 hello 활동에 대 한 정보를 제공 하는 창 오른쪽에 섹션입니다. 오류가 경우 hello 오류에 대 한 세부 정보를 제공 합니다. 예를 들어 hello 폴더 또는 컨테이너를 입력 하는 경우 하지 존재 않으며 hello 조각 처리 실패 하면 해당 hello 컨테이너 없다는 오류 메시지가 표시 또는 폴더가 존재 하지 않습니다.

    ![활동 실행 시도](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. 시작 **SQL Server Management Studio**toohello Azure SQL 데이터베이스를 연결 하 고 hello 행 toohello에 넣었는지 확인 **emp** hello 데이터베이스의 테이블입니다.
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.

### <a name="monitor-pipeline-using-diagram-view"></a>다이어그램 보기를 사용하여 파이프라인 모니터링
Hello 다이어그램 보기를 사용 하 여 모니터 데이터 파이프라인 수도 있습니다.  

1. Hello에 **Data Factory** 블레이드에서 클릭 **다이어그램**합니다.
   
    ![데이터 팩터리 블레이드 - 다이어그램 타일](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. 다음 이미지 hello 다이어그램 비슷한 toohello를 나타나야 합니다. 
   
    ![다이어그램 뷰](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. Hello 다이어그램 보기에서 두 번 클릭 **InputDataset** hello 데이터 집합에 대 한 toosee 슬라이스입니다.  
   
    ![InputDataset을 선택한 데이터 집합](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. 클릭 **더 보려면** toosee 모든 hello에 대 한 데이터 분할 영역을 연결 합니다. 24시간의 매시간 조각 중 파이프라인의 시작 시간과 종료 시간 사이에 있는 조각이 표시됩니다. 
   
    ![모든 입력 데이터 조각](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    데이터 조각이 toohello 현재 UTC 시간을 hello 모든 **준비** 때문에 hello **emp.txt** hello blob 컨테이너에 파일이 있는 모든 hello 시간: **adftutorial\input**. hello 조각 hello 이후 시간에 대 한 준비 상태에 아직 없는 합니다. 조각이 없습니다 hello에 표시 되는지 확인 **최근에 실패 한 조각이** hello 아래쪽 섹션.
6. 닫기 hello 블레이드 할 때까지 hello 다이어그램 보기 (또는) 스크롤 왼쪽된 toosee hello 다이어그램 보기를 참조 하십시오. 그런 다음 **OutputDataset**을 두 번 클릭합니다. 
8. 클릭 **더 보려면** hello에 대 한 링크 **테이블** 블레이드 **OutputDataset** toosee 모든 분할 영역을 hello 합니다.

    ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. Toohello 현재 UTC 시간을 분할 영역을 hello 모든 공지에서 이동 **실행 보류** 상태 = > **진행에서** ==> **준비** 상태입니다. 지난 hello 분할 영역 hello (현재 시간 전) 최신 toooldest에서 기본적으로 처리 됩니다. 예를 들어 hello 현재 시간이 오후 8시 12분 UTC 일 경우 hello 분할 영역에 대 한 오후 7 시-오후 8 시 hello 오후 6 시-오후 7 시 분할 영역 보다 먼저 처리 됩니다. hello 오후 8 시-오후 9 시 분할 영역 hello 시간 간격의 hello 끝에 오후 9 시 뒤에 있는 기본적으로 처리 됩니다.  
10. Hello 목록에서 데이터 조각을 아무 것 이나 클릭 하 고 hello 표시 되어야 **데이터 조각을** 블레이드입니다. 활동 창과 연결된 데이터 부분을 조각이라고 합니다. 조각은 하나의 파일이거나 여러 파일일 수 있습니다.  
    
     ![데이터 조각 블레이드](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     Hello 조각 hello에 없는 경우 **준비** 상태 hello 업스트림 슬라이스입니다. 준비 되지 않은 hello 현재 조각 hello에서 실행할 수 없도록 차단 하 고 볼 수 있습니다 **준비 되지 않은 업스트림 슬라이스** 목록입니다.
11. Hello에 **데이터 조각을** 블레이드를 표시 되어야 hello 맨 아래에 hello 목록에서 모든 활동을 실행 합니다. 클릭는 **작업 실행** toosee hello **활동 실행 정보** 블레이드입니다. 
    
    ![작업 실행 세부 정보](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    이 블레이드에 표시 긴 hello 복사 작업을 진행 하려면 방법 어떤 출력은 데이터의 바이트 수 된 읽기 및 작성, 실행 시작 시간, 종료 시간 등을 실행 하는입니다.  
12. 클릭 **X** tooclose 할 때까지 모든 hello 블레이드에 돌아갈 hello에 대 한 홈 블레이드 toohello **ADFTutorialDataFactory**합니다.
13. (선택 사항)을 클릭 hello **데이터 집합** 타일 또는 **파이프라인** 타일 tooget hello 블레이드 살펴본 hello 앞의 단계입니다. 
14. 시작 **SQL Server Management Studio**toohello Azure SQL 데이터베이스를 연결 하 고 hello 행 toohello에 넣었는지 확인 **emp** hello 데이터베이스의 테이블입니다.
    
    ![SQL 쿼리 결과](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a>요약
이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다. Hello Azure 포털 toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다. 이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.  

1. Azure **데이터 팩터리**를 만들었습니다.
2. **연결된 서비스**를 만들었습니다.
   1. **Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하 여 Azure 저장소 계정을 연결 합니다.     
   2. **Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다. 
3. 파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합** 을 만들었습니다.
4. 원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다.  

## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.
