---
title: "aaaAdd 푸시 알림 tooyour Xamarin.iOS 앱을 Azure 앱 서비스"
description: "Azure 앱 서비스 toosend toouse 밀어넣기 알림 tooyour Xamarin.iOS 앱에 알아봅니다"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a>푸시 알림 tooyour Xamarin.iOS 앱 추가
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>개요
이 자습서에서는 푸시 알림을 toohello 추가한 [Xamarin.iOS 퀵 스타트](app-service-mobile-xamarin-ios-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치가 전송 되도록 합니다.

사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다. 참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건
* 전체 hello [Xamarin.iOS 퀵 스타트](app-service-mobile-xamarin-ios-get-started.md) 자습서입니다.
* 실제 iOS 장치. 푸시 알림은 hello iOS 시뮬레이터에서 지원 되지 않습니다.

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Apple 개발자 포털에서 푸시 알림을 hello 앱 등록
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a>프로그램 모바일 앱 toosend 푸시 알림 구성
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a>업데이트 hello 서버 프로젝트 toosend 푸시 알림
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a>Xamarin.iOS 프로젝트 구성
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a>푸시 알림 tooyour 앱 추가
1. **QSTodoService**, hello 다음 속성을 추가 되도록 **AppDelegate** hello 모바일 클라이언트를 얻을 수 있습니다.
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. Hello 다음 추가 `using` 문 toohello 맨 hello **AppDelegate.cs** 파일입니다.
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. **AppDelegate**, hello 재정의 **FinishedLaunching** 이벤트:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. 동일한 파일 hello 하 hello 재정의 **RegisteredForRemoteNotifications** 이벤트입니다. 이 코드에 대 한 hello 서버에서 지원 되는 모든 플랫폼에서 전송 되는 간단한 템플릿 알림을 등록 하는 합니다.
   
    알림 허브를 사용하는 템플릿에 대한 자세한 내용은 [템플릿](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. 그런 다음 재정의 하는 hello **DidReceivedRemoteNotification** 이벤트:
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

앱 업데이트 toosupport 푸시 알림이 되었습니다.

## <a name="test"></a>앱에서 푸시 알림 테스트
1. 키를 눌러 hello **실행** toobuild hello 프로젝트 단추 하 고 iOS 지원 장치에서 hello 응용 프로그램을 시작 합니다. 다음 클릭 **확인** tooaccept 푸시 알림을 합니다.
   
   > [!NOTE]
   > 앱에서 푸시 알림을 명시적으로 수락해야 합니다. 이 요청은만 hello 앱이 실행 hello 처음으로 발생 합니다.
   > 
   > 
2. Hello 응용 프로그램에서 작업을 입력 한 다음 더하기 hello (**+**) 아이콘입니다.
3. 알림이 수신 되 면 다음 클릭 확인 **확인** toodismiss hello 알림입니다.
4. 단계 2와 종가 즉시 hello 앱 반복 다음 알림을 표시 되는지 확인 하십시오.

이 자습서를 성공적으로 완료했습니다.

<!-- Images. -->

<!-- URLs. -->



