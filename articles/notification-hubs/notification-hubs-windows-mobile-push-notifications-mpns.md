---
title: "Windows Phone에서 Azure 알림 허브를 사용하여 푸시 알림 보내기 | Microsoft Docs"
description: "이 자습서에서는 Azure 알림 허브를 사용하여 Windows Phone 8 또는 Windows Phone 8.1 Silverlight 응용 프로그램에 푸시 알림을 보내는 방법을 알아봅니다."
services: notification-hubs
documentationcenter: windows
keywords: "푸시 알림, 푸시 알림, windows phone 푸시"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="a6db4-104">Windows Phone에서 Azure 알림 허브를 사용하여 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="a6db4-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a6db4-105">개요</span><span class="sxs-lookup"><span data-stu-id="a6db4-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="a6db4-106">이 자습서를 완료하려면 활성 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a6db4-107">계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a6db4-108">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6db4-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="a6db4-109">이 자습서에서는 Azure 알림 허브를 사용하여 Windows Phone 8 또는 Windows Phone 8.1 Silverlight 응용 프로그램에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="a6db4-110">Windows Phone 8.1(비 Silverlight)을 대상으로 하는 경우 [Windows 범용](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 버전을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6db4-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="a6db4-111">이 자습서에서는 MPNS(Microsoft 푸시 알림 서비스)를 사용하여 푸시 알림을 받는 빈 Windows Phone 8 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="a6db4-112">완료하면 알림 허브를 사용하여 앱을 실행하는 모든 장치로 푸시 알림을 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="a6db4-113">알림 허브 Windows Phone SDK에서는 Windows Phone 8.1 Silverlight 앱에서의 WNS(Windows 푸시 알림 서비스) 사용을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="a6db4-114">Windows Phone 8.1 Silverlight 앱에서 MPNS 대신 WNS를 사용하려면 REST API를 사용하는 [알림 허브 - Windows Phone Silverlight 자습서]를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="a6db4-115">이 자습서에서는 알림 허브를 사용하는 간단한 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6db4-116">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a6db4-116">Prerequisites</span></span>
<span data-ttu-id="a6db4-117">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="a6db4-118">[Visual Studio 2012 Express for Windows Phone]이상 버전</span><span class="sxs-lookup"><span data-stu-id="a6db4-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="a6db4-119">이 자습서를 완료해야 다른 모든 Windows Phone 8 앱용 알림 허브 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="a6db4-120">알림 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="a6db4-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="a6db4-121"><b>알림 서비스</b> 섹션(<i>설정</i> 내에서)을 클릭한 후 <b>Windows Phone(MPNS)</b>을 클릭한 후 <b>인증되지 않은 푸시 알림 사용</b> 확인란을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure 포털 - 인증되지 않은 푸시 알림 사용](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="a6db4-123">이제 Windows Phone의 인증되지 않은 알림을 보낼 수 있는 허브가 생성 및 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="a6db4-124">이 자습서에서는 인증되지 않은 모드로 MPNS를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="a6db4-125">MPNS 인증되지 않은 모드에는 각 채널로 보낼 수 있는 알림에 대한 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="a6db4-126">알림 허브는 인증서를 업로드할 수 있도록 하여 [MPNS 인증 모드](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) 를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="a6db4-127">알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="a6db4-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="a6db4-128">Visual Studio에서 새 Windows Phone 8 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="a6db4-129">Visual Studio 2013 업데이트 2 이상에서는 대신 Windows Phone Silverlight 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - 새 프로젝트 - 새 응용 프로그램 - Windows Phone Silverlight][11]
2. <span data-ttu-id="a6db4-131">Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="a6db4-132">그러면 **NuGet 패키지 관리** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="a6db4-133">`WindowsAzure.Messaging.Managed` 를 검색하고 **설치**를 클릭한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio - NuGet 패키지 관리자][20]
   
    <span data-ttu-id="a6db4-135">그러면 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 패키지</a>를 사용하여 Windows용 Azure 메시징 라이브러리에 대한 참조가 다운로드, 설치 및 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="a6db4-136">App.xaml.cs 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="a6db4-137">App.xaml.cs의 **Application_Launching** 메서드 맨 위에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="a6db4-138">값 **MyPushChannel** 은 [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) 컬렉션에서 기존 채널을 조회하는 데 사용되는 인덱스입니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="a6db4-139">항목이 없으면 해당 이름을 가진 새 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="a6db4-140">허브 이름과 이전 섹션에서 얻은 **DefaultListenSharedAccessSignature** 라는 연결 문자열을 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="a6db4-141">이 코드는 MPNS에서 앱의 채널 URI를 검색한 후 해당 채널 URI를 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="a6db4-142">또한 이 코드는 응용 프로그램이 시작될 때마다 채널 URI가 알림 허브에 등록되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6db4-143">이 자습서에서는 알림 메시지를 장치로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="a6db4-144">타일 알림을 보내는 경우 채널에서 **BindToShellTile** 메서드를 대신 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="a6db4-145">알림 메시지와 타일 알림을 둘 다 지원하려면 **BindToShellTile** 및 **BindToShellToast**를 둘 다 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="a6db4-146">솔루션 탐색기에서 **속성**을 확장하고 `WMAppManifest.xml` 파일을 연 후 **기능** 탭을 클릭하고 **ID_CAP_PUSH_NOTIFICATION** 기능이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="a6db4-147">`F5` 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="a6db4-148">앱에 등록 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="a6db4-149">앱을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="a6db4-150">푸시 알림 메시지를 받으려면 응용 프로그램이 포그라운드에서 실행되고 있지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="a6db4-151">백 엔드에서 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="a6db4-151">Send push notifications from your backend</span></span>
<span data-ttu-id="a6db4-152">공용 <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST 인터페이스</a>를 통해 모든 백 엔드에서 알림 허브를 사용하여 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="a6db4-153">이 자습서에서는 .NET 콘솔 응용 프로그램을 사용하여 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="a6db4-154">알림 허브와 통합된 ASP.NET Web API 백 엔드에서 푸시 알림을 보내는 방법에 대한 예제는 [.NET 백 엔드를 통한 Azure 알림 허브의 사용자 알림](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6db4-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="a6db4-155">[REST API](https://msdn.microsoft.com/library/azure/dn223264.aspx)를 사용하여 푸시 알림을 보내는 방법에 대한 예는 [Java에서 알림 허브를 사용하는 방법](notification-hubs-java-push-notification-tutorial.md) 및 [PHP에서 알림 허브를 사용하는 방법](notification-hubs-php-push-notification-tutorial.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6db4-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="a6db4-156">솔루션을 마우스 오른쪽 단추로 클릭하고, **추가** 및 **새 프로젝트...**를 선택한 후에 **Visual C#** 아래에서 **Windows** 및 **콘솔 응용 프로그램**을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="a6db4-157">그러면 새 Visual C# 콘솔 응용 프로그램이 솔루션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="a6db4-158">별도의 솔루션에서 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="a6db4-159">**도구**를 클릭하고 **라이브러리 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="a6db4-160">그러면 패키지 관리자 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="a6db4-161">**패키지 관리자 콘솔** 창에서 **기본 프로젝트**를 새 콘솔 응용 프로그램 프로젝트로 설정한 후 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="a6db4-162">그러면 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 패키지</a>를 사용하는 Azure 알림 허브 SDK에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="a6db4-163">`Program.cs` 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="a6db4-164">`Program` 클래스에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-164">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="a6db4-165">`<hub name>` 자리 표시자를 포털에 나타나는 알림 허브의 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="a6db4-166">또한 연결 문자열 자리 표시자를 "알림 허브 구성" 섹션에서 가져온 **DefaultFullSharedAccessSignature** 라는 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a6db4-167">**수신 대기** 권한이 아니라 **모든** 권한을 가진 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="a6db4-168">수신 대기 권한 문자열은 푸시 알림을 보낼 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="a6db4-169">`Main` 메서드에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="a6db4-170">Windows Phone 에뮬레이터를 실행하고 앱을 닫은 상태에서 콘솔 응용 프로그램 프로젝트를 기본 시작 프로젝트로 설정한 후 `F5` 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="a6db4-171">푸시 알림 메시지가 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-171">You will receive a toast push notification.</span></span> <span data-ttu-id="a6db4-172">알림 배너를 누르면 앱이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="a6db4-173">MSDN의 [알림 카탈로그] 및 [타일 카탈로그] 항목에서 가능한 모든 페이로드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6db4-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a6db4-174">Next steps</span></span>
<span data-ttu-id="a6db4-175">이 간단한 예제에서는 모든 Windows Phone 8 장치로 푸시 알림을 브로드캐스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="a6db4-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="a6db4-176">특정 사용자를 대상으로 하려면 [알림 허브를 사용하여 사용자에게 알림 푸시] (영문) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a6db4-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="a6db4-177">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="a6db4-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="a6db4-178">[알림 허브 지침]에서 알림 허브 사용 방법을 자세히 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="a6db4-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
<span data-ttu-id="a6db4-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="a6db4-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="a6db4-180">[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="a6db4-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="a6db4-181">[알림 허브를 사용하여 사용자에게 알림 푸시]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="a6db4-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="a6db4-182">[알림 허브를 사용하여 뉴스 속보 보내기]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="a6db4-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="a6db4-183">[알림 카탈로그]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="a6db4-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="a6db4-184">[타일 카탈로그]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="a6db4-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="a6db4-185">[알림 허브 - Windows Phone Silverlight 자습서]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="a6db4-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

