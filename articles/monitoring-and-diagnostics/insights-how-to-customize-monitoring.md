---
title: "Microsoft Azure에서 메트릭 aaaOverview | Microsoft Docs"
description: "Azure에서 차트 toocustomize 모니터링 방법에 대해 알아봅니다."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure의 메트릭 개요
모든 Azure 서비스 toomonitor hello 상태, 성능, 가용성 및 서비스의 사용을 허용 하는 주요 메트릭을 추적 합니다. Hello Azure 포털에서에서 이러한 메트릭을 볼 수 있으며 hello를 사용할 수도 있습니다 [REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello 전체 메트릭 집합을 프로그래밍 방식으로 합니다.

일부 서비스에 대 한 모든 메트릭을 순서 toosee에서 진단에 tooturn을 할 수 있습니다. 가상 컴퓨터와 같은 다른 사용자에 대 한 메트릭, 기본 집합이 받아볼 수 있지만 필요한 tooenable hello 일부만 고주파 메트릭. 참조 [모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toolearn 더 합니다.

## <a name="using-monitoring-charts"></a>모니터링 차트 사용
Hello 메트릭 중 하나를 차트 선택한 기간을 통해 합니다.

1. Hello에 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기**, 다음 리소스에 관심이 모니터링 하 고 있습니다.
2. hello **모니터링** 섹션에는 각 Azure 리소스에 대 한 가장 중요 한 메트릭을 hello 포함 되어 있습니다. 예를 들어 웹앱에는 **요청 및 오류**가 있고, 가상 컴퓨터에는 **CPU 비율** 및 **디스크 읽기 및 쓰기**: ![모니터링 렌즈](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)가 있습니다.
3. 모든 차트에서 클릭 하면 hello 하면 표시 됩니다 **메트릭을** 블레이드입니다. Hello 블레이드 뿐만 아니라 toohello 그래프는 hello 메트릭 (예: 평균, 최소 및 최대 선택한 hello 시간 범위 동안) 집계를 표시 하는 테이블입니다. 다음 hello hello 리소스에 대 한 경고 규칙은입니다.
    ![메트릭 블레이드](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. 표시 되는 toocustomize hello 선을 클릭 hello **편집** hello 차트 단추 또는 환영 **차트 편집** hello 메트릭 블레이드 명령을 합니다.
5. Hello 쿼리 편집 블레이드에서 다음 세 가지 작업을 수행할 수 있습니다.
   
   * Hello 시간 범위를 변경 합니다.
   * Hello 모양 사이 전환 막대 및 선
   * 다른 메트릭 ![쿼리 편집](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png) 선택
6. Hello 시간 범위를 변경 하는 것은 다른 범위를 선택 하는 것 처럼 쉽게 (같은 **지난 시간**)를 클릭 하 고 **저장** hello hello 블레이드 맨 아래에 있습니다. 선택할 수도 있습니다 **사용자 지정**, 있습니다 toochoose 얼마 hello를 통해 지난 2 주 동안 발생 합니다. 예를 들어 hello 전체 2 주, 또는 어제부터 1 시간에만 볼 수 있습니다. 다른 hello 텍스트 상자 tooenter 입력 시간입니다.
    ![사용자 지정 시간 범위](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Hello 시간 범위를 아래 채널 있습니다 hello 차트에서 메트릭 tooshow 개수에 관계 없이 선택 합니다.
8. 저장을 클릭하면 해당 리소스에 대해 변경 내용이 저장됩니다. 예를 들어 두 개의 가상 컴퓨터가 있고 하나에 차트를 변경 하는 경우 영향을 주지 않을 hello 다른 합니다.

## <a name="creating-side-by-side-charts"></a>병렬 차트 만들기
Hello 포털에서 강력한 사용자 지정 hello와 원하는 만큼 많은 차트를 추가할 수 있습니다.

1. Hello에 **...**  hello 블레이드 클릭의 hello 위쪽 메뉴 **타일 추가**:  
    ![메뉴 추가](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. 그런 다음, 선택에서에서 선택할 수 차트 hello **갤러리** hello 화면 오른쪽에: ![갤러리](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Hello 메트릭을 보이지 않으면 언제 추가할 수 있습니다 중 hello 메트릭, 기본 설정 및 **편집** 해야 하는 차트 tooshow hello 메트릭을 hello 합니다.

## <a name="monitoring-usage-quotas"></a>사용 할당량 모니터링
대부분의 메트릭은 시간에 따른 추세를 보여 주지만 사용 할당량와 같은 특정 데이터는 임계값을 포함하는 지정 시간 정보입니다.

또한 hello 블레이드의 리소스 할당량에 대 한 사용 할당량을 확인할 수 있습니다.

![사용](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

메트릭을 사용 하 여 hello을 사용할 수와 [REST API](https://msdn.microsoft.com/library/azure/dn931963.aspx) 또는 [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess 사용 할당량의 전체 집합을 프로그래밍 방식으로 hello 합니다.

## <a name="next-steps"></a>다음 단계
* [경고 알림을 수신](insights-receive-alert-notifications.md) 합니다.
* [모니터링을 활성화 및 진단](insights-how-to-use-diagnostics.md) toocollect 고주파 메트릭 서비스에서 자세히 설명 합니다.
* [인스턴스 수를 자동으로 크기 조정](insights-how-to-scale.md) toomake 서비스를 사용 가능 하 고 응답 합니다.
* [응용 프로그램 성능 모니터링](../application-insights/app-insights-azure-web-apps.md) toounderstand 하려면 정확 하 게 코드 작업 수행 방식을 hello 클라우드에서 합니다.
* 사용 하 여 [JavaScript 앱과 웹 페이지에 대 한 Application Insights](../application-insights/app-insights-web-track-usage.md) 웹 페이지를 방문 하는 hello 브라우저에 대 한 tooget 클라이언트 분석 합니다.
* [웹 페이지의 가용성 및 응답성을 모니터링](../application-insights/app-insights-monitor-web-app-availability.md) 합니다.

