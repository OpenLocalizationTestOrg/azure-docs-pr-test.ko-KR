---
title: "수동으로 또는 Azure 포털에 자동 크기 조정 인스턴스 수를 aaaScale | Microsoft Docs"
description: "자세한 내용은 방법 tooscale Azure 서비스입니다."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>수동 또는 자동으로 인스턴스 개수 조정
Hello에 [Azure 포털](https://portal.azure.com/), 서비스의 hello 인스턴스 수를 수동으로 설정할 수 있습니다 또는, toohave 자동으로 크기 조정 요청에 따라 매개 변수를 설정할 수 있습니다. 이 일반적으로 참조 tooas *확장할* 또는 *으로 크기를 조정*합니다.

크기 조정 인스턴스 수에 따라, 전에 확장은 영향을 고려해 야 **가격 책정 계층** 더하기 tooinstance 수에서 있습니다. 다른 숫자 코어와 메모리를 가질 수 있습니다 가격대 하 고 hello에 대 한 더 나은 성능을 한 하므로 다른 동일한 인스턴스 수 (변수인 *수직* 또는 *규모 축소*). 이 문서에서는 특히 *규모 감축* 및 *규모 확장*에 대해 설명합니다.

Hello 포털에서 확장할 수 있고 hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931953.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust 수동 또는 자동으로 크기를 조정 합니다.

> [!NOTE]
> 이 문서에서는 설명 어떻게 자동 크기 조정 설정 hello 포털에 toocreate [http://portal.azure.com](http://portal.azure.com)합니다. 이 포털에서 만든 자동 크기 조정 설정을 제공할 수 없습니다 hello 클래식 포털 편집할 ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>수동으로 크기 조정
1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기**, 다음와 같은 tooscale, 사용 하려는 toohello 리소스 탐색는 **앱 서비스 계획**합니다.
2. **설정 > 규모 확장(App Service 계획)**을 클릭합니다.
3. Hello의 hello 위쪽 **배율** 블레이드 hello 서비스의 자동 크기 조정 작업의 기록을 볼 수 있습니다.
   
    ![크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > 자동 크기 조정에 의해 수행되는 작업만 이 차트에 표시됩니다. Hello 인스턴스 수를 수동으로 조정 hello 변경이이 차트에 반영 되지 않습니다.
   > 
   > 
4. Hello 번호를 수동으로 조정할 수 **인스턴스** 슬라이더를 사용 합니다.
5. Hello 클릭 **저장** 명령과 있습니다 수 거의 즉시 toothat 인스턴스 수를 조정 합니다.

## <a name="scaling-based-on-a-pre-set-metric"></a>미리 설정된 메트릭을 기준으로 크기 조정
선택 hello에 원하는 메트릭을 hello hello 메트릭에 따라 tooautomatically 조정 인스턴스 수를 원하는 경우 **하 여 확장할** 드롭다운입니다. 예를 들어 **App Service 계획**의 경우 **CPU 비율**을 기준으로 크기를 조정할 수 있습니다.

1. 메트릭 선택 슬라이더를 얻을 수 및 tooscale 사이의 원하는 텍스트 상자 tooenter hello 인스턴스의 수 있습니다:
   
    ![CPU 비율이 있는 크기 조정 블레이드](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    자동 크기 조정 서비스 또는 부하에 관계 없이 사용자가 설정한 hello 경계를 벗어나는 받아들이지 않습니다.
2. 둘째, hello 메트릭에 대 한 hello 대상 범위를 선택 합니다. 예를 들어, 선택한 **CPU 비율**, 대상을 설정할 수 있습니다는 hello 평균 CPU에 대 한 hello 인스턴스의 모든 서비스에 있습니다. 규모 확장 동작이 발생 하는지에 정의한 hello 최대값을 초과 하는 hello 평균 CPU, hello 평균 CPU가 최소 hello 이하가 될 때마다 눈금의 마찬가지로 수행 됩니다.
3. Hello 클릭 **저장** 명령입니다. 자동 크기 조정에 메트릭에 대 한 hello 인스턴스 범위 및 대상에는 모든 몇 분 toomake를 확인 합니다. 서비스가 추가 트래픽을 받으면 아무 작업도 수행하지 않고 더 많은 인스턴스를 얻을 수 있습니다.

## <a name="scale-based-on-other-metrics"></a>기타 메트릭을 기준으로 크기 조정
이외의 hello에 나타나는 hello 사전 설정에 따라 메트릭 확장할 수 있습니다 **하 여 확장할** 드롭다운을 수도 규모 확장의 복잡 한 집합 및 규칙으로 크기를 조정 합니다.

### <a name="adding-or-changing-a-rule"></a>규칙 추가 또는 변경
1. Hello 선택 **일정 및 성능 규칙이** hello에 **하 여 확장할** 드롭다운: ![성능 규칙](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. 자동 크기 조정을 이전에 설치한 경우에 사용 된 hello 정확한 규칙의 보기를 표시 됩니다.
3. 다른 메트릭 클릭 hello에 따라 tooscale **규칙 추가** 행입니다. 클릭할 수도 있습니다 hello 메트릭에서 기존 행 toochange hello의 이전에 사용 했던 여 tooscale toohello 메트릭을 합니다.
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. 이제 tooscale 하 여 원하는 메트릭이 tooselect을 해야 합니다. 선택 된 메트릭이 있는 경우 몇 가지 tooconsider:
   
   * hello *리소스* 에서 hello 메트릭을 제공 합니다. 일반적으로이 될 hello hello 리소스 조정할 수와 동일 합니다. 그러나 tooscale hello 큐 깊이를 저장 하 여 원하는 hello 리소스는 hello 큐 tooscale 하 여 원하는입니다.
   * hello *메트릭 이름을* 자체입니다.
   * hello *집계 시간* hello 메트릭. 이 컬렉션은 hello를 통해 hello 데이터 결합 되어 감사가 만들어집니다는 어떻게 *기간*합니다.
5. 프로그램 메트릭을 선택한 후 hello 메트릭 및 hello 연산자에 대 한 hello 임계값을 선택할 수 있습니다. 예를 들어 **80%****보다 큼**이라고 설정할 수 있습니다.
6. Hello 동작 선택 tootake 되도록 합니다. 다음과 같은 몇 가지 유형의 작업이 있습니다.
   
   * 증가 또는 감소-이 추가 하거나 hello 제거 **값** 정의한 인스턴스 수
   * 퍼센트 늘리거나-hello 인스턴스 수는 % 변경 됩니다. 예를 들어 hello에서 25를 배치할 수 있습니다 **값** 필드 및 현재 인스턴스 8을 설치한 경우 2는 추가 됩니다.
   * -인스턴스 수가 toohello hello 설정 합니다 너무 늘리거나 **값** 정의 합니다.
7. 마지막으로, 쿨 다운-hello 이전 크기 조정 작업 tooscale 다시 후이 규칙은 대기 시간을 선택할 수 있습니다.
8. 규칙을 구성한 후 **확인**을 누릅니다.
9. 원하는 hello 규칙을 모두 구성 되 면 수 있는지 toohit hello **저장** 명령입니다.

### <a name="scaling-with-multiple-steps"></a>여러 단계로 크기 조정
위의 hello 예제는 매우 기본적인입니다. 그러나 toobe를 지정 하려면 확장 (또는 축소) 하는 방법에 대 한 보다 적극적으로 추가할 수도 있습니다 hello에 대 한 여러 확장 규칙 동일한 메트릭을 합니다. 예를 들어 CPU 비율에 대해 2개의 크기 조정 규칙을 정의할 수 있습니다.

1. CPU 비율이 60%를 초과하는 경우 1개 인스턴스 규모 확장
2. CPU 비율이 85%를 초과하는 경우 3개 인스턴스 규모 확장

![여러 크기 조정 규칙](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

이 추가 규칙을 사용하면 크기 조정 작업 이전에 로드가 85%를 넘는 경우 1개가 아니라 2개의 추가 인스턴스를 얻게 됩니다.

## <a name="scale-based-on-a-schedule"></a>일정을 기준으로 크기 조정
기본적으로 크기 조정 규칙을 만드는 경우 항상 적용됩니다. Hello 프로필 머리글을 클릭할 때를 확인할 수 있습니다.

![프로필](./media/insights-how-to-scale/Insights_Profile.png)

그러나 좋습니다 toohave hello 주말에 보다 hello 하루 또는 hello 일주일 동안 간격 보다 적극적으로. 근무 외 시간에는 서비스를 완전히 종료할 수도 있습니다.

1. toodo이 있으면 hello 프로필 선택 **되풀이** 대신 **항상** hello hello 프로필 tooapply 되도록 시간을 선택 합니다.
2. 예를 들어 toohave hello 주 hello에 적용 되는 프로필 **일** 드롭다운의 선택을 취소 **토요일** 및 **일요일**합니다.
3. toohave hello 주간, set hello 하는 동안 적용 되는 프로필 **시작 시간** toostart에서 원하는 toohello 시간입니다.
   
    ![기본 되풀이](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. **확인**을 클릭합니다.
5. 다음으로, 다른 시간에 tooapply 되도록 tooadd hello 프로필이 필요 합니다. Hello 클릭 **프로필 추가** 행입니다.
    ![근무 외 시간](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. 두 번째 새 프로필에 이름을 지정합니다. 예를 들어 **근무 외 시간**으로 지정할 수 있습니다.
7. 다음 선택 **되풀이** 다시이 시간 동안 원하는 hello 인스턴스 수 범위를 선택 합니다.
8. 기본 프로필 hello로 선택 하는 hello **일** 있으며 hello 프로필 tooapply이 원하는 **시작 시간** hello 하루 동안 합니다.
   
   > [!NOTE]
   > 자동 크기 조정 hello 일광 절약 규칙을 사용 하 여 작은 값에 대 한 **시간대** 선택 합니다. 그러나 일광 절약 시간 hello UTC 오프셋은 hello 기본 표준 시간대 오프셋이 없습니다 hello 일광 절약 UTC 오프셋을 표시 하는 동안 합니다.
   > 
   > 
9. **확인**을 클릭합니다.
10. 이제 해야 tooadd 있습니다 규칙 무엇이 든 tooapply 두 번째 프로필 시 원하는 합니다. 클릭 **규칙 추가**, 및 hello hello 기본 프로필 실행 되 고 있어야 동일한 규칙을 구성할 수 있습니다.
    
    ![규칙 toooff 작업 추가](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. 있는지 toocreate 수평 확장 및 눈금에 대 한 규칙 수를 hello 하는 동안 또는 else 프로필 hello 인스턴스 수만 증가 (하거나 감소 합니다).
12. 끝으로, **저장**을 클릭합니다.

## <a name="next-steps"></a>다음 단계
* [서비스 메트릭스를 모니터링](insights-how-to-customize-monitoring.md) toomake 서비스를 사용 가능 하 고 응답 합니다.
* [모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.
* 작업 이벤트가 발생하거나 메트릭이 임계값을 초과할 때마다 [경고 알림을 수신](insights-receive-alert-notifications.md)합니다.
* [응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.
* [이벤트 및 활동 로그 보기](insights-debugging-with-events.md) toolearn 모든 서비스에 발생 한 것입니다.
* [웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.

