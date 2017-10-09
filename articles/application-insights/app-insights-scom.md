---
title: "Application Insights와 통합 aaaSCOM | Microsoft Docs"
description: "SCOM 사용자인 경우 Application Insights로 성능을 모니터링하고 문제를 진단합니다. 포괄적 대시보드, 스마트 경고, 강력한 진단 도구 및 분석 쿼리."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>SCOM에 대해 Application Insights를 사용하여 응용 프로그램 성능 모니터링
성능을 모니터링 하 고 사용 하 여 hello 성능 문제를 진단할 수 System Center Operations Manager (SCOM) toomanage 서버를 사용 하면 [Azure Application Insights](app-insights-asp-net.md)합니다. Application Insights는 사용자 웹 응용 프로그램에 들어오는 요청과 나가는 REST 및 SQL 호출, 예외 및 로그 추적을 모니터링합니다. 메트릭 차트 및 스마트 경고뿐만 아니라 이 원격 분석을 통한 강력한 진단 검색 및 분석 쿼리가 포함된 대시보드를 제공합니다. 

SCOM 관리 팩을 사용하여 Application Insights 모니터링으로 전환할 수 있습니다.

## <a name="before-you-start"></a>시작하기 전에
다음을 가정합니다.

* SCOM, 익숙한 하 고 사용 하는 SCOM 2012 R2 또는 2016 toomanage IIS 웹 서버.
* 이미 설치한 서버에 Application Insights로 toomonitor 원하는 웹 응용 프로그램입니다.
* 앱 프레임워크 버전은 .NET 4.5 이상입니다.
* 대 한 액세스 tooa 구독이 있는 [Microsoft Azure](https://azure.com) toohello에 서명할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 조직 구독에 있고 Microsoft 계정 tooit를 추가할 수 있습니다.

(hello 개발 팀 hello를 빌드할 수 있습니다 [Application Insights SDK](app-insights-asp-net.md) hello 웹 앱에 있습니다. 이 빌드 시간 계측은 사용자 지정 원격 분석을 작성하는 데 더 많은 유연성을 제공합니다. 그러나 문제가 되지 않습니다: 또는 SDK에서 기본적으로 제공 하는 hello 비 여기에 설명 된 hello 단계를 수행 합니다.)

## <a name="one-time-install-application-insights-management-pack"></a>(한 번) Application Insights 관리 팩 설치
Operations Manager를 실행 하는 hello 컴퓨터:

1. 모든 이전 버전의 hello 관리 팩을 제거 합니다.
   1. Operations Manager에서 관리, 관리 팩을 엽니다. 
   2. Hello 이전 버전을 삭제 합니다.
2. 다운로드 하 여 hello 카탈로그에서 hello 관리 팩을 설치 합니다.
3. Operations Manager를 다시 시작합니다.

## <a name="create-a-management-pack"></a>관리 팩 만들기
1. Operations Manager에서 **작성**, **.NET...with Application Insights**, **모니터링 추가 마법사**를 열고 **.NET...with Application Insights**를 한 번 더 선택합니다.
   
    ![](./media/app-insights-scom/020.png)
2. Hello 구성 후 응용 프로그램 이름입니다. (한 번에 하나의 앱 tooinstrument 있어야 합니다.)
   
    ![](./media/app-insights-scom/030.png)
3. 에 동일한 hello 마법사 페이지를 만들거나 새 관리 팩, 또는 이전에 만든 Application Insights에 대 한 팩을 선택 합니다.
   
     (Application Insights hello [관리 팩](https://technet.microsoft.com/library/cc974491.aspx) 는 인스턴스를 만들고 있는 템플릿입니다. 다시 사용할 수 있습니다 hello 나중 인스턴스 동일 합니다.)

    ![일반 속성 탭 hello에 hello 응용 프로그램의 hello 이름을 입력 합니다. 새로 만들기를 클릭하고 관리 팩의 이름을 입력합니다. 확인을 클릭한 후 다음을 클릭합니다.](./media/app-insights-scom/040.png)

1. 응용 프로그램 하나를 선택 toomonitor 되도록 합니다. 서버에 설치 된 앱 간에 hello 검색 기능을 검색 합니다.
   
    ![어떤 tooMonitor 탭에서 추가, hello 앱 이름의 일부를 입력, 검색, 확인 hello 앱을 선택한 다음 추가 선택 합니다.](./media/app-insights-scom/050.png)
   
    hello 선택적 모니터링 범위 필드 toomonitor hello 앱에서 모든 서버를 표시 하지 않으려는 경우 사용 되는 toospecify 서버 하위 집합을 수 있습니다.
2. Hello 다음 마법사 페이지에서 먼저 tooMicrosoft Azure에서에서 사용자 자격 증명 toosign를 제공 해야 합니다.
   
    이 페이지에서 분석 하 고 표시 hello 원격 분석 데이터 toobe 저장할 hello Application Insights 리소스를 선택 합니다. 
   
   * Hello 응용 프로그램을 개발 하는 동안 Application Insights에 대해 구성 된 경우 기존 리소스를 선택 합니다.
   * 그렇지 않으면 hello 앱에 대 한 라는 새 리소스를 만듭니다. 구성 요소는 앱이 다른 경우 hello의 동일한 시스템에에서 저장 hello 동일한 리소스 그룹, toomake 액세스 toohello 원격 분석 쉽게 toomanage 합니다.
     
     나중에 이러한 설정을 변경할 수 있습니다.
     
     ![Application Insights 설정 탭에서 '로그인'을 클릭하고 Azure에 대한 Microsoft 계정 자격 증명을 제공합니다. 그런 다음 구독, 리소스 그룹 및 리소스를 선택합니다.](./media/app-insights-scom/060.png)
3. 전체 hello 마법사입니다.
   
    ![만들기 클릭](./media/app-insights-scom/070.png)

원하는 toomonitor 각 앱에 대해이 절차를 반복 합니다.

나중에 toochange 설정이 필요 hello 제작 창에서 모니터링 하는 hello의 hello 속성 다시 열어야 합니다.

![작성에서 .NET Application Performance Monitoring with Application Insights를 선택하고 모니터를 선택한 후 속성을 클릭합니다.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>모니터링 확인
모든 서버에서 앱에 대 한 검색을 설치 해야 하는 hello 모니터입니다. Application Insights 상태 모니터 toomonitor hello 응용 프로그램에서는 hello 응용 프로그램을 찾는 구성 합니다. 필요한 경우 먼저 hello 서버에 상태 모니터를 설치 합니다.

발견 hello 응용 프로그램의 인스턴스를 확인할 수 있습니다.

![모니터링에서 Application Insights를 엽니다.](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Application Insights에서 원격 분석 보기
Hello에 [Azure 포털](https://portal.azure.com), 앱에 대 한 toohello 리소스를 검색 합니다. 앱에서 [원격 분석을 보여 주는 차트를 확인](app-insights-dashboards.md) 합니다. (것 하지 않은 표시 hello 기본 페이지에서 아직을 클릭 합니다 라이브 메트릭 스트림을.)

## <a name="next-steps"></a>다음 단계
* [대시보드 설정](app-insights-dashboards.md) toobring 함께 hello 가장 중요 한 차트가 및 다른 응용 프로그램을 모니터링 합니다.
* [매트릭에 대해 알아보기](app-insights-metrics-explorer.md)
* [경고 설정](app-insights-alerts.md)
* [성능 문제 진단](app-insights-detect-triage-diagnose.md)
* [강력한 분석 쿼리](app-insights-analytics.md)
* [가용성 웹 테스트](app-insights-monitor-web-app-availability.md)

