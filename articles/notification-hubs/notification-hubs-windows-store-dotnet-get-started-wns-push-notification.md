---
title: "Windows 유니버설 플랫폼 앱용 Azure Notification Hubs 시작 | Microsoft Docs"
description: "이 자습서에서는 Azure Notification Hubs를 사용하여 Windows 유니버설 플랫폼 응용 프로그램으로 알림을 푸시하는 방법을 알아봅니다."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="47900-103">Windows 유니버설 플랫폼 앱용 Notification Hubs 시작</span><span class="sxs-lookup"><span data-stu-id="47900-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="47900-104">개요</span><span class="sxs-lookup"><span data-stu-id="47900-104">Overview</span></span>
<span data-ttu-id="47900-105">이 자습서에서는 Azure Notification Hubs를 사용하여 UWP(유니버설 Windows 플랫폼) 앱에 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47900-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="47900-106">이 자습서에서는 WNS(Windows 푸시 알림 서비스)를 사용하여 푸시 알림을 받는 새 Windows 스토어 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="47900-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="47900-107">완료하면 알림 허브를 사용하여 앱을 실행하는 모든 장치로 푸시 알림을 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="47900-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="47900-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="47900-109">이 자습서에 대해 완료된 코드는 GitHub의 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47900-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="47900-110">Prerequisites</span></span>
<span data-ttu-id="47900-111">이 자습서를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="47900-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 이상 버전</span><span class="sxs-lookup"><span data-stu-id="47900-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="47900-113">유니버설 Windows 앱 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="47900-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="47900-114">활성 Azure 계정 </span><span class="sxs-lookup"><span data-stu-id="47900-114">An active Azure account</span></span> <br/><span data-ttu-id="47900-115">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="47900-116">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47900-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="47900-117">활성 Windows 스토어 계정</span><span class="sxs-lookup"><span data-stu-id="47900-117">An active Windows Store account</span></span>

<span data-ttu-id="47900-118">이 자습서를 완료해야 다른 모든 Windows 유니버설 플랫폼 앱용 Notification Hubs 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="47900-119">Windows 스토어에 앱 등록</span><span class="sxs-lookup"><span data-stu-id="47900-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="47900-120">UWP 앱으로 푸시 알림을 보내려면 앱을 Windows 스토어와 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="47900-121">그런 다음 WNS와 통합되도록 알림 허브를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="47900-122">앱을 아직 등록하지 않은 경우 [Windows 개발자 센터](https://dev.windows.com/overview)로 이동하여 Microsoft 계정으로 로그인한 다음 **새 앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="47900-123">앱의 이름을 입력하고 **앱 이름 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="47900-124">이렇게 하면 앱을 새로 Windows 스토어에 등록하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="47900-125">Visual Studio에서 Windows 범용 **비어 있는 앱** 템플릿을 사용하여 새 Visual C# 스토어 앱 프로젝트를 만들고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="47900-126">대상 및 최소 플랫폼 버전에 대한 기본값을 그대로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="47900-127">솔루션 탐색기에서 Windows 스토어 앱 프로젝트를 마우스 오른쪽 단추로 클릭하고 **스토어**를 클릭한 후 **응용 프로그램을 스토어에 연결...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="47900-128">**응용 프로그램을 Windows 스토어에 연결** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="47900-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="47900-129">마법사에서 Microsoft 계정으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="47900-130">2단계에서 등록한 앱을 클릭하고 **다음**을 클릭한 후 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="47900-131">이렇게 하면 필요한 Windows 스토어 등록 정보가 응용 프로그램 매니페스트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="47900-132">다시 새 앱의 [Windows 개발자 센터](http://dev.windows.com/overview) 페이지에서 **서비스**, **푸시 알림**, **WNS/MPNS**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="47900-133">**새 알림**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="47900-134">**빈 값(알림)** 템플릿을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="47900-135">알림 **이름** 및 시각적 **컨텍스트** 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="47900-136">그런 후 **임시 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="47900-137">[응용 프로그램 등록 포털](http://apps.dev.microsoft.com)로 이동하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="47900-138">응용 프로그램 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-138">Click on your application name.</span></span> <span data-ttu-id="47900-139">**Windows 스토어** 플랫폼 설정에 있는 **응용 프로그램 비밀** 암호 및 **패키지 SID(보안 식별자)**를 메모해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="47900-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="47900-140">응용 프로그램 암호와 패키지 SID는 중요한 보안 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="47900-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="47900-141">다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="47900-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="47900-142">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="47900-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="47900-143"><b>Notification Services</b> 옵션 및 <b>Windows(WNS)</b> 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="47900-144">그런 다음 <b>보안 키</b> 필드에 <b>응용 프로그램 암호</b> 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="47900-145">이전 섹션의 WNS에서 얻은 <b>패키지 SID</b> 값을 입력한 다음 <b>저장</b>을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="47900-146">이제 알림 허브가 WNS와 작동하도록 구성되었으며 앱을 등록하고 알림을 보내기 위한 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="47900-147">알림 허브에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="47900-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="47900-148">Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭한 후 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="47900-149">그러면 **NuGet 패키지 관리** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="47900-150">`WindowsAzure.Messaging.Managed`를 검색하고 **설치**를 클릭한 후 사용 약관에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="47900-151">그러면 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 패키지</a>를 사용하여 Windows용 Azure 메시징 라이브러리에 대한 참조가 다운로드, 설치 및 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="47900-152">App.xaml.cs 프로젝트 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="47900-153">또한 App.xaml.cs에서 다음과 같은 **InitNotificationsAsync** 메서드 정의를 **App** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="47900-154">이 코드는 WNS에서 앱의 채널 URI를 검색한 후 해당 채널 URI를 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="47900-155">"허브 이름" 자리 표시자를 Azure Portal에 나타나는 알림 허브의 이름으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="47900-156">또한 연결 문자열 자리 표시자를 이전 섹션에 있는 Notification Hub **액세스 정책** 페이지에서 가져온 **DefaultListenSharedAccessSignature** 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="47900-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="47900-157">App.xaml.cs에서 **OnLaunched** 이벤트 처리기의 맨 위에 다음과 같은 새 **InitNotificationsAsync** 메서드 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="47900-158">이 코드는 응용 프로그램이 시작될 때마다 채널 URI가 알림 허브에 등록되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="47900-159">**F5** 키를 눌러 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="47900-160">등록 키가 포함된 팝업 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="47900-161">이제 앱에서 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="47900-162">알림 보내기</span><span class="sxs-lookup"><span data-stu-id="47900-162">Send notifications</span></span>
<span data-ttu-id="47900-163">아래 화면과 같이 알림 허브의 [테스트 보내기](https://portal.azure.com/) 단추를 사용하여 **Azure Portal**에서 알림을 보내 앱의 알림 수신을 신속하게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="47900-164">푸시 알림은 일반적으로 호환 라이브러리를 사용하는 Mobile Services 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="47900-165">백 엔드에 라이브러리를 사용할 수 없는 경우 직접 REST API를 사용하여 알림 메시지를 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="47900-166">이 자습서에서는 과정을 단순하게 유지하고 백엔드 서비스 대신 콘솔 응용 프로그램에서 알림 허브에 .NET SDK를 사용하여 알림을 보내서 클라이언트 앱의 테스트만 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47900-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="47900-167">ASP.NET 백엔드에서 알림을 보내기 위한 다음 단계로 [Notification Hubs를 사용하여 사용자에게 알림 푸시] 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="47900-168">그러나 다음 접근 방식을 사용하여 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="47900-169">**REST 인터페이스**: [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)를 사용하여 백 엔드 플랫폼에서 알림을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="47900-170">**Microsoft Azure Notification Hubs .NET SDK**: Visual Studio용 Nuget 패키지 관리자에서 [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="47900-171">**Node.js** : [Node.js에서 Notification Hubs 사용 방법](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="47900-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="47900-172">**Azure Mobile Apps**: Notification Hubs와 통합된 Azure 모바일 앱에서 알림을 보내는 방법에 대한 예제는 [Mobile Apps에 대한 푸시 알림 추가](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="47900-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="47900-173">**Java / PHP**: REST API를 사용하여 알림을 보내는 방법에 대한 예는 "Java/PHP에서 Notification Hubs를 사용하는 방법"([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md))을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47900-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="47900-174">(선택 사항) 콘솔 응용 프로그램에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="47900-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="47900-175">.NET 콘솔 응용 프로그램을 사용하여 알림을 보내려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="47900-176">솔루션을 마우스 오른쪽 단추로 클릭하고, **추가** 및 **새 프로젝트...**를 선택한 후에 **Visual C#** 아래에서 **Windows** 및 **콘솔 응용 프로그램**을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="47900-177">그러면 새 Visual C# 콘솔 응용 프로그램이 솔루션에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="47900-178">별도의 솔루션에서 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="47900-179">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="47900-180">그러면 Visual Studio에 패키지 관리자 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="47900-181">패키지 관리자 콘솔 창에서 **기본 프로젝트**를 새 콘솔 응용 프로그램 프로젝트로 설정한 후 콘솔 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="47900-182">그러면 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet 패키지</a>를 사용하는 Azure Notification Hubs SDK에 대한 참조가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="47900-183">Program.cs 파일을 열고 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="47900-184">**Program** 클래스에서 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="47900-185">**수신 대기** 권한이 아니라 **모든** 권한을 가진 연결 문자열을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="47900-186">수신 대기 권한 문자열은 알림을 보낼 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="47900-187">**Main** 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="47900-188">Visual Studio에서 콘솔 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트로 설정**을 클릭하여 시작 프로젝트로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="47900-189">그런 다음 **F5** 키를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="47900-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="47900-190">그러면 등록된 모든 장치에 대한 알림 메시지를 수신하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="47900-191">알림 배너를 클릭하거나 누르면 앱이 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="47900-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="47900-192">MSDN의 [알림 카탈로그], [타일 카탈로그] 및 [배지 개요] 항목에서 지원되는 모든 페이로드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47900-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="47900-193">Next steps</span></span>
<span data-ttu-id="47900-194">이 간단한 예제에서는 포털 또는 콘솔 앱을 사용하여 모든 Windows 장치로 브로드캐스트 알림을 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="47900-195">다음 단계로 [Notification Hubs를 사용하여 사용자에게 알림 푸시] 자습서를 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="47900-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="47900-196">특정 사용자를 대상으로 하는 태그를 사용하여 ASP.NET 백엔드에서 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="47900-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="47900-197">사용자를 관심 그룹별로 분할하려면 [Notification Hubs를 사용하여 뉴스 속보 보내기](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="47900-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="47900-198">Notification Hubs에 대한 더 일반적인 정보를 알아보려면 [Notification Hubs 지침](notification-hubs-push-notification-overview.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="47900-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="47900-199">[Notification Hubs를 사용하여 사용자에게 알림 푸시]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="47900-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="47900-200">[Notification Hubs를 사용하여 뉴스 속보 보내기]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="47900-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="47900-201">[알림 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="47900-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="47900-202">[타일 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="47900-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="47900-203">[배지 개요]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="47900-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
