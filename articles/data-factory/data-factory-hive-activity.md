---
title: "Hive 활동을 사용하여 데이터 변환 - Azure | Microsoft Docs"
description: "Azure 데이터 공장에서 Hive 활동을 사용하여 필요 시/사용자 고유의 HDInsight 클러스터에서 Hive 쿼리를 실행하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 80083218-743e-4da8-bdd2-60d1c77b1227
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: a3e9b2d0a8c851939acd228d8086ddfc9f38a4c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="4fe2f-103">Azure Data Factory에서 Hive 활동을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="4fe2f-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4fe2f-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4fe2f-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4fe2f-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4fe2f-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4fe2f-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4fe2f-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4fe2f-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4fe2f-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4fe2f-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4fe2f-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4fe2f-114">Data Factory [파이프라인](data-factory-create-pipelines.md)에서 HDInsight Hive 작업은 [사용자 고유](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터의 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-114">The HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4fe2f-115">이 문서는 데이터 변환 및 지원되는 변환 활동의 일반적인 개요를 표시하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 문서에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-115">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="4fe2f-116">Azure Data Factory를 처음 접하는 경우 [Azure Data Factory 소개](data-factory-introduction.md)를 읽고 이 문서를 읽기 전에 [첫 번째 데이터 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 자습서를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-116">If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](data-factory-introduction.md) and do the tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="4fe2f-117">구문</span><span class="sxs-lookup"><span data-stu-id="4fe2f-117">Syntax</span></span>

```JSON
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
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
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```
## <a name="syntax-details"></a><span data-ttu-id="4fe2f-118">구문 세부 정보</span><span class="sxs-lookup"><span data-stu-id="4fe2f-118">Syntax details</span></span>
| <span data-ttu-id="4fe2f-119">속성</span><span class="sxs-lookup"><span data-stu-id="4fe2f-119">Property</span></span> | <span data-ttu-id="4fe2f-120">설명</span><span class="sxs-lookup"><span data-stu-id="4fe2f-120">Description</span></span> | <span data-ttu-id="4fe2f-121">필수</span><span class="sxs-lookup"><span data-stu-id="4fe2f-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4fe2f-122">name</span><span class="sxs-lookup"><span data-stu-id="4fe2f-122">name</span></span> |<span data-ttu-id="4fe2f-123">작업의 이름</span><span class="sxs-lookup"><span data-stu-id="4fe2f-123">Name of the activity</span></span> |<span data-ttu-id="4fe2f-124">예</span><span class="sxs-lookup"><span data-stu-id="4fe2f-124">Yes</span></span> |
| <span data-ttu-id="4fe2f-125">설명</span><span class="sxs-lookup"><span data-stu-id="4fe2f-125">description</span></span> |<span data-ttu-id="4fe2f-126">작업이 무엇에 사용되는지 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-126">Text describing what the activity is used for</span></span> |<span data-ttu-id="4fe2f-127">아니요</span><span class="sxs-lookup"><span data-stu-id="4fe2f-127">No</span></span> |
| <span data-ttu-id="4fe2f-128">type</span><span class="sxs-lookup"><span data-stu-id="4fe2f-128">type</span></span> |<span data-ttu-id="4fe2f-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="4fe2f-129">HDinsightHive</span></span> |<span data-ttu-id="4fe2f-130">예</span><span class="sxs-lookup"><span data-stu-id="4fe2f-130">Yes</span></span> |
| <span data-ttu-id="4fe2f-131">inputs</span><span class="sxs-lookup"><span data-stu-id="4fe2f-131">inputs</span></span> |<span data-ttu-id="4fe2f-132">Hive 활동에서 사용된 입력</span><span class="sxs-lookup"><span data-stu-id="4fe2f-132">Inputs consumed by the Hive activity</span></span> |<span data-ttu-id="4fe2f-133">아니요</span><span class="sxs-lookup"><span data-stu-id="4fe2f-133">No</span></span> |
| <span data-ttu-id="4fe2f-134">outputs</span><span class="sxs-lookup"><span data-stu-id="4fe2f-134">outputs</span></span> |<span data-ttu-id="4fe2f-135">Hive 활동에서 생성된 출력</span><span class="sxs-lookup"><span data-stu-id="4fe2f-135">Outputs produced by the Hive activity</span></span> |<span data-ttu-id="4fe2f-136">예</span><span class="sxs-lookup"><span data-stu-id="4fe2f-136">Yes</span></span> |
| <span data-ttu-id="4fe2f-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4fe2f-137">linkedServiceName</span></span> |<span data-ttu-id="4fe2f-138">데이터 팩터리에서 연결된 서비스로 등록된 HDInsight 클러스터에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="4fe2f-138">Reference to the HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="4fe2f-139">예</span><span class="sxs-lookup"><span data-stu-id="4fe2f-139">Yes</span></span> |
| <span data-ttu-id="4fe2f-140">script</span><span class="sxs-lookup"><span data-stu-id="4fe2f-140">script</span></span> |<span data-ttu-id="4fe2f-141">Hive 스크립트 인라인 지정</span><span class="sxs-lookup"><span data-stu-id="4fe2f-141">Specify the Hive script inline</span></span> |<span data-ttu-id="4fe2f-142">아니요</span><span class="sxs-lookup"><span data-stu-id="4fe2f-142">No</span></span> |
| <span data-ttu-id="4fe2f-143">script path</span><span class="sxs-lookup"><span data-stu-id="4fe2f-143">script path</span></span> |<span data-ttu-id="4fe2f-144">Hive 스크립트를 Azure blob 저장소에 저장하고 파일에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-144">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="4fe2f-145">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="4fe2f-146">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-146">Both cannot be used together.</span></span> <span data-ttu-id="4fe2f-147">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-147">The file name is case-sensitive.</span></span> |<span data-ttu-id="4fe2f-148">아니요</span><span class="sxs-lookup"><span data-stu-id="4fe2f-148">No</span></span> |
| <span data-ttu-id="4fe2f-149">defines</span><span class="sxs-lookup"><span data-stu-id="4fe2f-149">defines</span></span> |<span data-ttu-id="4fe2f-150">'hiveconf'를 사용하는 Hive 스크립트 내에서 참조하기 위해 매개 변수를 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="4fe2f-150">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="4fe2f-151">아니요</span><span class="sxs-lookup"><span data-stu-id="4fe2f-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="4fe2f-152">예</span><span class="sxs-lookup"><span data-stu-id="4fe2f-152">Example</span></span>
<span data-ttu-id="4fe2f-153">회사에서 출시한 게임을 사용자가 플레이한 시간을 파악하려는 게임 로그 분석의 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-153">Let’s consider an example of game logs analytics where you want to identify the time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="4fe2f-154">다음 로그는 쉼표(`,`)로 구분되고 ProfileID, SessionStart, Duration, SrcIPAddress 및 GameType 필드를 포함하는 샘플 게임 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-154">The following log is a sample game log, which is comma (`,`) separated and contains the following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="4fe2f-155">이 데이터를 처리하는 **Hive 스크립트**는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-155">The **Hive script** to process this data:</span></span>

```
DROP TABLE IF EXISTS HiveSampleIn; 
CREATE EXTERNAL TABLE HiveSampleIn 
(
    ProfileID        string, 
    SessionStart     string, 
    Duration         int, 
    SrcIPAddress     string, 
    GameType         string
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/samplein/'; 

DROP TABLE IF EXISTS HiveSampleOut; 
CREATE EXTERNAL TABLE HiveSampleOut 
(    
    ProfileID     string, 
    Duration     int
) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION 'wasb://adfwalkthrough@<storageaccount>.blob.core.windows.net/sampleout/';

INSERT OVERWRITE TABLE HiveSampleOut
Select 
    ProfileID,
    SUM(Duration)
FROM HiveSampleIn Group by ProfileID
```

<span data-ttu-id="4fe2f-156">데이터 팩터리 파이프라인에서 이 Hive 스크립트를 실행하려면 다음을 수행해야 합니다</span><span class="sxs-lookup"><span data-stu-id="4fe2f-156">To execute this Hive script in a Data Factory pipeline, you need to do the following</span></span>

1. <span data-ttu-id="4fe2f-157">연결된 서비스를 만들어 [자체적인 HDInsight 컴퓨팅 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)를 등록하거나 [주문형 HDInsight 컴퓨팅 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-157">Create a linked service to register [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="4fe2f-158">이 연결된 서비스를 "HDInsightLinkedService"라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="4fe2f-159">[연결된 서비스](data-factory-azure-blob-connector.md)를 만들어 데이터를 호스팅하는 Azure Blob 저장소에 연결을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-159">Create a [linked service](data-factory-azure-blob-connector.md) to configure the connection to Azure Blob storage hosting the data.</span></span> <span data-ttu-id="4fe2f-160">이 연결된 서비스를 "StorageLinkedService"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="4fe2f-161">입력 및 출력 데이터를 가리키는 [데이터 집합](data-factory-create-datasets.md)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-161">Create [datasets](data-factory-create-datasets.md) pointing to the input and the output data.</span></span> <span data-ttu-id="4fe2f-162">입력 데이터 집합을 "HiveSampleIn"라고 하고 출력 데이터 집합을 "HiveSampleOut"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-162">Let’s call the input dataset “HiveSampleIn” and the output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="4fe2f-163">\#2단계에서 구성된 Azure Blob Storage에 Hive 쿼리를 파일로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-163">Copy the Hive query as a file to Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="4fe2f-164">데이터를 호스팅하는 저장소가 이 쿼리 파일을 호스트하는 저장소와 다른 경우 서비스에 연결된 별도 Azure 저장소를 만들고 작업에서 이를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-164">if the storage for hosting the data is different from the one hosting this query file, create a separate Azure Storage linked service and refer to it in the activity.</span></span> <span data-ttu-id="4fe2f-165">**scriptPath**를 사용하여 hive 쿼리 파일에 대한 경로를 지정하고 **scriptLinkedService**를 사용하여 스크립트 파일을 포함하는 Azure 저장소를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-165">Use **scriptPath **to specify the path to hive query file and **scriptLinkedService** to specify the Azure storage that contains the script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="4fe2f-166">**script** 속성을 사용하여 활동 정의에서 Hive 스크립트를 인라인으로 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-166">You can also provide the Hive script inline in the activity definition by using the **script** property.</span></span> <span data-ttu-id="4fe2f-167">이렇게 하면 JSON 문서 내의 스크립트 모든 특수 문자를 이스케이프 처리해야 하므로 디버그 관련 문제가 발생할 수 있기 때문에 이 방식은 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-167">We do not recommend this approach as all special characters in the script within the JSON document needs to be escaped and may cause debugging issues.</span></span> <span data-ttu-id="4fe2f-168">모법 사례는 4단계를 수행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-168">The best practice is to follow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="4fe2f-169">HDInsightHive 활동이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-169">Create a pipeline with the HDInsightHive activity.</span></span> <span data-ttu-id="4fe2f-170">작업은 데이터를 프로세스/변환합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-170">The activity processes/transforms the data.</span></span>

    ```JSON   
    {   
        "name": "HiveActivitySamplePipeline",
        "properties": {
        "activities": [
            {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                {
                    "name": "HiveSampleIn"
                }
                ],
                "outputs": [
                {
                    "name": "HiveSampleOut"
                }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
            ]
        }
    }
    ```
6. <span data-ttu-id="4fe2f-171">파이프라인을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-171">Deploy the pipeline.</span></span> <span data-ttu-id="4fe2f-172">자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="4fe2f-173">데이터 팩터리 모니터링 및 관리 보기를 사용하여 파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-173">Monitor the pipeline using the data factory monitoring and management views.</span></span> <span data-ttu-id="4fe2f-174">자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="4fe2f-175">Hive 스크립트에 대한 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="4fe2f-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="4fe2f-176">이 예에서 게임 로그는 Azure Blob Storage에 매일 수집되고 날짜 및 시간으로 분할된 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="4fe2f-177">Hive 스크립트를 매개 변수화하고 런타임 동안 입력 폴더 위치를 동적으로 전달하며 날짜 및 시간으로 분할된 출력을 생성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-177">You want to parameterize the Hive script and pass the input folder location dynamically during runtime and also produce the output partitioned with date and time.</span></span>

<span data-ttu-id="4fe2f-178">매개 변수가 있는 Hive 스크립트를 사용하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-178">To use parameterized Hive script, do the following</span></span>

* <span data-ttu-id="4fe2f-179">**defines**에서 매개 변수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-179">Define the parameters in **defines**.</span></span>

    ```JSON  
    {
        "name": "HiveActivitySamplePipeline",
          "properties": {
        "activities": [
             {
                "name": "HiveActivitySample",
                "type": "HDInsightHive",
                "inputs": [
                      {
                        "name": "HiveSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "HiveSampleOut"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      },
                       "scheduler": {
                          "frequency": "Hour",
                          "interval": 1
                    }
                }
              }
        ]
      }
    }
    ```
* <span data-ttu-id="4fe2f-180">Hive 스크립트에서 **${hiveconf:parameterName}**를 사용하는 매개 변수를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe2f-180">In the Hive Script, refer to the parameter using **${hiveconf:parameterName}**.</span></span> 
  
    ```
    DROP TABLE IF EXISTS HiveSampleIn; 
    CREATE EXTERNAL TABLE HiveSampleIn 
    (
        ProfileID     string, 
        SessionStart     string, 
        Duration     int, 
        SrcIPAddress     string, 
        GameType     string
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Input}'; 

    DROP TABLE IF EXISTS HiveSampleOut; 
    CREATE EXTERNAL TABLE HiveSampleOut 
    (
        ProfileID     string, 
        Duration     int
    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

    INSERT OVERWRITE TABLE HiveSampleOut
    Select 
        ProfileID,
        SUM(Duration)
    FROM HiveSampleIn Group by ProfileID
    ```
## <a name="see-also"></a><span data-ttu-id="4fe2f-181">참고 항목</span><span class="sxs-lookup"><span data-stu-id="4fe2f-181">See Also</span></span>
* [<span data-ttu-id="4fe2f-182">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="4fe2f-183">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="4fe2f-184">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="4fe2f-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="4fe2f-185">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="4fe2f-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="4fe2f-186">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="4fe2f-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

