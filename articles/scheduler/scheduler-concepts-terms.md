---
title: "aaaScheduler 개념, 용어 및 엔터티 | Microsoft Docs"
description: "작업 및 작업 컬렉션을 포함하는 Azure 스케줄러 개념, 용어 및 엔터티 계층 구조입니다.  예약된 작업의 자세한 예를 보여줍니다."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="f75f9-104">스케줄러 개념, 용어 + 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="f75f9-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="f75f9-105">스케줄러 엔터티 계층 구조</span><span class="sxs-lookup"><span data-stu-id="f75f9-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="f75f9-106">hello 다음 표에서 설명 hello를 주요 리소스로 hello 스케줄러 API에서 노출 하거나 사용:</span><span class="sxs-lookup"><span data-stu-id="f75f9-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="f75f9-107">리소스</span><span class="sxs-lookup"><span data-stu-id="f75f9-107">Resource</span></span> | <span data-ttu-id="f75f9-108">설명</span><span class="sxs-lookup"><span data-stu-id="f75f9-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f75f9-109">**작업 컬렉션**</span><span class="sxs-lookup"><span data-stu-id="f75f9-109">**Job collection**</span></span> |<span data-ttu-id="f75f9-110">작업 컬렉션 작업 그룹을 포함 하 고 설정, 할당량 및 공유 hello 컬렉션 내에서 작업 하는 스로틀을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="f75f9-111">작업 컬렉션은 구독 소유자가 만들며, 사용 또는 응용 프로그램 경계를 기준으로 작업을 함께 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="f75f9-112">이 제한 된 tooone 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-112">It’s constrained tooone region.</span></span> <span data-ttu-id="f75f9-113">또한 있습니다 hello 할당량을 적용 tooconstrain hello 전체 작업 사용량을 해당 컬렉션에.</span><span class="sxs-lookup"><span data-stu-id="f75f9-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="f75f9-114">hello 할당량 MaxJobs 및 maxrecurrence가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="f75f9-115">**작업**</span><span class="sxs-lookup"><span data-stu-id="f75f9-115">**Job**</span></span> |<span data-ttu-id="f75f9-116">작업은 간단하거나 복잡한 실행 전략을 통해 단일 반복 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="f75f9-117">작업은 HTTP, 저장소 큐, 서비스 버스 큐 또는 서비스 버스 항목 요청을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="f75f9-118">**작업 기록**</span><span class="sxs-lookup"><span data-stu-id="f75f9-118">**Job history**</span></span> |<span data-ttu-id="f75f9-119">작업 기록의 경우 작업 실행에 대한 세부 정보를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="f75f9-120">응답 세부 정보와 함께 성공 또는 실패를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="f75f9-121">스케줄러 엔터티 관리</span><span class="sxs-lookup"><span data-stu-id="f75f9-121">Scheduler entity management</span></span>
<span data-ttu-id="f75f9-122">상위 수준 hello 스케줄러 및 hello 서비스 관리 API는 hello 리소스에 대 한 작업을 수행 하는 hello를 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="f75f9-123">기능</span><span class="sxs-lookup"><span data-stu-id="f75f9-123">Capability</span></span> | <span data-ttu-id="f75f9-124">설명 및 URI 주소</span><span class="sxs-lookup"><span data-stu-id="f75f9-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="f75f9-125">**작업 컬렉션 관리**</span><span class="sxs-lookup"><span data-stu-id="f75f9-125">**Job collection management**</span></span> |<span data-ttu-id="f75f9-126">GET, PUT 및 DELETE 만들기 및 수정 작업 컬렉션 및 그 안에 포함 된 hello 작업에 대 한 지원.</span><span class="sxs-lookup"><span data-stu-id="f75f9-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="f75f9-127">작업 컬렉션 작업에 대 한 컨테이너로 사용 되며 tooquotas 및 공유 설정 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="f75f9-128">나중에 설명하는 할당량은 최대 작업 수와 최소 반복 간격을 예로 듭니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="f75f9-129">PUT 및 DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="f75f9-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="f75f9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="f75f9-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="f75f9-131">**작업 관리**</span><span class="sxs-lookup"><span data-stu-id="f75f9-131">**Job management**</span></span> |<span data-ttu-id="f75f9-132">작업의 생성 및 수정 지원을 위한 GET, PUT, POST, PATCH 및 DELETE 지원 </span><span class="sxs-lookup"><span data-stu-id="f75f9-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="f75f9-133">모든 작업 이므로 암시적 작성 없음 이미 존재 하는 tooa jobcollection을 속해 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="f75f9-134">**작업 기록 관리**</span><span class="sxs-lookup"><span data-stu-id="f75f9-134">**Job history management**</span></span> |<span data-ttu-id="f75f9-135">GET은 작업 경과 시간, 작업 실행 결과 등, 60일 간의 작업 실행 기록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="f75f9-136">상태를 기초로 한 필터링을 위해 쿼리 문자열 매개 변수 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="f75f9-137">작업 유형</span><span class="sxs-lookup"><span data-stu-id="f75f9-137">Job types</span></span>
<span data-ttu-id="f75f9-138">HTTP 작업(SSL을 지원하는 HTTPS 작업 포함), 저장소 큐 작업, 서비스 버스 큐 작업 및 서비스 버스 항목 작업 등 여러 가지 유형의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="f75f9-139">HTTP 작업은 기존 작업 부하 또는 서비스의 끝점을 사용하는 경우에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="f75f9-140">있으므로 이러한 작업은 저장소 큐를 사용 하는 작업에 대 한 이상적인 저장소 큐 작업 toopost 메시지 toostorage 큐를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="f75f9-141">마찬가지로, 서비스 버스 작업은 서비스 버스 큐와 토픽을 사용하는 워크로드에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="f75f9-142">hello "job" 엔터티 세부 정보</span><span class="sxs-lookup"><span data-stu-id="f75f9-142">hello "job" entity in detail</span></span>
<span data-ttu-id="f75f9-143">기본 수준에서, 예약된 작업에는 다음과 같은 여러 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="f75f9-144">hello 동작 tooperform hello 작업 타이머가 발생할 때</span><span class="sxs-lookup"><span data-stu-id="f75f9-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="f75f9-145">(선택 사항) hello 시간 toorun hello 작업</span><span class="sxs-lookup"><span data-stu-id="f75f9-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="f75f9-146">(선택 사항) 시기와 빈도 toorepeat hello 작업</span><span class="sxs-lookup"><span data-stu-id="f75f9-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="f75f9-147">(선택 사항) 작업 toofire hello 기본 작업에 실패할 경우</span><span class="sxs-lookup"><span data-stu-id="f75f9-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="f75f9-148">내부적으로 예약된 된 작업 hello 다음 예약된 실행 시간 등의 시스템 제공 데이터도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="f75f9-149">hello 코드 다음 예약된 된 작업의 자세한 예를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="f75f9-150">세부 정보는 이후의 섹션에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="f75f9-151">Hello 샘플 예약 된 작업 위의 같이 작업 정의는 여러 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="f75f9-152">시작 시간("startTime")</span><span class="sxs-lookup"><span data-stu-id="f75f9-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="f75f9-153">오류 동작("errorAction")을 포함하는 동작("action")</span><span class="sxs-lookup"><span data-stu-id="f75f9-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="f75f9-154">되풀이("recurrence")</span><span class="sxs-lookup"><span data-stu-id="f75f9-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="f75f9-155">상태(“state”)</span><span class="sxs-lookup"><span data-stu-id="f75f9-155">State (“state”)</span></span>  
* <span data-ttu-id="f75f9-156">상태(“status”)</span><span class="sxs-lookup"><span data-stu-id="f75f9-156">Status (“status”)</span></span>  
* <span data-ttu-id="f75f9-157">재시도 정책("retryPolicy")</span><span class="sxs-lookup"><span data-stu-id="f75f9-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="f75f9-158">각각에 대해 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="f75f9-159">startTime</span><span class="sxs-lookup"><span data-stu-id="f75f9-159">startTime</span></span>
<span data-ttu-id="f75f9-160">"startTime" hello hello 시작 시간 및 hello 호출자 toospecify 시간대 오프셋에 hello 통신 중에 허용 [ISO 8601 형식](http://en.wikipedia.org/wiki/ISO_8601)합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="f75f9-161">action 및 errorAction</span><span class="sxs-lookup"><span data-stu-id="f75f9-161">action and errorAction</span></span>
<span data-ttu-id="f75f9-162">hello "action" 각 항목에서 호출 하는 hello 동작 속하며 서비스 호출 유형을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="f75f9-163">hello 동작은 hello 제공 일정에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="f75f9-164">스케줄러는 HTTP, 저장소 큐, 서비스 버스 항목 또는 서비스 버스 큐 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="f75f9-165">hello 위의 hello 예제에서 동작은 HTTP 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="f75f9-166">다음은 저장소 큐 동작의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="f75f9-167">다음은 서비스 버스 항목 작업의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="f75f9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="f75f9-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="f75f9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="f75f9-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="f75f9-170">다음은 서비스 버스 큐 동작의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="f75f9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="f75f9-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="f75f9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="f75f9-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="f75f9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span><span class="sxs-lookup"><span data-stu-id="f75f9-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="f75f9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="f75f9-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="f75f9-175">"errorAction" hello은 hello 오류 처리기, hello 동작 hello 기본 작업에 실패할 때 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="f75f9-176">이 변수 toocall 오류 처리 끝점을 사용 하거나 사용자 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="f75f9-177">이 사용할 수 있습니다는 hello에 hello 경우에서 보조 끝점에 연결 하기 위한 기본을 사용할 수 없습니다 (예: hello 끝점의 사이트에서 재해의 경우 hello) 또는 오류 처리 끝점을 알리는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="f75f9-178">Hello 기본 동작과 마찬가지로 hello 오류 동작은 다른 동작을 기반으로 단순 또는 복합 논리 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="f75f9-179">toocreate SAS 토큰이 너무 참조 하는 방법 toolearn[공유 액세스 서명 만들기 및 사용](https://msdn.microsoft.com/library/azure/jj721951.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="f75f9-180">되풀이</span><span class="sxs-lookup"><span data-stu-id="f75f9-180">recurrence</span></span>
<span data-ttu-id="f75f9-181">되풀이에는 여러 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="f75f9-182">빈도: 분, 시간, 일, 주, 월, 년 중 하나</span><span class="sxs-lookup"><span data-stu-id="f75f9-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="f75f9-183">Hello 되풀이 빈도 지정 하는 hello 간격이 간격:</span><span class="sxs-lookup"><span data-stu-id="f75f9-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="f75f9-184">정해진된 일정: 분, 시간, 요일, 월 및 되풀이할 hello 되풀이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="f75f9-185">개수: 발생 횟수</span><span class="sxs-lookup"><span data-stu-id="f75f9-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="f75f9-186">종료 시간: 작업이 실행 되지 것입니다 hello 종료 시간을 지정한 후</span><span class="sxs-lookup"><span data-stu-id="f75f9-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="f75f9-187">JSON 정의에 지정된 되풀이 개체가 있으면 작업이 반복됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="f75f9-188">Count 및 endTime이 모두 지정 된 경우에 먼저 발생 하는 hello 완료 규칙이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="f75f9-189">state</span><span class="sxs-lookup"><span data-stu-id="f75f9-189">state</span></span>
<span data-ttu-id="f75f9-190">hello hello 작업의 상태가 4 개의 값 중 하나: 활성화, 비활성화, 완료 됨 또는 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="f75f9-191">넣을 수 있습니다 또는 패치 tooupdate로 작업 하므로 해당 toohello 사용 또는 사용 안 함 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="f75f9-192">작업이 완료 되었거나 오류가 발생 하는 경우 (hello 작업 수 여전히 삭제할 수 있더라도) 업데이트할 수 없는 최종 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="f75f9-193">Hello state 속성의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="f75f9-194">완료 및 오류 작업은 60일 후 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="f75f9-195">status</span><span class="sxs-lookup"><span data-stu-id="f75f9-195">status</span></span>
<span data-ttu-id="f75f9-196">스케줄러 작업이 시작 되 면 hello hello 작업의 현재 상태에 대 한 정보가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="f75f9-197">이 개체는 hello 사용자가 설정할 수 없습니다-hello 시스템에 의해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="f75f9-198">그러나 하나 작업의 hello 상태를 쉽게 얻을 수 있도록 hello 작업 개체 (아니라 별도 연결 된 리소스)에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="f75f9-199">Hello hello 이전 실행 시간 (있는 경우)를 포함 하는 작업 상태 (진행 중인 작업의 경우)에 대 한 hello 다음 예약된 실행 시간 및 hello 작업의 실행 수 hello hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="f75f9-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="f75f9-200">retryPolicy</span></span>
<span data-ttu-id="f75f9-201">스케줄러 작업이 실패할 경우 가능한 toospecify hello 작업의 다시 시도 여부 및 방법을 다시 시도 정책 toodetermine입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="f75f9-202">Hello에서 결정 **retryType** 개체-너무 설정은**none** 없으면 다시 시도 정책이 없으면 위와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="f75f9-203">너무 설정**고정** 다시 시도 정책이 있는 경우.</span><span class="sxs-lookup"><span data-stu-id="f75f9-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="f75f9-204">tooset을 다시 시도 정책에 두 가지 추가 설정을 지정할 수 있습니다: 재시도 간격 (**retryInterval**) 및 재시도 횟수 hello (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="f75f9-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="f75f9-205">hello로 지정 된 hello 재시도 간격이 **retryInterval** 개체, 재시도 사이의 hello 간격입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="f75f9-206">기본값은 30초이며 구성 가능한 최소값은 15초, 최대값은 18개월입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="f75f9-207">무료 작업 컬렉션에 있는 작업의 구성 가능한 최소값은 1시간입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="f75f9-208">Hello ISO 8601 형식으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="f75f9-209">Hello로 hello 재시도 횟수의 hello 값을 지정 하는 마찬가지로, **retryCount** 개체 hello 번호 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="f75f9-210">값이 기본값으로 4이 고 최대값은 20\ 합니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="f75f9-211">둘 다 **retryInterval** 및 **retryCount** 는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="f75f9-212">하는 경우의 기본 값이 지정 됩니다 **retryType** 너무 설정**고정** 값이 없는 명시적으로 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f75f9-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="f75f9-213">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f75f9-213">See also</span></span>
 [<span data-ttu-id="f75f9-214">Scheduler란?</span><span class="sxs-lookup"><span data-stu-id="f75f9-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="f75f9-215">Hello Azure 포털에서에서 스케줄러 사용 시작</span><span class="sxs-lookup"><span data-stu-id="f75f9-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="f75f9-216">Azure 스케줄러의 버전 및 요금 청구</span><span class="sxs-lookup"><span data-stu-id="f75f9-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="f75f9-217">일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이</span><span class="sxs-lookup"><span data-stu-id="f75f9-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="f75f9-218">Azure 스케줄러 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="f75f9-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="f75f9-219">Azure 스케줄러 PowerShell cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="f75f9-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="f75f9-220">Azure 스케줄러 고가용성 및 안정성</span><span class="sxs-lookup"><span data-stu-id="f75f9-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="f75f9-221">Azure 스케줄러 제한, 기본값 및 오류 코드</span><span class="sxs-lookup"><span data-stu-id="f75f9-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="f75f9-222">Azure 스케줄러 아웃바운드 인증</span><span class="sxs-lookup"><span data-stu-id="f75f9-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

