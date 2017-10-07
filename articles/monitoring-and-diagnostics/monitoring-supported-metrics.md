---
title: "모니터 메트릭-리소스 유형 마다 지원 되는 메트릭 aaaAzure | Microsoft Docs"
description: "Azure Monitor의 각 리소스 유형별로 사용 가능한 메트릭 목록."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 63d4ac65-1688-40d1-85c8-7cd408285b0f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/05/2017
ms.author: johnkem
ms.openlocfilehash: 66834238a1a4fcd7db1464cc023c18ee2563517a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-metrics-with-azure-monitor"></a>Azure Monitor에서 지원되는 메트릭
Azure 모니터 hello 포털에서이 차트, hello REST API를 통한 액세스 또는 쿼리 하기를 포함 하 여 메트릭을 사용 하 여 여러 가지 방법으로 toointeract 제공 PowerShell 또는 CLI를 사용 하 여 합니다. 다음은 현재 Azure Monitor의 메트릭 파이프라인을 통해 사용할 수 있는 모든 메트릭의 전체 목록입니다. 

> [!NOTE]
> 기타 메트릭을 hello 포털 또는 레거시 Api를 사용 하 여 사용할 수 있습니다. 이 목록에 통합 하는 hello Azure 모니터 메트릭 파이프라인의 hello 공개 미리 보기를 사용 하 여 사용 가능한 공개 미리 보기 메트릭만을 포함 됩니다.
>
>

## <a name="microsoftanalysisservicesservers"></a>Microsoft.AnalysisServices/servers

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|qpu_metric|QPU|개수|평균|QPU. 범위는 S1의 경우 0-100, S2의 경우 0-200, S4의 경우 0-400임|
|memory_metric|메모리|바이트|평균|메모리. 범위는 S1의 경우 0-25GB, S2의 경우 0-50GB, S4의 경우 0-100GB임|
|TotalConnectionRequests|총 연결 요청 수|개수|평균|도착한 총 연결 요청 수입니다.|
|SuccessfullConnectionsPerSec|초당 성공한 연결 수|초당 개수|평균|성공적으로 완료된 연결 비율입니다.|
|TotalConnectionFailures|총 연결 실패 수|개수|평균|실패한 총 연결 시도 수입니다.|
|CurrentUserSessions|현재 사용자 세션 수|개수|평균|현재 설정된 사용자 세션 수입니다.|
|QueryPoolBusyThreads|쿼리 풀의 사용 중인 스레드|개수|평균|hello 쿼리 스레드 풀에서 사용 중인 스레드 수입니다.|
|CommandPoolJobQueueLength|명령 풀의 작업 큐 길이|개수|평균|Hello 명령 스레드 풀의 hello 큐에 있는 작업 수입니다.|
|ProcessingPoolJobQueueLength|처리 풀의 작업 큐 길이|개수|평균|스레드 풀을 처리 하는 hello의 hello 큐에 비-I/o 작업 수입니다.|
|CurrentConnections|연결: 현재 연결|개수|평균|현재 설정된 클라이언트 연결 수입니다.|
|CleanerCurrentPrice|메모리: 클리너 현재 가격|개수|평균|메모리, $/ 바이트/시간, 정규화 된 too1000의 현재 가격입니다.|
|CleanerMemoryShrinkable|메모리: 클리너 메모리 축소 가능|바이트|평균|메모리의 양 (바이트)에서 hello 백그라운드 클리너로 주체 toopurging 합니다.|
|CleanerMemoryNonshrinkable|메모리: 클리너 메모리 축소 불가능|바이트|평균|메모리의 양 (바이트)에서 hello 백그라운드 클리너로 주체 toopurging 되지 않습니다.|
|MemoryUsage|메모리: 메모리 사용량|바이트|평균|더욱 명확한 메모리 비용 계산에 사용 되는 hello 서버 프로세스의 메모리 사용량입니다. 같은 toocounter Process\PrivateBytes hello와 크기를 더한 메모리 매핑된 데이터를 메모리 매핑 되었거나 hello xVelocity 메모리 내 분석 엔진 (VertiPaq) hello xVelocity 엔진 Memory Limit를 초과 하 여 할당 된는 무시 합니다.|
|MemoryLimitHard|메모리: 메모리 제한 하드|바이트|평균|하드 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitHigh|메모리: 메모리 제한 상한|바이트|평균|상한 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitLow|메모리: 메모리 제한 하한|바이트|평균|하한 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitVertiPaq|메모리: 메모리 제한 VertiPaq|바이트|평균|메모리 내 제한, 구성 파일 원본입니다.|
|할당량|메모리: 할당량|바이트|평균|현재 메모리 할당량, 바이트 단위입니다. 메모리 할당량은 메모리 부여 또는 메모리 예약이라고도 합니다.|
|QuotaBlocked|메모리: 차단된 할당량|개수|평균|다른 메모리 할당량이 해제될 때까지 차단되는 할당량 요청의 현재 수입니다.|
|VertiPaqNonpaged|메모리: 페이징되지 않은 VertiPaq|바이트|평균|바이트의 메모리 사용에 대 한 hello 작업 집합에 hello 메모리 내 엔진에 의해 잠겼습니다.|
|VertiPaqPaged|메모리: 페이징된 VertiPaq|바이트|평균|메모리 내 데이터에 사용 중인 페이징된 메모리 바이트입니다.|
|RowsReadPerSec|처리: 초당 읽은 행|초당 개수|평균|모든 관계형 데이터베이스에서 읽은 행의 비율입니다.|
|RowsConvertedPerSec|처리: 초당 변환된 행|초당 개수|평균|처리하는 동안 변환된 행의 비율입니다.|
|RowsWrittenPerSec|처리: 초당 작성된 행|초당 개수|평균|처리하는 동안 작성된 행의 비율입니다.|
|CommandPoolBusyThreads|스레드: 명령 풀 사용 중인 스레드|개수|평균|hello 명령 스레드 풀에서 사용 중인 스레드 수입니다.|
|CommandPoolIdleThreads|스레드: 명령 풀 유휴 상태 스레드|개수|평균|Hello 명령 스레드 풀의 유휴 상태 스레드 수입니다.|
|LongParsingBusyThreads|스레드: 긴 구문 분석 사용 중인 스레드|개수|평균|긴 스레드 풀 구문 분석 하는 hello 사용 중인 스레드 수입니다.|
|LongParsingIdleThreads|스레드: 긴 구문 분석 유휴 상태 스레드|개수|평균|긴 스레드 풀 구문 분석 하는 hello의 유휴 상태 스레드 수입니다.|
|LongParsingJobQueueLength|스레드: 긴 구문 분석 작업 큐 길이|개수|평균|긴 스레드 풀 구문 분석 하는 hello의 hello 큐에서 작업 수입니다.|
|ProcessingPoolBusyIOJobThreads|스레드: 처리 풀 사용 중인 I/O 작업 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업을 실행 중인 스레드 수입니다.|
|ProcessingPoolBusyNonIOThreads|스레드: 처리 풀 사용 중인 비-I/O 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 비-I/o 작업을 실행 중인 스레드 수입니다.|
|ProcessingPoolIOJobQueueLength|스레드: 처리 풀 I/O 작업 큐 길이|개수|평균|스레드 풀을 처리 하는 hello의 hello 큐에서 I/O 작업 수입니다.|
|ProcessingPoolIdleIOJobThreads|스레드: 처리 풀 유휴 상태 I/O 작업 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업에 대 한 유휴 상태 스레드 수입니다.|
|ProcessingPoolIdleNonIOThreads|스레드: 처리 풀 유휴 상태 비-I/O 스레드|개수|평균|스레드 풀을 처리 하는 hello에 유휴 상태 스레드 수는 toonon-I/o 작업 전용입니다.|
|QueryPoolIdleThreads|스레드: 쿼리 풀 유휴 상태 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업에 대 한 유휴 상태 스레드 수입니다.|
|QueryPoolJobQueueLength|스레드: 쿼리 풀 작업 큐 길이|개수|평균|Hello 쿼리 스레드 풀의 hello 큐에 있는 작업 수입니다.|
|ShortParsingBusyThreads|스레드: 짧은 구문 분석 사용 중인 스레드|개수|평균|스레드 풀 구문 분석 짧은 hello 사용 중인 스레드 수입니다.|
|ShortParsingIdleThreads|스레드: 짧은 구문 분석 유휴 상태 스레드|개수|평균|스레드 풀 구문 분석 짧은 hello의 유휴 상태 스레드 수입니다.|
|ShortParsingJobQueueLength|스레드: 짧은 구문 분석 작업 큐 길이|개수|평균|스레드 풀 구문 분석 짧은 hello의 hello 큐에서 작업 수입니다.|
|memory_thrashing_metric|메모리 쓰래싱|백분율|평균|평균 메모리 쓰래싱입니다.|

## <a name="microsoftapimanagementservice"></a>Microsoft.ApiManagement/service

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|TotalRequests|총 게이트웨이 요청|개수|합계|게이트웨이 요청 수|
|SuccessfulRequests|성공적인 게이트웨이 요청|개수|합계|성공적인 게이트웨이 요청 수|
|UnauthorizedRequests|허가되지 않은 게이트웨이 요청|개수|합계|허가되지 않은 게이트웨이 요청 수|
|FailedRequests|실패한 게이트웨이 요청|개수|합계|게이트웨이 요청 실패 수|
|OtherRequests|기타 게이트웨이 요청|개수|합계|기타 게이트웨이 요청 수|

## <a name="microsoftbatchbatchaccounts"></a>Microsoft.Batch/batchAccounts

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|CoreCount|전용된 코어 수|개수|합계|Hello 일괄 처리 계정에 전용된 코어의 총 수|
|TotalNodeCount|전용된 노드 수|개수|합계|Hello 일괄 처리 계정에 대 한 전용 노드의 총 수|
|LowPriorityCoreCount|LowPriority 코어 수|개수|합계|Hello 일괄 처리 계정에 우선 순위가 낮은 코어의 총 수|
|TotalLowPriorityNodeCount|우선 순위가 낮은 노드 수|개수|합계|Hello 일괄 처리 계정에 대 한 우선 순위가 낮은 노드의 총 수|
|CreatingNodeCount|노드 수 만들기|개수|합계|만든 노드 수|
|StartingNodeCount|시작 노드 수|개수|합계|시작 노드 수|
|WaitingForStartTaskNodeCount|작업 시작 대기 노드 수|개수|합계|작업 시작 toocomplete hello에 대 한 대기 하는 노드 수|
|StartTaskFailedNodeCount|시작 작업 실패 노드 수|개수|합계|노드 hello 작업 시작에 실패 한 위치 수|
|IdleNodeCount|유휴 상태인 노드 수|개수|합계|유휴 노드 수|
|OfflineNodeCount|오프라인 노드 수|개수|합계|오프라인 노드 수|
|RebootingNodeCount|재부팅 노드 수|개수|합계|다시 부팅하는 노드의 수|
|ReimagingNodeCount|이미지로 다시 설치하는 노드 수|개수|합계|이미지로 다시 설치하는 노드의 수|
|RunningNodeCount|실행 노드 수|개수|합계|실행 중인 노드의 수|
|LeavingPoolNodeCount|나가는 풀 노드 수|개수|합계|Hello 풀을 유지 하는 노드 수|
|UnusableNodeCount|사용 불가 노드 수|개수|합계|사용할 수 없는 노드 수|
|PreemptedNodeCount|선점된 노드 수|개수|합계|선점된 노드 수|
|TaskStartEvent|작업 시작 이벤트|개수|합계|시작된 총 작업 수|
|TaskCompleteEvent|작업 완료 이벤트|개수|합계|완료된 총 작업 수|
|TaskFailEvent|작업 실패 이벤트|개수|합계|실패한 상태로 완료된 총 작업 수|
|PoolCreateEvent|풀 만들기 이벤트|개수|합계|만든 총 풀 수|
|PoolResizeStartEvent|풀 크기 조정 시작 이벤트|개수|합계|시작된 총 풀 크기 조정 작업 수|
|PoolResizeCompleteEvent|풀 크기 조정 완료 이벤트|개수|합계|완료된 총 풀 크기 조정 수|
|PoolDeleteStartEvent|풀 삭제 시작 이벤트|개수|합계|시작된 총 풀 삭제 수|
|PoolDeleteCompleteEvent|풀 삭제 완료 이벤트|개수|합계|완료된 총 풀 삭제 수|

## <a name="microsoftcacheredis"></a>Microsoft.Cache/redis

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|connectedclients|연결된 클라이언트|개수|최대||
|totalcommandsprocessed|총 작업|개수|합계||
|cachehits|캐시 적중|개수|합계||
|cachemisses|캐시 누락|개수|합계||
|getcommands|가져오기|개수|합계||
|setcommands|설정|개수|합계||
|evictedkeys|제거된 키|개수|합계||
|totalkeys|전체 키|개수|최대||
|expiredkeys|만료된 키|개수|합계||
|usedmemory|사용된 메모리|바이트|최대||
|usedmemoryRss|사용된 메모리 RSS|바이트|최대||
|serverLoad|서버 부하|백분율|최대||
|cacheWrite|캐시 쓰기|초당 바이트 수|최대||
|cacheRead|캐시 읽기|초당 바이트 수|최대||
|percentProcessorTime|CPU|백분율|최대||
|connectedclients0|연결된 클라이언트(분할 0)|개수|최대||
|totalcommandsprocessed0|총 작업(분할 0)|개수|합계||
|cachehits0|캐시 적중(분할 0)|개수|합계||
|cachemisses0|캐시 누락(분할 0)|개수|합계||
|getcommands0|가져오기(분할 0)|개수|합계||
|setcommands0|설정(분할 0)|개수|합계||
|evictedkeys0|제거된 키(분할 0)|개수|합계||
|totalkeys0|총 키(분할 0)|개수|최대||
|expiredkeys0|만료된 키(분할 0)|개수|합계||
|usedmemory0|사용된 메모리(분할 0)|바이트|최대||
|usedmemoryRss0|사용된 메모리 RSS(분할 0)|바이트|최대||
|serverLoad0|서버 부하(분할 0)|백분율|최대||
|cacheWrite0|캐시 쓰기(분할 0)|초당 바이트 수|최대||
|cacheRead0|캐시 읽기(분할 0)|초당 바이트 수|최대||
|percentProcessorTime0|CPU(분할 0)|백분율|최대||
|connectedclients1|연결된 클라이언트(분할 1)|개수|최대||
|totalcommandsprocessed1|총 작업(분할 1)|개수|합계||
|cachehits1|캐시 적중(분할 1)|개수|합계||
|cachemisses1|캐시 누락(분할 1)|개수|합계||
|getcommands1|가져오기(분할 1)|개수|합계||
|setcommands1|집합(분할 1)|개수|합계||
|evictedkeys1|제거된 키(분할 1)|개수|합계||
|totalkeys1|총 키(분할 1)|개수|최대||
|expiredkeys1|만료된 키(분할 1)|개수|합계||
|usedmemory1|사용된 메모리(분할 1)|바이트|최대||
|usedmemoryRss1|사용된 메모리 RSS(분할 1)|바이트|최대||
|serverLoad1|서버 부하(분할 1)|백분율|최대||
|cacheWrite1|캐시 쓰기(분할 1)|초당 바이트 수|최대||
|cacheRead1|캐시 읽기(분할 1)|초당 바이트 수|최대||
|percentProcessorTime1|CPU(분할 1)|백분율|최대||
|connectedclients2|연결된 클라이언트(분할 2)|개수|최대||
|totalcommandsprocessed2|총 작업(분할 2)|개수|합계||
|cachehits2|캐시 적중(분할 2)|개수|합계||
|cachemisses2|캐시 누락(분할 2)|개수|합계||
|getcommands2|가져오기(분할 2)|개수|합계||
|setcommands2|설정(분할 2)|개수|합계||
|evictedkeys2|제거된 키(분할 2)|개수|합계||
|totalkeys2|총 키(분할 2)|개수|최대||
|expiredkeys2|만료된 키(분할 2)|개수|합계||
|usedmemory2|사용된 메모리(분할 2)|바이트|최대||
|usedmemoryRss2|사용된 메모리 RSS(분할 2)|바이트|최대||
|serverLoad2|서버 부하(분할 2)|백분율|최대||
|cacheWrite2|캐시 쓰기(분할 2)|초당 바이트 수|최대||
|cacheRead2|캐시 읽기(분할 2)|초당 바이트 수|최대||
|percentProcessorTime2|CPU(분할 2)|백분율|최대||
|connectedclients3|연결된 클라이언트(분할 3)|개수|최대||
|totalcommandsprocessed3|총 작업(분할 3)|개수|합계||
|cachehits3|캐시 적중(분할 3)|개수|합계||
|cachemisses3|캐시 누락(분할 3)|개수|합계||
|getcommands3|가져오기(분할 3)|개수|합계||
|setcommands3|설정(분할 3)|개수|합계||
|evictedkeys3|제거된 키(분할 3)|개수|합계||
|totalkeys3|총 키(분할 3)|개수|최대||
|expiredkeys3|만료된 키(분할 3)|개수|합계||
|usedmemory3|사용된 메모리(분할 3)|바이트|최대||
|usedmemoryRss3|사용된 메모리 RSS(분할 3)|바이트|최대||
|serverLoad3|서버 부하(분할 3)|백분율|최대||
|cacheWrite3|캐시 쓰기(분할 3)|초당 바이트 수|최대||
|cacheRead3|캐시 읽기(분할 3)|초당 바이트 수|최대||
|percentProcessorTime3|CPU(분할 3)|백분율|최대||
|connectedclients4|연결된 클라이언트(분할 4)|개수|최대||
|totalcommandsprocessed4|총 작업(분할 4)|개수|합계||
|cachehits4|캐시 적중(분할 4)|개수|합계||
|cachemisses4|캐시 누락(분할 4)|개수|합계||
|getcommands4|가져오기(분할 4)|개수|합계||
|setcommands4|설정(분할 4)|개수|합계||
|evictedkeys4|제거된 키(분할 4)|개수|합계||
|totalkeys4|총 키(분할 4)|개수|최대||
|expiredkeys4|만료된 키(분할 4)|개수|합계||
|usedmemory4|사용된 메모리(분할 4)|바이트|최대||
|usedmemoryRss4|사용된 메모리 RSS(분할 4)|바이트|최대||
|serverLoad4|서버 부하(분할 4)|백분율|최대||
|cacheWrite4|캐시 쓰기(분할 4)|초당 바이트 수|최대||
|cacheRead4|캐시 읽기(분할 4)|초당 바이트 수|최대||
|percentProcessorTime4|CPU(분할 4)|백분율|최대||
|connectedclients5|연결된 클라이언트(분할 5)|개수|최대||
|totalcommandsprocessed5|총 작업(분할 5)|개수|합계||
|cachehits5|캐시 적중(분할 5)|개수|합계||
|cachemisses5|캐시 누락(분할 5)|개수|합계||
|getcommands5|가져오기(분할 5)|개수|합계||
|setcommands5|설정(분할 5)|개수|합계||
|evictedkeys5|제거된 키(분할 5)|개수|합계||
|totalkeys5|총 키(분할 5)|개수|최대||
|expiredkeys5|만료된 키(분할 5)|개수|합계||
|usedmemory5|사용된 메모리(분할 5)|바이트|최대||
|usedmemoryRss5|사용된 메모리 RSS(분할 5)|바이트|최대||
|serverLoad5|서버 부하(분할 5)|백분율|최대||
|cacheWrite5|캐시 쓰기(분할 5)|초당 바이트 수|최대||
|cacheRead5|캐시 읽기(분할 5)|초당 바이트 수|최대||
|percentProcessorTime5|CPU(분할 5)|백분율|최대||
|connectedclients6|연결된 클라이언트(분할 6)|개수|최대||
|totalcommandsprocessed6|총 작업(분할 6)|개수|합계||
|cachehits6|캐시 적중(분할 6)|개수|합계||
|cachemisses6|캐시 누락(분할 6)|개수|합계||
|getcommands6|가져오기(분할 6)|개수|합계||
|setcommands6|설정(분할 6)|개수|합계||
|evictedkeys6|제거된 키(분할 6)|개수|합계||
|totalkeys6|총 키(분할 6)|개수|최대||
|expiredkeys6|만료된 키(분할 6)|개수|합계||
|usedmemory6|사용된 메모리(분할 6)|바이트|최대||
|usedmemoryRss6|사용된 메모리 RSS(분할 6)|바이트|최대||
|serverLoad6|서버 부하(분할 6)|백분율|최대||
|cacheWrite6|캐시 쓰기(분할 6)|초당 바이트 수|최대||
|cacheRead6|캐시 읽기(분할 6)|초당 바이트 수|최대||
|percentProcessorTime6|CPU(분할 6)|백분율|최대||
|connectedclients7|연결된 클라이언트(분할 7)|개수|최대||
|totalcommandsprocessed7|총 작업(분할 7)|개수|합계||
|cachehits7|캐시 적중(분할 7)|개수|합계||
|cachemisses7|캐시 누락(분할 7)|개수|합계||
|getcommands7|가져오기(분할 7)|개수|합계||
|setcommands7|설정(분할 7)|개수|합계||
|evictedkeys7|제거된 키(분할 7)|개수|합계||
|totalkeys7|총 키(분할 7)|개수|최대||
|expiredkeys7|만료된 키(분할 7)|개수|합계||
|usedmemory7|사용된 메모리(분할 7)|바이트|최대||
|usedmemoryRss7|사용된 메모리 RSS(분할 7)|바이트|최대||
|serverLoad7|서버 부하(분할 7)|백분율|최대||
|cacheWrite7|캐시 쓰기(분할 7)|초당 바이트 수|최대||
|cacheRead7|캐시 읽기(분할 7)|초당 바이트 수|최대||
|percentProcessorTime7|CPU(분할 7)|백분율|최대||
|connectedclients8|연결된 클라이언트(분할 8)|개수|최대||
|totalcommandsprocessed8|총 작업(분할 8)|개수|합계||
|cachehits8|캐시 적중(분할 8)|개수|합계||
|cachemisses8|캐시 누락(분할 8)|개수|합계||
|getcommands8|가져오기(분할 8)|개수|합계||
|setcommands8|설정(분할 8)|개수|합계||
|evictedkeys8|제거된 키(분할 8)|개수|합계||
|totalkeys8|총 키(분할 8)|개수|최대||
|expiredkeys8|만료된 키(분할 8)|개수|합계||
|usedmemory8|사용된 메모리(분할 8)|바이트|최대||
|usedmemoryRss8|사용된 메모리 RSS(분할 8)|바이트|최대||
|serverLoad8|서버 부하(분할 8)|백분율|최대||
|cacheWrite8|캐시 쓰기(분할 8)|초당 바이트 수|최대||
|cacheRead8|캐시 읽기(분할 8)|초당 바이트 수|최대||
|percentProcessorTime8|CPU(분할 8)|백분율|최대||
|connectedclients9|연결된 클라이언트(분할 9)|개수|최대||
|totalcommandsprocessed9|총 작업(분할 9)|개수|합계||
|cachehits9|캐시 적중(분할 9)|개수|합계||
|cachemisses9|캐시 누락(분할 9)|개수|합계||
|getcommands9|가져오기(분할 9)|개수|합계||
|setcommands9|설정(분할 9)|개수|합계||
|evictedkeys9|제거된 키(분할 9)|개수|합계||
|totalkeys9|총 키(분할 9)|개수|최대||
|expiredkeys9|만료된 키(분할 9)|개수|합계||
|usedmemory9|사용된 메모리(분할 9)|바이트|최대||
|usedmemoryRss9|사용된 메모리 RSS(분할 9)|바이트|최대||
|serverLoad9|서버 부하(분할 9)|백분율|최대||
|cacheWrite9|캐시 쓰기(분할 9)|초당 바이트 수|최대||
|cacheRead9|캐시 읽기(분할 9)|초당 바이트 수|최대||
|percentProcessorTime9|CPU(분할 9)|백분율|최대||

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.CognitiveServices/accounts

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|TotalCalls|총 호출|개수|합계|총 호출 수.|
|SuccessfulCalls|성공한 호출|개수|합계|성공한 호출 수입니다.|
|TotalErrors|총 오류|개수|합계|오류 응답(HTTP 응답 코드 4xx 또는 5xx)이 있는 총 호출 수입니다.|
|BlockedCalls|차단된 호출|개수|합계|요금 또는 할당량 한도를 초과한 호출 수입니다.|
|ServerErrors|서버 오류|개수|합계|서비스 내부 오류(HTTP 응답 코드 5xx)가 있는 호출 수입니다.|
|ClientErrors|클라이언트 오류|개수|합계|클라이언트 쪽 오류(HTTP 응답 코드 4xx)가 있는 호출 수입니다.|
|DataIn|데이터 입력|바이트|합계|들어오는 데이터 크기(바이트)입니다.|
|DataOut|데이터 출력|바이트|합계|나가는 데이터 크기(바이트)입니다.|
|대기 시간|대기 시간|밀리초|평균|대기 시간(밀리초)입니다.|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.Compute/virtualMachines

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|백분율 CPU|백분율 CPU|백분율|평균|현재 hello 가상 컴퓨터에서 사용 중인 할당 된 계산 단위의 hello 백분율|
|네트워크 인|네트워크 인|바이트|합계|hello hello (들어오는 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 받은 바이트 수|
|네트워크 아웃|네트워크 아웃|바이트|합계|hello hello (송신 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 바이트 수|
|디스크 읽기 바이트|디스크 읽기 바이트|바이트|합계|모니터링 기간 동안 디스크에서 읽은 총 바이트|
|디스크 쓰기 바이트|디스크 쓰기 바이트|바이트|합계|Toodisk 기간을 모니터링 하는 동안 쓴 총 바이트|
|디스크 읽기 작업/초|디스크 읽기 작업/초|초당 개수|평균|디스크 읽기 IOPS|
|디스크 쓰기 작업/초|디스크 쓰기 작업/초|초당 개수|평균|디스크 쓰기 IOPS|

## <a name="microsoftcomputevirtualmachinescalesets"></a>Microsoft.Compute/virtualMachineScaleSets

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|백분율 CPU|백분율 CPU|백분율|평균|현재 hello 가상 컴퓨터에서 사용 중인 할당 된 계산 단위의 hello 백분율|
|네트워크 인|네트워크 인|바이트|합계|hello hello (들어오는 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 받은 바이트 수|
|네트워크 아웃|네트워크 아웃|바이트|합계|hello hello (송신 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 바이트 수|
|디스크 읽기 바이트|디스크 읽기 바이트|바이트|합계|모니터링 기간 동안 디스크에서 읽은 총 바이트|
|디스크 쓰기 바이트|디스크 쓰기 바이트|바이트|합계|Toodisk 기간을 모니터링 하는 동안 쓴 총 바이트|
|디스크 읽기 작업/초|디스크 읽기 작업/초|초당 개수|평균|디스크 읽기 IOPS|
|디스크 쓰기 작업/초|디스크 쓰기 작업/초|초당 개수|평균|디스크 쓰기 IOPS|

## <a name="microsoftcomputevirtualmachinescalesetsvirtualmachines"></a>Microsoft.Compute/virtualMachineScaleSets/virtualMachines

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|백분율 CPU|백분율 CPU|백분율|평균|현재 hello 가상 컴퓨터에서 사용 중인 할당 된 계산 단위의 hello 백분율|
|네트워크 인|네트워크 인|바이트|합계|hello hello (들어오는 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 받은 바이트 수|
|네트워크 아웃|네트워크 아웃|바이트|합계|hello hello (송신 트래픽) 가상 컴퓨터에서 모든 네트워크 인터페이스에서 바이트 수|
|디스크 읽기 바이트|디스크 읽기 바이트|바이트|합계|모니터링 기간 동안 디스크에서 읽은 총 바이트|
|디스크 쓰기 바이트|디스크 쓰기 바이트|바이트|합계|Toodisk 기간을 모니터링 하는 동안 쓴 총 바이트|
|디스크 읽기 작업/초|디스크 읽기 작업/초|초당 개수|평균|디스크 읽기 IOPS|
|디스크 쓰기 작업/초|디스크 쓰기 작업/초|초당 개수|평균|디스크 쓰기 IOPS|

## <a name="microsoftcustomerinsightshubs"></a>Microsoft.CustomerInsights/hubs

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|DCIApiCalls|Customer Insights API 호출 수|개수|합계||
|DCIMappingImportOperationSuccessfulLines|매핑 가져오기 작업 성공 줄 수|개수|합계||
|DCIMappingImportOperationFailedLines|매핑 가져오기 작업 실패 줄 수|개수|합계||
|DCIMappingImportOperationTotalLines|매핑 가져오기 작업 총 줄 수|개수|합계||
|DCIMappingImportOperationRuntimeInSeconds|매핑 가져오기 작업 런타임(초)|초|합계||
|DCIOutboundProfileExportSucceeded|아웃바운드 프로필 내보내기 성공|개수|합계||
|DCIOutboundProfileExportFailed|아웃바운드 프로필 내보내기 실패|개수|합계||
|DCIOutboundProfileExportDuration|아웃바운드 프로필 내보내기 기간|초|합계||
|DCIOutboundKpiExportSucceeded|아웃바운드 Kpi 내보내기 성공|개수|합계||
|DCIOutboundKpiExportFailed|아웃바운드 Kpi 내보내기 실패|개수|합계||
|DCIOutboundKpiExportDuration|아웃바운드 Kpi 내보내기 기간|초|합계||
|DCIOutboundKpiExportStarted|아웃바운드 Kpi 내보내기 시작|초|합계||
|DCIOutboundKpiRecordCount|아웃바운드 Kpi 레코드 수|초|합계||
|DCIOutboundProfileExportCount|아웃바운드 프로필 내보내기 수|초|합계||
|DCIOutboundInitialProfileExportFailed|아웃바운드 초기 프로필 내보내기 실패|초|합계||
|DCIOutboundInitialProfileExportSucceeded|아웃바운드 초기 프로필 내보내기 성공|초|합계||
|DCIOutboundInitialKpiExportFailed|아웃바운드 초기 Kpi 내보내기 실패|초|합계||
|DCIOutboundInitialKpiExportSucceeded|아웃바운드 초기 Kpi 내보내기 성공|초|합계||
|DCIOutboundInitialProfileExportDurationInSeconds|아웃바운드 초기 프로필 내보내기 기간(초)|초|합계||
|AdlaJobForStandardKpiFailed|표준 Kpi에 대한 Adla 작업 실패(초)|초|합계||
|AdlaJobForStandardKpiTimeOut|표준 Kpi에 대한 Adla 작업 시간 제한(초)|초|합계||
|AdlaJobForStandardKpiCompleted|표준 Kpi에 대한 Adla 작업 완료(초)|초|합계||
|ImportASAValuesFailed|ASA 값 가져오기 실패 수|개수|합계||
|ImportASAValuesSucceeded|ASA 값 가져오기 성공 수|개수|합계||

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.DataLakeAnalytics/accounts

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|JobEndedSuccess|성공한 작업|개수|합계|성공한 작업의 수입니다.|
|JobEndedFailure|실패한 작업|개수|합계|실패한 작업 수입니다.|
|JobEndedCancelled|취소된 작업|개수|합계|취소된 작업 수입니다.|
|JobAUEndedSuccess|성공한 AU 시간|초|합계|성공한 작업에 대한 총 AU 시간입니다.|
|JobAUEndedFailure|실패한 AU 시간|초|합계|실패한 작업에 대한 총 AU 시간입니다.|
|JobAUEndedCancelled|취소된 AU 시간|초|합계|취소된 작업에 대한 총 AU 시간입니다.|

## <a name="microsoftdbformysqlservers"></a>Microsoft.DBforMySQL/servers

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|cpu_percent|CPU 백분율|백분율|평균|CPU 백분율|
|compute_limit|계산 단위 제한|개수|평균|계산 단위 제한|
|compute_consumption_percent|계산 단위 백분율|백분율|평균|계산 단위 백분율|
|memory_percent|메모리 백분율|백분율|평균|메모리 백분율|
|io_consumption_percent|IO 백분율|백분율|평균|IO 백분율|
|storage_percent|저장소 비율|백분율|평균|저장소 비율|
|storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|
|storage_limit|저장소 제한|바이트|평균|저장소 제한|
|active_connections|전체 활성 연결|개수|평균|전체 활성 연결|
|connections_failed|실패한 전체 연결|개수|평균|실패한 전체 연결|

## <a name="microsoftdbforpostgresqlservers"></a>Microsoft.DBforPostgreSQL/servers

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|cpu_percent|CPU 백분율|백분율|평균|CPU 백분율|
|compute_limit|계산 단위 제한|개수|평균|계산 단위 제한|
|compute_consumption_percent|계산 단위 백분율|백분율|평균|계산 단위 백분율|
|memory_percent|메모리 백분율|백분율|평균|메모리 백분율|
|io_consumption_percent|IO 백분율|백분율|평균|IO 백분율|
|storage_percent|저장소 비율|백분율|평균|저장소 비율|
|storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|
|storage_limit|저장소 제한|바이트|평균|저장소 제한|
|active_connections|전체 활성 연결|개수|평균|전체 활성 연결|
|connections_failed|실패한 전체 연결|개수|평균|실패한 전체 연결|

## <a name="microsoftdevicesiothubs"></a>Microsoft.Devices/IotHubs

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|d2c.telemetry.ingress.allProtocol|원격 분석 메시지 보내기 시도|개수|합계|Tooyour IoT 허브를 전송 하는 원격 분석 장치-클라우드 메시지 시도한 toobe의 수|
|d2c.telemetry.ingress.success|보낸 원격 분석 메시지|개수|합계|원격 분석 장치-클라우드 메시지 수가 성공적으로 보낸 tooyour IoT 허브|
|c2d.commands.egress.complete.success|완료된 명령|개수|합계|클라우드-장치 명령 hello 장치에 의해 완료 수입니다.|
|c2d.commands.egress.abandon.success|중단된 명령|개수|합계|Hello 장치에 의해 중단 된 클라우드-장치 명령 수입니다.|
|c2d.commands.egress.reject.success|거부된 명령|개수|합계|Hello 장치에 의해 거부 클라우드-장치 명령 수입니다.|
|devices.totalDevices|총 장치|개수|합계|Tooyour IoT 허브 등록 된 장치 수|
|devices.connectedDevices.allProtocol|연결된 장치|개수|합계|Tooyour IoT 허브를 연결 된 장치 수|
|d2c.telemetry.egress.success|배달된 원격 분석 메시지|개수|합계|메시지 tooendpoints (합계)을 성공적으로 작성 된 횟수|
|d2c.telemetry.egress.dropped|삭제된 메시지|개수|합계|Hello 배달 끝점 데드 않아 삭제 된 메시지 수|
|d2c.telemetry.egress.orphaned|분리된 메시지|개수|합계|hello 메시지의 수 hello 대체 경로 포함 하 여 모든 경로 일치 하지 않습니다|
|d2c.telemetry.egress.invalid|잘못된 메시지|개수|합계|hello 메시지의 수 배달 되지 인해 tooincompatibility hello 끝점과|
|d2c.telemetry.egress.fallback|대체(fallback) 조건과 일치하는 메시지|개수|합계|대체 끝점 toohello 작성 된 메시지 수|
|d2c.endpoints.egress.eventHubs|메시지가 배달 tooEvent 허브 끝점|개수|합계|메시지가 성공적으로 작성 된 tooEvent 허브 끝점 된 횟수|
|d2c.endpoints.latency.eventHubs|이벤트 허브 끝점에 대한 메시지 대기 시간|밀리초|평균|밀리초에서의 이벤트 허브 끝점으로 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.serviceBusQueues|메시지가 배달 tooService 버스 큐 끝점|개수|합계|메시지 버스 큐 끝점 tooService 성공적으로 작성된 된 횟수|
|d2c.endpoints.latency.serviceBusQueues|Service Bus 큐 끝점에 대한 메시지 대기 시간|밀리초|평균|시간 (밀리초)에 있는 서비스 버스 큐 끝점에 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.serviceBusTopics|메시지가 배달 tooService 버스 항목 끝점|개수|합계|메시지 버스 항목 끝점 성공적으로 작성 된 tooService 된 횟수|
|d2c.endpoints.latency.serviceBusTopics|Service Bus 항목 끝점에 대한 메시지 대기 시간|밀리초|평균|시간 (밀리초)에 있는 서비스 버스 주제 끝점에 메시지 수신 toohello IoT hub 및 메시지 수신 간의 hello 평균 대기|
|d2c.endpoints.egress.builtIn.events|메시지가 배달 toohello 기본 제공 끝점 (메시지/이벤트)|개수|합계|메시지가 성공적으로 작성 된 toohello 기본 제공 끝점 (메시지/이벤트) 된 횟수|
|d2c.endpoints.latency.builtIn.events|Hello 기본 제공 끝점 (메시지/이벤트)에 대 한 메시지 대기 시간|밀리초|평균|hello 평균 대기 시간 메시지 수신 toohello IoT hub 및 메시지 수신 사이의 밀리초에서 hello 기본 제공 끝점 (메시지/이벤트) |
|d2c.twin.read.success|장치에서의 성공한 쌍 읽기|개수|합계|성공한 모든 장치에서 시작한로 이중 hello 수를 읽습니다.|
|d2c.twin.read.failure|장치에서의 실패한 쌍 읽기|개수|합계|모든의 hello 개수 장치 시작로 이중 읽기 실패 했습니다.|
|d2c.twin.read.size|장치에서의 쌍 읽기 응답 크기|바이트|평균|hello average, min, 및 최대 성공한 모든 장치에서 시작한로 이중 읽습니다.|
|d2c.twin.update.success|장치에서의 성공한 쌍 업데이트|개수|합계|성공한 모든 장치에서 시작한로 이중 업데이트 hello 수입니다.|
|d2c.twin.update.failure|장치에서의 실패한 쌍 업데이트|개수|합계|hello 수가 모두로 이중 장치에서 시작 된 업데이트에 실패 했습니다.|
|d2c.twin.update.size|장치에서의 쌍 업데이트 크기|바이트|평균|hello 평균, 최소값, 및 성공한 모든의 최대 크기 장치 시작로 이중 업데이트 합니다.|
|c2d.methods.success|성공한 직접 메서드 호출|개수|합계|성공한 모든 직접 메서드 호출의 hello 수입니다.|
|c2d.methods.failure|실패한 직접 메서드 호출|개수|합계|모든의 hello 개수 직접 메서드 호출에 실패 했습니다.|
|c2d.methods.requestSize|직접 메서드 호출의 요청 크기|바이트|평균|hello 평균, 최소 및 최대 성공한 모든 메서드가 요청에 전달 합니다.|
|c2d.methods.responseSize|직접 메서드 호출의 응답 크기|바이트|평균|hello average, min, 및 성공적인 직접적인 방법에 대 한 모든 응답의 최대값입니다.|
|c2d.twin.read.success|백 엔드에서의 성공한 쌍 읽기|개수|합계|성공한 모든 백 엔드 시작로 이중 hello 수를 읽습니다.|
|c2d.twin.read.failure|백 엔드에서의 실패한 쌍 읽기|개수|합계|모든의 hello 개수 읽기로 이중 백 엔드 시작 실패 했습니다.|
|c2d.twin.read.size|백 엔드에서의 쌍 읽기 응답 크기|바이트|평균|hello average, min, 및 최대 성공한 모든 백 엔드 시작로 이중 읽습니다.|
|c2d.twin.update.success|백 엔드에서의 성공한 쌍 업데이트|개수|합계|성공한 모든로 이중 백 엔드 시작 업데이트의 hello 수입니다.|
|c2d.twin.update.failure|백 엔드에서의 실패한 쌍 업데이트|개수|합계|모든의 hello 개수로 이중 백 엔드 시작 된 업데이트에 실패 했습니다.|
|c2d.twin.update.size|백 엔드에서의 쌍 업데이트 크기|바이트|평균|hello average, min, 및 성공한 모든의 최대 크기 백 엔드 시작로 이중 업데이트 합니다.|
|twinQueries.success|성공한 쌍 쿼리|개수|합계|모든 성공적인로 이중 쿼리의 hello 수입니다.|
|twinQueries.failure|실패한 쌍 쿼리|개수|합계|모든 실패 한로 이중 쿼리의 hello 수입니다.|
|twinQueries.resultSize|쌍 쿼리 결과 크기|바이트|평균|hello average, min, 및 모든 성공적인로 이중 쿼리의 hello 결과 크기의 최대값입니다.|
|jobs.createTwinUpdateJob.success|쌍 업데이트 작업에 대한 성공한 만들기|개수|합계|hello 모든 성공적으로 만드는 이중 업데이트 작업의 수입니다.|
|jobs.createTwinUpdateJob.failure|쌍 업데이트 작업에 대한 실패한 만들기|개수|합계|실패 한 모두로 이중 업데이트 작업 만들기의 hello 수입니다.|
|jobs.createDirectMethodJob.success|메서드 호출 작업에 대한 성공한 만들기|개수|합계|직접 메서드 호출 작업의 모든 성공적으로 만드는 hello 수입니다.|
|jobs.createDirectMethodJob.failure|실패한 메서드 호출 작업 만들기|개수|합계|직접 메서드 호출 작업의 모든 실패 한 만들기의 hello 수입니다.|
|jobs.listJobs.success|성공한 호출 toolist 작업|개수|합계|모든 호출이 성공 toolist 작업의 hello 수입니다.|
|jobs.listJobs.failure|실패 한 호출 toolist 작업|개수|합계|모든 실패 한 호출 toolist 작업의 hello 수입니다.|
|jobs.cancelJob.success|성공한 작업 취소|개수|합계|성공한 모든 hello 수 toocancel 작업을 호출합니다.|
|jobs.cancelJob.failure|실패한 작업 취소|개수|합계|모든 실패 한 호출 toocancel 작업의 hello 수입니다.|
|jobs.queryJobs.success|성공한 작업 쿼리|개수|합계|모든 호출이 성공 tooquery 작업의 hello 수입니다.|
|jobs.queryJobs.failure|실패한 작업 쿼리|개수|합계|모든 실패 한 호출 tooquery 작업의 hello 수입니다.|
|jobs.completed|완료된 작업|개수|합계|모든 완료 된 작업의 hello 수입니다.|
|jobs.failed|실패한 작업|개수|합계|모든 실패 한 작업의 hello 수입니다.|
|d2c.telemetry.ingress.sendThrottle|제한 오류 수|개수|합계|Toodevice 처리량 스로틀 인해 제한 오류 수|
|dailyMessageQuotaUsed|사용된 전체 메시지 수|개수|평균|현재 사용되는 전체 메시지 수|

## <a name="microsofteventhubnamespaces"></a>Microsoft.EventHub/namespaces

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|INREQS|들어오는 보내기 요청|개수|합계|알림 허브에 대해 들어오는 전체 보내기 요청|
|SUCCREQ|성공한 요청|개수|합계|네임스페이스에 대한 총 성공한 요청|
|FAILREQ|실패한 요청|개수|합계|네임스페이스에 대한 총 실패한 요청|
|SVRBSY|서버 작업 중 오류|개수|합계|네임스페이스에 대한 총 서버 작업 중 오류|
|INTERR|내부 서버 오류|개수|합계|네임스페이스에 대한 총 내부 서버 오류|
|MISCERR|다른 오류|개수|합계|네임스페이스에 대한 총 실패한 요청|
|INMSGS|들어오는 메시지 |개수|합계|네임스페이스에 대한 총 들어오는 메시지|
|OUTMSGS|보내는 메시지 |개수|합계|네임스페이스에 대한 총 나가는 메시지|
|EHINMBS|들어오는 바이트|바이트|합계|Event Hub 네임스페이스에 대한 들어오는 메시지 처리량|
|EHOUTMBS|나가는 바이트|바이트|합계|네임스페이스에 대한 총 나가는 메시지|
|EHABL|백로그 메시지 보관|개수|합계|Event Hub 네임스페이스에 대한 백로그에 메시지 보관|
|EHAMSGS|메시지 보관|개수|합계|Event Hub 네임스페이스에 보관된 메시지|
|EHAMBS|메시지 보관 처리량|바이트|합계|Event Hub 네임스페이스에서 보관된 메시지 처리량|

## <a name="microsoftlogicworkflows"></a>Microsoft.Logic/workflows

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|RunsStarted|실행 시작됨|개수|합계|실행 시작된 워크플로 수|
|RunsCompleted|실행 완료됨|개수|합계|실행 완료된 워크플로 수|
|RunsSucceeded|실행 성공함|개수|합계|실행 성공한 워크플로 수|
|RunsFailed|실행 실패함|개수|합계|실행 실패한 워크플로 수|
|RunsCancelled|실행 취소됨|개수|합계|실행 취소된 워크플로 수|
|RunLatency|실행 대기 시간|초|평균|완료된 워크플로 실행 대기 시간 |
|RunSuccessLatency|실행 성공 대기 시간|초|평균|성공한 워크플로 실행 대기 시간 |
|RunThrottledEvents|실행 제한 이벤트|개수|합계|워크플로 작업 또는 트리거 제한 이벤트 수|
|RunFailurePercentage|실행 오류 비율|백분율|합계|실행 실패한 워크플로 비율.|
|ActionsStarted|작업 시작됨 |개수|합계|시작된 워크플로 작업 수|
|ActionsCompleted|작업 완료됨 |개수|합계|완료된 워크플로 작업 수|
|ActionsSucceeded|작업 성공함 |개수|합계|성공한 워크플로 작업 수|
|ActionsFailed|작업 실패함|개수|합계|실패한 워크플로 작업 수|
|ActionsSkipped|작업 생략됨 |개수|합계|생략한 워크플로 작업 수|
|ActionLatency|작업 대기 시간 |초|평균|완료된 워크플로 작업 대기 시간 |
|ActionSuccessLatency|작업 성공 대기 시간 |초|평균|성공한 워크플로 작업 대기 시간 |
|ActionThrottledEvents|작업 제한 이벤트|개수|합계|워크플로 작업 제한 이벤트 수|
|TriggersStarted|트리거 시작됨 |개수|합계|시작된 워크플로 트리거 수|
|TriggersCompleted|트리거 완료됨 |개수|합계|완료된 워크플로 트리거 수|
|TriggersSucceeded|트리거 성공함 |개수|합계|성공한 워크플로 트리거 수|
|TriggersFailed|트리거 실패함 |개수|합계|실패한 워크플로 트리거 수|
|TriggersSkipped|트리거 생략함|개수|합계|생략한 워크플로 트리거 수|
|TriggersFired|트리거 실행됨 |개수|합계|실행한 워크플로 트리거 수|
|TriggerLatency|트리거 대기 시간 |초|평균|완료된 워크플로 트리거 대기 시간 |
|TriggerFireLatency|트리거 실행 대기 시간 |초|평균|실행한 워크플로 트리거 대기 시간|
|TriggerSuccessLatency|트리거 성공 대기 시간 |초|평균|성공한 워크플로 트리거 대기 시간|
|TriggerThrottledEvents|트리거 제한 이벤트|개수|합계|워크플로 트리거 제한 이벤트 수|
|BillableActionExecutions|청구 가능한 작업 실행|개수|합계|청구되는 워크플로 작업 실행 수.|
|BillableTriggerExecutions|청구 가능한 트리거 실행|개수|합계|청구되는 워크플로 트리거 실행 수.|
|TotalBillableExecutions|총 청구 가능 실행|개수|합계|청구되는 워크플로 실행 수.|

## <a name="microsoftnetworkapplicationgateways"></a>Microsoft.Network/applicationGateways

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|처리량|처리량|초당 바이트 수|평균||

## <a name="microsoftnetworkexpressroutecircuits"></a>Microsoft.Network/expressRouteCircuits

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|BytesIn|BytesIn|개수|합계||
|BytesOut|BytesOut|개수|합계||

## <a name="microsoftnotificationhubsnamespacesnotificationhubs"></a>Microsoft.NotificationHubs/Namespaces/NotificationHubs

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|registration.all|등록 작업|개수|합계|hello 성공한 모든 등록 작업 (업데이트 쿼리 만들기 및 삭제) 수입니다. |
|registration.create|등록 만들기 작업|개수|합계|성공한 모든 등록 만들기의 hello 수입니다.|
|registration.update|등록 업데이트 작업|개수|합계|성공한 모든 등록 업데이트의 hello 수입니다.|
|registration.get|등록 읽기 작업|개수|합계|모든 성공적인 등록 쿼리의 hello 수입니다.|
|registration.delete|등록 삭제 작업|개수|합계|성공한 모든 등록 삭제의 hello 수입니다.|
|incoming|들어오는 메시지 |개수|합계|hello 수가 성공한 모든 보내기 API 호출 합니다. |
|incoming.scheduled|전송된 예약된 푸시 알림|개수|합계|취소된 예약된 푸시 알림|
|incoming.scheduled.cancel|취소된 예약된 푸시 알림|개수|합계|취소된 예약된 푸시 알림|
|scheduled.pending|보류 중인 예약된 알림|개수|합계|보류 중인 예약된 알림|
|installation.all|설치 관리 작업|개수|합계|설치 관리 작업|
|installation.get|설치 작업 가져오기|개수|합계|설치 작업 가져오기|
|installation.upsert|설치 작업 만들기 또는 업데이트|개수|합계|설치 작업 만들기 또는 업데이트|
|installation.patch|설치 작업 패치|개수|합계|설치 작업 패치|
|installation.delete|설치 작업 삭제|개수|합계|설치 작업 삭제|
|outgoing.allpns.success|성공적인 알림|개수|합계|성공한 모든 알림의 hello 수입니다.|
|outgoing.allpns.invalidpayload|페이로드 오류|개수|합계|hello PNS 반환 된 잘못 된 페이로드 오류 때문에 실패 한 푸시의 수를 hello입니다.|
|outgoing.allpns.pnserror|외부 알림 시스템 오류|개수|합계|hello PNS (인증 문제는 제외)와 통신에 문제가 있기 때문에 실패 한 푸시의 수를 hello입니다.|
|outgoing.allpns.channelerror|채널 오류|개수|합계|hello 채널이 잘못 되었거나 올바른 앱 정체 또는 만료 hello와 연결 되지 않은 때문에 실패 한 푸시의 hello 수 있습니다.|
|outgoing.allpns.badorexpiredchannel|잘못되거나 만료된 채널 오류|개수|합계|hello 채널/token/registrationId hello 등록이 만료 되었거나 잘못 때문에 실패 한 푸시의 hello 수 있습니다.|
|outgoing.wns.success|WNS 성공적인 알림|개수|합계|성공한 모든 알림의 hello 수입니다.|
|outgoing.wns.invalidcredentials|WNS 권한 부여 오류(잘못된 자격 증명)|개수|합계|hello PNS에서 자격 증명이 나 hello 차단 된 hello 제공 받아들이지 않으므로 실패 한 푸시의 hello 수 있습니다. (Windows Live 인식 하지 못합니다 hello 자격 증명).|
|outgoing.wns.badchannel|WNS 잘못된 채널 오류|개수|합계|hello hello 등록의 ChannelURI hello 인식 되지 않아 실패 한 푸시의 수입니다 (WNS 상태: 404 찾을 수 없음).|
|outgoing.wns.expiredchannel|WNS 만료된 채널 오류|개수|합계|hello hello ChannelURI가 만료 되어 실패 한 푸시의 수입니다 (WNS 상태: 410 없음).|
|outgoing.wns.throttled|WNS 제한된 알림|개수|합계|hello WNS이이 응용 프로그램을 조절 하 여 실패 한 푸시의 수입니다 (WNS 상태: 406 허용 되지 않습니다).|
|outgoing.wns.tokenproviderunreachable|WNS 권한 부여 오류(연결할 수 없음)|개수|합계|Windows Live에 연결할 수 없습니다.|
|outgoing.wns.invalidtoken|WNS 권한 부여 오류(잘못된 토큰)|개수|합계|hello 토큰이 제공 tooWNS 잘못 되었습니다 (WNS 상태: 401 권한 없음).|
|outgoing.wns.wrongtoken|WNS 권한 부여 오류(잘못된 토큰)|개수|합계|제공 된 tooWNS는 유효 하지만 다른 응용 프로그램에 대 한 토큰을 hello (WNS 상태: 403 사용할 수 없음). 이 hello 등록의 ChannelURI hello는 다른 앱과 연결 하는 경우 발생할 수 있습니다. Hello와 연결 된 해당 hello 클라이언트 응용 프로그램 확인 hello 알림 허브에 자격 증명이 있는 동일한 응용 프로그램입니다.|
|outgoing.wns.invalidnotificationformat|WNS 잘못된 알림 형식|개수|합계|hello 알림의 hello 형식이 잘못 되었습니다 (WNS 상태: 400). WNS가 잘못된 모든 페이로드를 거부하지는 않습니다.|
|outgoing.wns.invalidnotificationsize|WNS 잘못된 알림 크기 오류|개수|합계|hello 알림 페이로드가 너무 큽니다 (WNS 상태: 413).|
|outgoing.wns.channelthrottled|WNS 채널 제한|개수|합계|스로틀 되는 hello 등록의 ChannelURI hello hello 알림이 삭제 되었습니다 (WNS 응답 헤더: X-WNS-NotificationStatus:channelThrottled).|
|outgoing.wns.channeldisconnected|WNS 채널 연결 끊김|개수|합계|스로틀 되는 hello 등록의 ChannelURI hello hello 알림이 삭제 되었습니다 (WNS 응답 헤더: DeviceConnectionStatus-WNS-X: 연결 끊김).|
|outgoing.wns.dropped|WNS 삭제된 알림|개수|합계|스로틀 되는 hello 등록의 ChannelURI hello hello 알림이 삭제 되었습니다 (X-WNS-NotificationStatus: 삭제 하지만 하지: X-WNS-DeviceConnectionStatus: 연결 끊김).|
|outgoing.wns.pnserror|WNS 오류|개수|합계|WNS와의 통신 오류로 인해 알림이 배달되지 않습니다.|
|outgoing.wns.authenticationerror|WNS 인증 오류|개수|합계|Windows Live와의 통신 오류(잘못된 자격 증명 또는 잘못된 토큰)로 인해 알림이 배달되지 않습니다.|
|outgoing.apns.success|APNS 성공적인 알림|개수|합계|성공한 모든 알림의 hello 수입니다.|
|outgoing.apns.invalidcredentials|APNS 권한 부여 오류|개수|합계|hello PNS에서 자격 증명이 나 hello 차단 된 hello 제공 받아들이지 않으므로 실패 한 푸시의 hello 수 있습니다.|
|outgoing.apns.badchannel|APNS 잘못된 채널 오류|개수|합계|hello hello 토큰이 잘못 되었습니다. 실패 한 푸시의 수입니다 (APNS 상태 코드: 8).|
|outgoing.apns.expiredchannel|APNS 만료된 채널 오류|개수|합계|hello APNS 피드백 채널에서 무효화 된 토큰의 hello 수입니다.|
|outgoing.apns.invalidnotificationsize|APNS 잘못된 알림 크기 오류|개수|합계|hello hello 페이로드가 너무 커서 실패 한 푸시의 수입니다 (APNS 상태 코드: 7).|
|outgoing.apns.pnserror|APNS 오류|개수|합계|APNS와의 통신 오류로 인해 실패 한 푸시의 hello 수입니다.|
|outgoing.gcm.success|GCM 성공적인 알림|개수|합계|성공한 모든 알림의 hello 수입니다.|
|outgoing.gcm.invalidcredentials|GCM 권한 부여 오류(잘못된 자격 증명)|개수|합계|hello PNS에서 자격 증명이 나 hello 차단 된 hello 제공 받아들이지 않으므로 실패 한 푸시의 hello 수 있습니다.|
|outgoing.gcm.badchannel|GCM 잘못된 채널 오류|개수|합계|hello hello 등록의 registrationId hello 인식 되지 않아 실패 한 푸시의 수입니다 (GCM 결과: 잘못 된 등록).|
|outgoing.gcm.expiredchannel|GCM 만료된 채널 오류|개수|합계|hello hello 등록의 hello registrationId가 만료 되어 실패 한 푸시의 수입니다 (GCM 결과: NotRegistered).|
|outgoing.gcm.throttled|GCM 제한된 알림|개수|합계|hello GCM이이 앱을 제한 하기 때문에 실패 한 푸시의 수입니다 (GCM 상태 코드: 501-599 또는 결과: 사용할 수 없음).|
|outgoing.gcm.invalidnotificationformat|GCM 잘못된 알림 형식|개수|합계|hello hello 페이로드 형식이 올바르지 않습니다. 실패 한 푸시의 수입니다 (GCM 결과: InvalidDataKey 또는 InvalidTtl).|
|outgoing.gcm.invalidnotificationsize|GCM 잘못된 알림 크기 오류|개수|합계|hello hello 페이로드가 너무 커서 실패 한 푸시의 수입니다 (GCM 결과: MessageTooBig).|
|outgoing.gcm.wrongchannel|GCM 잘못된 채널 오류|개수|합계|hello 등록의 registrationId hello 없기 때문에 실패 한 푸시의 수 hello toohello 현재 앱에 연결 (GCM 결과: InvalidPackageName).|
|outgoing.gcm.pnserror|GCM 오류|개수|합계|GCM과의 통신 오류로 인해 실패 한 푸시의 hello 수입니다.|
|outgoing.gcm.authenticationerror|GCM 인증 오류|개수|합계|hello PNS 자격 증명 hello 자격 증명이 차단 hello 제공을 수락 하지 않았거나 hello 또는 hello SenderId가 hello 응용 프로그램에서 올바르게 구성 되지 않아 실패 한 푸시의 수입니다 (GCM 결과: MismatchedSenderId).|
|outgoing.mpns.success|MPNS 성공적인 알림|개수|합계|성공한 모든 알림의 hello 수입니다.|
|outgoing.mpns.invalidcredentials|MPNS 잘못된 자격 증명|개수|합계|hello PNS에서 자격 증명이 나 hello 차단 된 hello 제공 받아들이지 않으므로 실패 한 푸시의 hello 수 있습니다.|
|outgoing.mpns.badchannel|MPNS 잘못된 채널 오류|개수|합계|hello hello 등록의 ChannelURI hello 인식 되지 않아 실패 한 푸시의 수입니다 (MPNS 상태: 404 찾을 수 없음).|
|outgoing.mpns.throttled|MPNS 제한된 알림|개수|합계|hello MPNS이이 응용 프로그램을 조절 하 여 실패 한 푸시의 수입니다 (WNS MPNS: 406 허용 되지 않습니다).|
|outgoing.mpns.invalidnotificationformat|MPNS 잘못된 알림 형식|개수|합계|hello 알림의 hello 페이로드가 너무 커서 때문에 실패 한 푸시의 hello 수입니다.|
|outgoing.mpns.channeldisconnected|MPNS 채널 연결 끊김|개수|합계|hello hello 등록의 ChannelURI hello 연결이 끊어졌습니다. 실패 한 푸시의 수입니다 (MPNS 상태: 412 찾을 수 없음).|
|outgoing.mpns.dropped|MPNS 삭제된 알림|개수|합계|hello MPNS에 의해 삭제 된 푸시의 수입니다 (MPNS 응답 헤더: X NotificationStatus: QueueFull 또는 억제).|
|outgoing.mpns.pnserror|MPNS 오류|개수|합계|MPNS와의 통신 오류로 인해 실패 한 푸시의 hello 수입니다.|
|outgoing.mpns.authenticationerror|MPNS 인증 오류|개수|합계|hello PNS에서 자격 증명이 나 hello 차단 된 hello 제공 받아들이지 않으므로 실패 한 푸시의 hello 수 있습니다.|
|notificationhub.pushes|모든 나가는 알림 수|개수|합계|Hello 알림 허브의 모든 나가는 알림|
|incoming.all.requests|들어오는 모든 요청|개수|합계|알림 허브에 대해 들어오는 전체 요청|
|incoming.all.failedrequests|들어오는 모든 실패한 요청|개수|합계|알림 허브에 대해 들어오는 실패한 전체 요청|

## <a name="microsoftpowerbidedicatedcapacities"></a>Microsoft.PowerBIDedicated/capacities

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|qpu_metric|QPU|개수|평균|QPU. 범위는 S1의 경우 0-100, S2의 경우 0-200, S4의 경우 0-400임|
|memory_metric|메모리|바이트|평균|메모리. 범위는 S1의 경우 0-25GB, S2의 경우 0-50GB, S4의 경우 0-100GB임|
|TotalConnectionRequests|총 연결 요청 수|개수|평균|도착한 총 연결 요청 수입니다.|
|SuccessfullConnectionsPerSec|초당 성공한 연결 수|초당 개수|평균|성공적으로 완료된 연결 비율입니다.|
|TotalConnectionFailures|총 연결 실패 수|개수|평균|실패한 총 연결 시도 수입니다.|
|CurrentUserSessions|현재 사용자 세션 수|개수|평균|현재 설정된 사용자 세션 수입니다.|
|QueryPoolBusyThreads|쿼리 풀의 사용 중인 스레드|개수|평균|hello 쿼리 스레드 풀에서 사용 중인 스레드 수입니다.|
|CommandPoolJobQueueLength|명령 풀의 작업 큐 길이|개수|평균|Hello 명령 스레드 풀의 hello 큐에 있는 작업 수입니다.|
|ProcessingPoolJobQueueLength|처리 풀의 작업 큐 길이|개수|평균|스레드 풀을 처리 하는 hello의 hello 큐에 비-I/o 작업 수입니다.|
|CurrentConnections|연결: 현재 연결|개수|평균|현재 설정된 클라이언트 연결 수입니다.|
|CleanerCurrentPrice|메모리: 클리너 현재 가격|개수|평균|메모리, $/ 바이트/시간, 정규화 된 too1000의 현재 가격입니다.|
|CleanerMemoryShrinkable|메모리: 클리너 메모리 축소 가능|바이트|평균|메모리의 양 (바이트)에서 hello 백그라운드 클리너로 주체 toopurging 합니다.|
|CleanerMemoryNonshrinkable|메모리: 클리너 메모리 축소 불가능|바이트|평균|메모리의 양 (바이트)에서 hello 백그라운드 클리너로 주체 toopurging 되지 않습니다.|
|MemoryUsage|메모리: 메모리 사용량|바이트|평균|더욱 명확한 메모리 비용 계산에 사용 되는 hello 서버 프로세스의 메모리 사용량입니다. 같은 toocounter Process\PrivateBytes hello와 크기를 더한 메모리 매핑된 데이터를 메모리 매핑 되었거나 hello xVelocity 메모리 내 분석 엔진 (VertiPaq) hello xVelocity 엔진 Memory Limit를 초과 하 여 할당 된는 무시 합니다.|
|MemoryLimitHard|메모리: 메모리 제한 하드|바이트|평균|하드 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitHigh|메모리: 메모리 제한 상한|바이트|평균|상한 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitLow|메모리: 메모리 제한 하한|바이트|평균|하한 메모리 제한, 구성 파일 원본입니다.|
|MemoryLimitVertiPaq|메모리: 메모리 제한 VertiPaq|바이트|평균|메모리 내 제한, 구성 파일 원본입니다.|
|할당량|메모리: 할당량|바이트|평균|현재 메모리 할당량, 바이트 단위입니다. 메모리 할당량은 메모리 부여 또는 메모리 예약이라고도 합니다.|
|QuotaBlocked|메모리: 차단된 할당량|개수|평균|다른 메모리 할당량이 해제될 때까지 차단되는 할당량 요청의 현재 수입니다.|
|VertiPaqNonpaged|메모리: 페이징되지 않은 VertiPaq|바이트|평균|바이트의 메모리 사용에 대 한 hello 작업 집합에 hello 메모리 내 엔진에 의해 잠겼습니다.|
|VertiPaqPaged|메모리: 페이징된 VertiPaq|바이트|평균|메모리 내 데이터에 사용 중인 페이징된 메모리 바이트입니다.|
|RowsReadPerSec|처리: 초당 읽은 행|초당 개수|평균|모든 관계형 데이터베이스에서 읽은 행의 비율입니다.|
|RowsConvertedPerSec|처리: 초당 변환된 행|초당 개수|평균|처리하는 동안 변환된 행의 비율입니다.|
|RowsWrittenPerSec|처리: 초당 작성된 행|초당 개수|평균|처리하는 동안 작성된 행의 비율입니다.|
|CommandPoolBusyThreads|스레드: 명령 풀 사용 중인 스레드|개수|평균|hello 명령 스레드 풀에서 사용 중인 스레드 수입니다.|
|CommandPoolIdleThreads|스레드: 명령 풀 유휴 상태 스레드|개수|평균|Hello 명령 스레드 풀의 유휴 상태 스레드 수입니다.|
|LongParsingBusyThreads|스레드: 긴 구문 분석 사용 중인 스레드|개수|평균|긴 스레드 풀 구문 분석 하는 hello 사용 중인 스레드 수입니다.|
|LongParsingIdleThreads|스레드: 긴 구문 분석 유휴 상태 스레드|개수|평균|긴 스레드 풀 구문 분석 하는 hello의 유휴 상태 스레드 수입니다.|
|LongParsingJobQueueLength|스레드: 긴 구문 분석 작업 큐 길이|개수|평균|긴 스레드 풀 구문 분석 하는 hello의 hello 큐에서 작업 수입니다.|
|ProcessingPoolBusyIOJobThreads|스레드: 처리 풀 사용 중인 I/O 작업 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업을 실행 중인 스레드 수입니다.|
|ProcessingPoolBusyNonIOThreads|스레드: 처리 풀 사용 중인 비-I/O 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 비-I/o 작업을 실행 중인 스레드 수입니다.|
|ProcessingPoolIOJobQueueLength|스레드: 처리 풀 I/O 작업 큐 길이|개수|평균|스레드 풀을 처리 하는 hello의 hello 큐에서 I/O 작업 수입니다.|
|ProcessingPoolIdleIOJobThreads|스레드: 처리 풀 유휴 상태 I/O 작업 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업에 대 한 유휴 상태 스레드 수입니다.|
|ProcessingPoolIdleNonIOThreads|스레드: 처리 풀 유휴 상태 비-I/O 스레드|개수|평균|스레드 풀을 처리 하는 hello에 유휴 상태 스레드 수는 toonon-I/o 작업 전용입니다.|
|QueryPoolIdleThreads|스레드: 쿼리 풀 유휴 상태 스레드|개수|평균|스레드 풀을 처리 하는 hello에서 I/O 작업에 대 한 유휴 상태 스레드 수입니다.|
|QueryPoolJobQueueLength|스레드: 쿼리 풀 작업 큐 길이|개수|평균|Hello 쿼리 스레드 풀의 hello 큐에 있는 작업 수입니다.|
|ShortParsingBusyThreads|스레드: 짧은 구문 분석 사용 중인 스레드|개수|평균|스레드 풀 구문 분석 짧은 hello 사용 중인 스레드 수입니다.|
|ShortParsingIdleThreads|스레드: 짧은 구문 분석 유휴 상태 스레드|개수|평균|스레드 풀 구문 분석 짧은 hello의 유휴 상태 스레드 수입니다.|
|ShortParsingJobQueueLength|스레드: 짧은 구문 분석 작업 큐 길이|개수|평균|스레드 풀 구문 분석 짧은 hello의 hello 큐에서 작업 수입니다.|
|memory_thrashing_metric|메모리 쓰래싱|백분율|평균|평균 메모리 쓰래싱입니다.|

## <a name="microsoftsearchsearchservices"></a>Microsoft.Search/searchServices

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|SearchLatency|검색 대기 시간|초|평균|Hello 검색 서비스에 대 한 평균 검색 대기 시간|
|SearchQueriesPerSecond|초당 검색 쿼리 수|초당 개수|평균|Hello 검색 서비스에 대 한 초당 검색 쿼리|
|ThrottledSearchQueriesPercentage|제한된 검색 쿼리 백분율|백분율|평균|Hello 검색 서비스에 대 한 제한 된 검색 쿼리의 비율|

## <a name="microsoftservicebusnamespaces"></a>Microsoft.ServiceBus/namespaces

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|CPUXNS|네임스페이스당 CPU 사용량|백분율|최대|서비스 버스 프리미엄 네임스페이스 CPU 사용량 메트릭|
|WSXNS|네임스페이스당 메모리 크기 사용|백분율|최대|서비스 버스 프리미엄 네임스페이스 메모리 사용량 메트릭|

## <a name="microsoftsqlserversdatabases"></a>Microsoft.Sql/servers/databases

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|cpu_percent|CPU 비율|백분율|평균|CPU 비율|
|physical_data_read_percent|데이터 IO 비율|백분율|평균|데이터 IO 비율|
|log_write_percent|로그 IO 비율|백분율|평균|로그 IO 비율|
|dtu_consumption_percent|DTU 비율|백분율|평균|DTU 비율|
|저장소|총 데이터베이스 크기|바이트|최대|총 데이터베이스 크기|
|connection_successful|성공적인 연결|개수|합계|성공적인 연결|
|connection_failed|실패한 연결|개수|합계|실패한 연결|
|blocked_by_firewall|방화벽에 의해 차단|개수|합계|방화벽에 의해 차단|
|교착 상태|교착 상태|개수|합계|교착 상태|
|storage_percent|데이터베이스 크기 비율|백분율|최대|데이터베이스 크기 비율|
|xtp_storage_percent|메모리 내 OLTP 저장소 백분율|백분율|평균|메모리 내 OLTP 저장소 백분율|
|workers_percent|작업자 백분율|백분율|평균|작업자 백분율|
|sessions_percent|세션 백분율|백분율|평균|세션 백분율|
|dtu_limit|DTU 제한|개수|평균|DTU 제한|
|dtu_used|DTU 사용됨|개수|평균|DTU 사용됨|
|dwu_limit|DWU 제한|개수|최대|DWU 제한|
|dwu_consumption_percent|DWU 백분율|백분율|최대|DWU 백분율|
|dwu_used|DWU 사용됨|개수|최대|DWU 사용됨|

## <a name="microsoftsqlserverselasticpools"></a>Microsoft.Sql/servers/elasticPools

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|cpu_percent|CPU 비율|백분율|평균|CPU 비율|
|database_cpu_percent|CPU 비율|백분율|평균|CPU 비율|
|physical_data_read_percent|데이터 IO 비율|백분율|평균|데이터 IO 비율|
|database_physical_data_read_percent|데이터 IO 비율|백분율|평균|데이터 IO 비율|
|log_write_percent|로그 IO 비율|백분율|평균|로그 IO 비율|
|database_log_write_percent|로그 IO 비율|백분율|평균|로그 IO 비율|
|dtu_consumption_percent|DTU 비율|백분율|평균|DTU 비율|
|database_dtu_consumption_percent|DTU 비율|백분율|평균|DTU 비율|
|storage_percent|저장소 비율|백분율|평균|저장소 비율|
|workers_percent|작업자 백분율|백분율|평균|작업자 백분율|
|database_workers_percent|작업자 백분율|백분율|평균|작업자 백분율|
|sessions_percent|세션 백분율|백분율|평균|세션 백분율|
|database_sessions_percent|세션 백분율|백분율|평균|세션 백분율|
|eDTU_limit|eDTU 제한|개수|평균|eDTU 제한|
|storage_limit|저장소 제한|바이트|평균|저장소 제한|
|eDTU_used|eDTU 사용|개수|평균|eDTU 사용|
|storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|
|database_storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|
|xtp_storage_percent|메모리 내 OLTP 저장소 백분율|백분율|평균|메모리 내 OLTP 저장소 백분율|

## <a name="microsoftsqlservers"></a>Microsoft.Sql/servers

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|dtu_consumption_percent|DTU 비율|백분율|평균|DTU 비율|
|database_dtu_consumption_percent|DTU 비율|백분율|평균|DTU 비율|
|storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|
|database_storage_used|저장소 사용됨|바이트|평균|저장소 사용됨|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|ResourceUtilization|SU % 사용률|백분율|최대|SU % 사용률|
|InputEvents|입력 이벤트|개수|합계|입력 이벤트|
|InputEventBytes|입력 이벤트 바이트|바이트|합계|입력 이벤트 바이트|
|LateInputEvents|늦은 입력 이벤트|개수|합계|늦은 입력 이벤트|
|OutputEvents|출력 이벤트|개수|합계|출력 이벤트|
|ConversionErrors|데이터 변환 오류|개수|합계|데이터 변환 오류|
|오류|런타임 오류|개수|합계|런타임 오류|
|DroppedOrAdjustedEvents|잘못된 이벤트|개수|합계|잘못된 이벤트|
|AMLCalloutRequests|기능 요청|개수|합계|기능 요청|
|AMLCalloutFailedRequests|실패한 기능 요청|개수|합계|실패한 기능 요청|
|AMLCalloutInputEvents|함수 이벤트|개수|합계|함수 이벤트|

## <a name="microsoftwebserverfarms"></a>Microsoft.Web/serverfarms

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|CpuPercentage|CPU 비율|백분율|평균|CPU 비율|
|MemoryPercentage|메모리 비율|백분율|평균|메모리 비율|
|DiskQueueLength|디스크 큐 길이|개수|합계|디스크 큐 길이|
|HttpQueueLength|Http 큐 길이|개수|합계|Http 큐 길이|
|BytesReceived|데이터 입력|바이트|합계|데이터 입력|
|BytesSent|데이터 출력|바이트|합계|데이터 출력|

## <a name="microsoftwebsites-excluding-functions"></a>Microsoft.Web/sites(Functions 제외)

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|CpuTime|CPU 시간|초|합계|CPU 시간|
|요청|요청|개수|합계|요청|
|BytesReceived|데이터 입력|바이트|합계|데이터 입력|
|BytesSent|데이터 출력|바이트|합계|데이터 출력|
|Http101|Http 101|개수|합계|Http 101|
|Http2xx|Http 2xx|개수|합계|Http 2xx|
|Http3xx|Http 3xx|개수|합계|Http 3xx|
|Http401|Http 401|개수|합계|Http 401|
|Http403|Http 403|개수|합계|Http 403|
|Http404|Http 404|개수|합계|Http 404|
|Http406|Http 406|개수|합계|Http 406|
|Http4xx|Http 4xx|개수|합계|Http 4xx|
|Http5xx|Http 서버 오류|개수|합계|Http 서버 오류|
|MemoryWorkingSet|메모리 작업 집합|바이트|평균|메모리 작업 집합|
|AverageMemoryWorkingSet|평균 메모리 작업 집합|바이트|평균|평균 메모리 작업 집합|
|AverageResponseTime|평균 응답 시간|초|평균|평균 응답 시간|

## <a name="microsoftwebsites-functions"></a>Microsoft.Web/sites(functions)

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|BytesReceived|데이터 입력|바이트|합계|데이터 입력|
|BytesSent|데이터 출력|바이트|합계|데이터 출력|
|Http5xx|Http 서버 오류|개수|합계|Http 서버 오류|
|MemoryWorkingSet|메모리 작업 집합|바이트|평균|메모리 작업 집합|
|AverageMemoryWorkingSet|평균 메모리 작업 집합|바이트|평균|평균 메모리 작업 집합|
|FunctionExecutionUnits|함수 실행 단위|개수|평균|함수 실행 단위|
|FunctionExecutionCount|함수 실행 횟수|개수|평균|함수 실행 횟수|

## <a name="microsoftwebsitesslots"></a>Microsoft.Web/sites/slots

|메트릭|메트릭 표시 이름|단위|집계 형식|설명|
|---|---|---|---|---|
|CpuTime|CPU 시간|초|합계|CPU 시간|
|요청|요청|개수|합계|요청|
|BytesReceived|데이터 입력|바이트|합계|데이터 입력|
|BytesSent|데이터 출력|바이트|합계|데이터 출력|
|Http101|Http 101|개수|합계|Http 101|
|Http2xx|Http 2xx|개수|합계|Http 2xx|
|Http3xx|Http 3xx|개수|합계|Http 3xx|
|Http401|Http 401|개수|합계|Http 401|
|Http403|Http 403|개수|합계|Http 403|
|Http404|Http 404|개수|합계|Http 404|
|Http406|Http 406|개수|합계|Http 406|
|Http4xx|Http 4xx|개수|합계|Http 4xx|
|Http5xx|Http 서버 오류|개수|합계|Http 서버 오류|
|MemoryWorkingSet|메모리 작업 집합|바이트|평균|메모리 작업 집합|
|AverageMemoryWorkingSet|평균 메모리 작업 집합|바이트|평균|평균 메모리 작업 집합|
|AverageResponseTime|평균 응답 시간|초|평균|평균 응답 시간|
|FunctionExecutionUnits|함수 실행 단위|개수|평균|함수 실행 단위|
|FunctionExecutionCount|함수 실행 횟수|개수|평균|함수 실행 횟수|

## <a name="next-steps"></a>다음 단계
* [Azure Monitor의 메트릭에 대해 읽기](monitoring-overview-metrics.md)
* [메트릭에 대한 경고 만들기](insights-receive-alert-notifications.md)
* [메트릭 toostorage, 이벤트 허브 또는 분석 로그 내보내기](monitoring-overview-of-diagnostic-logs.md)
