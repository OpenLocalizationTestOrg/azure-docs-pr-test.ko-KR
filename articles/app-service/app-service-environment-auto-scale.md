---
title: "aaaAutoscaling 및 앱 서비스 환경 v1"
description: "자동 크기 조정 및 앱 서비스 환경"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>자동 크기 조정 및 App Service Environment v1

> [!NOTE]
> 앱 서비스 환경 v1 hello에 대 한이 문서는입니다.  최신 버전의 hello 쉽게 toouse 되며 더 강력한 인프라에서 실행 하는 앱 서비스 환경 있습니다. hello로 시작 하는 hello 새 버전에 대 한 자세한 toolearn [소개 toohello 앱 서비스 환경](../app-service/app-service-environment/intro.md)합니다.
> 

Azure 앱 서비스 환경은 *자동 크기 조정*을 지원합니다. 메트릭 또는 일정에 따라 개별 작업자 풀을 자동 크기 조정할 수 있습니다.

![작업자 풀에 대한 자동 크기 조정 옵션입니다.][intro]

자동 크기 조정 최적화 하면 리소스 사용률 자동으로 증가 하 고 앱 서비스 환경 toofit 축소 예산 또는 부하 프로필 합니다.

## <a name="configure-worker-pool-autoscale"></a>작업자 풀 자동 크기 조정 구성
Hello에서 hello 자동 크기 조정 기능에 액세스할 수 **설정을** hello 작업자 풀의 탭 합니다.

![Hello 작업자 풀의 설정 탭 합니다.][settings-scale]

여기에서 hello 인터페이스 이후 매우 친숙 한는 hello 응용 프로그램 서비스를 확장할 때 나타나는 동일한 환경을 계획입니다. 

![수동 크기 조정 설정입니다.][scale-manual]

또한 자동 크기 조정 프로필을 구성할 수 있습니다.

![자동 크기 조정 설정입니다.][scale-profile]

자동 크기 조정 프로필은 눈금에 대해 유용한 tooset 제한 합니다. 이렇게 하면 하한 크기 값(1)을 설정하여 일관된 성능 환경을 유지하고 상한(2)을 설정하여 예측 가능한 지출 한도를 정할 수 있습니다.

![프로필의 크기 조정 설정입니다.][scale-profile2]

프로필을 정의한 후에 hello 작업자 풀 hello 프로필에 정의 된 hello 범위 내에 있는 인스턴스의 hello 수의 위아래로 자동 크기 조정 규칙 tooscale를 추가할 수 있습니다. 자동 크기 조정 규칙은 메트릭을 기반으로 합니다.

![크기 조정 규칙입니다.][scale-rule]

 모든 작업자 풀 또는 프런트 엔드 메트릭을 사용 하는 toodefine 자동 크기 조정 규칙 수 있습니다. 이러한 메트릭은 hello에 대 한 경고가 동일한 메트릭을 hello 리소스 블레이드 그래프에 모니터링 하거나 설정할 수 있습니다.

## <a name="autoscale-example"></a>자동 크기 조정 예제
앱 서비스 환경의 자동 크기 조정은 시나리오를 살펴보면서 가장 잘 설명할 수 있습니다.

이 문서에서는 자동 크기 조정을 설정할 때 모든 hello 필요한 고려 사항이 설명 합니다. hello 문서에서는 앱 서비스 환경에서 호스트 되는 앱 서비스 환경에서 자동 크기 조정 고려 하는 경우에 상호 작용 재생 hello을 안내 합니다.

### <a name="scenario-introduction"></a>시나리오 소개
Frank가 마이그레이션 tooan 앱 서비스 환경 관리 하는 hello 작업 부하의 일부는 엔터프라이즈에 대 한 sysadmin입니다.

hello 앱 서비스 환경이 toomanual 크기 조정을 구성 다음과 같습니다.

* **프런트 엔드:** 3
* **작업자 풀 1**: 10
* **작업자 풀 2**: 5
* **작업자 풀 3**: 5

작업자 풀 1은 프로덕션 워크로드에, 작업자 풀 2 및 작업자 풀 3은 QA(품질 보증) 및 개발 워크로드에 사용됩니다.

hello 앱 서비스 계획에 대 한 QA 및 dev toomanual 크기 조정을 구성 합니다. 앱 서비스 계획 hello 프로덕션 부하 및 트래픽 tooautoscale toodeal 변형으로 설정 되어 있습니다.

Frank가 hello 응용 프로그램에 잘 알고 있습니다. 그 hello office 상태인 직원이 사용 하는 기간 업무 (LOB) 응용 프로그램 이므로 부하에 대 한 hello 사용이 많은 시간별 오전 9시 및 오후 6시 사이 알고 있습니다. 사용자가 퇴근한 후에는 사용량이 줍니다. 사용이 많은 시간 외 여전히 일부 부하는 사용자가 액세스할 수 있으므로 hello 앱 원격으로 자신의 모바일 장치 또는 홈 Pc를 사용 하 여. 앱 서비스 계획은 이미 hello 프로덕션 tooautoscale 규칙에 따라 hello로 CPU 사용량에 따라 구성 합니다.

![LOB 앱에 대한 특정 설정입니다.][asp-scale]

| **자동 크기 조정 프로필 - 주중 - 앱 서비스 계획** | **자동 크기 조정 프로필 - 주말 - 앱 서비스 계획** |
| --- | --- |
| **이름:** 주중 프로필 |**이름:** 주말 프로필 |
| **크기 조정 기준:** 일정 및 성능 규칙 |**크기 조정 기준:** 일정 및 성능 규칙 |
| **프로필:** 주중 |**프로필:** 주말 |
| **유형:** 반복 |**유형:** 반복 |
| **대상 범위:** 5 too20 인스턴스 |**대상 범위:** 3 too10 인스턴스 |
| **요일:** 월요일, 화요일, 수요일, 목요일, 금요일 |**요일:** 토요일, 일요일 |
| **시작 시간:** 오전 9시 |**시작 시간:** 오전 9시 |
| **표준 시간대:** UTC-08 |**표준 시간대:** UTC-08 |
|  | |
| **자동 크기 조정 규칙(확장)** |**자동 크기 조정 규칙(확장)** |
| **리소스:** 프로덕션(앱 서비스 환경) |**리소스:** 프로덕션(앱 서비스 환경) |
| **메트릭:** CPU % |**메트릭:** CPU % |
| **작업:** 60% 초과 |**작업:** 80% 초과 |
| **기간:** 5분 |**기간:** 10분 |
| **집계 시간:** 평균 |**집계 시간:** 평균 |
| **작업:** 개수 2씩 증가 |**작업:** 개수 1씩 증가 |
| **정지(분):** 15 |**정지(분):** 20 |
|  | |
| **자동 크기 조정 규칙(축소)** |**자동 크기 조정 규칙(축소)** |
| **리소스:** 프로덕션(앱 서비스 환경) |**리소스:** 프로덕션(앱 서비스 환경) |
| **메트릭:** CPU % |**메트릭:** CPU % |
| **작업:** 30% 미만 |**작업:** 20% 미만 |
| **기간:** 10분 |**기간:** 15분 |
| **집계 시간:** 평균 |**집계 시간:** 평균 |
| **작업:** 개수 1씩 감소 |**작업:** 개수 1씩 감소 |
| **정지(분):** 20 |**정지(분):** 10 |

### <a name="app-service-plan-inflation-rate"></a>앱 서비스 계획 인플레이션 속도
앱 서비스 계획을 구성 된 tooautoscale 있는 시간당 최대 속도로 이렇게 합니다. 이 속도 수 수 기반으로 계산 hello hello 자동 크기 조정 규칙에서 제공 합니다.

이해 하 고 계산 hello *앱 서비스 계획 인플레이션이 요금* 배율 변경 내용을 tooa 작업자 풀 순간 없기 때문에 앱 서비스 환경 크기 자동 조정에 대 한 중요 합니다.

앱 서비스 계획 인플레이션이 요금 hello 다음과 같이 계산 됩니다.

![앱 서비스 계획 인플레이션 속도 계산입니다.][ASP-Inflation]

Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 요일 프로필에 대 한 크기 확장 규칙 기반으로 합니다.

![자동 크기 조정 - 확장 규칙에 따른 주중의 앱 서비스 계획 인플레이션 속도입니다.][Equation1]

Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 주말 프로필에 대 한 크기 확장 규칙의 hello 경우에서 hello 수식을 확인 합니다.

![자동 크기 조정 - 확장 규칙에 따른 주말의 앱 서비스 계획 인플레이션 속도입니다.][Equation2]

이 값은 축소 작업에 대해서도 산출할 수 있습니다.

Hello 자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 요일 프로필에 대 한 아래쪽 크기 조정 규칙에 따라이 보여 줍니다.

![자동 크기 조정 - 축소 규칙에 따른 주중의 앱 서비스 계획 인플레이션 속도입니다.][Equation3]

자동 크기 조정-hello 프로덕션 앱 서비스 계획의 hello 주말 프로필에 대 한 배율 아래로 규칙 hello hello 경우에서 hello 수식을 확인 합니다.  

![자동 크기 조정 - 축소 규칙에 따른 주말의 앱 서비스 계획 인플레이션 속도입니다.][Equation4]

hello 프로덕션 앱 서비스 계획에서 최대 속도는 hello 주 인스턴스/시간 및 주말 hello 4 개의 인스턴스/시간 증가할 수 있습니다. Hello 주간에 4 개의 인스턴스/시간에서 최대 속도로 인스턴스 및 주말 중 6 개 인스턴스/시간을 해제할 수 있습니다.

앱 서비스 계획을 여러 작업자 풀에서 호스트 되는, 있으면 toocalculate hello *인플레이션이 초 당 총* 앱 서비스 계획을 만들고 있는 모든 hello에 대 한 hello 인플레이션이 비율의 hello 합계로 작업자 풀의 호스트입니다.

![작업자 풀에서 호스팅되는 여러 앱 서비스 계획에 대한 총 인플레이션 속도 계산입니다.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>사용 하 여 hello 앱 서비스 계획 인플레이션이 속도 toodefine 작업자 풀 자동 크기 조정 규칙
작업자는 tooautoscale 구성된 되어 있는 앱 서비스 계획의 용량 버퍼 할당 해야 합니다. 해당 호스트를 풀링합니다. hello 버퍼 hello 자동 크기 조정 작업 toogrow 허용 하며 필요에 따라 앱 서비스 계획을 축소 합니다. hello 앱 서비스 계획 인플레이션이 초 당 총 계산 hello 최소 버퍼 수 있습니다.

앱 서비스 환경 크기 조정 작업이 몇 시간 tooapply 걸리므로 모든 변경 내용이 추가 크기 조정 작업이 진행 중인 동안이 오류가 발생할 수 있는 요청 변경을 고려해 야 합니다. tooaccommodate 이러한 대기 시간은 권장를 사용 하는 hello hello 최소 각 자동 크기 조정 작업에 대해 추가 된 인스턴스 수로 전체 앱 서비스 계획 인플레이션이 비율을 계산 합니다.

이 정보를 사용 하 여 Frank hello 정의할 수 자동 크기 조정 프로필 및 규칙:

![LOB 예제에 대한 자동 크기 조정 프로필 규칙입니다.][Worker-Pool-Scale]

| **자동 크기 조정 프로필 – 주중** | **자동 크기 조정 프로필 – 주말** |
| --- | --- |
| **이름:** 주중 프로필 |**이름:** 주말 프로필 |
| **크기 조정 기준:** 일정 및 성능 규칙 |**크기 조정 기준:** 일정 및 성능 규칙 |
| **프로필:** 주중 |**프로필:** 주말 |
| **유형:** 반복 |**유형:** 반복 |
| **대상 범위:** 13 too25 인스턴스 |**대상 범위:** 6 too15 인스턴스 |
| **요일:** 월요일, 화요일, 수요일, 목요일, 금요일 |**요일:** 토요일, 일요일 |
| **시작 시간:** 오전 7시 |**시작 시간:** 오전 9시 |
| **표준 시간대:** UTC-08 |**표준 시간대:** UTC-08 |
|  | |
| **자동 크기 조정 규칙(확장)** |**자동 크기 조정 규칙(확장)** |
| **리소스:** 작업자 풀 1 |**리소스:** 작업자 풀 1 |
| **메트릭:** WorkersAvailable |**메트릭:** WorkersAvailable |
| **작업:** 8 미만 |**작업:** 3 미만 |
| **기간:** 20분 |**기간:** 30분 |
| **집계 시간:** 평균 |**집계 시간:** 평균 |
| **작업:** 개수 8씩 증가 |**작업:** 개수 3씩 증가 |
| **정지(분):** 180 |**정지(분):** 180 |
|  | |
| **자동 크기 조정 규칙(축소)** |**자동 크기 조정 규칙(축소)** |
| **리소스:** 작업자 풀 1 |**리소스:** 작업자 풀 1 |
| **메트릭:** WorkersAvailable |**메트릭:** WorkersAvailable |
| **작업:** 8 초과 |**작업:** 3 초과 |
| **기간:** 20분 |**기간:** 15분 |
| **집계 시간:** 평균 |**집계 시간:** 평균 |
| **작업:** 개수 2씩 감소 |**작업:** 개수 3씩 감소 |
| **정지(분):** 120 |**정지(분):** 120 |

hello hello 프로필에 정의 된 대상 범위는 hello 앱 서비스 계획에 대 한 프로필 + 버퍼에 정의 된 hello 최소 인스턴스 여 계산 됩니다.

hello 최대 범위 hello 합계 hello 작업자 풀에서 호스팅되는 모든 앱 서비스 계획에 대 한 모든 hello 최대 범위를 가진 것입니다.

hello hello 수직 확장 규칙에 대 한 증가 수를 눈금에 대 한 앱 서비스 계획 인플레이션이 요금 X 집합 tooat 최소 1 이어야 합니다.

1 X 아래로 눈금에 대 한 앱 서비스 계획 인플레이션이 속도 hello 또는 감소 수 조정된 toosomething X 1/2 사이 수 있습니다.

### <a name="autoscale-for-front-end-pool"></a>프런트 엔드 풀에 대한 자동 크기 조정
프런트 엔드 자동 크기 조정에 대한 규칙은 작업자 풀에 대한 것보다 간단합니다. 기본적으로  
앱 서비스 계획에서 크기 조정 작업 순간 없는 hello 측정 및 hello 쿨 다운 타이머의 기간을 고려 하 고 있는지 확인 합니다.

이 시나리오에서는 Frank 알고 해당 hello 오류율 프런트 엔드 CPU 사용률이 80%에 도달 하는 후 늘어나고 hello 자동 크기 조정 규칙 tooincrease 인스턴스 다음과 같이 설정 합니다.

![프런트 엔드 풀에 대한 자동 크기 조정 설정입니다.][Front-End-Scale]

| **자동 크기 조정 프로필 – 프런트 엔드** |
| --- |
| **이름:** 자동 크기 조정 - 프런트 엔드 |
| **크기 조정 기준:** 일정 및 성능 규칙 |
| **프로필:** 매일 |
| **유형:** 반복 |
| **대상 범위:** 3 too10 인스턴스 |
| **요일:** 매일 |
| **시작 시간:** 오전 9시 |
| **표준 시간대:** UTC-08 |
|  |
| **자동 크기 조정 규칙(확장)** |
| **리소스:** 프런트 엔드 풀 |
| **메트릭:** CPU % |
| **작업:** 60% 초과 |
| **기간:** 20분 |
| **집계 시간:** 평균 |
| **작업:** 개수 3씩 증가 |
| **정지(분):** 120 |
|  |
| **자동 크기 조정 규칙(축소)** |
| **리소스:** 작업자 풀 1 |
| **메트릭:** CPU % |
| **작업:** 30% 미만 |
| **기간:** 20분 |
| **집계 시간:** 평균 |
| **작업:** 개수 3씩 감소 |
| **정지(분):** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
