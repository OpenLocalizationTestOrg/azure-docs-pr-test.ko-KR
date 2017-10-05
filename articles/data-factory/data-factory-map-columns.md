---
title: "Azure Data Factory에서 데이터 집합 열 매핑 | Microsoft Docs"
description: "원본 열을 대상 열에 매핑하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="20113-103">원본 데이터 집합 열을 대상 데이터 집합 열에 매핑</span><span class="sxs-lookup"><span data-stu-id="20113-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="20113-104">열 매핑은 원본 테이블 맵의 “structure”에서 지정한 열을 싱크 테이블의 “structure”에서 지정한 열과 매핑하는 방법을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20113-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="20113-105">**columnMapping** 속성은 Copy 작업의 **typeProperties** 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20113-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="20113-106">열 매핑에서는 다음과 같은 시나리오가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="20113-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="20113-107">원본 데이터 집합 구조에 있는 모든 열이 싱크 데이터 집합 구조의 모든 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="20113-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="20113-108">원본 데이터 집합 구조에 있는 열의 하위 집합이 싱크 데이터 집합 구조의 모든 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="20113-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="20113-109">다음은 예외가 발생하는 오류 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="20113-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="20113-110">더 적은 열 또는 더 많은 열 "의 구조에서" 싱크 테이블 보다 매핑에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20113-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="20113-111">중복 매핑</span><span class="sxs-lookup"><span data-stu-id="20113-111">Duplicate mapping.</span></span>
* <span data-ttu-id="20113-112">SQL 쿼리 결과에는 매개 변수 매핑에서 지정한 열 이름이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="20113-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="20113-113">다음 샘플은 Azure SQL 및 Azure Blob에 대한 것이지만, 직사각 데이터 집합을 지원하는 모든 데이터 저장소에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20113-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="20113-114">예에서 관련 데이터 원본의 데이터를 가리키도록 데이터 집합과 연결 서비스를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="20113-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="20113-115">예제 1 – Azure SQL에서 Azure Blob으로의 열 매핑</span><span class="sxs-lookup"><span data-stu-id="20113-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="20113-116">이 예제에서 입력 테이블에는 구조가 있고 그 구조가 Azure SQL 데이터베이스에 있는 SQL 테이블을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="20113-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="20113-117">이 예제에서 출력 테이블에는 구조가 있으며 그 구조가 Azure Blob 저장소에 있는 Blob을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="20113-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="20113-118">다음 JSON은 파이프라인으로 복사 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="20113-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="20113-119">원본의 열과 싱크(**columnMappings**)의 열 간 매핑은 **Translator** 속성을 사용하여 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="20113-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="20113-120">**열 매핑 흐름:**</span><span class="sxs-lookup"><span data-stu-id="20113-120">**Column mapping flow:**</span></span>

![열 매핑 흐름 ](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="20113-122">예제 2 – SQL 쿼리를 사용하여 Azure SQL에서 Azure Blob로 열 매핑</span><span class="sxs-lookup"><span data-stu-id="20113-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="20113-123">이 예제에서는 단순히 “structure” 섹션에서 테이블 이름과 열 이름을 지정하는 대신 SQL 쿼리를 사용하여 Azure SQL의 데이터를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="20113-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="20113-124">이 경우 쿼리 결과가 먼저 원본의 "structure"에서 지정된 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="20113-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="20113-125">다음으로, 원본 "structure"의 열이 columnMappings에서 지정된 규칙을 통해 싱크 "structure"의 열에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="20113-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="20113-126">쿼리가 5개 열, 원본의 "structure"에 지정된 열보다 두 개 더 많은 열을 차례로 반환한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="20113-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="20113-127">**열 매핑 흐름**</span><span class="sxs-lookup"><span data-stu-id="20113-127">**Column mapping flow**</span></span>

![열 매핑 흐름 - 2 ](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="20113-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="20113-129">Next steps</span></span>
<span data-ttu-id="20113-130">복사 작업 사용에 대한 자습서 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="20113-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="20113-131">Blob Storage에서 SQL Database로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="20113-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
