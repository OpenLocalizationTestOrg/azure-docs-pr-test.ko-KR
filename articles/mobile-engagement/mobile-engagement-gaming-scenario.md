---
title: "게임 앱에 대 한 aaaAzure Mobile Engagement 구현"
description: "게임 앱 시나리오 tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a>게임 앱에서 Mobile Engagement 구현
## <a name="overview"></a>개요
새 낚시 기반 롤플레이/전략 게임 앱을 출시했습니다. 6 개월 동안 실행 되 고 hello 게임이 되었습니다. 이 게임의 거 대 한 성공 다운로드 수많은 있기 및 hello 보존은 매우 높은 비교 tooother 시작 게임 응용 프로그램입니다. Hello 분기별 검토 회의 이해 관계자 (ARPU) 사용자 당 평균 수익 tooincrease 필요한 동의 합니다. 프리미엄 게임 내 패키지가 특별 제공으로 나와 있습니다. 이러한 게임 팩 hello 게임에서 사용자가 tooupgrade hello 모양과 어 줄 및 lures 또는 tackles 성능을 허용합니다. 그러나 패키지 판매는 매우 낮은 실정입니다. 결정 되므로 분석 도구를 사용한 첫 번째 tooanalyze hello 고객 환경 및 engagement 프로그램 tooincrease 판매 사용 하 여 프로그램 toodevelop 나오는 조각화 합니다.

Hello에 따라 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md) engagement 전략을 작성 합니다.

## <a name="objectives-and-kpis"></a>목표 및 KPI
Hello 게임에 대 한 주요 이해 관계자 충족합니다. 모든 주요 목표-15 %tooincrease 프리미엄 패키지 sales에 동의합니다. 만들 비즈니스 핵심 성과 지표 (Kpi) toomeasure 및 드라이브이 목표

* Hello 게임의 수준에서 이러한 패키지를 구매는?
* 사용자 당, 세션당, 일주일, 및 한 달 hello 수익 이란?
* Hello 즐겨 찾는 구매 유형은 무엇 인가요?

Hello 1 부에서 [시작 가이드](mobile-engagement-getting-started-best-practices.md) toodefine 목표 및 Kpi를 hello 하는 방법에 대해 설명 합니다. 

Hello 비즈니스 Kpi 정의 되었으며,로 Engagement Kpi toodetermine 새 사용자 추세 및 보존 hello 모바일 제품 관리자를 만듭니다.

* 보존을 모니터링 하 고 hello 다음 간격에 걸쳐 사용: 매일, 2 일 마다, 매주, 매월 및 3 개월 마다 해당 날짜
* 활성 사용자 수
* hello 앱 등급 hello에 저장

다음 기술 Kpi hello hello IT 팀의에서 권장 사항에 따라, 질문 다음 tooanswer hello가 추가 되었습니다.

* 사용자 경로(방문한 페이지, 사용자가 이곳에서 사용한 시간)
* 세션별 발생한 중단 또는 버그 수
* 사용자가 실행하는 OS 버전
* 내 사용자를 위해 화면의 평균 크기 hello 이란?
* 사용자가 사용하는 인터넷 연결 종류

각 KPI에 대 한 hello 모바일 제품 관리자 hello 데이터 그녀가 필요한 및 그녀의 플레이 북에서 위치를 지정 합니다.

## <a name="engagement-program-and-integration"></a>Engagement 프로그램 및 통합
고급 engagement 프로그램을 구축 하기 전에 hello 프로젝트를 담당 모바일 프로젝트 디렉터 hello 제품 hello 사용자가 사용 된 방법 및 시기에 대 한 심층적 이해가 있어야 합니다.

3 개월 후 그의 앱에 푸시 알림 sales hello 모바일 프로젝트 디렉터 충분 한 데이터 tooenhance 수집 했습니다. 알아낸 사실은 다음과 같습니다.

* 첫 번째 구매 hello hello 수준 14에서 일반적으로 발생합니다. 90%의 경우, hello 구매 $3에 대 한 새 전설의 웨는입니다.
* 경우 80%가 hello 제품을 계속 하 고 더 많은 구매를 수행한 사용자가 구입 했습니다.
* 사용자 조건이 충족 hello 수준 20, $10/주 이상 toospend 시작입니다.
* 사용자 수준 16, 24 및 32에서 toobuy 프리미엄 패키지는 경향이 있습니다.

앱 판매 toocreate 특정 푸시 알림 시퀀스 tooincrease를 결정 하는 hello 모바일 프로젝트 디렉터 toothis 분석을 감사 합니다. 세 가지 푸시 순서, 즉 시작 프로그램, 판매 프로그램 및 비활성 프로그램을 만들고 이대로 호출합니다. 자세한 내용은 참조 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
