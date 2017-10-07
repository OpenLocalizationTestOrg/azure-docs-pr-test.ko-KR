---
title: "Azure Application Insights에서 aaaMonitor Docker 응용 프로그램 | Microsoft Docs"
description: "Docker 성능 카운터, 이벤트 및 예외 hello 컨테이너 화 가능한 응용 프로그램에서 원격 분석 hello 함께 Application Insights에 표시할 수 있습니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>Application Insights에서 Docker 응용 프로그램 모니터링
[Docker](https://www.docker.com/) 컨테이너의 수명 주기 이벤트 및 성능 카운터를 Application Insights에서 차트로 표시할 수 있습니다. Hello 설치 [Application Insights](app-insights-overview.md) hello 다른 이미지도로 대 한 호스트에 컨테이너의 이미지 hello 호스트에 대 한 성능 카운터 표시 됩니다.

Docker를 사용하여 모든 종속성이 포함된 경량 컨테이너에 앱을 배포합니다. Docker 엔진을 실행하는 모든 호스트 컴퓨터에서 앱이 실행됩니다.

Hello를 실행 하는 경우 [Application Insights 이미지](https://hub.docker.com/r/microsoft/applicationinsights/) Docker 호스트에 이러한 이점을 얻을 수 있습니다.

* 실행 되는 모든 hello 컨테이너에 대 한 원격 분석 수명 주기-hello 호스트에서 시작, 중지 및 등입니다.
* 모든 hello 컨테이너에 대 한 성능 카운터입니다. CPU, 메모리, 네트워크 사용량 외 다수
* 경우 있습니다 [Java 용 Application Insights SDK를 설치](app-insights-java-live.md) hello hello 컨테이너에서 실행 중인 앱에서이 앱의 모든 hello 원격 분석 hello 컨테이너와 호스트 컴퓨터를 식별 하는 추가 속성이 갖습니다. 예를 들어 둘 이상의 호스트에서 실행되는 앱 인스턴스가 있다면 앱 원격 분석을 호스트별로 쉽게 필터링할 수 있습니다.

![예제](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>Application Insights 리소스 설정
1. 에 로그인 [Microsoft Azure 포털](https://azure.com) hello Application Insights 리소스 앱;에 대 한 열 및 또는 [새로 만들](app-insights-create-new-resource.md)합니다. 
   
    *어떤 리소스를 사용해야 하나요?* 다른 사용자가 호스트에서 실행 중인 hello 앱 개발 된 경우 너무 필요한[새 Application Insights 리소스 만들기](app-insights-create-new-resource.md)합니다. 보고와 분석 hello 원격 분석입니다. ('일반' hello 앱 형식에 대 한 선택.)
   
    Hello 앱의 hello 개발자 인 경우 다음 경험을 있습니다 하지만 [Application Insights SDK 추가](app-insights-java-live.md) 그중에서 tooeach 합니다. 경우 실제로의 모든 구성 요소는 단일 비즈니스 응용 프로그램 모두 toosend 원격 분석 tooone 리소스를 구성할 수 있습니다 하 고이 리소스 toodisplay hello Docker 수명 주기 및 성능 데이터를 사용 합니다. 
   
    세 번째 시나리오는 대부분의 hello 앱을 개발 하지만 사용 하는 별도 리소스 toodisplay 해당 원격 분석입니다. 이 경우 있습니다 것도 원하는 toocreate hello Docker 데이터에 대 한 별도 리소스입니다. 
2. Hello Docker 타일 추가: 선택 **타일 추가**hello Docker 타일 hello 갤러리에서 끌어 놓은 다음 클릭 **수행**합니다. 
   
    ![예제](./media/app-insights-docker/03.png)
3. Hello 클릭 **Essentials** 드롭 다운 및 hello 계측 키를 복사 합니다. 이 tootell hello SDK를 사용 하 여 여기서 toosend 해당 원격 분석 합니다.

    ![예제](./media/app-insights-docker/02-props.png)

브라우저 창을 편리 하므로 계속 하면 다시 돌아오겠습니다 tooit 곧 toolook 원격 분석에서.

## <a name="run-hello-application-insights-monitor-on-your-host"></a>호스트에서 hello Application Insights 모니터 실행
이제를 가져온 위치 toodisplay hello 원격 분석을 수집 하 고 보낼 됩니다는 hello 컨테이너 화 된 앱을 설정할 수 있습니다.

1. Tooyour Docker 호스트를 연결 합니다. 
2. 계측 키를 아래 명령에 넣어 편집하고 실행합니다.
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

Application Insights 이미지는 Docker 호스트당 하나만 필요합니다. 다음 응용 프로그램을 여러 Docker 호스트에 배포 된 경우에 모든 호스트에 hello 명령을 반복 합니다.

## <a name="update-your-app"></a>앱 업데이트
Hello로 응용 프로그램 파일을 계측 하는 경우 [Java 용 Application Insights SDK](app-insights-java-get-started.md), hello hello에서 프로젝트의 hello ApplicationInsights.xml 파일에 다음 줄 추가 `<TelemetryInitializers>` 요소:

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

이 컨테이너와 호스트 id tooevery 원격 분석 항목 응용 프로그램에서 보낸 같은 Docker 정보를 추가 합니다.

## <a name="view-your-telemetry"></a>원격 분석 보기
Hello Azure 포털에서에서 tooyour Application Insights 리소스를 다시 이동 합니다.

Hello Docker 타일을 클릭 합니다.

Docker 엔진에서 실행 되는 기타 컨테이너가 있는 경우에 특히 곧 hello Docker 앱에서 데이터를 표시 됩니다.

다음은 몇 hello 보기를 가져올 수 있습니다.

### <a name="perf-counters-by-host-activity-by-image"></a>호스트별 성능 카운터, 이미지별 활동
![예제](./media/app-insights-docker/10.png)

![예제](./media/app-insights-docker/11.png)

자세한 내용을 보려면 호스트 또는 이미지 이름을 클릭합니다.

toocustomize hello 뷰는 모든 차트, hello 표 머리글을 클릭 또는 추가 차트를 사용 합니다. 

[메트릭 탐색기에 대해 자세히 알아봅니다](app-insights-metrics-explorer.md).

### <a name="docker-container-events"></a>Docker 컨테이너 이벤트
![예제](./media/app-insights-docker/13.png)

tooinvestigate 개별 이벤트를 클릭 하 여 [검색](app-insights-diagnostic-search.md)합니다. 검색 하 고 원하는 toofind hello 이벤트를 필터링 합니다. 모든 이벤트 tooget 자세히를 클릭 합니다.

### <a name="exceptions-by-container-name"></a>컨테이너 이름별 예외
![예제](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Docker 컨텍스트 tooapp 원격 분석 추가
원격 분석 정보와 함께 AI SDK, Docker 컨텍스트를 제공 하도록 향상 hello 응용 프로그램에서 보낸 요청입니다.

![예제](./media/app-insights-docker/16.png)

프로세서 시간 및 사용 가능한 메모리 성능 카운터는 Docker 컨테이너 이름으로 그룹화되고 보강됩니다.

![예제](./media/app-insights-docker/15.png)

## <a name="q--a"></a>질문과 대답
*Docker에서 얻을 수 없는 어떤 기능을 Application Insights가 제공하나요?*

* 컨테이너 및 이미지별로 성능 카운터의 자세한 분석 결과를 제공합니다.
* 하나의 대시보드에서 컨테이너 및 앱 데이터를 통합합니다.
* [원격 분석 내보낼](app-insights-export-telemetry.md) 추가 분석 tooa 데이터베이스, Power BI 또는 다른 대시보드에 대 한 합니다.

*Hello 앱 자체에서 원격 분석 가져오기*

* Hello 응용 프로그램에서 hello Application Insights SDK를 설치 합니다. [Java 웹앱](app-insights-java-get-started.md), [Windows 웹앱](app-insights-asp-net.md)에 대한 방법을 알아봅니다.

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>다음 단계

* [Java용 Application Insights](app-insights-java-get-started.md)
* [Node.js용 Application Insights](app-insights-nodejs.md)
* [ASP.NET용 Application Insights](app-insights-asp-net.md)
