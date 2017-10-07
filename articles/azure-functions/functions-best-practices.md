---
title: "Azure 기능에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Azure Functions에 대한 모범 사례 및 패턴에 알아봅니다."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 패턴, 모범 사례, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>함수를 Azure의 hello 성능 및 안정성 최적화

이 문서에서는 지침 tooimprove hello 성능 및 안정성 기능 앱을 제공 합니다. 


## <a name="avoid-long-running-functions"></a>장기 실행 함수 방지

큰 장기 실행 함수는 예기치 않은 시간 초과 문제를 발생시킬 수 있습니다. 함수는 toomany Node.js 종속성 인해 커질 수 있습니다. 또한 종속성을 가져올 때 로드 시간이 증가하여 예기치 않은 시간 초과가 발생할 수 있습니다. 종속성은 명시적 및 암시적으로 로드됩니다. 코드를 통해 로드되는 단일 모듈은 자체 추가 모듈을 로드할 수 있습니다.  

큰 함수를 더 작은 함수 집합으로 리팩터링할 때마다 함께 작동하고 빠른 응답을 반환합니다. 예를 들어 webhook 또는 HTTP 트리거 함수 해야 된 승인 응답 시간 제한 내; 것에 대 한 webhook toorequire 즉시 응답 합니다. 큐 트리거 함수에 의해 처리 큐 toobe에 hello HTTP 트리거 페이로드를 전달할 수 있습니다. 이 방법은 toodefer hello 실제 작업을 허용 하 고 즉각적인 응답을 반환 합니다.


## <a name="cross-function-communication"></a>함수 통신 교차

여러 기능을 통합할 때 일반적으로 모범 사례 toouse 저장소 큐에 대 한 함수 통신 합니다.  hello 주요 이유는 저장소 큐는 비용이 저렴 하 고 훨씬 쉽게 tooprovision 합니다. 

저장소 큐에 있는 개별 메시지 크기 too64 제한 됩니다 (kb)입니다. 함수 사이 toopass 보다 큰 메시지가 필요한 경우 Azure 서비스 버스 큐 too256 (kb) 사용 하는 toosupport 메시지 크기를 수 있습니다.

Service Bus 토픽은 메시지를 처리하기 전에 필터링해야 하는 경우에 유용합니다.

이벤트 허브는 유용한 toosupport 고용량 통신 합니다.


## <a name="write-functions-toobe-stateless"></a>상태 비저장 함수 toobe 작성 

함수는 가능하면 상태 비저장이며 idempotent여야 합니다. 필요한 모든 상태 정보를 사용자 데이터에 연결합니다. 예를 들어 처리할 주문에 연결된 `state` 멤버가 있을 수 있습니다. 함수는 hello 함수 자체는 상태 비저장 상태로 유지 하면서 해당 상태에 따라 주문을 처리할 수 있습니다. 

Idempotent 함수는 특히 타이머 트리거 사용이 권장됩니다. 예를 들어 절대적으로 하루에 한 번 실행 해야 하는 문제가 있다면 작성 실행할 수 있도록 hello 하루 동안 언제 든 지 hello로 동일한 결과입니다. 특정 날에 대 한 작업이 없는 경우 hello 함수 나갈 수 있습니다. 또한 이전 실행 toocomplete 실패 한 경우 다음 실행 하는 hello 중단 된 위치를 선택 해야 합니다.


## <a name="write-defensive-functions"></a>방어적 함수 작성

함수에는 언제든지 예외가 발생할 수 있다고 가정합니다. Hello 다음 실행 하는 동안 hello 기능 toocontinue 이전 장애 지점에서 사용 하 여 함수를 디자인 합니다. Hello 동작을 수행 해야 하는 시나리오를 고려 합니다.

1. Db의 10,000개 행에 대해 쿼리합니다.
2. 각 hello 줄 아래로 더 행 tooprocess 이러한에 대 한 큐 메시지를 만듭니다.
 
시스템의 복잡성에 따라 잘못 작동되는 관련된 다운스트림 서비스, 네트워킹 작동 중단 또는 할당량 제한 초과 등이 있을 수 있습니다. 이러한 항목은 모두 언제든지 함수에 영향을 줄 수 있습니다. 것에 대비 하 여 함수 toobe toodesign 필요 합니다.

이러한 항목 중 5,000개를 처리를 위해 큐에 삽입한 후 오류가 발생한다면 코드는 어떻게 반응할까요? 사용자가 완료한 집합에서 항목을 추적합니다. 다른 방법으로 다음 번에 해당 항목을 삽입할 수도 있습니다. 이는 작업 흐름에 심각한 영향을 미칠 수 있습니다. 

큐 항목을 이미 처리 된 함수 toobe no-op를 허용 합니다.

Hello 함수 Azure 플랫폼에서 사용 하는 구성 요소에 대해 이미 제공 방어 수단을 활용 합니다. 예를 들어 참조 **포이즌 큐 메시지를 처리할** hello 설명서에서 [Azure 저장소 큐 트리거합니다](functions-bindings-storage-queue.md#trigger)합니다.
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>하지 혼합 테스트 및 프로덕션 코드 hello에 동일 함수 응용 프로그램

함수 앱 공유 리소스 내에서 작용합니다. 예를 들어 메모리는 공유됩니다. 테스트 관련 기능 및 리소스 tooit 함수 응용 프로그램을 프로덕션 환경에서 사용 하는 경우 추가 하지 마십시오. 프로덕션 코드를 실행하는 동안 예기치 않은 오버 헤드가 발생할 수 있습니다.

프로덕션 함수 앱에서 로드하는 것에 주의하세요. 각 함수 hello 앱에 메모리는 평균입니다.

여러.Net 함수에서 참조되는 공유 어셈블리가 있는 경우 일반적인 공유 폴더에 저장합니다. 다음 예에서는 문 비슷한 toohello 사용 하 여 hello 어셈블리를 참조 합니다. 

    #r "..\Shared\MyAssembly.dll". 

그렇지 않으면 쉽습니다 tooaccidentally 사이 다르게 동작 하는 같은 이진 함수 hello의 여러 테스트 버전을 배포 합니다.

프로덕션 코드에 너무 많은 로깅을 사용하지 마세요. 부정적인 영향을 미칩니다.



## <a name="use-async-code-but-avoid-blocking-calls"></a>비동기 코드는 사용, 호출 차단 방지

비동기 프로그래밍은 권장되는 최상의 방법입니다. 그러나 항상 참조 하지 않을 hello `Result` 속성 또는 호출 `Wait` 에서 메서드는 `Task` 인스턴스. 이 방법은 toothread 소모가 될 수 있습니다.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>다음 단계
자세한 내용은 다음 리소스는 hello 참조:

Azure Functions에서는 Azure App Service를 사용하므로 App Service 지침도 알아야 합니다.
* [패턴 및 사례 HTTP 성능 최적화](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

