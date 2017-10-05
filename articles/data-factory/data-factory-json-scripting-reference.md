---
title: "Azure Data Factory - JSON 스크립팅 참조 | Microsoft Docs"
description: "Data Factory 엔터티에 JSON 스키마를 제공합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 805106c0a5cdbff1f143f22a2ae59f6d2a0bf126
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="3b729-103">Azure Data Factory - JSON 스크립팅 참조</span><span class="sxs-lookup"><span data-stu-id="3b729-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="3b729-104">이 문서에서는 Azure Data Factory 엔터티(파이프라인, 활동, 데이터 집합 및 연결된 서비스)를 정의하기 위한 JSON 스키마와 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="3b729-105">파이프라인</span><span class="sxs-lookup"><span data-stu-id="3b729-105">Pipeline</span></span> 
<span data-ttu-id="3b729-106">파이프라인 정의에 대한 간략한 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-106">The high-level structure for a pipeline definition is as follows:</span></span> 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="3b729-107">다음 표에서는 파이프라인 JSON 정의의 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-107">Following table describes the properties within the pipeline JSON definition:</span></span>

| <span data-ttu-id="3b729-108">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-108">Property</span></span> | <span data-ttu-id="3b729-109">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-109">Description</span></span> | <span data-ttu-id="3b729-110">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="3b729-111">name</span><span class="sxs-lookup"><span data-stu-id="3b729-111">name</span></span> | <span data-ttu-id="3b729-112">파이프라인의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-112">Name of the pipeline.</span></span> <span data-ttu-id="3b729-113">작업 또는 파이프라인이 수행되도록 구성된 작업을 나타내는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-113">Specify a name that represents the action that the activity or pipeline is configured to do</span></span><br/><ul><li><span data-ttu-id="3b729-114">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="3b729-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="3b729-115">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="3b729-116">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="3b729-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="3b729-117">예</span><span class="sxs-lookup"><span data-stu-id="3b729-117">Yes</span></span> |
| <span data-ttu-id="3b729-118">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-118">description</span></span> |<span data-ttu-id="3b729-119">작업 또는 파이프라인이 무엇에 사용되는지 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-119">Text describing what the activity or pipeline is used for</span></span> | <span data-ttu-id="3b729-120">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-120">No</span></span> |
| <span data-ttu-id="3b729-121">작업</span><span class="sxs-lookup"><span data-stu-id="3b729-121">activities</span></span> | <span data-ttu-id="3b729-122">활동의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-122">Contains a list of activities.</span></span> | <span data-ttu-id="3b729-123">예</span><span class="sxs-lookup"><span data-stu-id="3b729-123">Yes</span></span> |
| <span data-ttu-id="3b729-124">start</span><span class="sxs-lookup"><span data-stu-id="3b729-124">start</span></span> |<span data-ttu-id="3b729-125">파이프라인에 대한 시작 날짜-시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-125">Start date-time for the pipeline.</span></span> <span data-ttu-id="3b729-126">[ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="3b729-127">예: 2014-10-14T16:32:41</span><span class="sxs-lookup"><span data-stu-id="3b729-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="3b729-128">예를 들어 EST 시간처럼 현지 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-128">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="3b729-129">예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="3b729-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="3b729-130">start 및 end 속성은 함께 파이프라인의 활성 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-130">The start and end properties together specify active period for the pipeline.</span></span> <span data-ttu-id="3b729-131">출력 조각은 이 활성 기간에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="3b729-132">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-132">No</span></span><br/><br/><span data-ttu-id="3b729-133">end 속성에 대한 값을 지정하는 경우 반드시 start 속성에 대한 값도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-133">If you specify a value for the end property, you must specify value for the start property.</span></span><br/><br/><span data-ttu-id="3b729-134">파이프라인을 만들 때에는 시작 및 종료 시간을 비워 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-134">The start and end times can both be empty to create a pipeline.</span></span> <span data-ttu-id="3b729-135">파이프라인을 실행할 활성 기간을 설정하려면 두 값 모두를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-135">You must specify both values to set an active period for the pipeline to run.</span></span> <span data-ttu-id="3b729-136">파이프라인을 만들 때 시작 시간과 종료 시간을 지정하지 않으면 나중에 Set-AzureRmDataFactoryPipelineActivePeriod cmdlet를 사용하여 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-136">If you do not specify start and end times when creating a pipeline, you can set them using the Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="3b729-137">end</span><span class="sxs-lookup"><span data-stu-id="3b729-137">end</span></span> |<span data-ttu-id="3b729-138">파이프라인에 대한 종료 날짜-시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-138">End date-time for the pipeline.</span></span> <span data-ttu-id="3b729-139">지정된 경우 ISO 형식에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-139">If specified must be in ISO format.</span></span> <span data-ttu-id="3b729-140">예: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="3b729-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="3b729-141">예를 들어 EST 시간처럼 현지 시간을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-141">It is possible to specify a local time, for example an EST time.</span></span> <span data-ttu-id="3b729-142">예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="3b729-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="3b729-143">파이프라인을 무기한 실행하려면 end 속성 값으로 9999-09-09를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-143">To run the pipeline indefinitely, specify 9999-09-09 as the value for the end property.</span></span> |<span data-ttu-id="3b729-144">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-144">No</span></span> <br/><br/><span data-ttu-id="3b729-145">시작 속성에 대한 값을 지정하는 경우 반드시 끝 속성에 대한 값도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-145">If you specify a value for the start property, you must specify value for the end property.</span></span><br/><br/><span data-ttu-id="3b729-146">**start** 속성에 대한 참조를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-146">See notes for the **start** property.</span></span> |
| <span data-ttu-id="3b729-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="3b729-147">isPaused</span></span> |<span data-ttu-id="3b729-148">파이프라인을 true로 설정하면 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-148">If set to true the pipeline does not run.</span></span> <span data-ttu-id="3b729-149">기본값 = false입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-149">Default value = false.</span></span> <span data-ttu-id="3b729-150">이 속성을 사용하여 활성화 또는 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-150">You can use this property to enable or disable.</span></span> |<span data-ttu-id="3b729-151">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-151">No</span></span> |
| <span data-ttu-id="3b729-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="3b729-152">pipelineMode</span></span> |<span data-ttu-id="3b729-153">파이프라인에 대한 실행을 예약하는 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-153">The method for scheduling runs for the pipeline.</span></span> <span data-ttu-id="3b729-154">허용되는 값은 scheduled(기본), onetime입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="3b729-155">‘Scheduled’는 파이프라인이 활성 기간(시작 및 종료 시간)에 따라 지정된 시간 간격으로 실행된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-155">‘Scheduled’ indicates that the pipeline runs at a specified time interval according to its active period (start and end time).</span></span> <span data-ttu-id="3b729-156">‘Onetime’은 파이프라인이 한 번만 실행된다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-156">‘Onetime’ indicates that the pipeline runs only once.</span></span> <span data-ttu-id="3b729-157">현재는, Onetime 파이프라인이 생성된 후에 수정/업데이트가 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="3b729-158">일회성 설정에 대한 세부 정보는 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="3b729-159">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-159">No</span></span> |
| <span data-ttu-id="3b729-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="3b729-160">expirationTime</span></span> |<span data-ttu-id="3b729-161">생성 후에 파이프라인이 유효하고 프로비전된 상태로 유지해야 하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-161">Duration of time after creation for which the pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="3b729-162">활성 작업, 실패한 작업 또는 보류 중인 작업이 없는 경우 만료 시간이 되면 파이프라인은 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-162">If it does not have any active, failed, or pending runs, the pipeline is deleted automatically once it reaches the expiration time.</span></span> |<span data-ttu-id="3b729-163">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="3b729-164">작업</span><span class="sxs-lookup"><span data-stu-id="3b729-164">Activity</span></span> 
<span data-ttu-id="3b729-165">파이프라인 정의(activities 요소) 내의 활동(activity)에 대한 간략한 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-165">The high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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
    }
    "scheduler":
    {
    }
}
```

<span data-ttu-id="3b729-166">다음 표에서는 activity JSON 정의 내의 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-166">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="3b729-167">태그</span><span class="sxs-lookup"><span data-stu-id="3b729-167">Tag</span></span> | <span data-ttu-id="3b729-168">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-168">Description</span></span> | <span data-ttu-id="3b729-169">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-170">name</span><span class="sxs-lookup"><span data-stu-id="3b729-170">name</span></span> |<span data-ttu-id="3b729-171">활동의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-171">Name of the activity.</span></span> <span data-ttu-id="3b729-172">활동을 수행하도록 구성된 작업을 나타내는 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-172">Specify a name that represents the action that the activity is configured to do</span></span><br/><ul><li><span data-ttu-id="3b729-173">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="3b729-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="3b729-174">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="3b729-175">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="3b729-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="3b729-176">예</span><span class="sxs-lookup"><span data-stu-id="3b729-176">Yes</span></span> |
| <span data-ttu-id="3b729-177">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-177">description</span></span> |<span data-ttu-id="3b729-178">활동의 용도를 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-178">Text describing what the activity is used for.</span></span> |<span data-ttu-id="3b729-179">예</span><span class="sxs-lookup"><span data-stu-id="3b729-179">Yes</span></span> |
| <span data-ttu-id="3b729-180">type</span><span class="sxs-lookup"><span data-stu-id="3b729-180">type</span></span> |<span data-ttu-id="3b729-181">작업의 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-181">Specifies the type of the activity.</span></span> <span data-ttu-id="3b729-182">다른 유형의 작업에 대해서는 [데이터 저장소](#data-stores) 및 [데이터 변환 작업](#data-transformation-activities) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-182">See the [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="3b729-183">예</span><span class="sxs-lookup"><span data-stu-id="3b729-183">Yes</span></span> |
| <span data-ttu-id="3b729-184">inputs</span><span class="sxs-lookup"><span data-stu-id="3b729-184">inputs</span></span> |<span data-ttu-id="3b729-185">작업에서 사용하는 입력 테이블</span><span class="sxs-lookup"><span data-stu-id="3b729-185">Input tables used by the activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="3b729-186">예</span><span class="sxs-lookup"><span data-stu-id="3b729-186">Yes</span></span> |
| <span data-ttu-id="3b729-187">outputs</span><span class="sxs-lookup"><span data-stu-id="3b729-187">outputs</span></span> |<span data-ttu-id="3b729-188">활동에서 사용하는 출력 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-188">Output tables used by the activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="3b729-189">예</span><span class="sxs-lookup"><span data-stu-id="3b729-189">Yes</span></span> |
| <span data-ttu-id="3b729-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3b729-190">linkedServiceName</span></span> |<span data-ttu-id="3b729-191">작업에서 사용하는 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-191">Name of the linked service used by the activity.</span></span> <br/><br/><span data-ttu-id="3b729-192">작업은 필요한 계산 환경에 연결하는 연결된 서비스를 지정해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-192">An activity may require that you specify the linked service that links to the required compute environment.</span></span> |<span data-ttu-id="3b729-193">HDInsight 활동, Azure Machine Learning 활동 및 저장 프로시저 활동의 경우 예</span><span class="sxs-lookup"><span data-stu-id="3b729-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="3b729-194">다른 모든 사용자의 경우 아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-194">No for all others</span></span> |
| <span data-ttu-id="3b729-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="3b729-195">typeProperties</span></span> |<span data-ttu-id="3b729-196">typeProperties 섹션의 속성은 작업의 종류에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-196">Properties in the typeProperties section depend on type of the activity.</span></span> |<span data-ttu-id="3b729-197">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-197">No</span></span> |
| <span data-ttu-id="3b729-198">policy</span><span class="sxs-lookup"><span data-stu-id="3b729-198">policy</span></span> |<span data-ttu-id="3b729-199">작업의 런타임 동작에 영향을 주는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-199">Policies that affect the run-time behavior of the activity.</span></span> <span data-ttu-id="3b729-200">지정하지 않으면 기본 정책이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="3b729-201">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-201">No</span></span> |
| <span data-ttu-id="3b729-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="3b729-202">scheduler</span></span> |<span data-ttu-id="3b729-203">"scheduler" 속성은 작업에 원하는 일정을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-203">“scheduler” property is used to define desired scheduling for the activity.</span></span> <span data-ttu-id="3b729-204">하위 속성은 [데이터 집합에서 가용성 속성](data-factory-create-datasets.md#dataset-availability)에 있는 속성과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-204">Its subproperties are the same as the ones in the [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="3b729-205">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="3b729-206">정책</span><span class="sxs-lookup"><span data-stu-id="3b729-206">Policies</span></span>
<span data-ttu-id="3b729-207">정책은 특히 테이블의 조각을 처리할 때 활동의 런타임 동작에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-207">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="3b729-208">다음 테이블에서는 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-208">The following table provides the details.</span></span>

| <span data-ttu-id="3b729-209">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-209">Property</span></span> | <span data-ttu-id="3b729-210">허용된 값</span><span class="sxs-lookup"><span data-stu-id="3b729-210">Permitted values</span></span> | <span data-ttu-id="3b729-211">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-211">Default Value</span></span> | <span data-ttu-id="3b729-212">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-213">동시성</span><span class="sxs-lookup"><span data-stu-id="3b729-213">concurrency</span></span> |<span data-ttu-id="3b729-214">정수 </span><span class="sxs-lookup"><span data-stu-id="3b729-214">Integer</span></span> <br/><br/><span data-ttu-id="3b729-215">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="3b729-215">Max value: 10</span></span> |<span data-ttu-id="3b729-216">1</span><span class="sxs-lookup"><span data-stu-id="3b729-216">1</span></span> |<span data-ttu-id="3b729-217">작업의 동시 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-217">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="3b729-218">다른 조각에 발생할 수 있는 병렬 작업 실행 횟수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-218">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="3b729-219">예를 들어 활동이 사용 가능한 많은 데이터 집합을 거쳐야 하는 경우 동시성 값을 높이면 데이터 처리가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-219">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="3b729-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="3b729-220">executionPriorityOrder</span></span> |<span data-ttu-id="3b729-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="3b729-221">NewestFirst</span></span><br/><br/><span data-ttu-id="3b729-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="3b729-222">OldestFirst</span></span> |<span data-ttu-id="3b729-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="3b729-223">OldestFirst</span></span> |<span data-ttu-id="3b729-224">처리 중인 데이터 조각의 순서를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-224">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="3b729-225">예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="3b729-226">executionPriorityOrder를 설정하여 NewestFirst가 되도록 하면 오후 5시에 조각이 먼저 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-226">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="3b729-227">마찬가지로 executionPriorityORder를 OldestFIrst로 설정하면 오후 4시의 조각이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-227">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="3b729-228">retry</span><span class="sxs-lookup"><span data-stu-id="3b729-228">retry</span></span> |<span data-ttu-id="3b729-229">정수 </span><span class="sxs-lookup"><span data-stu-id="3b729-229">Integer</span></span><br/><br/><span data-ttu-id="3b729-230">최대값이 10이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="3b729-230">Max value can be 10</span></span> |<span data-ttu-id="3b729-231">0</span><span class="sxs-lookup"><span data-stu-id="3b729-231">0</span></span> |<span data-ttu-id="3b729-232">조각에 대한 데이터 처리 전에 다시 시도 횟수가 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-232">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="3b729-233">데이터 조각에 대한 활동 실행은 지정된 재시도 횟수까지 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-233">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="3b729-234">재시도는 실패 후 가능한 한 빨리 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-234">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="3b729-235">시간 제한</span><span class="sxs-lookup"><span data-stu-id="3b729-235">timeout</span></span> |<span data-ttu-id="3b729-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b729-236">TimeSpan</span></span> |<span data-ttu-id="3b729-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="3b729-237">00:00:00</span></span> |<span data-ttu-id="3b729-238">활동에 대한 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-238">Timeout for the activity.</span></span> <span data-ttu-id="3b729-239">예: 00:10:00(시간 제한 10분을 의미함)</span><span class="sxs-lookup"><span data-stu-id="3b729-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="3b729-240">값이 지정되지 않거나 0인 경우 시간 제한은 무한입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-240">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="3b729-241">조각의 데이터 처리 시간이 시간 제한 값을 초과하면 취소되고 시스템이 처리를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-241">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="3b729-242">다시 시도 횟수는 다시 시도 속성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-242">The number of retries depends on the retry property.</span></span> <span data-ttu-id="3b729-243">시간 제한이 발생할 때 상태는 TimedOut으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-243">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="3b729-244">delay</span><span class="sxs-lookup"><span data-stu-id="3b729-244">delay</span></span> |<span data-ttu-id="3b729-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b729-245">TimeSpan</span></span> |<span data-ttu-id="3b729-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="3b729-246">00:00:00</span></span> |<span data-ttu-id="3b729-247">조각의 데이터 처리 작업이 시작되기 전에 지연을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-247">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="3b729-248">데이터 조각에 대한 활동의 실행은 지연이 예상된 실행 시간을 지난 후에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-248">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="3b729-249">예: 00:10:00(10분의 지연을 의미함)</span><span class="sxs-lookup"><span data-stu-id="3b729-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="3b729-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="3b729-250">longRetry</span></span> |<span data-ttu-id="3b729-251">정수 </span><span class="sxs-lookup"><span data-stu-id="3b729-251">Integer</span></span><br/><br/><span data-ttu-id="3b729-252">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="3b729-252">Max value: 10</span></span> |<span data-ttu-id="3b729-253">1</span><span class="sxs-lookup"><span data-stu-id="3b729-253">1</span></span> |<span data-ttu-id="3b729-254">조각 실행이 실패하기 전까지의 긴 재시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-254">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="3b729-255">longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="3b729-256">따라서 재시도 간의 시간을 지정해야 하는 경우 longRetry를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-256">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="3b729-257">Retry 및 longRetry를 둘 다 지정하면 각 longRetry 시도에는 Retry 시도가 포함되고 최대 시도 횟수는 Retry * longRetry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="3b729-258">예를 들어 활동 정책에 다음 설정이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="3b729-258">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="3b729-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="3b729-259">Retry: 3</span></span><br/><span data-ttu-id="3b729-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="3b729-260">longRetry: 2</span></span><br/><span data-ttu-id="3b729-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="3b729-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="3b729-262">실행할 조각이 하나뿐이며(Waiting 상태) 작업 실행이 매번 실패한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-262">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="3b729-263">우선 3번 연속 실행 시도를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="3b729-264">시도한 후 각 조각 상태는 다시 시도입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-264">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="3b729-265">처음 3번 시도 후에 조각 상태는 LongRetry입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-265">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="3b729-266">한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="3b729-267">그 후에 조각 상태가 실패이면 다시 시도는 더 이상 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-267">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="3b729-268">즉, 전체적으로 6번의 시도가 일어납니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="3b729-269">모든 실행에 성공하면 조각 상태는 준비 상태가 되며 더 이상 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-269">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="3b729-270">longRetry는 종속 데이터가 명확하지 않은 시간에 도착하거나 데이터 처리가 발생하는 전체적인 환경을 신뢰할 수 없는 상황에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="3b729-271">이러한 경우 하나씩 다시 시도를 수행해도 도움이 되지 않을 수 있으며 특정 시간 간격 후에 시도할 경우 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="3b729-272">주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="3b729-273">일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="3b729-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="3b729-274">longRetryInterval</span></span> |<span data-ttu-id="3b729-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3b729-275">TimeSpan</span></span> |<span data-ttu-id="3b729-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="3b729-276">00:00:00</span></span> |<span data-ttu-id="3b729-277">긴 다시 시도 간의 지연</span><span class="sxs-lookup"><span data-stu-id="3b729-277">The delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="3b729-278">typeProperties 섹션</span><span class="sxs-lookup"><span data-stu-id="3b729-278">typeProperties section</span></span>
<span data-ttu-id="3b729-279">typeProperties 섹션은 각 활동마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-279">The typeProperties section is different for each activity.</span></span> <span data-ttu-id="3b729-280">변환 활동에는 type 속성만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-280">Transformation activities have just the type properties.</span></span> <span data-ttu-id="3b729-281">파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="3b729-282">**복사 활동**(Copy activity)의 typeProperties 섹션에는 두 하위 섹션, 즉 **source** 및 **sink**가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-282">**Copy activity** has two subsections in the typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="3b729-283">데이터 저장소를 소스 및/또는 싱크로 사용하는 방법을 보여 주는 JSON 샘플은 이 문서의 [데이터 저장소](#data-stores) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="3b729-284">샘플 복사 파이프라인</span><span class="sxs-lookup"><span data-stu-id="3b729-284">Sample copy pipeline</span></span>
<span data-ttu-id="3b729-285">다음 샘플 파이프라인에는 **Copy** in the **활동** 유형의 하나의 활동이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-285">In the following sample pipeline, there is one activity of type **Copy** in the **activities** section.</span></span> <span data-ttu-id="3b729-286">샘플에서 [복사 작업](data-factory-data-movement-activities.md)은 Azure Blob 저장소의 데이터를 Azure SQL 데이터베이스에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-286">In this sample, the [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage to an Azure SQL database.</span></span> 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="3b729-287">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-287">Note the following points:</span></span>

* <span data-ttu-id="3b729-288">작업 섹션에는 **형식**이 **복사**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span>
* <span data-ttu-id="3b729-289">작업에 대한 입력을 **InputDataset**으로 설정하고 작업에 대한 출력을 **OutputDataset**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-289">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span>
* <span data-ttu-id="3b729-290">**typeProperties** 섹션에서 **BlobSource**를 원본 유형으로 지정하고 **SqlSink**를 싱크 유형으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-290">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="3b729-291">데이터 저장소를 소스 및/또는 싱크로 사용하는 방법을 보여 주는 JSON 샘플은 이 문서의 [데이터 저장소](#data-stores) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how to use a data store as a source and/or sink.</span></span>    

<span data-ttu-id="3b729-292">이 파이프라인을 만드는 전체 연습은 [자습서: Blob Storage의 데이터를 SQL Database에 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="3b729-293">샘플 변환 파이프라인</span><span class="sxs-lookup"><span data-stu-id="3b729-293">Sample transformation pipeline</span></span>
<span data-ttu-id="3b729-294">다음 샘플 파이프라인에는 **HDInsightHive** in the **활동** 유형의 하나의 활동이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-294">In the following sample pipeline, there is one activity of type **HDInsightHive** in the **activities** section.</span></span> <span data-ttu-id="3b729-295">이 샘플에서 [HDInsight Hive 활동](data-factory-hive-activity.md) 은 Azure HDInsight Hadoop 클러스터에서 Hive 스크립트 파일을 실행하여 Azure Blob 저장소에서 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-295">In this sample, the [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="3b729-296">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-296">Note the following points:</span></span> 

* <span data-ttu-id="3b729-297">activities 섹션에는 **type**이 **HDInsightHive**로 설정된 작업만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-297">In the activities section, there is only one activity whose **type** is set to **HDInsightHive**.</span></span>
* <span data-ttu-id="3b729-298">Hive 스크립트 파일 **partitionweblogs.hql**은 Azure Storage 계정(**AzureStorageLinkedService**라고 하는 scriptLinkedService에 의해 지정됨)과 **adfgetstarted** 컨테이너에 있는 **스크립트** 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-298">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>
* <span data-ttu-id="3b729-299">**defines** 섹션은 Hive 스크립트에 Hive 구성 값(예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`)으로 전달되는 런타임 설정을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-299">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="3b729-300">파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="3b729-301">이 파이프라인을 만드는 전체 연습은 [자습서: Hadoop 클러스터를 사용하여 데이터를 처리하는 첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline to process data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="3b729-302">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-302">Linked service</span></span>
<span data-ttu-id="3b729-303">연결된 서비스 정의의 간략한 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-303">The high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of the linked service>",
    "properties": {
        "type": "<type of the linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="3b729-304">다음 표에서는 activity JSON 정의 내의 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-304">Following table describe the properties within the activity JSON definition:</span></span>

| <span data-ttu-id="3b729-305">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-305">Property</span></span> | <span data-ttu-id="3b729-306">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-306">Description</span></span> | <span data-ttu-id="3b729-307">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="3b729-308">name</span><span class="sxs-lookup"><span data-stu-id="3b729-308">name</span></span> | <span data-ttu-id="3b729-309">연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-309">Name of the linked service.</span></span> | <span data-ttu-id="3b729-310">예</span><span class="sxs-lookup"><span data-stu-id="3b729-310">Yes</span></span> | 
| <span data-ttu-id="3b729-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="3b729-311">properties - type</span></span> | <span data-ttu-id="3b729-312">연결된 서비스의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-312">Type of the linked service.</span></span> <span data-ttu-id="3b729-313">예: Azure Storage, Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3b729-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="3b729-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="3b729-314">typeProperties</span></span> | <span data-ttu-id="3b729-315">typeProperties 섹션에는 각 데이터 저장소 또는 계산 환경마다 다른 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-315">The typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="3b729-316">모든 데이터 저장소 연결된 서비스는 [데이터 저장소](#datastores) 섹션을, 모든 계산 연결된 서비스는 [계산 환경](#compute-environments)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-316">See [data stores](#datastores) section for all the data store linked services and [compute environments](#compute-environments) for all the compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="3b729-317">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-317">Dataset</span></span> 
<span data-ttu-id="3b729-318">Azure Data Factory의 데이터 집합은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="3b729-319">다음 표에서는 위의 JSON에서 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-319">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="3b729-320">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-320">Property</span></span> | <span data-ttu-id="3b729-321">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-321">Description</span></span> | <span data-ttu-id="3b729-322">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-322">Required</span></span> | <span data-ttu-id="3b729-323">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-324">name</span><span class="sxs-lookup"><span data-stu-id="3b729-324">name</span></span> | <span data-ttu-id="3b729-325">데이터 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-325">Name of the dataset.</span></span> <span data-ttu-id="3b729-326">명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="3b729-327">예</span><span class="sxs-lookup"><span data-stu-id="3b729-327">Yes</span></span> |<span data-ttu-id="3b729-328">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-328">NA</span></span> |
| <span data-ttu-id="3b729-329">type</span><span class="sxs-lookup"><span data-stu-id="3b729-329">type</span></span> | <span data-ttu-id="3b729-330">데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-330">Type of the dataset.</span></span> <span data-ttu-id="3b729-331">Azure Data Factory에서 지원되는 형식(예: AzureBlob, AzureSqlTable) 중 하나를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-331">Specify one of the types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="3b729-332">Data Factory에서 지원하는 모든 데이터 저장소 및 데이터 집합 유형에 대해서는 [데이터 저장소](#data-stores) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-332">See [DATA STORES](#data-stores) section for all the data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="3b729-333">structure</span><span class="sxs-lookup"><span data-stu-id="3b729-333">structure</span></span> | <span data-ttu-id="3b729-334">데이터 집합의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-334">Schema of the dataset.</span></span> <span data-ttu-id="3b729-335">열, 해당 형식 등을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="3b729-336">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-336">No</span></span> |<span data-ttu-id="3b729-337">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-337">NA</span></span> |
| <span data-ttu-id="3b729-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="3b729-338">typeProperties</span></span> | <span data-ttu-id="3b729-339">선택한 형식에 해당하는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-339">Properties corresponding to the selected type.</span></span> <span data-ttu-id="3b729-340">지원되는 형식 및 해당 속성은 [데이터 저장소](#data-stores) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="3b729-341">예</span><span class="sxs-lookup"><span data-stu-id="3b729-341">Yes</span></span> |<span data-ttu-id="3b729-342">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-342">NA</span></span> |
| <span data-ttu-id="3b729-343">external</span><span class="sxs-lookup"><span data-stu-id="3b729-343">external</span></span> | <span data-ttu-id="3b729-344">데이터 집합이 데이터 팩터리 파이프라인에 의해 명시적으로 생성되는지를 지정하는 부울 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-344">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="3b729-345">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-345">No</span></span> |<span data-ttu-id="3b729-346">false</span><span class="sxs-lookup"><span data-stu-id="3b729-346">false</span></span> |
| <span data-ttu-id="3b729-347">availability</span><span class="sxs-lookup"><span data-stu-id="3b729-347">availability</span></span> | <span data-ttu-id="3b729-348">데이터 집합 생성에 대한 처리 창 또는 조각화 모델을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-348">Defines the processing window or the slicing model for the dataset production.</span></span> <span data-ttu-id="3b729-349">데이터 집합 조각화 모델에 대한 자세한 내용은 [예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-349">For details on the dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="3b729-350">예</span><span class="sxs-lookup"><span data-stu-id="3b729-350">Yes</span></span> |<span data-ttu-id="3b729-351">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-351">NA</span></span> |
| <span data-ttu-id="3b729-352">policy</span><span class="sxs-lookup"><span data-stu-id="3b729-352">policy</span></span> |<span data-ttu-id="3b729-353">데이터 집합 조각이 충족해야 하는 기준 또는 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-353">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="3b729-354">세부 정보는 [데이터 집합 정책](#Policy) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="3b729-355">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-355">No</span></span> |<span data-ttu-id="3b729-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-356">NA</span></span> |

<span data-ttu-id="3b729-357">**structure** 섹션의 각 열에는 다음과 같은 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-357">Each column in the **structure** section contains the following properties:</span></span>

| <span data-ttu-id="3b729-358">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-358">Property</span></span> | <span data-ttu-id="3b729-359">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-359">Description</span></span> | <span data-ttu-id="3b729-360">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-361">name</span><span class="sxs-lookup"><span data-stu-id="3b729-361">name</span></span> |<span data-ttu-id="3b729-362">열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-362">Name of the column.</span></span> |<span data-ttu-id="3b729-363">예</span><span class="sxs-lookup"><span data-stu-id="3b729-363">Yes</span></span> |
| <span data-ttu-id="3b729-364">type</span><span class="sxs-lookup"><span data-stu-id="3b729-364">type</span></span> |<span data-ttu-id="3b729-365">열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-365">Data type of the column.</span></span>  |<span data-ttu-id="3b729-366">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-366">No</span></span> |
| <span data-ttu-id="3b729-367">culture</span><span class="sxs-lookup"><span data-stu-id="3b729-367">culture</span></span> |<span data-ttu-id="3b729-368">지정된 형식이 .NET 형식 `Datetime` 또는 `Datetimeoffset`일 때 사용할 .NET 기반 culture입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-368">.NET based culture to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="3b729-369">기본값은 `en-us`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-369">Default is `en-us`.</span></span> |<span data-ttu-id="3b729-370">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-370">No</span></span> |
| <span data-ttu-id="3b729-371">format</span><span class="sxs-lookup"><span data-stu-id="3b729-371">format</span></span> |<span data-ttu-id="3b729-372">지정된 형식이 .NET 형식 `Datetime` 또는 `Datetimeoffset`일 때 사용할 형식 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-372">Format string to be used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="3b729-373">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-373">No</span></span> |

<span data-ttu-id="3b729-374">다음 예제에서는 데이터 집합에 3개의 열 `slicetimestamp`, `projectname` 및 `pageviews`가 있으며 형식은 각각 문자열, 문자열 및 10진수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-374">In the following example, the dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="3b729-375">다음 표에서는 **availability** 섹션에서 사용할 수 있는 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-375">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="3b729-376">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-376">Property</span></span> | <span data-ttu-id="3b729-377">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-377">Description</span></span> | <span data-ttu-id="3b729-378">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-378">Required</span></span> | <span data-ttu-id="3b729-379">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-380">frequency</span><span class="sxs-lookup"><span data-stu-id="3b729-380">frequency</span></span> |<span data-ttu-id="3b729-381">데이터 집합 조각 생성을 위한 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-381">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="3b729-382"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="3b729-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="3b729-383">예</span><span class="sxs-lookup"><span data-stu-id="3b729-383">Yes</span></span> |<span data-ttu-id="3b729-384">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-384">NA</span></span> |
| <span data-ttu-id="3b729-385">interval</span><span class="sxs-lookup"><span data-stu-id="3b729-385">interval</span></span> |<span data-ttu-id="3b729-386">빈도 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="3b729-387">"빈도 x 간격"은 조각을 생성하는 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-387">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="3b729-388">데이터 집합을 시간 단위로 조각화해야 하는 경우 <b>frequency</b>를 <b>Hour</b>로, <b>interval</b>을 <b>1</b>로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-388">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="3b729-389"><b>참고:</b> 빈도를 Minute(분)으로 지정하면 15 이상으로 간격을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="3b729-390">예</span><span class="sxs-lookup"><span data-stu-id="3b729-390">Yes</span></span> |<span data-ttu-id="3b729-391">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-391">NA</span></span> |
| <span data-ttu-id="3b729-392">style</span><span class="sxs-lookup"><span data-stu-id="3b729-392">style</span></span> |<span data-ttu-id="3b729-393">간격의 시작/끝에 조각을 생성해야 하는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-393">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="3b729-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="3b729-394">StartOfInterval</span></span></li><li><span data-ttu-id="3b729-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="3b729-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="3b729-396">Frequency를 Month로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 월의 마지막 날에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-396">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="3b729-397">style을 StartOfInterval로 설정하는 경우 조각을 달의 첫 번째 날에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-397">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="3b729-398">frequency를 Day로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 일의 마지막 시간에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-398">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="3b729-399">Frequency를 Hour로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 시간의 끝에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-399">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="3b729-400">예를 들어 오후 1~2시 기간에 대한 조각은 오후 2시에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-400">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="3b729-401">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-401">No</span></span> |<span data-ttu-id="3b729-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="3b729-402">EndOfInterval</span></span> |
| <span data-ttu-id="3b729-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="3b729-403">anchorDateTime</span></span> |<span data-ttu-id="3b729-404">스케줄러에서 사용하는 시간에 절대 위치를 정의하여 데이터 집합 조각 경계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-404">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="3b729-405"><b>참고:</b> AnchorDateTime에 빈도보다 더 세분화된 날짜 부분이 있는 경우 더 세분화된 부분을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-405"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="3b729-406">예를 들어 <b>간격</b>이 <b>매시간</b>(frequency: Hour 및 interval: 1)이고 <b>AnchorDateTime</b>에서 <b>분 및 초</b>를 포함하는 경우 AnchorDateTime의 <b>분 및 초</b> 부분은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-406">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="3b729-407">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-407">No</span></span> |<span data-ttu-id="3b729-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="3b729-408">01/01/0001</span></span> |
| <span data-ttu-id="3b729-409">offset</span><span class="sxs-lookup"><span data-stu-id="3b729-409">offset</span></span> |<span data-ttu-id="3b729-410">모든 데이터 집합 조각의 시작과 끝이 이동에 의한 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-410">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="3b729-411"><b>참고:</b> anchorDateTime 및 offset이 모두 지정되면 결과적으로 이동이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-411"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="3b729-412">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-412">No</span></span> |<span data-ttu-id="3b729-413">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-413">NA</span></span> |

<span data-ttu-id="3b729-414">다음 availability 섹션에서는 출력 데이터 집합을 시간마다 생성하거나 (또는) 입력 데이터 집합을 시간마다 사용할 수 있도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-414">The following availability section specifies that the output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="3b729-415">데이터 집합 정의의 **정책** 섹션에서 데이터 집합 조각이 충족해야 하는 기준 또는 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-415">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

| <span data-ttu-id="3b729-416">정책 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-416">Policy Name</span></span> | <span data-ttu-id="3b729-417">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-417">Description</span></span> | <span data-ttu-id="3b729-418">에 적용</span><span class="sxs-lookup"><span data-stu-id="3b729-418">Applied To</span></span> | <span data-ttu-id="3b729-419">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-419">Required</span></span> | <span data-ttu-id="3b729-420">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="3b729-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="3b729-421">minimumSizeMB</span></span> |<span data-ttu-id="3b729-422">**Azure Blob** 에서 데이터가 최소 크기 요구 사항(메가바이트)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-422">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="3b729-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="3b729-423">Azure Blob</span></span> |<span data-ttu-id="3b729-424">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-424">No</span></span> |<span data-ttu-id="3b729-425">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-425">NA</span></span> |
| <span data-ttu-id="3b729-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="3b729-426">minimumRows</span></span> |<span data-ttu-id="3b729-427">**Azure SQL Database** 또는 **Azure 테이블**에서 데이터가 최소 행 수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-427">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="3b729-428">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3b729-428">Azure SQL Database</span></span></li><li><span data-ttu-id="3b729-429">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="3b729-429">Azure Table</span></span></li></ul> |<span data-ttu-id="3b729-430">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-430">No</span></span> |<span data-ttu-id="3b729-431">해당 없음</span><span class="sxs-lookup"><span data-stu-id="3b729-431">NA</span></span> |

<span data-ttu-id="3b729-432">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3b729-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="3b729-433">데이터 집합이 Azure Data Factory에서 생성되지 않는 한 **external**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="3b729-434">이 설정은 작업 또는 파이프라인 연결을 활용하고 있지 않는 한 파이프라인에서 첫 번째 작업의 입력에 일반적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-434">This setting generally applies to the inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="3b729-435">name</span><span class="sxs-lookup"><span data-stu-id="3b729-435">Name</span></span> | <span data-ttu-id="3b729-436">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-436">Description</span></span> | <span data-ttu-id="3b729-437">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-437">Required</span></span> | <span data-ttu-id="3b729-438">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="3b729-439">dataDelay</span></span> |<span data-ttu-id="3b729-440">지정된 조각에 대한 외부 데이터의 가용성 확인을 지연하는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-440">Time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="3b729-441">예를 들어 데이터를 매시간 사용할 수 있는 경우 외부 데이터를 볼 수 있고 해당 조각이 준비(Ready) 상태인지 확인하기 위한 검사는 dataDelay를 사용하여 지연시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-441">For example, if the data is available hourly, the check to see the external data is available and the corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="3b729-442">를 사용하여 지연할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-442">Only applies to the present time.</span></span>  <span data-ttu-id="3b729-443">예를 들어 현재 오후 1시이고 이 값이 10 분이라면 유효성 검사는 오후 1시 10분에 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-443">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="3b729-444">이 설정은 과거의 조각(조각 종료 시간 + dataDelay < Now를 사용한 조각)에는 영향을 주지 않아 아무런 지연 없이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-444">This setting does not affect slices in the past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="3b729-445">23:59보다 큰 시간은 `day.hours:minutes:seconds` 형식을 사용하여 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-445">Time greater than 23:59 hours need to specified using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="3b729-446">예를 들어 24시간을 지정하려면 24:00:00을 사용하는 대신 1.00:00:00을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-446">For example, to specify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="3b729-447">24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="3b729-448">1일 4시간의 경우 1:04:00:00을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="3b729-449">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-449">No</span></span> |<span data-ttu-id="3b729-450">0</span><span class="sxs-lookup"><span data-stu-id="3b729-450">0</span></span> |
| <span data-ttu-id="3b729-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="3b729-451">retryInterval</span></span> |<span data-ttu-id="3b729-452">오류 발생과 다음 다시 시도 사이의 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-452">The wait time between a failure and the next retry attempt.</span></span> <span data-ttu-id="3b729-453">시도가 실패하는 경우 다음 시도는 retryInterval 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-453">If a try fails, the next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="3b729-454">오후 1시가 되면 첫 번째 시도를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-454">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="3b729-455">첫 번째 유효성 검사를 완료하는 데 걸리는 기간이 1분이고 작업이 실패하는 경우 다음 다시 시도는 1시 + 1분(기간) + 1분(다시 시도 간격) = 오후 1시 2분입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-455">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="3b729-456">과거 조각의 경우 지연이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-456">For slices in the past, there is no delay.</span></span> <span data-ttu-id="3b729-457">재시도는 곧바로 이뤄집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-457">The retry happens immediately.</span></span> |<span data-ttu-id="3b729-458">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-458">No</span></span> |<span data-ttu-id="3b729-459">00:01:00 (1분)</span><span class="sxs-lookup"><span data-stu-id="3b729-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="3b729-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-460">retryTimeout</span></span> |<span data-ttu-id="3b729-461">각 재시도에 대한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-461">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="3b729-462">이 속성이 10분으로 설정한 경우 유효성 검사를 10분 내에 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-462">If this property is set to 10 minutes, the validation needs to be completed within 10 minutes.</span></span> <span data-ttu-id="3b729-463">유효성 검사를 수행하는 데 10분 보다 오래 걸리는 경우 재시도는 제한 시간을 초과합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-463">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="3b729-464">유효성 검사에 대한 모든 시도의 시간이 초과되면 조각에 TimedOut이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-464">If all attempts for the validation times out, the slice is marked as TimedOut.</span></span> |<span data-ttu-id="3b729-465">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-465">No</span></span> |<span data-ttu-id="3b729-466">00:10:00 (10분)</span><span class="sxs-lookup"><span data-stu-id="3b729-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="3b729-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="3b729-467">maximumRetry</span></span> |<span data-ttu-id="3b729-468">외부 데이터의 가용성을 검사한 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-468">Number of times to check for the availability of the external data.</span></span> <span data-ttu-id="3b729-469">허용되는 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-469">The allowed maximum value is 10.</span></span> |<span data-ttu-id="3b729-470">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-470">No</span></span> |<span data-ttu-id="3b729-471">3</span><span class="sxs-lookup"><span data-stu-id="3b729-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="3b729-472">데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="3b729-472">DATA STORES</span></span>
<span data-ttu-id="3b729-473">[연결된 서비스](#linked-service) 섹션에서 모든 유형의 연결된 서비스에 공통적인 JSON 요소에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-473">The [Linked service](#linked-service) section provided descriptions for JSON elements that are common to all types of linked services.</span></span> <span data-ttu-id="3b729-474">이 섹션에서는 각 데이터 저장소와 관련된 JSON 요소에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-474">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="3b729-475">[데이터 집합](#dataset) 섹션에서 모든 유형의 데이터 집합에 공통적인 JSON 요소에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-475">The [Dataset](#dataset) section provided descriptions for JSON elements that are common to all types of datasets.</span></span> <span data-ttu-id="3b729-476">이 섹션에서는 각 데이터 저장소와 관련된 JSON 요소에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-476">This section provides details about JSON elements that are specific to each data store.</span></span>

<span data-ttu-id="3b729-477">[활동](#activity) 섹션에서 모든 유형의 활동에 공통적인 JSON 요소에 대해 설명했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-477">The [Activity](#activity) section provided descriptions for JSON elements that are common to all types of activities.</span></span> <span data-ttu-id="3b729-478">이 섹션에서는 복사 활동의 소스/싱크로 사용될 때 각 데이터 저장소와 관련된 JSON 요소에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-478">This section provides details about JSON elements that are specific to each data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="3b729-479">관심 있는 저장소 링크를 클릭하여 복사 활동의 연결된 서비스, 데이터 집합 및 소스/싱크에 대한 JSON 스키마를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-479">Click the link for the store you are interested in to see the JSON schemas for linked service, dataset, and the source/sink for the copy activity.</span></span>

| <span data-ttu-id="3b729-480">Category</span><span class="sxs-lookup"><span data-stu-id="3b729-480">Category</span></span> | <span data-ttu-id="3b729-481">데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="3b729-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="3b729-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="3b729-482">**Azure**</span></span> |[<span data-ttu-id="3b729-483">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="3b729-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="3b729-484">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="3b729-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="3b729-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3b729-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="3b729-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3b729-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="3b729-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b729-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="3b729-488">Azure 검색</span><span class="sxs-lookup"><span data-stu-id="3b729-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="3b729-489">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="3b729-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="3b729-490">**데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="3b729-490">**Databases**</span></span> |[<span data-ttu-id="3b729-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="3b729-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="3b729-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="3b729-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="3b729-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="3b729-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="3b729-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="3b729-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="3b729-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3b729-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="3b729-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b729-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="3b729-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b729-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="3b729-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3b729-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="3b729-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="3b729-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="3b729-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="3b729-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="3b729-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="3b729-501">**NoSQL**</span></span> |[<span data-ttu-id="3b729-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="3b729-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="3b729-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="3b729-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="3b729-504">**파일**</span><span class="sxs-lookup"><span data-stu-id="3b729-504">**File**</span></span> |[<span data-ttu-id="3b729-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="3b729-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="3b729-506">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="3b729-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="3b729-507">FTP</span><span class="sxs-lookup"><span data-stu-id="3b729-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="3b729-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="3b729-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="3b729-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="3b729-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="3b729-510">**기타**</span><span class="sxs-lookup"><span data-stu-id="3b729-510">**Others**</span></span> |[<span data-ttu-id="3b729-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="3b729-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="3b729-512">OData</span><span class="sxs-lookup"><span data-stu-id="3b729-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="3b729-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="3b729-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="3b729-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="3b729-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="3b729-515">웹 테이블</span><span class="sxs-lookup"><span data-stu-id="3b729-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="3b729-516">데이터 이동</span><span class="sxs-lookup"><span data-stu-id="3b729-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-517">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-517">Linked service</span></span>
<span data-ttu-id="3b729-518">연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="3b729-519">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="3b729-520">**계정 키**를 사용하여 Azure 저장소 계정을 데이터 팩터리에 연결하려면 Azure Storage 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-520">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="3b729-521">Azure Storage 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureStorage**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-521">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="3b729-522">그런 다음 **typeProperties** 섹션에서 다음 속성을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-522">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-523">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-523">Property</span></span> | <span data-ttu-id="3b729-524">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-524">Description</span></span> | <span data-ttu-id="3b729-525">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-526">connectionString</span></span> |<span data-ttu-id="3b729-527">connectionString 속성에 대한 Azure 저장소에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-527">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="3b729-528">예</span><span class="sxs-lookup"><span data-stu-id="3b729-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="3b729-529">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-529">Example</span></span>  

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="3b729-530">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="3b729-531">Azure 저장소 SAS 연결된 서비스에서 SAS(공유 액세스 서명)을 사용하여 Azure 저장소 계정을 Azure Data Factory에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-531">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="3b729-532">이 서비스는 저장소의 모든/특정 리소스(Blob/컨테이너)에 대해 제한된/시간 제한 액세스를 데이터 팩터리에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-532">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="3b729-533">공유 액세스 서명을 사용하여 Azure 저장소 계정을 데이터 팩터리에 연결하려면 Azure Storage SAS 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-533">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="3b729-534">Azure Storage SAS 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureStorageSas**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-534">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="3b729-535">그런 다음 **typeProperties** 섹션에서 다음 속성을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-535">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="3b729-536">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-536">Property</span></span> | <span data-ttu-id="3b729-537">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-537">Description</span></span> | <span data-ttu-id="3b729-538">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="3b729-539">sasUri</span></span> |<span data-ttu-id="3b729-540">BLOB, 컨테이너, 테이블 등의 Azure 저장소 리소스에 공유 액세스 서명 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-540">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="3b729-541">예</span><span class="sxs-lookup"><span data-stu-id="3b729-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="3b729-542">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-542">Example</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="3b729-543">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Blob Storage 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-544">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-544">Dataset</span></span>
<span data-ttu-id="3b729-545">Azure Blob 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureBlob**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-545">To define an Azure Blob dataset, set the **type** of the dataset to **AzureBlob**.</span></span> <span data-ttu-id="3b729-546">그런 다음 **typeProperties** 섹션에서 다음 Azure Blob 특정 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-546">Then, specify the following Azure Blob specific properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-547">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-547">Property</span></span> | <span data-ttu-id="3b729-548">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-548">Description</span></span> | <span data-ttu-id="3b729-549">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-550">folderPath</span></span> |<span data-ttu-id="3b729-551">blob 저장소에서 컨테이너 및 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-551">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="3b729-552">예제: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="3b729-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="3b729-553">예</span><span class="sxs-lookup"><span data-stu-id="3b729-553">Yes</span></span> |
| <span data-ttu-id="3b729-554">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-554">fileName</span></span> |<span data-ttu-id="3b729-555">Blob의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-555">Name of the blob.</span></span> <span data-ttu-id="3b729-556">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="3b729-557">filename을 지정하는 경우 활동(복사 포함)은 특정 Blob에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-557">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="3b729-558">fileName을 지정하지 않으면 복사는 입력 데이터 집합에 대한 folderPath에 모든 Blob을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-558">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="3b729-559">fileName이 출력 데이터 집합에 대해 지정되지 않으면 생성된 파일의 이름은 다음 형식을 사용합니다. Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-559">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3b729-560">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-560">No</span></span> |
| <span data-ttu-id="3b729-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-561">partitionedBy</span></span> |<span data-ttu-id="3b729-562">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="3b729-563">동적 folderPath 및 시계열 데이터에 대한 filename을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-563">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="3b729-564">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-565">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-565">No</span></span> |
| <span data-ttu-id="3b729-566">format</span><span class="sxs-lookup"><span data-stu-id="3b729-566">format</span></span> | <span data-ttu-id="3b729-567">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-567">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-568">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-568">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-569">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-570">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-570">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-571">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-571">No</span></span> |
| <span data-ttu-id="3b729-572">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-572">compression</span></span> | <span data-ttu-id="3b729-573">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-573">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-574">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-575">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-576">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-577">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-578">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-578">Example</span></span>

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


<span data-ttu-id="3b729-579">자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="3b729-580">복사 활동의 BlobSource</span><span class="sxs-lookup"><span data-stu-id="3b729-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="3b729-581">Azure Blob Storage에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **BlobSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-581">If you are copying data from an Azure Blob Storage, set the **source type** of the copy activity to **BlobSource**, and specify following properties in the **source **section:</span></span>

| <span data-ttu-id="3b729-582">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-582">Property</span></span> | <span data-ttu-id="3b729-583">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-583">Description</span></span> | <span data-ttu-id="3b729-584">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-584">Allowed values</span></span> | <span data-ttu-id="3b729-585">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-586">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-586">recursive</span></span> |<span data-ttu-id="3b729-587">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-587">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-588">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="3b729-588">True (default value), False</span></span> |<span data-ttu-id="3b729-589">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="3b729-590">예제: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="3b729-590">Example: BlobSource**</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="3b729-591">복사 활동의 BlobSink</span><span class="sxs-lookup"><span data-stu-id="3b729-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="3b729-592">Azure Blob Storage에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **BlobSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-592">If you are copying data to an Azure Blob Storage, set the **sink type** of the copy activity to **BlobSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-593">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-593">Property</span></span> | <span data-ttu-id="3b729-594">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-594">Description</span></span> | <span data-ttu-id="3b729-595">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-595">Allowed values</span></span> | <span data-ttu-id="3b729-596">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="3b729-597">copyBehavior</span></span> |<span data-ttu-id="3b729-598">원본이 BlobSource 또는 FileSystem인 경우 복사 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-598">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="3b729-599"><b>PreserveHierarchy</b>: 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-599"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="3b729-600">원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-600">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="3b729-601"><b>FlattenHierarchy</b>: 원본 폴더의 모든 파일은 대상 폴더의 첫 번째 수준에 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-601"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="3b729-602">대상 파일은 자동 생성된 이름을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-602">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="3b729-603"><b>MergeFiles(기본값):</b> 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-603"><b>MergeFiles (default):</b> merges all files from the source folder to one file.</span></span> <span data-ttu-id="3b729-604">파일/Blob 이름이 지정된 경우 지정된 이름이 병합된 파일 이름이 됩니다. 그렇지 않으면 자동 생성된 파일 이름이 병합된 파일 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-604">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="3b729-605">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="3b729-606">예제: BlobSink</span><span class="sxs-lookup"><span data-stu-id="3b729-606">Example: BlobSink</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-607">자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="3b729-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3b729-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-609">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-609">Linked service</span></span>
<span data-ttu-id="3b729-610">Azure Data Lake Store 연결된 서비스를 정의하려면 연결된 서비스의 type을 **AzureDataLakeStore**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-610">To define an Azure Data Lake Store linked service, set the type of the linked service to **AzureDataLakeStore**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-611">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-611">Property</span></span> | <span data-ttu-id="3b729-612">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-612">Description</span></span> | <span data-ttu-id="3b729-613">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-614">type</span><span class="sxs-lookup"><span data-stu-id="3b729-614">type</span></span> | <span data-ttu-id="3b729-615">type 속성은 **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="3b729-615">The type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="3b729-616">예</span><span class="sxs-lookup"><span data-stu-id="3b729-616">Yes</span></span> |
| <span data-ttu-id="3b729-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="3b729-617">dataLakeStoreUri</span></span> | <span data-ttu-id="3b729-618">Azure 데이터 레이크 저장소 계정에 대한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-618">Specify information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="3b729-619">형식 예: `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="3b729-619">It is in the following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="3b729-620">예</span><span class="sxs-lookup"><span data-stu-id="3b729-620">Yes</span></span> |
| <span data-ttu-id="3b729-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3b729-621">subscriptionId</span></span> | <span data-ttu-id="3b729-622">Data Lake Store가 속하는 Azure 구독 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-622">Azure subscription Id to which Data Lake Store belongs.</span></span> | <span data-ttu-id="3b729-623">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="3b729-623">Required for sink</span></span> |
| <span data-ttu-id="3b729-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3b729-624">resourceGroupName</span></span> | <span data-ttu-id="3b729-625">Data Lake Store가 속하는 Azure 리소스 그룹 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-625">Azure resource group name to which Data Lake Store belongs.</span></span> | <span data-ttu-id="3b729-626">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="3b729-626">Required for sink</span></span> |
| <span data-ttu-id="3b729-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="3b729-627">servicePrincipalId</span></span> | <span data-ttu-id="3b729-628">응용 프로그램의 클라이언트 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-628">Specify the application's client ID.</span></span> | <span data-ttu-id="3b729-629">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="3b729-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="3b729-630">servicePrincipalKey</span></span> | <span data-ttu-id="3b729-631">응용 프로그램의 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-631">Specify the application's key.</span></span> | <span data-ttu-id="3b729-632">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="3b729-633">tenant</span><span class="sxs-lookup"><span data-stu-id="3b729-633">tenant</span></span> | <span data-ttu-id="3b729-634">응용 프로그램이 있는 테넌트 정보(도메인 이름 또는 테넌트 ID)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-634">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="3b729-635">Azure Portal의 오른쪽 위 모서리에 마우스를 이동하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-635">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> | <span data-ttu-id="3b729-636">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="3b729-637">authorization</span><span class="sxs-lookup"><span data-stu-id="3b729-637">authorization</span></span> | <span data-ttu-id="3b729-638">**Data Factory 편집기**에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 자동 생성된 authorization URL이 이 속성에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-638">Click **Authorize** button in the **Data Factory Editor** and enter your credential that assigns the auto-generated authorization URL to this property.</span></span> | <span data-ttu-id="3b729-639">예(사용자 자격 증명 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="3b729-640">sessionid</span><span class="sxs-lookup"><span data-stu-id="3b729-640">sessionId</span></span> | <span data-ttu-id="3b729-641">OAuth 권한 부여 세션에서 가져온 OAuth 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-641">OAuth session id from the OAuth authorization session.</span></span> <span data-ttu-id="3b729-642">각 세션 ID는 고유하고 한 번만 사용될 수 있으며 </span><span class="sxs-lookup"><span data-stu-id="3b729-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="3b729-643">이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="3b729-644">예(사용자 자격 증명 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="3b729-645">예제: 서비스 주체 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-645">Example: using service principal authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="3b729-646">예제: 사용자 자격 증명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-646">Example: using user credential authentication</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

<span data-ttu-id="3b729-647">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-648">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-648">Dataset</span></span>
<span data-ttu-id="3b729-649">Azure Data Lake Store 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureDataLakeStore**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-649">To define an Azure Data Lake Store dataset, set the **type** of the dataset to **AzureDataLakeStore**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-650">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-650">Property</span></span> | <span data-ttu-id="3b729-651">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-651">Description</span></span> | <span data-ttu-id="3b729-652">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-653">folderPath</span></span> |<span data-ttu-id="3b729-654">Azure 데이터 레이크 저장소의 컨테이너 및 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-654">Path to the container and folder in the Azure Data Lake store.</span></span> |<span data-ttu-id="3b729-655">예</span><span class="sxs-lookup"><span data-stu-id="3b729-655">Yes</span></span> |
| <span data-ttu-id="3b729-656">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-656">fileName</span></span> |<span data-ttu-id="3b729-657">Azure 데이터 레이크 저장소에 있는 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-657">Name of the file in the Azure Data Lake store.</span></span> <span data-ttu-id="3b729-658">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="3b729-659">filename을 지정하는 경우 활동(복사 포함)은 특정 파일에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-659">If you specify a filename, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="3b729-660">fileName을 지정하지 않으면 복사는 입력 데이터 집합에 대한 folderPath에 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-660">When fileName is not specified, Copy includes all files in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="3b729-661">fileName이 출력 데이터 집합에 대해 지정되지 않으면 생성된 파일의 이름은 다음 형식을 사용합니다. Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-661">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3b729-662">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-662">No</span></span> |
| <span data-ttu-id="3b729-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-663">partitionedBy</span></span> |<span data-ttu-id="3b729-664">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="3b729-665">동적 folderPath 및 시계열 데이터에 대한 filename을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-665">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="3b729-666">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-667">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-667">No</span></span> |
| <span data-ttu-id="3b729-668">format</span><span class="sxs-lookup"><span data-stu-id="3b729-668">format</span></span> | <span data-ttu-id="3b729-669">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-669">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-670">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-670">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-671">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-672">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-672">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-673">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-673">No</span></span> |
| <span data-ttu-id="3b729-674">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-674">compression</span></span> | <span data-ttu-id="3b729-675">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-675">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-676">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-677">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-678">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-679">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-680">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-680">Example</span></span>
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-681">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="3b729-682">복사 활동의 Azure Data Lake Store 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="3b729-683">Azure Data Lake Store에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **AzureDataLakeStoreSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-683">If you are copying data from an Azure Data Lake Store, set the **source type** of the copy activity to **AzureDataLakeStoreSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="3b729-684">**AzureDataLakeStoreSource**는 **typeProperties** 섹션에서 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-684">**AzureDataLakeStoreSource** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="3b729-685">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-685">Property</span></span> | <span data-ttu-id="3b729-686">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-686">Description</span></span> | <span data-ttu-id="3b729-687">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-687">Allowed values</span></span> | <span data-ttu-id="3b729-688">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-689">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-689">recursive</span></span> |<span data-ttu-id="3b729-690">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-690">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-691">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="3b729-691">True (default value), False</span></span> |<span data-ttu-id="3b729-692">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="3b729-693">예제: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="3b729-693">Example: AzureDataLakeStoreSource</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-694">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="3b729-695">복사 활동의 Azure Data Lake Store 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-696">Azure Data Lake Store에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **AzureDataLakeStoreSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-696">If you are copying data to an Azure Data Lake Store, set the **sink type** of the copy activity to **AzureDataLakeStoreSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-697">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-697">Property</span></span> | <span data-ttu-id="3b729-698">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-698">Description</span></span> | <span data-ttu-id="3b729-699">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-699">Allowed values</span></span> | <span data-ttu-id="3b729-700">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="3b729-701">copyBehavior</span></span> |<span data-ttu-id="3b729-702">복사 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-702">Specifies the copy behavior.</span></span> |<span data-ttu-id="3b729-703"><b>PreserveHierarchy</b>: 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-703"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="3b729-704">원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-704">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="3b729-705"><b>FlattenHierarchy</b>: 원본 폴더의 모든 파일이 대상 폴더의 첫 번째 수준에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-705"><b>FlattenHierarchy</b>: all files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="3b729-706">대상 파일은 자동 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-706">The target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="3b729-707"><b>MergeFiles</b>: 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-707"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="3b729-708">파일/Blob 이름이 지정된 경우 지정된 이름이 병합된 파일 이름이 됩니다. 그렇지 않으면 자동 생성된 파일 이름이 병합된 파일 이름이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-708">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="3b729-709">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="3b729-710">예제: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="3b729-710">Example: AzureDataLakeStoreSink</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-711">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="3b729-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3b729-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="3b729-713">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-713">Linked service</span></span>
<span data-ttu-id="3b729-714">Azure Cosmos DB 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **DocumentDb**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-714">To define an Azure Cosmos DB linked service, set the **type** of the linked service to **DocumentDb**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-715">**속성**</span><span class="sxs-lookup"><span data-stu-id="3b729-715">**Property**</span></span> | <span data-ttu-id="3b729-716">**설명**</span><span class="sxs-lookup"><span data-stu-id="3b729-716">**Description**</span></span> | <span data-ttu-id="3b729-717">**필수**</span><span class="sxs-lookup"><span data-stu-id="3b729-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-718">connectionString</span></span> |<span data-ttu-id="3b729-719">Azure Cosmos DB 데이터베이스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-719">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="3b729-720">예</span><span class="sxs-lookup"><span data-stu-id="3b729-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-721">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-721">Example</span></span>

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
<span data-ttu-id="3b729-722">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-723">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-723">Dataset</span></span>
<span data-ttu-id="3b729-724">Azure Cosmos DB 데이터 집합을 정의하려면 데이터 집합의 **type**을 **DocumentDbCollection**으로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-724">To define an Azure Cosmos DB dataset, set the **type** of the dataset to **DocumentDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-725">**속성**</span><span class="sxs-lookup"><span data-stu-id="3b729-725">**Property**</span></span> | <span data-ttu-id="3b729-726">**설명**</span><span class="sxs-lookup"><span data-stu-id="3b729-726">**Description**</span></span> | <span data-ttu-id="3b729-727">**필수**</span><span class="sxs-lookup"><span data-stu-id="3b729-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="3b729-728">collectionName</span></span> |<span data-ttu-id="3b729-729">Azure Cosmos DB 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-729">Name of the Azure Cosmos DB collection.</span></span> |<span data-ttu-id="3b729-730">예</span><span class="sxs-lookup"><span data-stu-id="3b729-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-731">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-731">Example</span></span>

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="3b729-732">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="3b729-733">복사 작업에서 Azure Cosmos DB 컬렉션 원본</span><span class="sxs-lookup"><span data-stu-id="3b729-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="3b729-734">Azure Cosmos DB에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **DocumentDbCollectionSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-734">If you are copying data from an Azure Cosmos DB, set the **source type** of the copy activity to **DocumentDbCollectionSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-735">**속성**</span><span class="sxs-lookup"><span data-stu-id="3b729-735">**Property**</span></span> | <span data-ttu-id="3b729-736">**설명**</span><span class="sxs-lookup"><span data-stu-id="3b729-736">**Description**</span></span> | <span data-ttu-id="3b729-737">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="3b729-737">**Allowed values**</span></span> | <span data-ttu-id="3b729-738">**필수**</span><span class="sxs-lookup"><span data-stu-id="3b729-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-739">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-739">query</span></span> |<span data-ttu-id="3b729-740">데이터를 읽는 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-740">Specify the query to read data.</span></span> |<span data-ttu-id="3b729-741">Azure Cosmos DB에서 지원하는 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="3b729-742">예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="3b729-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="3b729-743">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-743">No</span></span> <br/><br/><span data-ttu-id="3b729-744">지정하지 않는 경우 실행되는 SQL 문: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="3b729-744">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="3b729-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="3b729-745">nestingSeparator</span></span> |<span data-ttu-id="3b729-746">문서가 중첩됨을 나타내는 특수 문자</span><span class="sxs-lookup"><span data-stu-id="3b729-746">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="3b729-747">모든 character입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-747">Any character.</span></span> <br/><br/><span data-ttu-id="3b729-748">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="3b729-749">Azure 데이터 팩터리를 사용하면 nestingSeparator, 즉 위 예에서 "."를 통해 계층 구조를</span><span class="sxs-lookup"><span data-stu-id="3b729-749">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="3b729-750">표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-750">in the above examples.</span></span> <span data-ttu-id="3b729-751">테이블 정의에서 "Name.First", "Name.Middle" 및 "Name.Last"에 따르면 구분 기호를 사용하여 복사 작업이 3개의 자식 요소(처음, 중간 및 마지막)가 있는 "Name" 개체를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-751">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="3b729-752">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-753">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-753">Example</span></span>

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="3b729-754">복사 작업의 Azure Cosmos DB 컬렉션 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-755">Azure Cosmos DB에 데이터를 복사하는 경우 복사 작업의 **sink type**을 **DocumentDbCollectionSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-755">If you are copying data to Azure Cosmos DB, set the **sink type** of the copy activity to **DocumentDbCollectionSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-756">**속성**</span><span class="sxs-lookup"><span data-stu-id="3b729-756">**Property**</span></span> | <span data-ttu-id="3b729-757">**설명**</span><span class="sxs-lookup"><span data-stu-id="3b729-757">**Description**</span></span> | <span data-ttu-id="3b729-758">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="3b729-758">**Allowed values**</span></span> | <span data-ttu-id="3b729-759">**필수**</span><span class="sxs-lookup"><span data-stu-id="3b729-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="3b729-760">nestingSeparator</span></span> |<span data-ttu-id="3b729-761">중첩된 해당 문서를 나타내는 원본 열 이름에 특수 문자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-761">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="3b729-762">위의 예에서 출력 테이블의 `Name.First`는 Cosmos DB 문서에서 다음 JSON 구조를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-762">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="3b729-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="3b729-763">"Name": {</span></span><br/>    <span data-ttu-id="3b729-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="3b729-764">"First": "John"</span></span><br/><span data-ttu-id="3b729-765">},</span><span class="sxs-lookup"><span data-stu-id="3b729-765">},</span></span> |<span data-ttu-id="3b729-766">중첩 수준을 구분하는데 사용되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-766">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="3b729-767">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="3b729-768">중첩 수준을 구분하는데 사용되는 문자입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-768">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="3b729-769">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="3b729-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-770">writeBatchSize</span></span> |<span data-ttu-id="3b729-771">문서를 작성하는 Azure Cosmos DB 서비스에 대한 병렬 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-771">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="3b729-772">이 속성을 사용하여 Azure Cosmos DB 간 데이터를 복사하는 경우 성능을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-772">You can fine-tune the performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="3b729-773">Azure Cosmos DB에 더 많은 병렬 요청이 전송되기 때문에 writeBatchSize 증가하는 경우 더 나은 성능을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-773">You can expect a better performance when you increase writeBatchSize because more parallel requests to Azure Cosmos DB are sent.</span></span> <span data-ttu-id="3b729-774">하지만 오류 메시지: “요청 빈도가 높습니다."를 발생 시킬 수 있는 제한을 방지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-774">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="3b729-775">제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 활동의 경우 더 나은 컬렉션(예: S3)을 사용하여 가장 많은 처리량(2,500 요청 단위/초)을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="3b729-776">Integer</span><span class="sxs-lookup"><span data-stu-id="3b729-776">Integer</span></span> |<span data-ttu-id="3b729-777">아니요(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="3b729-777">No (default: 5)</span></span> |
| <span data-ttu-id="3b729-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-778">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-779">시간이 초과 되기 전에 완료하려는 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-779">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="3b729-780">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-780">timespan</span></span><br/><br/> <span data-ttu-id="3b729-781">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="3b729-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3b729-782">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-783">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-783">Example</span></span>

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

<span data-ttu-id="3b729-784">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="3b729-785">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3b729-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-786">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-786">Linked service</span></span>
<span data-ttu-id="3b729-787">Azure SQL Database 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureSqlDatabase**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-787">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-788">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-788">Property</span></span> | <span data-ttu-id="3b729-789">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-789">Description</span></span> | <span data-ttu-id="3b729-790">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-791">connectionString</span></span> |<span data-ttu-id="3b729-792">connectionString 속성에 대한 Azure SQL 데이터베이스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-792">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="3b729-793">예</span><span class="sxs-lookup"><span data-stu-id="3b729-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-794">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-794">Example</span></span>
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="3b729-795">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-796">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-796">Dataset</span></span>
<span data-ttu-id="3b729-797">Azure SQL Database 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureSqlTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-797">To define an Azure SQL Database dataset, set the **type** of the dataset to **AzureSqlTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-798">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-798">Property</span></span> | <span data-ttu-id="3b729-799">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-799">Description</span></span> | <span data-ttu-id="3b729-800">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-801">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-801">tableName</span></span> |<span data-ttu-id="3b729-802">연결된 서비스가 참조하는 Azure SQL 데이터베이스 인스턴스에서 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-802">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b729-803">예</span><span class="sxs-lookup"><span data-stu-id="3b729-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-804">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-804">Example</span></span>

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="3b729-805">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="3b729-806">복사 활동의 SQL 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="3b729-807">Azure SQL Database에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **SqlSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-807">If you are copying data from an Azure SQL Database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-808">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-808">Property</span></span> | <span data-ttu-id="3b729-809">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-809">Description</span></span> | <span data-ttu-id="3b729-810">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-810">Allowed values</span></span> | <span data-ttu-id="3b729-811">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3b729-812">sqlReaderQuery</span></span> |<span data-ttu-id="3b729-813">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-813">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-814">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-814">SQL query string.</span></span> <span data-ttu-id="3b729-815">예: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="3b729-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-816">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-816">No</span></span> |
| <span data-ttu-id="3b729-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="3b729-818">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-818">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="3b729-819">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-819">Name of the stored procedure.</span></span> |<span data-ttu-id="3b729-820">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-820">No</span></span> |
| <span data-ttu-id="3b729-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-821">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-822">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-822">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3b729-823">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-823">Name/value pairs.</span></span> <span data-ttu-id="3b729-824">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-824">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3b729-825">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-826">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-826">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="3b729-827">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="3b729-828">복사 활동의 SQL 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-829">Azure SQL Database에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **SqlSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-829">If you are copying data to Azure SQL Database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-830">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-830">Property</span></span> | <span data-ttu-id="3b729-831">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-831">Description</span></span> | <span data-ttu-id="3b729-832">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-832">Allowed values</span></span> | <span data-ttu-id="3b729-833">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-834">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-835">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-835">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3b729-836">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-836">timespan</span></span><br/><br/> <span data-ttu-id="3b729-837">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="3b729-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3b729-838">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-838">No</span></span> |
| <span data-ttu-id="3b729-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-839">writeBatchSize</span></span> |<span data-ttu-id="3b729-840">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="3b729-840">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="3b729-841">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="3b729-841">Integer (number of rows)</span></span> |<span data-ttu-id="3b729-842">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="3b729-842">No (default: 10000)</span></span> |
| <span data-ttu-id="3b729-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3b729-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3b729-844">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-844">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="3b729-845">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-845">A query statement.</span></span> |<span data-ttu-id="3b729-846">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-846">No</span></span> |
| <span data-ttu-id="3b729-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3b729-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="3b729-848">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-848">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="3b729-849">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="3b729-850">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-850">No</span></span> |
| <span data-ttu-id="3b729-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="3b729-852">대상 테이블에 대한 데이터 Upsert(업데이트/삽입)를 수행하는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-852">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="3b729-853">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-853">Name of the stored procedure.</span></span> |<span data-ttu-id="3b729-854">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-854">No</span></span> |
| <span data-ttu-id="3b729-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-855">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-856">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-856">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3b729-857">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-857">Name/value pairs.</span></span> <span data-ttu-id="3b729-858">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-858">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3b729-859">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-859">No</span></span> |
| <span data-ttu-id="3b729-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="3b729-860">sqlWriterTableType</span></span> |<span data-ttu-id="3b729-861">저장 프로시저에 사용할 테이블 형식 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-861">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="3b729-862">복사 작업을 사용하면 이 테이블 형식으로 임시 테이블에서 사용할 수 있는 데이터를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-862">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="3b729-863">그러면 저장 프로시저 코드가 복사되는 데이터를 기존 데이터와 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-863">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="3b729-864">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-864">A table type name.</span></span> |<span data-ttu-id="3b729-865">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-866">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-866">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-867">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="3b729-868">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="3b729-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-869">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-869">Linked service</span></span>
<span data-ttu-id="3b729-870">Azure SQL Data Warehouse 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureSqlDW**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-870">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-871">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-871">Property</span></span> | <span data-ttu-id="3b729-872">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-872">Description</span></span> | <span data-ttu-id="3b729-873">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-874">connectionString</span></span> |<span data-ttu-id="3b729-875">connectionString 속성에 대한 Azure SQL 데이터 웨어하우스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-875">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="3b729-876">예</span><span class="sxs-lookup"><span data-stu-id="3b729-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="3b729-877">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-877">Example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="3b729-878">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-879">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-879">Dataset</span></span>
<span data-ttu-id="3b729-880">Azure SQL Data Warehouse 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureSqlDWTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-880">To define an Azure SQL Data Warehouse dataset, set the **type** of the dataset to **AzureSqlDWTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-881">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-881">Property</span></span> | <span data-ttu-id="3b729-882">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-882">Description</span></span> | <span data-ttu-id="3b729-883">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-884">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-884">tableName</span></span> |<span data-ttu-id="3b729-885">연결된 서비스에서 참조하는 Azure SQL Data Warehouse 데이터베이스에 있는 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-885">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="3b729-886">예</span><span class="sxs-lookup"><span data-stu-id="3b729-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-887">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-887">Example</span></span>

```json
{
    "name": "AzureSqlDWInput",
    "properties": {
    "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-888">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="3b729-889">복사 활동의 SQL DW 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="3b729-890">Azure SQL Data Warehouse에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **SqlDWSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-890">If you are copying data from Azure SQL Data Warehouse, set the **source type** of the copy activity to **SqlDWSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-891">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-891">Property</span></span> | <span data-ttu-id="3b729-892">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-892">Description</span></span> | <span data-ttu-id="3b729-893">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-893">Allowed values</span></span> | <span data-ttu-id="3b729-894">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3b729-895">sqlReaderQuery</span></span> |<span data-ttu-id="3b729-896">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-896">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-897">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-897">SQL query string.</span></span> <span data-ttu-id="3b729-898">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-899">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-899">No</span></span> |
| <span data-ttu-id="3b729-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="3b729-901">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-901">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="3b729-902">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-902">Name of the stored procedure.</span></span> |<span data-ttu-id="3b729-903">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-903">No</span></span> |
| <span data-ttu-id="3b729-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-904">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-905">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-905">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3b729-906">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-906">Name/value pairs.</span></span> <span data-ttu-id="3b729-907">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-907">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3b729-908">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-909">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-909">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlDWSource",
                    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-910">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="3b729-911">복사 활동의 SQL DW 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-912">Azure SQL Data Warehouse에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **SqlDWSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-912">If you are copying data to Azure SQL Data Warehouse, set the **sink type** of the copy activity to **SqlDWSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-913">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-913">Property</span></span> | <span data-ttu-id="3b729-914">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-914">Description</span></span> | <span data-ttu-id="3b729-915">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-915">Allowed values</span></span> | <span data-ttu-id="3b729-916">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3b729-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3b729-918">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-918">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="3b729-919">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-919">A query statement.</span></span> |<span data-ttu-id="3b729-920">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-920">No</span></span> |
| <span data-ttu-id="3b729-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="3b729-921">allowPolyBase</span></span> |<span data-ttu-id="3b729-922">BULKINSERT 메커니즘 대신 PolyBase(있는 경우)를 사용할지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-922">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="3b729-923">**PolyBase를 사용하여 SQL Data Warehouse에 데이터를 로드하는 것이 좋습니다.**</span><span class="sxs-lookup"><span data-stu-id="3b729-923">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="3b729-924">True </span><span class="sxs-lookup"><span data-stu-id="3b729-924">True</span></span> <br/><span data-ttu-id="3b729-925">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-925">False (default)</span></span> |<span data-ttu-id="3b729-926">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-926">No</span></span> |
| <span data-ttu-id="3b729-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="3b729-927">polyBaseSettings</span></span> |<span data-ttu-id="3b729-928">**allowPolybase** 속성이 **true**로 설정된 경우 지정될 수 있는 속성의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-928">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="3b729-929">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-929">No</span></span> |
| <span data-ttu-id="3b729-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="3b729-930">rejectValue</span></span> |<span data-ttu-id="3b729-931">쿼리가 실패하기 전에 거부될 수 있는 행의 수 또는 백분율을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-931">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="3b729-932">**외부 테이블 만들기(Transact-SQL)** 토픽의 [인수](https://msdn.microsoft.com/library/dn935021.aspx) 섹션에 있는 PolyBase의 거부 옵션에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-932">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="3b729-933">0(기본값), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="3b729-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="3b729-934">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-934">No</span></span> |
| <span data-ttu-id="3b729-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="3b729-935">rejectType</span></span> |<span data-ttu-id="3b729-936">rejectValue 옵션을 리터럴 값 또는 백분율로 지정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-936">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="3b729-937">값(기본값), 백분율</span><span class="sxs-lookup"><span data-stu-id="3b729-937">Value (default), Percentage</span></span> |<span data-ttu-id="3b729-938">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-938">No</span></span> |
| <span data-ttu-id="3b729-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="3b729-939">rejectSampleValue</span></span> |<span data-ttu-id="3b729-940">PolyBase가 거부된 행의 비율을 다시 계산하기 전에 검색할 행 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-940">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="3b729-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="3b729-941">1, 2, …</span></span> |<span data-ttu-id="3b729-942">예. **rejectType**이 **백분율**인 경우</span><span class="sxs-lookup"><span data-stu-id="3b729-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="3b729-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="3b729-943">useTypeDefault</span></span> |<span data-ttu-id="3b729-944">PolyBase가 텍스트 파일에서 데이터를 검색할 경우 구분된 텍스트 파일에서 누락된 값을 처리하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-944">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="3b729-945">[외부 파일 서식 만들기(Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx)를 사용하여 파이프라인을 만드는 데 사용할 수 있는 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-945">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="3b729-946">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-946">True, False (default)</span></span> |<span data-ttu-id="3b729-947">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-947">No</span></span> |
| <span data-ttu-id="3b729-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-948">writeBatchSize</span></span> |<span data-ttu-id="3b729-949">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="3b729-949">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="3b729-950">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="3b729-950">Integer (number of rows)</span></span> |<span data-ttu-id="3b729-951">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="3b729-951">No (default: 10000)</span></span> |
| <span data-ttu-id="3b729-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-952">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-953">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-953">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3b729-954">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-954">timespan</span></span><br/><br/> <span data-ttu-id="3b729-955">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="3b729-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3b729-956">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-957">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-957">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
            "typeProperties": {
                "source": {
                "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlDWSink",
                    "allowPolyBase": true
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-958">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="3b729-959">Azure 검색</span><span class="sxs-lookup"><span data-stu-id="3b729-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-960">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-960">Linked service</span></span>
<span data-ttu-id="3b729-961">Azure Search 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureSearch**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-961">To define an Azure Search linked service, set the **type** of the linked service to **AzureSearch**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-962">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-962">Property</span></span> | <span data-ttu-id="3b729-963">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-963">Description</span></span> | <span data-ttu-id="3b729-964">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="3b729-965">URL</span><span class="sxs-lookup"><span data-stu-id="3b729-965">url</span></span> | <span data-ttu-id="3b729-966">Azure Search 서비스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-966">URL for the Azure Search service.</span></span> | <span data-ttu-id="3b729-967">예</span><span class="sxs-lookup"><span data-stu-id="3b729-967">Yes</span></span> |
| <span data-ttu-id="3b729-968">key</span><span class="sxs-lookup"><span data-stu-id="3b729-968">key</span></span> | <span data-ttu-id="3b729-969">Azure Search 서비스의 관리자 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-969">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="3b729-970">예</span><span class="sxs-lookup"><span data-stu-id="3b729-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-971">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-971">Example</span></span>

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="3b729-972">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-973">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-973">Dataset</span></span>
<span data-ttu-id="3b729-974">Azure Search 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureSearchIndex**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-974">To define an Azure Search dataset, set the **type** of the dataset to **AzureSearchIndex**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-975">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-975">Property</span></span> | <span data-ttu-id="3b729-976">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-976">Description</span></span> | <span data-ttu-id="3b729-977">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="3b729-978">type</span><span class="sxs-lookup"><span data-stu-id="3b729-978">type</span></span> | <span data-ttu-id="3b729-979">형식 속성은 **AzureSearchIndex**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-979">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="3b729-980">예</span><span class="sxs-lookup"><span data-stu-id="3b729-980">Yes</span></span> |
| <span data-ttu-id="3b729-981">indexName</span><span class="sxs-lookup"><span data-stu-id="3b729-981">indexName</span></span> | <span data-ttu-id="3b729-982">Azure 검색 인덱스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-982">Name of the Azure Search index.</span></span> <span data-ttu-id="3b729-983">Data Factory는 인덱스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-983">Data Factory does not create the index.</span></span> <span data-ttu-id="3b729-984">Azure Search에는 인덱스가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-984">The index must exist in Azure Search.</span></span> | <span data-ttu-id="3b729-985">예</span><span class="sxs-lookup"><span data-stu-id="3b729-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-986">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-986">Example</span></span>

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

<span data-ttu-id="3b729-987">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="3b729-988">복사 활동의 Azure Search 인덱스 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-989">Azure Search 인덱스에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **AzureSearchIndexSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-989">If you are copying data to an Azure Search index, set the **sink type** of the copy activity to **AzureSearchIndexSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-990">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-990">Property</span></span> | <span data-ttu-id="3b729-991">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-991">Description</span></span> | <span data-ttu-id="3b729-992">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-992">Allowed values</span></span> | <span data-ttu-id="3b729-993">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="3b729-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="3b729-994">WriteBehavior</span></span> | <span data-ttu-id="3b729-995">문서가 인덱스에 이미 있는 경우 병합할지 또는 바꿀지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-995">Specifies whether to merge or replace when a document already exists in the index.</span></span> | <span data-ttu-id="3b729-996">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-996">Merge (default)</span></span><br/><span data-ttu-id="3b729-997">업로드</span><span class="sxs-lookup"><span data-stu-id="3b729-997">Upload</span></span>| <span data-ttu-id="3b729-998">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-998">No</span></span> |
| <span data-ttu-id="3b729-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-999">WriteBatchSize</span></span> | <span data-ttu-id="3b729-1000">버퍼 크기가 writeBatchSize에 도달한 경우 Azure Search 인덱스에 데이터를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1000">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="3b729-1001">1~1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1001">1 to 1,000.</span></span> <span data-ttu-id="3b729-1002">기본값은 1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1002">Default value is 1000.</span></span> | <span data-ttu-id="3b729-1003">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1004">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1004">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1005">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="3b729-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="3b729-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1007">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1007">Linked service</span></span>
<span data-ttu-id="3b729-1008">연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="3b729-1009">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="3b729-1010">**계정 키**를 사용하여 Azure 저장소 계정을 데이터 팩터리에 연결하려면 Azure Storage 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1010">To link your Azure storage account to a data factory by using the **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="3b729-1011">Azure Storage 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureStorage**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1011">To define an Azure Storage linked service, set the **type** of the linked service to **AzureStorage**.</span></span> <span data-ttu-id="3b729-1012">그런 다음 **typeProperties** 섹션에서 다음 속성을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1012">Then, you can specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1013">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1013">Property</span></span> | <span data-ttu-id="3b729-1014">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1014">Description</span></span> | <span data-ttu-id="3b729-1015">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-1016">type</span><span class="sxs-lookup"><span data-stu-id="3b729-1016">type</span></span> |<span data-ttu-id="3b729-1017">형식 속성은 **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="3b729-1017">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="3b729-1018">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1018">Yes</span></span> |
| <span data-ttu-id="3b729-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-1019">connectionString</span></span> |<span data-ttu-id="3b729-1020">connectionString 속성에 대한 Azure 저장소에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1020">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="3b729-1021">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1021">Yes</span></span> |

<span data-ttu-id="3b729-1022">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3b729-1022">**Example:**</span></span>  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="3b729-1023">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="3b729-1024">Azure 저장소 SAS 연결된 서비스에서 SAS(공유 액세스 서명)을 사용하여 Azure 저장소 계정을 Azure Data Factory에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1024">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="3b729-1025">이 서비스는 저장소의 모든/특정 리소스(Blob/컨테이너)에 대해 제한된/시간 제한 액세스를 데이터 팩터리에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1025">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="3b729-1026">공유 액세스 서명을 사용하여 Azure 저장소 계정을 데이터 팩터리에 연결하려면 Azure Storage SAS 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1026">To link your Azure storage account to a data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="3b729-1027">Azure Storage SAS 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureStorageSas**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1027">To define an Azure Storage SAS linked service, set the **type** of the linked service to **AzureStorageSas**.</span></span> <span data-ttu-id="3b729-1028">그런 다음 **typeProperties** 섹션에서 다음 속성을 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1028">Then, you can specify following properties in the **typeProperties** section:</span></span>   

| <span data-ttu-id="3b729-1029">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1029">Property</span></span> | <span data-ttu-id="3b729-1030">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1030">Description</span></span> | <span data-ttu-id="3b729-1031">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-1032">type</span><span class="sxs-lookup"><span data-stu-id="3b729-1032">type</span></span> |<span data-ttu-id="3b729-1033">형식 속성은 **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="3b729-1033">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="3b729-1034">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1034">Yes</span></span> |
| <span data-ttu-id="3b729-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="3b729-1035">sasUri</span></span> |<span data-ttu-id="3b729-1036">BLOB, 컨테이너, 테이블 등의 Azure 저장소 리소스에 공유 액세스 서명 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1036">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="3b729-1037">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1037">Yes</span></span> |

<span data-ttu-id="3b729-1038">**예제:**</span><span class="sxs-lookup"><span data-stu-id="3b729-1038">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

<span data-ttu-id="3b729-1039">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1040">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1040">Dataset</span></span>
<span data-ttu-id="3b729-1041">Azure Table 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AzureTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1041">To define an Azure Table dataset, set the **type** of the dataset to **AzureTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1042">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1042">Property</span></span> | <span data-ttu-id="3b729-1043">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1043">Description</span></span> | <span data-ttu-id="3b729-1044">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1045">tableName</span></span> |<span data-ttu-id="3b729-1046">연결된 서비스가 참조하는 Azure 테이블 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1046">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b729-1047">예.</span><span class="sxs-lookup"><span data-stu-id="3b729-1047">Yes.</span></span> <span data-ttu-id="3b729-1048">azureTableSourceQuery 없이 tableName을 지정하면 테이블의 모든 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1048">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="3b729-1049">또한 azureTableSourceQuery를 지정하면 쿼리를 만족 하는 테이블의 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1049">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1050">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1050">Example</span></span>

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1051">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="3b729-1052">복사 활동의 Azure Table 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1053">Azure Table Storage에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **AzureTableSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1053">If you are copying data from Azure Table Storage, set the **source type** of the copy activity to **AzureTableSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1054">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1054">Property</span></span> | <span data-ttu-id="3b729-1055">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1055">Description</span></span> | <span data-ttu-id="3b729-1056">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1056">Allowed values</span></span> | <span data-ttu-id="3b729-1057">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="3b729-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="3b729-1059">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1059">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1060">Azure 테이블 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1060">Azure table query string.</span></span> <span data-ttu-id="3b729-1061">다음 섹션의 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1061">See examples in the next section.</span></span> |<span data-ttu-id="3b729-1062">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1062">No.</span></span> <span data-ttu-id="3b729-1063">azureTableSourceQuery 없이 tableName을 지정하면 테이블의 모든 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1063">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="3b729-1064">또한 azureTableSourceQuery를 지정하면 쿼리를 만족 하는 테이블의 레코드를 대상에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1064">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="3b729-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="3b729-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="3b729-1066">존재하지 않는 테이블의 예외를 받아들이는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1066">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="3b729-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="3b729-1067">TRUE</span></span><br/><span data-ttu-id="3b729-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="3b729-1068">FALSE</span></span> |<span data-ttu-id="3b729-1069">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1070">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1070">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1071">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="3b729-1072">복사 활동의 Azure Table 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-1073">Azure Table Storage에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **AzureTableSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1073">If you are copying data to Azure Table Storage, set the **sink type** of the copy activity to **AzureTableSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-1074">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1074">Property</span></span> | <span data-ttu-id="3b729-1075">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1075">Description</span></span> | <span data-ttu-id="3b729-1076">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1076">Allowed values</span></span> | <span data-ttu-id="3b729-1077">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="3b729-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="3b729-1079">싱크에서 사용할 수 있는 기본 파티션 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1079">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="3b729-1080">문자열 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1080">A string value.</span></span> |<span data-ttu-id="3b729-1081">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1081">No</span></span> |
| <span data-ttu-id="3b729-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="3b729-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="3b729-1083">해당 값이 파티션 키로 사용되는 열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1083">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="3b729-1084">지정하지 않으면 AzureTableDefaultPartitionKeyValue가 파티션 키로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="3b729-1085">열 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1085">A column name.</span></span> |<span data-ttu-id="3b729-1086">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1086">No</span></span> |
| <span data-ttu-id="3b729-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="3b729-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="3b729-1088">해당 열 값이 행 키로 사용되는 열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1088">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="3b729-1089">지정하지 않으면 각 행에 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="3b729-1090">열 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1090">A column name.</span></span> |<span data-ttu-id="3b729-1091">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1091">No</span></span> |
| <span data-ttu-id="3b729-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="3b729-1092">azureTableInsertType</span></span> |<span data-ttu-id="3b729-1093">Azure 테이블에 데이터를 삽입하는 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1093">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="3b729-1094">이 속성은 출력 테이블에서 파티션 및 행 키가 일치하는 기존 행의 값을 바꿀지 또는 병합할지 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1094">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="3b729-1095">이러한 설정(병합 및 바꾸기)이 작동하는 방법을 알아보려면 [엔터티 삽입 또는 병합](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [엔터티 삽입 또는 바꾸기](https://msdn.microsoft.com/library/azure/hh452242.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1095">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="3b729-1096">이 설정은 테이블 수준이 아니라 행 수준에서 적용되며, 두 옵션 모두 출력 테이블에서 입력에 존재하지 않는 행을 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1096">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="3b729-1097">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-1097">merge (default)</span></span><br/><span data-ttu-id="3b729-1098">바꾸기</span><span class="sxs-lookup"><span data-stu-id="3b729-1098">replace</span></span> |<span data-ttu-id="3b729-1099">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1099">No</span></span> |
| <span data-ttu-id="3b729-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-1100">writeBatchSize</span></span> |<span data-ttu-id="3b729-1101">WriteBatchSize 또는 writeBatchTimeout에 도달하면 Azure 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1101">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="3b729-1102">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="3b729-1102">Integer (number of rows)</span></span> |<span data-ttu-id="3b729-1103">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="3b729-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="3b729-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-1104">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-1105">WriteBatchSize 또는 writeBatchTimeout에 도달하면 Azure 테이블에 데이터를 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1105">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="3b729-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-1106">timespan</span></span><br/><br/><span data-ttu-id="3b729-1107">예: "00:20:00"(20분)</span><span class="sxs-lookup"><span data-stu-id="3b729-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="3b729-1108">No (기본적으로 저장소 클라이언트 기본 시간 제한 값인 90초로 설정)</span><span class="sxs-lookup"><span data-stu-id="3b729-1108">No (Default to storage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1109">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1109">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="3b729-1110">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="3b729-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="3b729-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1112">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1112">Linked service</span></span>
<span data-ttu-id="3b729-1113">Amazon Redshift 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AmazonRedshift**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1113">To define an Amazon Redshift linked service, set the **type** of the linked service to **AmazonRedshift**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1114">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1114">Property</span></span> | <span data-ttu-id="3b729-1115">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1115">Description</span></span> | <span data-ttu-id="3b729-1116">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1117">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1117">server</span></span> |<span data-ttu-id="3b729-1118">Amazon Redshift 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1118">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="3b729-1119">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1119">Yes</span></span> |
| <span data-ttu-id="3b729-1120">포트</span><span class="sxs-lookup"><span data-stu-id="3b729-1120">port</span></span> |<span data-ttu-id="3b729-1121">Amazon Redshift 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1121">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="3b729-1122">기본값이 없음: 5439</span><span class="sxs-lookup"><span data-stu-id="3b729-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="3b729-1123">database</span><span class="sxs-lookup"><span data-stu-id="3b729-1123">database</span></span> |<span data-ttu-id="3b729-1124">Amazon Redshift 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1124">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="3b729-1125">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1125">Yes</span></span> |
| <span data-ttu-id="3b729-1126">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1126">username</span></span> |<span data-ttu-id="3b729-1127">데이터베이스에 대한 액세스 권한이 있는 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1127">Name of user who has access to the database.</span></span> |<span data-ttu-id="3b729-1128">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1128">Yes</span></span> |
| <span data-ttu-id="3b729-1129">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1129">password</span></span> |<span data-ttu-id="3b729-1130">사용자 계정의 password입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1130">Password for the user account.</span></span> |<span data-ttu-id="3b729-1131">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1132">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1132">Example</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

<span data-ttu-id="3b729-1133">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#linked-service-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1134">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1134">Dataset</span></span>
<span data-ttu-id="3b729-1135">Amazon Redshift 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1135">To define an Amazon Redshift dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1136">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1136">Property</span></span> | <span data-ttu-id="3b729-1137">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1137">Description</span></span> | <span data-ttu-id="3b729-1138">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1139">tableName</span></span> |<span data-ttu-id="3b729-1140">연결된 서비스가 참조하는 Amazon Redshift 데이터베이스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1140">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="3b729-1141">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-1142">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1142">Example</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="3b729-1143">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#dataset-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1144">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="3b729-1145">Amazon Redshift에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1145">If you are copying data from Amazon Redshift, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1146">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1146">Property</span></span> | <span data-ttu-id="3b729-1147">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1147">Description</span></span> | <span data-ttu-id="3b729-1148">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1148">Allowed values</span></span> | <span data-ttu-id="3b729-1149">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1150">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1150">query</span></span> |<span data-ttu-id="3b729-1151">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1151">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1152">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1152">SQL query string.</span></span> <span data-ttu-id="3b729-1153">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-1154">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1155">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1155">Example</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="3b729-1156">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#copy-activity-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="3b729-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="3b729-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1158">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1158">Linked service</span></span>
<span data-ttu-id="3b729-1159">IBM DB2 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesDB2**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1159">To define an IBM DB2 linked service, set the **type** of the linked service to **OnPremisesDB2**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1160">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1160">Property</span></span> | <span data-ttu-id="3b729-1161">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1161">Description</span></span> | <span data-ttu-id="3b729-1162">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1163">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1163">server</span></span> |<span data-ttu-id="3b729-1164">DB2 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1164">Name of the DB2 server.</span></span> |<span data-ttu-id="3b729-1165">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1165">Yes</span></span> |
| <span data-ttu-id="3b729-1166">database</span><span class="sxs-lookup"><span data-stu-id="3b729-1166">database</span></span> |<span data-ttu-id="3b729-1167">DB2 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1167">Name of the DB2 database.</span></span> |<span data-ttu-id="3b729-1168">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1168">Yes</span></span> |
| <span data-ttu-id="3b729-1169">schema</span><span class="sxs-lookup"><span data-stu-id="3b729-1169">schema</span></span> |<span data-ttu-id="3b729-1170">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1170">Name of the schema in the database.</span></span> <span data-ttu-id="3b729-1171">schema 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1171">The schema name is case-sensitive.</span></span> |<span data-ttu-id="3b729-1172">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1172">No</span></span> |
| <span data-ttu-id="3b729-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1173">authenticationType</span></span> |<span data-ttu-id="3b729-1174">DB2 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1174">Type of authentication used to connect to the DB2 database.</span></span> <span data-ttu-id="3b729-1175">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3b729-1176">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1176">Yes</span></span> |
| <span data-ttu-id="3b729-1177">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1177">username</span></span> |<span data-ttu-id="3b729-1178">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3b729-1179">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1179">No</span></span> |
| <span data-ttu-id="3b729-1180">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1180">password</span></span> |<span data-ttu-id="3b729-1181">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1181">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-1182">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1182">No</span></span> |
| <span data-ttu-id="3b729-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1183">gatewayName</span></span> |<span data-ttu-id="3b729-1184">데이터 팩터리 서비스가 온-프레미스 DB2 데이터 베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1184">Name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="3b729-1185">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1186">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1186">Example</span></span>
```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="3b729-1187">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1188">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1188">Dataset</span></span>
<span data-ttu-id="3b729-1189">DB2 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1189">To define a DB2 dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="3b729-1190">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1190">Property</span></span> | <span data-ttu-id="3b729-1191">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1191">Description</span></span> | <span data-ttu-id="3b729-1192">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1193">tableName</span></span> |<span data-ttu-id="3b729-1194">연결된 서비스가 참조하는 DB2 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1194">Name of the table in the DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="3b729-1195">tableName은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1195">The tableName is case-sensitive.</span></span> |<span data-ttu-id="3b729-1196">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="3b729-1197">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1197">Example</span></span>
```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1198">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1199">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1200">IBM DB2에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1200">If you are copying data from IBM DB2, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1201">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1201">Property</span></span> | <span data-ttu-id="3b729-1202">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1202">Description</span></span> | <span data-ttu-id="3b729-1203">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1203">Allowed values</span></span> | <span data-ttu-id="3b729-1204">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1205">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1205">query</span></span> |<span data-ttu-id="3b729-1206">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1206">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1207">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1207">SQL query string.</span></span> <span data-ttu-id="3b729-1208">예: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="3b729-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="3b729-1209">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1210">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1210">Example</span></span>
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"Orders\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
<span data-ttu-id="3b729-1211">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="3b729-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="3b729-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1213">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1213">Linked service</span></span>
<span data-ttu-id="3b729-1214">MySQL 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesMySql**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1214">To define a MySQL linked service, set the **type** of the linked service to **OnPremisesMySql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1215">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1215">Property</span></span> | <span data-ttu-id="3b729-1216">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1216">Description</span></span> | <span data-ttu-id="3b729-1217">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1218">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1218">server</span></span> |<span data-ttu-id="3b729-1219">MySQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1219">Name of the MySQL server.</span></span> |<span data-ttu-id="3b729-1220">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1220">Yes</span></span> |
| <span data-ttu-id="3b729-1221">database</span><span class="sxs-lookup"><span data-stu-id="3b729-1221">database</span></span> |<span data-ttu-id="3b729-1222">MySQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1222">Name of the MySQL database.</span></span> |<span data-ttu-id="3b729-1223">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1223">Yes</span></span> |
| <span data-ttu-id="3b729-1224">schema</span><span class="sxs-lookup"><span data-stu-id="3b729-1224">schema</span></span> |<span data-ttu-id="3b729-1225">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1225">Name of the schema in the database.</span></span> |<span data-ttu-id="3b729-1226">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1226">No</span></span> |
| <span data-ttu-id="3b729-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1227">authenticationType</span></span> |<span data-ttu-id="3b729-1228">MySQL 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1228">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="3b729-1229">가능한 값은 `Basic`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="3b729-1230">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1230">Yes</span></span> |
| <span data-ttu-id="3b729-1231">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1231">username</span></span> |<span data-ttu-id="3b729-1232">MySQL 데이터베이스에 연결할 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1232">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="3b729-1233">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1233">Yes</span></span> |
| <span data-ttu-id="3b729-1234">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1234">password</span></span> |<span data-ttu-id="3b729-1235">지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1235">Specify password for the user account you specified.</span></span> |<span data-ttu-id="3b729-1236">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1236">Yes</span></span> |
| <span data-ttu-id="3b729-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1237">gatewayName</span></span> |<span data-ttu-id="3b729-1238">데이터 팩터리 서비스가 온-프레미스 MySQL 데이터 베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1238">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="3b729-1239">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1240">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1240">Example</span></span>

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

<span data-ttu-id="3b729-1241">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1242">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1242">Dataset</span></span>
<span data-ttu-id="3b729-1243">MySQL 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1243">To define a MySQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1244">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1244">Property</span></span> | <span data-ttu-id="3b729-1245">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1245">Description</span></span> | <span data-ttu-id="3b729-1246">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1247">tableName</span></span> |<span data-ttu-id="3b729-1248">연결된 서비스가 참조하는 MySQL 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1248">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b729-1249">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1250">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1250">Example</span></span>

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="3b729-1251">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1252">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1253">MySQL 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1253">If you are copying data from a MySQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1254">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1254">Property</span></span> | <span data-ttu-id="3b729-1255">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1255">Description</span></span> | <span data-ttu-id="3b729-1256">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1256">Allowed values</span></span> | <span data-ttu-id="3b729-1257">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1258">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1258">query</span></span> |<span data-ttu-id="3b729-1259">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1259">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1260">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1260">SQL query string.</span></span> <span data-ttu-id="3b729-1261">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-1262">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-1263">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1263">Example</span></span>
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1264">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="3b729-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="3b729-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-1266">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1266">Linked service</span></span>
<span data-ttu-id="3b729-1267">Oracle 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesOracle**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1267">To define an Oracle linked service, set the **type** of the linked service to **OnPremisesOracle**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1268">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1268">Property</span></span> | <span data-ttu-id="3b729-1269">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1269">Description</span></span> | <span data-ttu-id="3b729-1270">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="3b729-1271">driverType</span></span> | <span data-ttu-id="3b729-1272">Oracle Database로 데이터를 복사하거나 Oracle Database에서 데이터를 복사하는 데 사용할 드라이버를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1272">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="3b729-1273">허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="3b729-1274">드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="3b729-1275">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1275">No</span></span> |
| <span data-ttu-id="3b729-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-1276">connectionString</span></span> | <span data-ttu-id="3b729-1277">connectionString 속성에 대한 Oracle 데이터베이스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1277">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="3b729-1278">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1278">Yes</span></span> |
| <span data-ttu-id="3b729-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1279">gatewayName</span></span> | <span data-ttu-id="3b729-1280">온-프레미스 Oracle 서버에 연결하는 데 사용할 게이트웨이 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1280">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="3b729-1281">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1282">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1282">Example</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3b729-1283">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1284">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1284">Dataset</span></span>
<span data-ttu-id="3b729-1285">Oracle 데이터 집합을 정의하려면 데이터 집합의 **type**을 **OracleTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1285">To define an Oracle dataset, set the **type** of the dataset to **OracleTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1286">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1286">Property</span></span> | <span data-ttu-id="3b729-1287">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1287">Description</span></span> | <span data-ttu-id="3b729-1288">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1289">tableName</span></span> |<span data-ttu-id="3b729-1290">연결된 서비스가 참조하는 Oracle 데이터베이스에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1290">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="3b729-1291">아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1292">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1292">Example</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="3b729-1293">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="3b729-1294">복사 활동의 Oracle 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1295">Oracle 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **OracleSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1295">If you are copying data from an Oracle database, set the **source type** of the copy activity to **OracleSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1296">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1296">Property</span></span> | <span data-ttu-id="3b729-1297">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1297">Description</span></span> | <span data-ttu-id="3b729-1298">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1298">Allowed values</span></span> | <span data-ttu-id="3b729-1299">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3b729-1300">oracleReaderQuery</span></span> |<span data-ttu-id="3b729-1301">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1301">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1302">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1302">SQL query string.</span></span> <span data-ttu-id="3b729-1303">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="3b729-1304">지정하지 않는 경우 실행되는 SQL 문: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1304">If not specified, the SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="3b729-1305">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1306">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1306">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1307">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="3b729-1308">복사 활동의 Oracle 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-1309">Oracle 데이터베이스에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **OracleSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1309">If you are copying data to am Oracle database, set the **sink type** of the copy activity to **OracleSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-1310">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1310">Property</span></span> | <span data-ttu-id="3b729-1311">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1311">Description</span></span> | <span data-ttu-id="3b729-1312">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1312">Allowed values</span></span> | <span data-ttu-id="3b729-1313">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-1314">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-1315">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1315">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3b729-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-1316">timespan</span></span><br/><br/> <span data-ttu-id="3b729-1317">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="3b729-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="3b729-1318">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1318">No</span></span> |
| <span data-ttu-id="3b729-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-1319">writeBatchSize</span></span> |<span data-ttu-id="3b729-1320">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="3b729-1320">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="3b729-1321">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="3b729-1321">Integer (number of rows)</span></span> |<span data-ttu-id="3b729-1322">아니요(기본값: 100)</span><span class="sxs-lookup"><span data-stu-id="3b729-1322">No (default: 100)</span></span> |
| <span data-ttu-id="3b729-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3b729-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3b729-1324">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1324">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="3b729-1325">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1325">A query statement.</span></span> |<span data-ttu-id="3b729-1326">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1326">No</span></span> |
| <span data-ttu-id="3b729-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3b729-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="3b729-1328">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1328">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="3b729-1329">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="3b729-1330">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1331">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1331">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="3b729-1332">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="3b729-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="3b729-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1334">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1334">Linked service</span></span>
<span data-ttu-id="3b729-1335">PostgreSQL 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesPostgreSql**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1335">To define a PostgreSQL linked service, set the **type** of the linked service to **OnPremisesPostgreSql**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1336">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1336">Property</span></span> | <span data-ttu-id="3b729-1337">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1337">Description</span></span> | <span data-ttu-id="3b729-1338">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1339">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1339">server</span></span> |<span data-ttu-id="3b729-1340">PostgreSQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1340">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="3b729-1341">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1341">Yes</span></span> |
| <span data-ttu-id="3b729-1342">database</span><span class="sxs-lookup"><span data-stu-id="3b729-1342">database</span></span> |<span data-ttu-id="3b729-1343">PostgreSQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1343">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="3b729-1344">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1344">Yes</span></span> |
| <span data-ttu-id="3b729-1345">schema</span><span class="sxs-lookup"><span data-stu-id="3b729-1345">schema</span></span> |<span data-ttu-id="3b729-1346">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1346">Name of the schema in the database.</span></span> <span data-ttu-id="3b729-1347">schema 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1347">The schema name is case-sensitive.</span></span> |<span data-ttu-id="3b729-1348">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1348">No</span></span> |
| <span data-ttu-id="3b729-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1349">authenticationType</span></span> |<span data-ttu-id="3b729-1350">PostgreSQL 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1350">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="3b729-1351">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3b729-1352">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1352">Yes</span></span> |
| <span data-ttu-id="3b729-1353">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1353">username</span></span> |<span data-ttu-id="3b729-1354">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3b729-1355">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1355">No</span></span> |
| <span data-ttu-id="3b729-1356">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1356">password</span></span> |<span data-ttu-id="3b729-1357">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1357">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-1358">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1358">No</span></span> |
| <span data-ttu-id="3b729-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1359">gatewayName</span></span> |<span data-ttu-id="3b729-1360">데이터 팩터리 서비스가 온-프레미스 PostgreSQL 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1360">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="3b729-1361">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1362">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1362">Example</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="3b729-1363">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1364">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1364">Dataset</span></span>
<span data-ttu-id="3b729-1365">PostgreSQL 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1365">To define a PostgreSQL dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1366">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1366">Property</span></span> | <span data-ttu-id="3b729-1367">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1367">Description</span></span> | <span data-ttu-id="3b729-1368">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1369">tableName</span></span> |<span data-ttu-id="3b729-1370">연결된 서비스가 참조하는 PostgreSQL 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1370">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="3b729-1371">tableName은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1371">The tableName is case-sensitive.</span></span> |<span data-ttu-id="3b729-1372">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1373">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1373">Example</span></span>
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="3b729-1374">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1375">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1376">PostgreSQL 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1376">If you are copying data from a PostgreSQL database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1377">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1377">Property</span></span> | <span data-ttu-id="3b729-1378">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1378">Description</span></span> | <span data-ttu-id="3b729-1379">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1379">Allowed values</span></span> | <span data-ttu-id="3b729-1380">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1381">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1381">query</span></span> |<span data-ttu-id="3b729-1382">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1382">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1383">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1383">SQL query string.</span></span> <span data-ttu-id="3b729-1384">예: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="3b729-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="3b729-1385">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1386">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1386">Example</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1387">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="3b729-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="3b729-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-1389">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1389">Linked service</span></span>
<span data-ttu-id="3b729-1390">SAP BW(Business Warehouse) 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **SapBw**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1390">To define a SAP Business Warehouse (BW) linked service, set the **type** of the linked service to **SapBw**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="3b729-1391">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1391">Property</span></span> | <span data-ttu-id="3b729-1392">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1392">Description</span></span> | <span data-ttu-id="3b729-1393">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1393">Allowed values</span></span> | <span data-ttu-id="3b729-1394">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3b729-1395">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1395">server</span></span> | <span data-ttu-id="3b729-1396">SAP BW 인스턴스가 상주하는 서버의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-1396">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="3b729-1397">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1397">string</span></span> | <span data-ttu-id="3b729-1398">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1398">Yes</span></span>
<span data-ttu-id="3b729-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="3b729-1399">systemNumber</span></span> | <span data-ttu-id="3b729-1400">SAP BW 시스템의 시스템 번호.</span><span class="sxs-lookup"><span data-stu-id="3b729-1400">System number of the SAP BW system.</span></span> | <span data-ttu-id="3b729-1401">문자열로 표현되는 두 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="3b729-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="3b729-1402">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1402">Yes</span></span>
<span data-ttu-id="3b729-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="3b729-1403">clientId</span></span> | <span data-ttu-id="3b729-1404">SAP W 시스템에 있는 클라이언트의 클라이언트 ID.</span><span class="sxs-lookup"><span data-stu-id="3b729-1404">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="3b729-1405">문자열로 표현되는 세 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="3b729-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="3b729-1406">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1406">Yes</span></span>
<span data-ttu-id="3b729-1407">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1407">username</span></span> | <span data-ttu-id="3b729-1408">SAP 서버에 대한 액세스 권한이 있는 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1408">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="3b729-1409">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1409">string</span></span> | <span data-ttu-id="3b729-1410">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1410">Yes</span></span>
<span data-ttu-id="3b729-1411">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1411">password</span></span> | <span data-ttu-id="3b729-1412">사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1412">Password for the user.</span></span> | <span data-ttu-id="3b729-1413">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1413">string</span></span> | <span data-ttu-id="3b729-1414">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1414">Yes</span></span>
<span data-ttu-id="3b729-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1415">gatewayName</span></span> | <span data-ttu-id="3b729-1416">Data Factory 서비스가 온-프레미스 SAP BW 인스턴스에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-1416">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="3b729-1417">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1417">string</span></span> | <span data-ttu-id="3b729-1418">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1418">Yes</span></span>
<span data-ttu-id="3b729-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-1419">encryptedCredential</span></span> | <span data-ttu-id="3b729-1420">암호화된 자격 증명 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1420">The encrypted credential string.</span></span> | <span data-ttu-id="3b729-1421">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1421">string</span></span> | <span data-ttu-id="3b729-1422">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-1423">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1423">Example</span></span>

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3b729-1424">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1425">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1425">Dataset</span></span>
<span data-ttu-id="3b729-1426">SAP BW 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1426">To define a SAP BW dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="3b729-1427">**RelationalTable** 형식의 SAP BW 데이터 집합에 대해 지원되는 type별 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1427">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="3b729-1428">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1428">Example</span></span>

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="3b729-1429">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1430">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1431">SAP Business Warehouse에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1431">If you are copying data from SAP Business Warehouse, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1432">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1432">Property</span></span> | <span data-ttu-id="3b729-1433">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1433">Description</span></span> | <span data-ttu-id="3b729-1434">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1434">Allowed values</span></span> | <span data-ttu-id="3b729-1435">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1436">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1436">query</span></span> | <span data-ttu-id="3b729-1437">SAP BW 인스턴스에서 데이터를 읽을 MDX 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1437">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="3b729-1438">MDX 쿼리.</span><span class="sxs-lookup"><span data-stu-id="3b729-1438">MDX query.</span></span> | <span data-ttu-id="3b729-1439">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1440">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1440">Example</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1441">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="3b729-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="3b729-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1443">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1443">Linked service</span></span>
<span data-ttu-id="3b729-1444">SAP HANA 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **SapHana**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1444">To define a SAP HANA linked service, set the **type** of the linked service to **SapHana**, and specify following properties in the **typeProperties** section:</span></span>  

<span data-ttu-id="3b729-1445">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1445">Property</span></span> | <span data-ttu-id="3b729-1446">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1446">Description</span></span> | <span data-ttu-id="3b729-1447">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1447">Allowed values</span></span> | <span data-ttu-id="3b729-1448">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="3b729-1449">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1449">server</span></span> | <span data-ttu-id="3b729-1450">SAP HANA 인스턴스가 상주하는 서버의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-1450">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="3b729-1451">서버에서 사용자 지정된 포트를 사용하는 경우 `server:port`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="3b729-1452">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1452">string</span></span> | <span data-ttu-id="3b729-1453">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1453">Yes</span></span>
<span data-ttu-id="3b729-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1454">authenticationType</span></span> | <span data-ttu-id="3b729-1455">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1455">Type of authentication.</span></span> | <span data-ttu-id="3b729-1456">string.</span><span class="sxs-lookup"><span data-stu-id="3b729-1456">string.</span></span> <span data-ttu-id="3b729-1457">"Basic" 또는 "Windows"</span><span class="sxs-lookup"><span data-stu-id="3b729-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="3b729-1458">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1458">Yes</span></span> 
<span data-ttu-id="3b729-1459">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1459">username</span></span> | <span data-ttu-id="3b729-1460">SAP 서버에 대한 액세스 권한이 있는 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1460">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="3b729-1461">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1461">string</span></span> | <span data-ttu-id="3b729-1462">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1462">Yes</span></span>
<span data-ttu-id="3b729-1463">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1463">password</span></span> | <span data-ttu-id="3b729-1464">사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1464">Password for the user.</span></span> | <span data-ttu-id="3b729-1465">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1465">string</span></span> | <span data-ttu-id="3b729-1466">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1466">Yes</span></span>
<span data-ttu-id="3b729-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1467">gatewayName</span></span> | <span data-ttu-id="3b729-1468">Data Factory 서비스가 온-프레미스 SAP HANA 인스턴스에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-1468">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="3b729-1469">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1469">string</span></span> | <span data-ttu-id="3b729-1470">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1470">Yes</span></span>
<span data-ttu-id="3b729-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-1471">encryptedCredential</span></span> | <span data-ttu-id="3b729-1472">암호화된 자격 증명 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1472">The encrypted credential string.</span></span> | <span data-ttu-id="3b729-1473">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1473">string</span></span> | <span data-ttu-id="3b729-1474">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-1475">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1475">Example</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
<span data-ttu-id="3b729-1476">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="3b729-1477">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1477">Dataset</span></span>
<span data-ttu-id="3b729-1478">SAP HANA 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1478">To define a SAP HANA dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="3b729-1479">**RelationalTable** 형식의 SAP HANA 데이터 집합에 대해 지원되는 type별 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1479">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="3b729-1480">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1480">Example</span></span>

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="3b729-1481">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1482">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1483">SAP HANA 데이터 저장소에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1483">If you are copying data from a SAP HANA data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1484">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1484">Property</span></span> | <span data-ttu-id="3b729-1485">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1485">Description</span></span> | <span data-ttu-id="3b729-1486">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1486">Allowed values</span></span> | <span data-ttu-id="3b729-1487">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1488">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1488">query</span></span> | <span data-ttu-id="3b729-1489">SAP HANA 인스턴스에서 데이터를 읽을 SQL 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1489">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="3b729-1490">SQL 쿼리.</span><span class="sxs-lookup"><span data-stu-id="3b729-1490">SQL query.</span></span> | <span data-ttu-id="3b729-1491">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-1492">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1492">Example</span></span>


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1493">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="3b729-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3b729-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1495">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1495">Linked service</span></span>
<span data-ttu-id="3b729-1496">**OnPremisesSqlServer** 형식의 연결된 서비스를 만들어 온-프레미스 SQL Server 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1496">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="3b729-1497">다음 테이블은 온-프레미스 SQL Server 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1497">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="3b729-1498">다음 표에서는 SQL Server 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1498">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="3b729-1499">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1499">Property</span></span> | <span data-ttu-id="3b729-1500">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1500">Description</span></span> | <span data-ttu-id="3b729-1501">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1502">type</span><span class="sxs-lookup"><span data-stu-id="3b729-1502">type</span></span> |<span data-ttu-id="3b729-1503">type 속성은 **OnPremisesSqlServer**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1503">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="3b729-1504">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1504">Yes</span></span> |
| <span data-ttu-id="3b729-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-1505">connectionString</span></span> |<span data-ttu-id="3b729-1506">SQL 인증 또는 Windows 인증을 사용하여 온-프레미스 SQL Server 데이터베이스에 연결하는 데 필요한 connectionString 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1506">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="3b729-1507">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1507">Yes</span></span> |
| <span data-ttu-id="3b729-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1508">gatewayName</span></span> |<span data-ttu-id="3b729-1509">데이터 팩터리 서비스가 온-프레미스 SQL Server 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1509">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="3b729-1510">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1510">Yes</span></span> |
| <span data-ttu-id="3b729-1511">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1511">username</span></span> |<span data-ttu-id="3b729-1512">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="3b729-1513">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="3b729-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="3b729-1514">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1514">No</span></span> |
| <span data-ttu-id="3b729-1515">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1515">password</span></span> |<span data-ttu-id="3b729-1516">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1516">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-1517">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1517">No</span></span> |

<span data-ttu-id="3b729-1518">**New-AzureRmDataFactoryEncryptValue** cmdlet를 사용하여 자격 증명을 암호화하고 다음 예제와 같이 연결 문자열에 해당 자격 증명을 사용할 수 있습니다(**EncryptedCredential** 속성).</span><span class="sxs-lookup"><span data-stu-id="3b729-1518">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="3b729-1519">예제: SQL 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="3b729-1519">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="3b729-1520">예제: Windows 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="3b729-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="3b729-1521">사용자 이름 및 암호가 지정된 경우 게이트웨이는 이러한 정보를 사용해 지정된 사용자 계정을 가장하여 온-프레미스 SQL Server Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1521">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="3b729-1522">그렇지 않은 경우 게이트웨이는 게이트웨이의 보안 컨텍스트(시작 계정)를 사용하여 SQL Server에 직접 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1522">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3b729-1523">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1524">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1524">Dataset</span></span>
<span data-ttu-id="3b729-1525">SQL Server 데이터 집합을 정의하려면 데이터 집합의 **type**을 **SqlServerTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1525">To define a SQL Server dataset, set the **type** of the dataset to **SqlServerTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1526">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1526">Property</span></span> | <span data-ttu-id="3b729-1527">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1527">Description</span></span> | <span data-ttu-id="3b729-1528">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1529">tableName</span></span> |<span data-ttu-id="3b729-1530">연결된 서비스가 참조하는 SQL Server 데이터베이스 인스턴스에서 테이블 또는 보기의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1530">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b729-1531">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1532">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1532">Example</span></span>
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1533">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="3b729-1534">복사 활동의 SQL 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1535">SQL Server 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **SqlSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1535">If you are copying data from a SQL Server database, set the **source type** of the copy activity to **SqlSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1536">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1536">Property</span></span> | <span data-ttu-id="3b729-1537">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1537">Description</span></span> | <span data-ttu-id="3b729-1538">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1538">Allowed values</span></span> | <span data-ttu-id="3b729-1539">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="3b729-1540">sqlReaderQuery</span></span> |<span data-ttu-id="3b729-1541">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1541">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1542">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1542">SQL query string.</span></span> <span data-ttu-id="3b729-1543">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="3b729-1544">입력 데이터 집합에 의해 참조되는 데이터베이스의 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1544">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="3b729-1545">지정하지 않는 경우 실행되는 SQL 문: select from MyTable.</span><span class="sxs-lookup"><span data-stu-id="3b729-1545">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="3b729-1546">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1546">No</span></span> |
| <span data-ttu-id="3b729-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="3b729-1548">원본 테이블에서 데이터를 읽는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1548">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="3b729-1549">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1549">Name of the stored procedure.</span></span> |<span data-ttu-id="3b729-1550">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1550">No</span></span> |
| <span data-ttu-id="3b729-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-1551">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-1552">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1552">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3b729-1553">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1553">Name/value pairs.</span></span> <span data-ttu-id="3b729-1554">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1554">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3b729-1555">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1555">No</span></span> |

<span data-ttu-id="3b729-1556">**sqlReaderQuery** 가 SqlSource에 지정되면 복사 작업은 데이터를 가져오는 SQL Server 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1556">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="3b729-1557">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="3b729-1557">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="3b729-1558">sqlReaderQuery 또는 sqlReaderStoredProcedureName을 지정하지 않으면 structure 섹션에 정의된 열을 사용하여 SQL Server Database에 대해 실행할 선택 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="3b729-1559">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1559">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="3b729-1560">**sqlReaderStoredProcedureName**을 사용하는 경우에도 데이터 집합 JSON에서 **tableName** 속성 값을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1560">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="3b729-1561">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="3b729-1562">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1562">Example</span></span>
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1563">위의 예에서는 SqlSource에 대해 **sqlReaderQuery** 가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1563">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="3b729-1564">복사 작업은 데이터를 가져오는 SQL Server 데이터베이스 원본에 대해 이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1564">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="3b729-1565">또는 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters**를 지정하여 저장 프로시저를 지정할 수 있습니다(저장 프로시저가 매개 변수를 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="3b729-1565">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="3b729-1566">sqlReaderQuery는 입력 데이터 집합에서 참조하는 데이터베이스 내의 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1566">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="3b729-1567">즉, 데이터 집합의 tableName typeProperty로 설정된 테이블만 참조하도록 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1567">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="3b729-1568">sqlReaderQuery 또는 sqlReaderStoredProcedureName을 지정하지 않으면 structure 섹션에 정의된 열을 사용하여 SQL Server Database에 대해 실행할 선택 쿼리를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="3b729-1569">데이터 집합 정의에 구조가 없는 경우 모든 열은 테이블에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1569">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="3b729-1570">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="3b729-1571">복사 활동의 SQL 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-1572">SQL Server 데이터베이스에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **SqlSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1572">If you are copying data to a SQL Server database, set the **sink type** of the copy activity to **SqlSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-1573">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1573">Property</span></span> | <span data-ttu-id="3b729-1574">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1574">Description</span></span> | <span data-ttu-id="3b729-1575">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1575">Allowed values</span></span> | <span data-ttu-id="3b729-1576">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-1577">writeBatchTimeout</span></span> |<span data-ttu-id="3b729-1578">시간이 초과되기 전에 완료하려는 배치 삽입 작업을 위한 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1578">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="3b729-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="3b729-1579">timespan</span></span><br/><br/> <span data-ttu-id="3b729-1580">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="3b729-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="3b729-1581">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1581">No</span></span> |
| <span data-ttu-id="3b729-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="3b729-1582">writeBatchSize</span></span> |<span data-ttu-id="3b729-1583">버퍼 크기가 writeBatchSize에 도달하는 경우 SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="3b729-1583">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="3b729-1584">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="3b729-1584">Integer (number of rows)</span></span> |<span data-ttu-id="3b729-1585">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="3b729-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="3b729-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="3b729-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="3b729-1587">특정 조각의 데이터를 정리하기 위해 복사 활동에 대해 실행할 쿼리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1587">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="3b729-1588">자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="3b729-1589">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1589">A query statement.</span></span> |<span data-ttu-id="3b729-1590">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1590">No</span></span> |
| <span data-ttu-id="3b729-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="3b729-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="3b729-1592">자동 생성된 조각 식별자를 입력할 복사 활동의 열 이름을 지정합니다. 이 식별자는 복사 활동을 다시 실행할 때 특정 조각의 데이터를 정리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1592">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="3b729-1593">자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="3b729-1594">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="3b729-1595">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1595">No</span></span> |
| <span data-ttu-id="3b729-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="3b729-1597">대상 테이블에 대한 데이터 Upsert(업데이트/삽입)를 수행하는 저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1597">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="3b729-1598">저장 프로시저의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1598">Name of the stored procedure.</span></span> |<span data-ttu-id="3b729-1599">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1599">No</span></span> |
| <span data-ttu-id="3b729-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-1600">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-1601">저장 프로시저에 대한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1601">Parameters for the stored procedure.</span></span> |<span data-ttu-id="3b729-1602">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1602">Name/value pairs.</span></span> <span data-ttu-id="3b729-1603">매개 변수의 이름 및 대소문자와, 저장 프로시저 매개변수의 이름 및 대소문자와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1603">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="3b729-1604">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1604">No</span></span> |
| <span data-ttu-id="3b729-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="3b729-1605">sqlWriterTableType</span></span> |<span data-ttu-id="3b729-1606">저장 프로시저에 사용할 테이블 형식 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1606">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="3b729-1607">복사 작업을 사용하면 이 테이블 형식으로 임시 테이블에서 사용할 수 있는 데이터를 이동시킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1607">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="3b729-1608">그러면 저장 프로시저 코드가 복사되는 데이터를 기존 데이터와 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1608">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="3b729-1609">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-1609">A table type name.</span></span> |<span data-ttu-id="3b729-1610">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1611">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1611">Example</span></span>
<span data-ttu-id="3b729-1612">파이프라인은 이러한 입력 및 출력 데이터 집합을 사용하도록 구성되며 매시간 실행되도록 예약되는 복사 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1612">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="3b729-1613">파이프라인 JSON 정의에서 **원본** 형식은 **BlobSource**로 설정되고 **싱크** 형식은 **SqlSink**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1613">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1614">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="3b729-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="3b729-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1616">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1616">Linked service</span></span>
<span data-ttu-id="3b729-1617">Sybase 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesSybase**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1617">To define a Sybase linked service, set the **type** of the linked service to **OnPremisesSybase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1618">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1618">Property</span></span> | <span data-ttu-id="3b729-1619">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1619">Description</span></span> | <span data-ttu-id="3b729-1620">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1621">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1621">server</span></span> |<span data-ttu-id="3b729-1622">Sybase 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1622">Name of the Sybase server.</span></span> |<span data-ttu-id="3b729-1623">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1623">Yes</span></span> |
| <span data-ttu-id="3b729-1624">database</span><span class="sxs-lookup"><span data-stu-id="3b729-1624">database</span></span> |<span data-ttu-id="3b729-1625">Sybase 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1625">Name of the Sybase database.</span></span> |<span data-ttu-id="3b729-1626">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1626">Yes</span></span> |
| <span data-ttu-id="3b729-1627">schema</span><span class="sxs-lookup"><span data-stu-id="3b729-1627">schema</span></span> |<span data-ttu-id="3b729-1628">데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1628">Name of the schema in the database.</span></span> |<span data-ttu-id="3b729-1629">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1629">No</span></span> |
| <span data-ttu-id="3b729-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1630">authenticationType</span></span> |<span data-ttu-id="3b729-1631">Sybase 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1631">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="3b729-1632">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3b729-1633">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1633">Yes</span></span> |
| <span data-ttu-id="3b729-1634">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1634">username</span></span> |<span data-ttu-id="3b729-1635">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3b729-1636">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1636">No</span></span> |
| <span data-ttu-id="3b729-1637">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1637">password</span></span> |<span data-ttu-id="3b729-1638">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1638">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-1639">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1639">No</span></span> |
| <span data-ttu-id="3b729-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1640">gatewayName</span></span> |<span data-ttu-id="3b729-1641">데이터 팩터리 서비스가 온-프레미스 Sybase 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1641">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="3b729-1642">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1643">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1643">Example</span></span>
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="3b729-1644">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1645">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1645">Dataset</span></span>
<span data-ttu-id="3b729-1646">Sybase 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1646">To define a Sybase dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1647">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1647">Property</span></span> | <span data-ttu-id="3b729-1648">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1648">Description</span></span> | <span data-ttu-id="3b729-1649">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1650">tableName</span></span> |<span data-ttu-id="3b729-1651">연결된 서비스가 참조하는 Sybase 데이터베이스 인스턴스에서 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1651">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="3b729-1652">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1653">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1653">Example</span></span>

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1654">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1655">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1656">Sybase 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1656">If you are copying data from a Sybase database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1657">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1657">Property</span></span> | <span data-ttu-id="3b729-1658">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1658">Description</span></span> | <span data-ttu-id="3b729-1659">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1659">Allowed values</span></span> | <span data-ttu-id="3b729-1660">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1661">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1661">query</span></span> |<span data-ttu-id="3b729-1662">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1662">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1663">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1663">SQL query string.</span></span> <span data-ttu-id="3b729-1664">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-1665">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1666">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1666">Example</span></span>

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1667">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="3b729-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="3b729-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1669">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1669">Linked service</span></span>
<span data-ttu-id="3b729-1670">Teradata 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesTeradata**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1670">To define a Teradata linked service, set the **type** of the linked service to **OnPremisesTeradata**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1671">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1671">Property</span></span> | <span data-ttu-id="3b729-1672">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1672">Description</span></span> | <span data-ttu-id="3b729-1673">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1674">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1674">server</span></span> |<span data-ttu-id="3b729-1675">Teradata 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1675">Name of the Teradata server.</span></span> |<span data-ttu-id="3b729-1676">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1676">Yes</span></span> |
| <span data-ttu-id="3b729-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1677">authenticationType</span></span> |<span data-ttu-id="3b729-1678">Teradata 데이터베이스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1678">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="3b729-1679">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3b729-1680">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1680">Yes</span></span> |
| <span data-ttu-id="3b729-1681">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1681">username</span></span> |<span data-ttu-id="3b729-1682">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="3b729-1683">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1683">No</span></span> |
| <span data-ttu-id="3b729-1684">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1684">password</span></span> |<span data-ttu-id="3b729-1685">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1685">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-1686">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1686">No</span></span> |
| <span data-ttu-id="3b729-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1687">gatewayName</span></span> |<span data-ttu-id="3b729-1688">데이터 팩터리 서비스가 온-프레미스 Teradata 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1688">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="3b729-1689">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1690">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1690">Example</span></span>
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="3b729-1691">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1692">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1692">Dataset</span></span>
<span data-ttu-id="3b729-1693">Teradata Blob 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1693">To define a Teradata Blob dataset, set the **type** of the dataset to **RelationalTable**.</span></span> <span data-ttu-id="3b729-1694">현재 Teradata 데이터 집합에 대해 지원되는 형식 속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1694">Currently, there are no type properties supported for the Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="3b729-1695">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1695">Example</span></span>
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1696">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-1697">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1698">Teradata 데이터베이스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1698">If you are copying data from a Teradata database, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1699">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1699">Property</span></span> | <span data-ttu-id="3b729-1700">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1700">Description</span></span> | <span data-ttu-id="3b729-1701">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1701">Allowed values</span></span> | <span data-ttu-id="3b729-1702">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1703">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1703">query</span></span> |<span data-ttu-id="3b729-1704">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1704">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1705">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-1705">SQL query string.</span></span> <span data-ttu-id="3b729-1706">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-1707">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1708">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1708">Example</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="3b729-1709">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="3b729-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="3b729-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-1711">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1711">Linked service</span></span>
<span data-ttu-id="3b729-1712">Cassandra 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesCassandra**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1712">To define a Cassandra linked service, set the **type** of the linked service to **OnPremisesCassandra**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1713">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1713">Property</span></span> | <span data-ttu-id="3b729-1714">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1714">Description</span></span> | <span data-ttu-id="3b729-1715">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1716">host</span><span class="sxs-lookup"><span data-stu-id="3b729-1716">host</span></span> |<span data-ttu-id="3b729-1717">Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="3b729-1718">모든 서버에 동시에 연결하려면 쉼표로 구분된 IP 주소 또는 호스트 이름 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1718">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="3b729-1719">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1719">Yes</span></span> |
| <span data-ttu-id="3b729-1720">포트</span><span class="sxs-lookup"><span data-stu-id="3b729-1720">port</span></span> |<span data-ttu-id="3b729-1721">Cassandra 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1721">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="3b729-1722">아니요. 기본값: 9042</span><span class="sxs-lookup"><span data-stu-id="3b729-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="3b729-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1723">authenticationType</span></span> |<span data-ttu-id="3b729-1724">Basic 또는 Anonymous</span><span class="sxs-lookup"><span data-stu-id="3b729-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="3b729-1725">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1725">Yes</span></span> |
| <span data-ttu-id="3b729-1726">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1726">username</span></span> |<span data-ttu-id="3b729-1727">사용자 계정의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1727">Specify user name for the user account.</span></span> |<span data-ttu-id="3b729-1728">예. authenticationType은 Basic으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1728">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="3b729-1729">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1729">password</span></span> |<span data-ttu-id="3b729-1730">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1730">Specify password for the user account.</span></span> |<span data-ttu-id="3b729-1731">예. authenticationType은 Basic으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1731">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="3b729-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1732">gatewayName</span></span> |<span data-ttu-id="3b729-1733">온-프레미스 Cassandra 데이터베이스에 연결하는 데 사용되는 게이트웨이 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1733">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="3b729-1734">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1734">Yes</span></span> |
| <span data-ttu-id="3b729-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-1735">encryptedCredential</span></span> |<span data-ttu-id="3b729-1736">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1736">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="3b729-1737">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1738">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1738">Example</span></span>

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="3b729-1739">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-1740">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1740">Dataset</span></span>
<span data-ttu-id="3b729-1741">Cassandra 데이터 집합을 정의하려면 데이터 집합의 **type**을 **CassandraTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1741">To define a Cassandra dataset, set the **type** of the dataset to **CassandraTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1742">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1742">Property</span></span> | <span data-ttu-id="3b729-1743">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1743">Description</span></span> | <span data-ttu-id="3b729-1744">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="3b729-1745">keyspace</span></span> |<span data-ttu-id="3b729-1746">Cassandra 데이터베이스의 키스페이스 또는 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1746">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="3b729-1747">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="3b729-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-1748">tableName</span></span> |<span data-ttu-id="3b729-1749">Cassandra 데이터베이스에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1749">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="3b729-1750">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1751">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1751">Example</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1752">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="3b729-1753">복사 활동의 Cassandra 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1754">Cassandra에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **CassandraSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1754">If you are copying data from Cassandra, set the **source type** of the copy activity to **CassandraSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1755">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1755">Property</span></span> | <span data-ttu-id="3b729-1756">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1756">Description</span></span> | <span data-ttu-id="3b729-1757">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1757">Allowed values</span></span> | <span data-ttu-id="3b729-1758">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1759">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1759">query</span></span> |<span data-ttu-id="3b729-1760">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1760">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1761">SQL-92 쿼리 또는 CQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="3b729-1762">[CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="3b729-1763">SQL 쿼리를 사용할 경우 **keyspace name.table name** 을 지정하여 쿼리하려는 테이블을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1763">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="3b729-1764">아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="3b729-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="3b729-1765">consistencyLevel</span></span> |<span data-ttu-id="3b729-1766">일관성 수준은 클라이언트 응용 프로그램에 데이터를 반환하기 전에 읽기 요청에 응답해야 하는 복제본 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1766">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="3b729-1767">Cassandra는 데이터의 지정된 수의 복제본이 읽기 요청을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1767">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="3b729-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="3b729-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="3b729-1769">자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="3b729-1770">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1770">No.</span></span> <span data-ttu-id="3b729-1771">기본값은 ONE입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1772">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-1773">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="3b729-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="3b729-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-1775">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1775">Linked service</span></span>
<span data-ttu-id="3b729-1776">MongoDB 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesMongoDB**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1776">To define a MongoDB linked service, set the **type** of the linked service to **OnPremisesMongoDB**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1777">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1777">Property</span></span> | <span data-ttu-id="3b729-1778">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1778">Description</span></span> | <span data-ttu-id="3b729-1779">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1780">server</span><span class="sxs-lookup"><span data-stu-id="3b729-1780">server</span></span> |<span data-ttu-id="3b729-1781">MongoDB 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1781">IP address or host name of the MongoDB server.</span></span> |<span data-ttu-id="3b729-1782">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1782">Yes</span></span> |
| <span data-ttu-id="3b729-1783">포트</span><span class="sxs-lookup"><span data-stu-id="3b729-1783">port</span></span> |<span data-ttu-id="3b729-1784">MongoDB 서버가 클라이언트 연결을 수신하는 데 사용하는 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1784">TCP port that the MongoDB server uses to listen for client connections.</span></span> |<span data-ttu-id="3b729-1785">선택 사항, 기본값: 27017</span><span class="sxs-lookup"><span data-stu-id="3b729-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="3b729-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-1786">authenticationType</span></span> |<span data-ttu-id="3b729-1787">Basic 또는 Anonymous입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="3b729-1788">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1788">Yes</span></span> |
| <span data-ttu-id="3b729-1789">username</span><span class="sxs-lookup"><span data-stu-id="3b729-1789">username</span></span> |<span data-ttu-id="3b729-1790">MongoDB에 액세스하는 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1790">User account to access MongoDB.</span></span> |<span data-ttu-id="3b729-1791">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="3b729-1792">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1792">password</span></span> |<span data-ttu-id="3b729-1793">사용자에 대한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1793">Password for the user.</span></span> |<span data-ttu-id="3b729-1794">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="3b729-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="3b729-1795">authSource</span></span> |<span data-ttu-id="3b729-1796">인증에 대한 자격 증명을 확인하는 데 사용하려는 MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1796">Name of the MongoDB database that you want to use to check your credentials for authentication.</span></span> |<span data-ttu-id="3b729-1797">선택 사항(기본 인증을 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="3b729-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="3b729-1798">기본값: 관리자 계정 및 databaseName 속성을 사용하는 지정된 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1798">default: uses the admin account and the database specified using databaseName property.</span></span> |
| <span data-ttu-id="3b729-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="3b729-1799">databaseName</span></span> |<span data-ttu-id="3b729-1800">액세스하려는 MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1800">Name of the MongoDB database that you want to access.</span></span> |<span data-ttu-id="3b729-1801">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1801">Yes</span></span> |
| <span data-ttu-id="3b729-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1802">gatewayName</span></span> |<span data-ttu-id="3b729-1803">데이터 저장소에 액세스하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1803">Name of the gateway that accesses the data store.</span></span> |<span data-ttu-id="3b729-1804">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1804">Yes</span></span> |
| <span data-ttu-id="3b729-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-1805">encryptedCredential</span></span> |<span data-ttu-id="3b729-1806">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="3b729-1807">옵션</span><span class="sxs-lookup"><span data-stu-id="3b729-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1808">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< The IP address or host name of the MongoDB server >",
            "port": "<The number of the TCP port that the MongoDB server uses to listen for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< The database that you want to use to check your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="3b729-1809">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1810">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1810">Dataset</span></span>
<span data-ttu-id="3b729-1811">MongoDB 데이터 집합을 정의하려면 데이터 집합의 **type**을 **MongoDbCollection**으로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1811">To define a MongoDB dataset, set the **type** of the dataset to **MongoDbCollection**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1812">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1812">Property</span></span> | <span data-ttu-id="3b729-1813">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1813">Description</span></span> | <span data-ttu-id="3b729-1814">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="3b729-1815">collectionName</span></span> |<span data-ttu-id="3b729-1816">MongoDB 데이터베이스에 있는 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1816">Name of the collection in MongoDB database.</span></span> |<span data-ttu-id="3b729-1817">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1818">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1818">Example</span></span>

```json
{
    "name": "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="3b729-1819">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="3b729-1820">복사 활동의 MongoDB 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1821">MongoDB에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **MongoDbSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1821">If you are copying data from MongoDB, set the **source type** of the copy activity to **MongoDbSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1822">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1822">Property</span></span> | <span data-ttu-id="3b729-1823">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1823">Description</span></span> | <span data-ttu-id="3b729-1824">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1824">Allowed values</span></span> | <span data-ttu-id="3b729-1825">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1826">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-1826">query</span></span> |<span data-ttu-id="3b729-1827">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1827">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-1828">SQL-92 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1828">SQL-92 query string.</span></span> <span data-ttu-id="3b729-1829">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-1830">아니요(**데이터 집합**의 **collectionName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1831">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1831">Example</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1832">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="3b729-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="3b729-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-1834">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1834">Linked service</span></span>
<span data-ttu-id="3b729-1835">Amazon S3 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AwsAccessKey**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1835">To define an Amazon S3 linked service, set the **type** of the linked service to **AwsAccessKey**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-1836">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1836">Property</span></span> | <span data-ttu-id="3b729-1837">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1837">Description</span></span> | <span data-ttu-id="3b729-1838">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1838">Allowed values</span></span> | <span data-ttu-id="3b729-1839">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="3b729-1840">accessKeyID</span></span> |<span data-ttu-id="3b729-1841">비밀 액세스 키의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1841">ID of the secret access key.</span></span> |<span data-ttu-id="3b729-1842">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1842">string</span></span> |<span data-ttu-id="3b729-1843">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1843">Yes</span></span> |
| <span data-ttu-id="3b729-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="3b729-1844">secretAccessKey</span></span> |<span data-ttu-id="3b729-1845">비밀 액세스 키 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1845">The secret access key itself.</span></span> |<span data-ttu-id="3b729-1846">암호화된 비밀 문자열</span><span class="sxs-lookup"><span data-stu-id="3b729-1846">Encrypted secret string</span></span> |<span data-ttu-id="3b729-1847">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-1848">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1848">Example</span></span>
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

<span data-ttu-id="3b729-1849">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1850">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1850">Dataset</span></span>
<span data-ttu-id="3b729-1851">Amazon S3 데이터 집합을 정의하려면 데이터 집합의 **type**을 **AmazonS3**으로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1851">To define an Amazon S3 dataset, set the **type** of the dataset to **AmazonS3**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1852">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1852">Property</span></span> | <span data-ttu-id="3b729-1853">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1853">Description</span></span> | <span data-ttu-id="3b729-1854">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1854">Allowed values</span></span> | <span data-ttu-id="3b729-1855">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="3b729-1856">bucketName</span></span> |<span data-ttu-id="3b729-1857">S3 버킷 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1857">The S3 bucket name.</span></span> |<span data-ttu-id="3b729-1858">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1858">String</span></span> |<span data-ttu-id="3b729-1859">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1859">Yes</span></span> |
| <span data-ttu-id="3b729-1860">key</span><span class="sxs-lookup"><span data-stu-id="3b729-1860">key</span></span> |<span data-ttu-id="3b729-1861">S3 개체 키입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1861">The S3 object key.</span></span> |<span data-ttu-id="3b729-1862">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1862">String</span></span> |<span data-ttu-id="3b729-1863">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1863">No</span></span> |
| <span data-ttu-id="3b729-1864">접두사</span><span class="sxs-lookup"><span data-stu-id="3b729-1864">prefix</span></span> |<span data-ttu-id="3b729-1865">S3 개체 키에 대한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1865">Prefix for the S3 object key.</span></span> <span data-ttu-id="3b729-1866">이 접두사로 시작하는 키를 가진 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="3b729-1867">키가 비어 있을 때에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="3b729-1868">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1868">String</span></span> |<span data-ttu-id="3b729-1869">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1869">No</span></span> |
| <span data-ttu-id="3b729-1870">버전</span><span class="sxs-lookup"><span data-stu-id="3b729-1870">version</span></span> |<span data-ttu-id="3b729-1871">S3 버전 관리를 사용하도록 설정되면 S3 개체의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1871">The version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="3b729-1872">string</span><span class="sxs-lookup"><span data-stu-id="3b729-1872">String</span></span> |<span data-ttu-id="3b729-1873">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1873">No</span></span> |
| <span data-ttu-id="3b729-1874">format</span><span class="sxs-lookup"><span data-stu-id="3b729-1874">format</span></span> | <span data-ttu-id="3b729-1875">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1875">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-1876">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1876">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-1877">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-1878">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1878">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-1879">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1879">No</span></span> | |
| <span data-ttu-id="3b729-1880">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-1880">compression</span></span> | <span data-ttu-id="3b729-1881">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1881">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-1882">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-1883">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1883">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-1884">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-1885">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="3b729-1886">bucketName + 키는 S3 개체의 위치를 지정합니다. 여기서 버킷은 S3 개체에 대한 루트 컨테이너이며 키는 S3 개체의 전체 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1886">bucketName + key specifies the location of the S3 object where bucket is the root container for S3 objects and key is the full path to S3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="3b729-1887">예제: 샘플 데이터 집합(prefix 포함)</span><span class="sxs-lookup"><span data-stu-id="3b729-1887">Example: Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="3b729-1888">예제: 샘플 데이터 집합(version 포함)</span><span class="sxs-lookup"><span data-stu-id="3b729-1888">Example: Sample data set (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="3b729-1889">예제: S3에 대한 동적 경로</span><span class="sxs-lookup"><span data-stu-id="3b729-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="3b729-1890">이 샘플에서는 Amazon S3 데이터 집합의 키 및 bucketName 속성에 대해 고정 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1890">In the sample, we use fixed values for key and bucketName properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="3b729-1891">SliceStart와 같은 시스템 변수를 사용하여 데이터 팩터리가 런타임에 동적으로 키와 bucketName 계산하게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1891">You can have Data Factory calculate the key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="3b729-1892">Amazon S3 데이터 집합의 접두사 속성에 대해서도 동일하게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1892">You can do the same for the prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="3b729-1893">지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="3b729-1894">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#dataset-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="3b729-1895">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1896">Amazon S3에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **FileSystemSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1896">If you are copying data from Amazon S3, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>


| <span data-ttu-id="3b729-1897">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1897">Property</span></span> | <span data-ttu-id="3b729-1898">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1898">Description</span></span> | <span data-ttu-id="3b729-1899">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1899">Allowed values</span></span> | <span data-ttu-id="3b729-1900">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-1901">recursive</span></span> |<span data-ttu-id="3b729-1902">S3 개체를 디렉터리 아래에 재귀적으로 나열할 것인지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1902">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="3b729-1903">True/False</span><span class="sxs-lookup"><span data-stu-id="3b729-1903">true/false</span></span> |<span data-ttu-id="3b729-1904">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-1905">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1905">Example</span></span>


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

<span data-ttu-id="3b729-1906">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="3b729-1907">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="3b729-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-1908">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-1908">Linked service</span></span>
<span data-ttu-id="3b729-1909">**온-프레미스 파일 서버** 연결 서비스를 사용하면 Azure Data Factory에 온-프레미스 파일 시스템을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1909">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="3b729-1910">다음 표에서는 온-프레미스 파일 서버 연결 서비스에 지정된 JSON 요소에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1910">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="3b729-1911">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1911">Property</span></span> | <span data-ttu-id="3b729-1912">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1912">Description</span></span> | <span data-ttu-id="3b729-1913">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1914">type</span><span class="sxs-lookup"><span data-stu-id="3b729-1914">type</span></span> |<span data-ttu-id="3b729-1915">type 속성은 **OnPremisesFileServer**로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1915">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="3b729-1916">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1916">Yes</span></span> |
| <span data-ttu-id="3b729-1917">host</span><span class="sxs-lookup"><span data-stu-id="3b729-1917">host</span></span> |<span data-ttu-id="3b729-1918">복사할 폴더의 루트 경로를 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1918">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="3b729-1919">문자열에서 특수 문자로 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1919">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="3b729-1920">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="3b729-1921">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1921">Yes</span></span> |
| <span data-ttu-id="3b729-1922">userId</span><span class="sxs-lookup"><span data-stu-id="3b729-1922">userid</span></span> |<span data-ttu-id="3b729-1923">서버에 대한 액세스 권한이 있는 사용자의 ID를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1923">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="3b729-1924">아니요(encryptedCredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="3b729-1925">password</span><span class="sxs-lookup"><span data-stu-id="3b729-1925">password</span></span> |<span data-ttu-id="3b729-1926">사용자(userid)의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1926">Specify the password for the user (userid).</span></span> |<span data-ttu-id="3b729-1927">아니요(encryptedcredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="3b729-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-1928">encryptedCredential</span></span> |<span data-ttu-id="3b729-1929">New-AzureRmDataFactoryEncryptValue cmdlet을 실행하여 얻을 수 있는 암호화된 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1929">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="3b729-1930">아니요(일반 텍스트에 userid 및 암호를 지정하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-1930">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="3b729-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-1931">gatewayName</span></span> |<span data-ttu-id="3b729-1932">Data Factory에서 온-프레미스 파일 서버에 연결하는 데 사용해야 하는 게이트웨이의 이름을 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1932">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="3b729-1933">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="3b729-1934">샘플 폴더 경로 정의</span><span class="sxs-lookup"><span data-stu-id="3b729-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="3b729-1935">시나리오</span><span class="sxs-lookup"><span data-stu-id="3b729-1935">Scenario</span></span> | <span data-ttu-id="3b729-1936">연결된 서비스 정의의 호스트</span><span class="sxs-lookup"><span data-stu-id="3b729-1936">Host in linked service definition</span></span> | <span data-ttu-id="3b729-1937">데이터 집합 정의의 folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1938">데이터 관리 게이트웨이 컴퓨터의 로컬 폴더: </span><span class="sxs-lookup"><span data-stu-id="3b729-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="3b729-1939">예: D:\\\* 또는 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="3b729-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="3b729-1940">D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="3b729-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="3b729-1941">localhost(데이터 관리 게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="3b729-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="3b729-1942">.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="3b729-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="3b729-1943">D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="3b729-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="3b729-1944">원격 공유 폴더: </span><span class="sxs-lookup"><span data-stu-id="3b729-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="3b729-1945">예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="3b729-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="3b729-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="3b729-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="3b729-1947">.\\\\ 또는 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="3b729-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="3b729-1948">예제: 일반 텍스트에 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-1948">Example: Using username and password in plain text</span></span>

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="3b729-1949">예제: encryptedcredential 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-1949">Example: Using encryptedcredential</span></span>

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="3b729-1950">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-1951">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-1951">Dataset</span></span>
<span data-ttu-id="3b729-1952">파일 시스템 데이터 집합을 정의하려면 데이터 집합의 **type**을 **FileShare**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1952">To define a File System dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-1953">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1953">Property</span></span> | <span data-ttu-id="3b729-1954">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1954">Description</span></span> | <span data-ttu-id="3b729-1955">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-1956">folderPath</span></span> |<span data-ttu-id="3b729-1957">폴더의 하위 경로를 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1957">Specifies the subpath to the folder.</span></span> <span data-ttu-id="3b729-1958">문자열에서 특수 문자로 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1958">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="3b729-1959">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="3b729-1960">이 속성을 **partitionBy** 와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1960">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="3b729-1961">예</span><span class="sxs-lookup"><span data-stu-id="3b729-1961">Yes</span></span> |
| <span data-ttu-id="3b729-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-1962">fileName</span></span> |<span data-ttu-id="3b729-1963">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1963">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="3b729-1964">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1964">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="3b729-1965">출력 데이터 집합에 대한 fileName이 지정되는 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1965">When fileName is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="3b729-1966">`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="3b729-1967">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1967">No</span></span> |
| <span data-ttu-id="3b729-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="3b729-1968">fileFilter</span></span> |<span data-ttu-id="3b729-1969">모든 파일이 아닌 folderPath의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1969">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="3b729-1970">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="3b729-1971">예 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="3b729-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="3b729-1972">예 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="3b729-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="3b729-1973">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="3b729-1974">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1974">No</span></span> |
| <span data-ttu-id="3b729-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-1975">partitionedBy</span></span> |<span data-ttu-id="3b729-1976">partitionedBy를 사용하면 시계열 데이터의 동적 folderPath/fileName을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1976">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="3b729-1977">예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-1978">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1978">No</span></span> |
| <span data-ttu-id="3b729-1979">format</span><span class="sxs-lookup"><span data-stu-id="3b729-1979">format</span></span> | <span data-ttu-id="3b729-1980">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1980">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-1981">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1981">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-1982">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-1983">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1983">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-1984">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1984">No</span></span> |
| <span data-ttu-id="3b729-1985">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-1985">compression</span></span> | <span data-ttu-id="3b729-1986">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1986">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-1987">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-1988">[Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-1989">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3b729-1990">fileName 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-1991">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-1991">Example</span></span>

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-1992">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="3b729-1993">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="3b729-1994">파일 시스템에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **FileSystemSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-1994">If you are copying data from File System, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-1995">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-1995">Property</span></span> | <span data-ttu-id="3b729-1996">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-1996">Description</span></span> | <span data-ttu-id="3b729-1997">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-1997">Allowed values</span></span> | <span data-ttu-id="3b729-1998">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-1999">recursive</span></span> |<span data-ttu-id="3b729-2000">하위 폴더 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2000">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-2001">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-2001">True, False (default)</span></span> |<span data-ttu-id="3b729-2002">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2003">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2003">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
            "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
<span data-ttu-id="3b729-2004">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="3b729-2005">복사 활동의 파일 시스템 싱크</span><span class="sxs-lookup"><span data-stu-id="3b729-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="3b729-2006">파일 시스템에 데이터를 복사하는 경우 복사 활동의 **sink type**을 **FileSystemSink**로 설정하고 **sink** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2006">If you are copying data to File System, set the **sink type** of the copy activity to **FileSystemSink**, and specify following properties in the **sink** section:</span></span>

| <span data-ttu-id="3b729-2007">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2007">Property</span></span> | <span data-ttu-id="3b729-2008">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2008">Description</span></span> | <span data-ttu-id="3b729-2009">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2009">Allowed values</span></span> | <span data-ttu-id="3b729-2010">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="3b729-2011">copyBehavior</span></span> |<span data-ttu-id="3b729-2012">원본이 BlobSource 또는 FileSystem인 경우 복사 동작을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2012">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="3b729-2013">**PreserveHierarchy:** 대상 폴더에서 파일 계층 구조를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2013">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="3b729-2014">즉, 원본 폴더의 원본 파일 상대 경로는 대상 폴더의 대상 파일 상대 경로와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2014">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="3b729-2015">**FlattenHierarchy:** 원본 폴더의 모든 파일이 대상 폴더의 첫 번째 수준에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2015">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="3b729-2016">대상 파일은 자동 생성된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2016">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="3b729-2017">**MergeFiles:** 원본 폴더의 모든 파일을 하나의 파일로 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2017">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="3b729-2018">병합되는 파일 이름은 지정된 파일 이름/Blob 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2018">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="3b729-2019">그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="3b729-2020">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2020">No</span></span> |
<span data-ttu-id="3b729-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="3b729-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-2022">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2022">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-2023">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="3b729-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="3b729-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-2025">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2025">Linked service</span></span>
<span data-ttu-id="3b729-2026">FTP 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **FtpServer**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2026">To define an FTP linked service, set the **type** of the linked service to **FtpServer**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2027">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2027">Property</span></span> | <span data-ttu-id="3b729-2028">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2028">Description</span></span> | <span data-ttu-id="3b729-2029">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2029">Required</span></span> | <span data-ttu-id="3b729-2030">기본값</span><span class="sxs-lookup"><span data-stu-id="3b729-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2031">host</span><span class="sxs-lookup"><span data-stu-id="3b729-2031">host</span></span> |<span data-ttu-id="3b729-2032">FTP 서버의 이름 또는 IP 주소</span><span class="sxs-lookup"><span data-stu-id="3b729-2032">Name or IP address of the FTP Server</span></span> |<span data-ttu-id="3b729-2033">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="3b729-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2034">authenticationType</span></span> |<span data-ttu-id="3b729-2035">인증 유형 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2035">Specify authentication type</span></span> |<span data-ttu-id="3b729-2036">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2036">Yes</span></span> |<span data-ttu-id="3b729-2037">기본, 익명</span><span class="sxs-lookup"><span data-stu-id="3b729-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="3b729-2038">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2038">username</span></span> |<span data-ttu-id="3b729-2039">FTP 서버에 액세스하는 사용자</span><span class="sxs-lookup"><span data-stu-id="3b729-2039">User who has access to the FTP server</span></span> |<span data-ttu-id="3b729-2040">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="3b729-2041">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2041">password</span></span> |<span data-ttu-id="3b729-2042">사용자(사용자 이름) 암호</span><span class="sxs-lookup"><span data-stu-id="3b729-2042">Password for the user (username)</span></span> |<span data-ttu-id="3b729-2043">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="3b729-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-2044">encryptedCredential</span></span> |<span data-ttu-id="3b729-2045">FTP 서버 액세스를 위한 암호화된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="3b729-2045">Encrypted credential to access the FTP server</span></span> |<span data-ttu-id="3b729-2046">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="3b729-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2047">gatewayName</span></span> |<span data-ttu-id="3b729-2048">온-프레미스 FTP 서버에 연결하기 위한 데이터 관리 게이트웨이 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-2048">Name of the Data Management Gateway gateway to connect to an on-premises FTP server</span></span> |<span data-ttu-id="3b729-2049">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="3b729-2050">포트</span><span class="sxs-lookup"><span data-stu-id="3b729-2050">port</span></span> |<span data-ttu-id="3b729-2051">FTP 서버가 수신 대기하는 포트</span><span class="sxs-lookup"><span data-stu-id="3b729-2051">Port on which the FTP server is listening</span></span> |<span data-ttu-id="3b729-2052">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2052">No</span></span> |<span data-ttu-id="3b729-2053">21</span><span class="sxs-lookup"><span data-stu-id="3b729-2053">21</span></span> |
| <span data-ttu-id="3b729-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="3b729-2054">enableSsl</span></span> |<span data-ttu-id="3b729-2055">SSL/TLS 채널을 통해 FTP를 사용할지 여부</span><span class="sxs-lookup"><span data-stu-id="3b729-2055">Specify whether to use FTP over SSL/TLS channel</span></span> |<span data-ttu-id="3b729-2056">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2056">No</span></span> |<span data-ttu-id="3b729-2057">true</span><span class="sxs-lookup"><span data-stu-id="3b729-2057">true</span></span> |
| <span data-ttu-id="3b729-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="3b729-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="3b729-2059">SSL/TLS 채널을 통해 FTP를 사용할 때 서버 SSL 인증서 유효성 검사를 사용할지 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2059">Specify whether to enable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="3b729-2060">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2060">No</span></span> |<span data-ttu-id="3b729-2061">true</span><span class="sxs-lookup"><span data-stu-id="3b729-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="3b729-2062">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2062">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="3b729-2063">예제: 기본 인증에 일반 텍스트 형식의 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2063">Example: Using username and password in plain text for basic authentication</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="3b729-2064">예제: port, enableSsl, enableServerCertificateValidation 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="3b729-2065">예제: 인증 및 게이트웨이에 encryptedCredential 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

<span data-ttu-id="3b729-2066">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-2067">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2067">Dataset</span></span>
<span data-ttu-id="3b729-2068">FTP 데이터 집합을 정의하려면 데이터 집합의 **type**을 **FileShare**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2068">To define an FTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2069">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2069">Property</span></span> | <span data-ttu-id="3b729-2070">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2070">Description</span></span> | <span data-ttu-id="3b729-2071">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-2072">folderPath</span></span> |<span data-ttu-id="3b729-2073">폴더에 대한 하위 경로.</span><span class="sxs-lookup"><span data-stu-id="3b729-2073">Sub path to the folder.</span></span> <span data-ttu-id="3b729-2074">문자열의 특수 문자에 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2074">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="3b729-2075">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="3b729-2076">이 속성을 **partitionBy** 와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2076">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="3b729-2077">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2077">Yes</span></span> 
| <span data-ttu-id="3b729-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-2078">fileName</span></span> |<span data-ttu-id="3b729-2079">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2079">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="3b729-2080">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2080">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="3b729-2081">출력 데이터 집합에 대한 fileName이 지정되는 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2081">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="3b729-2082">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3b729-2083">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2083">No</span></span> |
| <span data-ttu-id="3b729-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="3b729-2084">fileFilter</span></span> |<span data-ttu-id="3b729-2085">모든 파일이 아닌 folderPath의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2085">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="3b729-2086">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="3b729-2087">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="3b729-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="3b729-2088">예 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="3b729-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="3b729-2089">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="3b729-2090">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="3b729-2091">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2091">No</span></span> |
| <span data-ttu-id="3b729-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-2092">partitionedBy</span></span> |<span data-ttu-id="3b729-2093">동적 folderPath, 시계열 데이터에 대한 filename을 지정하는 데 partitionedBy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2093">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="3b729-2094">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-2095">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2095">No</span></span> |
| <span data-ttu-id="3b729-2096">format</span><span class="sxs-lookup"><span data-stu-id="3b729-2096">format</span></span> | <span data-ttu-id="3b729-2097">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2097">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-2098">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2098">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-2099">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-2100">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2100">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-2101">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2101">No</span></span> |
| <span data-ttu-id="3b729-2102">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-2102">compression</span></span> | <span data-ttu-id="3b729-2103">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2103">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-2104">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-2105">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-2106">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2106">No</span></span> |
| <span data-ttu-id="3b729-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="3b729-2107">useBinaryTransfer</span></span> |<span data-ttu-id="3b729-2108">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="3b729-2109">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="3b729-2110">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2110">Default value: True.</span></span> <span data-ttu-id="3b729-2111">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="3b729-2112">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3b729-2113">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-2114">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="3b729-2115">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="3b729-2116">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2117">FTP 서버에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **FileSystemSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2117">If you are copying data from an FTP server, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2118">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2118">Property</span></span> | <span data-ttu-id="3b729-2119">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2119">Description</span></span> | <span data-ttu-id="3b729-2120">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2120">Allowed values</span></span> | <span data-ttu-id="3b729-2121">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-2122">recursive</span></span> |<span data-ttu-id="3b729-2123">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2123">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-2124">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-2124">True, False (default)</span></span> |<span data-ttu-id="3b729-2125">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2126">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2126">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

<span data-ttu-id="3b729-2127">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="3b729-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="3b729-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-2129">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2129">Linked service</span></span>
<span data-ttu-id="3b729-2130">HDFS 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **Hdfs**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2130">To define a HDFS linked service, set the **type** of the linked service to **Hdfs**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2131">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2131">Property</span></span> | <span data-ttu-id="3b729-2132">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2132">Description</span></span> | <span data-ttu-id="3b729-2133">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2134">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2134">type</span></span> |<span data-ttu-id="3b729-2135">형식 속성은 다음으로 설정해야 함: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="3b729-2135">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="3b729-2136">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2136">Yes</span></span> |
| <span data-ttu-id="3b729-2137">Url</span><span class="sxs-lookup"><span data-stu-id="3b729-2137">Url</span></span> |<span data-ttu-id="3b729-2138">HDFS에 대한 URL</span><span class="sxs-lookup"><span data-stu-id="3b729-2138">URL to the HDFS</span></span> |<span data-ttu-id="3b729-2139">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2139">Yes</span></span> |
| <span data-ttu-id="3b729-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2140">authenticationType</span></span> |<span data-ttu-id="3b729-2141">익명 또는 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="3b729-2142">HDFS 커넥터에 **Kerberos 인증**을 사용하려면 [이 섹션](#use-kerberos-authentication-for-hdfs-connector)을 참조하여 온-프레미스 환경을 적절히 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2142">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="3b729-2143">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2143">Yes</span></span> |
| <span data-ttu-id="3b729-2144">userName</span><span class="sxs-lookup"><span data-stu-id="3b729-2144">userName</span></span> |<span data-ttu-id="3b729-2145">Windows 인증에 대한 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="3b729-2146">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="3b729-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="3b729-2147">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2147">password</span></span> |<span data-ttu-id="3b729-2148">Windows 인증에 대한 암호.</span><span class="sxs-lookup"><span data-stu-id="3b729-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="3b729-2149">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="3b729-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="3b729-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2150">gatewayName</span></span> |<span data-ttu-id="3b729-2151">데이터 팩터리 서비스가 HDFS에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-2151">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="3b729-2152">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2152">Yes</span></span> |
| <span data-ttu-id="3b729-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-2153">encryptedCredential</span></span> |<span data-ttu-id="3b729-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) 출력.</span><span class="sxs-lookup"><span data-stu-id="3b729-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="3b729-2155">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="3b729-2156">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2156">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="3b729-2157">예제: Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2157">Example: Using Windows authentication</span></span>

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="3b729-2158">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-2159">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2159">Dataset</span></span>
<span data-ttu-id="3b729-2160">HDFS 데이터 집합을 정의하려면 데이터 집합의 **type**을 **FileShare**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2160">To define a HDFS dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2161">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2161">Property</span></span> | <span data-ttu-id="3b729-2162">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2162">Description</span></span> | <span data-ttu-id="3b729-2163">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-2164">folderPath</span></span> |<span data-ttu-id="3b729-2165">파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2165">Path to the folder.</span></span> <span data-ttu-id="3b729-2166">예: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="3b729-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="3b729-2167">문자열의 특수 문자에 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2167">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="3b729-2168">예: 폴더\하위 폴더의 경우 폴더\\\\하위 폴더를 지정하고 d:\samplefolder의 경우 d:\\\\samplefolder를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="3b729-2169">이 속성을 **partitionBy**와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2169">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="3b729-2170">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2170">Yes</span></span> |
| <span data-ttu-id="3b729-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-2171">fileName</span></span> |<span data-ttu-id="3b729-2172">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2172">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="3b729-2173">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2173">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="3b729-2174">출력 데이터 집합에 대한 fileName이 지정되는 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2174">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="3b729-2175">Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3b729-2176">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2176">No</span></span> |
| <span data-ttu-id="3b729-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-2177">partitionedBy</span></span> |<span data-ttu-id="3b729-2178">동적 folderPath, 시계열 데이터에 대한 filename을 지정하는 데 partitionedBy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2178">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="3b729-2179">예를 들어 folderPath는 매시간 데이터에 대해 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-2180">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2180">No</span></span> |
| <span data-ttu-id="3b729-2181">format</span><span class="sxs-lookup"><span data-stu-id="3b729-2181">format</span></span> | <span data-ttu-id="3b729-2182">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2182">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-2183">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2183">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-2184">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-2185">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2185">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-2186">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2186">No</span></span> |
| <span data-ttu-id="3b729-2187">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-2187">compression</span></span> | <span data-ttu-id="3b729-2188">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2188">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-2189">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-2190">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-2191">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-2192">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3b729-2193">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-2194">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2194">Example</span></span>

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="3b729-2195">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="3b729-2196">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2197">HDFS에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **FileSystemSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2197">If you are copying data from HDFS, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

<span data-ttu-id="3b729-2198">**FileSystemSource**는 다음 속성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2198">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="3b729-2199">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2199">Property</span></span> | <span data-ttu-id="3b729-2200">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2200">Description</span></span> | <span data-ttu-id="3b729-2201">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2201">Allowed values</span></span> | <span data-ttu-id="3b729-2202">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-2203">recursive</span></span> |<span data-ttu-id="3b729-2204">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2204">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-2205">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-2205">True, False (default)</span></span> |<span data-ttu-id="3b729-2206">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2207">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2207">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

<span data-ttu-id="3b729-2208">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="3b729-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="3b729-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-2210">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2210">Linked service</span></span>
<span data-ttu-id="3b729-2211">SFTP 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **Sftp**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2211">To define an SFTP linked service, set the **type** of the linked service to **Sftp**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2212">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2212">Property</span></span> | <span data-ttu-id="3b729-2213">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2213">Description</span></span> | <span data-ttu-id="3b729-2214">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2215">host</span><span class="sxs-lookup"><span data-stu-id="3b729-2215">host</span></span> | <span data-ttu-id="3b729-2216">SFTP 서버의 이름 또는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2216">Name or IP address of the SFTP server.</span></span> |<span data-ttu-id="3b729-2217">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2217">Yes</span></span> |
| <span data-ttu-id="3b729-2218">포트</span><span class="sxs-lookup"><span data-stu-id="3b729-2218">port</span></span> |<span data-ttu-id="3b729-2219">SFTP 서버가 수신하는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2219">Port on which the SFTP server is listening.</span></span> <span data-ttu-id="3b729-2220">기본값은 21입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2220">The default value is: 21</span></span> |<span data-ttu-id="3b729-2221">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2221">No</span></span> |
| <span data-ttu-id="3b729-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2222">authenticationType</span></span> |<span data-ttu-id="3b729-2223">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2223">Specify authentication type.</span></span> <span data-ttu-id="3b729-2224">허용되는 값은 **기본** 및 **SshPublicKey**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="3b729-2225">더 많은 속성 및 각 속성의 JSON 샘플은 [기본 인증 사용](#using-basic-authentication) 및 [SSH 공개 키 인증 사용](#using-ssh-public-key-authentication) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2225">Refer to [Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="3b729-2226">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2226">Yes</span></span> |
| <span data-ttu-id="3b729-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="3b729-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="3b729-2228">호스트 키 유효성 검사를 건너뛸지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2228">Specify whether to skip host key validation.</span></span> | <span data-ttu-id="3b729-2229">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2229">No.</span></span> <span data-ttu-id="3b729-2230">기본값: false</span><span class="sxs-lookup"><span data-stu-id="3b729-2230">The default value: false</span></span> |
| <span data-ttu-id="3b729-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="3b729-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="3b729-2232">호스트 키의 지문을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2232">Specify the finger print of the host key.</span></span> | <span data-ttu-id="3b729-2233">`skipHostKeyValidation`이 false로 지정되면 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2233">Yes if the `skipHostKeyValidation` is set to false.</span></span>  |
| <span data-ttu-id="3b729-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2234">gatewayName</span></span> |<span data-ttu-id="3b729-2235">온-프레미스 SFTP 서버에 연결하기 위한 데이터 관리 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2235">Name of the Data Management Gateway to connect to an on-premises SFTP server.</span></span> | <span data-ttu-id="3b729-2236">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="3b729-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-2237">encryptedCredential</span></span> | <span data-ttu-id="3b729-2238">SFTP 서버 액세스를 위한 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2238">Encrypted credential to access the SFTP server.</span></span> <span data-ttu-id="3b729-2239">복사 마법사 또는 ClickOnce 팝업 대화 상자에서 기본 인증(사용자 이름 + 암호) 또는 SshPublicKey 인증(사용자 이름 + 개인 키 경로 또는 콘텐츠)를 지정할 때 자정으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="3b729-2240">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2240">No.</span></span> <span data-ttu-id="3b729-2241">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="3b729-2242">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="3b729-2243">기본 인증을 사용하려면 `authenticationType`을 `Basic`으로 설정하고, 마지막 섹션에서 소개한 SFTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2243">To use basic authentication, set `authenticationType` as `Basic`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="3b729-2244">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2244">Property</span></span> | <span data-ttu-id="3b729-2245">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2245">Description</span></span> | <span data-ttu-id="3b729-2246">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2247">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2247">username</span></span> | <span data-ttu-id="3b729-2248">SFTP 서버에 액세스하는 사용자.</span><span class="sxs-lookup"><span data-stu-id="3b729-2248">User who has access to the SFTP server.</span></span> |<span data-ttu-id="3b729-2249">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2249">Yes</span></span> |
| <span data-ttu-id="3b729-2250">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2250">password</span></span> | <span data-ttu-id="3b729-2251">사용자(사용자 이름) 암호.</span><span class="sxs-lookup"><span data-stu-id="3b729-2251">Password for the user (username).</span></span> | <span data-ttu-id="3b729-2252">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2252">Yes</span></span> |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="3b729-2253">예제: 암호화된 자격 증명으로 기본 인증**</span><span class="sxs-lookup"><span data-stu-id="3b729-2253">Example: Basic authentication with encrypted credential**</span></span>

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="3b729-2254">SSH 공개 키 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="3b729-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="3b729-2255">기본 인증을 사용하려면 `authenticationType`을 `SshPublicKey`으로 설정하고, 마지막 섹션에서 소개한 SFTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2255">To use basic authentication, set `authenticationType` as `SshPublicKey`, and specify the following properties besides the SFTP connector generic ones introduced in the last section:</span></span>

| <span data-ttu-id="3b729-2256">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2256">Property</span></span> | <span data-ttu-id="3b729-2257">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2257">Description</span></span> | <span data-ttu-id="3b729-2258">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2259">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2259">username</span></span> |<span data-ttu-id="3b729-2260">SFTP 서버에 액세스하는 사용자</span><span class="sxs-lookup"><span data-stu-id="3b729-2260">User who has access to the SFTP server</span></span> |<span data-ttu-id="3b729-2261">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2261">Yes</span></span> |
| <span data-ttu-id="3b729-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="3b729-2262">privateKeyPath</span></span> | <span data-ttu-id="3b729-2263">게이트웨이에서 액세스할 수 있는 개인 키 파일의 절대 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2263">Specify absolute path to the private key file that gateway can access.</span></span> | <span data-ttu-id="3b729-2264">`privateKeyPath` 또는 `privateKeyContent`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2264">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="3b729-2265">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="3b729-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="3b729-2266">privateKeyContent</span></span> | <span data-ttu-id="3b729-2267">개인 키 콘텐츠의 직렬화된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2267">A serialized string of the private key content.</span></span> <span data-ttu-id="3b729-2268">복사 마법사는 개인 키 파일을 읽고 개인 키 콘텐츠를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2268">The Copy Wizard can read the private key file and extract the private key content automatically.</span></span> <span data-ttu-id="3b729-2269">다른 도구/SDK를 사용하는 경우 privateKeyPath 속성을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2269">If you are using any other tool/SDK, use the privateKeyPath property instead.</span></span> | <span data-ttu-id="3b729-2270">`privateKeyPath` 또는 `privateKeyContent`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2270">Specify either the `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="3b729-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="3b729-2271">passPhrase</span></span> | <span data-ttu-id="3b729-2272">키 파일이 암호문으로 보호되는 경우 개인 키를 해독하는 암호문/암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2272">Specify the pass phrase/password to decrypt the private key if the key file is protected by a pass phrase.</span></span> | <span data-ttu-id="3b729-2273">개인 키 파일이 암호문으로 보호되는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2273">Yes if the private key file is protected by a pass phrase.</span></span> |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="3b729-2274">예제: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증**</span><span class="sxs-lookup"><span data-stu-id="3b729-2274">Example: SshPublicKey authentication using private key content**</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of the private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="3b729-2275">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-2276">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2276">Dataset</span></span>
<span data-ttu-id="3b729-2277">SFTP 데이터 집합을 정의하려면 데이터 집합의 **type**을 **FileShare**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2277">To define an SFTP dataset, set the **type** of the dataset to **FileShare**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2278">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2278">Property</span></span> | <span data-ttu-id="3b729-2279">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2279">Description</span></span> | <span data-ttu-id="3b729-2280">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="3b729-2281">folderPath</span></span> |<span data-ttu-id="3b729-2282">폴더에 대한 하위 경로.</span><span class="sxs-lookup"><span data-stu-id="3b729-2282">Sub path to the folder.</span></span> <span data-ttu-id="3b729-2283">문자열의 특수 문자에 이스케이프 문자 '\'를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2283">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="3b729-2284">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="3b729-2285">이 속성을 **partitionBy** 와 결합하여 조각 시작/종료 날짜/시간을 기준으로 폴더 경로를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2285">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="3b729-2286">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2286">Yes</span></span> |
| <span data-ttu-id="3b729-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="3b729-2287">fileName</span></span> |<span data-ttu-id="3b729-2288">폴더에서 특정 파일을 참조하기 위해 테이블을 사용하려는 경우 **folderPath** 에 있는 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2288">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="3b729-2289">이 속성에 값을 지정하지 않으면 테이블은 폴더에 있는 모든 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2289">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="3b729-2290">출력 데이터 집합에 대한 fileName이 지정되는 경우 생성되는 파일의 이름 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2290">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="3b729-2291">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="3b729-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="3b729-2292">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2292">No</span></span> |
| <span data-ttu-id="3b729-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="3b729-2293">fileFilter</span></span> |<span data-ttu-id="3b729-2294">모든 파일이 아닌 folderPath의 파일 하위 집합을 선택하는데 사용할 필터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2294">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="3b729-2295">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="3b729-2296">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="3b729-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="3b729-2297">예 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="3b729-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="3b729-2298">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="3b729-2299">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="3b729-2300">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2300">No</span></span> |
| <span data-ttu-id="3b729-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="3b729-2301">partitionedBy</span></span> |<span data-ttu-id="3b729-2302">동적 folderPath, 시계열 데이터에 대한 filename을 지정하는 데 partitionedBy를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2302">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="3b729-2303">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="3b729-2304">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2304">No</span></span> |
| <span data-ttu-id="3b729-2305">format</span><span class="sxs-lookup"><span data-stu-id="3b729-2305">format</span></span> | <span data-ttu-id="3b729-2306">**TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2306">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-2307">이 값 중 하나로 서식에서 **type** 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2307">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="3b729-2308">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="3b729-2309">파일 기반 저장소(이진 복사) 간에 **파일을 있는 그대로 복사**하려는 경우 입력 및 출력 데이터 집합 정의 둘 다에서 형식 섹션을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2309">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="3b729-2310">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2310">No</span></span> |
| <span data-ttu-id="3b729-2311">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-2311">compression</span></span> | <span data-ttu-id="3b729-2312">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2312">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-2313">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-2314">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-2315">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-2316">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2316">No</span></span> |
| <span data-ttu-id="3b729-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="3b729-2317">useBinaryTransfer</span></span> |<span data-ttu-id="3b729-2318">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="3b729-2319">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="3b729-2320">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2320">Default value: True.</span></span> <span data-ttu-id="3b729-2321">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="3b729-2322">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="3b729-2323">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-2324">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path to shared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="3b729-2325">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="3b729-2326">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2327">SFTP 소스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **FileSystemSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2327">If you are copying data from an SFTP source, set the **source type** of the copy activity to **FileSystemSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2328">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2328">Property</span></span> | <span data-ttu-id="3b729-2329">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2329">Description</span></span> | <span data-ttu-id="3b729-2330">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2330">Allowed values</span></span> | <span data-ttu-id="3b729-2331">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="3b729-2332">recursive</span></span> |<span data-ttu-id="3b729-2333">하위 폴더에서 또는 지정된 폴더에서만 데이터를 재귀적으로 읽을지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2333">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="3b729-2334">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="3b729-2334">True, False (default)</span></span> |<span data-ttu-id="3b729-2335">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="3b729-2336">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2336">Example</span></span>

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

<span data-ttu-id="3b729-2337">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="3b729-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="3b729-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-2339">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2339">Linked service</span></span>
<span data-ttu-id="3b729-2340">HTTP 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **Http**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2340">To define a HTTP linked service, set the **type** of the linked service to **Http**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2341">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2341">Property</span></span> | <span data-ttu-id="3b729-2342">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2342">Description</span></span> | <span data-ttu-id="3b729-2343">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2344">URL</span><span class="sxs-lookup"><span data-stu-id="3b729-2344">url</span></span> | <span data-ttu-id="3b729-2345">웹 서버에 대한 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2345">Base URL to the Web Server</span></span> | <span data-ttu-id="3b729-2346">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2346">Yes</span></span> |
| <span data-ttu-id="3b729-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2347">authenticationType</span></span> | <span data-ttu-id="3b729-2348">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2348">Specifies the authentication type.</span></span> <span data-ttu-id="3b729-2349">허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="3b729-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="3b729-2350">각 인증 형식에 대한 더 많은 속성 및 JSON 샘플은 표 아래 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2350">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="3b729-2351">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2351">Yes</span></span> |
| <span data-ttu-id="3b729-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="3b729-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="3b729-2353">소스가 HTTPS 웹 서버인 경우 서버 SSL 인증서 유효성 검사를 사용할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2353">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="3b729-2354">아니요. 기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2354">No, default is true</span></span> |
| <span data-ttu-id="3b729-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2355">gatewayName</span></span> | <span data-ttu-id="3b729-2356">온-프레미스 HTTP 소스에 연결하기 위한 데이터 관리 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2356">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="3b729-2357">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="3b729-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-2358">encryptedCredential</span></span> | <span data-ttu-id="3b729-2359">HTTP 끝점 액세스를 위한 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2359">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="3b729-2360">복사 마법사 또는 ClickOnce 팝업 대화 상자에서 인증 정보를 구성할 때 자동 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2360">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="3b729-2361">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2361">No.</span></span> <span data-ttu-id="3b729-2362">온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="3b729-2363">예제: Basic, Digest 또는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="3b729-2364">`authenticationType`을 `Basic`, `Digest` 또는 `Windows`로 설정하고, 위에서 소개한 HTTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="3b729-2365">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2365">Property</span></span> | <span data-ttu-id="3b729-2366">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2366">Description</span></span> | <span data-ttu-id="3b729-2367">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2368">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2368">username</span></span> | <span data-ttu-id="3b729-2369">HTTP 끝점 액세스를 위한 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2369">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="3b729-2370">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2370">Yes</span></span> |
| <span data-ttu-id="3b729-2371">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2371">password</span></span> | <span data-ttu-id="3b729-2372">사용자(사용자 이름) 암호.</span><span class="sxs-lookup"><span data-stu-id="3b729-2372">Password for the user (username).</span></span> | <span data-ttu-id="3b729-2373">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2373">Yes</span></span> |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="3b729-2374">예제: ClientCertificate 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="3b729-2375">기본 인증을 사용하려면 `authenticationType`을 `ClientCertificate`로 설정하고, 위에서 소개한 HTTP 커넥터 일반 속성 외에 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2375">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="3b729-2376">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2376">Property</span></span> | <span data-ttu-id="3b729-2377">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2377">Description</span></span> | <span data-ttu-id="3b729-2378">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="3b729-2379">embeddedCertData</span></span> | <span data-ttu-id="3b729-2380">PFX(개인 정보 교환) 파일의 이진 데이터에 대해 Base64로 인코딩된 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="3b729-2380">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="3b729-2381">`embeddedCertData` 또는 `certThumbprint`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2381">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="3b729-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="3b729-2382">certThumbprint</span></span> | <span data-ttu-id="3b729-2383">게이트웨이 컴퓨터의 인증서 저장소에 설치된 인증서의 지문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2383">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="3b729-2384">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="3b729-2385">`embeddedCertData` 또는 `certThumbprint`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2385">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="3b729-2386">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2386">password</span></span> | <span data-ttu-id="3b729-2387">인증서와 연결된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2387">Password associated with the certificate.</span></span> | <span data-ttu-id="3b729-2388">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2388">No</span></span> |

<span data-ttu-id="3b729-2389">인증에 `certThumbprint`를 사용하고 인증서가 로컬 컴퓨터의 개인 저장소에 설치된 경우 게이트웨이 서비스에 읽기 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2389">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="3b729-2390">MMC(Microsoft Management Console)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="3b729-2391">**로컬 컴퓨터**를 대상으로 하는 **인증서** 스냅인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2391">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="3b729-2392">**인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="3b729-2393">개인 저장소에서 인증서를 마우스 오른쪽 단추로 클릭하고 **모든 작업**->**개인 키 관리...**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2393">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="3b729-2394">**보안** 탭에서 인증서에 대한 읽기 권한으로 데이터 관리 게이트웨이 호스트 서비스를 실행 중인 사용자 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2394">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

<span data-ttu-id="3b729-2395">**예제: 클라이언트 인증서 사용:** 이 연결된 서비스는 데이터 팩터리를 온-프레미스 HTTP 웹 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2395">**Example: using client certificate:** This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="3b729-2396">데이터 관리 게이트웨이가 설치된 컴퓨터에 설치된 클라이언트 인증서를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2396">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="3b729-2397">예제: 파일로 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="3b729-2398">이 연결된 서비스는 데이터 팩터리를 온-프레미스 HTTP 웹 서버에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2398">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="3b729-2399">데이터 관리 게이트웨이가 설치된 컴퓨터에서 클라이언트 인증서 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2399">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

<span data-ttu-id="3b729-2400">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-2401">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2401">Dataset</span></span>
<span data-ttu-id="3b729-2402">HTTP 데이터 집합을 정의하려면 데이터 집합의 **type**을 **Http**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2402">To define a HTTP dataset, set the **type** of the dataset to **Http**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2403">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2403">Property</span></span> | <span data-ttu-id="3b729-2404">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2404">Description</span></span> | <span data-ttu-id="3b729-2405">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="3b729-2406">relativeUrl</span></span> | <span data-ttu-id="3b729-2407">데이터를 포함하는 리소스에 대한 상대 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2407">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="3b729-2408">경로를 지정하지 않으면 연결된 서비스 정의에 지정된 URL만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2408">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="3b729-2409">동적 URL을 구성하려면 [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md)를 사용할 수 있습니다. 예제: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`</span><span class="sxs-lookup"><span data-stu-id="3b729-2409">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="3b729-2410">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2410">No</span></span> |
| <span data-ttu-id="3b729-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="3b729-2411">requestMethod</span></span> | <span data-ttu-id="3b729-2412">HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2412">Http method.</span></span> <span data-ttu-id="3b729-2413">허용되는 값은 **GET** 또는 **POST**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="3b729-2414">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2414">No.</span></span> <span data-ttu-id="3b729-2415">기본값은 `GET`입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="3b729-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="3b729-2416">additionalHeaders</span></span> | <span data-ttu-id="3b729-2417">추가 HTTP 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="3b729-2418">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2418">No</span></span> |
| <span data-ttu-id="3b729-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="3b729-2419">requestBody</span></span> | <span data-ttu-id="3b729-2420">HTTP 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2420">Body for HTTP request.</span></span> | <span data-ttu-id="3b729-2421">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2421">No</span></span> |
| <span data-ttu-id="3b729-2422">format</span><span class="sxs-lookup"><span data-stu-id="3b729-2422">format</span></span> | <span data-ttu-id="3b729-2423">데이터를 구문 분석하지 않고 **HTTP 끝점에서 데이터를 그대로 검색**하려면 이 서식 설정을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2423">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="3b729-2424">복사 중에 HTTP 응답 내용을 구문 분석하려면 **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**과 같은 서식 유형이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2424">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="3b729-2425">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="3b729-2426">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2426">No</span></span> |
| <span data-ttu-id="3b729-2427">압축</span><span class="sxs-lookup"><span data-stu-id="3b729-2427">compression</span></span> | <span data-ttu-id="3b729-2428">데이터에 대한 압축 유형 및 수준을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2428">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="3b729-2429">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="3b729-2430">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="3b729-2431">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="3b729-2432">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2432">No</span></span> |

#### <a name="example-using-the-get-default-method"></a><span data-ttu-id="3b729-2433">예제: GET(기본) 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2433">Example: using the GET (default) method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-the-post-method"></a><span data-ttu-id="3b729-2434">예제: POST 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2434">Example: using the POST method</span></span>

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="3b729-2435">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="3b729-2436">복사 활동의 HTTP 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2437">HTTP 소스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **HttpSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2437">If you are copying data from a HTTP source, set the **source type** of the copy activity to **HttpSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2438">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2438">Property</span></span> | <span data-ttu-id="3b729-2439">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2439">Description</span></span> | <span data-ttu-id="3b729-2440">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="3b729-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="3b729-2441">httpRequestTimeout</span></span> | <span data-ttu-id="3b729-2442">HTTP 요청이 응답을 받을 시간 제한(TimeSpan)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2442">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="3b729-2443">응답 데이터를 읽는 시간 제한이 아니라, 응답을 받을 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2443">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="3b729-2444">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2444">No.</span></span> <span data-ttu-id="3b729-2445">기본값: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="3b729-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-2446">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-2447">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="3b729-2448">OData</span><span class="sxs-lookup"><span data-stu-id="3b729-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-2449">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2449">Linked service</span></span>
<span data-ttu-id="3b729-2450">OData 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OData**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2450">To define an OData linked service, set the **type** of the linked service to **OData**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2451">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2451">Property</span></span> | <span data-ttu-id="3b729-2452">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2452">Description</span></span> | <span data-ttu-id="3b729-2453">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2454">URL</span><span class="sxs-lookup"><span data-stu-id="3b729-2454">url</span></span> |<span data-ttu-id="3b729-2455">OData 서비스의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2455">Url of the OData service.</span></span> |<span data-ttu-id="3b729-2456">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2456">Yes</span></span> |
| <span data-ttu-id="3b729-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2457">authenticationType</span></span> |<span data-ttu-id="3b729-2458">OData 소스에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2458">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="3b729-2459">클라우드 OData의 경우 가능한 값은 익명, 기본 및 OAuth입니다(Azure Data Factory는 현재 Azure Active Directory 기반 OAuth만 지원).</span><span class="sxs-lookup"><span data-stu-id="3b729-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="3b729-2460">온-프레미스 OData의 경우 가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="3b729-2461">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2461">Yes</span></span> |
| <span data-ttu-id="3b729-2462">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2462">username</span></span> |<span data-ttu-id="3b729-2463">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="3b729-2464">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="3b729-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="3b729-2465">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2465">password</span></span> |<span data-ttu-id="3b729-2466">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2466">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-2467">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="3b729-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="3b729-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="3b729-2468">authorizedCredential</span></span> |<span data-ttu-id="3b729-2469">OAuth를 사용하는 경우 Data Factory Copy Wizard 또는 Editor에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 이 속성의 값이 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2469">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="3b729-2470">예(OAuth 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="3b729-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="3b729-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2471">gatewayName</span></span> |<span data-ttu-id="3b729-2472">데이터 팩터리 서비스가 온-프레미스 OData 서비스에 연결하는 데 사용해야 하는 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-2472">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="3b729-2473">온-프레미스 OData 소스의 데이터를 복사하는 경우에만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="3b729-2474">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="3b729-2475">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2475">Example - Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="3b729-2476">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2476">Example - Using Anonymous authentication</span></span>

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="3b729-2477">예제: 온-프레미스 OData 소스에 액세스하는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="3b729-2478">예제: 클라우드 OData 소스에 액세스하는 OAuth 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="3b729-2479">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="3b729-2480">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2480">Dataset</span></span>
<span data-ttu-id="3b729-2481">OData 데이터 집합을 정의하려면 데이터 집합의 **type**을 **ODataResource**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2481">To define an OData dataset, set the **type** of the dataset to **ODataResource**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2482">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2482">Property</span></span> | <span data-ttu-id="3b729-2483">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2483">Description</span></span> | <span data-ttu-id="3b729-2484">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2485">경로</span><span class="sxs-lookup"><span data-stu-id="3b729-2485">path</span></span> |<span data-ttu-id="3b729-2486">OData 리소스에 대한 경로</span><span class="sxs-lookup"><span data-stu-id="3b729-2486">Path to the OData resource</span></span> |<span data-ttu-id="3b729-2487">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2488">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2488">Example</span></span>

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

<span data-ttu-id="3b729-2489">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-2490">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2491">OData 소스에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2491">If you are copying data from an OData source, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2492">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2492">Property</span></span> | <span data-ttu-id="3b729-2493">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2493">Description</span></span> | <span data-ttu-id="3b729-2494">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2494">Example</span></span> | <span data-ttu-id="3b729-2495">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2496">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-2496">query</span></span> |<span data-ttu-id="3b729-2497">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2497">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="3b729-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="3b729-2499">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2500">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2500">Example</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

<span data-ttu-id="3b729-2501">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="3b729-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="3b729-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-2503">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2503">Linked service</span></span>
<span data-ttu-id="3b729-2504">ODBC 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **OnPremisesOdbc**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2504">To define an ODBC linked service, set the **type** of the linked service to **OnPremisesOdbc**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2505">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2505">Property</span></span> | <span data-ttu-id="3b729-2506">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2506">Description</span></span> | <span data-ttu-id="3b729-2507">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-2508">connectionString</span></span> |<span data-ttu-id="3b729-2509">선택적 암호화된 자격 증명 및 연결 문자열의 비 액세스 자격 증명 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2509">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="3b729-2510">다음 섹션의 예제를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="3b729-2510">See examples in the following sections.</span></span> |<span data-ttu-id="3b729-2511">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2511">Yes</span></span> |
| <span data-ttu-id="3b729-2512">자격 증명</span><span class="sxs-lookup"><span data-stu-id="3b729-2512">credential</span></span> |<span data-ttu-id="3b729-2513">드라이버 관련 속성 값 형식에 지정된 연결 문자열의 액세스 자격 증명 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2513">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="3b729-2514">예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="3b729-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="3b729-2515">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2515">No</span></span> |
| <span data-ttu-id="3b729-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2516">authenticationType</span></span> |<span data-ttu-id="3b729-2517">ODBC 데이터 저장소에 연결하는 데 사용되는 인증 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2517">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="3b729-2518">가능한 값은 익명 및 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="3b729-2519">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2519">Yes</span></span> |
| <span data-ttu-id="3b729-2520">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2520">username</span></span> |<span data-ttu-id="3b729-2521">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="3b729-2522">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2522">No</span></span> |
| <span data-ttu-id="3b729-2523">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2523">password</span></span> |<span data-ttu-id="3b729-2524">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2524">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-2525">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2525">No</span></span> |
| <span data-ttu-id="3b729-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2526">gatewayName</span></span> |<span data-ttu-id="3b729-2527">데이터 팩터리 서비스가 ODBC 데이터 저장소에 연결하는 데 사용해야 하는 게이트웨이의 이름.</span><span class="sxs-lookup"><span data-stu-id="3b729-2527">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="3b729-2528">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="3b729-2529">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2529">Example - Using Basic authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="3b729-2530">예제: 암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="3b729-2531">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx)(Azure PowerShell의 1.0 버전 ) cmdlet 또는 [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx)(Azure PowerShell의 0.9 이전 버전)를 사용하여 자격 증명을 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2531">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="3b729-2532">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="3b729-2532">Example: Using Anonymous authentication</span></span>

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="3b729-2533">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-2534">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2534">Dataset</span></span>
<span data-ttu-id="3b729-2535">ODBC 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2535">To define an ODBC dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2536">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2536">Property</span></span> | <span data-ttu-id="3b729-2537">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2537">Description</span></span> | <span data-ttu-id="3b729-2538">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-2539">tableName</span></span> |<span data-ttu-id="3b729-2540">ODBC 데이터 저장소에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2540">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="3b729-2541">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="3b729-2542">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2542">Example</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-2543">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-2544">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2545">ODBC 데이터 저장소에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2545">If you are copying data from an ODBC data store, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2546">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2546">Property</span></span> | <span data-ttu-id="3b729-2547">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2547">Description</span></span> | <span data-ttu-id="3b729-2548">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2548">Allowed values</span></span> | <span data-ttu-id="3b729-2549">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2550">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-2550">query</span></span> |<span data-ttu-id="3b729-2551">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2551">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-2552">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="3b729-2552">SQL query string.</span></span> <span data-ttu-id="3b729-2553">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="3b729-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="3b729-2554">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2555">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2555">Example</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

<span data-ttu-id="3b729-2556">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="3b729-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="3b729-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="3b729-2558">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2558">Linked service</span></span>
<span data-ttu-id="3b729-2559">Salesforce 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **Salesforce**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2559">To define a Salesforce linked service, set the **type** of the linked service to **Salesforce**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2560">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2560">Property</span></span> | <span data-ttu-id="3b729-2561">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2561">Description</span></span> | <span data-ttu-id="3b729-2562">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="3b729-2563">environmentUrl</span></span> | <span data-ttu-id="3b729-2564">Salesforce 인스턴스의 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2564">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="3b729-2565">-기본값은 " https://login.salesforce.com " 입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="3b729-2566">-샌드박스에서 데이터를 복사하려면  " https://test.salesforce.com " 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2566">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="3b729-2567">-사용자 지정 도메인에서 데이터를 복사하려면 예를 들어 "https://[domain].my.salesforce.com"을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2567">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="3b729-2568">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2568">No</span></span> |
| <span data-ttu-id="3b729-2569">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2569">username</span></span> |<span data-ttu-id="3b729-2570">사용자 계정의 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2570">Specify a user name for the user account.</span></span> |<span data-ttu-id="3b729-2571">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2571">Yes</span></span> |
| <span data-ttu-id="3b729-2572">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2572">password</span></span> |<span data-ttu-id="3b729-2573">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2573">Specify a password for the user account.</span></span> |<span data-ttu-id="3b729-2574">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2574">Yes</span></span> |
| <span data-ttu-id="3b729-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="3b729-2575">securityToken</span></span> |<span data-ttu-id="3b729-2576">사용자 계정에 대한 보안 토큰을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2576">Specify a security token for the user account.</span></span> <span data-ttu-id="3b729-2577">보안 토큰을 재설정하거나 가져오는 방법에 대한 자세한 내용은 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="3b729-2578">일반적인 보안 토큰에 대해 자세히 알아보려면 [보안 및 API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2578">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="3b729-2579">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2580">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2580">Example</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

<span data-ttu-id="3b729-2581">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-2582">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2582">Dataset</span></span>
<span data-ttu-id="3b729-2583">Salesforce 데이터 집합을 정의하려면 데이터 집합의 **type**을 **RelationalTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2583">To define a Salesforce dataset, set the **type** of the dataset to **RelationalTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2584">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2584">Property</span></span> | <span data-ttu-id="3b729-2585">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2585">Description</span></span> | <span data-ttu-id="3b729-2586">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="3b729-2587">tableName</span></span> |<span data-ttu-id="3b729-2588">Salesforce에 있는 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2588">Name of the table in Salesforce.</span></span> |<span data-ttu-id="3b729-2589">아니요(**RelationalSource**의 **query**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2590">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2590">Example</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="3b729-2591">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="3b729-2592">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2593">Salesforce에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **RelationalSource**로 설정하고 **source** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2593">If you are copying data from Salesforce, set the **source type** of the copy activity to **RelationalSource**, and specify following properties in the **source** section:</span></span>

| <span data-ttu-id="3b729-2594">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2594">Property</span></span> | <span data-ttu-id="3b729-2595">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2595">Description</span></span> | <span data-ttu-id="3b729-2596">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="3b729-2596">Allowed values</span></span> | <span data-ttu-id="3b729-2597">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3b729-2598">쿼리</span><span class="sxs-lookup"><span data-stu-id="3b729-2598">query</span></span> |<span data-ttu-id="3b729-2599">사용자 지정 쿼리를 사용하여 데이터를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2599">Use the custom query to read data.</span></span> |<span data-ttu-id="3b729-2600">SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="3b729-2601">예제: `select * from MyTable__c`</span><span class="sxs-lookup"><span data-stu-id="3b729-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="3b729-2602">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-2602">No (if the **tableName** of the **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2603">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="3b729-2604">모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2604">The "__c" part of the API Name is needed for any custom object.</span></span>

<span data-ttu-id="3b729-2605">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="3b729-2606">웹 데이터</span><span class="sxs-lookup"><span data-stu-id="3b729-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2607">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2607">Linked service</span></span>
<span data-ttu-id="3b729-2608">웹 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **Web**으로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2608">To define a Web linked service, set the **type** of the linked service to **Web**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2609">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2609">Property</span></span> | <span data-ttu-id="3b729-2610">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2610">Description</span></span> | <span data-ttu-id="3b729-2611">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2612">Url</span><span class="sxs-lookup"><span data-stu-id="3b729-2612">Url</span></span> |<span data-ttu-id="3b729-2613">웹 원본에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2613">URL to the Web source</span></span> |<span data-ttu-id="3b729-2614">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2614">Yes</span></span> |
| <span data-ttu-id="3b729-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="3b729-2615">authenticationType</span></span> |<span data-ttu-id="3b729-2616">익명</span><span class="sxs-lookup"><span data-stu-id="3b729-2616">Anonymous.</span></span> |<span data-ttu-id="3b729-2617">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="3b729-2618">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2618">Example</span></span>


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="3b729-2619">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="3b729-2620">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="3b729-2620">Dataset</span></span>
<span data-ttu-id="3b729-2621">웹 데이터 집합을 정의하려면 데이터 집합의 **type**을 **WebTable**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2621">To define a Web dataset, set the **type** of the dataset to **WebTable**, and specify the following properties in the **typeProperties** section:</span></span> 

| <span data-ttu-id="3b729-2622">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2622">Property</span></span> | <span data-ttu-id="3b729-2623">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2623">Description</span></span> | <span data-ttu-id="3b729-2624">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-2625">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2625">type</span></span> |<span data-ttu-id="3b729-2626">데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2626">type of the dataset.</span></span> <span data-ttu-id="3b729-2627">**데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="3b729-2627">must be set to **WebTable**</span></span> |<span data-ttu-id="3b729-2628">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2628">Yes</span></span> |
| <span data-ttu-id="3b729-2629">path</span><span class="sxs-lookup"><span data-stu-id="3b729-2629">path</span></span> |<span data-ttu-id="3b729-2630">테이블을 포함하는 리소스에 대한 상대 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2630">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="3b729-2631">아니요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2631">No.</span></span> <span data-ttu-id="3b729-2632">경로를 지정하지 않으면 연결된 서비스 정의에 지정된 URL만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2632">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="3b729-2633">index</span><span class="sxs-lookup"><span data-stu-id="3b729-2633">index</span></span> |<span data-ttu-id="3b729-2634">리소스에 있는 테이블의 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2634">The index of the table in the resource.</span></span> <span data-ttu-id="3b729-2635">HTML 페이지에서 테이블의 인덱스를 가져오는 단계는 [HTML 페이지에서 테이블의 인덱스 가져오기](#get-index-of-a-table-in-an-html-page) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="3b729-2636">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="3b729-2637">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2637">Example</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="3b729-2638">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="3b729-2639">복사 활동의 웹 소스</span><span class="sxs-lookup"><span data-stu-id="3b729-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="3b729-2640">웹 테이블에서 데이터를 복사하는 경우 복사 활동의 **source type**을 **WebSource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2640">If you are copying data from a web table, set the **source type** of the copy activity to **WebSource**.</span></span> <span data-ttu-id="3b729-2641">현재 복사 작업의 원본이 **WebSource**형식인 경우 추가 속성이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2641">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="3b729-2642">예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table to an Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

<span data-ttu-id="3b729-2643">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="3b729-2644">계산 환경</span><span class="sxs-lookup"><span data-stu-id="3b729-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="3b729-2645">다음 표에서는 Data Factory에서 지원하는 계산 환경과 이러한 환경에서 실행할 수 있는 변환 활동을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2645">The following table lists the compute environments supported by Data Factory and the transformation activities that can run on them.</span></span> <span data-ttu-id="3b729-2646">관심 있는 계산 링크를 클릭하여 연결된 서비스에서 데이터 팩터리에 연결하기 위한 JSON 스키마를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2646">Click the link for the compute you are interested in to see the JSON schemas for linked service to link it to a data factory.</span></span> 

| <span data-ttu-id="3b729-2647">컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="3b729-2647">Compute environment</span></span> | <span data-ttu-id="3b729-2648">활동</span><span class="sxs-lookup"><span data-stu-id="3b729-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="3b729-2649">[주문형 HDInsight 클러스터](#on-demand-azure-hdinsight-cluster) 또는 [사용자 고유의 HDInsight 클러스터](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="3b729-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="3b729-2650">[.NET 사용자 지정 활동](#net-custom-activity), [Hive 활동](#hdinsight-hive-activity), [Pig 활동](#hdinsight-pig-activity), [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 활동](#hdinsight-streaming-activityd), [Spark 활동](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="3b729-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="3b729-2651">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="3b729-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="3b729-2652">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="3b729-2653">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="3b729-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="3b729-2654">[Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity), [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="3b729-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="3b729-2655">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="3b729-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="3b729-2656">데이터 레이크 분석 U-SQL</span><span class="sxs-lookup"><span data-stu-id="3b729-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="3b729-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="3b729-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="3b729-2658">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="3b729-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="3b729-2659">주문형 Azure HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="3b729-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="3b729-2660">Azure 데이터 팩터리 서비스는 데이터를 처리하는 Windows/Linux 기반 주문형 HDInsight 클러스터를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2660">The Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster to process data.</span></span> <span data-ttu-id="3b729-2661">클러스터는 클러스터와 연결된 저장소 계정(JSON에서 linkedServiceName 속성)과 동일한 하위 지역에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2661">The cluster is created in the same region as the storage account (linkedServiceName property in the JSON) associated with the cluster.</span></span> <span data-ttu-id="3b729-2662">이 연결된 서비스에서는 변환 활동, 즉 [.NET 사용자 지정 활동](#net-custom-activity), [Hive 활동](#hdinsight-hive-activity), [Pig 활동](#hdinsight-pig-activity), [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 활동](#hdinsight-streaming-activityd), [Spark 활동](#hdinsight-spark-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2662">You can run the following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2663">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2663">Linked service</span></span> 
<span data-ttu-id="3b729-2664">다음 표에서는 주문형 HDInsight 연결된 서비스의 Azure JSON 정의에 사용된 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2664">The following table provides descriptions for the properties used in the Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="3b729-2665">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2665">Property</span></span> | <span data-ttu-id="3b729-2666">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2666">Description</span></span> | <span data-ttu-id="3b729-2667">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2668">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2668">type</span></span> |<span data-ttu-id="3b729-2669">형식 속성은 **HDInsightOnDemand**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2669">The type property should be set to **HDInsightOnDemand**.</span></span> |<span data-ttu-id="3b729-2670">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2670">Yes</span></span> |
| <span data-ttu-id="3b729-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="3b729-2671">clusterSize</span></span> |<span data-ttu-id="3b729-2672">클러스터의 작업자/데이터 노드 수</span><span class="sxs-lookup"><span data-stu-id="3b729-2672">Number of worker/data nodes in the cluster.</span></span> <span data-ttu-id="3b729-2673">HDInsight 클러스터는 속성에 지정한 작업자 노드의 수와 함께 2개의 헤드 노드로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2673">The HDInsight cluster is created with 2 head nodes along with the number of worker nodes you specify for this property.</span></span> <span data-ttu-id="3b729-2674">노드의 크기는 4개 코어를 포함한 Standard_D3이므로, 4개 작업자 노드 클러스터에서 24개 코어(작업자 노드용 4\*4 = 16코어 및 헤드 노드용 2\*4 = 8코어)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2674">The nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="3b729-2675">Standard_D3 계층에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about the Standard_D3 tier.</span></span> |<span data-ttu-id="3b729-2676">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2676">Yes</span></span> |
| <span data-ttu-id="3b729-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="3b729-2677">timetolive</span></span> |<span data-ttu-id="3b729-2678">주문형 HDInsight 클러스터에 대한 허용된 유휴 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2678">The allowed idle time for the on-demand HDInsight cluster.</span></span> <span data-ttu-id="3b729-2679">클러스터에 다른 활성 작업이 없으면 작업이 완료된 후에 주문형 HDInsight 클러스터가 유지될 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2679">Specifies how long the on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in the cluster.</span></span><br/><br/><span data-ttu-id="3b729-2680">예를 들어 활동 실행에 6분이 걸리고 timetolive이 5분으로 설정된 경우 클러스터는 활동을 처리하는 6분 동안 실행된 후에 5분 동안 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2680">For example, if an activity run takes 6 minutes and timetolive is set to 5 minutes, the cluster stays alive for 5 minutes after the 6 minutes of processing the activity run.</span></span> <span data-ttu-id="3b729-2681">다른 활동 실행이 6분 창을 실행하는 경우 동일한 클러스터에 의해 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2681">If another activity run is executed with the 6 minutes window, it is processed by the same cluster.</span></span><br/><br/><span data-ttu-id="3b729-2682">주문형 HDInsight 클러스터를 만드는 데는 많은 시간이 걸려 값 비싼 작업이 되므로 필요할 때마다 이 설정을 사용하여 주문형 HDInsight 클러스터를 다시 사용함으로써 데이터 팩터리의 성능을 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed to improve performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="3b729-2683">timetolive 값을 0으로 설정한 경우 클러스터는 활동이 처리되는 즉시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2683">If you set timetolive value to 0, the cluster is deleted as soon as the activity run in processed.</span></span> <span data-ttu-id="3b729-2684">반면 높은 값을 설정하는 경우 클러스터는 불필요하게 많은 비용이 발생하는 유휴 상태에 머무를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2684">On the other hand, if you set a high value, the cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="3b729-2685">따라서 필요에 따라 적절한 값을 설정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2685">Therefore, it is important that you set the appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="3b729-2686">timetolive 속성 값이 적절하게 설정되는 경우 여러 파이프라인은 주문형 HDInsight 클러스터의 동일한 인스턴스를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2686">Multiple pipelines can share the same instance of the on-demand HDInsight cluster if the timetolive property value is appropriately set</span></span> |<span data-ttu-id="3b729-2687">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2687">Yes</span></span> |
| <span data-ttu-id="3b729-2688">버전</span><span class="sxs-lookup"><span data-stu-id="3b729-2688">version</span></span> |<span data-ttu-id="3b729-2689">HDInsight 클러스터의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2689">Version of the HDInsight cluster.</span></span> <span data-ttu-id="3b729-2690">자세한 내용은 [Azure Data Factory에서 지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="3b729-2691">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2691">No</span></span> |
| <span data-ttu-id="3b729-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3b729-2692">linkedServiceName</span></span> |<span data-ttu-id="3b729-2693">데이터를 저장 및 처리하기 위해 주문형 클러스터에서 사용하는 Azure Storage 연결 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2693">Azure Storage linked service to be used by the on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="3b729-2694">현재 Azure Data Lake Store를 저장소로 사용하는 주문형 HDInsight 클러스터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as the storage.</span></span> <span data-ttu-id="3b729-2695">HDInsight 처리의 결과 데이터를 Azure Data Lake Store에 저장하려면 복사 작업을 사용하여 Azure Blob Storage의 데이터를 Azure Data Lake Store로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2695">If you want to store the result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity to copy the data from the Azure Blob Storage to the Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="3b729-2696">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2696">Yes</span></span> |
| <span data-ttu-id="3b729-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="3b729-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="3b729-2698">HDInsight 연결된 서비스에 대한 추가 저장소 계정을 지정하므로 데이터 팩터리 서비스가 사용자를 대신해 계정을 등록할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="3b729-2698">Specifies additional storage accounts for the HDInsight linked service so that the Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="3b729-2699">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2699">No</span></span> |
| <span data-ttu-id="3b729-2700">osType</span><span class="sxs-lookup"><span data-stu-id="3b729-2700">osType</span></span> |<span data-ttu-id="3b729-2701">운영 체제 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2701">Type of operating system.</span></span> <span data-ttu-id="3b729-2702">허용되는 값은 Windows(기본값) 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="3b729-2703">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2703">No</span></span> |
| <span data-ttu-id="3b729-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3b729-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="3b729-2705">HCatalog 데이터베이스를 가리키는 Azure SQL 연결된 서비스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2705">The name of Azure SQL linked service that point to the HCatalog database.</span></span> <span data-ttu-id="3b729-2706">주문형 HDInsight 클러스터는 Azure SQL Database를 metastore로 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2706">The on-demand HDInsight cluster is created by using the Azure SQL database as the metastore.</span></span> |<span data-ttu-id="3b729-2707">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="3b729-2708">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2708">JSON example</span></span>
<span data-ttu-id="3b729-2709">다음 JSON는 Linux 기반 주문형 HDInsight 연결된 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2709">The following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="3b729-2710">Data Factory 서비스는 데이터 조각을 처리하는 경우 **Linux 기반** HDInsight 클러스터를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2710">The Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

<span data-ttu-id="3b729-2711">자세한 내용은 [계산 연결된 서비스](data-factory-compute-linked-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="3b729-2712">기존 Azure HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="3b729-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="3b729-2713">Azure HDInsight 연결된 서비스를 만들어서 데이터 팩터리를 사용하는 사용자 고유의 HDInsight 클러스터를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2713">You can create an Azure HDInsight linked service to register your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="3b729-2714">이 연결된 서비스에서는 데이터 변환 활동, 즉 [.NET 사용자 지정 활동](#net-custom-activity), [Hive 활동](#hdinsight-hive-activity), [Pig 활동](#hdinsight-pig-activity), [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 활동](#hdinsight-streaming-activityd), [Spark 활동](#hdinsight-spark-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2714">You can run the following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2715">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2715">Linked service</span></span>
<span data-ttu-id="3b729-2716">다음 표에서는 Azure HDInsight 연결된 서비스의 Azure JSON 정의에 사용된 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2716">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="3b729-2717">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2717">Property</span></span> | <span data-ttu-id="3b729-2718">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2718">Description</span></span> | <span data-ttu-id="3b729-2719">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2720">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2720">type</span></span> |<span data-ttu-id="3b729-2721">형식 속성은 **HDInsight**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2721">The type property should be set to **HDInsight**.</span></span> |<span data-ttu-id="3b729-2722">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2722">Yes</span></span> |
| <span data-ttu-id="3b729-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="3b729-2723">clusterUri</span></span> |<span data-ttu-id="3b729-2724">HDInsight 클러스터의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2724">The URI of the HDInsight cluster.</span></span> |<span data-ttu-id="3b729-2725">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2725">Yes</span></span> |
| <span data-ttu-id="3b729-2726">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2726">username</span></span> |<span data-ttu-id="3b729-2727">기존 HDInsight 클러스터에 연결하는데 사용할 사용자의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2727">Specify the name of the user to be used to connect to an existing HDInsight cluster.</span></span> |<span data-ttu-id="3b729-2728">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2728">Yes</span></span> |
| <span data-ttu-id="3b729-2729">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2729">password</span></span> |<span data-ttu-id="3b729-2730">사용자 계정으로 password를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2730">Specify password for the user account.</span></span> |<span data-ttu-id="3b729-2731">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2731">Yes</span></span> |
| <span data-ttu-id="3b729-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3b729-2732">linkedServiceName</span></span> | <span data-ttu-id="3b729-2733">HDInsight 클러스터에서 사용하는 Azure Blob Storage를 참조하는 Azure Storage 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2733">Name of the Azure Storage linked service that refers to the Azure blob storage used by the HDInsight cluster.</span></span> <p><span data-ttu-id="3b729-2734">현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="3b729-2735">HDInsight 클러스터가 Data Lake Store에 액세스할 경우 Hive/Pig 스크립트의 Azure Data Lake Store에 있는 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2735">You may access data in the Azure Data Lake Store from Hive/Pig scripts if the HDInsight cluster has access to the Data Lake Store.</span></span> </p>  |<span data-ttu-id="3b729-2736">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2736">Yes</span></span> |

<span data-ttu-id="3b729-2737">지원되는 HDInsight 클러스터 버전은 [지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="3b729-2738">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2738">JSON example</span></span>

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a><span data-ttu-id="3b729-2739">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="3b729-2739">Azure Batch</span></span>
<span data-ttu-id="3b729-2740">Azure 배치 연결된 서비스를 만들어 데이터 팩터리에 가상 컴퓨터(VM)의 배치 풀을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2740">You can create an Azure Batch linked service to register a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="3b729-2741">Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="3b729-2742">이 연결된 서비스에서 [.NET 사용자 지정 활동](#net-custom-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2743">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2743">Linked service</span></span>
<span data-ttu-id="3b729-2744">다음 표에서는 Azure 배치 연결된 서비스의 Azure JSON 정의에 사용된 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2744">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="3b729-2745">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2745">Property</span></span> | <span data-ttu-id="3b729-2746">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2746">Description</span></span> | <span data-ttu-id="3b729-2747">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2748">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2748">type</span></span> |<span data-ttu-id="3b729-2749">형식 속성은 **AzureBatch**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2749">The type property should be set to **AzureBatch**.</span></span> |<span data-ttu-id="3b729-2750">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2750">Yes</span></span> |
| <span data-ttu-id="3b729-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="3b729-2751">accountName</span></span> |<span data-ttu-id="3b729-2752">Azure Batch 계정의 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-2752">Name of the Azure Batch account.</span></span> |<span data-ttu-id="3b729-2753">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2753">Yes</span></span> |
| <span data-ttu-id="3b729-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="3b729-2754">accessKey</span></span> |<span data-ttu-id="3b729-2755">Azure Batch 계정에 대한 선택키</span><span class="sxs-lookup"><span data-stu-id="3b729-2755">Access key for the Azure Batch account.</span></span> |<span data-ttu-id="3b729-2756">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2756">Yes</span></span> |
| <span data-ttu-id="3b729-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="3b729-2757">poolName</span></span> |<span data-ttu-id="3b729-2758">가상 컴퓨터의 풀 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2758">Name of the pool of virtual machines.</span></span> |<span data-ttu-id="3b729-2759">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2759">Yes</span></span> |
| <span data-ttu-id="3b729-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="3b729-2760">linkedServiceName</span></span> |<span data-ttu-id="3b729-2761">Azure 일괄 처리 연결된 서비스와 관련된 Azure 저장소 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2761">Name of the Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="3b729-2762">이 연결된 서비스는 활동을 실행하는 데 필요한 파일을 스테이징하고 활동 실행 로그를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2762">This linked service is used for staging files required to run the activity and storing the activity execution logs.</span></span> |<span data-ttu-id="3b729-2763">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="3b729-2764">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2764">JSON example</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a><span data-ttu-id="3b729-2765">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="3b729-2765">Azure Machine Learning</span></span>
<span data-ttu-id="3b729-2766">Azure Machine Learning 연결된 서비스를 만들어 데이터 팩터리에 Machine Learning 배치 점수 매기기 끝점을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2766">You create an Azure Machine Learning linked service to register a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="3b729-2767">이 연결된 서비스에서는 두 가지 데이터 변환 활동, 즉 [Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity)과, [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2768">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2768">Linked service</span></span>
<span data-ttu-id="3b729-2769">다음 표에서는 Azure Machine Learning 연결된 서비스의 Azure JSON 정의에 사용된 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2769">The following table provides descriptions for the properties used in the Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="3b729-2770">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2770">Property</span></span> | <span data-ttu-id="3b729-2771">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2771">Description</span></span> | <span data-ttu-id="3b729-2772">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2773">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2773">Type</span></span> |<span data-ttu-id="3b729-2774">형식 속성은 **AzureML**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2774">The type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="3b729-2775">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2775">Yes</span></span> |
| <span data-ttu-id="3b729-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="3b729-2776">mlEndpoint</span></span> |<span data-ttu-id="3b729-2777">일괄 처리 점수 매기기 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2777">The batch scoring URL.</span></span> |<span data-ttu-id="3b729-2778">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2778">Yes</span></span> |
| <span data-ttu-id="3b729-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="3b729-2779">apiKey</span></span> |<span data-ttu-id="3b729-2780">게시된 작업 영역 모델의 API입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2780">The published workspace model’s API.</span></span> |<span data-ttu-id="3b729-2781">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="3b729-2782">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2782">JSON example</span></span>

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="3b729-2783">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="3b729-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="3b729-2784">파이프 라인에서 **데이터 레이크 분석 U-SQL 작업** 을 사용하기 전에 Azure 데이터 레이크 분석 계산 서비스와 Azure Data Factory에 연결하는 [Azure 데이터 레이크 분석](data-factory-usql-activity.md) 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2784">You create an **Azure Data Lake Analytics** linked service to link an Azure Data Lake Analytics compute service to an Azure data factory before using the [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="3b729-2785">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2785">Linked service</span></span>

<span data-ttu-id="3b729-2786">다음 표에서는 Azure Data Lake Analytics 연결된 서비스의 JSON 정의에 사용된 속성에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2786">The following table provides descriptions for the properties used in the JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="3b729-2787">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2787">Property</span></span> | <span data-ttu-id="3b729-2788">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2788">Description</span></span> | <span data-ttu-id="3b729-2789">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2790">형식</span><span class="sxs-lookup"><span data-stu-id="3b729-2790">Type</span></span> |<span data-ttu-id="3b729-2791">type 속성은 **AzureDataLakeAnalytics**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2791">The type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="3b729-2792">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2792">Yes</span></span> |
| <span data-ttu-id="3b729-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="3b729-2793">accountName</span></span> |<span data-ttu-id="3b729-2794">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="3b729-2795">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2795">Yes</span></span> |
| <span data-ttu-id="3b729-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="3b729-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="3b729-2797">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="3b729-2798">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2798">No</span></span> |
| <span data-ttu-id="3b729-2799">권한 부여</span><span class="sxs-lookup"><span data-stu-id="3b729-2799">authorization</span></span> |<span data-ttu-id="3b729-2800">Data Factory 편집기에서 **권한 부여** 단추를 클릭하고 OAuth 로그인을 완료하면 인증 코드가 자동으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2800">Authorization code is automatically retrieved after clicking **Authorize** button in the Data Factory Editor and completing the OAuth login.</span></span> |<span data-ttu-id="3b729-2801">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2801">Yes</span></span> |
| <span data-ttu-id="3b729-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="3b729-2802">subscriptionId</span></span> |<span data-ttu-id="3b729-2803">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="3b729-2803">Azure subscription id</span></span> |<span data-ttu-id="3b729-2804">아니요(지정하지 않으면 Data Factory의 구독이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="3b729-2804">No (If not specified, subscription of the data factory is used).</span></span> |
| <span data-ttu-id="3b729-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="3b729-2805">resourceGroupName</span></span> |<span data-ttu-id="3b729-2806">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="3b729-2806">Azure resource group name</span></span> |<span data-ttu-id="3b729-2807">아니요(지정하지 않으면 Data Factory의 리소스 그룹이 사용됨).</span><span class="sxs-lookup"><span data-stu-id="3b729-2807">No (If not specified, resource group of the data factory is used).</span></span> |
| <span data-ttu-id="3b729-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="3b729-2808">sessionId</span></span> |<span data-ttu-id="3b729-2809">OAuth 권한 부여 세션의 세션 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2809">session id from the OAuth authorization session.</span></span> <span data-ttu-id="3b729-2810">각 세션 ID는 고유하고 한 번만 사용될 수 있으며 </span><span class="sxs-lookup"><span data-stu-id="3b729-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="3b729-2811">Data Factory 편집기를 사용하면 이 ID가 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2811">When you use the Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="3b729-2812">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="3b729-2813">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2813">JSON example</span></span>
<span data-ttu-id="3b729-2814">다음 예제에서는 Azure 데이터 레이크 분석 연결된 서비스에 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2814">The following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a><span data-ttu-id="3b729-2815">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3b729-2815">Azure SQL Database</span></span>
<span data-ttu-id="3b729-2816">Azure SQL 연결된 서비스를 만들고 [저장 프로시저 활동](#stored-procedure-activity) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2816">You create an Azure SQL linked service and use it with the [Stored Procedure Activity](#stored-procedure-activity) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2817">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2817">Linked service</span></span>
<span data-ttu-id="3b729-2818">Azure SQL Database 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureSqlDatabase**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2818">To define an Azure SQL Database linked service, set the **type** of the linked service to **AzureSqlDatabase**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2819">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2819">Property</span></span> | <span data-ttu-id="3b729-2820">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2820">Description</span></span> | <span data-ttu-id="3b729-2821">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-2822">connectionString</span></span> |<span data-ttu-id="3b729-2823">connectionString 속성에 대한 Azure SQL 데이터베이스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2823">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> |<span data-ttu-id="3b729-2824">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="3b729-2825">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2825">JSON example</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="3b729-2826">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="3b729-2827">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="3b729-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="3b729-2828">Azure SQL 데이터 웨어하우스 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2828">You create an Azure SQL Data Warehouse linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2829">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2829">Linked service</span></span>
<span data-ttu-id="3b729-2830">Azure SQL Data Warehouse 연결된 서비스를 정의하려면 연결된 서비스의 **type**을 **AzureSqlDW**로 설정하고 **typeProperties** 섹션에서 다음 속성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2830">To define an Azure SQL Data Warehouse linked service, set the **type** of the linked service to **AzureSqlDW**, and specify following properties in the **typeProperties** section:</span></span>  

| <span data-ttu-id="3b729-2831">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2831">Property</span></span> | <span data-ttu-id="3b729-2832">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2832">Description</span></span> | <span data-ttu-id="3b729-2833">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-2834">connectionString</span></span> |<span data-ttu-id="3b729-2835">connectionString 속성에 대한 Azure SQL 데이터 웨어하우스 인스턴스에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2835">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> |<span data-ttu-id="3b729-2836">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="3b729-2837">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2837">JSON example</span></span>

```json
{
    "name": "AzureSqlDWLinkedService",
    "properties": {
        "type": "AzureSqlDW",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

<span data-ttu-id="3b729-2838">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="3b729-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3b729-2839">SQL Server</span></span> 
<span data-ttu-id="3b729-2840">SQL Server 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2840">You create a SQL Server linked service and use it with the [Stored Procedure Activity](data-factory-stored-proc-activity.md) to invoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="3b729-2841">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="3b729-2841">Linked service</span></span>
<span data-ttu-id="3b729-2842">**OnPremisesSqlServer** 형식의 연결된 서비스를 만들어 온-프레미스 SQL Server 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2842">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="3b729-2843">다음 테이블은 온-프레미스 SQL Server 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2843">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="3b729-2844">다음 표에서는 SQL Server 연결된 서비스와 관련된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2844">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="3b729-2845">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2845">Property</span></span> | <span data-ttu-id="3b729-2846">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2846">Description</span></span> | <span data-ttu-id="3b729-2847">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2848">type</span><span class="sxs-lookup"><span data-stu-id="3b729-2848">type</span></span> |<span data-ttu-id="3b729-2849">type 속성은 **OnPremisesSqlServer**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2849">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="3b729-2850">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2850">Yes</span></span> |
| <span data-ttu-id="3b729-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="3b729-2851">connectionString</span></span> |<span data-ttu-id="3b729-2852">SQL 인증 또는 Windows 인증을 사용하여 온-프레미스 SQL Server 데이터베이스에 연결하는 데 필요한 connectionString 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2852">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="3b729-2853">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2853">Yes</span></span> |
| <span data-ttu-id="3b729-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="3b729-2854">gatewayName</span></span> |<span data-ttu-id="3b729-2855">데이터 팩터리 서비스가 온-프레미스 SQL Server 데이터베이스에 연결하는 데 사용해야 하는 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2855">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="3b729-2856">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2856">Yes</span></span> |
| <span data-ttu-id="3b729-2857">username</span><span class="sxs-lookup"><span data-stu-id="3b729-2857">username</span></span> |<span data-ttu-id="3b729-2858">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="3b729-2859">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="3b729-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="3b729-2860">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2860">No</span></span> |
| <span data-ttu-id="3b729-2861">password</span><span class="sxs-lookup"><span data-stu-id="3b729-2861">password</span></span> |<span data-ttu-id="3b729-2862">사용자 이름에 지정한 사용자 계정의 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2862">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="3b729-2863">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2863">No</span></span> |

<span data-ttu-id="3b729-2864">**New-AzureRmDataFactoryEncryptValue** cmdlet를 사용하여 자격 증명을 암호화하고 다음 예제와 같이 연결 문자열에 해당 자격 증명을 사용할 수 있습니다(**EncryptedCredential** 속성).</span><span class="sxs-lookup"><span data-stu-id="3b729-2864">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="3b729-2865">예제: SQL 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="3b729-2865">Example: JSON for using SQL Authentication</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="3b729-2866">예제: Windows 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="3b729-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="3b729-2867">사용자 이름 및 암호가 지정된 경우 게이트웨이는 이러한 정보를 사용해 지정된 사용자 계정을 가장하여 온-프레미스 SQL Server Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2867">If username and password are specified, gateway uses them to impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> <span data-ttu-id="3b729-2868">그렇지 않은 경우 게이트웨이는 게이트웨이의 보안 컨텍스트(시작 계정)를 사용하여 SQL Server에 직접 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2868">Otherwise, gateway connects to the SQL Server directly with the security context of Gateway (its startup account).</span></span>

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="3b729-2869">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="3b729-2870">데이터 변환 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="3b729-2871">작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2871">Activity</span></span> | <span data-ttu-id="3b729-2872">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="3b729-2873">HDInsight Hive 활동</span><span class="sxs-lookup"><span data-stu-id="3b729-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="3b729-2874">Data Factory 파이프라인에서 HDInsight Hive 작업은 사용자 고유 또는 주문형 Windows/Linux 기반 HDInsight 클러스터의 Hive 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2874">The HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="3b729-2875">HDInsight Pig 활동</span><span class="sxs-lookup"><span data-stu-id="3b729-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="3b729-2876">Data Factory 파이프라인에서 HDInsight Pig 작업은 사용자 고유 또는 주문형 Windows/Linux 기반 HDInsight 클러스터의 Pig 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2876">The HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="3b729-2877">HDInsight MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="3b729-2878">Data Factory 파이프라인의 HDInsight MapReduce 작업은 사용자 고유 또는 주문형 Windows/Linux 기반 HDInsight 클러스터에서 MapReduce 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2878">The HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="3b729-2879">HDInsight 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="3b729-2880">Data Factory 파이프라인의 HDInsight 스트리밍 작업은 사용자 고유 또는 주문형 Windows/Linux 기반 HDInsight 클러스터에서 Hadoop 스트리밍 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2880">The HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="3b729-2881">HDInsight Spark 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="3b729-2882">Data Factory 파이프라인에서 HDInsight Spark 작업은 사용자 고유 HDInsight 클러스터에서 Spark 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2882">The HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="3b729-2883">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="3b729-2884">Azure Data Factory를 사용하면 예측 분석을 위해 게시된 Azure Machine Learning 웹 서비스를 사용하는 파이프라인을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2884">Azure Data Factory enables you to easily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="3b729-2885">Azure Data Factory 파이프라인에서 배치 실행 활동을 사용하면 Machine Learning 웹 서비스를 호출하여 데이터를 일괄적으로 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2885">Using the Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service to make predictions on the data in batch.</span></span> 
[<span data-ttu-id="3b729-2886">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="3b729-2887">시간이 지남에 따라 Machine Learning 점수 매기기 실험의 예측 모델은 새 입력 데이터 집합을 사용하여 다시 학습되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2887">Over time, the predictive models in the Machine Learning scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="3b729-2888">재학습으로 완료한 후에는 재학습한 Machine Learning 모델로 점수 매기기 웹 서비스를 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2888">After you are done with retraining, you want to update the scoring web service with the retrained Machine Learning model.</span></span> <span data-ttu-id="3b729-2889">업데이트 리소스 활동을 사용하여 새로 학습된 모델로 웹 서비스를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2889">You can use the Update Resource Activity to update the web service with the newly trained model.</span></span>
[<span data-ttu-id="3b729-2890">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="3b729-2891">Data Factory 파이프라인에서 저장 프로시저 활동을 사용하여 엔터프라이즈 또는 Azure VM에 있는 Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database 데이터 저장소 중 하나에서 저장 프로시저를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2891">You can use the Stored Procedure activity in a Data Factory pipeline to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="3b729-2892">Data Lake Analytics U-SQL 활동</span><span class="sxs-lookup"><span data-stu-id="3b729-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="3b729-2893">Data Lake Analytics U-SQL 작업은 Azure Data Lake Analytics 클러스터에 대해 U-SQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="3b729-2894">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="3b729-2895">Data Factory에서 지원되지 않는 방식으로 데이터를 변환해야 하는 경우 고유의 데이터 이동 논리가 포함된 사용자 지정 작업을 만들어서 파이프라인에 해당 작업을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2895">If you need to transform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use the activity in the pipeline.</span></span> <span data-ttu-id="3b729-2896">Azure 배치 서비스 또는 Azure HDInsight 클러스터를 사용하여 실행되도록 사용자 지정 .NET 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2896">You can configure the custom .NET activity to run using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="3b729-2897">HDInsight Hive 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="3b729-2898">Hive 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2898">You can specify the following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="3b729-2899">활동의 type 속성은 **HDInsightHive**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2899">The type property for the activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="3b729-2900">먼저 HDInsight 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2900">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-2901">활동의 type을 HDInsightHive로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2901">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightHive:</span></span>

| <span data-ttu-id="3b729-2902">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2902">Property</span></span> | <span data-ttu-id="3b729-2903">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2903">Description</span></span> | <span data-ttu-id="3b729-2904">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2905">script</span><span class="sxs-lookup"><span data-stu-id="3b729-2905">script</span></span> |<span data-ttu-id="3b729-2906">Hive 스크립트 인라인 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2906">Specify the Hive script inline</span></span> |<span data-ttu-id="3b729-2907">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2907">No</span></span> |
| <span data-ttu-id="3b729-2908">script path</span><span class="sxs-lookup"><span data-stu-id="3b729-2908">script path</span></span> |<span data-ttu-id="3b729-2909">Hive 스크립트를 Azure blob 저장소에 저장하고 파일에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2909">Store the Hive script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="3b729-2910">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="3b729-2911">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2911">Both cannot be used together.</span></span> <span data-ttu-id="3b729-2912">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2912">The file name is case-sensitive.</span></span> |<span data-ttu-id="3b729-2913">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2913">No</span></span> |
| <span data-ttu-id="3b729-2914">defines</span><span class="sxs-lookup"><span data-stu-id="3b729-2914">defines</span></span> |<span data-ttu-id="3b729-2915">'hiveconf'를 사용하는 Hive 스크립트 내에서 참조하기 위해 매개 변수를 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2915">Specify parameters as key/value pairs for referencing within the Hive script using 'hiveconf'</span></span> |<span data-ttu-id="3b729-2916">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2916">No</span></span> |

<span data-ttu-id="3b729-2917">이러한 type 속성은 Hive 활동에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2917">These type properties are specific to the Hive Activity.</span></span> <span data-ttu-id="3b729-2918">typeProperties 섹션 외부의 다른 속성은 모든 활동에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2918">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="3b729-2919">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2919">JSON example</span></span>
<span data-ttu-id="3b729-2920">다음 JSON은 파이프라인에서 HDInsight Hive 활동을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2920">The following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

```json
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

<span data-ttu-id="3b729-2921">자세한 내용은 [Hive 활동](data-factory-hive-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="3b729-2922">HDInsight Pig 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="3b729-2923">Pig 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2923">You can specify the following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="3b729-2924">활동의 type 속성은 **HDInsightPig**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2924">The type property for the activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="3b729-2925">먼저 HDInsight 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2925">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-2926">활동의 type을 HDInsightPig로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2926">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightPig:</span></span> 

| <span data-ttu-id="3b729-2927">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2927">Property</span></span> | <span data-ttu-id="3b729-2928">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2928">Description</span></span> | <span data-ttu-id="3b729-2929">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2930">script</span><span class="sxs-lookup"><span data-stu-id="3b729-2930">script</span></span> |<span data-ttu-id="3b729-2931">Pig 스크립트 인라인 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2931">Specify the Pig script inline</span></span> |<span data-ttu-id="3b729-2932">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2932">No</span></span> |
| <span data-ttu-id="3b729-2933">script path</span><span class="sxs-lookup"><span data-stu-id="3b729-2933">script path</span></span> |<span data-ttu-id="3b729-2934">Pig 스크립트를 Azure blob 저장소에 저장하고 파일에 대한 경로를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2934">Store the Pig script in an Azure blob storage and provide the path to the file.</span></span> <span data-ttu-id="3b729-2935">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="3b729-2936">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2936">Both cannot be used together.</span></span> <span data-ttu-id="3b729-2937">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2937">The file name is case-sensitive.</span></span> |<span data-ttu-id="3b729-2938">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2938">No</span></span> |
| <span data-ttu-id="3b729-2939">defines</span><span class="sxs-lookup"><span data-stu-id="3b729-2939">defines</span></span> |<span data-ttu-id="3b729-2940">Pig 스크립트 내에서 참조하기 위해 매개 변수를 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="3b729-2940">Specify parameters as key/value pairs for referencing within the Pig script</span></span> |<span data-ttu-id="3b729-2941">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2941">No</span></span> |

<span data-ttu-id="3b729-2942">이러한 type 속성은 Pig 활동에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2942">These type properties are specific to the Pig Activity.</span></span> <span data-ttu-id="3b729-2943">typeProperties 섹션 외부의 다른 속성은 모든 활동에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2943">Other properties (outside the typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="3b729-2944">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2944">JSON example</span></span>

```json
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

<span data-ttu-id="3b729-2945">자세한 내용은 [Pig 활동](#data-factory-pig-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="3b729-2946">HDInsight MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="3b729-2947">MapReduce 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2947">You can specify the following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="3b729-2948">활동의 type 속성은 **HDInsightMapReduce**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2948">The type property for the activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="3b729-2949">먼저 HDInsight 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2949">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-2950">활동의 type을 HDInsightMapReduce로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2950">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightMapReduce:</span></span> 

| <span data-ttu-id="3b729-2951">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2951">Property</span></span> | <span data-ttu-id="3b729-2952">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2952">Description</span></span> | <span data-ttu-id="3b729-2953">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="3b729-2954">jarLinkedService</span></span> | <span data-ttu-id="3b729-2955">JAR 파일이 포함된 Azure Storage에 대한 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2955">Name of the linked service for the Azure Storage that contains the JAR file.</span></span> | <span data-ttu-id="3b729-2956">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2956">Yes</span></span> |
| <span data-ttu-id="3b729-2957">jarFilePath </span><span class="sxs-lookup"><span data-stu-id="3b729-2957">jarFilePath</span></span> | <span data-ttu-id="3b729-2958">Azure Storage의 JAR 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2958">Path to the JAR file in the Azure Storage.</span></span> | <span data-ttu-id="3b729-2959">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2959">Yes</span></span> | 
| <span data-ttu-id="3b729-2960">className</span><span class="sxs-lookup"><span data-stu-id="3b729-2960">className</span></span> | <span data-ttu-id="3b729-2961">JAR 파일의 주 클래스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2961">Name of the main class in the JAR file.</span></span> | <span data-ttu-id="3b729-2962">예</span><span class="sxs-lookup"><span data-stu-id="3b729-2962">Yes</span></span> | 
| <span data-ttu-id="3b729-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="3b729-2963">arguments</span></span> | <span data-ttu-id="3b729-2964">MapReduce 프로그램에 대해 쉼표로 구분된 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2964">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="3b729-2965">런타임에 MapReduce 프레임워크의 몇 개 인수(예: mapreduce.job.tags)가 추가로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="3b729-2966">MapReduce 인수로 사용자 인수를 구분하려면 다음 예제와 같이 인수로 옵션과 값을 모두 사용하는 것이 좋습니다(-s, --input, --output 등은 바로 뒤에 해당 값이 있는 옵션임).</span><span class="sxs-lookup"><span data-stu-id="3b729-2966">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="3b729-2967">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="3b729-2968">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline to Run a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix to determine the similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
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
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="3b729-2969">자세한 내용은 [MapReduce 활동](data-factory-map-reduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="3b729-2970">HDInsight 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="3b729-2971">Hadoop 스트리밍 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2971">You can specify the following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="3b729-2972">활동의 type 속성은 **HDInsightStreaming**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2972">The type property for the activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="3b729-2973">먼저 HDInsight 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2973">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-2974">활동의 type을 HDInsightStreaming으로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2974">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightStreaming:</span></span> 

| <span data-ttu-id="3b729-2975">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-2975">Property</span></span> | <span data-ttu-id="3b729-2976">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="3b729-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="3b729-2977">mapper</span></span> | <span data-ttu-id="3b729-2978">매퍼 실행 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2978">Name of the mapper executable.</span></span> <span data-ttu-id="3b729-2979">예제에서는 cat.exe가 매퍼 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2979">In the example, cat.exe is the mapper executable.</span></span>| 
| <span data-ttu-id="3b729-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="3b729-2980">reducer</span></span> | <span data-ttu-id="3b729-2981">리듀서 실행 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2981">Name of the reducer executable.</span></span> <span data-ttu-id="3b729-2982">예제에서는 wc.exe가 리듀서 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2982">In the example, wc.exe is the reducer executable.</span></span> | 
| <span data-ttu-id="3b729-2983">input</span><span class="sxs-lookup"><span data-stu-id="3b729-2983">input</span></span> | <span data-ttu-id="3b729-2984">매퍼의 입력 파일(위치 포함)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2984">Input file (including location) for the mapper.</span></span> <span data-ttu-id="3b729-2985">예제의 "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt"에서 adfsample은 BLOB 컨테이너이고 example/data/Gutenberg는 폴더이며 davinci.txt는 BOLB입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2985">In the example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is the blob container, example/data/Gutenberg is the folder, and davinci.txt is the blob.</span></span> |
| <span data-ttu-id="3b729-2986">output</span><span class="sxs-lookup"><span data-stu-id="3b729-2986">output</span></span> | <span data-ttu-id="3b729-2987">리듀서의 출력 파일(위치 포함)입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2987">Output file (including location) for the reducer.</span></span> <span data-ttu-id="3b729-2988">Hadoop 스트리밍 작업의 출력이 이 속성에 지정된 위치에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2988">The output of the Hadoop Streaming job is written to the location specified for this property.</span></span> |
| <span data-ttu-id="3b729-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="3b729-2989">filePaths</span></span> | <span data-ttu-id="3b729-2990">매퍼 및 리듀서 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2990">Paths for the mapper and reducer executables.</span></span> <span data-ttu-id="3b729-2991">"adfsample/example/apps/wc.exe" 예에서 adfsample은 Blob 컨테이너, example/apps는 폴더, wc.exe는 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2991">In the example: "adfsample/example/apps/wc.exe", adfsample is the blob container, example/apps is the folder, and wc.exe is the executable.</span></span> | 
| <span data-ttu-id="3b729-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="3b729-2992">fileLinkedService</span></span> | <span data-ttu-id="3b729-2993">filePaths 섹션에 지정된 파일이 포함된 Azure 저장소를 나타내는 Azure Storage 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2993">Azure Storage linked service that represents the Azure storage that contains the files specified in the filePaths section.</span></span> | 
| <span data-ttu-id="3b729-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="3b729-2994">arguments</span></span> | <span data-ttu-id="3b729-2995">MapReduce 프로그램에 대해 쉼표로 구분된 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2995">A list of comma-separated arguments for the MapReduce program.</span></span> <span data-ttu-id="3b729-2996">런타임에 MapReduce 프레임워크의 몇 개 인수(예: mapreduce.job.tags)가 추가로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from the MapReduce framework.</span></span> <span data-ttu-id="3b729-2997">MapReduce 인수로 사용자 인수를 구분하려면 다음 예제와 같이 인수로 옵션과 값을 모두 사용하는 것이 좋습니다(-s, --input, --output 등은 바로 뒤에 해당 값이 있는 옵션임).</span><span class="sxs-lookup"><span data-stu-id="3b729-2997">To differentiate your arguments with the MapReduce arguments, consider using both option and value as arguments as shown in the following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="3b729-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="3b729-2998">getDebugInfo</span></span> | <span data-ttu-id="3b729-2999">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-2999">An optional element.</span></span> <span data-ttu-id="3b729-3000">Failure로 설정되면 실패한 경우에만 로그가 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3000">When it is set to Failure, the logs are downloaded only on failure.</span></span> <span data-ttu-id="3b729-3001">All로 설정되면 실행 상태에 관계 없이 로그가 항상 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3001">When it is set to All, logs are always downloaded irrespective of the execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="3b729-3002">**outputs** 속성의 Hadoop 스트리밍 활동에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3002">You must specify an output dataset for the Hadoop Streaming Activity for the **outputs** property.</span></span> <span data-ttu-id="3b729-3003">이 데이터 집합은 파이프라인 일정(매시간, 매일 등)을 진행하는 데 필요한 더미 데이터 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3003">This dataset can be just a dummy dataset that is required to drive the pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="3b729-3004">활동에서 입력(input)을 사용하지 않는 경우 **inputs** 속성의 활동에 대한 입력 데이터 집합을 지정하지 않은 채 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3004">If the activity doesn't take an input, you can skip specifying an input dataset for the activity for the **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="3b729-3005">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3005">JSON example</span></span>

```json
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
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
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
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

<span data-ttu-id="3b729-3006">자세한 내용은 [Hadoop 스트리밍 활동](data-factory-hadoop-streaming-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="3b729-3007">HDInsight Spark 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="3b729-3008">Spark 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3008">You can specify the following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="3b729-3009">활동의 type 속성은 **HDInsightSpark**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3009">The type property for the activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="3b729-3010">먼저 HDInsight 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3010">You must create a HDInsight linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-3011">활동의 type을 HDInsightSpark로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3011">The following properties are supported in the **typeProperties** section when you set the type of activity to HDInsightSpark:</span></span> 

| <span data-ttu-id="3b729-3012">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3012">Property</span></span> | <span data-ttu-id="3b729-3013">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3013">Description</span></span> | <span data-ttu-id="3b729-3014">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="3b729-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="3b729-3015">rootPath</span></span> | <span data-ttu-id="3b729-3016">Spark 파일이 포함된 Azure Blob 컨테이너 및 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3016">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="3b729-3017">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3017">The file name is case-sensitive.</span></span> | <span data-ttu-id="3b729-3018">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3018">Yes</span></span> |
| <span data-ttu-id="3b729-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="3b729-3019">entryFilePath</span></span> | <span data-ttu-id="3b729-3020">Spark 코드/패키지의 루트 폴더에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3020">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="3b729-3021">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3021">Yes</span></span> |
| <span data-ttu-id="3b729-3022">className</span><span class="sxs-lookup"><span data-stu-id="3b729-3022">className</span></span> | <span data-ttu-id="3b729-3023">응용 프로그램의 Java/Spark main 클래스</span><span class="sxs-lookup"><span data-stu-id="3b729-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="3b729-3024">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3024">No</span></span> | 
| <span data-ttu-id="3b729-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="3b729-3025">arguments</span></span> | <span data-ttu-id="3b729-3026">Spark 프로그램에 대한 명령줄 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3026">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="3b729-3027">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3027">No</span></span> | 
| <span data-ttu-id="3b729-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="3b729-3028">proxyUser</span></span> | <span data-ttu-id="3b729-3029">Spark 프로그램 실행을 가장하는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="3b729-3029">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="3b729-3030">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3030">No</span></span> | 
| <span data-ttu-id="3b729-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="3b729-3031">sparkConfig</span></span> | <span data-ttu-id="3b729-3032">Spark 구성 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3032">Spark configuration properties.</span></span> | <span data-ttu-id="3b729-3033">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3033">No</span></span> | 
| <span data-ttu-id="3b729-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="3b729-3034">getDebugInfo</span></span> | <span data-ttu-id="3b729-3035">sparkJobLinkedService에 지정되었거나 HDInsight 클러스터에 사용된 Azure Storage에 Spark 로그 파일을 언제 복사할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3035">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="3b729-3036">허용되는 값: None, Always 또는 Failure.</span><span class="sxs-lookup"><span data-stu-id="3b729-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="3b729-3037">기본값: None.</span><span class="sxs-lookup"><span data-stu-id="3b729-3037">Default value: None.</span></span> | <span data-ttu-id="3b729-3038">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3038">No</span></span> | 
| <span data-ttu-id="3b729-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="3b729-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="3b729-3040">Spark 작업 파일, 종속성 및 로그를 보유하는 Azure Storage 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3040">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="3b729-3041">이 속성에 대한 값을 지정하지 않으면 HDInsight 클러스터와 연결된 저장소가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3041">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="3b729-3042">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="3b729-3043">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3043">JSON example</span></span>

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
<span data-ttu-id="3b729-3044">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3044">Note the following points:</span></span> 

- <span data-ttu-id="3b729-3045">**type** 속성은 **HDInsightSpark**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3045">The **type** property is set to **HDInsightSpark**.</span></span>
- <span data-ttu-id="3b729-3046">**rootPath**는 **adfspark\\pyFiles**로 설정되며, 여기서 adfspark는 Azure Blob 컨테이너이고, pyFiles는 해당 컨테이너의 파일 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3046">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="3b729-3047">이 예에서 Azure Blob Storage는 Spark 클러스터와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3047">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="3b729-3048">파일을 다른 Azure Storage에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3048">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="3b729-3049">이렇게 하는 경우 해당 저장소 계정을 데이터 팩터리에 연결하는 Azure Storage 연결된 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3049">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="3b729-3050">그런 다음 연결된 서비스의 이름을 **sparkJobLinkedService** 속성의 값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3050">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="3b729-3051">이 속성과 Spark 작업에서 지원하는 기타 속성에 대한 자세한 내용은 [Spark 작업 속성](#spark-activity-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>
- <span data-ttu-id="3b729-3052">**entryFilePath**는 python 파일인 **test.py**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3052">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span> 
- <span data-ttu-id="3b729-3053">**getDebugInfo** 속성은 **Always**로 설정되며, 이는 로그 파일이 항상 생성(성공 또는 실패)된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3053">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="3b729-3054">문제를 해결하는 경우가 아니라면 프로덕션 환경에서 이 속성을 Always로 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3054">We recommend that you do not set this property to Always in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="3b729-3055">**outputs** 섹션에는 하나의 출력 데이터 집합만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3055">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="3b729-3056">Spark 프로그램이 출력을 생성하지 않더라도 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3056">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="3b729-3057">출력 데이터 집합은 파이프라인의 일정(매시간, 매일 등)을 구동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3057">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="3b729-3058">활동에 대한 자세한 내용은 [Spark 활동](data-factory-spark.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3058">For more information about the activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="3b729-3059">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="3b729-3060">Azure ML 배치 실행 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3060">You can specify the following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="3b729-3061">활동의 type 속성은 **AzureMLBatchExecution**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3061">The type property for the activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="3b729-3062">먼저 Azure Machine Learning 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3062">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-3063">활동의 type을 AzureMLBatchExecution로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3063">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLBatchExecution:</span></span>

<span data-ttu-id="3b729-3064">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3064">Property</span></span> | <span data-ttu-id="3b729-3065">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3065">Description</span></span> | <span data-ttu-id="3b729-3066">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="3b729-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="3b729-3067">webServiceInput</span></span> | <span data-ttu-id="3b729-3068">Azure ML 웹 서비스의 입력(input)으로 전달되는 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3068">The dataset to be passed as an input for the Azure ML web service.</span></span> <span data-ttu-id="3b729-3069">이 데이터 집합은 활동의 입력에도 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3069">This dataset must also be included in the inputs for the activity.</span></span> |<span data-ttu-id="3b729-3070">webServiceInput 또는 webServiceInputs를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="3b729-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="3b729-3071">webServiceInputs</span></span> | <span data-ttu-id="3b729-3072">Azure ML 웹 서비스의 입력(inputs)으로 전달되는 데이터 집합들을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3072">Specify datasets to be passed as inputs for the Azure ML web service.</span></span> <span data-ttu-id="3b729-3073">웹 서비스에서 여러 입력을 사용하는 경우 webServiceInput 속성 대신 webServiceInputs 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3073">If the web service takes multiple inputs, use the webServiceInputs property instead of using the webServiceInput property.</span></span> <span data-ttu-id="3b729-3074">**webServiceInputs**에서 참조하는 데이터 집합은 또한 **입력** 작업에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3074">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span> | <span data-ttu-id="3b729-3075">webServiceInput 또는 webServiceInputs를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="3b729-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="3b729-3076">webServiceOutputs</span></span> | <span data-ttu-id="3b729-3077">Azure ML 웹 서비스의 출력으로 할당되는 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3077">The datasets that are assigned as outputs for the Azure ML web service.</span></span> <span data-ttu-id="3b729-3078">웹 서비스는 이 데이터 집합의 출력 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3078">The web service returns output data in this dataset.</span></span> | <span data-ttu-id="3b729-3079">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3079">Yes</span></span> | 
<span data-ttu-id="3b729-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-3080">globalParameters</span></span> | <span data-ttu-id="3b729-3081">이 섹션에서 웹 서비스 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3081">Specify values for the web service parameters in this section.</span></span> | <span data-ttu-id="3b729-3082">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="3b729-3083">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3083">JSON example</span></span>
<span data-ttu-id="3b729-3084">이 예제의 활동에는 입력으로 **MLSqlInput** 데이터 집합이, 출력으로 **MLSqlOutput**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3084">In this example, the activity has the dataset **MLSqlInput** as input and **MLSqlOutput** as the output.</span></span> <span data-ttu-id="3b729-3085">**MLSqlInput**은 **webServiceInput** JSON 속성을 사용하여 입력으로 웹 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3085">The **MLSqlInput** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="3b729-3086">**MLSqlOutput**은 **webServiceOutputs** JSON 속성을 사용하여 출력으로 웹 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3086">The **MLSqlOutput** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span> 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

<span data-ttu-id="3b729-3087">JSON 예제에서 배포된 Azure Machine Learning 웹 서비스는 판독기와 기록기 모듈을 사용하여 Azure SQL Database에서 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3087">In the JSON example, the deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="3b729-3088">이 웹 서비스는 네 개의 매개 변수, 즉 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3088">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="3b729-3089">AzureMLBatchExecution 작업의 입력 및 출력만 웹 서비스에 매개 변수로 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3089">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="3b729-3090">예를 들어 위의 JSON 조각에서 MLSqlInput은 AzureMLBatchExecution 활동에 대한 입력이며, webServiceInput 매개 변수를 통해 입력으로 웹 서비스에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3090">For example, in the above JSON snippet, MLSqlInput is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="3b729-3091">Machine Learning 업데이트 리소스 활동</span><span class="sxs-lookup"><span data-stu-id="3b729-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="3b729-3092">Azure ML 업데이트 리소스 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3092">You can specify the following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="3b729-3093">활동의 type 속성은 **AzureMLUpdateResource**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3093">The type property for the activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="3b729-3094">먼저 Azure Machine Learning 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3094">You must create a Azure Machine Learning linked service first and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-3095">활동의 type을 AzureMLUpdateResource로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3095">The following properties are supported in the **typeProperties** section when you set the type of activity to AzureMLUpdateResource:</span></span>

<span data-ttu-id="3b729-3096">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3096">Property</span></span> | <span data-ttu-id="3b729-3097">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3097">Description</span></span> | <span data-ttu-id="3b729-3098">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="3b729-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="3b729-3099">trainedModelName</span></span> | <span data-ttu-id="3b729-3100">다시 학습된 모델의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3100">Name of the retrained model.</span></span> | <span data-ttu-id="3b729-3101">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3101">Yes</span></span> |  
<span data-ttu-id="3b729-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="3b729-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="3b729-3103">재학습 작업으로 반환된 iLearner 파일을 가리키는 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3103">Dataset pointing to the iLearner file returned by the retraining operation.</span></span> | <span data-ttu-id="3b729-3104">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="3b729-3105">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3105">JSON example</span></span>
<span data-ttu-id="3b729-3106">파이프라인에는 **AzureMLBatchExecution** 및 **AzureMLUpdateResource**라는 두 활동이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3106">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="3b729-3107">Azure ML 배치 실행 작업은 학습 데이터를 입력으로 사용하여 .iLearner 파일을 출력으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3107">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="3b729-3108">이 작업은 입력 교육 데이터와 함께 학습 웹 서비스(웹 서비스로 노출된 학습 실험)를 호출하고 웹 서비스로부터 ilearner 파일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3108">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="3b729-3109">placeholderBlob는 Azure 데이터 팩터리 서비스가 파이프라인을 실행하기 위해 필요로 하는 더미 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3109">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="3b729-3110">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="3b729-3111">U-SQL 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3111">You can specify the following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="3b729-3112">활동의 type 속성은 **DataLakeAnalyticsU-SQL**이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3112">The type property for the activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="3b729-3113">Azure Data Lake Analytics 연결된 서비스를 만들고 해당 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3113">You must create an Azure Data Lake Analytics linked service and specify the name of it as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-3114">활동의 type을 DataLakeAnalyticsU-SQL로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3114">The following properties are supported in the **typeProperties** section when you set the type of activity to DataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="3b729-3115">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3115">Property</span></span> | <span data-ttu-id="3b729-3116">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3116">Description</span></span> | <span data-ttu-id="3b729-3117">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="3b729-3118">scriptPath</span></span> |<span data-ttu-id="3b729-3119">U-SQL 스크립트가 포함된 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3119">Path to folder that contains the U-SQL script.</span></span> <span data-ttu-id="3b729-3120">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3120">Name of the file is case-sensitive.</span></span> |<span data-ttu-id="3b729-3121">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-3121">No (if you use script)</span></span> |
| <span data-ttu-id="3b729-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="3b729-3122">scriptLinkedService</span></span> |<span data-ttu-id="3b729-3123">스크립트가 포함된 저장소를 Data Factory에 연결하는 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3123">Linked service that links the storage that contains the script to the data factory</span></span> |<span data-ttu-id="3b729-3124">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-3124">No (if you use script)</span></span> |
| <span data-ttu-id="3b729-3125">script</span><span class="sxs-lookup"><span data-stu-id="3b729-3125">script</span></span> |<span data-ttu-id="3b729-3126">scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="3b729-3127">예: "script" : "CREATE DATABASE test"</span><span class="sxs-lookup"><span data-stu-id="3b729-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="3b729-3128">아니요(scriptPath 및 scriptLinkedService를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="3b729-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="3b729-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="3b729-3129">degreeOfParallelism</span></span> |<span data-ttu-id="3b729-3130">작업을 실행하는 데 동시에 사용되는 최대 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3130">The maximum number of nodes simultaneously used to run the job.</span></span> |<span data-ttu-id="3b729-3131">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3131">No</span></span> |
| <span data-ttu-id="3b729-3132">우선 순위</span><span class="sxs-lookup"><span data-stu-id="3b729-3132">priority</span></span> |<span data-ttu-id="3b729-3133">대기열에 있는 모든 작업 중에서 먼저 실행해야 하는 작업을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3133">Determines which jobs out of all that are queued should be selected to run first.</span></span> <span data-ttu-id="3b729-3134">번호가 낮을수록 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3134">The lower the number, the higher the priority.</span></span> |<span data-ttu-id="3b729-3135">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3135">No</span></span> |
| <span data-ttu-id="3b729-3136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3b729-3136">parameters</span></span> |<span data-ttu-id="3b729-3137">U-SQL 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3b729-3137">Parameters for the U-SQL script</span></span> |<span data-ttu-id="3b729-3138">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="3b729-3139">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3139">JSON example</span></span>

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="3b729-3140">자세한 내용은 [Data Lake Analytics U-SQL 활동](data-factory-usql-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="3b729-3141">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="3b729-3142">저장 프로시저 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3142">You can specify the following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="3b729-3143">활동의 type 속성은 **SqlServerStoredProcedure**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3143">The type property for the activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="3b729-3144">다음 연결된 서비스 중 하나를 만들고 해당 연결된 서비스의 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3144">You must create an one of the following linked services and specify the name of the linked service as a value for the **linkedServiceName** property:</span></span>

- <span data-ttu-id="3b729-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3b729-3145">SQL Server</span></span> 
- <span data-ttu-id="3b729-3146">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="3b729-3146">Azure SQL Database</span></span>
- <span data-ttu-id="3b729-3147">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="3b729-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="3b729-3148">활동의 type을 SqlServerStoredProcedure로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3148">The following properties are supported in the **typeProperties** section when you set the type of activity to SqlServerStoredProcedure:</span></span>

| <span data-ttu-id="3b729-3149">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3149">Property</span></span> | <span data-ttu-id="3b729-3150">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3150">Description</span></span> | <span data-ttu-id="3b729-3151">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b729-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="3b729-3152">storedProcedureName</span></span> |<span data-ttu-id="3b729-3153">출력 테이블에서 사용하는 연결된 서비스로 표시되는 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스의 저장 프로시저 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3153">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="3b729-3154">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3154">Yes</span></span> |
| <span data-ttu-id="3b729-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="3b729-3155">storedProcedureParameters</span></span> |<span data-ttu-id="3b729-3156">저장 프로시저 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="3b729-3157">매개 변수에 대해 null을 전달해야 하는 경우 구문: "param1": null(모두 소문자)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3157">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="3b729-3158">이 속성을 사용하는 방법에 대한 자세한 내용은 다음 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3158">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="3b729-3159">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3159">No</span></span> |

<span data-ttu-id="3b729-3160">입력 데이터 집합을 지정하는 경우 실행할 저장 프로시저 작업에 사용할 수 있어야 합니다('Ready' 상태).</span><span class="sxs-lookup"><span data-stu-id="3b729-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="3b729-3161">저장 프로시저에서 입력 데이터 집합을 매개 변수로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3161">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="3b729-3162">저장 프로시저 작업을 시작하기 전에 종속성을 확인하는 데만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3162">It is only used to check the dependency before starting the stored procedure activity.</span></span> <span data-ttu-id="3b729-3163">저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="3b729-3164">출력 데이터 집합은 저장 프로시저 작업에 대한 **일정** (매시간, 매주, 매월 등)을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3164">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="3b729-3165">출력 데이터 집합은 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스나 저장 프로시저를 실행하려는 SQL Server 데이터베이스를 참조하는 **연결된 서비스** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3165">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="3b729-3166">출력 데이터 집합은 파이프라인에서 다른 작업에 의한 후속 처리([활동 체이닝](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline))를 위해 저장 프로시저의 결과를 전달하는 방법으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3166">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in the pipeline.</span></span> <span data-ttu-id="3b729-3167">그러나 Data Factory는 저장 프로시저의 출력을 이 데이터 집합에 자동으로 쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3167">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="3b729-3168">출력 데이터 집합이 가리키는 SQL 테이블에 기록하는 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3168">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="3b729-3169">경우에 따라 출력 데이터 집합은 저장 프로시저 작업을 실행하는 일정을 지정하기 위해서만 사용되는 **더미 데이터 집합**일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3169">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="3b729-3170">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3170">JSON example</span></span>

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

<span data-ttu-id="3b729-3171">자세한 내용은 [저장 프로시저 활동](data-factory-stored-proc-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="3b729-3172">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="3b729-3172">.NET custom activity</span></span>
<span data-ttu-id="3b729-3173">.NET 사용자 지정 활동 JSON 정의에서 다음 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3173">You can specify the following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="3b729-3174">활동의 type 속성은 **DotNetActivity**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3174">The type property for the activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="3b729-3175">Azure HDInsight 연결된 서비스 또는 Azure 배치 연결된 서비스를 만들고 해당 연결된 서비스의 이름을 **linkedServiceName** 속성의 값으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify the name of the linked service as a value for the **linkedServiceName** property.</span></span> <span data-ttu-id="3b729-3176">활동의 type을 DotNetActivity로 설정하는 경우 **typeProperties** 섹션에서 지원되는 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3176">The following properties are supported in the **typeProperties** section when you set the type of activity to DotNetActivity:</span></span>
 
| <span data-ttu-id="3b729-3177">속성</span><span class="sxs-lookup"><span data-stu-id="3b729-3177">Property</span></span> | <span data-ttu-id="3b729-3178">설명</span><span class="sxs-lookup"><span data-stu-id="3b729-3178">Description</span></span> | <span data-ttu-id="3b729-3179">필수</span><span class="sxs-lookup"><span data-stu-id="3b729-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="3b729-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="3b729-3180">AssemblyName</span></span> | <span data-ttu-id="3b729-3181">어셈블리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3181">Name of the assembly.</span></span> <span data-ttu-id="3b729-3182">예제에서는 **MyDotnetActivity.dll**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3182">In the example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="3b729-3183">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3183">Yes</span></span> |
| <span data-ttu-id="3b729-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="3b729-3184">EntryPoint</span></span> |<span data-ttu-id="3b729-3185">IDotNetActivity 인터페이스를 구현하는 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3185">Name of the class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="3b729-3186">예제에서는 **MyDotNetActivityNS.MyDotNetActivity**이며, 여기서 MyDotNetActivityNS는 네임스페이스이고, MyDotNetActivity는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3186">In the example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is the namespace and MyDotNetActivity is the class.</span></span>  | <span data-ttu-id="3b729-3187">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3187">Yes</span></span> | 
| <span data-ttu-id="3b729-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="3b729-3188">PackageLinkedService</span></span> | <span data-ttu-id="3b729-3189">사용자 지정 활동 zip 파일이 포함된 Blob 저장소를 가리키는 Azure Storage 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3189">Name of the Azure Storage linked service that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="3b729-3190">예제에서는 **AzureStorageLinkedService**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3190">In the example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="3b729-3191">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3191">Yes</span></span> |
| <span data-ttu-id="3b729-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="3b729-3192">PackageFile</span></span> | <span data-ttu-id="3b729-3193">zip 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3193">Name of the zip file.</span></span> <span data-ttu-id="3b729-3194">예제에서는 **customactivitycontainer/MyDotNetActivity.zip**입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3194">In the example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="3b729-3195">예</span><span class="sxs-lookup"><span data-stu-id="3b729-3195">Yes</span></span> |
| <span data-ttu-id="3b729-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="3b729-3196">extendedProperties</span></span> | <span data-ttu-id="3b729-3197">정의하고 .NET 코드에 전달할 수 있는 확장된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3197">Extended properties that you can define and pass on to the .NET code.</span></span> <span data-ttu-id="3b729-3198">예제에서 **SliceStart** 변수는 SliceStart 시스템 변수에 기반한 값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b729-3198">In this example, the **SliceStart** variable is set to a value based on the SliceStart system variable.</span></span> | <span data-ttu-id="3b729-3199">아니요</span><span class="sxs-lookup"><span data-stu-id="3b729-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="3b729-3200">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="3b729-3200">JSON example</span></span>

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

<span data-ttu-id="3b729-3201">자세한 내용은 [Data Factory에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3b729-3202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b729-3202">Next Steps</span></span>
<span data-ttu-id="3b729-3203">다음 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3b729-3203">See the following tutorials:</span></span> 

- [<span data-ttu-id="3b729-3204">자습서: 복사 활동이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="3b729-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="3b729-3205">자습서: Hive 활동이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="3b729-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)