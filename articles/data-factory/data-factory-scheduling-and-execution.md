---
title: "Data Factory에서 예약 및 실행 | Microsoft Docs"
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
ms.openlocfilehash: e6fd92cde91ae5f171c855c07fa8974a19703b41
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="data-factory-scheduling-and-execution"></a><span data-ttu-id="7ab6b-103">Data Factory 예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="7ab6b-103">Data Factory scheduling and execution</span></span>
<span data-ttu-id="7ab6b-104">이 문서에서는 Azure Data Factory 응용 프로그램 모델의 예약 및 실행에 대한 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-104">This article explains the scheduling and execution aspects of the Azure Data Factory application model.</span></span> <span data-ttu-id="7ab6b-105">이 문서는 사용자가 작업, 파이프라인, 연결된 서비스 및 데이터 집합과 같은 Data Factory 응용 프로그램 모델 개념을 이해하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-105">This article assumes that you understand basics of Data Factory application model concepts, including activity, pipelines, linked services, and datasets.</span></span> <span data-ttu-id="7ab6b-106">Azure Data Factory의 기본 개념은 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-106">For basic concepts of Azure Data Factory, see the following articles:</span></span>

* [<span data-ttu-id="7ab6b-107">데이터 팩터리 소개</span><span class="sxs-lookup"><span data-stu-id="7ab6b-107">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="7ab6b-108">파이프라인</span><span class="sxs-lookup"><span data-stu-id="7ab6b-108">Pipelines</span></span>](data-factory-create-pipelines.md)
* [<span data-ttu-id="7ab6b-109">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="7ab6b-109">Datasets</span></span>](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a><span data-ttu-id="7ab6b-110">파이프라인의 시작 및 종료 시간</span><span class="sxs-lookup"><span data-stu-id="7ab6b-110">Start and end times of pipeline</span></span>
<span data-ttu-id="7ab6b-111">파이프라인은 **시작** 시간과 **종료** 시간 사이에서만 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-111">A pipeline is active only between its **start** time and **end** time.</span></span> <span data-ttu-id="7ab6b-112">시작 시간 이전 또는 종료 시간 이후에 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-112">It is not executed before the start time or after the end time.</span></span> <span data-ttu-id="7ab6b-113">파이프라인이 일시 중지되면 시작 및 종료 시간에 관계없이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-113">If the pipeline is paused, it is not executed irrespective of its start and end time.</span></span> <span data-ttu-id="7ab6b-114">실행될 파이프라인의 경우 일시 중지되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-114">For a pipeline to run, it should not be paused.</span></span> <span data-ttu-id="7ab6b-115">파이프라인 정의에서 이러한 설정(start, end, paused)을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-115">You find these settings (start, end, paused) in the pipeline definition:</span></span> 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

<span data-ttu-id="7ab6b-116">이러한 속성에 대한 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-116">For more information these properties, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> 


## <a name="specify-schedule-for-an-activity"></a><span data-ttu-id="7ab6b-117">활동 일정 지정</span><span class="sxs-lookup"><span data-stu-id="7ab6b-117">Specify schedule for an activity</span></span>
<span data-ttu-id="7ab6b-118">실행되는 파이프라인이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-118">It is not the pipeline that is executed.</span></span> <span data-ttu-id="7ab6b-119">파이프라인의 전체 컨텍스트에서 실행되는 것은 파이프라인의 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-119">It is the activities in the pipeline that are executed in the overall context of the pipeline.</span></span> <span data-ttu-id="7ab6b-120">활동 JSON의 **scheduler** 섹션을 사용하여 활동에 대한 되풀이 일정을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-120">You can specify a recurring schedule for an activity by using the **scheduler** section of activity JSON.</span></span> <span data-ttu-id="7ab6b-121">예를 들어 활동을 다음과 같이 시간별로 실행하도록 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-121">For example, you can schedule an activity to run hourly as follows:</span></span>  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

<span data-ttu-id="7ab6b-122">다음 다이어그램과 같이 활동 일정을 지정하면 파이프라인 시작 및 종료 시간에 일련의 연속 창이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-122">As shown in the following diagram, specifying a schedule for an activity creates a series of tumbling windows with in the pipeline start and end times.</span></span> <span data-ttu-id="7ab6b-123">연속 창은 일련의 고정된 크기의 겹치지 않는 연속적인 시간 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-123">Tumbling windows are a series of fixed-size non-overlapping, contiguous time intervals.</span></span> <span data-ttu-id="7ab6b-124">활동에 대한 이러한 논리적 연속 창을 **활동 기간**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-124">These logical tumbling windows for an activity are called **activity windows**.</span></span>

![활동 스케줄러 예제](media/data-factory-scheduling-and-execution/scheduler-example.png)

<span data-ttu-id="7ab6b-126">활동에 대한 **scheduler** 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-126">The **scheduler** property for an activity is optional.</span></span> <span data-ttu-id="7ab6b-127">이 속성을 지정하면 활동에 대한 출력 데이터 집합 정의에 지정하는 빈도와 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-127">If you do specify this property, it must match the cadence you specify in the definition of output dataset for the activity.</span></span> <span data-ttu-id="7ab6b-128">현재 출력 데이터 집합은 일정을 작동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-128">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="7ab6b-129">따라서 활동에서 출력을 생성하지 않더라도 출력 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-129">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> 

## <a name="specify-schedule-for-a-dataset"></a><span data-ttu-id="7ab6b-130">데이터 집합 일정 지정</span><span class="sxs-lookup"><span data-stu-id="7ab6b-130">Specify schedule for a dataset</span></span>
<span data-ttu-id="7ab6b-131">Data Factory 파이프라인의 활동은 0개 이상의 입력 **데이터 집합**을 받고, 하나 이상의 출력 데이터 집합을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-131">An activity in a Data Factory pipeline can take zero or more input **datasets** and produce one or more output datasets.</span></span> <span data-ttu-id="7ab6b-132">활동의 경우 데이터 집합 정의의 **availability** 섹션을 사용하여 입력 데이터를 사용할 수 있거나 출력 데이터를 생성하는 빈도를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-132">For an activity, you can specify the cadence at which the input data is available or the output data is produced by using the **availability** section in the dataset definitions.</span></span> 

<span data-ttu-id="7ab6b-133">**availability** 섹션의 **frequency**는 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-133">**Frequency** in the **availability** section specifies the time unit.</span></span> <span data-ttu-id="7ab6b-134">frequency에 허용되는 값은 Minute, Hour, Day, Week 및 Month입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-134">The allowed values for frequency are: Minute, Hour, Day, Week, and Month.</span></span> <span data-ttu-id="7ab6b-135">availability 섹션의 **interval** 속성은 frequency에 대한 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-135">The **interval** property in the availability section specifies a multiplier for frequency.</span></span> <span data-ttu-id="7ab6b-136">예를 들어 출력 데이터 집합에 대해 frequency가 Day로 설정되고 interval이 1로 설정되면 출력 데이터를 매일 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-136">For example: if the frequency is set to Day and interval is set to 1 for an output dataset, the output data is produced daily.</span></span> <span data-ttu-id="7ab6b-137">frequency를 Minute로 지정하는 경우 interval을 15 이상으로 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-137">If you specify the frequency as minute, we recommend that you set the interval to no less than 15.</span></span> 

<span data-ttu-id="7ab6b-138">다음 예제에서 입력 데이터는 매시간 사용할 수 있으며 출력 데이터는 매시간(`"frequency": "Hour", "interval": 1`) 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-138">In the following example, the input data is available hourly and the output data is produced hourly (`"frequency": "Hour", "interval": 1`).</span></span> 

<span data-ttu-id="7ab6b-139">**입력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-139">**Input dataset:**</span></span> 

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


<span data-ttu-id="7ab6b-140">**출력 데이터 집합:**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-140">**Output dataset**</span></span>

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

<span data-ttu-id="7ab6b-141">현재 **출력 데이터 집합은 일정을 작동하고 있습니다**.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-141">Currently, **output dataset drives the schedule**.</span></span> <span data-ttu-id="7ab6b-142">즉 출력 데이터 집합에 대해 지정된 일정은 런타임에 활동을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-142">In other words, the schedule specified for the output dataset is used to run an activity at runtime.</span></span> <span data-ttu-id="7ab6b-143">따라서 활동에서 출력을 생성하지 않더라도 출력 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-143">Therefore, you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="7ab6b-144">활동이 입력을 가져오지 않으면 입력 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-144">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 

<span data-ttu-id="7ab6b-145">다음 파이프라인 정의에서 **scheduler** 속성은 활동에 대한 일정을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-145">In the following pipeline definition, the **scheduler** property is used to specify schedule for the activity.</span></span> <span data-ttu-id="7ab6b-146">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-146">This property is optional.</span></span> <span data-ttu-id="7ab6b-147">현재 활동에 대한 일정은 출력 데이터 집합에 지정된 일정과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-147">Currently, the schedule for the activity must match the schedule specified for the output dataset.</span></span>
 
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

<span data-ttu-id="7ab6b-148">이 예제에서는 활동은 파이프라인의 시작과 끝 시간 사이에서 매시간 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-148">In this example, the activity runs hourly between the start and end times of the pipeline.</span></span> <span data-ttu-id="7ab6b-149">출력 데이터는 3시간 기간(오전 8-9시, 오전 9-10시, 오전 10-11시) 동안 매시간 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-149">The output data is produced hourly for three-hour windows (8 AM - 9 AM, 9 AM - 10 AM, and 10 AM - 11 AM).</span></span> 

<span data-ttu-id="7ab6b-150">활동 실행에서 사용하거나 생성한 데이터의 각 단위를 **데이터 조각**이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-150">Each unit of data consumed or produced by an activity run is called a **data slice**.</span></span> <span data-ttu-id="7ab6b-151">다음 다이어그램에서는 입력 데이터 집합과 출력 데이터 집합이 하나씩 포함된 활동의 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-151">The following diagram shows an example of an activity with one input dataset and one output dataset:</span></span> 

![가용성 스케줄러](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

<span data-ttu-id="7ab6b-153">위 다이어그램에서는 입력 및 출력 데이터 집합에 대한 매시간 데이터 조각을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-153">The diagram shows the hourly data slices for the input and output dataset.</span></span> <span data-ttu-id="7ab6b-154">다이어그램은 처리할 준비가 된 입력 조각 3개를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-154">The diagram shows three input slices that are ready for processing.</span></span> <span data-ttu-id="7ab6b-155">오전 10-11시 작업이 진행 중이며 오전 10-11시 출력 조각이 생성되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-155">The 10-11 AM activity is in progress, producing the 10-11 AM output slice.</span></span> 

<span data-ttu-id="7ab6b-156">[SliceStart](data-factory-functions-variables.md#data-factory-system-variables) 및 [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables) 변수를 사용하여 데이터 집합 JSON에서 현재 조각과 관련된 시간 간격에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-156">You can access the time interval associated with the current slice in the dataset JSON by using variables: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) and [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables).</span></span> <span data-ttu-id="7ab6b-157">마찬가지로 WindowStart 및 WindowEnd를 사용하여 활동 기간과 관련된 시간 간격에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-157">Similarly, you can access the time interval associated with an activity window by using the WindowStart and WindowEnd.</span></span> <span data-ttu-id="7ab6b-158">활동 일정은 해당 활동의 출력 데이터 집합 일정과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-158">The schedule of an activity must match the schedule of the output dataset for the activity.</span></span> <span data-ttu-id="7ab6b-159">따라서 SliceStart 및 SliceEnd 값은 각각 WindowStart 및 WindowEnd 값과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-159">Therefore, the SliceStart and SliceEnd values are the same as WindowStart and WindowEnd values respectively.</span></span> <span data-ttu-id="7ab6b-160">이러한 변수에 대한 자세한 내용은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md#data-factory-system-variables) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-160">For more information on these variables, see [Data Factory functions and system variables](data-factory-functions-variables.md#data-factory-system-variables) articles.</span></span>  

<span data-ttu-id="7ab6b-161">이러한 변수를 작업 JSON에서 다양한 용도로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-161">You can use these variables for different purposes in your activity JSON.</span></span> <span data-ttu-id="7ab6b-162">예를 들어 시계열 데이터(예: 오전 8시에서 오전 9시)를 나타내는 입력 및 출력 데이터 집합에서 데이터를 선택하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-162">For example, you can use them to select data from input and output datasets representing time series data (for example: 8 AM to 9 AM).</span></span> <span data-ttu-id="7ab6b-163">또한 이 예제에서는 **WindowStart** 및 **WindowEnd**를 사용하여 활동 실행에 대한 관련 데이터를 선택하고 적절한 **folderPath**의 Blob에 이 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-163">This example also uses **WindowStart** and **WindowEnd** to select relevant data for an activity run and copy it to a blob with the appropriate **folderPath**.</span></span> <span data-ttu-id="7ab6b-164">**folderPath** 는 매시간 별도의 폴더를 포함하도록 매개 변수화됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-164">The **folderPath** is parameterized to have a separate folder for every hour.</span></span>  

<span data-ttu-id="7ab6b-165">앞의 예에서 입력 및 출력 데이터 집합에 대해 지정된 일정은 동일합니다(매시간).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-165">In the preceding example, the schedule specified for input and output datasets is the same (hourly).</span></span> <span data-ttu-id="7ab6b-166">활동에 대한 입력 데이터 집합을 다른 빈도(예: 15분마다)에서 사용할 수 있는 경우 출력 데이터 집합이 활동 일정을 작동하는 것이므로 이 출력 데이터 집합을 생성하는 활동은 한 시간에 한 번씩 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-166">If the input dataset for the activity is available at a different frequency, say every 15 minutes, the activity that produces this output dataset still runs once an hour as the output dataset is what drives the activity schedule.</span></span> <span data-ttu-id="7ab6b-167">자세한 내용은 [다양한 빈도로 데이터 집합 모델링](#model-datasets-with-different-frequencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-167">For more information, see [Model datasets with different frequencies](#model-datasets-with-different-frequencies).</span></span>

## <a name="dataset-availability-and-policies"></a><span data-ttu-id="7ab6b-168">데이터 집합 가용성 및 정책</span><span class="sxs-lookup"><span data-stu-id="7ab6b-168">Dataset availability and policies</span></span>
<span data-ttu-id="7ab6b-169">데이터 집합 정의의 availability 섹션에서 frequency 및 interval 속성의 사용을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-169">You have seen the usage of frequency and interval properties in the availability section of dataset definition.</span></span> <span data-ttu-id="7ab6b-170">활동의 예약 및 실행에 영향을 주는 몇 가지 다른 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-170">There are a few other properties that affect the scheduling and execution of an activity.</span></span> 

### <a name="dataset-availability"></a><span data-ttu-id="7ab6b-171">데이터 집합 가용성</span><span class="sxs-lookup"><span data-stu-id="7ab6b-171">Dataset availability</span></span> 
<span data-ttu-id="7ab6b-172">다음 표에서는 **availability** 섹션에서 사용할 수 있는 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-172">The following table describes properties you can use in the **availability** section:</span></span>

| <span data-ttu-id="7ab6b-173">속성</span><span class="sxs-lookup"><span data-stu-id="7ab6b-173">Property</span></span> | <span data-ttu-id="7ab6b-174">설명</span><span class="sxs-lookup"><span data-stu-id="7ab6b-174">Description</span></span> | <span data-ttu-id="7ab6b-175">필수</span><span class="sxs-lookup"><span data-stu-id="7ab6b-175">Required</span></span> | <span data-ttu-id="7ab6b-176">기본값</span><span class="sxs-lookup"><span data-stu-id="7ab6b-176">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7ab6b-177">frequency</span><span class="sxs-lookup"><span data-stu-id="7ab6b-177">frequency</span></span> |<span data-ttu-id="7ab6b-178">데이터 집합 조각 생성을 위한 시간 단위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-178">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="7ab6b-179"><b>지원되는 빈도</b>: 분, 시, 일, 주, 월</span><span class="sxs-lookup"><span data-stu-id="7ab6b-179"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="7ab6b-180">예</span><span class="sxs-lookup"><span data-stu-id="7ab6b-180">Yes</span></span> |<span data-ttu-id="7ab6b-181">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-181">NA</span></span> |
| <span data-ttu-id="7ab6b-182">interval</span><span class="sxs-lookup"><span data-stu-id="7ab6b-182">interval</span></span> |<span data-ttu-id="7ab6b-183">빈도 승수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-183">Specifies a multiplier for frequency</span></span><br/><br/><span data-ttu-id="7ab6b-184">"빈도 x 간격"은 조각을 생성하는 빈도를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-184">”Frequency x interval” determines how often the slice is produced.</span></span><br/><br/><span data-ttu-id="7ab6b-185">데이터 집합을 시간 단위로 조각화해야 하는 경우 <b>frequency</b>를 <b>Hour</b>로, <b>interval</b>을 <b>1</b>로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-185">If you need the dataset to be sliced on an hourly basis, you set <b>Frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="7ab6b-186"><b>참고:</b> 빈도를 Minute(분)으로 지정하면 15 이상으로 간격을 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-186"><b>Note</b>: If you specify Frequency as Minute, we recommend that you set the interval to no less than 15</span></span> |<span data-ttu-id="7ab6b-187">예</span><span class="sxs-lookup"><span data-stu-id="7ab6b-187">Yes</span></span> |<span data-ttu-id="7ab6b-188">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-188">NA</span></span> |
| <span data-ttu-id="7ab6b-189">style</span><span class="sxs-lookup"><span data-stu-id="7ab6b-189">style</span></span> |<span data-ttu-id="7ab6b-190">간격의 시작/끝에 조각을 생성해야 하는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-190">Specifies whether the slice should be produced at the start/end of the interval.</span></span><ul><li><span data-ttu-id="7ab6b-191">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="7ab6b-191">StartOfInterval</span></span></li><li><span data-ttu-id="7ab6b-192">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="7ab6b-192">EndOfInterval</span></span></li></ul><br/><br/><span data-ttu-id="7ab6b-193">Frequency를 Month로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 월의 마지막 날에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-193">If Frequency is set to Month and style is set to EndOfInterval, the slice is produced on the last day of month.</span></span> <span data-ttu-id="7ab6b-194">style을 StartOfInterval로 설정하는 경우 조각을 달의 첫 번째 날에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-194">If the style is set to StartOfInterval, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="7ab6b-195">frequency를 Day로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 일의 마지막 시간에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-195">If Frequency is set to Day and style is set to EndOfInterval, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="7ab6b-196">Frequency를 Hour로 설정하고 style을 EndOfInterval로 설정하는 경우 조각을 시간의 끝에 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-196">If Frequency is set to Hour and style is set to EndOfInterval, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="7ab6b-197">예를 들어 오후 1~2시 기간에 대한 조각은 오후 2시에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-197">For example, for a slice for 1 PM – 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="7ab6b-198">아니요</span><span class="sxs-lookup"><span data-stu-id="7ab6b-198">No</span></span> |<span data-ttu-id="7ab6b-199">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="7ab6b-199">EndOfInterval</span></span> |
| <span data-ttu-id="7ab6b-200">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="7ab6b-200">anchorDateTime</span></span> |<span data-ttu-id="7ab6b-201">스케줄러에서 사용하는 시간에 절대 위치를 정의하여 데이터 집합 조각 경계를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-201">Defines the absolute position in time used by scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="7ab6b-202"><b>참고:</b> AnchorDateTime에 빈도보다 더 세분화된 날짜 부분이 있는 경우 더 세분화된 부분을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-202"><b>Note</b>: If the AnchorDateTime has date parts that are more granular than the frequency then the more granular parts are ignored.</span></span> <br/><br/><span data-ttu-id="7ab6b-203">예를 들어 <b>간격</b>이 <b>매시간</b>(frequency: Hour 및 interval: 1)이고 <b>AnchorDateTime</b>에서 <b>분 및 초</b>를 포함하는 경우 AnchorDateTime의 <b>분 및 초</b> 부분은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-203">For example, if the <b>interval</b> is <b>hourly</b> (frequency: hour and interval: 1) and the <b>AnchorDateTime</b> contains <b>minutes and seconds</b>, then the <b>minutes and seconds</b> parts of the AnchorDateTime are ignored.</span></span> |<span data-ttu-id="7ab6b-204">아니요</span><span class="sxs-lookup"><span data-stu-id="7ab6b-204">No</span></span> |<span data-ttu-id="7ab6b-205">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="7ab6b-205">01/01/0001</span></span> |
| <span data-ttu-id="7ab6b-206">offset</span><span class="sxs-lookup"><span data-stu-id="7ab6b-206">offset</span></span> |<span data-ttu-id="7ab6b-207">모든 데이터 집합 조각의 시작과 끝이 이동에 의한 Timespan입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-207">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="7ab6b-208"><b>참고:</b> anchorDateTime 및 offset이 모두 지정되면 결과적으로 이동이 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-208"><b>Note</b>: If both anchorDateTime and offset are specified, the result is the combined shift.</span></span> |<span data-ttu-id="7ab6b-209">아니요</span><span class="sxs-lookup"><span data-stu-id="7ab6b-209">No</span></span> |<span data-ttu-id="7ab6b-210">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-210">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="7ab6b-211">offset example</span><span class="sxs-lookup"><span data-stu-id="7ab6b-211">offset example</span></span>
<span data-ttu-id="7ab6b-212">기본적으로 매일(`"frequency": "Day", "interval": 1`) 조각은 UTC 시간으로 오전 12시(자정)에서 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-212">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM UTC time (midnight).</span></span> <span data-ttu-id="7ab6b-213">대신, 시작 시간을 UTC 시간으로 오전 6시로 설정하려면 다음 코드 조각과 같이 오프셋을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-213">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="7ab6b-214">anchorDateTime 예제</span><span class="sxs-lookup"><span data-stu-id="7ab6b-214">anchorDateTime example</span></span>
<span data-ttu-id="7ab6b-215">다음 예제에서는 데이터 집합이 23시간마다 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-215">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="7ab6b-216">첫 번째 조각은 `2017-04-19T08:00:00`(UTC 시간)으로 설정된 anchorDateTime 지정 시간에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-216">The first slice starts at the time specified by the anchorDateTime, which is set to `2017-04-19T08:00:00` (UTC time).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="7ab6b-217">offset/style 예제</span><span class="sxs-lookup"><span data-stu-id="7ab6b-217">offset/style Example</span></span>
<span data-ttu-id="7ab6b-218">다음 데이터 집합은 월별 데이터 집합으로, 매월 3일, 오전 8시(`3.08:00:00`)에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-218">The following dataset is a monthly dataset and is produced on 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a><span data-ttu-id="7ab6b-219">데이터 집합 정책</span><span class="sxs-lookup"><span data-stu-id="7ab6b-219">Dataset policy</span></span>
<span data-ttu-id="7ab6b-220">데이터 집합에는 조각 실행으로 생성된 데이터를 사용하기 전에 유효성 검사하는 방법을 지정하는 유효성 검사 정책이 정의되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-220">A dataset can have a validation policy defined that specifies how the data generated by a slice execution can be validated before it is ready for consumption.</span></span> <span data-ttu-id="7ab6b-221">이러한 경우 조각의 실행이 완료된 후 출력 조각 상태는 **Validation**의 하위 상태를 포함한 **Waiting**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-221">In such cases, after the slice has finished execution, the output slice status is changed to **Waiting** with a substatus of **Validation**.</span></span> <span data-ttu-id="7ab6b-222">조각의 유효성이 검사되었으면 조각 상태는 **Ready**로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-222">After the slices are validated, the slice status changes to **Ready**.</span></span> <span data-ttu-id="7ab6b-223">데이터 조각이 생성되었으나 유효성 검사를 통과하지 못하면 이 조각에 따라 다운스트림 조각에 대한 작업 실행은 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-223">If a data slice has been produced but did not pass the validation, activity runs for downstream slices that depend on this slice are not processed.</span></span> <span data-ttu-id="7ab6b-224">[파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 에서는 Data Factory에 있는 데이터 조각의 다양한 상태에 대해 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-224">[Monitor and manage pipelines](data-factory-monitor-manage-pipelines.md) covers the various states of data slices in Data Factory.</span></span>

<span data-ttu-id="7ab6b-225">데이터 집합 정의의 **정책** 섹션에서 데이터 집합 조각이 충족해야 하는 기준 또는 조건을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-225">The **policy** section in dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span> <span data-ttu-id="7ab6b-226">다음 표에서는 **policy** 섹션에서 사용할 수 있는 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-226">The following table describes properties you can use in the **policy** section:</span></span>

| <span data-ttu-id="7ab6b-227">정책 이름</span><span class="sxs-lookup"><span data-stu-id="7ab6b-227">Policy Name</span></span> | <span data-ttu-id="7ab6b-228">설명</span><span class="sxs-lookup"><span data-stu-id="7ab6b-228">Description</span></span> | <span data-ttu-id="7ab6b-229">에 적용</span><span class="sxs-lookup"><span data-stu-id="7ab6b-229">Applied To</span></span> | <span data-ttu-id="7ab6b-230">필수</span><span class="sxs-lookup"><span data-stu-id="7ab6b-230">Required</span></span> | <span data-ttu-id="7ab6b-231">기본값</span><span class="sxs-lookup"><span data-stu-id="7ab6b-231">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="7ab6b-232">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="7ab6b-232">minimumSizeMB</span></span> | <span data-ttu-id="7ab6b-233">**Azure Blob** 에서 데이터가 최소 크기 요구 사항(메가바이트)을 충족하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-233">Validates that the data in an **Azure blob** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="7ab6b-234">Azure Blob</span><span class="sxs-lookup"><span data-stu-id="7ab6b-234">Azure Blob</span></span> |<span data-ttu-id="7ab6b-235">아니요</span><span class="sxs-lookup"><span data-stu-id="7ab6b-235">No</span></span> |<span data-ttu-id="7ab6b-236">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-236">NA</span></span> |
| <span data-ttu-id="7ab6b-237">minimumRows</span><span class="sxs-lookup"><span data-stu-id="7ab6b-237">minimumRows</span></span> | <span data-ttu-id="7ab6b-238">**Azure SQL Database** 또는 **Azure 테이블**에서 데이터가 최소 행 수를 포함하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-238">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="7ab6b-239">Azure SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="7ab6b-239">Azure SQL Database</span></span></li><li><span data-ttu-id="7ab6b-240">Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="7ab6b-240">Azure Table</span></span></li></ul> |<span data-ttu-id="7ab6b-241">아니요</span><span class="sxs-lookup"><span data-stu-id="7ab6b-241">No</span></span> |<span data-ttu-id="7ab6b-242">해당 없음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-242">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="7ab6b-243">예</span><span class="sxs-lookup"><span data-stu-id="7ab6b-243">Examples</span></span>
<span data-ttu-id="7ab6b-244">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-244">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="7ab6b-245">**minimumRows**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-245">**minimumRows**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

<span data-ttu-id="7ab6b-246">이러한 속성과 예제에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-246">For more information about these properties and examples, see [Create datasets](data-factory-create-datasets.md) article.</span></span> 

## <a name="activity-policies"></a><span data-ttu-id="7ab6b-247">활동 정책</span><span class="sxs-lookup"><span data-stu-id="7ab6b-247">Activity policies</span></span>
<span data-ttu-id="7ab6b-248">정책은 특히 테이블의 조각을 처리할 때 활동의 런타임 동작에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-248">Policies affect the run-time behavior of an activity, specifically when the slice of a table is processed.</span></span> <span data-ttu-id="7ab6b-249">다음 테이블에서는 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-249">The following table provides the details.</span></span>

| <span data-ttu-id="7ab6b-250">속성</span><span class="sxs-lookup"><span data-stu-id="7ab6b-250">Property</span></span> | <span data-ttu-id="7ab6b-251">허용된 값</span><span class="sxs-lookup"><span data-stu-id="7ab6b-251">Permitted values</span></span> | <span data-ttu-id="7ab6b-252">기본값</span><span class="sxs-lookup"><span data-stu-id="7ab6b-252">Default Value</span></span> | <span data-ttu-id="7ab6b-253">설명</span><span class="sxs-lookup"><span data-stu-id="7ab6b-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7ab6b-254">동시성</span><span class="sxs-lookup"><span data-stu-id="7ab6b-254">concurrency</span></span> |<span data-ttu-id="7ab6b-255">정수 </span><span class="sxs-lookup"><span data-stu-id="7ab6b-255">Integer</span></span> <br/><br/><span data-ttu-id="7ab6b-256">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="7ab6b-256">Max value: 10</span></span> |<span data-ttu-id="7ab6b-257">1</span><span class="sxs-lookup"><span data-stu-id="7ab6b-257">1</span></span> |<span data-ttu-id="7ab6b-258">작업의 동시 실행 수입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-258">Number of concurrent executions of the activity.</span></span><br/><br/><span data-ttu-id="7ab6b-259">다른 조각에 발생할 수 있는 병렬 작업 실행 횟수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-259">It determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="7ab6b-260">예를 들어 활동이 사용 가능한 많은 데이터 집합을 거쳐야 하는 경우 동시성 값을 높이면 데이터 처리가 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-260">For example, if an activity needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> |
| <span data-ttu-id="7ab6b-261">executionPriorityOrder</span><span class="sxs-lookup"><span data-stu-id="7ab6b-261">executionPriorityOrder</span></span> |<span data-ttu-id="7ab6b-262">NewestFirst</span><span class="sxs-lookup"><span data-stu-id="7ab6b-262">NewestFirst</span></span><br/><br/><span data-ttu-id="7ab6b-263">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="7ab6b-263">OldestFirst</span></span> |<span data-ttu-id="7ab6b-264">OldestFirst</span><span class="sxs-lookup"><span data-stu-id="7ab6b-264">OldestFirst</span></span> |<span data-ttu-id="7ab6b-265">처리 중인 데이터 조각의 순서를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-265">Determines the ordering of data slices that are being processed.</span></span><br/><br/><span data-ttu-id="7ab6b-266">예를 들어 2개의 조각이 있으며(각각 오후 4시 및 오후 5시에 발생) 둘 다 실행 보류 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-266">For example, if you have 2 slices (one happening at 4pm, and another one at 5pm), and both are pending execution.</span></span> <span data-ttu-id="7ab6b-267">executionPriorityOrder를 설정하여 NewestFirst가 되도록 하면 오후 5시에 조각이 먼저 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-267">If you set the executionPriorityOrder to be NewestFirst, the slice at 5 PM is processed first.</span></span> <span data-ttu-id="7ab6b-268">마찬가지로 executionPriorityORder를 OldestFIrst로 설정하면 오후 4시의 조각이 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-268">Similarly if you set the executionPriorityORder to be OldestFIrst, then the slice at 4 PM is processed.</span></span> |
| <span data-ttu-id="7ab6b-269">retry</span><span class="sxs-lookup"><span data-stu-id="7ab6b-269">retry</span></span> |<span data-ttu-id="7ab6b-270">정수 </span><span class="sxs-lookup"><span data-stu-id="7ab6b-270">Integer</span></span><br/><br/><span data-ttu-id="7ab6b-271">최대값이 10이 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="7ab6b-271">Max value can be 10</span></span> |<span data-ttu-id="7ab6b-272">0</span><span class="sxs-lookup"><span data-stu-id="7ab6b-272">0</span></span> |<span data-ttu-id="7ab6b-273">조각에 대한 데이터 처리 전에 다시 시도 횟수가 실패로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-273">Number of retries before the data processing for the slice is marked as Failure.</span></span> <span data-ttu-id="7ab6b-274">데이터 조각에 대한 활동 실행은 지정된 재시도 횟수까지 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-274">Activity execution for a data slice is retried up to the specified retry count.</span></span> <span data-ttu-id="7ab6b-275">재시도는 실패 후 가능한 한 빨리 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-275">The retry is done as soon as possible after the failure.</span></span> |
| <span data-ttu-id="7ab6b-276">시간 제한</span><span class="sxs-lookup"><span data-stu-id="7ab6b-276">timeout</span></span> |<span data-ttu-id="7ab6b-277">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7ab6b-277">TimeSpan</span></span> |<span data-ttu-id="7ab6b-278">00:00:00</span><span class="sxs-lookup"><span data-stu-id="7ab6b-278">00:00:00</span></span> |<span data-ttu-id="7ab6b-279">활동에 대한 시간 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-279">Timeout for the activity.</span></span> <span data-ttu-id="7ab6b-280">예: 00:10:00(시간 제한 10분을 의미함)</span><span class="sxs-lookup"><span data-stu-id="7ab6b-280">Example: 00:10:00 (implies timeout 10 mins)</span></span><br/><br/><span data-ttu-id="7ab6b-281">값이 지정되지 않거나 0인 경우 시간 제한은 무한입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-281">If a value is not specified or is 0, the timeout is infinite.</span></span><br/><br/><span data-ttu-id="7ab6b-282">조각의 데이터 처리 시간이 시간 제한 값을 초과하면 취소되고 시스템이 처리를 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-282">If the data processing time on a slice exceeds the timeout value, it is canceled, and the system attempts to retry the processing.</span></span> <span data-ttu-id="7ab6b-283">다시 시도 횟수는 다시 시도 속성에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-283">The number of retries depends on the retry property.</span></span> <span data-ttu-id="7ab6b-284">시간 제한이 발생할 때 상태는 TimedOut으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-284">When timeout occurs, the status is set to TimedOut.</span></span> |
| <span data-ttu-id="7ab6b-285">delay</span><span class="sxs-lookup"><span data-stu-id="7ab6b-285">delay</span></span> |<span data-ttu-id="7ab6b-286">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7ab6b-286">TimeSpan</span></span> |<span data-ttu-id="7ab6b-287">00:00:00</span><span class="sxs-lookup"><span data-stu-id="7ab6b-287">00:00:00</span></span> |<span data-ttu-id="7ab6b-288">조각의 데이터 처리 작업이 시작되기 전에 지연을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-288">Specify the delay before data processing of the slice starts.</span></span><br/><br/><span data-ttu-id="7ab6b-289">데이터 조각에 대한 활동의 실행은 지연이 예상된 실행 시간을 지난 후에 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-289">The execution of activity for a data slice is started after the Delay is past the expected execution time.</span></span><br/><br/><span data-ttu-id="7ab6b-290">예: 00:10:00(10분의 지연을 의미함)</span><span class="sxs-lookup"><span data-stu-id="7ab6b-290">Example: 00:10:00 (implies delay of 10 mins)</span></span> |
| <span data-ttu-id="7ab6b-291">longRetry</span><span class="sxs-lookup"><span data-stu-id="7ab6b-291">longRetry</span></span> |<span data-ttu-id="7ab6b-292">정수 </span><span class="sxs-lookup"><span data-stu-id="7ab6b-292">Integer</span></span><br/><br/><span data-ttu-id="7ab6b-293">최대값: 10</span><span class="sxs-lookup"><span data-stu-id="7ab6b-293">Max value: 10</span></span> |<span data-ttu-id="7ab6b-294">1</span><span class="sxs-lookup"><span data-stu-id="7ab6b-294">1</span></span> |<span data-ttu-id="7ab6b-295">조각 실행이 실패하기 전까지의 긴 재시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-295">The number of long retry attempts before the slice execution is failed.</span></span><br/><br/><span data-ttu-id="7ab6b-296">longRetry 시도는 longRetryInterval에 따라 간격이 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-296">longRetry attempts are spaced by longRetryInterval.</span></span> <span data-ttu-id="7ab6b-297">따라서 재시도 간의 시간을 지정해야 하는 경우 longRetry를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-297">So if you need to specify a time between retry attempts, use longRetry.</span></span> <span data-ttu-id="7ab6b-298">Retry 및 longRetry를 둘 다 지정하면 각 longRetry 시도에는 Retry 시도가 포함되고 최대 시도 횟수는 Retry * longRetry가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-298">If both Retry and longRetry are specified, each longRetry attempt includes Retry attempts and the max number of attempts is Retry * longRetry.</span></span><br/><br/><span data-ttu-id="7ab6b-299">예를 들어 활동 정책에 다음 설정이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="7ab6b-299">For example, if we have the following settings in the activity policy:</span></span><br/><span data-ttu-id="7ab6b-300">Retry: 3</span><span class="sxs-lookup"><span data-stu-id="7ab6b-300">Retry: 3</span></span><br/><span data-ttu-id="7ab6b-301">longRetry: 2</span><span class="sxs-lookup"><span data-stu-id="7ab6b-301">longRetry: 2</span></span><br/><span data-ttu-id="7ab6b-302">longRetryInterval: 01:00:00</span><span class="sxs-lookup"><span data-stu-id="7ab6b-302">longRetryInterval: 01:00:00</span></span><br/><br/><span data-ttu-id="7ab6b-303">실행할 조각이 하나뿐이며(Waiting 상태) 작업 실행이 매번 실패한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-303">Assume there is only one slice to execute (status is Waiting) and the activity execution fails every time.</span></span> <span data-ttu-id="7ab6b-304">우선 3번 연속 실행 시도를 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-304">Initially there would be 3 consecutive execution attempts.</span></span> <span data-ttu-id="7ab6b-305">시도한 후 각 조각 상태는 다시 시도입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-305">After each attempt, the slice status would be Retry.</span></span> <span data-ttu-id="7ab6b-306">처음 3번 시도 후에 조각 상태는 LongRetry입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-306">After first 3 attempts are over, the slice status would be LongRetry.</span></span><br/><br/><span data-ttu-id="7ab6b-307">한 시간(즉, longRetryInteval의 값) 후에 3번 연속 실행이 다시 시도됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-307">After an hour (that is, longRetryInteval’s value), there would be another set of 3 consecutive execution attempts.</span></span> <span data-ttu-id="7ab6b-308">그 후에 조각 상태가 실패이면 다시 시도는 더 이상 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-308">After that, the slice status would be Failed and no more retries would be attempted.</span></span> <span data-ttu-id="7ab6b-309">즉, 전체적으로 6번의 시도가 일어납니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-309">Hence overall 6 attempts were made.</span></span><br/><br/><span data-ttu-id="7ab6b-310">모든 실행에 성공하면 조각 상태는 준비 상태가 되며 더 이상 다시 시도하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-310">If any execution succeeds, the slice status would be Ready and no more retries are attempted.</span></span><br/><br/><span data-ttu-id="7ab6b-311">longRetry는 종속 데이터가 명확하지 않은 시간에 도착하거나 데이터 처리가 발생하는 전체적인 환경을 신뢰할 수 없는 상황에서 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-311">longRetry may be used in situations where dependent data arrives at non-deterministic times or the overall environment is flaky under which data processing occurs.</span></span> <span data-ttu-id="7ab6b-312">이러한 경우 하나씩 다시 시도를 수행해도 도움이 되지 않을 수 있으며 특정 시간 간격 후에 시도할 경우 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-312">In such cases, doing retries one after another may not help and doing so after an interval of time results in the desired output.</span></span><br/><br/><span data-ttu-id="7ab6b-313">주의: longRetry 또는 longRetryInterval에 높은 값을 설정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-313">Word of caution: do not set high values for longRetry or longRetryInterval.</span></span> <span data-ttu-id="7ab6b-314">일반적으로 더 높은 값을 지정하면 다른 시스템 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-314">Typically, higher values imply other systemic issues.</span></span> |
| <span data-ttu-id="7ab6b-315">longRetryInterval</span><span class="sxs-lookup"><span data-stu-id="7ab6b-315">longRetryInterval</span></span> |<span data-ttu-id="7ab6b-316">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="7ab6b-316">TimeSpan</span></span> |<span data-ttu-id="7ab6b-317">00:00:00</span><span class="sxs-lookup"><span data-stu-id="7ab6b-317">00:00:00</span></span> |<span data-ttu-id="7ab6b-318">긴 다시 시도 간의 지연</span><span class="sxs-lookup"><span data-stu-id="7ab6b-318">The delay between long retry attempts</span></span> |

<span data-ttu-id="7ab6b-319">자세한 내용은 [파이프라인](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-319">For more information, see [Pipelines](data-factory-create-pipelines.md) article.</span></span> 

## <a name="parallel-processing-of-data-slices"></a><span data-ttu-id="7ab6b-320">데이터 조각의 병렬 처리</span><span class="sxs-lookup"><span data-stu-id="7ab6b-320">Parallel processing of data slices</span></span>
<span data-ttu-id="7ab6b-321">파이프라인에 대해 과거의 시작 날짜를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-321">You can set the start date for the pipeline in the past.</span></span> <span data-ttu-id="7ab6b-322">이렇게 하면 Data Factory에서 과거의 모든 데이터 조각을 자동으로 계산(뒤 채우기)하고 처리를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-322">When you do so, Data Factory automatically calculates (back fills) all data slices in the past and begins processing them.</span></span> <span data-ttu-id="7ab6b-323">예를 들어 시작 날짜가 2017년 4월 1일이고 현재 날짜가 2017년 4월 10일인 파이프라인을 만드는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-323">For example: if you create a pipeline with start date 2017-04-01 and the current date is 2017-04-10.</span></span> <span data-ttu-id="7ab6b-324">출력 데이터 집합의 빈도가 매일이면 시작 날짜가 과거이므로 Data Factory에서 2017년 4월 1일에서 2017년 4월 9일까지의 모든 조각을 즉시 처리하기 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-324">If the cadence of the output dataset is daily, then Data Factory starts processing all the slices from 2017-04-01 to 2017-04-09 immediately because the start date is in the past.</span></span> <span data-ttu-id="7ab6b-325">availability 섹션의 style 속성 값은 기본적으로 EndOfInterval이므로 2017년 4월 10일의 조각은 아직 처리되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-325">The slice from 2017-04-10 is not processed yet because the value of style property in the availability section is EndOfInterval by default.</span></span> <span data-ttu-id="7ab6b-326">executionPriorityOrder의 기본값이 OldestFirst이므로 가장 오래된 조각이 먼저 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-326">The oldest slice is processed first as the default value of executionPriorityOrder is OldestFirst.</span></span> <span data-ttu-id="7ab6b-327">style 속성에 대한 내용은 [데이터 집합 가용성](#dataset-availability) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-327">For a description of the style property, see [dataset availability](#dataset-availability) section.</span></span> <span data-ttu-id="7ab6b-328">executionPriorityOrder 섹션에 대한 내용은 [활동 정책](#activity-policies) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-328">For a description of the executionPriorityOrder section, see the [activity policies](#activity-policies) section.</span></span> 

<span data-ttu-id="7ab6b-329">활동 JSON의 **policy** 섹션에서 **concurrency** 속성을 설정하여 뒷면 채우기된 데이터 조각을 병렬로 처리하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-329">You can configure back-filled data slices to be processed in parallel by setting the **concurrency** property in the **policy** section of the activity JSON.</span></span> <span data-ttu-id="7ab6b-330">이 속성은 여러 조각에 발생할 수 있는 병렬 활동 실행 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-330">This property determines the number of parallel activity executions that can happen on different slices.</span></span> <span data-ttu-id="7ab6b-331">concurrency 속성의 기본값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-331">The default value for the concurrency property is 1.</span></span> <span data-ttu-id="7ab6b-332">따라서 기본적으로 조각이 한 번에 하나씩 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-332">Therefore, one slice is processed at a time by default.</span></span> <span data-ttu-id="7ab6b-333">최대값은 10입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-333">The maximum value is 10.</span></span> <span data-ttu-id="7ab6b-334">파이프라인이 사용 가능한 많은 데이터 집합을 거쳐야 하는 경우 concurrency 값을 높이면 데이터 처리가 더 빨라집니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-334">When a pipeline needs to go through a large set of available data, having a larger concurrency value speeds up the data processing.</span></span> 

## <a name="rerun-a-failed-data-slice"></a><span data-ttu-id="7ab6b-335">실패한 데이터 조각 다시 실행</span><span class="sxs-lookup"><span data-stu-id="7ab6b-335">Rerun a failed data slice</span></span>
<span data-ttu-id="7ab6b-336">데이터 조각을 처리하는 동안 오류가 발생하면 Azure Portal 블레이드 또는 모니터 및 관리 앱을 사용하여 조각 처리가 실패한 이유를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-336">When an error occurs while processing a data slice, you can find out why the processing of a slice failed by using Azure portal blades or Monitor and Manage App.</span></span> <span data-ttu-id="7ab6b-337">자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 또는 [앱 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-337">See [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md) for details.</span></span>

<span data-ttu-id="7ab6b-338">두 활동을 보여주는 다음 예제를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-338">Consider the following example, which shows two activities.</span></span> <span data-ttu-id="7ab6b-339">활동 1 및 활동 2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-339">Activity1 and Activity 2.</span></span> <span data-ttu-id="7ab6b-340">활동 1은 데이터 집합 1 조각을 사용하고 데이터 집합 2 조각을 생성합니다. 활동 2에서는 입력으로 데이터 집합 2 조각을 사용하여 최종 데이터 집합의 조각을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-340">Activity1 consumes a slice of Dataset1 and produces a slice of Dataset2, which is consumed as an input by Activity2 to produce a slice of the Final Dataset.</span></span>

![실패한 조각](./media/data-factory-scheduling-and-execution/failed-slice.png)

<span data-ttu-id="7ab6b-342">다이어그램은 최근 3개 조각 중 데이터 집합 2에 대한 오전 9-10시 조각을 생성하는 데 오류가 있음을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-342">The diagram shows that out of three recent slices, there was a failure producing the 9-10 AM slice for Dataset2.</span></span> <span data-ttu-id="7ab6b-343">Data Factory는 시계열 데이터 집합에 대한 종속성을 자동으로 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-343">Data Factory automatically tracks dependency for the time series dataset.</span></span> <span data-ttu-id="7ab6b-344">따라서 오전 9-10시 다운스트림 조각에 대한 작업 실행은 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-344">As a result, it does not start the activity run for the 9-10 AM downstream slice.</span></span>

<span data-ttu-id="7ab6b-345">Data Factory 모니터링 및 관리 도구를 사용하면 실패한 조각에 대한 진단 로그를 자세히 보고 문제에 대한 근본 원인을 쉽게 파악하여 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-345">Data Factory monitoring and management tools allow you to drill into the diagnostic logs for the failed slice to easily find the root cause for the issue and fix it.</span></span> <span data-ttu-id="7ab6b-346">문제를 해결했으면 작업 실행을 쉽게 시작하여 실패한 조각을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-346">After you have fixed the issue, you can easily start the activity run to produce the failed slice.</span></span> <span data-ttu-id="7ab6b-347">데이터 조각의 상태 전환을 다시 실행하고 이해하는 방법에 대한 자세한 내용은 [Azure Portal 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 또는 [앱 모니터링 및 관리 앱](data-factory-monitor-manage-app.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-347">For more information on how to rerun and understand state transitions for data slices, see [Monitoring and managing pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) or [Monitoring and Management app](data-factory-monitor-manage-app.md).</span></span>

<span data-ttu-id="7ab6b-348">**Dataset2**에 대한 오전 9-10시 조각을 다시 실행한 후 Data Factory는 최종 데이터 집합에서 오전 9-10시 종속 조각에 대한 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-348">After you rerun the 9-10 AM slice for **Dataset2**, Data Factory starts the run for the 9-10 AM dependent slice on the final dataset.</span></span>

![실패한 조각 다시 실행](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a><span data-ttu-id="7ab6b-350">파이프라인의 여러 활동</span><span class="sxs-lookup"><span data-stu-id="7ab6b-350">Multiple activities in a pipeline</span></span>
<span data-ttu-id="7ab6b-351">그렇지만 하나의 파이프라인에 여러 개의 활동이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-351">You can have more than one activity in a pipeline.</span></span> <span data-ttu-id="7ab6b-352">파이프라인에 여러 활동이 있고 활동의 출력이 다른 활동의 입력이 아닌 경우, 해당 활동에 대한 입력 데이터 조각이 준비되면 활동을 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-352">If you have multiple activities in a pipeline and the output of an activity is not an input of another activity, the activities may run in parallel if input data slices for the activities are ready.</span></span>

<span data-ttu-id="7ab6b-353">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정하여 두 활동을 연결하면 해당 활동을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-353">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="7ab6b-354">활동은 동일한 파이프라인 또는 다른 파이프라인에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-354">The activities can be in the same pipeline or in different pipelines.</span></span> <span data-ttu-id="7ab6b-355">두 번째 활동은 첫 번째 활동이 완료된 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-355">The second activity executes only when the first one finishes successfully.</span></span>

<span data-ttu-id="7ab6b-356">예를 들어 파이프라인에 다음 두 활동이 있는 경우를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-356">For example, consider the following case where a pipeline has two activities:</span></span>

1. <span data-ttu-id="7ab6b-357">외부 입력 데이터 집합 D1이 필요하고 출력 데이터 집합 D2를 생성하는 활동 A1</span><span class="sxs-lookup"><span data-stu-id="7ab6b-357">Activity A1 that requires external input dataset D1, and produces output dataset D2.</span></span>
2. <span data-ttu-id="7ab6b-358">데이터 집합 D2로부터의 입력이 필요하고 출력 데이터 집합 D3을 생성하는 활동 A2</span><span class="sxs-lookup"><span data-stu-id="7ab6b-358">Activity A2 that requires input from dataset D2, and produces output dataset D3.</span></span>

<span data-ttu-id="7ab6b-359">이 시나리오에서는 활동 A1과 A2가 동일한 파이프라인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-359">In this scenario, activities A1 and A2 are in the same pipeline.</span></span> <span data-ttu-id="7ab6b-360">활동 A1은 외부 데이터를 사용할 수 있고 예약된 가용성 빈도에 도달할 때 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-360">The activity A1 runs when the external data is available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="7ab6b-361">활동 A2는 D2에서 예약된 조각을 사용할 수 있고 예약된 가용성 빈도에 도달할 때 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-361">The activity A2 runs when the scheduled slices from D2 become available and the scheduled availability frequency is reached.</span></span> <span data-ttu-id="7ab6b-362">데이터 집합 D2의 조각 중 하나에 오류가 있으면 해당 조각을 사용할 수 있을 때까지 A2가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-362">If there is an error in one of the slices in dataset D2, A2 does not run for that slice until it becomes available.</span></span>

<span data-ttu-id="7ab6b-363">동일한 파이프라인에서 두 활동을 사용하는 다이어그램 뷰는 다음 다이어그램과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-363">The Diagram view with both activities in the same pipeline would look like the following diagram:</span></span>

![동일한 파이프라인에서 활동 연결](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

<span data-ttu-id="7ab6b-365">앞에서 설명한 대로 활동은 다른 파이프라인에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-365">As mentioned earlier, the activities could be in different pipelines.</span></span> <span data-ttu-id="7ab6b-366">이러한 시나리오의 다이어그램은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-366">In such a scenario, the diagram view would look like the following diagram:</span></span>

![두 개의 파이프라인에서 활동 연결](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

<span data-ttu-id="7ab6b-368">예제는 부록의 [순차적으로 복사](#copy-sequentially) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-368">See the [copy sequentially](#copy-sequentially) section in the appendix for an example.</span></span>

## <a name="model-datasets-with-different-frequencies"></a><span data-ttu-id="7ab6b-369">다양한 빈도로 데이터 집합 모델링</span><span class="sxs-lookup"><span data-stu-id="7ab6b-369">Model datasets with different frequencies</span></span>
<span data-ttu-id="7ab6b-370">샘플에서 입력 및 출력 데이터 집합과 작업 일정 창에 대한 빈도는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-370">In the samples, the frequencies for input and output datasets and the activity schedule window were the same.</span></span> <span data-ttu-id="7ab6b-371">일부 시나리오에서는 하나 이상의 입력 빈도와 다른 빈도로 출력을 생성하는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-371">Some scenarios require the ability to produce output at a frequency different than the frequencies of one or more inputs.</span></span> <span data-ttu-id="7ab6b-372">Data Factory가 이러한 시나리오의 모델링을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-372">Data Factory supports modeling these scenarios.</span></span>

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a><span data-ttu-id="7ab6b-373">샘플 1: 매시간 제공되는 입력 데이터에 대해 일별 출력 보고서 생성</span><span class="sxs-lookup"><span data-stu-id="7ab6b-373">Sample 1: Produce a daily output report for input data that is available every hour</span></span>
<span data-ttu-id="7ab6b-374">Azure Blob 저장소에서 매시간 사용 가능한 센서로부터 입력 측정값 데이터가 있는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-374">Consider a scenario in which you have input measurement data from sensors available every hour in Azure Blob storage.</span></span> <span data-ttu-id="7ab6b-375">[Data Factory hive 작업](data-factory-hive-activity.md)을 사용하여 평균, 최대값, 최소값 등 특정일의 통계가 포함된 일별 집계 보고서를 생성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-375">You want to produce a daily aggregate report with statistics such as mean, maximum, and minimum for the day with [Data Factory hive activity](data-factory-hive-activity.md).</span></span>

<span data-ttu-id="7ab6b-376">다음은 Data Factory로 이 시나리오를 모델링하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-376">Here is how you can model this scenario with Data Factory:</span></span>

<span data-ttu-id="7ab6b-377">**입력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-377">**Input dataset**</span></span>

<span data-ttu-id="7ab6b-378">매시간 입력 파일이 지정된 날에 대한 폴더에서 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-378">The hourly input files are dropped in the folder for the given day.</span></span> <span data-ttu-id="7ab6b-379">입력에 대한 Availability가 **Hour** 로 설정됩니다(frequency: Hour, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-379">Availability for input is set at **Hour** (frequency: Hour, interval: 1).</span></span>

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
<span data-ttu-id="7ab6b-380">**출력 데이터 집합**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-380">**Output dataset**</span></span>

<span data-ttu-id="7ab6b-381">하나의 출력 파일이 그 날에 대한 폴더에서 매일 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-381">One output file is created every day in the day's folder.</span></span> <span data-ttu-id="7ab6b-382">출력의 Availability는 **Day** 로 설정됩니다(frequency: Day 및 interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-382">Availability of output is set at **Day** (frequency: Day and interval: 1).</span></span>

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

<span data-ttu-id="7ab6b-383">**작업: 파이프라인에서 hive 작업**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-383">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="7ab6b-384">hive 스크립트는 적절한 *DateTime* 정보를 매개 변수로 받아 **WindowStart** 변수를 다음 코드 조각에 표시된 대로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-384">The hive script receives the appropriate *DateTime* information as parameters that use the **WindowStart** variable as shown in the following snippet.</span></span> <span data-ttu-id="7ab6b-385">hive 스크립트는 이 변수를 사용하여 그 날의 정확한 폴더에서 데이터를 로드하고 집계를 실행하여 출력을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-385">The hive script uses this variable to load the data from the correct folder for the day and run the aggregation to generate the output.</span></span>

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

<span data-ttu-id="7ab6b-386">다음 다이어그램은 데이터 종속성 관점에서 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-386">The following diagram shows the scenario from a data-dependency point of view.</span></span>

![데이터 종속성](./media/data-factory-scheduling-and-execution/data-dependency.png)

<span data-ttu-id="7ab6b-388">매일 출력 조각은 입력 데이터 집합에서 24시간 조각에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-388">The output slice for every day depends on 24 hourly slices from an input dataset.</span></span> <span data-ttu-id="7ab6b-389">Data Factory는 동일한 기간에 속하는 입력 데이터 조각을 생성할 출력 조각으로 파악하여 이러한 종속성을 자동으로 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-389">Data Factory computes these dependencies automatically by figuring out the input data slices that fall in the same time period as the output slice to be produced.</span></span> <span data-ttu-id="7ab6b-390">24개의 입력 조각 모두를 사용할 수 없는 경우 Data Factory는 입력 조각이 준비될 때까지 기다렸다가 일별 작업 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-390">If any of the 24 input slices is not available, Data Factory waits for the input slice to be ready before starting the daily activity run.</span></span>

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a><span data-ttu-id="7ab6b-391">샘플 2: 식 및 데이터 Data Factory 함수로 종속성 지정</span><span class="sxs-lookup"><span data-stu-id="7ab6b-391">Sample 2: Specify dependency with expressions and Data Factory functions</span></span>
<span data-ttu-id="7ab6b-392">다른 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-392">Let’s consider another scenario.</span></span> <span data-ttu-id="7ab6b-393">두 개의 입력 데이터 집합을 처리하는 hive 작업이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-393">Suppose you have a hive activity that processes two input datasets.</span></span> <span data-ttu-id="7ab6b-394">그 중 하나는 매일 새 데이터가 제공되지만 다른 하나는 매주 새 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-394">One of them has new data daily, but one of them gets new data every week.</span></span> <span data-ttu-id="7ab6b-395">두 입력에 조인을 수행하여 매일 출력을 생성하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-395">Suppose you wanted to do a join across the two inputs and produce an output every day.</span></span>

<span data-ttu-id="7ab6b-396">Data Factory가 출력 데이터 조각의 기간에 맞추어 처리할 적절한 입력 조각을 자동으로 확인하는 단순한 접근법은 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-396">The simple approach in which Data Factory automatically figures out the right input slices to process by aligning to the output data slice’s time period does not work.</span></span>

<span data-ttu-id="7ab6b-397">모든 작업 실행에 대해 지정해야 하며 Data Factory에서 매주 입력 데이터 집합에 대해 마지막 주의 데이터 조각을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-397">You must specify that for every activity run, the Data Factory should use last week’s data slice for the weekly input dataset.</span></span> <span data-ttu-id="7ab6b-398">다음 코드 조각에 나와 있는 것처럼 Azure Data Factory 함수를 사용하여 이 동작을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-398">You use Azure Data Factory functions as shown in the following snippet to implement this behavior.</span></span>

<span data-ttu-id="7ab6b-399">**입력1: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-399">**Input1: Azure blob**</span></span>

<span data-ttu-id="7ab6b-400">첫 번째 입력은 매일 업데이트된 Azure Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-400">The first input is the Azure blob being updated daily.</span></span>

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

<span data-ttu-id="7ab6b-401">**입력2: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-401">**Input2: Azure blob**</span></span>

<span data-ttu-id="7ab6b-402">입력2는 매주 업데이트된 Azure Blob입니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-402">Input2 is the Azure blob being updated weekly.</span></span>

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

<span data-ttu-id="7ab6b-403">**출력: Azure Blob**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-403">**Output: Azure blob**</span></span>

<span data-ttu-id="7ab6b-404">하나의 출력 파일이 그 날에 대한 폴더에서 매일 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-404">One output file is created every day in the folder for the day.</span></span> <span data-ttu-id="7ab6b-405">출력의 Availability는 **day** 로 설정됩니다(frequency: Day, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="7ab6b-405">Availability of output is set to **day** (frequency: Day, interval: 1).</span></span>

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

<span data-ttu-id="7ab6b-406">**작업: 파이프라인에서 hive 작업**</span><span class="sxs-lookup"><span data-stu-id="7ab6b-406">**Activity: hive activity in a pipeline**</span></span>

<span data-ttu-id="7ab6b-407">hive 작업에서는 2개의 입력을 받아 매일 출력 조각을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-407">The hive activity takes the two inputs and produces an output slice every day.</span></span> <span data-ttu-id="7ab6b-408">다음과 같이 매주 입력에 대한 이전 주의 입력 조각에 따라 매일 출력 조각을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-408">You can specify every day’s output slice to depend on the previous week’s input slice for weekly input as follows.</span></span>

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

<span data-ttu-id="7ab6b-409">Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-409">See [Data Factory functions and system variables](data-factory-functions-variables.md) for a list of functions and system variables that Data Factory supports.</span></span>

## <a name="appendix"></a><span data-ttu-id="7ab6b-410">부록</span><span class="sxs-lookup"><span data-stu-id="7ab6b-410">Appendix</span></span>

### <a name="example-copy-sequentially"></a><span data-ttu-id="7ab6b-411">예제: 순차적으로 복사</span><span class="sxs-lookup"><span data-stu-id="7ab6b-411">Example: copy sequentially</span></span>
<span data-ttu-id="7ab6b-412">순차/순서가 지정된 방식으로 하나씩 여러 복사 작업을 실행하는 것이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-412">It is possible to run multiple copy operations one after another in a sequential/ordered manner.</span></span> <span data-ttu-id="7ab6b-413">예를 들어 파이프라인에 두 개의 복사 활동, 즉 다음과 같은 입력 데이터 및 출력 데이터 집합을 포함하는 CopyActivity1과 CopyActivity2가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-413">For example, you might have two copy activities in a pipeline (CopyActivity1 and CopyActivity2) with the following input data output datasets:</span></span>   

<span data-ttu-id="7ab6b-414">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="7ab6b-414">CopyActivity1</span></span>

<span data-ttu-id="7ab6b-415">입력: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-415">Input: Dataset.</span></span> <span data-ttu-id="7ab6b-416">출력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-416">Output: Dataset2.</span></span>

<span data-ttu-id="7ab6b-417">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="7ab6b-417">CopyActivity2</span></span>

<span data-ttu-id="7ab6b-418">입력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-418">Input: Dataset2.</span></span>  <span data-ttu-id="7ab6b-419">출력: Dataset3.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-419">Output: Dataset3.</span></span>

<span data-ttu-id="7ab6b-420">CopyActivity2는 CopyActivity1을 성공적으로 실행하고 Dataset2를 사용할 수 있는 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-420">CopyActivity2 would run only if the CopyActivity1 has run successfully and Dataset2 is available.</span></span>

<span data-ttu-id="7ab6b-421">샘플 파이프라인 JSON은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-421">Here is the sample pipeline JSON:</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="7ab6b-422">예제에서는 첫 번째 복사 활동의 출력 데이터 집합(Dataset2)이 두 번째 활동의 입력으로 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-422">Notice that in the example, the output dataset of the first copy activity (Dataset2) is specified as input for the second activity.</span></span> <span data-ttu-id="7ab6b-423">따라서 첫 번째 활동의 출력 데이터 집합이 준비되어야 두 번째 활동이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-423">Therefore, the second activity runs only when the output dataset from the first activity is ready.</span></span>  

<span data-ttu-id="7ab6b-424">예제에서 CopyActivity2에 다른 입력(예: Dataset3)을 지정할 수 있지만 CopyActivity2에 대한 입력으로 Dataset2를 지정해야 CopyActivity1을 끝낼 때까지 작업이 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-424">In the example, CopyActivity2 can have a different input, such as Dataset3, but you specify Dataset2 as an input to CopyActivity2, so the activity does not run until CopyActivity1 finishes.</span></span> <span data-ttu-id="7ab6b-425">예:</span><span class="sxs-lookup"><span data-stu-id="7ab6b-425">For example:</span></span>

<span data-ttu-id="7ab6b-426">CopyActivity1</span><span class="sxs-lookup"><span data-stu-id="7ab6b-426">CopyActivity1</span></span>

<span data-ttu-id="7ab6b-427">입력: Dataset1.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-427">Input: Dataset1.</span></span> <span data-ttu-id="7ab6b-428">출력: Dataset2.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-428">Output: Dataset2.</span></span>

<span data-ttu-id="7ab6b-429">CopyActivity2</span><span class="sxs-lookup"><span data-stu-id="7ab6b-429">CopyActivity2</span></span>

<span data-ttu-id="7ab6b-430">입력: Dataset3, Dataset2.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-430">Inputs: Dataset3, Dataset2.</span></span> <span data-ttu-id="7ab6b-431">출력: Dataset4.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-431">Output: Dataset4.</span></span>

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
                "description": "Copy data from a blob to another"
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
                "description": "Copy data from a blob to another"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="7ab6b-432">예제에서는 두 번째 복사 활동에 대해 입력 데이터 집합 두 개가 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-432">Notice that in the example, two input datasets are specified for the second copy activity.</span></span> <span data-ttu-id="7ab6b-433">여러 입력을 지정하는 경우 첫 번째 입력 데이터 집합만 데이터를 복사하는 데 사용되고 다른 데이터 집합은 종속성으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-433">When multiple inputs are specified, only the first input dataset is used for copying data, but other datasets are used as dependencies.</span></span> <span data-ttu-id="7ab6b-434">CopyActivity2는 다음 조건을 충족한 후에만 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-434">CopyActivity2 would start only after the following conditions are met:</span></span>

* <span data-ttu-id="7ab6b-435">CopyActivity1이 성공적으로 완료되고 Dataset2가 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-435">CopyActivity1 has successfully completed and Dataset2 is available.</span></span> <span data-ttu-id="7ab6b-436">이 데이터 집합은 Dataset4에 데이터를 복사할 때 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-436">This dataset is not used when copying data to Dataset4.</span></span> <span data-ttu-id="7ab6b-437">CopyActivity2에 대한 일정 종속성으로만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-437">It only acts as a scheduling dependency for CopyActivity2.</span></span>   
* <span data-ttu-id="7ab6b-438">Dataset3을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-438">Dataset3 is available.</span></span> <span data-ttu-id="7ab6b-439">이 데이터 집합은 대상에 복사되는 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7ab6b-439">This dataset represents the data that is copied to the destination.</span></span> 