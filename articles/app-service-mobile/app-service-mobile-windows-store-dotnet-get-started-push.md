---
title: "UWP(유니버설 Windows 플랫폼) 앱에 푸시 알림 추가 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱 및 Azure 알림 허브를 사용하여 UWP(유니버설 Windows 플랫폼) 앱에 푸시 알림을 보내는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="94c32-103">Windows 앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="94c32-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="94c32-104">개요</span><span class="sxs-lookup"><span data-stu-id="94c32-104">Overview</span></span>
<span data-ttu-id="94c32-105">이 자습서에서는 푸시 알림을 [Windows 빠른 시작](app-service-mobile-windows-store-dotnet-get-started.md) 프로젝트에 추가하여 레코드가 삽입될 때마다 장치에 푸시 알림이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="94c32-106">다운로드한 빠른 시작 서버 프로젝트를 사용하지 않는 경우 푸시 알림 확장 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="94c32-107">자세한 내용은 [Azure Mobile Apps용 .NET 백 엔드 서버 SDK 사용](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94c32-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="94c32-108"><a name="configure-hub"></a>알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="94c32-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="94c32-109">푸시 알림에 대해 앱 등록</span><span class="sxs-lookup"><span data-stu-id="94c32-109">Register your app for push notifications</span></span>
<span data-ttu-id="94c32-110">Windows 스토어에 앱을 제출한 다음 푸시를 전송하는 WNS(Windows Notification Services)를 통합하도록 서버 프로젝트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="94c32-111">Visual Studio 솔루션 탐색기에서 UWP 앱 프로젝트를 마우스 오른쪽 단추로 클릭하고 **스토어** > **스토어와 앱을 연결...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="94c32-113">마법사에서 **다음**을 클릭하고, Microsoft 계정으로 로그인하고, **새로운 앱 이름 예약**에서 앱 이름을 입력한 후 **예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="94c32-114">앱을 성공적으로 등록한 후에 새로운 앱 이름을 선택하고 **다음** 및 **연결**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="94c32-115">이렇게 하면 필요한 Windows 스토어 등록 정보가 응용 프로그램 매니페스트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="94c32-116">[Windows 개발자 센터](https://dev.windows.com/en-us/overview)로 이동하여 Microsoft 계정을 사용해 로그인하고 **내 앱**에서 새 앱 등록을 클릭한 후 **서비스** > **푸시 알림**을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="94c32-117">**푸시 알림** 페이지에서 **Microsoft Azure Mobile Services** 아래의 **Live Services 사이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="94c32-118">등록 페이지에서 **응용 프로그램 암호** 및 **패키지 SID**에 있는 값을 기록합니다. 이 값은 모바일 앱 백 엔드를 구성하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Windows 스토어에 응용 프로그램 연결](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="94c32-120">클라이언트 암호와 패키지 SID는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="94c32-121">다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="94c32-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="94c32-122">**응용 프로그램 ID** 는 Microsoft 계정 인증을 구성하는 암호와 함게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="94c32-123">푸시 알림을 전송하도록 백 엔드 구성</span><span class="sxs-lookup"><span data-stu-id="94c32-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="94c32-124"><a id="update-service"></a>푸시 알림을 전송하도록 서버 업데이트</span><span class="sxs-lookup"><span data-stu-id="94c32-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="94c32-125">백 엔드 프로젝트 형식&mdash;([.NET 백 엔드](#dotnet) 또는 [Node.js 백 엔드](#nodejs))과 일치하는 아래의 절차를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="94c32-126"><a name="dotnet"></a>.NET 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="94c32-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="94c32-127">Visual Studio에서 서버 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭합니다. Microsoft.Azure.NotificationHubs를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="94c32-128">알림 허브 클라이언트 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="94c32-129">**컨트롤러**를 확장하고 TodoItemController.cs를 열고 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="94c32-130">**PostTodoItem** 메서드에서 **InsertAsync**에 대한 호출 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="94c32-131">이 코드는 새 항목을 삽입한 후에 알림 허브에 푸시 알림을 전송하도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="94c32-132">서버 프로젝트를 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-132">Republish the server project.</span></span>

### <span data-ttu-id="94c32-133"><a name="nodejs"></a>Node.js 백 엔드 프로젝트</span><span class="sxs-lookup"><span data-stu-id="94c32-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="94c32-134">아직 수행하지 않은 경우 [빠른 시작 프로젝트를 다운로드](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart)하거나 [Azure 포털에서 온라인 편집기](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="94c32-135">todoitem.js 파일의 기존 코드를 다음으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
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
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="94c32-136">이는 새 todo 항목이 삽입된 경우 item.text가 포함된 WNS 알림 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="94c32-137">로컬 컴퓨터에서 파일을 편집할 때 서버 프로젝트를 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="94c32-138"><a id="update-app"></a>앱에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="94c32-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="94c32-139">다음으로 앱은 시작에서 푸시 알림에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="94c32-140">사용할 수 있는 인증이 있는 경우 푸시 알림을 등록하기 전에 사용자가 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="94c32-141">**App.xaml.cs** 프로젝트 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="94c32-142">동일한 파일에서 다음 **InitNotificationsAsync** 메서드 정의를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="94c32-143">이 코드는 WNS에서 앱의 ChannelURI를 검색한 후 해당 ChannelURI를 앱 서비스 모바일 앱에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="94c32-144">**App.xaml.cs**의 **OnLaunched** 이벤트 처리기 맨 위에서 다음 예제와 같이 메서드 정의에 **비동기** 한정자를 추가하고 새 **InitNotificationsAsync**메서드에 다음 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="94c32-145">이제 응용 프로그램을 시작할 때마다 단기 ChannelURI가 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="94c32-146">UWP 앱 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="94c32-147">이제 앱에서 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="94c32-148"><a id="test"></a>앱에서 푸시 알림 테스트</span><span class="sxs-lookup"><span data-stu-id="94c32-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="94c32-149"><a id="more"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="94c32-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="94c32-150">푸시 알림에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="94c32-151">Azure 모바일 앱에 관리되는 클라이언트를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="94c32-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="94c32-152">템플릿은 유연성을 제공하여 플랫폼간 푸시 및 지역화된 푸시를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="94c32-153">템플릿을 등록하는 방법에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="94c32-154">푸시 알림 문제 진단</span><span class="sxs-lookup"><span data-stu-id="94c32-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="94c32-155">장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="94c32-156">이 항목에서는 푸시 알림 실패의 근본 원인을 분석 및 파악하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="94c32-157">다음 자습서 중 하나를 진행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="94c32-158">앱에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="94c32-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="94c32-159">ID 공급자를 사용하여 앱 사용자를 인증하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="94c32-160">앱에 오프라인 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="94c32-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="94c32-161">모바일 앱 백 엔드를 사용하여 앱에 오프라인 지원을 추가하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="94c32-162">오프라인 동기화를 사용하면 최종 사용자는 네트워크에 연결되어 있지 않을 때도 모바일 앱&mdash;데이터 보기, 추가 또는 수정&mdash;과 같은 상호 작용을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94c32-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
