---
title: "Hadoop 스트리밍 작업을 사용하여 데이터 변환 - Azure | Microsoft Docs"
description: "Azure Data Factory에서 Hadoop 스트리밍 작업을 사용하여 주문형/사용자 고유의 HDInsight 클러스터에서 Hadoop 스트리밍 프로그램을 실행함으로써 데이터를 변환하는 방법을 알아봅니다."
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
ms.openlocfilehash: bfe62aa60f5a0ff339e1d495d22a5fdfac10d5dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a><span data-ttu-id="2b349-103">Azure Data Factory에서 Hadoop 스트리밍 작업을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="2b349-103">Transform data using Hadoop Streaming Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2b349-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="2b349-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2b349-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2b349-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2b349-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2b349-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2b349-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2b349-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2b349-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2b349-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="2b349-114">HDInsightStreamingActivity 작업을 사용하여 Azure Data Factory 파이프라인에서 Hadoop 스트리밍 작업을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-114">You can use the HDInsightStreamingActivity Activity invoke a Hadoop Streaming job from an Azure Data Factory pipeline.</span></span> <span data-ttu-id="2b349-115">다음 JSON 조각은 파이프라인 JSON 파일에서 HDInsightStreamingActivity를 사용하기 위한 구문을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-115">The following JSON snippet shows the syntax for using the HDInsightStreamingActivity in a pipeline JSON file.</span></span> 

<span data-ttu-id="2b349-116">Data Factory [파이프라인](data-factory-create-pipelines.md)의 HDInsight 스트리밍 작업은 [사용자 고유](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터에서 Hadoop 스트리밍 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-116">The HDInsight Streaming Activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hadoop Streaming programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2b349-117">이 문서는 데이터 변환 및 지원되는 변환 활동의 일반적인 개요를 표시하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="2b349-118">Azure Data Factory를 처음 접하는 경우 [Azure Data Factory 소개](data-factory-introduction.md)를 읽고 이 문서를 읽기 전에 [첫 번째 데이터 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 자습서를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="2b349-118">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="json-sample"></a><span data-ttu-id="2b349-119">JSON 샘플</span><span class="sxs-lookup"><span data-stu-id="2b349-119">JSON sample</span></span>
<span data-ttu-id="2b349-120">HDInsight 클러스터는 예제 프로그램(wc.exe 및 cat.exe) 및 데이터(davinci.txt)와 함께 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-120">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="2b349-121">기본적으로 HDInsight 클러스터에 사용되는 컨테이너의 이름은 클러스터 자체의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-121">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="2b349-122">예를 들어, 클러스터 이름이 myhdicluster이면 연결된 BLOB 컨테이너의 이름은 myhdicluster가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-122">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span> 

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

<span data-ttu-id="2b349-123">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="2b349-123">Note the following points:</span></span>

1. <span data-ttu-id="2b349-124">**linkedServiceName** 을 스트리밍 mapreduce 작업을 실행할 수 있는 HDInsight 클러스터를 가리키는 연결된 서비스의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-124">Set the **linkedServiceName** to the name of the linked service that points to your HDInsight cluster on which the streaming mapreduce job is run.</span></span>
2. <span data-ttu-id="2b349-125">activity의 type을 **HDInsightStreaming**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-125">Set the type of the activity to **HDInsightStreaming**.</span></span>
3. <span data-ttu-id="2b349-126">**mapper** 속성에는 매퍼 실행 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-126">For the **mapper** property, specify the name of mapper executable.</span></span> <span data-ttu-id="2b349-127">예제에서는 cat.exe가 매퍼 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-127">In the example, cat.exe is the mapper executable.</span></span>
4. <span data-ttu-id="2b349-128">**reducer** 속성에는 리듀서 실행 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-128">For the **reducer** property, specify the name of reducer executable.</span></span> <span data-ttu-id="2b349-129">예제에서는 wc.exe가 리듀서 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-129">In the example, wc.exe is the reducer executable.</span></span>
5. <span data-ttu-id="2b349-130">**input** 유형 속성에는 매퍼의 입력 파일(위치 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-130">For the **input** type property, specify the input file (including the location) for the mapper.</span></span> <span data-ttu-id="2b349-131">예제의 "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt"에서 adfsample은 BLOB 컨테이너이고 example/data/Gutenberg는 폴더이며 davinci.txt는 BOLB입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-131">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span>
6. <span data-ttu-id="2b349-132">**output** 유형 속성에는 리듀서의 출력 파일(위치 포함)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-132">For the **output** type property, specify the output file (including the location) for the reducer.</span></span> <span data-ttu-id="2b349-133">Hadoop 스트리밍 작업의 출력이 이 속성에 지정된 위치에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-133">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span>
7. <span data-ttu-id="2b349-134">**filePaths** 섹션에서 매퍼 및 리듀서 실행 파일의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-134">In the **filePaths** section, specify the paths for the mapper and reducer executables.</span></span> <span data-ttu-id="2b349-135">"adfsample/example/apps/wc.exe" 예에서 adfsample은 Blob 컨테이너, example/apps는 폴더, wc.exe는 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-135">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span>
8. <span data-ttu-id="2b349-136">**fileLinkedService** 속성에는 filePaths 섹션에 지정된 파일이 포함된 Azure 저장소를 나타내는 Azure 저장소 연결된 서비스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-136">For the **fileLinkedService** property, specify the Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span>
9. <span data-ttu-id="2b349-137">**arguments** 속성에는 스트리밍 작업의 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-137">For the **arguments** property, specify the arguments for the streaming job.</span></span>
10. <span data-ttu-id="2b349-138">**getDebugInfo** 속성은 선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-138">The **getDebugInfo** property is an optional element.</span></span> <span data-ttu-id="2b349-139">Failure로 설정되면 실패한 경우에만 로그가 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-139">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="2b349-140">Always로 설정되면 실행 상태에 관계없이 로그가 항상 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-140">When it is set to Always, logs are always downloaded irrespective of the execution status.</span></span>

> [!NOTE]
> <span data-ttu-id="2b349-141">예제에서 볼 수 있듯이 **output** 속성에 대해 Hadoop 스트리밍 작업에 대한 출력 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-141">As shown in the example, you specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="2b349-142">이 데이터 집합은 파이프라인 일정을 진행하는데 필요한 더미 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-142">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> <span data-ttu-id="2b349-143">**input** 속성에 대한 작업에 입력 데이터 집합을 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-143">You do not need to specify any input dataset for the activity for the **inputs** property.</span></span>  
> 
> 

## <a name="example"></a><span data-ttu-id="2b349-144">예</span><span class="sxs-lookup"><span data-stu-id="2b349-144">Example</span></span>
<span data-ttu-id="2b349-145">이번 연습의 파이프라인에서는 Azure HDInsight 클러스터에서 Word Count 스트리밍 Map/Reduce 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-145">The pipeline in this walkthrough runs the Word Count streaming Map/Reduce program on your Azure HDInsight cluster.</span></span> 

### <a name="linked-services"></a><span data-ttu-id="2b349-146">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="2b349-146">Linked services</span></span>
#### <a name="azure-storage-linked-service"></a><span data-ttu-id="2b349-147">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="2b349-147">Azure Storage linked service</span></span>
<span data-ttu-id="2b349-148">우선 Azure HDInsight 클러스터에서 사용되는 Azure 저장소를 Azure 데이터 팩터리에 연결하도록 연결된 서비스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-148">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="2b349-149">다음 코드를 복사하여 붙여넣는 경우, 잊지 말고 계정 이름과 계정 키를 사용자의 Azure 저장소의 이름과 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-149">If you copy/paste the following code, do not forget to replace account name and account key with the name and key of your Azure Storage.</span></span> 

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="2b349-150">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="2b349-150">Azure HDInsight linked service</span></span>
<span data-ttu-id="2b349-151">다음으로, Azure HDInsight 클러스터를 Azure 데이터 팩터리에 연결하도록 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-151">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="2b349-152">다음 코드를 복사하여 붙여넣는 경우, HDInsight 클러스터 이름을 사용자의 HDInsight 클러스터 이름으로 바꾸고 사용자 이름과 암호 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-152">If you copy/paste the following code, replace HDInsight cluster name with the name of your HDInsight cluster, and change user name and password values.</span></span> 

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

### <a name="datasets"></a><span data-ttu-id="2b349-153">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="2b349-153">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="2b349-154">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="2b349-154">Output dataset</span></span>
<span data-ttu-id="2b349-155">이 예제의 파이프라인은 input을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-155">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="2b349-156">HDInsight 스트리밍 작업에 대한 출력 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-156">You specify an output dataset for the HDInsight Streaming Activity.</span></span> <span data-ttu-id="2b349-157">이 데이터 집합은 파이프라인 일정을 진행하는데 필요한 더미 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-157">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span> 

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

### <a name="pipeline"></a><span data-ttu-id="2b349-158">파이프라인</span><span class="sxs-lookup"><span data-stu-id="2b349-158">Pipeline</span></span>
<span data-ttu-id="2b349-159">이 예제의 파이프라인은 **HDInsightStreaming**형식의 작업을 하나만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-159">The pipeline in this example has only one activity that is of type: **HDInsightStreaming**.</span></span> 

<span data-ttu-id="2b349-160">HDInsight 클러스터는 예제 프로그램(wc.exe 및 cat.exe) 및 데이터(davinci.txt)와 함께 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-160">The HDInsight cluster is automatically populated with example programs (wc.exe and cat.exe) and data (davinci.txt).</span></span> <span data-ttu-id="2b349-161">기본적으로 HDInsight 클러스터에 사용되는 컨테이너의 이름은 클러스터 자체의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-161">By default, name of the container that is used by the HDInsight cluster is the name of the cluster itself.</span></span> <span data-ttu-id="2b349-162">예를 들어, 클러스터 이름이 myhdicluster이면 연결된 BLOB 컨테이너의 이름은 myhdicluster가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b349-162">For example, if your cluster name is myhdicluster, name of the blob container associated would be myhdicluster.</span></span>  

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
## <a name="see-also"></a><span data-ttu-id="2b349-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2b349-163">See Also</span></span>
* [<span data-ttu-id="2b349-164">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-164">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="2b349-165">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-165">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="2b349-166">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="2b349-166">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="2b349-167">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="2b349-167">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="2b349-168">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="2b349-168">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

