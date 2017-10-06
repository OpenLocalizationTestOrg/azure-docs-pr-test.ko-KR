---
title: "aaaUnderstand Azure IoT 허브 작업 | Microsoft Docs"
description: "개발자 가이드-여러 장치에서 작업 toorun 예약 tooyour IoT 허브를 연결 합니다. 작업은 태그와 원하는 속성을 업데이트하고 여러 장치에서 직접 메서드를 호출할 수 있습니다."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="f19c5-104">여러 장치에서 작업 예약</span><span class="sxs-lookup"><span data-stu-id="f19c5-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="f19c5-105">개요</span><span class="sxs-lookup"><span data-stu-id="f19c5-105">Overview</span></span>
<span data-ttu-id="f19c5-106">이전 문서에 설명된 대로, Azure IoT Hub를 통해 다양한 구성 요소([장치 쌍 속성 및 태그][lnk-twin-devguide] 및 [직접 메서드][lnk-dev-methods])를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="f19c5-107">일반적으로 백 엔드 응용 프로그램 장치 관리자 및 운영자 tooupdate를 사용 하도록 설정 하 고 IoT 장치를 대량 및 예약된 된 시간에 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="f19c5-108">작업 일정 시간에는 장치로 이중 업데이트 및 일련의 장치에 대해 직접 메서드 hello 실행을 캡슐화합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="f19c5-109">예를 들어 운영자는 시작 및 작업 tooreboot 43 및 3 층 hello 건물의 중단 toohello 작업 되지 않은 한 번에 빌드 장치 집합을 추적 하는 백 엔드 응용 프로그램을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="f19c5-110">때 toouse</span><span class="sxs-lookup"><span data-stu-id="f19c5-110">When toouse</span></span>
<span data-ttu-id="f19c5-111">고려 될 경우 작업을 사용 하 여: 솔루션 백 엔드 요구 tooschedule 및 추적 진행 hello 활동 장치 집합에서 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="f19c5-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="f19c5-112">desired 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="f19c5-112">Update desired properties</span></span>
* <span data-ttu-id="f19c5-113">tags 업데이트</span><span class="sxs-lookup"><span data-stu-id="f19c5-113">Update tags</span></span>
* <span data-ttu-id="f19c5-114">직접 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="f19c5-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="f19c5-115">작업 수명 주기</span><span class="sxs-lookup"><span data-stu-id="f19c5-115">Job lifecycle</span></span>
<span data-ttu-id="f19c5-116">작업은 hello 솔루션 백 엔드에 의해 시작 되 고 IoT 허브에 의해 유지 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="f19c5-117">서비스 지향 URI(`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`)를 통해 작업을 시작하고 서비스 지향 URI(`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`)를 통해 작업 실행 진행 상태를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="f19c5-118">작업이 시작 되 면 작업에 대 한 쿼리 실행 중인 작업의 hello 백 엔드 앱 toorefresh hello 상태를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="f19c5-119">작업을 시작 하면 속성 이름 및 값만 포함 될 수 있습니다 US-ASCII 인쇄 가능한 hello 관계 집합에서 제외 하 고 영숫자: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="f19c5-120">참조 항목:</span><span class="sxs-lookup"><span data-stu-id="f19c5-120">Reference topics:</span></span>
<span data-ttu-id="f19c5-121">다음 참조 항목 hello 작업을 사용 하는 방법에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="f19c5-122">작업 tooexecute 직접 메서드</span><span class="sxs-lookup"><span data-stu-id="f19c5-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="f19c5-123">hello 다음은를 실행 하기 위한 HTTP 1.1 hello 요청 세부 정보는 [직접적인 방법] [ lnk-dev-methods] 일련의 작업을 사용 하는 장치에서:</span><span class="sxs-lookup"><span data-stu-id="f19c5-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="f19c5-124">hello 쿼리 조건이 수도 있습니다는 단일 장치 Id 또는 장치 Id 목록에서 아래와 같이</span><span class="sxs-lookup"><span data-stu-id="f19c5-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="f19c5-125">**예**</span><span class="sxs-lookup"><span data-stu-id="f19c5-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="f19c5-126">[IoT Hub 쿼리 언어][lnk-query]는 추가 세부 정보에서 IoT Hub 쿼리 언어를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="f19c5-127">작업 tooupdate 장치로 이중 속성</span><span class="sxs-lookup"><span data-stu-id="f19c5-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="f19c5-128">hello 다음은 작업을 사용 하는 장치로 이중 속성을 업데이트 하기 위한 HTTP 1.1 hello 요청 세부 정보:</span><span class="sxs-lookup"><span data-stu-id="f19c5-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="f19c5-129">작업 진행 상태 쿼리</span><span class="sxs-lookup"><span data-stu-id="f19c5-129">Querying for progress on jobs</span></span>
<span data-ttu-id="f19c5-130">hello 다음은 hello에 대 한 HTTP 1.1 요청 정보 [작업에 대 한 쿼리][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="f19c5-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="f19c5-131">hello continuationToken hello 응답에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="f19c5-132">작업 속성</span><span class="sxs-lookup"><span data-stu-id="f19c5-132">Jobs Properties</span></span>
<span data-ttu-id="f19c5-133">hello 다음은 속성 및 작업 또는 작업 결과 쿼리할 때 사용할 수 있는 해당 설명의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="f19c5-134">속성</span><span class="sxs-lookup"><span data-stu-id="f19c5-134">Property</span></span> | <span data-ttu-id="f19c5-135">설명</span><span class="sxs-lookup"><span data-stu-id="f19c5-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f19c5-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="f19c5-136">**jobId**</span></span> |<span data-ttu-id="f19c5-137">Hello 작업에 대 한 ID를 제공 하는 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="f19c5-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="f19c5-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="f19c5-138">**startTime**</span></span> |<span data-ttu-id="f19c5-139">Hello 작업에 대 한 제공 된 응용 프로그램 시작 시간 (ISO 8601)입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="f19c5-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="f19c5-140">**endTime**</span></span> |<span data-ttu-id="f19c5-141">IoT Hub hello 작업 완료에 대 한 날짜 (ISO 8601)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="f19c5-142">Hello 작업에는 '완료' hello 상태에 도달한 후에 유효 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="f19c5-143">**type**</span><span class="sxs-lookup"><span data-stu-id="f19c5-143">**type**</span></span> |<span data-ttu-id="f19c5-144">작업 형식:</span><span class="sxs-lookup"><span data-stu-id="f19c5-144">Types of jobs:</span></span> |
| <span data-ttu-id="f19c5-145">**scheduledUpdateTwin**: 사용 작업 tooupdate 원하는 속성 또는 태그의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="f19c5-146">**scheduledDeviceMethod**: 사용 작업 tooinvoke 장치 트윈스 집합이 장치 메서드.</span><span class="sxs-lookup"><span data-stu-id="f19c5-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="f19c5-147">**상태**</span><span class="sxs-lookup"><span data-stu-id="f19c5-147">**status**</span></span> |<span data-ttu-id="f19c5-148">Hello 작업의 현재 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-148">Current state of hello job.</span></span> <span data-ttu-id="f19c5-149">가능한 상태 값:</span><span class="sxs-lookup"><span data-stu-id="f19c5-149">Possible values for status:</span></span> |
| <span data-ttu-id="f19c5-150">**보류 중인** : 예약 하 고 대기 toobe hello 작업 서비스에 의해 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="f19c5-151">**예약 된** : 시간 보다 이후 hello에 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="f19c5-152">**실행 중** : 현재 활성 상태의 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="f19c5-153">**취소됨** : 작업이 취소되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="f19c5-154">**실패함** : 작업이 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="f19c5-155">**완료됨** : 작업이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="f19c5-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="f19c5-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="f19c5-157">Hello 작업의 실행에 대 한 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="f19c5-158">**deviceJobStatistics** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="f19c5-159">속성</span><span class="sxs-lookup"><span data-stu-id="f19c5-159">Property</span></span> | <span data-ttu-id="f19c5-160">설명</span><span class="sxs-lookup"><span data-stu-id="f19c5-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f19c5-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="f19c5-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="f19c5-162">Hello 작업에는 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="f19c5-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="f19c5-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="f19c5-164">Hello 작업에 실패 하는 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="f19c5-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="f19c5-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="f19c5-166">여기서 hello 작업이 성공적으로 수행 하는 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="f19c5-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="f19c5-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="f19c5-168">Hello 작업이 현재 실행 중인 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="f19c5-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="f19c5-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="f19c5-170">Toorun hello 작업이 보류 중인 장치 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="f19c5-171">추가 참조 자료</span><span class="sxs-lookup"><span data-stu-id="f19c5-171">Additional reference material</span></span>
<span data-ttu-id="f19c5-172">Hello IoT 허브 개발자 가이드에서에서 다른 참조 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f19c5-173">[IoT Hub 끝점] [ lnk-endpoints] 설명 hello 런타임 및 관리 작업에 대 한 각 IoT 허브를 노출 하는 다양 한 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f19c5-174">[제한 및 할당량] [ lnk-quotas] hello 서비스를 사용 하는 경우 조정 동작 tooexpect hello와 toohello IoT 허브 서비스를 적용 하는 hello 할당량에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="f19c5-175">[Azure IoT 장치 및 서비스 Sdk] [ lnk-sdks] 목록에는 다양 한 언어 Sdk hello IoT Hub와 상호 작용 하는 장치 및 서비스 모두 앱을 개발할 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f19c5-176">[장치 트윈스, 작업 및 메시지 라우팅에 대 한 IoT Hub 쿼리 언어] [ lnk-query] hello 장치 트윈스 및 작업에 대 한 IoT 허브에서 tooretrieve 정보를 사용 하려면 IoT Hub 쿼리 언어에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f19c5-177">[IoT 허브 MQTT 지원] [ lnk-devguide-mqtt] hello MQTT 프로토콜에 대 한 IoT Hub 지원에 대 한 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f19c5-178">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f19c5-178">Next steps</span></span>
<span data-ttu-id="f19c5-179">이 문서에서 설명 하는 hello 개념 중 일부는 tootry, 원하는 경우 IoT Hub 자습서 hello에 관심이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f19c5-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="f19c5-180">[작업 예약 및 브로드캐스트][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f19c5-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
