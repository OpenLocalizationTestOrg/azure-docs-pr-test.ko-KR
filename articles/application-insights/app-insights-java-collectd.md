---
title: "Linux-Azure에서 Java 웹 응용 프로그램 성능 aaaMonitor | Microsoft Docs"
description: "Application Insights에 대 한 플러그 인 CollectD hello로 Java 웹 사이트의 응용 프로그램 성능 모니터링을 확장 합니다."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 40c68f45-197a-4624-bf89-541eb7323002
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: f783e8607a83b2b43f67d3a2fc20f100aa2f75ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collectd-linux-performance-metrics-in-application-insights"></a>collectd: Application Insights에서 Linux 성능 메트릭


tooexplore Linux 시스템 성능 메트릭을 [Application Insights](app-insights-overview.md), 설치 [collectd](http://collectd.org/)Application Insights 플러그 인을 함께 합니다. 이 오픈 소스 솔루션은 다양한 시스템 및 네트워크 통계를 수집합니다.

이미 [Application Insights로 Java 웹 서비스를 계측][java]한 경우 일반적으로 collectd를 사용합니다. 더 많은 데이터 toohelp 제공 하면 tooenhance 앱의 성능 문제를 진단 하거나 합니다. 

![예제 차트](./media/app-insights-java-collectd/sample.png)

## <a name="get-your-instrumentation-key"></a>계측 키 가져오기
Hello에 [Microsoft Azure 포털](https://portal.azure.com)개방형 hello [Application Insights](app-insights-overview.md) hello 데이터 tooappear 하려는 리소스입니다. (또는 [새 리소스를 만듭니다](app-insights-create-new-resource.md).)

Hello 리소스를 식별 하는 hello 계측 키의 복사본을 수행 합니다.

![모두 찾아보기 리소스를 연 다음 Essentials 드롭 다운 hello에서 선택 하 고 복사 hello 계측 키](./media/app-insights-java-collectd/02-props.png)

## <a name="install-collectd-and-hello-plug-in"></a>Collectd 및 hello 플러그 인 설치
Linux 서버 컴퓨터에서:

1. [collectd](http://collectd.org/) 5.4.0 버전 또는 그 이상을 설치합니다.
2. Hello 다운로드 [Application Insights collectd 기록기 플러그 인](https://aka.ms/aijavasdk)합니다. Note hello 버전 번호입니다.
3. Hello 플러그 인 JAR 복사로 `/usr/share/collectd/java`합니다.
4. 편집 `/etc/collectd/collectd.conf`:
   * 되도록 [Java 플러그 인 hello](https://collectd.org/wiki/index.php/Plugin:Java) 를 사용할 수 있습니다.
   * Hello JVMArg JAR 다음 hello java.class.path tooinclude hello에 대 한 업데이트 합니다. Hello 버전 번호 toomatch hello 한 다운로드 한 업데이트 합니다.
   * `/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar`
   * 이 코드 조각에서 리소스의 계측 키 hello를 사용 하 여 추가 합니다.

```XML

     LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"
     <Plugin ApplicationInsightsWriter>
        InstrumentationKey "Your key"
     </Plugin>
```

다음은 샘플 구성 파일의 일부입니다.

```XML

    ...
    # collectd plugins
    LoadPlugin cpu
    LoadPlugin disk
    LoadPlugin load
    ...

    # Enable Java Plugin
    LoadPlugin "java"

    # Configure Java Plugin
    <Plugin "java">
      JVMArg "-verbose:jni"
      JVMArg "-Djava.class.path=/usr/share/collectd/java/applicationinsights-collectd-1.0.5.jar:/usr/share/collectd/java/collectd-api.jar"

      # Enabling Application Insights plugin
      LoadPlugin "com.microsoft.applicationinsights.collectd.ApplicationInsightsWriter"

      # Configuring Application Insights plugin
      <Plugin ApplicationInsightsWriter>
        InstrumentationKey "12345678-1234-1234-1234-123456781234"
      </Plugin>

      # Other plugin configurations ...
      ...
    </Plugin>
    ...
```

다른 [collectd 플러그인](https://collectd.org/wiki/index.php/Table_of_Plugins)을 구성하여 다른 원본에서 다양한 데이터를 수집할 수 있습니다.

Collectd tooits에 따라 다시 시작 [수동](https://collectd.org/wiki/index.php/First_steps)합니다.

## <a name="view-hello-data-in-application-insights"></a>Application Insights에서 hello 데이터 보기
Application Insights 리소스를 열고 [메트릭 탐색기 차트를 추가 하 고][metrics], hello 메트릭을 선택 hello 사용자 지정 범주에서 toosee 합니다.

![](./media/app-insights-java-collectd/result.png)

기본적으로 hello 메트릭은 hello 메트릭 수집한 모든 호스트 컴퓨터에서 집계 됩니다. hello 차트 세부 정보 블레이드에서 호스트당 tooview hello 메트릭을 그룹화 켜고 toogroup CollectD 호스트를 선택 합니다.

## <a name="tooexclude-upload-of-specific-statistics"></a>특정 통계의 tooexclude 업로드
기본적으로 hello Application Insights 플러그 인 모든 활성화 hello collectd에 의해 수집 된 모든 hello 데이터 '읽기' 플러그 인을 보냅니다. 

특정 플러그 인 또는 데이터 원본에서 데이터를 tooexclude:

* Hello 구성 파일을 편집 합니다. 
* `<Plugin ApplicationInsightsWriter>`에서 다음과 같은 지시문 줄을 추가 합니다.

| 지시문 | 결과 |
| --- | --- |
| `Exclude disk` |Hello에 의해 수집 된 모든 데이터를 제외 `disk` 플러그 인 |
| `Exclude disk:read,write` |명명 된 hello 원본을 제외 `read` 및 `write` hello에서 `disk` 플러그 인 합니다. |

새 줄을 포함한 별도 지시문입니다.

## <a name="problems"></a>문제가 있습니까?
*데이터 hello 포털에 표시 되지 않습니다.*

* 열기 [검색] [ diagnostic] toosee hello 원시 이벤트 도착 한 경우. 경우에 따라 긴 tooappear 메트릭 탐색기에서 수행 합니다.
* 너무 해야[나가는 데이터에 대 한 방화벽 예외를 설정 합니다.](app-insights-ip-addresses.md)
* Hello Application Insights 플러그 인에서 추적을 설정 합니다. `<Plugin ApplicationInsightsWriter>`에서 이 줄 추가:
  * `SDKLogger true`
* 터미널 열고 보고 하는 모든 문제 collectd toosee 세부 정보 표시 모드로 시작 합니다.
  * `sudo collectd -f`

## <a name="known-issue"></a>알려진 문제

플러그 인 응용 프로그램 통찰력 쓰는 hello 특정 읽기 플러그 인와 호환 되지 않습니다. 일부 플러그 인 경우에 따라 "NaN" hello Application Insights 플러그 인 부동 소수점 숫자를 예상 하는 위치를 보냅니다.

증상: hello collectd 로그 AI::... "를 포함 하는 오류를 보여 줍니다. SyntaxError: 예기치 않은 토큰 N”을 포함하는 오류가 표시됩니다.

해결 방법: hello 문제 쓰기 플러그인에 의해 수집 된 데이터를 제외 합니다. 

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md


