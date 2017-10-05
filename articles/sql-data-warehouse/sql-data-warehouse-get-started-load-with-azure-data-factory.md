---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Azure Data Factory를 사용하여 데이터 로드 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 데이터를 로드하는 방법을 알아보세요."
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
ms.openlocfilehash: 0b01c77c916b616974545fc3da442e72e5336399
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-azure-data-factory"></a>Azure Data Factory를 사용하여 데이터 로드
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [데이터 팩터리](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)  
> 
> 

이 자습서는 Azure Data Factory에서 파이프라인을 만들어 Azure Storage Blob에서 Azure SQL Data Warehouse로 데이터를 이동하는 방법을 보여 줍니다. 다음 단계에서 수행할 작업은 다음과 같습니다.

* Azure Storage Blob에서 샘플 데이터를 설정합니다.
* Azure Data Factory로 리소스를 연결합니다.
* 저장소 BLOB에서 SQL 데이터 웨어하우스로 데이터를 이동하는 파이프라인을 만듭니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a>시작하기 전에
Azure Data Factory를 익히려면 [Azure Data Factory 소개][Introduction to Azure Data Factory]를 참조하세요.

### <a name="create-or-identify-resources"></a>리소스 만들기 또는 식별
이 자습서를 시작하기 전에 다음 리소스가 있어야 합니다.

* **Azure 저장소 BLOB**: 이 자습서에서는 Azure Data Factory 파이프라인에 대한 데이터 원본으로 Azure BLOB 저장소를 사용하므로 샘플 데이터를 저장할 Azure BLOB 저장소가 필요합니다. 저장소 계정이 아직 없는 경우 [저장소 계정을 만드는 방법][Create a storage account]을 알아봅니다.
* **SQL Data Warehouse**: 이 자습서는 Azure Storage Blob에서 SQL Data Warehouse로 데이터를 이동하므로 AdventureWorksDW 샘플 데이터와 함께 로드되는 데이터 웨어하우스 온라인이 필요합니다. 데이터 웨어하우스가 아직 없는 경우 [프로비전하는 방법][Create a SQL Data Warehouse]을 알아봅니다. 데이터 웨어하우스가 있지만 샘플 데이터를 사용하여 프로비전하지 않은 경우 [수동으로 로드][Load sample data into SQL Data Warehouse]할 수 있습니다.
* **Azure Data Factory**: Azure Data Factory는 실제 부하를 완료하므로 보유하여 데이터 이동 파이프라인을 빌드하는 데 사용할 수 있어야 합니다. Azure Data Factory가 없는 경우 [Azure Data Factory 시작(데이터 팩터리 편집기)][Get started with Azure Data Factory (Data Factory Editor)]의 1단계에서 만드는 방법을 알아봅니다.
* **AZCopy**: 로컬 클라이언트에서 Azure 저장소 BLOB으로 샘플 데이터를 복사할 AZCopy가 필요합니다. 설치 지침은 [AZCopy 설명서][AZCopy documentation]를 참조하세요.

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a>1단계: 샘플 데이터를 Azure 저장소 Blob에 복사
모든 부분이 준비되면 샘플 데이터를 Azure Storage Blob에 복사할 준비가 됩니다.

1. [샘플 데이터를 다운로드][Download sample data]합니다. 이 데이터는 AdventureWorksDW 샘플 데이터에 3년의 판매 데이터를 추가합니다.
2. 이 AZCopy 명령을 사용하여 Azure 저장소 Blob에 3년 분량의 데이터를 복사합니다.
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-to-azure-data-factory"></a>2단계: Azure Data Factory로 리소스를 연결합니다.
이제 데이터가 생성되었으므로 Azure 데이터 팩터리 파이프라인을 만들어 Azure Blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 이동할 수 있습니다.

시작하려면 [Azure Portal][Azure portal]을 열고 왼쪽 메뉴에서 사용자의 데이터 팩터리를 선택합니다.

### <a name="step-21-create-linked-service"></a>2.1단계: 연결된 서비스 만들기
Azure 저장소 계정과 SQL 데이터 웨어하우스를 데이터 팩터리로 연결합니다.  

1. 우선 데이터 팩터리의 '연결된 서비스' 섹션을 클릭한 다음 '새 데이터 저장소'를 클릭하여 등록 프로세스를 시작합니다. Azure 저장소를 등록할 이름을 선택하고 유형으로 Azure 저장소를 선택한 다음 계정 이름과 계정 키를 입력합니다.
2. SQL 데이터 웨어하우스를 등록하려면 '작성 및 배포' 섹션을 탐색하고 '새 데이터 저장소'와 'Azure SQL 데이터 웨어하우스'를 차례로 선택합니다. 이 템플릿에 붙여 넣은 다음 특정 정보를 입력합니다.
   
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

### <a name="step-22-define-the-dataset"></a>2.2단계: 데이터 집합 정의
연결된 서비스를 만든 다음 데이터 집합을 정의해야 합니다.  여기서 저장소에서 데이터 웨어하우스로 이동하는 데이터의 구조를 정의하는 것을 의미합니다.  만들기에 대해 자세히 알아볼 수 있습니다.

1. 이 프로세스를 시작하려면 가장 먼저 사용자 데이터 팩터리의 '작성 및 배포' 섹션으로 이동합니다.
2. '새 데이터 집합'을 클릭한 다음 'Azure BLOB 저장소'를 클릭하여 저장소를 데이터 팩터리에 연결합니다.  아래 스크립트를 사용하여 Azure BLOB 저장소에서 데이터를 정의할 수 있습니다.
   
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
3. 이제 SQL Data Warehouse의 데이터 집합을 정의합니다. 마찬가지로 '새 데이터 집합'을 클릭한 다음 'Azure SQL 데이터 웨어하우스'를 클릭합니다.
   
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
마지막으로 Azure Data Factory에서 파이프라인을 설정 및 실행합니다.  이 작업을 수행하면 실제 데이터 이동이 완료됩니다.  [여기][Move data to and from Azure SQL Data Warehouse using Azure Data Factory]에서 SQL Data Warehouse와 Azure Data Factory를 사용하여 완료할 수 있는 전체 작업을 볼 수 있습니다.

'작성 및 배포' 섹션에서 '추가 명령'을 클릭한 다음 '새 파이프라인'을 클릭합니다.  파이프라인을 만든 다음 아래 코드를 사용하여 데이터를 데이터 웨어하우스로 전송할 수 있습니다.

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
자세한 내용은 다음을 확인하여 시작합니다.

* [Azure Data Factory 학습 경로][Azure Data Factory learning path]
* [Azure SQL Data Warehouse 커넥터][Azure SQL Data Warehouse Connector] Azure SQL 데이터 웨어하우스와 함께 Azure Data Factory를 사용하기 위한 핵심 참조 항목입니다.

이러한 항목은 Azure Data Factory에 대한 자세한 정보를 제공합니다. Azure SQL Database 또는 HDInsight를 설명하지만 해당 정보는 Azure SQL Data Warehouse에도 적용됩니다.

* [자습서: Azure Data Factory 시작][Tutorial: Get started with Azure Data Factory] Azure Data Factory를 사용하여 데이터를 처리하기 위한 핵심 자습서입니다. 이 자습서에서 HDInsight를 사용하여 매월 기준으로 웹 로그를 변환 및 분석하는 첫 번째 파이프라인을 빌드합니다. 이 자습서에는 복사 작업이 없습니다.
* [자습서: Azure Storage Blob에서 Azure SQL Database로 데이터 복사][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database] 이 자습서에서는 Azure Storage Blob에서 Azure SQL Database로 데이터를 복사하는 파이프라인을 Azure Data Factory에 만듭니다.

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
