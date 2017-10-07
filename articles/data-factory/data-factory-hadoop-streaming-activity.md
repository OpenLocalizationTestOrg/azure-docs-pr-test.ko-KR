---
title: "Hadoop 스트리밍 작업-Azure를 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "에-필요 시/사용자 고유의 HDInsight 클러스터에서 Hadoop 스트리밍 프로그램을 실행 하 여 Azure 데이터 팩터리 tootransform 데이터에서 Hadoop 스트리밍 작업 hello를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="b088b-103">Azure Data Factory에서 Hadoop 스트리밍 작업을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="b088b-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="b088b-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="b088b-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="b088b-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="b088b-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="b088b-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="b088b-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="b088b-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="b088b-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="b088b-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="b088b-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="b088b-114">사용할 수 있습니다 HDInsightStreamingActivity 활동 hello Azure 데이터 팩터리 파이프라인에서 Hadoop 스트리밍 작업을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-114">You can use hello HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="b088b-115">hello 다음 JSON 코드 조각은 구문을 보여 줍니다 hello HDInsightStreamingActivity hello를 사용 하 여 파이프라인 JSON 파일.</span><span class="sxs-lookup"><span data-stu-id="b088b-115">hello following JSON snippet shows hello syntax for using hello HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="b088b-116">Data Factory에 HDInsight 스트리밍 활동 hello [파이프라인](data-factory-create-pipelines.md) 에서 Hadoop 스트리밍 프로그램을 실행 합니다. [고유한](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-116">hello HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b088b-117">Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="b088b-118">새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-118">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="b088b-119">JSON 샘플</span><span class="sxs-lookup"><span data-stu-id="b088b-119">JSON sample</span></span>
<span data-ttu-id="b088b-120">hello HDInsight 클러스터 (wc.exe 및 cat.exe) 예제 프로그램 및 데이터 (davinci.txt)으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-120">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b088b-121">기본적으로 hello HDInsight 클러스터에서 사용 되는 hello 컨테이너의 이름에는 hello 클러스터 자체의 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-121">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="b088b-122">예를 들어 클러스터 이름이 myhdicluster 이면 연결 된 hello blob 컨테이너의 이름을 myhdicluster 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-122">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span> 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

<span data-ttu-id="b088b-123">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="b088b-123">Note hello following points:</span></span>

1. <span data-ttu-id="b088b-124">집합 hello **linkedServiceName** 연결 된 서비스는 hello 스트리밍 mapreduce 작업 실행 tooyour HDInsight 클러스터를 가리키는의 hello toohello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-124">Set hello **linkedServiceName** toohello name of hello linked service that points tooyour HDInsight cluster on which hello streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="b088b-125">너무 hello 유형의 hello 활동 설정**HDInsightStreaming**합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-125">Set hello type of hello activity too**HDInsightStreaming**.</span></span>
3. <span data-ttu-id="b088b-126">Hello에 대 한 **매퍼** 속성을 hello 매퍼 실행 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-126">For hello **mapper** property, specify hello name of mapper executable.</span></span> <span data-ttu-id="b088b-127">Hello 예제 cat.exe는 hello 매퍼 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-127">In hello example, cat.exe is hello mapper executable.</span></span>
4. <span data-ttu-id="b088b-128">Hello에 대 한 **리 듀 서** 속성 리 듀 서 실행 파일의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-128">For hello **reducer** property, specify hello name of reducer executable.</span></span> <span data-ttu-id="b088b-129">Hello 예제 wc.exe는 hello 리 듀 서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-129">In hello example, wc.exe is hello reducer executable.</span></span>
5. <span data-ttu-id="b088b-130">Hello에 대 한 **입력** type 속성을 hello 맵 편집기에 대 한 hello 입력된 파일 (hello 위치)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-130">For hello **input** type property, specify hello input file (including hello location) for hello mapper.</span></span> <span data-ttu-id="b088b-131">Hello 예에서: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample이 blob 컨테이너 hello, 예제/data/Gutenberg hello 폴더 이며 davinci.txt가 blob hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-131">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span>
6. <span data-ttu-id="b088b-132">Hello에 대 한 **출력** type 속성을 hello 리 듀 서에 대 한 hello 출력 파일 (hello 위치 포함)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-132">For hello **output** type property, specify hello output file (including hello location) for hello reducer.</span></span> <span data-ttu-id="b088b-133">hello Hadoop 스트리밍 작업의 hello 출력은이 속성에 지정 된 toohello 위치를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-133">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span>
7. <span data-ttu-id="b088b-134">Hello에 **filePaths** 섹션에서 hello 매퍼 및 리 듀 서 실행 파일에 대 한 hello 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-134">In hello **filePaths** section, specify hello paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="b088b-135">Hello 예에서: "adfsample/example/apps/wc.exe" adfsample이 blob 컨테이너 hello, example/apps가 hello 폴더 및 wc.exe는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-135">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span>
8. <span data-ttu-id="b088b-136">Hello에 대 한 **fileLinkedService** 속성을 hello Azure 저장소 연결 된 서비스를 나타내는 hello hello filePaths 섹션에 지정 된 hello 파일이 포함 된 Azure 저장소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-136">For hello **fileLinkedService** property, specify hello Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span>
9. <span data-ttu-id="b088b-137">Hello에 대 한 **인수** 속성을 hello 스트리밍 작업에 대 한 hello 인수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-137">For hello **arguments** property, specify hello arguments for hello streaming job.</span></span>
10. <span data-ttu-id="b088b-138">hello **getDebugInfo** 속성은 선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-138">hello **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="b088b-139">TooFailure, 설정 되 면 hello 로그 오류에 대해서만 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-139">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="b088b-140">TooAlways, 설정 되어 있는 경우 로그 hello 실행 상태에 관계 없이 항상 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-140">When it is set tooAlways, logs are always downloaded irrespective of hello execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="b088b-141">Hello에 대 한 hello Hadoop 스트리밍 작업에 대 한 출력 데이터 집합 지정 hello 예제 에서처럼 **출력** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-141">As shown in hello example, you specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="b088b-142">이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-142">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> <span data-ttu-id="b088b-143">않아도 toospecify 모든 입력된 데이터 집합 hello에 대 한 hello 활동에 대 한 **입력** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-143">You do not need toospecify any input dataset for hello activity for hello **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="b088b-144">예제</span><span class="sxs-lookup"><span data-stu-id="b088b-144">Example</span></span>
<span data-ttu-id="b088b-145">Azure HDInsight 클러스터에서 hello 단어 개수 스트리밍 Map/Reduce 프로그램을 실행 하는이 연습에서 hello 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="b088b-145">hello pipeline in this walkthrough runs hello Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="b088b-146">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b088b-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="b088b-147">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b088b-147">Azure Storage linked service</span></span>
<span data-ttu-id="b088b-148">먼저, 연결 된 서비스 toolink hello hello Azure HDInsight 클러스터 toohello Azure 데이터 팩터리에서 사용 되는 Azure 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-148">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b088b-149">경우 하면 복사/붙여넣기 코드 다음 hello 잊지 마십시오 hello 이름의 tooreplace 계정 이름 및 계정 키 및 Azure 저장소의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-149">If you copy/paste hello following code, do not forget tooreplace account name and account key with hello name and key of your Azure Storage.</span></span> 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="b088b-150">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="b088b-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="b088b-151">다음으로 연결 된 서비스 toolink Azure HDInsight 클러스터 toohello Azure 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-151">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="b088b-152">경우 하면 복사/붙여넣기 코드 다음 hello HDInsight 클러스터의 hello 이름의 HDInsight 클러스터 이름을 바꾼 사용자 이름 및 암호 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-152">If you copy/paste hello following code, replace HDInsight cluster name with hello name of your HDInsight cluster, and change user name and password values.</span></span> 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a><span data-ttu-id="b088b-153">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b088b-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="b088b-154">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="b088b-154">Output dataset</span></span>
<span data-ttu-id="b088b-155">이 예제에서 hello 파이프라인 어떤 입력도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-155">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="b088b-156">Hello HDInsight 스트리밍 활동에 대 한 출력 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-156">You specify an output dataset for hello HDInsight Streaming Activity.</span></span> <span data-ttu-id="b088b-157">이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-157">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span> 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="b088b-158">파이프라인</span><span class="sxs-lookup"><span data-stu-id="b088b-158">Pipeline</span></span>
<span data-ttu-id="b088b-159">이 예에서 hello 파이프라인에 유형의 활동이 하나만: **HDInsightStreaming**합니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-159">hello pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="b088b-160">hello HDInsight 클러스터 (wc.exe 및 cat.exe) 예제 프로그램 및 데이터 (davinci.txt)으로 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-160">hello HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="b088b-161">기본적으로 hello HDInsight 클러스터에서 사용 되는 hello 컨테이너의 이름에는 hello 클러스터 자체의 hello 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-161">By default, name of hello container that is used by hello HDInsight cluster is hello name of hello cluster itself.</span></span> <span data-ttu-id="b088b-162">예를 들어 클러스터 이름이 myhdicluster 이면 연결 된 hello blob 컨테이너의 이름을 myhdicluster 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b088b-162">For example, if your cluster name is myhdicluster, name of hello blob container associated would be myhdicluster.</span></span>  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a><span data-ttu-id="b088b-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="b088b-163">See Also</span></span>
* [<span data-ttu-id="b088b-164">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="b088b-165">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="b088b-166">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="b088b-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="b088b-167">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="b088b-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="b088b-168">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="b088b-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

