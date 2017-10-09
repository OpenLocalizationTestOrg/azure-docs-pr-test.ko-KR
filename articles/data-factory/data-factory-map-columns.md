---
title: "Azure Data Factory에서 데이터 집합 열 aaaMapping | Microsoft Docs"
description: "어떻게 toomap 원본 열 toodestination 열에 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>원본 데이터 집합 열 toodestination 데이터 집합 열 매핑
열 매핑이 싱크 테이블의 hello "구조"에서 원본 테이블 맵 toocolumns의 "구조" hello에 지정 된 열을 지정 하는 방법을 사용 하는 toospecify 될 수 있습니다. hello **columnMapping** hello에서 사용할 수 있는 속성은 **typeProperties** hello 복사 작업의 섹션입니다.

열 매핑 hello 다음 시나리오를 지원 합니다.

* Hello 원본 데이터 집합 구조에서 모든 열은 매핑된 tooall hello 싱크 데이터 집합 구조 열입니다.
* Hello 원본 데이터 집합 구조에서 hello 열의 하위 집합에는 hello 싱크 데이터 집합 구조에서 매핑된 tooall 열입니다.

hello 다음 예외가 발생 하는 오류 조건이:

* 적은 개수의 열 또는 많은 열에 hello "" 테이블의 구조 싱크 보다 hello 매핑에서 지정 합니다.
* 중복 매핑
* SQL 쿼리 결과 hello 매핑에 지정 된 열 이름을 없습니다.

> [!NOTE]
> hello 다음 샘플은 SQL Azure 및 Azure Blob에 대 한 있지만 사각형 데이터 집합을 지 원하는 해당 tooany 데이터 저장소입니다. 데이터 집합 및 예제 toopoint toodata hello 관련 데이터 원본에서에 연결 된 서비스 정의 조정 합니다.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>예제 1-열 Azure SQL tooAzure blob에서 매핑
이 샘플에서는 hello 입력된 테이블의 구조는 및 Azure SQL 데이터베이스에서 tooa SQL 테이블을 가리키도록 합니다.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

이 샘플에서는 hello 출력 테이블의 구조는 및 Azure blob 저장소에 tooa blob를 가리키도록 합니다.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

다음 JSON hello 파이프라인에서 복사 작업을 정의 합니다. 원본의 hello 열 매핑된 싱크의 toocolumns (**columnMappings**) hello를 사용 하 여 **변환기** 속성입니다.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**열 매핑 흐름:**

![열 매핑 흐름 ](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>예제 2-Azure SQL tooAzure blob에서 SQL 쿼리로 매핑 열
이 샘플에서는 SQL 쿼리는 단순히 hello 테이블 이름과 열 이름은 hello "구조" 섹션에서 지정 하는 대신 Azure SQL 데이터로 사용 되는 tooextract 합니다. 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
이 경우 hello 쿼리 결과는 소스의 "구조"에 지정 된 첫 번째 매핑된 toocolumns 됩니다. 다음에 "structure" 원본의 hello 열은 싱크 "구조" columnMappings에 지정 된 규칙에 매핑된 toocolumns 됩니다.  가정 hello 쿼리는 열이 5, 보다 hello 소스의 "구조"에 지정 된 두 개 이상의 열을 반환 합니다.

**열 매핑 흐름**

![열 매핑 흐름 - 2 ](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>다음 단계
복사 활동 사용에 대 한 자습서에 대 한 hello 문서를 참조 합니다. 

- [Blob 저장소 tooSQL 데이터베이스에서에서 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
