---
title: "Visual Studio에서 Azure Application Insights를 사용한 응용 프로그램 aaaDebug | Microsoft Docs"
description: "디버깅 및 프로덕션 중에 웹앱 성능 분석 및 진단입니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 2059802b-1131-477e-a7b4-5f70fb53f974
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/7/2017
ms.author: bwren
ms.openlocfilehash: 20491fbe4505bf719039e5d1c220b1afec01db25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-applications-with-azure-application-insights-in-visual-studio"></a>Visual Studio에서 Azure Application Insights로 응용 프로그램 디버그
Visual Studio(2015 이상)에서 [Azure Application Insights](app-insights-overview.md)의 원격 분석을 사용하여 디버깅 및 프로덕션의 성능을 분석하고 ASP.NET 웹앱의 문제를 진단할 수 있습니다.

Visual Studio 2017을 사용 하 여 ASP.NET 웹 앱 만들거나 나중 hello Application Insights SDK 이미 있습니다. 아직 그렇게 하지 않은 경우 그렇지 [Application Insights tooyour 앱 추가](app-insights-asp-net.md)합니다.

toomonitor 앱 라이브 프로덕션 환경에서 되었을 때 일반적으로 hello Application Insights 원격 분석에서에서 보면 hello [Azure 포털](https://portal.azure.com), 경고를 설정 하 고 수 있는 강력한 모니터링 도구의 적용 합니다. 하지만 디버깅을 위해 또한을 검색 하 고 Visual Studio에서 원격 분석 hello를 분석 합니다. 프로덕션 사이트에서 한 개발 컴퓨터에서 실행 됨 디버깅에서 Visual Studio tooanalyze 원격 분석을 사용할 수 있습니다. 후자의 경우 hello에에서 hello SDK toosend 원격 분석 toohello Azure 포털을 아직 구성 하지 않은 경우에 디버깅 실행을 분석할 수 있습니다. 

## <a name="run"></a> 프로젝트 디버깅
F5 키를 사용하여 로컬 디버그 모드로 웹앱을 실행합니다. 일부 원격 분석 toogenerate 서로 다른 페이지를 엽니다.

Visual Studio 프로젝트에 Application Insights 모듈 hello에 의해 기록 된 hello 이벤트의 개수를 볼 수 있습니다.

![Visual Studio에서 디버깅 하는 동안 hello Application Insights 단추 표시 됩니다.](./media/app-insights-visual-studio/appinsights-09eventcount.png)

이 단추 toosearch 원격 분석을 클릭 합니다. 

## <a name="application-insights-search"></a>Application Insights 검색
hello Application Insights 검색 창에 기록 된 이벤트를 표시 합니다. (로그인 하면 tooAzure Application Insights를 설정 하는 경우 검색할 수 있습니다 hello Azure 포털의에서 동일한 이벤트 hello.)

![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights 선택 검색](./media/app-insights-visual-studio/34.png)

> [!NOTE] 
> 를 선택 하거나 필터를 선택 취소 한 후에 hello 텍스트 검색 필드의 hello 끝 hello 검색 단추를 클릭 합니다.
>

hello 자유 텍스트 검색 hello 이벤트의 모든 필드에서 작동합니다. 예를 들어; 페이지의 hello URL의 일부 검색 또는 클라이언트 city;와 같은 속성 값을 환영 합니다. 또는 추적 로그에 특정 단어입니다.

모든 이벤트 toosee의 자세한 속성을 클릭 합니다.

요청 tooyour 웹 앱에 대 한 toohello 코드를 통해 클릭 수 있습니다.

![요청 세부 사항에서 toohello 코드를 통해 클릭](./media/app-insights-visual-studio/31.png)

관련된 항목을 열 수도 있습니다 toohelp 실패 한 요청 또는 예외를 진단 합니다.

![요청 세부 사항에서 toorelated 항목 아래로 스크롤하십시오.](./media/app-insights-visual-studio/41.png)

## <a name="view-exceptions-and-failed-requests"></a>예외 및 실패한 요청 보기
Hello 검색 창에 예외 보고서 표시 합니다. (ASP.NET 응용 프로그램의 일부 이전 형식에서는 있는 너무[예외 모니터링 설정](app-insights-asp-net-exceptions.md) hello 프레임 워크에 의해 처리 되는 예외를 toosee.)

예외 tooget 스택 추적을 클릭 합니다. Hello 코드 hello 앱의 Visual Studio에서 열려 있으면 hello 스택 추적 toohello 관련 코드 줄에서 hello 통해 클릭 수 있습니다.

![예외 스택 추적](./media/app-insights-visual-studio/17.png)

## <a name="view-request-and-exception-summaries-in-hello-code"></a>Hello 코드에서 요청 및 예외 요약 확인
코드 렌즈 윗줄 각 처리기 메서드 hello hello 요청 및 지난 24 시간 동안 hello에 Application Insights에 의해 기록 된 예외 수를 볼 수 있습니다.

![예외 스택 추적](./media/app-insights-visual-studio/21.png)

> [!NOTE] 
> 코드 렌즈 데이터를 보여 줍니다 Application Insights만 있으면 [응용 프로그램 원격 분석 toosend toohello Application Insights 포털 구성](app-insights-asp-net.md)합니다.
>

[코드 렌즈의 Application Insights에 대한 자세한 정보](app-insights-visual-studio-codelens.md)

## <a name="trends"></a>추세
추세는 시간이 지남에 따라 앱의 동작 방식을 시각화하는 도구입니다. 

선택 **원격 분석 추세 탐색** hello Application Insights 도구 모음 단추 또는 Application Insights 검색 창에서. 시작 하는 일반적인 쿼리 tooget 5 개 중 하나를 선택 합니다. 원격 분석 유형, 시간 범위 및 기타 속성에 따라 서로 다른 데이터 집합을 분석할 수 있습니다. 

데이터에 잘못 된 부분 toofind hello "보기 유형" 드롭다운 아래 hello 비정상 옵션 중 하나를 선택 합니다. hello 필터링 옵션 hello hello 창 맨 아래에 원격 분석의 특정 하위 집합에서에서 쉽게 toohone 지정.

![추세](./media/app-insights-visual-studio/51.png)

[추세 자세히 알아보기](app-insights-visual-studio-trends.md).

## <a name="local-monitoring"></a>로컬 모니터링
(Visual Studio 2015 업데이트 2)에서 Hello SDK toosend 원격 분석 toohello Application Insights 포털 (있도록 ApplicationInsights.config의 계측 키가) 구성 하지 않은 경우 hello 진단 창 최신 디버깅 세션에서 원격 분석을 표시 합니다. 

이전 버전의 앱을 이미 게시한 경우에 바람직합니다. 디버깅 세션 toobe 프로그램에서 원격 분석 hello 혼합 해 서 사용 hello에 대 한 hello 원격 분석 hello 게시 된 앱에서 Application Insights 포털 되기를 원하지 않습니다.

경우에 유용도 몇 가지 [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md) toohello 포털 원격 분석 보내기 전에 toodebug 되도록 합니다.

* *처음에 완전히 toosend 원격 분석 toohello 포털 Application Insights를 구성 합니다. 하지만 Visual Studio에서만 toosee hello 원격 분석을 이제 좋을 것입니다.*
  
  * Hello 검색 창 설정, 즉 옵션 toosearch 로컬 진단 응용 프로그램 원격 분석 toohello 포털 보낸 경우에 있습니다.
  * 포털 toohello hello 줄 주석 송신할 toostop 원격 분석 `<instrumentationkey>...` ApplicationInsights.config에서 합니다. 준비 toosend 원격 분석 toohello 포털을 다시 했으면 주석 처리를 제거 합니다.


## <a name="next-steps"></a>다음 단계
|  |  |
| --- | --- |
| **[더 많은 데이터 추가](app-insights-asp-net-more.md)**<br/>사용량, 가용성, 종속성, 예외를 모니터링합니다. 로깅 프레임 워크의 추적을 통합합니다. 사용자 지정 원격 분석을 작성합니다. |![Visual studio](./media/app-insights-visual-studio/64.png) |
| **[Hello Application Insights 포털 작업](app-insights-dashboards.md)**<br/>대시보드, 강력한 분석 및 진단 도구, 경고, 응용 프로그램의 라이브 종속성 맵 및 내보낸 원격 분석 데이터를 봅니다. |![Visual studio](./media/app-insights-visual-studio/62.png) |

