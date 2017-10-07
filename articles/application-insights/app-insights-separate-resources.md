---
title: "aaaSeparating 원격 분석에서 개발, 테스트 및 Azure Application Insights에서 릴리스 | Microsoft Docs"
description: "개발, 테스트 및 프로덕션 스탬프에 대 한 직접 원격 분석 toodifferent 리소스입니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>개발, 테스트 및 프로덕션의 원격 분석 구분

Hello 다음 버전의 웹 응용 프로그램을 개발 하는 hello toomix 않을 [Application Insights](app-insights-overview.md) hello 새 버전과 hello 이미 릴리스 버전에서 원격 분석 합니다. 다양 한 개발에서 송신 hello 원격 분석 tooavoid 혼동 (ikeys) 별도 계측 키를 가진 tooseparate Application Insights 리소스를 준비 합니다. toomake 하는 것이 유용한 tooset hello ikey hello 구성 파일 대신 코드에서 한 단계로 tooanother에서 쉽게 toochange hello 계측 키 버전으로 이동 합니다. 

시스템이 Azure 클라우드 서비스인 경우 [별도의 ikey를 설정하는 다른 방법](app-insights-cloudservices.md)이 있습니다.

## <a name="about-resources-and-instrumentation-keys"></a>리소스 및 계측 키 정보

사용자 웹앱에 대해 Application Insights 모니터링을 설정할 경우 Microsoft Azure에서 Application Insights *리소스*를 만듭니다. Hello 순서 toosee에서 Azure 포털에서에서이 리소스를 열고 응용 프로그램에서 수집 된 hello 원격 분석 분석 합니다. hello 리소스로 식별 되는 *계측 키* (ikey). Application Insights toomonitor 앱 패키지, hello를 설치할 때 구성한 hello 계측 키를 가진 toosend 원격 분석 hello를 알 수 있도록 합니다.

일반적으로 선택할 있습니다 toouse 별도 리소스 또는 공유 하는 단일 리소스 다양 한 시나리오에서:

* 서로 다른 독립적인 응용 프로그램 - 각 앱에 대해 별도의 리소스와 ikey를 사용합니다.
* 여러 구성 요소 또는 한 비즈니스 응용 프로그램-의 역할을 사용 하 여 한 [단일 공유 리소스](app-insights-monitor-multi-role-apps.md) 모든 hello 구성 요소 응용 프로그램에 대 한 합니다. 원격 분석을 필터링 또는 기준 hello cloud_RoleName 속성으로 분할할 수 있습니다.
* 개발, 테스트 및 릴리스-'스탬프' hello 시스템의 버전 또는 프로덕션의 단계에 대 한 ikey와 별도 리소스를 사용합니다.
* A | B 테스트 - 단일 리소스를 사용합니다. TelemetryInitializer tooadd hello variant를 식별 하는 속성 toohello 원격 분석을 만듭니다.


## <a name="dynamic-ikey"></a> 동적 계측 키

hello 구성 파일에 대신 코드에서 설정 프로덕션에서의 단계 간에 이동 하는 hello 코드로 toochange hello ikey 쉽게 toomake 합니다.

초기화 메서드에서 global.aspx.cs ASP.NET 서비스에서 같은 hello 키를 설정 합니다.

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

이 예제에서는 hello ikeys hello 다른 리소스에 대 한 서로 다른 버전의 hello 웹 구성 파일에 배치 됩니다. 교환 hello 웹 구성 파일을-hello 릴리스 스크립트의 일부로 수행할 수 있습니다-됩니다 hello 대상 리소스를 교체 합니다.

### <a name="web-pages"></a>웹 페이지
hello iKey hello에 응용 프로그램의 웹 페이지에는 또한 [hello 빠른 시작 블레이드에서 가져온 스크립트](app-insights-javascript.md)합니다. 를 코딩 대신 해당 문자 그대로 hello 스크립트로 hello 서버 상태를 생성 합니다. 예를 들어, ASP.NET 응용 프로그램에서:

*Razor에서 JavaScript*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>추가 Application Insights 리소스 만들기
원격 분석 tooseparate hello에 대 한 다른 스탬프 (프로덕션/개발/테스트) 또는 다른 응용 프로그램 구성 요소에 대 한 동일한 구성 요소를 다음 갖게 toocreate 새 Application Insights 리소스입니다.

Hello에 [portal.azure.com](https://portal.azure.com), Application Insights 리소스를 추가 합니다.

![새로 만들기, Application Insights 클릭](./media/app-insights-separate-resources/01-new.png)

* **응용 프로그램 종류** hello 개요 블레이드 및에서 사용할 수 있는 hello 속성에 표시 되는 내용에 영향을 줍니다 [메트릭 탐색기](app-insights-metrics-explorer.md)합니다. 응용 프로그램 유형과 보이지 않으면 웹 페이지에 대 한 hello 웹 유형 중 하나를 선택 합니다.
* **리소스 그룹** 은 [액세스 제어](app-insights-resources-roles-access-control.md)와 같은 속성을 관리하기 위한 편의 기능입니다. 개발, 테스트 및 프로덕션 환경에 대 한 별도 리소스 그룹을 사용할 수 있습니다.
* **구독** 은 Azure의 지불 계정입니다.
* **위치** 는 데이터를 보관하는 곳입니다. 현재는 변경할 수 없습니다. 
* **추가 toodashboard** 리소스에 대 한 빠른 액세스 타일 Azure 홈 페이지에 배치 합니다. 

Hello 리소스를 만드는 데 몇 초 정도 걸립니다. 완료되면 알림이 표시 됩니다.

(작성할 수 있습니다는 [PowerShell 스크립트](app-insights-powershell-script-create-resource.md) toocreate 리소스 자동으로.)

### <a name="getting-hello-instrumentation-key"></a>Hello 계측 키 가져오기
hello 계측 키 만든 hello 리소스를 식별 합니다. 

![Essentials, hello 계측 키, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Hello 계측 키가 필요한 응용 프로그램은 데이터의 모든 hello 리소스 toowhich 보냅니다.

## <a name="filter-on-build-number"></a>빌드 번호 필터링
응용 프로그램의 새 버전을 게시 하면 다양 한 빌드에서 toobe 수 tooseparate hello 원격 분석을 합니다.

필터링 할 수 있도록 hello 응용 프로그램 버전 속성을 설정할 수 있습니다 [검색](app-insights-diagnostic-search.md) 및 [메트릭 탐색기](app-insights-metrics-explorer.md) 결과입니다.

![속성 필터링](./media/app-insights-separate-resources/050-filter.png)

Hello 응용 프로그램 버전 속성을 설정할 때의 여러 가지 방법이 있습니다.

* 직접 설정:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* 해당 줄을 래핑하는 [원격 분석 이니셜라이저](app-insights-api-custom-events-metrics.md#defaults) 모든 TelemetryClient 인스턴스 일관성 있게 설정 tooensure 합니다.
* [ASP.NET] set hello 버전 `BuildInfo.config`합니다. hello 웹 모듈이 hello BuildLabel 노드에서 hello 버전을 선택 합니다. 이 파일을 프로젝트에 포함 하 고 tooset hello 항상 복사 속성 솔루션 탐색기에서를 기억 합니다.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] MSBuild에서 BuildInfo.config를 자동으로 생성합니다. toodo이 몇 줄 tooyour 추가 `.csproj` 파일:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    라는 파일을 생성이 *yourProjectName*합니다. BuildInfo.config. hello 게시 프로세스가 tooBuildInfo.config을 바꿉니다.

    Visual Studio에서 빌드 hello 빌드 레이블 자리 표시자 (AutoGen_...)를 포함 합니다. 하지만 MSBuild를 작성할 때이 채워집니다 hello 올바른 버전 번호.

    MSBuild toogenerate 버전 번호 tooallow 집합 hello 버전 같은 `1.0.*` AssemblyReference.cs에서

## <a name="version-and-release-tracking"></a>버전 및 릴리스 추적
tootrack hello 응용 프로그램 버전 확인 `buildinfo.config` Microsoft Build Engine 프로세스에 의해 생성 됩니다. .csproj 파일에서 다음을 추가합니다.  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Hello Application Insights 웹 모듈이 자동으로 추가 hello 빌드 정보에 있을 때 **응용 프로그램 버전** 원격 분석의 속성 tooevery 항목으로 합니다. 수 있는 toofilter 버전에서 수행 하는 경우 [진단 검색](app-insights-diagnostic-search.md), 되거나 있습니다 [메트릭을 탐색](app-insights-metrics-explorer.md)합니다.

그러나 Microsoft Build Engine을 hello 개발자가 아니라 Visual Studio에서 작성 하는 hello에 의해서만 hello 빌드 버전 번호가 생성 되도록 확인 합니다.

### <a name="release-annotations"></a>릴리스 주석
Visual Studio Team Services를 사용 하는 경우 다음을 할 수 있습니다 [주석 표식 가져올](app-insights-annotations.md) 새 버전을 출시 될 때마다 tooyour 차트를 추가 합니다. 다음 이미지는 hello이이 표식을 표시 되는 방식을 보여 줍니다.

![차트의 샘플 릴리스 주석 스크린샷](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>다음 단계

* [여러 역할에 대한 공유 리소스](app-insights-monitor-multi-role-apps.md)
* [원격 분석 이니셜라이저 toodistinguish A 만들기 | B 변형](app-insights-api-filtering-sampling.md#add-properties)
