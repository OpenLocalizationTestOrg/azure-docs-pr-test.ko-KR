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
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="4e78b-103">알림 허브를 사용하여 속보 보내기</span><span class="sxs-lookup"><span data-stu-id="4e78b-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="4e78b-104">개요</span><span class="sxs-lookup"><span data-stu-id="4e78b-104">Overview</span></span>
<span data-ttu-id="4e78b-105">이 항목에서는 Azure 알림 허브를 사용하여 iOS 앱에 속보 알림을 브로드캐스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="4e78b-106">완료하면, 관심이 있는 속보 범주를 등록하고 해당 범주의 푸시 알림만 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="4e78b-107">이 시나리오는 RSS 수집기, 음악 애호가를 위한 앱 등 이전에 관심을 보인 사용자 그룹에 알림을 보내야 하는 많은 앱에 공통된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="4e78b-108">브로드캐스트 시나리오를 사용하려면 알림 허브에서 등록을 만들 때 하나 이상의 *태그*를 포함하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="4e78b-109">태그에 알림이 전송되면 태그에 대해 등록된 모든 장치에서 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="4e78b-110">태그는 단순히 문자열이므로 사전에 프로비전해야 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="4e78b-111">태그에 대한 자세한 내용은 [알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4e78b-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e78b-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4e78b-112">Prerequisites</span></span>
<span data-ttu-id="4e78b-113">이 항목은 [Notification Hubs 시작][get-started]에서 만든 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="4e78b-114">이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="4e78b-115">앱에 범주 선택 추가</span><span class="sxs-lookup"><span data-stu-id="4e78b-115">Add category selection to the app</span></span>
<span data-ttu-id="4e78b-116">첫 번째 단계는 기존의 스토리보드에 사용자가 등록할 범주를 선택할 수 있도록 하는 UI 요소를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="4e78b-117">사용자가 선택한 범주는 장치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="4e78b-118">앱을 시작하면 장치 등록이 선택한 범주와 함께 태그로서 알림 허브에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="4e78b-119">MainStoryboard_iPhone.storyboard의 개체 라이브러리에서 다음 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="4e78b-120">"Breaking News" 텍스트가 포함된 레이블</span><span class="sxs-lookup"><span data-stu-id="4e78b-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="4e78b-121">"World", "Politics", "Business", "Technology", "Science", "Sports" 범주 텍스트가 포함된 레이블</span><span class="sxs-lookup"><span data-stu-id="4e78b-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="4e78b-122">범주당 하나씩인 6개의 스위치는 각 스위치 **상태**를 기본적으로 **Off(꺼짐)**가 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="4e78b-123">"Subscribe" 단추</span><span class="sxs-lookup"><span data-stu-id="4e78b-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="4e78b-124">스토리보드는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="4e78b-125">단말기 편집기에서 모든 스위치에 대한 콘센트를 만든 다음 "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="4e78b-126">"subscribe" 단추에 대한 동작을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="4e78b-127">ViewController.h에는 다음이 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="4e78b-128">`Notifications`라는 새 **Cocoa Touch 클래스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="4e78b-129">다음 코드를 Notifications.h 파일의 인터페이스 섹션에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="4e78b-130">다음 import 지시문을 Notifications.m에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="4e78b-131">다음 코드를 Notifications.m 파일의 구현 섹션에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
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



    <span data-ttu-id="4e78b-132">이 클래스는 로컬 저장소를 사용하여 이 장치에서 받을 뉴스의 범주를 저장하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="4e78b-133">또한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 등록을 사용하여 이러한 범주에 등록하는 메서드도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="4e78b-134">AppDelegate.h 파일에서 Notifications.h에 대한 import 문을 추가하고 알림 클래스의 인스턴스에 대한 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="4e78b-135">AppDelegate.m의 **didFinishLaunchingWithOptions** 메서드에서 메서드 시작 부분에 알림 인스턴스를 초기화하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="4e78b-136">`HUBNAME`과 `HUBLISTENACCESS`(hubinfo.h에 정의됨)는 `<hub name>` 및 `<connection string with listen access>` 자리 표시자를 알림 허브 이름과 앞서 얻었던 *DefaultListenSharedAccessSignature*의 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="4e78b-137">클라이언트 앱과 함께 배포되는 자격 증명은 일반적으로 안전하지 않기 때문에 클라이언트 앱과 함께 listen access용 키만 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="4e78b-138">Listen access를 통해 앱에서 알림을 등록할 수 있지만, 기존 등록을 수정할 수 없으며 알림을 전송할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="4e78b-139">안전한 백 엔드 서비스에서 알림을 보내고 기존 등록을 변경하는 데에는 모든 권한 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="4e78b-140">AppDelegate.m의 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드에서 메서드의 코드를 다음 코드로 바꿔 알림 클래스에 장치 토큰을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="4e78b-141">알림 클래스는 범주를 사용하여 알림에 대해 등록을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="4e78b-142">사용자가 범주 선택 항목을 변경하는 경우 **구독** 단추에 대한 응답으로 `subscribeWithCategories` 메서드를 호출하여 범주 선택 항목을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4e78b-143">APNS(Apple Push Notification Service)에서 할당하는 장치 토큰은 언제든지 변경될 수 있으므로 알림 실패를 피하려면 알림을 자주 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="4e78b-144">이 예제에서는 앱이 시작될 때마다 알림을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="4e78b-145">자주(하루 두 번 이상) 실행되는 앱에서는 이전 등록 이후 만 하루가 지나지 않은 경우 대역폭 유지를 위한 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
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

    <span data-ttu-id="4e78b-146">이때 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드에 다른 코드가 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="4e78b-147">다음 방법 이미 있어야 AppDelegate.m 완료는 [알림 허브 시작] [ get-started] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="4e78b-148">그렇지 않은 경우 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-148">If not, add them.</span></span>
   
    <span data-ttu-id="4e78b-149">-(void) MessageBox:(NSString *) 제목 메시지:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="4e78b-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="4e78b-150">}</span><span class="sxs-lookup"><span data-stu-id="4e78b-150">}</span></span>
   
   * <span data-ttu-id="4e78b-151">응용 프로그램 (void):(UIApplication *) 응용 프로그램 didReceiveRemoteNotification: (NSDictionary *) 사용자 정보 {NSLog (@"% @", 사용자 정보);   [메시지 자체 MessageBox:@"Notification": [[사용자 정보 objectForKey:@"aps"] valueForKey:@"alert"]]; }</span><span class="sxs-lookup"><span data-stu-id="4e78b-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="4e78b-152">이 메서드는 단일 **UIAlert**를 표시하여 앱이 실행 중일 때 수신된 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="4e78b-153">ViewController.m에서 AppDelegate.h에 대해 import 문을 추가하고 다음 코드를 XCode 생성 **구독** 메서드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="4e78b-154">이 코드는 사용자 인터페이스에서 사용자가 선택한 새 범주 태그를 사용하도록 알림 등록을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
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
   
   <span data-ttu-id="4e78b-155">이 메서드는 범주의 **NSMutableArray**를 만들고 **Notifications** 클래스를 사용하여, 로컬 저장소에 목록을 저장하고 알림 허브에 해당 태그를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="4e78b-156">범주가 변경되면 새 범주로 등록이 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="4e78b-157">ViewController.m에서 **viewDidLoad** 메서드에 다음 코드를 추가하여 이전에 저장한 범주를 기반으로 사용자 인터페이스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="4e78b-158">이제 앱은 앱이 시작할 때마다 알림 허브에 등록하는 데 사용한 장치 로컬 저장소에 범주 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="4e78b-159">사용자는 런타임 시 범주 선택 사항을 변경하고 **구독** 메서드를 클릭하여 장치에 대한 등록을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="4e78b-160">다음으로, 앱 자체에서 직접 속보 알림을 보내도록 앱을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="4e78b-161">(선택 사항) 태그가 지정된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4e78b-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="4e78b-162">Visual Studio에 액세스할 수 없는 경우 다음 섹션으로 건너뛰고 앱 자체에서 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="4e78b-163">또한 알림 허브에 대한 디버그 탭을 사용하여 [Azure 클래식 포털] 에서 적절한 템플릿 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="4e78b-164">(선택 사항) 장치에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="4e78b-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="4e78b-165">일반적으로 백 엔드 서비스에서 알림을 보내지만 속보 알림은 앱 자체에서 직접 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="4e78b-166">이 업데이트 될 작업을 수행 하는 `SendNotificationRESTAPI` 에 정의한 메서드는 [알림 허브 시작] [ get-started] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="4e78b-167">ViewController.m에서 범주 태그에 대한 매개 변수를 허용하고 적절한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 알림을 보내도록 다음과 같이 `SendNotificationRESTAPI` 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
2. <span data-ttu-id="4e78b-168">ViewController.m에서 다음 코드에 표시된 것처럼 **알림 보내기** 작업을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="4e78b-169">그러면 개별적으로 각 태그를 사용하여 알림을 보내고 여러 플랫폼으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

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



1. <span data-ttu-id="4e78b-170">프로젝트를 다시 빌드하고 빌드 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="4e78b-171">앱 실행 및 알림 생성</span><span class="sxs-lookup"><span data-stu-id="4e78b-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="4e78b-172">실행 단추를 눌러 프로젝트를 빌드하고 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="4e78b-173">구독할 속보 옵션을 선택하고 **구독** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="4e78b-174">알림 구독을 나타내는 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="4e78b-175">**구독**을 선택하면 앱은 선택한 범주를 태그로 변환하고 알림 허브에서 선택한 태그에 대한 새로운 장치 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="4e78b-176">속보로 보낼 메시지를 입력하고 **알림 보내기** 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="4e78b-177">또는 .NET 콘솔 앱을 실행하여 알림을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="4e78b-178">속보를 구독하는 각 장치에서 방금 보낸 속보 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e78b-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4e78b-179">Next steps</span></span>
<span data-ttu-id="4e78b-180">이 자습서에서는 범주별로 속보를 브로드캐스트하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="4e78b-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="4e78b-181">이제 기타 고급 알림 허브 시나리오를 다루는 다음 자습서 중 하나를 완료해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4e78b-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="4e78b-182">**[Notification Hubs를 사용하여 지역화된 속보 브로드캐스트]**</span><span class="sxs-lookup"><span data-stu-id="4e78b-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="4e78b-183">지역화된 알림을 보낼 수 있도록 속보 앱을 확장하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4e78b-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="4e78b-184">[Notification Hubs를 사용하여 지역화된 속보 브로드캐스트]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="4e78b-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="4e78b-185">[Azure 클래식 포털]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="4e78b-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
