---
title: "aaaWindows 유니버설 앱 SDK 업그레이드 절차"
description: "Azure Mobile Engagement용 Windows 유니버설 앱 SDK 업그레이드 절차"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Windows 유니버설 앱 SDK 업그레이드 절차
통합 한 경우 이미 이전 버전의 서비스 응용 프로그램으로, tooconsider hello hello SDK로 업그레이드 하는 경우 지점 뒤에 있어야 합니다.

여러 버전의 SDK hello 누락 하는 경우 몇 가지 절차 toofollow 있을 수 있습니다. 예를 들어 0.10.1에서 마이그레이션하는 경우 toofirst hello를 따라 있는 too0.11.0 "0.9.0에서 too0.10.1" 프로시저 다음 hello "0.10.1에서 too0.11.0" 프로시저입니다.

## <a name="from-330-too340"></a>3.3.0에서 too3.4.0
### <a name="test-logs"></a>테스트 로그
Hello SDK에서 생성 되는 콘솔 로그 사용/사용 안 함/필터링 될 수 있습니다. toocustomize이, 업데이트 hello 속성 `EngagementAgent.Instance.TestLogEnabled` hello에서 사용할 수 있는 hello 값의 tooone `EngagementTestLogLevel` 열거형 예를 들어:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>리소스
hello Reach 오버레이 향상 되었습니다. Hello SDK NuGet 패키지 리소스의 일부인 것입니다.

Toohello hello SDK의 새 버전을 업그레이드 하는 동안 여부 hello에서 기존 파일의 리소스 폴더를 오버레이 tookeep 할지 여부를 선택할 수 있습니다.

* Hello 이전 오버레이를 작동 하거나 hello를 통합 하는 경우 `WebView` 요소 수동으로 tookeep 기존 파일을 결정할 수, 한 다음 계속 작동 합니다. 
* Tooupdate toohello 새 오버레이 정당한 바꾸기 hello 전체 경우 `overlay` hello SDK 패키지에서 새 hello로 리소스에서 폴더 (UWP 앱: hello 업그레이드 후 hello 새 오버레이 폴더 % USERPROFILE %에서 얻을 수 있습니다\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources)입니다.

> [!WARNING]
> Hello 새 오버레이 사용 하 여 hello 이전 버전에서 적용 된 모든 사용자 지정을 덮어쓰게 됩니다.
> 
> 

## <a name="from-320-too330"></a>3.2.0에서 too3.3.0
### <a name="resources"></a>리소스
이 단계는 사용자 지정된 리소스에만 관련됩니다. Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.

## <a name="from-310-too320"></a>3.1.0에서 too3.2.0
### <a name="resources"></a>리소스
이 단계는 사용자 지정된 리소스에만 관련됩니다. Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.

### <a name="webview-integration"></a>웹 보기 통합을 사용하지 마세요.
몇 가지 향상 된 기능 toomatch 다른 장치 폼 팩터가이 버전에서 도입 되었습니다. Hello webview의 통합 hello 다음 일치 하는지 확인 합니다.

XAML 페이지 ()에서:

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

그리고 연결된 .cs파일에서:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>2.0.0에서 too3.0.0
### <a name="resources"></a>리소스
이 단계는 사용자 지정된 리소스에만 관련됩니다. Toobackup 있는 hello (html, 이미지, 오버레이) SDK에서 제공 하는 hello 리소스를 사용자 지정한 경우 업그레이드 하 고 다시 적용 하기 전에에 사용자 지정 업그레이드 리소스입니다.

## <a name="from-111-too200"></a>1.1.1에서 too2.0.0
hello 다음 설명 방법을 toomigrate SDK 통합 hello Capptain 서비스에서에서 제공한 Capptain SAS Azure Mobile Engagement에서 제공 하는 응용 프로그램에 합니다. 

> [!IMPORTANT]
> Capptain 및 Mobile Engagement는 동일한 서비스 하지 hello 및 아래에 주어진 hello 프로시저 어떻게 toomigrate hello 클라이언트 응용 프로그램을 강조 표시 합니다. Hello 앱에 마이그레이션 hello SDK hello Capptain 서버 toohello Mobile Engagement 서버에서 데이터를 마이그레이션하지 않습니다.
> 
> 

이전 버전에서 마이그레이션하려는 경우 하십시오 hello Capptain 웹 사이트 toomigrate too1.1.1를 먼저 참조 다음 절차를 수행 하는 hello를 적용 합니다.

### <a name="nuget-package"></a>NuGet 패키지
**Capptain.WindowsPhone**을 **MicrosoftAzure.MobileEngagement** Nuget 패키지로 대체합니다.

### <a name="applying-mobile-engagement"></a>Mobile Engagement 적용
hello SDK hello 단어를 사용 하 여 `Engagement`합니다. Tooupdate 프로젝트 toomatch 해야이 변경 합니다.

Toouninstall 현재 Capptain nuget 패키지를 해야합니다. Capptain 리소스 폴더의 모든 변경 내용도 제거됩니다. Tookeep 하려는 경우 해당 파일의 복사본을 확인 합니다.

그 후 hello 새 Microsoft Azure Engagement nuget 패키지를 프로젝트에 설치 합니다. 해당 패키지는 [NuGet 웹 사이트]에서 직접 찾을 수 있습니다. 또는 여기서 인덱스입니다. 프로젝트 참조를 Engagement에서 사용 되는 및 hello 새 Engagement DLL tooyour 추가 하는 모든 리소스 파일에이 작업으로 바꿉니다.

해야 tooclean 프로젝트 참조 Capptain DLL 참조를 삭제 하 여 합니다. 이 적용 하지 않을 경우 hello 버전 Capptain의 충돌 하는 및 오류가 발생 합니다.

Capptain 리소스를 사용자 지정한 경우 이전 파일 내용을 복사한 hello 새 Engagement 파일에 붙여 넣습니다. Xaml 및 cs 파일을 모두 업데이트 toobe 한지 note 하십시오.

이러한 단계가 완료 되 면 hello 새 Engagement 참조에 의해 tooreplace 이전 Capptain 참조가 있습니다.

1. 모든 Capptain 네임 스페이스 업데이트 toobe가 있어야 합니다.
   
    마이그레이션 전:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    마이그레이션 후:
   
        using Microsoft.Azure.Engagement;
2. "Capptain"을 포함하는 모든 Capptain 클래스는 이제 "Engagement"를 포함해야 합니다.
   
    마이그레이션 전:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    마이그레이션 후:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. xaml 파일에서는 Capptain 네임스페이스와 특성도 변경됩니다.
   
    마이그레이션 전:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    마이그레이션 후:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. 오버레이 페이지 변경
   
   > [!IMPORTANT]
   > 오버레이도 변경됩니다. 새 네임스페이스는 `Microsoft.Azure.Engagement.Overlay`입니다. Cs와 xaml 파일에서 사용 되는 toobe를 있습니다. 또한 `CapptainGrid` toobe 라는 `EngagementGrid`, `capptain_notification_content` 및 `capptain_announcement_content` 이름은 `engagement_notification_content` 및 `engagement_announcement_content`합니다.
   > 
   > 
   
    오버레이의 경우 아래 코드는
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    아래와 같이 변경됩니다.
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Hello에 대 한 Capptain 사진 및 HTML 파일 등의 다른 리소스 참고는 또한 있다가 이름이 바뀐된 toouse "계약"입니다.

### <a name="project-declaration"></a>프로젝트 선언
Package.appxmanifest에서 `File Type Associations` 이(가) 다음과 같이 업데이트되었습니다.

* capptain\_도달\_콘텐츠 tooengagement\_도달\_콘텐츠
* capptain\_로그\_tooengagement 파일\_로그\_파일

### <a name="application-id--sdk-key"></a>응용 프로그램 ID/SDK 키
Engagement에서는 연결 문자열을 사용합니다. 응용 프로그램 ID 및 Mobile Engagement와 SDK 키 toospecify 없는, 하기만 하면 toospecify 연결 문자열입니다. EngagementConfiguration 파일에서 연결 문자열을 설정할 수 있습니다.

hello Engagement 구성에서 설정할 수 있습니다 프로그램 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.

이 파일 toospecify를 편집 합니다.

* `<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열

런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.

### <a name="items-name-change"></a>항목 이름 변경
*capptain*이라는 모든 항목은 *engagement*라고 이름을 지정합니다. 마찬가지로 *Capptain* 너무*Engagement*합니다.

일반적으로 사용되는 Capptain 항목의 예제:

* CapptainConfiguration의 이름은 EngagementConfiguration으로 바뀌었습니다.
* CapptainAgent의 이름은 EngagementAgent로 바뀌었습니다.
* CapptainReach의 이름은 EngagementReach로 바뀌었습니다.
* CapptainHttpConfig의 이름은 EngagementHttpConfig로 바뀌었습니다.
* GetCapptainPageName의 이름은 GetEngagementPageName으로 바뀌었습니다.

이와 같이 바뀐 이름은 재정의되는 메서드에도 영향을 줍니다.

