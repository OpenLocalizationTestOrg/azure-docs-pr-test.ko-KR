---
title: "Azure 데이터 팩터리에서 Pig 작업을 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "에-필요 시/사용자 고유의 HDInsight 클러스터에서 Pig 작업은 Azure 데이터 팩터리 toorun Pig 스크립트에 hello를 사용 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a><span data-ttu-id="2ee9a-103">Azure Data Factory에서 Pig 활동을 사용하여 데이터 변환</span><span class="sxs-lookup"><span data-stu-id="2ee9a-103">Transform data using Pig Activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2ee9a-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="2ee9a-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2ee9a-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2ee9a-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2ee9a-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2ee9a-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2ee9a-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2ee9a-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2ee9a-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2ee9a-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="2ee9a-114">Data Factory에 HDInsight Pig 작업 hello [파이프라인](data-factory-create-pipelines.md) 에서 Pig 쿼리를 실행 [고유한](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-114">hello HDInsight Pig activity in a Data Factory [pipeline](data-factory-create-pipelines.md) executes Pig queries on [your own](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or [on-demand](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2ee9a-115">Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-115">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities.</span></span>

> [!NOTE] 
> <span data-ttu-id="2ee9a-116">새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-116">If you are new tooAzure Data Factory, read through [Introduction tooAzure Data Factory](data-factory-introduction.md) and do hello tutorial: [Build your first data pipeline](data-factory-build-your-first-pipeline.md) before reading this article.</span></span> 

## <a name="syntax"></a><span data-ttu-id="2ee9a-117">구문</span><span class="sxs-lookup"><span data-stu-id="2ee9a-117">Syntax</span></span>

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
## <a name="syntax-details"></a><span data-ttu-id="2ee9a-118">구문 세부 정보</span><span class="sxs-lookup"><span data-stu-id="2ee9a-118">Syntax details</span></span>
| <span data-ttu-id="2ee9a-119">속성</span><span class="sxs-lookup"><span data-stu-id="2ee9a-119">Property</span></span> | <span data-ttu-id="2ee9a-120">설명</span><span class="sxs-lookup"><span data-stu-id="2ee9a-120">Description</span></span> | <span data-ttu-id="2ee9a-121">필수</span><span class="sxs-lookup"><span data-stu-id="2ee9a-121">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2ee9a-122">name</span><span class="sxs-lookup"><span data-stu-id="2ee9a-122">name</span></span> |<span data-ttu-id="2ee9a-123">Hello 활동의 이름</span><span class="sxs-lookup"><span data-stu-id="2ee9a-123">Name of hello activity</span></span> |<span data-ttu-id="2ee9a-124">예</span><span class="sxs-lookup"><span data-stu-id="2ee9a-124">Yes</span></span> |
| <span data-ttu-id="2ee9a-125">설명</span><span class="sxs-lookup"><span data-stu-id="2ee9a-125">description</span></span> |<span data-ttu-id="2ee9a-126">어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-126">Text describing what hello activity is used for</span></span> |<span data-ttu-id="2ee9a-127">아니요</span><span class="sxs-lookup"><span data-stu-id="2ee9a-127">No</span></span> |
| <span data-ttu-id="2ee9a-128">type</span><span class="sxs-lookup"><span data-stu-id="2ee9a-128">type</span></span> |<span data-ttu-id="2ee9a-129">HDinsightPig</span><span class="sxs-lookup"><span data-stu-id="2ee9a-129">HDinsightPig</span></span> |<span data-ttu-id="2ee9a-130">예</span><span class="sxs-lookup"><span data-stu-id="2ee9a-130">Yes</span></span> |
| <span data-ttu-id="2ee9a-131">inputs</span><span class="sxs-lookup"><span data-stu-id="2ee9a-131">inputs</span></span> |<span data-ttu-id="2ee9a-132">하나 이상의 입력 사용한 hello Pig 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-132">One or more inputs consumed by hello Pig activity</span></span> |<span data-ttu-id="2ee9a-133">아니요</span><span class="sxs-lookup"><span data-stu-id="2ee9a-133">No</span></span> |
| <span data-ttu-id="2ee9a-134">outputs</span><span class="sxs-lookup"><span data-stu-id="2ee9a-134">outputs</span></span> |<span data-ttu-id="2ee9a-135">Pig 작업 hello에서 하나 이상의 출력 생성</span><span class="sxs-lookup"><span data-stu-id="2ee9a-135">One or more outputs produced by hello Pig activity</span></span> |<span data-ttu-id="2ee9a-136">예</span><span class="sxs-lookup"><span data-stu-id="2ee9a-136">Yes</span></span> |
| <span data-ttu-id="2ee9a-137">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="2ee9a-137">linkedServiceName</span></span> |<span data-ttu-id="2ee9a-138">Data Factory에 연결 된 서비스로 등록 toohello HDInsight 클러스터를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-138">Reference toohello HDInsight cluster registered as a linked service in Data Factory</span></span> |<span data-ttu-id="2ee9a-139">예</span><span class="sxs-lookup"><span data-stu-id="2ee9a-139">Yes</span></span> |
| <span data-ttu-id="2ee9a-140">script</span><span class="sxs-lookup"><span data-stu-id="2ee9a-140">script</span></span> |<span data-ttu-id="2ee9a-141">Hello Pig 스크립트를 인라인으로 지정</span><span class="sxs-lookup"><span data-stu-id="2ee9a-141">Specify hello Pig script inline</span></span> |<span data-ttu-id="2ee9a-142">아니요</span><span class="sxs-lookup"><span data-stu-id="2ee9a-142">No</span></span> |
| <span data-ttu-id="2ee9a-143">script path</span><span class="sxs-lookup"><span data-stu-id="2ee9a-143">script path</span></span> |<span data-ttu-id="2ee9a-144">Azure blob 저장소에 hello Pig 스크립트를 저장 하 고 hello toohello 파일 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-144">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="2ee9a-145">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-145">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="2ee9a-146">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-146">Both cannot be used together.</span></span> <span data-ttu-id="2ee9a-147">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-147">hello file name is case-sensitive.</span></span> |<span data-ttu-id="2ee9a-148">아니요</span><span class="sxs-lookup"><span data-stu-id="2ee9a-148">No</span></span> |
| <span data-ttu-id="2ee9a-149">defines</span><span class="sxs-lookup"><span data-stu-id="2ee9a-149">defines</span></span> |<span data-ttu-id="2ee9a-150">키/값 쌍으로 hello Pig 스크립트 내에서 참조 하는 것에 대 한 매개 변수를 지정</span><span class="sxs-lookup"><span data-stu-id="2ee9a-150">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="2ee9a-151">아니요</span><span class="sxs-lookup"><span data-stu-id="2ee9a-151">No</span></span> |

## <a name="example"></a><span data-ttu-id="2ee9a-152">예제</span><span class="sxs-lookup"><span data-stu-id="2ee9a-152">Example</span></span>
<span data-ttu-id="2ee9a-153">살펴보겠습니다 게임의 예가 기록 하려는 회사에서 시작 하는 게임을 즐기고 플레이어에서 사용한 tooidentify hello 시간 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-153">Let’s consider an example of game logs analytics where you want tooidentify hello time spent by players playing games launched by your company.</span></span>

<span data-ttu-id="2ee9a-154">다음 샘플 게임 로그 hello 쉼표 (,) 구분 된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-154">hello following sample game log is a comma (,) separated file.</span></span> <span data-ttu-id="2ee9a-155">다음 필드 – 프로필 Id, SessionStart, 기간, SrcIPAddress, 및 게임 종류 hello를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-155">It contains hello following fields – ProfileID, SessionStart, Duration, SrcIPAddress, and GameType.</span></span>

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

<span data-ttu-id="2ee9a-156">hello **Pig 스크립트** tooprocess이이 데이터:</span><span class="sxs-lookup"><span data-stu-id="2ee9a-156">hello **Pig script** tooprocess this data:</span></span>

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

<span data-ttu-id="2ee9a-157">데이터 팩터리 파이프라인에서이 Pig 스크립트 tooexecute 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-157">tooexecute this Pig script in a Data Factory pipeline, do hello following steps:</span></span>

1. <span data-ttu-id="2ee9a-158">연결 된 서비스 tooregister 만들기 [고유한 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 구성 또는 [주문형 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-158">Create a linked service tooregister [your own HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) or configure [on-demand HDInsight compute cluster](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span></span> <span data-ttu-id="2ee9a-159">이 연결된 서비스를 **HDInsightLinkedService**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-159">Let’s call this linked service **HDInsightLinkedService**.</span></span>
2. <span data-ttu-id="2ee9a-160">만들기는 [연결 된 서비스](data-factory-azure-blob-connector.md) tooconfigure hello 연결 tooAzure Blob 저장소 hello 데이터를 호스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-160">Create a [linked service](data-factory-azure-blob-connector.md) tooconfigure hello connection tooAzure Blob storage hosting hello data.</span></span> <span data-ttu-id="2ee9a-161">이 연결된 서비스를 **StorageLinkedService**라고 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-161">Let’s call this linked service **StorageLinkedService**.</span></span>
3. <span data-ttu-id="2ee9a-162">만들 [데이터 집합](data-factory-create-datasets.md) toohello 입력과 hello를 가리키는 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-162">Create [datasets](data-factory-create-datasets.md) pointing toohello input and hello output data.</span></span> <span data-ttu-id="2ee9a-163">입력된 데이터 집합 hello 부르겠습니다 **PigSampleIn** hello 출력 데이터 집합 및 **PigSampleOut**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-163">Let’s call hello input dataset **PigSampleIn** and hello output dataset **PigSampleOut**.</span></span>
4. <span data-ttu-id="2ee9a-164">Hello Pig 쿼리 파일 hello 2 단계에서 구성 된 Azure Blob 저장소에에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-164">Copy hello Pig query in a file hello Azure Blob Storage configured in step #2.</span></span> <span data-ttu-id="2ee9a-165">Hello hello 데이터를 호스팅하는 Azure 저장소 hello 쿼리 파일을 호스팅하는 하나 hello와에서 다른 경우에 별도 Azure 저장소 연결 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-165">If hello Azure storage that hosts hello data is different from hello one that hosts hello query file, create a separate Azure Storage linked service.</span></span> <span data-ttu-id="2ee9a-166">Hello 작업 구성에서 toohello 연결 된 서비스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-166">Refer toohello linked service in hello activity configuration.</span></span> <span data-ttu-id="2ee9a-167">사용 하 여 * * scriptPath * * toospecify hello toopig 스크립트 파일 경로 및 **scriptLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-167">Use **scriptPath **toospecify hello path toopig script file and **scriptLinkedService**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2ee9a-168">Hello를 사용 하 여 hello Pig 스크립트를 인라인으로 hello 활동 정의에서 제공할 수도 있습니다 **스크립트** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-168">You can also provide hello Pig script inline in hello activity definition by using hello **script** property.</span></span> <span data-ttu-id="2ee9a-169">그러나 권장 하지는 않습니다이 방법으로 hello 스크립트에 모든 특수 문자 이스케이프 toobe 하며 디버깅 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-169">However, we do not recommend this approach as all special characters in hello script needs toobe escaped and may cause debugging issues.</span></span> <span data-ttu-id="2ee9a-170">hello 최상의 방법 #4 toofollow 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-170">hello best practice is toofollow step #4.</span></span>
   > 
   > 
5. <span data-ttu-id="2ee9a-171">Hello HDInsightPig 활동으로 hello 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-171">Create hello pipeline with hello HDInsightPig activity.</span></span> <span data-ttu-id="2ee9a-172">이 작업은 HDInsight 클러스터에서 Pig 스크립트를 실행 하 여 hello 입력된 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-172">This activity processes hello input data by running Pig script on HDInsight cluster.</span></span>

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
6. <span data-ttu-id="2ee9a-173">Hello 파이프라인을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-173">Deploy hello pipeline.</span></span> <span data-ttu-id="2ee9a-174">자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-174">See [Creating pipelines](data-factory-create-pipelines.md) article for details.</span></span> 
7. <span data-ttu-id="2ee9a-175">Hello 데이터 팩터리 모니터링을 사용 하 여 hello 파이프라인 및 관리 뷰를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-175">Monitor hello pipeline using hello data factory monitoring and management views.</span></span> <span data-ttu-id="2ee9a-176">자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-176">See [Monitoring and manage Data Factory pipelines](data-factory-monitor-manage-pipelines.md) article for details.</span></span>

## <a name="specifying-parameters-for-a-pig-script"></a><span data-ttu-id="2ee9a-177">Pig 스크립트에 대한 매개 변수 지정</span><span class="sxs-lookup"><span data-stu-id="2ee9a-177">Specifying parameters for a Pig script</span></span>
<span data-ttu-id="2ee9a-178">다음 예제는 hello 고려: 게임 로그는 Azure Blob 저장소에 매일 수집 된 및 분할된에 따라 날짜 및 시간 폴더에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-178">Consider hello following example: game logs are ingested daily into Azure Blob Storage and stored in a folder partitioned based on date and time.</span></span> <span data-ttu-id="2ee9a-179">Tooparameterize hello Pig 스크립트 및 런타임 시 hello 입력된 폴더 위치를 동적으로 전달할 한도 날짜 및 시간을 사용 하 여 분할 하는 hello 출력을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-179">You want tooparameterize hello Pig script and pass hello input folder location dynamically during runtime and also produce hello output partitioned with date and time.</span></span>

<span data-ttu-id="2ee9a-180">toouse Pig 스크립트를 매개 변수화를 수행 하는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-180">toouse parameterized Pig script, do hello following:</span></span>

* <span data-ttu-id="2ee9a-181">Hello 매개 변수에서 정의 **정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="2ee9a-181">Define hello parameters in **defines**.</span></span>

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
* <span data-ttu-id="2ee9a-182">Pig 스크립트 hello toohello 매개 변수를 사용 하 여 참조 하는 '**$parameterName**' hello 다음 예제와 같이:</span><span class="sxs-lookup"><span data-stu-id="2ee9a-182">In hello Pig Script, refer toohello parameters using '**$parameterName**' as shown in hello following example:</span></span>

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a><span data-ttu-id="2ee9a-183">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2ee9a-183">See Also</span></span>
* [<span data-ttu-id="2ee9a-184">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-184">Hive Activity</span></span>](data-factory-hive-activity.md)
* [<span data-ttu-id="2ee9a-185">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-185">MapReduce Activity</span></span>](data-factory-map-reduce.md)
* [<span data-ttu-id="2ee9a-186">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="2ee9a-186">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
* [<span data-ttu-id="2ee9a-187">Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="2ee9a-187">Invoke Spark programs</span></span>](data-factory-spark.md)
* [<span data-ttu-id="2ee9a-188">R 스크립트 호출</span><span class="sxs-lookup"><span data-stu-id="2ee9a-188">Invoke R scripts</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

