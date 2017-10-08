---
title: "aaaWindows 전화 Silverlight Engagement SDK 통합"
description: "어떻게 tooIntegrate Windows Phone Silverlight 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Windows Phone Silverlight Engagement SDK 통합
> [!div class="op_single_selector"]
> * [Windows 범용](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

이 절차에서는 hello 가장 간단한 방법은 tooactivate Azure Mobile Engagement의 분석 및 Windows Phone Silverlight 응용 프로그램의 함수 모니터링을 설명 합니다.

단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다. hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 Windows Phone Silverlight 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md) 아래) 이후이 통계는 응용 프로그램에 따라 다릅니다.

## <a name="supported-versions"></a>지원되는 버전
hello Windows Silverlight에 대 한 Mobile Engagement SDK 대상으로 응용 프로그램에 통합할 수만 있습니다.

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Windows Phone 8.1 (Silverlight가 아닌) 대상으로 하는 다음이 toohello 참조 [Windows 유니버설 통합 절차](mobile-engagement-windows-store-integrate-engagement.md)합니다.
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Hello Mobile Engagement Silverlight SDK를 설치 합니다.
Windows Silverlight에 대 한 Mobile Engagement SDK hello 라는 Nuget 패키지로 사용할 수는 *MicrosoftAzure.MobileEngagement*합니다. Hello Visual Studio Nuget 패키지 관리자에서에서 설치할 수 있습니다. 

## <a name="add-hello-capabilities"></a>Hello 기능 추가
hello Engagement SDK 순서 toowork에 hello Windows Phone Silverlight SDK의 일부 기능을 제대로 필요합니다.

Open 프로그램 `WMAppManifest.xml` 파일 및 기능에 따라 해당 hello hello에 선언 해야 `Capabilities` 패널:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Hello Engagement SDK를 초기화 합니다.
### <a name="engagement-configuration"></a>Engagement 구성
hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.

이 파일 toospecify를 편집 합니다.

* `<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열

런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.

### <a name="engagement-initialization"></a>Engagement 초기화
새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다. 이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다. 사용 되는 tooinitialize hello Engagement SDK도 됩니다.

Hello 수정 `App.xaml.cs`:

* 추가 tooyour `using` 문:
  
      using Microsoft.Azure.Engagement;
* 삽입 `EngagementAgent.Instance.Init` hello에 `Application_Launching` 메서드:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* 삽입 `EngagementAgent.Instance.OnActivated` hello에 `Application_Activated` 메서드:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> 강력 하 게 하면 tooadd hello Engagement 초기화를 응용 프로그램의 다른 장소에 좋습니다. 그러나 해당 hello `EngagementAgent.Instance.Init` hello UI 스레드가 아닌는 전용된 스레드와 메서드를 실행 합니다.
> 
> 

## <a name="basic-reporting"></a>기본 보고
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>권장 방법: `PhoneApplicationPage` 클래스 오버로드
Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `PhoneApplicationPage` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.

방법의 예로 toodo 응용 프로그램의 페이지에 대 한이 있습니다. 할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.

#### <a name="c-source-file"></a>C# 소스 파일
페이지 `.xaml.cs` 파일을 수정합니다.

* 추가 tooyour `using` 문:
  
      using Microsoft.Azure.Engagement;
* `PhoneApplicationPage`을(를) `EngagementPage`(으)로 바꿉니다.

**Engagement 사용 안 함:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Engagement 사용:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> 페이지 hello에서 상속 하는 경우 `OnNavigatedTo` 메서드를 신중 하 게 toolet hello 수 `base.OnNavigatedTo(e)` 호출 합니다. 그렇지 않으면 hello 활동 보고 되지 않습니다. 실제로, hello `EngagementPage` 호출 하는 중 `StartActivity` hello 내 `OnNavigatedTo` 메서드.
> 
> 

#### <a name="xaml-file"></a>XAML 파일
페이지 `.xaml` 파일을 수정합니다.

* Tooyour 네임 스페이스 선언을 추가 합니다.
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* `phone:PhoneApplicationPage`을(를) `engagement:EngagementPage`(으)로 바꿉니다.

**Engagement 사용 안 함:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Engagement 사용:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Hello 기본 동작 재정의
기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다. Hello 클래스 hello "페이지" 접미사를 사용 하는 경우 서비스 에서도 제거 됩니다.

Hello 이름에 대 한 toooverride hello 기본 동작을 수행 하는 경우이 tooyour 코드를 추가 합니다.

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

원하는 tooreport 추가적인 정보를 작업과이 tooyour 코드를 추가할 수 있습니다.

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.

### <a name="alternate-method-call-startactivity-manually"></a>대체 메서드: 수동으로 `StartActivity()` 호출
처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `PhoneApplicationPage` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.

PhoneApplicationPage 페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출하는 것이 좋습니다.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> 세션을 올바르게 종료해야 합니다.
> 
> hello를 자동으로 호출 하는 hello SDK `EndActivity` hello 응용 프로그램을 닫으면 메서드. 즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드. 이 메서드는 현재 사용자 hello 남아 서 hello 응용 프로그램 및 모든 응용 프로그램 로그에 영향을 주는 메시지 toohello Engagement 서버를 보냅니다.
> 
> 

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다. hello Engagement API Engagement의 고급 기능을 모두 toouse 있습니다.

자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 Windows Phone Silverlight 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)합니다.

## <a name="advanced-configuration"></a>고급 구성
### <a name="disable-automatic-crash-reporting"></a>자동 작동 중단 보고를 사용하지 않도록 설정
Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다. 이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.

> [!WARNING]
> 이 기능은 toodisable을 계획할 경우 처리 되지 않은 충돌, 응용 프로그램에서 발생 한 경우 Engagement hello 크래시 보내지 것입니다 주의 해야 **AND** hello 세션 및 작업 닫히지 것입니다.
> 
> 

방금 toodisable 자동 충돌 보고에 선언한 hello 방식에 따라 구성을 사용자 지정:

#### <a name="from-engagementconfigurationxml-file"></a>`EngagementConfiguration.xml` 파일에서
보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>런타임에 `EngagementConfiguration` 개체에서
보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>버스트 모드
기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다. 더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우는 일반 기본 시간 ("버스트 모드" hello 라는)에서 한 번에 모두 있습니다.

따라서 toodo hello 메서드를 호출 합니다.

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

hello 인수에는 **밀리초**합니다. 언제 든 지 tooreactivate hello 실시간 로깅 하려는 경우만 hello 메서드 hello 0 값 또는 모든 매개 변수 없이 호출 합니다.

hello 버스트 모드 약간 증가 hello 배터리 수명 하지만 영향을 주 hello Engagement 모니터: 모든 세션 및 작업 기간 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 둥근된 toohello 버스트 임계값도 됩니다. toouse 30000 (30 초) 보다 버스트 임계값 것이 좋습니다. Toobe 제한 too300 항목이 저장 된 로그를 인식 해야 합니다. 보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.

> [!WARNING]
> hello 버스트 임계값을 구성할 수 없습니다 tooa 기간이 더 적은 보다 1 초입니다. Hello SDK hello 오류와 함께 추적 표시 되며가 자동으로 toohello 기본값 다시 설정 하므로 toodo를 시도 하면, 즉 0 초입니다. 이렇게 하면 hello SDK tooreport hello 로그를 실시간으로 트리거됩니다.
> 
> 

