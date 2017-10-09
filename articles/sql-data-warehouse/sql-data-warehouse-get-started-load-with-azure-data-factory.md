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
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="0b558-103">Azure Data Factory를 사용하여 데이터 로드</span><span class="sxs-lookup"><span data-stu-id="0b558-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b558-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="0b558-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="0b558-105">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="0b558-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="0b558-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="0b558-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="0b558-107">BCP</span><span class="sxs-lookup"><span data-stu-id="0b558-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="0b558-108">이 자습서에서는 Azure 저장소 Blob tooAzure SQL 데이터 웨어하우스에서에서 toomove 데이터를 Azure 데이터 팩터리 파이프라인 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="0b558-109">단계를 수행 하는 hello로 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-109">With hello following steps you will:</span></span>

* <span data-ttu-id="0b558-110">Azure Storage Blob에서 샘플 데이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="0b558-111">리소스 tooAzure Data Factory를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="0b558-112">데이터 웨어하우스 저장소 Blob tooSQL에서 파이프라인 toomove 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="0b558-113">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0b558-113">Before you begin</span></span>
<span data-ttu-id="0b558-114">toofamiliarize Azure 데이터 팩터리와 직접 참조 [소개 tooAzure Data Factory][Introduction tooAzure Data Factory]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="0b558-115">리소스 만들기 또는 식별</span><span class="sxs-lookup"><span data-stu-id="0b558-115">Create or identify resources</span></span>
<span data-ttu-id="0b558-116">이 자습서를 시작 하기 전에 다음 리소스 toohave hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="0b558-117">**Azure 저장소 Blob**: toohave 하나의 사용 가능한 toostore hello 샘플 데이터가 필요 하므로 및이 자습서에서는 hello Azure 데이터 팩터리 파이프라인에 대 한 Azure 저장소 Blob hello 데이터 원본으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="0b558-118">없는 경우 하나 이미, 너무 방법을 알아보려면[저장소 계정을 만드는][Create a storage account]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="0b558-119">**SQL 데이터 웨어하우스**: Azure 저장소 Blob에서이 자습서 이동 hello 데이터 너무 SQL 데이터 웨어하우스 등 필요한 toohave AdventureWorksDW 예제 데이터 hello로 로드 되는 데이터 웨어하우스의 온라인입니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="0b558-120">데이터 웨어하우스 아직 없는 경우 너무 방법을 알아볼[하나를 프로 비전][Create a SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="0b558-121">데이터 웨어하우스를 갖지만 hello 예제 데이터와 함께 프로 비전 하지 않은 경우 다음을 할 수 있습니다 [수동으로 로드][Load sample data into SQL Data Warehouse]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="0b558-122">**Azure Data Factory**: Azure Data Factory hello 실제 부하를 완료 하 고 따라서 toobuild hello 데이터 이동을 파이프라인을 사용할 수 있는 하나 toohave 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="0b558-123">없는 이미, 경우에 대해 배울 방법 toocreate 하나 1 단계에서에서의 [(데이터 팩터리 편집기) Azure 데이터 팩터리 시작][Get started with Azure Data Factory (Data Factory Editor)]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="0b558-124">**AZCopy**: 사용자 로컬 클라이언트 tooyour Azure 저장소 Blob에서에서 AZCopy toocopy hello 샘플 데이터가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="0b558-125">설치 지침은 hello [AZCopy 설명서][AZCopy documentation]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="0b558-126">1 단계: 샘플 데이터 tooAzure 저장소 Blob 복사</span><span class="sxs-lookup"><span data-stu-id="0b558-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="0b558-127">모든 hello 조각을 준비 했으면 준비 toocopy 샘플 데이터 tooyour Azure 저장소 Blob 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="0b558-128">[샘플 데이터를 다운로드][Download sample data]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="0b558-129">이 데이터는 다른 3 년의 판매 데이터 tooyour AdventureWorksDW 예제 데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="0b558-130">데이터 tooyour Azure 저장소 Blob의 3 년이 AZCopy 명령 toocopy hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="0b558-131">2 단계: 리소스 tooAzure Data Factory에 연결</span><span class="sxs-lookup"><span data-stu-id="0b558-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="0b558-132">Hello 데이터 준비에서는에서는 만들 수 hello Azure 데이터 팩터리 파이프라인 toomove hello 데이터 Azure blob 저장소의 SQL 데이터 웨어하우스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="0b558-133">tooget 시작 열기 hello [Azure 포털] [ Azure portal] hello 왼쪽 메뉴에서 데이터 팩터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="0b558-134">2.1단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0b558-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="0b558-135">Azure 저장소 계정 및 SQL 데이터 웨어하우스 tooyour 데이터 팩터리에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="0b558-136">먼저, 데이터 팩터리의 hello ' 연결 된 서비스 ' 섹션을 클릭 하 여 hello 등록 프로세스를 시작 하 고 '새 데이터 저장소'를 클릭 한 다음</span><span class="sxs-lookup"><span data-stu-id="0b558-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="0b558-137">이름 tooregister 사용자 형식으로 선택 Azure 저장소에서 azure 저장소를 선택 하 고 계정 이름과 계정 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="0b558-138">SQL 데이터 웨어하우스 tooregister toohello '작성자 및 배포' 섹션 이동 ' 새 데이터 저장소 ' 및 ' Azure SQL 데이터 웨어하우스 '를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="0b558-139">이 템플릿에 붙여 넣은 다음 특정 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="0b558-140">2.2 단계: hello 데이터 집합 정의</span><span class="sxs-lookup"><span data-stu-id="0b558-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="0b558-141">연결 된 서비스를 만드는 hello, म toodefine hello 데이터 집합을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="0b558-142">이 의미 여기 저장소 tooyour 데이터 웨어하우스에서 이동 하는 hello 데이터의 hello 구조를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="0b558-143">만들기에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-143">You can read more about creating</span></span>

1. <span data-ttu-id="0b558-144">데이터 팩터리의 toohello '작성자 및 배포' 섹션을 탐색 하 여이 프로세스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="0b558-145">'새 데이터 집합' 및 'Azure Blob 저장소' toolink 저장소 tooyour 데이터 팩터리를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="0b558-146">Azure Blob 저장소에 스크립트 toodefine 아래 hello 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="0b558-147">이제 SQL Data Warehouse의 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="0b558-148">Hello에서 시작 '새 데이터 집합' 및 ' Azure SQL 데이터 웨어하우스 '를 클릭 하 여 동일한 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="0b558-149">3단계: 파이프라인 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="0b558-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="0b558-150">마지막으로 설정 하 고 Azure Data Factory에서 hello 파이프라인을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="0b558-151">이 hello 작업 완료 hello 실제 데이터 이동입니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="0b558-152">SQL 데이터 웨어하우스 및 Azure Data Factory를 완료할 수 있는 hello 작업의 전체 뷰를 찾을 수 [여기][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="0b558-153">Hello' 작성자 및 배포 ', ' 기타 명령을 ' 및 ' 새 파이프라인 '를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="0b558-154">Hello 파이프라인을 만든 후에 아래 코드 tootransfer hello 데이터 tooyour 데이터 웨어하우스 hello를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0b558-155">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b558-155">Next steps</span></span>
<span data-ttu-id="0b558-156">toolearn을 확인 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="0b558-157">[Azure Data Factory 학습 경로][Azure Data Factory learning path]</span><span class="sxs-lookup"><span data-stu-id="0b558-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="0b558-158">[Azure SQL Data Warehouse 커넥터][Azure SQL Data Warehouse Connector]</span><span class="sxs-lookup"><span data-stu-id="0b558-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="0b558-159">Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스에 대 한 hello 코어 참조 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="0b558-160">이러한 항목은 Azure Data Factory에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="0b558-161">Azure SQL 데이터베이스 또는 HDInsight에 이야기 있지만 tooAzure SQL 데이터 웨어하우스 hello 정보에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="0b558-162">[자습서: Azure 데이터 팩터리 시작] [ Tutorial: Get started with Azure Data Factory] Azure 데이터 팩터리를 사용 하 여 데이터를 처리 하기 위한 hello 코어 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="0b558-163">이 자습서에서는 HDInsight tootransform를 사용 하 여 첫 번째 파이프라인 빌드하고 월별로 웹 로그 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="0b558-164">이 자습서에는 복사 작업이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="0b558-165">[자습서: Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 데이터를 복사][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]합니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="0b558-166">이 자습서에서는 Azure 저장소 Blob tooAzure SQL 데이터베이스에서에서 Azure Data Factory toocopy 데이터에서 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b558-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

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
