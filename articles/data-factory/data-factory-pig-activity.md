---
title: "Azure Data Factory에서 Pig 활동을 사용하여 데이터 변환 | Microsoft Docs"
description: "Azure Data Factory에서 Pig 작업을 사용하여 주문형/사용자 고유의 HDInsight 클러스터에서 Pig 스크립트를 실행하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 182a637ab98955129d269e2afc3ba581aa1a7c03
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="01bae-103">Azure Data Factory에서 Pig 활동을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="01bae-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="01bae-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="01bae-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="01bae-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="01bae-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="01bae-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="01bae-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="01bae-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="01bae-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="01bae-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="01bae-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="01bae-114">Data Factory [파이프라인](data-factory-create-pipelines.md)의 HDInsight Pig 작업은 [사용자 고유](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터의 Pig 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-114">The HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="01bae-115">이 문서는 데이터 변환 및 지원되는 변환 활동의 일반적인 개요를 표시하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="01bae-116">Azure Data Factory를 처음 접하는 경우 [Azure Data Factory 소개](data-factory-introduction.md)를 읽고 이 문서를 읽기 전에 [첫 번째 데이터 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 자습서를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="01bae-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="01bae-117">구문</span><span class="sxs-lookup"><span data-stu-id="01bae-117">Syntax</span></span>

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a><span data-ttu-id="01bae-118">구문 세부 정보</span><span class="sxs-lookup"><span data-stu-id="01bae-118">Syntax details</span></span>
| <span data-ttu-id="01bae-119">속성</span><span class="sxs-lookup"><span data-stu-id="01bae-119">Property</span></span> | <span data-ttu-id="01bae-120">설명</span><span class="sxs-lookup"><span data-stu-id="01bae-120">Description</span></span> | <span data-ttu-id="01bae-121">필수</span><span class="sxs-lookup"><span data-stu-id="01bae-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="01bae-122">name</span><span class="sxs-lookup"><span data-stu-id="01bae-122">name</span></span> |<span data-ttu-id="01bae-123">작업의 이름</span><span class="sxs-lookup"><span data-stu-id="01bae-123">Name of the activity</span></span> |<span data-ttu-id="01bae-124">예</span><span class="sxs-lookup"><span data-stu-id="01bae-124">Yes</span></span> |
| <span data-ttu-id="01bae-125">설명</span><span class="sxs-lookup"><span data-stu-id="01bae-125">description</span></span> |<span data-ttu-id="01bae-126">작업이 무엇에 사용되는지 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="01bae-127">아니요</span><span class="sxs-lookup"><span data-stu-id="01bae-127">No</span></span> |
| <span data-ttu-id="01bae-128">type</span><span class="sxs-lookup"><span data-stu-id="01bae-128">type</span></span> |<span data-ttu-id="01bae-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="01bae-129">HDinsightPig</span></span> |<span data-ttu-id="01bae-130">예</span><span class="sxs-lookup"><span data-stu-id="01bae-130">Yes</span></span> |
| <span data-ttu-id="01bae-131">inputs</span><span class="sxs-lookup"><span data-stu-id="01bae-131">inputs</span></span> |<span data-ttu-id="01bae-132">Pig 활동에서 사용하는 하나 이상의 입력</span><span class="sxs-lookup"><span data-stu-id="01bae-132">One or more inputs consumed by the Pig activity</span></span> |<span data-ttu-id="01bae-133">아니요</span><span class="sxs-lookup"><span data-stu-id="01bae-133">No</span></span> |
| <span data-ttu-id="01bae-134">outputs</span><span class="sxs-lookup"><span data-stu-id="01bae-134">outputs</span></span> |<span data-ttu-id="01bae-135">Pig 활동에서 생성하는 하나 이상의 출력</span><span class="sxs-lookup"><span data-stu-id="01bae-135">One or more outputs produced by the Pig activity</span></span> |<span data-ttu-id="01bae-136">예</span><span class="sxs-lookup"><span data-stu-id="01bae-136">Yes</span></span> |
| <span data-ttu-id="01bae-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="01bae-137">linkedServiceName</span></span> |<span data-ttu-id="01bae-138">데이터 팩터리에서 연결된 서비스로 등록된 HDInsight 클러스터에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="01bae-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="01bae-139">예</span><span class="sxs-lookup"><span data-stu-id="01bae-139">Yes</span></span> |
| <span data-ttu-id="01bae-140">script</span><span class="sxs-lookup"><span data-stu-id="01bae-140">script</span></span> |<span data-ttu-id="01bae-141">Pig 스크립트 인라인 지정</span><span class="sxs-lookup"><span data-stu-id="01bae-141">Specify the Pig script inline</span></span> |<span data-ttu-id="01bae-142">아니요</span><span class="sxs-lookup"><span data-stu-id="01bae-142">No</span></span> |
| <span data-ttu-id="01bae-143">script path</span><span class="sxs-lookup"><span data-stu-id="01bae-143">script path</span></span> |<span data-ttu-id="01bae-144">Pig 스크립트를 Azure blob 저장소에 저장하고 파일에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-144">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="01bae-145">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="01bae-146">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-146">Both cannot be used together.</span></span> <span data-ttu-id="01bae-147">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="01bae-148">아니요</span><span class="sxs-lookup"><span data-stu-id="01bae-148">No</span></span> |
| <span data-ttu-id="01bae-149">defines</span><span class="sxs-lookup"><span data-stu-id="01bae-149">defines</span></span> |<span data-ttu-id="01bae-150">Pig 스크립트 내에서 참조하기 위해 매개 변수를 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="01bae-150">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="01bae-151">아니요</span><span class="sxs-lookup"><span data-stu-id="01bae-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="01bae-152">예</span><span class="sxs-lookup"><span data-stu-id="01bae-152">Example</span></span>
<span data-ttu-id="01bae-153">회사에서 출시한 게임을 플레이어가 플레이한 시간을 파악하려는 게임 로그 분석의 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-153">Let’s consider an example of game logs analytics where you want to identify the time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="01bae-154">다음 샘플 게임 로그는 쉼표(,)로 구분된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-154">The following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="01bae-155">이 파일에는 ProfileID, SessionStart, Duration, SrcIPAddress 및 GameType 필드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-155">It contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="01bae-156">이 데이터를 처리하는 **Pig 스크립트** 는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-156">The **Pig script** to process this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="01bae-157">데이터 팩터리 파이프라인에서 이 Pig 스크립트를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-157">To execute this Pig script in a Data Factory pipeline, do the following steps:</span></span>

1. <span data-ttu-id="01bae-158">연결된 서비스를 만들어 [자체적인 HDInsight 컴퓨팅 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)를 등록하거나 [주문형 HDInsight 컴퓨팅 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-158">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="01bae-159">이 연결된 서비스를 **HDInsightLinkedService**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="01bae-160">데이터를 호스팅하는 Azure Blob 저장소로의 연결을 구성하기 위해 [연결된 서비스](data-factory-azure-blob-connector.md) 를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-160">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="01bae-161">이 연결된 서비스를 **StorageLinkedService**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="01bae-162">입력 및 출력 데이터를 가리키는 [데이터 집합](data-factory-create-datasets.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-162">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="01bae-163">입력 데이터 집합을 **PigSampleIn**이라고 하고, 출력 데이터 집합을 **PigSampleOut**이라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-163">Let’s call the input dataset **PigSampleIn** and the output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="01bae-164">2단계에서 구성한 Azure Blob 저장소의 파일에 Pig 쿼리를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-164">Copy the Pig query in a file the Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="01bae-165">데이터를 호스트하는 Azure Storage가 쿼리 파일을 호스트하는 Azure Storage와 다른 경우에는 별도의 Azure Storage 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-165">If the Azure storage that hosts the data is different from the one that hosts the query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="01bae-166">활동 구성에서 연결된 서비스를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-166">Refer to the linked service in the activity configuration.</span></span> <span data-ttu-id="01bae-167">그런 다음 **scriptPath**를 사용하여 Pig 스크립트 파일 및 **scriptLinkedService**의 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-167">Use **scriptPath **to specify the path to pig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="01bae-168">**script** 속성을 사용하여 활동 정의에서 Pig 스크립트를 인라인으로 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-168">You can also provide the Pig script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="01bae-169">그러나 이렇게 하면 스크립트의 모든 특수 문자를 이스케이프 처리해야 하므로 디버그 관련 문제가 발생할 수 있기 때문에 이 방식은 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-169">However, we do not recommend this approach as all special characters in the script needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="01bae-170">모법 사례는 4단계를 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-170">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="01bae-171">HDInsightPig 활동이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-171">Create the pipeline with the HDInsightPig activity.</span></span> <span data-ttu-id="01bae-172">이 활동은 HDInsight 클러스터에서 Pig 스크립트를 실행하여 입력 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-172">This activity processes the input data by running Pig script on HDInsight cluster.</span></span>

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. <span data-ttu-id="01bae-173">파이프라인을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-173">Deploy the pipeline.</span></span> <span data-ttu-id="01bae-174">자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01bae-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="01bae-175">데이터 팩터리 모니터링 및 관리 보기를 사용하여 파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-175">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="01bae-176">자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="01bae-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="01bae-177">Pig 스크립트에 대한 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="01bae-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="01bae-178">게임 로그가 Azure Blob 저장소에 매일 수집되고 날짜 및 시간을 기준으로 분할된 폴더에 저장되는 경우의 예를 들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-178">Consider the following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="01bae-179">Pig 스크립트에 매개 변수를 사용하여 런타임 동안 입력 폴더 위치를 동적으로 전달하며 날짜 및 시간으로 분할된 출력을 생성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-179">You want to parameterize the Pig script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="01bae-180">매개 변수가 있는 Pig 스크립트를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-180">To use parameterized Pig script, do the following:</span></span>

* <span data-ttu-id="01bae-181">**defines**에서 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-181">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* <span data-ttu-id="01bae-182">Pig 스크립트에서 다음 예와 같이 '**$parameterName**'을 사용하여 매개 변수를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="01bae-182">In the Pig Script, refer to the parameters using '**$parameterName**' as shown in the following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="01bae-183">참고 항목</span><span class="sxs-lookup"><span data-stu-id="01bae-183">See Also</span></span>
* [<span data-ttu-id="01bae-184">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="01bae-185">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="01bae-186">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="01bae-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="01bae-187">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="01bae-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="01bae-188">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="01bae-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

