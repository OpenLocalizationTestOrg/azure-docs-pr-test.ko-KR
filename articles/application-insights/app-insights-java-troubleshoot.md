---
title: "Java 웹 프로젝트에서 Application Insights 문제 해결"
description: "문제 해결 가이드 - Application Insights를 사용하여 라이브 Java 앱을 모니터링합니다."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Java용 Application Insights 문제 해결과 질문 및 답변
[Java의 Azure Application Insights][java]와 관련된 질문이나 문제가 있나요? 다음은 몇 가지 팁입니다.

## <a name="build-errors"></a>빌드 오류
**Eclipse에서 Maven 또는 Gradle을 통해 Application Insights SDK를 추가할 때 빌드 또는 체크섬 유효성 검사 오류가 표시됩니다.**

* 종속성 <version> 요소가 와일드카드 문자가 포함된 패턴을 사용하는 경우(예: (Maven) `<version>[1.0,)</version>` 또는 (Gradle) `version:'1.0.+'`) `1.0.2`과 같이 특정 버전을 대신 지정해 보세요. 최신 버전은 [릴리스 정보](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) 를 참조하세요.

## <a name="no-data"></a>데이터 없음
**Application Insights를 추가하고 내 앱을 실행했는데 포털에 데이터가 표시되지 않습니다.**

* 잠시 기다린 후 새로 고침을 클릭합니다. 차트는 주기적으로 새로 고쳐지지만 수동으로 새로 고칠 수도 있습니다. 새로 고침 간격은 차트의 시간 범위에 따라 달라집니다.
* ApplicationInsights.xml 파일(프로젝트의 리소스 폴더에 있음)에 계측 키가 정의되어 있는지 확인합니다.
* xml 파일에 `<DisableTelemetry>true</DisableTelemetry>` 노드가 없는지 확인합니다.
* 방화벽에서 dc.services.visualstudio.com으로 나가는 트래픽에 대해 TCP 포트 80 및 443을 열어야 할 수 있습니다. 최신 버전은 [방화벽 예외의 전체 목록](app-insights-ip-addresses.md)
* Microsoft Azure 시작 보드에서 서비스 상태 맵을 살펴보세요. 어떤 경고 표시가 있는 경우 정상으로 돌아갈 때까지 기다린 후 Application Insights 응용 프로그램 블레이드를 닫고 다시 엽니다.
* ApplicationInsights.xml 파일(프로젝트의 리소스 폴더에 있음)의 루트 노드 아래에 `<SDKLogger />` 요소를 추가하여 IDE 콘솔 창에 기록을 켜고 앞에 [Error]가 붙은 항목을 확인합니다.
* 콘솔의 출력 메시지에서 “구성 파일을 찾았습니다.”라는 문을 찾아 ApplicationInsights.xml 파일이 Java SDK에 의해 성공적으로 로드되었음을 확인합니다.
* 구성 파일이 없으면 출력 메시지를 확인하여 구성 파일이 검색되고 있는 위치를 확인하고, ApplicationInsights.xml이 그러한 검색 위치 중 한 위치에 있는지 확인합니다. 일반적으로 구성 파일을 Application Insights SDK JAR 주위에 배치할 수 있습니다. 예: Tomcat에서는 WEB-INF/lib 폴더를 의미합니다.

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>데이터를 보는 데 중지되었습니다.
* [상태 블로그](http://blogs.msdn.com/b/applicationinsights-status/)를 참조하세요.
* 데이터 요소의 월간 할당량에 도달했습니까? 설정/할당량 및 가격을 열어 알아봅니다. 그렇다면 계획을 업그레이드하거나 추가 용량에 대한 비용을 지불할 수 있습니다. [가격 체계](https://azure.microsoft.com/pricing/details/application-insights/)를 참조하세요.

#### <a name="i-dont-see-all-the-data-im-expecting"></a>기대한 모든 데이터가 표시되지 않는 경우
* 할당량 및 가격 책정 블레이드를 열고 [샘플링](app-insights-sampling.md)이 작동하는지 여부를 확인합니다. (100% 전송이란 샘플링을 사용하지 않는다는 의미입니다.) Application Insights 서비스는 앱에서 도착하는 원격 분석의 일부만 허용하도록 설정할 수 있습니다. 이렇게 하면 원격 분석의 월간 할당량 내로 유지하는 데 도움이 됩니다. 

## <a name="no-usage-data"></a>사용 현황 데이터 없음
**요청 및 응답 시간에 대한 데이터는 표시되는데 페이지 보기, 브라우저 또는 사용자 데이터는 표시되지 않습니다.**

서버에서 원격 분석을 보내도록 앱을 설정했습니다. 이제 다음 단계로 [웹 브라우저에서 원격 분석을 보내도록 웹 페이지를 설정][usage]해야 합니다.

또는 클라이언트가 [휴대폰이나 기타 장치][platforms]의 앱인 경우 해당 장치에서 원격 분석을 보낼 수 있습니다. 

동일한 계측 키를 사용하여 클라이언트 및 서버 원격 분석을 둘 다 설정합니다. 데이터가 동일한 Application Insights 리소스에 표시되며, 클라이언트와 서버의 이벤트에 상관 관계를 지정할 수 있습니다.


## <a name="disabling-telemetry"></a>원격 분석 사용 안 함
**원격 분석 수집을 사용하지 않도록 설정하려면 어떻게 해야 하나요?**

코드:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**또는** 

ApplicationInsights.xml(프로젝트의 리소스 폴더에 있음)을 업데이트합니다. 루트 노드 아래에 다음을 추가합니다.

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

XML 메서드를 사용하여 값 변경 시 응용 프로그램을 다시 시작해야 합니다.

## <a name="changing-the-target"></a>대상 변경
**내 프로젝트에서 데이터를 보내는 Azure 리소스를 변경하려면 어떻게 해야 하나요?**

* [새 리소스의 계측 키를 가져옵니다.][java]
* Azure Toolkit for Eclipse를 사용하여 프로젝트에 Application Insights를 추가한 경우 웹 프로젝트를 마우스 오른쪽 단추로 클릭하고**Azure**, **Application Insights 구성**을 차례로 선택한 다음 키를 변경합니다.
* 그렇지 않으면 프로젝트의 리소스 폴더에 있는 ApplicationInsights.xml에서 키를 업데이트합니다.

## <a name="debug-data-from-the-sdk"></a>SDK에서 데이터 디버깅

**SDK가 수행하는 작업을 찾는 방법**

API의 상황에 대한 자세한 정보를 가져오려면 ApplicationInsights.xml 구성 파일의 루트 노드에 `<SDKLogger/>`를 추가합니다.

파일에 출력하도록 로거에 지시할 수도 있습니다.

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Tomcat 서버의 경우 `%temp%\javasdklogs` 또는 `java.io.tmpdir` 아래에서 파일을 찾을 수 있습니다.


## <a name="the-azure-start-screen"></a>Azure 시작 화면
**[Azure Portal](https://portal.azure.com)을 보고 있습니다. 맵에 내 앱에 대한 정보가 표시되나요?**

아니요, 전 세계 Azure 서버의 상태가 표시됩니다.

*Azure 시작 보드(홈 화면)에서 내 앱에 대한 데이터를 찾으려면 어떻게 해야 하나요?*

[Application Insights에 대해 앱을 설정][java]한 경우 찾아보기를 클릭하고 Application Insights를 선택한 다음 앱을 위해 만든 앱 리소스를 선택합니다. 이후에 더 빨리 액세스하기 위해 앱을 시작 보드에 고정할 수 있습니다.

## <a name="intranet-servers"></a>인트라넷 서버
**내 인트라넷의 서버를 모니터링할 수 있나요?**

예, 서버가 공용 인터넷을 통해 Application Insights 포털에 원격 분석을 보낼 수 있는 경우 가능합니다. 

방화벽에서 dc.services.visualstudio.com 및 f5.services.visualstudio.com으로 나가는 트래픽에 대해 TCP 포트 80 및 443을 열어야 할 수 있습니다.

## <a name="data-retention"></a>데이터 보존
**데이터가 포털에 얼마나 오래 보존되나요? 안전한가요?**

[데이터 보존 및 개인 정보][data]를 참조하세요.

## <a name="next-steps"></a>다음 단계
**내 Java 서버 앱에 대해 Application Insights를 설정했습니다. 다른 어떤 작업을 할 수 있나요?**

* [웹 페이지의 가용성 모니터링][availability]
* [웹 페이지 사용 모니터링][usage]
* [장치 앱의 사용 추적 및 문제 진단][platforms]
* [코드를 작성하여 앱의 사용 추적][track]
* [진단 로그 캡처][javalogs]

## <a name="get-help"></a>도움말 보기
* [스택 오버플로](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

