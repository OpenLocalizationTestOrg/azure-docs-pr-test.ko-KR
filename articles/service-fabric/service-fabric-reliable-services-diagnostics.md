---
title: "신뢰할 수 있는 서비스 진단 aaaStateful | Microsoft Docs"
description: "상태 저장 Reliable Services의 진단 기능"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ae0e8f99-69ab-4d45-896d-1fa80ed45659
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 6200800b858957c06039d9af062633b12a446318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostic-functionality-for-stateful-reliable-services"></a>상태 저장 Reliable Services의 진단 기능
상태 저장 Reliable Services StatefulServiceBase 클래스 hello 내보냅니다 [EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) toodebug 사용된 될 수 있는 이벤트 서비스 hello hello 런타임 운영은 및 문제 해결에 도움이 되는 방법에 대 한 정보를 제공 합니다.

## <a name="eventsource-events"></a>EventSource 이벤트
hello EventSource hello 상태 저장 Reliable Services StatefulServiceBase 클래스 이름은 "Microsoft ServiceFabric 서비스"입니다. 이 이벤트 소스에서 이벤트에 표시는 [진단 이벤트](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md#view-service-fabric-system-events-in-visual-studio) hello 서비스가 되는 경우 창 [Visual Studio에서 디버깅](service-fabric-debugging-your-application.md)합니다.

EventSource 이벤트를 수집하거나 보는 데 도움이 되는 도구 및 기술의 예로 [PerfView](http://www.microsoft.com/download/details.aspx?id=28567), [Microsoft Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) 및 [Microsoft TraceEvent 라이브러리](http://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent)가 있습니다.

## <a name="events"></a>이벤트
| 이벤트 이름 | 이벤트 ID | Level | 이벤트 설명 |
| --- | --- | --- | --- |
| StatefulRunAsyncInvocation |1 |정보 제공 |서비스 RunAsync 작업이 시작되면 내보내집니다. |
| StatefulRunAsyncCancellation |2 |정보 제공 |서비스 RunAsync 작업이 취소되면 내보내집니다. |
| StatefulRunAsyncCompletion |3 |정보 제공 |서비스 RunAsync 작업이 완료되면 내보내집니다. |
| StatefulRunAsyncSlowCancellation |4 |Warning |서비스 RunAsync 작업이 너무 길어서 toocomplete 취소를 사용 하는 경우에 발생 |
| StatefulRunAsyncFailure |5 |오류 |서비스 RunAsync 작업이 예외를 throw하면 내보내집니다. |

## <a name="interpret-events"></a>이벤트 해석
StatefulRunAsyncInvocation, StatefulRunAsyncCompletion, 및 StatefulRunAsyncCancellation 이벤트는 유용한 toohello 서비스 기록기 toounderstand hello 수명 주기 서비스를 시작, 취소 또는 완료에 대 한 hello 타이밍 뿐만 아니라 서비스- . 서비스 문제 또는 hello 서비스 수명 주기 이해를 디버깅할 때 유용할 수 있습니다.

서비스 작성자 hello 서비스 문제가 나타내기 때문에 주의 기울여야 tooStatefulRunAsyncSlowCancellation 및 StatefulRunAsyncFailure 이벤트 기울여야 합니다.

Hello 서비스 RunAsync() 작업에서 예외가 throw 될 때마다 StatefulRunAsyncFailure 내보내집니다. 일반적으로 발생 하는 예외 hello 서비스의 버그 또는 오류를 나타냅니다. 또한 hello 예외 hello 서비스 toofail로 인해 다른 노드로 이동된 tooa 되기 때문입니다. 이 작업 수 있으며 hello 서비스를 이동 하는 동안 들어오는 요청을 지연 될 수 있습니다. 서비스 작성자 결정 hello 예외를 hello 발생 하 고, 가능한 경우 완화 합니다.

4 초 보다 오래 걸리는 hello RunAsync 작업에 대 한 취소 요청 될 때마다 StatefulRunAsyncSlowCancellation 내보내집니다. 너무 긴 toocomplete 취소를 사용 하는 서비스를 신속 하 게 다른 노드에서 다시 시작 하는 hello 서비스 toobe hello 기능이 영향을 줍니다. 이 영향을 줄 수 hello 서비스의 전체 가용성 hello 합니다.

## <a name="next-steps"></a>다음 단계
* [PerfView의 EventSource 공급자](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/)
