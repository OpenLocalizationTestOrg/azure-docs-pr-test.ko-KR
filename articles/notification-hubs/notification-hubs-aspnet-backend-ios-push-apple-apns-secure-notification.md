---
title: "Azure 알림 허브 보안 푸시"
description: "Azure에서 iOS 앱에 보안 푸시 알림을 보내는 방법에 대해 알아봅니다. 코드 샘플은 Objective-C 및 C#으로 작성되었습니다."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="eed93-104">Azure 알림 허브 보안 푸시</span><span class="sxs-lookup"><span data-stu-id="eed93-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eed93-105">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="eed93-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="eed93-106">iOS</span><span class="sxs-lookup"><span data-stu-id="eed93-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="eed93-107">Android</span><span class="sxs-lookup"><span data-stu-id="eed93-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="eed93-108">개요</span><span class="sxs-lookup"><span data-stu-id="eed93-108">Overview</span></span>
<span data-ttu-id="eed93-109">Microsoft Azure의 푸시 알림 지원을 통해 사용하기 쉬운 다중 플랫폼 및 규모 확장 푸시 인프라에 액세스할 수 있어, 모바일 플랫폼용 소비자 응용 프로그램 및 엔터프라이즈 응용 프로그램 모두에 대한 푸시 알림을 매우 간단하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="eed93-110">규제나 보안 제약 조건 때문에 응용 프로그램의 알림에 표준 푸시 알림 인프라를 통해 전송할 수 없는 어떤 항목을 포함해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="eed93-111">이 자습서에서는 클라이언트 장치와 앱 백 엔드 간에 인증된 보안 연결을 통해 중요한 정보를 전송하여 동일한 경험을 얻는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="eed93-112">개략적으로 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="eed93-113">앱 백 엔드:</span><span class="sxs-lookup"><span data-stu-id="eed93-113">The app back-end:</span></span>
   * <span data-ttu-id="eed93-114">백 엔드 데이터베이스에 보안 페이로드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="eed93-115">이 알림의 ID를 장치에 보냅니다(보안 정보는 전송되지 않음).</span><span class="sxs-lookup"><span data-stu-id="eed93-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="eed93-116">알림 수신 시 장치의 앱:</span><span class="sxs-lookup"><span data-stu-id="eed93-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="eed93-117">장치가 보안 페이로드를 요청하는 백 엔드에 접속합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="eed93-118">앱이 장치에서 페이로드를 알림으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="eed93-119">앞의 흐름과 이 자습서에서는 사용자가 로그인한 후 장치가 인증 토큰을 로컬 저장소에 저장한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="eed93-120">이렇게 하면 장치가 이 토큰을 사용하여 알림의 보안 페이로드를 검색할 수 있으므로 매우 원활한 환경이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="eed93-121">응용 프로그램이 인증 토큰을 장치에 저장하지 않거나 이 토큰이 만료될 수 없으면 알림 수신 시 장치 앱은 사용자에게 앱을 시작할지 묻는 메시지가 포함된 일반 알림을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="eed93-122">그리고 나서 앱은 사용자를 인증하고 알림 페이로드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="eed93-123">이 보안 푸시 자습서에서는 푸시 알림을 안전하게 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="eed93-124">이 자습서는 [사용자에게 알림](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) 자습서를 기반으로 빌드되므로 해당 자습서의 단계를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="eed93-125">이 자습서에서는 [알림 허브 시작(iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다</span><span class="sxs-lookup"><span data-stu-id="eed93-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="eed93-126">iOS 프로젝트 수정</span><span class="sxs-lookup"><span data-stu-id="eed93-126">Modify the iOS project</span></span>
<span data-ttu-id="eed93-127">알림의 *id* 만 보내도록 앱 백 엔드를 수정했으므로 해당 알림을 처리하고 백 엔드를 콜백하여 표시할 보안 메시지를 검색하도록 iOS 앱을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="eed93-128">이 목표를 달성하려면 앱 백 엔드에서 보안 콘텐츠를 검색하는 논리를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="eed93-129">**AppDelegate.m**에서 앱이 자동 알림을 등록하여 백 엔드에서 전송된 알림 ID를 처리하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="eed93-130">didFinishLaunchingWithOptions에 **UIRemoteNotificationTypeNewsstandContentAvailability** 옵션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="eed93-131">**AppDelegate.m** 에서 맨 위에 다음 선언과 함께 구현 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="eed93-132">그리고 나서 구현 섹션에 다음 코드를 추가하여 자리 표시자 `{back-end endpoint}` 를 이전에 얻은 백 엔드의 끝점으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="eed93-133">이제 들어오는 알림을 처리하고 위의 메서드를 사용하여 표시할 콘텐츠를 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="eed93-134">먼저 푸시 알림을 받을 때 iOS 앱이 백그라운드에서 실행될 수 있도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="eed93-135">**XCode**의 왼쪽 패널에서 앱 프로젝트를 선택하고 가운데 창의 **대상** 섹션에서 기본 앱 대상을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="eed93-136">그리고 가운데 창의 맨 위에서 **기능** 탭을 클릭하고 **원격 알림** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="eed93-137">**AppDelegate.m** 에서 다음 메서드를 추가하여 푸시 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="eed93-138">백 엔드에 의해 거부되거나 인증 헤더 속성이 누락되는 경우를 처리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="eed93-139">이러한 경우의 특수 처리는 대부분 대상 사용자 환경에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="eed93-140">한 가지 옵션은 실제 알림을 검색하기 위해 사용자가 인증을 받도록 하는 일반 프롬프트가 포함된 알림을 표시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="eed93-141">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="eed93-141">Run the Application</span></span>
<span data-ttu-id="eed93-142">응용 프로그램을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="eed93-143">XCode에서는 실제 iOS 장치에서 앱을 실행합니다(푸시 알림은 시뮬레이터에서 작동하지 않음).</span><span class="sxs-lookup"><span data-stu-id="eed93-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="eed93-144">iOS 앱 UI에서 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="eed93-145">이는 임의 문자열일 수 있지만 같은 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="eed93-146">iOS 앱 UI에서 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="eed93-147">그리고 나서 **푸시 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-147">Then click **Send push**.</span></span> <span data-ttu-id="eed93-148">알림 센터에 보안 알림이 표시되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eed93-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
