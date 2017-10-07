---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "aaaLoad 데이터를 Azure blob 저장소에 Azure SQL 데이터 웨어하우스 (Azure 데이터 팩터리) | Microsoft Docs"
description: "Azure 데이터 팩터리를 사용 하 여 tooload 데이터에 알아봅니다"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="1db68-103">Azure Blob 저장소에서 Azure SQL 데이터 웨어하우스로 데이터 로드(Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="1db68-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1db68-104">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="1db68-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="1db68-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1db68-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="1db68-106">이 자습서에서는 Azure 저장소 Blob tooSQL 데이터 웨어하우스에서에서 toomove 데이터를 Azure 데이터 팩터리 파이프라인 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-106">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooSQL Data Warehouse.</span></span> <span data-ttu-id="1db68-107">단계를 수행 하는 hello로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-107">With hello following steps you will:</span></span>

* <span data-ttu-id="1db68-108">Azure 저장소 BLOB에서 샘플 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="1db68-109">리소스 tooAzure Data Factory를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-109">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="1db68-110">데이터 웨어하우스 저장소 Blob tooSQL에서 파이프라인 toomove 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-110">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="1db68-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="1db68-111">Before you begin</span></span>
<span data-ttu-id="1db68-112">toofamiliarize Azure 데이터 팩터리와 직접 참조 [소개 tooAzure Data Factory][Introduction tooAzure Data Factory]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-112">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="1db68-113">리소스 만들기 또는 식별</span><span class="sxs-lookup"><span data-stu-id="1db68-113">Create or identify resources</span></span>
<span data-ttu-id="1db68-114">이 자습서를 시작 하기 전에 다음 리소스 toohave hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-114">Before starting this tutorial, you need toohave hello following resources.</span></span>

* <span data-ttu-id="1db68-115">**Azure 저장소 Blob**: toohave 하나의 사용 가능한 toostore hello 샘플 데이터가 필요 하므로 및이 자습서에서는 hello Azure 데이터 팩터리 파이프라인에 대 한 Azure 저장소 Blob hello 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="1db68-116">없는 경우 하나 이미, 너무 방법을 알아보려면[저장소 계정을 만드는][Create a storage account]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-116">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="1db68-117">**SQL 데이터 웨어하우스**: Azure 저장소 Blob에서이 자습서 이동 hello 데이터 너무 SQL 데이터 웨어하우스 등 필요한 toohave AdventureWorksDW 예제 데이터 hello로 로드 되는 데이터 웨어하우스의 온라인입니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-117">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="1db68-118">데이터 웨어하우스 아직 없는 경우 너무 방법을 알아볼[하나를 프로 비전][Create a SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-118">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="1db68-119">데이터 웨어하우스를 갖지만 hello 예제 데이터와 함께 프로 비전 하지 않은 경우 다음을 할 수 있습니다 [수동으로 로드][Load sample data into SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-119">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="1db68-120">**Azure Data Factory**: Azure Data Factory hello 실제 부하가 완료 되 고 따라서 toobuild hello 데이터 이동을 파이프라인을 사용할 수 있는 하나 toohave 해야 합니다. 없는 이미, 경우에 대해 배울 방법 toocreate 하나 1 단계에서에서의 [(데이터 팩터리 편집기) Azure 데이터 팩터리 시작][Get started with Azure Data Factory (Data Factory Editor)]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-120">**Azure Data Factory**: Azure Data Factory will complete hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="1db68-121">**AZCopy**: 사용자 로컬 클라이언트 tooyour Azure 저장소 Blob에서에서 AZCopy toocopy hello 샘플 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-121">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="1db68-122">설치 지침은 hello [AZCopy 설명서][AZCopy documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-122">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="1db68-123">1 단계: 샘플 데이터 tooAzure 저장소 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="1db68-123">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="1db68-124">모든 hello 조각을 준비 했으면 준비 toocopy 샘플 데이터 tooyour Azure 저장소 Blob 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-124">Once you have all of hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="1db68-125">[샘플 데이터를 다운로드][Download sample data]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="1db68-126">이 데이터는 다른 3 년의 판매 데이터 tooyour AdventureWorksDW 예제 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-126">This data will add another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="1db68-127">데이터 tooyour Azure 저장소 Blob의 3 년이 AZCopy 명령 toocopy hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-127">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="1db68-128">2 단계: 리소스 tooAzure Data Factory에 연결</span><span class="sxs-lookup"><span data-stu-id="1db68-128">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="1db68-129">Hello 데이터 준비에서는에서는 만들 수 hello Azure 데이터 팩터리 파이프라인 toomove hello 데이터 Azure blob 저장소의 SQL 데이터 웨어하우스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-129">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="1db68-130">tooget 시작 열기 hello [Azure 포털] [ Azure portal] hello 왼쪽 메뉴에서 데이터 팩터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-130">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="1db68-131">2.1단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="1db68-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="1db68-132">Azure 저장소 계정 및 SQL 데이터 웨어하우스 tooyour 데이터 팩터리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-132">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="1db68-133">먼저, 데이터 팩터리의 hello ' 연결 된 서비스 ' 섹션을 클릭 하 여 hello 등록 프로세스를 시작 하 고 '새 데이터 저장소'를 클릭 한 다음</span><span class="sxs-lookup"><span data-stu-id="1db68-133">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="1db68-134">이름 tooregister 사용자 형식으로 선택 Azure 저장소에서 azure 저장소를 선택 하 고 계정 이름과 계정 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-134">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="1db68-135">SQL 데이터 웨어하우스 tooregister toohello '작성자 및 배포' 섹션 이동 ' 새 데이터 저장소 ' 및 ' Azure SQL 데이터 웨어하우스 '를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-135">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="1db68-136">이 템플릿에 붙여 넣은 다음 특정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-136">Copy and paste in this template, and then fill in your specific information.</span></span>

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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="1db68-137">2.2 단계: hello 데이터 집합 정의</span><span class="sxs-lookup"><span data-stu-id="1db68-137">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="1db68-138">연결 된 서비스를 만드는 hello, म toodefine hello 데이터 집합을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-138">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="1db68-139">이 의미 여기 저장소 tooyour 데이터 웨어하우스에서 이동 하는 hello 데이터의 hello 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-139">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="1db68-140">만들기에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-140">You can read more about creating</span></span>

1. <span data-ttu-id="1db68-141">데이터 팩터리의 toohello '작성자 및 배포' 섹션을 탐색 하 여이 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-141">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="1db68-142">'새 데이터 집합' 및 'Azure Blob 저장소' toolink 저장소 tooyour 데이터 팩터리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-142">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="1db68-143">Azure Blob 저장소에 스크립트 toodefine 아래 hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-143">You can use hello below script toodefine your data in Azure Blob storage:</span></span>

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


1. <span data-ttu-id="1db68-144">이제 SQL 데이터 웨어하우스의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="1db68-145">Hello에서 시작 '새 데이터 집합' 및 ' Azure SQL 데이터 웨어하우스 '를 클릭 하 여 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-145">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="1db68-146">3단계: 파이프라인 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="1db68-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="1db68-147">마지막으로, Azure 데이터 팩터리에서 hello 파이프라인을 설정 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-147">Finally, we will set-up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="1db68-148">Hello 실제 데이터 이동이 완료 되는 hello 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-148">This is hello operation that will complete hello actual data movement.</span></span>  <span data-ttu-id="1db68-149">SQL 데이터 웨어하우스 및 Azure Data Factory를 완료할 수 있는 hello 작업의 전체 뷰를 찾을 수 [여기][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-149">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="1db68-150">Hello '작성자 및 배포' 섹션에서 이제 ' 기타 명령을 ' 및 ' 새 파이프라인 '을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-150">In hello 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="1db68-151">Hello 파이프라인을 만든 후에 아래 코드 tootransfer hello 데이터 tooyour 데이터 웨어하우스 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-151">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1db68-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1db68-152">Next steps</span></span>
<span data-ttu-id="1db68-153">toolearn을 확인 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-153">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="1db68-154">[Azure Data Factory 학습 경로][Azure Data Factory learning path]</span><span class="sxs-lookup"><span data-stu-id="1db68-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="1db68-155">[Azure SQL Data Warehouse 커넥터][Azure SQL Data Warehouse Connector]</span><span class="sxs-lookup"><span data-stu-id="1db68-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="1db68-156">Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스에 대 한 hello 코어 참조 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-156">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="1db68-157">이러한 항목은 Azure Data Factory에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="1db68-158">Azure SQL 데이터베이스 또는 HDinsight에 이야기 있지만 tooAzure SQL 데이터 웨어하우스 hello 정보에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-158">They discuss Azure SQL Database or HDinsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="1db68-159">[자습서: Azure 데이터 팩터리 시작] [ Tutorial: Get started with Azure Data Factory] Azure 데이터 팩터리를 사용 하 여 데이터를 처리 하기 위한 hello 코어 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="1db68-160">이 자습서에서는 HDInsight tootransform를 사용 하 여 첫 번째 파이프라인 빌드하고 월별로 웹 로그 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-160">In this tutorial you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="1db68-161">이 자습서에는 복사 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="1db68-162">[자습서: Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]합니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-162">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="1db68-163">이 자습서에서는 Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 Azure Data Factory toocopy 데이터에서 파이프라인을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1db68-163">In this tutorial, you will create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

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
