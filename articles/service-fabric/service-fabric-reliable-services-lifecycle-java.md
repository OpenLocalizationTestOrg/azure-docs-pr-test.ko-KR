---
title: "Azure 서비스 패브릭 신뢰할 수 있는 서비스의 수명 주기 hello aaaOverview | Microsoft Docs"
description: "서비스 패브릭 신뢰할 수 있는 서비스의 hello 다른 수명 주기 이벤트에 알아보기"
services: Service-Fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: Service-Fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: pakunapa;
ms.openlocfilehash: 6d48c217d12bc5248c2da57b544aac747cecd872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-lifecycle-overview"></a>Reliable Services 수명 주기 개요
> [!div class="op_single_selector"]
> * [Windows에서 C#](service-fabric-reliable-services-lifecycle.md)
> * [Linux에서 Java](service-fabric-reliable-services-lifecycle-java.md)
>
>

신뢰할 수 있는 서비스의 hello 주기를 고려할 때는 hello 수명 주기의 hello 기본 사항 가장 중요 한 hello 됩니다. 일반적으로:

* 시작 중
  * 서비스가 생성됩니다.
  * 기회 tooconstruct 변수와 0 개 이상의 수신기를 반환 합니다.
  * 반환 된 모든 수신기 열려 hello 서비스와의 통신을 허용 합니다.
  * hello 서비스 runAsync 메서드가 호출 되 면 장기 실행 서비스 toodo hello 또는 작업을 배경 허용
* 종료 중
  * hello 취소 토큰 전달된 toorunAsync 취소 되 고 hello 수신기 닫혀 있습니다.
  * 완료 되 면 hello 서비스 개체 자체은 이벤트 소멸

이러한 이벤트의 순서 지정 정확한 hello 자세한 내용은 있습니다. 특히 이벤트 hello 순서 Stateless 또는 상태 저장 hello 신뢰할 수 있는 서비스 인지에 따라 약간 변경 될 수 있습니다. 또한 상태 저장 서비스에 대 한 주 스왑 시나리오 hello와 toodeal이 있는 합니다. 이 시퀀스 하는 동안 주 hello 역할은 전송 된 tooanother 복제 (또는 다시 시작) hello 서비스를 종료 하지 않고 있습니다. 마지막으로, 오류나 오류 조건에 대 한 toothink을 했습니다.

## <a name="stateless-service-startup"></a>상태 비저장 서비스 시작
상태 비저장 서비스의 hello 수명 주기는 매우 간단 합니다. 이벤트의 hello 순서는 다음과 같습니다.

1. hello 서비스가 생성 되
2. 그런 다음 두 가지 작업이 병렬로 수행됩니다.
    - `StatelessService.createServiceInstanceListeners()`이 호출되고 반환된 모든 수신기가 열립니다(`CommunicationListener.openAsync()`이 각 수신기에서 호출됨).
    - 서비스의 runAsync 메서드 hello (`StatelessService.runAsync()`) 호출
3. 있는 경우 hello 서비스의 onOpenAsync 메서드는 (특히, `StatelessService.onOpenAsync()` 호출 됩니다. 이 항목은 일반적이지 않은 재정의이지만 사용 가능합니다).

것이 중요 한 toonote 한지 hello 호출 toocreate 및 열기 hello 수신기 및 runAsync 간 순서가 없습니다. hello 수신기 runAsync를 시작 하기 전에 열릴 수 있습니다. 마찬가지로, runAsync 될 수 hello 통신 수신기 열려 있거나도 생성 되기 전에 호출 됩니다. 동기화가 필요한 경우 연습 toohello 구현자로 유지 됩니다. 일반적인 솔루션:

* 경우에 따라 다른 정보를 만들거나 수행할 때까지 수신기는 작동할 수 없습니다. 작업 도중에 hello 수행 hello 서비스의 생성자에서 일반적으로 상태 비저장 서비스에 대 한 `createServiceInstanceListeners()` 를 호출 하거나 자체 hello 수신기의 hello 생성의 일부로 합니다.
* 경우에 따라 hello runAsync의 코드를 원하지 않습니다 toostart hello 수신기 열려 있는 될 때까지. 이 경우에 추가 조정이 필요합니다. 일반적인 솔루션은 때 수행한 tooactual 작업을 계속 하기 전에 runAsync이 선택 되어 있는 나타내는 hello 수신기 내에서 일부 플래그입니다.

## <a name="stateless-service-shutdown"></a>상태 비저장 서비스 종료
상태 비저장 서비스를 종료할 때 hello 동일한 패턴 뒤, 반대 방향으로 바로:

1. 병렬로
    - 열려 있는 수신기 닫힙니다(각 수신기에서 `CommunicationListener.closeAsync()`을 호출함).
    - hello 취소 토큰이 전달 너무`runAsync()` 취소 (hello 취소 토큰을 검사 `isCancelled` 속성 true를 반환 hello 토큰을 호출 하 고 `throwIfCancellationRequested` 메서드가 throw는 `CancellationException`)
2. 한 번 `closeAsync()` 각 수신기에서 완료 되 고 `runAsync()` 도 완료 되 면 hello 서비스의 `StatelessService.onCloseAsync()` 있는 경우 메서드가 호출 되 (다시 이것이 일반적이 지 않은 재정의).
3. 후 `StatelessService.onCloseAsync()` 완료 되 면 서비스 개체 hello은 이벤트 소멸

## <a name="notes-on-service-lifecycle"></a>서비스 수명 주기에 대한 참고 사항
* 두 hello `runAsync()` 메서드와 hello `createServiceInstanceListeners` 호출은 선택 사항입니다. 서비스에는 이러한 항목이 있거나 없을 수도 있습니다. 예를 들어 응답 toouser 호출에는 모든 작업을 수행 하는 hello 서비스, 있는지 사용할 필요가 없다고 tooimplement `runAsync()`합니다. Hello 통신 수신기만 및 해당 관련된 코드는 필요 합니다. 마찬가지로, 만들고 통신 수신기를 반환 hello 서비스 toodo를 작동 하는 배경만 있을 수 있습니다는 선택 사항, 하며만 tooimplement`runAsync()`
* 서비스 toocomplete에 대해 유효한 `runAsync()` 성공적으로 및에서 반환 합니다. 실패 조건으로 간주 되지 않으므로 하 고는 hello 서비스 완료 하는 hello 백그라운드 작업을 나타냅니다. 신뢰할 수 있는 상태 저장 서비스에 대 한 `runAsync()` hello 서비스 주에서 강등 다음 백 tooprimary를 승격 하는 경우 다시 호출 합니다.
* 서비스에서 종료 되 면 `runAsync()` 오류 일부 예기치 않은 예외를 throw 하 여입니다와 hello 서비스 개체 종료 되 고 상태 오류를 보고 합니다.
* 이러한 방법 중에서 반환 하는 방법에 시간 제한이 없으며 상태인 동안 즉시 hello 기능 toowrite 손실 되 고 모든 실제 작업을 완료할 수 없습니다. 가능한 한 빨리 hello 취소 요청을 받으면 반환 하는 것이 좋습니다. 서비스는 적절 한 시간 내에 서비스 패브릭 강제로 수 toothese API 호출 응답 하지 않을 경우 서비스를 종료 합니다. 이러한 상황은 일반적으로 응용 프로그램을 업그레이드하거나 서비스를 삭제할 때 발생합니다. 이 시간 제한은 기본적으로 15분입니다.
* Hello에서 발생 한 실패 `onCloseAsync()` path 결과에서 `onAbort()` hello에 대 한 마지막 발생할 가능성이 있는 최상의 기회는 호출 되 고 tooclean를 서비스 하 고 요청할가 있는 모든 리소스를 해제 합니다.

> [!NOTE]
> 상태 저장 Reliable Services는 Java에서 아직 지원되지 않습니다.
>
>

## <a name="next-steps"></a>다음 단계
* [TooReliable 서비스 소개](service-fabric-reliable-services-introduction.md)
* [Reliable Services 빠른 시작](service-fabric-reliable-services-quick-start.md)
* [신뢰할 수 있는 서비스 고급 사용법](service-fabric-reliable-services-advanced-usage.md)
