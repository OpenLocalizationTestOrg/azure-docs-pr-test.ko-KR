---
title: "aaaNotification 허브 주요 속보 자습서-iOS"
description: "자세한 방법을 toouse Azure 서비스 버스 알림 허브 toosend 뉴스 알림 tooiOS 장치를 중단 합니다."
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
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>알림 허브 toosend 최신 뉴스를 사용 하 여
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>개요
이 항목에서는 toouse Azure 알림 허브 toobroadcast 주요 뉴스 알림 tooan iOS 앱. 완료 되 면에 관심이 있는 뉴스 범주 파괴 수 tooregister 수 및 해당 범주에 대 한 푸시 알림을 수신 합니다. 이 시나리오는 알림을 그 예: RSS 수집기, 음악 팬 속도 등에 대 한 앱에 대 한 관심 선언 이전에 사용자의 전송 toobe toogroups 있는 많은 응용 프로그램에 대 한 일반적인 패턴입니다.

브로드캐스트 시나리오 하나 이상 포함 하 여 설정 된 *태그* hello 알림 허브의 등록을 만들 때. 알림을 tooa 태그를 보내면 hello 태그에 대 한 모든 장치를 등록 한 hello 알림을 받게 됩니다. 태그는 단순히 문자열을 하기 때문에 미리 프로 비전 toobe를 갖지 않습니다. 태그에 대 한 자세한 내용은 참조 너무[알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)합니다.

## <a name="prerequisites"></a>필수 조건
이 항목에서는에서 만든 hello 앱 [알림 허브 시작][get-started]합니다. 이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.

## <a name="add-category-selection-toohello-app"></a>범주 선택 toohello 앱 추가
hello 첫 번째 단계는 tooadd hello UI 요소 tooyour 기존 스토리 보드 hello 사용자 tooselect 범주 tooregister 수 있도록 합니다. 사용자가 선택한 hello 범주 hello 장치에 저장 됩니다. Hello 앱이 시작 되 면 태그로 hello 선택한 범주와 알림 허브에 장치 등록이 만들어집니다.

1. 프로그램 MainStoryboard_iPhone.storyboard hello 개체 라이브러리에서 다음과 같은 구성 요소가 hello를 추가 합니다.
   
   * "Breaking News" 텍스트가 포함된 레이블
   * "World", "Politics", "Business", "Technology", "Science", "Sports" 범주 텍스트가 포함된 레이블
   * 각 스위치를 설정 하는 범주를 하나씩 6 개의 스위치 **상태** toobe **오프** 기본적으로 합니다.
   * "Subscribe" 단추
     
     스토리보드는 다음과 같이 표시됩니다.
     
     ![][3]
2. Hello 도우미 편집기에서 모든 hello 스위치에 대해 콘센트 만들고 "WorldSwitch" 전화할 "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. "subscribe" 단추에 대한 동작을 만듭니다. 프로그램 ViewController.h hello 다음을 포함 되어야 합니다.
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. `Notifications`라는 새 **Cocoa Touch 클래스**를 만듭니다. Hello 코드 hello 파일 Notifications.h의 hello 인터페이스 섹션에 다음을 복사 합니다.
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. 다음 가져오기 지시문 tooNotifications.m hello를 추가 합니다.
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Hello 코드 hello 파일 Notifications.m의 hello 구현 섹션에서 다음을 복사 합니다.
   
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



    이 클래스는 toostore 로컬 저장소를 사용 하 여 하 고이 장치를 받을 뉴스의 hello 범주를 검색 합니다. 또한 사용 하 여 이러한 범주에 대 한 메서드 tooregister을 포함 한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 등록 합니다.

1. Hello AppDelegate.h 파일에서 Notifications.h에 대 한 import 문을 추가 하 고 hello 알림 클래스의 인스턴스에 대 한 속성을 추가 합니다.
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Hello에 **didFinishLaunchingWithOptions** AppDelegate.m에서 메서드 hello hello 메서드 시작 시 hello 코드 tooinitialize hello 알림을 인스턴스를 추가 합니다.  
   
    `HUBNAME`및 `HUBLISTENACCESS` (hubinfo.h에 정의 됨)은 hello 이미 `<hub name>` 및 `<connection string with listen access>` 와 알림 허브 이름 및 hello 연결 문자열에 대 한 자리 표시자 *DefaultListenSharedAccessSignature*이전에 얻은입니다
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > 클라이언트 응용 프로그램과 함께 배포 되는 자격 증명에 일반적으로 안전 하지 않으므로 클라이언트 응용 프로그램과 함께 수신 액세스에 대 한 hello 키만 배포 해야 합니다. 알림, 하지만 기존 등록에 대 한 응용 프로그램 tooregister 프로그램을 수정할 수 없는 액세스 활성화를 수신 하 고 알림을 보낼 수 없습니다. hello 전체 액세스 키를 사용 하 여 보안 된 백 엔드 서비스 알림을 전송 하 고 기존 등록을 변경 합니다.
   > 
   > 
3. Hello에 **didRegisterForRemoteNotificationsWithDeviceToken** AppDelegate.m에서 메서드 코드 toopass hello 장치 토큰 toohello 알림을 클래스 다음 hello hello 코드 hello 메서드를 바꿉니다. hello 알림을 클래스 hello hello 범주를 사용 하 여 알림을 등록을 수행 합니다. Hello 이라고 hello 사용자 범주를 선택할 변경 되 면 `subscribeWithCategories` 응답 toohello에서 메서드 **구독** 단추 tooupdate 해당 합니다.
   
   > [!NOTE]
   > 를 언제 든 지 hello 푸시 알림 서비스 APNS (Apple)에서 할당 하는 hello 장치 토큰 변경 수 때문에 등록 해야 알림에 대 한 자주 tooavoid 알림 오류가 발생 했습니다. 이 예제에서는 hello 이러한 앱이 시작 될 때마다 알림을 등록 합니다. 자주 실행 되는 응용 프로그램의 경우 하루에 한 번 이상 건너뛸 수 있습니다 아마도 등록 toopreserve 대역폭 hello 이전 등록 이후 1 일 미만 경과한 경우.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    이 시점에서 있습니다 수 있어야 다른 코드 hello에 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드.

1. hello 다음 방법 이미 있는 것은 AppDelegate.m에 hello 완료 [알림 허브 시작] [ get-started] 자습서입니다.  그렇지 않은 경우 메서드를 추가합니다.
   
    -(void) MessageBox:(NSString *) 제목 메시지:(NSString *) messageText {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * 응용 프로그램 (void):(UIApplication *) 응용 프로그램 didReceiveRemoteNotification: (NSDictionary *) 사용자 정보 {NSLog (@"% @", 사용자 정보);   [메시지 자체 MessageBox:@"Notification": [[사용자 정보 objectForKey:@"aps"] valueForKey:@"alert"]]; }
   
   이 메서드는 간단한 표시 하 여 hello 응용 프로그램을 실행 하는 경우 수신 하는 알림을 처리 **UIAlert**합니다.
2. ViewController.m, hello에 코드를 다음 AppDelegate.h 및 복사 hello에 대 한 import 문을 추가 XCode에서 생성 된 **구독** 메서드. 이 코드는 hello 알림을 등록 toouse hello 새 범주 태그가 hello 사용자 인터페이스에서 hello 사용자가 선택한 업데이트 됩니다.
   
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
   
   이 메서드가 만드는 **NSMutableArray** 의 범주 및 사용 하 여 hello **알림** hello 로컬 저장소 및 레지스터 hello 해당 태그와 알림 허브에에서 클래스 toostore hello 목록입니다. 범주 변경 되 면 hello 등록 hello 새 범주와 다시 만들어집니다.
3. ViewController.m, 추가 hello에서 코드 다음 hello **viewDidLoad** hello 이전에 저장 된 범주에 따라 메서드 tooset hello 사용자 인터페이스입니다.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



이제 hello 앱 hello 알림 허브와 장치 사용 되는 로컬 저장소 tooregister hello에에서 범주 집합에를 저장할 수 hello 앱 시작 될 때마다 합니다.  hello 사용자 런타임에 범주의 hello 선택을 변경 하 고 hello를 클릭 하 **구독** hello 장치에 대 한 메서드 tooupdate hello 등록 합니다. 다음으로 hello 앱 toosend hello 알림을 hello 앱 자체에서 직접 주요 업데이트 합니다.

## <a name="optional-sending-tagged-notifications"></a>(선택 사항) 태그가 지정된 알림 보내기
액세스 tooVisual Studio가 없는 경우 toohello 다음 섹션 건너뛰고 hello 앱 자체에서 알림을 보낼 수 있습니다. Hello에서 hello 적절 한 템플릿 알림을 보낼 수도 있습니다 [Azure 클래식 포털] hello 디버그 탭을 사용 하 여 알림 허브에 대 한 합니다. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(선택 사항) Hello 장치에서 알림을 보내는합니다
알림을 보낼 백 엔드 서비스에 의해 일반적으로 하지만 hello 앱에서 직접 최신 알림을 보낼 수 있습니다. toodo hello 업데이트할 것이 `SendNotificationRESTAPI` hello에 정의한 메서드 [알림 허브 시작] [ get-started] 자습서입니다.

1. ViewController.m 업데이트 hello에 `SendNotificationRESTAPI` 메서드로 뒤 hello 범주 태그에 대 한 매개 변수를 허용 하 고 적절 한 hello 보냅니다 있도록 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 알림입니다.
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
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
2. ViewController.m 업데이트 hello에 **알림 보내기** 뒤에 오는 hello 코드에 나와 있는 것 처럼 동작 합니다. 개별적으로 각 태그를 사용 하 여 hello 알림을 보내도록 되 고 toomultiple 플랫폼을 보냅니다 되도록.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. 프로젝트를 다시 빌드하고 빌드 오류가 없는지 확인합니다.

## <a name="run-hello-app-and-generate-notifications"></a>Hello 앱을 실행 하 고 알림 생성
1. 키를 눌러 hello 단추 toobuild hello 프로젝트를 실행 하 고 hello 응용 프로그램을 시작 합니다. 몇 가지 주요 뉴스 옵션 toosubscribe tooand를 선택 하 고 hello 키를 누릅니다 **Subscribe** 단추입니다. 알림을 구독 하는 hello 나타내는 대화 상자가 표시 됩니다.
   
    ![][1]
   
    선택 하는 경우 **Subscribe**, 앱 변환 hello 선택한 범주 태그에 hello 및 hello 알림 허브에서 선택 하는 hello 태그에 대 한 새 장치 등록을 요청 합니다.
2. 주요 뉴스 누릅니다 hello 송신할 메시지 toobe 입력 **알림 보내기** 단추입니다. 또는 hello.NET 콘솔 응용 프로그램 toogenerate 알림을 실행 합니다.
   
    ![][2]
3. 각 구독 장치 toobreaking 뉴스 hello 최신 알림을 방금 전송 받은 받게 됩니다.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 이전에 배운 것 어떻게 toobroadcast 최신 뉴스 범주별으로 보여 줍니다. 기타 고급 알림 허브 시나리오를 강조 표시 하는 자습서를 따라 hello 중 하나를 완료 하는 것이 좋습니다.

* **[알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]**
  
    뉴스 앱 tooenable 보내는 주요 tooexpand hello 알림을 지역화 하는 방법에 대해 알아봅니다.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[Azure 클래식 포털]: https://manage.windowsazure.com
