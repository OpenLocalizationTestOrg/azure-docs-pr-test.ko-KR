---
title: "자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기 | Microsoft Docs"
description: "이 자습서에서는 Visual Studio를 사용하여 복사 작업이 있는 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a>자습서: Visual Studio를 사용하여 복사 작업이 있는 파이프라인 만들기
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

이 문서에서는 어떻게 toouse hello Microsoft Visual Studio toocreate Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인으로 데이터 팩터리 방법을 배웁니다. 새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.   

이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다. hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다. 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요. hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.

파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.

> [!NOTE] 
> 이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.

## <a name="prerequisites"></a>필수 조건
1. 자세히 읽고 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 아티클과 전체 hello **필수** 단계입니다.       
2. toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.
3. Hello 다음이 컴퓨터에 설치 되어 있어야 합니다. 
   * Visual Studio 2013 또는 Visual Studio 2015
   * Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다. 너무 이동[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/) 클릭 **VS 2013** 또는 **VS 2015** hello에 **.NET** 섹션.
   * Visual Studio에 대 한 hello 최신 Azure Data Factory 플러그 인을 다운로드: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)합니다. Hello 다음 단계를 수행 하 여 hello 플러그 인을 업데이트할 수도 있습니다: hello 메뉴를 클릭 **도구** -> **확장명 및 업데이트** -> **온라인**  ->  **Visual Studio 갤러리** -> **Visual Studio 용 Microsoft Azure 데이터 팩터리 도구** -> **업데이트**합니다.

## <a name="steps"></a>단계
이 자습서의 일환으로 수행 하는 hello 단계는 다음과 같습니다.

1. 만들 **연결 된 서비스** hello data factory에 있습니다. 이 단계에서는 두 가지 연결된 서비스 유형, 즉 Azure Storage와 Azure SQL Database를 만듭니다. 
    
    AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

    AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 SQL 테이블을 만들었습니다.     
2. 입력 및 출력 만들기 **데이터 집합** hello data factory에 있습니다.  
    
    hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

    마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 출력 SQL 테이블의 데이터 집합 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.
3. 만들기는 **파이프라인** hello data factory에 있습니다. 이 단계에서는 복사 활동을 사용하여 파이프라인을 만듭니다.   
    
    hello 복사 활동 hello Azure blob 저장소 tooa hello Azure SQL 데이터베이스의 테이블에 blob에서 데이터를 복사합니다. 모든 지원 되는 원본 tooany 지원 대상에서 파이프라인 toocopy 데이터에서 복사 작업을 사용할 수 있습니다. 지원되는 데이터 저장소 목록은 [데이터 이동 활동](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 문서를 참조하세요. 
4. Data Factory 엔터티(연결된 서비스, 데이터 집합/테이블 및 파이프라인)를 배포할 때 Azure **데이터 팩터리**를 만듭니다. 

## <a name="create-visual-studio-project"></a>Visual Studio 프로젝트 만들기
1. **Visual Studio 2015**를 시작합니다. 클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다. Hello 표시 되어야 **새 프로젝트** 대화 상자.  
2. Hello에 **새 프로젝트** 대화 상자에서 선택 hello **DataFactory** 템플릿과 클릭 **빈 데이터 팩터리 프로젝트**합니다.  
   
    ![새 프로젝트 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. Hello 이름 hello 프로젝트, hello 솔루션에 대 한 위치 및 hello 솔루션의 이름을 지정 하 고 클릭 **확인**합니다.
   
    ![솔루션 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a>연결된 서비스 만들기
데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다. 이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다. Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다. 

따라서 두 가지 연결된 서비스 유형, 즉 AzureStorage와 AzureSqlDatabase를 만듭니다.  

hello Azure 저장소는 Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결합니다. 이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.   

Azure SQL Azure SQL 데이터베이스 toohello 데이터 팩터리 서비스 링크를 연결합니다. hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다. 이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.

연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다. 참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다. 참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 합니다. 이 자습서에서는 계산 서비스를 사용하지 않습니다. 

### <a name="create-hello-azure-storage-linked-service"></a>Hello Azure 저장소 연결 된 서비스 만들기
1. **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **연결 된 서비스**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.      
2. Hello에 **새 항목 추가** 대화 상자에서 **Azure 저장소 연결 된 서비스** hello 목록 및 클릭에서 **추가**합니다. 
   
    ![새 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. 대체 `<accountname>` 및 `<accountkey>`* Azure 저장소 계정 및 키의 hello 이름의 합니다. 
   
    ![Azure 저장소 연결된 서비스](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. Hello 저장 **AzureStorageLinkedService1.json** 파일입니다.

    연결 된 hello 서비스 정의에 JSON 속성에 대 한 자세한 내용은 참조 [Azure Blob 저장소 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서.

### <a name="create-hello-azure-sql-linked-service"></a>Hello Azure SQL 연결 서비스 만들기
1. 마우스 오른쪽 단추로 클릭 **연결 된 서비스** hello에 대 한 노드 **솔루션 탐색기** 다시 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다. 
2. 이번에는 **Azure SQL 연결된 서비스**를 선택하고 **추가**를 클릭합니다. 
3. Hello에 **AzureSqlLinkedService1.json 파일**, 대체 `<servername>`, `<databasename>`, `<username@servername>`, 및 `<password>` Azure SQL server, 데이터베이스, 사용자 계정 및 암호의 이름으로 합니다.    
4. Hello 저장 **AzureSqlLinkedService1.json** 파일입니다. 
    
    이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL Database 커넥터](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.


## <a name="create-datasets"></a>데이터 집합 만들기
Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다. 이 단계에서는 InputDataset 및 입력을 나타내는 OutputDataset 각각 AzureStorageLinkedService1 및 AzureSqlLinkedService1에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.

hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 고 hello 입력된 blob 데이터 집합 (InputDataset) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.  

마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다. 및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다. 

### <a name="create-input-dataset"></a>입력 데이터 집합 만들기
이 단계에서는 hello hello AzureStorageLinkedService1 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 InputDataset 라는 데이터 집합이 만듭니다. 하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다. 이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다. 

여기에서 "데이터 집합" 아닌 hello 용어 "tables"를 사용합니다. 사각형 데이터 집합은 테이블과 현재 지원 되는 데이터 집합의 hello만 유형입니다. 

1. 마우스 오른쪽 단추로 클릭 **테이블** hello에 **솔루션 탐색기**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. Hello에 **새 항목 추가** 대화 상자에서 **Azure Blob**를 클릭 하 고 **추가**합니다.   
3. 텍스트 다음 hello로 hello JSON 텍스트를 바꾸고 hello 저장 **AzureBlobLocation1.json** 파일입니다. 

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
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
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

### <a name="create-output-dataset"></a>출력 데이터 집합 만들기
이 단계에서는 **OutputDataset**이라는 출력 데이터 집합을 만듭니다. 이 데이터 집합으로 표시 하는 hello Azure SQL 데이터베이스의 tooa SQL 테이블 점은 **AzureSqlLinkedService1**합니다. 

1. 마우스 오른쪽 단추로 클릭 **테이블** hello에 **솔루션 탐색기** 다시 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. Hello에 **새 항목 추가** 대화 상자에서 **Azure SQL**를 클릭 하 고 **추가**합니다. 
3. 다음 JSON hello로 hello JSON 텍스트를 바꾸고 hello 저장 **AzureSqlTableLocation1.json** 파일입니다.

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
       "linkedServiceName": "AzureSqlLinkedService1",
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

## <a name="create-pipeline"></a>파이프라인 만들기
이 단계에서는 **InputDataset**을 입력으로 사용하고 **OutputDataset**을 출력으로 사용하는 **복사 활동**을 포함한 파이프라인을 만듭니다.

현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다. 이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다. hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다. 따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다. 

1. 마우스 오른쪽 단추로 클릭 **파이프라인** hello에 **솔루션 탐색기**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.  
2. 선택 **복사본 데이터 파이프라인** hello에 **새 항목 추가** 대화 상자와 클릭 **추가**합니다. 
3. 다음 JSON hello hello JSON 바꾸고 hello 저장 **CopyActivity1.json** 파일입니다.

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
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다. Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다. Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.
    - Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다. 
    - Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다. 원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.  
     
    Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다. Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다. 예를 들어 "2016-02-03", 즉 너무 "2016-02-03T00:00:00Z"
     
    start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예를 들어 2016-10-14T16:32:41Z입니다. hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다. 
     
    Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다. toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.
     
    앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.

    파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요. BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요. SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.

## <a name="publishdeploy-data-factory-entities"></a>데이터 팩터리 엔터티 게시/배포
이 단계에서는 이전에 만든 Data Factory 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)를 게시합니다. 또한 이러한 엔터티 toohold 만든 hello 새 데이터 팩터리 toobe의 hello 이름을 지정 합니다.  

1. Hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다. 
2. 표시 되 면 **tooyour Microsoft 계정 로그인** 대화 상자에서 Azure 구독이 있는 hello 계정에 대 한 자격 증명을 입력 하 고 클릭 **로그인**합니다.
3. 대화 상자를 수행 하는 hello를 표시 되어야 합니다.
   
   ![게시 대화 상자](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. Hello 구성 데이터 팩터리 페이지에서 다음 단계 hello지 않습니다. 
   
   1. **새 데이터 팩터리 만들기** 옵션을 선택합니다.
   2. **이름**에 **VSTutorialFactory**를 입력합니다.  
      
      > [!IMPORTANT]
      > hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. 게시 하는 경우 데이터 팩터리의 이름 hello에 대 한 오류가 나타나면 hello 이름 (예를 들어 yournameVSTutorialFactory) hello 데이터 팩터리 및 다시 게시 시도 변경 합니다. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.        
      > 
      > 
   3. Hello에 대 한 Azure 구독 선택 **구독** 필드입니다.
      
      > [!IMPORTANT]
      > 모든 구독을 표시 되지 않으면 관리자 또는 hello 구독 공동 관리자 인 계정을 사용 하 여 로그인을 확인 합니다.  
      > 
      > 
   4. 선택 hello **리소스 그룹** hello 데이터 팩터리 toobe 생성에 대 한 합니다. 
   5. 선택 hello **지역** hello 데이터 팩토리에 대 한 합니다. Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.
   6. 클릭 **다음** tooswitch toohello **게시 항목** 페이지.
      
       ![데이터 팩터리 페이지 구성](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. Hello에 **게시 항목** 페이지에서 엔터티를 선택 하 고 클릭 하 여 데이터 팩터리를 hello 모든 **다음** tooswitch toohello **요약** 페이지.
   
   ![항목 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. Hello 요약을 검토 하 고 클릭 **다음** toostart hello 배포 프로세스와 보기 hello **배포 상태**합니다.
   
   ![요약 페이지 게시](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. Hello에 **배포 상태** 페이지 hello 배포 프로세스의 hello 상태 표시 되어야 합니다. Hello 배포를 완료 한 후 마침을 클릭 합니다.
 
   ![배포 상태 페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

포인트 다음 참고 hello: 

* Hello 오류가 나타나면: "이이 등록은 등록된 toouse 네임 스페이스가 microsoft.datafactory가 아닙니다" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오. 
  
  * Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다. 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다. 이 동작은 hello 공급자를 자동으로 등록합니다.
* hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.

> [!IMPORTANT]
> 관리자/공동 관리자의 Azure 구독 hello toobe 해야 toocreate 데이터 팩터리 인스턴스

## <a name="monitor-pipeline"></a>파이프라인 모니터링
데이터 팩토리에 대 한 toohello 홈 페이지를 탐색 합니다.

1. 로그 너무[Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **더 많은 서비스** 왼쪽된 메뉴 hello 되 고 클릭 **데이터 팩터리**합니다.

    ![데이터 팩터리 찾아보기](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. 데이터 팩터리의 hello 이름을 입력 하기 시작 합니다.

    ![데이터 팩터리의 이름](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. 데이터 팩터리 hello 결과 목록 toosee hello 홈 페이지에서 데이터 팩터리를 클릭 합니다.

    ![데이터 팩터리 홈페이지](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. 지침에 따라 [모니터링 데이터 집합 및 파이프라인](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) 이 자습서에서 만든 toomonitor hello 파이프라인 및 데이터 집합입니다. Visual Studio는 현재 Data Factory 파이프라인 모니터링을 지원하지 않습니다. 

## <a name="summary"></a>요약
이 자습서에서는 Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 만들었습니다. Visual Studio toocreate hello 데이터 팩터리, 연결 된 서비스, 데이터 집합 및 파이프라인을 사용 했습니다. 이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.  

1. Azure **데이터 팩터리**를 만들었습니다.
2. **연결된 서비스**를 만들었습니다.
   1. **Azure 저장소** 서비스 toolink 입력된 데이터를 보유 하 여 Azure 저장소 계정을 연결 합니다.     
   2. **Azure SQL** 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다. 
3. 파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합**을 만들었습니다.
4. 원본으로 **BlobSource**를 사용하고 싱크로 **SqlSink**를 사용하는 **복사 작업**으로 **파이프라인**을 만들었습니다. 

toouse Azure HDInsight 클러스터를 사용 하 여 HDInsight Hive 활동 tootransform 데이터를 확인 하려면 어떻게 toosee [ 자습서: Hadoop 클러스터를 사용 하 여 첫 번째 파이프라인 tootransform 데이터 빌드](data-factory-build-your-first-pipeline.md)합니다.

Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요. 

## <a name="view-all-data-factories-in-server-explorer"></a>서버 탐색기에서 모든 데이터 팩터리 보기
이 섹션에서는 toouse 모든 hello 데이터 팩터리에 Azure 구독에서 서버 탐색기에서 Visual Studio tooview hello 및 기존 데이터 팩토리를 기반으로 Visual Studio 프로젝트를 만드는 방법을 설명 합니다. 

1. **Visual Studio**, 클릭 **보기** 메뉴 hello 되 고 클릭 **서버 탐색기**합니다.
2. Hello 서버 탐색기 창에서 확장 **Azure** 확장 **Data Factory**합니다. 표시 되 면 **tooVisual Studio에에서 로그인**, hello 입력 **계정** 연결 된 Azure 구독 및 클릭 **계속**합니다. **암호**를 입력하고 **로그인**을 클릭합니다. Visual Studio에는 구독에서 모든 Azure 데이터 팩토리에 대 한 정보 tooget 하려고 시도합니다. Hello에이 작업의 hello 상태를 확인할 **데이터 팩터리에 작업 목록** 창.

    ![서버 탐색기](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a>기존 데이터 팩터리에 대한 Visual Studio 프로젝트 만들기

- 서버 탐색기에서 데이터 팩터리를 마우스 오른쪽 단추로 클릭 하 고 선택 **데이터 팩터리의 내보내기 tooNew 프로젝트** toocreate 기존 데이터 팩토리를 기반으로 한 Visual Studio 프로젝트입니다.

    ![데이터 팩터리 tooa VS 프로젝트 내보내기](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a>Visual Studio용 데이터 팩터리 도구 업데이트
Visual Studio 용 Azure Data Factory 도구 tooupdate 단계 hello지 않습니다.

1. 클릭 **도구** hello 메뉴를 선택 **확장명 및 업데이트**합니다. 
2. 선택 **업데이트** 에 왼쪽된 창의 hello 선택한 후 **Visual Studio 갤러리**합니다.
3. **Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다. 이 항목을 표시 되지 않으면 최신 버전의 hello 도구 hello이 이미 있습니다. 

## <a name="use-configuration-files"></a>구성 파일 사용
연결 된 서비스/테이블/파이프라인 각 환경에 대해 다른 방식에 대 한 Visual Studio tooconfigure 속성에서 구성 파일을 사용할 수 있습니다.

다음은 Azure 저장소 연결 서비스에 대 한 JSON 정의 hello를 것이 좋습니다. toospecify **connectionString** accountname 및 accountkey hello (프로덕션/개발/테스트) 환경 toowhich 기준에 대 한 값이 서로 다른 배포 하는 데이터 팩터리 엔터티. 각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a>구성 파일 추가
Hello 다음 단계를 수행 하 여 각 환경에 대 한 구성 파일을 추가 합니다.   

1. Visual Studio 솔루션의 hello Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.
2. 선택 **Config** hello hello 왼쪽에 설치 된 템플릿 목록에서 선택 **구성 파일**를 입력 한 **이름** hello 구성에 대 한 파일을 찾아 클릭 **추가**합니다.

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. 형식에 따라 hello에 구성 매개 변수 및 해당 값을 추가 합니다.

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다. Hello 구문 이름을 지정 하는 [JsonPath](http://goessner.net/articles/JsonPath/)합니다.   

    JSON에 hello 코드 다음에 나와 있는 값의 배열을 포함 하는 속성:  

    ```json
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
    ```

    다음 구성 파일 (사용 하 여 인덱스가 0부터 시작) hello에 표시 된 대로 속성을 구성 합니다.

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a>공백이 포함된 속성 이름
속성 이름에 공백이 있으면, 다음 예제 (데이터베이스 서버 이름) hello와 같이 대괄호를 사용 합니다.

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a>구성을 사용하여 솔루션 배포
Azure Data Factory 엔터티에 VS에서 게시 하는 hello 원하는 구성으로 toouse 해당 게시 작업에 대해 지정할 수 있습니다.

구성 파일을 사용 하 여 Azure Data Factory 프로젝트에서 toopublish 엔터티:   

1. 데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시** toosee hello **게시 항목** 대화 상자.
2. 기존 데이터 팩토리를 선택 하거나 hello에 데이터 팩터리 만들기에 대 한 값을 지정할 **구성 데이터 팩터리의** 페이지를 클릭 하 여 **다음**합니다.   
3. Hello에 **게시 항목** 페이지: hello에 대 한 사용 가능한 구성으로 드롭 다운 목록을 보려면 **배포 구성 선택** 필드입니다.

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. 선택 hello **구성 파일** 있는지 toouse 선택한 클릭 **다음**합니다.
5. Hello에 대 한 JSON 파일의 hello 이름 표시 되는지 확인 **요약** 페이지 클릭 하 여 **다음**합니다.
6. 클릭 **마침** hello 배포 작업이 완료 된 후입니다.

를 배포할 때 hello 구성 파일에서 hello 값은 hello 엔터티는 배포 된 tooAzure 데이터 팩터리 서비스 전에 hello JSON 파일의 속성에 대 한 tooset 사용 되는 값입니다.   

## <a name="use-azure-key-vault"></a>Azure Key Vault 사용
권장 및 종종 연결 문자열 toohello 코드 저장소와 같은 보안 정책 toocommit 중요 한 데이터에 대 한 아닙니다. 참조 [ADF 게시 Secure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure 키 자격 증명 모음에 중요 한 정보를 저장 하 고 사용 하 여 데이터 팩터리 엔터티를 게시 하는 동안에 대 한 GitHub toolearn 샘플. Visual Studio 용 확장명 게시 Secure hello hello 비밀 toobe 주요 자격 증명 모음에 저장 된 있으며 참조 toothem만 연결 된 서비스에 지정 된 / 배포 구성. Data Factory 엔터티에 tooAzure를 게시 하는 경우 이러한 참조는 확인 됩니다. 이러한 파일 비밀이 노출 하지 않고 커밋된 toosource 리포지토리 수 있습니다.


## <a name="next-steps"></a>다음 단계
이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다. hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.
