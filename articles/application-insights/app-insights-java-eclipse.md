---
title: "Eclipse에서 Java 통해 Azure Application Insights 시작 aaaGet | Microsoft docs"
description: "Hello Eclipse 플러그 인 tooadd 성능 및 사용량 Application Insights를 사용한 tooyour Java 웹 사이트 모니터링을 사용 하 여"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>Eclipse에서 Java를 사용하여 Application Insights 시작하기
Application Insights SDK hello 사용과 성능을 분석할 수 있도록 Java 웹 응용 프로그램에서 원격 분석을 보냅니다. hello Eclipse Application Insights에 대 한 플러그 인에 자동으로 설치 hello SDK 프로젝트 hello 상자 원격 분석 및 toowrite 사용자 지정 원격 분석을 사용할 수 있는 API에서 얻을 수 있도록 합니다.   

## <a name="prerequisites"></a>필수 조건
현재 Maven 프로젝트와 Eclipse에서 동적 웹 프로젝트에 대 한 hello 플러그 인 작동합니다.
([Application Insights 추가 tooother 유형의 Java 프로젝트][java].)

필요한 사항:

* Oracle JRE 1.6 이상
* 구독 너무[Microsoft Azure](https://azure.microsoft.com/)합니다.
* [Java EE Developers용 Eclipse IDE](http://www.eclipse.org/downloads/), Indigo 이상.
* Windows 7 이상 또는 Windows Server 2008 이상

## <a name="install-hello-sdk-on-eclipse-one-time"></a>Eclipse (한 번)에 hello SDK를 설치 합니다.
하기만 하면 toodo 컴퓨터 마다 한 번씩이 됩니다. 이 단계는 hello SDK tooeach 동적 웹 프로젝트를 추가할 수 있는 도구 키트를 설치 합니다.

1. Eclipse에서 도움말, 새 소프트웨어 설치를 클릭합니다.

    ![도움말, 새 소프트웨어 설치](./media/app-insights-java-eclipse/0-plugin.png)
2. Azure 도구 키트에서 http://dl.microsoft.com/eclipse hello SDK입니다.
3. **모든 업데이트 사이트 문의...**

    ![Application Insights SDK의 경우 모든 업데이트 사이트 문의 지우기](./media/app-insights-java-eclipse/1-plugin.png)

Hello 남아 있는 각 Java 프로젝트에 대 한 단계를 따릅니다.

## <a name="create-an-application-insights-resource-in-azure"></a>Azure에서 Application Insights 리소스 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 새 Application Insights 리소스를 만듭니다. Hello 응용 프로그램 종류 tooJava 웹 응용 프로그램을 설정 합니다.  

    ![+를 클릭하고 Application Insights 선택](./media/app-insights-java-eclipse/01-create.png)  

4. Hello 새 리소스의 계측 키를 hello를 찾습니다. 이것이 필요 합니다 toopaste 코드 프로젝트에 곧 합니다.  

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>Application Insights tooyour 프로젝트 추가
1. Java 웹 프로젝트의 hello 상황에 맞는 메뉴에서 Application Insights를 추가 합니다.

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/02-context-menu.png)
2. Hello Azure 포털에서에서 가져온 hello 계측 키를 붙여 넣습니다.

    ![새 리소스 개요 hello에서에서 속성을 클릭 하 고 hello 계측 키 복사](./media/app-insights-java-eclipse/03-ikey.png)

hello 키 원격 분석의 모든 항목이 함께 전송 되 고 Application Insights toodisplay 지시, 리소스에 해당 합니다.

## <a name="run-hello-application-and-see-metrics"></a>Hello 응용 프로그램을 실행 하 고 메트릭을 확인합니다
응용 프로그램을 실행합니다.

Microsoft Azure에서 tooyour Application Insights 리소스를 반환 합니다.

HTTP 요청 데이터는 hello 개요 블레이드에 표시 됩니다. (없는 경우 몇 초 정도 기다린 다음 새로고침을 클릭합니다.)

![서버 응답, 요청 횟수 및 오류 ](./media/app-insights-java-eclipse/5-results.png)

클릭 하 여 더 자세한 메트릭을 통해 모든 차트 toosee 합니다.

![이름별 요청 수](./media/app-insights-java-eclipse/6-barchart.png)

[메트릭에 대해 자세히 알아봅니다.][metrics]

요청 hello 속성을 볼 때 요청 및 예외와 같은 연관 된 hello 원격 분석 이벤트를 볼 수 있습니다.

![이 요청에 대한 모든 추적](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>클라이언트쪽 원격 분석
Hello 빠른 시작 블레이드에서 Get 코드 toomonitor 내 웹 페이지를 클릭 합니다.

![응용 프로그램 개요 블레이드를 사용 하 여 빠른 시작을 선택에서 내 웹 페이지 코드 toomonitor 가져오기 합니다. Hello 스크립트를 복사 합니다.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

HTML 파일을 hello 헤드에서 hello 코드 조각을 삽입 합니다.

#### <a name="view-client-side-data"></a>클라이언트쪽 데이터 보기
업데이트 된 웹 페이지를 열고 사용 합니다. 를 2 분 정도로 기다립니다 다음 tooApplication Insights 및 열기 hello 사용 블레이드를 반환 합니다. (Hello 개요 블레이드에서 아래로 스크롤하여 사용을 클릭 합니다.)

페이지 보기, 사용자 및 세션 메트릭 hello 사용 블레이드에 표시 됩니다.

![세션, 사용자 및 페이지 보기](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[클라이언트 쪽 원격 분석 설정에 대해 자세히 알아봅니다.][usage]

## <a name="publish-your-application"></a>응용 프로그램 게시
이제 앱 toohello 서버를 게시, 사용자가을 사용 하 고 hello 포털에 표시 하는 hello 원격 분석을 조사할 수 있습니다.

* 방화벽이 허용 응용 프로그램 toosend 원격 분석 toothese 포트 있는지 확인 합니다.

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* Windows 서버에 다음을 설치합니다.

  * [Microsoft Visual C++ 재배포 가능 패키지](http://www.microsoft.com/download/details.aspx?id=40784)

    (이를 통해 성능 카운터를 사용할 수 있게 됩니다.)

## <a name="exceptions-and-request-failures"></a>예외 및 요청 실패
처리되지 않은 예외는 자동으로 수집됩니다.

![](./media/app-insights-java-eclipse/21-exceptions.png)

다른 예외에서 toocollect 데이터를 두 가지 옵션이 있습니다.

* [코드에서 tooTrackException를 호출 하는 insert](app-insights-api-custom-events-metrics.md#trackexception)합니다.
* [서버에 hello Java 에이전트 설치](app-insights-java-agent.md)합니다. Toowatch hello 메서드를 지정 합니다.

## <a name="monitor-method-calls-and-external-dependencies"></a>메서드 호출 및 외부 종속성 모니터링
[Hello Java 에이전트 설치](app-insights-java-agent.md) toolog 지정 내부 메서드 및 타이밍 데이터와 함께 JDBC를 통해 호출 합니다.

## <a name="performance-counters"></a>성능 카운터
개요 블레이드에서 아래로 스크롤하여 클릭 hello **서버** 바둑판식으로 배열입니다. 다양한 성능 카운터가 표시됩니다.

![Tooclick hello 서버 타일 아래로 스크롤](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>성능 카운터 수집 사용자 지정
hello 표준 성능 카운터 집합의 toodisable 컬렉션 hello 코드 hello ApplicationInsights.xml 파일의 hello 루트 노드 아래에서 다음을 추가 합니다.

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>추가 성능 카운터 수집
추가 성능 카운터 toobe 수집된을 지정할 수 있습니다.

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>JMX 카운터 (hello Java 가상 컴퓨터에 의해 노출 됨)

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– hello Application Insights 포털에 표시 된 hello 이름입니다.
* `objectName`– hello JMX 개체 이름입니다.
* `attribute`– hello JMX 개체 이름 toofetch hello 특성
* `type`(선택 사항)-JMX 개체의 특성 유형의 hello:
  * 기본값: int 또는 long과 같은 단순 유형입니다.
  * `composite`: hello 성능 카운터 데이터는 'Attribute.Data' hello 형식으로 되어
  * `tabular`: hello 성능 카운터 데이터는 테이블 행의 hello 형식

#### <a name="windows-performance-counters"></a>Windows 성능 카운터
각 [Windows 성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) 범주의 멤버인 (hello에서 필드는 클래스의 멤버가 동일한 방식으로). 범주는 전역일 수 있으며, 번호 또는 이름이 지정된 인스턴스를 가질 수도 있습니다.

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName hello Application Insights 포털에 표시 된 hello 이름입니다.
* categoryName hello 성능 카운터 범주 (성능 개체)이 성능 카운터와 관련 된 합니다.
* counterName hello 성능 카운터의 hello 이름입니다.
* -instanceName hello hello 성능 카운터 범주 인스턴스 이름, 또는 빈 문자열 ("") hello 범주에는 단일 인스턴스가 포함 된 경우. Hello categoryName 프로세스, and toocollect 원하는 성능 카운터를 hello hello 현재 JVM 프로세스에서 실행 중인 앱을 지정 `"__SELF__"`합니다.

성능 카운터에서가 [메트릭 탐색기][metrics]에서 사용자 지정 메트릭으로 보입니다.

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix 성능 카운터
* [Collectd hello Application Insights 플러그 인 설치](app-insights-java-collectd.md) tooget 다양 한 시스템 및 네트워크 데이터입니다.

## <a name="availability-web-tests"></a>가용성 웹 테스트
Application Insights는 사용자가 정기적으로 toocheck 및 잘 응답에서 웹 사이트를 테스트할 수 있습니다. [tooset][availability], tooclick 가용성 아래로 스크롤합니다.

![아래로 스크롤하여 가용성, 추가 웹 테스트를 차례로 클릭](./media/app-insights-java-eclipse/31-config-web-test.png)

사이트가 다운되는 경우 응답 시간 차트는 물론 이메일 알림을 얻게 됩니다.

![웹 테스트의 예](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[가용성 웹 테스트에 대한 자세히 알아봅니다.][availability]

## <a name="diagnostic-logs"></a>진단 로그
Log4J 또는 Logback을 사용 중인 경우 (v 1.2 또는 v2.0) 추적을 위한 tooApplication Insights 탐색 하 고 검색 하 수를 자동으로 전송 하 여 추적 로그를 사용할 수 있습니다.

[진단 로그에 대해 자세히 알아보기][javalogs]

## <a name="custom-telemetry"></a>사용자 지정 원격 분석
함께 수행 하는 사용자가 out는 Java 웹 응용 프로그램 toofind에 몇 줄의 코드를 넣거나 toohelp 문제를 진단 합니다.

JavaScript 웹 페이지와 hello 서버 쪽 java에서 코드를 삽입할 수 있습니다.

[사용자 지정 원격 분석에 대해 자세히 알아보기][track]

## <a name="next-steps"></a>다음 단계
#### <a name="detect-and-diagnose-issues"></a>문제 감지 및 진단
* [웹 클라이언트 원격 분석 추가] [ usage] hello 웹 클라이언트에서 tooget 성능 원격 분석 합니다.
* [웹 테스트 설정] [ availability] toomake 라이브 및 응답성이 뛰어난 응용 프로그램 없이 계속 합니다.
* [이벤트 및 로그를 검색할] [ diagnostic] toohelp 문제를 진단 합니다.
* [Log4J 또는 Logback 추적 캡처][javalogs]

#### <a name="track-usage"></a>사용 현황 추적
* [웹 클라이언트 원격 분석 추가] [ usage] 뷰와 기본 사용자 메트릭을 toomonitor 페이지입니다.
* [사용자 지정 이벤트 및 메트릭을 추적](app-insights-web-track-usage.md) toolearn 응용 프로그램 사용량, hello 클라이언트와 서버 hello에 모두에 대 한 합니다.

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
