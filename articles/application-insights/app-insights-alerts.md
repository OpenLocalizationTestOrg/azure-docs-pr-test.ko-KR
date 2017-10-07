---
title: "Azure Application Insights에서 경고를 aaaSet | Microsoft Docs"
description: "느린 응답 시간, 예외 및 웹앱의 기타 성능 또는 사용 변경에 대한 알림을 받습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: e160cb173e68fda2e6d97f29da342c46b7ac4f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-alerts-in-application-insights"></a>Application Insights에서 경고 설정
[Azure Application Insights] [ start] 웹 앱의 성능 및 사용 현황 메트릭에서 toochanges 경고할 수 있습니다. 

Application Insights는 라이브 앱에서 모니터링 한 [다양 한 플랫폼] [ platforms] toohelp 성능 문제를 진단 및 사용 패턴을 이해 합니다.

경고의 종류는 세 가지입니다.

* **메트릭 경고**는 메트릭이 응답 시간, 예외 수, CPU 사용량 또는 페이지 보기 등의 임계값을 일정 기간 동안 초과하면 그 사실을 알려 줍니다. 
* [**웹 테스트** ] [ availability] 사이트 hello에서 사용할 수 없는 경우 알려 인터넷 또는 느리게 응답 합니다. [자세한 정보][availability].
* [**예방 진단** ](app-insights-proactive-diagnostics.md) 자동으로 구성 된 toonotify 비정상적인 성능 패턴에 대 한 있습니다.

이 문서에서는 메트릭 경고에 집중합니다.

## <a name="set-a-metric-alert"></a>메트릭 경고 설정
열기 hello 경고 규칙 블레이드 차례로 사용 하 여 hello 단추를 추가합니다. 

![Hello 경고 규칙 블레이드 추가 경고를 선택 합니다. 앱 리소스 toomeasure hello 설정, hello 경고에 대 한 이름을 제공 하 고 메트릭을 선택 합니다.](./media/app-insights-alerts/01-set-metric.png)

* Hello 하기 전에 hello 리소스 다른 속성을 설정 합니다. **"(구성 요소)" hello 리소스 선택** 성능 및 사용 현황 메트릭 tooset 경고를 발생 시킬 경우.
* toohello 경고를 지정 하는 hello 이름은 hello 리소스 그룹 (뿐 아니라 응용 프로그램) 내에서 고유 해야 합니다.
* 묻는 메시지가 tooenter hello 임계값 신중 하 게 toonote hello 단위 수입니다.
* Hello 상자 "전자 메일 소유자..."를 선택 하는 경우 경고는 전자 메일 tooeveryone 액세스 toothis 리소스 그룹을 가진으로 전송 됩니다. 이 사람의 설정 tooexpand 추가할 toohello [리소스 그룹이 나 구독](app-insights-resources-roles-access-control.md) (하지 hello 리소스).
* "추가 전자 메일"을 지정 하면 경고 toothose 개인 이나 그룹 (여부 상자를 선택 하면 hello "... 소유자 메일")를 전송 됩니다. 
* 설정 된 [webhook 주소](../monitoring-and-diagnostics/insights-webhooks-alerts.md) tooalerts 응답 하는 웹 앱을 설정한 경우. Hello 경고가 활성화 될 때와 해결 될 때 호출 됩니다. 그러나 현재 쿼리 매개 변수는 웹후크 속성으로 전달되지 않습니다.
* 사용 하지 않도록 설정할 수 있습니다 또는 사용 hello 경고: hello hello 블레이드 맨 아래에 hello 단추를 참조 하십시오.

*Hello 추가 경고 단추를 나타나지 않습니다.* 

* 조직 계정을 사용 중이신가요? 소유자 또는 참가자 액세스 toothis 응용 프로그램 리소스를 사용할 경우 경고를 설정할 수 있습니다. Hello 액세스 제어 블레이드를 살펴보십시오. [액세스 제어에 대해 자세히 알아보세요][roles].

> [!NOTE]
> 에 hello 경고 블레이드 표시 경고 집합 이미 중임: [예방 진단](app-insights-proactive-failure-diagnostics.md)합니다. 자동 경고 hello 하나의 특정 메트릭, 요청 실패율을 모니터링합니다. Toodisable hello 자동 관리 경고 기능을 결정 하지 않는 한 요청 실패율에서 고유한 경고 tooset 필요 없습니다. 
> 
> 

## <a name="see-your-alerts"></a>경고 보기
알림 상태가 비활성 및 활성 간에 변경될 때 전자 메일이 제공됩니다. 

각 경고의 현재 상태 hello hello 경고 규칙 블레이드에 표시 됩니다.

드롭다운은 최근 활동 hello 경고에 대 한 요약:

![경고 드롭다운](./media/app-insights-alerts/010-alert-drop.png)

상태 변경 기록이 hello는 hello 활동 로그에에서 있습니다.

![Hello 개요 블레이드에 설정, 감사 로그를 클릭](./media/app-insights-alerts/09-alerts.png)

## <a name="how-alerts-work"></a>경고 작동 방식
* 경고에는 "활성화되지 않음", "활성화됨", "해결됨"의 세 가지 상태가 있습니다. 활성화 된 의미 hello가 마지막으로 평가 된 경우 true를 지정 된 조건입니다.
* 경고 상태가 변경되면 알림이 생성됩니다. (Hello 경고 조건이 true를 때가 이미 hello 경고를 만든 경우 발생할 수 있습니다 하지 알림을 hello 조건이 false가 될 때까지.)
* 각 알림에 hello 메일 상자를 선택 하거나 전자 메일 주소를 제공 하는 경우 전자 메일을 생성 합니다. Hello 알림 드롭 다운 목록도 볼 수 있습니다.
* 메트릭이 도착할 때마다 경고가 평가되고 그렇지 않은 경우는 평가되지 않습니다.
* hello 평가 기간을 앞에 오는 hello를 통해 hello 메트릭을 집계 하 고 toohello 임계값 toodetermine hello 새 상태 비교 합니다.
* 사용자가 선택한 hello 기간은 집계 된 메트릭 매길 hello 간격을 지정 합니다. 얼마나 자주 hello 경고가 평가 되는 영향을 주지 않습니다: 메트릭 도착 hello 빈도에 따라 다릅니다.
* 일정 시간 동안 특정 메트릭에 대 한 데이터가 도착 하는 경우 hello 간격, 메트릭 탐색기에서 hello 막대형 경고 평가에 다양 한 효과 있습니다. 메트릭 탐색기에서 데이터가 없는 hello 차트의 샘플링 간격 보다 오랫동안 발생 하는 경우 hello 차트에는 0 값을 표시 됩니다. 하지만 동일한 메트릭이 않습니다 hello에 기반 하 여 경고를 다시 평가 하 고 경고의 상태 그대로 hello 합니다. 
  
    결국 데이터가 도착 하면 hello 차트 백 tooa 0이 아닌 값을 이동 합니다. hello 경고 평가 지정한 hello 기간에 사용할 수 있는 hello 데이터를 기반으로 합니다. 새 데이터 요소가 hello hello 기간에 사용할 수 있는 하나의 hello 이면 hello 집계 기반 있는 것이 아니라 데이터 요소는 합니다.
* 경고는 긴 기간을 설정한 경우에도 경고와 정상 상태 사이에서 자주 깜박거릴 수 있습니다. Hello 메트릭 값 hello 임계값 넘나드는 경우일 수 있습니다. Hello 임계값 중인 임계값 이력 없음: hello 전환 tooalert hello 전환 toohealthy과 같은 값인 hello에서 발생 합니다.

## <a name="what-are-good-alerts-tooset"></a>좋은 경고 tooset 무엇입니까?
응용 프로그램에 따라 다릅니다. toostart, 것이 좋습니다 하지 tooset 너무 많은 수의 메트릭이 있습니다. 앱이 실행 되는 동안 메트릭 차트를 보면 시간을 할애해 tooget 정상적으로 동작 하는 방식에 대 한 느낌 합니다. 이 이렇게 하면 성능의 방법을 tooimprove를 찾을 수 있습니다. 다음 경고 tootell 있습니다 때 설정 hello 메트릭 hello 보통 영역 외부로 이동 됩니다. 

다음은 많은 사람들이 사용하는 경고입니다.

* [브라우저 메트릭][client], 특히 브라우저 **페이지 로드 시간**은 웹 응용 프로그램에 매우 유용합니다. 페이지에 스크립트가 많은 경우 **브라우저 예외**를 확인해야 합니다. 순서 tooget에 이러한 메트릭 및 경고를가지고 있어야 tooset [웹 페이지 모니터링][client]합니다.
* **서버 응답 시간의** 웹 응용 프로그램의 서버 쪽 hello에 대 한 합니다. 높은 요청 속도가 크게 다를 경우에 경고를 설정 뿐만 아니라이 메트릭 toosee 모니터링 하기: 변형 앱 리소스 부족 함을 나타낼 수 있습니다. 
* **서버 예외** -toosee 일부 toodo 사용 해야 하거나 [추가 설정](app-insights-asp-net-exceptions.md)합니다.

[자동 관리 오류 속도 진단](app-insights-proactive-failure-diagnostics.md) 앱 toorequests 오류 코드로 응답 하는 모니터 hello 속도 자동으로 합니다. 

## <a name="automation"></a>Automation
* [경고를 PowerShell tooautomate 설정을 사용 하 여](app-insights-powershell-alerts.md)
* [또한 webhook tooautomate 응답 tooalerts를 사용 하 여](../monitoring-and-diagnostics/insights-webhooks-alerts.md)

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>참고 항목
* [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)
* [경고 설정 자동화](app-insights-powershell-alerts.md)
* [사전 진단](app-insights-proactive-diagnostics.md) 

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[platforms]: app-insights-platforms.md
[roles]: app-insights-resources-roles-access-control.md
[start]: app-insights-overview.md

