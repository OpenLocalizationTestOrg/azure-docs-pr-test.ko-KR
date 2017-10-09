---
title: "aaaGet은 Azure Mobile Engagement에 대 한 Windows Phone Silverlight 앱 시작"
description: "자세한 방법을 Windows Phone Silverlight 앱에 대 한 분석 및 푸시 알림과 함께 Azure Mobile Engagement toouse 합니다."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Windows Phone Silverlight 앱용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 알림을 toosegmented 사용자는 Windows Phone Silverlight 응용 프로그램의 합니다.
이 자습서에는 hello 간단한 브로드캐스트 시나리오를 Mobile Engagement를 사용 하 여 보여 줍니다. 여기서는 MPNS(Microsoft 푸시 알림 서비스)를 사용하여 푸시 알림을 받고 기본적인 데이터를 수집하는 빈 Windows Phone Silverlight 앱을 만듭니다.

> [!NOTE]
> hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다. 자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.

> [!NOTE]
> Windows Phone 8.1 및 이전 버전 프로젝트는 Visual Studio 2017에서 지원되지 않습니다.  자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.

> [!NOTE]
> Windows Phone 8.1 (Silverlight가 아닌) 대상으로 하는 경우 참조 toohello [Windows 유니버설 자습서](mobile-engagement-windows-store-dotnet-get-started.md)합니다.
> 
> 

이 자습서는 hello 다음을 사항이 필요합니다.

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement] Nuget 패키지

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started)을 참조하세요.
> 
> 

## <a id="setup-azme"></a>Windows Phone 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서는 기본적인 "통합", 최소 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다. hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement Windows Phone SDK 통합](mobile-engagement-windows-phone-sdk-overview.md)

Visual Studio toodemonstrate hello 통합 된 기본 응용 프로그램을 만듭니다.

### <a name="create-a-new-windows-phone-silverlight-project"></a>새 Windows Phone Silverlight 프로젝트 만들기
hello 다음 단계에서는 가정 hello를 사용 하 여 Visual Studio 2015의 hello 단계는 이전 버전의 Visual Studio에서 유사 합니다. 

1. Visual Studio를 시작 및 hello **홈** 화면에서 **새 프로젝트**합니다.
2. Hello 팝업에 선택 **Windows 8** -> **Windows Phone** -> **비어 있는 앱 (Windows Phone Silverlight)**합니다. Hello 앱 입력 **이름** 및 **솔루션 이름**, 클릭 하 고 **확인**합니다.
   
    ![][1]
3. Tootarget 하거나 선택할 수 있습니다 **Windows Phone 8.0** 또는 **Windows Phone 8.1**합니다.

이제 새 Windows Phone Silverlight 앱을 hello Azure Mobile Engagement SDK를 통합할 만들어졌습니다.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
1. Hello 설치 [MicrosoftAzure.MobileEngagement] 프로젝트에서 nuget 패키지 합니다.
2. 열기 `WMAppManifest.xml` (hello 속성 폴더 아래) hello 다음 선언 되어 있는지 확인 하 고 (추가할 그렇지 않은 경우) hello에 `<Capabilities />` 태그:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. 이제 Mobile Engagement 응용 프로그램에 대 한 앞에서 복사한 hello 연결 문자열을 붙여 넣고 hello에 붙여 `Resources\EngagementConfiguration.xml` hello 간의 파일 `<connectionString>` 및 `</connectionString>` 태그:
   
    ![][3]
4. Hello에 `App.xaml.cs` 파일:
   
    a. Hello 추가 `using` 문:
   
            using Microsoft.Azure.Engagement;
   
    b. Hello에 SDK hello 초기화 `Application_Launching` 메서드:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Hello에 hello 다음 삽입 `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>실시간 모니터링 사용
순서 toostart 데이터를 보내고는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 보내야 합니다.

1. MainPage.xaml.cs hello에서 추가 hello `using` 문:
   
        using Microsoft.Azure.Engagement;
2. Hello의 기본 클래스 대체 **MainPage**, 전에 변수인 **PhoneApplicationPage**와 **EngagementPage**합니다.
   
        class MainPage : EngagementPage 
3. `MainPage.xml` 파일에서:
   
    a. Tooyour 네임 스페이스 선언을 추가 합니다.
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. 대체 `phone:PhoneApplicationPage` hello XML 태그 이름에 `engagement:EngagementPage`합니다.

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement toointeract 있으며 푸시 알림 및 캠페인의 hello 컨텍스트에서 앱 내 메시징을 사용 하 여 사용자에 게 도달 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>사용자 응용 프로그램 tooreceive MPNS 푸시 알림을 사용 하도록 설정
새 기능 tooyour 추가 `WMAppManifest.xml` 파일:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>REACH SDK hello를 초기화 합니다.
1. `App.xaml.cs`, 호출 `EngagementReach.Instance.Init();` hello에 **Application_Launching** hello 에이전트 초기화 직후 함수:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. `App.xaml.cs`, 호출 `EngagementReach.Instance.OnActivated(e);` hello에 **Application_Activated** hello 에이전트 초기화 직후 함수:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

모든 설정을 완료했습니다. 이제 이 기본 통합을 제대로 수행했는지 확인합니다.

## <a id="send"></a>보낼 알림 tooyour 앱
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

이제 표시 되어야 알림을 장치에 표시 될 수 있는 앱에서 알림으로 hello 앱 hello 다음과 같은 알림 메시지로 그렇지 않은 경우 열려 있으면: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
