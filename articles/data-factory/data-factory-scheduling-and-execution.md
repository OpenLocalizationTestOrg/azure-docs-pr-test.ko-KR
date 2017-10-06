---
title: "aaaScheduling 및 데이터 팩터리를 사용 하 여 실행 | Microsoft Docs"
description: "Azure Data Factory 응용 프로그램 모델의 예약 및 실행에 대한 내용을 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="300f6-103">Data Factory 예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="300f6-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="300f6-104">이 문서는 hello Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-104">This article explains hello scheduling and execution aspects of hello Azure Data Factory application model.</span></span> <span data-ttu-id="300f6-105">이 문서는 사용자가 작업, 파이프라인, 연결된 서비스 및 데이터 집합과 같은 Data Factory 응용 프로그램 모델 개념을 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="300f6-106">Azure Data Factory의 기본 개념에 대 한 참조 문서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="300f6-106">For basic concepts of Azure Data Factory, see hello following articles:</span></span>

* [<span data-ttu-id="300f6-107">소개 tooData 팩터리</span><span class="sxs-lookup"><span data-stu-id="300f6-107">Introduction tooData Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="300f6-108">파이프라인</span><span class="sxs-lookup"><span data-stu-id="300f6-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="300f6-109">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="300f6-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="300f6-110">파이프라인의 시작 및 종료 시간</span><span class="sxs-lookup"><span data-stu-id="300f6-110">Start and end times of pipeline</span></span>
<span data-ttu-id="300f6-111">파이프라인은 **시작** 시간과 **종료** 시간 사이에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="300f6-112">Hello 시작 시간 이전 또는 hello 종료 시간 이후에 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-112">It is not executed before hello start time or after hello end time.</span></span> <span data-ttu-id="300f6-113">Hello 파이프라인이 일시 중지, 시작 및 종료 시간에 관계 없이 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-113">If hello pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="300f6-114">파이프라인 toorun에 대 한 것 해야 일시 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-114">For a pipeline toorun, it should not be paused.</span></span> <span data-ttu-id="300f6-115">Hello 파이프라인 정의에서 이러한 설정을 (시작, 종료, 일시 중지)을 찾을:</span><span class="sxs-lookup"><span data-stu-id="300f6-115">You find these settings (start, end, paused) in hello pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="300f6-116">이러한 속성에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="300f6-117">활동 일정 지정</span><span class="sxs-lookup"><span data-stu-id="300f6-117">Specify schedule for an activity</span></span>
<span data-ttu-id="300f6-118">Hello 파이프라인 실행 되는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-118">It is not hello pipeline that is executed.</span></span> <span data-ttu-id="300f6-119">Hello에 실행 되는 hello 파이프라인의 hello 작업은 hello 파이프라인의 전체적인 맥락 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-119">It is hello activities in hello pipeline that are executed in hello overall context of hello pipeline.</span></span> <span data-ttu-id="300f6-120">Hello를 사용 하 여 활동에 대 한 되풀이 일정을 지정할 수 있습니다 **스케줄러** 활동 JSON의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-120">You can specify a recurring schedule for an activity by using hello **scheduler** section of activity JSON.</span></span> <span data-ttu-id="300f6-121">예를 들어 예약할 수 있습니다 활동 toorun 매시간 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-121">For example, you can schedule an activity toorun hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="300f6-122">Hello 다음 다이어그램에에서 나와 있는 것 처럼 활동에 대 한 일정 계열을 사용 하 여 연속 창의 hello 지정 파이프라인 시작 시간 및 종료.</span><span class="sxs-lookup"><span data-stu-id="300f6-122">As shown in hello following diagram, specifying a schedule for an activity creates a series of tumbling windows with in hello pipeline start and end times.</span></span> <span data-ttu-id="300f6-123">연속 창은 일련의 고정된 크기의 겹치지 않는 연속적인 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="300f6-124">활동에 대한 이러한 논리적 연속 창을 **활동 기간**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![활동 스케줄러 예제](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="300f6-126">hello **스케줄러** 활동에 대 한 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-126">hello **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="300f6-127">이 속성을 지정 하면 경우 hello 활동에 대 한 출력 데이터 집합의 hello 정의에서 지정 하는 hello 흐름을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-127">If you do specify this property, it must match hello cadence you specify in hello definition of output dataset for hello activity.</span></span> <span data-ttu-id="300f6-128">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-128">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="300f6-129">따라서 만들어야 출력 데이터 집합의 관계를 hello 활동 출력을 생성 하지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-129">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="300f6-130">데이터 집합 일정 지정</span><span class="sxs-lookup"><span data-stu-id="300f6-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="300f6-131">Data Factory 파이프라인의 활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="300f6-132">활동에 대 한 입력된 데이터를 사용할 수 있는 hello에 hello 흐름을 지정할 수 있습니다 또는 hello를 사용 하 여 hello 출력 데이터 생성 **가용성** hello 데이터 집합 정의에 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-132">For an activity, you can specify hello cadence at which hello input data is available or hello output data is produced by using hello **availability** section in hello dataset definitions.</span></span> 

<span data-ttu-id="300f6-133">**빈도** hello에 **가용성** 섹션 hello 시간 단위를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-133">**Frequency** in hello **availability** section specifies hello time unit.</span></span> <span data-ttu-id="300f6-134">hello 빈도 대 한 값은 허용: 분, 시간, 일, 주 및 월.</span><span class="sxs-lookup"><span data-stu-id="300f6-134">hello allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="300f6-135">hello **간격** hello 가용성 섹션에서 속성 빈도의 승수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-135">hello **interval** property in hello availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="300f6-136">예를 들어: hello 출력 데이터가 매일 생성 hello 주기 tooDay 설정 하는 경우 출력 데이터 집합에 대 한 too1 간격을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-136">For example: if hello frequency is set tooDay and interval is set too1 for an output dataset, hello output data is produced daily.</span></span> <span data-ttu-id="300f6-137">분으로 hello 빈도 지정 하는 경우에 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-137">If you specify hello frequency as minute, we recommend that you set hello interval toono less than 15.</span></span> 

<span data-ttu-id="300f6-138">다음 예제는 hello에서 hello 입력된 데이터를 사용할 수 매시간 hello 출력 데이터가 매시간 생성 됩니다 (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="300f6-138">In hello following example, hello input data is available hourly and hello output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="300f6-139">**입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="300f6-139">**Input dataset:**</span></span> 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


<span data-ttu-id="300f6-140">**출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="300f6-140">**Output dataset**</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="300f6-141">현재 **출력 데이터 집합 드라이브 hello 일정**합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-141">Currently, **output dataset drives hello schedule**.</span></span> <span data-ttu-id="300f6-142">즉, hello 출력 데이터 집합에 대해 지정 된 hello 일정은 런타임에 작업에서 사용 되는 toorun 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-142">In other words, hello schedule specified for hello output dataset is used toorun an activity at runtime.</span></span> <span data-ttu-id="300f6-143">따라서 만들어야 출력 데이터 집합의 관계를 hello 활동 출력을 생성 하지 않는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-143">Therefore, you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="300f6-144">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-144">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 

<span data-ttu-id="300f6-145">다음 예제 hello 파이프라인 정의 hello **스케줄러** 속성은 hello 활동에 대 한 사용 되는 toospecify 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-145">In hello following pipeline definition, hello **scheduler** property is used toospecify schedule for hello activity.</span></span> <span data-ttu-id="300f6-146">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-146">This property is optional.</span></span> <span data-ttu-id="300f6-147">현재 hello 활동에 대 한 hello 일정 hello 일정 hello 출력 데이터 집합에 대해 지정 된 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-147">Currently, hello schedule for hello activity must match hello schedule specified for hello output dataset.</span></span>
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

<span data-ttu-id="300f6-148">이 예제에서는 hello 활동을 1 시간 마다 실행 hello 사이의 시작 시간 및 종료 hello 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="300f6-148">In this example, hello activity runs hourly between hello start and end times of hello pipeline.</span></span> <span data-ttu-id="300f6-149">hello 출력 데이터는 3 개의 시간 창 (8-9 오전, 오전 9 시에서 오전 10, 및 10-11 오전)에 대 한 매시간 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-149">hello output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="300f6-150">활동 실행에서 사용하거나 생성한 데이터의 각 단위를 **데이터 조각**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="300f6-151">다이어그램을 다음 hello 하나의 입력 데이터 집합과 하나의 출력 데이터 집합 작업의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-151">hello following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![가용성 스케줄러](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="300f6-153">hello 다이어그램 hello에 대 한 데이터 조각이 입력 및 출력 데이터 집합 1 시간 마다 hello를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-153">hello diagram shows hello hourly data slices for hello input and output dataset.</span></span> <span data-ttu-id="300f6-154">hello 다이어그램에는 처리를 위해 준비 하는 세 가지 입력된 조각을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-154">hello diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="300f6-155">hello 10-11 오전 활동 hello 10-11 오전 출력 조각을 생성 하는 진행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-155">hello 10-11 AM activity is in progress, producing hello 10-11 AM output slice.</span></span> 

<span data-ttu-id="300f6-156">변수를 사용 하 여 hello 데이터 집합 JSON의에서 현재 조각 hello와 관련 된 hello 시간 간격에 액세스할 수 있습니다: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) 및 [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables)합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-156">You can access hello time interval associated with hello current slice in hello dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="300f6-157">마찬가지로, WindowStart hello 및 WindowEnd를 사용 하 여 연결 된 활동 hello 시간 간격을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-157">Similarly, you can access hello time interval associated with an activity window by using hello WindowStart and WindowEnd.</span></span> <span data-ttu-id="300f6-158">활동의 hello 일정 hello 활동에 대 한 hello 출력 데이터 집합의 일정을 hello 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-158">hello schedule of an activity must match hello schedule of hello output dataset for hello activity.</span></span> <span data-ttu-id="300f6-159">따라서 SliceStart hello 및 SliceEnd 값은 hello 동일 WindowStart WindowEnd 값으로 각각.</span><span class="sxs-lookup"><span data-stu-id="300f6-159">Therefore, hello SliceStart and SliceEnd values are hello same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="300f6-160">이러한 변수에 대한 자세한 내용은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md#data-factory-system-variables) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="300f6-161">이러한 변수를 작업 JSON에서 다양한 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="300f6-162">예를 들어 데이터 사용할 수 있습니다 이러한 tooselect 시계열 데이터를 나타내는 입력 및 출력 데이터 집합에서 (예: 8 AM too9 AM).</span><span class="sxs-lookup"><span data-stu-id="300f6-162">For example, you can use them tooselect data from input and output datasets representing time series data (for example: 8 AM too9 AM).</span></span> <span data-ttu-id="300f6-163">또한이 예제에서는 **WindowStart** 및 **WindowEnd** tooselect 관련 데이터를 활동에 대해 실행 하 고 적절 한 hello로 tooa blob 복사 **folderPath**합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-163">This example also uses **WindowStart** and **WindowEnd** tooselect relevant data for an activity run and copy it tooa blob with hello appropriate **folderPath**.</span></span> <span data-ttu-id="300f6-164">hello **folderPath** 매시간에 대 한 매개 변수가 있는 toohave 별도 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-164">hello **folderPath** is parameterized toohave a separate folder for every hour.</span></span>  

<span data-ttu-id="300f6-165">앞 예제는 hello, 입력 및 출력 데이터 집합에 대해 지정 된 hello 일정이 동일 (매시간) hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-165">In hello preceding example, hello schedule specified for input and output datasets is hello same (hourly).</span></span> <span data-ttu-id="300f6-166">Hello hello 활동에 대 한 입력된 데이터 집합을 사용할 수 경우 다른 빈도로 예: 15 분 마다 hello 출력 데이터 집합은 어떤 드라이브 hello 활동 일정으로이 출력 데이터 집합을 생성 하는 hello 활동이 계속 한 시간에 한 번 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-166">If hello input dataset for hello activity is available at a different frequency, say every 15 minutes, hello activity that produces this output dataset still runs once an hour as hello output dataset is what drives hello activity schedule.</span></span> <span data-ttu-id="300f6-167">자세한 내용은 [다양한 빈도로 데이터 집합 모델링](#model-datasets-with-different-frequencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="300f6-168">데이터 집합 가용성 및 정책</span><span class="sxs-lookup"><span data-stu-id="300f6-168">Dataset availability and policies</span></span>
<span data-ttu-id="300f6-169">데이터 집합 정의의 hello 가용성 섹션의 빈도 및 간격이 속성의 hello 사용에 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-169">You have seen hello usage of frequency and interval properties in hello availability section of dataset definition.</span></span> <span data-ttu-id="300f6-170">hello 예약 및 실행 작업에 영향을 주는 다른 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-170">There are a few other properties that affect hello scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="300f6-171">데이터 집합 가용성</span><span class="sxs-lookup"><span data-stu-id="300f6-171">Dataset availability</span></span> 
<span data-ttu-id="300f6-172">hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **가용성** 섹션:</span><span class="sxs-lookup"><span data-stu-id="300f6-172">hello following table describes properties you can use in hello **availability** section:</span></span>

| <span data-ttu-id="300f6-173">속성</span><span class="sxs-lookup"><span data-stu-id="300f6-173">Property</span></span> | <span data-ttu-id="300f6-174">설명</span><span class="sxs-lookup"><span data-stu-id="300f6-174">Description</span></span> | <span data-ttu-id="300f6-175">필수</span><span class="sxs-lookup"><span data-stu-id="300f6-175">Required</span></span> | <span data-ttu-id="300f6-176">기본값</span><span class="sxs-lookup"><span data-stu-id="300f6-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="300f6-177">frequency</span><span class="sxs-lookup"><span data-stu-id="300f6-177">frequency</span></span> |<span data-ttu-id="300f6-178">데이터 집합 조각 프로덕션에 대 한 hello 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-178">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="300f6-179"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="300f6-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="300f6-180">예</span><span class="sxs-lookup"><span data-stu-id="300f6-180">Yes</span></span> |<span data-ttu-id="300f6-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="300f6-181">NA</span></span> |
| <span data-ttu-id="300f6-182">interval</span><span class="sxs-lookup"><span data-stu-id="300f6-182">interval</span></span> |<span data-ttu-id="300f6-183">빈도 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="300f6-184">"X 주파수 간격" 결정 얼마나 자주 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-184">”Frequency x interval” determines how often hello slice is produced.</span></span><br/><br/><span data-ttu-id="300f6-185">설정 하는 경우는 시간 단위로 분할 되는 데이터 집합 toobe hello 필요, <b>주파수</b> 너무<b>시간</b>, 및 <b>간격</b> 너무<b>1</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-185">If you need hello dataset toobe sliced on an hourly basis, you set <b>Frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="300f6-186"><b>참고</b>: 1 분으로 주파수를 지정 하면 15 보다 작은 간격 toono hello 설정 하는 것이 좋습니다</span><span class="sxs-lookup"><span data-stu-id="300f6-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set hello interval toono less than 15</span></span> |<span data-ttu-id="300f6-187">예</span><span class="sxs-lookup"><span data-stu-id="300f6-187">Yes</span></span> |<span data-ttu-id="300f6-188">해당 없음</span><span class="sxs-lookup"><span data-stu-id="300f6-188">NA</span></span> |
| <span data-ttu-id="300f6-189">style</span><span class="sxs-lookup"><span data-stu-id="300f6-189">style</span></span> |<span data-ttu-id="300f6-190">Hello 간격의 시작/끝 hello에 hello 분할 영역을 생성 해야 하는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-190">Specifies whether hello slice should be produced at hello start/end of hello interval.</span></span><ul><li><span data-ttu-id="300f6-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="300f6-191">StartOfInterval</span></span></li><li><span data-ttu-id="300f6-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="300f6-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="300f6-193">Frequency를 tooMonth를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 달의 마지막 날에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-193">If Frequency is set tooMonth and style is set tooEndOfInterval, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="300f6-194">Hello 스타일 tooStartOfInterval을 설정 하는 경우에 월의 첫째 날으로 hello에 hello 조각이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-194">If hello style is set tooStartOfInterval, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="300f6-195">Frequency를 tooDay를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 지난 1 시간 동안 hello 하루 중에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-195">If Frequency is set tooDay and style is set tooEndOfInterval, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="300f6-196">Frequency를 tooHour를 설정 하는 경우 스타일 tooEndOfInterval 설정 되어 있으면 hello 조각이 hello 시간 hello 끝에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-196">If Frequency is set tooHour and style is set tooEndOfInterval, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="300f6-197">예를 들어, 오후 1 ~ 2 시 기간에 조각의 hello 조각이 오후 2 시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-197">For example, for a slice for 1 PM – 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="300f6-198">아니요</span><span class="sxs-lookup"><span data-stu-id="300f6-198">No</span></span> |<span data-ttu-id="300f6-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="300f6-199">EndOfInterval</span></span> |
| <span data-ttu-id="300f6-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="300f6-200">anchorDateTime</span></span> |<span data-ttu-id="300f6-201">스케줄러 toocompute 데이터 집합 분할 영역 경계에 의해 사용 된 시간에 hello 절대 위치를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-201">Defines hello absolute position in time used by scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="300f6-202"><b>참고</b>: hello AnchorDateTime에 hello 빈도 보다 더 세부적인 날짜 부분이 경우 hello 더 세분화 된 부분은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-202"><b>Note</b>: If hello AnchorDateTime has date parts that are more granular than hello frequency then hello more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="300f6-203">예를 들어 경우 hello, <b>간격</b> 은 <b>매시간</b> (빈도: 시간 및 간격: 1) 및 hello <b>AnchorDateTime</b> 포함 <b>, 분, 초</b>, 다음 hello <b>, 분, 초</b> hello AnchorDateTime의 일부는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-203">For example, if hello <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and hello <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then hello <b>minutes and seconds</b> parts of hello AnchorDateTime are ignored.</span></span> |<span data-ttu-id="300f6-204">아니요</span><span class="sxs-lookup"><span data-stu-id="300f6-204">No</span></span> |<span data-ttu-id="300f6-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="300f6-205">01/01/0001</span></span> |
| <span data-ttu-id="300f6-206">offset</span><span class="sxs-lookup"><span data-stu-id="300f6-206">offset</span></span> |<span data-ttu-id="300f6-207">어떤 hello에서 모든 데이터 집합 분할 영역의 시작과 끝을 향해 이동 하는 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-207">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="300f6-208"><b>참고</b>: hello 결과 결합 된 hello shift anchorDateTime 및 offset을 모두를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-208"><b>Note</b>: If both anchorDateTime and offset are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="300f6-209">아니요</span><span class="sxs-lookup"><span data-stu-id="300f6-209">No</span></span> |<span data-ttu-id="300f6-210">해당 없음</span><span class="sxs-lookup"><span data-stu-id="300f6-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="300f6-211">offset example</span><span class="sxs-lookup"><span data-stu-id="300f6-211">offset example</span></span>
<span data-ttu-id="300f6-212">기본적으로 매일(`"frequency": "Day", "interval": 1`) 조각은 UTC 시간으로 오전 12시(자정)에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="300f6-213">대신 hello 시작 시간 toobe 오전 6 시 UTC 시간을 하려는 경우 hello hello 다음 코드 조각에에서 나와 있는 것 처럼 오프셋을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-213">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="300f6-214">anchorDateTime 예제</span><span class="sxs-lookup"><span data-stu-id="300f6-214">anchorDateTime example</span></span>
<span data-ttu-id="300f6-215">다음 예제는 hello, hello dataset 23 시간 마다 한 번 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-215">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="300f6-216">hello 첫 번째 조각의 시작 시 hello anchorDateTime 너무 설정으로 지정 된 hello`2017-04-19T08:00:00` (UTC 시간).</span><span class="sxs-lookup"><span data-stu-id="300f6-216">hello first slice starts at hello time specified by hello anchorDateTime, which is set too`2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="300f6-217">offset/style 예제</span><span class="sxs-lookup"><span data-stu-id="300f6-217">offset/style Example</span></span>
<span data-ttu-id="300f6-218">hello 다음 데이터 집합은 월별 데이터 집합 및 오전 8시 매월 세 번째 점입니다 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="300f6-218">hello following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="300f6-219">데이터 집합 정책</span><span class="sxs-lookup"><span data-stu-id="300f6-219">Dataset policy</span></span>
<span data-ttu-id="300f6-220">데이터 집합 방법을 조각 실행에서 생성 된 hello 데이터 유효성을 검사할 수 소비에 대 한 준비가 될 때까지 지정 하는 유효성 검사 정책 정의 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-220">A dataset can have a validation policy defined that specifies how hello data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="300f6-221">이러한 경우 hello 조각 실행을 마친 후 hello 출력 조각 상태가 변경 되 너무**대기** 의 하위 상태와 **유효성 검사**합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-221">In such cases, after hello slice has finished execution, hello output slice status is changed too**Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="300f6-222">Hello 조각 상태 쪽 변경 hello 분할 영역 확인 되 면**준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-222">After hello slices are validated, hello slice status changes too**Ready**.</span></span> <span data-ttu-id="300f6-223">데이터 조각 생성 되었으면 hello 유효성 검사를 통과 하지 못한 경우,이 조각의에 의존 하는 다운스트림 분할 영역에 대 한 활동 실행 처리 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-223">If a data slice has been produced but did not pass hello validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="300f6-224">[모니터링 하 고 파이프라인 관리](data-factory-monitor-manage-pipelines.md) 표지 hello Data Factory에 데이터 조각이의 다양 한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers hello various states of data slices in Data Factory.</span></span>

<span data-ttu-id="300f6-225">hello **정책** 데이터 집합 정의 섹션 hello 조건 정의 또는 데이터 집합 분할 영역 hello hello 조건을 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-225">hello **policy** section in dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <span data-ttu-id="300f6-226">hello 다음 표에서 설명 hello에 사용할 수 있는 속성 **정책** 섹션:</span><span class="sxs-lookup"><span data-stu-id="300f6-226">hello following table describes properties you can use in hello **policy** section:</span></span>

| <span data-ttu-id="300f6-227">정책 이름</span><span class="sxs-lookup"><span data-stu-id="300f6-227">Policy Name</span></span> | <span data-ttu-id="300f6-228">설명</span><span class="sxs-lookup"><span data-stu-id="300f6-228">Description</span></span> | <span data-ttu-id="300f6-229">너무 적용</span><span class="sxs-lookup"><span data-stu-id="300f6-229">Applied too</span></span>| <span data-ttu-id="300f6-230">필수</span><span class="sxs-lookup"><span data-stu-id="300f6-230">Required</span></span> | <span data-ttu-id="300f6-231">기본값</span><span class="sxs-lookup"><span data-stu-id="300f6-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="300f6-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="300f6-232">minimumSizeMB</span></span> | <span data-ttu-id="300f6-233">Hello 데이터에 유효성을 검사 한 **Azure blob** 충족 hello 최소 크기 요구 사항 (메가바이트)입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-233">Validates that hello data in an **Azure blob** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="300f6-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="300f6-234">Azure Blob</span></span> |<span data-ttu-id="300f6-235">아니요</span><span class="sxs-lookup"><span data-stu-id="300f6-235">No</span></span> |<span data-ttu-id="300f6-236">해당 없음</span><span class="sxs-lookup"><span data-stu-id="300f6-236">NA</span></span> |
| <span data-ttu-id="300f6-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="300f6-237">minimumRows</span></span> | <span data-ttu-id="300f6-238">Hello 데이터에 유효성을 검사 한 **Azure SQL 데이터베이스** 또는 **Azure 테이블** hello 최소 행 수를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-238">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="300f6-239">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="300f6-239">Azure SQL Database</span></span></li><li><span data-ttu-id="300f6-240">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="300f6-240">Azure Table</span></span></li></ul> |<span data-ttu-id="300f6-241">아니요</span><span class="sxs-lookup"><span data-stu-id="300f6-241">No</span></span> |<span data-ttu-id="300f6-242">해당 없음</span><span class="sxs-lookup"><span data-stu-id="300f6-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="300f6-243">예</span><span class="sxs-lookup"><span data-stu-id="300f6-243">Examples</span></span>
<span data-ttu-id="300f6-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="300f6-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="300f6-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="300f6-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="300f6-246">이러한 속성과 예제에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="300f6-247">활동 정책</span><span class="sxs-lookup"><span data-stu-id="300f6-247">Activity policies</span></span>
<span data-ttu-id="300f6-248">정책은은 hello 테이블 조각이 처리 시에 특히는 활동의 런타임 동작을 hello는 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-248">Policies affect hello run-time behavior of an activity, specifically when hello slice of a table is processed.</span></span> <span data-ttu-id="300f6-249">다음 표에서 hello hello 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-249">hello following table provides hello details.</span></span>

| <span data-ttu-id="300f6-250">속성</span><span class="sxs-lookup"><span data-stu-id="300f6-250">Property</span></span> | <span data-ttu-id="300f6-251">허용된 값</span><span class="sxs-lookup"><span data-stu-id="300f6-251">Permitted values</span></span> | <span data-ttu-id="300f6-252">기본값</span><span class="sxs-lookup"><span data-stu-id="300f6-252">Default Value</span></span> | <span data-ttu-id="300f6-253">설명</span><span class="sxs-lookup"><span data-stu-id="300f6-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="300f6-254">동시성</span><span class="sxs-lookup"><span data-stu-id="300f6-254">concurrency</span></span> |<span data-ttu-id="300f6-255">정수 </span><span class="sxs-lookup"><span data-stu-id="300f6-255">Integer</span></span> <br/><br/><span data-ttu-id="300f6-256">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="300f6-256">Max value: 10</span></span> |<span data-ttu-id="300f6-257">1</span><span class="sxs-lookup"><span data-stu-id="300f6-257">1</span></span> |<span data-ttu-id="300f6-258">Hello 활동의 동시 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-258">Number of concurrent executions of hello activity.</span></span><br/><br/><span data-ttu-id="300f6-259">Hello 여러 조각에서 발생할 수 있는 병렬 활동 실행 횟수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-259">It determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="300f6-260">예를 들어 활동을 통해 toogo 해야 하는 경우 다양 한 사용 가능한 데이터에 더 큰 동시성 가치가 속도가 향상 hello 데이터 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-260">For example, if an activity needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> |
| <span data-ttu-id="300f6-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="300f6-261">executionPriorityOrder</span></span> |<span data-ttu-id="300f6-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="300f6-262">NewestFirst</span></span><br/><br/><span data-ttu-id="300f6-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="300f6-263">OldestFirst</span></span> |<span data-ttu-id="300f6-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="300f6-264">OldestFirst</span></span> |<span data-ttu-id="300f6-265">Hello 데이터 조각이 처리 중인의 순서를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-265">Determines hello ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="300f6-266">예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="300f6-267">Hello executionPriorityOrder toobe NewestFirst로 설정 하면 오후 5 시의 hello 조각이 먼저 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-267">If you set hello executionPriorityOrder toobe NewestFirst, hello slice at 5 PM is processed first.</span></span> <span data-ttu-id="300f6-268">마찬가지로 executionPriorityORder toobe hello OldestFIrst로 설정 하면 오후 4 시의 hello 조각이 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-268">Similarly if you set hello executionPriorityORder toobe OldestFIrst, then hello slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="300f6-269">retry</span><span class="sxs-lookup"><span data-stu-id="300f6-269">retry</span></span> |<span data-ttu-id="300f6-270">정수 </span><span class="sxs-lookup"><span data-stu-id="300f6-270">Integer</span></span><br/><br/><span data-ttu-id="300f6-271">최대값이 10이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="300f6-271">Max value can be 10</span></span> |<span data-ttu-id="300f6-272">0</span><span class="sxs-lookup"><span data-stu-id="300f6-272">0</span></span> |<span data-ttu-id="300f6-273">Hello 조각에 대 한 hello 데이터 처리 전 까지의 재시도 횟수 Failure로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-273">Number of retries before hello data processing for hello slice is marked as Failure.</span></span> <span data-ttu-id="300f6-274">지정 된 toohello를 데이터 조각에 대 한 활동 실행을 다시 시도 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-274">Activity execution for a data slice is retried up toohello specified retry count.</span></span> <span data-ttu-id="300f6-275">hello 재시도 hello 실패 후 가능한 한 빨리 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-275">hello retry is done as soon as possible after hello failure.</span></span> |
| <span data-ttu-id="300f6-276">시간 제한</span><span class="sxs-lookup"><span data-stu-id="300f6-276">timeout</span></span> |<span data-ttu-id="300f6-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="300f6-277">TimeSpan</span></span> |<span data-ttu-id="300f6-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="300f6-278">00:00:00</span></span> |<span data-ttu-id="300f6-279">Hello 활동에 대 한 제한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-279">Timeout for hello activity.</span></span> <span data-ttu-id="300f6-280">예: 00:10:00(시간 제한 10분을 의미함)</span><span class="sxs-lookup"><span data-stu-id="300f6-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="300f6-281">값을 지정 하지 않거나 0으로 하는 경우에 hello 시간 초과 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-281">If a value is not specified or is 0, hello timeout is infinite.</span></span><br/><br/><span data-ttu-id="300f6-282">분할 영역에 데이터 처리 시간이 hello hello 제한 시간 값을 초과 하는 경우 취소 되 및 hello 시스템 tooretry hello 처리를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-282">If hello data processing time on a slice exceeds hello timeout value, it is canceled, and hello system attempts tooretry hello processing.</span></span> <span data-ttu-id="300f6-283">재시도 횟수 hello hello retry 속성에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-283">hello number of retries depends on hello retry property.</span></span> <span data-ttu-id="300f6-284">시간 제한이 발생 hello 상태 tooTimedOut 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-284">When timeout occurs, hello status is set tooTimedOut.</span></span> |
| <span data-ttu-id="300f6-285">delay</span><span class="sxs-lookup"><span data-stu-id="300f6-285">delay</span></span> |<span data-ttu-id="300f6-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="300f6-286">TimeSpan</span></span> |<span data-ttu-id="300f6-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="300f6-287">00:00:00</span></span> |<span data-ttu-id="300f6-288">데이터 처리 hello 조각 시작 하기 전에 hello 지연 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-288">Specify hello delay before data processing of hello slice starts.</span></span><br/><br/><span data-ttu-id="300f6-289">데이터 조각에 대 한 활동의 hello 실행 hello 지연 되는 hello 예상 실행 시간 후에 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-289">hello execution of activity for a data slice is started after hello Delay is past hello expected execution time.</span></span><br/><br/><span data-ttu-id="300f6-290">예: 00:10:00(10분의 지연을 의미함)</span><span class="sxs-lookup"><span data-stu-id="300f6-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="300f6-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="300f6-291">longRetry</span></span> |<span data-ttu-id="300f6-292">정수 </span><span class="sxs-lookup"><span data-stu-id="300f6-292">Integer</span></span><br/><br/><span data-ttu-id="300f6-293">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="300f6-293">Max value: 10</span></span> |<span data-ttu-id="300f6-294">1</span><span class="sxs-lookup"><span data-stu-id="300f6-294">1</span></span> |<span data-ttu-id="300f6-295">hello 긴 다시 시도 횟수 후 hello 조각 실행이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-295">hello number of long retry attempts before hello slice execution is failed.</span></span><br/><br/><span data-ttu-id="300f6-296">longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="300f6-297">따라서 다시 시도 사이의 시간 toospecify 해야 할 경우 longRetry를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-297">So if you need toospecify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="300f6-298">Retry와 longRetry를 둘 다 지정 된 경우 다시 시도 횟수를 포함 하는 각 longRetry 시도 및 hello 최대 시도 횟수가 다시 시도 * longRetry 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and hello max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="300f6-299">예를 들어, hello 활동 정책의 설정에에서 따라 hello 사항이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="300f6-299">For example, if we have hello following settings in hello activity policy:</span></span><br/><span data-ttu-id="300f6-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="300f6-300">Retry: 3</span></span><br/><span data-ttu-id="300f6-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="300f6-301">longRetry: 2</span></span><br/><span data-ttu-id="300f6-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="300f6-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="300f6-303">하나의 분할 영역 tooexecute 가정 (상태 대기 중) hello 활동 실행 될 때마다가 실패 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-303">Assume there is only one slice tooexecute (status is Waiting) and hello activity execution fails every time.</span></span> <span data-ttu-id="300f6-304">우선 3번 연속 실행 시도를 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="300f6-305">각 시도 후 조각 상태 hello 재시도 것입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-305">After each attempt, hello slice status would be Retry.</span></span> <span data-ttu-id="300f6-306">통해 처음 3 시도 되 면 hello 조각 상태 LongRetry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-306">After first 3 attempts are over, hello slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="300f6-307">한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="300f6-308">그 후 hello 조각 상태가 Failed가 고 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-308">After that, hello slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="300f6-309">즉, 전체적으로 6번의 시도가 일어납니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="300f6-310">실행에 성공 hello 조각 상태는 준비와 더 이상 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-310">If any execution succeeds, hello slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="300f6-311">longRetry 명확 하지 않은 시간에 도착 하면 종속 데이터 또는 hello 전체 환경 연결이 잘 끊어지는 어떤 데이터 처리가 수행 아래 있는 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or hello overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="300f6-312">이러한 경우에 한 번에 하나씩 재시도 수행 하 도움이 되지 않을 수 및 출력을 원하는 hello에 결과 시간 간격 후 이렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in hello desired output.</span></span><br/><br/><span data-ttu-id="300f6-313">주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="300f6-314">일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="300f6-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="300f6-315">longRetryInterval</span></span> |<span data-ttu-id="300f6-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="300f6-316">TimeSpan</span></span> |<span data-ttu-id="300f6-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="300f6-317">00:00:00</span></span> |<span data-ttu-id="300f6-318">긴 시도 간의 지연을 hello</span><span class="sxs-lookup"><span data-stu-id="300f6-318">hello delay between long retry attempts</span></span> |

<span data-ttu-id="300f6-319">자세한 내용은 [파이프라인](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="300f6-320">데이터 조각의 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="300f6-320">Parallel processing of data slices</span></span>
<span data-ttu-id="300f6-321">지난 hello에 hello 파이프라인에 대 한 hello 시작 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-321">You can set hello start date for hello pipeline in hello past.</span></span> <span data-ttu-id="300f6-322">이렇게 하면 데이터 팩터리 자동으로 이전 hello에서 모든 데이터 조각 (뒤로 채우기)을 계산 하 고 처리를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-322">When you do so, Data Factory automatically calculates (back fills) all data slices in hello past and begins processing them.</span></span> <span data-ttu-id="300f6-323">예를 들어: 경우 시작 날짜가 2017-04-01 파이프라인을 생성 하 고 hello 현재 날짜는 2017-04-10입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-323">For example: if you create a pipeline with start date 2017-04-01 and hello current date is 2017-04-10.</span></span> <span data-ttu-id="300f6-324">Hello의 hello 흐름 출력 데이터 집합은 매일, 다음 2017-04-01에서 모든 hello 분할 영역을 처리 하는 데이터 팩터리 하기 시작 하는 경우 too2017-04-09 즉시 시작 날짜를 hello 이므로 지난 hello에 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-324">If hello cadence of hello output dataset is daily, then Data Factory starts processing all hello slices from 2017-04-01 too2017-04-09 immediately because hello start date is in hello past.</span></span> <span data-ttu-id="300f6-325">hello 조각이 2017-04-10에서 처리 되지 않습니다 아직 hello 가용성 섹션의 스타일 속성의 hello 값은 EndOfInterval 때문에 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-325">hello slice from 2017-04-10 is not processed yet because hello value of style property in hello availability section is EndOfInterval by default.</span></span> <span data-ttu-id="300f6-326">hello 가장 오래 된 조각을 처리 하는 먼저 OldestFirst가 executionPriorityOrder 값 hello 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-326">hello oldest slice is processed first as hello default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="300f6-327">Hello 스타일 속성에 대 한 참조 [dataset 가용성](#dataset-availability) 섹션.</span><span class="sxs-lookup"><span data-stu-id="300f6-327">For a description of hello style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="300f6-328">Hello executionPriorityOrder 섹션에 대 한 참조 hello [활동 정책](#activity-policies) 섹션.</span><span class="sxs-lookup"><span data-stu-id="300f6-328">For a description of hello executionPriorityOrder section, see hello [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="300f6-329">다시 채워진 데이터 조각을 toobe hello 설정 하 여 동시에 처리를 구성할 수 있습니다 **동시성** hello에 대 한 속성 **정책** hello 활동 JSON의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-329">You can configure back-filled data slices toobe processed in parallel by setting hello **concurrency** property in hello **policy** section of hello activity JSON.</span></span> <span data-ttu-id="300f6-330">이 속성은 여러 조각에서 발생할 수 있는 병렬 활동 실행 hello 수를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-330">This property determines hello number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="300f6-331">hello hello 동시성 속성 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-331">hello default value for hello concurrency property is 1.</span></span> <span data-ttu-id="300f6-332">따라서 기본적으로 조각이 한 번에 하나씩 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="300f6-333">hello 최 댓 값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-333">hello maximum value is 10.</span></span> <span data-ttu-id="300f6-334">파이프라인에서 큰 사용 가능한 데이터에 더 큰 동시성 값 집합을 통해 toogo를 필요로 하는 경우 데이터 처리 hello 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-334">When a pipeline needs toogo through a large set of available data, having a larger concurrency value speeds up hello data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="300f6-335">실패한 데이터 조각 다시 실행</span><span class="sxs-lookup"><span data-stu-id="300f6-335">Rerun a failed data slice</span></span>
<span data-ttu-id="300f6-336">데이터 조각을 처리 하는 동안 오류가 발생 하는 경우 Azure 포털 블레이드 또는 모니터 및 앱 관리를 사용 하 여 조각 hello 처리 실패 한 이유를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-336">When an error occurs while processing a data slice, you can find out why hello processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="300f6-337">자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 또는 [앱 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="300f6-338">다음 예에서는 두 개의 활동을 보여 주는 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-338">Consider hello following example, which shows two activities.</span></span> <span data-ttu-id="300f6-339">활동 1 및 활동 2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="300f6-340">Activity1은 Dataset1의 조각을 사용 하 고 Dataset2 Activity2 tooproduce hello 최종 데이터 집합의 조각 한 입력으로 사용 되는 조각을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 tooproduce a slice of hello Final Dataset.</span></span>

![실패한 조각](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="300f6-342">hello 다이어그램을 보여 줍니다 세 최근 분할 영역 외부로 오류가 생성 hello 오전 9 10에 대 한 슬라이스 Dataset2 했습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-342">hello diagram shows that out of three recent slices, there was a failure producing hello 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="300f6-343">데이터 팩터리 hello 시간 시계열 데이터 집합에 대 한 종속성을 자동으로 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-343">Data Factory automatically tracks dependency for hello time series dataset.</span></span> <span data-ttu-id="300f6-344">결과적으로, hello 활동 hello 오전 9 10 다운스트림 조각에 대 한 실행 시작 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-344">As a result, it does not start hello activity run for hello 9-10 AM downstream slice.</span></span>

<span data-ttu-id="300f6-345">데이터 팩터리 모니터링 및 관리 도구를 사용 하면 toodrill hello 진단 로그 hello 실패 한 조각 tooeasily 찾기 hello 루트 hello 문제에 대 한 발생 하 고 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-345">Data Factory monitoring and management tools allow you toodrill into hello diagnostic logs for hello failed slice tooeasily find hello root cause for hello issue and fix it.</span></span> <span data-ttu-id="300f6-346">Hello 문제를 해결 한 후에 tooproduce hello 실패 한 조각을 실행 하는 hello 활동을 쉽게 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-346">After you have fixed hello issue, you can easily start hello activity run tooproduce hello failed slice.</span></span> <span data-ttu-id="300f6-347">방법에 대 한 자세한 내용은 toorerun 참조, 데이터 조각에 대 한 상태 전환 이해 하 고 [모니터링 및 관리 Azure 포털 블레이드를 사용 하 여 파이프라인](data-factory-monitor-manage-pipelines.md) 또는 [모니터링 및 관리 앱](data-factory-monitor-manage-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-347">For more information on how toorerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="300f6-348">오전 9 10에 대 한 조각화 hello를 다시 실행 한 후 **Dataset2**, Data Factory hello hello 최종 데이터 집합에서 hello 오전 9 10 종속 조각에 대 한 실행을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-348">After you rerun hello 9-10 AM slice for **Dataset2**, Data Factory starts hello run for hello 9-10 AM dependent slice on hello final dataset.</span></span>

![실패한 조각 다시 실행](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="300f6-350">파이프라인의 여러 활동</span><span class="sxs-lookup"><span data-stu-id="300f6-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="300f6-351">그렇지만 하나의 파이프라인에 여러 개의 활동이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="300f6-352">파이프라인의 여러 활동을 있고 hello 활동 출력은 다른 활동의 입력 하지 hello 활동에 대 한 입력된 데이터 조각이 준비가 되었는지 여부 hello 활동 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-352">If you have multiple activities in a pipeline and hello output of an activity is not an input of another activity, hello activities may run in parallel if input data slices for hello activities are ready.</span></span>

<span data-ttu-id="300f6-353">Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-353">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="300f6-354">hello에 hello 활동 수 있는 동일한 파이프라인 또는 다른 파이프라인.</span><span class="sxs-lookup"><span data-stu-id="300f6-354">hello activities can be in hello same pipeline or in different pipelines.</span></span> <span data-ttu-id="300f6-355">두 번째 활동 hello hello 먼저 하나 성공적으로 완료 하는 경우에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-355">hello second activity executes only when hello first one finishes successfully.</span></span>

<span data-ttu-id="300f6-356">예를 들어 파이프라인의 두 활동에 있는 경우 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="300f6-356">For example, consider hello following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="300f6-357">외부 입력 데이터 집합 D1이 필요하고 출력 데이터 집합 D2를 생성하는 활동 A1</span><span class="sxs-lookup"><span data-stu-id="300f6-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="300f6-358">데이터 집합 D2로부터의 입력이 필요하고 출력 데이터 집합 D3을 생성하는 활동 A2</span><span class="sxs-lookup"><span data-stu-id="300f6-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="300f6-359">이 시나리오, A1 및 A2 활동에는 hello에 동일한 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-359">In this scenario, activities A1 and A2 are in hello same pipeline.</span></span> <span data-ttu-id="300f6-360">hello 활동 A1 hello 외부 데이터를 사용할 수를 예약 된 hello 가용성 주파수에 도달할 때 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-360">hello activity A1 runs when hello external data is available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="300f6-361">hello 활동 A2 실행 hello d 2에서 예약 된 조각을 사용할 수 있으며 hello 사용 가능한 일정된 빈도 도달 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-361">hello activity A2 runs when hello scheduled slices from D2 become available and hello scheduled availability frequency is reached.</span></span> <span data-ttu-id="300f6-362">데이터 집합 d 2의에서 hello 조각 중 하나에 오류가 발생 하는, 사용 가능 해질 때까지 A2 해당 조각에 대 한 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-362">If there is an error in one of hello slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="300f6-363">동일한 파이프라인 hello 다음 다이어그램은 같습니다. 두 활동 hello에 다이어그램 보기 hello:</span><span class="sxs-lookup"><span data-stu-id="300f6-363">hello Diagram view with both activities in hello same pipeline would look like hello following diagram:</span></span>

![동일한 파이프라인 활동 hello에 연결](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="300f6-365">앞서 언급 했 듯이 hello 활동 다른 파이프라인에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-365">As mentioned earlier, hello activities could be in different pipelines.</span></span> <span data-ttu-id="300f6-366">이 시나리오에서는 hello 다이어그램 보기 다이어그램을 다음 hello와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-366">In such a scenario, hello diagram view would look like hello following diagram:</span></span>

![두 개의 파이프라인에서 활동 연결](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="300f6-368">Hello 참조 [순차적으로 복사](#copy-sequentially) 예제를 보려면 hello 부록에서 섹션.</span><span class="sxs-lookup"><span data-stu-id="300f6-368">See hello [copy sequentially](#copy-sequentially) section in hello appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="300f6-369">다양한 빈도로 데이터 집합 모델링</span><span class="sxs-lookup"><span data-stu-id="300f6-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="300f6-370">Hello 샘플에서 창에 대 한 입력 및 출력 데이터 집합 및 hello 활동 일정 hello 주파수 같은 hello 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-370">In hello samples, hello frequencies for input and output datasets and hello activity schedule window were hello same.</span></span> <span data-ttu-id="300f6-371">일부 시나리오에는 하나 이상의 입력의 hello 빈도 아닌 다른 빈도로 hello 기능 tooproduce 출력을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-371">Some scenarios require hello ability tooproduce output at a frequency different than hello frequencies of one or more inputs.</span></span> <span data-ttu-id="300f6-372">Data Factory가 이러한 시나리오의 모델링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="300f6-373">샘플 1: 매시간 제공되는 입력 데이터에 대해 일별 출력 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="300f6-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="300f6-374">Azure Blob 저장소에서 매시간 사용 가능한 센서로부터 입력 측정값 데이터가 있는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="300f6-375">Hello 날에 대 한 tooproduce 평균, 최대값 및 최소값 등의 통계를 매일 집계 보고서를 원하는 [Data Factory hive 작업](data-factory-hive-activity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-375">You want tooproduce a daily aggregate report with statistics such as mean, maximum, and minimum for hello day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="300f6-376">다음은 Data Factory로 이 시나리오를 모델링하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="300f6-377">**입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="300f6-377">**Input dataset**</span></span>

<span data-ttu-id="300f6-378">매시간 hello는 일을 지정 하는 hello에 대 한 hello 폴더에 파일을 삭제할 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-378">hello hourly input files are dropped in hello folder for hello given day.</span></span> <span data-ttu-id="300f6-379">입력에 대한 Availability가 **Hour** 로 설정됩니다(frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="300f6-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="300f6-380">**출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="300f6-380">**Output dataset**</span></span>

<span data-ttu-id="300f6-381">하나의 출력 파일은 매일 hello 날의 폴더에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-381">One output file is created every day in hello day's folder.</span></span> <span data-ttu-id="300f6-382">출력의 Availability는 **Day** 로 설정됩니다(frequency: Day 및 interval: 1).</span><span class="sxs-lookup"><span data-stu-id="300f6-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="300f6-383">**작업: 파이프라인에서 hive 작업**</span><span class="sxs-lookup"><span data-stu-id="300f6-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="300f6-384">hello 하이브 스크립트에 적절 한 hello 받는 *DateTime* hello를 사용 하는 매개 변수로 정보 **WindowStart** hello 다음 코드 조각에에서 나와 있는 것 처럼 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-384">hello hive script receives hello appropriate *DateTime* information as parameters that use hello **WindowStart** variable as shown in hello following snippet.</span></span> <span data-ttu-id="300f6-385">hello 하이브 스크립트 hello 날에 대 한 hello 올바른 폴더에서이 변수 tooload hello 데이터를 사용 하 고 hello 집계 toogenerate hello 출력을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-385">hello hive script uses this variable tooload hello data from hello correct folder for hello day and run hello aggregation toogenerate hello output.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
                    "Month": "$$Text.Format('{0:MM}',WindowStart)",
                    "Day": "$$Text.Format('{0:dd}',WindowStart)"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },            
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 2,
                "timeout": "01:00:00"
            }
         }
     ]
   }
}
```

<span data-ttu-id="300f6-386">hello 다음 그림에 데이터 종속성 관점에서 hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-386">hello following diagram shows hello scenario from a data-dependency point of view.</span></span>

![데이터 종속성](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="300f6-388">hello 출력 분할 영역을 매일 24 시간 조각에서 입력된 데이터 집합에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-388">hello output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="300f6-389">이러한 종속성을 파악 하 여 자동으로 hello hello에 속하는 입력된 데이터 조각을 데이터 팩터리 계산 동일한 시간으로 생성 된 출력 조각 toobe hello 기간입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-389">Data Factory computes these dependencies automatically by figuring out hello input data slices that fall in hello same time period as hello output slice toobe produced.</span></span> <span data-ttu-id="300f6-390">Hello 24 입력된 분할 영역 중 하나를 사용할 수 없는 경우 데이터 팩터리의 hello 입력된 조각 toobe hello 일별 작업 실행을 시작 하기 전에 준비를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-390">If any of hello 24 input slices is not available, Data Factory waits for hello input slice toobe ready before starting hello daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="300f6-391">샘플 2: 식 및 데이터 Data Factory 함수로 종속성 지정</span><span class="sxs-lookup"><span data-stu-id="300f6-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="300f6-392">다른 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-392">Let’s consider another scenario.</span></span> <span data-ttu-id="300f6-393">두 개의 입력 데이터 집합을 처리하는 hive 작업이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="300f6-394">그 중 하나는 매일 새 데이터가 제공되지만 다른 하나는 매주 새 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="300f6-395">매일은 출력을 생성 하 고 hello 두 개의 입력 간에 조인을 toodo 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-395">Suppose you wanted toodo a join across hello two inputs and produce an output every day.</span></span>

<span data-ttu-id="300f6-396">데이터 팩터리 자동으로 알아 hello 오른쪽 입력 hello 간단한 방법은 데이터 조각이 시간이 기간 작동 하지 않는다 toohello 출력을 정렬 하 여 tooprocess을 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-396">hello simple approach in which Data Factory automatically figures out hello right input slices tooprocess by aligning toohello output data slice’s time period does not work.</span></span>

<span data-ttu-id="300f6-397">실행 하는 모든 활동에 대 한 데이터 팩터리 hello 사용 하도록 지난 주 데이터 조각을 hello 매주 입력된 데이터 집합에 대 한을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-397">You must specify that for every activity run, hello Data Factory should use last week’s data slice for hello weekly input dataset.</span></span> <span data-ttu-id="300f6-398">이 동작은 hello 조각 tooimplement 뒤에 표시 된 대로 Azure 데이터 팩터리 함수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-398">You use Azure Data Factory functions as shown in hello following snippet tooimplement this behavior.</span></span>

<span data-ttu-id="300f6-399">**입력1: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="300f6-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="300f6-400">hello는 hello Azure blob 업데이트 되 고 매일 첫 번째 입력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-400">hello first input is hello Azure blob being updated daily.</span></span>

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="300f6-401">**입력2: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="300f6-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="300f6-402">Input2는 hello 매주 업데이트 되 고 Azure blob입니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-402">Input2 is hello Azure blob being updated weekly.</span></span>

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

<span data-ttu-id="300f6-403">**출력: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="300f6-403">**Output: Azure blob**</span></span>

<span data-ttu-id="300f6-404">하나의 출력 파일은 hello 날에 대 한 hello 폴더에 매일을 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-404">One output file is created every day in hello folder for hello day.</span></span> <span data-ttu-id="300f6-405">출력의 가용성을 너무 설정**일** (빈도: 일, 간격: 1).</span><span class="sxs-lookup"><span data-stu-id="300f6-405">Availability of output is set too**day** (frequency: Day, interval: 1).</span></span>

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="300f6-406">**작업: 파이프라인에서 hive 작업**</span><span class="sxs-lookup"><span data-stu-id="300f6-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="300f6-407">hello은 두 개의 입력 하 고 출력 조각을 매일 생성 하는 hello hive 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-407">hello hive activity takes hello two inputs and produces an output slice every day.</span></span> <span data-ttu-id="300f6-408">에 매일의 출력 조각 toodepend hello 주간 입력에 대 한 지난 주의 입력된 조각은 다음과 같이 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-408">You can specify every day’s output slice toodepend on hello previous week’s input slice for weekly input as follows.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
            "Month": "$$Text.Format('{0:MM}',WindowStart)",
            "Day": "$$Text.Format('{0:dd}',WindowStart)"
          }
        },
        "scheduler": {
          "frequency": "Day",
          "interval": 1
        },            
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 2,  
          "timeout": "01:00:00"
        }
       }
     ]
   }
}
```

<span data-ttu-id="300f6-409">Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="300f6-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="300f6-410">부록</span><span class="sxs-lookup"><span data-stu-id="300f6-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="300f6-411">예제: 순차적으로 복사</span><span class="sxs-lookup"><span data-stu-id="300f6-411">Example: copy sequentially</span></span>
<span data-ttu-id="300f6-412">것은 가능한 toorun 여러 복사 작업 차례로 정렬/순차적 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-412">It is possible toorun multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="300f6-413">예를 들어 두 개의 복사본 입력 다음 hello로 (CopyActivity1 및 CopyActivity2) 파이프라인의 활동 데이터 출력 데이터 집합을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with hello following input data output datasets:</span></span>   

<span data-ttu-id="300f6-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="300f6-414">CopyActivity1</span></span>

<span data-ttu-id="300f6-415">입력: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="300f6-415">Input: Dataset.</span></span> <span data-ttu-id="300f6-416">출력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="300f6-416">Output: Dataset2.</span></span>

<span data-ttu-id="300f6-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="300f6-417">CopyActivity2</span></span>

<span data-ttu-id="300f6-418">입력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="300f6-418">Input: Dataset2.</span></span>  <span data-ttu-id="300f6-419">출력: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="300f6-419">Output: Dataset3.</span></span>

<span data-ttu-id="300f6-420">CopyActivity2 hello CopyActivity1을 성공적으로 실행 하 고 Dataset2 ´ ï ´ 경우에 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-420">CopyActivity2 would run only if hello CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="300f6-421">Hello 샘플 파이프라인 JSON 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-421">Here is hello sample pipeline JSON:</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="300f6-422">확인 hello 예 hello 출력 데이터 집합의 첫 번째 복사 작업 (Dataset2) hello hello 두 번째 활동에 대 한 입력으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-422">Notice that in hello example, hello output dataset of hello first copy activity (Dataset2) is specified as input for hello second activity.</span></span> <span data-ttu-id="300f6-423">따라서 두 번째 활동 hello hello 첫 번째 활동에서 hello 출력 데이터 집합은 준비 하는 경우에 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-423">Therefore, hello second activity runs only when hello output dataset from hello first activity is ready.</span></span>  

<span data-ttu-id="300f6-424">hello 예제 CopyActivity2 수 Dataset3, 등의 다른 입력 있지만 않아 hello 활동 CopyActivity1 완료 될 때까지 실행 되지 않습니다는 입력된 tooCopyActivity2로 Dataset2를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-424">In hello example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input tooCopyActivity2, so hello activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="300f6-425">예:</span><span class="sxs-lookup"><span data-stu-id="300f6-425">For example:</span></span>

<span data-ttu-id="300f6-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="300f6-426">CopyActivity1</span></span>

<span data-ttu-id="300f6-427">입력: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="300f6-427">Input: Dataset1.</span></span> <span data-ttu-id="300f6-428">출력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="300f6-428">Output: Dataset2.</span></span>

<span data-ttu-id="300f6-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="300f6-429">CopyActivity2</span></span>

<span data-ttu-id="300f6-430">입력: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="300f6-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="300f6-431">출력: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="300f6-431">Output: Dataset4.</span></span>

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="300f6-432">Hello 예에서는 두 입력된 데이터 집합 hello 두 번째 복사 작업에 지정 된 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-432">Notice that in hello example, two input datasets are specified for hello second copy activity.</span></span> <span data-ttu-id="300f6-433">여러 입력을 지정 하는 경우에만 hello 첫 번째 입력된 데이터 집합은 데이터를 복사 하는 데 사용 되는 있지만 다른 데이터 집합 종속성으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-433">When multiple inputs are specified, only hello first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="300f6-434">CopyActivity2 hello 다음 조건이 충족 되 후에 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-434">CopyActivity2 would start only after hello following conditions are met:</span></span>

* <span data-ttu-id="300f6-435">CopyActivity1이 성공적으로 완료되고 Dataset2가 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="300f6-436">데이터 tooDataset4를 복사 하는 경우에이 데이터 집합 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-436">This dataset is not used when copying data tooDataset4.</span></span> <span data-ttu-id="300f6-437">CopyActivity2에 대한 일정 종속성으로만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="300f6-438">Dataset3을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-438">Dataset3 is available.</span></span> <span data-ttu-id="300f6-439">이 데이터 집합 대상인 복사한 toohello hello 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="300f6-439">This dataset represents hello data that is copied toohello destination.</span></span> 
