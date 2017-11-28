---
title: "Azure 알림 허브와 aaaSending 푸시 알림 tooiOS | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브 toosend toouse 알림 tooan iOS 응용 프로그램을 강제 하는 방법을 배웁니다."
services: notification-hubs
documentationcenter: ios
keywords: "푸시 알림, 푸시알림,ios 푸시 알림"
author: ysxu
manager: erikre
editor: 
ms.assetid: b7fcd916-8db8-41a6-ae88-fc02d57cb914
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: d8bb47fee4c229b3ed2a7a4dbff25a56a7a7d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-tooios-with-azure-notification-hubs"></a><span data-ttu-id="6bc4e-104">Azure 알림 허브 푸시 알림을 tooiOS 보내기</span><span class="sxs-lookup"><span data-stu-id="6bc4e-104">Sending push notifications tooiOS with Azure Notification Hubs</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6bc4e-105">개요</span><span class="sxs-lookup"><span data-stu-id="6bc4e-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="6bc4e-106">toocomplete이이 자습서에서는 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6bc4e-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6bc4e-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="6bc4e-109">이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooan iOS 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span> <span data-ttu-id="6bc4e-110">Hello를 사용 하 여 푸시 알림을 수신 하는 비어 있는 iOS 앱을 만듭니다 [Apple 푸시 알림 서비스 (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-110">You'll create a blank iOS app that receives push notifications by using hello [Apple Push Notification service (APNs)](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html).</span></span> 

<span data-ttu-id="6bc4e-111">수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6bc4e-112">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="6bc4e-112">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="6bc4e-113">이 자습서를 완료 하는 hello 코드 있습니다 [GitHub에서](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-113">hello completed code for this tutorial can be found [on GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/iOS/GetStartedNH/GetStarted).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6bc4e-114">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6bc4e-114">Prerequisites</span></span>
<span data-ttu-id="6bc4e-115">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6bc4e-116">[모바일 서비스 iOS SDK 버전 1.2.4]</span><span class="sxs-lookup"><span data-stu-id="6bc4e-116">[Mobile Services iOS SDK version 1.2.4]</span></span>
* <span data-ttu-id="6bc4e-117">[Xcode]</span><span class="sxs-lookup"><span data-stu-id="6bc4e-117">Latest version of [Xcode]</span></span>
* <span data-ttu-id="6bc4e-118">iOS 8(이상) 지원 장치</span><span class="sxs-lookup"><span data-stu-id="6bc4e-118">An iOS 8 (or later version)-capable device</span></span>
* <span data-ttu-id="6bc4e-119">[Apple 개발자 프로그램](https://developer.apple.com/programs/) 멤버 자격</span><span class="sxs-lookup"><span data-stu-id="6bc4e-119">[Apple Developer Program](https://developer.apple.com/programs/) membership.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="6bc4e-120">푸시 알림에 대 한 구성 요구 사항 때문에 배포 하 고 hello iOS 시뮬레이터 대신 실제 iOS 장치 (iPhone 또는 iPad)에 푸시 알림을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-120">Because of configuration requirements for push notifications, you must deploy and test push notifications on a physical iOS device (iPhone or iPad) instead of hello iOS Simulator.</span></span>
  > 
  > 

<span data-ttu-id="6bc4e-121">이 자습서를 완료해야 다른 모든 iOS 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub-for-ios-push-notifications"></a><span data-ttu-id="6bc4e-122">iOS 푸시 알림에 대해 알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="6bc4e-122">Configure your Notification Hub for iOS push notifications</span></span>
<span data-ttu-id="6bc4e-123">이 섹션에서는 새 알림 허브 만들기 및 hello를 사용 하 여 APNS를 사용 하 여 인증을 구성 하는 과정을 설명 **.p12** 사용자가 만든 푸시 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="6bc4e-124">이미 만든 알림 허브 toouse 원하는 toostep 5를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">

<li>

<p><span data-ttu-id="6bc4e-125">Hello 클릭 <b>Notification Services</b> hello 단추 <b>설정</b> 블레이드에서 다음을 선택 <b>APNS (Apple)</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-125">Click hello <b>Notification Services</b> button in hello <b>Settings</b> blade, then select <b>Apple (APNS)</b>.</span></span> <span data-ttu-id="6bc4e-126">클릭 <b>인증서 업로드</b> 및 선택 hello <b>.p12</b> 앞에서 내보낸 파일.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-126">Click on <b>Upload Certificate</b> and select hello <b>.p12</b> file that you exported earlier.</span></span> <span data-ttu-id="6bc4e-127">또한 hello 올바른 암호를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-127">Make sure you also specify hello correct password.</span></span></p>

<p><span data-ttu-id="6bc4e-128">있는지 tooselect 확인 <b>샌드박스</b> 때문에이 개발을 위한 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-128">Make sure tooselect <b>Sandbox</b> mode since this is for development.</span></span> <span data-ttu-id="6bc4e-129">만 hello를 사용 하 여 <b>프로덕션</b> hello 스토어에서 앱을 구매한 toosend 푸시 알림을 toousers 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-129">Only use hello <b>Production</b> if you want toosend push notifications toousers who purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="6bc4e-130">&emsp;&emsp;&emsp;&emsp;![Azure 포털에서 APNS 구성](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span><span class="sxs-lookup"><span data-stu-id="6bc4e-130">&emsp;&emsp;&emsp;&emsp;![Configure APNS in Azure Portal](./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png)</span></span>

&emsp;&emsp;&emsp;&emsp;![Azure 포털에서 APNS 인증 구성](./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png)

<span data-ttu-id="6bc4e-132">알림 허브는 이제 구성 된 toowork apns, 그리고 푸시 알림을 보낼 및 hello 연결 문자열 tooregister 응용 프로그램을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-132">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-ios-app-toonotification-hubs"></a><span data-ttu-id="6bc4e-133">IOS 앱 tooNotification 허브 연결</span><span class="sxs-lookup"><span data-stu-id="6bc4e-133">Connect your iOS app tooNotification Hubs</span></span>
1. <span data-ttu-id="6bc4e-134">Xcode에서 새 iOS 프로젝트를 만들고 hello 선택 **단일 보기 응용 프로그램** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-134">In Xcode, create a new iOS project and select hello **Single View Application** template.</span></span>
   
    ![Xcode - 단일 보기 응용 프로그램][8]
    
2. <span data-ttu-id="6bc4e-136">새 프로젝트에 대 한 hello 옵션을 설정할 때 동일한 toouse hello 있는지 확인 **제품 이름** 및 **조직 식별자** hello Apple 개발자에서 hello 번들 ID를 이전에 설정한 때 사용 했는지 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-136">When setting hello options for your new project, make sure toouse hello same **Product Name** and **Organization Identifier** that you used when you previously set hello bundle ID on hello Apple Developer portal.</span></span>
   
    ![Xcode - 프로젝트 옵션][11]
    
3. <span data-ttu-id="6bc4e-138">아래 **대상**프로젝트 이름을 클릭 하 고 hello **빌드 설정** 탭을 확장 하 고 **코드 서명 Id**, 그 다음 **디버그**, 코드 서명 id를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-138">Under **Targets**, click your project name, click hello **Build Settings** tab and expand **Code Signing Identity**, and then under **Debug**, set your code-signing identity.</span></span> <span data-ttu-id="6bc4e-139">설정/해제 **수준** 에서 **기본** 너무**모든**, 설정 및 **프로 비전 프로필** toohello 이전에 만든 프로필을 프로 비전 .</span><span class="sxs-lookup"><span data-stu-id="6bc4e-139">Toggle **Levels** from **Basic** too**All**, and set **Provisioning Profile** toohello provisioning profile that you created previously.</span></span>
   
    <span data-ttu-id="6bc4e-140">새로운 Xcode에서 만든 프로필을 프로 비전 하는 hello 보이지 않으면 서명 id에 대 한 hello 프로필을 새로 고쳐 보십시오.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-140">If you don't see hello new provisioning profile that you created in Xcode, try refreshing hello profiles for your signing identity.</span></span> <span data-ttu-id="6bc4e-141">클릭 **Xcode** hello 메뉴 모음에서 **기본 설정**, hello 클릭 **계정** hello 탭에서 **세부 정보 보기** 단추를 클릭 하면 id를 서명 및 hello 오른쪽 아래 모서리에 hello 새로 고침 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-141">Click **Xcode** on hello menu bar, click **Preferences**, click hello **Account** tab, click hello **View Details** button, click your signing identity, and then click hello refresh button in hello bottom-right corner.</span></span>
   
    ![Xcode - 프로비전 프로필][9]
4. <span data-ttu-id="6bc4e-143">Hello 다운로드 [모바일 서비스 iOS SDK 버전 1.2.4] 고 hello 파일 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-143">Download hello [Mobile Services iOS SDK version 1.2.4] and unzip hello file.</span></span> <span data-ttu-id="6bc4e-144">Xcode에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 hello 클릭 **파일을 추가** 옵션 tooadd hello **WindowsAzureMessaging.framework** 폴더 tooyour Xcode 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-144">In Xcode, right-click your project and click hello **Add Files to** option tooadd hello **WindowsAzureMessaging.framework** folder tooyour Xcode project.</span></span> <span data-ttu-id="6bc4e-145">**필요한 경우 항목 복사**를 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-145">Select **Copy items if needed**, and then click **Add**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6bc4e-146">hello 알림 허브 SDK bitcode Xcode 7에서 현재 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-146">hello notification hubs SDK does not currently support bitcode on Xcode 7.</span></span>  <span data-ttu-id="6bc4e-147">설정 해야 **사용 Bitcode** 너무**아니요** hello에 **빌드 옵션** 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-147">You must set **Enable Bitcode** too**No** in hello **Build Options** for your project.</span></span>
   > 
   > 
   
    ![Azure SDK 압축 해제][10]
5. <span data-ttu-id="6bc4e-149">라는 새 헤더 파일 tooyour 프로젝트 추가 `HubInfo.h`합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-149">Add a new header file tooyour project named `HubInfo.h`.</span></span> <span data-ttu-id="6bc4e-150">이 파일에서는 알림 허브에 대 한 hello 상수를 보관 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-150">This file will hold hello constants for your notification hub.</span></span>  <span data-ttu-id="6bc4e-151">Hello 다음 정의 추가 하 고 hello 문자열 리터럴 자리 표시자를 바꿉니다 프로그램 *허브 이름* 및 hello *DefaultListenSharedAccessSignature* 앞에서 설명한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-151">Add hello following definitions and replace hello string literal placeholders with your *hub name* and hello *DefaultListenSharedAccessSignature* that you noted earlier.</span></span>
   
        #ifndef HubInfo_h
        #define HubInfo_h
   
            #define HUBNAME @"<Enter hello name of your hub>"
            #define HUBLISTENACCESS @"<Enter your DefaultListenSharedAccess connection string"
   
        #endif /* HubInfo_h */
6. <span data-ttu-id="6bc4e-152">Open 프로그램 `AppDelegate.h` 파일 추가 import 지시문 뒤 hello:</span><span class="sxs-lookup"><span data-stu-id="6bc4e-152">Open your `AppDelegate.h` file add hello following import directives:</span></span>
   
         #import <WindowsAzureMessaging/WindowsAzureMessaging.h> 
         #import "HubInfo.h"
7. <span data-ttu-id="6bc4e-153">사용자 `AppDelegate.m file`, hello 코드 hello에 다음 추가 `didFinishLaunchingWithOptions` iOS 버전을 기반으로 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-153">In your `AppDelegate.m file`, add hello following code in hello `didFinishLaunchingWithOptions` method based on your version of iOS.</span></span> <span data-ttu-id="6bc4e-154">이 코드는 APNS로 장치 핸들을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-154">This code registers your device handle with APNs:</span></span>
   
    <span data-ttu-id="6bc4e-155">iOS 8의 경우</span><span class="sxs-lookup"><span data-stu-id="6bc4e-155">For iOS 8:</span></span>
   
         UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                UIUserNotificationTypeAlert | UIUserNotificationTypeBadge categories:nil];
   
        [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
   
    <span data-ttu-id="6bc4e-156">IOS 버전 이전 too8에 대 한:</span><span class="sxs-lookup"><span data-stu-id="6bc4e-156">For iOS versions prior too8:</span></span>
   
         [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
8. <span data-ttu-id="6bc4e-157">동일한 파일 hello에 hello 다음 메서드를 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-157">In hello same file, add hello following methods.</span></span> <span data-ttu-id="6bc4e-158">이 코드는 HubInfo.h에 지정 된 hello 연결 정보를 사용 하 여 toohello 알림 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-158">This code connects toohello notification hub using hello connection information you specified in HubInfo.h.</span></span> <span data-ttu-id="6bc4e-159">그런 다음 hello 알림 허브 알림을 보낼 수 있도록 hello 장치 토큰 toohello 알림 허브를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-159">It then gives hello device token toohello notification hub so that hello notification hub can send notifications:</span></span>
   
        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *) deviceToken {
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:HUBLISTENACCESS
                                        notificationHubPath:HUBNAME];
   
            [hub registerNativeWithDeviceToken:deviceToken tags:nil completion:^(NSError* error) {
                if (error != nil) {
                    NSLog(@"Error registering for notifications: %@", error);
                }
                else {
                    [self MessageBox:@"Registration Status" message:@"Registered"];
                }
            }];
        }
   
        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }
9. <span data-ttu-id="6bc4e-160">동일한 파일 hello 하 hello 메서드 toodisplay 다음 추가 **UIAlert** hello 앱 활성 상태인 동안 hello 알림이 수신 되는 경우:</span><span class="sxs-lookup"><span data-stu-id="6bc4e-160">In hello same file, add hello following method toodisplay a **UIAlert** if hello notification is received while hello app is active:</span></span>

        - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
            NSLog(@"%@", userInfo);
            [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
        }

1. <span data-ttu-id="6bc4e-161">빌드하고에 없는 오류 프로그램 장치 tooverify hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-161">Build and run hello app on your device tooverify that there are no failures.</span></span>

## <a name="send-test-push-notifications"></a><span data-ttu-id="6bc4e-162">테스트 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="6bc4e-162">Send test push notifications</span></span>
<span data-ttu-id="6bc4e-163">Hello에 푸시 알림을 전송 하 여 앱에서 알림 받기 테스트할 수 [Azure 포털] hello를 통해 **문제 해결** hello 허브 블레이드에서 섹션 (hello를 사용 하 여 *테스트보내기* 옵션).</span><span class="sxs-lookup"><span data-stu-id="6bc4e-163">You can test receiving notifications in your app by sending push notifications in hello [Azure Portal] via hello **Troubleshooting** section in hello hub blade (use hello *Test Send* option).</span></span>

![Azure 포털 - 보내기 테스트][30]

[!INCLUDE [notification-hubs-sending-notifications-from-the-portal](../../includes/notification-hubs-sending-notifications-from-the-portal.md)]

## <a name="optional-send-push-notifications-from-hello-app"></a><span data-ttu-id="6bc4e-165">(선택 사항) Hello 응용 프로그램에서 푸시 알림을 보내는합니다</span><span class="sxs-lookup"><span data-stu-id="6bc4e-165">(Optional) Send push notifications from hello app</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6bc4e-166">이 예에서는 hello 클라이언트 앱에서 알림을 보낼 학습 목적 으로만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-166">This example of sending notifications from hello client app is provided for learning purposes only.</span></span> <span data-ttu-id="6bc4e-167">이 경우 hello 해야 하므로 `DefaultFullSharedAccessSignature` toobe hello 클라이언트 응용 프로그램에 있는, 사용자 수 얻을 있는 액세스 권한이 없는 toosend 알림 tooyour 클라이언트 알림 허브 toohello 위험에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-167">Since this will require hello `DefaultFullSharedAccessSignature` toobe present on hello client app, it exposes your notification hub toohello risk that a user may gain access toosend unauthorized notifications tooyour clients.</span></span>
> 
> 

<span data-ttu-id="6bc4e-168">이 섹션에서는 방법의 예를 제공 하려는 경우 응용 프로그램 내에서 푸시 알림을 toosend, toodo REST 인터페이스 hello 사용 하 여이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-168">If you want toosend push notifications from within an app, this section provides an example of how toodo this using hello REST interface.</span></span>

1. <span data-ttu-id="6bc4e-169">Xcode에서 엽니다 `Main.storyboard` hello hello 앱에서 hello 개체 라이브러리 tooallow hello 사용자 푸시 알림을 toosend에서 다음과 같은 UI 구성 요소가 추가:</span><span class="sxs-lookup"><span data-stu-id="6bc4e-169">In Xcode, open `Main.storyboard` and add hello following UI components from hello object library tooallow hello user toosend push notifications in hello app:</span></span>
   
   * <span data-ttu-id="6bc4e-170">레이블 텍스트가 없는 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-170">A label with no label text.</span></span> <span data-ttu-id="6bc4e-171">알림 전송에서 사용 되는 tooreport 오류 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-171">It will be used tooreport errors in sending notifications.</span></span> <span data-ttu-id="6bc4e-172">hello **줄** 너무 속성을 설정 해야**0** 제한 된 toohello 오른쪽 및 왼쪽된 여백 및 hello 보기의 hello 위쪽 크기 자동으로 조정할지 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-172">hello **Lines** property should be set too**0** so that it will automatically size constrained toohello right and left margins and hello top of hello view.</span></span>
   * <span data-ttu-id="6bc4e-173">와 함께 텍스트 필드 **자리 표시자** 텍스트가 너무 설정**알림 메시지를 입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-173">A text field with **Placeholder** text set too**Enter Notification Message**.</span></span> <span data-ttu-id="6bc4e-174">아래와 같이 hello 레이블 바로 아래 hello 필드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-174">Constrain hello field just below hello label as shown below.</span></span> <span data-ttu-id="6bc4e-175">Hello 콘센트 대리자로 hello 뷰-컨트롤러를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-175">Set hello View Controller as hello outlet delegate.</span></span>
   * <span data-ttu-id="6bc4e-176">단추가 **알림 보내기** hello 텍스트 필드 바로 아래 및 hello 가로 센터에서 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-176">A button titled **Send Notification** constrained just below hello text field and in hello horizontal center.</span></span>
     
     <span data-ttu-id="6bc4e-177">hello 보기는 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-177">hello view should look as follows:</span></span>
     
     ![Xcode 디자이너][32]
2. <span data-ttu-id="6bc4e-179">[추가 콘센트](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) hello 레이블 및 텍스트 필드에서 보기를 연결 하 고 업데이트 프로그램 `interface` 정의 toosupport `UITextFieldDelegate` 및 `NSXMLParserDelegate`합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-179">[Add outlets](https://developer.apple.com/library/ios/recipes/xcode_help-IB_connections/chapters/CreatingOutlet.html) for hello label and text field connected your view, and update your `interface` definition toosupport `UITextFieldDelegate` and `NSXMLParserDelegate`.</span></span> <span data-ttu-id="6bc4e-180">Hello REST API를 호출 하 고 hello 응답을 구문 분석 toohelp 지원 아래에 표시 된 hello 3 개의 속성 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-180">Add hello three property declarations shown below toohelp support calling hello REST API and parsing hello response.</span></span>
   
    <span data-ttu-id="6bc4e-181">ViewController.h 파일은 다음과 같이 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-181">Your ViewController.h file should look as follows:</span></span>
   
        #import <UIKit/UIKit.h>
   
        @interface ViewController : UIViewController <UITextFieldDelegate, NSXMLParserDelegate>
        {
            NSXMLParser *xmlParser;
        }
   
        // Make sure these outlets are connected tooyour UI by ctrl+dragging
        @property (weak, nonatomic) IBOutlet UITextField *notificationMessage;
        @property (weak, nonatomic) IBOutlet UILabel *sendResults;
   
        @property (copy, nonatomic) NSString *statusResult;
        @property (copy, nonatomic) NSString *currentElement;
   
        @end
3. <span data-ttu-id="6bc4e-182">열기 `HubInfo.h` hello 상수 tooyour 허브 알림을 보내는 데 사용 되는 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-182">Open `HubInfo.h` and add hello following constants which will be used for sending notifications tooyour hub.</span></span> <span data-ttu-id="6bc4e-183">실제 hello 자리 표시자 문자열 리터럴을 대체 *DefaultFullSharedAccessSignature* 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-183">Replace hello placeholder string literal with your actual *DefaultFullSharedAccessSignature* connection string.</span></span>
   
        #define API_VERSION @"?api-version=2015-01"
        #define HUBFULLACCESS @"<Enter Your DefaultFullSharedAccess Connection string>"
4. <span data-ttu-id="6bc4e-184">Hello 다음 추가 `#import` 문 tooyour `ViewController.h` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-184">Add hello following `#import` statements tooyour `ViewController.h` file.</span></span>
   
        #import <CommonCrypto/CommonHMAC.h>
        #import "HubInfo.h"
5. <span data-ttu-id="6bc4e-185">`ViewController.m` hello toohello 인터페이스 구현 코드를 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-185">In `ViewController.m` add hello following code toohello interface implementation.</span></span> <span data-ttu-id="6bc4e-186">이 코드는 *DefaultFullSharedAccessSignature* 연결 문자열을 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-186">This code will parse your *DefaultFullSharedAccessSignature* connection string.</span></span> <span data-ttu-id="6bc4e-187">Hello에 설명 된 대로 [REST API 참조](http://msdn.microsoft.com/library/azure/dn495627.aspx),이 구문 분석 된 정보에 사용 되는 toogenerate hello에 대 한 SaS 토큰 됩니다 **권한 부여** 요청 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-187">As mentioned in hello [REST API reference](http://msdn.microsoft.com/library/azure/dn495627.aspx), this parsed information will be used toogenerate a SaS token for hello **Authorization** request header.</span></span>
   
        NSString *HubEndpoint;
        NSString *HubSasKeyName;
        NSString *HubSasKeyValue;
   
        -(void)ParseConnectionString
        {
            NSArray *parts = [HUBFULLACCESS componentsSeparatedByString:@";"];
            NSString *part;
   
            if ([parts count] != 3)
            {
                NSException* parseException = [NSException exceptionWithName:@"ConnectionStringParseException"
                    reason:@"Invalid full shared access connection string" userInfo:nil];
   
                @throw parseException;
            }
   
            for (part in parts)
            {
                if ([part hasPrefix:@"Endpoint"])
                {
                    HubEndpoint = [NSString stringWithFormat:@"https%@",[part substringFromIndex:11]];
                }
                else if ([part hasPrefix:@"SharedAccessKeyName"])
                {
                    HubSasKeyName = [part substringFromIndex:20];
                }
                else if ([part hasPrefix:@"SharedAccessKey"])
                {
                    HubSasKeyValue = [part substringFromIndex:16];
                }
            }
        }
6. <span data-ttu-id="6bc4e-188">`ViewController.m`, 업데이트 hello `viewDidLoad` hello 보기 로드 될 때 메서드 tooparse hello 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-188">In `ViewController.m`, update hello `viewDidLoad` method tooparse hello connection string when hello view loads.</span></span> <span data-ttu-id="6bc4e-189">추가적으로 hello 유틸리티 메서드를 아래 표시 된 toohello 인터페이스를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-189">Also add hello utility methods, shown below, toohello interface implementation.</span></span>  

        - (void)viewDidLoad
        {
            [super viewDidLoad];
            [self ParseConnectionString];
            [_notificationMessage setDelegate:self];
        }

        -(NSString *)CF_URLEncodedString:(NSString *)inputString
        {
           return (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(NULL, (CFStringRef)inputString,
                NULL, (CFStringRef)@"!*'();:@&=+$,/?%#[]", kCFStringEncodingUTF8);
        }

        -(void)MessageBox:(NSString *)title message:(NSString *)messageText
        {
            UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
                cancelButtonTitle:@"OK" otherButtonTitles: nil];
            [alert show];
        }





1. <span data-ttu-id="6bc4e-190">`ViewController.m`, 다음 코드 toohello 인터페이스 구현 toogenerate hello SaS 권한 부여 토큰 hello에 제공 되는 hello 추가 **권한 부여** 헤더로, hello에 설명 된 대로 [REST API 참조](http://msdn.microsoft.com/library/azure/dn495627.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-190">In `ViewController.m`, add hello following code toohello interface implementation toogenerate hello SaS authorization token that will be provided in hello **Authorization** header, as mentioned in hello [REST API Reference](http://msdn.microsoft.com/library/azure/dn495627.aspx).</span></span>
   
        -(NSString*) generateSasToken:(NSString*)uri
        {
            NSString *targetUri;
            NSString* utf8LowercasedUri = NULL;
            NSString *signature = NULL;
            NSString *token = NULL;
   
            @try
            {
                // Add expiration
                uri = [uri lowercaseString];
                utf8LowercasedUri = [self CF_URLEncodedString:uri];
                targetUri = [utf8LowercasedUri lowercaseString];
                NSTimeInterval expiresOnDate = [[NSDate date] timeIntervalSince1970];
                int expiresInMins = 60; // 1 hour
                expiresOnDate += expiresInMins * 60;
                UInt64 expires = trunc(expiresOnDate);
                NSString* toSign = [NSString stringWithFormat:@"%@\n%qu", targetUri, expires];
   
                // Get an hmac_sha1 Mac instance and initialize with hello signing key
                const char *cKey  = [HubSasKeyValue cStringUsingEncoding:NSUTF8StringEncoding];
                const char *cData = [toSign cStringUsingEncoding:NSUTF8StringEncoding];
                unsigned char cHMAC[CC_SHA256_DIGEST_LENGTH];
                CCHmac(kCCHmacAlgSHA256, cKey, strlen(cKey), cData, strlen(cData), cHMAC);
                NSData *rawHmac = [[NSData alloc] initWithBytes:cHMAC length:sizeof(cHMAC)];
                signature = [self CF_URLEncodedString:[rawHmac base64EncodedStringWithOptions:0]];
   
                // Construct authorization token string
                token = [NSString stringWithFormat:@"SharedAccessSignature sig=%@&se=%qu&skn=%@&sr=%@",
                    signature, expires, HubSasKeyName, targetUri];
            }
            @catch (NSException *exception)
            {
                [self MessageBox:@"Exception Generating SaS Token" message:[exception reason]];
            }
            @finally
            {
                if (utf8LowercasedUri != NULL)
                    CFRelease((CFStringRef)utf8LowercasedUri);
                if (signature != NULL)
                CFRelease((CFStringRef)signature);
            }
   
            return token;
        }
2. <span data-ttu-id="6bc4e-191">Ctrl + 드래그에서 hello **알림 보내기** 너무 단추`ViewController.m` tooadd 라는 동작 **SendNotificationMessage** hello에 대 한 **터치 다운** 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-191">Ctrl+drag from hello **Send Notification** button too`ViewController.m` tooadd an action named **SendNotificationMessage** for hello **Touch Down** event.</span></span> <span data-ttu-id="6bc4e-192">Hello REST API를 사용 하 여 코드 toosend hello 알림을 다음 hello로 메서드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-192">Update method with hello following code toosend hello notification using hello REST API.</span></span>
   
        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";
            [self SendNotificationRESTAPI];
        }
   
        - (void)SendNotificationRESTAPI
        {
            NSURLSession* session = [NSURLSession
                             sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                             delegate:nil delegateQueue:nil];
   
            // Apple Notification format of hello notification message
            NSString *json = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"%@\"}}",
                                self.notificationMessage.text];
   
            // Construct hello message's REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                                HUBNAME, API_VERSION]];
   
            // Generate hello token toobe used in hello authorization header
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello APNs notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            // Signify Apple notification format
            [request setValue:@"apple" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (error || (httpResponse.statusCode != 200 && httpResponse.statusCode != 201))
                {
                    NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                }
                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                       [xmlParser parse];
                }
            }];
            [dataTask resume];
        }
3. <span data-ttu-id="6bc4e-193">`ViewController.m`, 대리자 메서드 toosupport hello 텍스트 필드에 대 한 hello 키보드를 닫으면 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-193">In `ViewController.m`, add hello following delegate method toosupport closing hello keyboard for hello text field.</span></span> <span data-ttu-id="6bc4e-194">Ctrl + 드래그 hello 인터페이스 디자이너 tooset hello hello 텍스트 필드 toohello 뷰-컨트롤러 아이콘에서 hello 콘센트 대리자로 컨트롤러를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-194">Ctrl+drag from hello text field toohello View Controller icon in hello interface designer tooset hello view controller as hello outlet delegate.</span></span>
   
        //===[ Implement UITextFieldDelegate methods ]===
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
4. <span data-ttu-id="6bc4e-195">`ViewController.m`, hello 다음 메서드 toosupport 구문 분석 hello 응답을 사용 하 여 위임할 추가 `NSXMLParser`합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-195">In `ViewController.m`, add hello following delegate methods toosupport parsing hello response by using `NSXMLParser`.</span></span>
   
       //===[ Implement NSXMLParserDelegate methods ]===
   
       -(void)parserDidStartDocument:(NSXMLParser *)parser
       {
           self.statusResult = @"";
       }
   
       -(void)parser:(NSXMLParser *)parser didStartElement:(NSString *)elementName
           namespaceURI:(NSString *)namespaceURI qualifiedName:(NSString *)qName
           attributes:(NSDictionary *)attributeDict
       {
           NSString * element = [elementName lowercaseString];
           NSLog(@"*** New element parsed : %@ ***",element);
   
           if ([element isEqualToString:@"code"] | [element isEqualToString:@"detail"])
           {
               self.currentElement = element;
           }
       }
   
       -(void) parser:(NSXMLParser *)parser foundCharacters:(NSString *)parsedString
       {
           self.statusResult = [self.statusResult stringByAppendingString:
               [NSString stringWithFormat:@"%@ : %@\n", self.currentElement, parsedString]];
       }
   
       -(void)parserDidEndDocument:(NSXMLParser *)parser
       {
           // Set hello status label text on hello UI thread
           dispatch_async(dispatch_get_main_queue(),
           ^{
               [self.sendResults setText:self.statusResult];
           });
       }
5. <span data-ttu-id="6bc4e-196">Hello 프로젝트를 빌드하고 오류가 없는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-196">Build hello project and verify that there are no errors.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc4e-197">Hello 변경할지 bitcode 지원에 대 한 Xcode7에 빌드 오류가 발생 하는 경우 **빌드 설정** > **Bitcode 사용 (ENABLE_BITCODE)** 너무**아니요** Xcode에서.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-197">If you encounter a build error in Xcode7 about bitcode support, you should change hello **Build Settings** > **Enable Bitcode (ENABLE_BITCODE)** too**NO** in Xcode.</span></span> <span data-ttu-id="6bc4e-198">알림 허브 SDK hello bitcode 현재 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-198">hello Notification Hubs SDK does not currently support bitcode.</span></span> 
> 
> 

<span data-ttu-id="6bc4e-199">Apple hello에서 모든 hello 가능한 알림 페이로드를 찾을 수 있습니다 [로컬 및 푸시 알림 프로그래밍 가이드]합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-199">You can find all hello possible notification payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

## <a name="checking-if-your-app-can-receive-push-notifications"></a><span data-ttu-id="6bc4e-200">앱이 푸시 알림을 받을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-200">Checking if your app can receive push notifications</span></span>
<span data-ttu-id="6bc4e-201">iOS에서 푸시 알림을 tootest hello 앱 tooa 실제 iOS 장치를 배포 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-201">tootest push notifications on iOS, you must deploy hello app tooa physical iOS device.</span></span> <span data-ttu-id="6bc4e-202">Hello iOS 시뮬레이터를 사용 하 여 Apple 푸시 알림을 보낼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-202">You cannot send Apple push notifications by using hello iOS Simulator.</span></span>

1. <span data-ttu-id="6bc4e-203">Hello 앱을 실행 하 고 확인에 성공 하면 등록 키를 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-203">Run hello app and verify that registration succeeds, and then press **OK**.</span></span>
   
    ![iOS 앱 푸시 알림 등록 테스트][33]
2. <span data-ttu-id="6bc4e-205">Hello에서 테스트 푸시 알림을 보낼 수 있습니다 [Azure 포털]위에서 설명한 것 처럼, 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-205">You can send a test push notification from hello [Azure Portal], as described above.</span></span> <span data-ttu-id="6bc4e-206">Hello 앱에 푸시 알림을 보내는 경우에 코드를 추가한 경우 터치 hello 텍스트 필드 tooenter 내 알림 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-206">If you added code for sending push notifications in hello app, touch inside hello text field tooenter a notification message.</span></span> <span data-ttu-id="6bc4e-207">Hello 키를 누릅니다 **보낼** 단추 hello 키보드 또는 hello **알림 보내기** hello 보기 toosend hello 알림 메시지에는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-207">Then press hello **Send** button on hello keyboard or hello **Send Notification** button in hello view toosend hello notification message.</span></span>
   
    ![iOS 앱 푸시 알림 전송 테스트][34]
3. <span data-ttu-id="6bc4e-209">hello 푸시 알림을 보내는 tooall는 장치에 등록 된 tooreceive hello 알림을에서 특정 알림 허브 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-209">hello push notification is sent tooall devices that are registered tooreceive hello notifications from hello particular Notification Hub.</span></span>
   
    ![iOS 앱 푸시 알림 수신 테스트][35]

## <a name="next-steps"></a><span data-ttu-id="6bc4e-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6bc4e-211">Next steps</span></span>
<span data-ttu-id="6bc4e-212">이 간단한 예제에서는 푸시 알림을 tooall 등록 된 iOS 장치를 브로드캐스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-212">In this simple example, you broadcasted push notifications tooall your registered iOS devices.</span></span> <span data-ttu-id="6bc4e-213">Toohello 진행 하는 학습의 다음 단계로 제안 [Azure 알림 허브 사용자에 게 알림.NET 백 엔드와 iOS 용] 자습서 백 엔드 toosend 푸시 알림 태그를 사용 하 여 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-213">We suggest as a next step in your learning that you proceed toohello [Azure Notification Hubs Notify Users for iOS with .NET backend] tutorial, which will walk you through creating a backend toosend push notifications using tags.</span></span> 

<span data-ttu-id="6bc4e-214">관심 그룹으로 사용자 toosegment 하려는 경우 또한으로 이동할 수 있습니다 toohello [최신 뉴스 사용 하 여 알림 허브 toosend] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-214">If you want toosegment your users by interest groups, you can additionally move on toohello [Use Notification Hubs toosend breaking news] tutorial.</span></span> 

<span data-ttu-id="6bc4e-215">알림 허브에 대한 일반적인 정보는 [알림 허브 지침]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6bc4e-215">For general information about Notification Hubs, see [Notification Hubs Guidance].</span></span>

<!-- Images. -->

[6]: ./media/notification-hubs-ios-get-started/notification-hubs-configure-ios.png
[8]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app.png
[9]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app2.png
[10]: ./media/notification-hubs-ios-get-started/notification-hubs-create-ios-app3.png
[11]: ./media/notification-hubs-ios-get-started/notification-hubs-xcode-product-name.png

[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png

[31]: ./media/notification-hubs-ios-get-started/notification-hubs-ios-ui.png
[32]: ./media/notification-hubs-ios-get-started/notification-hubs-storyboard-view.png
[33]: ./media/notification-hubs-ios-get-started/notification-hubs-test1.png
[34]: ./media/notification-hubs-ios-get-started/notification-hubs-test2.png
[35]: ./media/notification-hubs-ios-get-started/notification-hubs-test3.png



<!-- URLs. -->
[모바일 서비스 iOS SDK 버전 1.2.4]: http://aka.ms/kymw2g
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Azure Classic Portal]: https://manage.windowsazure.com/
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
[Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Get started with push notifications in Mobile Services]: ../mobile-services-javascript-backend-ios-get-started-push.md
[Azure 알림 허브 사용자에 게 알림.NET 백 엔드와 iOS 용]: notification-hubs-aspnet-backend-ios-apple-apns-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-ios-xplat-segmented-apns-push-notification.md

[로컬 및 푸시 알림 프로그래밍 가이드]: http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW1
[Azure 포털]: https://portal.azure.com
