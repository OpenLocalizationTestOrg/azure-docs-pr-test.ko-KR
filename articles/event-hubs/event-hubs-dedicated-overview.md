---
title: "Azure 이벤트 허브 전용 용량의 aaaOverview | Microsoft Docs"
description: "Azure Event Hubs Dedicated 용량에 대한 개요입니다."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: sethm;babanisa
ms.openlocfilehash: 79c09975e5c0a6d4729c8f836576770abaaf322e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-event-hubs-dedicated"></a>Event Hubs Dedicated의 개요

*이벤트 허브 전용* 용량 hello 사용 하는 고객에 대 한 단일 테 넌 트 배포를 가장 까다로운 요구 사항도 제공 합니다. 전체 배율을 사용할 때 Azure 이벤트 허브는 수신 수 / 초 또는 too2 g B / 초 완전 내구성이 있는 저장소 및 1 초 미만의 대기 시간으로 원격 분석의 드릴업 2 백만 개 이벤트입니다. 이 또한 수 있도록 통합된 솔루션을 처리 하 여 실시간 및 일괄 처리에서 동일한 시스템을 hello 합니다. 이벤트 허브, 보관 저장소 hello 제품에 포함 된 단일 스트림을 실시간 분석과 일괄 처리 기반 파이프라인을 지원 하 여 솔루션의 hello 복잡성을 줄일 수 있습니다.

hello 다음 표에서 비교 하 여 이벤트 허브의 hello 사용 가능한 서비스 계층입니다. hello 이벤트 허브 전용 제공 된 고정 된 월간 가격의 Standard 및 Basic 기능을 대부분에 대 한 가격 책정 비교 toousage를은 합니다. hello 전용된 계층 hello 표준 계획의 있지만 많은 작업을 사용 하는 고객에 대 한 엔터프라이즈 눈금 용량을 사용 하는 hello 기능을 제공합니다. 

| 기능 | Basic | Standard | 전용 |
| --- |:---:|:---:|:---:|
| 수신 이벤트 | 100만 이벤트당 요금 부과 | 100만 이벤트당 요금 부과 | 포함됨 |
| 처리량 단위(1MB/초 수신, 2MB/초 송신) | 시간당 요금 부과 | 시간당 요금 부과 | 포함됨 |
| 메시지 크기 | 256 KB | 256 KB | 1MB |
| 게시자 정책 | 해당 없음 | 예 | 예 |     
| 소비자 그룹 | 1 - 기본값 | 20 | 20 |
| 메시지 재생 | 예 | 예 | 예 |
| 최대 처리량 단위 | 20 | 20 (유연한 too100)  | 1 CU≈200 |
| 조정된 연결 | 100개 포함 | 1,000개 포함 | 100,000개 포함 |
| 추가 조정된 연결 | 해당 없음 | 예 | 예 |
| 메시지 보존 | 1일 포함 | 1일 포함 | Too7 일 수까지 포함 |
| 보관(미리 보기) | 해당 없음   | 시간당 요금 부과 | 포함됨 |

## <a name="benefits-of-event-hubs-dedicated-capacity"></a>Event Hubs Dedicated 용량의 이점

이벤트 허브 전용 사용 하는 경우 이점은 다음 hello를 사용할 수 있습니다.

* 다른 테넌트의 노이즈가 없는 단일 테넌트 호스팅
* 메시지 크기를 비교할 때 too1 MB 증가 too256 KB 스탠더드 및 Basic입니다.
* 매번 반복 가능한 성능
* 용량 toomeet을 프로그램 버스트 필요한 것이 좋습니다.
* 확장 가능 8 용량 단위 (CU)-1 사이의 초당 too2 백만 수신 이벤트를 제공 합니다.
  * 사용자는 Dedicated에 대해 이벤트 허브, 각 CU 200 처리량 단위 (화 ()) hello 해당 키를 제공할 수 있는 hello 눈금을 관리 합니다.
* 유지 관리 시간 없음: 부하 분산, 운영 체제 업데이트, 보안 패치 및 분할을 Microsoft에서 관리
* 고정 월 요금

또한 이벤트 허브 전용 hello 표준 제품의 hello 처리량이 제한 사항 중 일부를 제거합니다. 기본 및 표준 계층의 처리량 단위 (화) 및 해당 양의 송신 double 당 수신의 초 당 두 번째 또는 1 MB 당 too1000 이벤트 자격 부여 합니다. hello 전용된 눈금 제공 수신에 제한 없는 및 송신 이벤트 수를 계산 합니다. 이러한 제한은 hello 구입 이벤트 허브의 용량을 처리 하는 hello만 적용 됩니다.

이 서비스는 사용자를 대상으로 hello 가장 큰 원격 분석 되며는 기업 계약과 toocustomers를 사용할 수 있습니다.

## <a name="how-tooonboard"></a>어떻게 tooonboard

hello 이벤트 허브 전용 플랫폼은 다양 한 크기와 사용자의 기업 계약을 통해 제공 됩니다. 각 CU 200 처리량 단위 hello 해당 키를 제공합니다. 확장할 수 있습니다 용량에 위로 또는 아래로 hello 월 toomeet 전체에서 요구 사항에 추가 하거나 제거할 사용자. hello 전용된 계획은 이벤트 허브 제품 팀 tooget hello 유연한 배포에 적합 한 hello에서 더 다양 등록 발생 한다는 점에서 고유 합니다. 

## <a name="next-steps"></a>다음 단계
Microsoft 판매 담당자 또는 이벤트 허브 전용 용량에 대 한 tooget 자세한 내용은 Microsoft 기술 지원 서비스에 게 문의 하십시오. 또한 hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수도 있습니다.

가격에 대 한 자세한 정보에 대 한 링크를 따라 hello 방문.

- [Event Hubs Dedicated 가격 책정](https://azure.microsoft.com/pricing/details/event-hubs/) 또한 Microsoft 판매 담당자 또는 Microsoft 기술 지원 서비스 tooget 이벤트 허브 전용 용량에 대 한 추가 정보를 문의할 수 있습니다.
- hello [이벤트 허브 FAQ](event-hubs-faq.md) 가격 책정 정보를 포함 하며 이벤트 허브에 대 한 자주 묻는 질문과 대답을 제공 합니다. 
