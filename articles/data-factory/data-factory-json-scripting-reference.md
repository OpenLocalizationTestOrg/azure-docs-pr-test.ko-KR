---
title: "데이터 팩터리-aaaAzure JSON 스크립팅 참조 | Microsoft Docs"
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
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a><span data-ttu-id="e44c9-103">Azure Data Factory - JSON 스크립팅 참조</span><span class="sxs-lookup"><span data-stu-id="e44c9-103">Azure Data Factory - JSON Scripting Reference</span></span>
<span data-ttu-id="e44c9-104">이 문서에서는 Azure Data Factory 엔터티(파이프라인, 활동, 데이터 집합 및 연결된 서비스)를 정의하기 위한 JSON 스키마와 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-104">This article provides JSON schemas and examples for defining Azure Data Factory entities (pipeline, activity, dataset, and linked service).</span></span>  

## <a name="pipeline"></a><span data-ttu-id="e44c9-105">파이프라인</span><span class="sxs-lookup"><span data-stu-id="e44c9-105">Pipeline</span></span> 
<span data-ttu-id="e44c9-106">hello 파이프라인 정의 대 한 고급 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-106">hello high-level structure for a pipeline definition is as follows:</span></span> 

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

<span data-ttu-id="e44c9-107">다음 표에서 hello 파이프라인 JSON 정의 내에서 hello 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-107">Following table describes hello properties within hello pipeline JSON definition:</span></span>

| <span data-ttu-id="e44c9-108">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-108">Property</span></span> | <span data-ttu-id="e44c9-109">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-109">Description</span></span> | <span data-ttu-id="e44c9-110">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-110">Required</span></span>
-------- | ----------- | --------
| <span data-ttu-id="e44c9-111">name</span><span class="sxs-lookup"><span data-stu-id="e44c9-111">name</span></span> | <span data-ttu-id="e44c9-112">Hello 파이프라인의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-112">Name of hello pipeline.</span></span> <span data-ttu-id="e44c9-113">활동 hello hello 동작을 나타내는 이름을 지정 하거나 파이프라인은 구성 된 toodo</span><span class="sxs-lookup"><span data-stu-id="e44c9-113">Specify a name that represents hello action that hello activity or pipeline is configured toodo</span></span><br/><ul><li><span data-ttu-id="e44c9-114">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="e44c9-114">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="e44c9-115">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-115">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="e44c9-116">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="e44c9-116">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="e44c9-117">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-117">Yes</span></span> |
| <span data-ttu-id="e44c9-118">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-118">description</span></span> |<span data-ttu-id="e44c9-119">어떤 hello 활동 또는 파이프라인을 설명 하는 텍스트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-119">Text describing what hello activity or pipeline is used for</span></span> | <span data-ttu-id="e44c9-120">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-120">No</span></span> |
| <span data-ttu-id="e44c9-121">작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-121">activities</span></span> | <span data-ttu-id="e44c9-122">활동의 목록을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-122">Contains a list of activities.</span></span> | <span data-ttu-id="e44c9-123">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-123">Yes</span></span> |
| <span data-ttu-id="e44c9-124">start</span><span class="sxs-lookup"><span data-stu-id="e44c9-124">start</span></span> |<span data-ttu-id="e44c9-125">시작 날짜 / 시간 hello 파이프라인에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-125">Start date-time for hello pipeline.</span></span> <span data-ttu-id="e44c9-126">[ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-126">Must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="e44c9-127">예: 2014-10-14T16:32:41</span><span class="sxs-lookup"><span data-stu-id="e44c9-127">For example: 2014-10-14T16:32:41.</span></span> <br/><br/><span data-ttu-id="e44c9-128">이제는 현지 시간을 가능한 toospecify 예는 EST입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-128">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="e44c9-129">예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="e44c9-129">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="e44c9-130">hello 시작 및 끝 속성 함께 지정 hello 파이프라인에 대 한 활성 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-130">hello start and end properties together specify active period for hello pipeline.</span></span> <span data-ttu-id="e44c9-131">출력 조각은 이 활성 기간에만 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-131">Output slices are only produced with in this active period.</span></span> |<span data-ttu-id="e44c9-132">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-132">No</span></span><br/><br/><span data-ttu-id="e44c9-133">Hello end 속성에 대 한 값을 지정 하는 경우 hello 시작 속성에 대 한 값을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-133">If you specify a value for hello end property, you must specify value for hello start property.</span></span><br/><br/><span data-ttu-id="e44c9-134">hello 시작 및 종료 시간 둘 다 수 빈 toocreate 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="e44c9-134">hello start and end times can both be empty toocreate a pipeline.</span></span> <span data-ttu-id="e44c9-135">값을 모두 지정 해야 합니다는 파이프라인 toorun hello에 대 한 활성 기간 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-135">You must specify both values tooset an active period for hello pipeline toorun.</span></span> <span data-ttu-id="e44c9-136">시작 및 종료 시간을 지정 하지 않을 경우 파이프라인을 만들 때 설정할 수 있습니다 hello 집합 AzureRmDataFactoryPipelineActivePeriod cmdlet를 사용 하 여 나중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-136">If you do not specify start and end times when creating a pipeline, you can set them using hello Set-AzureRmDataFactoryPipelineActivePeriod cmdlet later.</span></span> |
| <span data-ttu-id="e44c9-137">end</span><span class="sxs-lookup"><span data-stu-id="e44c9-137">end</span></span> |<span data-ttu-id="e44c9-138">Hello 파이프라인에 대 한 날짜 및 시간을 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-138">End date-time for hello pipeline.</span></span> <span data-ttu-id="e44c9-139">지정된 경우 ISO 형식에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-139">If specified must be in ISO format.</span></span> <span data-ttu-id="e44c9-140">예: 2014-10-14T17:32:41</span><span class="sxs-lookup"><span data-stu-id="e44c9-140">For example: 2014-10-14T17:32:41</span></span> <br/><br/><span data-ttu-id="e44c9-141">이제는 현지 시간을 가능한 toospecify 예는 EST입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-141">It is possible toospecify a local time, for example an EST time.</span></span> <span data-ttu-id="e44c9-142">예: `2016-02-27T06:00:00**-05:00`(오전 6시 동부 표준시)</span><span class="sxs-lookup"><span data-stu-id="e44c9-142">Here is an example: `2016-02-27T06:00:00**-05:00`, which is 6 AM EST.</span></span><br/><br/><span data-ttu-id="e44c9-143">toorun hello 파이프라인 hello hello 최종 속성 값으로 9999-09-09를 무제한으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-143">toorun hello pipeline indefinitely, specify 9999-09-09 as hello value for hello end property.</span></span> |<span data-ttu-id="e44c9-144">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-144">No</span></span> <br/><br/><span data-ttu-id="e44c9-145">Hello 시작 속성에 대 한 값을 지정 하는 경우 hello end 속성에 대 한 값을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-145">If you specify a value for hello start property, you must specify value for hello end property.</span></span><br/><br/><span data-ttu-id="e44c9-146">Hello에 대 한 메모를 참조 하세요 **시작** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-146">See notes for hello **start** property.</span></span> |
| <span data-ttu-id="e44c9-147">isPaused</span><span class="sxs-lookup"><span data-stu-id="e44c9-147">isPaused</span></span> |<span data-ttu-id="e44c9-148">집합 tootrue hello 파이프라인 실행 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-148">If set tootrue hello pipeline does not run.</span></span> <span data-ttu-id="e44c9-149">기본값 = false입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-149">Default value = false.</span></span> <span data-ttu-id="e44c9-150">속성 tooenable이를 사용 하거나 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-150">You can use this property tooenable or disable.</span></span> |<span data-ttu-id="e44c9-151">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-151">No</span></span> |
| <span data-ttu-id="e44c9-152">pipelineMode</span><span class="sxs-lookup"><span data-stu-id="e44c9-152">pipelineMode</span></span> |<span data-ttu-id="e44c9-153">hello 메서드 hello 파이프라인에 대 한 실행을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-153">hello method for scheduling runs for hello pipeline.</span></span> <span data-ttu-id="e44c9-154">허용되는 값은 scheduled(기본), onetime입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-154">Allowed values are: scheduled (default), onetime.</span></span><br/><br/><span data-ttu-id="e44c9-155">'예약' hello 파이프라인 tooits 활성 기간 (시작 및 종료 시간)에 따라 지정 된 시간 간격으로 실행을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-155">‘Scheduled’ indicates that hello pipeline runs at a specified time interval according tooits active period (start and end time).</span></span> <span data-ttu-id="e44c9-156">'Onetime' hello 파이프라인 실행 한 번만 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-156">‘Onetime’ indicates that hello pipeline runs only once.</span></span> <span data-ttu-id="e44c9-157">현재는, Onetime 파이프라인이 생성된 후에 수정/업데이트가 불가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-157">Onetime pipelines once created cannot be modified/updated currently.</span></span> <span data-ttu-id="e44c9-158">일회성 설정에 대한 세부 정보는 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-158">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details about onetime setting.</span></span> |<span data-ttu-id="e44c9-159">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-159">No</span></span> |
| <span data-ttu-id="e44c9-160">expirationTime</span><span class="sxs-lookup"><span data-stu-id="e44c9-160">expirationTime</span></span> |<span data-ttu-id="e44c9-161">hello에 대 한 파이프라인 올바른지와 프로 비전 된 유지할지를 만든 후 기간.</span><span class="sxs-lookup"><span data-stu-id="e44c9-161">Duration of time after creation for which hello pipeline is valid and should remain provisioned.</span></span> <span data-ttu-id="e44c9-162">없는 모든 활성 실패 하거나 삭제 한 경우 실행 보류 중인 hello 파이프라인은 한 번 자동으로 hello 만료 시간에 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-162">If it does not have any active, failed, or pending runs, hello pipeline is deleted automatically once it reaches hello expiration time.</span></span> |<span data-ttu-id="e44c9-163">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-163">No</span></span> |


## <a name="activity"></a><span data-ttu-id="e44c9-164">작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-164">Activity</span></span> 
<span data-ttu-id="e44c9-165">hello 파이프라인 정의 (활동 요소) 내에서 활동에 대 한 고급 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-165">hello high-level structure for an activity within a pipeline definition (activities element) is as follows:</span></span>

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

<span data-ttu-id="e44c9-166">다음 테이블 hello 활동 JSON 정의 내에서 hello 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-166">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="e44c9-167">태그</span><span class="sxs-lookup"><span data-stu-id="e44c9-167">Tag</span></span> | <span data-ttu-id="e44c9-168">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-168">Description</span></span> | <span data-ttu-id="e44c9-169">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-170">name</span><span class="sxs-lookup"><span data-stu-id="e44c9-170">name</span></span> |<span data-ttu-id="e44c9-171">Hello 활동의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-171">Name of hello activity.</span></span> <span data-ttu-id="e44c9-172">Hello 동작 hello 활동을 나타내는 이름을 toodo 구성 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-172">Specify a name that represents hello action that hello activity is configured toodo</span></span><br/><ul><li><span data-ttu-id="e44c9-173">최대 문자 수: 260</span><span class="sxs-lookup"><span data-stu-id="e44c9-173">Maximum number of characters: 260</span></span></li><li><span data-ttu-id="e44c9-174">문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-174">Must start with a letter number, or an underscore (_)</span></span></li><li><span data-ttu-id="e44c9-175">다음 문자는 사용할 수 없습니다. “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="e44c9-175">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”,”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |<span data-ttu-id="e44c9-176">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-176">Yes</span></span> |
| <span data-ttu-id="e44c9-177">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-177">description</span></span> |<span data-ttu-id="e44c9-178">어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-178">Text describing what hello activity is used for.</span></span> |<span data-ttu-id="e44c9-179">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-179">Yes</span></span> |
| <span data-ttu-id="e44c9-180">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-180">type</span></span> |<span data-ttu-id="e44c9-181">Hello hello 활동 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-181">Specifies hello type of hello activity.</span></span> <span data-ttu-id="e44c9-182">Hello 참조 [데이터 저장소](#data-stores) 및 [데이터 변환 작업](#data-transformation-activities) 다양 한 유형의 활동에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-182">See hello [DATA STORES](#data-stores) and [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) sections for different types of activities.</span></span> |<span data-ttu-id="e44c9-183">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-183">Yes</span></span> |
| <span data-ttu-id="e44c9-184">inputs</span><span class="sxs-lookup"><span data-stu-id="e44c9-184">inputs</span></span> |<span data-ttu-id="e44c9-185">Hello 활동에서 사용 하는 입력된 테이블</span><span class="sxs-lookup"><span data-stu-id="e44c9-185">Input tables used by hello activity</span></span><br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |<span data-ttu-id="e44c9-186">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-186">Yes</span></span> |
| <span data-ttu-id="e44c9-187">outputs</span><span class="sxs-lookup"><span data-stu-id="e44c9-187">outputs</span></span> |<span data-ttu-id="e44c9-188">Hello 활동에 의해 사용 되는 출력된 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-188">Output tables used by hello activity.</span></span><br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |<span data-ttu-id="e44c9-189">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-189">Yes</span></span> |
| <span data-ttu-id="e44c9-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e44c9-190">linkedServiceName</span></span> |<span data-ttu-id="e44c9-191">Hello 활동에서 사용 하는 hello 연결 된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-191">Name of hello linked service used by hello activity.</span></span> <br/><br/><span data-ttu-id="e44c9-192">활동은 toohello 필요한 계산 환경에 연결 하는 hello 연결 된 서비스를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-192">An activity may require that you specify hello linked service that links toohello required compute environment.</span></span> |<span data-ttu-id="e44c9-193">HDInsight 활동, Azure Machine Learning 활동 및 저장 프로시저 활동의 경우 예</span><span class="sxs-lookup"><span data-stu-id="e44c9-193">Yes for HDInsight activities, Azure Machine Learning activities, and Stored Procedure Activity.</span></span> <br/><br/><span data-ttu-id="e44c9-194">다른 모든 사용자의 경우 아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-194">No for all others</span></span> |
| <span data-ttu-id="e44c9-195">typeProperties</span><span class="sxs-lookup"><span data-stu-id="e44c9-195">typeProperties</span></span> |<span data-ttu-id="e44c9-196">Hello typeProperties 섹션의 속성 hello 활동의 형식에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-196">Properties in hello typeProperties section depend on type of hello activity.</span></span> |<span data-ttu-id="e44c9-197">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-197">No</span></span> |
| <span data-ttu-id="e44c9-198">policy</span><span class="sxs-lookup"><span data-stu-id="e44c9-198">policy</span></span> |<span data-ttu-id="e44c9-199">Hello 활동의 hello 런타임 동작에 영향을 주는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-199">Policies that affect hello run-time behavior of hello activity.</span></span> <span data-ttu-id="e44c9-200">지정하지 않으면 기본 정책이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-200">If it is not specified, default policies are used.</span></span> |<span data-ttu-id="e44c9-201">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-201">No</span></span> |
| <span data-ttu-id="e44c9-202">scheduler</span><span class="sxs-lookup"><span data-stu-id="e44c9-202">scheduler</span></span> |<span data-ttu-id="e44c9-203">"스케줄러" 속성은 사용 되는 toodefine을 원하는 hello 활동에 대 한 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-203">“scheduler” property is used toodefine desired scheduling for hello activity.</span></span> <span data-ttu-id="e44c9-204">해당 속성의 하위 hello hello에서와 동일 hello는 [데이터 집합의 가용성 속성](data-factory-create-datasets.md#dataset-availability)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-204">Its subproperties are hello same as hello ones in hello [availability property in a dataset](data-factory-create-datasets.md#dataset-availability).</span></span> |<span data-ttu-id="e44c9-205">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-205">No</span></span> |

### <a name="policies"></a><span data-ttu-id="e44c9-206">정책</span><span class="sxs-lookup"><span data-stu-id="e44c9-206">Policies</span></span>
<span data-ttu-id="e44c9-207">정책은은 hello 테이블 조각이 처리 시에 특히는 활동의 런타임 동작을 hello는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-207">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="e44c9-208">다음 표에서 hello hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-208">hello following table provides hello details.</span></span>

| <span data-ttu-id="e44c9-209">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-209">Property</span></span> | <span data-ttu-id="e44c9-210">허용된 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-210">Permitted values</span></span> | <span data-ttu-id="e44c9-211">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-211">Default Value</span></span> | <span data-ttu-id="e44c9-212">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-212">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-213">동시성</span><span class="sxs-lookup"><span data-stu-id="e44c9-213">concurrency</span></span> |<span data-ttu-id="e44c9-214">정수 </span><span class="sxs-lookup"><span data-stu-id="e44c9-214">Integer</span></span> <br/><br/><span data-ttu-id="e44c9-215">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="e44c9-215">Max value: 10</span></span> |<span data-ttu-id="e44c9-216">1</span><span class="sxs-lookup"><span data-stu-id="e44c9-216">1</span></span> |<span data-ttu-id="e44c9-217">Hello 활동의 동시 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-217">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="e44c9-218">Hello 여러 조각에서 발생할 수 있는 병렬 활동 실행 횟수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-218">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="e44c9-219">예를 들어 활동을 통해 toogo 해야 하는 경우 다양 한 사용 가능한 데이터에 더 큰 동시성 가치가 속도가 향상 hello 데이터 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-219">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="e44c9-220">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="e44c9-220">executionPriorityOrder</span></span> |<span data-ttu-id="e44c9-221">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="e44c9-221">NewestFirst</span></span><br/><br/><span data-ttu-id="e44c9-222">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="e44c9-222">OldestFirst</span></span> |<span data-ttu-id="e44c9-223">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="e44c9-223">OldestFirst</span></span> |<span data-ttu-id="e44c9-224">Hello 데이터 조각이 처리 중인의 순서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-224">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="e44c9-225">예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-225">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="e44c9-226">Hello executionPriorityOrder toobe NewestFirst로 설정 하면 오후 5 시의 hello 조각이 먼저 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-226">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="e44c9-227">마찬가지로 executionPriorityORder toobe hello OldestFIrst로 설정 하면 오후 4 시의 hello 조각이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-227">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="e44c9-228">retry</span><span class="sxs-lookup"><span data-stu-id="e44c9-228">retry</span></span> |<span data-ttu-id="e44c9-229">정수 </span><span class="sxs-lookup"><span data-stu-id="e44c9-229">Integer</span></span><br/><br/><span data-ttu-id="e44c9-230">최대값이 10이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="e44c9-230">Max value can be 10</span></span> |<span data-ttu-id="e44c9-231">0</span><span class="sxs-lookup"><span data-stu-id="e44c9-231">0</span></span> |<span data-ttu-id="e44c9-232">Hello 조각에 대 한 hello 데이터 처리 전 까지의 재시도 횟수 Failure로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-232">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="e44c9-233">지정 된 toohello를 데이터 조각에 대 한 활동 실행을 다시 시도 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-233">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="e44c9-234">hello 재시도 hello 실패 후 가능한 한 빨리 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-234">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="e44c9-235">시간 제한</span><span class="sxs-lookup"><span data-stu-id="e44c9-235">timeout</span></span> |<span data-ttu-id="e44c9-236">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e44c9-236">TimeSpan</span></span> |<span data-ttu-id="e44c9-237">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e44c9-237">00:00:00</span></span> |<span data-ttu-id="e44c9-238">Hello 활동에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-238">Timeout for hello activity.</span></span> <span data-ttu-id="e44c9-239">예: 00:10:00(시간 제한 10분을 의미함)</span><span class="sxs-lookup"><span data-stu-id="e44c9-239">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="e44c9-240">값을 지정 하지 않거나 0으로 하는 경우에 hello 시간 초과 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-240">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="e44c9-241">분할 영역에 데이터 처리 시간이 hello hello 제한 시간 값을 초과 하는 경우 취소 되 및 hello 시스템 tooretry hello 처리를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-241">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="e44c9-242">재시도 횟수 hello hello retry 속성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-242">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="e44c9-243">시간 제한이 발생 hello 상태 tooTimedOut 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-243">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="e44c9-244">delay</span><span class="sxs-lookup"><span data-stu-id="e44c9-244">delay</span></span> |<span data-ttu-id="e44c9-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e44c9-245">TimeSpan</span></span> |<span data-ttu-id="e44c9-246">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e44c9-246">00:00:00</span></span> |<span data-ttu-id="e44c9-247">데이터 처리 hello 조각 시작 하기 전에 hello 지연 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-247">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="e44c9-248">데이터 조각에 대 한 활동의 hello 실행 hello 지연 되는 hello 예상 실행 시간 후에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-248">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="e44c9-249">예: 00:10:00(10분의 지연을 의미함)</span><span class="sxs-lookup"><span data-stu-id="e44c9-249">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="e44c9-250">longRetry</span><span class="sxs-lookup"><span data-stu-id="e44c9-250">longRetry</span></span> |<span data-ttu-id="e44c9-251">정수 </span><span class="sxs-lookup"><span data-stu-id="e44c9-251">Integer</span></span><br/><br/><span data-ttu-id="e44c9-252">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="e44c9-252">Max value: 10</span></span> |<span data-ttu-id="e44c9-253">1</span><span class="sxs-lookup"><span data-stu-id="e44c9-253">1</span></span> |<span data-ttu-id="e44c9-254">hello 긴 다시 시도 횟수 후 hello 조각 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-254">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="e44c9-255">longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-255">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="e44c9-256">따라서 다시 시도 사이의 시간 toospecify 해야 할 경우 longRetry를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-256">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="e44c9-257">Retry와 longRetry를 둘 다 지정 된 경우 다시 시도 횟수를 포함 하는 각 longRetry 시도 및 hello 최대 시도 횟수가 다시 시도 * longRetry 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-257">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="e44c9-258">예를 들어, hello 활동 정책의 설정에에서 따라 hello 사항이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="e44c9-258">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="e44c9-259">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="e44c9-259">Retry: 3</span></span><br/><span data-ttu-id="e44c9-260">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="e44c9-260">longRetry: 2</span></span><br/><span data-ttu-id="e44c9-261">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="e44c9-261">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="e44c9-262">하나의 분할 영역 tooexecute 가정 (상태 대기 중) hello 활동 실행 될 때마다가 실패 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-262">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="e44c9-263">우선 3번 연속 실행 시도를 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-263">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="e44c9-264">각 시도 후 조각 상태 hello 재시도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-264">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="e44c9-265">통해 처음 3 시도 되 면 hello 조각 상태 LongRetry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-265">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="e44c9-266">한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-266">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="e44c9-267">그 후 hello 조각 상태가 Failed가 고 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-267">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="e44c9-268">즉, 전체적으로 6번의 시도가 일어납니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-268">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="e44c9-269">실행에 성공 hello 조각 상태는 준비와 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-269">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="e44c9-270">longRetry 명확 하지 않은 시간에 도착 하면 종속 데이터 또는 hello 전체 환경 연결이 잘 끊어지는 어떤 데이터 처리가 수행 아래 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-270">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="e44c9-271">이러한 경우에 한 번에 하나씩 재시도 수행 하 도움이 되지 않을 수 및 출력을 원하는 hello에 결과 시간 간격 후 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-271">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="e44c9-272">주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-272">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="e44c9-273">일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-273">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="e44c9-274">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="e44c9-274">longRetryInterval</span></span> |<span data-ttu-id="e44c9-275">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e44c9-275">TimeSpan</span></span> |<span data-ttu-id="e44c9-276">00:00:00</span><span class="sxs-lookup"><span data-stu-id="e44c9-276">00:00:00</span></span> |<span data-ttu-id="e44c9-277">긴 시도 간의 지연을 hello</span><span class="sxs-lookup"><span data-stu-id="e44c9-277">hello delay between long retry attempts</span></span> |

### <a name="typeproperties-section"></a><span data-ttu-id="e44c9-278">typeProperties 섹션</span><span class="sxs-lookup"><span data-stu-id="e44c9-278">typeProperties section</span></span>
<span data-ttu-id="e44c9-279">hello typeProperties 섹션은 각 활동 마다 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-279">hello typeProperties section is different for each activity.</span></span> <span data-ttu-id="e44c9-280">변환 작업에는 방금 hello 형식 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-280">Transformation activities have just hello type properties.</span></span> <span data-ttu-id="e44c9-281">파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-281">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span> 

<span data-ttu-id="e44c9-282">**복사 작업이** hello typeProperties 섹션에는 하위 섹션 두 개가: **소스** 및 **싱크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-282">**Copy activity** has two subsections in hello typeProperties section: **source** and **sink**.</span></span> <span data-ttu-id="e44c9-283">참조 [데이터 저장소](#data-stores) JSON toouse 데이터 소스 및/또는 싱크로 저장 하는 방법을 보여 주는 샘플에 대 한이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-283">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span> 

### <a name="sample-copy-pipeline"></a><span data-ttu-id="e44c9-284">샘플 복사 파이프라인</span><span class="sxs-lookup"><span data-stu-id="e44c9-284">Sample copy pipeline</span></span>
<span data-ttu-id="e44c9-285">다음 샘플 파이프라인 hello에 하나의 활동 형식의 **복사** hello에 **활동** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-285">In hello following sample pipeline, there is one activity of type **Copy** in hello **activities** section.</span></span> <span data-ttu-id="e44c9-286">이 샘플에서는 hello [복사 작업이](data-factory-data-movement-activities.md) Azure Blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-286">In this sample, hello [Copy activity](data-factory-data-movement-activities.md) copies data from an Azure Blob storage tooan Azure SQL database.</span></span> 

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
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

<span data-ttu-id="e44c9-287">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="e44c9-287">Note hello following points:</span></span>

* <span data-ttu-id="e44c9-288">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span>
* <span data-ttu-id="e44c9-289">Hello 활동 너무 설정 되어 입력**InputDataset** 및 hello 활동 너무 설정 되어 출력**OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-289">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span>
* <span data-ttu-id="e44c9-290">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-290">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span>

<span data-ttu-id="e44c9-291">참조 [데이터 저장소](#data-stores) JSON toouse 데이터 소스 및/또는 싱크로 저장 하는 방법을 보여 주는 샘플에 대 한이 문서의 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-291">See [DATA STORES](#data-stores) section in this article for JSON samples that show how toouse a data store as a source and/or sink.</span></span>    

<span data-ttu-id="e44c9-292">이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-292">For a complete walkthrough of creating this pipeline, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="sample-transformation-pipeline"></a><span data-ttu-id="e44c9-293">샘플 변환 파이프라인</span><span class="sxs-lookup"><span data-stu-id="e44c9-293">Sample transformation pipeline</span></span>
<span data-ttu-id="e44c9-294">다음 샘플 파이프라인 hello에 하나의 활동 형식의 **HDInsightHive** hello에 **활동** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-294">In hello following sample pipeline, there is one activity of type **HDInsightHive** in hello **activities** section.</span></span> <span data-ttu-id="e44c9-295">이 샘플에서는 hello [HDInsight Hive 활동](data-factory-hive-activity.md) Azure HDInsight Hadoop 클러스터에서 하이브 스크립트 파일을 실행 하 여 Azure Blob 저장소에서 데이터를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-295">In this sample, hello [HDInsight Hive activity](data-factory-hive-activity.md) transforms data from an Azure Blob storage by running a Hive script file on an Azure HDInsight Hadoop cluster.</span></span> 

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

<span data-ttu-id="e44c9-296">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="e44c9-296">Note hello following points:</span></span> 

* <span data-ttu-id="e44c9-297">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**HDInsightHive**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-297">In hello activities section, there is only one activity whose **type** is set too**HDInsightHive**.</span></span>
* <span data-ttu-id="e44c9-298">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-298">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>
* <span data-ttu-id="e44c9-299">hello **정의** 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span><span class="sxs-lookup"><span data-stu-id="e44c9-299">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).</span></span>

<span data-ttu-id="e44c9-300">파이프라인에서 변환 활동을 정의하는 JSON 샘플은 이 문서의 [데이터 변환 활동](#data-transformation-activities) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-300">See [DATA TRANSFORMATION ACTIVITIES](#data-transformation-activities) section in this article for JSON samples that define transformation activities in a pipeline.</span></span>

<span data-ttu-id="e44c9-301">이 파이프라인을 만드는 전체 연습을 참조 하십시오. [자습서: 첫 번째 파이프라인 tooprocess 데이터 Hadoop 클러스터를 사용 하 여 빌드](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-301">For a complete walkthrough of creating this pipeline, see [Tutorial: Build your first pipeline tooprocess data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="linked-service"></a><span data-ttu-id="e44c9-302">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-302">Linked service</span></span>
<span data-ttu-id="e44c9-303">연결 된 서비스 정의 대 한 hello 고급 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-303">hello high-level structure for a linked service definition is as follows:</span></span>

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

<span data-ttu-id="e44c9-304">다음 테이블 hello 활동 JSON 정의 내에서 hello 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-304">Following table describe hello properties within hello activity JSON definition:</span></span>

| <span data-ttu-id="e44c9-305">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-305">Property</span></span> | <span data-ttu-id="e44c9-306">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-306">Description</span></span> | <span data-ttu-id="e44c9-307">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-307">Required</span></span> |
| -------- | ----------- | -------- | 
| <span data-ttu-id="e44c9-308">name</span><span class="sxs-lookup"><span data-stu-id="e44c9-308">name</span></span> | <span data-ttu-id="e44c9-309">Hello 연결 된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-309">Name of hello linked service.</span></span> | <span data-ttu-id="e44c9-310">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-310">Yes</span></span> | 
| <span data-ttu-id="e44c9-311">properties - type</span><span class="sxs-lookup"><span data-stu-id="e44c9-311">properties - type</span></span> | <span data-ttu-id="e44c9-312">Hello 연결 된 서비스 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-312">Type of hello linked service.</span></span> <span data-ttu-id="e44c9-313">예: Azure Storage, Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e44c9-313">For example: Azure Storage, Azure SQL Database.</span></span> |
| <span data-ttu-id="e44c9-314">typeProperties</span><span class="sxs-lookup"><span data-stu-id="e44c9-314">typeProperties</span></span> | <span data-ttu-id="e44c9-315">hello typeProperties 섹션에는 각 데이터 저장소에 대 한 서로 하거나 환경을 계산 하는 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-315">hello typeProperties section has elements that are different for each data store or compute environment.</span></span> <span data-ttu-id="e44c9-316">참조 [데이터 저장소](#datastores) 모든 hello 데이터 저장소 연결 된 서비스에 대 한 섹션 및 [환경 계산](#compute-environments) 모든 hello에 대 한 계산 연결 된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-316">See [data stores](#datastores) section for all hello data store linked services and [compute environments](#compute-environments) for all hello compute linked services</span></span> |   

## <a name="dataset"></a><span data-ttu-id="e44c9-317">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-317">Dataset</span></span> 
<span data-ttu-id="e44c9-318">Azure Data Factory의 데이터 집합은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-318">A dataset in Azure Data Factory is defined as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="e44c9-319">다음 표에 hello JSON 위에 hello에 대 한 속성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-319">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="e44c9-320">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-320">Property</span></span> | <span data-ttu-id="e44c9-321">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-321">Description</span></span> | <span data-ttu-id="e44c9-322">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-322">Required</span></span> | <span data-ttu-id="e44c9-323">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-323">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-324">name</span><span class="sxs-lookup"><span data-stu-id="e44c9-324">name</span></span> | <span data-ttu-id="e44c9-325">Hello 데이터 집합의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-325">Name of hello dataset.</span></span> <span data-ttu-id="e44c9-326">명명 규칙은 [Azure Data Factory - 명명 규칙](data-factory-naming-rules.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-326">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="e44c9-327">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-327">Yes</span></span> |<span data-ttu-id="e44c9-328">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-328">NA</span></span> |
| <span data-ttu-id="e44c9-329">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-329">type</span></span> | <span data-ttu-id="e44c9-330">hello 데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-330">Type of hello dataset.</span></span> <span data-ttu-id="e44c9-331">Azure Data Factory에서 지 원하는 hello 형식 중 하나를 지정 (예: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="e44c9-331">Specify one of hello types supported by Azure Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <span data-ttu-id="e44c9-332">참조 [데이터 저장소](#data-stores) 데이터 저장소 및 데이터 집합 형식 Data Factory에서 지 원하는 모든 hello에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-332">See [DATA STORES](#data-stores) section for all hello data stores and dataset types supported by Data Factory.</span></span> | 
| <span data-ttu-id="e44c9-333">structure</span><span class="sxs-lookup"><span data-stu-id="e44c9-333">structure</span></span> | <span data-ttu-id="e44c9-334">Hello 데이터 집합의 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-334">Schema of hello dataset.</span></span> <span data-ttu-id="e44c9-335">열, 해당 형식 등을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-335">It contains columns, their types, etc.</span></span> | <span data-ttu-id="e44c9-336">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-336">No</span></span> |<span data-ttu-id="e44c9-337">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-337">NA</span></span> |
| <span data-ttu-id="e44c9-338">typeProperties</span><span class="sxs-lookup"><span data-stu-id="e44c9-338">typeProperties</span></span> | <span data-ttu-id="e44c9-339">Toohello에 해당 하는 속성 유형을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-339">Properties corresponding toohello selected type.</span></span> <span data-ttu-id="e44c9-340">지원되는 형식 및 해당 속성은 [데이터 저장소](#data-stores) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-340">See [DATA STORES](#data-stores) section for supported types and their properties.</span></span> |<span data-ttu-id="e44c9-341">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-341">Yes</span></span> |<span data-ttu-id="e44c9-342">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-342">NA</span></span> |
| <span data-ttu-id="e44c9-343">external</span><span class="sxs-lookup"><span data-stu-id="e44c9-343">external</span></span> | <span data-ttu-id="e44c9-344">부울 여부 데이터 팩터리 파이프라인에서 명시적으로 데이터 집합은 생성 여부 toospecify를 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-344">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> |<span data-ttu-id="e44c9-345">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-345">No</span></span> |<span data-ttu-id="e44c9-346">false</span><span class="sxs-lookup"><span data-stu-id="e44c9-346">false</span></span> |
| <span data-ttu-id="e44c9-347">availability</span><span class="sxs-lookup"><span data-stu-id="e44c9-347">availability</span></span> | <span data-ttu-id="e44c9-348">창 또는 데이터 집합 프로덕션 hello에 대 한 모델을 조각화 하는 hello를 처리 하는 hello를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-348">Defines hello processing window or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="e44c9-349">모델을 조각화 하는 hello 데이터 집합에 대 한 세부 정보를 참조 하십시오. [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="e44c9-349">For details on hello dataset slicing model, see [Scheduling and Execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="e44c9-350">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-350">Yes</span></span> |<span data-ttu-id="e44c9-351">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-351">NA</span></span> |
| <span data-ttu-id="e44c9-352">policy</span><span class="sxs-lookup"><span data-stu-id="e44c9-352">policy</span></span> |<span data-ttu-id="e44c9-353">Hello 조건 또는 hello 데이터 집합 분할 영역 충족 해야 하는 hello 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-353">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="e44c9-354">세부 정보는 [데이터 집합 정책](#Policy) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-354">For details, see [Dataset Policy](#Policy) section.</span></span> |<span data-ttu-id="e44c9-355">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-355">No</span></span> |<span data-ttu-id="e44c9-356">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-356">NA</span></span> |

<span data-ttu-id="e44c9-357">각 열에 hello **구조** 섹션에서는 다음과 같은 속성 hello:</span><span class="sxs-lookup"><span data-stu-id="e44c9-357">Each column in hello **structure** section contains hello following properties:</span></span>

| <span data-ttu-id="e44c9-358">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-358">Property</span></span> | <span data-ttu-id="e44c9-359">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-359">Description</span></span> | <span data-ttu-id="e44c9-360">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-360">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-361">name</span><span class="sxs-lookup"><span data-stu-id="e44c9-361">name</span></span> |<span data-ttu-id="e44c9-362">Hello 열의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-362">Name of hello column.</span></span> |<span data-ttu-id="e44c9-363">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-363">Yes</span></span> |
| <span data-ttu-id="e44c9-364">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-364">type</span></span> |<span data-ttu-id="e44c9-365">Hello 열의 데이터 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-365">Data type of hello column.</span></span>  |<span data-ttu-id="e44c9-366">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-366">No</span></span> |
| <span data-ttu-id="e44c9-367">culture</span><span class="sxs-lookup"><span data-stu-id="e44c9-367">culture</span></span> |<span data-ttu-id="e44c9-368">.NET 기반 유형을 지정 하 고.NET 형식이 사용 되는 문화권 toobe `Datetime` 또는 `Datetimeoffset`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-368">.NET based culture toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="e44c9-369">기본값은 `en-us`입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-369">Default is `en-us`.</span></span> |<span data-ttu-id="e44c9-370">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-370">No</span></span> |
| <span data-ttu-id="e44c9-371">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-371">format</span></span> |<span data-ttu-id="e44c9-372">포맷 유형을 지정 하 고.NET 형식이 사용 되는 문자열 toobe `Datetime` 또는 `Datetimeoffset`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-372">Format string toobe used when type is specified and is .NET type `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="e44c9-373">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-373">No</span></span> |

<span data-ttu-id="e44c9-374">다음 예제는 hello, hello 데이터 집합에 3 개의 열이 `slicetimestamp`, `projectname`, 및 `pageviews` 유형의 일부인 및: 문자열, 문자열 및 Decimal 각각.</span><span class="sxs-lookup"><span data-stu-id="e44c9-374">In hello following example, hello dataset has three columns `slicetimestamp`, `projectname`, and `pageviews` and they are of type: String, String, and Decimal respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="e44c9-375">hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **가용성** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-375">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="e44c9-376">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-376">Property</span></span> | <span data-ttu-id="e44c9-377">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-377">Description</span></span> | <span data-ttu-id="e44c9-378">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-378">Required</span></span> | <span data-ttu-id="e44c9-379">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-379">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-380">frequency</span><span class="sxs-lookup"><span data-stu-id="e44c9-380">frequency</span></span> |<span data-ttu-id="e44c9-381">데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-381">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="e44c9-382"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="e44c9-382"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="e44c9-383">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-383">Yes</span></span> |<span data-ttu-id="e44c9-384">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-384">NA</span></span> |
| <span data-ttu-id="e44c9-385">interval</span><span class="sxs-lookup"><span data-stu-id="e44c9-385">interval</span></span> |<span data-ttu-id="e44c9-386">빈도 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-386">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="e44c9-387">"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-387">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="e44c9-388">설정 하는 경우는 시간 단위로 분할 되는 데이터 집합 toobe hello 필요, <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-388">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="e44c9-389"><b>참고</b>: 1 분으로 주파수를 지정 하면 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다</span><span class="sxs-lookup"><span data-stu-id="e44c9-389"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="e44c9-390">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-390">Yes</span></span> |<span data-ttu-id="e44c9-391">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-391">NA</span></span> |
| <span data-ttu-id="e44c9-392">style</span><span class="sxs-lookup"><span data-stu-id="e44c9-392">style</span></span> |<span data-ttu-id="e44c9-393">Hello 간격의 시작/끝 hello에 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-393">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="e44c9-394">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="e44c9-394">StartOfInterval</span></span></li><li><span data-ttu-id="e44c9-395">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="e44c9-395">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="e44c9-396">Frequency를 tooMonth를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 달의 마지막 날에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-396">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="e44c9-397">Hello 스타일 tooStartOfInterval을 설정 하는 경우에 월의 첫째 날으로 hello에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-397">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="e44c9-398">Frequency를 tooDay를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 지난 1 시간 동안 hello 하루 중에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-398">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="e44c9-399">Frequency를 tooHour를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 시간 hello 끝에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-399">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="e44c9-400">예를 들어, 오후 1 ~ 2 시 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-400">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="e44c9-401">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-401">No</span></span> |<span data-ttu-id="e44c9-402">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="e44c9-402">EndOfInterval</span></span> |
| <span data-ttu-id="e44c9-403">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="e44c9-403">anchorDateTime</span></span> |<span data-ttu-id="e44c9-404">스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-404">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="e44c9-405"><b>참고</b>: hello AnchorDateTime에 hello 빈도 보다 더 세부적인 날짜 부분이 경우 hello 더 세분화 된 부분은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-405"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="e44c9-406">예를 들어 경우 hello, <b>간격</b> 은 <b>매시간</b> (빈도: 시간 및 간격: 1) 및 hello <b>AnchorDateTime</b> 포함 <b>, 분, 초</b>다음 hello <b>, 분, 초</b> hello AnchorDateTime의 일부는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-406">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b> then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="e44c9-407">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-407">No</span></span> |<span data-ttu-id="e44c9-408">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="e44c9-408">01/01/0001</span></span> |
| <span data-ttu-id="e44c9-409">offset</span><span class="sxs-lookup"><span data-stu-id="e44c9-409">offset</span></span> |<span data-ttu-id="e44c9-410">어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-410">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="e44c9-411"><b>참고</b>: hello 결과 결합 된 hello shift anchorDateTime 및 offset을 모두를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-411"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="e44c9-412">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-412">No</span></span> |<span data-ttu-id="e44c9-413">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-413">NA</span></span> |

<span data-ttu-id="e44c9-414">가용성 섹션 뒤 hello 지정 hello 출력 데이터 집합의는 생성 된 시간별 (또는) 입력 데이터 집합은 1 시간 마다:</span><span class="sxs-lookup"><span data-stu-id="e44c9-414">hello following availability section specifies that hello output dataset is either produced hourly (or) input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="e44c9-415">hello **정책** 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-415">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

| <span data-ttu-id="e44c9-416">정책 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-416">Policy Name</span></span> | <span data-ttu-id="e44c9-417">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-417">Description</span></span> | <span data-ttu-id="e44c9-418">너무 적용</span><span class="sxs-lookup"><span data-stu-id="e44c9-418">Applied too</span></span>| <span data-ttu-id="e44c9-419">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-419">Required</span></span> | <span data-ttu-id="e44c9-420">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-420">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e44c9-421">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="e44c9-421">minimumSizeMB</span></span> |<span data-ttu-id="e44c9-422">Hello 데이터에 유효성을 검사 한 **Azure blob** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-422">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="e44c9-423">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="e44c9-423">Azure Blob</span></span> |<span data-ttu-id="e44c9-424">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-424">No</span></span> |<span data-ttu-id="e44c9-425">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-425">NA</span></span> |
| <span data-ttu-id="e44c9-426">minimumRows</span><span class="sxs-lookup"><span data-stu-id="e44c9-426">minimumRows</span></span> |<span data-ttu-id="e44c9-427">Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-427">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="e44c9-428">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e44c9-428">Azure SQL Database</span></span></li><li><span data-ttu-id="e44c9-429">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="e44c9-429">Azure Table</span></span></li></ul> |<span data-ttu-id="e44c9-430">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-430">No</span></span> |<span data-ttu-id="e44c9-431">해당 없음</span><span class="sxs-lookup"><span data-stu-id="e44c9-431">NA</span></span> |

<span data-ttu-id="e44c9-432">**예제:**</span><span class="sxs-lookup"><span data-stu-id="e44c9-432">**Example:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="e44c9-433">데이터 집합이 Azure Data Factory에서 생성되지 않는 한 **external**로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-433">Unless a dataset is being produced by Azure Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="e44c9-434">이 설정은 일반적으로 활동 또는 파이프라인 체인 사용 되지 않은 경우 파이프라인의 첫 번째 활동의 toohello 입력을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-434">This setting generally applies toohello inputs of first activity in a pipeline unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="e44c9-435">이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-435">Name</span></span> | <span data-ttu-id="e44c9-436">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-436">Description</span></span> | <span data-ttu-id="e44c9-437">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-437">Required</span></span> | <span data-ttu-id="e44c9-438">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-438">Default Value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-439">dataDelay</span><span class="sxs-lookup"><span data-stu-id="e44c9-439">dataDelay</span></span> |<span data-ttu-id="e44c9-440">시간 toodelay hello 가능 여부 확인 hello hello slice를 지정 하는 hello에 대 한 외부 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-440">Time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="e44c9-441">예를 들어 매시간 hello 데이터를 사용할 수, hello 검사 toosee hello 외부 데이터를 사용할 수 있으며 해당 조각이 hello dataDelay를 사용 하 여 준비 지연 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-441">For example, if hello data is available hourly, hello check toosee hello external data is available and hello corresponding slice is Ready can be delayed by using dataDelay.</span></span><br/><br/><span data-ttu-id="e44c9-442">만 toohello를 현재 시간 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-442">Only applies toohello present time.</span></span>  <span data-ttu-id="e44c9-443">예를 들어 지금 바로 오후 1시 이므로이 값은 10 분 hello 유효성 검사 오후 1 시 10 분에 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-443">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="e44c9-444">이 설정은 지난 hello에서 분할 영역에는 영향을 주지 (분할 영역 조각 종료 시간 + dataDelay < 이제) 지연 없이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-444">This setting does not affect slices in hello past (slices with Slice End Time + dataDelay < Now) are processed without any delay.</span></span><br/><br/><span data-ttu-id="e44c9-445">23:59 시간 필요 toospecified hello를 사용 하 여 보다 큰 시간 `day.hours:minutes:seconds` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-445">Time greater than 23:59 hours need toospecified using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="e44c9-446">예를 들어 toospecify 24 시간 동안 사용 하지 않는 24시: 00입니다. 나타내는 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-446">For example, toospecify 24 hours, don't use 24:00:00; instead, use 1.00:00:00.</span></span> <span data-ttu-id="e44c9-447">24:00:00을 사용하면 24일(24.00:00:00)로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-447">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="e44c9-448">1일 4시간의 경우 1:04:00:00을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-448">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="e44c9-449">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-449">No</span></span> |<span data-ttu-id="e44c9-450">0</span><span class="sxs-lookup"><span data-stu-id="e44c9-450">0</span></span> |
| <span data-ttu-id="e44c9-451">retryInterval</span><span class="sxs-lookup"><span data-stu-id="e44c9-451">retryInterval</span></span> |<span data-ttu-id="e44c9-452">hello 대기는 실패 및 hello 다음 다시 시도 사이의 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-452">hello wait time between a failure and hello next retry attempt.</span></span> <span data-ttu-id="e44c9-453">Try 실패할 경우 retryInterval 후 hello 다음 시도가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-453">If a try fails, hello next try is after retryInterval.</span></span> <br/><br/><span data-ttu-id="e44c9-454">지금 바로 오후 1시 이면 hello 첫 번째 시도 시작 하기.</span><span class="sxs-lookup"><span data-stu-id="e44c9-454">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="e44c9-455">Hello 기간 toocomplete hello 첫 번째 유효성 검사 1 분 이며 hello 작업이 실패 했습니다 hello 다음 재시도에 않은 경우에 1시 + 1 분 (기간) + 1 분 (다시 시도 간격) = 오후 1시 02분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-455">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1 min (duration) + 1 min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="e44c9-456">지난 hello에 조각에 대 한 지연 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-456">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="e44c9-457">hello 재시도 즉시 전파 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-457">hello retry happens immediately.</span></span> |<span data-ttu-id="e44c9-458">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-458">No</span></span> |<span data-ttu-id="e44c9-459">00:01:00 (1분)</span><span class="sxs-lookup"><span data-stu-id="e44c9-459">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="e44c9-460">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-460">retryTimeout</span></span> |<span data-ttu-id="e44c9-461">각 다시 시도 대 한 hello 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-461">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="e44c9-462">이 속성을 설정 하는 경우 too10 분 hello 유효성 검사 요구 toobe 10 분 이내에 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-462">If this property is set too10 minutes, hello validation needs toobe completed within 10 minutes.</span></span> <span data-ttu-id="e44c9-463">10 분 tooperform hello 유효성 검사 보다 시간이 오래 걸리는 경우 제한 시간이 초과 hello에 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-463">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="e44c9-464">Hello 유효성 검사에 대 한 모든 시도 시간이 초과 되 면 hello 조각 TimedOut으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-464">If all attempts for hello validation times out, hello slice is marked as TimedOut.</span></span> |<span data-ttu-id="e44c9-465">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-465">No</span></span> |<span data-ttu-id="e44c9-466">00:10:00 (10분)</span><span class="sxs-lookup"><span data-stu-id="e44c9-466">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="e44c9-467">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="e44c9-467">maximumRetry</span></span> |<span data-ttu-id="e44c9-468">횟수 toocheck hello 외부 데이터의 가용성을 hello에 대 한입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-468">Number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="e44c9-469">hello 허용 최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-469">hello allowed maximum value is 10.</span></span> |<span data-ttu-id="e44c9-470">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-470">No</span></span> |<span data-ttu-id="e44c9-471">3</span><span class="sxs-lookup"><span data-stu-id="e44c9-471">3</span></span> |


## <a name="data-stores"></a><span data-ttu-id="e44c9-472">데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="e44c9-472">DATA STORES</span></span>
<span data-ttu-id="e44c9-473">hello [연결 된 서비스](#linked-service) 일반적인 tooall 유형의 연결 된 서비스 JSON 요소에 대 한 설명 섹션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-473">hello [Linked service](#linked-service) section provided descriptions for JSON elements that are common tooall types of linked services.</span></span> <span data-ttu-id="e44c9-474">이 섹션에서는 JSON 요소를 특정 tooeach 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-474">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="e44c9-475">hello [Dataset](#dataset) JSON 요소를 일반적인 tooall 유형의 데이터 집합에 대 한 설명 섹션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-475">hello [Dataset](#dataset) section provided descriptions for JSON elements that are common tooall types of datasets.</span></span> <span data-ttu-id="e44c9-476">이 섹션에서는 JSON 요소를 특정 tooeach 데이터 저장소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-476">This section provides details about JSON elements that are specific tooeach data store.</span></span>

<span data-ttu-id="e44c9-477">hello [활동](#activity) JSON 요소를 일반적인 tooall 유형의 활동에 대 한 설명 섹션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-477">hello [Activity](#activity) section provided descriptions for JSON elements that are common tooall types of activities.</span></span> <span data-ttu-id="e44c9-478">이 섹션에서는 특정 tooeach 데이터 저장소는 복사 작업에는 원본/싱크로 사용 하는 경우 JSON 요소에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-478">This section provides details about JSON elements that are specific tooeach data store when it is used as a source/sink in a copy activity.</span></span>  

<span data-ttu-id="e44c9-479">Hello 저장소 연결 된 서비스, 데이터 집합에 대 한 toosee hello JSON 스키마에 관심이 및 소스/hello 복사 작업에 대 한 싱크 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-479">Click hello link for hello store you are interested in toosee hello JSON schemas for linked service, dataset, and hello source/sink for hello copy activity.</span></span>

| <span data-ttu-id="e44c9-480">Category</span><span class="sxs-lookup"><span data-stu-id="e44c9-480">Category</span></span> | <span data-ttu-id="e44c9-481">데이터 저장소</span><span class="sxs-lookup"><span data-stu-id="e44c9-481">Data store</span></span> 
|:--- |:--- |
| <span data-ttu-id="e44c9-482">**Azure**</span><span class="sxs-lookup"><span data-stu-id="e44c9-482">**Azure**</span></span> |[<span data-ttu-id="e44c9-483">Azure Blob 저장소</span><span class="sxs-lookup"><span data-stu-id="e44c9-483">Azure Blob storage</span></span>](#azure-blob-storage) |
| &nbsp; |[<span data-ttu-id="e44c9-484">Azure 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="e44c9-484">Azure Data Lake Store</span></span>](#azure-datalake-store) |
| &nbsp; |[<span data-ttu-id="e44c9-485">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e44c9-485">Azure Cosmos DB</span></span>](#azure-cosmos-db) |
| &nbsp; |[<span data-ttu-id="e44c9-486">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e44c9-486">Azure SQL Database</span></span>](#azure-sql-database) |
| &nbsp; |[<span data-ttu-id="e44c9-487">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e44c9-487">Azure SQL Data Warehouse</span></span>](#azure-sql-data-warehouse) |
| &nbsp; |[<span data-ttu-id="e44c9-488">Azure 검색</span><span class="sxs-lookup"><span data-stu-id="e44c9-488">Azure Search</span></span>](#azure-search) |
| &nbsp; |[<span data-ttu-id="e44c9-489">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="e44c9-489">Azure Table storage</span></span>](#azure-table-storage) |
| <span data-ttu-id="e44c9-490">**데이터베이스**</span><span class="sxs-lookup"><span data-stu-id="e44c9-490">**Databases**</span></span> |[<span data-ttu-id="e44c9-491">Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="e44c9-491">Amazon Redshift</span></span>](#amazon-redshift) |
| &nbsp; |[<span data-ttu-id="e44c9-492">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="e44c9-492">IBM DB2</span></span>](#ibm-db2) |
| &nbsp; |[<span data-ttu-id="e44c9-493">MySQL</span><span class="sxs-lookup"><span data-stu-id="e44c9-493">MySQL</span></span>](#mysql) |
| &nbsp; |[<span data-ttu-id="e44c9-494">Oracle</span><span class="sxs-lookup"><span data-stu-id="e44c9-494">Oracle</span></span>](#oracle) |
| &nbsp; |[<span data-ttu-id="e44c9-495">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e44c9-495">PostgreSQL</span></span>](#postgresql) |
| &nbsp; |[<span data-ttu-id="e44c9-496">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="e44c9-496">SAP Business Warehouse</span></span>](#sap-business-warehouse) |
| &nbsp; |[<span data-ttu-id="e44c9-497">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e44c9-497">SAP HANA</span></span>](#sap-hana) |
| &nbsp; |[<span data-ttu-id="e44c9-498">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e44c9-498">SQL Server</span></span>](#sql-server) |
| &nbsp; |[<span data-ttu-id="e44c9-499">Sybase</span><span class="sxs-lookup"><span data-stu-id="e44c9-499">Sybase</span></span>](#sybase) |
| &nbsp; |[<span data-ttu-id="e44c9-500">Teradata</span><span class="sxs-lookup"><span data-stu-id="e44c9-500">Teradata</span></span>](#teradata) |
| <span data-ttu-id="e44c9-501">**NoSQL**</span><span class="sxs-lookup"><span data-stu-id="e44c9-501">**NoSQL**</span></span> |[<span data-ttu-id="e44c9-502">Cassandra</span><span class="sxs-lookup"><span data-stu-id="e44c9-502">Cassandra</span></span>](#cassandra) |
| &nbsp; |[<span data-ttu-id="e44c9-503">MongoDB</span><span class="sxs-lookup"><span data-stu-id="e44c9-503">MongoDB</span></span>](#mongodb) |
| <span data-ttu-id="e44c9-504">**파일**</span><span class="sxs-lookup"><span data-stu-id="e44c9-504">**File**</span></span> |[<span data-ttu-id="e44c9-505">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="e44c9-505">Amazon S3</span></span>](#amazon-s3) |
| &nbsp; |[<span data-ttu-id="e44c9-506">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="e44c9-506">File System</span></span>](#file-system) |
| &nbsp; |[<span data-ttu-id="e44c9-507">FTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-507">FTP</span></span>](#ftp) |
| &nbsp; |[<span data-ttu-id="e44c9-508">HDFS</span><span class="sxs-lookup"><span data-stu-id="e44c9-508">HDFS</span></span>](#hdfs) |
| &nbsp; |[<span data-ttu-id="e44c9-509">SFTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-509">SFTP</span></span>](#sftp) |
| <span data-ttu-id="e44c9-510">**기타**</span><span class="sxs-lookup"><span data-stu-id="e44c9-510">**Others**</span></span> |[<span data-ttu-id="e44c9-511">HTTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-511">HTTP</span></span>](#http) |
| &nbsp; |[<span data-ttu-id="e44c9-512">OData</span><span class="sxs-lookup"><span data-stu-id="e44c9-512">OData</span></span>](#odata) |
| &nbsp; |[<span data-ttu-id="e44c9-513">ODBC</span><span class="sxs-lookup"><span data-stu-id="e44c9-513">ODBC</span></span>](#odbc) |
| &nbsp; |[<span data-ttu-id="e44c9-514">Salesforce</span><span class="sxs-lookup"><span data-stu-id="e44c9-514">Salesforce</span></span>](#salesforce) |
| &nbsp; |[<span data-ttu-id="e44c9-515">웹 테이블</span><span class="sxs-lookup"><span data-stu-id="e44c9-515">Web Table</span></span>](#web-table) |

## <a name="azure-blob-storage"></a><span data-ttu-id="e44c9-516">데이터 이동</span><span class="sxs-lookup"><span data-stu-id="e44c9-516">Azure Blob Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-517">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-517">Linked service</span></span>
<span data-ttu-id="e44c9-518">연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-518">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e44c9-519">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-519">Azure Storage Linked Service</span></span>
<span data-ttu-id="e44c9-520">toolink hello를 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리 **계정 키**, Azure 저장소 연결 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-520">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="e44c9-521">toodefine Azure 저장소 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureStorage**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-521">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="e44c9-522">그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-522">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-523">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-523">Property</span></span> | <span data-ttu-id="e44c9-524">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-524">Description</span></span> | <span data-ttu-id="e44c9-525">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-525">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-526">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-526">connectionString</span></span> |<span data-ttu-id="e44c9-527">Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-527">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-528">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-528">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="e44c9-529">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-529">Example</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="e44c9-530">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-530">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="e44c9-531">hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-531">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="e44c9-532">Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-532">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="e44c9-533">toolink 공유 액세스 서명을 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리는 Azure 저장소 SAS 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-533">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="e44c9-534">연결 된 서비스를 집합 hello Azure 저장소 SAS toodefine **형식** hello 연결 서비스 너무**AzureStorageSas**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-534">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="e44c9-535">그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-535">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="e44c9-536">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-536">Property</span></span> | <span data-ttu-id="e44c9-537">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-537">Description</span></span> | <span data-ttu-id="e44c9-538">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-538">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-539">sasUri</span><span class="sxs-lookup"><span data-stu-id="e44c9-539">sasUri</span></span> |<span data-ttu-id="e44c9-540">Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-540">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="e44c9-541">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-541">Yes</span></span> |

##### <a name="example"></a><span data-ttu-id="e44c9-542">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-542">Example</span></span>

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

<span data-ttu-id="e44c9-543">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Blob Storage 커넥터](data-factory-azure-blob-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-543">For more information about these linked services, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-544">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-544">Dataset</span></span>
<span data-ttu-id="e44c9-545">toodefine 된 Azure Blob 데이터 집합을 집합 hello **형식** hello 데이터 집합의 너무**AzureBlob**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-545">toodefine an Azure Blob dataset, set hello **type** of hello dataset too**AzureBlob**.</span></span> <span data-ttu-id="e44c9-546">그런 다음 hello 다음과 같은 Azure Blob hello에서 특정 속성을 지정 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-546">Then, specify hello following Azure Blob specific properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-547">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-547">Property</span></span> | <span data-ttu-id="e44c9-548">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-548">Description</span></span> | <span data-ttu-id="e44c9-549">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-549">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-550">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-550">folderPath</span></span> |<span data-ttu-id="e44c9-551">경로 toohello 컨테이너 및 blob 저장소 hello에에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-551">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="e44c9-552">예제: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="e44c9-552">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="e44c9-553">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-553">Yes</span></span> |
| <span data-ttu-id="e44c9-554">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-554">fileName</span></span> |<span data-ttu-id="e44c9-555">Hello blob 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-555">Name of hello blob.</span></span> <span data-ttu-id="e44c9-556">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-556">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="e44c9-557">에 파일 이름, hello 작업 (복사본 포함) 작동을 지정한 경우에 특정 Blob을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-557">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="e44c9-558">파일 이름을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath에 모든 Blob을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-558">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="e44c9-559">Hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,: 데이터입니다. <Guid>.txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="e44c9-559">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e44c9-560">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-560">No</span></span> |
| <span data-ttu-id="e44c9-561">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-561">partitionedBy</span></span> |<span data-ttu-id="e44c9-562">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-562">partitionedBy is an optional property.</span></span> <span data-ttu-id="e44c9-563">사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-563">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="e44c9-564">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-564">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-565">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-565">No</span></span> |
| <span data-ttu-id="e44c9-566">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-566">format</span></span> | <span data-ttu-id="e44c9-567">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-567">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-568">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-568">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-569">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-569">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-570">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-570">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-571">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-571">No</span></span> |
| <span data-ttu-id="e44c9-572">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-572">compression</span></span> | <span data-ttu-id="e44c9-573">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-573">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-574">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-574">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-575">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-575">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-576">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-576">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-577">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-577">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-578">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-578">Example</span></span>

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


<span data-ttu-id="e44c9-579">자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-579">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) article.</span></span>

### <a name="blobsource-in-copy-activity"></a><span data-ttu-id="e44c9-580">복사 활동의 BlobSource</span><span class="sxs-lookup"><span data-stu-id="e44c9-580">BlobSource in Copy Activity</span></span>
<span data-ttu-id="e44c9-581">Azure Blob 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**BlobSource**, 다음 hello에 대 한 속성을 지정 하 고 * * 소스 * * 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-581">If you are copying data from an Azure Blob Storage, set hello **source type** of hello copy activity too**BlobSource**, and specify following properties in hello **source **section:</span></span>

| <span data-ttu-id="e44c9-582">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-582">Property</span></span> | <span data-ttu-id="e44c9-583">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-583">Description</span></span> | <span data-ttu-id="e44c9-584">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-584">Allowed values</span></span> | <span data-ttu-id="e44c9-585">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-585">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-586">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-586">recursive</span></span> |<span data-ttu-id="e44c9-587">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-587">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-588">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="e44c9-588">True (default value), False</span></span> |<span data-ttu-id="e44c9-589">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-589">No</span></span> |

#### <a name="example-blobsource"></a><span data-ttu-id="e44c9-590">예제: BlobSource**</span><span class="sxs-lookup"><span data-stu-id="e44c9-590">Example: BlobSource**</span></span>
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
### <a name="blobsink-in-copy-activity"></a><span data-ttu-id="e44c9-591">복사 활동의 BlobSink</span><span class="sxs-lookup"><span data-stu-id="e44c9-591">BlobSink in Copy Activity</span></span>
<span data-ttu-id="e44c9-592">데이터 tooan Azure Blob 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**BlobSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-592">If you are copying data tooan Azure Blob Storage, set hello **sink type** of hello copy activity too**BlobSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-593">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-593">Property</span></span> | <span data-ttu-id="e44c9-594">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-594">Description</span></span> | <span data-ttu-id="e44c9-595">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-595">Allowed values</span></span> | <span data-ttu-id="e44c9-596">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-596">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-597">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e44c9-597">copyBehavior</span></span> |<span data-ttu-id="e44c9-598">파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-598">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="e44c9-599"><b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-599"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="e44c9-600">hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-600">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="e44c9-601"><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일에에서 있는 hello 먼저 대상 폴더의 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-601"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="e44c9-602">hello 대상 파일에는 자동 생성 된 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-602">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="e44c9-603"><b>(기본값) MergeFiles:</b> hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-603"><b>MergeFiles (default):</b> merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="e44c9-604">Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-604">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="e44c9-605">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-605">No</span></span> |

#### <a name="example-blobsink"></a><span data-ttu-id="e44c9-606">예제: BlobSink</span><span class="sxs-lookup"><span data-stu-id="e44c9-606">Example: BlobSink</span></span>

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

<span data-ttu-id="e44c9-607">자세한 내용은 [Azure Blob 커넥터](data-factory-azure-blob-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-607">For more information, see [Azure Blob connector](data-factory-azure-blob-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-data-lake-store"></a><span data-ttu-id="e44c9-608">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e44c9-608">Azure Data Lake Store</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-609">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-609">Linked service</span></span>
<span data-ttu-id="e44c9-610">Azure 데이터 레이크 저장소 연결 서비스 toodefine 집합 hello 유형의 hello 연결 된 서비스 너무**AzureDataLakeStore**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-610">toodefine an Azure Data Lake Store linked service, set hello type of hello linked service too**AzureDataLakeStore**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-611">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-611">Property</span></span> | <span data-ttu-id="e44c9-612">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-612">Description</span></span> | <span data-ttu-id="e44c9-613">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-613">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-614">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-614">type</span></span> | <span data-ttu-id="e44c9-615">hello type 속성 설정 해야 합니다: **AzureDataLakeStore**</span><span class="sxs-lookup"><span data-stu-id="e44c9-615">hello type property must be set to: **AzureDataLakeStore**</span></span> | <span data-ttu-id="e44c9-616">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-616">Yes</span></span> |
| <span data-ttu-id="e44c9-617">dataLakeStoreUri</span><span class="sxs-lookup"><span data-stu-id="e44c9-617">dataLakeStoreUri</span></span> | <span data-ttu-id="e44c9-618">Hello Azure 데이터 레이크 저장소 계정에 대 한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-618">Specify information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="e44c9-619">형식에 따라 hello에: `https://[accountname].azuredatalakestore.net/webhdfs/v1` 또는 `adl://[accountname].azuredatalakestore.net/`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-619">It is in hello following format: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="e44c9-620">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-620">Yes</span></span> |
| <span data-ttu-id="e44c9-621">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e44c9-621">subscriptionId</span></span> | <span data-ttu-id="e44c9-622">Azure 구독 Id toowhich 데이터 레이크 저장소 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-622">Azure subscription Id toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="e44c9-623">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="e44c9-623">Required for sink</span></span> |
| <span data-ttu-id="e44c9-624">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e44c9-624">resourceGroupName</span></span> | <span data-ttu-id="e44c9-625">Azure 리소스 그룹 이름 toowhich 데이터 레이크 저장소 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-625">Azure resource group name toowhich Data Lake Store belongs.</span></span> | <span data-ttu-id="e44c9-626">싱크에 필요</span><span class="sxs-lookup"><span data-stu-id="e44c9-626">Required for sink</span></span> |
| <span data-ttu-id="e44c9-627">servicePrincipalId</span><span class="sxs-lookup"><span data-stu-id="e44c9-627">servicePrincipalId</span></span> | <span data-ttu-id="e44c9-628">Hello 응용 프로그램의 클라이언트 ID를 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-628">Specify hello application's client ID.</span></span> | <span data-ttu-id="e44c9-629">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-629">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="e44c9-630">servicePrincipalKey</span><span class="sxs-lookup"><span data-stu-id="e44c9-630">servicePrincipalKey</span></span> | <span data-ttu-id="e44c9-631">Hello 응용 프로그램의 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-631">Specify hello application's key.</span></span> | <span data-ttu-id="e44c9-632">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-632">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="e44c9-633">tenant</span><span class="sxs-lookup"><span data-stu-id="e44c9-633">tenant</span></span> | <span data-ttu-id="e44c9-634">응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-634">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="e44c9-635">Hello Azure 포털의 hello 오른쪽 위 모서리에 hello 마우스 호버 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-635">You can retrieve it by hovering hello mouse in hello top-right corner of hello Azure portal.</span></span> | <span data-ttu-id="e44c9-636">예(서비스 주체 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-636">Yes (for service principal authentication)</span></span> |
| <span data-ttu-id="e44c9-637">권한 부여</span><span class="sxs-lookup"><span data-stu-id="e44c9-637">authorization</span></span> | <span data-ttu-id="e44c9-638">클릭 **Authorize** hello 단추 **데이터 팩터리 편집기** hello 자동 생성 된 권한 부여 URL toothis 속성에 할당 하 여 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-638">Click **Authorize** button in hello **Data Factory Editor** and enter your credential that assigns hello auto-generated authorization URL toothis property.</span></span> | <span data-ttu-id="e44c9-639">예(사용자 자격 증명 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-639">Yes (for user credential authentication)</span></span>|
| <span data-ttu-id="e44c9-640">sessionId</span><span class="sxs-lookup"><span data-stu-id="e44c9-640">sessionId</span></span> | <span data-ttu-id="e44c9-641">Hello OAuth 권한 부여 세션에서 OAuth 세션 id입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-641">OAuth session id from hello OAuth authorization session.</span></span> <span data-ttu-id="e44c9-642">각 세션 ID는 고유하고 한 번만 사용될 수 있으며 </span><span class="sxs-lookup"><span data-stu-id="e44c9-642">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="e44c9-643">이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-643">This setting is automatically generated when you use Data Factory Editor.</span></span> | <span data-ttu-id="e44c9-644">예(사용자 자격 증명 인증의 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-644">Yes (for user credential authentication)</span></span> |

#### <a name="example-using-service-principal-authentication"></a><span data-ttu-id="e44c9-645">예제: 서비스 주체 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-645">Example: using service principal authentication</span></span>
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

#### <a name="example-using-user-credential-authentication"></a><span data-ttu-id="e44c9-646">예제: 사용자 자격 증명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-646">Example: using user credential authentication</span></span>
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

<span data-ttu-id="e44c9-647">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-647">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-648">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-648">Dataset</span></span>
<span data-ttu-id="e44c9-649">Azure 데이터 레이크 저장소에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureDataLakeStore**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-649">toodefine an Azure Data Lake Store dataset, set hello **type** of hello dataset too**AzureDataLakeStore**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-650">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-650">Property</span></span> | <span data-ttu-id="e44c9-651">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-651">Description</span></span> | <span data-ttu-id="e44c9-652">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-652">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-653">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-653">folderPath</span></span> |<span data-ttu-id="e44c9-654">Hello Azure 데이터 레이크의 경로 toohello 컨테이너 및 폴더를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-654">Path toohello container and folder in hello Azure Data Lake store.</span></span> |<span data-ttu-id="e44c9-655">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-655">Yes</span></span> |
| <span data-ttu-id="e44c9-656">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-656">fileName</span></span> |<span data-ttu-id="e44c9-657">Hello Azure 데이터 레이크 저장소의 hello 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-657">Name of hello file in hello Azure Data Lake store.</span></span> <span data-ttu-id="e44c9-658">fileName은 선택 사항이며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-658">fileName is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="e44c9-659">이름을 지정 하는 경우 (복사본 포함) hello 활동 hello 특정 파일에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-659">If you specify a filename, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="e44c9-660">FileName을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath의 모든 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-660">When fileName is not specified, Copy includes all files in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="e44c9-661">Hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,: 데이터입니다. <Guid>.txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="e44c9-661">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e44c9-662">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-662">No</span></span> |
| <span data-ttu-id="e44c9-663">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-663">partitionedBy</span></span> |<span data-ttu-id="e44c9-664">partitionedBy는 선택적 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-664">partitionedBy is an optional property.</span></span> <span data-ttu-id="e44c9-665">사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-665">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="e44c9-666">예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-666">For example, folderPath can be parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-667">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-667">No</span></span> |
| <span data-ttu-id="e44c9-668">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-668">format</span></span> | <span data-ttu-id="e44c9-669">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-669">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-670">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-670">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-671">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-671">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-672">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-672">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-673">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-673">No</span></span> |
| <span data-ttu-id="e44c9-674">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-674">compression</span></span> | <span data-ttu-id="e44c9-675">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-675">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-676">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-676">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-677">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-677">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-678">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-678">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-679">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-679">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-680">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-680">Example</span></span>
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

<span data-ttu-id="e44c9-681">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-681">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-data-lake-store-source-in-copy-activity"></a><span data-ttu-id="e44c9-682">복사 활동의 Azure Data Lake Store 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-682">Azure Data Lake Store Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-683">Azure 데이터 레이크 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**AzureDataLakeStoreSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**  섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-683">If you are copying data from an Azure Data Lake Store, set hello **source type** of hello copy activity too**AzureDataLakeStoreSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="e44c9-684">**AzureDataLakeStoreSource** hello 다음과 같은 속성을 지 원하는 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-684">**AzureDataLakeStoreSource** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="e44c9-685">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-685">Property</span></span> | <span data-ttu-id="e44c9-686">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-686">Description</span></span> | <span data-ttu-id="e44c9-687">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-687">Allowed values</span></span> | <span data-ttu-id="e44c9-688">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-688">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-689">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-689">recursive</span></span> |<span data-ttu-id="e44c9-690">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-690">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-691">True(기본값), False</span><span class="sxs-lookup"><span data-stu-id="e44c9-691">True (default value), False</span></span> |<span data-ttu-id="e44c9-692">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-692">No</span></span> |

#### <a name="example-azuredatalakestoresource"></a><span data-ttu-id="e44c9-693">예제: AzureDataLakeStoreSource</span><span class="sxs-lookup"><span data-stu-id="e44c9-693">Example: AzureDataLakeStoreSource</span></span>

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

<span data-ttu-id="e44c9-694">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-694">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span>

### <a name="azure-data-lake-store-sink-in-copy-activity"></a><span data-ttu-id="e44c9-695">복사 활동의 Azure Data Lake Store 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-695">Azure Data Lake Store Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-696">데이터 tooan Azure 데이터 레이크 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureDataLakeStoreSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-696">If you are copying data tooan Azure Data Lake Store, set hello **sink type** of hello copy activity too**AzureDataLakeStoreSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-697">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-697">Property</span></span> | <span data-ttu-id="e44c9-698">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-698">Description</span></span> | <span data-ttu-id="e44c9-699">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-699">Allowed values</span></span> | <span data-ttu-id="e44c9-700">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-700">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-701">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e44c9-701">copyBehavior</span></span> |<span data-ttu-id="e44c9-702">Hello 복사 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-702">Specifies hello copy behavior.</span></span> |<span data-ttu-id="e44c9-703"><b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-703"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="e44c9-704">hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-704">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="e44c9-705"><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-705"><b>FlattenHierarchy</b>: all files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="e44c9-706">hello 대상 파일은 자동 생성 된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-706">hello target files are created with auto generated name.</span></span><br/><br/><span data-ttu-id="e44c9-707"><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-707"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="e44c9-708">Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-708">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="e44c9-709">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-709">No</span></span> |

#### <a name="example-azuredatalakestoresink"></a><span data-ttu-id="e44c9-710">예제: AzureDataLakeStoreSink</span><span class="sxs-lookup"><span data-stu-id="e44c9-710">Example: AzureDataLakeStoreSink</span></span>
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

<span data-ttu-id="e44c9-711">자세한 내용은 [Azure Data Lake Store 커넥터](data-factory-azure-datalake-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-711">For more information, see [Azure Data Lake Store connector](data-factory-azure-datalake-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-cosmos-db"></a><span data-ttu-id="e44c9-712">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e44c9-712">Azure Cosmos DB</span></span>  

### <a name="linked-service"></a><span data-ttu-id="e44c9-713">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-713">Linked service</span></span>
<span data-ttu-id="e44c9-714">연결 된 서비스를 집합 hello Azure Cosmos DB toodefine **형식** hello 연결 서비스 너무**DocumentDb**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-714">toodefine an Azure Cosmos DB linked service, set hello **type** of hello linked service too**DocumentDb**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-715">**속성**</span><span class="sxs-lookup"><span data-stu-id="e44c9-715">**Property**</span></span> | <span data-ttu-id="e44c9-716">**설명**</span><span class="sxs-lookup"><span data-stu-id="e44c9-716">**Description**</span></span> | <span data-ttu-id="e44c9-717">**필수**</span><span class="sxs-lookup"><span data-stu-id="e44c9-717">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-718">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-718">connectionString</span></span> |<span data-ttu-id="e44c9-719">Tooconnect tooAzure Cosmos DB 데이터베이스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-719">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="e44c9-720">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-720">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-721">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-721">Example</span></span>

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
<span data-ttu-id="e44c9-722">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-722">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-723">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-723">Dataset</span></span>
<span data-ttu-id="e44c9-724">toodefine Azure Cosmos DB dataset 집합 hello **형식** hello 데이터 집합의 너무**DocumentDbCollection**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-724">toodefine an Azure Cosmos DB dataset, set hello **type** of hello dataset too**DocumentDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-725">**속성**</span><span class="sxs-lookup"><span data-stu-id="e44c9-725">**Property**</span></span> | <span data-ttu-id="e44c9-726">**설명**</span><span class="sxs-lookup"><span data-stu-id="e44c9-726">**Description**</span></span> | <span data-ttu-id="e44c9-727">**필수**</span><span class="sxs-lookup"><span data-stu-id="e44c9-727">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-728">collectionName</span><span class="sxs-lookup"><span data-stu-id="e44c9-728">collectionName</span></span> |<span data-ttu-id="e44c9-729">Hello Azure Cosmos DB 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-729">Name of hello Azure Cosmos DB collection.</span></span> |<span data-ttu-id="e44c9-730">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-730">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-731">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-731">Example</span></span>

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
<span data-ttu-id="e44c9-732">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-732">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#dataset-properties) article.</span></span>

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a><span data-ttu-id="e44c9-733">복사 작업에서 Azure Cosmos DB 컬렉션 원본</span><span class="sxs-lookup"><span data-stu-id="e44c9-733">Azure Cosmos DB Collection Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-734">Azure Cosmos DB에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**DocumentDbCollectionSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-734">If you are copying data from an Azure Cosmos DB, set hello **source type** of hello copy activity too**DocumentDbCollectionSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-735">**속성**</span><span class="sxs-lookup"><span data-stu-id="e44c9-735">**Property**</span></span> | <span data-ttu-id="e44c9-736">**설명**</span><span class="sxs-lookup"><span data-stu-id="e44c9-736">**Description**</span></span> | <span data-ttu-id="e44c9-737">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="e44c9-737">**Allowed values**</span></span> | <span data-ttu-id="e44c9-738">**필수**</span><span class="sxs-lookup"><span data-stu-id="e44c9-738">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-739">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-739">query</span></span> |<span data-ttu-id="e44c9-740">Hello tooread 데이터 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-740">Specify hello query tooread data.</span></span> |<span data-ttu-id="e44c9-741">Azure Cosmos DB에서 지원하는 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-741">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="e44c9-742">예: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="e44c9-742">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="e44c9-743">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-743">No</span></span> <br/><br/><span data-ttu-id="e44c9-744">지정 하지 않으면 실행 되는 SQL 문을 hello:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="e44c9-744">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="e44c9-745">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e44c9-745">nestingSeparator</span></span> |<span data-ttu-id="e44c9-746">문서 hello 특수 문자 tooindicate 중첩</span><span class="sxs-lookup"><span data-stu-id="e44c9-746">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="e44c9-747">모든 character입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-747">Any character.</span></span> <br/><br/><span data-ttu-id="e44c9-748">Azure Cosmos DB는 중첩된 구조를 허용하는 JSON 문서용 NoSQL 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-748">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="e44c9-749">Azure 데이터 팩터리는 nestingSeparator 통해 사용자 toodenote 계층 구조를 사용 하면 "."</span><span class="sxs-lookup"><span data-stu-id="e44c9-749">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="e44c9-750">위의 예제 안녕하세요에.</span><span class="sxs-lookup"><span data-stu-id="e44c9-750">in hello above examples.</span></span> <span data-ttu-id="e44c9-751">Hello 구분 기호 hello 복사 작업에서는 생성 3 명의 자식 요소가 있는 hello "Name" 개체 첫 번째, 중간 및 마지막를 따라 too"Name.First", "Name.Middle" 및 "Name.Last" hello에 테이블 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-751">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="e44c9-752">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-752">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-753">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-753">Example</span></span>

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

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a><span data-ttu-id="e44c9-754">복사 작업의 Azure Cosmos DB 컬렉션 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-754">Azure Cosmos DB Collection Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-755">데이터 tooAzure Cosmos DB 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**DocumentDbCollectionSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-755">If you are copying data tooAzure Cosmos DB, set hello **sink type** of hello copy activity too**DocumentDbCollectionSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-756">**속성**</span><span class="sxs-lookup"><span data-stu-id="e44c9-756">**Property**</span></span> | <span data-ttu-id="e44c9-757">**설명**</span><span class="sxs-lookup"><span data-stu-id="e44c9-757">**Description**</span></span> | <span data-ttu-id="e44c9-758">**허용되는 값**</span><span class="sxs-lookup"><span data-stu-id="e44c9-758">**Allowed values**</span></span> | <span data-ttu-id="e44c9-759">**필수**</span><span class="sxs-lookup"><span data-stu-id="e44c9-759">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-760">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e44c9-760">nestingSeparator</span></span> |<span data-ttu-id="e44c9-761">Hello 원본 열 이름 tooindicate 중첩 문서에에서 특수 문자 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-761">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="e44c9-762">예를 들어 위의: `Name.First` hello 출력 테이블 생성 하는 hello Cosmos DB 문서의 JSON 구조를 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="e44c9-762">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="e44c9-763">"Name": {</span><span class="sxs-lookup"><span data-stu-id="e44c9-763">"Name": {</span></span><br/>    <span data-ttu-id="e44c9-764">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="e44c9-764">"First": "John"</span></span><br/><span data-ttu-id="e44c9-765">},</span><span class="sxs-lookup"><span data-stu-id="e44c9-765">},</span></span> |<span data-ttu-id="e44c9-766">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-766">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="e44c9-767">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-767">Default value is `.` (dot).</span></span> |<span data-ttu-id="e44c9-768">문자는 사용 되는 tooseparate 중첩 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-768">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="e44c9-769">기본값은 `.`.(점)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-769">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="e44c9-770">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-770">writeBatchSize</span></span> |<span data-ttu-id="e44c9-771">TooAzure Cosmos DB 서비스 toocreate 문서를 요청 하는 병렬의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-771">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="e44c9-772">이 속성을 사용 하 여 Azure Cosmos DB에서 데이터를 복사할 때 hello 성능을 미세 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-772">You can fine-tune hello performance when copying data to/from Azure Cosmos DB by using this property.</span></span> <span data-ttu-id="e44c9-773">더 많은 병렬 요청 tooAzure Cosmos DB 보내지므로 writeBatchSize를 늘리면 성능이 향상을 기대할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-773">You can expect a better performance when you increase writeBatchSize because more parallel requests tooAzure Cosmos DB are sent.</span></span> <span data-ttu-id="e44c9-774">그러나 조정을 tooavoid 해야 hello 오류 메시지가 발생할 수 있습니다: "요청 빈도가 높습니다."입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-774">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="e44c9-775">제한은 문서의 크기, 문서에서 용어의 수, 대상 컬렉션의 인덱싱 정책 등 여러 가지 요인으로 결정됩니다. 복사 작업을 사용할 수 있습니다 더 나은 컬렉션 (예를 들어 S3) toohave hello 사용 가능한 대부분 처리량 (2,500 단위 수/초를 요청 하는 데 사용).</span><span class="sxs-lookup"><span data-stu-id="e44c9-775">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (for example, S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="e44c9-776">Integer</span><span class="sxs-lookup"><span data-stu-id="e44c9-776">Integer</span></span> |<span data-ttu-id="e44c9-777">아니요(기본값: 5)</span><span class="sxs-lookup"><span data-stu-id="e44c9-777">No (default: 5)</span></span> |
| <span data-ttu-id="e44c9-778">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-778">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-779">대기 시간이 초과 되기 전에 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-779">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="e44c9-780">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-780">timespan</span></span><br/><br/> <span data-ttu-id="e44c9-781">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="e44c9-781">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e44c9-782">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-782">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-783">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-783">Example</span></span>

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
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
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

<span data-ttu-id="e44c9-784">자세한 내용은 [Azure Cosmos DB 커넥터](data-factory-azure-documentdb-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-784">For more information, see [Azure Cosmos DB connector](data-factory-azure-documentdb-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-sql-database"></a><span data-ttu-id="e44c9-785">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e44c9-785">Azure SQL Database</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-786">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-786">Linked service</span></span>
<span data-ttu-id="e44c9-787">toodefine Azure SQL 데이터베이스에 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureSqlDatabase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-787">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-788">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-788">Property</span></span> | <span data-ttu-id="e44c9-789">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-789">Description</span></span> | <span data-ttu-id="e44c9-790">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-790">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-791">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-791">connectionString</span></span> |<span data-ttu-id="e44c9-792">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-792">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-793">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-793">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-794">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-794">Example</span></span>
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

<span data-ttu-id="e44c9-795">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-795">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-796">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-796">Dataset</span></span>
<span data-ttu-id="e44c9-797">Azure SQL 데이터베이스에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSqlTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-797">toodefine an Azure SQL Database dataset, set hello **type** of hello dataset too**AzureSqlTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-798">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-798">Property</span></span> | <span data-ttu-id="e44c9-799">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-799">Description</span></span> | <span data-ttu-id="e44c9-800">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-800">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-801">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-801">tableName</span></span> |<span data-ttu-id="e44c9-802">Hello 테이블 또는 뷰의 연결 된 서비스는 hello Azure SQL 데이터베이스 인스턴스의 이름이 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-802">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="e44c9-803">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-803">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-804">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-804">Example</span></span>

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
<span data-ttu-id="e44c9-805">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-805">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="e44c9-806">복사 활동의 SQL 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-806">SQL Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-807">Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-807">If you are copying data from an Azure SQL Database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-808">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-808">Property</span></span> | <span data-ttu-id="e44c9-809">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-809">Description</span></span> | <span data-ttu-id="e44c9-810">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-810">Allowed values</span></span> | <span data-ttu-id="e44c9-811">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-811">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-812">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e44c9-812">sqlReaderQuery</span></span> |<span data-ttu-id="e44c9-813">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-813">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-814">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-814">SQL query string.</span></span> <span data-ttu-id="e44c9-815">예: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="e44c9-815">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-816">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-816">No</span></span> |
| <span data-ttu-id="e44c9-817">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-817">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="e44c9-818">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-818">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="e44c9-819">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-819">Name of hello stored procedure.</span></span> |<span data-ttu-id="e44c9-820">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-820">No</span></span> |
| <span data-ttu-id="e44c9-821">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-821">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-822">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-822">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e44c9-823">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-823">Name/value pairs.</span></span> <span data-ttu-id="e44c9-824">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-824">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e44c9-825">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-825">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-826">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-826">Example</span></span>

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
<span data-ttu-id="e44c9-827">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-827">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="e44c9-828">복사 활동의 SQL 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-828">SQL Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-829">데이터 tooAzure SQL 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-829">If you are copying data tooAzure SQL Database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-830">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-830">Property</span></span> | <span data-ttu-id="e44c9-831">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-831">Description</span></span> | <span data-ttu-id="e44c9-832">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-832">Allowed values</span></span> | <span data-ttu-id="e44c9-833">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-833">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-834">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-834">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-835">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-835">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e44c9-836">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-836">timespan</span></span><br/><br/> <span data-ttu-id="e44c9-837">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="e44c9-837">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e44c9-838">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-838">No</span></span> |
| <span data-ttu-id="e44c9-839">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-839">writeBatchSize</span></span> |<span data-ttu-id="e44c9-840">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-840">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e44c9-841">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="e44c9-841">Integer (number of rows)</span></span> |<span data-ttu-id="e44c9-842">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="e44c9-842">No (default: 10000)</span></span> |
| <span data-ttu-id="e44c9-843">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e44c9-843">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e44c9-844">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-844">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="e44c9-845">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-845">A query statement.</span></span> |<span data-ttu-id="e44c9-846">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-846">No</span></span> |
| <span data-ttu-id="e44c9-847">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e44c9-847">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e44c9-848">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-848">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="e44c9-849">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-849">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e44c9-850">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-850">No</span></span> |
| <span data-ttu-id="e44c9-851">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-851">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="e44c9-852">Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-852">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="e44c9-853">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-853">Name of hello stored procedure.</span></span> |<span data-ttu-id="e44c9-854">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-854">No</span></span> |
| <span data-ttu-id="e44c9-855">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-855">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-856">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-856">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e44c9-857">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-857">Name/value pairs.</span></span> <span data-ttu-id="e44c9-858">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-858">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e44c9-859">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-859">No</span></span> |
| <span data-ttu-id="e44c9-860">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="e44c9-860">sqlWriterTableType</span></span> |<span data-ttu-id="e44c9-861">Hello 저장 프로시저에 사용 하는 테이블 형식 이름 toobe를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-861">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="e44c9-862">복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-862">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="e44c9-863">저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-863">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="e44c9-864">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-864">A table type name.</span></span> |<span data-ttu-id="e44c9-865">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-865">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-866">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-866">Example</span></span>

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

<span data-ttu-id="e44c9-867">자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-867">For more information, see [Azure SQL connector](data-factory-azure-sql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="e44c9-868">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="e44c9-868">Azure SQL Data Warehouse</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-869">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-869">Linked service</span></span>
<span data-ttu-id="e44c9-870">연결 된 서비스를 집합 hello Azure SQL 데이터 웨어하우스 toodefine **형식** hello 연결 서비스 너무**AzureSqlDW**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-870">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-871">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-871">Property</span></span> | <span data-ttu-id="e44c9-872">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-872">Description</span></span> | <span data-ttu-id="e44c9-873">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-873">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-874">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-874">connectionString</span></span> |<span data-ttu-id="e44c9-875">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-875">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-876">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-876">Yes</span></span> |



#### <a name="example"></a><span data-ttu-id="e44c9-877">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-877">Example</span></span>

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

<span data-ttu-id="e44c9-878">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-878">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-879">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-879">Dataset</span></span>
<span data-ttu-id="e44c9-880">Azure SQL 데이터 웨어하우스 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSqlDWTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-880">toodefine an Azure SQL Data Warehouse dataset, set hello **type** of hello dataset too**AzureSqlDWTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-881">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-881">Property</span></span> | <span data-ttu-id="e44c9-882">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-882">Description</span></span> | <span data-ttu-id="e44c9-883">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-883">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-884">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-884">tableName</span></span> |<span data-ttu-id="e44c9-885">Hello 테이블 또는 뷰의 연결 된 서비스 hello hello Azure SQL 데이터 웨어하우스 데이터베이스의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-885">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="e44c9-886">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-886">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-887">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-887">Example</span></span>

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

<span data-ttu-id="e44c9-888">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-888">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-dw-source-in-copy-activity"></a><span data-ttu-id="e44c9-889">복사 활동의 SQL DW 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-889">SQL DW Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-890">Azure SQL 데이터 웨어하우스 로부터 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlDWSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-890">If you are copying data from Azure SQL Data Warehouse, set hello **source type** of hello copy activity too**SqlDWSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-891">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-891">Property</span></span> | <span data-ttu-id="e44c9-892">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-892">Description</span></span> | <span data-ttu-id="e44c9-893">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-893">Allowed values</span></span> | <span data-ttu-id="e44c9-894">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-894">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-895">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e44c9-895">sqlReaderQuery</span></span> |<span data-ttu-id="e44c9-896">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-896">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-897">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-897">SQL query string.</span></span> <span data-ttu-id="e44c9-898">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-898">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-899">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-899">No</span></span> |
| <span data-ttu-id="e44c9-900">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-900">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="e44c9-901">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-901">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="e44c9-902">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-902">Name of hello stored procedure.</span></span> |<span data-ttu-id="e44c9-903">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-903">No</span></span> |
| <span data-ttu-id="e44c9-904">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-904">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-905">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-905">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e44c9-906">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-906">Name/value pairs.</span></span> <span data-ttu-id="e44c9-907">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-907">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e44c9-908">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-908">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-909">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-909">Example</span></span>

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

<span data-ttu-id="e44c9-910">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-910">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-dw-sink-in-copy-activity"></a><span data-ttu-id="e44c9-911">복사 활동의 SQL DW 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-911">SQL DW Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-912">SQL 데이터 웨어하우스 데이터 tooAzure 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlDWSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-912">If you are copying data tooAzure SQL Data Warehouse, set hello **sink type** of hello copy activity too**SqlDWSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-913">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-913">Property</span></span> | <span data-ttu-id="e44c9-914">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-914">Description</span></span> | <span data-ttu-id="e44c9-915">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-915">Allowed values</span></span> | <span data-ttu-id="e44c9-916">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-916">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-917">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e44c9-917">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e44c9-918">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-918">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="e44c9-919">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-919">A query statement.</span></span> |<span data-ttu-id="e44c9-920">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-920">No</span></span> |
| <span data-ttu-id="e44c9-921">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="e44c9-921">allowPolyBase</span></span> |<span data-ttu-id="e44c9-922">나타냅니다 여부 BULKINSERT 메커니즘 대신 toouse PolyBase (있는 경우).</span><span class="sxs-lookup"><span data-stu-id="e44c9-922">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="e44c9-923">**PolyBase를 사용 하는 권장 방법은 tooload 데이터를 SQL 데이터 웨어하우스에 하는 hello입니다.**</span><span class="sxs-lookup"><span data-stu-id="e44c9-923">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> |<span data-ttu-id="e44c9-924">True</span><span class="sxs-lookup"><span data-stu-id="e44c9-924">True</span></span> <br/><span data-ttu-id="e44c9-925">False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-925">False (default)</span></span> |<span data-ttu-id="e44c9-926">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-926">No</span></span> |
| <span data-ttu-id="e44c9-927">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="e44c9-927">polyBaseSettings</span></span> |<span data-ttu-id="e44c9-928">속성 때 hello 지정할 수 있는 그룹을 **allowPolybase** 너무 속성이**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-928">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="e44c9-929">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-929">No</span></span> |
| <span data-ttu-id="e44c9-930">rejectValue</span><span class="sxs-lookup"><span data-stu-id="e44c9-930">rejectValue</span></span> |<span data-ttu-id="e44c9-931">Hello 쿼리가 실패 하기 전에 거부 될 수 있는 행의 hello 개수 또는 비율을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-931">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="e44c9-932">Hello에 대 한 옵션을 거부 hello PolyBase에 대해 자세히 알아보려면 **인수** 섹션 [CREATE EXTERNAL TABLE (TRANSACT-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-932">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="e44c9-933">0(기본값), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="e44c9-933">0 (default), 1, 2, …</span></span> |<span data-ttu-id="e44c9-934">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-934">No</span></span> |
| <span data-ttu-id="e44c9-935">rejectType</span><span class="sxs-lookup"><span data-stu-id="e44c9-935">rejectType</span></span> |<span data-ttu-id="e44c9-936">리터럴 값 또는 백분율 hello rejectValue 옵션이 지정 되었는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-936">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="e44c9-937">값(기본값), 백분율</span><span class="sxs-lookup"><span data-stu-id="e44c9-937">Value (default), Percentage</span></span> |<span data-ttu-id="e44c9-938">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-938">No</span></span> |
| <span data-ttu-id="e44c9-939">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="e44c9-939">rejectSampleValue</span></span> |<span data-ttu-id="e44c9-940">PolyBase hello 다시 거부 된 행의 hello 비율을 계산 하기 전에 행 tooretrieve hello 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-940">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="e44c9-941">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="e44c9-941">1, 2, …</span></span> |<span data-ttu-id="e44c9-942">예. **rejectType**이 **백분율**인 경우</span><span class="sxs-lookup"><span data-stu-id="e44c9-942">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="e44c9-943">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="e44c9-943">useTypeDefault</span></span> |<span data-ttu-id="e44c9-944">PolyBase hello 텍스트 파일에서 데이터를 검색 하는 경우 toohandle 누락 값의 텍스트 파일을 구분 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-944">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="e44c9-945">hello 인수 섹션에서이 속성에 대 한 자세한 [CREATE EXTERNAL FILE FORMAT (Transact SQL)](https://msdn.microsoft.com/library/dn935026.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-945">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="e44c9-946">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-946">True, False (default)</span></span> |<span data-ttu-id="e44c9-947">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-947">No</span></span> |
| <span data-ttu-id="e44c9-948">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-948">writeBatchSize</span></span> |<span data-ttu-id="e44c9-949">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="e44c9-949">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="e44c9-950">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="e44c9-950">Integer (number of rows)</span></span> |<span data-ttu-id="e44c9-951">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="e44c9-951">No (default: 10000)</span></span> |
| <span data-ttu-id="e44c9-952">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-952">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-953">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-953">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e44c9-954">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-954">timespan</span></span><br/><br/> <span data-ttu-id="e44c9-955">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="e44c9-955">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e44c9-956">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-956">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-957">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-957">Example</span></span>

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

<span data-ttu-id="e44c9-958">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-958">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="azure-search"></a><span data-ttu-id="e44c9-959">Azure 검색</span><span class="sxs-lookup"><span data-stu-id="e44c9-959">Azure Search</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-960">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-960">Linked service</span></span>
<span data-ttu-id="e44c9-961">연결 된 서비스를 집합 hello Azure 검색 toodefine **형식** hello 연결 서비스 너무**AzureSearch**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-961">toodefine an Azure Search linked service, set hello **type** of hello linked service too**AzureSearch**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-962">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-962">Property</span></span> | <span data-ttu-id="e44c9-963">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-963">Description</span></span> | <span data-ttu-id="e44c9-964">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-964">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="e44c9-965">url</span><span class="sxs-lookup"><span data-stu-id="e44c9-965">url</span></span> | <span data-ttu-id="e44c9-966">Hello Azure 검색 서비스에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-966">URL for hello Azure Search service.</span></span> | <span data-ttu-id="e44c9-967">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-967">Yes</span></span> |
| <span data-ttu-id="e44c9-968">key</span><span class="sxs-lookup"><span data-stu-id="e44c9-968">key</span></span> | <span data-ttu-id="e44c9-969">Hello Azure 검색 서비스에 대 한 관리자 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-969">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="e44c9-970">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-970">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-971">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-971">Example</span></span>

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

<span data-ttu-id="e44c9-972">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-972">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-973">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-973">Dataset</span></span>
<span data-ttu-id="e44c9-974">Azure 검색 된 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureSearchIndex**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 :</span><span class="sxs-lookup"><span data-stu-id="e44c9-974">toodefine an Azure Search dataset, set hello **type** of hello dataset too**AzureSearchIndex**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-975">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-975">Property</span></span> | <span data-ttu-id="e44c9-976">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-976">Description</span></span> | <span data-ttu-id="e44c9-977">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-977">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="e44c9-978">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-978">type</span></span> | <span data-ttu-id="e44c9-979">너무 hello 유형 속성을 설정 해야**AzureSearchIndex**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-979">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="e44c9-980">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-980">Yes</span></span> |
| <span data-ttu-id="e44c9-981">indexName</span><span class="sxs-lookup"><span data-stu-id="e44c9-981">indexName</span></span> | <span data-ttu-id="e44c9-982">Hello Azure 검색 인덱스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-982">Name of hello Azure Search index.</span></span> <span data-ttu-id="e44c9-983">데이터 팩터리 hello 인덱스가 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-983">Data Factory does not create hello index.</span></span> <span data-ttu-id="e44c9-984">hello 인덱스 Azure 검색에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-984">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="e44c9-985">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-985">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-986">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-986">Example</span></span>

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

<span data-ttu-id="e44c9-987">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-987">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#dataset-properties) article.</span></span>

### <a name="azure-search-index-sink-in-copy-activity"></a><span data-ttu-id="e44c9-988">복사 활동의 Azure Search 인덱스 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-988">Azure Search Index Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-989">데이터 tooan Azure 검색 인덱스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureSearchIndexSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-989">If you are copying data tooan Azure Search index, set hello **sink type** of hello copy activity too**AzureSearchIndexSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-990">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-990">Property</span></span> | <span data-ttu-id="e44c9-991">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-991">Description</span></span> | <span data-ttu-id="e44c9-992">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-992">Allowed values</span></span> | <span data-ttu-id="e44c9-993">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-993">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="e44c9-994">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="e44c9-994">WriteBehavior</span></span> | <span data-ttu-id="e44c9-995">Toomerge 또는 교체 때 문서에에서 이미 있는지 hello 인덱스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-995">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> | <span data-ttu-id="e44c9-996">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-996">Merge (default)</span></span><br/><span data-ttu-id="e44c9-997">업로드</span><span class="sxs-lookup"><span data-stu-id="e44c9-997">Upload</span></span>| <span data-ttu-id="e44c9-998">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-998">No</span></span> |
| <span data-ttu-id="e44c9-999">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-999">WriteBatchSize</span></span> | <span data-ttu-id="e44c9-1000">WriteBatchSize hello 버퍼 크기에 이르면 hello Azure 검색 인덱스에 데이터를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1000">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> | <span data-ttu-id="e44c9-1001">too1이 1, 000입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1001">1 too1,000.</span></span> <span data-ttu-id="e44c9-1002">기본값은 1,000입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1002">Default value is 1000.</span></span> | <span data-ttu-id="e44c9-1003">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1003">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1004">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1004">Example</span></span>

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

<span data-ttu-id="e44c9-1005">자세한 내용은 [Azure Search 커넥터](data-factory-azure-search-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1005">For more information, see [Azure Search connector](data-factory-azure-search-connector.md#copy-activity-properties) article.</span></span>

## <a name="azure-table-storage"></a><span data-ttu-id="e44c9-1006">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="e44c9-1006">Azure Table Storage</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1007">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1007">Linked service</span></span>
<span data-ttu-id="e44c9-1008">연결된 서비스에는 두 가지 유형, 즉 Azure Storage 연결된 서비스와 Azure Storage SAS 연결된 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1008">There are two types of linked services: Azure Storage linked service and Azure Storage SAS linked service.</span></span>

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="e44c9-1009">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1009">Azure Storage Linked Service</span></span>
<span data-ttu-id="e44c9-1010">toolink hello를 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리 **계정 키**, Azure 저장소 연결 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1010">toolink your Azure storage account tooa data factory by using hello **account key**, create an Azure Storage linked service.</span></span> <span data-ttu-id="e44c9-1011">toodefine Azure 저장소 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureStorage**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1011">toodefine an Azure Storage linked service, set hello **type** of hello linked service too**AzureStorage**.</span></span> <span data-ttu-id="e44c9-1012">그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1012">Then, you can specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1013">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1013">Property</span></span> | <span data-ttu-id="e44c9-1014">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1014">Description</span></span> | <span data-ttu-id="e44c9-1015">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1015">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-1016">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-1016">type</span></span> |<span data-ttu-id="e44c9-1017">hello type 속성 설정 해야 합니다: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="e44c9-1017">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="e44c9-1018">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1018">Yes</span></span> |
| <span data-ttu-id="e44c9-1019">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-1019">connectionString</span></span> |<span data-ttu-id="e44c9-1020">Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1020">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-1021">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1021">Yes</span></span> |

<span data-ttu-id="e44c9-1022">**예제:**</span><span class="sxs-lookup"><span data-stu-id="e44c9-1022">**Example:**</span></span>  

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

#### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="e44c9-1023">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1023">Azure Storage SAS Linked Service</span></span>
<span data-ttu-id="e44c9-1024">hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1024">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="e44c9-1025">Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1025">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="e44c9-1026">toolink 공유 액세스 서명을 사용 하 여 Azure 저장소 계정 tooa 데이터 팩터리는 Azure 저장소 SAS 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1026">toolink your Azure storage account tooa data factory by using Shared Access Signature, create an Azure Storage SAS linked service.</span></span> <span data-ttu-id="e44c9-1027">연결 된 서비스를 집합 hello Azure 저장소 SAS toodefine **형식** hello 연결 서비스 너무**AzureStorageSas**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1027">toodefine an Azure Storage SAS linked service, set hello **type** of hello linked service too**AzureStorageSas**.</span></span> <span data-ttu-id="e44c9-1028">그런 다음, 다음 속성 hello에 지정할 수 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1028">Then, you can specify following properties in hello **typeProperties** section:</span></span>   

| <span data-ttu-id="e44c9-1029">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1029">Property</span></span> | <span data-ttu-id="e44c9-1030">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1030">Description</span></span> | <span data-ttu-id="e44c9-1031">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1031">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-1032">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-1032">type</span></span> |<span data-ttu-id="e44c9-1033">hello type 속성 설정 해야 합니다: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="e44c9-1033">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="e44c9-1034">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1034">Yes</span></span> |
| <span data-ttu-id="e44c9-1035">sasUri</span><span class="sxs-lookup"><span data-stu-id="e44c9-1035">sasUri</span></span> |<span data-ttu-id="e44c9-1036">Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1036">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span> |<span data-ttu-id="e44c9-1037">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1037">Yes</span></span> |

<span data-ttu-id="e44c9-1038">**예제:**</span><span class="sxs-lookup"><span data-stu-id="e44c9-1038">**Example:**</span></span>

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

<span data-ttu-id="e44c9-1039">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1039">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1040">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1040">Dataset</span></span>
<span data-ttu-id="e44c9-1041">Azure 테이블에서 데이터 집합 toodefine 집합 hello **형식** hello 데이터 집합의 너무**AzureTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1041">toodefine an Azure Table dataset, set hello **type** of hello dataset too**AzureTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1042">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1042">Property</span></span> | <span data-ttu-id="e44c9-1043">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1043">Description</span></span> | <span data-ttu-id="e44c9-1044">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1044">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1045">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1045">tableName</span></span> |<span data-ttu-id="e44c9-1046">연결 된 서비스는 hello Azure 테이블 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1046">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="e44c9-1047">예.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1047">Yes.</span></span> <span data-ttu-id="e44c9-1048">를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1048">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="e44c9-1049">Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1049">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1050">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1050">Example</span></span>

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

<span data-ttu-id="e44c9-1051">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1051">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#dataset-properties) article.</span></span> 

### <a name="azure-table-source-in-copy-activity"></a><span data-ttu-id="e44c9-1052">복사 활동의 Azure Table 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1052">Azure Table Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1053">Azure 테이블 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**AzureTableSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1053">If you are copying data from Azure Table Storage, set hello **source type** of hello copy activity too**AzureTableSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1054">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1054">Property</span></span> | <span data-ttu-id="e44c9-1055">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1055">Description</span></span> | <span data-ttu-id="e44c9-1056">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1056">Allowed values</span></span> | <span data-ttu-id="e44c9-1057">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1057">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1058">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="e44c9-1058">azureTableSourceQuery</span></span> |<span data-ttu-id="e44c9-1059">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1059">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1060">Azure 테이블 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1060">Azure table query string.</span></span> <span data-ttu-id="e44c9-1061">Hello 다음 섹션의 예제를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1061">See examples in hello next section.</span></span> |<span data-ttu-id="e44c9-1062">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1062">No.</span></span> <span data-ttu-id="e44c9-1063">를 azureTableSourceQuery 없이 tableName을 지정 하는 경우 hello 테이블의 모든 레코드가 복사한 toohello 대상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1063">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="e44c9-1064">Hello 쿼리를 충족 하는 hello 테이블에서 레코드는 azureTableSourceQuery도 지정 되어 경우 복사한 toohello 대상 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1064">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="e44c9-1065">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="e44c9-1065">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="e44c9-1066">테이블의 hello 예외를 무시할지 존재 하지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1066">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="e44c9-1067">TRUE</span><span class="sxs-lookup"><span data-stu-id="e44c9-1067">TRUE</span></span><br/><span data-ttu-id="e44c9-1068">FALSE</span><span class="sxs-lookup"><span data-stu-id="e44c9-1068">FALSE</span></span> |<span data-ttu-id="e44c9-1069">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1069">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1070">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1070">Example</span></span>

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

<span data-ttu-id="e44c9-1071">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1071">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

### <a name="azure-table-sink-in-copy-activity"></a><span data-ttu-id="e44c9-1072">복사 활동의 Azure Table 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-1072">Azure Table Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-1073">데이터 tooAzure 테이블 저장소를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**AzureTableSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1073">If you are copying data tooAzure Table Storage, set hello **sink type** of hello copy activity too**AzureTableSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-1074">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1074">Property</span></span> | <span data-ttu-id="e44c9-1075">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1075">Description</span></span> | <span data-ttu-id="e44c9-1076">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1076">Allowed values</span></span> | <span data-ttu-id="e44c9-1077">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1077">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1078">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="e44c9-1078">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="e44c9-1079">기본 파티션 키 값 hello 싱크에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1079">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="e44c9-1080">문자열 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1080">A string value.</span></span> |<span data-ttu-id="e44c9-1081">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1081">No</span></span> |
| <span data-ttu-id="e44c9-1082">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1082">azureTablePartitionKeyName</span></span> |<span data-ttu-id="e44c9-1083">해당 값은 파티션 키로 사용 하는 hello 열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1083">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="e44c9-1084">지정 하지 않으면 AzureTableDefaultPartitionKeyValue hello 파티션 키로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1084">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="e44c9-1085">열 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1085">A column name.</span></span> |<span data-ttu-id="e44c9-1086">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1086">No</span></span> |
| <span data-ttu-id="e44c9-1087">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1087">azureTableRowKeyName</span></span> |<span data-ttu-id="e44c9-1088">해당 열 값은 행 키로 사용 되는 hello 열의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1088">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="e44c9-1089">지정하지 않으면 각 행에 GUID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1089">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="e44c9-1090">열 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1090">A column name.</span></span> |<span data-ttu-id="e44c9-1091">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1091">No</span></span> |
| <span data-ttu-id="e44c9-1092">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1092">azureTableInsertType</span></span> |<span data-ttu-id="e44c9-1093">Azure 테이블에 hello 모드 tooinsert 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1093">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="e44c9-1094">이 속성은 파티션 및 행 키 일치 하는 hello 출력 테이블의 기존 행에는 값을 바꾸거나 병합 있는지 여부를 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1094">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="e44c9-1095">이러한 설정을 (병합 및 대체) 작동 방법에 대해 toolearn 참조 [삽입 또는 병합 엔터티](https://msdn.microsoft.com/library/azure/hh452241.aspx) 및 [삽입 또는 교체 엔터티](https://msdn.microsoft.com/library/azure/hh452242.aspx) 항목.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1095">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="e44c9-1096">두 옵션 모두 hello 입력에 존재 하지 않는 hello 출력 테이블에 행을 삭제 및 hello 테이블 수준이 아닌 hello 행 수준에서이 설정을 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1096">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="e44c9-1097">병합(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1097">merge (default)</span></span><br/><span data-ttu-id="e44c9-1098">바꾸기</span><span class="sxs-lookup"><span data-stu-id="e44c9-1098">replace</span></span> |<span data-ttu-id="e44c9-1099">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1099">No</span></span> |
| <span data-ttu-id="e44c9-1100">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-1100">writeBatchSize</span></span> |<span data-ttu-id="e44c9-1101">Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우에 hello Azure 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1101">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="e44c9-1102">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1102">Integer (number of rows)</span></span> |<span data-ttu-id="e44c9-1103">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1103">No (default: 10000)</span></span> |
| <span data-ttu-id="e44c9-1104">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-1104">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-1105">Hello writeBatchSize 또는 writebatchtimeout에 도달 하는 경우 hello Azure 테이블에 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="e44c9-1105">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="e44c9-1106">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-1106">timespan</span></span><br/><br/><span data-ttu-id="e44c9-1107">예: "00:20:00"(20분)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1107">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="e44c9-1108">더 (기본 toostorage 클라이언트 기본 제한 시간 값인 90 초)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1108">No (Default toostorage client default timeout value 90 sec)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1109">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1109">Example</span></span>

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
<span data-ttu-id="e44c9-1110">이러한 연결된 서비스에 대한 자세한 내용은 [Azure Table Storage 커넥터](data-factory-azure-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1110">For more information about these linked services, see [Azure Table Storage connector](data-factory-azure-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="amazon-redshift"></a><span data-ttu-id="e44c9-1111">Amazon RedShift</span><span class="sxs-lookup"><span data-stu-id="e44c9-1111">Amazon RedShift</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1112">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1112">Linked service</span></span>
<span data-ttu-id="e44c9-1113">연결 된 서비스를 집합 hello toodefine Amazon Redshift **형식** hello 연결 서비스 너무**AmazonRedshift**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1113">toodefine an Amazon Redshift linked service, set hello **type** of hello linked service too**AmazonRedshift**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1114">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1114">Property</span></span> | <span data-ttu-id="e44c9-1115">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1115">Description</span></span> | <span data-ttu-id="e44c9-1116">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1116">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1117">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1117">server</span></span> |<span data-ttu-id="e44c9-1118">Hello Amazon Redshift 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1118">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="e44c9-1119">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1119">Yes</span></span> |
| <span data-ttu-id="e44c9-1120">포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-1120">port</span></span> |<span data-ttu-id="e44c9-1121">Amazon Redshift 서버 hello hello TCP 포트 수가 hello toolisten를 사용 하 여 클라이언트 연결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1121">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="e44c9-1122">기본값이 없음: 5439</span><span class="sxs-lookup"><span data-stu-id="e44c9-1122">No, default value: 5439</span></span> |
| <span data-ttu-id="e44c9-1123">database</span><span class="sxs-lookup"><span data-stu-id="e44c9-1123">database</span></span> |<span data-ttu-id="e44c9-1124">Hello Amazon Redshift 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1124">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="e44c9-1125">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1125">Yes</span></span> |
| <span data-ttu-id="e44c9-1126">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1126">username</span></span> |<span data-ttu-id="e44c9-1127">Access toohello 데이터베이스를 갖고 있는 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1127">Name of user who has access toohello database.</span></span> |<span data-ttu-id="e44c9-1128">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1128">Yes</span></span> |
| <span data-ttu-id="e44c9-1129">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1129">password</span></span> |<span data-ttu-id="e44c9-1130">Hello 사용자 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1130">Password for hello user account.</span></span> |<span data-ttu-id="e44c9-1131">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1131">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1132">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1132">Example</span></span>

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

<span data-ttu-id="e44c9-1133">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#linked-service-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1133">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1134">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1134">Dataset</span></span>
<span data-ttu-id="e44c9-1135">Amazon Redshift 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1135">toodefine an Amazon Redshift dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1136">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1136">Property</span></span> | <span data-ttu-id="e44c9-1137">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1137">Description</span></span> | <span data-ttu-id="e44c9-1138">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1138">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1139">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1139">tableName</span></span> |<span data-ttu-id="e44c9-1140">연결 된 서비스는 hello Amazon Redshift 데이터베이스에 대 한 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1140">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="e44c9-1141">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1141">No (if **query** of **RelationalSource** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-1142">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1142">Example</span></span>

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
<span data-ttu-id="e44c9-1143">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#dataset-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1143">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1144">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1144">Relational Source in Copy Activity</span></span> 
<span data-ttu-id="e44c9-1145">Amazon Redshift에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1145">If you are copying data from Amazon Redshift, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1146">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1146">Property</span></span> | <span data-ttu-id="e44c9-1147">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1147">Description</span></span> | <span data-ttu-id="e44c9-1148">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1148">Allowed values</span></span> | <span data-ttu-id="e44c9-1149">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1149">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1150">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1150">query</span></span> |<span data-ttu-id="e44c9-1151">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1151">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1152">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1152">SQL query string.</span></span> <span data-ttu-id="e44c9-1153">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1153">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-1154">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1154">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1155">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1155">Example</span></span>

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
<span data-ttu-id="e44c9-1156">자세한 내용은 [Amazon Redshift 커넥터](#data-factory-amazon-redshift-connector.md#copy-activity-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1156">For more information, see [Amazon Redshift connector](#data-factory-amazon-redshift-connector.md#copy-activity-properties) article.</span></span>

## <a name="ibm-db2"></a><span data-ttu-id="e44c9-1157">IBM DB2</span><span class="sxs-lookup"><span data-stu-id="e44c9-1157">IBM DB2</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1158">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1158">Linked service</span></span>
<span data-ttu-id="e44c9-1159">연결 된 서비스를 집합 hello toodefine IBM DB2 **형식** hello 연결 서비스 너무**OnPremisesDB2**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1159">toodefine an IBM DB2 linked service, set hello **type** of hello linked service too**OnPremisesDB2**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1160">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1160">Property</span></span> | <span data-ttu-id="e44c9-1161">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1161">Description</span></span> | <span data-ttu-id="e44c9-1162">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1163">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1163">server</span></span> |<span data-ttu-id="e44c9-1164">Hello DB2 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1164">Name of hello DB2 server.</span></span> |<span data-ttu-id="e44c9-1165">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1165">Yes</span></span> |
| <span data-ttu-id="e44c9-1166">database</span><span class="sxs-lookup"><span data-stu-id="e44c9-1166">database</span></span> |<span data-ttu-id="e44c9-1167">Hello DB2 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1167">Name of hello DB2 database.</span></span> |<span data-ttu-id="e44c9-1168">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1168">Yes</span></span> |
| <span data-ttu-id="e44c9-1169">schema</span><span class="sxs-lookup"><span data-stu-id="e44c9-1169">schema</span></span> |<span data-ttu-id="e44c9-1170">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1170">Name of hello schema in hello database.</span></span> <span data-ttu-id="e44c9-1171">hello 스키마 이름이 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1171">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="e44c9-1172">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1172">No</span></span> |
| <span data-ttu-id="e44c9-1173">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1173">authenticationType</span></span> |<span data-ttu-id="e44c9-1174">Tooconnect toohello DB2 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1174">Type of authentication used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="e44c9-1175">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1175">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e44c9-1176">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1176">Yes</span></span> |
| <span data-ttu-id="e44c9-1177">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1177">username</span></span> |<span data-ttu-id="e44c9-1178">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1178">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e44c9-1179">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1179">No</span></span> |
| <span data-ttu-id="e44c9-1180">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1180">password</span></span> |<span data-ttu-id="e44c9-1181">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1181">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-1182">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1182">No</span></span> |
| <span data-ttu-id="e44c9-1183">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1183">gatewayName</span></span> |<span data-ttu-id="e44c9-1184">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 DB2 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1184">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="e44c9-1185">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1185">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1186">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1186">Example</span></span>
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
<span data-ttu-id="e44c9-1187">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1187">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1188">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1188">Dataset</span></span>
<span data-ttu-id="e44c9-1189">toodefine DB2 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1189">toodefine a DB2 dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="e44c9-1190">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1190">Property</span></span> | <span data-ttu-id="e44c9-1191">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1191">Description</span></span> | <span data-ttu-id="e44c9-1192">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1192">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1193">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1193">tableName</span></span> |<span data-ttu-id="e44c9-1194">연결 된 서비스는 hello DB2 데이터베이스 인스턴스의 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1194">Name of hello table in hello DB2 Database instance that linked service refers to.</span></span> <span data-ttu-id="e44c9-1195">hello tableName은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1195">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="e44c9-1196">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1196">No (if **query** of **RelationalSource** is specified)</span></span> 

#### <a name="example"></a><span data-ttu-id="e44c9-1197">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1197">Example</span></span>
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

<span data-ttu-id="e44c9-1198">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1198">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1199">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1199">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1200">IBM d b 2에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1200">If you are copying data from IBM DB2, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1201">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1201">Property</span></span> | <span data-ttu-id="e44c9-1202">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1202">Description</span></span> | <span data-ttu-id="e44c9-1203">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1203">Allowed values</span></span> | <span data-ttu-id="e44c9-1204">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1204">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1205">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1205">query</span></span> |<span data-ttu-id="e44c9-1206">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1206">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1207">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1207">SQL query string.</span></span> <span data-ttu-id="e44c9-1208">예: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1208">For example: `"query": "select * from "MySchema"."MyTable""`.</span></span> |<span data-ttu-id="e44c9-1209">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1209">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1210">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1210">Example</span></span>
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
<span data-ttu-id="e44c9-1211">자세한 내용은 [IBM DB2 커넥터](#data-factory-onprem-db2-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1211">For more information, see [IBM DB2 connector](#data-factory-onprem-db2-connector.md#copy-activity-properties) article.</span></span>

## <a name="mysql"></a><span data-ttu-id="e44c9-1212">MySQL</span><span class="sxs-lookup"><span data-stu-id="e44c9-1212">MySQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1213">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1213">Linked service</span></span>
<span data-ttu-id="e44c9-1214">연결 된 서비스를 집합 hello toodefine MySQL **형식** hello 연결 서비스 너무**OnPremisesMySql**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1214">toodefine a MySQL linked service, set hello **type** of hello linked service too**OnPremisesMySql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1215">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1215">Property</span></span> | <span data-ttu-id="e44c9-1216">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1216">Description</span></span> | <span data-ttu-id="e44c9-1217">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1217">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1218">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1218">server</span></span> |<span data-ttu-id="e44c9-1219">Hello MySQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1219">Name of hello MySQL server.</span></span> |<span data-ttu-id="e44c9-1220">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1220">Yes</span></span> |
| <span data-ttu-id="e44c9-1221">database</span><span class="sxs-lookup"><span data-stu-id="e44c9-1221">database</span></span> |<span data-ttu-id="e44c9-1222">Hello MySQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1222">Name of hello MySQL database.</span></span> |<span data-ttu-id="e44c9-1223">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1223">Yes</span></span> |
| <span data-ttu-id="e44c9-1224">schema</span><span class="sxs-lookup"><span data-stu-id="e44c9-1224">schema</span></span> |<span data-ttu-id="e44c9-1225">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1225">Name of hello schema in hello database.</span></span> |<span data-ttu-id="e44c9-1226">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1226">No</span></span> |
| <span data-ttu-id="e44c9-1227">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1227">authenticationType</span></span> |<span data-ttu-id="e44c9-1228">Tooconnect toohello MySQL 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1228">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="e44c9-1229">가능한 값은 `Basic`입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1229">Possible values are: `Basic`.</span></span> |<span data-ttu-id="e44c9-1230">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1230">Yes</span></span> |
| <span data-ttu-id="e44c9-1231">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1231">username</span></span> |<span data-ttu-id="e44c9-1232">사용자 이름 tooconnect toohello MySQL 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1232">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="e44c9-1233">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1233">Yes</span></span> |
| <span data-ttu-id="e44c9-1234">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1234">password</span></span> |<span data-ttu-id="e44c9-1235">지정한 hello 사용자 계정에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1235">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="e44c9-1236">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1236">Yes</span></span> |
| <span data-ttu-id="e44c9-1237">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1237">gatewayName</span></span> |<span data-ttu-id="e44c9-1238">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 MySQL 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1238">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="e44c9-1239">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1239">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1240">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1240">Example</span></span>

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

<span data-ttu-id="e44c9-1241">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1241">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1242">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1242">Dataset</span></span>
<span data-ttu-id="e44c9-1243">toodefine MySQL dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1243">toodefine a MySQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1244">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1244">Property</span></span> | <span data-ttu-id="e44c9-1245">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1245">Description</span></span> | <span data-ttu-id="e44c9-1246">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1247">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1247">tableName</span></span> |<span data-ttu-id="e44c9-1248">MySQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1248">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="e44c9-1249">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1249">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1250">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1250">Example</span></span>

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
<span data-ttu-id="e44c9-1251">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1251">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1252">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1252">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1253">MySQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1253">If you are copying data from a MySQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1254">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1254">Property</span></span> | <span data-ttu-id="e44c9-1255">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1255">Description</span></span> | <span data-ttu-id="e44c9-1256">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1256">Allowed values</span></span> | <span data-ttu-id="e44c9-1257">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1257">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1258">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1258">query</span></span> |<span data-ttu-id="e44c9-1259">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1259">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1260">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1260">SQL query string.</span></span> <span data-ttu-id="e44c9-1261">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1261">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-1262">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1262">No (if **tableName** of **dataset** is specified)</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-1263">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1263">Example</span></span>
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

<span data-ttu-id="e44c9-1264">자세한 내용은 [MySQL 커넥터](data-factory-onprem-mysql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1264">For more information, see [MySQL connector](data-factory-onprem-mysql-connector.md#copy-activity-properties) article.</span></span> 

## <a name="oracle"></a><span data-ttu-id="e44c9-1265">Oracle</span><span class="sxs-lookup"><span data-stu-id="e44c9-1265">Oracle</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-1266">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1266">Linked service</span></span>
<span data-ttu-id="e44c9-1267">연결 된 서비스를 집합 hello toodefine Oracle **형식** hello 연결 서비스 너무**OnPremisesOracle**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1267">toodefine an Oracle linked service, set hello **type** of hello linked service too**OnPremisesOracle**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1268">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1268">Property</span></span> | <span data-ttu-id="e44c9-1269">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1269">Description</span></span> | <span data-ttu-id="e44c9-1270">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1270">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1271">driverType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1271">driverType</span></span> | <span data-ttu-id="e44c9-1272">드라이버 toouse toocopy 데이터 지정 / tooOracle 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1272">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="e44c9-1273">허용되는 값은 **Microsoft** 또는 **ODP**(기본값)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1273">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="e44c9-1274">드라이버 세부 정보에 대해서는 [지원되는 버전 및 설치](#supported-versions-and-installation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1274">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="e44c9-1275">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1275">No</span></span> |
| <span data-ttu-id="e44c9-1276">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-1276">connectionString</span></span> | <span data-ttu-id="e44c9-1277">Hello connectionString 속성에 대 한 tooconnect toohello Oracle 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1277">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="e44c9-1278">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1278">Yes</span></span> |
| <span data-ttu-id="e44c9-1279">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1279">gatewayName</span></span> | <span data-ttu-id="e44c9-1280">사용 하는 tooconnect toohello 온-프레미스 Oracle 서버 hello 게이트웨이의 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1280">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="e44c9-1281">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1281">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1282">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1282">Example</span></span>
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

<span data-ttu-id="e44c9-1283">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1283">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1284">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1284">Dataset</span></span>
<span data-ttu-id="e44c9-1285">Oracle 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**OracleTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1285">toodefine an Oracle dataset, set hello **type** of hello dataset too**OracleTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1286">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1286">Property</span></span> | <span data-ttu-id="e44c9-1287">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1287">Description</span></span> | <span data-ttu-id="e44c9-1288">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1288">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1289">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1289">tableName</span></span> |<span data-ttu-id="e44c9-1290">Oracle 데이터베이스를 연결 된 서비스 hello hello에 hello 테이블의 이름은 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1290">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="e44c9-1291">아니요(**OracleSource**의 **oracleReaderQuery**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1291">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1292">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1292">Example</span></span>

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
<span data-ttu-id="e44c9-1293">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1293">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#dataset-properties) article.</span></span>

### <a name="oracle-source-in-copy-activity"></a><span data-ttu-id="e44c9-1294">복사 활동의 Oracle 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1294">Oracle Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1295">Oracle 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**OracleSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1295">If you are copying data from an Oracle database, set hello **source type** of hello copy activity too**OracleSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1296">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1296">Property</span></span> | <span data-ttu-id="e44c9-1297">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1297">Description</span></span> | <span data-ttu-id="e44c9-1298">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1298">Allowed values</span></span> | <span data-ttu-id="e44c9-1299">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1299">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1300">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e44c9-1300">oracleReaderQuery</span></span> |<span data-ttu-id="e44c9-1301">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1301">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1302">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1302">SQL query string.</span></span> <span data-ttu-id="e44c9-1303">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1303">For example: `select * from MyTable`</span></span> <br/><br/><span data-ttu-id="e44c9-1304">지정 하지 않으면 실행 되는 SQL 문을 hello:`select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1304">If not specified, hello SQL statement that is executed: `select * from MyTable`</span></span> |<span data-ttu-id="e44c9-1305">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1305">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1306">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1306">Example</span></span>

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

<span data-ttu-id="e44c9-1307">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1307">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

### <a name="oracle-sink-in-copy-activity"></a><span data-ttu-id="e44c9-1308">복사 활동의 Oracle 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-1308">Oracle Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-1309">데이터 tooam Oracle 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**OracleSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1309">If you are copying data tooam Oracle database, set hello **sink type** of hello copy activity too**OracleSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-1310">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1310">Property</span></span> | <span data-ttu-id="e44c9-1311">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1311">Description</span></span> | <span data-ttu-id="e44c9-1312">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1312">Allowed values</span></span> | <span data-ttu-id="e44c9-1313">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1313">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1314">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-1314">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-1315">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1315">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e44c9-1316">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-1316">timespan</span></span><br/><br/> <span data-ttu-id="e44c9-1317">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="e44c9-1317">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="e44c9-1318">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1318">No</span></span> |
| <span data-ttu-id="e44c9-1319">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-1319">writeBatchSize</span></span> |<span data-ttu-id="e44c9-1320">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1320">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e44c9-1321">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1321">Integer (number of rows)</span></span> |<span data-ttu-id="e44c9-1322">아니요(기본값: 100)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1322">No (default: 100)</span></span> |
| <span data-ttu-id="e44c9-1323">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e44c9-1323">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e44c9-1324">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1324">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="e44c9-1325">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1325">A query statement.</span></span> |<span data-ttu-id="e44c9-1326">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1326">No</span></span> |
| <span data-ttu-id="e44c9-1327">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1327">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e44c9-1328">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1328">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="e44c9-1329">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1329">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e44c9-1330">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1330">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1331">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1331">Example</span></span>
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
<span data-ttu-id="e44c9-1332">자세한 내용은 [Oracle 커넥터](data-factory-onprem-oracle-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1332">For more information, see [Oracle connector](data-factory-onprem-oracle-connector.md#copy-activity-properties) article.</span></span>

## <a name="postgresql"></a><span data-ttu-id="e44c9-1333">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e44c9-1333">PostgreSQL</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1334">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1334">Linked service</span></span>
<span data-ttu-id="e44c9-1335">연결 된 서비스를 집합 hello toodefine는 PostgreSQL **형식** hello 연결 서비스 너무**OnPremisesPostgreSql**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1335">toodefine a PostgreSQL linked service, set hello **type** of hello linked service too**OnPremisesPostgreSql**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1336">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1336">Property</span></span> | <span data-ttu-id="e44c9-1337">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1337">Description</span></span> | <span data-ttu-id="e44c9-1338">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1338">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1339">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1339">server</span></span> |<span data-ttu-id="e44c9-1340">Hello PostgreSQL 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1340">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="e44c9-1341">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1341">Yes</span></span> |
| <span data-ttu-id="e44c9-1342">database</span><span class="sxs-lookup"><span data-stu-id="e44c9-1342">database</span></span> |<span data-ttu-id="e44c9-1343">Hello PostgreSQL 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1343">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="e44c9-1344">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1344">Yes</span></span> |
| <span data-ttu-id="e44c9-1345">schema</span><span class="sxs-lookup"><span data-stu-id="e44c9-1345">schema</span></span> |<span data-ttu-id="e44c9-1346">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1346">Name of hello schema in hello database.</span></span> <span data-ttu-id="e44c9-1347">hello 스키마 이름이 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1347">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="e44c9-1348">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1348">No</span></span> |
| <span data-ttu-id="e44c9-1349">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1349">authenticationType</span></span> |<span data-ttu-id="e44c9-1350">Tooconnect toohello PostgreSQL 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1350">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="e44c9-1351">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1351">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e44c9-1352">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1352">Yes</span></span> |
| <span data-ttu-id="e44c9-1353">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1353">username</span></span> |<span data-ttu-id="e44c9-1354">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1354">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e44c9-1355">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1355">No</span></span> |
| <span data-ttu-id="e44c9-1356">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1356">password</span></span> |<span data-ttu-id="e44c9-1357">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1357">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-1358">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1358">No</span></span> |
| <span data-ttu-id="e44c9-1359">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1359">gatewayName</span></span> |<span data-ttu-id="e44c9-1360">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 PostgreSQL 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1360">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="e44c9-1361">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1361">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1362">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1362">Example</span></span>

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
<span data-ttu-id="e44c9-1363">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1363">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1364">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1364">Dataset</span></span>
<span data-ttu-id="e44c9-1365">toodefine PostgreSQL dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1365">toodefine a PostgreSQL dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1366">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1366">Property</span></span> | <span data-ttu-id="e44c9-1367">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1367">Description</span></span> | <span data-ttu-id="e44c9-1368">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1368">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1369">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1369">tableName</span></span> |<span data-ttu-id="e44c9-1370">PostgreSQL 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1370">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="e44c9-1371">hello tableName은 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1371">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="e44c9-1372">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1372">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1373">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1373">Example</span></span>
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
<span data-ttu-id="e44c9-1374">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1374">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1375">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1375">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1376">PostgreSQL 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1376">If you are copying data from a PostgreSQL database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1377">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1377">Property</span></span> | <span data-ttu-id="e44c9-1378">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1378">Description</span></span> | <span data-ttu-id="e44c9-1379">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1379">Allowed values</span></span> | <span data-ttu-id="e44c9-1380">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1380">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1381">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1381">query</span></span> |<span data-ttu-id="e44c9-1382">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1382">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1383">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1383">SQL query string.</span></span> <span data-ttu-id="e44c9-1384">예: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="e44c9-1384">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="e44c9-1385">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1385">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1386">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1386">Example</span></span>

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

<span data-ttu-id="e44c9-1387">자세한 내용은 [PostgreSQL 커넥터](data-factory-onprem-postgresql-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1387">For more information, see [PostgreSQL connector](data-factory-onprem-postgresql-connector.md#copy-activity-properties) article.</span></span>

## <a name="sap-business-warehouse"></a><span data-ttu-id="e44c9-1388">SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="e44c9-1388">SAP Business Warehouse</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-1389">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1389">Linked service</span></span>
<span data-ttu-id="e44c9-1390">연결 된 서비스를 집합 hello toodefine SAP 비즈니스 웨어하우스 (BW) **형식** hello 연결 서비스 너무**SapBw**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1390">toodefine a SAP Business Warehouse (BW) linked service, set hello **type** of hello linked service too**SapBw**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="e44c9-1391">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1391">Property</span></span> | <span data-ttu-id="e44c9-1392">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1392">Description</span></span> | <span data-ttu-id="e44c9-1393">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1393">Allowed values</span></span> | <span data-ttu-id="e44c9-1394">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1394">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="e44c9-1395">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1395">server</span></span> | <span data-ttu-id="e44c9-1396">SAP BW는 hello에 인스턴스가 있는 hello 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1396">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="e44c9-1397">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1397">string</span></span> | <span data-ttu-id="e44c9-1398">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1398">Yes</span></span>
<span data-ttu-id="e44c9-1399">systemNumber</span><span class="sxs-lookup"><span data-stu-id="e44c9-1399">systemNumber</span></span> | <span data-ttu-id="e44c9-1400">Hello SAP BW 시스템의 시스템 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1400">System number of hello SAP BW system.</span></span> | <span data-ttu-id="e44c9-1401">문자열로 표현되는 두 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1401">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="e44c9-1402">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1402">Yes</span></span>
<span data-ttu-id="e44c9-1403">clientId</span><span class="sxs-lookup"><span data-stu-id="e44c9-1403">clientId</span></span> | <span data-ttu-id="e44c9-1404">클라이언트 hello W SAP 시스템에서에서 hello 클라이언트의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1404">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="e44c9-1405">문자열로 표현되는 세 자리 10진수.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1405">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="e44c9-1406">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1406">Yes</span></span>
<span data-ttu-id="e44c9-1407">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1407">username</span></span> | <span data-ttu-id="e44c9-1408">Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1408">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="e44c9-1409">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1409">string</span></span> | <span data-ttu-id="e44c9-1410">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1410">Yes</span></span>
<span data-ttu-id="e44c9-1411">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1411">password</span></span> | <span data-ttu-id="e44c9-1412">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1412">Password for hello user.</span></span> | <span data-ttu-id="e44c9-1413">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1413">string</span></span> | <span data-ttu-id="e44c9-1414">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1414">Yes</span></span>
<span data-ttu-id="e44c9-1415">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1415">gatewayName</span></span> | <span data-ttu-id="e44c9-1416">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP BW 인스턴스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1416">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="e44c9-1417">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1417">string</span></span> | <span data-ttu-id="e44c9-1418">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1418">Yes</span></span>
<span data-ttu-id="e44c9-1419">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-1419">encryptedCredential</span></span> | <span data-ttu-id="e44c9-1420">hello 암호화 된 자격 증명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1420">hello encrypted credential string.</span></span> | <span data-ttu-id="e44c9-1421">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1421">string</span></span> | <span data-ttu-id="e44c9-1422">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1422">No</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-1423">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1423">Example</span></span>

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

<span data-ttu-id="e44c9-1424">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1424">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1425">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1425">Dataset</span></span>
<span data-ttu-id="e44c9-1426">SAP BW 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1426">toodefine a SAP BW dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="e44c9-1427">형식의 hello SAP BW 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1427">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span>  

#### <a name="example"></a><span data-ttu-id="e44c9-1428">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1428">Example</span></span>

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
<span data-ttu-id="e44c9-1429">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1429">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1430">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1430">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1431">SAP Business Warehouse에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1431">If you are copying data from SAP Business Warehouse, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1432">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1432">Property</span></span> | <span data-ttu-id="e44c9-1433">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1433">Description</span></span> | <span data-ttu-id="e44c9-1434">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1434">Allowed values</span></span> | <span data-ttu-id="e44c9-1435">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1435">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1436">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1436">query</span></span> | <span data-ttu-id="e44c9-1437">Hello hello SAP BW 인스턴스에서 MDX 쿼리 tooread 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1437">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="e44c9-1438">MDX 쿼리.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1438">MDX query.</span></span> | <span data-ttu-id="e44c9-1439">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1439">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1440">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1440">Example</span></span>

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

<span data-ttu-id="e44c9-1441">자세한 내용은 [SAP Business Warehouse 커넥터](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1441">For more information, see [SAP Business Warehouse connector](data-factory-sap-business-warehouse-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sap-hana"></a><span data-ttu-id="e44c9-1442">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="e44c9-1442">SAP HANA</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1443">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1443">Linked service</span></span>
<span data-ttu-id="e44c9-1444">연결 된 서비스를 집합 hello toodefine SAP HANA **형식** hello 연결 서비스 너무**SapHana**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1444">toodefine a SAP HANA linked service, set hello **type** of hello linked service too**SapHana**, and specify following properties in hello **typeProperties** section:</span></span>  

<span data-ttu-id="e44c9-1445">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1445">Property</span></span> | <span data-ttu-id="e44c9-1446">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1446">Description</span></span> | <span data-ttu-id="e44c9-1447">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1447">Allowed values</span></span> | <span data-ttu-id="e44c9-1448">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1448">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="e44c9-1449">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1449">server</span></span> | <span data-ttu-id="e44c9-1450">SAP HANA는 hello에 인스턴스가 있는 hello 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1450">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="e44c9-1451">서버에서 사용자 지정된 포트를 사용하는 경우 `server:port`를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1451">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="e44c9-1452">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1452">string</span></span> | <span data-ttu-id="e44c9-1453">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1453">Yes</span></span>
<span data-ttu-id="e44c9-1454">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1454">authenticationType</span></span> | <span data-ttu-id="e44c9-1455">인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1455">Type of authentication.</span></span> | <span data-ttu-id="e44c9-1456">string.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1456">string.</span></span> <span data-ttu-id="e44c9-1457">"Basic" 또는 "Windows"</span><span class="sxs-lookup"><span data-stu-id="e44c9-1457">"Basic" or "Windows"</span></span> | <span data-ttu-id="e44c9-1458">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1458">Yes</span></span> 
<span data-ttu-id="e44c9-1459">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1459">username</span></span> | <span data-ttu-id="e44c9-1460">Toohello SAP 서버 액세스를 갖고 있는 hello 사용자의 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1460">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="e44c9-1461">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1461">string</span></span> | <span data-ttu-id="e44c9-1462">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1462">Yes</span></span>
<span data-ttu-id="e44c9-1463">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1463">password</span></span> | <span data-ttu-id="e44c9-1464">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1464">Password for hello user.</span></span> | <span data-ttu-id="e44c9-1465">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1465">string</span></span> | <span data-ttu-id="e44c9-1466">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1466">Yes</span></span>
<span data-ttu-id="e44c9-1467">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1467">gatewayName</span></span> | <span data-ttu-id="e44c9-1468">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SAP HANA 인스턴스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1468">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="e44c9-1469">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1469">string</span></span> | <span data-ttu-id="e44c9-1470">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1470">Yes</span></span>
<span data-ttu-id="e44c9-1471">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-1471">encryptedCredential</span></span> | <span data-ttu-id="e44c9-1472">hello 암호화 된 자격 증명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1472">hello encrypted credential string.</span></span> | <span data-ttu-id="e44c9-1473">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1473">string</span></span> | <span data-ttu-id="e44c9-1474">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1474">No</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-1475">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1475">Example</span></span>

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
<span data-ttu-id="e44c9-1476">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1476">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#linked-service-properties) article.</span></span>
 
### <a name="dataset"></a><span data-ttu-id="e44c9-1477">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1477">Dataset</span></span>
<span data-ttu-id="e44c9-1478">SAP HANA 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1478">toodefine a SAP HANA dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="e44c9-1479">형식의 hello SAP HANA 데이터 집합에 대 한 지원 유형별 속성이 없는 **RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1479">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 

#### <a name="example"></a><span data-ttu-id="e44c9-1480">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1480">Example</span></span>

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
<span data-ttu-id="e44c9-1481">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1481">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1482">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1482">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1483">SAP HANA 데이터 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1483">If you are copying data from a SAP HANA data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1484">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1484">Property</span></span> | <span data-ttu-id="e44c9-1485">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1485">Description</span></span> | <span data-ttu-id="e44c9-1486">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1486">Allowed values</span></span> | <span data-ttu-id="e44c9-1487">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1487">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1488">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1488">query</span></span> | <span data-ttu-id="e44c9-1489">Hello SAP HANA 인스턴스에서 hello SQL 쿼리 tooread 데이터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1489">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="e44c9-1490">SQL 쿼리.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1490">SQL query.</span></span> | <span data-ttu-id="e44c9-1491">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1491">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-1492">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1492">Example</span></span>


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

<span data-ttu-id="e44c9-1493">자세한 내용은 [SAP HANA 커넥터](data-factory-sap-hana-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1493">For more information, see [SAP HANA connector](data-factory-sap-hana-connector.md#copy-activity-properties) article.</span></span>


## <a name="sql-server"></a><span data-ttu-id="e44c9-1494">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1494">SQL Server</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1495">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1495">Linked service</span></span>
<span data-ttu-id="e44c9-1496">형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1496">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="e44c9-1497">다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1497">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="e44c9-1498">다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1498">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="e44c9-1499">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1499">Property</span></span> | <span data-ttu-id="e44c9-1500">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1500">Description</span></span> | <span data-ttu-id="e44c9-1501">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1501">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1502">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-1502">type</span></span> |<span data-ttu-id="e44c9-1503">hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1503">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="e44c9-1504">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1504">Yes</span></span> |
| <span data-ttu-id="e44c9-1505">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-1505">connectionString</span></span> |<span data-ttu-id="e44c9-1506">SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1506">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="e44c9-1507">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1507">Yes</span></span> |
| <span data-ttu-id="e44c9-1508">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1508">gatewayName</span></span> |<span data-ttu-id="e44c9-1509">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1509">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="e44c9-1510">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1510">Yes</span></span> |
| <span data-ttu-id="e44c9-1511">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1511">username</span></span> |<span data-ttu-id="e44c9-1512">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1512">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="e44c9-1513">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1513">Example: **domainname\\username**.</span></span> |<span data-ttu-id="e44c9-1514">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1514">No</span></span> |
| <span data-ttu-id="e44c9-1515">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1515">password</span></span> |<span data-ttu-id="e44c9-1516">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1516">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-1517">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1517">No</span></span> |

<span data-ttu-id="e44c9-1518">Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):</span><span class="sxs-lookup"><span data-stu-id="e44c9-1518">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="e44c9-1519">예제: SQL 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="e44c9-1519">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="e44c9-1520">예제: Windows 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="e44c9-1520">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="e44c9-1521">사용자 이름 및 암호를 지정 하는 경우 게이트웨이에서 사용 하 여 해당 tooimpersonate hello 지정 된 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1521">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="e44c9-1522">그렇지 않은 경우 게이트웨이 게이트웨이 (시작 계정)의 보안 컨텍스트 hello와 직접 toohello SQL Server를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1522">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="e44c9-1523">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1523">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1524">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1524">Dataset</span></span>
<span data-ttu-id="e44c9-1525">SQL Server 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**SqlServerTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1525">toodefine a SQL Server dataset, set hello **type** of hello dataset too**SqlServerTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1526">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1526">Property</span></span> | <span data-ttu-id="e44c9-1527">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1527">Description</span></span> | <span data-ttu-id="e44c9-1528">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1528">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1529">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1529">tableName</span></span> |<span data-ttu-id="e44c9-1530">Hello 테이블 또는 뷰의 연결 된 서비스는 hello SQL Server 데이터베이스 인스턴스의 이름이 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1530">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="e44c9-1531">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1531">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1532">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1532">Example</span></span>
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

<span data-ttu-id="e44c9-1533">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1533">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#dataset-properties) article.</span></span> 

### <a name="sql-source-in-copy-activity"></a><span data-ttu-id="e44c9-1534">복사 활동의 SQL 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1534">Sql Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1535">SQL Server 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**SqlSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1535">If you are copying data from a SQL Server database, set hello **source type** of hello copy activity too**SqlSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1536">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1536">Property</span></span> | <span data-ttu-id="e44c9-1537">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1537">Description</span></span> | <span data-ttu-id="e44c9-1538">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1538">Allowed values</span></span> | <span data-ttu-id="e44c9-1539">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1539">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1540">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e44c9-1540">sqlReaderQuery</span></span> |<span data-ttu-id="e44c9-1541">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1541">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1542">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1542">SQL query string.</span></span> <span data-ttu-id="e44c9-1543">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1543">For example: `select * from MyTable`.</span></span> <span data-ttu-id="e44c9-1544">Hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스에서 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1544">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="e44c9-1545">지정 하지 않으면 실행 되는 SQL 문을 hello: MyTable 중에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1545">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="e44c9-1546">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1546">No</span></span> |
| <span data-ttu-id="e44c9-1547">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1547">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="e44c9-1548">Hello 원본 테이블에서 데이터를 읽을 수 있는 프로시저를 저장 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1548">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="e44c9-1549">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1549">Name of hello stored procedure.</span></span> |<span data-ttu-id="e44c9-1550">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1550">No</span></span> |
| <span data-ttu-id="e44c9-1551">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-1551">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-1552">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1552">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e44c9-1553">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1553">Name/value pairs.</span></span> <span data-ttu-id="e44c9-1554">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1554">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e44c9-1555">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1555">No</span></span> |

<span data-ttu-id="e44c9-1556">경우 hello **sqlReaderQuery** 에 대해 지정 된 hello SqlSource, hello 복사 활동 hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1556">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="e44c9-1557">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="e44c9-1557">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="e44c9-1558">Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName 중 하나를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1558">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="e44c9-1559">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1559">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="e44c9-1560">사용 하는 경우 **sqlReaderStoredProcedureName**, hello에 대 한 값을 toospecify 보내야 **tableName** hello 데이터 집합 JSON의에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1560">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="e44c9-1561">그러나 이 테이블에 대해 수행되는 유효성 검사는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1561">There are no validations performed against this table though.</span></span>


#### <a name="example"></a><span data-ttu-id="e44c9-1562">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1562">Example</span></span>
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

<span data-ttu-id="e44c9-1563">이 예제에서는 **sqlReaderQuery** SqlSource hello에 대 한 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1563">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="e44c9-1564">복사 활동 hello hello SQL Server 데이터베이스 원본 tooget hello 데이터에 대해이 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1564">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="e44c9-1565">또는 hello를 지정 하 여 저장된 프로시저를 지정할 수 있습니다 **sqlReaderStoredProcedureName** 및 **storedProcedureParameters** (경우 hello 저장된 프로시저 매개 변수를 사용).</span><span class="sxs-lookup"><span data-stu-id="e44c9-1565">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="e44c9-1566">hello sqlReaderQuery hello 입력된 데이터 집합에서 참조 하는 hello 데이터베이스 내에서 여러 테이블을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1566">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="e44c9-1567">데이터 집합의 tableName typeProperty hello으로 설정 하는 제한 된 tooonly hello 테이블이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1567">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="e44c9-1568">Hello 구조 섹션에 정의 된 hello 열 sqlReaderQuery 또는 sqlReaderStoredProcedureName를 지정 하지 않으면 경우 사용 되는 toobuild hello SQL Server 데이터베이스에 대해 선택 쿼리 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1568">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="e44c9-1569">데이터 집합 정의 hello hello 구조 없으면 hello 테이블에서 모든 열을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1569">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="e44c9-1570">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1570">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

### <a name="sql-sink-in-copy-activity"></a><span data-ttu-id="e44c9-1571">복사 활동의 SQL 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-1571">Sql Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-1572">데이터 tooa SQL Server 데이터베이스를 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**SqlSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1572">If you are copying data tooa SQL Server database, set hello **sink type** of hello copy activity too**SqlSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-1573">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1573">Property</span></span> | <span data-ttu-id="e44c9-1574">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1574">Description</span></span> | <span data-ttu-id="e44c9-1575">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1575">Allowed values</span></span> | <span data-ttu-id="e44c9-1576">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1576">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1577">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-1577">writeBatchTimeout</span></span> |<span data-ttu-id="e44c9-1578">대기 시간이 초과 되기 전에 일괄 처리 삽입 작업 toocomplete hello에 대 한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1578">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="e44c9-1579">timespan</span><span class="sxs-lookup"><span data-stu-id="e44c9-1579">timespan</span></span><br/><br/> <span data-ttu-id="e44c9-1580">예: “00:30:00”(30분).</span><span class="sxs-lookup"><span data-stu-id="e44c9-1580">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e44c9-1581">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1581">No</span></span> |
| <span data-ttu-id="e44c9-1582">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-1582">writeBatchSize</span></span> |<span data-ttu-id="e44c9-1583">WriteBatchSize hello 버퍼 크기에 이르면 hello SQL 테이블에 데이터를 삽입 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1583">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e44c9-1584">정수(행 수)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1584">Integer (number of rows)</span></span> |<span data-ttu-id="e44c9-1585">아니요(기본값: 10000)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1585">No (default: 10000)</span></span> |
| <span data-ttu-id="e44c9-1586">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e44c9-1586">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e44c9-1587">특정 조각의 데이터 정리 되도록 tooexecute 복사 작업에 대 한 쿼리를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1587">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="e44c9-1588">자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1588">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="e44c9-1589">쿼리 문입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1589">A query statement.</span></span> |<span data-ttu-id="e44c9-1590">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1590">No</span></span> |
| <span data-ttu-id="e44c9-1591">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1591">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e44c9-1592">특정 조각 다시 실행 시점의 데이터를 사용 하는 tooclean 변수인 자동 생성 된 조각 식별자를 가진 toofill 복사 작업에 대 한 열 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1592">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="e44c9-1593">자세한 내용은 [반복성](#repeatability-during-copy) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1593">For more information, see [repeatability](#repeatability-during-copy) section.</span></span> |<span data-ttu-id="e44c9-1594">이진(32) 데이터 형식이 있는 열의 열 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1594">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e44c9-1595">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1595">No</span></span> |
| <span data-ttu-id="e44c9-1596">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1596">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="e44c9-1597">Hello 저장 프로시저의 이름 (업데이트/삽입) upserts 데이터 hello 대상 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1597">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="e44c9-1598">저장 프로시저를 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1598">Name of hello stored procedure.</span></span> |<span data-ttu-id="e44c9-1599">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1599">No</span></span> |
| <span data-ttu-id="e44c9-1600">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-1600">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-1601">Hello에 대 한 매개 변수 저장 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1601">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="e44c9-1602">이름/값 쌍입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1602">Name/value pairs.</span></span> <span data-ttu-id="e44c9-1603">Hello 이름과 대/소문자 hello 저장 프로시저 매개 변수의 이름 및 매개 변수는 대/소문자 구분 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1603">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="e44c9-1604">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1604">No</span></span> |
| <span data-ttu-id="e44c9-1605">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1605">sqlWriterTableType</span></span> |<span data-ttu-id="e44c9-1606">테이블 형식 이름 toobe hello 저장 프로시저에 사용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1606">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="e44c9-1607">복사 활동 임시 테이블과이 테이블 형식으로 사용할 수 있는 이동 된 hello 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1607">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="e44c9-1608">저장된 프로시저 코드 hello 데이터를 기존 데이터와 복사를 병합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1608">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="e44c9-1609">테이블 유형 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-1609">A table type name.</span></span> |<span data-ttu-id="e44c9-1610">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1610">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1611">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1611">Example</span></span>
<span data-ttu-id="e44c9-1612">복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1612">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e44c9-1613">Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1613">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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

<span data-ttu-id="e44c9-1614">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1614">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#copy-activity-properties) article.</span></span> 

## <a name="sybase"></a><span data-ttu-id="e44c9-1615">Sybase</span><span class="sxs-lookup"><span data-stu-id="e44c9-1615">Sybase</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1616">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1616">Linked service</span></span>
<span data-ttu-id="e44c9-1617">연결 된 서비스를 집합 hello toodefine는 Sybase **형식** hello 연결 서비스 너무**OnPremisesSybase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1617">toodefine a Sybase linked service, set hello **type** of hello linked service too**OnPremisesSybase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1618">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1618">Property</span></span> | <span data-ttu-id="e44c9-1619">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1619">Description</span></span> | <span data-ttu-id="e44c9-1620">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1620">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1621">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1621">server</span></span> |<span data-ttu-id="e44c9-1622">Hello Sybase 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1622">Name of hello Sybase server.</span></span> |<span data-ttu-id="e44c9-1623">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1623">Yes</span></span> |
| <span data-ttu-id="e44c9-1624">database</span><span class="sxs-lookup"><span data-stu-id="e44c9-1624">database</span></span> |<span data-ttu-id="e44c9-1625">Hello Sybase 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1625">Name of hello Sybase database.</span></span> |<span data-ttu-id="e44c9-1626">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1626">Yes</span></span> |
| <span data-ttu-id="e44c9-1627">schema</span><span class="sxs-lookup"><span data-stu-id="e44c9-1627">schema</span></span> |<span data-ttu-id="e44c9-1628">Hello hello 데이터베이스 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1628">Name of hello schema in hello database.</span></span> |<span data-ttu-id="e44c9-1629">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1629">No</span></span> |
| <span data-ttu-id="e44c9-1630">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1630">authenticationType</span></span> |<span data-ttu-id="e44c9-1631">Tooconnect toohello Sybase 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1631">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="e44c9-1632">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1632">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e44c9-1633">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1633">Yes</span></span> |
| <span data-ttu-id="e44c9-1634">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1634">username</span></span> |<span data-ttu-id="e44c9-1635">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1635">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e44c9-1636">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1636">No</span></span> |
| <span data-ttu-id="e44c9-1637">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1637">password</span></span> |<span data-ttu-id="e44c9-1638">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1638">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-1639">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1639">No</span></span> |
| <span data-ttu-id="e44c9-1640">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1640">gatewayName</span></span> |<span data-ttu-id="e44c9-1641">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Sybase 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1641">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="e44c9-1642">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1642">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1643">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1643">Example</span></span>
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

<span data-ttu-id="e44c9-1644">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1644">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1645">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1645">Dataset</span></span>
<span data-ttu-id="e44c9-1646">toodefine Sybase dataset 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1646">toodefine a Sybase dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1647">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1647">Property</span></span> | <span data-ttu-id="e44c9-1648">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1648">Description</span></span> | <span data-ttu-id="e44c9-1649">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1649">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1650">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1650">tableName</span></span> |<span data-ttu-id="e44c9-1651">Sybase 데이터베이스 인스턴스에 연결 된 서비스를 가리키는 hello에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1651">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="e44c9-1652">아니요(**RelationalSource**의 **쿼리**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1652">No (if **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1653">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1653">Example</span></span>

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

<span data-ttu-id="e44c9-1654">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1654">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1655">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1655">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1656">Sybase 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1656">If you are copying data from a Sybase database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1657">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1657">Property</span></span> | <span data-ttu-id="e44c9-1658">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1658">Description</span></span> | <span data-ttu-id="e44c9-1659">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1659">Allowed values</span></span> | <span data-ttu-id="e44c9-1660">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1660">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1661">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1661">query</span></span> |<span data-ttu-id="e44c9-1662">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1662">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1663">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1663">SQL query string.</span></span> <span data-ttu-id="e44c9-1664">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1664">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-1665">아니요(**데이터 집합**의 **tableName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1665">No (if **tableName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1666">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1666">Example</span></span>

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

<span data-ttu-id="e44c9-1667">자세한 내용은 [Sybase 커넥터](data-factory-onprem-sybase-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1667">For more information, see [Sybase connector](data-factory-onprem-sybase-connector.md#copy-activity-properties) article.</span></span>

## <a name="teradata"></a><span data-ttu-id="e44c9-1668">Teradata</span><span class="sxs-lookup"><span data-stu-id="e44c9-1668">Teradata</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1669">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1669">Linked service</span></span>
<span data-ttu-id="e44c9-1670">연결 된 서비스를 집합 hello toodefine는 Teradata **형식** hello 연결 서비스 너무**OnPremisesTeradata**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1670">toodefine a Teradata linked service, set hello **type** of hello linked service too**OnPremisesTeradata**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1671">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1671">Property</span></span> | <span data-ttu-id="e44c9-1672">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1672">Description</span></span> | <span data-ttu-id="e44c9-1673">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1673">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1674">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1674">server</span></span> |<span data-ttu-id="e44c9-1675">Hello Teradata 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1675">Name of hello Teradata server.</span></span> |<span data-ttu-id="e44c9-1676">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1676">Yes</span></span> |
| <span data-ttu-id="e44c9-1677">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1677">authenticationType</span></span> |<span data-ttu-id="e44c9-1678">Tooconnect toohello Teradata 데이터베이스를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1678">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="e44c9-1679">가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1679">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e44c9-1680">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1680">Yes</span></span> |
| <span data-ttu-id="e44c9-1681">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1681">username</span></span> |<span data-ttu-id="e44c9-1682">기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1682">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e44c9-1683">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1683">No</span></span> |
| <span data-ttu-id="e44c9-1684">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1684">password</span></span> |<span data-ttu-id="e44c9-1685">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1685">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-1686">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1686">No</span></span> |
| <span data-ttu-id="e44c9-1687">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1687">gatewayName</span></span> |<span data-ttu-id="e44c9-1688">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Teradata 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1688">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="e44c9-1689">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1689">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1690">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1690">Example</span></span>
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

<span data-ttu-id="e44c9-1691">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1691">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1692">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1692">Dataset</span></span>
<span data-ttu-id="e44c9-1693">toodefine Teradata Blob 데이터 집합 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1693">toodefine a Teradata Blob dataset, set hello **type** of hello dataset too**RelationalTable**.</span></span> <span data-ttu-id="e44c9-1694">현재,는 hello Teradata 데이터 집합에 대 한 지원 형식 속성이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1694">Currently, there are no type properties supported for hello Teradata dataset.</span></span> 

#### <a name="example"></a><span data-ttu-id="e44c9-1695">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1695">Example</span></span>
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

<span data-ttu-id="e44c9-1696">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1696">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-1697">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1697">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1698">Teradata 데이터베이스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1698">If you are copying data from a Teradata database, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1699">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1699">Property</span></span> | <span data-ttu-id="e44c9-1700">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1700">Description</span></span> | <span data-ttu-id="e44c9-1701">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1701">Allowed values</span></span> | <span data-ttu-id="e44c9-1702">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1702">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1703">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1703">query</span></span> |<span data-ttu-id="e44c9-1704">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1704">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1705">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1705">SQL query string.</span></span> <span data-ttu-id="e44c9-1706">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1706">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-1707">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1707">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1708">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1708">Example</span></span>

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

<span data-ttu-id="e44c9-1709">자세한 내용은 [Teradata 커넥터](data-factory-onprem-teradata-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1709">For more information, see [Teradata connector](data-factory-onprem-teradata-connector.md#copy-activity-properties) article.</span></span>

## <a name="cassandra"></a><span data-ttu-id="e44c9-1710">Cassandra</span><span class="sxs-lookup"><span data-stu-id="e44c9-1710">Cassandra</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-1711">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1711">Linked service</span></span>
<span data-ttu-id="e44c9-1712">연결 된 서비스를 집합 hello toodefine는 Cassandra **형식** hello 연결 서비스 너무**OnPremisesCassandra**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1712">toodefine a Cassandra linked service, set hello **type** of hello linked service too**OnPremisesCassandra**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1713">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1713">Property</span></span> | <span data-ttu-id="e44c9-1714">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1714">Description</span></span> | <span data-ttu-id="e44c9-1715">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1715">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1716">host</span><span class="sxs-lookup"><span data-stu-id="e44c9-1716">host</span></span> |<span data-ttu-id="e44c9-1717">Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1717">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="e44c9-1718">동시에 IP 주소 또는 호스트 이름 tooconnect tooall 서버의 쉼표로 구분 된 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1718">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="e44c9-1719">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1719">Yes</span></span> |
| <span data-ttu-id="e44c9-1720">포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-1720">port</span></span> |<span data-ttu-id="e44c9-1721">hello Cassandra 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1721">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="e44c9-1722">아니요. 기본값: 9042</span><span class="sxs-lookup"><span data-stu-id="e44c9-1722">No, default value: 9042</span></span> |
| <span data-ttu-id="e44c9-1723">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1723">authenticationType</span></span> |<span data-ttu-id="e44c9-1724">Basic 또는 Anonymous</span><span class="sxs-lookup"><span data-stu-id="e44c9-1724">Basic, or Anonymous</span></span> |<span data-ttu-id="e44c9-1725">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1725">Yes</span></span> |
| <span data-ttu-id="e44c9-1726">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1726">username</span></span> |<span data-ttu-id="e44c9-1727">Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1727">Specify user name for hello user account.</span></span> |<span data-ttu-id="e44c9-1728">예, authenticationType tooBasic 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1728">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="e44c9-1729">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1729">password</span></span> |<span data-ttu-id="e44c9-1730">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1730">Specify password for hello user account.</span></span> |<span data-ttu-id="e44c9-1731">예, authenticationType tooBasic 설정 된 경우.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1731">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="e44c9-1732">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1732">gatewayName</span></span> |<span data-ttu-id="e44c9-1733">데이터베이스가 사용 되는 tooconnect toohello 온-프레미스 Cassandra hello 게이트웨이의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1733">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="e44c9-1734">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1734">Yes</span></span> |
| <span data-ttu-id="e44c9-1735">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-1735">encryptedCredential</span></span> |<span data-ttu-id="e44c9-1736">Hello 게이트웨이로 암호화 된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1736">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="e44c9-1737">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1737">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1738">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1738">Example</span></span>

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

<span data-ttu-id="e44c9-1739">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1739">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-1740">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1740">Dataset</span></span>
<span data-ttu-id="e44c9-1741">toodefine Cassandra dataset 집합 hello **형식** hello 데이터 집합의 너무**CassandraTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1741">toodefine a Cassandra dataset, set hello **type** of hello dataset too**CassandraTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1742">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1742">Property</span></span> | <span data-ttu-id="e44c9-1743">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1743">Description</span></span> | <span data-ttu-id="e44c9-1744">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1744">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1745">keyspace</span><span class="sxs-lookup"><span data-stu-id="e44c9-1745">keyspace</span></span> |<span data-ttu-id="e44c9-1746">키 스페이스 hello 또는 Cassandra 데이터베이스에서 스키마의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1746">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="e44c9-1747">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1747">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="e44c9-1748">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1748">tableName</span></span> |<span data-ttu-id="e44c9-1749">Hello Cassandra 데이터베이스 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1749">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="e44c9-1750">예(**CassandraSource**의 **query**가 정의되지 않은 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1750">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1751">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1751">Example</span></span>

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

<span data-ttu-id="e44c9-1752">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1752">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#dataset-properties) article.</span></span> 

### <a name="cassandra-source-in-copy-activity"></a><span data-ttu-id="e44c9-1753">복사 활동의 Cassandra 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1753">Cassandra Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1754">Cassandra에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**CassandraSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 :</span><span class="sxs-lookup"><span data-stu-id="e44c9-1754">If you are copying data from Cassandra, set hello **source type** of hello copy activity too**CassandraSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1755">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1755">Property</span></span> | <span data-ttu-id="e44c9-1756">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1756">Description</span></span> | <span data-ttu-id="e44c9-1757">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1757">Allowed values</span></span> | <span data-ttu-id="e44c9-1758">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1758">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1759">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1759">query</span></span> |<span data-ttu-id="e44c9-1760">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1760">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1761">SQL-92 쿼리 또는 CQL 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1761">SQL-92 query or CQL query.</span></span> <span data-ttu-id="e44c9-1762">[CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1762">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="e44c9-1763">SQL 쿼리를 사용할 때 지정 **키 스페이스 name.table 이름** tooquery 원하는 toorepresent hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1763">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="e44c9-1764">아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1764">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="e44c9-1765">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="e44c9-1765">consistencyLevel</span></span> |<span data-ttu-id="e44c9-1766">hello 일관성 수준이 지정 복제 개수 데이터 toohello 클라이언트 응용 프로그램을 반환 하기 전에 tooa 읽기 요청 응답 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1766">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="e44c9-1767">Cassandra 검사 읽기 요청을 데이터 toosatisfy hello에 대 한 복제본의 지정 된 수를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1767">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="e44c9-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1768">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="e44c9-1769">자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1769">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="e44c9-1770">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1770">No.</span></span> <span data-ttu-id="e44c9-1771">기본값은 ONE입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1771">Default value is ONE.</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1772">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1772">Example</span></span>
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
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

<span data-ttu-id="e44c9-1773">자세한 내용은 [Cassandra 커넥터](data-factory-onprem-cassandra-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1773">For more information, see [Cassandra connector](data-factory-onprem-cassandra-connector.md#copy-activity-properties) article.</span></span>

## <a name="mongodb"></a><span data-ttu-id="e44c9-1774">MongoDB</span><span class="sxs-lookup"><span data-stu-id="e44c9-1774">MongoDB</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-1775">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1775">Linked service</span></span>
<span data-ttu-id="e44c9-1776">연결 된 서비스를 집합 hello toodefine는 MongoDB **형식** hello 연결 서비스 너무**OnPremisesMongoDB**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1776">toodefine a MongoDB linked service, set hello **type** of hello linked service too**OnPremisesMongoDB**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1777">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1777">Property</span></span> | <span data-ttu-id="e44c9-1778">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1778">Description</span></span> | <span data-ttu-id="e44c9-1779">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1779">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1780">server</span><span class="sxs-lookup"><span data-stu-id="e44c9-1780">server</span></span> |<span data-ttu-id="e44c9-1781">Hello MongoDB 서버의 IP 주소 또는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1781">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="e44c9-1782">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1782">Yes</span></span> |
| <span data-ttu-id="e44c9-1783">포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-1783">port</span></span> |<span data-ttu-id="e44c9-1784">MongoDB 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1784">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="e44c9-1785">선택 사항, 기본값: 27017</span><span class="sxs-lookup"><span data-stu-id="e44c9-1785">Optional, default value: 27017</span></span> |
| <span data-ttu-id="e44c9-1786">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-1786">authenticationType</span></span> |<span data-ttu-id="e44c9-1787">Basic 또는 Anonymous입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1787">Basic, or Anonymous.</span></span> |<span data-ttu-id="e44c9-1788">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1788">Yes</span></span> |
| <span data-ttu-id="e44c9-1789">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-1789">username</span></span> |<span data-ttu-id="e44c9-1790">사용자 계정 tooaccess MongoDB 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1790">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="e44c9-1791">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1791">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="e44c9-1792">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1792">password</span></span> |<span data-ttu-id="e44c9-1793">Hello 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1793">Password for hello user.</span></span> |<span data-ttu-id="e44c9-1794">예(기본 인증을 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1794">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="e44c9-1795">authSource</span><span class="sxs-lookup"><span data-stu-id="e44c9-1795">authSource</span></span> |<span data-ttu-id="e44c9-1796">원하는 toouse toocheck 자격 증명 인증에 대 한 hello MongoDB 데이터베이스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1796">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="e44c9-1797">선택 사항(기본 인증을 사용하는 경우).</span><span class="sxs-lookup"><span data-stu-id="e44c9-1797">Optional (if basic authentication is used).</span></span> <span data-ttu-id="e44c9-1798">기본값: hello 관리자 계정 및 databaseName 속성을 사용 하 여 지정 하는 hello 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1798">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="e44c9-1799">databaseName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1799">databaseName</span></span> |<span data-ttu-id="e44c9-1800">원하는 tooaccess hello MongoDB 데이터베이스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1800">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="e44c9-1801">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1801">Yes</span></span> |
| <span data-ttu-id="e44c9-1802">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1802">gatewayName</span></span> |<span data-ttu-id="e44c9-1803">Hello 데이터 저장소에 액세스 하는 hello 게이트웨이의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1803">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="e44c9-1804">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1804">Yes</span></span> |
| <span data-ttu-id="e44c9-1805">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-1805">encryptedCredential</span></span> |<span data-ttu-id="e44c9-1806">게이트웨이에 의해 암호화된 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1806">Credential encrypted by gateway.</span></span> |<span data-ttu-id="e44c9-1807">옵션</span><span class="sxs-lookup"><span data-stu-id="e44c9-1807">Optional</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1808">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1808">Example</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

<span data-ttu-id="e44c9-1809">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1809">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#linked-service-properties)</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1810">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1810">Dataset</span></span>
<span data-ttu-id="e44c9-1811">toodefine MongoDB dataset 집합 hello **형식** hello 데이터 집합의 너무**MongoDbCollection**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1811">toodefine a MongoDB dataset, set hello **type** of hello dataset too**MongoDbCollection**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1812">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1812">Property</span></span> | <span data-ttu-id="e44c9-1813">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1813">Description</span></span> | <span data-ttu-id="e44c9-1814">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1814">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1815">collectionName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1815">collectionName</span></span> |<span data-ttu-id="e44c9-1816">MongoDB 데이터베이스의 hello 컬렉션의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1816">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="e44c9-1817">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1817">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1818">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1818">Example</span></span>

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

<span data-ttu-id="e44c9-1819">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1819">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#dataset-properties)</span></span>

#### <a name="mongodb-source-in-copy-activity"></a><span data-ttu-id="e44c9-1820">복사 활동의 MongoDB 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1820">MongoDB Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1821">MongoDB에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**MongoDbSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1821">If you are copying data from MongoDB, set hello **source type** of hello copy activity too**MongoDbSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1822">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1822">Property</span></span> | <span data-ttu-id="e44c9-1823">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1823">Description</span></span> | <span data-ttu-id="e44c9-1824">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1824">Allowed values</span></span> | <span data-ttu-id="e44c9-1825">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1825">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1826">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-1826">query</span></span> |<span data-ttu-id="e44c9-1827">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1827">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-1828">SQL-92 쿼리 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1828">SQL-92 query string.</span></span> <span data-ttu-id="e44c9-1829">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-1829">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-1830">아니요(**데이터 집합**의 **collectionName**이 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1830">No (if **collectionName** of **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1831">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1831">Example</span></span>

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

<span data-ttu-id="e44c9-1832">자세한 내용은 [MongoDB 커넥터](data-factory-on-premises-mongodb-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1832">For more information, see [MongoDB connector article](data-factory-on-premises-mongodb-connector.md#copy-activity-properties)</span></span>

## <a name="amazon-s3"></a><span data-ttu-id="e44c9-1833">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="e44c9-1833">Amazon S3</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-1834">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1834">Linked service</span></span>
<span data-ttu-id="e44c9-1835">연결 된 서비스를 집합 hello toodefine Amazon S3 **형식** hello 연결 서비스 너무**AwsAccessKey**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션 :</span><span class="sxs-lookup"><span data-stu-id="e44c9-1835">toodefine an Amazon S3 linked service, set hello **type** of hello linked service too**AwsAccessKey**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-1836">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1836">Property</span></span> | <span data-ttu-id="e44c9-1837">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1837">Description</span></span> | <span data-ttu-id="e44c9-1838">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1838">Allowed values</span></span> | <span data-ttu-id="e44c9-1839">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1839">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1840">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="e44c9-1840">accessKeyID</span></span> |<span data-ttu-id="e44c9-1841">Hello 비밀 선택 키의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1841">ID of hello secret access key.</span></span> |<span data-ttu-id="e44c9-1842">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1842">string</span></span> |<span data-ttu-id="e44c9-1843">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1843">Yes</span></span> |
| <span data-ttu-id="e44c9-1844">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="e44c9-1844">secretAccessKey</span></span> |<span data-ttu-id="e44c9-1845">자체 hello 비밀 선택 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1845">hello secret access key itself.</span></span> |<span data-ttu-id="e44c9-1846">암호화된 비밀 문자열</span><span class="sxs-lookup"><span data-stu-id="e44c9-1846">Encrypted secret string</span></span> |<span data-ttu-id="e44c9-1847">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1847">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-1848">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1848">Example</span></span>
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

<span data-ttu-id="e44c9-1849">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1849">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1850">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1850">Dataset</span></span>
<span data-ttu-id="e44c9-1851">데이터 집합 toodefine Amazon S3 집합 hello **형식** hello 데이터 집합의 너무**AmazonS3**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1851">toodefine an Amazon S3 dataset, set hello **type** of hello dataset too**AmazonS3**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1852">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1852">Property</span></span> | <span data-ttu-id="e44c9-1853">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1853">Description</span></span> | <span data-ttu-id="e44c9-1854">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1854">Allowed values</span></span> | <span data-ttu-id="e44c9-1855">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1855">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1856">bucketName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1856">bucketName</span></span> |<span data-ttu-id="e44c9-1857">hello S3 버킷 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1857">hello S3 bucket name.</span></span> |<span data-ttu-id="e44c9-1858">문자열</span><span class="sxs-lookup"><span data-stu-id="e44c9-1858">String</span></span> |<span data-ttu-id="e44c9-1859">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1859">Yes</span></span> |
| <span data-ttu-id="e44c9-1860">key</span><span class="sxs-lookup"><span data-stu-id="e44c9-1860">key</span></span> |<span data-ttu-id="e44c9-1861">S3 hello 개체 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1861">hello S3 object key.</span></span> |<span data-ttu-id="e44c9-1862">문자열</span><span class="sxs-lookup"><span data-stu-id="e44c9-1862">String</span></span> |<span data-ttu-id="e44c9-1863">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1863">No</span></span> |
| <span data-ttu-id="e44c9-1864">접두사</span><span class="sxs-lookup"><span data-stu-id="e44c9-1864">prefix</span></span> |<span data-ttu-id="e44c9-1865">Hello S3 개체 키에 대 한 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1865">Prefix for hello S3 object key.</span></span> <span data-ttu-id="e44c9-1866">이 접두사로 시작하는 키를 가진 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1866">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="e44c9-1867">키가 비어 있을 때에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1867">Applies only when key is empty.</span></span> |<span data-ttu-id="e44c9-1868">string</span><span class="sxs-lookup"><span data-stu-id="e44c9-1868">String</span></span> |<span data-ttu-id="e44c9-1869">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1869">No</span></span> |
| <span data-ttu-id="e44c9-1870">버전</span><span class="sxs-lookup"><span data-stu-id="e44c9-1870">version</span></span> |<span data-ttu-id="e44c9-1871">S3 개체 S3 버전 관리를 사용 하는 경우의 hello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1871">hello version of S3 object if S3 versioning is enabled.</span></span> |<span data-ttu-id="e44c9-1872">문자열</span><span class="sxs-lookup"><span data-stu-id="e44c9-1872">String</span></span> |<span data-ttu-id="e44c9-1873">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1873">No</span></span> |
| <span data-ttu-id="e44c9-1874">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-1874">format</span></span> | <span data-ttu-id="e44c9-1875">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1875">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-1876">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1876">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-1877">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1877">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-1878">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1878">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-1879">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1879">No</span></span> | |
| <span data-ttu-id="e44c9-1880">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-1880">compression</span></span> | <span data-ttu-id="e44c9-1881">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1881">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-1882">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1882">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-1883">지원 되는 hello 수준은: **최적** 및 **fastest 이면**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1883">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-1884">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1884">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-1885">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1885">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="e44c9-1886">bucketName + 키 hello S3 개체 여기서 버킷에 S3 개체에 대 한 hello 루트 컨테이너 하 고 키가 hello 전체 경로 tooS3 개체의 hello 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1886">bucketName + key specifies hello location of hello S3 object where bucket is hello root container for S3 objects and key is hello full path tooS3 object.</span></span>

#### <a name="example-sample-dataset-with-prefix"></a><span data-ttu-id="e44c9-1887">예제: 샘플 데이터 집합(prefix 포함)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1887">Example: Sample dataset with prefix</span></span>

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
#### <a name="example-sample-data-set-with-version"></a><span data-ttu-id="e44c9-1888">예제: 샘플 데이터 집합(version 포함)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1888">Example: Sample data set (with version)</span></span>

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

#### <a name="example-dynamic-paths-for-s3"></a><span data-ttu-id="e44c9-1889">예제: S3에 대한 동적 경로</span><span class="sxs-lookup"><span data-stu-id="e44c9-1889">Example: Dynamic paths for S3</span></span>
<span data-ttu-id="e44c9-1890">Hello 샘플 hello Amazon S3 데이터 집합에서 키 및 bucketName 속성에 대 한 고정된 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1890">In hello sample, we use fixed values for key and bucketName properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

<span data-ttu-id="e44c9-1891">SliceStart와 같은 시스템 변수를 사용 하 여 hello 키와 bucketName 런타임에 동적으로 계산 되는 데이터 팩터리를 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1891">You can have Data Factory calculate hello key and bucketName dynamically at runtime by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="e44c9-1892">작업을 수행할 수는 Amazon S3 데이터 집합의 hello 접두사 속성에 대 한 hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1892">You can do hello same for hello prefix property of an Amazon S3 dataset.</span></span> <span data-ttu-id="e44c9-1893">지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1893">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of supported functions and variables.</span></span>

<span data-ttu-id="e44c9-1894">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#dataset-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1894">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="e44c9-1895">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1895">File System Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1896">Amazon s 3에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 :</span><span class="sxs-lookup"><span data-stu-id="e44c9-1896">If you are copying data from Amazon S3, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>


| <span data-ttu-id="e44c9-1897">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1897">Property</span></span> | <span data-ttu-id="e44c9-1898">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1898">Description</span></span> | <span data-ttu-id="e44c9-1899">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1899">Allowed values</span></span> | <span data-ttu-id="e44c9-1900">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1900">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1901">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-1901">recursive</span></span> |<span data-ttu-id="e44c9-1902">Hello 디렉터리 개체 toorecursively 목록 S3 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1902">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="e44c9-1903">True/False</span><span class="sxs-lookup"><span data-stu-id="e44c9-1903">true/false</span></span> |<span data-ttu-id="e44c9-1904">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1904">No</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-1905">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1905">Example</span></span>


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

<span data-ttu-id="e44c9-1906">자세한 내용은 [Amazon S3 커넥터](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties) 문서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1906">For more information, see [Amazon S3 connector article](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).</span></span>

## <a name="file-system"></a><span data-ttu-id="e44c9-1907">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="e44c9-1907">File System</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-1908">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1908">Linked service</span></span>
<span data-ttu-id="e44c9-1909">온-프레미스 파일 시스템 tooan Azure 데이터 팩터리에 hello로 연결할 수 있습니다 **온-프레미스 파일 서버** 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1909">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="e44c9-1910">다음 표에서 hello JSON 요소를 특정 toohello 온-프레미스 파일 서버를 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1910">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="e44c9-1911">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1911">Property</span></span> | <span data-ttu-id="e44c9-1912">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1912">Description</span></span> | <span data-ttu-id="e44c9-1913">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1913">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1914">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-1914">type</span></span> |<span data-ttu-id="e44c9-1915">Hello type 속성이 너무 설정 되어 있는지 확인**OnPremisesFileServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1915">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="e44c9-1916">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1916">Yes</span></span> |
| <span data-ttu-id="e44c9-1917">host</span><span class="sxs-lookup"><span data-stu-id="e44c9-1917">host</span></span> |<span data-ttu-id="e44c9-1918">Toocopy hello 폴더의 hello 루트 경로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1918">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="e44c9-1919">Hello 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1919">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="e44c9-1920">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1920">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="e44c9-1921">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1921">Yes</span></span> |
| <span data-ttu-id="e44c9-1922">userid</span><span class="sxs-lookup"><span data-stu-id="e44c9-1922">userid</span></span> |<span data-ttu-id="e44c9-1923">Hello 있는 사용자에 게 액세스 toohello 서버 hello ID를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1923">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="e44c9-1924">아니요(encryptedCredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1924">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="e44c9-1925">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-1925">password</span></span> |<span data-ttu-id="e44c9-1926">Hello 사용자 (userid)에 대 한 hello 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1926">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="e44c9-1927">아니요(encryptedcredential을 선택하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1927">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="e44c9-1928">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-1928">encryptedCredential</span></span> |<span data-ttu-id="e44c9-1929">새로 만들기-AzureRmDataFactoryEncryptValue hello cmdlet을 실행 하 여 얻을 수 있는 암호화 hello 자격 증명을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1929">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="e44c9-1930">아니요 (일반 텍스트로 toospecify userid 및 password 선택) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="e44c9-1930">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="e44c9-1931">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1931">gatewayName</span></span> |<span data-ttu-id="e44c9-1932">데이터 팩터리 tooconnect toohello 온-프레미스 파일 서버를 사용 해야 하는 hello 게이트웨이의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1932">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="e44c9-1933">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1933">Yes</span></span> |

#### <a name="sample-folder-path-definitions"></a><span data-ttu-id="e44c9-1934">샘플 폴더 경로 정의</span><span class="sxs-lookup"><span data-stu-id="e44c9-1934">Sample folder path definitions</span></span> 
| <span data-ttu-id="e44c9-1935">시나리오</span><span class="sxs-lookup"><span data-stu-id="e44c9-1935">Scenario</span></span> | <span data-ttu-id="e44c9-1936">연결된 서비스 정의의 호스트</span><span class="sxs-lookup"><span data-stu-id="e44c9-1936">Host in linked service definition</span></span> | <span data-ttu-id="e44c9-1937">데이터 집합 정의의 folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-1937">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1938">데이터 관리 게이트웨이 컴퓨터의 로컬 폴더: </span><span class="sxs-lookup"><span data-stu-id="e44c9-1938">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="e44c9-1939">예: D:\\\* 또는 D:\folder\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="e44c9-1939">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="e44c9-1940">D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1940">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="e44c9-1941">localhost(데이터 관리 게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1941">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="e44c9-1942">.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1942">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="e44c9-1943">D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1943">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="e44c9-1944">원격 공유 폴더: </span><span class="sxs-lookup"><span data-stu-id="e44c9-1944">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="e44c9-1945">예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\*</span><span class="sxs-lookup"><span data-stu-id="e44c9-1945">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="e44c9-1946">\\\\\\\\myserver\\\\share</span><span class="sxs-lookup"><span data-stu-id="e44c9-1946">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="e44c9-1947">.\\\\ 또는 folder\\\\subfolder</span><span class="sxs-lookup"><span data-stu-id="e44c9-1947">.\\\\ or folder\\\\subfolder</span></span> |


#### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="e44c9-1948">예제: 일반 텍스트에 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1948">Example: Using username and password in plain text</span></span>

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

#### <a name="example-using-encryptedcredential"></a><span data-ttu-id="e44c9-1949">예제: encryptedcredential 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1949">Example: Using encryptedcredential</span></span>

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

<span data-ttu-id="e44c9-1950">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1950">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#linked-service-properties).</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-1951">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-1951">Dataset</span></span>
<span data-ttu-id="e44c9-1952">파일 시스템 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1952">toodefine a File System dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-1953">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1953">Property</span></span> | <span data-ttu-id="e44c9-1954">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1954">Description</span></span> | <span data-ttu-id="e44c9-1955">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1955">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-1956">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-1956">folderPath</span></span> |<span data-ttu-id="e44c9-1957">Hello 하위 경로 toohello 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1957">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="e44c9-1958">Hello 이스케이프 문자를 사용 하 여 ' \' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1958">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="e44c9-1959">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1959">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="e44c9-1960">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1960">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="e44c9-1961">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-1961">Yes</span></span> |
| <span data-ttu-id="e44c9-1962">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-1962">fileName</span></span> |<span data-ttu-id="e44c9-1963">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1963">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="e44c9-1964">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1964">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="e44c9-1965">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면, hello hello 생성 된 파일의 이름이 형식에 따라 hello에:</span><span class="sxs-lookup"><span data-stu-id="e44c9-1965">When fileName is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="e44c9-1966">`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="e44c9-1966">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="e44c9-1967">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1967">No</span></span> |
| <span data-ttu-id="e44c9-1968">fileFilter</span><span class="sxs-lookup"><span data-stu-id="e44c9-1968">fileFilter</span></span> |<span data-ttu-id="e44c9-1969">필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1969">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="e44c9-1970">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1970">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="e44c9-1971">예 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="e44c9-1971">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="e44c9-1972">예 2: "fileFilter": 2016-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="e44c9-1972">Example 2: "fileFilter": 2016-1-?.txt"</span></span><br/><br/><span data-ttu-id="e44c9-1973">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1973">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="e44c9-1974">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1974">No</span></span> |
| <span data-ttu-id="e44c9-1975">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-1975">partitionedBy</span></span> |<span data-ttu-id="e44c9-1976">시계열 데이터에 대 한 partitionedBy toospecify 동적 folderPath/파일 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1976">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="e44c9-1977">예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1977">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-1978">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1978">No</span></span> |
| <span data-ttu-id="e44c9-1979">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-1979">format</span></span> | <span data-ttu-id="e44c9-1980">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1980">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-1981">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1981">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-1982">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1982">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-1983">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1983">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-1984">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1984">No</span></span> |
| <span data-ttu-id="e44c9-1985">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-1985">compression</span></span> | <span data-ttu-id="e44c9-1986">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1986">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-1987">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1987">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-1988">[Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1988">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-1989">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-1989">No</span></span> |

> [!NOTE]
> <span data-ttu-id="e44c9-1990">fileName 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1990">You cannot use fileName and fileFilter simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-1991">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-1991">Example</span></span>

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

<span data-ttu-id="e44c9-1992">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-1992">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#dataset-properties).</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="e44c9-1993">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-1993">File System Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-1994">파일 시스템에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-1994">If you are copying data from File System, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-1995">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-1995">Property</span></span> | <span data-ttu-id="e44c9-1996">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-1996">Description</span></span> | <span data-ttu-id="e44c9-1997">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-1997">Allowed values</span></span> | <span data-ttu-id="e44c9-1998">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-1998">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-1999">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-1999">recursive</span></span> |<span data-ttu-id="e44c9-2000">Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2000">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-2001">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2001">True, False (default)</span></span> |<span data-ttu-id="e44c9-2002">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2002">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2003">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2003">Example</span></span>

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
<span data-ttu-id="e44c9-2004">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2004">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

### <a name="file-system-sink-in-copy-activity"></a><span data-ttu-id="e44c9-2005">복사 활동의 파일 시스템 싱크</span><span class="sxs-lookup"><span data-stu-id="e44c9-2005">File System Sink in Copy Activity</span></span>
<span data-ttu-id="e44c9-2006">시스템 데이터 tooFile 복사 하는 경우 설정 hello **싱크 유형** hello의 복사 작업이 너무**FileSystemSink**, 다음 hello에 대 한 속성을 지정 하 고 **싱크** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2006">If you are copying data tooFile System, set hello **sink type** of hello copy activity too**FileSystemSink**, and specify following properties in hello **sink** section:</span></span>

| <span data-ttu-id="e44c9-2007">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2007">Property</span></span> | <span data-ttu-id="e44c9-2008">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2008">Description</span></span> | <span data-ttu-id="e44c9-2009">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2009">Allowed values</span></span> | <span data-ttu-id="e44c9-2010">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2010">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2011">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="e44c9-2011">copyBehavior</span></span> |<span data-ttu-id="e44c9-2012">파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2012">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="e44c9-2013">**PreserveHierarchy:** hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2013">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="e44c9-2014">즉, hello 소스 파일 toohello 원본 폴더의 상대 경로 hello hello hello 대상 파일 toohello 대상 폴더의 상대 경로와 같은 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2014">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="e44c9-2015">**FlattenHierarchy:** hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2015">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="e44c9-2016">hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2016">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="e44c9-2017">**MergeFiles:** hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2017">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="e44c9-2018">Hello 파일 이름/blob 이름이 지정 된 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2018">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="e44c9-2019">그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2019">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="e44c9-2020">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2020">No</span></span> |
<span data-ttu-id="e44c9-2021">auto-</span><span class="sxs-lookup"><span data-stu-id="e44c9-2021">auto-</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-2022">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2022">Example</span></span>

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

<span data-ttu-id="e44c9-2023">자세한 내용은 [파일 시스템 커넥터](data-factory-onprem-file-system-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2023">For more information, see [File System connector article](data-factory-onprem-file-system-connector.md#copy-activity-properties).</span></span>

## <a name="ftp"></a><span data-ttu-id="e44c9-2024">FTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-2024">FTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-2025">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2025">Linked service</span></span>
<span data-ttu-id="e44c9-2026">연결 된 서비스를 집합 hello toodefine FTP **형식** hello 연결 서비스 너무**ftp 서버**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2026">toodefine an FTP linked service, set hello **type** of hello linked service too**FtpServer**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2027">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2027">Property</span></span> | <span data-ttu-id="e44c9-2028">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2028">Description</span></span> | <span data-ttu-id="e44c9-2029">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2029">Required</span></span> | <span data-ttu-id="e44c9-2030">기본값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2030">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2031">host</span><span class="sxs-lookup"><span data-stu-id="e44c9-2031">host</span></span> |<span data-ttu-id="e44c9-2032">FTP 서버 hello의 이름 또는 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e44c9-2032">Name or IP address of hello FTP Server</span></span> |<span data-ttu-id="e44c9-2033">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2033">Yes</span></span> |&nbsp; |
| <span data-ttu-id="e44c9-2034">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2034">authenticationType</span></span> |<span data-ttu-id="e44c9-2035">인증 유형 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-2035">Specify authentication type</span></span> |<span data-ttu-id="e44c9-2036">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2036">Yes</span></span> |<span data-ttu-id="e44c9-2037">기본, 익명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2037">Basic, Anonymous</span></span> |
| <span data-ttu-id="e44c9-2038">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2038">username</span></span> |<span data-ttu-id="e44c9-2039">액세스 toohello FTP 서버에 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="e44c9-2039">User who has access toohello FTP server</span></span> |<span data-ttu-id="e44c9-2040">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2040">No</span></span> |&nbsp; |
| <span data-ttu-id="e44c9-2041">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2041">password</span></span> |<span data-ttu-id="e44c9-2042">Hello 사용자 (사용자 이름)에 대 한 암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2042">Password for hello user (username)</span></span> |<span data-ttu-id="e44c9-2043">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2043">No</span></span> |&nbsp; |
| <span data-ttu-id="e44c9-2044">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-2044">encryptedCredential</span></span> |<span data-ttu-id="e44c9-2045">암호화 된 자격 증명 tooaccess hello FTP 서버</span><span class="sxs-lookup"><span data-stu-id="e44c9-2045">Encrypted credential tooaccess hello FTP server</span></span> |<span data-ttu-id="e44c9-2046">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2046">No</span></span> |&nbsp; |
| <span data-ttu-id="e44c9-2047">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2047">gatewayName</span></span> |<span data-ttu-id="e44c9-2048">Hello 데이터 관리 게이트웨이에 게이트웨이 tooconnect tooan의 이름 온-프레미스 FTP 서버</span><span class="sxs-lookup"><span data-stu-id="e44c9-2048">Name of hello Data Management Gateway gateway tooconnect tooan on-premises FTP server</span></span> |<span data-ttu-id="e44c9-2049">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2049">No</span></span> |&nbsp; |
| <span data-ttu-id="e44c9-2050">포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-2050">port</span></span> |<span data-ttu-id="e44c9-2051">어떤 hello FTP 서버 수신 포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-2051">Port on which hello FTP server is listening</span></span> |<span data-ttu-id="e44c9-2052">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2052">No</span></span> |<span data-ttu-id="e44c9-2053">21</span><span class="sxs-lookup"><span data-stu-id="e44c9-2053">21</span></span> |
| <span data-ttu-id="e44c9-2054">enableSsl</span><span class="sxs-lookup"><span data-stu-id="e44c9-2054">enableSsl</span></span> |<span data-ttu-id="e44c9-2055">Toouse SSL/TLS 채널을 통해 FTP 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2055">Specify whether toouse FTP over SSL/TLS channel</span></span> |<span data-ttu-id="e44c9-2056">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2056">No</span></span> |<span data-ttu-id="e44c9-2057">true</span><span class="sxs-lookup"><span data-stu-id="e44c9-2057">true</span></span> |
| <span data-ttu-id="e44c9-2058">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="e44c9-2058">enableServerCertificateValidation</span></span> |<span data-ttu-id="e44c9-2059">SSL/TLS 채널을 통해 FTP를 사용 하는 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2059">Specify whether tooenable server SSL certificate validation when using FTP over SSL/TLS channel</span></span> |<span data-ttu-id="e44c9-2060">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2060">No</span></span> |<span data-ttu-id="e44c9-2061">true</span><span class="sxs-lookup"><span data-stu-id="e44c9-2061">true</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="e44c9-2062">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2062">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="e44c9-2063">예제: 기본 인증에 일반 텍스트 형식의 사용자 이름 및 암호 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2063">Example: Using username and password in plain text for basic authentication</span></span>

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

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="e44c9-2064">예제: port, enableSsl, enableServerCertificateValidation 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2064">Example: Using port, enableSsl, enableServerCertificateValidation</span></span>

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

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="e44c9-2065">예제: 인증 및 게이트웨이에 encryptedCredential 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2065">Example: Using encryptedCredential for authentication and gateway</span></span>

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

<span data-ttu-id="e44c9-2066">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2066">For more information, see [FTP connector](data-factory-ftp-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-2067">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2067">Dataset</span></span>
<span data-ttu-id="e44c9-2068">FTP toodefine 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2068">toodefine an FTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2069">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2069">Property</span></span> | <span data-ttu-id="e44c9-2070">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2070">Description</span></span> | <span data-ttu-id="e44c9-2071">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2071">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2072">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-2072">folderPath</span></span> |<span data-ttu-id="e44c9-2073">하위 경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2073">Sub path toohello folder.</span></span> <span data-ttu-id="e44c9-2074">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2074">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="e44c9-2075">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2075">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="e44c9-2076">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2076">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="e44c9-2077">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2077">Yes</span></span> 
| <span data-ttu-id="e44c9-2078">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2078">fileName</span></span> |<span data-ttu-id="e44c9-2079">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2079">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="e44c9-2080">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2080">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="e44c9-2081">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2081">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="e44c9-2082">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2082">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e44c9-2083">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2083">No</span></span> |
| <span data-ttu-id="e44c9-2084">fileFilter</span><span class="sxs-lookup"><span data-stu-id="e44c9-2084">fileFilter</span></span> |<span data-ttu-id="e44c9-2085">필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2085">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="e44c9-2086">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2086">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="e44c9-2087">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2087">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="e44c9-2088">예 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2088">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="e44c9-2089">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2089">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="e44c9-2090">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2090">This property is not supported with HDFS.</span></span> |<span data-ttu-id="e44c9-2091">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2091">No</span></span> |
| <span data-ttu-id="e44c9-2092">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-2092">partitionedBy</span></span> |<span data-ttu-id="e44c9-2093">partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2093">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="e44c9-2094">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2094">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-2095">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2095">No</span></span> |
| <span data-ttu-id="e44c9-2096">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-2096">format</span></span> | <span data-ttu-id="e44c9-2097">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2097">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-2098">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2098">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-2099">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2099">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-2100">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2100">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-2101">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2101">No</span></span> |
| <span data-ttu-id="e44c9-2102">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-2102">compression</span></span> | <span data-ttu-id="e44c9-2103">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2103">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-2104">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2104">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**; and supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-2105">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2105">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-2106">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2106">No</span></span> |
| <span data-ttu-id="e44c9-2107">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="e44c9-2107">useBinaryTransfer</span></span> |<span data-ttu-id="e44c9-2108">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2108">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="e44c9-2109">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2109">True for binary mode and false ASCII.</span></span> <span data-ttu-id="e44c9-2110">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2110">Default value: True.</span></span> <span data-ttu-id="e44c9-2111">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2111">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="e44c9-2112">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2112">No</span></span> |

> [!NOTE]
> <span data-ttu-id="e44c9-2113">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2113">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-2114">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2114">Example</span></span>

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="e44c9-2115">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2115">For more information, see [FTP connector](data-factory-ftp-connector.md#dataset-properties) article.</span></span>

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="e44c9-2116">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2116">File System Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2117">FTP 서버에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2117">If you are copying data from an FTP server, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2118">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2118">Property</span></span> | <span data-ttu-id="e44c9-2119">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2119">Description</span></span> | <span data-ttu-id="e44c9-2120">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2120">Allowed values</span></span> | <span data-ttu-id="e44c9-2121">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2121">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2122">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-2122">recursive</span></span> |<span data-ttu-id="e44c9-2123">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2123">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-2124">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2124">True, False (default)</span></span> |<span data-ttu-id="e44c9-2125">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2125">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2126">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2126">Example</span></span>

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

<span data-ttu-id="e44c9-2127">자세한 내용은 [FTP 커넥터](data-factory-ftp-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2127">For more information, see [FTP connector](data-factory-ftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="hdfs"></a><span data-ttu-id="e44c9-2128">HDFS</span><span class="sxs-lookup"><span data-stu-id="e44c9-2128">HDFS</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-2129">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2129">Linked service</span></span>
<span data-ttu-id="e44c9-2130">연결 된 서비스를 집합 hello toodefine는 HDFS **형식** hello 연결 서비스 너무**Hdfs**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2130">toodefine a HDFS linked service, set hello **type** of hello linked service too**Hdfs**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2131">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2131">Property</span></span> | <span data-ttu-id="e44c9-2132">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2132">Description</span></span> | <span data-ttu-id="e44c9-2133">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2133">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2134">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2134">type</span></span> |<span data-ttu-id="e44c9-2135">hello type 속성 설정 해야 합니다: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2135">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="e44c9-2136">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2136">Yes</span></span> |
| <span data-ttu-id="e44c9-2137">Url</span><span class="sxs-lookup"><span data-stu-id="e44c9-2137">Url</span></span> |<span data-ttu-id="e44c9-2138">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="e44c9-2138">URL toohello HDFS</span></span> |<span data-ttu-id="e44c9-2139">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2139">Yes</span></span> |
| <span data-ttu-id="e44c9-2140">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2140">authenticationType</span></span> |<span data-ttu-id="e44c9-2141">익명 또는 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2141">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="e44c9-2142">toouse **Kerberos 인증** HDFS 커넥터에 대 한 참조 너무[이 여기서](#use-kerberos-authentication-for-hdfs-connector) 온-프레미스 환경을 tooset 적절 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2142">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="e44c9-2143">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2143">Yes</span></span> |
| <span data-ttu-id="e44c9-2144">userName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2144">userName</span></span> |<span data-ttu-id="e44c9-2145">Windows 인증에 대한 사용자 이름.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2145">Username for Windows authentication.</span></span> |<span data-ttu-id="e44c9-2146">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2146">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="e44c9-2147">password</span><span class="sxs-lookup"><span data-stu-id="e44c9-2147">password</span></span> |<span data-ttu-id="e44c9-2148">Windows 인증에 대한 암호.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2148">Password for Windows authentication.</span></span> |<span data-ttu-id="e44c9-2149">예(Windows 인증에 대한)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2149">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="e44c9-2150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2150">gatewayName</span></span> |<span data-ttu-id="e44c9-2151">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello HDFS 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2151">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="e44c9-2152">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2152">Yes</span></span> |
| <span data-ttu-id="e44c9-2153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-2153">encryptedCredential</span></span> |<span data-ttu-id="e44c9-2154">[새 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 액세스 자격 증명의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2154">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="e44c9-2155">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2155">No</span></span> |

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="e44c9-2156">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2156">Example: Using Anonymous authentication</span></span>

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

#### <a name="example-using-windows-authentication"></a><span data-ttu-id="e44c9-2157">예제: Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2157">Example: Using Windows authentication</span></span>

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

<span data-ttu-id="e44c9-2158">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2158">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-2159">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2159">Dataset</span></span>
<span data-ttu-id="e44c9-2160">toodefine HDFS dataset 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2160">toodefine a HDFS dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2161">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2161">Property</span></span> | <span data-ttu-id="e44c9-2162">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2162">Description</span></span> | <span data-ttu-id="e44c9-2163">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2163">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2164">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-2164">folderPath</span></span> |<span data-ttu-id="e44c9-2165">경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2165">Path toohello folder.</span></span> <span data-ttu-id="e44c9-2166">예: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2166">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="e44c9-2167">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2167">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="e44c9-2168">예: 폴더\하위 폴더의 경우 폴더\\\\하위 폴더를 지정하고 d:\samplefolder의 경우 d:\\\\samplefolder를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2168">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="e44c9-2169">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2169">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="e44c9-2170">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2170">Yes</span></span> |
| <span data-ttu-id="e44c9-2171">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2171">fileName</span></span> |<span data-ttu-id="e44c9-2172">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2172">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="e44c9-2173">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2173">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="e44c9-2174">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2174">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="e44c9-2175">Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2175">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e44c9-2176">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2176">No</span></span> |
| <span data-ttu-id="e44c9-2177">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-2177">partitionedBy</span></span> |<span data-ttu-id="e44c9-2178">partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2178">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="e44c9-2179">예를 들어 folderPath는 매시간 데이터에 대해 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2179">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-2180">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2180">No</span></span> |
| <span data-ttu-id="e44c9-2181">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-2181">format</span></span> | <span data-ttu-id="e44c9-2182">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2182">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-2183">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2183">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-2184">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2184">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-2185">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2185">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-2186">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2186">No</span></span> |
| <span data-ttu-id="e44c9-2187">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-2187">compression</span></span> | <span data-ttu-id="e44c9-2188">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2188">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-2189">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2189">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-2190">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2190">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-2191">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2191">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-2192">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2192">No</span></span> |

> [!NOTE]
> <span data-ttu-id="e44c9-2193">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2193">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-2194">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2194">Example</span></span>

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

<span data-ttu-id="e44c9-2195">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2195">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="e44c9-2196">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2196">File System Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2197">HDFS에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2197">If you are copying data from HDFS, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

<span data-ttu-id="e44c9-2198">**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2198">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="e44c9-2199">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2199">Property</span></span> | <span data-ttu-id="e44c9-2200">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2200">Description</span></span> | <span data-ttu-id="e44c9-2201">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2201">Allowed values</span></span> | <span data-ttu-id="e44c9-2202">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2202">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2203">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-2203">recursive</span></span> |<span data-ttu-id="e44c9-2204">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2204">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-2205">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2205">True, False (default)</span></span> |<span data-ttu-id="e44c9-2206">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2206">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2207">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2207">Example</span></span>

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

<span data-ttu-id="e44c9-2208">자세한 내용은 [HDFS 커넥터](#data-factory-hdfs-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2208">For more information, see [HDFS connector](#data-factory-hdfs-connector.md#copy-activity-properties) article.</span></span>

## <a name="sftp"></a><span data-ttu-id="e44c9-2209">SFTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-2209">SFTP</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-2210">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2210">Linked service</span></span>
<span data-ttu-id="e44c9-2211">연결 된 서비스를 집합 hello toodefine SFTP **형식** hello 연결 서비스 너무**Sftp**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2211">toodefine an SFTP linked service, set hello **type** of hello linked service too**Sftp**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2212">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2212">Property</span></span> | <span data-ttu-id="e44c9-2213">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2213">Description</span></span> | <span data-ttu-id="e44c9-2214">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2214">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2215">host</span><span class="sxs-lookup"><span data-stu-id="e44c9-2215">host</span></span> | <span data-ttu-id="e44c9-2216">Hello SFTP 서버의 이름 또는 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2216">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="e44c9-2217">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2217">Yes</span></span> |
| <span data-ttu-id="e44c9-2218">포트</span><span class="sxs-lookup"><span data-stu-id="e44c9-2218">port</span></span> |<span data-ttu-id="e44c9-2219">어떤 hello SFTP 서버 수신 대기 중인 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2219">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="e44c9-2220">hello 기본값은: 21</span><span class="sxs-lookup"><span data-stu-id="e44c9-2220">hello default value is: 21</span></span> |<span data-ttu-id="e44c9-2221">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2221">No</span></span> |
| <span data-ttu-id="e44c9-2222">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2222">authenticationType</span></span> |<span data-ttu-id="e44c9-2223">인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2223">Specify authentication type.</span></span> <span data-ttu-id="e44c9-2224">허용되는 값은 **기본** 및 **SshPublicKey**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2224">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="e44c9-2225">너무 참조[기본 인증을 사용 하 여](#using-basic-authentication) 및 [를 사용 하 여 SSH 공개 키 인증](#using-ssh-public-key-authentication) 더 많은 속성 및 JSON 샘플에서 각각 섹션.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2225">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="e44c9-2226">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2226">Yes</span></span> |
| <span data-ttu-id="e44c9-2227">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="e44c9-2227">skipHostKeyValidation</span></span> | <span data-ttu-id="e44c9-2228">Tooskip 호스트 키 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2228">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="e44c9-2229">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2229">No.</span></span> <span data-ttu-id="e44c9-2230">hello 기본값: false</span><span class="sxs-lookup"><span data-stu-id="e44c9-2230">hello default value: false</span></span> |
| <span data-ttu-id="e44c9-2231">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="e44c9-2231">hostKeyFingerprint</span></span> | <span data-ttu-id="e44c9-2232">Hello 호스트 키의 지문 안녕하세요를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2232">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="e44c9-2233">예 경우 hello `skipHostKeyValidation` toofalse 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2233">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="e44c9-2234">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2234">gatewayName</span></span> |<span data-ttu-id="e44c9-2235">데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 SFTP 서버.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2235">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="e44c9-2236">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2236">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="e44c9-2237">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-2237">encryptedCredential</span></span> | <span data-ttu-id="e44c9-2238">암호화 된 자격 증명 tooaccess hello SFTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2238">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="e44c9-2239">자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에서 기본 인증 (사용자 이름 + 암호) 또는 SshPublicKey 인증 (사용자 이름 + 개인 키의 경로 또는 콘텐츠)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2239">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="e44c9-2240">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2240">No.</span></span> <span data-ttu-id="e44c9-2241">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2241">Apply only when copying data from an on-premises SFTP server.</span></span> |

#### <a name="example-using-basic-authentication"></a><span data-ttu-id="e44c9-2242">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2242">Example: Using basic authentication</span></span>

<span data-ttu-id="e44c9-2243">toouse 기본 인증 설정 `authenticationType` 으로 `Basic`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2243">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="e44c9-2244">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2244">Property</span></span> | <span data-ttu-id="e44c9-2245">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2245">Description</span></span> | <span data-ttu-id="e44c9-2246">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2246">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2247">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2247">username</span></span> | <span data-ttu-id="e44c9-2248">사용자가 액세스 toohello SFTP 서버입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2248">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="e44c9-2249">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2249">Yes</span></span> |
| <span data-ttu-id="e44c9-2250">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2250">password</span></span> | <span data-ttu-id="e44c9-2251">Hello 사용자 (사용자 이름)에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2251">Password for hello user (username).</span></span> | <span data-ttu-id="e44c9-2252">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2252">Yes</span></span> |

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

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="e44c9-2253">예제: 암호화된 자격 증명으로 기본 인증**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2253">Example: Basic authentication with encrypted credential**</span></span>

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

#### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="e44c9-2254">SSH 공개 키 인증 사용**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2254">Using SSH public key authentication:**</span></span>

<span data-ttu-id="e44c9-2255">toouse 기본 인증 설정 `authenticationType` 으로 `SshPublicKey`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2255">toouse basic authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="e44c9-2256">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2256">Property</span></span> | <span data-ttu-id="e44c9-2257">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2257">Description</span></span> | <span data-ttu-id="e44c9-2258">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2258">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2259">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2259">username</span></span> |<span data-ttu-id="e44c9-2260">액세스 toohello SFTP 서버에 있는 사용자</span><span class="sxs-lookup"><span data-stu-id="e44c9-2260">User who has access toohello SFTP server</span></span> |<span data-ttu-id="e44c9-2261">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2261">Yes</span></span> |
| <span data-ttu-id="e44c9-2262">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-2262">privateKeyPath</span></span> | <span data-ttu-id="e44c9-2263">절대 경로 toohello 지정 개인 키 파일 해당 게이트웨이에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2263">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="e44c9-2264">어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2264">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="e44c9-2265">온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2265">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="e44c9-2266">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="e44c9-2266">privateKeyContent</span></span> | <span data-ttu-id="e44c9-2267">Hello 개인 키 콘텐츠는 serialize 된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2267">A serialized string of hello private key content.</span></span> <span data-ttu-id="e44c9-2268">hello 복사 마법사 hello 개인 키 파일 읽고 hello 개인 키 콘텐츠를 자동으로 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2268">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="e44c9-2269">모든 다른 도구/SDK를 사용 하는 경우 hello privateKeyPath 속성을 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2269">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="e44c9-2270">어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2270">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="e44c9-2271">passPhrase</span><span class="sxs-lookup"><span data-stu-id="e44c9-2271">passPhrase</span></span> | <span data-ttu-id="e44c9-2272">암호 구문을 통해 hello 키 파일을 보호 하는 경우에 hello 전달 구를/암호 toodecrypt hello 개인 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2272">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="e44c9-2273">Yes 전달 구에 의해 hello 개인 키 파일 보호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2273">Yes if hello private key file is protected by a pass phrase.</span></span> |

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

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="e44c9-2274">예제: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2274">Example: SshPublicKey authentication using private key content**</span></span>

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
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

<span data-ttu-id="e44c9-2275">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2275">For more information, see [SFTP connector](data-factory-sftp-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-2276">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2276">Dataset</span></span>
<span data-ttu-id="e44c9-2277">toodefine SFTP 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**FileShare**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2277">toodefine an SFTP dataset, set hello **type** of hello dataset too**FileShare**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2278">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2278">Property</span></span> | <span data-ttu-id="e44c9-2279">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2279">Description</span></span> | <span data-ttu-id="e44c9-2280">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2280">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2281">folderPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-2281">folderPath</span></span> |<span data-ttu-id="e44c9-2282">하위 경로 toohello 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2282">Sub path toohello folder.</span></span> <span data-ttu-id="e44c9-2283">이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2283">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="e44c9-2284">예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2284">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="e44c9-2285">이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2285">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="e44c9-2286">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2286">Yes</span></span> |
| <span data-ttu-id="e44c9-2287">fileName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2287">fileName</span></span> |<span data-ttu-id="e44c9-2288">Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2288">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="e44c9-2289">이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2289">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="e44c9-2290">출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2290">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="e44c9-2291">Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2291">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="e44c9-2292">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2292">No</span></span> |
| <span data-ttu-id="e44c9-2293">fileFilter</span><span class="sxs-lookup"><span data-stu-id="e44c9-2293">fileFilter</span></span> |<span data-ttu-id="e44c9-2294">필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2294">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="e44c9-2295">허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2295">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="e44c9-2296">예 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2296">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="e44c9-2297">예 2: `"fileFilter": 2016-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2297">Example 2: `"fileFilter": 2016-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="e44c9-2298">fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2298">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="e44c9-2299">이 속성은 HDFS에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2299">This property is not supported with HDFS.</span></span> |<span data-ttu-id="e44c9-2300">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2300">No</span></span> |
| <span data-ttu-id="e44c9-2301">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="e44c9-2301">partitionedBy</span></span> |<span data-ttu-id="e44c9-2302">partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2302">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="e44c9-2303">예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2303">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="e44c9-2304">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2304">No</span></span> |
| <span data-ttu-id="e44c9-2305">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-2305">format</span></span> | <span data-ttu-id="e44c9-2306">hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2306">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-2307">집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2307">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="e44c9-2308">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2308">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="e44c9-2309">너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2309">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="e44c9-2310">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2310">No</span></span> |
| <span data-ttu-id="e44c9-2311">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-2311">compression</span></span> | <span data-ttu-id="e44c9-2312">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2312">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-2313">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2313">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-2314">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2314">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-2315">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2315">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-2316">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2316">No</span></span> |
| <span data-ttu-id="e44c9-2317">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="e44c9-2317">useBinaryTransfer</span></span> |<span data-ttu-id="e44c9-2318">이전 전송 모드를 사용할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2318">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="e44c9-2319">이진 모드인 경우 true이고 ASCII인 경우 false입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2319">True for binary mode and false ASCII.</span></span> <span data-ttu-id="e44c9-2320">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2320">Default value: True.</span></span> <span data-ttu-id="e44c9-2321">이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2321">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="e44c9-2322">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2322">No</span></span> |

> [!NOTE]
> <span data-ttu-id="e44c9-2323">filename 및 fileFilter는 동시에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2323">filename and fileFilter cannot be used simultaneously.</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-2324">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2324">Example</span></span>

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
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

<span data-ttu-id="e44c9-2325">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2325">For more information, see [SFTP connector](data-factory-sftp-connector.md#dataset-properties) article.</span></span> 

### <a name="file-system-source-in-copy-activity"></a><span data-ttu-id="e44c9-2326">복사 활동의 파일 시스템 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2326">File System Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2327">SFTP 원본에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**FileSystemSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2327">If you are copying data from an SFTP source, set hello **source type** of hello copy activity too**FileSystemSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2328">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2328">Property</span></span> | <span data-ttu-id="e44c9-2329">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2329">Description</span></span> | <span data-ttu-id="e44c9-2330">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2330">Allowed values</span></span> | <span data-ttu-id="e44c9-2331">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2331">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2332">recursive</span><span class="sxs-lookup"><span data-stu-id="e44c9-2332">recursive</span></span> |<span data-ttu-id="e44c9-2333">Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2333">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="e44c9-2334">True, False(기본값)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2334">True, False (default)</span></span> |<span data-ttu-id="e44c9-2335">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2335">No</span></span> |



#### <a name="example"></a><span data-ttu-id="e44c9-2336">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2336">Example</span></span>

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

<span data-ttu-id="e44c9-2337">자세한 내용은 [SFTP 커넥터](data-factory-sftp-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2337">For more information, see [SFTP connector](data-factory-sftp-connector.md#copy-activity-properties) article.</span></span>


## <a name="http"></a><span data-ttu-id="e44c9-2338">HTTP</span><span class="sxs-lookup"><span data-stu-id="e44c9-2338">HTTP</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-2339">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2339">Linked service</span></span>
<span data-ttu-id="e44c9-2340">연결 된 서비스를 집합 hello toodefine HTTP **형식** hello 연결 서비스 너무**Http**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2340">toodefine a HTTP linked service, set hello **type** of hello linked service too**Http**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2341">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2341">Property</span></span> | <span data-ttu-id="e44c9-2342">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2342">Description</span></span> | <span data-ttu-id="e44c9-2343">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2343">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2344">url</span><span class="sxs-lookup"><span data-stu-id="e44c9-2344">url</span></span> | <span data-ttu-id="e44c9-2345">기본 URL toohello 웹 서버</span><span class="sxs-lookup"><span data-stu-id="e44c9-2345">Base URL toohello Web Server</span></span> | <span data-ttu-id="e44c9-2346">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2346">Yes</span></span> |
| <span data-ttu-id="e44c9-2347">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2347">authenticationType</span></span> | <span data-ttu-id="e44c9-2348">Hello 인증 유형을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2348">Specifies hello authentication type.</span></span> <span data-ttu-id="e44c9-2349">허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2349">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="e44c9-2350">이 표 아래에 더 많은 속성 및 JSON 샘플 toosections 해당 인증 형식에 각각 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2350">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="e44c9-2351">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2351">Yes</span></span> |
| <span data-ttu-id="e44c9-2352">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="e44c9-2352">enableServerCertificateValidation</span></span> | <span data-ttu-id="e44c9-2353">소스 HTTPS 웹 서버인 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2353">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="e44c9-2354">아니요. 기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2354">No, default is true</span></span> |
| <span data-ttu-id="e44c9-2355">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2355">gatewayName</span></span> | <span data-ttu-id="e44c9-2356">데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 HTTP 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2356">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="e44c9-2357">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2357">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="e44c9-2358">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-2358">encryptedCredential</span></span> | <span data-ttu-id="e44c9-2359">암호화 된 자격 증명 tooaccess hello HTTP 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2359">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="e44c9-2360">자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에 hello 인증 정보를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2360">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="e44c9-2361">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2361">No.</span></span> <span data-ttu-id="e44c9-2362">온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2362">Apply only when copying data from an on-premises HTTP server.</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="e44c9-2363">예제: Basic, Digest 또는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2363">Example: Using Basic, Digest, or Windows authentication</span></span>
<span data-ttu-id="e44c9-2364">설정 `authenticationType` 으로 `Basic`, `Digest`, 또는 `Windows`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2364">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="e44c9-2365">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2365">Property</span></span> | <span data-ttu-id="e44c9-2366">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2366">Description</span></span> | <span data-ttu-id="e44c9-2367">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2367">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2368">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2368">username</span></span> | <span data-ttu-id="e44c9-2369">사용자 이름 tooaccess hello HTTP 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2369">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="e44c9-2370">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2370">Yes</span></span> |
| <span data-ttu-id="e44c9-2371">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2371">password</span></span> | <span data-ttu-id="e44c9-2372">Hello 사용자 (사용자 이름)에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2372">Password for hello user (username).</span></span> | <span data-ttu-id="e44c9-2373">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2373">Yes</span></span> |

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

#### <a name="example-using-clientcertificate-authentication"></a><span data-ttu-id="e44c9-2374">예제: ClientCertificate 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2374">Example: Using ClientCertificate authentication</span></span>

<span data-ttu-id="e44c9-2375">toouse 기본 인증 설정 `authenticationType` 으로 `ClientCertificate`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2375">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="e44c9-2376">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2376">Property</span></span> | <span data-ttu-id="e44c9-2377">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2377">Description</span></span> | <span data-ttu-id="e44c9-2378">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2378">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2379">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="e44c9-2379">embeddedCertData</span></span> | <span data-ttu-id="e44c9-2380">hello 개인 정보 교환 (PFX) 파일의 이진 데이터의 Base64 인코딩 내용 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2380">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="e44c9-2381">어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2381">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="e44c9-2382">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="e44c9-2382">certThumbprint</span></span> | <span data-ttu-id="e44c9-2383">게이트웨이 컴퓨터의 인증서 저장소에 설치 된 hello 인증서의 지문을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2383">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="e44c9-2384">온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2384">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="e44c9-2385">어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2385">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="e44c9-2386">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2386">password</span></span> | <span data-ttu-id="e44c9-2387">Hello 인증서와 연결 된 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2387">Password associated with hello certificate.</span></span> | <span data-ttu-id="e44c9-2388">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2388">No</span></span> |

<span data-ttu-id="e44c9-2389">사용 하는 경우 `certThumbprint` toogrant hello 읽기 권한은 toohello 게이트웨이 서비스가 필요한 경우 인증 및 hello 인증서 hello hello 로컬 컴퓨터의 개인 저장소에 설치 하면:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2389">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="e44c9-2390">MMC(Microsoft Management Console)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2390">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="e44c9-2391">Hello 추가 **인증서** 스냅인 해당 대상 hello **로컬 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2391">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="e44c9-2392">**인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2392">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="e44c9-2393">Hello 개인 저장소에서 hello 인증서를 마우스 오른쪽 단추로 클릭 하 고 선택 **모든 작업**->**개인 키 관리...**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2393">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="e44c9-2394">Hello에 **보안** 탭에서 데이터 관리 게이트웨이 호스트 서비스가 실행 되 고 있는 hello 읽기 액세스 toohello 인증서로 hello 사용자 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2394">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

<span data-ttu-id="e44c9-2395">**예: 클라이언트 인증서를 사용 하 여:** 이 연결 된 서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2395">**Example: using client certificate:** This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="e44c9-2396">데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 설치 된 클라이언트 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2396">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="e44c9-2397">예제: 파일로 클라이언트 인증서 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2397">Example: using client certificate in a file</span></span>
<span data-ttu-id="e44c9-2398">서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2398">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="e44c9-2399">데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 클라이언트 인증서 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2399">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

<span data-ttu-id="e44c9-2400">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2400">For more information, see [HTTP connector](data-factory-http-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-2401">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2401">Dataset</span></span>
<span data-ttu-id="e44c9-2402">HTTP toodefine 데이터 집합, 집합 hello **형식** hello 데이터 집합의 너무**Http**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2402">toodefine a HTTP dataset, set hello **type** of hello dataset too**Http**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2403">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2403">Property</span></span> | <span data-ttu-id="e44c9-2404">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2404">Description</span></span> | <span data-ttu-id="e44c9-2405">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2405">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-2406">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="e44c9-2406">relativeUrl</span></span> | <span data-ttu-id="e44c9-2407">상대 URL toohello 리소스 hello 데이터가 들어 있는입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2407">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="e44c9-2408">경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2408">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="e44c9-2409">사용할 수 있습니다 tooconstruct 동적 URL [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md), 예: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2409">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), Example: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`.</span></span> | <span data-ttu-id="e44c9-2410">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2410">No</span></span> |
| <span data-ttu-id="e44c9-2411">requestMethod</span><span class="sxs-lookup"><span data-stu-id="e44c9-2411">requestMethod</span></span> | <span data-ttu-id="e44c9-2412">HTTP 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2412">Http method.</span></span> <span data-ttu-id="e44c9-2413">허용되는 값은 **GET** 또는 **POST**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2413">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="e44c9-2414">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2414">No.</span></span> <span data-ttu-id="e44c9-2415">기본값은 `GET`입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2415">Default is `GET`.</span></span> |
| <span data-ttu-id="e44c9-2416">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="e44c9-2416">additionalHeaders</span></span> | <span data-ttu-id="e44c9-2417">추가 HTTP 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2417">Additional HTTP request headers.</span></span> | <span data-ttu-id="e44c9-2418">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2418">No</span></span> |
| <span data-ttu-id="e44c9-2419">requestBody</span><span class="sxs-lookup"><span data-stu-id="e44c9-2419">requestBody</span></span> | <span data-ttu-id="e44c9-2420">HTTP 요청의 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2420">Body for HTTP request.</span></span> | <span data-ttu-id="e44c9-2421">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2421">No</span></span> |
| <span data-ttu-id="e44c9-2422">format</span><span class="sxs-lookup"><span data-stu-id="e44c9-2422">format</span></span> | <span data-ttu-id="e44c9-2423">Toosimply 하려는 경우 **으로 HTTP 끝점에서 hello 데이터를 검색-은** 것, 구문 분석 하지 않고 형식 설정에이 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2423">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="e44c9-2424">복사 중 tooparse hello HTTP 응답을 콘텐츠에 삭제 하는 경우에 hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2424">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="e44c9-2425">자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2425">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="e44c9-2426">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2426">No</span></span> |
| <span data-ttu-id="e44c9-2427">압축</span><span class="sxs-lookup"><span data-stu-id="e44c9-2427">compression</span></span> | <span data-ttu-id="e44c9-2428">Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2428">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="e44c9-2429">지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2429">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="e44c9-2430">지원되는 수준은 **최적** 및 **가장 빠름**입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2430">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="e44c9-2431">자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2431">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="e44c9-2432">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2432">No</span></span> |

#### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="e44c9-2433">예: hello GET (기본값) 메서드 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2433">Example: using hello GET (default) method</span></span>

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

#### <a name="example-using-hello-post-method"></a><span data-ttu-id="e44c9-2434">예: hello POST 메서드를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e44c9-2434">Example: using hello POST method</span></span>

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
<span data-ttu-id="e44c9-2435">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2435">For more information, see [HTTP connector](data-factory-http-connector.md#dataset-properties) article.</span></span>

### <a name="http-source-in-copy-activity"></a><span data-ttu-id="e44c9-2436">복사 활동의 HTTP 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2436">HTTP Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2437">HTTP 소스에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**HttpSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2437">If you are copying data from a HTTP source, set hello **source type** of hello copy activity too**HttpSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2438">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2438">Property</span></span> | <span data-ttu-id="e44c9-2439">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2439">Description</span></span> | <span data-ttu-id="e44c9-2440">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2440">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="e44c9-2441">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="e44c9-2441">httpRequestTimeout</span></span> | <span data-ttu-id="e44c9-2442">안녕 hello HTTP 요청 tooget 응답 하기 위한 시간 제한 (TimeSpan).</span><span class="sxs-lookup"><span data-stu-id="e44c9-2442">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="e44c9-2443">Hello timeout tooget 응답으로 hello timeout tooread 응답 데이터가 아닌 경우</span><span class="sxs-lookup"><span data-stu-id="e44c9-2443">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="e44c9-2444">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2444">No.</span></span> <span data-ttu-id="e44c9-2445">기본값: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="e44c9-2445">Default value: 00:01:40</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-2446">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2446">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
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

<span data-ttu-id="e44c9-2447">자세한 내용은 [HTTP 커넥터](data-factory-http-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2447">For more information, see [HTTP connector](data-factory-http-connector.md#copy-activity-properties) article.</span></span>

## <a name="odata"></a><span data-ttu-id="e44c9-2448">OData</span><span class="sxs-lookup"><span data-stu-id="e44c9-2448">OData</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-2449">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2449">Linked service</span></span>
<span data-ttu-id="e44c9-2450">연결 된 서비스를 집합 hello toodefine OData **형식** hello 연결 서비스 너무**OData**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2450">toodefine an OData linked service, set hello **type** of hello linked service too**OData**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2451">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2451">Property</span></span> | <span data-ttu-id="e44c9-2452">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2452">Description</span></span> | <span data-ttu-id="e44c9-2453">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2453">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2454">url</span><span class="sxs-lookup"><span data-stu-id="e44c9-2454">url</span></span> |<span data-ttu-id="e44c9-2455">Hello OData 서비스의 Url입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2455">Url of hello OData service.</span></span> |<span data-ttu-id="e44c9-2456">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2456">Yes</span></span> |
| <span data-ttu-id="e44c9-2457">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2457">authenticationType</span></span> |<span data-ttu-id="e44c9-2458">Tooconnect toohello OData 원본을 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2458">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="e44c9-2459">클라우드 OData의 경우 가능한 값은 익명, 기본 및 OAuth입니다(Azure Data Factory는 현재 Azure Active Directory 기반 OAuth만 지원).</span><span class="sxs-lookup"><span data-stu-id="e44c9-2459">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="e44c9-2460">온-프레미스 OData의 경우 가능한 값은 익명, 기본 및 Windows입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2460">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e44c9-2461">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2461">Yes</span></span> |
| <span data-ttu-id="e44c9-2462">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2462">username</span></span> |<span data-ttu-id="e44c9-2463">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2463">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="e44c9-2464">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2464">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="e44c9-2465">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2465">password</span></span> |<span data-ttu-id="e44c9-2466">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2466">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-2467">예(기본 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2467">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="e44c9-2468">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="e44c9-2468">authorizedCredential</span></span> |<span data-ttu-id="e44c9-2469">OAuth를 사용 하는 경우 클릭 **Authorize** hello 데이터 팩터리 복사 마법사 또는 편집기에서 단추 및이 속성의 hello 값 자동 생성 됩니다. 사용자의 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2469">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="e44c9-2470">예(OAuth 인증을 사용하는 경우에만)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2470">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="e44c9-2471">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2471">gatewayName</span></span> |<span data-ttu-id="e44c9-2472">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 OData 서비스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2472">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="e44c9-2473">온-프레미스 OData 소스의 데이터를 복사하는 경우에만 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2473">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="e44c9-2474">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2474">No</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="e44c9-2475">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2475">Example - Using Basic authentication</span></span>
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

#### <a name="example---using-anonymous-authentication"></a><span data-ttu-id="e44c9-2476">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2476">Example - Using Anonymous authentication</span></span>

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

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="e44c9-2477">예제: 온-프레미스 OData 소스에 액세스하는 Windows 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2477">Example - Using Windows authentication accessing on-premises OData source</span></span>

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

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="e44c9-2478">예제: 클라우드 OData 소스에 액세스하는 OAuth 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2478">Example - Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

<span data-ttu-id="e44c9-2479">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2479">For more information, see [OData connector](data-factory-odata-connector.md#linked-service-properties) article.</span></span>

### <a name="dataset"></a><span data-ttu-id="e44c9-2480">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2480">Dataset</span></span>
<span data-ttu-id="e44c9-2481">OData 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**ODataResource**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2481">toodefine an OData dataset, set hello **type** of hello dataset too**ODataResource**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2482">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2482">Property</span></span> | <span data-ttu-id="e44c9-2483">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2483">Description</span></span> | <span data-ttu-id="e44c9-2484">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2484">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2485">path</span><span class="sxs-lookup"><span data-stu-id="e44c9-2485">path</span></span> |<span data-ttu-id="e44c9-2486">경로 toohello OData 리소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2486">Path toohello OData resource</span></span> |<span data-ttu-id="e44c9-2487">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2487">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2488">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2488">Example</span></span>

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

<span data-ttu-id="e44c9-2489">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2489">For more information, see [OData connector](data-factory-odata-connector.md#dataset-properties) article.</span></span>

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-2490">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2490">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2491">OData 원본에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2491">If you are copying data from an OData source, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2492">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2492">Property</span></span> | <span data-ttu-id="e44c9-2493">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2493">Description</span></span> | <span data-ttu-id="e44c9-2494">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2494">Example</span></span> | <span data-ttu-id="e44c9-2495">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2495">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2496">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-2496">query</span></span> |<span data-ttu-id="e44c9-2497">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2497">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-2498">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="e44c9-2498">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="e44c9-2499">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2499">No</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2500">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2500">Example</span></span>

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

<span data-ttu-id="e44c9-2501">자세한 내용은 [OData 커넥터](data-factory-odata-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2501">For more information, see [OData connector](data-factory-odata-connector.md#copy-activity-properties) article.</span></span>


## <a name="odbc"></a><span data-ttu-id="e44c9-2502">ODBC</span><span class="sxs-lookup"><span data-stu-id="e44c9-2502">ODBC</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-2503">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2503">Linked service</span></span>
<span data-ttu-id="e44c9-2504">연결 된 서비스를 집합 hello toodefine ODBC **형식** hello 연결 서비스 너무**OnPremisesOdbc**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2504">toodefine an ODBC linked service, set hello **type** of hello linked service too**OnPremisesOdbc**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2505">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2505">Property</span></span> | <span data-ttu-id="e44c9-2506">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2506">Description</span></span> | <span data-ttu-id="e44c9-2507">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2507">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2508">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-2508">connectionString</span></span> |<span data-ttu-id="e44c9-2509">hello 연결 문자열 및 선택적의 hello이 아닌 액세스 자격 증명 일부분 자격 증명을 암호화 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2509">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="e44c9-2510">Hello 다음 섹션의에서 예를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2510">See examples in hello following sections.</span></span> |<span data-ttu-id="e44c9-2511">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2511">Yes</span></span> |
| <span data-ttu-id="e44c9-2512">자격 증명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2512">credential</span></span> |<span data-ttu-id="e44c9-2513">hello 액세스 자격 증명 드라이버 관련 속성 값 형식으로 지정 하는 hello 연결 문자열의 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2513">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="e44c9-2514">예: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2514">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="e44c9-2515">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2515">No</span></span> |
| <span data-ttu-id="e44c9-2516">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2516">authenticationType</span></span> |<span data-ttu-id="e44c9-2517">Tooconnect toohello ODBC 데이터 저장소를 사용 하는 인증 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2517">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="e44c9-2518">가능한 값은 익명 및 기본입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2518">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="e44c9-2519">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2519">Yes</span></span> |
| <span data-ttu-id="e44c9-2520">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2520">username</span></span> |<span data-ttu-id="e44c9-2521">기본 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2521">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="e44c9-2522">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2522">No</span></span> |
| <span data-ttu-id="e44c9-2523">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2523">password</span></span> |<span data-ttu-id="e44c9-2524">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2524">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-2525">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2525">No</span></span> |
| <span data-ttu-id="e44c9-2526">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2526">gatewayName</span></span> |<span data-ttu-id="e44c9-2527">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello ODBC 데이터 저장소를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2527">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="e44c9-2528">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2528">Yes</span></span> |

#### <a name="example---using-basic-authentication"></a><span data-ttu-id="e44c9-2529">예제: 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2529">Example - Using Basic authentication</span></span>

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
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="e44c9-2530">예제: 암호화된 자격 증명으로 기본 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2530">Example - Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="e44c9-2531">Hello를 사용 하 여 hello 자격 증명을 암호화할 수 [새로 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 버전의 Azure PowerShell) cmdlet 또는 [New-azuredatafactoryencryptvalue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 또는 이전 버전의 hello Azure PowerShell)입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2531">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

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

#### <a name="example-using-anonymous-authentication"></a><span data-ttu-id="e44c9-2532">예제: 익명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2532">Example: Using Anonymous authentication</span></span>

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

<span data-ttu-id="e44c9-2533">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2533">For more information, see [ODBC connector](data-factory-odbc-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-2534">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2534">Dataset</span></span>
<span data-ttu-id="e44c9-2535">ODBC 데이터 집합, toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2535">toodefine an ODBC dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2536">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2536">Property</span></span> | <span data-ttu-id="e44c9-2537">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2537">Description</span></span> | <span data-ttu-id="e44c9-2538">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2538">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2539">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2539">tableName</span></span> |<span data-ttu-id="e44c9-2540">Hello ODBC 데이터 저장소의 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2540">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="e44c9-2541">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2541">Yes</span></span> |


#### <a name="example"></a><span data-ttu-id="e44c9-2542">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2542">Example</span></span>

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

<span data-ttu-id="e44c9-2543">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2543">For more information, see [ODBC connector](data-factory-odbc-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-2544">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2544">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2545">ODBC 데이터 저장소에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2545">If you are copying data from an ODBC data store, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2546">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2546">Property</span></span> | <span data-ttu-id="e44c9-2547">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2547">Description</span></span> | <span data-ttu-id="e44c9-2548">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2548">Allowed values</span></span> | <span data-ttu-id="e44c9-2549">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2549">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2550">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-2550">query</span></span> |<span data-ttu-id="e44c9-2551">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2551">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-2552">SQL 쿼리 문자열.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2552">SQL query string.</span></span> <span data-ttu-id="e44c9-2553">예: `select * from MyTable`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2553">For example: `select * from MyTable`.</span></span> |<span data-ttu-id="e44c9-2554">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2554">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2555">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2555">Example</span></span>

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

<span data-ttu-id="e44c9-2556">자세한 내용은 [ODBC 커넥터](data-factory-odbc-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2556">For more information, see [ODBC connector](data-factory-odbc-connector.md#copy-activity-properties) article.</span></span>

## <a name="salesforce"></a><span data-ttu-id="e44c9-2557">Salesforce</span><span class="sxs-lookup"><span data-stu-id="e44c9-2557">Salesforce</span></span>


### <a name="linked-service"></a><span data-ttu-id="e44c9-2558">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2558">Linked service</span></span>
<span data-ttu-id="e44c9-2559">연결 된 서비스를 집합 hello toodefine Salesforce **형식** hello 연결 서비스 너무**Salesforce**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2559">toodefine a Salesforce linked service, set hello **type** of hello linked service too**Salesforce**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2560">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2560">Property</span></span> | <span data-ttu-id="e44c9-2561">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2561">Description</span></span> | <span data-ttu-id="e44c9-2562">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2562">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2563">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="e44c9-2563">environmentUrl</span></span> | <span data-ttu-id="e44c9-2564">Hello URL의 Salesforce 인스턴스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2564">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="e44c9-2565">-기본값은 " https://login.salesforce.com " 입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2565">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="e44c9-2566">-toocopy 데이터로 샌드박스 "https://test.salesforce.com"를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2566">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="e44c9-2567">-사용자 지정 도메인에서 toocopy 데이터 지정, 예를 들어 "https://[domain].my.salesforce.com"입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2567">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="e44c9-2568">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2568">No</span></span> |
| <span data-ttu-id="e44c9-2569">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2569">username</span></span> |<span data-ttu-id="e44c9-2570">Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2570">Specify a user name for hello user account.</span></span> |<span data-ttu-id="e44c9-2571">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2571">Yes</span></span> |
| <span data-ttu-id="e44c9-2572">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2572">password</span></span> |<span data-ttu-id="e44c9-2573">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2573">Specify a password for hello user account.</span></span> |<span data-ttu-id="e44c9-2574">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2574">Yes</span></span> |
| <span data-ttu-id="e44c9-2575">securityToken</span><span class="sxs-lookup"><span data-stu-id="e44c9-2575">securityToken</span></span> |<span data-ttu-id="e44c9-2576">Hello 사용자 계정에 대 한 보안 토큰을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2576">Specify a security token for hello user account.</span></span> <span data-ttu-id="e44c9-2577">참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 방법에 대 한 보안 토큰 tooreset/get입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2577">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="e44c9-2578">보안 토큰에 대 한 toolearn 일반적으로 참조 [보안과 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2578">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="e44c9-2579">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2579">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2580">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2580">Example</span></span>

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

<span data-ttu-id="e44c9-2581">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2581">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-2582">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2582">Dataset</span></span>
<span data-ttu-id="e44c9-2583">Salesforce 데이터 집합을 toodefine 집합 hello **형식** hello 데이터 집합의 너무**RelationalTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2583">toodefine a Salesforce dataset, set hello **type** of hello dataset too**RelationalTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2584">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2584">Property</span></span> | <span data-ttu-id="e44c9-2585">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2585">Description</span></span> | <span data-ttu-id="e44c9-2586">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2586">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2587">tableName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2587">tableName</span></span> |<span data-ttu-id="e44c9-2588">Salesforce에 hello 테이블의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2588">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="e44c9-2589">아니요(**RelationalSource**의 **query**가 지정된 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2589">No (if a **query** of **RelationalSource** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2590">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2590">Example</span></span>

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

<span data-ttu-id="e44c9-2591">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2591">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#dataset-properties) article.</span></span> 

### <a name="relational-source-in-copy-activity"></a><span data-ttu-id="e44c9-2592">복사 활동의 Relational 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2592">Relational Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2593">Salesforce 로부터 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**RelationalSource**, 다음 hello에 대 한 속성을 지정 하 고 **소스** 섹션 내용</span><span class="sxs-lookup"><span data-stu-id="e44c9-2593">If you are copying data from Salesforce, set hello **source type** of hello copy activity too**RelationalSource**, and specify following properties in hello **source** section:</span></span>

| <span data-ttu-id="e44c9-2594">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2594">Property</span></span> | <span data-ttu-id="e44c9-2595">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2595">Description</span></span> | <span data-ttu-id="e44c9-2596">허용되는 값</span><span class="sxs-lookup"><span data-stu-id="e44c9-2596">Allowed values</span></span> | <span data-ttu-id="e44c9-2597">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2597">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e44c9-2598">쿼리</span><span class="sxs-lookup"><span data-stu-id="e44c9-2598">query</span></span> |<span data-ttu-id="e44c9-2599">사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2599">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e44c9-2600">SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2600">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="e44c9-2601">예제: `select * from MyTable__c`</span><span class="sxs-lookup"><span data-stu-id="e44c9-2601">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="e44c9-2602">더 (경우 hello **tableName** 의 hello **dataset** 지정)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2602">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2603">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2603">Example</span></span>  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
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
> <span data-ttu-id="e44c9-2604">모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2604">hello "__c" part of hello API Name is needed for any custom object.</span></span>

<span data-ttu-id="e44c9-2605">자세한 내용은 [Salesforce 커넥터](data-factory-salesforce-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2605">For more information, see [Salesforce connector](data-factory-salesforce-connector.md#copy-activity-properties) article.</span></span> 

## <a name="web-data"></a><span data-ttu-id="e44c9-2606">웹 데이터</span><span class="sxs-lookup"><span data-stu-id="e44c9-2606">Web Data</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2607">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2607">Linked service</span></span>
<span data-ttu-id="e44c9-2608">연결 된 서비스를 집합 hello toodefine 웹 **형식** hello 연결 서비스 너무**웹**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2608">toodefine a Web linked service, set hello **type** of hello linked service too**Web**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2609">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2609">Property</span></span> | <span data-ttu-id="e44c9-2610">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2610">Description</span></span> | <span data-ttu-id="e44c9-2611">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2611">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2612">Url</span><span class="sxs-lookup"><span data-stu-id="e44c9-2612">Url</span></span> |<span data-ttu-id="e44c9-2613">URL toohello 웹 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2613">URL toohello Web source</span></span> |<span data-ttu-id="e44c9-2614">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2614">Yes</span></span> |
| <span data-ttu-id="e44c9-2615">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2615">authenticationType</span></span> |<span data-ttu-id="e44c9-2616">익명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2616">Anonymous.</span></span> |<span data-ttu-id="e44c9-2617">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2617">Yes</span></span> |
 

#### <a name="example"></a><span data-ttu-id="e44c9-2618">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2618">Example</span></span>


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

<span data-ttu-id="e44c9-2619">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2619">For more information, see [Web Table connector](data-factory-web-table-connector.md#linked-service-properties) article.</span></span> 

### <a name="dataset"></a><span data-ttu-id="e44c9-2620">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="e44c9-2620">Dataset</span></span>
<span data-ttu-id="e44c9-2621">toodefine 웹 dataset 집합 hello **형식** hello 데이터 집합의 너무**WebTable**, hello 다음과 같은 hello에 대 한 속성을 지정 하 고 **typeProperties** 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2621">toodefine a Web dataset, set hello **type** of hello dataset too**WebTable**, and specify hello following properties in hello **typeProperties** section:</span></span> 

| <span data-ttu-id="e44c9-2622">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2622">Property</span></span> | <span data-ttu-id="e44c9-2623">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2623">Description</span></span> | <span data-ttu-id="e44c9-2624">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2624">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-2625">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2625">type</span></span> |<span data-ttu-id="e44c9-2626">hello 데이터 집합의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2626">type of hello dataset.</span></span> <span data-ttu-id="e44c9-2627">너무 설정 되어 있어야**WebTable**</span><span class="sxs-lookup"><span data-stu-id="e44c9-2627">must be set too**WebTable**</span></span> |<span data-ttu-id="e44c9-2628">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2628">Yes</span></span> |
| <span data-ttu-id="e44c9-2629">path</span><span class="sxs-lookup"><span data-stu-id="e44c9-2629">path</span></span> |<span data-ttu-id="e44c9-2630">상대 URL toohello 리소스 hello 테이블을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2630">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="e44c9-2631">아니요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2631">No.</span></span> <span data-ttu-id="e44c9-2632">경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2632">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="e44c9-2633">index</span><span class="sxs-lookup"><span data-stu-id="e44c9-2633">index</span></span> |<span data-ttu-id="e44c9-2634">hello 리소스에 대 한 hello 테이블의 hello 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2634">hello index of hello table in hello resource.</span></span> <span data-ttu-id="e44c9-2635">참조 [HTML 페이지에 테이블의 Get 인덱스](#get-index-of-a-table-in-an-html-page) 단계 toogetting 인덱스에 대 한 HTML 페이지에 테이블의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2635">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="e44c9-2636">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2636">Yes</span></span> |

#### <a name="example"></a><span data-ttu-id="e44c9-2637">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2637">Example</span></span>

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

<span data-ttu-id="e44c9-2638">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#dataset-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2638">For more information, see [Web Table connector](data-factory-web-table-connector.md#dataset-properties) article.</span></span> 

### <a name="web-source-in-copy-activity"></a><span data-ttu-id="e44c9-2639">복사 활동의 웹 소스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2639">Web Source in Copy Activity</span></span>
<span data-ttu-id="e44c9-2640">웹 테이블에서 데이터를 복사 하는 경우 설정 hello **소스 형식** hello의 복사 작업이 너무**WebSource**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2640">If you are copying data from a web table, set hello **source type** of hello copy activity too**WebSource**.</span></span> <span data-ttu-id="e44c9-2641">현재 복사 작업에서 hello 소스 경우 형식의 **WebSource**, 추가 속성이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2641">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>

#### <a name="example"></a><span data-ttu-id="e44c9-2642">예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2642">Example</span></span>

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
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

<span data-ttu-id="e44c9-2643">자세한 내용은 [웹 테이블 커넥터](data-factory-web-table-connector.md#copy-activity-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2643">For more information, see [Web Table connector](data-factory-web-table-connector.md#copy-activity-properties) article.</span></span> 

## <a name="compute-environments"></a><span data-ttu-id="e44c9-2644">계산 환경</span><span class="sxs-lookup"><span data-stu-id="e44c9-2644">COMPUTE ENVIRONMENTS</span></span>
<span data-ttu-id="e44c9-2645">hello 다음 표에 나열 hello 계산 환경에서 실행할 수 있는 Data Factory와 hello 변환 활동에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2645">hello following table lists hello compute environments supported by Data Factory and hello transformation activities that can run on them.</span></span> <span data-ttu-id="e44c9-2646">hello 계산에 대 한 hello 링크를 클릭에 관심이 toosee toolink 연결 된 서비스에 대 한 JSON 스키마를 hello 것 tooa 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2646">Click hello link for hello compute you are interested in toosee hello JSON schemas for linked service toolink it tooa data factory.</span></span> 

| <span data-ttu-id="e44c9-2647">컴퓨팅 환경</span><span class="sxs-lookup"><span data-stu-id="e44c9-2647">Compute environment</span></span> | <span data-ttu-id="e44c9-2648">활동</span><span class="sxs-lookup"><span data-stu-id="e44c9-2648">Activities</span></span> |
| --- | --- |
| <span data-ttu-id="e44c9-2649">[주문형 HDInsight 클러스터](#on-demand-azure-hdinsight-cluster) 또는 [사용자 고유의 HDInsight 클러스터](#existing-azure-hdinsight-cluster)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2649">[On-demand HDInsight cluster](#on-demand-azure-hdinsight-cluster) or [your own HDInsight cluster](#existing-azure-hdinsight-cluster)</span></span> |<span data-ttu-id="e44c9-2650">[.NET 사용자 지정 활동](#net-custom-activity), [Hive 활동](#hdinsight-hive-activity), [Pig 활동](#hdinsight-pig-activity), [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 활동](#hdinsight-streaming-activityd), [Spark 활동](#hdinsight-spark-activity)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2650">[.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity)</span></span> |
| [<span data-ttu-id="e44c9-2651">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="e44c9-2651">Azure Batch</span></span>](#azure-batch) |[<span data-ttu-id="e44c9-2652">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2652">.NET custom activity</span></span>](#net-custom-activity) |
| [<span data-ttu-id="e44c9-2653">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="e44c9-2653">Azure Machine Learning</span></span>](#azure-machine-learning) | <span data-ttu-id="e44c9-2654">[Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity), [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2654">[Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity)</span></span> |
| [<span data-ttu-id="e44c9-2655">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="e44c9-2655">Azure Data Lake Analytics</span></span>](#azure-data-lake-analytics) |[<span data-ttu-id="e44c9-2656">데이터 레이크 분석 U-SQL</span><span class="sxs-lookup"><span data-stu-id="e44c9-2656">Data Lake Analytics U-SQL</span></span>](#data-lake-analytics-u-sql-activity) |
| <span data-ttu-id="e44c9-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2657">[Azure SQL Database](#azure-sql-database-1), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1)</span></span> |[<span data-ttu-id="e44c9-2658">저장 프로시저</span><span class="sxs-lookup"><span data-stu-id="e44c9-2658">Stored Procedure</span></span>](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a><span data-ttu-id="e44c9-2659">주문형 Azure HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="e44c9-2659">On-demand Azure HDInsight cluster</span></span>
<span data-ttu-id="e44c9-2660">hello Azure 데이터 팩터리 서비스는 Windows/Linux 기반에 주문형 HDInsight 클러스터 tooprocess 데이터를 자동으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2660">hello Azure Data Factory service can automatically create a Windows/Linux-based on-demand HDInsight cluster tooprocess data.</span></span> <span data-ttu-id="e44c9-2661">hello 클러스터 hello hello 클러스터와 연결 된 hello 저장소 계정 (hello JSON의에서 linkedServiceName 속성)와 동일한 지역에에서 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2661">hello cluster is created in hello same region as hello storage account (linkedServiceName property in hello JSON) associated with hello cluster.</span></span> <span data-ttu-id="e44c9-2662">Hello에 나오는 변환 작업에 따라이 연결 된 서비스를 실행할 수 있습니다: [.NET 사용자 지정 활동](#net-custom-activity), [활동 하이브](#hdinsight-hive-activity), [활동 Pig] (#hdinsight pig-작업, [MapReduce 작업 ](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 작업](#hdinsight-streaming-activityd), [활동 멤버](#hdinsight-spark-activity)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2662">You can run hello following transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2663">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2663">Linked service</span></span> 
<span data-ttu-id="e44c9-2664">다음 표에서 hello 주문형 HDInsight 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2664">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an on-demand HDInsight linked service.</span></span>

| <span data-ttu-id="e44c9-2665">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2665">Property</span></span> | <span data-ttu-id="e44c9-2666">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2666">Description</span></span> | <span data-ttu-id="e44c9-2667">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2667">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2668">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2668">type</span></span> |<span data-ttu-id="e44c9-2669">너무 hello 유형 속성을 설정 해야**HDInsightOnDemand**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2669">hello type property should be set too**HDInsightOnDemand**.</span></span> |<span data-ttu-id="e44c9-2670">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2670">Yes</span></span> |
| <span data-ttu-id="e44c9-2671">clusterSize</span><span class="sxs-lookup"><span data-stu-id="e44c9-2671">clusterSize</span></span> |<span data-ttu-id="e44c9-2672">Hello 클러스터의 작업자/데이터 노드 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2672">Number of worker/data nodes in hello cluster.</span></span> <span data-ttu-id="e44c9-2673">hello HDInsight 클러스터는 헤드 노드 hello이이 속성에 대해 지정 하는 작업자 노드 수와 함께 2으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2673">hello HDInsight cluster is created with 2 head nodes along with hello number of worker nodes you specify for this property.</span></span> <span data-ttu-id="e44c9-2674">hello 노드는 크기는 4 작업자 노드 클러스터는 24 코어 4 개 코어에 Standard_D3 (4\*작업자 노드 + 2에 대 한 4 = 16 코어가\*헤드 노드에 대 한 4 = 8 코어).</span><span class="sxs-lookup"><span data-stu-id="e44c9-2674">hello nodes are of size Standard_D3 that has 4 cores, so a 4 worker node cluster takes 24 cores (4\*4 = 16 cores for worker nodes, plus 2\*4 = 8 cores for head nodes).</span></span> <span data-ttu-id="e44c9-2675">참조 [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 계층에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2675">See [Create Linux-based Hadoop clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) for details about hello Standard_D3 tier.</span></span> |<span data-ttu-id="e44c9-2676">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2676">Yes</span></span> |
| <span data-ttu-id="e44c9-2677">timetolive</span><span class="sxs-lookup"><span data-stu-id="e44c9-2677">timetolive</span></span> |<span data-ttu-id="e44c9-2678">hello는 hello 주문형 HDInsight 클러스터에 대 한 유휴 시간을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2678">hello allowed idle time for hello on-demand HDInsight cluster.</span></span> <span data-ttu-id="e44c9-2679">기간 hello 주문형 HDInsight 클러스터의 연결이 유지 hello 클러스터에 다른 활성 작업이 있는 경우 실행 작업을 완료 한 후 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2679">Specifies how long hello on-demand HDInsight cluster stays alive after completion of an activity run if there are no other active jobs in hello cluster.</span></span><br/><br/><span data-ttu-id="e44c9-2680">예를 들어 활동 실행 6 분 및 timetolive 않습니다 too5 분, 5 분 후 hello에 대 한 연결 유지 hello 클러스터 유지할 6 분의 처리를 실행 하는 hello 활동을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2680">For example, if an activity run takes 6 minutes and timetolive is set too5 minutes, hello cluster stays alive for 5 minutes after hello 6 minutes of processing hello activity run.</span></span> <span data-ttu-id="e44c9-2681">Hello에서 처리 된를 실행 하는 다른 활동을 hello 6 분 창을 실행 하는 경우 동일한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2681">If another activity run is executed with hello 6 minutes window, it is processed by hello same cluster.</span></span><br/><br/><span data-ttu-id="e44c9-2682">주문형 HDInsight 클러스터를 만드는 작업은 비용이 많이 드는 작업 (이 걸릴 수), 따라서 데이터 팩터리의 필요한 tooimprove 성능으로이 설정을 사용 하 여 주문형 HDInsight 클러스터를 다시 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2682">Creating an on-demand HDInsight cluster is an expensive operation (could take a while), so use this setting as needed tooimprove performance of a data factory by reusing an on-demand HDInsight cluster.</span></span><br/><br/><span data-ttu-id="e44c9-2683">Timetolive 값 too0로 설정 하면 hello 클러스터 hello 활동 실행 처리 되는 즉시 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2683">If you set timetolive value too0, hello cluster is deleted as soon as hello activity run in processed.</span></span> <span data-ttu-id="e44c9-2684">Hello에 다른 손을 높은 값을 설정 하는 경우 hello 클러스터 될 수 있습니다 유지 유휴 불필요 하 게 많은 비용이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2684">On hello other hand, if you set a high value, hello cluster may stay idle unnecessarily resulting in high costs.</span></span> <span data-ttu-id="e44c9-2685">따라서이 필요에 따라 hello 적절 한 값을 설정 하는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2685">Therefore, it is important that you set hello appropriate value based on your needs.</span></span><br/><br/><span data-ttu-id="e44c9-2686">여러 파이프라인을 공유할 수 hello timetolive 속성 값이 적절 하 게 설정 하는 경우 hello 주문형 HDInsight 클러스터의 동일한 인스턴스에 hello</span><span class="sxs-lookup"><span data-stu-id="e44c9-2686">Multiple pipelines can share hello same instance of hello on-demand HDInsight cluster if hello timetolive property value is appropriately set</span></span> |<span data-ttu-id="e44c9-2687">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2687">Yes</span></span> |
| <span data-ttu-id="e44c9-2688">버전</span><span class="sxs-lookup"><span data-stu-id="e44c9-2688">version</span></span> |<span data-ttu-id="e44c9-2689">Hello HDInsight 클러스터의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2689">Version of hello HDInsight cluster.</span></span> <span data-ttu-id="e44c9-2690">자세한 내용은 [Azure Data Factory에서 지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2690">For details, see [supported HDInsight versions in Azure Data Factory](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> |<span data-ttu-id="e44c9-2691">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2691">No</span></span> |
| <span data-ttu-id="e44c9-2692">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2692">linkedServiceName</span></span> |<span data-ttu-id="e44c9-2693">Azure 저장소 연결 서비스 toobe를 저장 하 고 데이터 처리에 대 한 hello 주문형 클러스터에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2693">Azure Storage linked service toobe used by hello on-demand cluster for storing and processing data.</span></span> <p><span data-ttu-id="e44c9-2694">현재, hello 저장소로 Azure 데이터 레이크 저장소를 사용 하는 주문형 HDInsight 클러스터를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2694">Currently, you cannot create an on-demand HDInsight cluster that uses an Azure Data Lake Store as hello storage.</span></span> <span data-ttu-id="e44c9-2695">Azure 데이터 레이크 저장소에서 처리 하는 HDInsight에서 toostore hello 결과 데이터를 원하는 hello Azure Blob 저장소 toohello Azure 데이터 레이크 저장소에서에서 복사 작업 toocopy hello 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2695">If you want toostore hello result data from HDInsight processing in an Azure Data Lake Store, use a Copy Activity toocopy hello data from hello Azure Blob Storage toohello Azure Data Lake Store.</span></span></p>  | <span data-ttu-id="e44c9-2696">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2696">Yes</span></span> |
| <span data-ttu-id="e44c9-2697">additionalLinkedServiceNames</span><span class="sxs-lookup"><span data-stu-id="e44c9-2697">additionalLinkedServiceNames</span></span> |<span data-ttu-id="e44c9-2698">HDInsight hello에 대 한 추가 저장소 계정을 연결 된 서비스 hello 데이터 팩터리 서비스에서 사용자 대신 등록할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2698">Specifies additional storage accounts for hello HDInsight linked service so that hello Data Factory service can register them on your behalf.</span></span> |<span data-ttu-id="e44c9-2699">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2699">No</span></span> |
| <span data-ttu-id="e44c9-2700">osType</span><span class="sxs-lookup"><span data-stu-id="e44c9-2700">osType</span></span> |<span data-ttu-id="e44c9-2701">운영 체제 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2701">Type of operating system.</span></span> <span data-ttu-id="e44c9-2702">허용되는 값은 Windows(기본값) 및 Linux입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2702">Allowed values are: Windows (default) and Linux</span></span> |<span data-ttu-id="e44c9-2703">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2703">No</span></span> |
| <span data-ttu-id="e44c9-2704">hcatalogLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2704">hcatalogLinkedServiceName</span></span> |<span data-ttu-id="e44c9-2705">Azure SQL 연결의 hello 이름에 해당 지점 toohello HCatalog 데이터베이스를 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2705">hello name of Azure SQL linked service that point toohello HCatalog database.</span></span> <span data-ttu-id="e44c9-2706">hello 주문형 HDInsight 클러스터는 hello metastore로 hello Azure SQL 데이터베이스를 사용 하 여 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2706">hello on-demand HDInsight cluster is created by using hello Azure SQL database as hello metastore.</span></span> |<span data-ttu-id="e44c9-2707">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2707">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="e44c9-2708">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2708">JSON example</span></span>
<span data-ttu-id="e44c9-2709">다음 JSON hello Linux 기반에 주문형 HDInsight 연결 된 서비스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2709">hello following JSON defines a Linux-based on-demand HDInsight linked service.</span></span> <span data-ttu-id="e44c9-2710">hello 데이터 팩터리 서비스를 자동으로 만듭니다는 **Linux 기반** HDInsight 클러스터는 데이터 조각을 처리 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2710">hello Data Factory service automatically creates a **Linux-based** HDInsight cluster when processing a data slice.</span></span> 

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

<span data-ttu-id="e44c9-2711">자세한 내용은 [계산 연결된 서비스](data-factory-compute-linked-services.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2711">For more information, see [Compute linked services](data-factory-compute-linked-services.md) article.</span></span> 

## <a name="existing-azure-hdinsight-cluster"></a><span data-ttu-id="e44c9-2712">기존 Azure HDInsight 클러스터</span><span class="sxs-lookup"><span data-stu-id="e44c9-2712">Existing Azure HDInsight cluster</span></span>
<span data-ttu-id="e44c9-2713">데이터 팩터리에 Azure HDInsight 연결 된 서비스 tooregister 고유한 HDInsight 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2713">You can create an Azure HDInsight linked service tooregister your own HDInsight cluster with Data Factory.</span></span> <span data-ttu-id="e44c9-2714">Hello에 나오는 데이터 변환 작업에 따라이 연결 된 서비스를 실행할 수 있습니다: [.NET 사용자 지정 활동](#net-custom-activity), [활동 하이브](#hdinsight-hive-activity), [활동 Pig] (#hdinsight pig-작업, [MapReduce 활동](#hdinsight-mapreduce-activity), [Hadoop 스트리밍 작업](#hdinsight-streaming-activityd), [활동 멤버](#hdinsight-spark-activity)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2714">You can run hello following data transformation activities on this linked service: [.NET custom activity](#net-custom-activity), [Hive activity](#hdinsight-hive-activity), [Pig activity](#hdinsight-pig-activity, [MapReduce activity](#hdinsight-mapreduce-activity), [Hadoop streaming activity](#hdinsight-streaming-activityd), [Spark activity](#hdinsight-spark-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2715">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2715">Linked service</span></span>
<span data-ttu-id="e44c9-2716">다음 표에서 hello Azure HDInsight 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2716">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure HDInsight linked service.</span></span>

| <span data-ttu-id="e44c9-2717">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2717">Property</span></span> | <span data-ttu-id="e44c9-2718">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2718">Description</span></span> | <span data-ttu-id="e44c9-2719">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2719">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2720">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2720">type</span></span> |<span data-ttu-id="e44c9-2721">너무 hello 유형 속성을 설정 해야**HDInsight**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2721">hello type property should be set too**HDInsight**.</span></span> |<span data-ttu-id="e44c9-2722">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2722">Yes</span></span> |
| <span data-ttu-id="e44c9-2723">clusterUri</span><span class="sxs-lookup"><span data-stu-id="e44c9-2723">clusterUri</span></span> |<span data-ttu-id="e44c9-2724">hello hello HDInsight 클러스터의 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2724">hello URI of hello HDInsight cluster.</span></span> |<span data-ttu-id="e44c9-2725">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2725">Yes</span></span> |
| <span data-ttu-id="e44c9-2726">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2726">username</span></span> |<span data-ttu-id="e44c9-2727">Tooconnect tooan 기존 HDInsight 클러스터를 사용 하는 hello 사용자 toobe의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2727">Specify hello name of hello user toobe used tooconnect tooan existing HDInsight cluster.</span></span> |<span data-ttu-id="e44c9-2728">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2728">Yes</span></span> |
| <span data-ttu-id="e44c9-2729">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2729">password</span></span> |<span data-ttu-id="e44c9-2730">Hello 사용자 계정의 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2730">Specify password for hello user account.</span></span> |<span data-ttu-id="e44c9-2731">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2731">Yes</span></span> |
| <span data-ttu-id="e44c9-2732">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2732">linkedServiceName</span></span> | <span data-ttu-id="e44c9-2733">Hello HDInsight 클러스터의 hello toohello Azure blob 저장소를 참조 하는 Azure 저장소 연결 서비스의 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2733">Name of hello Azure Storage linked service that refers toohello Azure blob storage used by hello HDInsight cluster.</span></span> <p><span data-ttu-id="e44c9-2734">현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2734">Currently, you cannot specify an Azure Data Lake Store linked service for this property.</span></span> <span data-ttu-id="e44c9-2735">Hello HDInsight 클러스터에 데이터 레이크 저장소 액세스 toohello 경우 Hive/Pig 스크립트에서 hello Azure 데이터 레이크 저장소의에서 데이터를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2735">You may access data in hello Azure Data Lake Store from Hive/Pig scripts if hello HDInsight cluster has access toohello Data Lake Store.</span></span> </p>  |<span data-ttu-id="e44c9-2736">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2736">Yes</span></span> |

<span data-ttu-id="e44c9-2737">지원되는 HDInsight 클러스터 버전은 [지원되는 HDInsight 버전](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2737">For versions of HDInsight clusters supported, see [supported HDInsight versions](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory).</span></span> 

#### <a name="json-example"></a><span data-ttu-id="e44c9-2738">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2738">JSON example</span></span>

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

## <a name="azure-batch"></a><span data-ttu-id="e44c9-2739">Azure 배치</span><span class="sxs-lookup"><span data-stu-id="e44c9-2739">Azure Batch</span></span>
<span data-ttu-id="e44c9-2740">데이터 팩터리와 연결 된 Azure 배치 서비스 tooregister 가상 컴퓨터 (Vm)의 일괄 처리 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2740">You can create an Azure Batch linked service tooregister a Batch pool of virtual machines (VMs) with a data factory.</span></span> <span data-ttu-id="e44c9-2741">Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2741">You can run .NET custom activities using either Azure Batch or Azure HDInsight.</span></span> <span data-ttu-id="e44c9-2742">이 연결된 서비스에서 [.NET 사용자 지정 활동](#net-custom-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2742">You can run a [.NET custom activity](#net-custom-activity) on this linked service.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2743">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2743">Linked service</span></span>
<span data-ttu-id="e44c9-2744">다음 표에서 hello Azure 배치 연결 된 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2744">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Batch linked service.</span></span>

| <span data-ttu-id="e44c9-2745">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2745">Property</span></span> | <span data-ttu-id="e44c9-2746">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2746">Description</span></span> | <span data-ttu-id="e44c9-2747">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2747">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2748">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2748">type</span></span> |<span data-ttu-id="e44c9-2749">너무 hello 유형 속성을 설정 해야**AzureBatch**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2749">hello type property should be set too**AzureBatch**.</span></span> |<span data-ttu-id="e44c9-2750">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2750">Yes</span></span> |
| <span data-ttu-id="e44c9-2751">accountName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2751">accountName</span></span> |<span data-ttu-id="e44c9-2752">Azure 배치 계정 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2752">Name of hello Azure Batch account.</span></span> |<span data-ttu-id="e44c9-2753">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2753">Yes</span></span> |
| <span data-ttu-id="e44c9-2754">accessKey</span><span class="sxs-lookup"><span data-stu-id="e44c9-2754">accessKey</span></span> |<span data-ttu-id="e44c9-2755">Hello Azure 배치 계정에 대 한 액세스 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2755">Access key for hello Azure Batch account.</span></span> |<span data-ttu-id="e44c9-2756">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2756">Yes</span></span> |
| <span data-ttu-id="e44c9-2757">poolName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2757">poolName</span></span> |<span data-ttu-id="e44c9-2758">가상 컴퓨터의 hello 풀의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2758">Name of hello pool of virtual machines.</span></span> |<span data-ttu-id="e44c9-2759">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2759">Yes</span></span> |
| <span data-ttu-id="e44c9-2760">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2760">linkedServiceName</span></span> |<span data-ttu-id="e44c9-2761">Hello이 Azure 배치 연결 된 서비스와 연결 된 Azure 저장소 연결 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2761">Name of hello Azure Storage linked service associated with this Azure Batch linked service.</span></span> <span data-ttu-id="e44c9-2762">준비 파일에 대 한이 연결 된 서비스는 필요한 toorun hello 활동 및 hello 활동 실행 로그를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2762">This linked service is used for staging files required toorun hello activity and storing hello activity execution logs.</span></span> |<span data-ttu-id="e44c9-2763">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2763">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="e44c9-2764">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2764">JSON example</span></span>

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

## <a name="azure-machine-learning"></a><span data-ttu-id="e44c9-2765">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="e44c9-2765">Azure Machine Learning</span></span>
<span data-ttu-id="e44c9-2766">기계 학습 일괄 점수 매기기 끝점용 데이터 팩터리에 Azure 기계 학습 연결 서비스 tooregister를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2766">You create an Azure Machine Learning linked service tooregister a Machine Learning batch scoring endpoint with a data factory.</span></span> <span data-ttu-id="e44c9-2767">이 연결된 서비스에서는 두 가지 데이터 변환 활동, 즉 [Machine Learning 배치 실행 활동](#machine-learning-batch-execution-activity)과, [Machine Learning 업데이트 리소스 활동](#machine-learning-update-resource-activity)을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2767">Two data transformation activities that can run on this linked service: [Machine Learning Batch Execution Activity](#machine-learning-batch-execution-activity), [Machine Learning Update Resource Activity](#machine-learning-update-resource-activity).</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2768">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2768">Linked service</span></span>
<span data-ttu-id="e44c9-2769">다음 표에서 hello Azure 기계 학습 연결 서비스의 hello Azure JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2769">hello following table provides descriptions for hello properties used in hello Azure JSON definition of an Azure Machine Learning linked service.</span></span>

| <span data-ttu-id="e44c9-2770">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2770">Property</span></span> | <span data-ttu-id="e44c9-2771">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2771">Description</span></span> | <span data-ttu-id="e44c9-2772">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2772">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2773">형식</span><span class="sxs-lookup"><span data-stu-id="e44c9-2773">Type</span></span> |<span data-ttu-id="e44c9-2774">hello type 속성이로 설정 해야: **AzureML**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2774">hello type property should be set to: **AzureML**.</span></span> |<span data-ttu-id="e44c9-2775">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2775">Yes</span></span> |
| <span data-ttu-id="e44c9-2776">mlEndpoint</span><span class="sxs-lookup"><span data-stu-id="e44c9-2776">mlEndpoint</span></span> |<span data-ttu-id="e44c9-2777">hello 일괄 처리 첨 수 매기기 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2777">hello batch scoring URL.</span></span> |<span data-ttu-id="e44c9-2778">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2778">Yes</span></span> |
| <span data-ttu-id="e44c9-2779">apiKey</span><span class="sxs-lookup"><span data-stu-id="e44c9-2779">apiKey</span></span> |<span data-ttu-id="e44c9-2780">hello 작업 영역 모델의 API를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2780">hello published workspace model’s API.</span></span> |<span data-ttu-id="e44c9-2781">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2781">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="e44c9-2782">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2782">JSON example</span></span>

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

## <a name="azure-data-lake-analytics"></a><span data-ttu-id="e44c9-2783">Azure 데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="e44c9-2783">Azure Data Lake Analytics</span></span>
<span data-ttu-id="e44c9-2784">만들 프로그램 **Azure 데이터 레이크 분석** hello를 사용 하기 전에 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 [데이터 레이크 분석 U-SQL 작업](data-factory-usql-activity.md) 파이프라인에서 .</span><span class="sxs-lookup"><span data-stu-id="e44c9-2784">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory before using hello [Data Lake Analytics U-SQL activity](data-factory-usql-activity.md) in a pipeline.</span></span>

### <a name="linked-service"></a><span data-ttu-id="e44c9-2785">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2785">Linked service</span></span>

<span data-ttu-id="e44c9-2786">다음 표에서 hello 연결 된 Azure Data Lake 분석 서비스의 hello JSON 정의에서 사용 되는 hello 속성에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2786">hello following table provides descriptions for hello properties used in hello JSON definition of an Azure Data Lake Analytics linked service.</span></span> 

| <span data-ttu-id="e44c9-2787">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2787">Property</span></span> | <span data-ttu-id="e44c9-2788">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2788">Description</span></span> | <span data-ttu-id="e44c9-2789">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2789">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2790">형식</span><span class="sxs-lookup"><span data-stu-id="e44c9-2790">Type</span></span> |<span data-ttu-id="e44c9-2791">hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2791">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="e44c9-2792">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2792">Yes</span></span> |
| <span data-ttu-id="e44c9-2793">accountName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2793">accountName</span></span> |<span data-ttu-id="e44c9-2794">Azure 데이터 레이크 분석 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2794">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="e44c9-2795">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2795">Yes</span></span> |
| <span data-ttu-id="e44c9-2796">dataLakeAnalyticsUri</span><span class="sxs-lookup"><span data-stu-id="e44c9-2796">dataLakeAnalyticsUri</span></span> |<span data-ttu-id="e44c9-2797">Azure 데이터 레이크 분석 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2797">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="e44c9-2798">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2798">No</span></span> |
| <span data-ttu-id="e44c9-2799">권한 부여</span><span class="sxs-lookup"><span data-stu-id="e44c9-2799">authorization</span></span> |<span data-ttu-id="e44c9-2800">인증 코드를 클릭 한 후 자동으로 검색 됩니다 **Authorize** hello 데이터 팩터리 편집기 및 완료 hello OAuth 로그인 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2800">Authorization code is automatically retrieved after clicking **Authorize** button in hello Data Factory Editor and completing hello OAuth login.</span></span> |<span data-ttu-id="e44c9-2801">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2801">Yes</span></span> |
| <span data-ttu-id="e44c9-2802">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e44c9-2802">subscriptionId</span></span> |<span data-ttu-id="e44c9-2803">Azure 구독 ID</span><span class="sxs-lookup"><span data-stu-id="e44c9-2803">Azure subscription id</span></span> |<span data-ttu-id="e44c9-2804">아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2804">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="e44c9-2805">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2805">resourceGroupName</span></span> |<span data-ttu-id="e44c9-2806">Azure 리소스 그룹 이름</span><span class="sxs-lookup"><span data-stu-id="e44c9-2806">Azure resource group name</span></span> |<span data-ttu-id="e44c9-2807">아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2807">No (If not specified, resource group of hello data factory is used).</span></span> |
| <span data-ttu-id="e44c9-2808">sessionId</span><span class="sxs-lookup"><span data-stu-id="e44c9-2808">sessionId</span></span> |<span data-ttu-id="e44c9-2809">hello OAuth 권한 부여 세션에서 세션 id입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2809">session id from hello OAuth authorization session.</span></span> <span data-ttu-id="e44c9-2810">각 세션 ID는 고유하고 한 번만 사용될 수 있으며 </span><span class="sxs-lookup"><span data-stu-id="e44c9-2810">Each session id is unique and may only be used once.</span></span> <span data-ttu-id="e44c9-2811">이 ID는 hello 데이터 팩터리 편집기를 사용 하면 자동으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2811">When you use hello Data Factory Editor, this ID is auto-generated.</span></span> |<span data-ttu-id="e44c9-2812">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2812">Yes</span></span> |


#### <a name="json-example"></a><span data-ttu-id="e44c9-2813">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2813">JSON example</span></span>
<span data-ttu-id="e44c9-2814">다음 예에서는 hello 연결 된 Azure Data Lake 분석 서비스에 대 한 JSON 정의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2814">hello following example provides JSON definition for an Azure Data Lake Analytics linked service.</span></span>

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

## <a name="azure-sql-database"></a><span data-ttu-id="e44c9-2815">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e44c9-2815">Azure SQL Database</span></span>
<span data-ttu-id="e44c9-2816">Azure SQL 연결 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](#stored-procedure-activity) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2816">You create an Azure SQL linked service and use it with hello [Stored Procedure Activity](#stored-procedure-activity) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2817">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2817">Linked service</span></span>
<span data-ttu-id="e44c9-2818">toodefine Azure SQL 데이터베이스에 연결 된 서비스를 집합 hello **형식** hello 연결 서비스 너무**AzureSqlDatabase**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2818">toodefine an Azure SQL Database linked service, set hello **type** of hello linked service too**AzureSqlDatabase**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2819">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2819">Property</span></span> | <span data-ttu-id="e44c9-2820">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2820">Description</span></span> | <span data-ttu-id="e44c9-2821">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2821">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2822">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-2822">connectionString</span></span> |<span data-ttu-id="e44c9-2823">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터베이스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2823">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-2824">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2824">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="e44c9-2825">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2825">JSON example</span></span>

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

<span data-ttu-id="e44c9-2826">이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2826">See [Azure SQL Connector](data-factory-azure-sql-connector.md#linked-service-properties) article for details about this linked service.</span></span>

## <a name="azure-sql-data-warehouse"></a><span data-ttu-id="e44c9-2827">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2827">Azure SQL Data Warehouse</span></span>
<span data-ttu-id="e44c9-2828">Azure SQL 데이터 웨어하우스 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2828">You create an Azure SQL Data Warehouse linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2829">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2829">Linked service</span></span>
<span data-ttu-id="e44c9-2830">연결 된 서비스를 집합 hello Azure SQL 데이터 웨어하우스 toodefine **형식** hello 연결 서비스 너무**AzureSqlDW**, 다음 hello에 대 한 속성을 지정 하 고 **typeProperties**섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2830">toodefine an Azure SQL Data Warehouse linked service, set hello **type** of hello linked service too**AzureSqlDW**, and specify following properties in hello **typeProperties** section:</span></span>  

| <span data-ttu-id="e44c9-2831">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2831">Property</span></span> | <span data-ttu-id="e44c9-2832">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2832">Description</span></span> | <span data-ttu-id="e44c9-2833">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2833">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2834">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-2834">connectionString</span></span> |<span data-ttu-id="e44c9-2835">Hello connectionString 속성에 대 한 tooconnect toohello Azure SQL 데이터 웨어하우스 인스턴스는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2835">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> |<span data-ttu-id="e44c9-2836">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2836">Yes</span></span> |

#### <a name="json-example"></a><span data-ttu-id="e44c9-2837">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2837">JSON example</span></span>

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

<span data-ttu-id="e44c9-2838">자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2838">For more information, see [Azure SQL Data Warehouse connector](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) article.</span></span> 

## <a name="sql-server"></a><span data-ttu-id="e44c9-2839">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e44c9-2839">SQL Server</span></span> 
<span data-ttu-id="e44c9-2840">SQL Server 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2840">You create a SQL Server linked service and use it with hello [Stored Procedure Activity](data-factory-stored-proc-activity.md) tooinvoke a stored procedure from a Data Factory pipeline.</span></span> 

### <a name="linked-service"></a><span data-ttu-id="e44c9-2841">연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-2841">Linked service</span></span>
<span data-ttu-id="e44c9-2842">형식의 연결 된 서비스를 만들면 **OnPremisesSqlServer** toolink 온-프레미스 SQL Server 데이터베이스 tooa 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2842">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="e44c9-2843">다음 표에서 hello JSON 요소 특정 tooon 온-프레미스 SQL Server 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2843">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="e44c9-2844">다음 표에서 hello JSON 요소 특정 tooSQL 연결 된 서버 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2844">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="e44c9-2845">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2845">Property</span></span> | <span data-ttu-id="e44c9-2846">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2846">Description</span></span> | <span data-ttu-id="e44c9-2847">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2847">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2848">type</span><span class="sxs-lookup"><span data-stu-id="e44c9-2848">type</span></span> |<span data-ttu-id="e44c9-2849">hello type 속성이로 설정 해야: **OnPremisesSqlServer**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2849">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="e44c9-2850">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2850">Yes</span></span> |
| <span data-ttu-id="e44c9-2851">connectionString</span><span class="sxs-lookup"><span data-stu-id="e44c9-2851">connectionString</span></span> |<span data-ttu-id="e44c9-2852">SQL 인증 또는 Windows 인증을 사용 하 여 tooconnect toohello 온-프레미스 SQL Server 데이터베이스는 데 필요한 connectionString 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2852">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="e44c9-2853">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2853">Yes</span></span> |
| <span data-ttu-id="e44c9-2854">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e44c9-2854">gatewayName</span></span> |<span data-ttu-id="e44c9-2855">데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 SQL Server 데이터베이스를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2855">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="e44c9-2856">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2856">Yes</span></span> |
| <span data-ttu-id="e44c9-2857">username</span><span class="sxs-lookup"><span data-stu-id="e44c9-2857">username</span></span> |<span data-ttu-id="e44c9-2858">Windows 인증을 사용하는 경우 사용자 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2858">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="e44c9-2859">예: **domainname\\username**.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2859">Example: **domainname\\username**.</span></span> |<span data-ttu-id="e44c9-2860">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2860">No</span></span> |
| <span data-ttu-id="e44c9-2861">암호</span><span class="sxs-lookup"><span data-stu-id="e44c9-2861">password</span></span> |<span data-ttu-id="e44c9-2862">Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2862">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e44c9-2863">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2863">No</span></span> |

<span data-ttu-id="e44c9-2864">Hello를 사용 하 여 자격 증명을 암호화할 수 **새로 AzureRmDataFactoryEncryptValue** cmdlet hello 다음 예제와 같이 hello 연결 문자열에서 사용 하 고 (**EncryptedCredential** 속성):</span><span class="sxs-lookup"><span data-stu-id="e44c9-2864">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a><span data-ttu-id="e44c9-2865">예제: SQL 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="e44c9-2865">Example: JSON for using SQL Authentication</span></span>

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
#### <a name="example-json-for-using-windows-authentication"></a><span data-ttu-id="e44c9-2866">예제: Windows 인증을 사용하는 JSON</span><span class="sxs-lookup"><span data-stu-id="e44c9-2866">Example: JSON for using Windows Authentication</span></span>

<span data-ttu-id="e44c9-2867">사용자 이름 및 암호를 지정 하는 경우 게이트웨이에서 사용 하 여 해당 tooimpersonate hello 지정 된 사용자 계정 tooconnect toohello 온-프레미스 SQL Server 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2867">If username and password are specified, gateway uses them tooimpersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> <span data-ttu-id="e44c9-2868">그렇지 않은 경우 게이트웨이 게이트웨이 (시작 계정)의 보안 컨텍스트 hello와 직접 toohello SQL Server를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2868">Otherwise, gateway connects toohello SQL Server directly with hello security context of Gateway (its startup account).</span></span>

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

<span data-ttu-id="e44c9-2869">자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2869">For more information, see [SQL Server connector](data-factory-sqlserver-connector.md#linked-service-properties) article.</span></span>

## <a name="data-transformation-activities"></a><span data-ttu-id="e44c9-2870">데이터 변환 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2870">DATA TRANSFORMATION ACTIVITIES</span></span>

<span data-ttu-id="e44c9-2871">작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2871">Activity</span></span> | <span data-ttu-id="e44c9-2872">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2872">Description</span></span>
-------- | -----------
[<span data-ttu-id="e44c9-2873">HDInsight Hive 활동</span><span class="sxs-lookup"><span data-stu-id="e44c9-2873">HDInsight Hive activity</span></span>](#hdinsight-hive-activity) | <span data-ttu-id="e44c9-2874">데이터 팩터리 파이프라인에서 HDInsight Hive 활동 hello 하이브 쿼리를 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2874">hello HDInsight Hive activity in a Data Factory pipeline executes Hive queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span> 
[<span data-ttu-id="e44c9-2875">HDInsight Pig 활동</span><span class="sxs-lookup"><span data-stu-id="e44c9-2875">HDInsight Pig activity</span></span>](#hdinsight-pig-activity) | <span data-ttu-id="e44c9-2876">hello 데이터 팩터리 파이프라인에서 HDInsight Pig 작업을 직접 Pig 쿼리 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2876">hello HDInsight Pig activity in a Data Factory pipeline executes Pig queries on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="e44c9-2877">HDInsight MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2877">HDInsight MapReduce Activity</span></span>](#hdinsight-mapreduce-activity) | <span data-ttu-id="e44c9-2878">데이터 팩터리 파이프라인에서 HDInsight MapReduce 작업 hello MapReduce 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2878">hello HDInsight MapReduce activity in a Data Factory pipeline executes MapReduce programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="e44c9-2879">HDInsight 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2879">HDInsight Streaming Activity</span></span>](#hdinsight-streaming-activity) | <span data-ttu-id="e44c9-2880">데이터 팩터리 파이프라인에서 HDInsight 스트리밍 활동 hello Hadoop 스트리밍 프로그램을 직접 또는 요청 시 Windows/Linux 기반 HDInsight 클러스터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2880">hello HDInsight Streaming Activity in a Data Factory pipeline executes Hadoop Streaming programs on your own or on-demand Windows/Linux-based HDInsight cluster.</span></span>
[<span data-ttu-id="e44c9-2881">HDInsight Spark 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2881">HDInsight Spark Activity</span></span>](#hdinsight-spark-activity) | <span data-ttu-id="e44c9-2882">데이터 팩터리 파이프라인에서 HDInsight Spark 활동 hello 고유한 HDInsight 클러스터에서 Spark 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2882">hello HDInsight Spark activity in a Data Factory pipeline executes Spark programs on your own HDInsight cluster.</span></span> 
[<span data-ttu-id="e44c9-2883">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2883">Machine Learning Batch Execution Activity</span></span>](#machine-learning-batch-execution-activity) | <span data-ttu-id="e44c9-2884">웹 predictive analytics에 대해 서비스에 tooeasily 하면 게시 된 Azure 기계 학습을 사용 하는 파이프라인을 생성 하는 azure Data Factory 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2884">Azure Data Factory enables you tooeasily create pipelines that use a published Azure Machine Learning web service for predictive analytics.</span></span> <span data-ttu-id="e44c9-2885">Azure 데이터 팩터리 파이프라인에서 일괄 처리 실행 작업 hello를 사용 하 여 hello 데이터 일괄 처리에 대 한 기계 학습 웹 서비스 toomake 예측을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2885">Using hello Batch Execution Activity in an Azure Data Factory pipeline, you can invoke a Machine Learning web service toomake predictions on hello data in batch.</span></span> 
[<span data-ttu-id="e44c9-2886">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2886">Machine Learning Update Resource Activity</span></span>](#machine-learning-update-resource-activity) | <span data-ttu-id="e44c9-2887">시간이 지남에 따라 hello 예측 모델 hello 점수 매기기 실험 toobe 다시 학습 되도록 new를 사용 하 여 필요한 기계 학습의에서 입력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2887">Over time, hello predictive models in hello Machine Learning scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="e44c9-2888">재교육를 완료 한 후 웹 서비스 hello와 점수 매기기 tooupdate hello 기계 학습 모델을 다시 학습 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2888">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained Machine Learning model.</span></span> <span data-ttu-id="e44c9-2889">Hello 새로 학습 모델로 hello 업데이트 리소스 작업 tooupdate hello 웹 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2889">You can use hello Update Resource Activity tooupdate hello web service with hello newly trained model.</span></span>
[<span data-ttu-id="e44c9-2890">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2890">Stored Procedure Activity</span></span>](#stored-procedure-activity) | <span data-ttu-id="e44c9-2891">데이터 팩터리 파이프라인 tooinvoke hello 데이터 저장소를 다음 중 하나에 있는 저장된 프로시저의에서 hello 저장 프로시저 작업을 사용할 수 있습니다: Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, 기업 내에 SQL Server 데이터베이스 또는 Azure VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2891">You can use hello Stored Procedure activity in a Data Factory pipeline tooinvoke a stored procedure in one of hello following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or an Azure VM.</span></span> 
[<span data-ttu-id="e44c9-2892">Data Lake Analytics U-SQL 활동</span><span class="sxs-lookup"><span data-stu-id="e44c9-2892">Data Lake Analytics U-SQL activity</span></span>](#data-lake-analytics-u-sql-activity) | <span data-ttu-id="e44c9-2893">Data Lake Analytics U-SQL 작업은 Azure Data Lake Analytics 클러스터에 대해 U-SQL 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2893">Data Lake Analytics U-SQL Activity runs a U-SQL script on an Azure Data Lake Analytics cluster.</span></span>  
[<span data-ttu-id="e44c9-2894">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2894">.NET custom activity</span></span>](#net-custom-activity) | <span data-ttu-id="e44c9-2895">데이터 팩터리에서 지원 되지 않는 방식으로 tootransform 데이터를 유지 해야 하는 경우 고유의 데이터 처리 논리와 사용자 지정 활동을 만들 있고 hello 파이프라인에서 hello 활동을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2895">If you need tootransform data in a way that is not supported by Data Factory, you can create a custom activity with your own data processing logic and use hello activity in hello pipeline.</span></span> <span data-ttu-id="e44c9-2896">Hello 사용자 지정.NET 작업 toorun Azure 배치 서비스 또는 Azure HDInsight 클러스터를 사용 하 여 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2896">You can configure hello custom .NET activity toorun using either an Azure Batch service or an Azure HDInsight cluster.</span></span> 

     
## <a name="hdinsight-hive-activity"></a><span data-ttu-id="e44c9-2897">HDInsight Hive 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2897">HDInsight Hive Activity</span></span>
<span data-ttu-id="e44c9-2898">Hello 다음과 같은 Hive 활동 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2898">You can specify hello following properties in a Hive Activity JSON definition.</span></span> <span data-ttu-id="e44c9-2899">hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightHive**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2899">hello type property for hello activity must be: **HDInsightHive**.</span></span> <span data-ttu-id="e44c9-2900">HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2900">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-2901">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightHive 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2901">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightHive:</span></span>

| <span data-ttu-id="e44c9-2902">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2902">Property</span></span> | <span data-ttu-id="e44c9-2903">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2903">Description</span></span> | <span data-ttu-id="e44c9-2904">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2904">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2905">script</span><span class="sxs-lookup"><span data-stu-id="e44c9-2905">script</span></span> |<span data-ttu-id="e44c9-2906">Hello Hive 스크립트를 인라인으로 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-2906">Specify hello Hive script inline</span></span> |<span data-ttu-id="e44c9-2907">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2907">No</span></span> |
| <span data-ttu-id="e44c9-2908">script path</span><span class="sxs-lookup"><span data-stu-id="e44c9-2908">script path</span></span> |<span data-ttu-id="e44c9-2909">저장소 hello 하이브 스크립트에는 Azure blob 저장소에 있으며 hello toohello 파일 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2909">Store hello Hive script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="e44c9-2910">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2910">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="e44c9-2911">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2911">Both cannot be used together.</span></span> <span data-ttu-id="e44c9-2912">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2912">hello file name is case-sensitive.</span></span> |<span data-ttu-id="e44c9-2913">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2913">No</span></span> |
| <span data-ttu-id="e44c9-2914">defines</span><span class="sxs-lookup"><span data-stu-id="e44c9-2914">defines</span></span> |<span data-ttu-id="e44c9-2915">매개 변수를 'hiveconf'를 사용 하 여 hello 하이브 스크립트 내에서 참조 하는 것에 대 한 키/값 쌍으로 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-2915">Specify parameters as key/value pairs for referencing within hello Hive script using 'hiveconf'</span></span> |<span data-ttu-id="e44c9-2916">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2916">No</span></span> |

<span data-ttu-id="e44c9-2917">이러한 형식 속성은 특정 toohello Hive 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2917">These type properties are specific toohello Hive Activity.</span></span> <span data-ttu-id="e44c9-2918">Hello typeProperties 섹션) (외부 다른 속성은 모든 활동에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2918">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="e44c9-2919">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2919">JSON example</span></span>
<span data-ttu-id="e44c9-2920">다음 JSON hello 파이프라인에서 HDInsight Hive 활동을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2920">hello following JSON defines a HDInsight Hive activity in a pipeline.</span></span>  

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

<span data-ttu-id="e44c9-2921">자세한 내용은 [Hive 활동](data-factory-hive-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2921">For more information, see [Hive Activity](data-factory-hive-activity.md) article.</span></span> 

## <a name="hdinsight-pig-activity"></a><span data-ttu-id="e44c9-2922">HDInsight Pig 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2922">HDInsight Pig Activity</span></span>
<span data-ttu-id="e44c9-2923">Hello 다음과 같은 Pig 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2923">You can specify hello following properties in a Pig Activity JSON definition.</span></span> <span data-ttu-id="e44c9-2924">hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightPig**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2924">hello type property for hello activity must be: **HDInsightPig**.</span></span> <span data-ttu-id="e44c9-2925">HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2925">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-2926">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightPig 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2926">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightPig:</span></span> 

| <span data-ttu-id="e44c9-2927">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2927">Property</span></span> | <span data-ttu-id="e44c9-2928">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2928">Description</span></span> | <span data-ttu-id="e44c9-2929">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2929">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2930">script</span><span class="sxs-lookup"><span data-stu-id="e44c9-2930">script</span></span> |<span data-ttu-id="e44c9-2931">Hello Pig 스크립트를 인라인으로 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-2931">Specify hello Pig script inline</span></span> |<span data-ttu-id="e44c9-2932">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2932">No</span></span> |
| <span data-ttu-id="e44c9-2933">script path</span><span class="sxs-lookup"><span data-stu-id="e44c9-2933">script path</span></span> |<span data-ttu-id="e44c9-2934">Azure blob 저장소에 hello Pig 스크립트를 저장 하 고 hello toohello 파일 경로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2934">Store hello Pig script in an Azure blob storage and provide hello path toohello file.</span></span> <span data-ttu-id="e44c9-2935">'script' 또는 'scriptPath' 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2935">Use 'script' or 'scriptPath' property.</span></span> <span data-ttu-id="e44c9-2936">둘 모두를 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2936">Both cannot be used together.</span></span> <span data-ttu-id="e44c9-2937">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2937">hello file name is case-sensitive.</span></span> |<span data-ttu-id="e44c9-2938">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2938">No</span></span> |
| <span data-ttu-id="e44c9-2939">defines</span><span class="sxs-lookup"><span data-stu-id="e44c9-2939">defines</span></span> |<span data-ttu-id="e44c9-2940">키/값 쌍으로 hello Pig 스크립트 내에서 참조 하는 것에 대 한 매개 변수를 지정</span><span class="sxs-lookup"><span data-stu-id="e44c9-2940">Specify parameters as key/value pairs for referencing within hello Pig script</span></span> |<span data-ttu-id="e44c9-2941">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2941">No</span></span> |

<span data-ttu-id="e44c9-2942">이러한 형식 속성은 특정 toohello Pig 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2942">These type properties are specific toohello Pig Activity.</span></span> <span data-ttu-id="e44c9-2943">Hello typeProperties 섹션) (외부 다른 속성은 모든 활동에 대해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2943">Other properties (outside hello typeProperties section) are supported for all activities.</span></span>   

### <a name="json-example"></a><span data-ttu-id="e44c9-2944">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2944">JSON example</span></span>

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

<span data-ttu-id="e44c9-2945">자세한 내용은 [Pig 활동](#data-factory-pig-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2945">For more information, see [Pig Activity](#data-factory-pig-activity.md) article.</span></span> 

## <a name="hdinsight-mapreduce-activity"></a><span data-ttu-id="e44c9-2946">HDInsight MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2946">HDInsight MapReduce Activity</span></span>
<span data-ttu-id="e44c9-2947">Hello 다음과 같은 MapReduce 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2947">You can specify hello following properties in a MapReduce Activity JSON definition.</span></span> <span data-ttu-id="e44c9-2948">hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightMapReduce**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2948">hello type property for hello activity must be: **HDInsightMapReduce**.</span></span> <span data-ttu-id="e44c9-2949">HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2949">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-2950">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightMapReduce 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2950">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightMapReduce:</span></span> 

| <span data-ttu-id="e44c9-2951">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2951">Property</span></span> | <span data-ttu-id="e44c9-2952">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2952">Description</span></span> | <span data-ttu-id="e44c9-2953">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-2953">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-2954">jarLinkedService</span><span class="sxs-lookup"><span data-stu-id="e44c9-2954">jarLinkedService</span></span> | <span data-ttu-id="e44c9-2955">Hello hello JAR 파일을 포함 하는 Azure 저장소에 대 한 서비스 연결 된 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2955">Name of hello linked service for hello Azure Storage that contains hello JAR file.</span></span> | <span data-ttu-id="e44c9-2956">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2956">Yes</span></span> |
| <span data-ttu-id="e44c9-2957">jarFilePath </span><span class="sxs-lookup"><span data-stu-id="e44c9-2957">jarFilePath</span></span> | <span data-ttu-id="e44c9-2958">Hello Azure 저장소에서에서 toohello JAR 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2958">Path toohello JAR file in hello Azure Storage.</span></span> | <span data-ttu-id="e44c9-2959">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2959">Yes</span></span> | 
| <span data-ttu-id="e44c9-2960">className</span><span class="sxs-lookup"><span data-stu-id="e44c9-2960">className</span></span> | <span data-ttu-id="e44c9-2961">Hello hello JAR 파일의 기본 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2961">Name of hello main class in hello JAR file.</span></span> | <span data-ttu-id="e44c9-2962">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-2962">Yes</span></span> | 
| <span data-ttu-id="e44c9-2963">arguments</span><span class="sxs-lookup"><span data-stu-id="e44c9-2963">arguments</span></span> | <span data-ttu-id="e44c9-2964">Hello MapReduce 프로그램에 대 한 쉼표로 구분 된 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2964">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="e44c9-2965">런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2965">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="e44c9-2966">toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2966">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | <span data-ttu-id="e44c9-2967">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-2967">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="e44c9-2968">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-2968">JSON example</span></span>

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
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
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

<span data-ttu-id="e44c9-2969">자세한 내용은 [MapReduce 활동](data-factory-map-reduce.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2969">For more information, see [MapReduce Activity](data-factory-map-reduce.md) article.</span></span> 

## <a name="hdinsight-streaming-activity"></a><span data-ttu-id="e44c9-2970">HDInsight 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-2970">HDInsight Streaming Activity</span></span>
<span data-ttu-id="e44c9-2971">Hello 다음과 같은 Hadoop 스트리밍 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2971">You can specify hello following properties in a Hadoop Streaming Activity JSON definition.</span></span> <span data-ttu-id="e44c9-2972">hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightStreaming**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2972">hello type property for hello activity must be: **HDInsightStreaming**.</span></span> <span data-ttu-id="e44c9-2973">HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2973">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-2974">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightStreaming 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-2974">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightStreaming:</span></span> 

| <span data-ttu-id="e44c9-2975">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-2975">Property</span></span> | <span data-ttu-id="e44c9-2976">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-2976">Description</span></span> | 
| --- | --- |
| <span data-ttu-id="e44c9-2977">mapper</span><span class="sxs-lookup"><span data-stu-id="e44c9-2977">mapper</span></span> | <span data-ttu-id="e44c9-2978">Hello 매퍼 실행 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2978">Name of hello mapper executable.</span></span> <span data-ttu-id="e44c9-2979">Hello 예제 cat.exe는 hello 매퍼 실행 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2979">In hello example, cat.exe is hello mapper executable.</span></span>| 
| <span data-ttu-id="e44c9-2980">reducer</span><span class="sxs-lookup"><span data-stu-id="e44c9-2980">reducer</span></span> | <span data-ttu-id="e44c9-2981">Hello 리 듀 서 실행 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2981">Name of hello reducer executable.</span></span> <span data-ttu-id="e44c9-2982">Hello 예제 wc.exe는 hello 리 듀 서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2982">In hello example, wc.exe is hello reducer executable.</span></span> | 
| <span data-ttu-id="e44c9-2983">input</span><span class="sxs-lookup"><span data-stu-id="e44c9-2983">input</span></span> | <span data-ttu-id="e44c9-2984">입력된 파일 (위치) hello 맵 편집기에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2984">Input file (including location) for hello mapper.</span></span> <span data-ttu-id="e44c9-2985">Hello 예에서: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample이 blob 컨테이너 hello, 예제/data/Gutenberg hello 폴더 이며 davinci.txt가 blob hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2985">In hello example: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample is hello blob container, example/data/Gutenberg is hello folder, and davinci.txt is hello blob.</span></span> |
| <span data-ttu-id="e44c9-2986">output</span><span class="sxs-lookup"><span data-stu-id="e44c9-2986">output</span></span> | <span data-ttu-id="e44c9-2987">출력 파일 위치 등 hello 리 듀 서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2987">Output file (including location) for hello reducer.</span></span> <span data-ttu-id="e44c9-2988">hello Hadoop 스트리밍 작업의 hello 출력은이 속성에 지정 된 toohello 위치를 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2988">hello output of hello Hadoop Streaming job is written toohello location specified for this property.</span></span> |
| <span data-ttu-id="e44c9-2989">filePaths</span><span class="sxs-lookup"><span data-stu-id="e44c9-2989">filePaths</span></span> | <span data-ttu-id="e44c9-2990">Hello 매퍼 및 리 듀 서 실행 파일에 대 한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2990">Paths for hello mapper and reducer executables.</span></span> <span data-ttu-id="e44c9-2991">Hello 예에서: "adfsample/example/apps/wc.exe" adfsample이 blob 컨테이너 hello, example/apps가 hello 폴더 및 wc.exe는 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2991">In hello example: "adfsample/example/apps/wc.exe", adfsample is hello blob container, example/apps is hello folder, and wc.exe is hello executable.</span></span> | 
| <span data-ttu-id="e44c9-2992">fileLinkedService</span><span class="sxs-lookup"><span data-stu-id="e44c9-2992">fileLinkedService</span></span> | <span data-ttu-id="e44c9-2993">Hello hello filePaths 섹션에 지정 된 hello 파일이 포함 된 Azure 저장소를 나타내는 azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2993">Azure Storage linked service that represents hello Azure storage that contains hello files specified in hello filePaths section.</span></span> | 
| <span data-ttu-id="e44c9-2994">arguments</span><span class="sxs-lookup"><span data-stu-id="e44c9-2994">arguments</span></span> | <span data-ttu-id="e44c9-2995">Hello MapReduce 프로그램에 대 한 쉼표로 구분 된 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2995">A list of comma-separated arguments for hello MapReduce program.</span></span> <span data-ttu-id="e44c9-2996">런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2996">At runtime, you see a few extra arguments (for example: mapreduce.job.tags) from hello MapReduce framework.</span></span> <span data-ttu-id="e44c9-2997">toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션)</span><span class="sxs-lookup"><span data-stu-id="e44c9-2997">toodifferentiate your arguments with hello MapReduce arguments, consider using both option and value as arguments as shown in hello following example (-s, --input, --output etc., are options immediately followed by their values)</span></span> | 
| <span data-ttu-id="e44c9-2998">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="e44c9-2998">getDebugInfo</span></span> | <span data-ttu-id="e44c9-2999">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-2999">An optional element.</span></span> <span data-ttu-id="e44c9-3000">TooFailure, 설정 되 면 hello 로그 오류에 대해서만 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3000">When it is set tooFailure, hello logs are downloaded only on failure.</span></span> <span data-ttu-id="e44c9-3001">TooAll, 설정 되어 있는 경우 로그 hello 실행 상태에 관계 없이 항상 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3001">When it is set tooAll, logs are always downloaded irrespective of hello execution status.</span></span> | 

> [!NOTE]
> <span data-ttu-id="e44c9-3002">Hello에 대 한 hello Hadoop 스트리밍 작업에 대 한 출력 데이터 집합을 지정 해야 **출력** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3002">You must specify an output dataset for hello Hadoop Streaming Activity for hello **outputs** property.</span></span> <span data-ttu-id="e44c9-3003">이 데이터 집합에만 dummy 하는 데이터 집합은 필요한 toodrive hello 파이프라인 일정 (시간별, 일별, 등) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3003">This dataset can be just a dummy dataset that is required toodrive hello pipeline schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="e44c9-3004">Hello 활동 입력을 사용 하지 않습니다, hello에 대 한 hello 활동에 대 한 입력된 데이터 집합 지정 건너뛸 수 있습니다 **입력** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3004">If hello activity doesn't take an input, you can skip specifying an input dataset for hello activity for hello **inputs** property.</span></span>  

## <a name="json-example"></a><span data-ttu-id="e44c9-3005">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3005">JSON example</span></span>

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

<span data-ttu-id="e44c9-3006">자세한 내용은 [Hadoop 스트리밍 활동](data-factory-hadoop-streaming-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3006">For more information, see [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md) article.</span></span> 

## <a name="hdinsight-spark-activity"></a><span data-ttu-id="e44c9-3007">HDInsight Spark 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-3007">HDInsight Spark Activity</span></span>
<span data-ttu-id="e44c9-3008">Hello 다음과 같은 Spark 활동 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3008">You can specify hello following properties in a Spark Activity JSON definition.</span></span> <span data-ttu-id="e44c9-3009">hello 활동에 대 한 hello type 속성 이어야 합니다: **HDInsightSpark**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3009">hello type property for hello activity must be: **HDInsightSpark**.</span></span> <span data-ttu-id="e44c9-3010">HDInsight 연결 된 서비스를 먼저 만든 하 고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3010">You must create a HDInsight linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-3011">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooHDInsightSpark 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3011">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooHDInsightSpark:</span></span> 

| <span data-ttu-id="e44c9-3012">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3012">Property</span></span> | <span data-ttu-id="e44c9-3013">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3013">Description</span></span> | <span data-ttu-id="e44c9-3014">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3014">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="e44c9-3015">rootPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-3015">rootPath</span></span> | <span data-ttu-id="e44c9-3016">hello Azure Blob 컨테이너 및 hello Spark 파일이 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3016">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="e44c9-3017">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3017">hello file name is case-sensitive.</span></span> | <span data-ttu-id="e44c9-3018">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3018">Yes</span></span> |
| <span data-ttu-id="e44c9-3019">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="e44c9-3019">entryFilePath</span></span> | <span data-ttu-id="e44c9-3020">Hello Spark 코드/패키지의 상대 경로 toohello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3020">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="e44c9-3021">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3021">Yes</span></span> |
| <span data-ttu-id="e44c9-3022">className</span><span class="sxs-lookup"><span data-stu-id="e44c9-3022">className</span></span> | <span data-ttu-id="e44c9-3023">응용 프로그램의 Java/Spark main 클래스</span><span class="sxs-lookup"><span data-stu-id="e44c9-3023">Application's Java/Spark main class</span></span> | <span data-ttu-id="e44c9-3024">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3024">No</span></span> | 
| <span data-ttu-id="e44c9-3025">arguments</span><span class="sxs-lookup"><span data-stu-id="e44c9-3025">arguments</span></span> | <span data-ttu-id="e44c9-3026">명령줄 인수 toohello Spark 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3026">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="e44c9-3027">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3027">No</span></span> | 
| <span data-ttu-id="e44c9-3028">proxyUser</span><span class="sxs-lookup"><span data-stu-id="e44c9-3028">proxyUser</span></span> | <span data-ttu-id="e44c9-3029">hello 사용자 계정 tooimpersonate tooexecute hello Spark 프로그램</span><span class="sxs-lookup"><span data-stu-id="e44c9-3029">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="e44c9-3030">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3030">No</span></span> | 
| <span data-ttu-id="e44c9-3031">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="e44c9-3031">sparkConfig</span></span> | <span data-ttu-id="e44c9-3032">Spark 구성 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3032">Spark configuration properties.</span></span> | <span data-ttu-id="e44c9-3033">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3033">No</span></span> | 
| <span data-ttu-id="e44c9-3034">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="e44c9-3034">getDebugInfo</span></span> | <span data-ttu-id="e44c9-3035">Hello Spark 로그 파일에서 복사한 toohello HDInsight 클러스터에서 사용 하는 Azure 저장소를가 하는 경우를 지정 합니다 (또는) sparkJobLinkedService 하 여 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3035">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="e44c9-3036">허용되는 값: None, Always 또는 Failure.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3036">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="e44c9-3037">기본값: None.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3037">Default value: None.</span></span> | <span data-ttu-id="e44c9-3038">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3038">No</span></span> | 
| <span data-ttu-id="e44c9-3039">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="e44c9-3039">sparkJobLinkedService</span></span> | <span data-ttu-id="e44c9-3040">hello hello Spark 작업 파일, 종속성 및 로그를 보유 하는 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3040">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="e44c9-3041">이 속성에 대 한 값을 지정 하지 않으면 HDInsight 클러스터와 연결 된 hello 저장소 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3041">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="e44c9-3042">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3042">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="e44c9-3043">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3043">JSON example</span></span>

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
<span data-ttu-id="e44c9-3044">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3044">Note hello following points:</span></span> 

- <span data-ttu-id="e44c9-3045">hello **형식** 너무 속성이**HDInsightSpark**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3045">hello **type** property is set too**HDInsightSpark**.</span></span>
- <span data-ttu-id="e44c9-3046">hello **rootPath** 너무 설정**adfspark\\pyFiles** adfspark 란 pyFiles 고 hello Azure Blob 컨테이너는 세밀 하 게 폴더 해당 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3046">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="e44c9-3047">이 예제에서는 hello Azure Blob 저장소는 hello 즉 hello Spark 클러스터와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3047">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="e44c9-3048">Hello 파일 tooa 업로드할 수 있습니다 다른 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3048">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="e44c9-3049">이렇게 하면 Azure 저장소 연결 서비스 toolink 해당 저장소 계정 toohello 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3049">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="e44c9-3050">그런 다음 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **sparkJobLinkedService** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3050">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="e44c9-3051">참조 [Spark 활동 속성](#spark-activity-properties) hello Spark 활동에서 지 원하는 다른 속성 및이 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3051">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>
- <span data-ttu-id="e44c9-3052">hello **entryFilePath** toohello 설정 **test.py**, hello python 파일인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3052">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span> 
- <span data-ttu-id="e44c9-3053">hello **getDebugInfo** 너무 속성이**항상**, (성공 또는 실패) 생성 된 hello 로그 파일은 항상 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3053">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>  

    > [!IMPORTANT]
    > <span data-ttu-id="e44c9-3054">설정 하지 않으면이 속성 tooAlways 프로덕션 환경에서 문제를 해결 하는 경우가 아니면 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3054">We recommend that you do not set this property tooAlways in a production environment unless you are troubleshooting an issue.</span></span> 
- <span data-ttu-id="e44c9-3055">hello **출력** 섹션에는 하나의 출력 데이터 집합에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3055">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="e44c9-3056">Hello spark 프로그램 출력을 생성 하지 않는 경우에 출력 데이터 집합을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3056">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="e44c9-3057">hello 출력 데이터 집합 드라이브 hello에 대 한 일정 hello 파이프라인 (시간별, 일별, 등).</span><span class="sxs-lookup"><span data-stu-id="e44c9-3057">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>

<span data-ttu-id="e44c9-3058">Hello 활동에 대 한 자세한 내용은 참조 [Spark 활동](data-factory-spark.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3058">For more information about hello activity, see [Spark Activity](data-factory-spark.md) article.</span></span>  

## <a name="machine-learning-batch-execution-activity"></a><span data-ttu-id="e44c9-3059">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-3059">Machine Learning Batch Execution Activity</span></span>
<span data-ttu-id="e44c9-3060">Hello 다음과 같은 Azure ML 일괄 처리 실행 활동 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3060">You can specify hello following properties in a Azure ML Batch Execution Activity JSON definition.</span></span> <span data-ttu-id="e44c9-3061">hello 활동에 대 한 hello type 속성 이어야 합니다: **AzureMLBatchExecution**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3061">hello type property for hello activity must be: **AzureMLBatchExecution**.</span></span> <span data-ttu-id="e44c9-3062">Azure 기계 학습 연결 된 서비스를 먼저 만들고 것의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3062">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-3063">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooAzureMLBatchExecution 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3063">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLBatchExecution:</span></span>

<span data-ttu-id="e44c9-3064">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3064">Property</span></span> | <span data-ttu-id="e44c9-3065">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3065">Description</span></span> | <span data-ttu-id="e44c9-3066">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3066">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="e44c9-3067">webServiceInput</span><span class="sxs-lookup"><span data-stu-id="e44c9-3067">webServiceInput</span></span> | <span data-ttu-id="e44c9-3068">데이터 집합 toobe hello hello Azure ML 웹 서비스에 대 한 입력으로 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3068">hello dataset toobe passed as an input for hello Azure ML web service.</span></span> <span data-ttu-id="e44c9-3069">이 데이터 집합 hello 활동에 대 한 hello 입력에 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3069">This dataset must also be included in hello inputs for hello activity.</span></span> |<span data-ttu-id="e44c9-3070">webServiceInput 또는 webServiceInputs를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3070">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="e44c9-3071">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="e44c9-3071">webServiceInputs</span></span> | <span data-ttu-id="e44c9-3072">Hello Azure ML 웹 서비스에 대 한 입력으로 전달 되는 데이터 집합 toobe를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3072">Specify datasets toobe passed as inputs for hello Azure ML web service.</span></span> <span data-ttu-id="e44c9-3073">Hello 웹 서비스는 여러 개의 입력을 hello webServiceInput 속성을 사용 하는 대신 hello webServiceInputs 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3073">If hello web service takes multiple inputs, use hello webServiceInputs property instead of using hello webServiceInput property.</span></span> <span data-ttu-id="e44c9-3074">Hello에서 참조 되는 데이터 집합 **webServiceInputs** hello 활동에에서도 포함 해야 **입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3074">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span> | <span data-ttu-id="e44c9-3075">webServiceInput 또는 webServiceInputs를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3075">Use either webServiceInput or webServiceInputs.</span></span> | 
<span data-ttu-id="e44c9-3076">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="e44c9-3076">webServiceOutputs</span></span> | <span data-ttu-id="e44c9-3077">hello Azure ML 웹 서비스에 대 한 출력으로 할당 된 hello 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3077">hello datasets that are assigned as outputs for hello Azure ML web service.</span></span> <span data-ttu-id="e44c9-3078">hello 웹 서비스는이 데이터 집합에 출력 데이터를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3078">hello web service returns output data in this dataset.</span></span> | <span data-ttu-id="e44c9-3079">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3079">Yes</span></span> | 
<span data-ttu-id="e44c9-3080">globalParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-3080">globalParameters</span></span> | <span data-ttu-id="e44c9-3081">이 섹션의 웹 서비스 매개 변수가 hello에 대 한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3081">Specify values for hello web service parameters in this section.</span></span> | <span data-ttu-id="e44c9-3082">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3082">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="e44c9-3083">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3083">JSON example</span></span>
<span data-ttu-id="e44c9-3084">이 예제에서는 hello 활동에 데이터 집합이 두 hello **MLSqlInput** 입력으로 및 **MLSqlOutput** hello 출력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3084">In this example, hello activity has hello dataset **MLSqlInput** as input and **MLSqlOutput** as hello output.</span></span> <span data-ttu-id="e44c9-3085">hello **MLSqlInput** hello를 사용 하 여 입력된 toohello 웹 서비스로 전달 되 **webServiceInput** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3085">hello **MLSqlInput** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="e44c9-3086">hello **MLSqlOutput** hello를 사용 하 여 출력 toohello 웹 서비스로 전달 되 **webServiceOutputs** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3086">hello **MLSqlOutput** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span> 

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

<span data-ttu-id="e44c9-3087">Hello Azure 컴퓨터 학습 웹 서비스에는 판독기와 기록기 모듈 tooread/쓰기 데이터를 사용 하 여 배포 된 hello JSON 예에서 / tooan Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3087">In hello JSON example, hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="e44c9-3088">이 웹 서비스는 hello 다음 4 개의 매개 변수가 노출: 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3088">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>

> [!NOTE]
> <span data-ttu-id="e44c9-3089">유일한 입 / 출력 hello AzureMLBatchExecution 활동의 매개 변수 toohello 웹 서비스 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3089">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="e44c9-3090">예를 들어 JSON 코드 조각은 위에 hello, MLSqlInput은 입력된 toohello webServiceInput 매개 변수를 통해 웹 서비스는 입력된 toohello 변수로 전달 되는 AzureMLBatchExecution 활동에는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3090">For example, in hello above JSON snippet, MLSqlInput is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>

## <a name="machine-learning-update-resource-activity"></a><span data-ttu-id="e44c9-3091">Machine Learning 업데이트 리소스 활동</span><span class="sxs-lookup"><span data-stu-id="e44c9-3091">Machine Learning Update Resource Activity</span></span>
<span data-ttu-id="e44c9-3092">Hello 다음과 같은 Azure ML 업데이트 리소스 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3092">You can specify hello following properties in a Azure ML Update Resource Activity JSON definition.</span></span> <span data-ttu-id="e44c9-3093">hello 활동에 대 한 hello type 속성 이어야 합니다: **AzureMLUpdateResource**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3093">hello type property for hello activity must be: **AzureMLUpdateResource**.</span></span> <span data-ttu-id="e44c9-3094">Azure 기계 학습 연결 된 서비스를 먼저 만들고 것의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3094">You must create a Azure Machine Learning linked service first and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-3095">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooAzureMLUpdateResource 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3095">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooAzureMLUpdateResource:</span></span>

<span data-ttu-id="e44c9-3096">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3096">Property</span></span> | <span data-ttu-id="e44c9-3097">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3097">Description</span></span> | <span data-ttu-id="e44c9-3098">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3098">Required</span></span> 
-------- | ----------- | --------
<span data-ttu-id="e44c9-3099">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="e44c9-3099">trainedModelName</span></span> | <span data-ttu-id="e44c9-3100">모델을 유지 하는 hello의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3100">Name of hello retrained model.</span></span> | <span data-ttu-id="e44c9-3101">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3101">Yes</span></span> |  
<span data-ttu-id="e44c9-3102">trainedModelDatasetName</span><span class="sxs-lookup"><span data-stu-id="e44c9-3102">trainedModelDatasetName</span></span> | <span data-ttu-id="e44c9-3103">Hello 재교육 작업에서 반환 된 포인팅 toohello iLearner 파일을 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3103">Dataset pointing toohello iLearner file returned by hello retraining operation.</span></span> | <span data-ttu-id="e44c9-3104">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3104">Yes</span></span> | 

### <a name="json-example"></a><span data-ttu-id="e44c9-3105">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3105">JSON example</span></span>
<span data-ttu-id="e44c9-3106">hello 파이프라인에는 두 개의 활동: **AzureMLBatchExecution** 및 **AzureMLUpdateResource**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3106">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="e44c9-3107">hello Azure ML 일괄 처리 실행 작업 hello 학습 데이터를 입력으로 사용 하 고 출력으로 iLearner 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3107">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="e44c9-3108">hello 활동 데이터를 학습 하는 hello 입력이 포함 된 hello 학습 웹 서비스 (학습 실험을 웹 서비스로 노출)을 호출 하 고 hello 웹 서비스에서 hello ilearner 파일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3108">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="e44c9-3109">hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3109">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>


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

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="e44c9-3110">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-3110">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="e44c9-3111">Hello 다음과 같은 U-SQL 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3111">You can specify hello following properties in a U-SQL Activity JSON definition.</span></span> <span data-ttu-id="e44c9-3112">hello 활동에 대 한 hello type 속성 이어야 합니다: **DataLakeAnalyticsU SQL**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3112">hello type property for hello activity must be: **DataLakeAnalyticsU-SQL**.</span></span> <span data-ttu-id="e44c9-3113">연결 된 Azure Data Lake 분석 서비스를 만들고 그의 hello 이름을 hello에 대 한 값으로 지정 해야 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3113">You must create an Azure Data Lake Analytics linked service and specify hello name of it as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-3114">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooDataLakeAnalyticsU SQL 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3114">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDataLakeAnalyticsU-SQL:</span></span> 

| <span data-ttu-id="e44c9-3115">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3115">Property</span></span> | <span data-ttu-id="e44c9-3116">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3116">Description</span></span> | <span data-ttu-id="e44c9-3117">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3117">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-3118">scriptPath</span><span class="sxs-lookup"><span data-stu-id="e44c9-3118">scriptPath</span></span> |<span data-ttu-id="e44c9-3119">Hello U-SQL 스크립트를 포함 하는 경로 toofolder 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3119">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="e44c9-3120">Hello 파일의 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3120">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="e44c9-3121">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-3121">No (if you use script)</span></span> |
| <span data-ttu-id="e44c9-3122">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="e44c9-3122">scriptLinkedService</span></span> |<span data-ttu-id="e44c9-3123">Hello 스크립트 toohello 데이터 팩터리를 포함 하는 hello 저장소를 연결 하는 연결 된 서비스</span><span class="sxs-lookup"><span data-stu-id="e44c9-3123">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="e44c9-3124">아니요(스크립트를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-3124">No (if you use script)</span></span> |
| <span data-ttu-id="e44c9-3125">script</span><span class="sxs-lookup"><span data-stu-id="e44c9-3125">script</span></span> |<span data-ttu-id="e44c9-3126">scriptPath 및 scriptLinkedService를 지정하는 대신 인라인 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3126">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="e44c9-3127">예: "script" : "CREATE DATABASE test"</span><span class="sxs-lookup"><span data-stu-id="e44c9-3127">For example: "script": "CREATE DATABASE test".</span></span> |<span data-ttu-id="e44c9-3128">아니요(scriptPath 및 scriptLinkedService를 사용하는 경우)</span><span class="sxs-lookup"><span data-stu-id="e44c9-3128">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="e44c9-3129">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="e44c9-3129">degreeOfParallelism</span></span> |<span data-ttu-id="e44c9-3130">hello 최대 노드 수는 동시에 toorun hello 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3130">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="e44c9-3131">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3131">No</span></span> |
| <span data-ttu-id="e44c9-3132">우선 순위</span><span class="sxs-lookup"><span data-stu-id="e44c9-3132">priority</span></span> |<span data-ttu-id="e44c9-3133">먼저 어떤 작업에서 대기 중인 모든 선택한 toorun 해야를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3133">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="e44c9-3134">hello 낮은 hello 수치로 hello hello 우선 순위가 높습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3134">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="e44c9-3135">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3135">No</span></span> |
| <span data-ttu-id="e44c9-3136">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3136">parameters</span></span> |<span data-ttu-id="e44c9-3137">Hello U-SQL 스크립트의 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3137">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="e44c9-3138">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3138">No</span></span> |

### <a name="json-example"></a><span data-ttu-id="e44c9-3139">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3139">JSON example</span></span>

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

<span data-ttu-id="e44c9-3140">자세한 내용은 [Data Lake Analytics U-SQL 활동](data-factory-usql-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3140">For more information, see [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md).</span></span> 

## <a name="stored-procedure-activity"></a><span data-ttu-id="e44c9-3141">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-3141">Stored Procedure Activity</span></span>
<span data-ttu-id="e44c9-3142">Hello 다음과 같은 저장 프로시저 작업 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3142">You can specify hello following properties in a Stored Procedure Activity JSON definition.</span></span> <span data-ttu-id="e44c9-3143">hello 활동에 대 한 hello type 속성 이어야 합니다: **SqlServerStoredProcedure**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3143">hello type property for hello activity must be: **SqlServerStoredProcedure**.</span></span> <span data-ttu-id="e44c9-3144">Hello 연결 된 서비스를 다음 중 하나는 만들고 해야 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **linkedServiceName** 속성:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3144">You must create an one of hello following linked services and specify hello name of hello linked service as a value for hello **linkedServiceName** property:</span></span>

- <span data-ttu-id="e44c9-3145">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e44c9-3145">SQL Server</span></span> 
- <span data-ttu-id="e44c9-3146">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e44c9-3146">Azure SQL Database</span></span>
- <span data-ttu-id="e44c9-3147">Azure SQL 데이터 웨어하우스</span><span class="sxs-lookup"><span data-stu-id="e44c9-3147">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="e44c9-3148">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooSqlServerStoredProcedure 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3148">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooSqlServerStoredProcedure:</span></span>

| <span data-ttu-id="e44c9-3149">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3149">Property</span></span> | <span data-ttu-id="e44c9-3150">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3150">Description</span></span> | <span data-ttu-id="e44c9-3151">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3151">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e44c9-3152">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="e44c9-3152">storedProcedureName</span></span> |<span data-ttu-id="e44c9-3153">Hello Azure SQL 데이터베이스 또는 출력 테이블 사용 hello hello 연결 된 서비스에 의해 표시 되는 Azure SQL 데이터 웨어하우스 hello 저장 프로시저의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3153">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="e44c9-3154">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3154">Yes</span></span> |
| <span data-ttu-id="e44c9-3155">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="e44c9-3155">storedProcedureParameters</span></span> |<span data-ttu-id="e44c9-3156">저장 프로시저 매개 변수의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3156">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="e44c9-3157">매개 변수에 대해 toopass을 null 필요 hello 구문 사용: "param1": null (모든 소문자).</span><span class="sxs-lookup"><span data-stu-id="e44c9-3157">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="e44c9-3158">이 속성을 사용 하는 방법에 대 한 샘플 toolearn 다음 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3158">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="e44c9-3159">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3159">No</span></span> |

<span data-ttu-id="e44c9-3160">입력된 데이터 집합을 지정 않습니다 ('준비' 상태)에서 사용할 수 있어야 hello에 대 한 저장 프로시저 활동 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3160">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="e44c9-3161">hello 입력된 데이터 집합 매개 변수로 hello 저장 프로시저에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3161">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="e44c9-3162">시작 hello 저장 프로시저 작업 전에 것만 사용 되는 toocheck hello 종속성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3162">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> <span data-ttu-id="e44c9-3163">저장 프로시저 작업에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3163">You must specify an output dataset for a stored procedure activity.</span></span> 

<span data-ttu-id="e44c9-3164">출력 데이터 집합 지정 hello **일정** hello에 대 한 저장 프로시저 작업 (시간별, 매주, 매월, 등).</span><span class="sxs-lookup"><span data-stu-id="e44c9-3164">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <span data-ttu-id="e44c9-3165">hello 출력 데이터 집합 사용 해야 합니다는 **연결 된 서비스** tooan Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 또는 저장된 프로시저 toorun hello 하려는 SQL Server 데이터베이스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3165">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="e44c9-3166">hello 출력 데이터 집합으로 사용할 수는 방식으로 toopass hello 결과 후속 처리에 대 한 hello 저장 프로시저의 다른 활동에 의해 ([활동 체인](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) hello 파이프라인에서.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3166">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) in hello pipeline.</span></span> <span data-ttu-id="e44c9-3167">그러나 데이터 팩터리는 저장된 프로시저 toothis 데이터 집합의 hello 출력을 자동으로 기록 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3167">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="e44c9-3168">Hello 저장 프로시저 출력 데이터 집합 가리키는 hello 해당 쓰기 tooa SQL 테이블 이며</span><span class="sxs-lookup"><span data-stu-id="e44c9-3168">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="e44c9-3169">경우에 따라 hello 출력 데이터 집합 수는 **더미 데이터 집합**, hello를 실행 하기 위한 toospecify hello 일정 저장 프로시저 작업에만 사용 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3169">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span>  

### <a name="json-example"></a><span data-ttu-id="e44c9-3170">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3170">JSON example</span></span>

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

<span data-ttu-id="e44c9-3171">자세한 내용은 [저장 프로시저 활동](data-factory-stored-proc-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3171">For more information, see [Stored Procedure Activity](data-factory-stored-proc-activity.md) article.</span></span> 

## <a name="net-custom-activity"></a><span data-ttu-id="e44c9-3172">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="e44c9-3172">.NET custom activity</span></span>
<span data-ttu-id="e44c9-3173">Hello 다음과 같은.NET 사용자 지정 활동 JSON 정의에서 속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3173">You can specify hello following properties in a .NET custom activity JSON definition.</span></span> <span data-ttu-id="e44c9-3174">hello 활동에 대 한 hello type 속성 이어야 합니다: **DotNetActivity**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3174">hello type property for hello activity must be: **DotNetActivity**.</span></span> <span data-ttu-id="e44c9-3175">Azure HDInsight 연결 된 서비스를 만들어야 합니다 또는 Azure 배치 연결 된 서비스를 마우스 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **linkedServiceName** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3175">You must create an Azure HDInsight linked service or an Azure Batch linked service, and specify hello name of hello linked service as a value for hello **linkedServiceName** property.</span></span> <span data-ttu-id="e44c9-3176">hello 다음 속성은 지원 hello **typeProperties** hello 유형의 활동 tooDotNetActivity 설정 섹션:</span><span class="sxs-lookup"><span data-stu-id="e44c9-3176">hello following properties are supported in hello **typeProperties** section when you set hello type of activity tooDotNetActivity:</span></span>
 
| <span data-ttu-id="e44c9-3177">속성</span><span class="sxs-lookup"><span data-stu-id="e44c9-3177">Property</span></span> | <span data-ttu-id="e44c9-3178">설명</span><span class="sxs-lookup"><span data-stu-id="e44c9-3178">Description</span></span> | <span data-ttu-id="e44c9-3179">필수</span><span class="sxs-lookup"><span data-stu-id="e44c9-3179">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e44c9-3180">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="e44c9-3180">AssemblyName</span></span> | <span data-ttu-id="e44c9-3181">Hello 어셈블리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3181">Name of hello assembly.</span></span> <span data-ttu-id="e44c9-3182">Hello 예제: **MyDotnetActivity.dll**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3182">In hello example, it is: **MyDotnetActivity.dll**.</span></span> | <span data-ttu-id="e44c9-3183">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3183">Yes</span></span> |
| <span data-ttu-id="e44c9-3184">EntryPoint</span><span class="sxs-lookup"><span data-stu-id="e44c9-3184">EntryPoint</span></span> |<span data-ttu-id="e44c9-3185">Hello IDotNetActivity 인터페이스를 구현 하는 hello 클래스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3185">Name of hello class that implements hello IDotNetActivity interface.</span></span> <span data-ttu-id="e44c9-3186">Hello 예제: **MyDotNetActivityNS.MyDotNetActivity** 여기서 MyDotNetActivityNS hello 네임 스페이스 이므로 MyDotNetActivity hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3186">In hello example, it is: **MyDotNetActivityNS.MyDotNetActivity** where MyDotNetActivityNS is hello namespace and MyDotNetActivity is hello class.</span></span>  | <span data-ttu-id="e44c9-3187">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3187">Yes</span></span> | 
| <span data-ttu-id="e44c9-3188">PackageLinkedService</span><span class="sxs-lookup"><span data-stu-id="e44c9-3188">PackageLinkedService</span></span> | <span data-ttu-id="e44c9-3189">Hello hello 사용자 지정 활동 zip 파일이 포함 된 toohello blob 저장소를 가리키는 Azure 저장소 연결 된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3189">Name of hello Azure Storage linked service that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="e44c9-3190">Hello 예제: **AzureStorageLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3190">In hello example, it is: **AzureStorageLinkedService**.</span></span>| <span data-ttu-id="e44c9-3191">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3191">Yes</span></span> |
| <span data-ttu-id="e44c9-3192">PackageFile</span><span class="sxs-lookup"><span data-stu-id="e44c9-3192">PackageFile</span></span> | <span data-ttu-id="e44c9-3193">Hello zip 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3193">Name of hello zip file.</span></span> <span data-ttu-id="e44c9-3194">Hello 예제: **customactivitycontainer/MyDotNetActivity.zip**합니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3194">In hello example, it is: **customactivitycontainer/MyDotNetActivity.zip**.</span></span> | <span data-ttu-id="e44c9-3195">예</span><span class="sxs-lookup"><span data-stu-id="e44c9-3195">Yes</span></span> |
| <span data-ttu-id="e44c9-3196">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="e44c9-3196">extendedProperties</span></span> | <span data-ttu-id="e44c9-3197">정의 하 고 toohello.NET 코드에 전달할 수 있는 확장 된 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3197">Extended properties that you can define and pass on toohello .NET code.</span></span> <span data-ttu-id="e44c9-3198">이 예제에서는 hello **SliceStart** 변수 tooa 값 hello SliceStart 시스템 변수를 기반으로 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3198">In this example, hello **SliceStart** variable is set tooa value based on hello SliceStart system variable.</span></span> | <span data-ttu-id="e44c9-3199">아니요</span><span class="sxs-lookup"><span data-stu-id="e44c9-3199">No</span></span> | 

### <a name="json-example"></a><span data-ttu-id="e44c9-3200">JSON 예제</span><span class="sxs-lookup"><span data-stu-id="e44c9-3200">JSON example</span></span>

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

<span data-ttu-id="e44c9-3201">자세한 내용은 [Data Factory에서 사용자 지정 활동 사용](data-factory-use-custom-activities.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3201">For detailed information, see [Use custom activities in Data Factory](data-factory-use-custom-activities.md) article.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e44c9-3202">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e44c9-3202">Next Steps</span></span>
<span data-ttu-id="e44c9-3203">자습서를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e44c9-3203">See hello following tutorials:</span></span> 

- [<span data-ttu-id="e44c9-3204">자습서: 복사 활동이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="e44c9-3204">Tutorial: create a pipeline with a copy activity</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [<span data-ttu-id="e44c9-3205">자습서: Hive 활동이 있는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="e44c9-3205">Tutorial: create a pipeline with a hive activity</span></span>](data-factory-build-your-first-pipeline-using-editor.md)