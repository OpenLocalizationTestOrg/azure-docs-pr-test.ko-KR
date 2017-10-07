---
title: "하이브 작업-Azure를 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "에-필요 시/사용자 고유의 HDInsight 클러스터에서 하이브 활동에는 Azure 데이터 팩터리 toorun 하이브 쿼리 hello를 사용 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 032400cdb8e8f9873f85b811b4ad7380f4410edf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hive-activity-in-azure-data-factory"></a><span data-ttu-id="22146-103">Azure Data Factory에서 Hive 활동을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="22146-103">Transform data using Hive Activity in Azure Data Factory</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="22146-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="22146-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="22146-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="22146-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="22146-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="22146-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="22146-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="22146-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="22146-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="22146-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="22146-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="22146-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="22146-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="22146-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="22146-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="22146-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="22146-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="22146-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="22146-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="22146-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="22146-114">Data Factory에 HDInsight Hive 활동 hello [파이프라인](data-factory-create-pipelines.md) 에서 하이브 쿼리를 실행 [고유한](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-114">hello HDInsight Hive activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Hive queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="22146-115">Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="22146-116">새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="22146-117">구문</span><span class="sxs-lookup"><span data-stu-id="22146-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="22146-118">구문 세부 정보</span><span class="sxs-lookup"><span data-stu-id="22146-118">Syntax details</span></span>
| <span data-ttu-id="22146-119">속성</span><span class="sxs-lookup"><span data-stu-id="22146-119">Property</span></span> | <span data-ttu-id="22146-120">설명</span><span class="sxs-lookup"><span data-stu-id="22146-120">Description</span></span> | <span data-ttu-id="22146-121">필수</span><span class="sxs-lookup"><span data-stu-id="22146-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22146-122">name</span><span class="sxs-lookup"><span data-stu-id="22146-122">name</span></span> |<span data-ttu-id="22146-123">Hello 활동의 이름</span><span class="sxs-lookup"><span data-stu-id="22146-123">Name of hello activity</span></span> |<span data-ttu-id="22146-124">예</span><span class="sxs-lookup"><span data-stu-id="22146-124">Yes</span></span> |
| <span data-ttu-id="22146-125">설명</span><span class="sxs-lookup"><span data-stu-id="22146-125">description</span></span> |<span data-ttu-id="22146-126">어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22146-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="22146-127">아니요</span><span class="sxs-lookup"><span data-stu-id="22146-127">No</span></span> |
| <span data-ttu-id="22146-128">type</span><span class="sxs-lookup"><span data-stu-id="22146-128">type</span></span> |<span data-ttu-id="22146-129">HDinsightHive</span><span class="sxs-lookup"><span data-stu-id="22146-129">HDinsightHive</span></span> |<span data-ttu-id="22146-130">예</span><span class="sxs-lookup"><span data-stu-id="22146-130">Yes</span></span> |
| <span data-ttu-id="22146-131">inputs</span><span class="sxs-lookup"><span data-stu-id="22146-131">inputs</span></span> |<span data-ttu-id="22146-132">Hello Hive 활동에서 사용 하는 입력</span><span class="sxs-lookup"><span data-stu-id="22146-132">Inputs consumed by hello Hive activity</span></span> |<span data-ttu-id="22146-133">아니요</span><span class="sxs-lookup"><span data-stu-id="22146-133">No</span></span> |
| <span data-ttu-id="22146-134">outputs</span><span class="sxs-lookup"><span data-stu-id="22146-134">outputs</span></span> |<span data-ttu-id="22146-135">Hello Hive 작업에서 생성 된 출력</span><span class="sxs-lookup"><span data-stu-id="22146-135">Outputs produced by hello Hive activity</span></span> |<span data-ttu-id="22146-136">예</span><span class="sxs-lookup"><span data-stu-id="22146-136">Yes</span></span> |
| <span data-ttu-id="22146-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="22146-137">linkedServiceName</span></span> |<span data-ttu-id="22146-138">Data Factory에 연결 된 서비스로 등록 toohello HDInsight 클러스터를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="22146-139">예</span><span class="sxs-lookup"><span data-stu-id="22146-139">Yes</span></span> |
| <span data-ttu-id="22146-140">script</span><span class="sxs-lookup"><span data-stu-id="22146-140">script</span></span> |<span data-ttu-id="22146-141">Hello Hive 스크립트를 인라인으로 지정</span><span class="sxs-lookup"><span data-stu-id="22146-141">Specify hello Hive script inline</span></span> |<span data-ttu-id="22146-142">아니요</span><span class="sxs-lookup"><span data-stu-id="22146-142">No</span></span> |
| <span data-ttu-id="22146-143">script path</span><span class="sxs-lookup"><span data-stu-id="22146-143">script path</span></span> |<span data-ttu-id="22146-144">저장소 hello 하이브 스크립트에는 Azure blob 저장소에 있으며 hello toohello 파일 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-144">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="22146-145">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="22146-146">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="22146-146">Both cannot be used together.</span></span> <span data-ttu-id="22146-147">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="22146-148">아니요</span><span class="sxs-lookup"><span data-stu-id="22146-148">No</span></span> |
| <span data-ttu-id="22146-149">defines</span><span class="sxs-lookup"><span data-stu-id="22146-149">defines</span></span> |<span data-ttu-id="22146-150">매개 변수를 'hiveconf'를 사용 하 여 hello 하이브 스크립트 내에서 참조 하는 것에 대 한 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="22146-150">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="22146-151">아니요</span><span class="sxs-lookup"><span data-stu-id="22146-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="22146-152">예제</span><span class="sxs-lookup"><span data-stu-id="22146-152">Example</span></span>
<span data-ttu-id="22146-153">살펴보겠습니다 게임의 예 분석 하려는 회사에서 실행 되는 게임을 재생 하는 사용자가 소모 tooidentify hello 시간을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by users playing games launched by your company.</span></span> 

<span data-ttu-id="22146-154">hello 다음 로그는는 쉼표가 샘플 게임 로그 (`,`) 분리 하 고 다음 필드 – 프로필 Id, SessionStart, 기간, SrcIPAddress, 및 게임 종류 hello가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22146-154">hello following log is a sample game log, which is comma (`,`) separated and contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="22146-155">hello **하이브 스크립트에** tooprocess이이 데이터:</span><span class="sxs-lookup"><span data-stu-id="22146-155">hello **Hive script** tooprocess this data:</span></span>

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

<span data-ttu-id="22146-156">toodo hello 다음 필요한 tooexecute 데이터 팩터리 파이프라인에서이 하이브 스크립트를</span><span class="sxs-lookup"><span data-stu-id="22146-156">tooexecute this Hive script in a Data Factory pipeline, you need toodo hello following</span></span>

1. <span data-ttu-id="22146-157">연결 된 서비스 tooregister 만들기 [고유한 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 구성 또는 [주문형 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-157">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="22146-158">이 연결된 서비스를 "HDInsightLinkedService"라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22146-158">Let’s call this linked service “HDInsightLinkedService”.</span></span>
2. <span data-ttu-id="22146-159">만들기는 [연결 된 서비스](data-factory-azure-blob-connector.md) tooconfigure hello 연결 tooAzure Blob 저장소 hello 데이터를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-159">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="22146-160">이 연결된 서비스를 "StorageLinkedService"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-160">Let’s call this linked service “StorageLinkedService”</span></span>
3. <span data-ttu-id="22146-161">만들 [데이터 집합](data-factory-create-datasets.md) toohello 입력과 hello를 가리키는 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-161">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="22146-162">Hello 입력된 데이터 집합 "HiveSampleIn"를 호출 하 고 출력 데이터 집합 "HiveSampleOut" hello 하겠습니다</span><span class="sxs-lookup"><span data-stu-id="22146-162">Let’s call hello input dataset “HiveSampleIn” and hello output dataset “HiveSampleOut”</span></span>
4. <span data-ttu-id="22146-163">파일 tooAzure 2 단계에서 구성 된 Blob 저장소로 hello 하이브 쿼리를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-163">Copy hello Hive query as a file tooAzure Blob Storage configured in step #2.</span></span> <span data-ttu-id="22146-164">hello 데이터를 호스팅하기 위해 hello 저장소가 쿼리 파일을 호스팅 하나 hello와에서 다른 경우 별도 Azure 저장소 연결 서비스 만들고 hello 활동에서 tooit 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-164">if hello storage for hosting hello data is different from hello one hosting this query file, create a separate Azure Storage linked service and refer tooit in hello activity.</span></span> <span data-ttu-id="22146-165">사용 하 여 * * scriptPath * * toospecify hello toohive 쿼리 파일 경로 및 **scriptLinkedService** toospecify hello hello 스크립트 파일을 포함 하는 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-165">Use **scriptPath **toospecify hello path toohive query file and **scriptLinkedService** toospecify hello Azure storage that contains hello script file.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="22146-166">Hello를 사용 하 여 hello Hive 스크립트를 인라인으로 hello 활동 정의에서 제공할 수도 있습니다 **스크립트** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-166">You can also provide hello Hive script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="22146-167">권장 하지는 않습니다이 방법은 hello JSON 문서 내에서 hello 스크립트에 모든 특수 문자가 이스케이프 toobe 필요 하 고 원인을 문제를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22146-167">We do not recommend this approach as all special characters in hello script within hello JSON document needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="22146-168">hello 최상의 방법 #4 toofollow 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="22146-168">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="22146-169">Hello HDInsightHive 활동으로 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="22146-169">Create a pipeline with hello HDInsightHive activity.</span></span> <span data-ttu-id="22146-170">hello 활동 프로세스/hello 데이터 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-170">hello activity processes/transforms hello data.</span></span>

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
6. <span data-ttu-id="22146-171">Hello 파이프라인을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-171">Deploy hello pipeline.</span></span> <span data-ttu-id="22146-172">자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22146-172">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="22146-173">Hello 데이터 팩터리 모니터링을 사용 하 여 hello 파이프라인 및 관리 뷰를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-173">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="22146-174">자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22146-174">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span> 

## <a name="specifying-parameters-for-a-hive-script"></a><span data-ttu-id="22146-175">Hive 스크립트에 대한 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="22146-175">Specifying parameters for a Hive script</span></span>
<span data-ttu-id="22146-176">이 예에서 게임 로그는 Azure Blob Storage에 매일 수집되고 날짜 및 시간으로 분할된 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22146-176">In this example, game logs are ingested daily into Azure Blob Storage and are stored in a folder partitioned with date and time.</span></span> <span data-ttu-id="22146-177">Tooparameterize hello 하이브 스크립트 및 런타임 시 hello 입력된 폴더 위치를 동적으로 전달할 한도 날짜 및 시간을 사용 하 여 분할 하는 hello 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-177">You want tooparameterize hello Hive script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="22146-178">toouse 하이브 스크립트 매개 변수가 있는 hello 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-178">toouse parameterized Hive script, do hello following</span></span>

* <span data-ttu-id="22146-179">Hello 매개 변수에서 정의 **정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-179">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="22146-180">Hive 스크립트 hello 참조 toohello 매개 변수를 사용 하 여 **${hiveconf: parametername}**합니다.</span><span class="sxs-lookup"><span data-stu-id="22146-180">In hello Hive Script, refer toohello parameter using **${hiveconf:parameterName}**.</span></span> 
  
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
## <a name="see-also"></a><span data-ttu-id="22146-181">참고 항목</span><span class="sxs-lookup"><span data-stu-id="22146-181">See Also</span></span>
* [<span data-ttu-id="22146-182">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="22146-182">Pig Activity</span></span>](data-factory-pig-activity.md)
* [<span data-ttu-id="22146-183">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="22146-183">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="22146-184">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="22146-184">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="22146-185">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="22146-185">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="22146-186">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="22146-186">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

