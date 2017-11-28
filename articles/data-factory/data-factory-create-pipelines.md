---
title: "aaaCreate/일정 파이프라인, Data Factory에 체인 활동 | Microsoft Docs"
description: "데이터 파이프라인에서 Azure Data Factory toomove toocreate 알아보고 데이터를 변환 합니다. 데이터 기반 워크플로 tooproduce 준비 toouse 정보를 만듭니다."
keywords: "데이터 파이프라인, 데이터 기반 워크플로"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 13b137c7-1033-406f-aea7-b66f25b313c0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: shlo
ms.openlocfilehash: 4a0fc20f98ce6453c16955e97fddb891926c173a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="pipelines-and-activities-in-azure-data-factory"></a><span data-ttu-id="945f1-105">Azure 데이터 팩터리의 파이프라인 및 활동</span><span class="sxs-lookup"><span data-stu-id="945f1-105">Pipelines and Activities in Azure Data Factory</span></span>
<span data-ttu-id="945f1-106">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하 고 데이터 이동 및 데이터 처리 시나리오에 대 한 tooconstruct 종단 간 데이터 기반 워크플로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-106">This article helps you understand pipelines and activities in Azure Data Factory and use them tooconstruct end-to-end data-driven workflows for your data movement and data processing scenarios.</span></span>  

> [!NOTE]
> <span data-ttu-id="945f1-107">이 문서에서는 통해 수행한 가정 [소개 tooAzure Data Factory](data-factory-introduction.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-107">This article assumes that you have gone through [Introduction tooAzure Data Factory](data-factory-introduction.md).</span></span> <span data-ttu-id="945f1-108">데이터 팩터리를 만드는 실습 경험이 없는 경우 [데이터 변환 자습서](data-factory-build-your-first-pipeline.md) 및/또는 [데이터 이동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 진행하면 이 문서를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-108">If you do not have hands-on-experience with creating data factories, going through [data transformation tutorial](data-factory-build-your-first-pipeline.md) and/or [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) would help you understand this article better.</span></span>  

## <a name="overview"></a><span data-ttu-id="945f1-109">개요</span><span class="sxs-lookup"><span data-stu-id="945f1-109">Overview</span></span>
<span data-ttu-id="945f1-110">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-110">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="945f1-111">파이프라인은 함께 작업을 수행하는 활동의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-111">A pipeline is a logical grouping of activities that together perform a task.</span></span> <span data-ttu-id="945f1-112">파이프라인의 hello 활동 데이터에 대해 작업 tooperform를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-112">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="945f1-113">예를 들어 온-프레미스 SQL Server tooan Azure Blob 저장소에서에서 복사 작업 toocopy 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-113">For example, you may use a copy activity toocopy data from an on-premises SQL Server tooan Azure Blob Storage.</span></span> <span data-ttu-id="945f1-114">그런 다음 hello blob 저장소 tooproduce 출력 데이터에서 Azure HDInsight 클러스터 tooprocess/변환 데이터에서 하이브 스크립트를 실행 하는 하이브 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-114">Then, use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess/transform data from hello blob storage tooproduce output data.</span></span> <span data-ttu-id="945f1-115">마지막으로, 두 번째 복사본 활동 toocopy hello 출력 데이터 tooan Azure SQL 데이터 웨어하우스는 비즈니스 인텔리전스 (BI)를 기반으로 작성 된 보고 솔루션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-115">Finally, use a second copy activity toocopy hello output data tooan Azure SQL Data Warehouse on top of which business intelligence (BI) reporting solutions are built.</span></span> 

<span data-ttu-id="945f1-116">활동은 0개 이상의 입력 [데이터 집합](data-factory-create-datasets.md)을 받고 하나 이상의 출력 [데이터 집합](data-factory-create-datasets.md)을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-116">An activity can take zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output [datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="945f1-117">hello 다음 보여 주는 다이어그램 파이프라인, 작업 및 데이터 집합 간의 hello 관계 Data Factory에:</span><span class="sxs-lookup"><span data-stu-id="945f1-117">hello following diagram shows hello relationship between pipeline, activity, and dataset in Data Factory:</span></span> 

![파이프라인, 활동, 데이터 집합 간 관계](media/data-factory-create-pipelines/relationship-pipeline-activity-dataset.png)

<span data-ttu-id="945f1-119">파이프라인이 있습니다 toomanage 활동을 각 하는 대신 집합으로 개별적으로.</span><span class="sxs-lookup"><span data-stu-id="945f1-119">A pipeline allows you toomanage activities as a set instead of each one individually.</span></span> <span data-ttu-id="945f1-120">예를 들어, 배포 하 고 예약 하 고 일시 중단, 수 있으며 독립적으로 hello 파이프라인에서 작업 하지 처리 하는 대신 파이프라인 다시 시작 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-120">For example, you can deploy, schedule, suspend, and resume a pipeline, instead of dealing with activities in hello pipeline independently.</span></span>

<span data-ttu-id="945f1-121">Data Factory는 데이터 이동 활동 및 데이터 변환 활동이라는 두 종류의 활동을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-121">Data Factory supports two types of activities: data movement activities and data transformation activities.</span></span> <span data-ttu-id="945f1-122">각 활동은 0개 이상의 입력 [데이터 집합](data-factory-create-datasets.md)을 갖고 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-122">Each activity can have zero or more input [datasets](data-factory-create-datasets.md) and produce one or more output datasets.</span></span>

<span data-ttu-id="945f1-123">입력된 데이터 집합 hello 파이프라인의 활동에 대 한 hello 입력을 나타내고 출력 데이터 집합 hello 활동에 대 한 hello 출력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-123">An input dataset represents hello input for an activity in hello pipeline and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="945f1-124">데이터 집합은 테이블, 파일, 폴더, 문서를 비롯한 다양한 데이터 저장소 내의 데이터를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-124">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="945f1-125">데이터 집합을 만든 후 파이프라인의 작업에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-125">After you create a dataset, you can use it with activities in a pipeline.</span></span> <span data-ttu-id="945f1-126">예를 들어 데이터 집합은 복사 작업 또는 HDInsightHive 작업의 입력/출력 데이터 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-126">For example, a dataset can be an input/output dataset of a Copy Activity or an HDInsightHive Activity.</span></span> <span data-ttu-id="945f1-127">데이터 집합에 대한 자세한 내용은 [Azure Data Factory의 데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-127">For more information about datasets, see [Datasets in Azure Data Factory](data-factory-create-datasets.md) article.</span></span>

### <a name="data-movement-activities"></a><span data-ttu-id="945f1-128">데이터 이동 활동</span><span class="sxs-lookup"><span data-stu-id="945f1-128">Data movement activities</span></span>
<span data-ttu-id="945f1-129">복사 활동 Data Factory에는 원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-129">Copy Activity in Data Factory copies data from a source data store tooa sink data store.</span></span> <span data-ttu-id="945f1-130">데이터 팩터리 hello 다음 데이터 저장소를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-130">Data Factory supports hello following data stores.</span></span> <span data-ttu-id="945f1-131">데이터 소스에서 tooany 싱크를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-131">Data from any source can be written tooany sink.</span></span> <span data-ttu-id="945f1-132">데이터 저장소 toolearn 방법을 클릭 해당 저장소에서 데이터 tooand toocopy 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-132">Click a data store toolearn how toocopy data tooand from that store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="945f1-133">데이터 저장소와 * 온-프레미스 될 수 있습니다 또는 Azure IaaS에서 고 tooinstall 있어야 하며 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 에-프레미스/Azure IaaS 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-133">Data stores with * can be on-premises or on Azure IaaS, and require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises/Azure IaaS machine.</span></span>

<span data-ttu-id="945f1-134">자세한 내용은 [데이터 이동 활동](data-factory-data-movement-activities.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-134">For more information, see [Data Movement Activities](data-factory-data-movement-activities.md) article.</span></span>

### <a name="data-transformation-activities"></a><span data-ttu-id="945f1-135">데이터 변환 활동</span><span class="sxs-lookup"><span data-stu-id="945f1-135">Data transformation activities</span></span>
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

<span data-ttu-id="945f1-136">자세한 내용은 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-136">For more information, see [Data Transformation Activities](data-factory-data-transformation-activities.md) article.</span></span>

### <a name="custom-net-activities"></a><span data-ttu-id="945f1-137">사용자 지정 .NET 활동</span><span class="sxs-lookup"><span data-stu-id="945f1-137">Custom .NET activities</span></span> 
<span data-ttu-id="945f1-138">데이터에서 복사 작업 hello 저장소 하지 않는 지원, 또는 변환 하는 고유한 논리를 사용 하 여 데이터 만들기/toomove 데이터를 유지 해야 하는 경우는 **사용자 지정.NET 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-138">If you need toomove data to/from a data store that hello Copy Activity doesn't support, or transform data using your own logic, create a **custom .NET activity**.</span></span> <span data-ttu-id="945f1-139">사용자 지정 활동을 만들고 사용하는 방법에 대한 자세한 내용은 [Azure Data Factory 파이프라인에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-139">For details on creating and using a custom activity, see [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md).</span></span>

## <a name="schedule-pipelines"></a><span data-ttu-id="945f1-140">파이프라인 예약</span><span class="sxs-lookup"><span data-stu-id="945f1-140">Schedule pipelines</span></span>
<span data-ttu-id="945f1-141">파이프라인은 **시작** 시간과 **종료** 시간 사이에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-141">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="945f1-142">Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-142">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="945f1-143">Hello 파이프라인의 일시 중지 되 면이 실행 되지 않도록 해당 시작 및 종료 시간에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-143">If hello pipeline is paused, it does not get executed irrespective of its start and end time.</span></span> <span data-ttu-id="945f1-144">파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-144">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="945f1-145">참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) toounderstand Azure Data Factory에서 예약 및 실행의 작동 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-145">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) toounderstand how scheduling and execution works in Azure Data Factory.</span></span>

## <a name="pipeline-json"></a><span data-ttu-id="945f1-146">파이프라인 JSON</span><span class="sxs-lookup"><span data-stu-id="945f1-146">Pipeline JSON</span></span>
<span data-ttu-id="945f1-147">JSON 형식으로 파이프라인을 정의하는 방법에 대해 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-147">Let us take a closer look on how a pipeline is defined in JSON format.</span></span> <span data-ttu-id="945f1-148">파이프라인에 대 한 일반 구조 hello 모양은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-148">hello generic structure for a pipeline looks as follows:</span></span>

```json
{
    "name": "PipelineName",
    "properties": 
    {
        "description" : "pipeline description",
        "activities":
        [

        ],
        "start": "<start date-time>",
        "end": "<end date-time>",
        "isPaused": true/false,
        "pipelineMode": "scheduled/onetime",
        "expirationTime": "15.00:00:00",
        "datasets": 
        [
        ]
    }
}
```

| <span data-ttu-id="945f1-149">태그</span><span class="sxs-lookup"><span data-stu-id="945f1-149">Tag</span></span> | <span data-ttu-id="945f1-150">설명</span><span class="sxs-lookup"><span data-stu-id="945f1-150">Description</span></span> | <span data-ttu-id="945f1-151">필수</span><span class="sxs-lookup"><span data-stu-id="945f1-151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="945f1-152">name</span><span class="sxs-lookup"><span data-stu-id="945f1-152">name</span></span> |<span data-ttu-id="945f1-153">Hello 파이프라인의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-153">Name of hello pipeline.</span></span> <span data-ttu-id="945f1-154">수행 하는 파이프라인 hello hello 동작을 나타내는 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-154">Specify a name that represents hello action that hello pipeline performs.</span></span> <br/><ul><li><span data-ttu-id="945f1-155">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="945f1-155">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="945f1-156">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-156">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="945f1-157">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="945f1-157">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="945f1-158">예</span><span class="sxs-lookup"><span data-stu-id="945f1-158">Yes</span></span> |
| <span data-ttu-id="945f1-159">설명</span><span class="sxs-lookup"><span data-stu-id="945f1-159">description</span></span> | <span data-ttu-id="945f1-160">에 대 한 어떤 hello 파이프라인을 사용 하는 설명 하는 hello 텍스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-160">Specify hello text describing what hello pipeline is used for.</span></span> |<span data-ttu-id="945f1-161">예</span><span class="sxs-lookup"><span data-stu-id="945f1-161">Yes</span></span> |
| <span data-ttu-id="945f1-162">작업</span><span class="sxs-lookup"><span data-stu-id="945f1-162">activities</span></span> | <span data-ttu-id="945f1-163">hello **활동** 섹션 내에 정의 된 하나 이상의 활동을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-163">hello **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="945f1-164">Hello hello 활동 JSON 요소에 대 한 자세한 내용은 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="945f1-164">See hello next section for details about hello activities JSON element.</span></span> | <span data-ttu-id="945f1-165">예</span><span class="sxs-lookup"><span data-stu-id="945f1-165">Yes</span></span> |  
| <span data-ttu-id="945f1-166">start</span><span class="sxs-lookup"><span data-stu-id="945f1-166">start</span></span> | <span data-ttu-id="945f1-167">시작 날짜 / 시간 hello 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-167">Start date-time for hello pipeline.</span></span> <span data-ttu-id="945f1-168">[ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-168">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="945f1-169">예: `2016-10-14T16:32:41Z`</span><span class="sxs-lookup"><span data-stu-id="945f1-169">For example: `2016-10-14T16:32:41Z`.</span></span> <br/><br/><span data-ttu-id="945f1-170">이제는 현지 시간을 가능한 toospecify 예는 EST입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-170">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="945f1-171">예제: `2016-02-27T06:00:00-05:00`”(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="945f1-171">Here is an example: `2016-02-27T06:00:00-05:00`", which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="945f1-172">hello 시작 및 끝 속성 함께 지정 hello 파이프라인에 대 한 활성 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-172">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="945f1-173">출력 조각은 이 활성 기간에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-173">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="945f1-174">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-174">No</span></span><br/><br/><span data-ttu-id="945f1-175">Hello end 속성에 대 한 값을 지정 하는 경우 hello 시작 속성에 대 한 값을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-175">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="945f1-176">hello 시작 및 종료 시간 둘 다 수 빈 toocreate 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="945f1-176">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="945f1-177">값을 모두 지정 해야 합니다는 파이프라인 toorun hello에 대 한 활성 기간 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-177">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="945f1-178">시작 및 종료 시간을 지정 하지 않을 경우 파이프라인을 만들 때 설정할 수 있습니다 hello 집합 AzureRmDataFactoryPipelineActivePeriod cmdlet를 사용 하 여 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-178">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="945f1-179">end</span><span class="sxs-lookup"><span data-stu-id="945f1-179">end</span></span> | <span data-ttu-id="945f1-180">Hello 파이프라인에 대 한 날짜 및 시간을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-180">End date-time for hello pipeline.</span></span> <span data-ttu-id="945f1-181">지정된 경우 ISO 형식에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-181">If specified must be in ISO format.</span></span> <span data-ttu-id="945f1-182">예: `2016-10-14T17:32:41Z`</span><span class="sxs-lookup"><span data-stu-id="945f1-182">For example: `2016-10-14T17:32:41Z`</span></span> <br/><br/><span data-ttu-id="945f1-183">이제는 현지 시간을 가능한 toospecify 예는 EST입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-183">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="945f1-184">예: `2016-02-27T06:00:00-05:00`(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="945f1-184">Here is an example: `2016-02-27T06:00:00-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="945f1-185">toorun hello 파이프라인 hello hello 최종 속성 값으로 9999-09-09를 무제한으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-185">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> <br/><br/> <span data-ttu-id="945f1-186">파이프라인은 시작 시간과 종료 시간 사이에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-186">A pipeline is active only between its start time and end time.</span></span> <span data-ttu-id="945f1-187">Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-187">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="945f1-188">Hello 파이프라인의 일시 중지 되 면이 실행 되지 않도록 해당 시작 및 종료 시간에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-188">If hello pipeline is paused, it does not get executed irrespective of its start and end time.</span></span> <span data-ttu-id="945f1-189">파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-189">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="945f1-190">참조 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) toounderstand Azure Data Factory에서 예약 및 실행의 작동 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-190">See [Scheduling and Execution](data-factory-scheduling-and-execution.md) toounderstand how scheduling and execution works in Azure Data Factory.</span></span> |<span data-ttu-id="945f1-191">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-191">No</span></span> <br/><br/><span data-ttu-id="945f1-192">Hello 시작 속성에 대 한 값을 지정 하는 경우 hello end 속성에 대 한 값을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-192">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="945f1-193">Hello에 대 한 메모를 참조 하세요 **시작** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-193">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="945f1-194">isPaused</span><span class="sxs-lookup"><span data-stu-id="945f1-194">isPaused</span></span> | <span data-ttu-id="945f1-195">집합 tootrue, hello 파이프라인 실행 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-195">If set tootrue, hello pipeline does not run.</span></span> <span data-ttu-id="945f1-196">에 hello에 일시 중지 된 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-196">It's in hello paused state.</span></span> <span data-ttu-id="945f1-197">기본값 = false입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-197">Default value = false.</span></span> <span data-ttu-id="945f1-198">이 속성 tooenable를 사용 하거나 파이프라인을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-198">You can use this property tooenable or disable a pipeline.</span></span> |<span data-ttu-id="945f1-199">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-199">No</span></span> |
| <span data-ttu-id="945f1-200">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="945f1-200">pipelineMode</span></span> | <span data-ttu-id="945f1-201">hello 메서드 hello 파이프라인에 대 한 실행을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-201">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="945f1-202">허용되는 값은 scheduled(기본), onetime입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-202">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="945f1-203">'예약' hello 파이프라인 tooits 활성 기간 (시작 및 종료 시간)에 따라 지정 된 시간 간격으로 실행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-203">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="945f1-204">'Onetime' hello 파이프라인 실행 한 번만 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-204">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="945f1-205">현재는, Onetime 파이프라인이 생성된 후에 수정/업데이트가 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-205">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="945f1-206">일회성 설정에 대한 세부 정보는 [일회성 파이프라인](#onetime-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-206">See [Onetime pipeline](#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="945f1-207">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-207">No</span></span> |
| <span data-ttu-id="945f1-208">expirationTime</span><span class="sxs-lookup"><span data-stu-id="945f1-208">expirationTime</span></span> | <span data-ttu-id="945f1-209">어떤 hello에 대 한 시간을 만든 후 [일회성 파이프라인](#onetime-pipeline) 유효 하 고 프로 비전 된 상태로 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-209">Duration of time after creation for which hello [one-time pipeline](#onetime-pipeline) is valid and should remain provisioned.</span></span> <span data-ttu-id="945f1-210">경우 없는 모든 활성 실패, 또는 실행을 보류 중인 hello 파이프라인은 자동으로 삭제 한 번에 도달 hello 만료 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-210">If it does not have any active, failed, or pending runs, hello pipeline is automatically deleted once it reaches hello expiration time.</span></span> <span data-ttu-id="945f1-211">기본값 hello:`"expirationTime": "3.00:00:00"`</span><span class="sxs-lookup"><span data-stu-id="945f1-211">hello default value: `"expirationTime": "3.00:00:00"`</span></span>|<span data-ttu-id="945f1-212">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-212">No</span></span> |
| <span data-ttu-id="945f1-213">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="945f1-213">datasets</span></span> |<span data-ttu-id="945f1-214">Hello 파이프라인에 정의 된 활동에서 사용 하는 데이터 집합 toobe의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-214">List of datasets toobe used by activities defined in hello pipeline.</span></span> <span data-ttu-id="945f1-215">이 속성을 특정 toothis 파이프라인 이며 hello 데이터 팩터리 내에 정의 된 있는 toodefine 사용 되는 데이터 집합 수입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-215">This property can be used toodefine datasets that are specific toothis pipeline and not defined within hello data factory.</span></span> <span data-ttu-id="945f1-216">이 파이프라인 내에 정의된 데이터 집합은 이 파이프라인에서만 사용될 수 있고 공유될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-216">Datasets defined within this pipeline can only be used by this pipeline and cannot be shared.</span></span> <span data-ttu-id="945f1-217">자세한 내용은 [범위가 지정된 데이터 집합](data-factory-create-datasets.md#scoped-datasets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-217">See [Scoped datasets](data-factory-create-datasets.md#scoped-datasets) for details.</span></span> |<span data-ttu-id="945f1-218">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-218">No</span></span> |

## <a name="activity-json"></a><span data-ttu-id="945f1-219">활동 JSON</span><span class="sxs-lookup"><span data-stu-id="945f1-219">Activity JSON</span></span>
<span data-ttu-id="945f1-220">hello **활동** 섹션 내에 정의 된 하나 이상의 활동을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-220">hello **activities** section can have one or more activities defined within it.</span></span> <span data-ttu-id="945f1-221">각 활동에는 다음 최상위 구조 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-221">Each activity has hello following top-level structure:</span></span>

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    },
    "scheduler":
    {
    }
}
```

<span data-ttu-id="945f1-222">다음 표에서 hello 활동 JSON 정의에서 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-222">Following table describes properties in hello activity JSON definition:</span></span>

| <span data-ttu-id="945f1-223">태그</span><span class="sxs-lookup"><span data-stu-id="945f1-223">Tag</span></span> | <span data-ttu-id="945f1-224">설명</span><span class="sxs-lookup"><span data-stu-id="945f1-224">Description</span></span> | <span data-ttu-id="945f1-225">필수</span><span class="sxs-lookup"><span data-stu-id="945f1-225">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="945f1-226">name</span><span class="sxs-lookup"><span data-stu-id="945f1-226">name</span></span> | <span data-ttu-id="945f1-227">Hello 활동의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-227">Name of hello activity.</span></span> <span data-ttu-id="945f1-228">Hello 활동을 수행 하는 hello 동작을 나타내는 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-228">Specify a name that represents hello action that hello activity performs.</span></span> <br/><ul><li><span data-ttu-id="945f1-229">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="945f1-229">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="945f1-230">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-230">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="945f1-231">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="945f1-231">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="945f1-232">예</span><span class="sxs-lookup"><span data-stu-id="945f1-232">Yes</span></span> |
| <span data-ttu-id="945f1-233">설명</span><span class="sxs-lookup"><span data-stu-id="945f1-233">description</span></span> | <span data-ttu-id="945f1-234">설명 하는 어떤 hello 활동에 사용 되는 텍스트</span><span class="sxs-lookup"><span data-stu-id="945f1-234">Text describing what hello activity or is used for</span></span> |<span data-ttu-id="945f1-235">예</span><span class="sxs-lookup"><span data-stu-id="945f1-235">Yes</span></span> |
| <span data-ttu-id="945f1-236">type</span><span class="sxs-lookup"><span data-stu-id="945f1-236">type</span></span> | <span data-ttu-id="945f1-237">Hello 활동의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-237">Type of hello activity.</span></span> <span data-ttu-id="945f1-238">Hello 참조 [데이터 이동 작업](#data-movement-activities) 및 [데이터 변환 작업](#data-transformation-activities) 다양 한 유형의 활동에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="945f1-238">See hello [Data Movement Activities](#data-movement-activities) and [Data Transformation Activities](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="945f1-239">예</span><span class="sxs-lookup"><span data-stu-id="945f1-239">Yes</span></span> |
| <span data-ttu-id="945f1-240">inputs</span><span class="sxs-lookup"><span data-stu-id="945f1-240">inputs</span></span> |<span data-ttu-id="945f1-241">Hello 활동에서 사용 하는 입력된 테이블</span><span class="sxs-lookup"><span data-stu-id="945f1-241">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="945f1-242">예</span><span class="sxs-lookup"><span data-stu-id="945f1-242">Yes</span></span> |
| <span data-ttu-id="945f1-243">outputs</span><span class="sxs-lookup"><span data-stu-id="945f1-243">outputs</span></span> |<span data-ttu-id="945f1-244">Hello 활동에 의해 사용 되는 출력된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-244">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": "outputtable1" } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": "outputtable1" }, { "name": "outputtable2" }  ],` |<span data-ttu-id="945f1-245">예</span><span class="sxs-lookup"><span data-stu-id="945f1-245">Yes</span></span> |
| <span data-ttu-id="945f1-246">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="945f1-246">linkedServiceName</span></span> |<span data-ttu-id="945f1-247">Hello 활동에서 사용 하는 hello 연결 된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-247">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="945f1-248">활동은 toohello 필요한 계산 환경에 연결 하는 hello 연결 된 서비스를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-248">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="945f1-249">HDInsight 작업 및 Azure 기계 학습 배치 평가 작업의 경우 예 </span><span class="sxs-lookup"><span data-stu-id="945f1-249">Yes for HDInsight Activity and Azure Machine Learning Batch Scoring Activity</span></span> <br/><br/><span data-ttu-id="945f1-250">다른 모든 사용자의 경우 아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-250">No for all others</span></span> |
| <span data-ttu-id="945f1-251">typeProperties</span><span class="sxs-lookup"><span data-stu-id="945f1-251">typeProperties</span></span> |<span data-ttu-id="945f1-252">Hello에 대 한 속성 **typeProperties** 섹션 hello 활동의 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-252">Properties in hello **typeProperties** section depend on type of hello activity.</span></span> <span data-ttu-id="945f1-253">활동에 대해 toosee 형식 속성 hello 이전 단원의 toohello 작업 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-253">toosee type properties for an activity, click links toohello activity in hello previous section.</span></span> | <span data-ttu-id="945f1-254">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-254">No</span></span> |
| <span data-ttu-id="945f1-255">policy</span><span class="sxs-lookup"><span data-stu-id="945f1-255">policy</span></span> |<span data-ttu-id="945f1-256">Hello 활동의 hello 런타임 동작에 영향을 주는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-256">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="945f1-257">지정하지 않으면 기본 정책이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-257">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="945f1-258">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-258">No</span></span> |
| <span data-ttu-id="945f1-259">scheduler</span><span class="sxs-lookup"><span data-stu-id="945f1-259">scheduler</span></span> | <span data-ttu-id="945f1-260">"스케줄러" 속성은 사용 되는 toodefine을 원하는 hello 활동에 대 한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-260">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="945f1-261">해당 속성의 하위 hello hello에서와 동일 hello는 [데이터 집합의 가용성 속성](data-factory-create-datasets.md#dataset-availability)합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-261">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="945f1-262">아니요</span><span class="sxs-lookup"><span data-stu-id="945f1-262">No</span></span> |


### <a name="policies"></a><span data-ttu-id="945f1-263">정책</span><span class="sxs-lookup"><span data-stu-id="945f1-263">Policies</span></span>
<span data-ttu-id="945f1-264">정책은은 hello 테이블 조각이 처리 시에 특히는 활동의 런타임 동작을 hello는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-264">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="945f1-265">다음 표에서 hello hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-265">hello following table provides hello details.</span></span>

| <span data-ttu-id="945f1-266">속성</span><span class="sxs-lookup"><span data-stu-id="945f1-266">Property</span></span> | <span data-ttu-id="945f1-267">허용된 값</span><span class="sxs-lookup"><span data-stu-id="945f1-267">Permitted values</span></span> | <span data-ttu-id="945f1-268">기본값</span><span class="sxs-lookup"><span data-stu-id="945f1-268">Default Value</span></span> | <span data-ttu-id="945f1-269">설명</span><span class="sxs-lookup"><span data-stu-id="945f1-269">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="945f1-270">동시성</span><span class="sxs-lookup"><span data-stu-id="945f1-270">concurrency</span></span> |<span data-ttu-id="945f1-271">정수 </span><span class="sxs-lookup"><span data-stu-id="945f1-271">Integer</span></span> <br/><br/><span data-ttu-id="945f1-272">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="945f1-272">Max value: 10</span></span> |<span data-ttu-id="945f1-273">1</span><span class="sxs-lookup"><span data-stu-id="945f1-273">1</span></span> |<span data-ttu-id="945f1-274">Hello 활동의 동시 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-274">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="945f1-275">Hello 여러 조각에서 발생할 수 있는 병렬 활동 실행 횟수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-275">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="945f1-276">예를 들어 활동을 통해 toogo 해야 하는 경우 다양 한 사용 가능한 데이터에 더 큰 동시성 가치가 속도가 향상 hello 데이터 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-276">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="945f1-277">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="945f1-277">executionPriorityOrder</span></span> |<span data-ttu-id="945f1-278">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="945f1-278">NewestFirst</span></span><br/><br/><span data-ttu-id="945f1-279">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="945f1-279">OldestFirst</span></span> |<span data-ttu-id="945f1-280">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="945f1-280">OldestFirst</span></span> |<span data-ttu-id="945f1-281">Hello 데이터 조각이 처리 중인의 순서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-281">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="945f1-282">예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-282">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="945f1-283">Hello executionPriorityOrder toobe NewestFirst로 설정 하면 오후 5 시의 hello 조각이 먼저 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-283">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="945f1-284">마찬가지로 executionPriorityORder toobe hello OldestFIrst로 설정 하면 오후 4 시의 hello 조각이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-284">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="945f1-285">retry</span><span class="sxs-lookup"><span data-stu-id="945f1-285">retry</span></span> |<span data-ttu-id="945f1-286">정수 </span><span class="sxs-lookup"><span data-stu-id="945f1-286">Integer</span></span><br/><br/><span data-ttu-id="945f1-287">최대값이 10이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="945f1-287">Max value can be 10</span></span> |<span data-ttu-id="945f1-288">0</span><span class="sxs-lookup"><span data-stu-id="945f1-288">0</span></span> |<span data-ttu-id="945f1-289">Hello 조각에 대 한 hello 데이터 처리 전 까지의 재시도 횟수 Failure로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-289">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="945f1-290">지정 된 toohello를 데이터 조각에 대 한 활동 실행을 다시 시도 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-290">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="945f1-291">hello 재시도 hello 실패 후 가능한 한 빨리 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-291">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="945f1-292">시간 제한</span><span class="sxs-lookup"><span data-stu-id="945f1-292">timeout</span></span> |<span data-ttu-id="945f1-293">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="945f1-293">TimeSpan</span></span> |<span data-ttu-id="945f1-294">00:00:00</span><span class="sxs-lookup"><span data-stu-id="945f1-294">00:00:00</span></span> |<span data-ttu-id="945f1-295">Hello 활동에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-295">Timeout for hello activity.</span></span> <span data-ttu-id="945f1-296">예: 00:10:00(시간 제한 10분을 의미함)</span><span class="sxs-lookup"><span data-stu-id="945f1-296">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="945f1-297">값을 지정 하지 않거나 0으로 하는 경우에 hello 시간 초과 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-297">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="945f1-298">분할 영역에 데이터 처리 시간이 hello hello 제한 시간 값을 초과 하는 경우 취소 되 및 hello 시스템 tooretry hello 처리를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-298">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="945f1-299">재시도 횟수 hello hello retry 속성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-299">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="945f1-300">시간 제한이 발생 hello 상태 tooTimedOut 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-300">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="945f1-301">delay</span><span class="sxs-lookup"><span data-stu-id="945f1-301">delay</span></span> |<span data-ttu-id="945f1-302">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="945f1-302">TimeSpan</span></span> |<span data-ttu-id="945f1-303">00:00:00</span><span class="sxs-lookup"><span data-stu-id="945f1-303">00:00:00</span></span> |<span data-ttu-id="945f1-304">데이터 처리 hello 조각 시작 하기 전에 hello 지연 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-304">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="945f1-305">데이터 조각에 대 한 활동의 hello 실행 hello 지연 되는 hello 예상 실행 시간 후에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-305">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="945f1-306">예: 00:10:00(10분의 지연을 의미함)</span><span class="sxs-lookup"><span data-stu-id="945f1-306">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="945f1-307">longRetry</span><span class="sxs-lookup"><span data-stu-id="945f1-307">longRetry</span></span> |<span data-ttu-id="945f1-308">정수 </span><span class="sxs-lookup"><span data-stu-id="945f1-308">Integer</span></span><br/><br/><span data-ttu-id="945f1-309">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="945f1-309">Max value: 10</span></span> |<span data-ttu-id="945f1-310">1</span><span class="sxs-lookup"><span data-stu-id="945f1-310">1</span></span> |<span data-ttu-id="945f1-311">hello 긴 다시 시도 횟수 후 hello 조각 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-311">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="945f1-312">longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-312">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="945f1-313">따라서 다시 시도 사이의 시간 toospecify 해야 할 경우 longRetry를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-313">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="945f1-314">Retry와 longRetry를 둘 다 지정 된 경우 다시 시도 횟수를 포함 하는 각 longRetry 시도 및 hello 최대 시도 횟수가 다시 시도 * longRetry 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-314">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="945f1-315">예를 들어, hello 활동 정책의 설정에에서 따라 hello 사항이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="945f1-315">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="945f1-316">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="945f1-316">Retry: 3</span></span><br/><span data-ttu-id="945f1-317">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="945f1-317">longRetry: 2</span></span><br/><span data-ttu-id="945f1-318">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="945f1-318">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="945f1-319">하나의 분할 영역 tooexecute 가정 (상태 대기 중) hello 활동 실행 될 때마다가 실패 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-319">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="945f1-320">우선 3번 연속 실행 시도를 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-320">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="945f1-321">각 시도 후 조각 상태 hello 재시도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-321">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="945f1-322">통해 처음 3 시도 되 면 hello 조각 상태 LongRetry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-322">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="945f1-323">한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-323">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="945f1-324">그 후 hello 조각 상태가 Failed가 고 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-324">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="945f1-325">즉, 전체적으로 6번의 시도가 일어납니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-325">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="945f1-326">실행에 성공 hello 조각 상태는 준비와 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-326">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="945f1-327">longRetry 명확 하지 않은 시간에 도착 하면 종속 데이터 또는 hello 전체 환경 연결이 잘 끊어지는 어떤 데이터 처리가 수행 아래 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-327">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="945f1-328">이러한 경우에 한 번에 하나씩 재시도 수행 하 도움이 되지 않을 수 및 출력을 원하는 hello에 결과 시간 간격 후 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-328">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="945f1-329">주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-329">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="945f1-330">일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-330">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="945f1-331">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="945f1-331">longRetryInterval</span></span> |<span data-ttu-id="945f1-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="945f1-332">TimeSpan</span></span> |<span data-ttu-id="945f1-333">00:00:00</span><span class="sxs-lookup"><span data-stu-id="945f1-333">00:00:00</span></span> |<span data-ttu-id="945f1-334">긴 시도 간의 지연을 hello</span><span class="sxs-lookup"><span data-stu-id="945f1-334">hello delay between long retry attempts</span></span> |

## <a name="sample-copy-pipeline"></a><span data-ttu-id="945f1-335">샘플 복사 파이프라인</span><span class="sxs-lookup"><span data-stu-id="945f1-335">Sample copy pipeline</span></span>
<span data-ttu-id="945f1-336">다음 샘플 파이프라인 hello에 하나의 활동 형식의 **복사** hello에 **활동** 섹션.</span><span class="sxs-lookup"><span data-stu-id="945f1-336">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="945f1-337">이 샘플에서는 hello [복사 작업이](data-factory-data-movement-activities.md) Azure Blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-337">In this sample, hello [copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
} 
```

<span data-ttu-id="945f1-338">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="945f1-338">Note hello following points:</span></span>

* <span data-ttu-id="945f1-339">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-339">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="945f1-340">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-340">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> <span data-ttu-id="945f1-341">JSON의 데이터 집합 정의에 대해서는 [데이터 집합](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-341">See [Datasets](data-factory-create-datasets.md) article for defining datasets in JSON.</span></span> 
* <span data-ttu-id="945f1-342">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-342">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="945f1-343">Hello에 [데이터 이동 활동](#data-movement-activities) 섹션에서 데이터 원본 또는 싱크 toolearn를 해당 데이터 저장소에서 데이터를 이동 하는 방법에 대 한 자세한으로 toouse 되도록 저장소 hello를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-343">In hello [Data movement activities](#data-movement-activities) section, click hello data store that you want toouse as a source or a sink toolearn more about moving data to/from that data store.</span></span> 

<span data-ttu-id="945f1-344">이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-344">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="sample-transformation-pipeline"></a><span data-ttu-id="945f1-345">샘플 변환 파이프라인</span><span class="sxs-lookup"><span data-stu-id="945f1-345">Sample transformation pipeline</span></span>
<span data-ttu-id="945f1-346">다음 샘플 파이프라인 hello에 하나의 활동 형식의 **HDInsightHive** hello에 **활동** 섹션.</span><span class="sxs-lookup"><span data-stu-id="945f1-346">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="945f1-347">이 샘플에서는 hello [HDInsight Hive 활동](data-factory-hive-activity.md) Azure HDInsight Hadoop 클러스터에서 하이브 스크립트 파일을 실행 하 여 Azure Blob 저장소에서 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-347">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00Z",
        "end": "2016-04-02T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="945f1-348">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="945f1-348">Note hello following points:</span></span> 

* <span data-ttu-id="945f1-349">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**HDInsightHive**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-349">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="945f1-350">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-350">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="945f1-351">hello `defines` 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="945f1-351">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="945f1-352">hello **typeProperties** 섹션은 각 변환 활동 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-352">hello **typeProperties** section is different for each transformation activity.</span></span> <span data-ttu-id="945f1-353">변환 작업을 위해 지원 되는 형식 속성에 대 한 toolearn 클릭 hello에 hello 변환 활동 [데이터 변환 작업](#data-transformation-activities) 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-353">toolearn about type properties supported for a transformation activity, click hello transformation activity in hello [Data transformation activities](#data-transformation-activities) table.</span></span> 

<span data-ttu-id="945f1-354">이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: 첫 번째 파이프라인 tooprocess 데이터 Hadoop 클러스터를 사용 하 여 빌드](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-354">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="945f1-355">파이프라인의 여러 활동</span><span class="sxs-lookup"><span data-stu-id="945f1-355">Multiple activities in a pipeline</span></span>
<span data-ttu-id="945f1-356">hello 이전 두 개의 샘플 파이프라인에 활동이 하나만 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-356">hello previous two sample pipelines have only one activity in them.</span></span> <span data-ttu-id="945f1-357">그렇지만 하나의 파이프라인에 여러 개의 활동이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-357">You can have more than one activity in a pipeline.</span></span>  

<span data-ttu-id="945f1-358">파이프라인의 여러 활동 있고 다른 활동의 입력이 아닌 출력을 작업의 경우 hello 활동에 대 한 입력된 데이터 조각이 준비가 되었는지 여부 hello 활동 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-358">If you have multiple activities in a pipeline and output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span> 

<span data-ttu-id="945f1-359">연결할 수 있습니다. 두 활동의 hello hello 입력된 데이터 집합으로 한 활동의 hello 출력 데이터 집합을 포함 하면 다른 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-359">You can chain two activities by having hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="945f1-360">두 번째 활동 hello hello 먼저 하나 성공적으로 완료 되는 경우에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-360">hello second activity executes only when hello first one completes successfully.</span></span>

![동일한 파이프라인 활동 hello에 연결](./media/data-factory-create-pipelines/chaining-one-pipeline.png)

<span data-ttu-id="945f1-362">이 샘플에서는 hello 파이프라인에는 두 개의 활동: t y 1과 Activity2 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-362">In this sample, hello pipeline has two activities: Activity1 and Activity2.</span></span> <span data-ttu-id="945f1-363">Dataset1 입력으로를 사용 하 고 출력을 생성 하는 hello Activity1 Dataset2 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-363">hello Activity1 takes Dataset1 as an input and produces an output Dataset2.</span></span> <span data-ttu-id="945f1-364">hello 활동은 입력으로 Dataset2 하 고 생성 출력 Dataset3 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-364">hello Activity takes Dataset2 as an input and produces an output Dataset3.</span></span> <span data-ttu-id="945f1-365">Y 1의 hello 출력 이후 Activity2 hello 입력이 됩니다 (Dataset2), Activity2 hello hello 활동이 성공적으로 완료 된 후에 실행 및 생성 hello Dataset2 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-365">Since hello output of Activity1 (Dataset2) is hello input of Activity2, hello Activity2 runs only after hello Activity completes successfully and produces hello Dataset2 slice.</span></span> <span data-ttu-id="945f1-366">Hello 활동 2 hello Activity1 어떤 이유로 실패 하 고 hello Dataset2 분할 영역을 생성 하지 않으므로, 해당 조각에 대 한 실행 되지 않습니다 (예: 9 AM too10 AM).</span><span class="sxs-lookup"><span data-stu-id="945f1-366">If hello Activity1 fails for some reason and does not produce hello Dataset2 slice, hello Activity 2 does not run for that slice (for example: 9 AM too10 AM).</span></span> 

<span data-ttu-id="945f1-367">다른 파이프라인에 있는 활동을 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-367">You can also chain activities that are in different pipelines.</span></span>

![두 개의 파이프라인에서 활동 연결](./media/data-factory-create-pipelines/chaining-two-pipelines.png)

<span data-ttu-id="945f1-369">이 샘플에서 Pipeline1은 Dataset1을 입력으로 받고 Dataset2를 출력으로 생성하는 하나의 활동만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-369">In this sample, Pipeline1 has only one activity that takes Dataset1 as an input and produces Dataset2 as an output.</span></span> <span data-ttu-id="945f1-370">hello Pipeline2에를 입력 및 출력으로 Dataset3 Dataset2 받아들이는 활동이 하나만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-370">hello Pipeline2 also has only one activity that takes Dataset2 as an input and Dataset3 as an output.</span></span> 

<span data-ttu-id="945f1-371">자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-371">For more information, see [scheduling and execution](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="create-and-monitor-pipelines"></a><span data-ttu-id="945f1-372">파이프라인 만들기 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="945f1-372">Create and monitor pipelines</span></span>
<span data-ttu-id="945f1-373">다음 도구 또는 SDK 중 하나를 사용하여 파이프라인을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-373">You can create pipelines by using one of these tools or SDKs.</span></span> 

- <span data-ttu-id="945f1-374">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="945f1-374">Copy Wizard.</span></span> 
- <span data-ttu-id="945f1-375">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="945f1-375">Azure portal</span></span>
- <span data-ttu-id="945f1-376">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="945f1-376">Visual Studio</span></span>
- <span data-ttu-id="945f1-377">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="945f1-377">Azure PowerShell</span></span>
- <span data-ttu-id="945f1-378">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="945f1-378">Azure Resource Manager template</span></span>
- <span data-ttu-id="945f1-379">REST API</span><span class="sxs-lookup"><span data-stu-id="945f1-379">REST API</span></span>
- <span data-ttu-id="945f1-380">.NET API</span><span class="sxs-lookup"><span data-stu-id="945f1-380">.NET API</span></span>

<span data-ttu-id="945f1-381">이러한 도구 또는 Sdk 중 하나를 사용 하 여 파이프라인 만들기에 대 한 단계별 지침에 대 한 자습서를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="945f1-381">See hello following tutorials for step-by-step instructions for creating pipelines by using one of these tools or SDKs.</span></span>
 
- [<span data-ttu-id="945f1-382">데이터 변환 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="945f1-382">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="945f1-383">데이터 이동 활동을 사용하여 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="945f1-383">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="945f1-384">파이프라인을 생성/배포를 관리 하 고 모니터링할 수를 사용 하 여 파이프라인 hello Azure 포털 블레이드 나 모니터와 응용 프로그램을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-384">Once a pipeline is created/deployed, you can manage and monitor your pipelines by using hello Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="945f1-385">Hello 다음 단계별 지침에 대 한 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="945f1-385">See hello following topics for step-by-step instructions.</span></span> 

- <span data-ttu-id="945f1-386">[Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md)</span><span class="sxs-lookup"><span data-stu-id="945f1-386">[Monitor and manage pipelines by using Azure portal blades](data-factory-monitor-manage-pipelines.md).</span></span>
- [<span data-ttu-id="945f1-387">모니터 및 관리 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="945f1-387">Monitor and manage pipelines by using Monitor and Manage App</span></span>](data-factory-monitor-manage-app.md)


## <a name="onetime-pipeline"></a><span data-ttu-id="945f1-388">일회성 파이프라인</span><span class="sxs-lookup"><span data-stu-id="945f1-388">Onetime pipeline</span></span>
<span data-ttu-id="945f1-389">만들고 파이프라인 toorun를 주기적으로 예약할 수 있습니다 (예: 시간 또는 일별로) hello 내에서 시작 및 종료 hello 파이프라인 정의에서 지정 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-389">You can create and schedule a pipeline toorun periodically (for example: hourly or daily) within hello start and end times you specify in hello pipeline definition.</span></span> <span data-ttu-id="945f1-390">자세한 내용은 [활동 예약](#scheduling-and-execution) 을 참고하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-390">See [Scheduling activities](#scheduling-and-execution) for details.</span></span> <span data-ttu-id="945f1-391">한 번만 실행되는 파이프라인을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-391">You can also create a pipeline that runs only once.</span></span> <span data-ttu-id="945f1-392">toodo hello 설정, **pipelineMode** hello에서 속성 정의 너무 파이프라인**onetime** hello JSON 샘플 다음에 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-392">toodo so, you set hello **pipelineMode** property in hello pipeline definition too**onetime** as shown in hello following JSON sample.</span></span> <span data-ttu-id="945f1-393">이 속성에 대 한 hello 기본값은 **예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-393">hello default value for this property is **scheduled**.</span></span>

```json
{
    "name": "CopyPipeline",
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
                        "name": "InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ]
                "name": "CopyActivity-0"
            }
        ]
        "pipelineMode": "OneTime"
    }
}
```

<span data-ttu-id="945f1-394">참고 hello 다음.</span><span class="sxs-lookup"><span data-stu-id="945f1-394">Note hello following:</span></span>

* <span data-ttu-id="945f1-395">**시작** 및 **끝** hello 파이프라인에 대 한 시간 지정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-395">**Start** and **end** times for hello pipeline are not specified.</span></span>
* <span data-ttu-id="945f1-396">**가용성** 입력 및 출력의 데이터 집합 지정 (**주파수** 및 **간격**) Data Factory hello 값을 사용 하지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-396">**Availability** of input and output datasets is specified (**frequency** and **interval**), even though Data Factory does not use hello values.</span></span>  
* <span data-ttu-id="945f1-397">다이어그램 뷰는 일회성 파이프라인을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-397">Diagram view does not show one-time pipelines.</span></span> <span data-ttu-id="945f1-398">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-398">This behavior is by design.</span></span>
* <span data-ttu-id="945f1-399">일회성 파이프라인은 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-399">One-time pipelines cannot be updated.</span></span> <span data-ttu-id="945f1-400">일회성 파이프라인 복제, 이름을 바꾸거나, 속성을 업데이트 한 toocreate 배포할 수 있습니다 다른 합니다.</span><span class="sxs-lookup"><span data-stu-id="945f1-400">You can clone a one-time pipeline, rename it, update properties, and deploy it toocreate another one.</span></span>


## <a name="next-steps"></a><span data-ttu-id="945f1-401">다음 단계</span><span class="sxs-lookup"><span data-stu-id="945f1-401">Next Steps</span></span>
- <span data-ttu-id="945f1-402">데이터 집합에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-402">For more information about datasets, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 
- <span data-ttu-id="945f1-403">파이프라인을 예약하고 실행하는 방법에 대한 자세한 내용은 [Azure Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="945f1-403">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md) article.</span></span> 
  

