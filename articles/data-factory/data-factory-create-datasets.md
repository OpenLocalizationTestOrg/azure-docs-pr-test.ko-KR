---
title: "Azure Data Factory에서 데이터 집합 만들기 | Microsoft Docs"
description: "offset 및 anchorDateTime과 같은 속성을 사용하는 예제를 통해 Azure Data Factory에서 데이터 집합을 만드는 방법에 대해 알아봅니다."
keywords: "데이터 집합 만들기, 데이터 집합 예제, 오프셋 예제"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="cb1fd-104">Azure 데이터 팩터리의 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="cb1fd-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="cb1fd-105">이 문서에서는 데이터 집합의 정의, 데이터 집합을 JSON 형식으로 정의하는 방법, Azure Data Factory 파이프라인에서 데이터 집합을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="cb1fd-106">데이터 집합 JSON 정의의 각 섹션(예: 구조, 가용성 및 정책)에 대한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="cb1fd-107">또한 데이터 집합 JSON 정의에서 **offset**, **anchorDateTime** 및 **style** 속성을 사용하기 위한 예제도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="cb1fd-108">Data Factory를 처음 사용하는 경우 [Azure Data Factory 소개](data-factory-introduction.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="cb1fd-109">데이터 팩터리를 실제로 만들어 본 경험이 없는 경우 [데이터 변환 자습서](data-factory-build-your-first-pipeline.md) 및 [데이터 이동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하면 더 나은 이해를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="cb1fd-110">개요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-110">Overview</span></span>
<span data-ttu-id="cb1fd-111">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="cb1fd-112">**파이프라인**은 함께 하나의 작업을 수행하는 **활동**의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="cb1fd-113">파이프라인의 활동은 데이터에 수행할 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="cb1fd-114">예를 들어 복사 활동을 사용하여 온-프레미스 SQL Server에서 Azure Blob 저장소로 데이터를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="cb1fd-115">그런 다음 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하는 Hive 활동을 사용하여 출력 데이터를 생성하도록 Blob 저장소의 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="cb1fd-116">마지막으로 두 번째 복사 활동을 사용하여 BI(비즈니스 인텔리전스) 보고 솔루션의 기반이 되는 Azure SQL Data Warehouse로 출력 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="cb1fd-117">파이프라인 및 활동에 대한 자세한 내용은 [Azure Data Factory의 파이프라인 및 활동](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="cb1fd-118">활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="cb1fd-119">파이프라인에서 입력 데이터 집합은 활동에 대한 입력을 나타내고, 출력 데이터 집합은 활동에 대한 출력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="cb1fd-120">데이터 집합은 테이블, 파일, 폴더, 문서를 비롯한 다양한 데이터 저장소 내의 데이터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="cb1fd-121">예를 들어 Azure Blob 데이터 집합은 파이프라인에서 데이터를 읽어들여야 하는 Blob 저장소의 Blob 컨테이너와 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="cb1fd-122">데이터 집합을 만들기 전에 **연결된 서비스**를 만들어 데이터 저장소를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="cb1fd-123">연결된 서비스는 Data Factory에서 외부 리소스에 연결하는 데 필요한 연결 정보를 정의하는 연결 문자열과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="cb1fd-124">데이터 집합은 SQL 테이블, 파일, 폴더, 문서를 비롯한 연결된 데이터 저장소 내의 데이터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="cb1fd-125">예를 들어 Azure Storage 연결된 서비스는 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="cb1fd-126">Azure Blob 데이터 집합은 blob 컨테이너 및 처리할 입력 blob이 포함된 폴더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="cb1fd-127">샘플 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-127">Here is a sample scenario.</span></span> <span data-ttu-id="cb1fd-128">데이터베이스를 Blob 저장소에서 Azure SQL Database로 복사하려면 두 개의 연결된 서비스, 즉 Azure Storage 및 Azure SQL Database를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="cb1fd-129">그런 다음 두 개의 데이터 집합, 즉 Azure Blob 데이터 집합(Azure Storage 연결된 서비스 참조), Azure SQL 테이블 데이터 집합(Azure SQL Database 연결된 서비스 참조)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="cb1fd-130">Azure Storage 및 Azure SQL Database 연결된 서비스에는 Data Factory가 런타임에 Azure Storage 및 Azure SQL Database 각각에 연결하는 데 사용하는 연결 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="cb1fd-131">Azure Blob 데이터 집합은 Blob 저장소에 입력 Blob을 포함하는 Blob 컨테이너와 Blob 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="cb1fd-132">Azure SQL 테이블 데이터 집합은 데이터를 복사할 Azure SQL Database의 SQL 테이블을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="cb1fd-133">다음 다이어그램에서는 Data Factory의 파이프라인, 활동, 데이터 집합 및 연결된 서비스 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![파이프라인, 활동, 데이터 집합, 연결된 서비스 간 관계](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="cb1fd-135">데이터 집합 JSON</span><span class="sxs-lookup"><span data-stu-id="cb1fd-135">Dataset JSON</span></span>
<span data-ttu-id="cb1fd-136">Data Factory의 데이터 집합은 다음과 같이 JSON 형식으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="cb1fd-137">다음 표에서는 위의 JSON에서 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="cb1fd-138">속성</span><span class="sxs-lookup"><span data-stu-id="cb1fd-138">Property</span></span> | <span data-ttu-id="cb1fd-139">설명</span><span class="sxs-lookup"><span data-stu-id="cb1fd-139">Description</span></span> | <span data-ttu-id="cb1fd-140">필수</span><span class="sxs-lookup"><span data-stu-id="cb1fd-140">Required</span></span> | <span data-ttu-id="cb1fd-141">기본값</span><span class="sxs-lookup"><span data-stu-id="cb1fd-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb1fd-142">name</span><span class="sxs-lookup"><span data-stu-id="cb1fd-142">name</span></span> |<span data-ttu-id="cb1fd-143">데이터 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-143">Name of the dataset.</span></span> <span data-ttu-id="cb1fd-144">명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="cb1fd-145">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-145">Yes</span></span> |<span data-ttu-id="cb1fd-146">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-146">NA</span></span> |
| <span data-ttu-id="cb1fd-147">type</span><span class="sxs-lookup"><span data-stu-id="cb1fd-147">type</span></span> |<span data-ttu-id="cb1fd-148">데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-148">Type of the dataset.</span></span> <span data-ttu-id="cb1fd-149">Data Factory에서 지원하는 형식(예: AzureBlob, AzureSqlTable) 중 하나를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="cb1fd-150">자세한 내용은 [데이터 집합 형식](#Type)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="cb1fd-151">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-151">Yes</span></span> |<span data-ttu-id="cb1fd-152">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-152">NA</span></span> |
| <span data-ttu-id="cb1fd-153">structure</span><span class="sxs-lookup"><span data-stu-id="cb1fd-153">structure</span></span> |<span data-ttu-id="cb1fd-154">데이터 집합의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="cb1fd-155">자세한 내용은 [데이터 집합 구조](#Structure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="cb1fd-156">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-156">No</span></span> |<span data-ttu-id="cb1fd-157">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-157">NA</span></span> |
| <span data-ttu-id="cb1fd-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="cb1fd-158">typeProperties</span></span> | <span data-ttu-id="cb1fd-159">형식 속성은 형식마다 다릅니다(예: Azure Blob, Azure SQL 테이블).</span><span class="sxs-lookup"><span data-stu-id="cb1fd-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="cb1fd-160">지원되는 형식 및 해당 속성에 대한 자세한 내용은 [데이터 집합 형식](#Type)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="cb1fd-161">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-161">Yes</span></span> |<span data-ttu-id="cb1fd-162">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-162">NA</span></span> |
| <span data-ttu-id="cb1fd-163">external</span><span class="sxs-lookup"><span data-stu-id="cb1fd-163">external</span></span> | <span data-ttu-id="cb1fd-164">데이터 집합이 데이터 팩터리 파이프라인에 의해 명시적으로 생성되는지를 지정하는 부울 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="cb1fd-165">활동에 대한 입력 데이터 집합이 현재 파이프라인에서 생성되지 않으면 이 플래그를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="cb1fd-166">파이프라인에서 첫 번째 활동의 입력 데이터 집합에 대해서는 이 플래그를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="cb1fd-167">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-167">No</span></span> |<span data-ttu-id="cb1fd-168">false</span><span class="sxs-lookup"><span data-stu-id="cb1fd-168">false</span></span> |
| <span data-ttu-id="cb1fd-169">availability</span><span class="sxs-lookup"><span data-stu-id="cb1fd-169">availability</span></span> | <span data-ttu-id="cb1fd-170">데이터 집합 생성에 대한 처리 기간(예: 매시간 또는 매일) 또는 조각화 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="cb1fd-171">각 데이터 단위는 데이터 조각이라는 작업 실행으로 사용되고 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="cb1fd-172">출력 데이터 집합의 가용성을 매일(frequency - Day, interval - 1)로 설정하면 조각이 매일 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="cb1fd-173">자세한 내용은 [데이터 집합 가용성](#Availability)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="cb1fd-174">데이터 집합 조각화 모델에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="cb1fd-175">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-175">Yes</span></span> |<span data-ttu-id="cb1fd-176">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-176">NA</span></span> |
| <span data-ttu-id="cb1fd-177">policy</span><span class="sxs-lookup"><span data-stu-id="cb1fd-177">policy</span></span> |<span data-ttu-id="cb1fd-178">데이터 집합 조각이 충족해야 하는 기준 또는 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="cb1fd-179">자세한 내용은 [데이터 집합 정책](#Policy)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="cb1fd-180">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-180">No</span></span> |<span data-ttu-id="cb1fd-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="cb1fd-182">데이터 집합 예제</span><span class="sxs-lookup"><span data-stu-id="cb1fd-182">Dataset example</span></span>
<span data-ttu-id="cb1fd-183">다음 예제에서 데이터 집합은 Azure SQL 데이터베이스에서 **MyTable**이라는 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="cb1fd-184">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-184">Note the following points:</span></span>

* <span data-ttu-id="cb1fd-185">**type**은 AzureSqlTable로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="cb1fd-186">AzureSqlTable 형식과 관련된 **tableName** 형식 속성은 MyTable로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="cb1fd-187">**linkedServiceName**은 다음 JSON 코드 조각으로 정의된 AzureSqlDatabase 형식의 연결된 서비스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="cb1fd-188">**availability frequency**는 Day로 설정되고, **interval**은 1로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="cb1fd-189">즉 데이터 집합 조각이 매일 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="cb1fd-190">**AzureSqlLinkedService**는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="cb1fd-191">앞의 JSON 코드 조각에서</span><span class="sxs-lookup"><span data-stu-id="cb1fd-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="cb1fd-192">**type**은 AzureSqlDatabase로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="cb1fd-193">**connectionString** 형식 속성은 SQL 데이터베이스에 연결하는 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="cb1fd-194">여기서 볼 수 있듯이 연결된 서비스는 Azure SQL 데이터베이스에 연결하는 방법을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="cb1fd-195">데이터 집합은 파이프라인의 활동에 대한 입력 및 출력으로 사용되는 테이블을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="cb1fd-196">데이터 집합이 파이프라인에서 생성되지 않으면 **external**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="cb1fd-197">이 설정은 파이프라인에서 첫 번째 작업의 입력에 일반적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="cb1fd-198"><a name="Type"></a> 데이터 집합 형식</span><span class="sxs-lookup"><span data-stu-id="cb1fd-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="cb1fd-199">데이터 집합의 형식은 사용하는 데이터 저장소에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="cb1fd-200">Data Factory에서 지원하는 데이터 저장소 목록은 다음 표를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="cb1fd-201">해당 데이터 저장소에 대해 연결된 서비스 및 데이터 집합을 만드는 방법을 알아보려면 데이터 저장소를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="cb1fd-202">*가 있는 데이터 저장소는 서비스(IaaS)로서 온-프레미스 또는 Azure 인프라에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="cb1fd-203">이러한 데이터 저장소에는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="cb1fd-204">이전 섹션의 예제에서 데이터 집합의 형식은 **AzureSqlTable**로 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="cb1fd-205">마찬가지로 Azure Blob 데이터 집합의 경우 데이터 집합의 형식이 다음 JSON과 같이 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="cb1fd-206"><a name="Structure"></a>데이터 집합 구조</span><span class="sxs-lookup"><span data-stu-id="cb1fd-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="cb1fd-207">**structure** 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-207">The **structure** section is optional.</span></span> <span data-ttu-id="cb1fd-208">열의 이름 및 데이터 형식 컬렉션을 포함하여 데이터 집합의 스키마를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="cb1fd-209">형식을 변환하고 열을 원본에서 대상으로 매핑하는 데 사용되는 형식 정보를 structure 섹션에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="cb1fd-210">다음 예제에서 데이터 집합에는 세 개의 열, 즉 `slicetimestamp`, `projectname` 및 `pageviews`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="cb1fd-211">형식은 각각 String, String 및 Decimal입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="cb1fd-212">structure의 각 열에는 다음과 같은 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="cb1fd-213">속성</span><span class="sxs-lookup"><span data-stu-id="cb1fd-213">Property</span></span> | <span data-ttu-id="cb1fd-214">설명</span><span class="sxs-lookup"><span data-stu-id="cb1fd-214">Description</span></span> | <span data-ttu-id="cb1fd-215">필수</span><span class="sxs-lookup"><span data-stu-id="cb1fd-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb1fd-216">name</span><span class="sxs-lookup"><span data-stu-id="cb1fd-216">name</span></span> |<span data-ttu-id="cb1fd-217">열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-217">Name of the column.</span></span> |<span data-ttu-id="cb1fd-218">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-218">Yes</span></span> |
| <span data-ttu-id="cb1fd-219">type</span><span class="sxs-lookup"><span data-stu-id="cb1fd-219">type</span></span> |<span data-ttu-id="cb1fd-220">열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-220">Data type of the column.</span></span>  |<span data-ttu-id="cb1fd-221">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-221">No</span></span> |
| <span data-ttu-id="cb1fd-222">culture</span><span class="sxs-lookup"><span data-stu-id="cb1fd-222">culture</span></span> |<span data-ttu-id="cb1fd-223">type이 `Datetime` 또는 `Datetimeoffset` .NET 형식일 때 사용할 .NET 기반 culture(문화권)입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="cb1fd-224">기본값은 `en-us`입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-224">The default is `en-us`.</span></span> |<span data-ttu-id="cb1fd-225">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-225">No</span></span> |
| <span data-ttu-id="cb1fd-226">format</span><span class="sxs-lookup"><span data-stu-id="cb1fd-226">format</span></span> |<span data-ttu-id="cb1fd-227">type이 `Datetime` 또는 `Datetimeoffset` .NET 형식일 때 사용할 format(서식) 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="cb1fd-228">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-228">No</span></span> |

<span data-ttu-id="cb1fd-229">다음 지침은 structure 정보를 포함할 시기 및 **structure** 섹션에 포함할 내용을 결정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="cb1fd-230">**구조화된 데이터 원본의 경우** 원본 열을 싱크 열에 매핑하고 해당 이름이 동일하지 않은 경우에만 structure 섹션을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="cb1fd-231">이러한 종류의 구조화된 데이터 원본은 데이터 스키마 및 형식 정보를 데이터 자체와 함께 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="cb1fd-232">구조화된 데이터 원본의 예로 SQL Server, Oracle 및 Azure 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="cb1fd-233">구조화된 데이터 원본에 대해 형식 정보를 이미 사용할 수 있으므로 "structure" 섹션을 포함할 때 형식 정보를 포함하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="cb1fd-234">**읽기 데이터 원본(특히 Blob 저장소)에 대한 스키마의 경우** 스키마 또는 형식 정보를 데이터와 함께 저장하지 않고도 데이터를 저장하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="cb1fd-235">이러한 유형의 데이터 원본인 경우 원본 열을 싱크 열로 매핑할 때 구조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="cb1fd-236">또한 데이터 집합이 복사 활동에 대한 입력인 경우 구조가 포함되고 원본 데이터 집합의 데이터 형식을 싱크의 네이티브 형식으로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="cb1fd-237">Data Factory는 structure에 형식 정보를 제공하기 위해 **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset 및 Timespan** 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="cb1fd-238">이러한 값은 CLS(공용 언어 사양) 규격 .NET 기반 type 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="cb1fd-239">데이터 팩터리는 원본 데이터 저장소의 데이터를 싱크 데이터 저장소로 복사할 때 형식 변환을 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="cb1fd-240">데이터 집합 가용성</span><span class="sxs-lookup"><span data-stu-id="cb1fd-240">Dataset availability</span></span>
<span data-ttu-id="cb1fd-241">데이터 집합의 **availability** 섹션은 데이터 집합에 대한 처리 기간(매시간, 매일, 매주 등)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="cb1fd-242">활동 기간에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="cb1fd-243">다음 availability 섹션에서는 매시간 출력 데이터 집합을 생성하거나 매시간 입력 데이터 집합을 사용할 수 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="cb1fd-244">파이프라인에 다음과 같은 시작 및 종료 시간이 있는 경우</span><span class="sxs-lookup"><span data-stu-id="cb1fd-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="cb1fd-245">출력 데이터 집합은 파이프라인 시작 시간 및 종료 시간 내에서 시간별로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="cb1fd-246">따라서 이 파이프라인에서는 각 활동 기간(오전 12-1시, 오전 1-2시, 오전 2-3시, 오전 3-4시, 오전 4-5시)마다 하나씩 5개의 데이터 집합 조각이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="cb1fd-247">다음 표에서는 availability 섹션에서 사용할 수 있는 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="cb1fd-248">속성</span><span class="sxs-lookup"><span data-stu-id="cb1fd-248">Property</span></span> | <span data-ttu-id="cb1fd-249">설명</span><span class="sxs-lookup"><span data-stu-id="cb1fd-249">Description</span></span> | <span data-ttu-id="cb1fd-250">필수</span><span class="sxs-lookup"><span data-stu-id="cb1fd-250">Required</span></span> | <span data-ttu-id="cb1fd-251">기본값</span><span class="sxs-lookup"><span data-stu-id="cb1fd-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb1fd-252">frequency</span><span class="sxs-lookup"><span data-stu-id="cb1fd-252">frequency</span></span> |<span data-ttu-id="cb1fd-253">데이터 집합 조각 생성을 위한 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="cb1fd-254"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="cb1fd-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="cb1fd-255">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-255">Yes</span></span> |<span data-ttu-id="cb1fd-256">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-256">NA</span></span> |
| <span data-ttu-id="cb1fd-257">interval</span><span class="sxs-lookup"><span data-stu-id="cb1fd-257">interval</span></span> |<span data-ttu-id="cb1fd-258">빈도에 대한 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="cb1fd-259">"frequency x interval"은 조각을 생성하는 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="cb1fd-260">예를 들어 데이터 집합을 매시간 조각화해야 하는 경우 <b>frequency</b>를 <b>Hour</b>로, <b>interval</b>을 <b>1</b>로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="cb1fd-261">**frequency**를 **Minute**로 지정하는 경우 interval을 15 이상으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="cb1fd-262">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-262">Yes</span></span> |<span data-ttu-id="cb1fd-263">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-263">NA</span></span> |
| <span data-ttu-id="cb1fd-264">style</span><span class="sxs-lookup"><span data-stu-id="cb1fd-264">style</span></span> |<span data-ttu-id="cb1fd-265">간격의 시작/끝에서 조각을 생성해야 하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="cb1fd-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="cb1fd-266">StartOfInterval</span></span></li><li><span data-ttu-id="cb1fd-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="cb1fd-267">EndOfInterval</span></span></li></ul><span data-ttu-id="cb1fd-268">**frequency**를 **Month**로 설정하고 **style**을 **EndOfInterval**로 설정하는 경우 조각을 매월 마지막 일에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="cb1fd-269">**style**을 **StartOfInterval**로 설정하는 경우 조각을 매월 첫째 일에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="cb1fd-270">**frequency**를 **Day**로 설정하고 **style**을 **EndOfInterval**로 설정하는 경우 조각을 매일 마지막 시간에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="cb1fd-271">**frequency**를 **Hour**로 설정하고 **style**을 **EndOfInterval**로 설정하는 경우 조각을 매시간 끝에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="cb1fd-272">예를 들어 오후 1-2시 기간에 대한 조각은 오후 2시에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="cb1fd-273">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-273">No</span></span> |<span data-ttu-id="cb1fd-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="cb1fd-274">EndOfInterval</span></span> |
| <span data-ttu-id="cb1fd-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="cb1fd-275">anchorDateTime</span></span> |<span data-ttu-id="cb1fd-276">스케줄러에서 사용하는 시간에 절대 위치를 정의하여 데이터 집합 조각 경계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="cb1fd-277">이 속성에 지정된 frequency보다 더 세분화된 날짜 부분이 있으면 이 날짜 부분은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="cb1fd-278">예를 들어 **간격**이 **매시간**(frequency: Hour 및 interval: 1)이고 **anchorDateTime**에 **분 및 초**가 포함되는 경우 **anchorDateTime**의 분 및 초 부분은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="cb1fd-279">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-279">No</span></span> |<span data-ttu-id="cb1fd-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="cb1fd-280">01/01/0001</span></span> |
| <span data-ttu-id="cb1fd-281">offset</span><span class="sxs-lookup"><span data-stu-id="cb1fd-281">offset</span></span> |<span data-ttu-id="cb1fd-282">모든 데이터 집합 조각의 시작과 끝이 이동에 의한 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="cb1fd-283">**anchorDateTime** 및 **offset**이 모두 지정되면 결합된 결과로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="cb1fd-284">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-284">No</span></span> |<span data-ttu-id="cb1fd-285">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="cb1fd-286">offset example</span><span class="sxs-lookup"><span data-stu-id="cb1fd-286">offset example</span></span>
<span data-ttu-id="cb1fd-287">기본적으로 조각은 매일(`"frequency": "Day", "interval": 1`) 오전 12시(자정) UTC(협정 세계시)에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="cb1fd-288">대신, 시작 시간을 UTC 시간으로 오전 6시로 설정하려면 다음 코드 조각과 같이 오프셋을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="cb1fd-289">anchorDateTime 예제</span><span class="sxs-lookup"><span data-stu-id="cb1fd-289">anchorDateTime example</span></span>
<span data-ttu-id="cb1fd-290">다음 예제에서는 데이터 집합이 23시간마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="cb1fd-291">첫 번째 조각은 **anchorDateTime**에 지정된 시간(`2017-04-19T08:00:00`(UTC)으로 설정됨)에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="cb1fd-292">offset/style 예제</span><span class="sxs-lookup"><span data-stu-id="cb1fd-292">offset/style example</span></span>
<span data-ttu-id="cb1fd-293">다음 데이터 집합은 매월 3일, 오전 8시(`3.08:00:00`)에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="cb1fd-294"><a name="Policy"></a>데이터 집합 정책</span><span class="sxs-lookup"><span data-stu-id="cb1fd-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="cb1fd-295">데이터 집합 정의의 **policy** 섹션은 데이터 집합 조각이 충족해야 하는 기준 또는 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="cb1fd-296">정책 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="cb1fd-296">Validation policies</span></span>
| <span data-ttu-id="cb1fd-297">정책 이름</span><span class="sxs-lookup"><span data-stu-id="cb1fd-297">Policy name</span></span> | <span data-ttu-id="cb1fd-298">설명</span><span class="sxs-lookup"><span data-stu-id="cb1fd-298">Description</span></span> | <span data-ttu-id="cb1fd-299">적용 대상</span><span class="sxs-lookup"><span data-stu-id="cb1fd-299">Applied to</span></span> | <span data-ttu-id="cb1fd-300">필수</span><span class="sxs-lookup"><span data-stu-id="cb1fd-300">Required</span></span> | <span data-ttu-id="cb1fd-301">기본값</span><span class="sxs-lookup"><span data-stu-id="cb1fd-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="cb1fd-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="cb1fd-302">minimumSizeMB</span></span> |<span data-ttu-id="cb1fd-303">**Azure Blob 저장소**의 데이터가 최소 크기 요구 사항(MB)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="cb1fd-304">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="cb1fd-304">Azure Blob storage</span></span> |<span data-ttu-id="cb1fd-305">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-305">No</span></span> |<span data-ttu-id="cb1fd-306">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-306">NA</span></span> |
| <span data-ttu-id="cb1fd-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="cb1fd-307">minimumRows</span></span> |<span data-ttu-id="cb1fd-308">**Azure SQL Database** 또는 **Azure 테이블**에서 데이터가 최소 행 수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="cb1fd-309">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="cb1fd-309">Azure SQL database</span></span></li><li><span data-ttu-id="cb1fd-310">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="cb1fd-310">Azure table</span></span></li></ul> |<span data-ttu-id="cb1fd-311">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-311">No</span></span> |<span data-ttu-id="cb1fd-312">해당 없음</span><span class="sxs-lookup"><span data-stu-id="cb1fd-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="cb1fd-313">예</span><span class="sxs-lookup"><span data-stu-id="cb1fd-313">Examples</span></span>
<span data-ttu-id="cb1fd-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="cb1fd-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="cb1fd-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="cb1fd-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="cb1fd-316">외부 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="cb1fd-316">External datasets</span></span>
<span data-ttu-id="cb1fd-317">외부 데이터 집합은 데이터 팩토리에서 실행 중인 파이프라인에 의해 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="cb1fd-318">데이터 집합이 **external**로 표시된 경우 **ExternalData** 정책을 정의하여 데이터 집합 조각 가용성의 동작에 영향을 미칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="cb1fd-319">Data Factory에서 데이터 집합을 생성하지 않는 한 **external**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="cb1fd-320">이 설정은 일반적으로 활동 또는 파이프라인 체이닝을 사용하지 않는 한 파이프라인의 첫 번째 활동에 대한 입력에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="cb1fd-321">이름</span><span class="sxs-lookup"><span data-stu-id="cb1fd-321">Name</span></span> | <span data-ttu-id="cb1fd-322">설명</span><span class="sxs-lookup"><span data-stu-id="cb1fd-322">Description</span></span> | <span data-ttu-id="cb1fd-323">필수</span><span class="sxs-lookup"><span data-stu-id="cb1fd-323">Required</span></span> | <span data-ttu-id="cb1fd-324">기본값</span><span class="sxs-lookup"><span data-stu-id="cb1fd-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb1fd-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="cb1fd-325">dataDelay</span></span> |<span data-ttu-id="cb1fd-326">지정된 조각에 대한 외부 데이터의 가용성 검사를 지연하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="cb1fd-327">예를 들어 이 설정을 사용하여 시간별 검사를 지연할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="cb1fd-328">이 설정은 현재 시간에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="cb1fd-329">예를 들어 현재 오후 1시이고 이 값이 10 분이라면 유효성 검사는 오후 1시 10분에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="cb1fd-330">이전 시간에는 이 설정으로 조각에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="cb1fd-331">**조각 종료 시간** + **dataDelay** < **현재 시간**인 경우 조각은 지연 없이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="cb1fd-332">23:59보다 큰 시간은 `day.hours:minutes:seconds` 형식을 사용하여 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="cb1fd-333">예를 들어 24시간을 지정하려면 24:00:00을 사용하는 대신</span><span class="sxs-lookup"><span data-stu-id="cb1fd-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="cb1fd-334">1.00:00:00을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="cb1fd-335">24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="cb1fd-336">1일 4시간의 경우 1:04:00:00을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="cb1fd-337">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-337">No</span></span> |<span data-ttu-id="cb1fd-338">0</span><span class="sxs-lookup"><span data-stu-id="cb1fd-338">0</span></span> |
| <span data-ttu-id="cb1fd-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="cb1fd-339">retryInterval</span></span> |<span data-ttu-id="cb1fd-340">실패 이후 다음 다시 시도까지의 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="cb1fd-341">이 설정은 현재 시간에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-341">This setting applies to present time.</span></span> <span data-ttu-id="cb1fd-342">이전 시도가 실패한 경우 다음 시도는 **retryInterval** 기간 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="cb1fd-343">오후 1시가 되면 첫 번째 시도를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="cb1fd-344">첫 번째 유효성 검사를 완료하는 데 걸리는 시간이 1분이고 작업이 실패한 경우 다음 다시 시도는 1시 + 1분(기간) + 1분(다시 시도 간격) = 오후 1시 2분입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="cb1fd-345">과거 조각의 경우 지연이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="cb1fd-346">재시도는 곧바로 이뤄집니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-346">The retry happens immediately.</span></span> |<span data-ttu-id="cb1fd-347">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-347">No</span></span> |<span data-ttu-id="cb1fd-348">00:01:00 (1분)</span><span class="sxs-lookup"><span data-stu-id="cb1fd-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="cb1fd-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="cb1fd-349">retryTimeout</span></span> |<span data-ttu-id="cb1fd-350">각 재시도에 대한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="cb1fd-351">이 속성을 10분으로 설정하면 유효성 검사를 10분 내에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="cb1fd-352">유효성 검사를 수행하는 데 10분 보다 오래 걸리는 경우 재시도는 제한 시간을 초과합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="cb1fd-353">모든 유효성 검사 시도에서 시간을 초과하면 조각이 **TimedOut**으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="cb1fd-354">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-354">No</span></span> |<span data-ttu-id="cb1fd-355">00:10:00 (10분)</span><span class="sxs-lookup"><span data-stu-id="cb1fd-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="cb1fd-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="cb1fd-356">maximumRetry</span></span> |<span data-ttu-id="cb1fd-357">외부 데이터의 가용성을 검사하는 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="cb1fd-358">허용되는 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="cb1fd-359">아니요</span><span class="sxs-lookup"><span data-stu-id="cb1fd-359">No</span></span> |<span data-ttu-id="cb1fd-360">3</span><span class="sxs-lookup"><span data-stu-id="cb1fd-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="cb1fd-361">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="cb1fd-361">Create datasets</span></span>
<span data-ttu-id="cb1fd-362">다음 도구 또는 SDK 중 하나를 사용하여 데이터 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="cb1fd-363">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="cb1fd-363">Copy Wizard</span></span> 
- <span data-ttu-id="cb1fd-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cb1fd-364">Azure portal</span></span>
- <span data-ttu-id="cb1fd-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb1fd-365">Visual Studio</span></span>
- <span data-ttu-id="cb1fd-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb1fd-366">PowerShell</span></span>
- <span data-ttu-id="cb1fd-367">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="cb1fd-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="cb1fd-368">REST API</span><span class="sxs-lookup"><span data-stu-id="cb1fd-368">REST API</span></span>
- <span data-ttu-id="cb1fd-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="cb1fd-369">.NET API</span></span>

<span data-ttu-id="cb1fd-370">다음 도구 또는 SDK 중 하나를 사용하여 파이프라인 및 데이터 집합을 만들기 위한 단계별 지침은 다음 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="cb1fd-371">데이터 변환 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="cb1fd-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="cb1fd-372">데이터 이동 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="cb1fd-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="cb1fd-373">파이프라인을 만들고 배포한 후에 Azure Portal 블레이드 또는 모니터링 및 관리 앱을 사용하여 파이프라인을 관리하고 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="cb1fd-374">단계별 지침은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="cb1fd-375">Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="cb1fd-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="cb1fd-376">모니터링 및 관리 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="cb1fd-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="cb1fd-377">범위가 지정된 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="cb1fd-377">Scoped datasets</span></span>
<span data-ttu-id="cb1fd-378">**datasets** 속성을 사용하여 파이프라인으로 범위가 지정되는 데이터 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="cb1fd-379">이러한 데이터 집합은 다른 파이프라인의 활동이 아니라 이 파이프라인 내의 활동에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="cb1fd-380">다음 예제에서는 파이프라인 내에서 사용되는 두 개의 데이터 집합(InputDataset-rdc 및 OutputDataset-rdc)이 있는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="cb1fd-381">범위가 지정된 데이터 집합은 일회성 파이프라인(**pipelineMode**가 **OneTime**으로 설정된 경우)에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="cb1fd-382">자세한 내용은 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="cb1fd-383">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cb1fd-383">Next steps</span></span>
- <span data-ttu-id="cb1fd-384">파이프라인에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="cb1fd-385">파이프라인을 예약하고 실행하는 방법에 대한 자세한 내용은 [Azure Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb1fd-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
