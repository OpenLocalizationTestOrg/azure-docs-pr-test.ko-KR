---
title: "Web API를 사용하여 푸시 알림에 현재 사용자 등록 | Microsoft Docs"
description: "ASP.NET Web API에서 등록을 수행할 때 Azure 알림 허브를 사용하여 iOS 앱에서 푸시 알림 등록을 요청하는 방법에 대해 알아봅니다."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: fd56bb2dd627b31f00363851a4e76484aa382988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="f28db-103">ASP.NET을 사용하여 푸시 알림에 현재 사용자 등록</span><span class="sxs-lookup"><span data-stu-id="f28db-103">Register the current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f28db-104">iOS</span><span class="sxs-lookup"><span data-stu-id="f28db-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f28db-105">개요</span><span class="sxs-lookup"><span data-stu-id="f28db-105">Overview</span></span>
<span data-ttu-id="f28db-106">이 항목에서는 ASP.NET Web API에서 등록을 수행할 때 Azure 알림 허브를 통해 푸시 알림 등록을 요청하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="f28db-107">이 항목은 [알림 허브를 통해 사용자에게 알림]자습서를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-107">This topic extends the tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="f28db-108">이미 해당 자습서의 필수 단계를 완료하여 인증된 모바일 서비스를 만든 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span></span> <span data-ttu-id="f28db-109">사용자 알림 시나리오에 대한 자세한 내용은 [알림 허브를 통해 사용자에게 알림]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f28db-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="f28db-110">앱 업데이트</span><span class="sxs-lookup"><span data-stu-id="f28db-110">Update your app</span></span>
1. <span data-ttu-id="f28db-111">MainStoryboard_iPhone.storyboard의 개체 라이브러리에서 다음 구성 요소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span></span>
   
   * <span data-ttu-id="f28db-112">**레이블**: "Push to User with Notification Hubs"</span><span class="sxs-lookup"><span data-stu-id="f28db-112">**Label**: "Push to User with Notification Hubs"</span></span>
   * <span data-ttu-id="f28db-113">**레이블**: "InstallationId"</span><span class="sxs-lookup"><span data-stu-id="f28db-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="f28db-114">**레이블**: "User"</span><span class="sxs-lookup"><span data-stu-id="f28db-114">**Label**: "User"</span></span>
   * <span data-ttu-id="f28db-115">**텍스트 필드**: "User"</span><span class="sxs-lookup"><span data-stu-id="f28db-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="f28db-116">**레이블**: "Password"</span><span class="sxs-lookup"><span data-stu-id="f28db-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="f28db-117">**텍스트 필드**: "Password"</span><span class="sxs-lookup"><span data-stu-id="f28db-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="f28db-118">**단추**: "Login"</span><span class="sxs-lookup"><span data-stu-id="f28db-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="f28db-119">이때 스토리보드가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-119">At this point, your storyboard looks like the following:</span></span>
     
      ![][0]
2. <span data-ttu-id="f28db-120">단말기 편집기에서 모든 전환된 컨트롤에 대한 콘센트를 만든 다음 호출하고, 텍스트 필드를 뷰 컨트롤러(대리자)에 연결하고, **로그인** 단추에 대한 **동작**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="f28db-121">**DeviceInfo**라는 클래스를 만들고 다음 코드를 DeviceInfo.h 파일의 인터페이스 섹션에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="f28db-122">다음 코드를 DeviceInfo.m 파일의 구현 섹션에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store the install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="f28db-123">PushToUserAppDelegate.h에서 다음 속성 단일 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-123">In PushToUserAppDelegate.h, add the following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="f28db-124">PushToUserAppDelegate.m의 **didFinishLaunchingWithOptions** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="f28db-125">첫 번째 행은 **DeviceInfo** 단일 항목을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-125">The first line initializes the **DeviceInfo** singleton.</span></span> <span data-ttu-id="f28db-126">두 번째 행은 푸시 알림 등록을 시작합니다. 이미 언급한 것처럼 [Notification Hubs 시작] 자습서를 이미 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="f28db-127">PushToUserAppDelegate.m의 AppDelegate에서 **didRegisterForRemoteNotificationsWithDeviceToken** 메서드를 구현하고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="f28db-128">이 코드는 요청에 대한 장치 토큰을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-128">This sets the device token for the request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f28db-129">이때 이 메서드에 다른 코드가 있어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="f28db-130">**알림 허브 시작** 자습서를 완료할 때 추가된 [registerNativeWithDeviceToken](/manage/services/notification-hubs/get-started-notification-hubs-ios/) 메서드에 대한 호출이 이미 있는 경우 해당 호출을 주석으로 처리하거나 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-130">If you already have a call to the **registerNativeWithDeviceToken** method that was added when you completed the [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="f28db-131">PushToUserAppDelegate.m 파일에서 다음 처리기 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-131">In the PushToUserAppDelegate.m file, add the following handler method:</span></span>
   
   * <span data-ttu-id="f28db-132">응용 프로그램 (void):(UIApplication *) 응용 프로그램 didReceiveRemoteNotification:(NSDictionary *) 사용자 정보 {NSLog (@"% @", 사용자 정보);   UIAlertView * 경고 = [[UIAlertView alloc] initWithTitle:@"Notification" 메시지: [사용자 정보 objectForKey:@"inAppMessage"] 대리자: nil cancelButtonTitle: @"확인" otherButtonTitles:nil, nil];   [경고 표시]; }</span><span class="sxs-lookup"><span data-stu-id="f28db-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="f28db-133">이 메서드는 앱이 실행되고 있는 동안 알림을 받으면 UI에 경고를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-133">This method displays an alert in the UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="f28db-134">PushToUserViewController.m 파일을 열고 다음 구현에 키보드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="f28db-135">PushToUserViewController.m 파일의 **viewDidLoad** 메서드에서 다음과 같이 installationId 레이블을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="f28db-136">PushToUserViewController.m의 인터페이스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-136">Add the following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="f28db-137">그 후에 다음 구현을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-137">Then, add the following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="f28db-138">XCode로 만든 **login** 처리기 메서드에 다음 코드를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-138">Copy the following code into the **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="f28db-139">이 메서드는 푸시 알림에 대한 설치 ID와 채널을 모두 가져온 다음, 알림 허브에서 등록을 만드는 인증된 웹 API 메서드에 장치 유형과 함께 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="f28db-140">이 웹 API는 [알림 허브를 통해 사용자에게 알림]에서 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="f28db-141">클라이언트 앱이 업데이트되었으므로 [알림 허브를 통해 사용자에게 알림] 으로 돌아가서 알림 허브를 사용하여 알림을 보내도록 모바일 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f28db-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
<span data-ttu-id="f28db-142">[알림 허브를 통해 사용자에게 알림]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="f28db-142">[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span></span>

<span data-ttu-id="f28db-143">[Notification Hubs 시작]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span><span class="sxs-lookup"><span data-stu-id="f28db-143">[Get Started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span></span>
