---
title: "aaaGet Xamarin.iOS에 대 한 Azure Mobile Engagement와 시작 됨"
description: "자세한 내용은 방법 toouse 분석 및 푸시 알림 Xamarin.iOS 앱에 대 한 Azure Mobile Engagement 합니다."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0448209e-fff6-47bd-985c-2cf074bac12f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 02340a744753dcc5cd1b6888a5fa87628be47b68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinios-apps"></a>Xamarin.iOS 앱용 Azure Mobile Engagement 시작
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

이 항목에서는 Azure Mobile Engagement toounderstand toouse Xamarin.iOS 응용 프로그램에서 응용 프로그램 사용 및 송신 푸시 알림을 toosegmented 사용자입니다.
이 자습서에서는 기본 데이터를 수집하고 APNS(Apple 푸시 알림 시스템)를 사용하여 푸시 알림을 받는 빈 Xamarin.iOS 앱을 만듭니다.

> [!NOTE]
> hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다. 자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.

이 자습서는 hello 다음을 사항이 필요합니다.

* [Xamarin Studio](http://xamarin.com/studio). Xamarin이 포함된 Visual Studio를 사용할 수도 있지만 이 자습서에서는 Xamarin Studio를 사용합니다. 또한 설치 지침은 [Visual Studio 및 Xamarin을 위한 설정 및 설치](https://msdn.microsoft.com/library/mt613162.aspx)를 참조하세요. 
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 평가판](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-ios-get-started)을 참조하세요.
> 
> 

## <a id="setup-azme"></a>iOS 앱용 Mobile Engagement 설정
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결
이 자습서에는 "기본 통합" hello 최소 필수 toocollect 데이터 설정 되 고 푸시 알림을 보내려면 표시 합니다.

Xamarin toodemonstrate hello 통합 기본 앱을 만듭니다.

### <a name="create-a-new-xamarinios-project"></a>새 Xamarin.iOS 프로젝트 만들기
1. Xamarin Studio를 시작합니다. 너무 이동**파일** -> **새로** -> **솔루션** 
   
    ![][1]
2. 선택 **단일 앱 보기**, 선택한 hello 언어 인지 확인 **C#** 클릭 하 고 **다음**합니다.
   
    ![][2]
3. Hello 입력 **응용 프로그램 이름** 및 hello **조직 식별자** 클릭 하 고 **다음**합니다. 
   
    ![][3]
   
   > [!IMPORTANT]
   > 게시 프로필을 iOS 앱에 일치 하는 응용 프로그램 ID를 사용 하는 hello 여기에 있는 번들 식별자와 정확 하 게 toodeploy 결국 사용 하면 해당 hello 있는지 확인 하십시오. 
   > 
   > 
4. 업데이트 hello **프로젝트 이름**, **솔루션 이름** 및 **위치** 필요 하 고 클릭 **만들기**합니다.
   
    ![][4]

Xamarin Studio는 Mobile Engagement 통합할 hello 데모 응용 프로그램을 만듭니다. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>응용 프로그램 tooMobile Engagement 백 엔드 연결
1. 마우스 오른쪽 단추로 클릭 하 여 hello **패키지** hello 솔루션 창과 선택에서 폴더 **패키지 추가 중...**
   
    ![][5]
2. Hello에 대 한 검색 **Microsoft Azure Mobile Engagement Xamarin SDK** tooyour 솔루션에 추가 합니다.  
   
    ![][6]
3. 열기 **AppDelegate.cs** hello 다음 추가 및 문을 사용 하 여:
   
        using Microsoft.Azure.Engagement.Xamarin;
4. Hello에 **FinishedLaunching** 메서드를 다음 Mobile Engagement 백 엔드와 tooinitialize hello 연결 hello를 추가 합니다. 있는지 tooadd 확인 프로그램 **ConnectionString**합니다. 이 코드에서는 dummy **NotificationIcon** hello 할 수도 있습니다는 Mobile Engagement SDK 추가할 tooreplace 합니다. 
   
        EngagementConfiguration config = new EngagementConfiguration {
                        ConnectionString = "YourConnectionStringFromAzurePortal",
                        NotificationIcon = UIImage.FromBundle("close")
                    };
        EngagementAgent.Init (config);

## <a id="monitor"></a>실시간 모니터링 사용
순서 toostart 데이터를 보내고 hello 사용자는 활성 하나 이상 화면 toohello Mobile Engagement 백 엔드를 보내야 합니다.

1. 열기 **ViewController.cs** hello 다음 추가 및 문을 사용 하 여:
   
        using Microsoft.Azure.Engagement.Xamarin;
2. Hello 클래스를 대체 `ViewController` 에서 상속 `UIViewController` 너무`EngagementViewController`합니다. 

## <a id="monitor"></a>실시간 모니터링과 앱 연결
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용
Mobile Engagement 사용 하면 사용자와 toointeract 및 도달 범위 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용 합니다. 이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.
hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.

### <a name="modify-your-application-delegate"></a>응용 프로그램 대리자 수정
1. 열기 hello **AppDelegate.cs** hello 다음 추가 및 문을 사용 하 여:
   
        using System; 
2. 이제 hello 내 `FinishedLaunching` 메서드를 hello tooregister 이후 푸시 메시지에 대 한 다음 추가`EngagementAgent.init(...)`
   
        if (UIDevice.CurrentDevice.CheckSystemVersion(8,0))
        {
            var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                (UIUserNotificationType.Badge |
                    UIUserNotificationType.Sound |
                    UIUserNotificationType.Alert),
                null);
            UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications ();
        }
        else
        {
            UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (
                UIRemoteNotificationType.Badge |
                UIRemoteNotificationType.Sound |
                UIRemoteNotificationType.Alert);
        }
3. -마지막으로 업데이트 하거나 hello 다음 메서드를 추가 합니다.
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, 
            Action<UIBackgroundFetchResult> completionHandler)
        {
            EngagementAgent.ApplicationDidReceiveRemoteNotification(userInfo, completionHandler);
        }
   
        public override void RegisteredForRemoteNotifications (UIApplication application, NSData deviceToken)
        {
            // Register device token on Engagement
            EngagementAgent.RegisterDeviceToken(deviceToken);
        }
   
        public override void FailedToRegisterForRemoteNotifications(UIApplication application, NSError error)
        {
            Console.WriteLine("Failed tooregister for remote notifications: Error '{0}'", error);
        }
4. 사용자 **Info.plist** hello 솔루션의 파일, 해당 hello 확인 **번들 식별자** hello로 일치 **앱 ID** hello Apple 개발자의에서 프로비저닝 프로필에 있는 가운데 맞춤 됩니다. 
   
    ![][7]
5. 동일한 hello **Info.plist** 파일, hello를 선택 했는지 확인 **백그라운드 모드를 사용 하도록 설정** 및 **원격 알림**합니다. 
   
     ![][8]
6. 이 게시 프로필에 연결 했는지 hello 장치의 hello 앱을 실행 합니다. 

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[1]: ./media/mobile-engagement-xamarin-ios-get-started/new-solution.png
[2]: ./media/mobile-engagement-xamarin-ios-get-started/app-type.png
[3]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-name.png
[4]: ./media/mobile-engagement-xamarin-ios-get-started/configure-project-confirm.png
[5]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget.png
[6]: ./media/mobile-engagement-xamarin-ios-get-started/add-nuget-azme.png
[7]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-confirm-bundle.png
[8]: ./media/mobile-engagement-xamarin-ios-get-started/info-plist-configure-push.png
