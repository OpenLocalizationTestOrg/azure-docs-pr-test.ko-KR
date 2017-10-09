---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Azure 데이터 팩터리를 사용 하 여 aaaLoad 데이터 | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 tooload 데이터에 알아봅니다"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a>Azure Data Factory를 사용하여 데이터 로드
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [데이터 팩터리](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

이 자습서에서는 Azure 저장소 Blob tooAzure SQL 데이터 웨어하우스에서에서 toomove 데이터를 Azure 데이터 팩터리 파이프라인 toocreate 합니다. 단계를 수행 하는 hello로 다음을 수행 합니다.

* Azure Storage Blob에서 샘플 데이터를 설정합니다.
* 리소스 tooAzure Data Factory를 연결 합니다.
* 데이터 웨어하우스 저장소 Blob tooSQL에서 파이프라인 toomove 데이터를 만듭니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>시작하기 전에
toofamiliarize Azure 데이터 팩터리와 직접 참조 [소개 tooAzure Data Factory][Introduction tooAzure Data Factory]합니다.

### <a name="create-or-identify-resources"></a>리소스 만들기 또는 식별
이 자습서를 시작 하기 전에 다음 리소스 toohave hello가 필요 합니다.

* **Azure 저장소 Blob**: toohave 하나의 사용 가능한 toostore hello 샘플 데이터가 필요 하므로 및이 자습서에서는 hello Azure 데이터 팩터리 파이프라인에 대 한 Azure 저장소 Blob hello 데이터 원본으로 사용 합니다. 없는 경우 하나 이미, 너무 방법을 알아보려면[저장소 계정을 만드는][Create a storage account]합니다.
* **SQL 데이터 웨어하우스**: Azure 저장소 Blob에서이 자습서 이동 hello 데이터 너무 SQL 데이터 웨어하우스 등 필요한 toohave AdventureWorksDW 예제 데이터 hello로 로드 되는 데이터 웨어하우스의 온라인입니다. 데이터 웨어하우스 아직 없는 경우 너무 방법을 알아볼[하나를 프로 비전][Create a SQL Data Warehouse]합니다. 데이터 웨어하우스를 갖지만 hello 예제 데이터와 함께 프로 비전 하지 않은 경우 다음을 할 수 있습니다 [수동으로 로드][Load sample data into SQL Data Warehouse]합니다.
* **Azure Data Factory**: Azure Data Factory hello 실제 부하를 완료 하 고 따라서 toobuild hello 데이터 이동을 파이프라인을 사용할 수 있는 하나 toohave 해야 합니다. 없는 이미, 경우에 대해 배울 방법 toocreate 하나 1 단계에서에서의 [(데이터 팩터리 편집기) Azure 데이터 팩터리 시작][Get started with Azure Data Factory (Data Factory Editor)]합니다.
* **AZCopy**: 사용자 로컬 클라이언트 tooyour Azure 저장소 Blob에서에서 AZCopy toocopy hello 샘플 데이터가 필요 합니다. 설치 지침은 hello [AZCopy 설명서][AZCopy documentation]합니다.

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a>1 단계: 샘플 데이터 tooAzure 저장소 Blob 복사
모든 hello 조각을 준비 했으면 준비 toocopy 샘플 데이터 tooyour Azure 저장소 Blob 됩니다.

1. [샘플 데이터를 다운로드][Download sample data]합니다. 이 데이터는 다른 3 년의 판매 데이터 tooyour AdventureWorksDW 예제 데이터를 추가합니다.
2. 데이터 tooyour Azure 저장소 Blob의 3 년이 AZCopy 명령 toocopy hello를 사용 합니다.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a>2 단계: 리소스 tooAzure Data Factory에 연결
Hello 데이터 준비에서는에서는 만들 수 hello Azure 데이터 팩터리 파이프라인 toomove hello 데이터 Azure blob 저장소의 SQL 데이터 웨어하우스로 합니다.

tooget 시작 열기 hello [Azure 포털] [ Azure portal] hello 왼쪽 메뉴에서 데이터 팩터리를 선택 합니다.

### <a name="step-21-create-linked-service"></a>2.1단계: 연결된 서비스 만들기
Azure 저장소 계정 및 SQL 데이터 웨어하우스 tooyour 데이터 팩터리에 연결 합니다.  

1. 먼저, 데이터 팩터리의 hello ' 연결 된 서비스 ' 섹션을 클릭 하 여 hello 등록 프로세스를 시작 하 고 '새 데이터 저장소'를 클릭 한 다음 이름 tooregister 사용자 형식으로 선택 Azure 저장소에서 azure 저장소를 선택 하 고 계정 이름과 계정 키를 입력 합니다.
2. SQL 데이터 웨어하우스 tooregister toohello '작성자 및 배포' 섹션 이동 ' 새 데이터 저장소 ' 및 ' Azure SQL 데이터 웨어하우스 '를 선택 합니다. 이 템플릿에 붙여 넣은 다음 특정 정보를 입력합니다.
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a>2.2 단계: hello 데이터 집합 정의
연결 된 서비스를 만드는 hello, म toodefine hello 데이터 집합을 갖게 됩니다.  이 의미 여기 저장소 tooyour 데이터 웨어하우스에서 이동 하는 hello 데이터의 hello 구조를 정의 합니다.  만들기에 대해 자세히 알아볼 수 있습니다.

1. 데이터 팩터리의 toohello '작성자 및 배포' 섹션을 탐색 하 여이 프로세스를 시작 합니다.
2. '새 데이터 집합' 및 'Azure Blob 저장소' toolink 저장소 tooyour 데이터 팩터리를 클릭 합니다.  Azure Blob 저장소에 스크립트 toodefine 아래 hello 데이터를 사용할 수 있습니다.
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
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
3. 이제 SQL Data Warehouse의 데이터 집합을 정의합니다. Hello에서 시작 '새 데이터 집합' 및 ' Azure SQL 데이터 웨어하우스 '를 클릭 하 여 동일한 방식으로 합니다.
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a>3단계: 파이프라인 만들기 및 실행
마지막으로 설정 하 고 Azure Data Factory에서 hello 파이프라인을 실행 합니다.  이 hello 작업 완료 hello 실제 데이터 이동입니다.  SQL 데이터 웨어하우스 및 Azure Data Factory를 완료할 수 있는 hello 작업의 전체 뷰를 찾을 수 [여기][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]합니다.

Hello' 작성자 및 배포 ', ' 기타 명령을 ' 및 ' 새 파이프라인 '를 클릭 합니다.  Hello 파이프라인을 만든 후에 아래 코드 tootransfer hello 데이터 tooyour 데이터 웨어하우스 hello를 사용할 수 있습니다.

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
              }
            ],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a>다음 단계
toolearn을 확인 하 여 시작 합니다.

* [Azure Data Factory 학습 경로][Azure Data Factory learning path]
* [Azure SQL Data Warehouse 커넥터][Azure SQL Data Warehouse Connector] Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스에 대 한 hello 코어 참조 항목입니다.

이러한 항목은 Azure Data Factory에 대한 자세한 정보를 제공합니다. Azure SQL 데이터베이스 또는 HDInsight에 이야기 있지만 tooAzure SQL 데이터 웨어하우스 hello 정보에도 적용 됩니다.

* [자습서: Azure 데이터 팩터리 시작] [ Tutorial: Get started with Azure Data Factory] Azure 데이터 팩터리를 사용 하 여 데이터를 처리 하기 위한 hello 코어 자습서입니다. 이 자습서에서는 HDInsight tootransform를 사용 하 여 첫 번째 파이프라인 빌드하고 월별로 웹 로그 분석 합니다. 이 자습서에는 복사 작업이 없습니다.
* [자습서: Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]합니다. 이 자습서에서는 Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 Azure Data Factory toocopy 데이터에서 파이프라인을 만듭니다.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
