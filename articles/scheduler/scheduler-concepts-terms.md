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
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>스케줄러 개념, 용어 + 엔터티 계층 구조
## <a name="scheduler-entity-hierarchy"></a>스케줄러 엔터티 계층 구조
hello 다음 표에서 설명 hello를 주요 리소스로 hello 스케줄러 API에서 노출 하거나 사용:

| 리소스 | 설명 |
| --- | --- |
| **작업 컬렉션** |작업 컬렉션 작업 그룹을 포함 하 고 설정, 할당량 및 공유 hello 컬렉션 내에서 작업 하는 스로틀을 유지 합니다. 작업 컬렉션은 구독 소유자가 만들며, 사용 또는 응용 프로그램 경계를 기준으로 작업을 함께 그룹화합니다. 이 제한 된 tooone 영역입니다. 또한 있습니다 hello 할당량을 적용 tooconstrain hello 전체 작업 사용량을 해당 컬렉션에. hello 할당량 MaxJobs 및 maxrecurrence가 포함 됩니다. |
| **작업** |작업은 간단하거나 복잡한 실행 전략을 통해 단일 반복 작업을 정의합니다. 작업은 HTTP, 저장소 큐, 서비스 버스 큐 또는 서비스 버스 항목 요청을 포함할 수 있습니다. |
| **작업 기록** |작업 기록의 경우 작업 실행에 대한 세부 정보를 나타냅니다. 응답 세부 정보와 함께 성공 또는 실패를 포함합니다. |

## <a name="scheduler-entity-management"></a>스케줄러 엔터티 관리
상위 수준 hello 스케줄러 및 hello 서비스 관리 API는 hello 리소스에 대 한 작업을 수행 하는 hello를 노출 합니다.

| 기능 | 설명 및 URI 주소 |
| --- | --- |
| **작업 컬렉션 관리** |GET, PUT 및 DELETE 만들기 및 수정 작업 컬렉션 및 그 안에 포함 된 hello 작업에 대 한 지원. 작업 컬렉션 작업에 대 한 컨테이너로 사용 되며 tooquotas 및 공유 설정 매핑합니다. 나중에 설명하는 할당량은 최대 작업 수와 최소 반복 간격을 예로 듭니다. <p>PUT 및 DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **작업 관리** |작업의 생성 및 수정 지원을 위한 GET, PUT, POST, PATCH 및 DELETE 지원  모든 작업 이므로 암시적 작성 없음 이미 존재 하는 tooa jobcollection을 속해 있어야 합니다. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **작업 기록 관리** |GET은 작업 경과 시간, 작업 실행 결과 등, 60일 간의 작업 실행 기록을 가져옵니다. 상태를 기초로 한 필터링을 위해 쿼리 문자열 매개 변수 지원을 추가합니다. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>작업 유형
HTTP 작업(SSL을 지원하는 HTTPS 작업 포함), 저장소 큐 작업, 서비스 버스 큐 작업 및 서비스 버스 항목 작업 등 여러 가지 유형의 작업이 있습니다. HTTP 작업은 기존 작업 부하 또는 서비스의 끝점을 사용하는 경우에 이상적입니다. 있으므로 이러한 작업은 저장소 큐를 사용 하는 작업에 대 한 이상적인 저장소 큐 작업 toopost 메시지 toostorage 큐를 사용할 수 있습니다. 마찬가지로, 서비스 버스 작업은 서비스 버스 큐와 토픽을 사용하는 워크로드에 적합합니다.

## <a name="hello-job-entity-in-detail"></a>hello "job" 엔터티 세부 정보
기본 수준에서, 예약된 작업에는 다음과 같은 여러 부분이 있습니다.

* hello 동작 tooperform hello 작업 타이머가 발생할 때  
* (선택 사항) hello 시간 toorun hello 작업  
* (선택 사항) 시기와 빈도 toorepeat hello 작업  
* (선택 사항) 작업 toofire hello 기본 작업에 실패할 경우  

내부적으로 예약된 된 작업 hello 다음 예약된 실행 시간 등의 시스템 제공 데이터도 포함합니다.

hello 코드 다음 예약된 된 작업의 자세한 예를 제공 합니다. 세부 정보는 이후의 섹션에서 제공합니다.

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

Hello 샘플 예약 된 작업 위의 같이 작업 정의는 여러 부분이 있습니다.

* 시작 시간("startTime")  
* 오류 동작("errorAction")을 포함하는 동작("action")
* 되풀이("recurrence")  
* 상태(“state”)  
* 상태(“status”)  
* 재시도 정책("retryPolicy")  

각각에 대해 자세히 살펴보겠습니다.

## <a name="starttime"></a>startTime
"startTime" hello hello 시작 시간 및 hello 호출자 toospecify 시간대 오프셋에 hello 통신 중에 허용 [ISO 8601 형식](http://en.wikipedia.org/wiki/ISO_8601)합니다.

## <a name="action-and-erroraction"></a>action 및 errorAction
hello "action" 각 항목에서 호출 하는 hello 동작 속하며 서비스 호출 유형을 설명 합니다. hello 동작은 hello 제공 일정에서 실행 됩니다. 스케줄러는 HTTP, 저장소 큐, 서비스 버스 항목 또는 서비스 버스 큐 작업을 지원합니다.

hello 위의 hello 예제에서 동작은 HTTP 동작 합니다. 다음은 저장소 큐 동작의 예입니다.

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

다음은 서비스 버스 항목 작업의 예입니다.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

다음은 서비스 버스 큐 동작의 예입니다.

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

"errorAction" hello은 hello 오류 처리기, hello 동작 hello 기본 작업에 실패할 때 호출 됩니다. 이 변수 toocall 오류 처리 끝점을 사용 하거나 사용자 알림을 보낼 수 있습니다. 이 사용할 수 있습니다는 hello에 hello 경우에서 보조 끝점에 연결 하기 위한 기본을 사용할 수 없습니다 (예: hello 끝점의 사이트에서 재해의 경우 hello) 또는 오류 처리 끝점을 알리는 데 사용할 수 있습니다. Hello 기본 동작과 마찬가지로 hello 오류 동작은 다른 동작을 기반으로 단순 또는 복합 논리 수 있습니다. toocreate SAS 토큰이 너무 참조 하는 방법 toolearn[공유 액세스 서명 만들기 및 사용](https://msdn.microsoft.com/library/azure/jj721951.aspx)합니다.

## <a name="recurrence"></a>되풀이
되풀이에는 여러 부분이 있습니다.

* 빈도: 분, 시간, 일, 주, 월, 년 중 하나  
* Hello 되풀이 빈도 지정 하는 hello 간격이 간격:  
* 정해진된 일정: 분, 시간, 요일, 월 및 되풀이할 hello 되풀이 지정 합니다.  
* 개수: 발생 횟수  
* 종료 시간: 작업이 실행 되지 것입니다 hello 종료 시간을 지정한 후  

JSON 정의에 지정된 되풀이 개체가 있으면 작업이 반복됩니다. Count 및 endTime이 모두 지정 된 경우에 먼저 발생 하는 hello 완료 규칙이 적용 됩니다.

## <a name="state"></a>state
hello hello 작업의 상태가 4 개의 값 중 하나: 활성화, 비활성화, 완료 됨 또는 오류가 발생 했습니다. 넣을 수 있습니다 또는 패치 tooupdate로 작업 하므로 해당 toohello 사용 또는 사용 안 함 상태입니다. 작업이 완료 되었거나 오류가 발생 하는 경우 (hello 작업 수 여전히 삭제할 수 있더라도) 업데이트할 수 없는 최종 상태입니다. Hello state 속성의 예는 다음과 같습니다.

        "state": "disabled", // enabled, disabled, completed, or faulted
완료 및 오류 작업은 60일 후 삭제됩니다.

## <a name="status"></a>status
스케줄러 작업이 시작 되 면 hello hello 작업의 현재 상태에 대 한 정보가 반환 됩니다. 이 개체는 hello 사용자가 설정할 수 없습니다-hello 시스템에 의해 설정 됩니다. 그러나 하나 작업의 hello 상태를 쉽게 얻을 수 있도록 hello 작업 개체 (아니라 별도 연결 된 리소스)에 포함 됩니다.

Hello hello 이전 실행 시간 (있는 경우)를 포함 하는 작업 상태 (진행 중인 작업의 경우)에 대 한 hello 다음 예약된 실행 시간 및 hello 작업의 실행 수 hello hello 합니다.

## <a name="retrypolicy"></a>retryPolicy
스케줄러 작업이 실패할 경우 가능한 toospecify hello 작업의 다시 시도 여부 및 방법을 다시 시도 정책 toodetermine입니다. Hello에서 결정 **retryType** 개체-너무 설정은**none** 없으면 다시 시도 정책이 없으면 위와 같이 합니다. 너무 설정**고정** 다시 시도 정책이 있는 경우.

tooset을 다시 시도 정책에 두 가지 추가 설정을 지정할 수 있습니다: 재시도 간격 (**retryInterval**) 및 재시도 횟수 hello (**retryCount**).

hello로 지정 된 hello 재시도 간격이 **retryInterval** 개체, 재시도 사이의 hello 간격입니다. 기본값은 30초이며 구성 가능한 최소값은 15초, 최대값은 18개월입니다. 무료 작업 컬렉션에 있는 작업의 구성 가능한 최소값은 1시간입니다.  Hello ISO 8601 형식으로 정의 됩니다. Hello로 hello 재시도 횟수의 hello 값을 지정 하는 마찬가지로, **retryCount** 개체 hello 번호 시도 횟수입니다. 값이 기본값으로 4이 고 최대값은 20\ 합니다. 둘 다 **retryInterval** 및 **retryCount** 는 선택 사항입니다. 하는 경우의 기본 값이 지정 됩니다 **retryType** 너무 설정**고정** 값이 없는 명시적으로 지정 됩니다.

## <a name="see-also"></a>참고 항목
 [Scheduler란?](scheduler-intro.md)

 [Hello Azure 포털에서에서 스케줄러 사용 시작](scheduler-get-started-portal.md)

 [Azure 스케줄러의 버전 및 요금 청구](scheduler-plans-billing.md)

 [일정을 toobuild 복잡 한 방법 및 Azure 스케줄러와 고급 되풀이](scheduler-advanced-complexity.md)

 [Azure 스케줄러 REST API 참조](https://msdn.microsoft.com/library/mt629143)

 [Azure 스케줄러 PowerShell cmdlet 참조](scheduler-powershell-reference.md)

 [Azure 스케줄러 고가용성 및 안정성](scheduler-high-availability-reliability.md)

 [Azure 스케줄러 제한, 기본값 및 오류 코드](scheduler-limits-defaults-errors.md)

 [Azure 스케줄러 아웃바운드 인증](scheduler-outbound-authentication.md)

