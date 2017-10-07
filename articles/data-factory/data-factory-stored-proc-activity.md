---
title: "aaaSQL 서버 저장 프로시저 작업"
description: "SQL Server 저장 프로시저 작업 tooinvoke hello 데이터 팩토리 파이프라인에서 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 저장된 프로시저를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a>SQL Server 저장 프로시저 작업
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 작업](data-factory-hive-activity.md) 
> * [Pig 작업](data-factory-pig-activity.md)
> * [MapReduce 작업](data-factory-map-reduce.md)
> * [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
> * [Spark 작업](data-factory-spark.md)
> * [Machine Learning Batch 실행 작업](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 업데이트 리소스 작업](data-factory-azure-ml-update-resource-activity.md)
> * [저장 프로시저 작업](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 작업](data-factory-usql-activity.md)
> * [.NET 사용자 지정 작업](data-factory-use-custom-activities.md)

## <a name="overview"></a>개요
데이터 변환 작업을 사용 하 여 데이터 팩터리에서 [파이프라인](data-factory-create-pipelines.md) 예측 및 통찰력으로 원시 데이터 tootransform 및 프로세스입니다. hello 저장 프로시저 작업은 데이터 팩터리의 지원 hello 변환 활동 중 하나입니다. Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 문서 데이터 변환 및 데이터 팩터리의 지원 hello 변환 작업에 대 한 일반적인 개요를 사용 합니다.

기업에서 또는 Azure 가상 컴퓨터 (VM)에 같은 데이터가 hello 중 하나에 있는 저장된 프로시저를 저장 하는 hello 저장 프로시저 작업 tooinvoke를 사용할 수 있습니다. 

- Azure SQL Database
- Azure SQL 데이터 웨어하우스
- SQL Server 데이터베이스.  SQL Server를 사용 하는 경우 hello 호스트 데이터베이스 hello 또는 access toohello 데이터베이스 있는 별도 컴퓨터에서 동일한 컴퓨터에 데이터 관리 게이트웨이 설치 합니다. 데이터 관리 게이트웨이는 온-프레미스/Azure VM에서 데이터 원본을 Cloud Services에 안전하고 관리되는 방식으로 연결하는 구성 요소입니다. 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요.

> [!IMPORTANT]
> Azure SQL 데이터베이스 또는 SQL Server에 데이터를 복사할 때 hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke hello를 사용 하 여 저장된 프로시저에서에서 **sqlWriterStoredProcedureName** 속성입니다. 자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요. Hello 속성에 대 한 자세한 커넥터 문서를 다음을 참조: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)합니다. 복사 작업을 사용하여 Azure SQL Data Warehouse로 데이터를 복사하는 동안 저장 프로시저를 호출하는 것은 지원되지 않습니다. 그러나 SQL 데이터 웨어하우스에 hello 저장 프로시저 활동 tooinvoke 저장된 프로시저를 사용할 수 있습니다. 
>  
> Azure SQL 데이터 웨어하우스 또는 SQL Server 나 Azure SQL 데이터베이스에서 데이터를 복사할 때 구성할 수 있습니다 **SqlSource** 복사 활동 tooinvoke hello를 사용 하 여 hello 원본 데이터베이스에서 저장된 프로시저 tooread 데이터에서에서  **sqlReaderStoredProcedureName** 속성입니다. 자세한 내용은 hello 다음 커넥터 문서를 참조 하세요.: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


연습에서는 다음 hello 파이프라인 tooinvoke Azure SQL 데이터베이스의 저장된 프로시저에서에서 저장 프로시저 작업 hello 합니다. 

## <a name="walkthrough"></a>연습
### <a name="sample-table-and-stored-procedure"></a>샘플 테이블 및 저장 프로시저
1. Hello 다음 만들기 **테이블** SQL Server Management Studio 또는 다른 익숙한 도구를 사용 하 여 Azure SQL 데이터베이스에 있습니다. hello datetimestamp 열은 hello 날짜 및 시간을 해당 하는 hello ID 생성 되는 경우.

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    Id는 hello 고유한 식별 하 고 hello datetimestamp 열은 hello 날짜 및 시간 hello 해당 ID가 생성 되는 경우 키를 누릅니다.
    
    ![샘플 데이터](./media/data-factory-stored-proc-activity/sample-data.png)

    이 샘플에서는 Azure SQL 데이터베이스에서 hello 저장 프로시저는입니다. Hello 저장된 프로시저에 있으면 Azure SQL 데이터 웨어하우스 및 SQL Server 데이터베이스, hello 방법은 비슷합니다. SQL Server Database의 경우 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 설치해야 합니다.
2. Hello 다음 만들기 **저장 프로시저** toohello에 데이터를 삽입 하는 **하세요**합니다.

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **이름** 및 **대/소문자** hello의 매개 변수 (이 예제의 DateTime)와 일치 해야 hello 파이프라인/활동 JSON에에서 지정 된 매개 변수입니다. 저장된 프로시저 정의 hello 하 되도록  **@**  hello 매개 변수에 대 한 접두사로 사용 됩니다.

### <a name="create-a-data-factory"></a>데이터 팩터리를 만듭니다.
1. 로그 너무[Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **새로** hello 왼쪽된 메뉴를 클릭 **인텔리전스 + 분석**를 클릭 하 고 **Data Factory**합니다.

    ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. Hello에 **새 데이터 팩터리** 블레이드에서 입력 **SProcDF** hello 이름에 대 한 합니다. Azure Data Factory 이름은 **전역적으로 고유**합니다. 해당 이름의 hello 팩터리의 tooenable hello 성공적으로 만드는 hello 데이터 팩터리의 tooprefix hello 이름이 필요 합니다.

   ![새 data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Azure **구독**을 선택합니다.
5. 에 대 한 **리소스 그룹**, hello 다음 단계 중 하나를 수행 합니다.
   1. 클릭 **새로 만들기** hello 리소스 그룹에 대 한 이름을 입력 합니다.
   2. **기존 항목 사용**을 클릭하고 기존 리소스 그룹을 선택합니다.  
6. 선택 hello **위치** hello 데이터 팩토리에 대 한 합니다.
7. 선택 **Pin toodashboard** 다음에 로그인 할 때 hello 대시보드에서 hello 데이터 팩터리를 볼 수 있습니다.
8. 클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.
9. Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello Azure 포털의. 보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.

   ![Data Factory 홈페이지](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Azure SQL 연결된 서비스 만들기
Hello 데이터 팩터리를 만든 후 hello 하세요 테이블 및 sp_sample 저장 프로시저, tooyour 데이터 팩터리를 포함 하 여 Azure SQL 데이터베이스를 연결 하는 Azure SQL 연결 서비스를 만듭니다.

1. 클릭 **작성자 및 배포** hello에 **Data Factory** 블레이드 **SProcDF** toolaunch hello 데이터 팩터리 편집기입니다.
2. 클릭 **새 데이터 저장소** 명령 모음 hello 되 고 선택 **Azure SQL 데이터베이스**합니다. Hello Azure SQL을 만들기 위한 JSON 스크립트는 연결 된 서비스 hello 편집기에 표시 됩니다.

   ![새 데이터 저장소](media/data-factory-stored-proc-activity/new-data-store.png)
3. Hello JSON 스크립트에서에서 변경 내용을 따라 hello를 확인 합니다.

   1. 대체 `<servername>` hello Azure SQL 데이터베이스 서버 이름을 사용 합니다.
   2. 대체 `<databasename>` hello 데이터베이스를 만든 hello 테이블과 hello와 저장 프로시저입니다.
   3. 대체 `<username@servername>` toohello 데이터베이스 액세스를 가진 hello 사용자 계정을 사용 합니다.
   4. 대체 `<password>` hello hello 사용자 계정의 암호를 사용 합니다.

      ![새 데이터 저장소](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다. Hello 왼쪽에서 볼 hello 트리에서 hello AzureSqlLinkedService 표시 되는지 확인 합니다.

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>출력 데이터 집합 만들기
저장된 프로시저 활동에 대 한 출력 데이터 집합 저장 프로시저를 hello 하는 경우에 생성 하지 않으므로 모든 데이터를 지정 해야 합니다. hello 출력 hello 활동 (얼마나 자주 hello 활동 실행-매시간, 매일, 등)의 일정을 hello를 구동 하는 데이터 집합 때문입니다. hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다. hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello 파이프라인에서. 그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다. Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며 경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합** (hello의 출력을 실제로 포함 되지 않는 tooa 테이블을 가리키는 데이터 집합 저장 프로시저). 이 더미 데이터 집합 저장 프로시저 작업 hello를 실행 하기 위한 toospecify hello 일정만 사용 됩니다. 

1. 도구 모음에서 **... 더 많은** hello 도구 모음에서 **새 데이터 집합**를 클릭 하 고 **Azure SQL**합니다. **새 데이터 집합** hello 명령 모음 및 선택에 **Azure SQL**합니다.

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/new-dataset.png)
2. 복사/붙여넣기 hello toohello JSON 편집기에서 JSON 스크립트를 수행 합니다.

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. toodeploy hello 데이터 집합, 클릭 **배포** hello 명령 모음에서 합니다. Hello 트리 뷰에서 hello 데이터 집합에 표시 되는지 확인 합니다.

    ![연결된 서비스와 트리 뷰](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>SqlServerStoredProcedure 작업을 사용하여 파이프라인 만들기
이제 저장 프로시저 작업을 사용하여 파이프라인 만들겠습니다. 

Hello 다음과 같은 속성을 확인 합니다. 

- hello **형식** 너무 속성이**SqlServerStoredProcedure**합니다. 
- hello **storedProcedureName** 속성이 너무 설정 글꼴로**sp_sample** (저장 프로시저 hello의 이름).
- hello **storedProcedureParameters** 라는 하나의 매개 변수를 포함 하는 섹션 **DataTime**합니다. Hello 이름과 대/소문자 hello 저장 프로시저 정의에 hello 매개 변수의 이름 및 JSON의 hello 매개 변수는 대/소문자 구분 일치 해야 합니다. 매개 변수에 대해 null을 전달 해야 hello 구문을 사용 하 여: `"param1": null` (모두 소문자).
 
1. 도구 모음에서 **... 더 많은** 명령 모음 hello 되 고 클릭 **새 파이프라인**합니다.
2. 다음 JSON 코드 조각은 복사/붙여넣기 hello:   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. toodeploy hello 파이프라인 클릭 **배포** hello 도구 모음입니다.  

### <a name="monitor-hello-pipeline"></a>모니터 hello 파이프라인
1. 클릭 **X** tooclose 데이터 팩터리 편집기 블레이드를 toonavigate toohello Data Factory 블레이드를 다시 마우스 클릭 **다이어그램**합니다.

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. Hello에 **다이어그램 보기**를 hello 파이프라인에 대 한 개요를 확인 하 고 데이터 집합에 사용 되는이 자습서입니다.

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. 다이어그램 보기 hello에서 hello 데이터 집합을 두 번 클릭 `sprocsampleout`합니다. 준비 상태에서 hello 조각이 표시 됩니다. 조각이 hello 시작 시간과 종료 시간 hello JSON에서에서 사이의 각 시간에 대해 생성 되 있으므로 5 개의 분할 영역 이어야 합니다.

    ![다이어그램 타일](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. 이 분할 영역에 있을 때 **준비** 실행 상태는 `select * from sampletable` 데이터 hello hello Azure SQL 데이터베이스 tooverify에 대 한 쿼리를 hello 저장 프로시저를 통해 toohello 테이블에 삽입 합니다.

   ![출력 데이터](./media/data-factory-stored-proc-activity/output.png)

   참조 [모니터 hello 파이프라인](data-factory-monitor-manage-pipelines.md) Azure 데이터 팩터리 파이프라인을 모니터링 하는 방법에 대 한 자세한 정보에 대 한 합니다.  


## <a name="specify-an-input-dataset"></a>입력 데이터 집합 지정
Hello 연습에서는 저장된 프로시저 작업 모든 입력된 데이터 집합이 필요 하지 않습니다. 입력된 데이터 집합을 지정 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 (준비 상태)에서 입력된 데이터 집합의 조각을 hello를 사용할 수 있습니다. hello 데이터 집합에는 외부 데이터 집합 수 (hello에 다른 활동에 의해 생성 되지 않습니다 동일한 파이프라인) 또는 업스트림 활동 (이 작업 이전에 실행 되 hello 활동)에서 생성 하는 내부 데이터 집합입니다. Hello 저장 프로시저 작업에 대 한 여러 입력된 데이터 집합을 지정할 수 있습니다. 이렇게 하면 hello 저장된 프로시저 작업 실행 모든 hello에 대 한 입력된 데이터 집합 분할 영역을 사용할 수 (준비 상태) 경우에 합니다. hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다. 시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다.

## <a name="chaining-with-other-activities"></a>다른 작업과 연결
Toochain는 업스트림 활동과이 활동을 사용 하도록 하려는 경우이 활동의 입력으로 hello 업스트림 활동의 hello 출력을 지정 합니다. 이렇게 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 hello 업스트림 활동이 완료 되 고 hello 업스트림 활동의 hello 출력 데이터 집합 (준비 됨 상태)에 사용할 수 있습니다. Hello 저장 프로시저 작업의 입력된 데이터 집합으로 업스트림 여러 활동의 출력 데이터 집합을 지정할 수 있습니다. 작업을 수행 하면 hello 저장 프로시저 작업 하므로 모든 hello에 대 한 입력된 데이터 집합 분할 영역을 사용할 수 있는 경우에 실행 됩니다.  

다음 예제는 hello, hello 복사 작업의 hello 출력은: OutputDataset hello의 입력이 있는 저장 프로시저 작업 합니다. 따라서 hello 저장된 프로시저 작업까지 실행 되지 않습니다 hello 복사 작업을 완료 되며 hello OutputDataset 분할 영역에서에서 사용할 수 (준비 상태). 여러 입력된 데이터 집합을 지정 하면 hello 저장된 프로시저 작업까지 실행 되지 않습니다 (준비 상태)에 사용할 수 있는 모든 hello 입력된 데이터 집합 슬라이스입니다. hello 입력된 데이터 집합 매개 변수 toohello 저장 프로시저 작업으로 직접 사용할 수 없습니다. 

연결 작업에 대한 자세한 내용은 [파이프라인의 여러 작업](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)을 참조하세요.

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

마찬가지로, toolink hello 저장 프로시저와 관련 된 활동 **다운스트림 작업** 으로 hello 저장 프로시저 작업의 hello 출력 데이터 집합을 지정 하는 (hello 활동 hello 저장된 프로시저 활동이 완료 된 후 실행 하는), 프로그램 hello 파이프라인의 hello 다운스트림 활동의 입력입니다.

> [!IMPORTANT]
> Azure SQL 데이터베이스 또는 SQL Server에 데이터를 복사할 때 hello를 구성할 수 있습니다 **SqlSink** 복사 활동 tooinvoke hello를 사용 하 여 저장된 프로시저에서에서 **sqlWriterStoredProcedureName** 속성입니다. 자세한 내용은 [복사 작업에서 저장 프로시저 호출](data-factory-invoke-stored-procedure-from-copy-activity.md)을 참조하세요. Hello 속성에 대 한 자세한 참조 커넥터 문서를 수행 하는 hello: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties)합니다.
>  
> Azure SQL 데이터 웨어하우스 또는 SQL Server 나 Azure SQL 데이터베이스에서 데이터를 복사할 때 구성할 수 있습니다 **SqlSource** 복사 활동 tooinvoke hello를 사용 하 여 hello 원본 데이터베이스에서 저장된 프로시저 tooread 데이터에서에서  **sqlReaderStoredProcedureName** 속성입니다. 자세한 내용은 hello 다음 커넥터 문서를 참조 하세요.: [Azure SQL 데이터베이스](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL 데이터 웨어하우스](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a>JSON 형식
저장 프로시저 작업을 정의 하기 위한 hello JSON 형식은 다음과 같습니다.

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

다음 표에서 hello 이러한 JSON 속성을 설명 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| name | Hello 활동의 이름 |예 |
| 설명 |어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다. |아니요 |
| type | **SqlServerStoredProcedure**로 설정되어야 합니다. | 예 |
| inputs | 선택 사항입니다. 입력된 데이터 집합을 지정 않습니다 ('준비' 상태)에서 사용할 수 있어야 hello에 대 한 저장 프로시저 활동 toorun 합니다. hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다. 시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다. |아니요 |
| outputs | 저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다. 출력 데이터 집합 지정 hello **일정** hello에 대 한 저장 프로시저 작업 (시간별, 매주, 매월, 등). <br/><br/>hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다. <br/><br/>hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) hello 파이프라인에서. 그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다. Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며 <br/><br/>경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합**, hello를 실행 하기 위한 toospecify hello 일정 저장 프로시저 작업에만 사용 되는 합니다. |예 |
| storedProcedureName |Hello Azure SQL 데이터베이스 또는 출력 테이블 사용 hello hello 연결 된 서비스에 의해 표시 되는 Azure SQL 데이터 웨어하우스 또는 SQL Server 데이터베이스의 hello 저장 프로시저의 hello 이름을 지정 합니다. |예 |
| storedProcedureParameters |저장 프로시저 매개 변수의 값을 지정합니다. 매개 변수에 대해 toopass을 null 필요 hello 구문 사용: "param1": null (모든 소문자). 이 속성을 사용 하는 방법에 대 한 샘플 toolearn 다음 hello를 참조 하십시오. |아니요 |

## <a name="passing-a-static-value"></a>정적 값 전달
이제 '샘플 문서' 라는 정적 값을 포함 하는 hello 테이블의 '시나리오' 라는 다른 열 추가 생각해 봅시다.

![샘플 데이터 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

**테이블:**

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

**저장 프로시저:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

이제, hello 통과 **시나리오** hello에서 매개 변수 및 hello 값 저장 프로시저 작업 합니다. hello **typeProperties** hello 샘플 같습니다 hello 다음 코드 조각 앞의 섹션:

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

**Data Factory 데이터 집합:**

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Data Factory 파이프라인**

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```