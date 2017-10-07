---
title: "aaaWindows 유니버설 앱 Engagement SDK 통합"
description: "어떻게 tooIntegrate Windows 유니버설 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Windows 유니버설 앱 Engagement SDK 통합
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

이 절차에서는 hello 가장 간단한 방법은 tooactivate Engagement의 분석 및 Windows 유니버설 응용 프로그램의 함수 모니터링을 설명 합니다.

단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다. hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) 이후 이 통계는 종속 응용 프로그램입니다.

## <a name="supported-versions"></a>지원되는 버전
hello Mobile Engagement SDK에 대 한 Windows 유니버설 앱 Windows 런타임 및 대상으로 하는 유니버설 Windows 플랫폼 응용 프로그램에 통합할 수만 있습니다.

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10(데스크톱 및 모바일 제품군)

> [!NOTE]
> Windows Phone Silverlight 대상으로 하는 다음이 toohello 참조 [Windows Phone Silverlight 통합 절차](mobile-engagement-windows-phone-integrate-engagement.md)합니다.
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Hello Mobile Engagement 유니버설 앱 SDK를 설치 합니다.
### <a name="all-platforms"></a>모든 플랫폼
Mobile Engagement SDK에 대 한 Windows 유니버설 앱 hello 라는 Nuget 패키지로 사용할 수는 *MicrosoftAzure.MobileEngagement*합니다. Hello Visual Studio Nuget 패키지 관리자에서에서 설치할 수 있습니다.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x 및 Windows Phone 8.1
NuGet hello의 hello SDK 리소스를 자동으로 배포 `Resources` 응용 프로그램 프로젝트의 hello 루트 폴더입니다.

### <a name="windows-10-universal-windows-platform-applications"></a>Windows 10 유니버설 Windows 플랫폼 응용 프로그램
NuGet은 아직 UWP 응용 프로그램의 hello SDK 리소스를 자동으로 배포 하지 않습니다. NuGet에서 리소스 배포 때까지 수동으로 다시 발생 toodo를 사용할 수 있습니다.

1. 파일 탐색기를 엽니다.
2. Toohello 수정할 수 있는 위치를 이동 (**x.x.x** 은 설치 하는 계약의 hello 버전): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. 끌어서 놓기 hello **리소스** hello Visual Studio에서 프로젝트의 파일 탐색기 toohello 루트 폴더입니다.
4. Visual Studio에서 프로젝트를 선택 하 고 hello 활성화 **모두 표시 파일** hello 위에 아이콘 **솔루션 탐색기**합니다.
5. 일부 파일 hello 프로젝트에 포함 되지 않습니다. 에 한 번에 마우스 오른쪽 단추로 클릭 hello tooimport **리소스** 폴더 **프로젝트에서 제외** hello에 다른 마우스 오른쪽 단추로 클릭 한 다음 **리소스** 폴더 **포함 프로젝트에서** toore-hello 전체 폴더를 포함 합니다. Hello에서 모든 파일을 **리소스** 폴더는 이제 프로젝트에 포함 되어 있습니다.

## <a name="add-hello-capabilities"></a>Hello 기능 추가
hello Engagement SDK 순서 toowork에 hello Windows SDK의 일부 기능을 제대로 필요합니다.

열기 프로그램 `Package.appxmanifest` 파일 및 기능에 따라 해당 hello 선언 해야 합니다.

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Hello Engagement SDK를 초기화 합니다.
### <a name="engagement-configuration"></a>Engagement 구성
hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.

이 파일 toospecify를 편집 합니다.

* `<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열

런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.

### <a name="engagement-initialization"></a>Engagement 초기화
새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다. 이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다. 사용 되는 tooinitialize hello Engagement SDK도 됩니다.

Hello 수정 `App.xaml.cs`:

* 추가 tooyour `using` 문:
  
      using Microsoft.Azure.Engagement;
* 모든 호출에 대해 한 번씩 메서드 tooshare hello Engagement 초기화를 정의 합니다.
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* 호출 `InitEngagement` hello에 `OnLaunched` 메서드:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* 다른 응용 프로그램이 나 hello 명령줄 hello 다음 사용자 지정 체계를 사용 하 여 응용 프로그램이 시작 되 면 `OnActivated` 메서드를 호출 합니다. 앱이 활성화 될 때에 tooinitiate hello Engagement SDK가 필요 합니다. toodo 따라서 재정의 `OnActivated` 메서드:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> 강력 하 게 하면 tooadd hello Engagement 초기화를 응용 프로그램의 다른 장소에 좋습니다.
> 
> 

## <a name="basic-reporting"></a>기본 보고
### <a name="recommended-method-overload-your-page-classes"></a>권장 방법: `Page` 클래스 오버로드
Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `Page` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.

방법의 예로 toodo 응용 프로그램의 페이지에 대 한이 있습니다. 할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.

#### <a name="c-source-file"></a>C# 소스 파일
페이지 `.xaml.cs` 파일 수정:

* 추가 tooyour `using` 문:
  
      using Microsoft.Azure.Engagement;
* `Page` 및 `EngagementPage` 교체:

**Engagement 사용 안 함:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Engagement 사용:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> 페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다. 그렇지 않으면 hello 활동 보고 되지 것입니다 (hello `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드).
> 
> 

#### <a name="xaml-file"></a>XAML 파일
페이지 `.xaml` 파일 수정:

* Tooyour 네임 스페이스 선언을 추가 합니다.
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* `Page` 및 `engagement:EngagementPage` 교체:

**Engagement 사용 안 함:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Engagement 사용:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Hello 기본 동작 재정의
기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다. Hello 클래스 hello "페이지" 접미사를 사용 하는 경우 서비스 에서도 제거 됩니다.

Hello 이름에 대 한 toooverride hello 기본 동작을 원하는 경우이 tooyour 코드를 추가 합니다.

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

원하는 tooreport 몇 가지 추가 정보를 작업과이 tooyour 코드를 추가할 수 있습니다.

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.

### <a name="alternate-method-call-startactivity-manually"></a>대체 메서드: 수동으로 `StartActivity()` 호출
처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `Page` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.

Toocall 권장 `StartActivity` 내부의 프로그램 `OnNavigatedTo` 페이지의 메서드.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> 세션을 올바르게 종료해야 합니다.
> 
> hello를 자동으로 호출 하는 Windows 유니버설 SDK hello `EndActivity` hello 응용 프로그램을 닫으면 메서드. 즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드에서이 메서드는 전송 tooEngagement 서버가 현재 사용자에 게 leave hello 응용 프로그램, 이렇게 설정이 하면 모든 응용 프로그램 로그에 영향을 줍니다.
> 
> 

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다. hello Engagement API Engagement의 고급 기능을 모두 toouse 있습니다.

자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)합니다.

## <a name="advanced-configuration"></a>고급 구성
### <a name="disable-automatic-crash-reporting"></a>자동 작동 중단 보고를 사용하지 않도록 설정
Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다. 이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.

> [!WARNING]
> 이 기능은 toodisable을 계획할 경우 처리 되지 않은 충돌, 응용 프로그램에서 발생 한 경우 Engagement hello 크래시 보내지 것입니다 주의 해야 **AND** hello 세션 및 작업을 닫지 것입니다.
> 
> 

방금 toodisable 자동 충돌 보고에 선언한 hello 방식에 따라 구성을 사용자 지정:

#### <a name="from-engagementconfigurationxml-file"></a>`EngagementConfiguration.xml` 파일에서
보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>런타임에 `EngagementConfiguration` 개체에서
보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>버스트 모드
기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다. 더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우는 일반 기본 시간 ("버스트 모드" hello 라는)에서 한 번에 모두 있습니다.

따라서 toodo hello 메서드를 호출 합니다.

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

hello 인수에는 **밀리초**합니다. 언제 든 지 tooreactivate hello 실시간 로깅 하려는 경우만 hello 메서드 hello 0 값 또는 모든 매개 변수 없이 호출 합니다.

hello 버스트 모드 약간 증가 hello 배터리 수명 하지만 영향을 주 hello Engagement 모니터: 모든 세션 및 작업 기간 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 둥근된 toohello 버스트 임계값도 됩니다. toouse 30000 (30 초) 보다 버스트 임계값 것이 좋습니다. Toobe 제한 too300 항목이 저장 된 로그를 인식 해야 합니다. 보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.

> [!WARNING]
> hello 버스트 임계값 1 s 보다 tooa 기간을 구성할 수 없습니다. 따라서 toodo를 시도 하면 hello SDK hello 오류와 함께 추적 표시 되며가 자동으로 다시 toohello 기본 값, 즉, 0을 설정 합니다. 이렇게 하면 hello SDK tooreport hello 로그를 실시간으로 트리거됩니다.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

