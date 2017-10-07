---
title: "aaaWhat Azure 이벤트 허브는 및 사용 하는 이유 | Microsoft Docs"
description: "개요 및 도입 tooAzure 이벤트 허브-웹 사이트, 앱 및 장치에서 클라우드 규모 원격 분석 수집"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm; babanisa
ms.openlocfilehash: f6199a2e5bee8506f529b6f561234d79f9c8d465
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-event-hubs"></a>Event Hubs란?

Azure Event Hubs는 초당 수백만 개의 이벤트를 수신하고 처리할 수 있는 확장성이 뛰어난 데이터 스트리밍 플랫폼 및 이벤트 수집 서비스입니다. Event Hubs는 분산된 소프트웨어와 장치에서 생성된 이벤트, 데이터 또는 원격 분석을 처리하고 저장할 수 있습니다. 데이터 전송 tooan 이벤트 허브 전환 하 여 모든 실시간 분석 공급자 또는 일괄 처리/저장소 어댑터를 사용 하 여 저장 합니다. Hello 기능 tooprovide와 [게시-구독 기능과](https://msdn.microsoft.com/library/aa560414.aspx) 빅 데이터에 대 한 이벤트 허브 역할 진입점"에" hello을 짧은 대기 시간으로 및 대규모 합니다.

## <a name="why-use-event-hubs"></a>Event Hubs를 사용하는 이유

Event Hubs 이벤트 및 원격 분석 처리 기능은 다음과 같은 경우에 특히 유용합니다.

* 응용 프로그램 계측
* 사용자 환경 또는 워크플로 처리
* IoT(사물 인터넷) 시나리오

예를 들어 Event Hubs를 사용하면 모바일 앱의 동작 추적, 웹 팜의 트래픽 정보, 콘솔 게임의 게임 내 이벤트 캡처 또는 산업용 컴퓨터, 연결된 차량 또는 다른 장치에서 수집한 원격 분석을 수행할 수 있습니다.

## <a name="azure-event-hubs-overview"></a>Azure Event Hubs 개요

hello 일반적인 역할 이벤트 허브에 솔루션 아키텍처는 hello "프런트 도어" 이벤트 파이프라인의 라고도 *생산과 이벤트 사용*합니다. 이벤트 수집기 구성 요소 또는 이벤트 게시자 및 해당 이벤트의 hello 소비에서 이벤트 스트림의 이벤트 소비자 toodecouple hello 프로덕션 사이 있는 서비스입니다. hello 다음 그림은 나타냅니다이 아키텍처를.

![Event Hubs](./media/event-hubs-what-is-event-hubs/event_hubs_full_pipeline.png)

Event Hubs는 메시지 스트림 처리 기능을 제공하지만 기존 엔터프라이즈 메시지와 다른 특징을 가지고 있습니다. Event Hubs 기능은 높은 처리량 및 이벤트 처리 시나리오를 중심으로 구축됩니다. 따라서 이벤트 허브와 다르면 [Azure 서비스 버스](https://azure.microsoft.com/services/service-bus/) 메시징과에 사용할 수 있는 hello 기능 중 일부를 구현 하지 않는 [서비스 버스 메시징](/azure/service-bus-messaging/) 항목 등의 엔터티.

## <a name="event-hubs-features"></a>Event Hubs 기능

이벤트 허브는 다음 주요 요소는 hello를 포함 되어 있습니다.

- [**이벤트 생산자/게시자**](event-hubs-features.md#event-publishers): tooan 이벤트 허브 데이터를 전송 하는 엔터티입니다. 이벤트는 AMQP 1.0 또는 HTTPS를 통해 게시됩니다.
- [**캡처**](event-hubs-features.md#capture): 스트리밍 데이터 toocapture 이벤트 허브를 사용 하면를 Azure Blob 저장소 계정에 저장 합니다.
- [**파티션**](event-hubs-features.md#partitions): 각 소비자 tooonly의 특정 하위 집합 또는 파티션, 읽을 수 있도록 hello 이벤트 스트림입니다.
- [**SAS 토큰**](event-hubs-features.md#sas-tokens): 식별 하 고 hello 이벤트 게시자를 인증 합니다.
- [**이벤트 소비자**](event-hubs-features.md#event-consumers): 이벤트 허브에서 이벤트 데이터를 읽는 엔터티입니다. 이벤트 소비자는 AMQP 1.0을 통해 연결합니다. 
- [**소비자 그룹**](event-hubs-features.md#consumer-groups): 각 여러 hello 이벤트 스트림에 대 한 별도 보기를 응용 프로그램 사용, 해당 소비자 tooact를 독립적으로 활성화를 제공 합니다.
- [**처리량 단위**](event-hubs-features.md#capacity): 미리 구입한 용량의 단위입니다. 단일 파티션에는 처리량 단위 하나의 최대 크기가 있습니다.

이러한 오류 코드 및 기타 이벤트 허브 기능에 대 한 기술 세부 정보에 대 한 참조 hello [이벤트 허브 기능 개요](event-hubs-features.md)합니다. 

## <a name="next-steps"></a>다음 단계

Event Hubs 가격에 대한 자세한 내용은 [Event Hubs 가격](https://azure.microsoft.com/pricing/details/event-hubs/)을 참조하세요.

이벤트 허브에 대 한 자세한 내용은 다음 링크는 hello 방문.

* [Event Hubs 자습서](event-hubs-dotnet-standard-getstarted-send.md) 시작
* [Event Hubs FAQ](event-hubs-faq.md)
* [Event Hubs를 사용하는 샘플 응용 프로그램](https://github.com/Azure/azure-event-hubs/tree/master/samples)
 
 

