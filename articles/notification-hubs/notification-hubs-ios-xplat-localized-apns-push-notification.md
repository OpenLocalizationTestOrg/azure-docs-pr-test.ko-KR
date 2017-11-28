---
title: "aaaNotification 허브 지역화 주요 속보 자습서 iOS에 대 한"
description: "Azure 서비스 버스 알림 허브 toosend toouse 최신 알림을 (iOS)을 지역화 하는 방법에 대해 알아봅니다."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="f6faa-103">알림 허브 지역화 toosend 주요 뉴스 tooiOS 장치를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="f6faa-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6faa-104">Windows 스토어 C#</span><span class="sxs-lookup"><span data-stu-id="f6faa-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="f6faa-105">iOS</span><span class="sxs-lookup"><span data-stu-id="f6faa-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f6faa-106">개요</span><span class="sxs-lookup"><span data-stu-id="f6faa-106">Overview</span></span>
<span data-ttu-id="f6faa-107">이 항목에서는 toouse hello [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 언어 및 장치에서 지역화 된 알림을 주요 Azure 알림 허브 toobroadcast의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="f6faa-108">이 자습서에서 만든 hello iOS 앱과 시작 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="f6faa-109">완료 되 면에 관심이 있는 범주에 대 한 수 tooregister 됩니다, 한 tooreceive hello 알림이에서 언어를 지정 하 고 해당 언어로 hello 선택한 범주에 대 한 푸시 알림을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="f6faa-110">두 개의 부분 toothis 시나리오는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="f6faa-111">장치 toospecify는 언어 및 뉴스 범주; 주요 toosubscribe toodifferent 클라이언트 허용 하는 iOS 앱</span><span class="sxs-lookup"><span data-stu-id="f6faa-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="f6faa-112">hello 백 엔드를 브로드캐스팅합니다. hello를 사용 하 여 hello 알림을, **태그** 및 **템플릿** Azure 알림 허브의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6faa-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f6faa-113">Prerequisites</span></span>
<span data-ttu-id="f6faa-114">이미 완료 한 상태 여야 hello [최신 뉴스 사용 하 여 알림 허브 toosend] 자습서와이 자습서에서는 해당 코드에 직접 작성 때문 hello 코드를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="f6faa-115">Visual Studio 2012 이상은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="f6faa-116">템플릿 개념</span><span class="sxs-lookup"><span data-stu-id="f6faa-116">Template concepts</span></span>
<span data-ttu-id="f6faa-117">[최신 뉴스 사용 하 여 알림 허브 toosend] 사용 하는 응용 프로그램을 빌드한 **태그** toosubscribe toonotifications 다른 뉴스 범주에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="f6faa-118">하지만 대부분의 앱은 여러 시장을 대상으로 하므로 지역화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="f6faa-119">이 hello 알림 자체의 hello 콘텐츠 지역화 toobe 있고 의미 배달된 toohello 장치 집합을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="f6faa-120">이 항목에서는 보여줍니다 어떻게 toouse hello **템플릿** tooeasily 배달 알림 허브의 기능에는 최신 알림을 지역화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="f6faa-121">참고:는 한 가지 방법은 toosend 지역화 된 알림 toocreate 각 태그의 여러 버전을 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="f6faa-122">예를 들어, toosupport 영어, 프랑스어, 및 북경어, 세계 뉴스에 대 한 세 개의 서로 다른 태그가 필요 합니다: "world_en", "world_fr" 및 "world_ch"입니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="f6faa-123">에서는 다음 것이 toosend 이러한 태그의 hello world 뉴스 tooeach의 지역화 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="f6faa-124">이 항목에 태그의 템플릿 tooavoid hello 급증 및 여러 메시지를 보내는의 hello 요구 사항을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="f6faa-125">상위 수준 템플릿은 방식으로 toospecify 어떻게 특정 장치에 알림을 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="f6faa-126">hello 템플릿은 앱 백 엔드에서 보낸 hello 메시지의 일부인 tooproperties 참조 하 여 hello 정확한 페이로드 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="f6faa-127">여기서는 모든 지원되는 언어를 포함하는 로캘을 알 수 없는 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="f6faa-128">다음에서는 사용 하면 장치 등록 toohello 올바른 속성을 참조 하는 템플릿을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="f6faa-129">예를 들어 프랑스어 뉴스 tooregister를가 하는 iOS 앱 hello 다음을 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="f6faa-130">템플릿은 매우 강력한 기능입니다. 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6faa-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="f6faa-131">hello 응용 프로그램 사용자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="f6faa-131">hello app user interface</span></span>
<span data-ttu-id="f6faa-132">에서는 이제 hello 항목에서 만든 hello 최신 뉴스 앱을 수정 합니다 [최신 뉴스 사용 하 여 알림 허브 toosend] toosend 템플릿을 사용 하 여 최신 뉴스를 지역화 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="f6faa-133">프로그램 MainStoryboard_iPhone.storyboard에서 지원 되며는 hello 3 언어와 세그먼트 컨트롤 추가: 영어, 프랑스어 및 북경어 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="f6faa-134">그런 다음 확인 있는지 tooadd는 IBOutlet 프로그램 ViewController.h에 아래와 같이:</span><span class="sxs-lookup"><span data-stu-id="f6faa-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="f6faa-135">Hello iOS 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="f6faa-135">Building hello iOS app</span></span>
1. <span data-ttu-id="f6faa-136">프로그램 Notification.h 추가 hello *retrieveLocale* 메서드, 및 hello 저장소를 수정 하 고 아래와 같이 메서드 구독:</span><span class="sxs-lookup"><span data-stu-id="f6faa-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="f6faa-137">프로그램 Notification.m 수정 hello *storeCategoriesAndSubscribe* hello 로캘 매개 변수를 추가 하 고 hello 사용자 기본값에서 저장 하 여 메서드:</span><span class="sxs-lookup"><span data-stu-id="f6faa-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="f6faa-138">그런 다음 hello 수정 *구독* 메서드 tooinclude hello 로캘:</span><span class="sxs-lookup"><span data-stu-id="f6faa-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="f6faa-139">Hello 메서드 지금 사용 방법을 확인 *registerTemplateWithDeviceToken*, 대신 *registerNativeWithDeviceToken*합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="f6faa-140">서식 파일에 대 한를 등록할 때 했으므로 tooprovide hello json 템플릿 및 hello 템플릿의 이름을 (대로 앱 tooregister 서로 다른 템플릿을 삭제할 수).</span><span class="sxs-lookup"><span data-stu-id="f6faa-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="f6faa-141">해당 뉴스 toomake 있는지 tooreceive hello notifciations 원하는 대로 있는지 tooregister 태그도 사용 하 여 범주를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="f6faa-142">Hello 사용자 기본 설정에서 메서드 tooretrieve hello 로캘을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="f6faa-143">이제 알림 클래스, 수정한 있는지 toomake 우리의 ViewController는 있는지의 hello 사용 하 여 새 UISegmentControl 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="f6faa-144">다음 줄에서 hello hello 추가 *viewDidLoad* 메서드 toomake 있는지 tooshow hello 로캘 현재 선택 된:</span><span class="sxs-lookup"><span data-stu-id="f6faa-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="f6faa-145">그런 다음 프로그램 *구독* 메서드를 호출 toohello 변경 *storeCategoriesAndSubscribe* toohello 다음:</span><span class="sxs-lookup"><span data-stu-id="f6faa-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="f6faa-146">Tooupdate hello가 마지막으로, *didRegisterForRemoteNotificationsWithDeviceToken* 프로그램 AppDelegate.m 메서드에서 앱이 시작 되 등록은 올바르게 새로 고칠 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6faa-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="f6faa-147">호출 toohello 변경 *구독* hello 다음과 같이 알림 메서드:</span><span class="sxs-lookup"><span data-stu-id="f6faa-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="f6faa-148">(선택 사항) .NET 콘솔 앱에서 지역화된 템플릿 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f6faa-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="f6faa-149">(선택 사항) Hello 장치에서 지역화 된 템플릿이 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="f6faa-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="f6faa-150">액세스 tooVisual Studio 했거나 hello 장치에서 앱 hello에서 직접 지역화 hello 템플릿 알림을 보내면 toojust 테스트 하지 마십시오 경우.</span><span class="sxs-lookup"><span data-stu-id="f6faa-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="f6faa-151">간단한 할 수 있습니다 지역화 hello 템플릿 매개 변수 toohello 추가 `SendNotificationRESTAPI` hello 이전 자습서에 정의 된 메서드.</span><span class="sxs-lookup"><span data-stu-id="f6faa-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a><span data-ttu-id="f6faa-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f6faa-152">Next Steps</span></span>
<span data-ttu-id="f6faa-153">템플릿 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f6faa-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="f6faa-154">[알림 허브를 통해 사용자에게 알림: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="f6faa-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="f6faa-155">[알림 허브를 통해 사용자에게 알림: 모바일 서비스]</span><span class="sxs-lookup"><span data-stu-id="f6faa-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[최신 뉴스 사용 하 여 알림 허브 toosend]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[알림 허브를 통해 사용자에게 알림: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[알림 허브를 통해 사용자에게 알림: 모바일 서비스]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
