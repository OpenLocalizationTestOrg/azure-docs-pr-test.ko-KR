---
title: "이벤트 허브 FAQ aaaAzure | Microsoft Docs"
description: "Azure Event Hubs FAQ(질문과 대답)"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: bfa10984-eb22-4671-861a-f377a90d9372
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm;shvija
ms.openlocfilehash: cc0844edcc38ad167cde9497d58d44155fc90b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-frequently-asked-questions"></a>Event Hubs 질문과 대답

## <a name="general"></a>일반

### <a name="what-is-hello-difference-between-event-hubs-basic-and-standard-tiers"></a>이벤트 허브 기본 및 표준 계층 간의 hello 차이점은 무엇입니까?

hello Azure 이벤트 허브 표준 계층은 hello 기본 계층에서 사용 가능한 것 보다 더 뛰어난 기능을 제공 합니다. 같은 기능 hello 표준에 포함 되어 있습니다.
* 더 길어진 이벤트 보존 기간
* 추가 조정 된 연결을 포함 하는 hello 수 이후에 남는 경우 요금
* 단일 소비자 그룹 이상
* [캡처](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview)

가격 책정 계층을 이벤트 허브 전용 포함 하는 방법에 대 한 자세한 내용은 참조 hello [이벤트 허브 가격 정보](https://azure.microsoft.com/pricing/details/event-hubs/)합니다.

### <a name="what-are-event-hubs-throughput-units"></a>이벤트 허브 처리량 단위는 무엇입니까?

이벤트 허브 처리량 단위, hello Azure 포털을 통해 또는 이벤트 허브 리소스 관리자 템플릿을 명시적으로 선택 합니다. 처리량 단위 tooall 이벤트 허브는 이벤트 허브 네임 스페이스에 적용 하 고 각 처리량 단위는 hello 네임 스페이스 toohello 다음 기능을 제공 합니다.

* 수신 이벤트 (이벤트 허브로 전송) 하지만 없는 1000 개 이상의 수신 이벤트, 관리 작업이 나 컨트롤의 초 당 too1 MB를 초당 API를 호출 합니다.
* too2 m B / 초 수신 이벤트 (이벤트 허브에서 사용 하는 이벤트).
* 이벤트 저장소 (hello 기본 24 시간 보존 기간에 대 한 충분 한) too84 g B를.

이벤트 허브 처리량 단위는 hello 최대 hello 시간을 지정 하는 동안 선택 된 단위 수에 따라 매시간, 청구 됩니다.

### <a name="how-are-event-hubs-throughput-unit-limits-enforced"></a>이벤트 허브 처리량 단위 제한을 적용하는 방법
Hello 전체 송신 처리량 또는 네임 스페이스에 모든 이벤트 허브 hello 전체 송신 이벤트 비율이 hello 집계 된 처리량 단위 허용 한도 초과 하면 발신자는 조절 됩니다와 해당 hello 송신 할당량을 초과 했음을 나타내는 오류를 수신 합니다.

Hello 전체 수신 처리량 또는 hello 전체 수신 이벤트 비율이 네임 스페이스에 모든 이벤트 허브 hello 집계 된 처리량 단위 허용 한도 초과 하면 수신기는 제한 된 및 해당 hello 송신 할당량을 초과 했음을 나타내는 오류를 수신 합니다. 송신 할당량과 수신 없도록 없는 보낸 사람으로 지정 하면 이벤트 소비 tooslow 다운와 수신기를 방지할 수 이벤트 허브로 전송 되지 개별적으로 적용 됩니다.

### <a name="is-there-a-limit-on-hello-number-of-throughput-units-that-can-be-selected"></a>이 hello 선택할 수 있는 처리량 단위 수에 제한이 있습니까?
네임스페이스 당 20개의 처리량 단위로 기본 할당량이 적용됩니다. 지원 티켓을 제출하여 더 많은 처리량 단위 할당량을 요청할 수 있습니다. 처리량 단위 제한인 20 hello 초과 번들을 20-100 처리량 단위에서 사용할 수 있습니다. 참고 20 개 이상의 처리량 단위를 사용 하 여 지원 티켓을 제출 하지 않으면 처리량 단위 hello 기능 toochange hello 수 제거 합니다.

### <a name="can-i-use-a-single-amqp-connection-toosend-and-receive-from-multiple-event-hubs"></a>단일 AMQP 연결 toosend를 사용 하 고 여러 이벤트 허브에서 받을 수 있습니까?
예, hello에서 모든 hello 이벤트 허브는으로 동일한 네임 스페이스입니다.

### <a name="what-is-hello-maximum-retention-period-for-events"></a>이벤트에 대 한 hello 최대 보존 기간 이란 무엇 인가요?
이벤트 허브 표준 계층은 현재 최대 7일의 보존 기간을 지원합니다. 이벤트 허브는 영구 데이터 저장소로 사용되지 않습니다. 보존 기간은 24 시간 동안 오버 로드는 시나리오 편리한 tooreplay에 이벤트를 스트리밍하는 것 보다 큰 hello 동일한 시스템 예를 들어 tootrain 또는 기존 데이터에 대해 새로운 기계 학습 모델을 확인 합니다. 7 일 이상 보존 메시지 필요를 사용 하도록 설정 [이벤트 허브 캡처](https://docs.microsoft.com/azure/event-hubs/event-hubs-capture-overview) 허브 이벤트에 이벤트 허브 toohello 저장소 계정 또는 선택 해 Azure 데이터 레이크 서비스 계정에서 hello 데이터를 가져오고 있습니다. 캡처를 사용하도록 설정하면 구매한 처리량 단위에 따라 요금이 부과됩니다.

### <a name="where-is-azure-event-hubs-available"></a>어디에서 Azure Event Hubs를 사용할 수 있나요?
Azure 이벤트 허브는 지원되는 모든 Azure 지역에서 사용할 수 있습니다. 목록에 대 한 방문 hello [Azure 지역](https://azure.microsoft.com/regions/) 페이지.  

## <a name="best-practices"></a>모범 사례

### <a name="how-many-partitions-do-i-need"></a>얼마나 많은 파티션이 필요한가요?
하십시오 hello 이벤트 허브의 파티션 수 있음을 명심 설치 후 수정할 수 없습니다. 이 점을 염두에서은 시작 하기 전에 해야 하는 파티션의 수에 대 한 중요 한 toothink 있습니다. 

이벤트 허브 소비자 그룹 마다 단일 파티션 독자 디자인 된 tooallow입니다. 대부분의 사용 경우 4 개의 파티션 hello 기본 설정인은 충분 합니다. 원하는 tooscale 처리 이벤트를 추가 하는 추가 파티션을 tooconsider를 수도 있습니다. 특정 처리량 제한이 없는 파티션에 있지만 hello 네임 스페이스에서 동시에 집계 처리량 hello 처리량 단위 수에 의해 제한 됩니다. 네임 스페이스에서 hello 처리량 단위 수를 늘리면 자신의 최대 처리량에 파티션을 추가로 tooallow 동시 판독기 tooachieve 할 수 있습니다.

그러나 응용 프로그램에 특정 한 파티션의 선호도 tooa 모델을 설정한 경우 hello 파티션 수를 늘리면 아니어야의 모든 혜택 tooyou 합니다. 자세한 내용은 [가용성 및 일관성](event-hubs-availability-and-consistency.md)을 참조하세요.

## <a name="pricing"></a>가격

### <a name="where-can-i-find-more-pricing-information"></a>추가 가격 책정 정보는 어디에서 찾을 수 있나요?
이벤트 허브 가격에 대 한 자세한 내용은 참조 hello [이벤트 허브 가격 정보](https://azure.microsoft.com/pricing/details/event-hubs/)합니다.

### <a name="is-there-a-charge-for-retaining-event-hubs-events-for-more-than-24-hours"></a>24시간 이상 이벤트 허브 이벤트를 유지 하려면 비용이 청구됩니까?
hello 이벤트 허브 표준 계층에서는 최대 7 일 동안 24 시간이 넘는 기간 메시지 보존 됩니다. Hello 허용 한도 초과 하는 hello 크기에 따라 청구 됩니다 저장 된 이벤트의 총 hello hello 크기가 선택한 처리량 단위 수 (처리량 단위당 84GB) hello 수에 대 한 hello 저장소 허용 한도 초과 하는 경우 hello Azure Blob 저장소 가격을 게시 합니다. 각 처리량 단위에서 hello 저장소 허용 한도 hello 처리량 단위는 toohello 최대 송신 허용 한도를 사용 하는 경우에 24 시간 (hello 기본값)의 보존 기간에 대 한 모든 저장소 비용을 설명 합니다.

### <a name="how-is-hello-event-hubs-storage-size-calculated-and-charged"></a>어떻게 hello 이벤트 허브 저장소 크기 계산 되 고 요금이 부과?
디스크 저장소 구조 또는 이벤트 헤더의 내부 오버 헤드를 포함 하 여 모든 이벤트 허브에서 저장 된 모든 이벤트의 총 크기 hello hello 하루 종일 측정 됩니다. Hello 종료 hello 시간, hello 최대 저장소 크기가 계산 됩니다. hello 일일 저장소 허용 한도 hello 최소 hello 일 (각 처리량 단위는 84GB의 여유를 제공 하는 데 사용) 중에 선택 된 처리량 단위 수에 따라 계산 됩니다. Hello 전체 크기를 초과 하는 경우 hello 저장소 허용 한도 매일 계산, Azure Blob 저장소 가격을 사용 하 여 hello 초과 저장소의 요금이 청구 됩니다 (hello에 **로컬 중복 저장소** 속도).

### <a name="how-are-event-hubs-ingress-events-calculated"></a>이벤트 허브 수신 이벤트 계산하는 방법
각 이벤트 전송 tooan 이벤트 허브는 청구 가능 메시지로 계산 됩니다. *송신 이벤트* 보다 크거나 작은 데이터 단위로 정의 too64 (kb)입니다. 보다 작거나 같은 모든 이벤트의 크기 (kb) too64 toobe 하나의 청구 가능한 이벤트를 간주 됩니다. Hello 이벤트가 64KB 보다 큰 경우 청구 가능한 이벤트 수가 hello 64KB의 배수로 toohello 이벤트 크기에 따라 계산 됩니다. 예를 들어 toohello 이벤트 허브 전송 된 8KB 이벤트는 하나의 이벤트로 청구 되지만 toohello 이벤트 허브 전송 된 96KB 메시지는 두 이벤트로 청구 됩니다.

이벤트 허브에서 소비 되는 이벤트 관리 작업과 마찬가지로 및 검사점 같은 제어 호출, 청구 가능한 이벤트로 계산 되지 않습니다 되지만 toohello 처리량 단위 허용 한도를 계산 합니다.

### <a name="do-brokered-connection-charges-apply-tooevent-hubs"></a>조정 된 연결 요금이 tooEvent 허브 적용지 않습니다?
연결 요금은 AMQP 프로토콜이 hello를 사용할 때만 적용 됩니다. Hello 시스템을 보내거나 장치 수에 관계 없이 HTTP를 사용 하 여 이벤트를 전송에 대 한 연결 요금이 부과 되지 있습니다. AMQP toouse 하려는 경우 (예를 들어 tooachieve IoT 명령 및 컨트롤 시나리오에 더 효율적인 이벤트 스트리밍 또는 tooenable 양방향 통신), hello 참조 [이벤트 허브 가격 책정 정보](https://azure.microsoft.com/pricing/details/event-hubs/) 방법에 대 한 세부 정보에 대 한 페이지 각 서비스 계층에 많은 연결이 포함 됩니다.

### <a name="how-is-event-hubs-capture-billed"></a>Event Hubs 캡처는 어떻게 청구되나요?
캡처는 hello 네임 스페이스의 모든 이벤트 허브에 hello 캡처 옵션을 사용 하는 경우에 활성화 됩니다. Event Hubs 캡처는 구매한 처리량 단위를 기준으로 시간당 청구됩니다. Hello 처리량 단위 수를 증가 하거나 감소 청구 이벤트 허브 캡처는 전체 시간 단위 증분에서 이러한 변경 내용을 반영 합니다. Event Hubs 캡처 청구에 대한 자세한 내용은 [Event Hubs 가격 정보](https://azure.microsoft.com/pricing/details/event-hubs/)를 참조하세요.

### <a name="will-i-be-billed-for-hello-storage-account-i-select-for-event-hubs-capture"></a>요금이 청구 이벤트 허브 캡처에 대 한 선택 hello 저장소 계정에 대 한?
이벤트 허브에서 설정된 경우 캡처는 사용자가 제공한 저장소 계정을 사용합니다. 저장소 계정, 이것이이 구성에 대 한 변경 청구 tooyour Azure 구독 됩니다.

## <a name="quotas"></a>할당량

### <a name="are-there-any-quotas-associated-with-event-hubs"></a>Event Hubs와 관련된 할당량이 있나요?
Event Hubs 할당량의 목록은 [할당량](event-hubs-quotas.md)을 참조하세요.

## <a name="troubleshooting"></a>문제 해결

### <a name="what-are-some-of-hello-exceptions-generated-by-event-hubs-and-their-suggested-actions"></a>이벤트 허브 및 해당 제안 된 작업에서 생성 된 hello 예외 중 일부 무엇입니까?
가능한 Event Hubs 예외의 목록은 [예외 개요](event-hubs-messaging-exceptions.md)를 참조하세요.

### <a name="diagnostic-logs"></a>진단 로그
이벤트 허브는 두 가지 유형의 [진단 로그](event-hubs-diagnostic-logs.md) -Azure 포털을 hello 캡처 오류 로그 및 작업 로그는 json에 표시 되 고 통해 켤 수 있습니다.

### <a name="support-and-sla"></a>지원 및 SLA
이벤트 허브에 대 한 기술 지원은 hello를 통해 제공 됩니다 [커뮤니티 포럼](https://social.msdn.microsoft.com/forums/azure/home)합니다. 청구 및 구독 관리 지원은 무료로 제공됩니다.

toolearn SLA는에 대 한 자세한 참조 hello [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/) 페이지.

## <a name="next-steps"></a>다음 단계
Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.

* [이벤트 허브 개요](event-hubs-what-is-event-hubs.md)
* [이벤트 허브 만들기](event-hubs-create.md)
