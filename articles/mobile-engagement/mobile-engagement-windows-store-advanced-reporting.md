---
title: "aaaWindows MobileApps Engagement와 유니버설 고급 보고"
description: "어떻게 tooIntegrate Windows 유니버설 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Hello Windows 유니버설 앱 Engagement SDK와의 고급 보고
> [!div class="op_single_selector"]
> * [유니버설 Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

이 항목에서는 Windows 유니버설 응용 프로그램에서 추가 보고 시나리오를 설명합니다. 이러한 시나리오 tooapply toohello hello에서 만든 응용 프로그램을 선택할 수 있는 옵션을 포함할 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서입니다.

## <a name="prerequisites"></a>필수 조건
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

이 자습서를 시작 하기 전에 먼저 완료 해야 hello [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서는 의도적으로 직접와 단순입니다. 이 자습서에서는 선택할 수 있는 추가 옵션에 관해 설명합니다.

## <a name="specifying-engagement-configuration-at-runtime"></a>런타임에 Engagement 구성 지정
hello에 hello Engagement 구성 한 곳에서 `Resources\EngagementConfiguration.xml` hello에 지정 된 위치는 프로젝트의 파일 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 항목입니다.

런타임 시 지정할 수도 있지만: hello 다음 hello Engagement 에이전트를 초기화 하기 전에 메서드를 호출할 수 있습니다.

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>권장 방법: `Page` 클래스 오버로드
모든 확인 Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 tooactivate hello 보고 프로그램 `Page` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.

아래에는 응용 프로그램 페이지에 대한 예제가 나와 있습니다. 할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.

### <a name="c-source-file"></a>C# 소스 파일
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
> 페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다. 그렇지 않으면 hello 활동 보고 되지 않습니다 (hello `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드).
> 
> 

### <a name="xaml-file"></a>XAML 파일
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

### <a name="override-hello-default-behaviour"></a>Hello 기본 동작 재정의
기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다. Hello 클래스 hello "페이지" 접미사를 사용 하면 계약으로 제거 됩니다.

이 코드를 추가 하는 hello 이름에 대 한 toooverride hello 기본 동작 합니다.

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport이이 코드를 추가 하 여 활동을 사용 하 여 추가 정보:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.

### <a name="alternate-method-call-startactivity-manually"></a>대체 메서드: 수동으로 `StartActivity()` 호출
처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `Page` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.

페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`를 호출하는 것이 좋습니다.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> 세션을 올바르게 종료해야 합니다.
> 
> hello를 자동으로 호출 하는 Windows 유니버설 SDK hello `EndActivity` hello 응용 프로그램을 닫으면 메서드. 즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드. 이 메서드 hello 현재 사용자에는 모든 응용 프로그램 로그에 영향을 주는 hello 응용 프로그램 없어진 hello Engagement 서버를에 알립니다.
> 
> 

## <a name="advanced-reporting"></a>고급 보고
필요에 따라 tooreport 응용 프로그램별 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다. hello Engagement API 모든 Engagement의 고급 기능을 사용할 수 있습니다.

자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)합니다.

