---
title: "자동 크기 조정에 대 한 aaaBest 사례 | Microsoft Docs"
description: "Azure에서 웹앱, 가상 컴퓨터 확장 집합 및 Cloud Services에 대한 자동 크기 조정 패턴"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>자동 크기 조정에 대한 모범 사례
이 문서에서는 Azure에서 모범 사례 tooautoscale에 설명 합니다. Azure 모니터의 자동 크기 조정 적용만 너무[가상 컴퓨터 크기 집합](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [클라우드 서비스](https://azure.microsoft.com/services/cloud-services/), 및 [앱 서비스-웹 응용 프로그램](https://azure.microsoft.com/services/app-service/web/)합니다. 다른 Azure 서비스에는 다른 크기 조정 방법이 사용됩니다.

## <a name="autoscale-concepts"></a>자동 크기 조정 개념
* 하나의 리소스에는 *하나의* 자동 크기 조정 설정만 있을 수 있습니다.
* 자동 크기 조정 설정에는 하나 이상의 프로필이 있을 수 있으며, 각 프로필에는 하나 이상의 자동 크기 조정 규칙이 있을 수 있습니다.
* 자동 크기 조정 설정 조정 인스턴스 가로로 변수인 *아웃* hello 인스턴스 수를 늘리면 여 및 *에* hello 인스턴스 수가 감소 하 여 합니다.
  자동 크기 조정 설정에는 최대, 최소 및 기본 인스턴스 값이 있습니다.
* 자동 크기 조정 작업은 항상 hello 경우 연결 된 메트릭 tooscale 확인 하 여, 확장 또는 배율 기능에 대 한 hello 구성 된 임계값을 초과 했음을 읽습니다. [Azure Monitor 자동 크기 조정 공통 메트릭](insights-autoscale-common-metrics.md)에서 자동 크기 조정을 통해 크기를 조정할 수 있는 메트릭 목록을 볼 수 있습니다.
* 모든 임계값은 인스턴스 수준에서 계산됩니다. 예를 들어, "1 인스턴스 축소 별 크기 조정 인스턴스 수는 2 때 CPU > 80%의 경우 평균", 모든 인 스턴에서 hello 평균 CPU가 80% 보다 크면 확장을 의미 합니다.
* 항상 메일을 통해 오류 알림이 제공됩니다. 특히, hello 소유자, 참가자 및 독자 hello 대상 리소스의 전자 메일을 수신 합니다. 또한 자동 크기 조정이 오류에서 복구하여 정상적으로 작동하기 시작하면 항상 *복구* 메일이 제공됩니다.
* 있습니다 수 옵트인 tooreceive 전자 메일 및 webhook을 통해 성공적으로 크기 조정 작업 알림 합니다.

## <a name="autoscale-best-practices"></a>자동 크기 조정 모범 사례
자동 크기 조정을 사용 하 여 모범 사례를 따르는 hello를 사용 합니다.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Hello 최대값과 최소값을 다른 있고 사이의 적절 한 여백을 확인합니다
최소한 된 설정이 있는 경우 = 2, 최대 2 = hello 현재 인스턴스 수는 2, 없음, 크기 조정 작업이 발생할 수 있습니다. 적절 한 여백 값이 포함 됩니다는 hello 최대 및 최소 인스턴스 수 간의 유지 합니다. 자동 크기 조정은 항상 이러한 한도 사이에서 크기를 조정합니다.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>수동 크기 조정이 자동 크기 조정 최소값 및 최대값으로 다시 설정됨
수동으로 위의 hello 인스턴스 개수 tooa 값을 업데이트 하거나 hello 최대 아래 자동 크기 조정 엔진을 자동으로 hello 백 toohello 최소 (아래 경우) 또는 hello 최대 (위의 경우)를 조정 합니다. 예를 들어 3 자에서 6 사이 hello 범위를 설정할 수 있습니다. 하나의 실행 중인 인스턴스를 설정한 경우 hello 자동 크기 조정 엔진에 다음 실행 too3 인스턴스를 확장 합니다. 마찬가지로, 것은 눈금 인 8 개의 인스턴스가에 다음 실행 too6를 백업 합니다.  Hello 자동 크기 조정 규칙에도 다시 설정 해야만 수동 크기 조정 하는 것은 매우 일시적인입니다.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>항상 증가 및 감소를 수행하는 규모 확장 및 감축 규칙 조합 사용
Hello 조합의 한 부분을 사용 하는 경우 자동 크기 조정 확장 스냅인의 hello 최대값 또는 최소값, 될 때까지 단일 out, 또는에 도달 했습니다.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>자동 크기 조정을 관리할 때 hello Azure 포털 및 Azure 클래식 포털 hello 간에 전환 되지 않습니다
클라우드 서비스 및 응용 프로그램 서비스 (웹 앱)에 대 한 Azure 포털 (portal.azure.com) toocreate hello를 사용 하 여 및 자동 크기 조정 설정을 관리 합니다. 가상 컴퓨터 크기 집합에 대 한 toocreate PowerShell, CLI 또는 REST API를 사용 하 여 및 자동 크기 조정 설정을 관리 합니다. 자동 크기 조정 구성을 관리 하는 경우 Azure 클래식 포털 (manage.windowsazure.com) hello 및 hello Azure 포털 (portal.azure.com) 간에 전환 하지 마십시오. Azure 클래식 포털 hello 및 해당 기본 백 엔드에 제한 사항이 있습니다. 그래픽 사용자 인터페이스를 사용 하 여 toohello Azure 포털 toomanage 자동 크기 조정을 이동 합니다. hello 옵션은 PowerShell, CLI 또는 (Azure 리소스 탐색기)를 통해 REST API toouse hello 자동 크기 조정 합니다.

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Hello 진단 메트릭에 대 한 적절 한 통계를 선택 합니다.
진단 메트릭에 대 한 중에서 선택할 수 있습니다 *평균*, *최소*, *최대* 및 *총* 하 여 메트릭 tooscale로 합니다. hello 가장 일반적인 통계는 *평균*합니다.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>모든 메트릭 형식에 대해 신중 하 게 hello 임계값을 선택 합니다.
현실적인 상황을 기반으로 서로 다른 규모 확장 및 규모 감축 임계값을 신중하게 선택하는 것이 좋습니다.

우리 *권장 하지는 않습니다* hello 예에서는 아래와 같은 자동 크기 조정 설정에 대 한 조건에 및 동일 하거나 매우 유사한 임계값 값 hello:

* 스레드 수가 600 이하인 경우 인스턴스 수 1개 증가
* 스레드 수가 600 이상인 경우 인스턴스 수 1개 감소

혼동 스 러 울 수 tooa 동작을 일으킬 수 있습니다 어떻게의 예를 살펴 보겠습니다. Hello를 순서를 따르는 것이 좋습니다.

1. 와 2 인스턴스 toobegin 많고 hello 평균 인스턴스당 스레드 수 too625 증가 하는 다음을 가정 합니다.
2. 자동 크기 조정에서 세 번째 인스턴스를 추가하여 규모를 확장합니다.
3. 다음으로, 인스턴스 전체에서 hello 평균 스레드 수가 too575 들어가는지 가정 합니다.
4. 자동 크기 조정 시도 줄일 하기 전에 tooestimate hello 최종 상태에 크기가 조정 하는 경우 됩니다 합니다. 예를 들어 575x3(현재 인스턴스 수) = 1,725/2(축소된 경우의 최종 인스턴스 수) = 862.5스레드입니다. 즉 자동 크기 조정은 tooimmediately 확장 다시을 확장 한 후에 동일한 또는 짝수 hello 평균 스레드 수 유지 hello 조금만 뒤쳐지면 합니다. 그러나 것 수직 확장 다시 hello 전체 프로세스를 반복 하는 경우 앞 tooan 무한 루프에 있습니다.
5. tooavoid 이러한 상황 (라 함 "날개를 퍼 덕"), 자동 크기 조정 확장 되지 않는 전혀 합니다. 대신, 건너뜁니다 고 hello 조건이 다시 hello 다음 시간 hello 서비스의 작업이 실행을 다시 평가 합니다. Hello 평균 스레드 수가 575 되었을 때 자동 크기 조정 toowork 표시 없게 되기 때문에 많은 사람들이 혼동을 줄 수이 합니다.

예측 중에 확장은 의도 한 tooavoid "플 래핑" 배율 기능 및 확장 작업 지속적으로 어디로 간에 상황입니다. Hello 및 확장에 대해 동일한 임계값을 선택 하면이 동작을 염두에 두십시오.

Hello 확장 사이 및 임계값에는 적절 한 여백을 선택 하는 것이 좋습니다. 예를 들어 hello를 더 나은 규칙 조합을 따르는 것이 좋습니다.

* CPU%가 80 이상인 경우 인스턴스 수 1개 증가
* CPU%가 60 이하인 경우 인스턴스 수 1개 감소

이 경우  

1. 와 2 인스턴스 toostart 있다고 가정해 보십시오.
2. 인스턴스 간에 hello 평균 CPU %too80 되 면 자동 크기 조정 세 번째 인스턴스를 추가 하 여 확장 합니다.
3. 이제 hello CPU 시간을 통해 % 들어가는지 too60 가정 합니다.
4. 자동 크기 조정의 눈금에 규칙 tooscale 인 경우 hello 최종 상태를 예측 합니다. 예를 들어 60x3(현재 인스턴스 수) = 180/2(축소된 경우의 최종 인스턴스 수) = 90입니다. 따라서 자동 크기 조정 않습니다 눈금-에 없는 했을 때 tooscale 아웃 즉시 다시 때문에 있습니다. 대신, 규모 축소를 건너뜁니다.
5. hello CPU 계속 toofall too50 hello 다음 시간 자동 크기 조정 확인 합니다. 50 x 3 인스턴스를 다시-추정 = 150 / 2 인스턴스 = too2 인스턴스에 성공적으로 확장 하므로 80, hello 확장 임계값 아래에 있는 75입니다.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>특정 메트릭의 임계값 조정에 대한 고려 사항
 저장소나 서비스 버스 큐 길이 메트릭에 같은 특별 한 메트릭을 hello 임계값의 현재 인스턴스 수가 당 사용할 수 있는 메시지의 hello 평균 수입니다. Hello를 신중 하 게 선택이 메트릭에 대 한 hello 임계값 값을 선택 합니다.

보겠습니다 보여 주기 예제 tooensure와 더 나은 hello 동작을 알고 있습니다.

* 저장소 큐 메시지 수가 50개 이상인 경우 인스턴스 수 1개 증가
* 저장소 큐 메시지 수가 10개 이하인 경우 인스턴스 수 1개 감소

시퀀스를 수행 하는 hello를 고려 합니다.

1. 2개의 저장소 큐 인스턴스가 있습니다.
2. 메시지 계속 나타나는 경우 및 hello 저장소 큐를 검토할 때는 hello 총 읽기 수 50입니다. 자동 크기 조정에서 규모 확장 동작을 시작해야 한다고 생각할 수 있습니다. 그러나 인스턴스당 메시지 수는 여전히 50/2 = 25개입니다. 따라서 규모 확장이 발생하지 않습니다. Hello 첫 번째 확장 toohappen, hello 저장소 큐에 hello 총 메시지 수가 100 이어야 합니다.
3. 다음으로 hello 총 메시지 수가 100에 도달 하는 것으로 가정 합니다.
4. 타사 저장소 큐 인스턴스 tooa 확장 동작 때문에 추가 됩니다.  hello 다음 확장 작업이 발생 하지 않고 hello 총 될 때까지 hello 큐의 메시지 수 때문에 150에 도달 하면 150/3 = 50입니다.
5. 이제 hello hello 큐의 메시지 수가 점점 더 작아집니다. 3 인스턴스와 hello 첫 번째 눈금에 수행 되는 동작 면 hello 때문에 모든 큐의 총 메시지 too30 합계 30/3 = hello에 대 한 크기 조정 임계값은 인스턴스당 10 메시지입니다.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>자동 크기 조정 설정에 여러 프로필이 구성된 경우 크기 조정에 대한 고려 사항
자동 크기 조정 설정에서 일정이나 시간에 종속되지 않고 항상 적용되는 기본 프로필을 선택하거나, 날짜 및 시간 범위가 있는 고정된 기간의 프로필 또는 되풀이 프로필을 선택할 수 있습니다.

자동 크기 조정 서비스를 처리 하는 경우 항상 순서에 따라 hello에 확인 합니다.

1. 고정된 날짜 프로필
2. 되풀이 프로필
3. 기본("항상") 프로필

프로필 조건이 충족 될 경우 자동 크기 조정 hello 그 아래의 다음 프로필 상태를 확인 하지 않습니다. 자동 크기 조정에서는 한 번에 하나의 프로필만 처리합니다. Hello 현재 프로필에도 해당 규칙을 포함 해야,이 즉 tooalso 하려는 경우 하위 계층 프로필에서 처리 조건이 포함 됩니다.

예제를 사용하여 이를 검토해 보겠습니다.

아래 hello 이미지 표시 자동 크기 조정 설정의 최소 인스턴스를 기본 프로필로 = 2 자에서 최대 인스턴스 = 10입니다. 이 예에서 규칙 hello 큐에 hello 메시지 개수 보다 크면 10과 배율에 hello 큐에 hello 메시지 수가 3 보다 작은 경우 구성 된 tooscale 아웃은입니다. 이제 hello 리소스 2 ~ 10 개 사이 인스턴스입니다 확장할 수 있습니다.

또한 월요일에 설정된 되풀이 프로필이 있습니다. 이는 최소 인스턴스 = 2, 최대 인스턴스 = 12에 대해 설정되어 있습니다. 즉, 월요일,이 조건에 대 한 hello 첫 번째 시간 자동 크기 조정 확인 toohello 새 최소 3까지 확장 hello 인스턴스 수가 2 인 경우. 자동 크기 조정 계속 toofind이 프로필 상태가 일치 (월요일), hello CPU 기반 스케일 아웃/인 규칙이이 프로필에 대해 구성 된 처리 합니다. 이때 hello 큐 길이 대 한 확인 하지 않습니다. 그러나 hello 큐 길이 조건 toobe 확인 하려면를 포함 해야 hello 기본 프로필에서 이러한 규칙도 월요일 프로필에서.

마찬가지로, 자동 크기 조정 백 toohello 기본 프로필이 전환 되는 경우 먼저 확인 hello 최소 및 최대 조건이 충족 될 경우. Hello hello 시간에 인스턴스 수가 12 이면 hello 기본 프로필에 대 한 허용 된 최대 hello too10에서 확장 됩니다.

![자동 크기 조정 설정](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>하나의 프로필에 여러 규칙이 구성된 경우 크기 조정에 대한 고려 사항
있는 tooset 여러 규칙 프로 파일에 있습니다. 여러 규칙을 설정 하는 경우 서비스를 사용 하 여 자동 크기 조정 규칙의 집합을 추적 하는 hello 사용 됩니다.

*규모 확장*의 경우 임의의 규칙이 충족되면 자동 크기 조정이 실행됩니다.
*눈금에서*, 자동 크기 조정 toobe 충족 하는 모든 규칙을 필요로 합니다.

tooillustrate, 자동 크기 조정 규칙에 4 hello 있다고 가정 합니다.

* CPU가 30% 미만인 경우 1만큼 규모 감축
* 메모리가 50% 미만인 경우 1만큼 규모 감축
* CPU가 75% 초과인 경우 1만큼 규모 확장
* 메모리가 75%를 초과하는 경우 1만큼 규모 확장

그런 다음 hello에 따라 발생합니다.

* CPU가 76%이고 메모리가 50%인 경우 규모가 확장됩니다.
* CPU가 50%이고 메모리가 76%인 경우 규모가 확장됩니다.

25%가 CPU 및 메모리는 51% 자동 크기 조정을 수행 하는 경우 다른 손에 hello **하지** 배율 기능을 합니다. Tooscale에 순서로 CPU 29% 및 메모리 49% 여야 합니다.

### <a name="always-select-a-safe-default-instance-count"></a>항상 안전한 기본 인스턴스 수 선택
hello 기본 인스턴스 수는 중요 한 메트릭을 사용할 수 없을 때 자동 크기 조정 서비스 toothat 수를 조정 합니다. 따라서 워크로드에 안전한 기본 인스턴스 수를 선택해야 합니다.

### <a name="configure-autoscale-notifications"></a>자동 크기 조정 알림 구성
자동 크기 조정에 게 알리는 hello 관리자 및 참가자 hello 리소스의 전자 메일을 통해 hello 다음 조건 중 하나가 발생 하는 경우:

* 자동 크기 조정 서비스 tootake 작업에 실패합니다.
* 자동 크기 조정 서비스 toomake 배율 의사 결정에 사용할 수 있는 메트릭이 합니다.
* 메트릭을 사용할 수 있는 (복구)은 다시 toomake 배율 의사 결정 합니다.
  또한 위의 toohello 조건 webhook 또는 전자 메일 알림을 tooget 성공적으로 크기 조정 작업에 대 한 알림을 구성할 수 있습니다.
  
Hello 자동 크기 조정 엔진의 작업 로그 경고 toomonitor hello 상태를 사용할 수 있습니다. 다음은 예제 너무[활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업을 만드는](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) 또는 너무[눈금의 자동 크기 조정 하지 못했습니다 모든 /에 작업을 확장 하는 활동 로그 경고 toomonitor 만들기 구독](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)합니다.

## <a name="next-steps"></a>다음 단계
- [활동 로그 경고 toomonitor 구독에 대 한 모든 자동 크기 조정 엔진 작업을 만듭니다.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [활동 로그 경고 toomonitor 눈금의 자동 크기 조정 하지 못했습니다 모든 / 구독에서 작업 확장 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
