---
title: "Azure 데이터 팩터리에서 MapReduce 프로그램 호출"
description: "Azure HDInsight 클러스터에서 Azure 데이터 팩터리의 MapReduce 프로그램을 실행하여 데이터를 처리하는 방법을 알아봅니다."
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
ms.openlocfilehash: 55fc2196cb4ba50eced4a463914ae188217d0fed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a><span data-ttu-id="e8c9f-103">데이터 팩터리에서 MapReduce 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="e8c9f-103">Invoke MapReduce Programs from Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="e8c9f-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="e8c9f-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="e8c9f-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="e8c9f-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="e8c9f-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="e8c9f-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="e8c9f-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="e8c9f-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="e8c9f-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="e8c9f-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="e8c9f-114">Data Factory [파이프라인](data-factory-create-pipelines.md)의 HDInsight MapReduce 작업은 [사용자 고유](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터에서 MapReduce 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-114">The HDInsight MapReduce activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes MapReduce programs on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e8c9f-115">이 문서는 데이터 변환 및 지원되는 변환 활동의 일반적인 개요를 표시하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="e8c9f-116">Azure Data Factory를 처음 접하는 경우 [Azure Data Factory 소개](data-factory-introduction.md)를 읽고 이 문서를 읽기 전에 [첫 번째 데이터 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 자습서를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span>  

## <a name="introduction"></a><span data-ttu-id="e8c9f-117">소개</span><span class="sxs-lookup"><span data-stu-id="e8c9f-117">Introduction</span></span>
<span data-ttu-id="e8c9f-118">Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-118">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="e8c9f-119">파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-119">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="e8c9f-120">이 문서에서는 HDInsight MapReduce 작업을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-120">This article describes using the HDInsight MapReduce Activity.</span></span>

<span data-ttu-id="e8c9f-121">HDInsight Pig 및 Hive를 사용하여 파이프라인에서 Windows/Linux 기반 HDInsight 클러스터에 대해 Pig/Hive 스크립트를 실행하는 방법에 대한 자세한 내용은 [Pig](data-factory-pig-activity.md) 및 [Hive](data-factory-hive-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-121">See [Pig](data-factory-pig-activity.md) and [Hive](data-factory-hive-activity.md) for details about running Pig/Hive scripts on a Windows/Linux-based HDInsight cluster from a pipeline by using HDInsight Pig and Hive activities.</span></span> 

## <a name="json-for-hdinsight-mapreduce-activity"></a><span data-ttu-id="e8c9f-122">HDInsight MapReduce 작업에 대한 JSON</span><span class="sxs-lookup"><span data-stu-id="e8c9f-122">JSON for HDInsight MapReduce Activity</span></span>
<span data-ttu-id="e8c9f-123">HDInsight 작업에 대한 JSON 정의에서 다음을 수행합니다:</span><span class="sxs-lookup"><span data-stu-id="e8c9f-123">In the JSON definition for the HDInsight Activity:</span></span> 

1. <span data-ttu-id="e8c9f-124">**activity**의 **type**을 **HDInsight**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-124">Set the **type** of the **activity** to **HDInsight**.</span></span>
2. <span data-ttu-id="e8c9f-125">**className** 속성에 대한 클래스 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-125">Specify the name of the class for **className** property.</span></span>
3. <span data-ttu-id="e8c9f-126">**jarFilePath** 속성의 JAR 파일 경로(파일 이름 포함)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-126">Specify the path to the JAR file including the file name for **jarFilePath** property.</span></span>
4. <span data-ttu-id="e8c9f-127">**jarLinkedService** 속성의 JAR 파일이 포함된 Azure Blob 저장소를 참조하는 연결된 서비스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-127">Specify the linked service that refers to the Azure Blob Storage that contains the JAR file for **jarLinkedService** property.</span></span>   
5. <span data-ttu-id="e8c9f-128">**arguments** 섹션에 MapReduce 프로그램의 모든 인수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-128">Specify any arguments for the MapReduce program in the **arguments** section.</span></span> <span data-ttu-id="e8c9f-129">런타임에 MapReduce 프레임워크의 몇 개 인수(예: mapreduce.job.tags)가 추가로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-129">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="e8c9f-130">MapReduce 인수와 사용자 인수를 구분하려면 다음 예제와 같이 옵션과 값을 둘 다 인수로 사용하는 것이 좋습니다(-s, --input, --output 등은 바로 뒤에 해당 값이 있는 옵션임).</span><span class="sxs-lookup"><span data-stu-id="e8c9f-130">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values).</span></span>

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix to determine the similarity between 2 items",
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
                    "description": "Custom Map Reduce to generate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
<span data-ttu-id="e8c9f-131">HDInsight MapReduce 작업을 사용하여 HDInsight 클러스터에서 모든 MapReduce jar 파일을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-131">You can use the HDInsight MapReduce Activity to run any MapReduce jar file on an HDInsight cluster.</span></span> <span data-ttu-id="e8c9f-132">다음 파이프라인의 샘플 JSON 정의에서 HDInsight 작업은 Mahout JAR 파일을 실행하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-132">In the following sample JSON definition of a pipeline, the HDInsight Activity is configured to run a Mahout JAR file.</span></span>

## <a name="sample-on-github"></a><span data-ttu-id="e8c9f-133">GitHub의 샘플</span><span class="sxs-lookup"><span data-stu-id="e8c9f-133">Sample on GitHub</span></span>
<span data-ttu-id="e8c9f-134">HDInsight MapReduce 작업을 사용하는 샘플은 [GitHub의 데이터 팩터리 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-134">You can download a sample for using the HDInsight MapReduce Activity from: [Data Factory Samples on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample).</span></span>  

## <a name="running-the-word-count-program"></a><span data-ttu-id="e8c9f-135">Word Count 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e8c9f-135">Running the Word Count program</span></span>
<span data-ttu-id="e8c9f-136">이 예제의 파이프라인에서는 Azure HDInsight 클러스터에서 Word Count Map/Reduce 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-136">The pipeline in this example runs the Word Count Map/Reduce program on your Azure HDInsight cluster.</span></span>   

### <a name="linked-services"></a><span data-ttu-id="e8c9f-137">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e8c9f-137">Linked Services</span></span>
<span data-ttu-id="e8c9f-138">우선 Azure HDInsight 클러스터에서 사용되는 Azure 저장소를 Azure 데이터 팩터리에 연결하도록 연결된 서비스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-138">First, you create a linked service to link the Azure Storage that is used by the Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="e8c9f-139">다음 코드를 복사하여 붙여넣을 경우 **계정 이름**과 **계정 키**를 Azure Storage의 이름과 키로 바꾸는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-139">If you copy/paste the following code, do not forget to replace **account name** and **account key** with the name and key of your Azure Storage.</span></span> 

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e8c9f-140">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e8c9f-140">Azure Storage linked service</span></span>

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

#### <a name="azure-hdinsight-linked-service"></a><span data-ttu-id="e8c9f-141">Azure HDInsight 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e8c9f-141">Azure HDInsight linked service</span></span>
<span data-ttu-id="e8c9f-142">다음으로, Azure HDInsight 클러스터를 Azure 데이터 팩터리에 연결하도록 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-142">Next, you create a linked service to link your Azure HDInsight cluster to the Azure data factory.</span></span> <span data-ttu-id="e8c9f-143">다음 코드를 복사하여 붙여넣는 경우, **HDInsight 클러스터 이름** 을 사용자의 HDInsight 클러스터 이름으로 바꾸고 사용자 이름과 암호 값을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-143">If you copy/paste the following code, replace **HDInsight cluster name** with the name of your HDInsight cluster, and change user name and password values.</span></span>   

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

### <a name="datasets"></a><span data-ttu-id="e8c9f-144">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e8c9f-144">Datasets</span></span>
#### <a name="output-dataset"></a><span data-ttu-id="e8c9f-145">출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e8c9f-145">Output dataset</span></span>
<span data-ttu-id="e8c9f-146">이 예제의 파이프라인은 input을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-146">The pipeline in this example does not take any inputs.</span></span> <span data-ttu-id="e8c9f-147">HDInsight MapReduce 작업에 대한 출력 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-147">You specify an output dataset for the HDInsight MapReduce Activity.</span></span> <span data-ttu-id="e8c9f-148">이 데이터 집합은 파이프라인 일정을 진행하는데 필요한 더미 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-148">This dataset is just a dummy dataset that is required to drive the pipeline schedule.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="e8c9f-149">파이프라인</span><span class="sxs-lookup"><span data-stu-id="e8c9f-149">Pipeline</span></span>
<span data-ttu-id="e8c9f-150">이 예제의 파이프라인은 HDInsightMapReduce 형식의 작업을 하나만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-150">The pipeline in this example has only one activity that is of type: HDInsightMapReduce.</span></span> <span data-ttu-id="e8c9f-151">JSON의 중요한 속성에 대한 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-151">Some of the important properties in the JSON are:</span></span> 

| <span data-ttu-id="e8c9f-152">속성</span><span class="sxs-lookup"><span data-stu-id="e8c9f-152">Property</span></span> | <span data-ttu-id="e8c9f-153">참고 사항</span><span class="sxs-lookup"><span data-stu-id="e8c9f-153">Notes</span></span> |
|:--- |:--- |
| <span data-ttu-id="e8c9f-154">type</span><span class="sxs-lookup"><span data-stu-id="e8c9f-154">type</span></span> |<span data-ttu-id="e8c9f-155">type은 **HDInsightMapReduce**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-155">The type must be set to **HDInsightMapReduce**.</span></span> |
| <span data-ttu-id="e8c9f-156">className</span><span class="sxs-lookup"><span data-stu-id="e8c9f-156">className</span></span> |<span data-ttu-id="e8c9f-157">클래스 이름은 **wordcount**</span><span class="sxs-lookup"><span data-stu-id="e8c9f-157">Name of the class is: **wordcount**</span></span> |
| <span data-ttu-id="e8c9f-158">jarFilePath </span><span class="sxs-lookup"><span data-stu-id="e8c9f-158">jarFilePath</span></span> |<span data-ttu-id="e8c9f-159">클래스를 포함하는 jar 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-159">Path to the jar file containing the class.</span></span> <span data-ttu-id="e8c9f-160">다음 코드를 복사하여 붙여넣는 경우 클러스터의 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-160">If you copy/paste the following code, don't forget to change the name of the cluster.</span></span> |
| <span data-ttu-id="e8c9f-161">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="e8c9f-161">jarLinkedService</span></span> |<span data-ttu-id="e8c9f-162">jar 파일을 포함하는 Azure 저장소 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-162">Azure Storage linked service that contains the jar file.</span></span> <span data-ttu-id="e8c9f-163">이 연결된 서비스는 HDInsight 클러스터와 연결되는 저장소를 지칭합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-163">This linked service refers to the storage that is associated with the HDInsight cluster.</span></span> |
| <span data-ttu-id="e8c9f-164">arguments</span><span class="sxs-lookup"><span data-stu-id="e8c9f-164">arguments</span></span> |<span data-ttu-id="e8c9f-165">Wordcount 프로그램에서는 input과 output의 두 가지 인수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-165">The wordcount program takes two arguments, an input and an output.</span></span> <span data-ttu-id="e8c9f-166">input 파일은 davinci.txt 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-166">The input file is the davinci.txt file.</span></span> |
| <span data-ttu-id="e8c9f-167">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e8c9f-167">frequency/interval</span></span> |<span data-ttu-id="e8c9f-168">이러한 속성의 값은 출력 데이터 집합과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-168">The values for these properties match the output dataset.</span></span> |
| <span data-ttu-id="e8c9f-169">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e8c9f-169">linkedServiceName</span></span> |<span data-ttu-id="e8c9f-170">이전에 만든 HDInsight 연결된 서비스를 말합니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-170">refers to the HDInsight linked service you had created earlier.</span></span> |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run the Word Count Program",
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

## <a name="run-spark-programs"></a><span data-ttu-id="e8c9f-171">Spark 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="e8c9f-171">Run Spark programs</span></span>
<span data-ttu-id="e8c9f-172">MapReduce 작업을 사용하여 HDInsight Spark 클러스터에서 Spark 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-172">You can use MapReduce activity to run Spark programs on your HDInsight Spark cluster.</span></span> <span data-ttu-id="e8c9f-173">자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](data-factory-spark.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8c9f-173">See [Invoke Spark programs from Azure Data Factory](data-factory-spark.md) for details.</span></span>  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a><span data-ttu-id="e8c9f-174">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e8c9f-174">See Also</span></span>
* [<span data-ttu-id="e8c9f-175">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-175">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="e8c9f-176">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-176">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="e8c9f-177">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="e8c9f-177">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="e8c9f-178">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="e8c9f-178">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="e8c9f-179">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="e8c9f-179">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

