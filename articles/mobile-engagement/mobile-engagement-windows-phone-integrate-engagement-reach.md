---
title: "aaaWindows 전화 Silverlight SDK 통합에 도달"
description: "어떻게 tooIntegrate Azure Mobile Engagement는 Windows Phone Silverlight 앱을 도달합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Windows Phone 도달률 Engagement SDK 통합
Hello에 설명 된 hello 통합 절차를 따라야 [Windows Phone Silverlight Engagement SDK 통합](mobile-engagement-windows-phone-integrate-engagement.md) 이 가이드를 수행 하기 전에.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Windows Phone Silverlight 프로젝트에 hello Engagement Reach SDK 포함
아무 것도 않아도 tooadd 합니다. `EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.

> [!TIP]
> Hello에 있는 이미지를 사용자 지정할 수 있습니다 `Resources` 특히 hello 브랜드 아이콘 (해당 기본 toohello Engagement 아이콘) 프로젝트의 폴더입니다.
> 
> 

## <a name="add-hello-capabilities"></a>Hello 기능 추가
hello Engagement Reach SDK에는 일부 유용한 기능이 필요합니다.

열기 프로그램 `WMAppManifest.xml` 파일 및 기능에 따라 해당 hello 선언 해야 합니다.

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

hello 하나는에서 처음 사용할 알림 메시지의 hello MPNS 서비스 tooallow hello 표시 합니다. hello 두 번째 메서드는 사용 되는 tooembed 브라우저 작업 hello SDK 나눕니다.

Hello 편집 `WMAppManifest.xml` hello 내에 추가 하 고 파일 `<Capabilities />` 태그:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Hello Microsoft 푸시 알림 서비스를 사용 하도록 설정
순서 toouse hello에 **Microsoft 푸시 알림 서비스** (MPNS 라고 함)에 `WMAppManifest.xml` 파일 있어야는 `<App />` 사용 하 여 태그는 `Publisher` 특성이 toohello 프로젝트 이름을 설정 합니다.

## <a name="initialize-hello-engagement-reach-sdk"></a>Hello Engagement Reach SDK를 초기화 합니다.
### <a name="engagement-configuration"></a>Engagement 구성
hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.

이 파일 toospecify reach 구성을 편집 합니다.

* *선택적*, 또는 여부를 나타냅니다 (MPNS) hello 네이티브 푸시가 활성화 사이 있지 않음 `<enableNativePush>` 및 `</enableNativePush>` 태그 (`true` 기본적으로).
* *선택적*, 간의 hello 푸시 채널의 hello 이름을 표시 `<channelName>` 및 `</channelName>` hello를 제공 하는 태그를 동일한 응용 프로그램 수 현재 사용 하거나 비워 두세요.

런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> 응용 프로그램의 hello MPNS 푸시 채널의 hello 이름을 지정할 수 있습니다. 기본적으로 Engagement hello appId를 기반으로 이름을 만듭니다. 없는 필요 toospecify hello 이름이 있는, 직접 Engagement 외부 toouse hello 푸시 채널을 계획 하는 경우를 제외 하 고 있습니다.
> 
> 

### <a name="engagement-initialization"></a>Engagement 초기화
Hello 수정 `App.xaml.cs`:

* 추가 tooyour `using` 문:
  
      using Microsoft.Azure.Engagement;
* `Application_Launching`에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* 삽입 `EngagementReach.Instance.OnActivated` hello에 `Application_Activated` 메서드:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> hello `EngagementReach.Instance.Init` 전용된 스레드를 실행 합니다. Toodo 없는 것 직접 합니다.
> 
> 

## <a name="app-store-submission-considerations"></a>앱 스토어 제출 고려 사항
Microsoft hello 푸시 알림을 사용 하는 경우 몇 가지 규칙을 설정 합니다.

Microsoft hello에서 [응용 프로그램 정책] 설명서, 2.9 섹션:

1) Hello 사용자 tooaccept tooreceive 푸시 알림을 요청 해야 합니다. 설정에서 방법을 toodisable hello 푸시 알림을 추가 합니다.

hello EngagementReach 개체 제공 두 메서드 toomanage hello opt-에/옵트아웃을 `EnableNativePush()` 및 `DisableNativePush()`합니다. 수, 예를 들어, 옵션 설정/해제 toodisable 사용 하 여 hello 설정에서 만들거나 MPNS를 사용 하도록 설정 합니다.

Hello Engagement 구성을 통해 MPNS toodeactivate 결정할 수도 있습니다\<windows-phone-sdk-reach-구성\>합니다.

> 2.9.1) hello 응용 프로그램에 제공 하는 hello 알림을 toobe 설명 먼저 해야 및 **(옵트인) hello 사용자의 명시적인 가져올**, 및 **사용자 수신 하지 않을 수 있는 hello를 통해 메커니즘을 제공 해야 푸시 알림**합니다. Hello Microsoft 푸시 알림 서비스를 사용 하 여 제공 하는 모든 알림 hello 설명이 제공 toohello 사용자와 일치 해야 하 고 모두 준수 해야 해당 [응용 프로그램 정책] [ Content Policies]및 [특정 응용 프로그램 종류에 대 한 추가 요구 사항이]합니다.
> 
> 

2) 푸시 알림을 너무 많이 사용해서는 안 됩니다. Engagement는 사용자에 대한 알림을 처리합니다.

> 2.9.2) hello 응용 프로그램 및 해당 Microsoft 푸시 알림 서비스 hello 사용 하지 과도 하 게 사용 해야 네트워크 용량 또는 hello Microsoft 푸시 알림 서비스의 대역폭 하거나 그렇지 않으면 백업용 부담을 Windows Phone 또는 다른 Microsoft 장치 또는 서비스 과도 한와 Microsoft의 합리적 판단에 따른 푸시 알림, 및를 손상 하거나 안 모든 Microsoft 네트워크 또는 서버 또는 모든 제 3 자 서버 또는 네트워크 연결 된 toohello Microsoft 푸시 알림 서비스에 방해가 됩니다.
> 
> 

3) MPNS toosend criticals 정보에 의존 하지 마십시오. Engagement MPNS를 사용 하 여이 규칙 hello Engagement 내에 프런트 엔드 만들어진 hello 캠페인에 대 한도 적용 됩니다.

> 2.9.3) 수명 또는 사망, 제한 중요 한 알림 관련된 tooa 의료 장비 또는 조건을 포함 하 여 중요 한 영향을 줄 수 hello Microsoft 푸시 알림 서비스에는 업무에 중요 해 지거나 다른 방법 사용된 toosend 알림이 되지 않을 수 있습니다. MICROSOFT 명시적으로 부인 ANY 보증은 hello 사용의 hello MICROSOFT 푸시 알림 서비스 또는 배달의 MICROSOFT 푸시 알림 서비스 알림 됩니다 수 중지 되지 않고 오류 무료 tooOCCUR ON A 실시간으로 또는 보장 합니다.
> 
> 

**응용 프로그램은 이러한 권장 사항을 고려 하지 않는 경우 hello 유효성 검사 프로세스를 전달 보장할 수 없습니다.**

## <a name="handle-data-push-optional"></a>데이터 푸시 처리(선택 사항)
응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 원하는 tooimplement 두 이벤트의 hello EngagementReach 클래스 사용 해야 합니다.

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

다음의 hello hello 콘텐츠를 설정 `EngagementReach.Instance.Handler` 필드에 사용자 지정 개체와 프로그램 `App.xaml.cs` hello 내 클래스 `Application_Launching` 메서드.

**샘플 코드:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다. Toocreate 없는 고유한, 이렇게 하면 없는 toooverride 모든 메서드에 합니다. hello 기본 동작은 tooselect hello Engagement 기준 개체입니다.
> 
> 

### <a name="layouts"></a>레이아웃
기본적으로 도달 범위는 hello DLL toodisplay hello 알림과 페이지의 hello 포함 리소스를 사용 합니다.

그러나 결정할 수 있습니다 toouse 고유한 리소스 tooreflect 브랜드 이러한 구성 요소에 있습니다.

재정의할 수 `EngagementReachHandler` 프로그램 하위 클래스 tootell Engagement toouse 메서드 레이아웃이:

**샘플 코드:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> hello `CreateNotification` 메서드에서 null을 반환할 수 있습니다. hello 알림이 표시 되지 않습니다 및 hello reach 캠페인에 삭제 됩니다.
> 
> 

toosimplify 레이아웃 구현에 제공 하 고 코드에 대 한 기초로 사용 될 수 있는 고유한 xaml입니다. Hello Engagement SDK 보관 파일에 있는 (/ src/reach /).

> [!WARNING]
> 동일 hello 정확 하 게 사용 하는 제공 하는 hello 원본입니다. 따라서 toomodify을를 직접 없습니다 toochange hello 네임 스페이스를 제거 하 고 이름을 hello 합니다.
> 
> 

### <a name="notification-position"></a>알림 위치
기본적으로 앱 내 알림이 hello 아래쪽 hello 응용 프로그램의 왼쪽에 표시 됩니다. Hello를 재정의 하 여이 동작을 변경할 수 `GetNotificationPosition` hello 방식의 `EngagementReachHandler` 개체입니다.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Hello를 선택할 수 있으며 현재 `BOTTOM` (기본값) 및 `TOP` 위치입니다.

### <a name="launch-message"></a>시작 메시지
사용자가 시스템 알림 (알림)를 클릭 하면 서비스를 실행 하는 hello 응용 프로그램, 부하 hello 내용의 hello 메시지를 푸시하고 캠페인에 해당 하는 hello에 대 한 hello 페이지를 표시 합니다.

Hello 시작 되지 않도록 (에 따라 네트워크의 속도 hello) hello 페이지의 hello 응용 프로그램 및 hello 표시 사이의 지연 시간이 있습니다.

로드 하는 문제가 tooindicate toohello 사용자, 진행률 표시줄 또는 진행률 표시기 등의 시각적 정보를 제공 해야 합니다. Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.

tooimplement 콜백 hello을 수행 합니다.

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

Hello 콜백에서 설정할 수 있습니다 프로그램 `Application_Launching` 방식의 프로그램 `App.xaml.cs` hello 전에 가급적 파일 `EngagementReach.Instance.Init()` 호출 합니다.

> [!TIP]
> 각 처리기는 UI 스레드 hello에 의해 호출 됩니다. 않아도 tooworry MessageBox 또는 다른 UI 관련를 사용 하는 경우.
> 
> 

[응용 프로그램 정책]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[특정 응용 프로그램 종류에 대 한 추가 요구 사항이]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

