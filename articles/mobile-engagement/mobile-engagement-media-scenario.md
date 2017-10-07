---
title: "미디어 응용 프로그램에 대 한 aaaAzure Mobile Engagement 구현"
description: "미디어 응용 프로그램 시나리오 tooimplement Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a495eb790993a30d5c03802aa9e6404fea983d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-media-app"></a>미디어 앱에 Mobile Engagement 구현
## <a name="overview"></a>개요
John은 큰 미디어 회사의 모바일 프로젝트 관리자입니다. 최근에 새로운 앱을 출시했는데 다운로드 수가 매우 높습니다. 다운로드 목표는 달성했지만 사용자당 투자 수익률(ROI)은 필요 조건을 충족하지 못하고 있습니다. 

John은 이미 ROI가 너무 낮은 이유를 확인했습니다. 사용자들이 앱 사용을 2주 후에 중단하는 경우가 빈번하고 이들 중 대부분이 다시 돌아오지 않고 있습니다. 그의 응용 프로그램의 tooincrease hello 보존을 하고자 했습니다.

몇 가지 초기 테스트를 마친 후 그이 알고 그의 사용자가 일어났거나 그 toocontinue 자신의 응용 프로그램을 사용 하 여 푸시 알림 광범위 합니다. 또한 활성화 하지 않은 사용자가는 종종 알림 보내 그에 따라 toohello 응용 프로그램을 반환 합니다. 이한일은 푸시 알림 고급 대상 지정을 사용 하 여 자신의 앱에 대 한 tooinvest Engagement 프로그램의 일부 종류에서를 결정 합니다.

이한일은 hello 읽기 최근에 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md) 및 hello 가이드에서 tooimplement hello 권장 사항을 결정 했습니다.

## <a name="objectives-and-kpis"></a>목표 및 KPI
John의 앱에 대한 주요 관련자 사용자가 미디어를 소비하면 광고를 통해 수입이 발생합니다. 사용자당 소비되는 콘텐츠를 증가시키면 John의 수익도 증가됩니다. 하나의 기본 목표에 동의 하는 모든: 25% 씩 광고에서 tooincrease 판매 합니다. 만들 비즈니스 핵심 성과 지표 (Kpi) toomeasure 및 드라이브이 목표

* 사용자당 클릭한 광고 수
* 방문한 페이지 수(사용자별/세션별/주별/월별)
* 즐겨찾는 범주는 무엇인가요?

John은 주요 관련자들과의 회의에 근거하여 비즈니스 KPI를 정의합니다. 그 뒤에 오는 hello의 1 부 [Azure Mobile Engagement 설명서와 모범 사례](mobile-engagement-getting-started-best-practices.md)합니다. 

다음으로, 그 다음 목표에 도달 하면 Engagement Kpi tooensure hello를 만듭니다.

* 보존 간격 뒤 hello 모니터링: 매일, 매주, 격주 및 월별 합니다.
* 활성 사용자 수
* hello 앱 등급 hello 응용 프로그램에서 저장

다음 기술 Kpi hello hello IT 팀의에서 권장 사항에 따라, 질문 다음 tooanswer hello가 추가 되었습니다.

* 사용자 경로(방문한 페이지, 사용자가 이곳에서 보낸 시간)
* 세션당 발생한 충돌 수 또는 버그 수
* 사용자가 실행하는 OS 버전
* 내 사용자를 위해 화면의 평균 크기 hello 이란?
* 사용자가 사용하는 인터넷 연결 종류

각 KPI에 대 한 필요한 hello 데이터를 분류 하는 그 및 그의 플레이 북의 hello 적절 한 위치에 기록 했습니다.

## <a name="engagement-program-and-integration"></a>Engagement 프로그램 및 통합
John은 KPI 정의를 완료한 후에 4개의 Engagement 프로그램과 목표를 정의하여 Engagement 전략 단계를 시작합니다.![][1]

John은 각 프로그램에 대한 푸시 알림을 자세히 열거하면서 깊이 들어갑니다. 푸시 알림은 다섯 가지 요소로 정의됩니다.

1. 목표: hello 알림 hello 목표 란
2. Hello 목표 연결할 수는 방법
3. 대상: 알림을 받을 사람을 hello?
4. 내용: hello 단어 및 hello 형식의 hello 알림 (App/Out의 앱에서) 란
5. 경우에: 어떤는 hello 최상의 순간 toosend이 푸시 알림
   
    ![][2]

자세한 내용은 참조 toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)합니다.

Toocollect 및 IT 팀 tooimplement hello 솔루션과 그의 태그를 공동으로 계획 하는 쓰기 toohello 파트 2/hello 백서 이한일은 사용 하 여 대상 섹션 toodefine 그에 데이터를 따르는입니다. 구현 1주일 후, 사용자 승인 테스트 후에 John은 드디어 프로그램을 출시할 수 있게 됩니다.

## <a name="program-results"></a>프로그램 결과
4개월 후 John은 프로그램의 성과를 검토합니다. 시작 프로그램 hello 및 hello 매주 프로그램의 목표 충족 합니다. hello 하나만 세션과 사용자 수가 감소 하 고 hello 응용 프로그램의 더 많은 기능을 사용 하 고 연결 수를 주별로 hello 수 두 배 향상 합니다.

hello **비활성 프로그램** 되어 사용자 경향을 이해 하는 John 지원 합니다. Hello 비활성 사용자의 15 %toohello 앱 돌아와서 나타납니다. 하지만 이들 대부분이 1달 이상 활성 상태를 유지하지 않습니다. John은 알림을 추가하고 콘텐츠 선택 범위를 확장하여 이렇게 반복되는 상황을 잠재적으로 최적화할 수 있다고 예상합니다.

hello **검색 프로그램** 제대로 작동 하지 않습니다. 그의 목적을 판매 중인 하지만 부족 tooreach 크로스 증가합니다. 이한일은 그 하지 않는 충분 한 데이터 toomake 관련 대상으로 지정 하 고 해당 콘텐츠를 제안 식별 합니다. 이 프로그램을 중지하고 Azure Mobile Engagement를 사용하여 “사설 푸시 알림”을 전송하는 것에 중점을 둡니다. 이미 그의 저널리스트 CMS 솔루션 toosend 푸시 알림을 있고 toochange 되지 않도록 합니다.

이한일은은 toouse hello Reach API는 Reach 캠페인 toouse AZME 웹 인터페이스 필요 없이 관리를 허용 하는 HTTP REST API를 결정 합니다. John이 방법을 사용 하며 그의 작성자를 허용 합니다. 그 hello 데이터를 수집할 수 tookeep hello CMS 솔루션을 사용 합니다.

기능이 올바르게 작동 하는 tooensure, John hello 지점 다음에 주의 IT 팀 toobe를 게 묻습니다.

1. **운영 체제** : 바쁘기 때문에 John toolist 모든 사례 및 검사 Api hello을 처리 하는 경우 자신의 규칙 tooadministrate 푸시 알림을가지고 있는 것입니다.
   예: Android 푸시 시스템 hello 경우 iOS와는 큰 그림을 수 있습니다.
2. **시간 프레임**: 이한일은 hello에 대 한 시간대를 설정 하 고 최종 toocampaigns를 설정 하는 API가 있습니다. 모든 장치를 중단 해야 알림 폭탄 테러 toopreserve 사용자가 원하는 합니다.
3. **범주**: 마케팅 팀은 각각의 경고 유형에 대한 템플릿을 준비합니다. 이한일은은 hello API 내 IT 팀 tooset 범주를 요청합니다.

테스트를 거친 후에 John은 만족하게 됩니다. 감사 toothis API 저널리스트 여전히 해당 CMS에서 푸시 알림을 보내고에 모든 동작 데이터를 수집 하는 Azure Mobile Engagement

초반 4개월이 지난 후에, 전반적으로 만족할만한 성과가 결과에 반영되었고, John과 이사회는 확신을 갖게 되었으며, 사용자당 ROI가 15% 증가하고 모바일 매출이 총 매출의 17.5 %를 차지하면서 단 4개월 만에 7.5%가 증가되었습니다.

<!--Image references-->
[1]: ./media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: ./media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks
