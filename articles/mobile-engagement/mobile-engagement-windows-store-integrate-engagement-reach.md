---
title: "aaaWindows 유니버설 앱 SDK 통합에 도달"
description: "어떻게 tooIntegrate Azure Mobile Engagement는 Windows 유니버설 앱을 도달합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Windows 유니버설 앱 도달률 SDK 통합
Hello에 설명 된 hello 통합 절차를 따라야 [Windows 유니버설 Engagement SDK 통합](mobile-engagement-windows-store-integrate-engagement.md) 이 가이드를 수행 하기 전에.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Windows 유니버설 프로젝트로 hello Engagement Reach SDK 포함
아무 것도 않아도 tooadd 합니다. `EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.

> [!TIP]
> Hello에 있는 이미지를 사용자 지정할 수 있습니다 `Resources` 특히 hello 브랜드 아이콘 (해당 기본 toohello Engagement 아이콘) 프로젝트의 폴더입니다. 유니버설 앱에서 이동할 수도 있습니다 hello `Resources` 폴더에 해당 콘텐츠 사이의 수 있지만 응용 프로그램, 갖습니다 프로그램 공유 프로젝트 tooshare tookeep hello `Resources\EngagementConfiguration.xml` 종속 플랫폼의 기본 위치에서의 파일.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Hello Windows 알림 서비스를 사용 하도록 설정
### <a name="windows-8x-and-windows-phone-81-only"></a>Windows 8.x 및 Windows Phone 8.1만 해당
순서 toouse hello에 **Windows 알림 서비스** (WNS 라고 함)에서 프로그램 `Package.appxmanifest` 파일 크기가 `Application UI` 클릭 `All Image Assets` hello bot 왼쪽된 상자에 합니다. Hello 상자 오른쪽의 hello에 `Notifications`, 변경 `toast capable` 에서 `(not set)` 너무`(Yes)`합니다.

### <a name="all-platforms"></a>모든 플랫폼
Toosynchronize 앱 tooyour Microsoft 계정과 toohello engagement 플랫폼을 해야합니다. 이 계정을 toocreate 하거나 여러 로그온 [windows 개발자 센터](https://dev.windows.com)합니다. 새 응용 프로그램을 만들고 찾을 있는 후 hello SID 및 비밀 키입니다. Hello engagement 프런트엔드에서의 응용 프로그램 설정에 이동 `native push` 자격 증명을 붙여 넣습니다. 그런 다음 프로젝트를 마우스 오른쪽 단추로 클릭하고 `store` 및 `Associate App with hello Store...`을(를) 선택합니다. 하기만 tooselect hello 응용 프로그램 사용자에 게 작성 toosynchronize 전에 것입니다.

## <a name="initialize-hello-engagement-reach-sdk"></a>Hello Engagement Reach SDK를 초기화 합니다.
Hello 수정 `App.xaml.cs`:

* `InitEngagement` 메서드에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  hello `EngagementReach.Instance.Init` 전용된 스레드를 실행 합니다. Toodo 없는 것 직접 합니다.

> [!NOTE]
> 응용 프로그램에서 푸시 알림을 다른 곳에서 사용 중인 경우 너무 있는[푸시 채널 공유](#push-channel-sharing) Engagement Reach와 합니다.
> 
> 

## <a name="integration"></a>통합
공지 및 설문 조사의 응용 프로그램에서 두 가지 방법으로 tooadd hello Reach 앱 내 배너 및 중간 뷰를 제공 하는 engagement: hello 통합 및 hello 웹 보기 수동 통합 오버레이 사용 합니다. 두 접근 방식을 hello에 결합할 수 없습니다 동일한 페이지.

hello hello 두 통합 중에 선택 이러한 방식으로 요약 될 수 없습니다.

* Hello 에이전트에서에서 페이지를 이미 상속 하는 경우에 hello 오버레이 통합을 선택할 수도 있습니다 `EngagementPage`, 대체 단순히는 `EngagementPage` 하 여 `EngagementPageOverlay` 및 `xmlns:engagement="using:Microsoft.Azure.Engagement"` 여 `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` 페이지에 합니다.
* 선택할 수 있습니다 hello 웹 보기 수동 통합 tooprecisely 위치 hello 도달 UI 페이지 내에서 하려는 경우 또는 tooadd 않도록 다른 상속 수준 tooyour 페이지. 

### <a name="overlay-integration"></a>오버레이 통합
hello Engagement 오버레이 hello UI 요소 toodisplay Reach 캠페인 페이지에 사용 되는 동적으로 추가 합니다. Hello 오버레이 레이아웃에 적합 하지 않는 경우 고려해 야 hello 웹 보기 수동 통합 대신.

.Xaml 파일 변경에 `EngagementPage` 너무 참조`EngagementPageOverlay`

* Tooyour 네임 스페이스 선언을 추가 합니다.
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* `engagement:EngagementPage` 및 `engagement:EngagementPageOverlay` 교체:

**EngagementPage를 사용하는 경우:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**EngagementPageOverlay를 사용하는 경우:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

그런 다음 .cs 파일에서 `EngagementPage` 대신 `EngagementPageOverlay`로 페이지에 태그를 지정하고 `Microsoft.Azure.Engagement.Overlay`를 가져옵니다.

            using Microsoft.Azure.Engagement.Overlay;

* `EngagementPage` 및 `EngagementPageOverlay` 교체:

**EngagementPage를 사용하는 경우:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**EngagementPageOverlay를 사용하는 경우:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


hello Engagement 오버레이 추가 `Grid` 페이지 맨 위에 요소 레이아웃 및 hello 두 구성 `WebView` hello에 대 한 요소 하나 배너와 hello hello 중간 보기에 대 한 다른 하나 있습니다.

Hello에서 직접 hello 오버레이 요소를 사용자 지정할 수 있습니다 `EngagementPageOverlay.cs` 파일입니다.

### <a name="web-views-manual-integration"></a>웹 보기 수동 통합
검색 두 hello에 대 한 페이지 도달 하는 `WebView` 요소 hello 배너와 hello 중간 보기를 표시 합니다. toodo 있는 점은 tooadd만 hello 그 두 `WebView` 요소 위치 페이지에서 다음은 예제:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


이 예제에서는 hello에 `WebView` 요소는 늘어난된 toofit 자동으로 화면 회전 또는 창 크기 변경이 발생 한 경우 다시 크기의 컨테이너입니다.

> [!WARNING]
> 동일한 명명 tookeep hello 반드시 `engagement_notification_content` 및 `engagement_announcement_content` hello에 대 한 `WebView` 요소입니다. 도달률은 요소를 이름으로 식별합니다. 
> 
> 

## <a name="handle-datapush-optional"></a>datapush 처리(선택 사항)
응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 원하는 tooimplement 두 이벤트의 hello EngagementReach 클래스 사용 해야 합니다.

App.xaml.cs hello App() 생성자에 추가 합니다.

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

각 메서드가 반환 되는 부울 값의 해당 hello 콜백에 볼 수 있습니다. 서비스는 hello 데이터 푸시 디스패치 후 피드백 tooits 백 엔드를 보냅니다. Hello 콜백이 false를 반환 하면 hello `exit` 피드백 전송 됩니다. 그렇지 않으면 `action`이(가) 반환됩니다. 콜백이 없는 hello 이벤트에 대 한을 설정 하는 경우 hello `drop` 피드백 tooEngagement 반환 됩니다.

> [!WARNING]
> 데이터 푸시에 대 한 여러 개의 차트 피드백 수 tooreceive engagement이 아닙니다. Tooset 여러 처리기는 이벤트를 하려는 경우에 hello 피드백은 모니터는 toohello 보낸 마지막 트랜잭션이 주의 해야 합니다. 이 경우 tooalways 권장 반환 hello 혼동 피드백 hello 프런트 엔드에 있는 동일한 값 tooavoid 합니다.
> 
> 

## <a name="customize-ui-optional"></a>UI 사용자 지정(선택 사항)
### <a name="first-step"></a>첫 번째 단계
Toocustomize hello reach UI을 허용 합니다.

toodo 따라서 해야 toocreate hello의 서브 클래스 `EngagementReachHandler` 클래스입니다.

**샘플 코드:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

다음의 hello hello 콘텐츠를 설정 `EngagementReach.Instance.Handler` 필드에 사용자 지정 개체와 프로그램 `App.xaml.cs` hello 내 클래스 `App()` 메서드.

**샘플 코드:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다.
> Toocreate 없는 고유한, 이렇게 하면 없는 toooverride 모든 메서드에 합니다. hello 기본 동작은 tooselect hello Engagement 기준 개체입니다.
> 
> 

### <a name="web-view"></a>웹 보기
기본적으로 도달 범위는 hello DLL toodisplay hello 알림과 페이지의 hello 포함 리소스를 사용 합니다.

tooprovide 전체 사용자 지정 가능한 웹 보기만 사용 합니다. Toocustomize 레이아웃을 하려는 경우 재정의 직접 hello 리소스 파일 `EngagementAnnouncement.html` 및 `EngagementNotification.html`합니다. 계약의 모든 코드를 필요한 `<body></body>` toorun 정확 합니다. 그러나 `engagement_webview_area`외부에 태그를 추가할 수 있습니다.

그러나 리소스 toouse를 결정할 수 있습니다.

재정의할 수 `EngagementReachHandler` 메서드 프로그램 하위 클래스 tootell Engagement toouse에 레이아웃, 보험 tooembedded hello engagement 메커니즘 하지만 변수:

**샘플 코드:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


기본적으로 AnnouncementHTML은 `ms-appx-web:///Resources/EngagementAnnouncement.html`입니다. Hello html 파일을 (텍스트 알림, 웹 anoucement 및 설문 조사 알림)는 푸시 메시지의 hello 내용 디자인을 나타냅니다. AnnouncementName은 `engagement_announcement_content`입니다. Xaml 페이지에서 hello webview 디자인의 hello 이름입니다.

NotfificationHTML은 `ms-appx-web:///Resources/EngagementNotification.html`입니다. 푸시 메시지에 대 한 hello 알림을 디자인 hello html 파일을 나타냅니다. NotfificationName은 `engagement_notification_content`입니다. Xaml 페이지에서 hello webview 디자인의 hello 이름입니다.

### <a name="customization"></a>사용자 지정
Engagement 개체를 보존하는 경우 원하는 알림 및 공지 웹 보기를 사용자 지정할 수 있습니다. 웹 보기 개체 설명 하는 세 번-hello xaml에서는 처음으로 hello "setwebview()" 메서드에서.cs 파일에서 시간이 두 번째 및 세 번째 시간 hello html 파일에 주의 해야 합니다.

* Xaml hello 현재 그래픽 레이아웃 webview 구성 요소에 설명합니다.
* .Cs 파일에서 "setwebview()" hello 두 webview (알림, 알림)의 hello 차원 설정한를 정의할 수 있습니다. Hello 응용 프로그램의 크기를 조정할 때 매우 효율적입니다.
* Hello Engagement html 파일에서는 hello webview 콘텐츠, 디자인에 설명 하 고 hello 서로 사이의 요소 위치입니다.

### <a name="launch-message"></a>시작 메시지
사용자가 시스템 알림 (알림)를 클릭 하면 Engagement hello 응용 프로그램을 시작, 부하 hello 내용의 hello 메시지를 푸시하고 hello 해당 캠페인에 대 한 hello 페이지를 표시 합니다.

Hello 시작 되지 않도록 (에 따라 네트워크의 속도 hello) hello 페이지의 hello 응용 프로그램 및 hello 표시 사이의 지연 시간이 있습니다.

로드 하는 문제가 tooindicate toohello 사용자, 진행률 표시줄 또는 진행률 표시기 등의 시각적 정보를 제공 해야 합니다. Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.

"공용 App() {}" App.xaml.cs에서 tooimplement hello 콜백을 추가 합니다.

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Hello 콜백 "공개 App() {}"는 방법을 설정할 수 있습니다 프로그램 `App.xaml.cs` hello 전에 가급적 파일 `EngagementReach.Instance.Init()` 호출 합니다.

> [!TIP]
> 각 처리기는 UI 스레드 hello에 의해 호출 됩니다. 않아도 tooworry MessageBox 또는 다른 UI 관련를 사용 하는 경우.
> 
> 

## <a id="push-channel-sharing"></a> 푸시 채널 공유
경우 푸시 알림을 응용 프로그램에서 다른 용도로 사용 하는 이름을 제공 해야 toouse hello 푸시 채널 hello Engagement SDK의 기능을 공유 합니다. 이 누락 tooavoid 푸시입니다.

* 사용자 고유의 푸시 채널 toohello Engagement Reach 초기화를 제공할 수 있습니다. hello SDK 한 새 요청 하는 대신 사용 합니다.

Hello에 푸시 채널 hello Engagement Reach 초기화 업데이트로 `InitEngagement` hello 메서드에서 `App.xaml.cs` 파일:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* 또는 원하는 경우 tooconsume hello 푸시 채널 hello Reach 초기화 된 후 hello SDK에서 만들어지면 콜백을 Engagement Reach tooget hello 푸시 채널에 설정할 수 있습니다.

콜백은 모든 위치에서 설정 **후** Reach 초기화 hello:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>사용자 지정 체계 팁
사용자 지정 체계 사용법이 제공됩니다. engagement 프런트 엔드 toobe engagement 응용 프로그램에서 사용 되는 다른 종류의 URI 보낼 수 있습니다. `http, ftp, ...` 와(과) 같은 기본 체계는 Windows에서 관리되며 장치에 기본 응용 프로그램이 설치되어 있지 않으면 해당 메시지가 포함된 창이 표시됩니다. 또한 응용 프로그램에 대해 사용자 지정 체계를 사용할 수도 있습니다.

hello 간단한 방법을 tooset 응용 프로그램에서 사용자 지정 체계는 tooopen 프로그램 `Package.appxmanifest` 에서 이동 `Declarations` 패널입니다. 선택 `Protocol` hello 사용 가능한 선언 스크롤 상자 영역을 추가 합니다. Hello 편집 `Name` 필드에 새 프로토콜에 필요한 이름입니다.

이제 toouse이이 프로토콜을 편집 하면 `App.xaml.cs` hello로 `OnActivated` 메서드를도 tooinitialize engagement 여기 유념 하십시오:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

