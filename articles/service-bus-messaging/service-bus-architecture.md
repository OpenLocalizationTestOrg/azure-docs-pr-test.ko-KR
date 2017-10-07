---
title: "aaaAzure 서비스 버스 메시지를 처리 하는 아키텍처 개요 | Microsoft Docs"
description: "Azure 서비스 버스의 hello 메시지 처리 아키텍처를 설명합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: baf94c2d-0e58-4d5d-a588-767f996ccf7f
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: f7606e40cdf6db3797a0db2de9365453ff2a158e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-architecture"></a>서비스 버스 아키텍처
이 문서에서는 Azure 서비스 버스의 hello 메시지 처리 아키텍처를 설명 합니다.

## <a name="service-bus-scale-units"></a>서비스 버스 배율 단위
서비스 버스는 *배율 단위*로 구성됩니다. 배율 단위 배포 단위 이며 모든 구성 요소 실행된 hello 필요한 서비스를 포함 합니다. 각 영역은 하나 이상의 서비스 버스 배율 단위를 배포합니다.

서비스 버스 네임 스페이스는 매핑된 tooa 배율 단위입니다. hello 배율 단위에는 서비스 버스 엔터티 (큐, 항목, 구독)의 모든 형식을 처리합니다. 서비스 버스 배율 단위 hello 다음과 같은 구성 요소가 구성 되어 있습니다.

* **게이트웨이 노드 집합.** 게이트웨이 노드는 들어오는 요청을 인증합니다. 각 게이트웨이 노드에는 공용 IP 주소가 있습니다.
* **메시징 브로커 노드 집합.** 메시징 브로커 노드는 메시징 엔터티에 관한 요청을 처리합니다.
* **게이트웨이 저장소 1개.** hello 게이트웨이 저장소가 배율 단위에 정의 된 모든 엔터티에 대 한 hello 데이터를 저장 합니다. hello 게이트웨이 저장소는 SQL Azure 데이터베이스를 기반으로 구현 됩니다.
* **여러 메시징 저장소.** 메시징 저장소의 모든 큐, 토픽 및 구독이 배율 단위에 정의 된 hello 메시지를 보관 합니다. 또한 모든 구독 데이터를 포함합니다. 하지 않는 한 [메시징 엔터티 분할](service-bus-partitioning.md) 가 사용 하도록 설정 된 큐 또는 항목은 매핑된 tooone 메시징 저장소입니다. 구독은 hello에 저장 된 항목의 부모와 같은 메시징 저장소입니다. 서비스 버스를 제외 하 고 [프리미엄 메시징](service-bus-premium-messaging.md), hello 메시징 저장소 SQL Azure 데이터베이스를 기반으로 구현 됩니다.

## <a name="containers"></a>컨테이너
각 메시징 엔터티에는 특정 컨테이너가 할당됩니다. 컨테이너는이 컨테이너에 대해 정확히 하나의 메시징 저장소 toostore 모든 관련 데이터를 사용 하는 논리적 구문입니다. 각 컨테이너에는 메시징 브로커 노드 tooa를 할당 됩니다. 일반적으로 메시징 브로커 노드 수보다 더 많은 컨테이너가 있습니다. 따라서 각 메시징 브로커 노드는 여러 컨테이너를 로드합니다. hello 배포의 컨테이너 tooa 메시징 브로커 노드는 모든 메시징 브로커 노드 동일 하 게 로드 되도록 구성 되어 있습니다. Hello 부하 패턴 변경 (예를 들어 중 하나 hello 컨테이너 가져옵니다 사용률이 매우 높은), 또는 메시징 브로커 노드 일시적으로 사용할 수 없게 되 면 hello 컨테이너 메시징 브로커 노드 hello 보다 짧은 됩니다.

## <a name="processing-of-incoming-messaging-requests"></a>들어오는 메시징 요청 처리
클라이언트가 요청 tooService 버스 보내면 hello Azure 부하 분산 장치 hello 게이트웨이 노드 tooany를 라우팅합니다. hello 게이트웨이 노드 hello 요청에 권한을 부여 합니다. 메시징 엔터티 (큐, 항목, 구독)와 관련 hello 요청 하는 경우 hello 게이트웨이 노드 hello 게이트웨이 저장소의 hello 엔터티를 조회 하 고 메시징 저장소 hello는 엔터티를 찾을 결정 합니다. 그런 다음 메시징 브로커 노드는 현재이 컨테이너를 서비스와 메시징 브로커 노드 hello 요청 toothat 보냅니다를 찾습니다. 메시징 브로커 노드 hello hello 요청을 처리 하 고 hello 컨테이너 저장소의 hello 엔터티 상태를 업데이트 합니다. hello 메시징 브로커 노드 다음에 적절 한 응답 백 toohello 클라이언트는 발급 된 hello 원래 요청을 전송 하는 hello 응답 백 toohello 게이트웨이 노드를 보냅니다.

![들어오는 메시징 요청 처리](./media/service-bus-architecture/ic690644.png)

## <a name="next-steps"></a>다음 단계
서비스 버스 아키텍처의 개요를 읽은 했으므로 hello에 대 한 자세한 내용은 링크를 따라 방문.

* [서비스 버스 메시징 개요](service-bus-messaging-overview.md)
* [서비스 버스 기본 사항](service-bus-fundamentals-hybrid-solutions.md)
* [Service Bus 큐를 사용하는 큐 메시징 솔루션](service-bus-dotnet-multi-tier-app-using-service-bus-queues.md)


