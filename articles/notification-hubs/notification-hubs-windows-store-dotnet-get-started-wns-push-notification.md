---
title: "Azure 알림 허브에 대 한 Windows 유니버설 플랫폼 앱 aaaGet 시작 | Microsoft Docs"
description: "이 자습서에 설명 어떻게 toouse Azure 알림 허브 toopush 알림 tooa 유니버설 Windows 플랫폼 응용 프로그램입니다."
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
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="0977e-103">Windows 유니버설 플랫폼 앱용 Notification Hubs 시작</span><span class="sxs-lookup"><span data-stu-id="0977e-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0977e-104">개요</span><span class="sxs-lookup"><span data-stu-id="0977e-104">Overview</span></span>
<span data-ttu-id="0977e-105">이 자습서에서는 Azure 알림 허브 toosend toouse 밀어넣기 알림 tooa 유니버설 Windows 플랫폼 (UWP) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="0977e-106">이 자습서에서는 Windows 푸시 알림 서비스 (WNS) hello를 사용 하 여 푸시 알림을 수신 하는 빈 Windows 스토어 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="0977e-107">수 toouse 수 완료 되 면 알림 허브 toobroadcast 푸시 알림을 tooall hello 장치 앱을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0977e-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0977e-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="0977e-109">이 자습서를 완료 하는 hello 코드 GitHub에서 확인할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0977e-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0977e-110">Prerequisites</span></span>
<span data-ttu-id="0977e-111">이 자습서는 hello 다음을 사항이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="0977e-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) 이상 버전</span><span class="sxs-lookup"><span data-stu-id="0977e-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="0977e-113">유니버설 Windows 앱 개발 도구 설치</span><span class="sxs-lookup"><span data-stu-id="0977e-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="0977e-114">활성 Azure 계정 </span><span class="sxs-lookup"><span data-stu-id="0977e-114">An active Azure account</span></span> <br/><span data-ttu-id="0977e-115">계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="0977e-116">자세한 내용은 [Azure 무료 체험](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0977e-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="0977e-117">활성 Windows 스토어 계정</span><span class="sxs-lookup"><span data-stu-id="0977e-117">An active Windows Store account</span></span>

<span data-ttu-id="0977e-118">이 자습서를 완료해야 다른 모든 Windows 유니버설 플랫폼 앱용 Notification Hubs 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="0977e-119">Hello Windows 스토어에 앱 등록</span><span class="sxs-lookup"><span data-stu-id="0977e-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="0977e-120">toosend 푸시 알림을 tooUWP 응용 프로그램, Windows 스토어에 앱 toohello를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="0977e-121">WNS 있는 알림 허브 toointegrate를 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="0977e-122">이미 앱을 등록 하지 않은 경우 탐색 toohello [Windows 개발자 센터](https://dev.windows.com/overview), Microsoft 계정으로 로그인 하 고 클릭 **새 앱 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="0977e-123">앱의 이름을 입력하고 **앱 이름 예약**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="0977e-124">이렇게 하면 앱을 새로 Windows 스토어에 등록하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="0977e-125">Visual Studio에서 유니버설 Windows hello를 사용 하 여 새 Visual C# 스토어 앱 프로젝트를 만들 **비어 있는 앱** 템플릿을 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="0977e-126">Hello 대상과 최소 플랫폼 버전에 대 한 hello 기본값을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="0977e-127">솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello Windows 스토어 응용 프로그램 프로젝트에서에서 클릭 **저장소**, 클릭 하 고 **hello 저장소로 응용 프로그램 연결 중...** . hello **연결로 앱을 Windows 스토어 hello** 마법사가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="0977e-128">Hello 마법사에서 Microsoft 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="0977e-129">2 단계에서 등록 된 hello 앱, **다음**, 클릭 하 고 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="0977e-130">이 hello 필요한 Windows 스토어 등록 정보 toohello 응용 프로그램 매니페스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="0977e-131">Hello에 다시 [Windows 개발자 센터](http://dev.windows.com/overview) 새 앱에 대 한 페이지에서 클릭 **서비스**, 클릭 **푸시 알림**, 클릭 하 고 **WNS/MPNS**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="0977e-132">**새 알림**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="0977e-133">**빈 값(알림)** 템플릿을 클릭하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="0977e-134">알림 **이름** 및 시각적 **컨텍스트** 메시지를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="0977e-135">그런 후 **임시 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="0977e-136">Toohello 이동 [응용 프로그램 등록 포털](http://apps.dev.microsoft.com) 로그인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="0977e-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="0977e-137">응용 프로그램 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-137">Click on your application name.</span></span> <span data-ttu-id="0977e-138">Hello 메모 **응용 프로그램 암호** 암호 및 hello **패키지 보안 식별자 (SID)** hello에 **Windows 스토어** 플랫폼 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="0977e-139">hello 응용 프로그램 암호와 패키지 SID는 중요 한 보안 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="0977e-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="0977e-140">다른 사람과 공유하지 말고 앱과 함께 분산하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0977e-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="0977e-141">알림 허브 구성</span><span class="sxs-lookup"><span data-stu-id="0977e-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="0977e-142">선택 hello <b>Notification Services</b> 옵션과 hello <b>WNS (Windows)</b> 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="0977e-143">다음 입력 hello <b>응용 프로그램 암호</b> hello에 암호 <b>보안 키</b> 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="0977e-144">입력 프로그램 <b>패키지 SID</b> hello 이전 단원의 WNS에서 가져온을 클릭 한 다음 값 <b>저장</b>합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="0977e-145">알림 허브 이제 WNS와 함께 구성 된 toowork 이며 앱 hello 연결 문자열 tooregister 있어야 하 고 알림을 보낼 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="0977e-146">응용 프로그램 toohello 알림 허브를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="0977e-147">Visual Studio에서 hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="0977e-148">Hello 표시 **NuGet 패키지 관리** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0977e-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="0977e-149">검색할 `WindowsAzure.Messaging.Managed` 클릭 **설치**, hello 사용 약관을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="0977e-150">다운로드이 설치 하 고 hello를 사용 하 여 Windows 용 참조 toohello Azure 메시징 라이브러리 추가 <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet 패키지</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="0977e-151">Hello App.xaml.cs 프로젝트 파일을 열고 hello 다음 추가 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="0977e-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="0977e-152">또한, App.xaml.cs에 hello 다음 추가 **InitNotificationsAsync** 메서드 정의 toohello **앱** 클래스:</span><span class="sxs-lookup"><span data-stu-id="0977e-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="0977e-153">이 코드는 WNS에서 hello 앱에 대 한 hello 채널 URI를 검색 하 고 알림 허브에 해당 채널 URI를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0977e-154">"허브 이름" hello Azure 포털에에서 표시 되는 hello 알림 허브의 hello 이름 자리 표시자 hello 있는지 tooreplace를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="0977e-155">또한 hello로 hello 연결 문자열 자리 표시자를 대체 **DefaultListenSharedAccessSignature** 연결 문자열 hello에서 가져온 **액세스 정책은** 에서 알림 허브의 페이지는 이전 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="0977e-156">Hello의 hello 위쪽 **OnLaunched** App.xaml.cs, 이벤트 처리기 추가 호출 toohello 새 다음 hello **InitNotificationsAsync** 메서드:</span><span class="sxs-lookup"><span data-stu-id="0977e-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="0977e-157">이렇게 하면 해당 hello 채널 URI 각 시간 hello 응용 프로그램이 시작 하 여 알림 허브에 등록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="0977e-158">키를 눌러 hello **F5** 키 toorun hello 앱.</span><span class="sxs-lookup"><span data-stu-id="0977e-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="0977e-159">Hello 등록 키를 포함 하는 팝업 대화 상자가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="0977e-160">이제 앱이 준비 tooreceive 알림 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="0977e-161">알림 보내기</span><span class="sxs-lookup"><span data-stu-id="0977e-161">Send notifications</span></span>
<span data-ttu-id="0977e-162">Hello에 알림을 전송 하 여 앱에서 알림 받기 신속 하 게 테스트할 수 있습니다 [Azure 포털](https://portal.azure.com/) hello를 사용 하 여 **테스트 보내기** hello 화면 아래에 나와 있는 것 처럼 hello 알림 허브에서 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="0977e-163">푸시 알림은 일반적으로 호환 라이브러리를 사용하는 Mobile Services 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="0977e-164">또한 toosend 알림 메시지는 라이브러리 백 엔드에 대해 사용할 수 없는 경우 직접 hello REST API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="0977e-165">이 자습서에서는 단순하게 유지 하 고 방금 hello.NET SDK를 사용 하 여 백 엔드 서비스는 대신 콘솔 응용 프로그램에서 알림 허브에 대 한 알림을 전송 하 여 클라이언트 앱을 테스트를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="0977e-166">Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] ASP.NET 백 엔드에서 알림을 보내기 위한 hello 다음 단계로 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="0977e-167">그러나 다음 방법 hello 알림을 보내는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="0977e-168">**REST 인터페이스**: hello를 사용 하 여 모든 백 엔드 플랫폼에서 알림을 지원할 수 있습니다 [REST 인터페이스](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="0977e-169">**Microsoft Azure 알림 허브.NET SDK**: Visual Studio 용 Nuget 패키지 관리자 hello 실행 [Install-package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="0977e-170">**Node.js** : [어떻게 toouse Node.js에서 알림 허브](notification-hubs-nodejs-push-notification-tutorial.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="0977e-171">**Azure 모바일 앱**: 방법의 예에 대 한 알림 허브와 통합 되는 Azure 모바일 앱에서 알림을 toosend 참조 [모바일 앱에 대 한 푸시 알림 추가](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="0977e-172">**Java / PHP**: toosend 알림을 사용 하 여 REST Api를 hello 하는 방법의 예제를 보려면 "어떻게 toouse Java/PHP에서 알림 허브" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="0977e-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="0977e-173">(선택 사항) 콘솔 응용 프로그램에서 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="0977e-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="0977e-174">toosend 알림을.NET 콘솔 응용 프로그램을 사용 하 여 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="0977e-175">마우스 오른쪽 단추로 클릭 hello 솔루션을 선택 **추가** 및 **새 프로젝트...** , 그 다음 **Visual C#**, 클릭 **Windows** 및 **콘솔 응용 프로그램**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="0977e-176">이 새 Visual C# 콘솔 응용 프로그램 toohello 솔루션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="0977e-177">별도의 솔루션에서 이 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="0977e-178">Visual Studio에서 **도구**를 클릭하고 **NuGet 패키지 관리자**를 클릭한 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="0977e-179">Visual Studio에서 패키지 관리자 콘솔 hello 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="0977e-180">Hello 패키지 관리자 콘솔 창에서에서 설정 hello **기본 프로젝트** tooyour 새 콘솔 응용 프로그램 프로젝트를 선택한 다음 hello 콘솔 창에 다음 명령을 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="0977e-181">이렇게 하면 추가 참조 toohello Azure 알림 허브 SDK hello를 사용 하 여 <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification 허브 NuGet 패키지</a>합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="0977e-182">Hello Program.cs 파일을 열고 hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="0977e-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="0977e-183">Hello에 **프로그램** 클래스, 메서드 뒤 hello 추가:</span><span class="sxs-lookup"><span data-stu-id="0977e-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="0977e-184">Hello 연결 문자열을 사용 하 고 있는지 확인 **전체** 액세스 되지 **수신** 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="0977e-185">hello 수신 액세스 문자열에는 사용 권한을 toosend 알림이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="0977e-186">Hello에 있는 줄을 다음 hello 추가 **Main** 메서드:</span><span class="sxs-lookup"><span data-stu-id="0977e-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="0977e-187">Visual Studio에서 hello 콘솔 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작 프로젝트로 설정** tooset hello 시작 프로젝트로 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="0977e-188">Hello 키를 누릅니다 **F5** toorun hello 응용 프로그램 키입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="0977e-189">그러면 등록된 모든 장치에 대한 알림 메시지를 수신하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="0977e-190">클릭 하거나 눌러 hello 알림을 배너 hello 앱을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="0977e-191">Hello에서 모든 지원 되는 hello 페이로드를 찾을 수 있습니다 [알림 카탈로그], [타일 카탈로그], 및 [개요 배지] msdn 항목.</span><span class="sxs-lookup"><span data-stu-id="0977e-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0977e-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0977e-192">Next steps</span></span>
<span data-ttu-id="0977e-193">이 간단한 예제에서는 브로드캐스트 알림을 tooall hello 포털 또는 콘솔 응용 프로그램을 사용 하 여 Windows 장치를 보냈습니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="0977e-194">Hello 권장 [사용 하 여 알림 허브 toopush 알림 toousers] hello 다음 단계로 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="0977e-195">설명에서 사용 하 여 ASP.NET 백 엔드 toosend 알림을 tootarget 특정 사용자에 게 태그를 삽입 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="0977e-196">Toosegment 관심 그룹으로 사용자, 참조 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="0977e-197">toolearn 알림 허브에 대 한 자세한 내용은 [알림 허브 지침](notification-hubs-push-notification-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0977e-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[사용 하 여 알림 허브 toopush 알림 toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[알림 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[타일 카탈로그]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[개요 배지]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
