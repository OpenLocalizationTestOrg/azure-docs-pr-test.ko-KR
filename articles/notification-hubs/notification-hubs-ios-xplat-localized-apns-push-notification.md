---
title: "iOS용 알림 허브 지역화된 속보 자습서"
description: "Azure 서비스 버스 알림 허브를 사용하여 지역화된 최신 뉴스 알림을 보내는 방법에 대해 알아봅니다(iOS)."
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
ms.openlocfilehash: fd2b7d9dfd4f432bbcbaa3ed76f8bec0b9677e17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="c96e2-103">알림 허브를 사용하여 iOS 장치로 지역화된 속보 보내기</span><span class="sxs-lookup"><span data-stu-id="c96e2-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c96e2-104">Windows 스토어 C#</span><span class="sxs-lookup"><span data-stu-id="c96e2-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="c96e2-105">iOS</span><span class="sxs-lookup"><span data-stu-id="c96e2-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="c96e2-106">개요</span><span class="sxs-lookup"><span data-stu-id="c96e2-106">Overview</span></span>
<span data-ttu-id="c96e2-107">이 항목에서는 Azure 알림 허브의 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 기능을 사용하여 언어 및 장치별로 지역화된 속보 알림을 브로드캐스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="c96e2-108">이 자습서에서는 [Notification Hubs를 사용하여 속보 보내기]에서 만든 iOS 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="c96e2-109">이 자습서를 완료하면 관심 있는 범주를 등록하고, 알림을 받을 언어를 지정하고, 선택한 범주에 대한 푸시 알림만 해당 언어로 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="c96e2-110">이 시나리오는 다음과 같은 두 부분으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="c96e2-111">iOS 앱을 통해 클라이언트 장치는 언어를 지정하고 다른 속보 범주를 구독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="c96e2-112">백 엔드에서 Azure Notification Hubs의 **태그** 및 **템플릿** 기능을 사용하여 알림을 브로드캐스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c96e2-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c96e2-113">Prerequisites</span></span>
<span data-ttu-id="c96e2-114">[Notification Hubs를 사용하여 속보 보내기] 자습서를 이미 완료하고 사용 가능한 코드가 있어야 합니다. 이 자습서는 해당 코드를 기반으로 직접 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="c96e2-115">Visual Studio 2012 이상은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="c96e2-116">템플릿 개념</span><span class="sxs-lookup"><span data-stu-id="c96e2-116">Template concepts</span></span>
<span data-ttu-id="c96e2-117">[Notification Hubs를 사용하여 속보 보내기] 에서는 **태그** 를 사용하여 다른 뉴스 범주에 대한 알림을 구독하는 앱을 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="c96e2-118">하지만 대부분의 앱은 여러 시장을 대상으로 하므로 지역화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="c96e2-119">즉, 알림 자체의 내용을 지역화해서 올바른 장치 집합으로 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="c96e2-120">이 항목에서는 알림 허브의 **템플릿** 기능을 사용하여 지역화된 속보 알림을 쉽게 제공하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="c96e2-121">참고: 지역화된 알림을 보내는 한 가지 방법은 각 태그의 여러 버전을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="c96e2-122">예를 들어 영어, 프랑스어 및 북경어를 지원하려면 세계 뉴스에 대한 3가지 태그 즉, "world_en", "world_fr" 및 "world_ch"가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="c96e2-123">그런 다음 이러한 각 태그로 세계 뉴스의 지역화된 버전을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="c96e2-124">이 항목에서는 템플릿을 사용하여 태그의 확산을 방지하고 여러 메시지를 보낼 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="c96e2-125">높은 수준의 템플릿을 사용하면 특정 장치에서 알림을 받는 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="c96e2-126">템플릿은 앱에서 백 엔드로 보낸 메시지에 포함된 속성을 참조하여 정확한 페이로드 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="c96e2-127">여기서는 모든 지원되는 언어를 포함하는 로캘을 알 수 없는 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="c96e2-128">그런 다음 올바른 속성을 참조하는 템플릿을 사용하여 장치가 등록되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="c96e2-129">예를 들어 프랑스어 뉴스를 등록하려는 iOS 앱은 다음을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="c96e2-130">템플릿은 매우 강력한 기능입니다. 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c96e2-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="c96e2-131">앱 사용자 인터페이스</span><span class="sxs-lookup"><span data-stu-id="c96e2-131">The app user interface</span></span>
<span data-ttu-id="c96e2-132">이제 [Notification Hubs를 사용하여 속보 보내기] 항목에서 만든 속보 앱을 수정하고 템플릿을 사용하여 지역화된 속보를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="c96e2-133">MainStoryboard_iPhone.storyboard에서 지원되는 3가지 언어, 즉 영어, 프랑스어 및 북경어로 분할된 제어를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="c96e2-134">그런 다음 아래와 같이 ViewController.h에 IBOutlet을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="c96e2-135">iOS 앱 빌드</span><span class="sxs-lookup"><span data-stu-id="c96e2-135">Building the iOS app</span></span>
1. <span data-ttu-id="c96e2-136">Notification.h에서 아래와 같이 *retrieveLocale* 메서드를 추가하고 저장 및 구독 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="c96e2-137">Notification.m에서 로캘 매개 변수를 추가하고 사용자 기본값에 저장하여 *storeCategoriesAndSubscribe* 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="c96e2-138">그런 다음 로캘을 포함하도록 *subscribe* 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-138">Then modify the *subscribe* method to include the locale:</span></span>
   
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
   
    <span data-ttu-id="c96e2-139">이제 *registerNativeWithDeviceToken* 대신 *registerTemplateWithDeviceToken* 메서드를 어떻게 사용하고 있는지 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="c96e2-140">템플릿을 등록할 때는 json 템플릿과 템플릿의 이름도 제공해야 합니다(이 앱이 다른 템플릿을 등록할 수 있으므로).</span><span class="sxs-lookup"><span data-stu-id="c96e2-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="c96e2-141">해당 뉴스에 대한 알림을 받도록 할 것이므로 범주를 태그로 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="c96e2-142">사용자 기본 설정에서 로캘을 검색하기 위한 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="c96e2-143">이제 Notifications 클래스를 수정했으므로 ViewController가 새 UISegmentControl을 사용하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="c96e2-144">*viewDidLoad* 메서드에 다음 줄을 추가하여 현재 선택된 로캘을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="c96e2-145">그런 다음 *subscribe* 메서드에서 *storeCategoriesAndSubscribe*에 대한 호출을 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
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
3. <span data-ttu-id="c96e2-146">마지막으로, 앱이 시작될 때 등록을 올바르게 새로 고칠 수 있도록 AppDelegate.m에서 *didRegisterForRemoteNotificationsWithDeviceToken* 메서드를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="c96e2-147">알림의 *subscribe* 메서드에 대한 호출을 다음으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="c96e2-148">(선택 사항) .NET 콘솔 앱에서 지역화된 템플릿 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c96e2-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="c96e2-149">(선택 사항) 장치에서 지역화된 템플릿 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="c96e2-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="c96e2-150">Visual Studio에 액세스할 수 없거나 장치의 앱에서 직접 지역화된 템플릿 알림을 보내는 테스트만 하기를 원하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="c96e2-151">이전 자습서에 정의한 `SendNotificationRESTAPI` 메서드에 지역화된 템플릿 매개 변수를 간단히 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c96e2-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

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




## <a name="next-steps"></a><span data-ttu-id="c96e2-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c96e2-152">Next Steps</span></span>
<span data-ttu-id="c96e2-153">템플릿 사용에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c96e2-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="c96e2-154">[알림 허브를 통해 사용자에게 알림: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="c96e2-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="c96e2-155">[알림 허브를 통해 사용자에게 알림: 모바일 서비스]</span><span class="sxs-lookup"><span data-stu-id="c96e2-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="c96e2-156">[Notification Hubs를 사용하여 속보 보내기]: /manage/services/notification-hubs/breaking-news-ios</span><span class="sxs-lookup"><span data-stu-id="c96e2-156">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
<span data-ttu-id="c96e2-157">[알림 허브를 통해 사용자에게 알림: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="c96e2-157">[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="c96e2-158">[알림 허브를 통해 사용자에게 알림: 모바일 서비스]: /manage/services/notification-hubs/notify-users</span><span class="sxs-lookup"><span data-stu-id="c96e2-158">[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users</span></span>
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
