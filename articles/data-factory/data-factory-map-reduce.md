---
title: "Azure 데이터 팩터리에서 MapReduce 프로그램 aaaInvoke"
description: "Azure data factory에서 Azure HDInsight에서 MapReduce 프로그램을 실행 하 여 tooprocess 데이터 클러스터링 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="db3fc-103">데이터 팩터리에서 MapReduce 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="db3fc-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="db3fc-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="db3fc-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="db3fc-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="db3fc-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="db3fc-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="db3fc-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="db3fc-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="db3fc-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="db3fc-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="db3fc-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="db3fc-114">Data Factory에 HDInsight MapReduce 작업 hello [파이프라인](data-factory-create-pipelines.md) 에서 MapReduce 프로그램을 실행 합니다. [직접](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형으로](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-114">hello HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="db3fc-115">Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="db3fc-116">새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="db3fc-117">소개</span><span class="sxs-lookup"><span data-stu-id="db3fc-117">Introduction</span></span>
<span data-ttu-id="db3fc-118">Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="db3fc-119">파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="db3fc-120">이 문서에서는 hello HDInsight MapReduce 작업을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-120">This article describes using hello HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="db3fc-121">HDInsight Pig 및 Hive를 사용하여 파이프라인에서 Windows/Linux 기반 HDInsight 클러스터에 대해 Pig/Hive 스크립트를 실행하는 방법에 대한 자세한 내용은 [Pig](data-factory-pig-activity.md) 및 [Hive](data-factory-hive-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db3fc-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="db3fc-122">HDInsight MapReduce 작업에 대한 JSON</span><span class="sxs-lookup"><span data-stu-id="db3fc-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="db3fc-123">지 원하는 HDInsight 활동 hello에 대 한 JSON 정의 hello:</span><span class="sxs-lookup"><span data-stu-id="db3fc-123">In hello JSON definition for hello HDInsight Activity:</span></span> 

1. <span data-ttu-id="db3fc-124">집합 hello **형식** 의 hello **활동** 너무**HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-124">Set hello **type** of hello **activity** too**HDInsight**.</span></span>
2. <span data-ttu-id="db3fc-125">Hello에 대 한 hello 클래스 이름을 지정 **className** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-125">Specify hello name of hello class for **className** property.</span></span>
3. <span data-ttu-id="db3fc-126">에 대 한 hello 파일 이름을 포함 하는 hello 경로 toohello JAR 파일을 지정 **jarfilepath가** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-126">Specify hello path toohello JAR file including hello file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="db3fc-127">Toohello에 대 한 hello JAR 파일이 포함 된 Azure Blob 저장소를 참조 하는 연결 된 hello 서비스 지정 **jarLinkedService** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-127">Specify hello linked service that refers toohello Azure Blob Storage that contains hello JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="db3fc-128">Hello에 hello MapReduce 프로그램에 대 한 인수를 지정한 **인수** 섹션.</span><span class="sxs-lookup"><span data-stu-id="db3fc-128">Specify any arguments for hello MapReduce program in hello **arguments** section.</span></span> <span data-ttu-id="db3fc-129">런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서.</span><span class="sxs-lookup"><span data-stu-id="db3fc-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="db3fc-130">toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션).</span><span class="sxs-lookup"><span data-stu-id="db3fc-130">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="db3fc-131">HDInsight 클러스터에 있는 모든 MapReduce jar 파일 hello HDInsight MapReduce 작업 toorun를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-131">You can use hello HDInsight MapReduce Activity toorun any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="db3fc-132">Hello hello HDInsight 활동은 파이프라인의 다음 샘플 JSON 정의 toorun Mahout JAR 파일을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-132">In hello following sample JSON definition of a pipeline, hello HDInsight Activity is configured toorun a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="db3fc-133">GitHub의 샘플</span><span class="sxs-lookup"><span data-stu-id="db3fc-133">Sample on GitHub</span></span>
<span data-ttu-id="db3fc-134">Hello HDInsight MapReduce 작업을 사용 하기 위한 샘플을 다운로드할 수에서: [GitHub에서 데이터 팩터리 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-134">You can download a sample for using hello HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-hello-word-count-program"></a><span data-ttu-id="db3fc-135">Hello 단어 개수 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="db3fc-135">Running hello Word Count program</span></span>
<span data-ttu-id="db3fc-136">이 예제에서 파이프라인 hello Azure HDInsight 클러스터에서 hello 단어 개수 Map/Reduce 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-136">hello pipeline in this example runs hello Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="db3fc-137">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="db3fc-137">Linked Services</span></span>
<span data-ttu-id="db3fc-138">먼저, 연결 된 서비스 toolink hello hello Azure HDInsight 클러스터 toohello Azure 데이터 팩터리에서 사용 되는 Azure 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-138">First, you create a linked service toolink hello Azure Storage that is used by hello Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="db3fc-139">경우 하면 복사/붙여넣기 코드 다음 hello tooreplace 잊지 마십시오 **계정 이름** 및 **계정 키** hello 이름 및 Azure 저장소의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-139">If you copy/paste hello following code, do not forget tooreplace **account name** and **account key** with hello name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="db3fc-140">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="db3fc-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="db3fc-141">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="db3fc-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="db3fc-142">다음으로 연결 된 서비스 toolink Azure HDInsight 클러스터 toohello Azure 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-142">Next, you create a linked service toolink your Azure HDInsight cluster toohello Azure data factory.</span></span> <span data-ttu-id="db3fc-143">하면 복사/붙여넣기 코드 다음 hello 하는 경우 대체 **HDInsight 클러스터 이름을** HDInsight 클러스터와 사용자 이름 및 암호 값 변경의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-143">If you copy/paste hello following code, replace **HDInsight cluster name** with hello name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="db3fc-144">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="db3fc-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="db3fc-145">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="db3fc-145">Output dataset</span></span>
<span data-ttu-id="db3fc-146">이 예제에서 hello 파이프라인 어떤 입력도 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-146">hello pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="db3fc-147">HDInsight MapReduce 작업 hello에 대 한 출력 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-147">You specify an output dataset for hello HDInsight MapReduce Activity.</span></span> <span data-ttu-id="db3fc-148">이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-148">This dataset is just a dummy dataset that is required toodrive hello pipeline schedule.</span></span>  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="db3fc-149">파이프라인</span><span class="sxs-lookup"><span data-stu-id="db3fc-149">Pipeline</span></span>
<span data-ttu-id="db3fc-150">이 예에서 hello 파이프라인에 유형의 활동이 하나만: HDInsightMapReduce 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-150">hello pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="db3fc-151">Hello hello JSON에서에서 중요 한 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-151">Some of hello important properties in hello JSON are:</span></span> 

| <span data-ttu-id="db3fc-152">속성</span><span class="sxs-lookup"><span data-stu-id="db3fc-152">Property</span></span> | <span data-ttu-id="db3fc-153">참고 사항</span><span class="sxs-lookup"><span data-stu-id="db3fc-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="db3fc-154">type</span><span class="sxs-lookup"><span data-stu-id="db3fc-154">type</span></span> |<span data-ttu-id="db3fc-155">hello 형식이 너무 설정 되어 있어야**HDInsightMapReduce**합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-155">hello type must be set too**HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="db3fc-156">className</span><span class="sxs-lookup"><span data-stu-id="db3fc-156">className</span></span> |<span data-ttu-id="db3fc-157">Hello 클래스의 이름은: **단어 수**</span><span class="sxs-lookup"><span data-stu-id="db3fc-157">Name of hello class is: **wordcount**</span></span> |
| <span data-ttu-id="db3fc-158">jarFilePath </span><span class="sxs-lookup"><span data-stu-id="db3fc-158">jarFilePath</span></span> |<span data-ttu-id="db3fc-159">Hello 클래스를 포함 경로 toohello jar 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-159">Path toohello jar file containing hello class.</span></span> <span data-ttu-id="db3fc-160">경우 하면 복사/붙여넣기 코드 다음 hello hello 클러스터의 toochange hello 이름을 잊지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="db3fc-160">If you copy/paste hello following code, don't forget toochange hello name of hello cluster.</span></span> |
| <span data-ttu-id="db3fc-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="db3fc-161">jarLinkedService</span></span> |<span data-ttu-id="db3fc-162">Hello jar 파일이 포함 된 azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-162">Azure Storage linked service that contains hello jar file.</span></span> <span data-ttu-id="db3fc-163">이 연결 된 서비스는 hello HDInsight 클러스터와 연결 된 toohello 저장소를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-163">This linked service refers toohello storage that is associated with hello HDInsight cluster.</span></span> |
| <span data-ttu-id="db3fc-164">arguments</span><span class="sxs-lookup"><span data-stu-id="db3fc-164">arguments</span></span> |<span data-ttu-id="db3fc-165">hello wordcount 프로그램에는 두 개의 인수, 입력 및 출력 확보합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-165">hello wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="db3fc-166">hello 입력된 파일은 hello davinci.txt 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-166">hello input file is hello davinci.txt file.</span></span> |
| <span data-ttu-id="db3fc-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="db3fc-167">frequency/interval</span></span> |<span data-ttu-id="db3fc-168">이러한 속성에 대 한 hello 값 hello 출력 데이터 집합을 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-168">hello values for these properties match hello output dataset.</span></span> |
| <span data-ttu-id="db3fc-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="db3fc-169">linkedServiceName</span></span> |<span data-ttu-id="db3fc-170">이전에 만든 했습니다 toohello HDInsight 연결 된 서비스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-170">refers toohello HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a><span data-ttu-id="db3fc-171">Spark 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="db3fc-171">Run Spark programs</span></span>
<span data-ttu-id="db3fc-172">MapReduce 작업 toorun Spark 프로그램 HDInsight Spark 클러스터에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db3fc-172">You can use MapReduce activity toorun Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="db3fc-173">자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](data-factory-spark.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="db3fc-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="db3fc-174">참고 항목</span><span class="sxs-lookup"><span data-stu-id="db3fc-174">See Also</span></span>
* [<span data-ttu-id="db3fc-175">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="db3fc-176">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="db3fc-177">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="db3fc-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="db3fc-178">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="db3fc-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="db3fc-179">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="db3fc-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

