---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Azure Blob 저장소에서 Azure SQL Data Warehouse(Azure Data Factory)로 데이터 로드 | Microsoft Docs"
description: "Azure Data Factory를 사용하여 데이터를 로드하는 방법을 알아보세요."
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
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="0f307-103">Azure Blob 저장소에서 Azure SQL 데이터 웨어하우스로 데이터 로드(Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="0f307-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f307-104">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="0f307-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="0f307-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="0f307-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="0f307-106">이 자습서는 Azure Data Factory에서 파이프라인을 만들어 Azure 저장소 BLOB에서 SQL 데이터 웨어하우스로 데이터를 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span></span> <span data-ttu-id="0f307-107">다음 단계에서 수행할 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-107">With the following steps you will:</span></span>

* <span data-ttu-id="0f307-108">Azure 저장소 BLOB에서 샘플 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="0f307-109">Azure Data Factory로 리소스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-109">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="0f307-110">저장소 BLOB에서 SQL 데이터 웨어하우스로 데이터를 이동하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="0f307-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0f307-111">Before you begin</span></span>
<span data-ttu-id="0f307-112">Azure Data Factory를 익히려면 [Azure Data Factory 소개][Introduction to Azure Data Factory]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f307-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="0f307-113">리소스 만들기 또는 식별</span><span class="sxs-lookup"><span data-stu-id="0f307-113">Create or identify resources</span></span>
<span data-ttu-id="0f307-114">이 자습서를 시작하기 전에 다음 리소스를 마련해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-114">Before starting this tutorial, you need to have the following resources.</span></span>

* <span data-ttu-id="0f307-115">**Azure 저장소 BLOB**: 이 자습서에서는 Azure Data Factory 파이프라인에 대한 데이터 원본으로 Azure BLOB 저장소를 사용하므로 샘플 데이터를 저장할 Azure BLOB 저장소가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="0f307-116">저장소 계정이 아직 없는 경우 [저장소 계정을 만드는 방법][Create a storage account]을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="0f307-117">**SQL Data Warehouse**: 이 자습서는 Azure Storage Blob에서 SQL Data Warehouse로 데이터를 이동하므로 AdventureWorksDW 샘플 데이터와 함께 로드되는 데이터 웨어하우스 온라인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="0f307-118">데이터 웨어하우스가 아직 없는 경우 [프로비전하는 방법][Create a SQL Data Warehouse]을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="0f307-119">데이터 웨어하우스가 있지만 샘플 데이터를 사용하여 프로비전하지 않은 경우 [수동으로 로드][Load sample data into SQL Data Warehouse]할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="0f307-120">**Azure Data Factory**: Azure Data Factory에서 실제로 로드를 완료하므로 데이터 이동 파이프라인을 빌드하는 데 사용할 수 있는 Azure Data Factory가 필요합니다. 아직 없는 경우 [Azure Data Factory 시작(Data Factory 편집기)][Get started with Azure Data Factory (Data Factory Editor)]의 1단계에서 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="0f307-121">**AZCopy**: 로컬 클라이언트에서 Azure 저장소 BLOB으로 샘플 데이터를 복사할 AZCopy가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="0f307-122">설치 지침은 [AZCopy 설명서][AZCopy documentation]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f307-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="0f307-123">1단계: 샘플 데이터를 Azure 저장소 Blob에 복사</span><span class="sxs-lookup"><span data-stu-id="0f307-123">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="0f307-124">모든 부분이 준비되면 샘플 데이터를 Azure 저장소 Blob에 복사할 준비가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="0f307-125">[샘플 데이터를 다운로드][Download sample data]합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="0f307-126">이 데이터는 AdventureWorksDW 샘플 데이터에 3년의 판매 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="0f307-127">이 AZCopy 명령을 사용하여 Azure 저장소 Blob에 3년 분량의 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="0f307-128">2단계: Azure Data Factory로 리소스를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-128">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="0f307-129">이제 데이터가 생성되었으므로 Azure 데이터 팩터리 파이프라인을 만들어 Azure Blob 저장소에서 SQL 데이터 웨어하우스로 데이터를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="0f307-130">시작하려면 [Azure Portal][Azure portal]을 열고 왼쪽 메뉴에서 사용자의 데이터 팩터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="0f307-131">2.1단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f307-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="0f307-132">Azure 저장소 계정과 SQL 데이터 웨어하우스를 데이터 팩터리로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="0f307-133">우선 데이터 팩터리의 '연결된 서비스' 섹션을 클릭한 다음 '새 데이터 저장소'를 클릭하여 등록 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="0f307-134">Azure 저장소를 등록할 이름을 선택하고 유형으로 Azure 저장소를 선택한 다음 계정 이름과 계정 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="0f307-135">SQL 데이터 웨어하우스를 등록하려면 '작성 및 배포' 섹션을 탐색하고 '새 데이터 저장소'와 'Azure SQL 데이터 웨어하우스'를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="0f307-136">이 템플릿에 붙여 넣은 다음 특정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-136">Copy and paste in this template, and then fill in your specific information.</span></span>

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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="0f307-137">2.2단계: 데이터 집합 정의</span><span class="sxs-lookup"><span data-stu-id="0f307-137">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="0f307-138">연결된 서비스를 만든 다음 데이터 집합을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-138">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="0f307-139">여기서 저장소에서 데이터 웨어하우스로 이동하는 데이터의 구조를 정의하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="0f307-140">만들기에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-140">You can read more about creating</span></span>

1. <span data-ttu-id="0f307-141">이 프로세스를 시작하려면 가장 먼저 사용자 데이터 팩터리의 '작성 및 배포' 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="0f307-142">'새 데이터 집합'을 클릭한 다음 'Azure BLOB 저장소'를 클릭하여 저장소를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="0f307-143">아래 스크립트를 사용하여 Azure BLOB 저장소에서 데이터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-143">You can use the below script to define your data in Azure Blob storage:</span></span>

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


1. <span data-ttu-id="0f307-144">이제 SQL 데이터 웨어하우스의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="0f307-145">마찬가지로 '새 데이터 집합'을 클릭한 다음 'Azure SQL 데이터 웨어하우스'를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="0f307-146">3단계: 파이프라인 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="0f307-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="0f307-147">마지막으로 Azure Data Factory에서 파이프라인을 설정 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="0f307-148">이 작업을 수행하면 실제 데이터 이동이 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-148">This is the operation that will complete the actual data movement.</span></span>  <span data-ttu-id="0f307-149">[여기][Move data to and from Azure SQL Data Warehouse using Azure Data Factory]서 SQL Data Warehouse와 Azure Data Factory를 사용하여 수행할 수 있는 작업에 대한 전체 보기를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="0f307-150">'작성 및 배포' 섹션에서 이제 '추가 명령'을 클릭한 다음 '새 파이프라인'을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="0f307-151">파이프라인을 만든 다음 아래 코드를 사용하여 데이터를 데이터 웨어하우스로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0f307-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f307-152">Next steps</span></span>
<span data-ttu-id="0f307-153">자세한 내용은 다음을 확인하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-153">To learn more, start by viewing:</span></span>

* <span data-ttu-id="0f307-154">[Azure Data Factory 학습 경로][Azure Data Factory learning path]</span><span class="sxs-lookup"><span data-stu-id="0f307-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="0f307-155">[Azure SQL Data Warehouse 커넥터][Azure SQL Data Warehouse Connector]</span><span class="sxs-lookup"><span data-stu-id="0f307-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="0f307-156">Azure SQL 데이터 웨어하우스와 함께 Azure Data Factory를 사용하기 위한 핵심 참조 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="0f307-157">이러한 항목은 Azure Data Factory에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="0f307-158">Azure SQL 데이터베이스 또는 HDinsight를 설명하지만 해당 정보는 Azure SQL 데이터 웨어하우스에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="0f307-159">[자습서: Azure Data Factory 시작][Tutorial: Get started with Azure Data Factory] Azure Data Factory를 사용하여 데이터를 처리하기 위한 핵심 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="0f307-160">이 자습서에서 HDInsight를 사용하여 월별 웹 로그를 변환 및 분석하는 첫 번째 파이프라인을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="0f307-161">이 자습서에는 복사 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="0f307-162">[자습서: Azure Storage Blob에서 Azure SQL Database로 데이터 복사][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]</span><span class="sxs-lookup"><span data-stu-id="0f307-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="0f307-163">이 자습서에서는 Azure 저장소 Blob에서 Azure SQL 데이터베이스로 데이터를 복사하는 파이프라인을 Azure 데이터 팩터리에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f307-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

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
