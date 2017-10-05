---
title: "알림 허브 속보 자습서 - iOS"
description: "Azure 서비스 버스 알림 허브를 사용하여 iOS 장치에 최신 뉴스 알림을 보내는 방법에 대해 알아봅니다."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a>알림 허브를 사용하여 속보 보내기
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>개요
이 항목에서는 Azure 알림 허브를 사용하여 iOS 앱에 속보 알림을 브로드캐스트하는 방법을 보여 줍니다. 완료하면, 관심이 있는 속보 범주를 등록하고 해당 범주의 푸시 알림만 받을 수 있습니다. 이 시나리오는 RSS 수집기, 음악 애호가를 위한 앱 등 이전에 관심을 보인 사용자 그룹에 알림을 보내야 하는 많은 앱에 공통된 패턴입니다.

브로드캐스트 시나리오를 사용하려면 알림 허브에서 등록을 만들 때 하나 이상의 *태그*를 포함하면 됩니다. 태그에 알림이 전송되면 태그에 대해 등록된 모든 장치에서 알림을 받게 됩니다. 태그는 단순히 문자열이므로 사전에 프로비전해야 할 필요가 없습니다. 태그에 대한 자세한 내용은 [알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
이 항목은 [Notification Hubs 시작][get-started]에서 만든 앱을 기반으로 합니다. 이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.

## <a name="add-category-selection-to-the-app"></a>앱에 범주 선택 추가
첫 번째 단계는 기존의 스토리보드에 사용자가 등록할 범주를 선택할 수 있도록 하는 UI 요소를 추가하는 것입니다. 사용자가 선택한 범주는 장치에 저장됩니다. 앱을 시작하면 장치 등록이 선택한 범주와 함께 태그로서 알림 허브에 생성됩니다.

1. MainStoryboard_iPhone.storyboard의 개체 라이브러리에서 다음 구성 요소를 추가합니다.
   
   * "Breaking News" 텍스트가 포함된 레이블
   * "World", "Politics", "Business", "Technology", "Science", "Sports" 범주 텍스트가 포함된 레이블
   * 범주당 하나씩인 6개의 스위치는 각 스위치 **상태**를 기본적으로 **Off(꺼짐)**가 되도록 설정합니다.
   * "Subscribe" 단추
     
     스토리보드는 다음과 같이 표시됩니다.
     
     ![][3]
2. 단말기 편집기에서 모든 스위치에 대한 콘센트를 만든 다음 "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"로 지정합니다.
3. "subscribe" 단추에 대한 동작을 만듭니다. ViewController.h에는 다음이 포함되어 있어야 합니다.
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. `Notifications`라는 새 **Cocoa Touch 클래스**를 만듭니다. 다음 코드를 Notifications.h 파일의 인터페이스 섹션에 복사합니다.
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. 다음 import 지시문을 Notifications.m에 추가합니다.
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. 다음 코드를 Notifications.m 파일의 구현 섹션에 복사합니다.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    이 클래스는 로컬 저장소를 사용하여 이 장치에서 받을 뉴스의 범주를 저장하고 검색합니다. 또한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 등록을 사용하여 이러한 범주에 등록하는 메서드도 포함되어 있습니다.

1. AppDelegate.h 파일에서 Notifications.h에 대한 import 문을 추가하고 알림 클래스의 인스턴스에 대한 속성을 추가합니다.
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. AppDelegate.m의 **didFinishLaunchingWithOptions** 메서드에서 메서드 시작 부분에 알림 인스턴스를 초기화하는 코드를 추가합니다.  
   
    `HUBNAME`과 `HUBLISTENACCESS`(hubinfo.h에 정의됨)는 `<hub name>` 및 `<connection string with listen access>` 자리 표시자를 알림 허브 이름과 앞서 얻었던 *DefaultListenSharedAccessSignature*의 연결 문자열로 바꿉니다.
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > 클라이언트 앱과 함께 배포되는 자격 증명은 일반적으로 안전하지 않기 때문에 클라이언트 앱과 함께 listen access용 키만 배포해야 합니다. Listen access를 통해 앱에서 알림을 등록할 수 있지만, 기존 등록을 수정할 수 없으며 알림을 전송할 수도 없습니다. 안전한 백 엔드 서비스에서 알림을 보내고 기존 등록을 변경하는 데에는 모든 권한 키가 사용됩니다.
   > 
   > 
3. AppDelegate.m의 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드에서 메서드의 코드를 다음 코드로 바꿔 알림 클래스에 장치 토큰을 전달합니다. 알림 클래스는 범주를 사용하여 알림에 대해 등록을 수행합니다. 사용자가 범주 선택 항목을 변경하는 경우 **구독** 단추에 대한 응답으로 `subscribeWithCategories` 메서드를 호출하여 범주 선택 항목을 업데이트합니다.
   
   > [!NOTE]
   > APNS(Apple Push Notification Service)에서 할당하는 장치 토큰은 언제든지 변경될 수 있으므로 알림 실패를 피하려면 알림을 자주 등록해야 합니다. 이 예제에서는 앱이 시작될 때마다 알림을 등록합니다. 자주(하루 두 번 이상) 실행되는 앱에서는 이전 등록 이후 만 하루가 지나지 않은 경우 대역폭 유지를 위한 등록을 건너뛸 수 있습니다.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    이때 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드에 다른 코드가 없어야 합니다.

1. 다음 방법 이미 있어야 AppDelegate.m 완료는 [알림 허브 시작] [ get-started] 자습서입니다.  그렇지 않은 경우 메서드를 추가합니다.
   
    -(void) MessageBox:(NSString *) 제목 메시지:(NSString *) messageText {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * 응용 프로그램 (void):(UIApplication *) 응용 프로그램 didReceiveRemoteNotification: (NSDictionary *) 사용자 정보 {NSLog (@"% @", 사용자 정보);   [메시지 자체 MessageBox:@"Notification": [[사용자 정보 objectForKey:@"aps"] valueForKey:@"alert"]]; }
   
   이 메서드는 단일 **UIAlert**를 표시하여 앱이 실행 중일 때 수신된 알림을 처리합니다.
2. ViewController.m에서 AppDelegate.h에 대해 import 문을 추가하고 다음 코드를 XCode 생성 **구독** 메서드에 복사합니다. 이 코드는 사용자 인터페이스에서 사용자가 선택한 새 범주 태그를 사용하도록 알림 등록을 업데이트합니다.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   이 메서드는 범주의 **NSMutableArray**를 만들고 **Notifications** 클래스를 사용하여, 로컬 저장소에 목록을 저장하고 알림 허브에 해당 태그를 등록합니다. 범주가 변경되면 새 범주로 등록이 다시 생성됩니다.
3. ViewController.m에서 **viewDidLoad** 메서드에 다음 코드를 추가하여 이전에 저장한 범주를 기반으로 사용자 인터페이스를 설정합니다.

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



이제 앱은 앱이 시작할 때마다 알림 허브에 등록하는 데 사용한 장치 로컬 저장소에 범주 집합을 저장할 수 있습니다.  사용자는 런타임 시 범주 선택 사항을 변경하고 **구독** 메서드를 클릭하여 장치에 대한 등록을 업데이트할 수 있습니다. 다음으로, 앱 자체에서 직접 속보 알림을 보내도록 앱을 업데이트합니다.

## <a name="optional-sending-tagged-notifications"></a>(선택 사항) 태그가 지정된 알림 보내기
Visual Studio에 액세스할 수 없는 경우 다음 섹션으로 건너뛰고 앱 자체에서 알림을 보낼 수 있습니다. 또한 알림 허브에 대한 디버그 탭을 사용하여 [Azure 클래식 포털] 에서 적절한 템플릿 알림을 보낼 수 있습니다. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a>(선택 사항) 장치에서 알림 보내기
일반적으로 백 엔드 서비스에서 알림을 보내지만 속보 알림은 앱 자체에서 직접 보낼 수 있습니다. 이 업데이트 될 작업을 수행 하는 `SendNotificationRESTAPI` 에 정의한 메서드는 [알림 허브 시작] [ get-started] 자습서입니다.

1. ViewController.m에서 범주 태그에 대한 매개 변수를 허용하고 적절한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 알림을 보내도록 다음과 같이 `SendNotificationRESTAPI` 메서드를 업데이트합니다.
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. ViewController.m에서 다음 코드에 표시된 것처럼 **알림 보내기** 작업을 업데이트합니다. 그러면 개별적으로 각 태그를 사용하여 알림을 보내고 여러 플랫폼으로 보냅니다.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. 프로젝트를 다시 빌드하고 빌드 오류가 없는지 확인합니다.

## <a name="run-the-app-and-generate-notifications"></a>앱 실행 및 알림 생성
1. 실행 단추를 눌러 프로젝트를 빌드하고 앱을 시작합니다. 구독할 속보 옵션을 선택하고 **구독** 단추를 누릅니다. 알림 구독을 나타내는 대화 상자가 표시됩니다.
   
    ![][1]
   
    **구독**을 선택하면 앱은 선택한 범주를 태그로 변환하고 알림 허브에서 선택한 태그에 대한 새로운 장치 등록을 요청합니다.
2. 속보로 보낼 메시지를 입력하고 **알림 보내기** 단추를 누릅니다. 또는 .NET 콘솔 앱을 실행하여 알림을 생성합니다.
   
    ![][2]
3. 속보를 구독하는 각 장치에서 방금 보낸 속보 알림을 받게 됩니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 범주별로 속보를 브로드캐스트하는 방법에 대해 알아보았습니다. 이제 기타 고급 알림 허브 시나리오를 다루는 다음 자습서 중 하나를 완료해 보세요.

* **[Notification Hubs를 사용하여 지역화된 속보 브로드캐스트]**
  
    지역화된 알림을 보낼 수 있도록 속보 앱을 확장하는 방법에 대해 알아보세요.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs를 사용하여 지역화된 속보 브로드캐스트]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Azure 클래식 포털]: https://manage.windowsazure.com
