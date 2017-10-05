---
title: "Azure IoT Hub 작업 이해 | Microsoft 문서"
description: "개발자 가이드 - IoT 허브에 연결된 여러 장치에서 실행할 작업 예약 작업은 태그와 원하는 속성을 업데이트하고 여러 장치에서 직접 메서드를 호출할 수 있습니다."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="fae28-104">여러 장치에서 작업 예약</span><span class="sxs-lookup"><span data-stu-id="fae28-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="fae28-105">개요</span><span class="sxs-lookup"><span data-stu-id="fae28-105">Overview</span></span>
<span data-ttu-id="fae28-106">이전 문서에 설명된 대로, Azure IoT Hub를 통해 다양한 구성 요소([장치 쌍 속성 및 태그][lnk-twin-devguide] 및 [직접 메서드][lnk-dev-methods])를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="fae28-107">일반적으로, 백 엔드 앱을 사용하면 장치 관리자와 운영자는 IoT 장치를 대량으로 예약된 시간에 업데이트하고 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="fae28-108">작업은 예약된 시간에 장치 집합에 대해 장치 쌍 업데이트 및 직접 메서드를 실행하는 것을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="fae28-109">예를 들어 운영자는 빌딩 운영에 지장을 주지 않는 시간에 빌딩 43 및 3층에서 장치 집합을 재부팅하기 위해 작업을 시작 및 추적하는 백 엔드 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="fae28-110">사용하는 경우</span><span class="sxs-lookup"><span data-stu-id="fae28-110">When to use</span></span>
<span data-ttu-id="fae28-111">솔루션 백 엔드가 장치 집합에서 다음 작업을 예약하고 진행 상태를 추적해야 하는 경우 작업을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="fae28-112">desired 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="fae28-112">Update desired properties</span></span>
* <span data-ttu-id="fae28-113">tags 업데이트</span><span class="sxs-lookup"><span data-stu-id="fae28-113">Update tags</span></span>
* <span data-ttu-id="fae28-114">직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="fae28-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="fae28-115">작업 수명 주기</span><span class="sxs-lookup"><span data-stu-id="fae28-115">Job lifecycle</span></span>
<span data-ttu-id="fae28-116">작업은 솔루션 백 엔드에 의해 시작되고 IoT Hub에 의해 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="fae28-117">서비스 지향 URI(`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`)를 통해 작업을 시작하고 서비스 지향 URI(`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`)를 통해 작업 실행 진행 상태를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="fae28-118">작업이 시작된 후에는 작업 쿼리를 통해 백 엔드 앱에서 실행 중인 작업의 상태를 새로 고칠 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="fae28-119">작업을 시작할 때 속성 이름과 값은 US-ASCII로 출력 가능한 영숫자만 포함할 수 있으며 다음 집합은 제외됩니다. ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``</span><span class="sxs-lookup"><span data-stu-id="fae28-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="fae28-120">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="fae28-120">Reference topics:</span></span>
<span data-ttu-id="fae28-121">다음 참조 항목에서는 작업 사용에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="fae28-122">직접 메서드를 실행할 작업</span><span class="sxs-lookup"><span data-stu-id="fae28-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="fae28-123">작업을 사용하여 장치 집합에서 [직접 메서드][lnk-dev-methods]를 실행하기 위한 HTTP 1.1 요청 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="fae28-124">쿼리 조건은 아래와 같이 단일 장치 ID 또는 장치 ID 목록에 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="fae28-125">**예**</span><span class="sxs-lookup"><span data-stu-id="fae28-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="fae28-126">[IoT Hub 쿼리 언어][lnk-query]는 추가 세부 정보에서 IoT Hub 쿼리 언어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="fae28-127">장치 쌍 속성을 업데이트하는 작업</span><span class="sxs-lookup"><span data-stu-id="fae28-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="fae28-128">작업을 사용하여 장치 쌍 속성을 업데이트하는 HTTP 1.1 요청 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="fae28-129">작업 진행 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="fae28-129">Querying for progress on jobs</span></span>
<span data-ttu-id="fae28-130">[작업 쿼리][lnk-query]를 위한 HTTP 1.1 요청 세부 정보는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="fae28-131">응답에서 continuationToken이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="fae28-132">작업 속성</span><span class="sxs-lookup"><span data-stu-id="fae28-132">Jobs Properties</span></span>
<span data-ttu-id="fae28-133">작업 또는 작업 결과를 쿼리할 때 사용할 수 있는 속성 목록 및 해당 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="fae28-134">속성</span><span class="sxs-lookup"><span data-stu-id="fae28-134">Property</span></span> | <span data-ttu-id="fae28-135">설명</span><span class="sxs-lookup"><span data-stu-id="fae28-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fae28-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="fae28-136">**jobId**</span></span> |<span data-ttu-id="fae28-137">작업에 대해 응용 프로그램에서 제공한 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="fae28-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="fae28-138">**startTime**</span></span> |<span data-ttu-id="fae28-139">작업에 대해 응용 프로그램에서 제공한 시작 시간(ISO-8601)입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="fae28-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="fae28-140">**endTime**</span></span> |<span data-ttu-id="fae28-141">작업이 완료될 때 IoT Hub에서 제공한 날짜(ISO-8601)입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="fae28-142">작업이 '완료됨' 상태에 도달한 후에만 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="fae28-143">**type**</span><span class="sxs-lookup"><span data-stu-id="fae28-143">**type**</span></span> |<span data-ttu-id="fae28-144">작업 형식:</span><span class="sxs-lookup"><span data-stu-id="fae28-144">Types of jobs:</span></span> |
| <span data-ttu-id="fae28-145">**scheduledUpdateTwin**: desired 속성 또는 태그 집합을 업데이트하는 데 사용되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="fae28-146">**scheduledDeviceMethod**: 장치 쌍 집합에서 장치 메서드를 호출하는 데 사용되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="fae28-147">**상태**</span><span class="sxs-lookup"><span data-stu-id="fae28-147">**status**</span></span> |<span data-ttu-id="fae28-148">작업의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-148">Current state of the job.</span></span> <span data-ttu-id="fae28-149">가능한 상태 값:</span><span class="sxs-lookup"><span data-stu-id="fae28-149">Possible values for status:</span></span> |
| <span data-ttu-id="fae28-150">**보류 중** : 예약되어 작업 서비스에서 선택되기를 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="fae28-151">**예약됨** : 이후 시간에 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="fae28-152">**실행 중** : 현재 활성 상태의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="fae28-153">**취소됨** : 작업이 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="fae28-154">**실패함** : 작업이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="fae28-155">**완료됨** : 작업이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="fae28-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="fae28-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="fae28-157">작업 실행에 대한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="fae28-158">**deviceJobStatistics** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="fae28-159">속성</span><span class="sxs-lookup"><span data-stu-id="fae28-159">Property</span></span> | <span data-ttu-id="fae28-160">설명</span><span class="sxs-lookup"><span data-stu-id="fae28-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fae28-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="fae28-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="fae28-162">작업에서 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="fae28-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="fae28-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="fae28-164">작업이 실패한 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="fae28-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="fae28-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="fae28-166">작업이 성공한 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="fae28-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="fae28-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="fae28-168">현재 작업을 실행 중인 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="fae28-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="fae28-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="fae28-170">작업 실행이 보류 중인 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="fae28-171">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="fae28-171">Additional reference material</span></span>
<span data-ttu-id="fae28-172">이 IoT Hub 개발자 가이드의 다른 참조 자료:</span><span class="sxs-lookup"><span data-stu-id="fae28-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="fae28-173">[IoT Hub 끝점][lnk-endpoints] - 각 IoT Hub에서 런타임 및 관리 작업에 대해 공개하는 다양한 끝점에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="fae28-174">[제한 및 할당량][lnk-quotas] - IoT Hub 서비스에 적용되는 할당량과 서비스를 사용할 때 예상되는 제한 동작에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="fae28-175">[Azure IoT 장치 및 서비스 SDK][lnk-sdks] - IoT Hub와 상호 작용하는 장치 및 서비스 앱 모두를 개발할 때 사용하는 다양한 언어 SDK를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="fae28-176">[장치 쌍, 작업 및 메시지 라우팅을 위한 IoT Hub 쿼리 언어][lnk-query]에서는 IoT Hub에서 장치 쌍 및 작업에 대한 정보를 검색하는 데 사용할 수 있는 IoT Hub 쿼리 언어에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="fae28-177">[IoT Hub MQTT 지원][lnk-devguide-mqtt] - MQTT 프로토콜에 대한 IoT Hub 지원에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="fae28-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fae28-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fae28-178">Next steps</span></span>
<span data-ttu-id="fae28-179">이 문서에서 설명한 일부 개념을 시도해 보려면 다음과 같은 IoT Hub 자습서를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="fae28-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="fae28-180">[작업 예약 및 브로드캐스트][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="fae28-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
