---
title: "가격 및 요금 청구 aaaService 버스 | Microsoft Docs"
description: "서비스 버스 가격 구조 개요"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a>서비스 버스 가격 및 대금 청구
Service Bus는 기본, 표준 및 [프리미엄](service-bus-premium-messaging.md) 계층으로 제공됩니다. 자신이 만든 Service Bus 서비스 네임스페이스 각각에 서비스 계층을 선택할 수 있으며, 이 계층 선택은 해당 네임스페이스 안에서 모든 엔터티에 적용됩니다.

> [!NOTE]
> 현재 서비스 버스 가격에 대 한 자세한 내용은 참조 hello [Azure 서비스 버스 가격 책정 페이지](https://azure.microsoft.com/pricing/details/service-bus/), 및 hello [서비스 버스 FAQ](service-bus-faq.md#pricing)합니다.
>
>

서비스 버스 큐 및 항목/구독에 대 한 두 가지 단위가 다음 hello를 사용 합니다.

1. **메시징 운영**: 큐 또는 토픽/구독 서비스 끝점에 대한 API 호출로 정의됩니다. 이 미터는 큐 및 항목/구독에 대 한 청구 가능 사용량의 hello 기본 단위로 보내거나 받는 메시지를 대체 됩니다.
2. **조정 된 연결**: 지정 된 1 시간의 샘플링 동안 큐, 항목 또는 구독에 대 한 영구 연결의 최대 수를 hello 오픈를 정의 합니다. 이 미터 추가 연결을 열 수 있는 hello 표준 계층에만 적용 됩니다 (이전에 연결 된 큐/항목/구독 당 제한 된 too100) 명목 연결당 요금에 대 한 합니다.

hello **표준** 계층 큐 및 항목/구독, too80 %hello 최고 사용량 수준에서의 볼륨 기반 할인이 결과적으로 수행 된 작업에 대해 누진 가격 제가 도입 되었습니다. Tooperform 추가 비용 없이 매월 too12.5 백만 작업을 사용 하면는 매월 $10의 표준 계층 기본 요금은 이기도 합니다.

hello **프리미엄** 계층은 각 고객 작업 격리 상태에서 실행 되도록 hello CPU 및 메모리 계층에서 리소스 격리를 제공 합니다. 이 리소스 컨테이너를 *메시징 단위*라고 합니다. 각 프리미엄 네임스페이스에는 하나 이상의 메시징 단위가 할당됩니다. 각 서비스 버스 프리미엄 네임스페이스에 대해 1, 2 또는 4 메시징 단위를 구입할 수 있습니다. 단일 작업 또는 엔터티 여러 메시징 단위에 걸쳐 있는 및 24 시간 또는 일별로 속도 요금이 청구는가 hello 메시징 단위 수를 변경할 수 있습니다. hello 결과 서비스 버스 기반 솔루션에 대 한 예측 가능 하 고 반복 가능한 성능입니다. 이로 인해 예측 가능성 및 가용성도 높아질 뿐 아니라 속도도 더 빨라집니다.

Note hello 표준 계층 기본 요금은 Azure 구독 당 매월 한 번만 청구 됩니다. 즉, 단일 표준 계층 서비스 버스 네임 스페이스를 만든 후 수 toocreate 수는 표준 만큼 네임 스페이스는 동일한 Azure 구독에서 추가 부담 없이 원하는 만큼를 추가로 기본 요금입니다.

hello [서비스 버스 가격](https://azure.microsoft.com/pricing/details/service-bus/) 표에 hello hello Basic, Standard 및 Premium 계층 간의 기능 차이가 요약 되어 있습니다.

## <a name="messaging-operations"></a>메시징 운영
Hello 새로운 가격 책정 모델의 일환으로, 큐 및 항목/구독에 대 한 청구 변경 됩니다. 이러한 엔터티에서 작업당 메시지 toobilling 당 청구 방식으로 전환 됩니다. "작업이" 큐 또는 항목/구독 서비스 끝점에 대해 수행 된 tooany API 호출을 의미 합니다. 여기에는 관리, 송신/수신 및 세션 상태 작업이 포함됩니다.

| 작업 유형 | 설명 |
| --- | --- |
| 관리 |큐나 토픽/구독에 대한 만들기, 읽기, 업데이트, 삭제(CRUD) |
| 메시징 |큐나 토픽/구독에서 메시지 송신 및 수신 |
| 세션 상태 |큐나 토픽/구독에서 세션 상태 가져오기 또는 설정. |

비용 정보 hello에 나열 된 hello 가격을 참조 하십시오. [서비스 버스 가격](https://azure.microsoft.com/pricing/details/service-bus/) 페이지.

## <a name="brokered-connections"></a>조정된 연결
*조정된 연결*에서는 큐, 토픽 또는 구독에 대해 대용량의 "영구적인 연결"을 포함하는 고객 사용 패턴을 허용합니다. 영구적으로 연결된 발신자/수신자는 0이 아닌 수신 시간 제한(예: HTTP 긴 폴링)이 있는 AMQP나 HTTP를 사용하여 연결합니다. 즉각적인 시간 제한이 적용된 HTTP 발신자와 수신자는 조정된 연결을 생성하지 않습니다.

연결 할당량 및 기타 서비스 제한에 대 한 참조 hello [서비스 버스 할당량](service-bus-quotas.md) 문서.

hello 표준 계층 hello 네임 스페이스 당 조정 된 연결 제한을 제거 및 hello Azure 구독에서 집계 조정 된 연결 사용을 계산 합니다. 자세한 내용은 참조 hello [조정 된 연결](https://azure.microsoft.com/pricing/details/service-bus/) 테이블입니다.

> [!NOTE]
> 조정 된 연결 1, 000 hello 표준 메시징 계층 (기본 요금 hello)를 통해 포함 되며 모든 큐, 항목 및 연결 된 hello Azure 구독 내에서 구독에서 공유할 수 있습니다.
>
>

<br />

> [!NOTE]
> 청구는 hello 최대 동시 연결 수를 기반으로 하며 월 744 시간을 기준으로 시간당 계산 됨.
>
>

| 프리미엄 계층 |
| --- |
| Hello 프리미엄 계층에서 조정 된 연결 요금이 부과 되지 않습니다. |

조정 된 연결에 대 한 자세한 내용은 참조 hello [FAQ](#faq) 이 항목의 뒷부분에 나오는 섹션.

## <a name="faq"></a>FAQ

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a>조정된 연결이 무엇이며 요금은 어떻게 청구되나요?
조정 된 연결은 hello 다음 중 하나로 정의 됩니다.

1. 클라이언트 tooa 서비스 버스 큐 또는 항목/구독에서 AMQP 연결 합니다.
2. HTTP tooreceive 메시지에서 서비스 버스 항목 또는 큐는 0 보다 큰 수신 시간 제한 값을 호출 합니다.

서비스 버스 요금은 hello를 초과 하는 동시 조정 된 연결의 최대 수를 hello에 대 한 수량 (표준 계층 hello에에서 1, 000) 포함 되어 있습니다. 최대치는 시간 단위로 측정 되는, 한 달에 744 시간으로 나눈 및 hello 매월 청구 기간 동안 추가 합니다. hello 포함 된 수량 (월 당 조정 된 연결 1, 000) hello 비례하여 지정 hello 시간당 계산 된 최고의 hello 합계에 대 한 hello 청구 기간 종료 시 적용 됩니다.

예:

1. 10,000개의 장치가 각각 단일 AMQP 연결을 통해 연결되며 Service Bus 토픽으로부터 명령을 받습니다. hello 장치 원격 분석 이벤트 tooan 이벤트 허브를 보냅니다. 모든 장치가 매일 12 시간 동안 연결을 하는 경우 연결 요금은 다음 hello 적용 (더하기 tooany에 다른 서비스 버스 항목 요금): 연결 10, 000 * 12 시간 * 31 일 / 744 = 5, 000 조정 된 연결입니다. Hello 월별 허용 되는 1, 000 조정 된 연결 후 $0.03 총 요금은 120의 조정 된 연결당 hello 속도로 4, 000 조정 된 연결에 대 한 청구 됩니다.
2. 10,000개의 장치가 시간 제한이 0이 아니며 HTTP를 통해 서비스 버스 큐에서 메시지를 수신합니다. 모든 장치가 매일 12 시간 동안 연결을 하는 경우에 연결 요금은 다음 hello 표시 됩니다 (더하기 tooany에 다른 서비스 버스 요금은): HTTP 수신 연결 10, 000 * 매일 12 시간 * 31 일/744 시간 = 5, 000 조정 된 연결입니다.

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a>Tooqueues 및 항목/구독 조정 된 연결 요금이 적용 수행 되나요?
예. Hello 시스템을 보내거나 장치 수에 관계 없이 HTTP를 사용 하 여 이벤트를 전송에 대 한 연결 요금이 부과 되지 있습니다. 0이 아닌 시간 제한을 사용한 HTTP를 통한 이벤트 수신은 경우에 따라 "긴 폴링"이라고 하며 조정된 연결 요금이 발생합니다. AMQP 연결 여부에 관계 없이 hello 연결 toosend 사용된 되는 수신 조정 된 연결 요금이 생성 합니다. 기본 네임스페이스에서는 조정된 연결 100개가 무료로 허용됩니다. Hello hello Azure 구독에 허용 되는 조정 된 연결의 최대 수 이기도 합니다. hello Azure 구독의 모든 표준 네임 스페이스에서 조정 된 연결을 처음 1, 000 포함 됩니다 (hello 기본 요금) 이외의 추가 비용 없이. 이러한 허용 한이도 충분 한 toocover 때문에 많은 서비스 간 메시징 시나리오에서 일반적으로 조정 된 연결 요금이 경우가 그렇습니다 toouse AMQP 또는 HTTP 긴 폴링 다 수의 클라이언트; 사용 하려는 경우 예를 들어 tooachieve 여러 장치 또는 응용 프로그램 인스턴스를 보다 효율적인 이벤트 스트리밍 또는 사용이 양방향 통신 합니다.

## <a name="next-steps"></a>다음 단계
* 서비스 버스 가격에 대 한 자세한 내용은 참조 hello [서비스 버스 가격 책정 페이지](https://azure.microsoft.com/pricing/details/service-bus/)합니다.
* Hello 참조 [서비스 버스 FAQ](service-bus-faq.md#pricing) 서비스 버스 가격 및 요금 청구에 대 한 일반적인 몇 가지 Faq에 대 한 합니다.

[Azure portal]: https://portal.azure.com
