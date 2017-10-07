---
title: "Windows 용 Insights 응용 프로그램 서버 및 작업자 역할 aaaAzure | Microsoft Docs"
description: "Hello Application Insights SDK tooyour ASP.NET 응용 프로그램 tooanalyze 사용, 가용성 및 성능에 수동으로 추가 합니다."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>.NET 응용 프로그램에 대한 Application Insights를 수동으로 구성

구성할 수 있습니다 [Application Insights](app-insights-overview.md) toomonitor 다양 한 응용 프로그램 또는 응용 프로그램 역할, 구성 요소 또는 microservices 합니다. 웹앱 및 서비스의 경우 Visual Studio에서 [한 단계 구성](app-insights-asp-net.md)을 제공합니다. 백 엔드 서버 역할 또는 데스크톱 응용 프로그램과 같은 다른 유형의 .NET 응용 프로그램의 경우 Application Insights를 수동으로 구성할 수 있습니다.

![예제 성능 모니터링 차트](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>시작하기 전에

다음 작업을 수행해야 합니다.

* 구독 너무[Microsoft Azure](http://azure.com)합니다. 팀 또는 조직에 Azure 구독이 있으면 hello 소유자 추가할 수 있습니다 tooit를 사용 하 여 프로그램 [Microsoft 계정](http://live.com)합니다.
* Visual Studio 2013 이상.

## <a name="add"></a>1. Application Insights 리소스 선택

hello 'resource' 데이터 수집 되 고 hello Azure 포털에에서 표시 됩니다. Toodecide 여부 필요한 toocreate 한 새 또는 기존 공유 합니다.

### <a name="part-of-a-larger-app-use-existing-resource"></a>더 큰 앱의 일부: 기존 리소스 사용

웹 응용 프로그램-예: 프런트 엔드 웹 응용 프로그램 및 하나 이상의 백 엔드 서비스-여러 구성 요소에 경우 모든 hello 구성 요소 toohello에서 원격 분석을 전송 해야 동일한 리소스입니다. 있도록 toobe 단일 응용 프로그램 지도에 표시 되 고 가능한 tootrace tooanother 하나의 구성 요소에서에서 요청을 확인 합니다.

따라서이 앱의 다른 구성 요소를 이미 모니터링 하는 경우 다음 사용할 hello 동일한 리소스입니다.

Hello에 hello 리소스 열기 [Azure 포털](https://portal.azure.com/)합니다. 

### <a name="self-contained-app-create-a-new-resource"></a>자체 포함된 앱: 새 리소스 만들기

관련 없는 tooother 응용 프로그램 hello 새 앱을 사용 하는 경우 자체 리소스가 되어 있어야 합니다.

Toohello 로그인 [Azure 포털](https://portal.azure.com/), 새 Application Insights 리소스를 만듭니다. ASP.NET hello 응용 프로그램 유형으로 선택 합니다.

![새로 만들기, Application Insights 클릭](./media/app-insights-windows-services/01-new-asp.png)

응용 프로그램 종류의 hello 선택 hello 리소스 블레이드 hello 기본 콘텐츠를 설정합니다.

## <a name="2-copy-hello-instrumentation-key"></a>2. Hello 계측 키 복사
hello 키 hello 리소스를 식별합니다. 순서 toodirect 데이터 toohello 리소스에 SDK, hello에 곧에 설치할 수 있습니다.

![속성을 클릭 hello 키를 선택 하 고 ctrl + C를 누릅니다.](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. 응용 프로그램에서 hello Application Insights 패키지를 설치 합니다.
설치 및 구성 hello Application Insights 패키지에서 작업 하는 hello 플랫폼에 따라 달라 집니다. 

1. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Nuget 패키지 관리**를 선택합니다.
   
    ![Hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Nuget 패키지 관리 선택](./media/app-insights-windows-services/03-nuget.png)
2. Windows server 응용 프로그램의 경우 "Microsoft.ApplicationInsights.WindowsServer" hello Application Insights 패키지 설치
   
    !["Application Insights" 검색](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *버전은?*

    확인 **시험판 포함** tootry 우리의 최신 기능을 선택 합니다. hello 관련 문서 또는 블로그 시험판 버전 해야 할지 여부를 확인 합니다.
    
    *다른 패키지를 사용할 수 있나요?*
   
    예. 원하는 경우 toouse hello API toosend 직접 원격 분석 "Microsoft.ApplicationInsights"를 선택 합니다. hello Windows Server 패키지 hello API와 다양 한 성능 카운터를 수집 및 종속성을 모니터링 하는 등의 다른 패키지를 포함 됩니다. 

### <a name="tooupgrade-toofuture-package-versions"></a>tooupgrade toofuture 패키지 버전
새 버전의 SDK에서 시간 tootime hello 릴리스 했습니다.

tooupgrade tooa [hello 패키지의 새 릴리스](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/)를 NuGet 패키지 관리자를 다시 열고 설치 된 패키지를 필터링 합니다. **Microsoft.ApplicationInsights.WindowsServer**을 선택하고 **업그레이드**를 선택합니다.

모든 사용자 지정 tooApplicationInsights.config를 수행한 경우, 업그레이드 하 고 나중에 변경 내용을 hello 새 버전에 병합 하기 전에 해당 복사본을 저장 합니다.

## <a name="4-send-telemetry"></a>4. 원격 분석 전송
**Hello API 패키지만 설치:**

* 예를 들어에 코드의 hello 계측 키를 설정 `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *키* `";` 
* [Hello API를 사용 하 여 사용자 고유의 원격 분석을 작성](app-insights-api-custom-events-metrics.md#ikey)합니다.

**다른 Application Insights 패키지를 설치한 경우** 사용할 수 있습니다, 원하는 경우 hello.config 파일 tooset hello 계측 키:

* ApplicationInsights.config (있음 hello NuGet을 설치 하 여 추가 된)를 편집 합니다. 이 hello 닫는 태그 바로 앞에 삽입 합니다.
  
    `<InstrumentationKey>`*hello 계측 키를 복사한*`</InstrumentationKey>`
* 솔루션 탐색기에서 ApplicationInsights.config의 hello 속성 너무 설정 되어 있는지 확인**빌드 작업 콘텐츠를 복사 tooOutput 디렉터리 = = 복사**합니다.

너무 원하는 경우 코드에서 유용한 tooset hello 계측 키에는[다양 한 빌드 구성에 대 한 스위치 hello 키](app-insights-separate-resources.md)합니다. 코드에서 hello 키를 설정 하면 없으면 tooset hello에서 `.config` 파일입니다.

## <a name="run"></a> 프로젝트 실행
사용 하 여 hello **F5** toorun 응용 프로그램을 사용해 보세요: 다른 열기 페이지 toogenerate 일부 원격 분석 합니다.

Visual Studio에서 전송 된 hello 이벤트 수가 표시 됩니다.

![Visual Studio에서 이벤트 수](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> 원격 분석 보기
Toohello 반환 [Azure 포털](https://portal.azure.com/) tooyour Application Insights 리소스를 찾습니다.

Hello 개요 차트의 데이터를 찾습니다. 처음에는 요소가 1~2개만 표시됩니다. 예:

![클릭 하 여 toomore 데이터](./media/app-insights-windows-services/12-first-perf.png)

클릭 하 여 더 자세한 메트릭을 통해 모든 차트 toosee 합니다. [메트릭에 대해 자세히 알아봅니다.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>데이터가 없나요?
* 일부 원격 분석을 생성할 수 있도록 각기 다른 페이지를 여는 hello 응용 프로그램을 사용 합니다.
* 열기 hello [검색](app-insights-diagnostic-search.md) 타일을 toosee 개별 이벤트입니다. 경우에 따라 이벤트 hello 메트릭 파이프라인을 통해 약간 더 오래 동안 tooget을 걸립니다.
* 몇 초 정도 기다렸다가 **새로고침**을 클릭합니다. 차트 자체 주기적으로 새로 고쳐집니다, 하지만 일부 데이터 tooshow 기다리는 경우 수동으로 새로 수 있습니다.
* [문제 해결](app-insights-troubleshoot-faq.md)을 참조하세요.

## <a name="publish-your-app"></a>앱 게시
이제 응용 프로그램 tooyour 서버를 배포 하거나 tooAzure 및 조사식 hello 데이터를 누적 합니다.

![Visual Studio toopublish 응용 프로그램 사용](./media/app-insights-windows-services/15-publish.png)

디버그 모드에서 실행 하는 경우 원격 분석 신속히 처리 hello 파이프라인을 통해 초 내에 나타나는 데이터를 찾도록 합니다. 릴리스 구성에서 앱을 배포할 때는 데이터가 더 천천히 누적됩니다.

### <a name="no-data-after-you-publish-tooyour-server"></a>데이터가 없는 tooyour 서버를 게시 한 후?
서버 방화벽에서 나가는 트래픽에 대해 포트를 엽니다. 참조 [이 페이지](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) hello 목록이 필요한 주소에 대 한 

### <a name="trouble-on-your-build-server"></a>빌드 서버에 문제가 있나요?
[이 문제 해결 항목](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild)을 참조하세요.

> [!NOTE]
> 응용 프로그램 원격 분석을 많이 생성, hello 적응 샘플링 모듈 toohello 포털 이벤트의 대표 일부만 전송 하 여 전송 된 hello 볼륨을 자동으로 줄어듭니다. 그러나 이벤트 하는 동일한 요청 선택 하거나 그룹으로 선택 취소 해야 하는 관련된 toohello 관련된 이벤트를 탐색할 수 있도록 합니다. 
> [샘플링에 대해 알아봅니다](app-insights-sampling.md).
> 
> 

## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>다음 단계
* [더 많은 원격 분석 추가](app-insights-asp-net-more.md) tooget hello 응용 프로그램의 전체 360도 보기.

