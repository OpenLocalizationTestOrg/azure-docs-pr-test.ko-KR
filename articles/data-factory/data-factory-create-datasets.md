---
title: "Azure Data Factory에서 데이터 집합 aaaCreate | Microsoft Docs"
description: "AnchorDateTime 및 등의 속성을 사용 하는 예제 Azure Data Factory에서 toocreate 데이터 집합 오프셋 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="6656d-104">Azure 데이터 팩터리의 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="6656d-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="6656d-105">이 문서에서는 데이터 집합의 정의, 데이터 집합을 JSON 형식으로 정의하는 방법, Azure Data Factory 파이프라인에서 데이터 집합을 사용하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="6656d-106">Hello 데이터 집합 JSON 정의에서 각 섹션 (예를 들어 구조, 가용성 및 정책)에 대 한 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="6656d-107">hello 문서도 예를 제공 hello를 사용 하 여 **오프셋**, **anchorDateTime**, 및 **스타일** 데이터 집합 JSON 정의에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="6656d-108">새 tooData 팩터리 인 경우 참조 [소개 tooAzure Data Factory](data-factory-introduction.md) 에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="6656d-109">데이터 팩터리를 만드는 것부터 직접 경험이 읽는 hello 하 여 더 잘 이해를 얻을 수 있습니다 [데이터 변환 자습서](data-factory-build-your-first-pipeline.md) 및 hello [데이터 이동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="6656d-110">개요</span><span class="sxs-lookup"><span data-stu-id="6656d-110">Overview</span></span>
<span data-ttu-id="6656d-111">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="6656d-112">**파이프라인**은 함께 하나의 작업을 수행하는 **활동**의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="6656d-113">파이프라인의 hello 활동 데이터에 대해 작업 tooperform를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="6656d-114">예를 들어 온-프레미스 SQL Server tooAzure Blob 저장소에서에서 복사 작업 toocopy 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="6656d-115">그런 다음 Azure HDInsight 클러스터 tooprocess 데이터에서 Blob 저장소 tooproduce 출력 데이터에서 하이브 스크립트를 실행 하는 하이브 활동을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="6656d-116">마지막으로 두 번째 복사본 활동 toocopy hello 출력 데이터 tooAzure SQL 데이터 웨어하우스 위에 있는 BI (비즈니스 인텔리전스) 솔루션은 빌드됩니다 보고를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="6656d-117">파이프라인 및 활동에 대한 자세한 내용은 [Azure Data Factory의 파이프라인 및 활동](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="6656d-118">활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="6656d-119">입력된 데이터 집합 hello 파이프라인의 활동에 대 한 hello 입력을 나타내고 출력 데이터 집합 hello 활동에 대 한 hello 출력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="6656d-120">데이터 집합은 테이블, 파일, 폴더, 문서를 비롯한 다양한 데이터 저장소 내의 데이터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="6656d-121">예를 들어 된 Azure Blob 데이터 집합에서 어떤 hello 파이프라인 hello 데이터 읽어야 하는 Blob 저장소에 hello blob 컨테이너 및 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="6656d-122">데이터 집합을 만들기 전에 만듭니다는 **연결 된 서비스** toolink 데이터 toohello 데이터 팩터리를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="6656d-123">연결 된 서비스 데이터 팩터리의 tooconnect tooexternal 리소스에 대 한 필요한 hello 연결 정보를 정의 하는 연결 문자열 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="6656d-124">SQL 테이블, 파일, 폴더, 문서 등 hello 연결 된 데이터 저장소 내에서 데이터를 식별 하는 데이터 집합.</span><span class="sxs-lookup"><span data-stu-id="6656d-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="6656d-125">예를 들어 Azure 저장소는 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="6656d-126">Azure Blob 데이터 집합을 hello blob 컨테이너 및 처리 하는 hello 입력된 blob toobe 있는 hello 폴더를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="6656d-127">샘플 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-127">Here is a sample scenario.</span></span> <span data-ttu-id="6656d-128">toocopy 데이터 Blob storage tooa SQL 데이터베이스의 경우, 두 개의 연결 된 서비스를 만들: Azure 저장소 및 Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="6656d-129">그런 다음 두 개의 데이터 집합을 만듭니다: Azure Blob 데이터 집합 (가리키는, toohello Azure 저장소 연결 된 서비스) 및 Azure SQL 테이블 (toohello 연결 된 Azure SQL 데이터베이스 서비스 참조)입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="6656d-130">hello Azure 저장소 및 Azure SQL 데이터베이스 연결 된 서비스 데이터 팩터리의 각각 런타임 tooconnect tooyour Azure 저장소 및 Azure SQL 데이터베이스에서 사용 하는 연결 문자열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="6656d-131">hello Azure Blob 데이터 집합 hello blob 컨테이너 및 Blob 저장소에 hello 입력된 blob이 포함 된 blob 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="6656d-132">hello Azure SQL 테이블의 데이터 집합에 SQL 데이터베이스 toowhich hello 데이터 hello SQL 테이블 복사 toobe을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="6656d-133">hello 다음 다이어그램 hello 사이의 관계를 표시 파이프라인, 활동, 데이터 집합 및 연결 된 서비스 Data Factory에:</span><span class="sxs-lookup"><span data-stu-id="6656d-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![파이프라인, 활동, 데이터 집합, 연결된 서비스 간 관계](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="6656d-135">데이터 집합 JSON</span><span class="sxs-lookup"><span data-stu-id="6656d-135">Dataset JSON</span></span>
<span data-ttu-id="6656d-136">Data Factory의 데이터 집합은 다음과 같이 JSON 형식으로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="6656d-137">다음 표에 hello JSON 위에 hello에 대 한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="6656d-138">속성</span><span class="sxs-lookup"><span data-stu-id="6656d-138">Property</span></span> | <span data-ttu-id="6656d-139">설명</span><span class="sxs-lookup"><span data-stu-id="6656d-139">Description</span></span> | <span data-ttu-id="6656d-140">필수</span><span class="sxs-lookup"><span data-stu-id="6656d-140">Required</span></span> | <span data-ttu-id="6656d-141">기본값</span><span class="sxs-lookup"><span data-stu-id="6656d-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6656d-142">name</span><span class="sxs-lookup"><span data-stu-id="6656d-142">name</span></span> |<span data-ttu-id="6656d-143">Hello 데이터 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-143">Name of hello dataset.</span></span> <span data-ttu-id="6656d-144">명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="6656d-145">예</span><span class="sxs-lookup"><span data-stu-id="6656d-145">Yes</span></span> |<span data-ttu-id="6656d-146">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-146">NA</span></span> |
| <span data-ttu-id="6656d-147">type</span><span class="sxs-lookup"><span data-stu-id="6656d-147">type</span></span> |<span data-ttu-id="6656d-148">hello 데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-148">Type of hello dataset.</span></span> <span data-ttu-id="6656d-149">Data Factory에서 지 원하는 hello 형식 중 하나를 지정 (예: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="6656d-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="6656d-150">자세한 내용은 [데이터 집합 형식](#Type)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="6656d-151">예</span><span class="sxs-lookup"><span data-stu-id="6656d-151">Yes</span></span> |<span data-ttu-id="6656d-152">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-152">NA</span></span> |
| <span data-ttu-id="6656d-153">structure</span><span class="sxs-lookup"><span data-stu-id="6656d-153">structure</span></span> |<span data-ttu-id="6656d-154">Hello 데이터 집합의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="6656d-155">자세한 내용은 [데이터 집합 구조](#Structure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="6656d-156">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-156">No</span></span> |<span data-ttu-id="6656d-157">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-157">NA</span></span> |
| <span data-ttu-id="6656d-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="6656d-158">typeProperties</span></span> | <span data-ttu-id="6656d-159">hello 유형 속성은 각 유형에 대해 서로 다릅니다 (예: Azure Blob, Azure SQL 테이블).</span><span class="sxs-lookup"><span data-stu-id="6656d-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="6656d-160">Hello 지원 형식 및 해당 속성에 대 한 자세한 내용은 참조 하십시오. [Dataset 형식](#Type)합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="6656d-161">예</span><span class="sxs-lookup"><span data-stu-id="6656d-161">Yes</span></span> |<span data-ttu-id="6656d-162">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-162">NA</span></span> |
| <span data-ttu-id="6656d-163">external</span><span class="sxs-lookup"><span data-stu-id="6656d-163">external</span></span> | <span data-ttu-id="6656d-164">부울 여부 데이터 팩터리 파이프라인에서 명시적으로 데이터 집합은 생성 여부 toospecify를 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="6656d-165">활동에 대 한 입력된 데이터 집합 hello hello 현재 파이프라인에 의해 생성 되지 않습니다, 하는 경우이 플래그 tootrue를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="6656d-166">이 플래그 tootrue hello hello 첫 번째 활동의 입력된 데이터 집합에 대 한 hello 파이프라인에서 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="6656d-167">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-167">No</span></span> |<span data-ttu-id="6656d-168">false</span><span class="sxs-lookup"><span data-stu-id="6656d-168">false</span></span> |
| <span data-ttu-id="6656d-169">availability</span><span class="sxs-lookup"><span data-stu-id="6656d-169">availability</span></span> | <span data-ttu-id="6656d-170">Hello 처리 기간이 (매시간 또는 매일) 또는 데이터 집합 프로덕션 hello에 대 한 모델을 조각화 하는 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="6656d-171">각 데이터 단위는 데이터 조각이라는 작업 실행으로 사용되고 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="6656d-172">출력 데이터 집합의 hello 가용성 집합 toodaily (빈도-Day, 간격-1) 이면 조각은 매일 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="6656d-173">자세한 내용은 [데이터 집합 가용성](#Availability)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="6656d-174">Hello 데이터 집합에 대 한 자세한 내용은 hello 참조 모델을 조각화 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="6656d-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="6656d-175">예</span><span class="sxs-lookup"><span data-stu-id="6656d-175">Yes</span></span> |<span data-ttu-id="6656d-176">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-176">NA</span></span> |
| <span data-ttu-id="6656d-177">policy</span><span class="sxs-lookup"><span data-stu-id="6656d-177">policy</span></span> |<span data-ttu-id="6656d-178">Hello 조건 또는 hello 데이터 집합 분할 영역 충족 해야 하는 hello 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="6656d-179">자세한 내용은 참조 hello [Dataset 정책](#Policy) 섹션.</span><span class="sxs-lookup"><span data-stu-id="6656d-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="6656d-180">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-180">No</span></span> |<span data-ttu-id="6656d-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="6656d-182">데이터 집합 예제</span><span class="sxs-lookup"><span data-stu-id="6656d-182">Dataset example</span></span>
<span data-ttu-id="6656d-183">다음 예제는 hello, hello 데이터 집합 이라는 테이블 나타냅니다 **MyTable** SQL 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="6656d-184">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="6656d-184">Note hello following points:</span></span>

* <span data-ttu-id="6656d-185">**형식** tooAzureSqlTable 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="6656d-186">**tableName** type 속성 (특정 tooAzureSqlTable 유형) tooMyTable 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="6656d-187">**linkedServiceName** AzureSqlDatabase hello 다음 JSON 코드 조각은에 정의 된 유형의 tooa 연결 된 서비스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="6656d-188">**가용성 주파수** tooDay, 설정 및 **간격** too1 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="6656d-189">즉, 해당 hello 데이터 집합 조각이 매일 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="6656d-190">**AzureSqlLinkedService**는 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="6656d-191">JSON 코드 조각은 앞 hello:</span><span class="sxs-lookup"><span data-stu-id="6656d-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="6656d-192">**형식** tooAzureSqlDatabase 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="6656d-193">**connectionString** type 속성 정보 tooconnect tooa SQL 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="6656d-194">볼 수 있듯이 hello 연결 된 서비스 정의 방법을 tooconnect tooa SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="6656d-195">hello 데이터 집합 테이블을 입력으로 사용 되 고 파이프라인의 hello 활동에 대 한 출력을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="6656d-196">로 표시 되어야 합니다 hello 파이프라인에서 데이터 집합을이 생성 하지 않는 한 **외부**합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="6656d-197">이 설정은 일반적으로 파이프라인의 첫 번째 활동의 tooinputs를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="6656d-198"><a name="Type"></a> 데이터 집합 형식</span><span class="sxs-lookup"><span data-stu-id="6656d-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="6656d-199">hello 데이터 저장소를 사용 하면에 hello 데이터 집합의 hello 유형에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="6656d-200">Hello 다음 Data Factory에서 지 원하는 데이터 저장소 목록에 대 한 표를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6656d-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="6656d-201">데이터 저장소 toolearn 클릭 toocreate 연결 된 서비스와 해당 데이터에 대 한 데이터 집합 저장 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="6656d-202">*가 있는 데이터 저장소는 서비스(IaaS)로서 온-프레미스 또는 Azure 인프라에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="6656d-203">이러한 데이터 저장소 요구 tooinstall [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="6656d-204">Hello 데이터 집합의 hello 유형이 너무 설정 hello 이전 단원의 hello 예에서**AzureSqlTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="6656d-205">마찬가지로, Azure Blob 데이터 집합의 경우 hello 유형이 hello 데이터 집합의 설정 되어 너무**AzureBlob**hello JSON 뒤에 나타난 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="6656d-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

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

## <span data-ttu-id="6656d-206"><a name="Structure"></a>데이터 집합 구조</span><span class="sxs-lookup"><span data-stu-id="6656d-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="6656d-207">hello **구조** 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-207">hello **structure** section is optional.</span></span> <span data-ttu-id="6656d-208">이름 및 데이터 형식 열의 컬렉션을 포함 하 여 hello 데이터 집합의 hello 스키마를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="6656d-209">Hello 구조 섹션 tooprovide 형식 정보를 사용 하는 tooconvert 형식과 hello 소스 toohello 대상에서 매핑되지 않은 열은 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="6656d-210">다음 예제는 hello, hello 데이터 집합에 3 개의 열이: `slicetimestamp`, `projectname`, 및 `pageviews`합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="6656d-211">형식은 각각 String, String 및 Decimal입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="6656d-212">Hello 구조에서 각 열에 다음 속성이 hello를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="6656d-213">속성</span><span class="sxs-lookup"><span data-stu-id="6656d-213">Property</span></span> | <span data-ttu-id="6656d-214">설명</span><span class="sxs-lookup"><span data-stu-id="6656d-214">Description</span></span> | <span data-ttu-id="6656d-215">필수</span><span class="sxs-lookup"><span data-stu-id="6656d-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6656d-216">name</span><span class="sxs-lookup"><span data-stu-id="6656d-216">name</span></span> |<span data-ttu-id="6656d-217">Hello 열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-217">Name of hello column.</span></span> |<span data-ttu-id="6656d-218">예</span><span class="sxs-lookup"><span data-stu-id="6656d-218">Yes</span></span> |
| <span data-ttu-id="6656d-219">type</span><span class="sxs-lookup"><span data-stu-id="6656d-219">type</span></span> |<span data-ttu-id="6656d-220">Hello 열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-220">Data type of hello column.</span></span>  |<span data-ttu-id="6656d-221">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-221">No</span></span> |
| <span data-ttu-id="6656d-222">culture</span><span class="sxs-lookup"><span data-stu-id="6656d-222">culture</span></span> |<span data-ttu-id="6656d-223">. Hello 형식이.NET 유형 때 사용 되는.NET 기반 culture toobe: `Datetime` 또는 `Datetimeoffset`합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="6656d-224">hello 기본값은 `en-us`합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-224">hello default is `en-us`.</span></span> |<span data-ttu-id="6656d-225">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-225">No</span></span> |
| <span data-ttu-id="6656d-226">format</span><span class="sxs-lookup"><span data-stu-id="6656d-226">format</span></span> |<span data-ttu-id="6656d-227">문자열 toobe hello 형식이.NET 형식이 때 사용 되는 형식: `Datetime` 또는 `Datetimeoffset`합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="6656d-228">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-228">No</span></span> |

<span data-ttu-id="6656d-229">hello 다음과 같은 지침이 도움이 tooinclude 정보를 구성 하는 경우 및 hello에 어떤 tooinclude 결정 **구조** 섹션.</span><span class="sxs-lookup"><span data-stu-id="6656d-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="6656d-230">**구조화 된 데이터 원본에 대 한**, 원본 열 toosink 열 매핑와 이름이 동일 hello 하지는 경우에 hello 구조 섹션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="6656d-231">이러한 종류의 구조화 된 데이터 소스 자체 hello 데이터와 함께 데이터 스키마 및 형식 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="6656d-232">구조화된 데이터 원본의 예로 SQL Server, Oracle 및 Azure 테이블이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="6656d-233">형식 정보를 구조화 된 데이터 원본에 대해 사용할 수 있는 대로 hello 구조 섹션 포함 않는 경우 형식 정보가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="6656d-234">**읽은 데이터 원본 (특히 Blob storage)에 스키마에 대 한**, hello 데이터와 스키마 또는 형식 정보를 저장 하지 않고 toostore 데이터를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="6656d-235">이러한 유형의 데이터 원본에 대 한 toomap 원본 열 toosink 열을 사용할 때 구조를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="6656d-236">또한 구조 때 포함 hello 데이터 집합은 복사 작업에 대 한 입력 및 원본 데이터 집합의 데이터 형식이 hello 싱크에 대 한 변환된 toonative 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="6656d-237">데이터 팩터리의 지원 다음 구조에 대 한 형식 정보를 제공 하는 값에는 hello: **Int16, Int32, Int64, 단일, Double, Decimal, 바이트, 부울, 문자열, Guid, Datetime, Datetimeoffset 및 Timespan**합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="6656d-238">이러한 값은 CLS(공용 언어 사양) 규격 .NET 기반 type 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="6656d-239">데이터 팩터리 tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동할 때 자동으로 형식 변환을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="6656d-240">데이터 집합 가용성</span><span class="sxs-lookup"><span data-stu-id="6656d-240">Dataset availability</span></span>
<span data-ttu-id="6656d-241">hello **가용성** 데이터 집합의 섹션 hello 처리 창 (예를 들어 매시간, 매일 또는 매주) hello 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="6656d-242">활동 기간에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="6656d-243">hello 출력 데이터 집합 중 하나 생성 매시간 또는 hello 입력된 데이터 집합은 매 hello 가용성 섹션 뒤에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="6656d-244">Hello 파이프라인에는 시작 및 종료 시간을 다음 hello 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="6656d-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="6656d-245">hello 출력 데이터 집합 생성 시간별 hello 파이프라인 내에서 시작 및 종료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="6656d-246">따라서 이 파이프라인에서는 각 활동 기간(오전 12-1시, 오전 1-2시, 오전 2-3시, 오전 3-4시, 오전 4-5시)마다 하나씩 5개의 데이터 집합 조각이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="6656d-247">hello 다음 표에서 속성 hello 가용성 섹션에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="6656d-248">속성</span><span class="sxs-lookup"><span data-stu-id="6656d-248">Property</span></span> | <span data-ttu-id="6656d-249">설명</span><span class="sxs-lookup"><span data-stu-id="6656d-249">Description</span></span> | <span data-ttu-id="6656d-250">필수</span><span class="sxs-lookup"><span data-stu-id="6656d-250">Required</span></span> | <span data-ttu-id="6656d-251">기본값</span><span class="sxs-lookup"><span data-stu-id="6656d-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6656d-252">frequency</span><span class="sxs-lookup"><span data-stu-id="6656d-252">frequency</span></span> |<span data-ttu-id="6656d-253">데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="6656d-254"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="6656d-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="6656d-255">예</span><span class="sxs-lookup"><span data-stu-id="6656d-255">Yes</span></span> |<span data-ttu-id="6656d-256">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-256">NA</span></span> |
| <span data-ttu-id="6656d-257">interval</span><span class="sxs-lookup"><span data-stu-id="6656d-257">interval</span></span> |<span data-ttu-id="6656d-258">빈도에 대한 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="6656d-259">"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="6656d-260">예를 들어 조각화는 시간 단위로 데이터 집합 toobe hello 필요, 설정한 <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="6656d-261">지정 하는 경우 유의 **주파수** 으로 **분**, 15 보다 작은 간격 toono hello 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="6656d-262">예</span><span class="sxs-lookup"><span data-stu-id="6656d-262">Yes</span></span> |<span data-ttu-id="6656d-263">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-263">NA</span></span> |
| <span data-ttu-id="6656d-264">style</span><span class="sxs-lookup"><span data-stu-id="6656d-264">style</span></span> |<span data-ttu-id="6656d-265">Hello 시작 또는 끝 hello 간격의 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="6656d-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="6656d-266">StartOfInterval</span></span></li><li><span data-ttu-id="6656d-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6656d-267">EndOfInterval</span></span></li></ul><span data-ttu-id="6656d-268">경우 **주파수** 너무 설정**월**, 및 **스타일** 너무 설정**EndOfInterval**, hello hello 달의 마지막 날에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="6656d-269">경우 **스타일** 너무 설정**StartOfInterval**, 달의 첫 번째 날 hello에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="6656d-270">경우 **주파수** 너무 설정 되어**일**, 및 **스타일** 너무 설정 되어**EndOfInterval**, 지난 1 시간 동안 hello 하루의 hello에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="6656d-271">경우 **주파수** 너무 설정 되어**시간**, 및 **스타일** 너무 설정**EndOfInterval**, hello 조각이 hello 시간 hello 끝에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="6656d-272">예를 들어, hello 오후 1-2 시의 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="6656d-273">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-273">No</span></span> |<span data-ttu-id="6656d-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="6656d-274">EndOfInterval</span></span> |
| <span data-ttu-id="6656d-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="6656d-275">anchorDateTime</span></span> |<span data-ttu-id="6656d-276">Hello 스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="6656d-277">이 propoerty hello 빈도 지정 된 것 보다 더 세부적인 날짜 부분이 있으면 hello 보다 세부적인 파트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="6656d-278">예를 들어 경우 hello, **간격** 은 **매시간** (빈도: 시간 및 간격: 1), 및 hello **anchorDateTime** 포함 **, 분, 초**, 분 및 초 부분을 다음 hello **anchorDateTime** 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="6656d-279">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-279">No</span></span> |<span data-ttu-id="6656d-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="6656d-280">01/01/0001</span></span> |
| <span data-ttu-id="6656d-281">offset</span><span class="sxs-lookup"><span data-stu-id="6656d-281">offset</span></span> |<span data-ttu-id="6656d-282">어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="6656d-283">경우에 두 **anchorDateTime** 및 **오프셋** hello 결과 결합 된 hello shift 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="6656d-284">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-284">No</span></span> |<span data-ttu-id="6656d-285">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="6656d-286">offset example</span><span class="sxs-lookup"><span data-stu-id="6656d-286">offset example</span></span>
<span data-ttu-id="6656d-287">기본적으로 조각은 매일(`"frequency": "Day", "interval": 1`) 오전 12시(자정) UTC(협정 세계시)에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="6656d-288">대신 hello 시작 시간 toobe 오전 6 시 UTC 시간을 하려는 경우 hello hello 다음 코드 조각에에서 나와 있는 것 처럼 오프셋을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="6656d-289">anchorDateTime 예제</span><span class="sxs-lookup"><span data-stu-id="6656d-289">anchorDateTime example</span></span>
<span data-ttu-id="6656d-290">다음 예제는 hello, hello dataset 23 시간 마다 한 번 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="6656d-291">hello 첫 번째 조각의 시작 하 여 지정 된 hello 시 **anchorDateTime**, 너무 설정 된`2017-04-19T08:00:00` (UTC)입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="6656d-292">offset/style 예제</span><span class="sxs-lookup"><span data-stu-id="6656d-292">offset/style example</span></span>
<span data-ttu-id="6656d-293">hello 다음 데이터 집합은 월별, 오전 8시 매월 세 번째 서비스로 hello에 생성 되 고 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="6656d-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="6656d-294"><a name="Policy"></a>데이터 집합 정책</span><span class="sxs-lookup"><span data-stu-id="6656d-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="6656d-295">hello **정책** hello 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="6656d-296">정책 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="6656d-296">Validation policies</span></span>
| <span data-ttu-id="6656d-297">정책 이름</span><span class="sxs-lookup"><span data-stu-id="6656d-297">Policy name</span></span> | <span data-ttu-id="6656d-298">설명</span><span class="sxs-lookup"><span data-stu-id="6656d-298">Description</span></span> | <span data-ttu-id="6656d-299">너무 적용</span><span class="sxs-lookup"><span data-stu-id="6656d-299">Applied too</span></span>| <span data-ttu-id="6656d-300">필수</span><span class="sxs-lookup"><span data-stu-id="6656d-300">Required</span></span> | <span data-ttu-id="6656d-301">기본값</span><span class="sxs-lookup"><span data-stu-id="6656d-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="6656d-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="6656d-302">minimumSizeMB</span></span> |<span data-ttu-id="6656d-303">Hello 데이터에 유효성을 검사 **Azure Blob 저장소** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="6656d-304">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="6656d-304">Azure Blob storage</span></span> |<span data-ttu-id="6656d-305">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-305">No</span></span> |<span data-ttu-id="6656d-306">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-306">NA</span></span> |
| <span data-ttu-id="6656d-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="6656d-307">minimumRows</span></span> |<span data-ttu-id="6656d-308">Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="6656d-309">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="6656d-309">Azure SQL database</span></span></li><li><span data-ttu-id="6656d-310">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="6656d-310">Azure table</span></span></li></ul> |<span data-ttu-id="6656d-311">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-311">No</span></span> |<span data-ttu-id="6656d-312">해당 없음</span><span class="sxs-lookup"><span data-stu-id="6656d-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="6656d-313">예</span><span class="sxs-lookup"><span data-stu-id="6656d-313">Examples</span></span>
<span data-ttu-id="6656d-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="6656d-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="6656d-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="6656d-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="6656d-316">외부 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="6656d-316">External datasets</span></span>
<span data-ttu-id="6656d-317">외부 데이터 집합은 hello hello 데이터 팩터리에서 실행 중인 파이프라인에서 생성 하지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="6656d-318">Hello 데이터 집합으로 표시 되어 있으면 **외부**, hello **ExternalData** 정책 hello 데이터 집합 분할 영역 가용성의 정의 된 tooinfluence hello 동작을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="6656d-319">Data Factory에서 데이터 집합을 생성하지 않는 한 **external**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="6656d-320">이 설정은 활동 또는 파이프라인 체인 사용 되지 않은 경우 파이프라인의 첫 번째 활동의 toohello 입력 일반적으로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="6656d-321">이름</span><span class="sxs-lookup"><span data-stu-id="6656d-321">Name</span></span> | <span data-ttu-id="6656d-322">설명</span><span class="sxs-lookup"><span data-stu-id="6656d-322">Description</span></span> | <span data-ttu-id="6656d-323">필수</span><span class="sxs-lookup"><span data-stu-id="6656d-323">Required</span></span> | <span data-ttu-id="6656d-324">기본값</span><span class="sxs-lookup"><span data-stu-id="6656d-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6656d-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="6656d-325">dataDelay</span></span> |<span data-ttu-id="6656d-326">hello toodelay hello hello hello에 대 한 외부 데이터의 hello 가용성 확인 시간은 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="6656d-327">예를 들어 이 설정을 사용하여 시간별 검사를 지연할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="6656d-328">hello 설정의 현재 시간 toohello를만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="6656d-329">예를 들어 지금 바로 오후 1시 이므로이 값은 10 분 hello 유효성 검사 오후 1 시 10 분에 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="6656d-330">참고가이 설정은 지난 hello에서 분할 영역에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="6656d-331">**조각 종료 시간** + **dataDelay** < **현재 시간**인 경우 조각은 지연 없이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="6656d-332">23시 59분 보다 큰 시간 hello를 사용 하 여 시간을 지정할 `day.hours:minutes:seconds` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="6656d-333">예를 들어, toospecify 24 시간, 24시: 00을 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="6656d-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="6656d-334">1.00:00:00을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="6656d-335">24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="6656d-336">1일 4시간의 경우 1:04:00:00을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="6656d-337">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-337">No</span></span> |<span data-ttu-id="6656d-338">0</span><span class="sxs-lookup"><span data-stu-id="6656d-338">0</span></span> |
| <span data-ttu-id="6656d-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="6656d-339">retryInterval</span></span> |<span data-ttu-id="6656d-340">hello 실패 및 hello 다음 시도 사이의 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="6656d-341">이 설정은 toopresent 시간이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-341">This setting applies toopresent time.</span></span> <span data-ttu-id="6656d-342">Hello 후 hello 다음 시도 hello 이전 시도 실패 한 경우 **retryInterval** 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="6656d-343">지금 바로 오후 1시 이면 hello 첫 번째 시도 시작 하기.</span><span class="sxs-lookup"><span data-stu-id="6656d-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="6656d-344">Hello 기간 toocomplete hello 첫 번째 유효성 검사 1 분 이며 hello 작업이 실패 했습니다 hello 다음 재시도에 않은 경우에 1시 + 1 분 (기간) + 1 분 (다시 시도 간격) = 오후 1시 02분 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="6656d-345">지난 hello에 조각에 대 한 지연 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="6656d-346">hello 재시도 즉시 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-346">hello retry happens immediately.</span></span> |<span data-ttu-id="6656d-347">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-347">No</span></span> |<span data-ttu-id="6656d-348">00:01:00 (1분)</span><span class="sxs-lookup"><span data-stu-id="6656d-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="6656d-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="6656d-349">retryTimeout</span></span> |<span data-ttu-id="6656d-350">각 다시 시도 대 한 hello 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="6656d-351">이 속성을 설정 하는 경우 too10 분, 10 분 이내에 hello 유효성 검사를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="6656d-352">10 분 tooperform hello 유효성 검사 보다 시간이 오래 걸리는 경우 제한 시간이 초과 hello에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="6656d-353">Hello 유효성 검사 시간 초과 대 한 모든 시도 hello 조각으로 표시 됩니다 **TimedOut**합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="6656d-354">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-354">No</span></span> |<span data-ttu-id="6656d-355">00:10:00 (10분)</span><span class="sxs-lookup"><span data-stu-id="6656d-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="6656d-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="6656d-356">maximumRetry</span></span> |<span data-ttu-id="6656d-357">hello 횟수 toocheck hello 외부 데이터의 가용성을 hello에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="6656d-358">hello 최대 허용 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="6656d-359">아니요</span><span class="sxs-lookup"><span data-stu-id="6656d-359">No</span></span> |<span data-ttu-id="6656d-360">3</span><span class="sxs-lookup"><span data-stu-id="6656d-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="6656d-361">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="6656d-361">Create datasets</span></span>
<span data-ttu-id="6656d-362">다음 도구 또는 SDK 중 하나를 사용하여 데이터 집합을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="6656d-363">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="6656d-363">Copy Wizard</span></span> 
- <span data-ttu-id="6656d-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6656d-364">Azure portal</span></span>
- <span data-ttu-id="6656d-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6656d-365">Visual Studio</span></span>
- <span data-ttu-id="6656d-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6656d-366">PowerShell</span></span>
- <span data-ttu-id="6656d-367">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="6656d-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="6656d-368">REST API</span><span class="sxs-lookup"><span data-stu-id="6656d-368">REST API</span></span>
- <span data-ttu-id="6656d-369">.NET API</span><span class="sxs-lookup"><span data-stu-id="6656d-369">.NET API</span></span>

<span data-ttu-id="6656d-370">이러한 도구나 Sdk 중 하나를 사용 하 여 파이프라인 및 데이터 집합을 만들기 위한 단계별 지침에 대 한 자습서를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6656d-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="6656d-371">데이터 변환 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="6656d-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="6656d-372">데이터 이동 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="6656d-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="6656d-373">파이프라인을 만들고 배포한 후에 관리 및 모니터링할 수 있습니다를 사용 하 여 파이프라인 hello Azure 포털 블레이드 또는 hello 모니터링 및 관리 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="6656d-374">Hello 다음 단계별 지침에 대 한 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6656d-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="6656d-375">Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="6656d-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="6656d-376">모니터링 하 고 hello 모니터링 및 관리 응용 프로그램을 사용 하 여 파이프라인 관리</span><span class="sxs-lookup"><span data-stu-id="6656d-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="6656d-377">범위가 지정된 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="6656d-377">Scoped datasets</span></span>
<span data-ttu-id="6656d-378">Hello를 사용 하 여 범위 지정 된 tooa 파이프라인 된 데이터 집합을 만들 수 있습니다 **데이터 집합** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="6656d-379">이러한 데이터 집합은 다른 파이프라인의 활동이 아니라 이 파이프라인 내의 활동에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="6656d-380">다음 예제는 hello와 두 개의 데이터 집합 (InputDataset rdc 및 OutputDataset rdc) toobe hello 파이프라인 내에서 사용 되는 파이프라인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6656d-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6656d-381">범위가 지정 된 데이터 집합 일회성 파이프라인만 지원 됩니다 (여기서 **pipelineMode** 너무 설정**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="6656d-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="6656d-382">자세한 내용은 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="6656d-383">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6656d-383">Next steps</span></span>
- <span data-ttu-id="6656d-384">파이프라인에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="6656d-385">파이프라인을 예약하고 실행하는 방법에 대한 자세한 내용은 [Azure Data Factory 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6656d-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
