---
title: "aaaAdd 푸시 알림 tooyour 유니버설 Windows 플랫폼 (UWP) 응용 프로그램 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱 toouse 및 Azure 알림 허브 toosend 밀어넣기 알림 tooyour 유니버설 Windows 플랫폼 (UWP) 응용 프로그램에 알아봅니다."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="12fa0-103">푸시 알림 tooyour Windows 앱 추가</span><span class="sxs-lookup"><span data-stu-id="12fa0-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="12fa0-104">개요</span><span class="sxs-lookup"><span data-stu-id="12fa0-104">Overview</span></span>
<span data-ttu-id="12fa0-105">이 자습서에서는 푸시 알림을 toohello 추가한 [Windows 빠른 시작](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트 레코드가 삽입 될 때마다 푸시 알림을 toohello 장치 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="12fa0-106">사용 하지 않는 경우 hello 퀵 스타트 서버 프로젝트를 다운로드, 푸시 알림 확장 패키지 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="12fa0-107">참조 [Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK에서 작동](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="12fa0-108"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="12fa0-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="12fa0-109">푸시 알림에 대해 앱 등록</span><span class="sxs-lookup"><span data-stu-id="12fa0-109">Register your app for push notifications</span></span>
<span data-ttu-id="12fa0-110">Windows 스토어에 앱 toohello toosubmit 필요한 서버 프로젝트 toointegrate toosend 푸시 알림 서비스 WNS (Windows) 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="12fa0-111">Visual Studio 솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello UWP 앱 프로젝트에서에서 클릭 **저장소** > **hello 저장소로 응용 프로그램 연결 중...** .</span><span class="sxs-lookup"><span data-stu-id="12fa0-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="12fa0-113">Hello 마법사에서 **다음**, इ न क ा Microsoft ख에서 응용 프로그램에 대 한 이름을 입력 **새로운 앱 이름 예약**, 클릭 **예약**합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="12fa0-114">Hello 앱 등록을 성공적으로 만든 hello 새로운 앱 이름 되 면 클릭 **다음**, 클릭 하 고 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="12fa0-115">이 hello 필요한 Windows 스토어 등록 정보 toohello 응용 프로그램 매니페스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="12fa0-116">Toohello 이동 [Windows 개발자 센터](https://dev.windows.com/en-us/overview), Microsoft 계정으로 로그인, 클릭 hello에 새 응용 프로그램 등록 **My apps**를 확장 한 다음 **서비스**  >  **푸시 알림**합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="12fa0-117">Hello에 **푸시 알림** 페이지 **Live 서비스 사이트** 아래 **Microsoft Azure 모바일 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="12fa0-118">Hello 등록 페이지에 아래 hello 값 기록해 **응용 프로그램 암호** 및 hello **패키지 SID**이며 다음 사용할 tooconfigure 모바일 앱 백 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="12fa0-120">hello 클라이언트 암호와 패키지 SID는 중요 한 보안 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="12fa0-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="12fa0-121">다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="12fa0-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="12fa0-122">hello **응용 프로그램 Id** hello 비밀 tooconfigure Microsoft 계정 인증과 함께 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="12fa0-123">Hello 백 엔드 toosend 푸시 알림 구성</span><span class="sxs-lookup"><span data-stu-id="12fa0-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="12fa0-124"><a id="update-service"></a>업데이트 hello 서버 toosend 푸시 알림</span><span class="sxs-lookup"><span data-stu-id="12fa0-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="12fa0-125">백 엔드 프로젝트 형식과 일치 하는 hello 절차 아래를 사용 하 여&mdash;어느 [.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs)합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="12fa0-126"><a name="dotnet"></a>.NET 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="12fa0-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="12fa0-127">Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**검색 Microsoft.Azure.NotificationHubs, 한 다음 클릭, **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="12fa0-128">Hello 알림 허브 클라이언트 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="12fa0-129">확장 **컨트롤러**TodoItemController.cs를 열고 hello 다음 추가 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="12fa0-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="12fa0-130">Hello에 **PostTodoItem** 메서드를 너무 hello 호출 후 코드를 다음 hello 추가**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="12fa0-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="12fa0-131">이 코드는 새 항목은 삽입 후 푸시 알림을 알림 허브 toosend hello를 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="12fa0-132">Hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-132">Republish hello server project.</span></span>

### <span data-ttu-id="12fa0-133"><a name="nodejs"></a>Node.js 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="12fa0-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="12fa0-134">따라서 아직 수행 하지 않은 경우 [hello 퀵 스타트 프로젝트를 다운로드](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) 하거나 다른 hello를 사용 하 여 [hello Azure 포털에서에서 온라인 편집기](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="12fa0-135">Hello 다음 hello hello todoitem.js 파일의 기존 코드를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="12fa0-136">이 hello item.text 새 할 일 항목을 삽입 하는 경우 포함 된 WNS 알림을 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="12fa0-137">로컬 컴퓨터에 hello 파일을 편집할 때 hello 서버 프로젝트를 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="12fa0-138"><a id="update-app"></a>푸시 알림 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="12fa0-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="12fa0-139">다음으로 앱은 시작에서 푸시 알림에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="12fa0-140">인증을 이미 활성화 하는 경우 해당 hello 사용자가 로그인 tooregister ध 전에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="12fa0-141">열기 hello **App.xaml.cs** 프로젝트 파일 및 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="12fa0-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="12fa0-142">동일한 파일 hello 하 hello 다음 추가 **InitNotificationsAsync** 메서드 정의 toohello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="12fa0-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="12fa0-143">이 코드는 WNS에서 hello 앱에 대 한 hello ChannelURI를 검색 하 고 만든 다음 해당 ChannelURI 앱 서비스 모바일 앱과 함께 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="12fa0-144">Hello 위쪽 hello에 **OnLaunched** 의 이벤트 처리기 **App.xaml.cs**, hello 추가 **비동기** 한정자 toohello 메서드 정의 하 고 hello 다음 호출은 toohello 새 추가 **InitNotificationsAsync** hello 다음 예제와 같이 메서드를:</span><span class="sxs-lookup"><span data-stu-id="12fa0-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="12fa0-145">이렇게 하면 해당 hello 수명이 짧은 ChannelURI hello 응용 프로그램이 시작 될 때마다 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="12fa0-146">UWP 앱 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="12fa0-147">이제 앱이 준비 tooreceive 알림 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="12fa0-148"><a id="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="12fa0-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="12fa0-149"><a id="more"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="12fa0-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="12fa0-150">푸시 알림에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="12fa0-151">Toouse hello Azure 모바일 앱에 대 한 클라이언트를 관리 하는 방법</span><span class="sxs-lookup"><span data-stu-id="12fa0-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="12fa0-152">서식 파일에는 유연성 toosend 플랫폼 간 푸시 및 지역화 된 푸시 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="12fa0-153">자세한 내용은 방법 tooregister 템플릿.</span><span class="sxs-lookup"><span data-stu-id="12fa0-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="12fa0-154">푸시 알림 문제 진단</span><span class="sxs-lookup"><span data-stu-id="12fa0-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="12fa0-155">장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="12fa0-156">이 항목에서는 tooanalyze 및 hello 루트 계산 푸시 알림 오류의 발생 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="12fa0-157">Tooone의 hello 다음 자습서를 계속 진행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="12fa0-158">인증 tooyour 앱 추가</span><span class="sxs-lookup"><span data-stu-id="12fa0-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="12fa0-159">자세한 내용은 방법 tooauthenticate 사용자가 id 공급자로 사용 하 여 앱의 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="12fa0-160">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="12fa0-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="12fa0-161">오프 라인 tooadd는 모바일 앱 백 엔드를 사용 하 여 앱을 지 원하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="12fa0-162">오프 라인 동기화 허용 모바일 앱과 함께 최종 사용자에 게 toointeract&mdash;보기, 추가 또는 데이터 수정&mdash;네트워크 연결이 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12fa0-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
