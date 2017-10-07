---
title: "aaaAvailability Azure 이벤트 허브의 | Microsoft Docs"
description: "어떻게 tooprovide hello 최대한의 가용성 및 사용 하 여 Azure 이벤트 허브와의 일관성을 분할 합니다."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a>Event Hubs의 가용성 및 일관성

## <a name="overview"></a>개요
Azure 이벤트 허브를 사용 하 여 한 [모델 분할](event-hubs-features.md#partitions) tooimprove 가용성 및 단일 이벤트 허브 내 평행 화 합니다. 예를 들어 이벤트 허브는 4 개의 파티션이 경우 부하 분산 작업에서에서 tooanother 하나의 서버에서에서 이동의 해당 파티션 중 하나 있습니다 여전히 보내고 받을 수에서 다른 3 개의 파티션과 합니다. 더욱이, 파티션을 더 필요 하면 toohave 집계 된 처리량을 향상 더 많은 동시 판독기 데이터를 처리 합니다. 분할 및 순서는 분산된 시스템에서의 hello 의미를 이해 하는 것은 솔루션 디자인의 중요 한 측면입니다.

toohelp 순서 지정 및 가용성 사이의 절충 값 hello 설명, hello 참조 [CAP 정리](https://en.wikipedia.org/wiki/CAP_theorem)가나다의 정리 라고도 합니다. 이 정리, 일관성, 가용성 및 파티션 허용 오차 사이 hello 선택을 설명합니다.

Brewer의 정리는 일관성 및 가용성을 다음과 같이 정의합니다.
* 허용 오차를 파티션: hello 파티션 오류가 발생 하는 경우에 데이터를 처리 하는 데이터 처리 시스템 toocontinue의 능력입니다.
* 가용성: 실패하지 않은 노드가 오류 또는 시간 제한 없이 적절한 시간 내에 적절한 응답을 반환합니다.
* 일관성: 읽기 tooreturn hello 지정된 된 클라이언트에 대 한 가장 최근의 쓰기가 보장 됩니다.

## <a name="partition-tolerance"></a>파티션 허용 오차
Event Hubs는 분할된 데이터 모델을 기반으로 빌드됩니다. 설치 하는 동안 이벤트 허브에 hello 파티션 수를 구성할 수 있지만 나중에이 값을 변경할 수 없습니다. 파티션은 이벤트 허브를 사용 해야 하므로 해야 toomake 가용성과 일관성을 유지 하는 방법에 대 한 의사 결정 응용 프로그램에 대 한 합니다.

## <a name="availability"></a>Availability
hello 가장 간단한 방법은 tooget 시작 이벤트 허브는 toouse hello 기본 동작입니다. 새 만들면 `EventHubClient` 개체 및 hello를 사용 하 여 `Send` 메서드를 이벤트에서 이벤트 허브 파티션 간에 자동으로 배포 됩니다. 이 동작은 hello 최대한의 시간이 걸릴 수 있습니다.

이 모델은 hello 최대 시간을 필요로 하는 사용 사례에 대 한 기본 설정입니다.

## <a name="consistency"></a>일관성
일부 시나리오에서는 이벤트의 순서 지정 hello 중요할 수 있습니다. 예를 들어 프로그램 백 엔드 시스템 tooprocess delete 명령 전에 update 명령을 좋습니다. 이 경우에는 이벤트에 hello 파티션 키를 설정 하거나 사용 하 여 한 `PartitionSender` 개체 tooonly 보낼 이벤트 tooa 특정 파티션 합니다. 이렇게 하면 이러한 이벤트는 hello 파티션에서 읽으면 순서로 읽어 됩니다.

이 구성을 사용 하 여 보내는 hello 특정 파티션의 toowhich 사용할 수 없는 경우 오류 응답이 수신 됩니다 염두에서에 둬야 합니다. 이벤트 허브 서비스 hello 선호도 tooa 단일 파티션에 없는 비교의 점으로 사용자 이벤트 toohello 사용 가능한 다음 파티션을 보냅니다.

순서 지정도 작동 시간을 극대화 하는 동안 한 가능한 해결 방법 tooensure 이벤트 처리 응용 프로그램의 일부로 tooaggregate 이벤트 것입니다. 이 가장 쉬운 방법은 tooaccomplish hello toostamp 사용자 정의 시퀀스 번호 속성을 갖는 사용자 이벤트입니다. hello 코드 다음 예를 보여 줍니다.

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

이 예제에서는 이벤트 허브에서 사용자 이벤트 tooone hello 사용 가능한 파티션 보내고 응용 프로그램에서 시퀀스 번호를 해당 하는 hello를 설정 합니다. 이 솔루션 상태 toobe 처리 응용 프로그램에 의해 유지 하는데 프로그램 보낸 사람을 사용할 수 있는 가능성이 toobe 되는 끝점을 제공 합니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [Event Hubs 서비스 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
