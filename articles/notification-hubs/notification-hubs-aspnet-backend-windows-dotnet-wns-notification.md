---
title: ".NET 백 엔드와 aaaAzure 알림 허브 사용자에 게 알림"
description: "어떻게 toosend 보안의 푸시 알림 Azure에 알아봅니다. Hello.NET API를 사용 하 여 C#으로 작성 된 코드 샘플입니다."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="55eef-104">.NET 백엔드를 통한 Azure 알림 허브의 사용자 알림</span><span class="sxs-lookup"><span data-stu-id="55eef-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="55eef-105">개요</span><span class="sxs-lookup"><span data-stu-id="55eef-105">Overview</span></span>
<span data-ttu-id="55eef-106">Azure의 푸시 알림 지원을 사용 하면 tooaccess는 사용 하기 쉬운, 다중 플랫폼, 및 수평 확장형 푸시 인프라를 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에 대 한 푸시 알림 hello 구현이 크게 간소화 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="55eef-107">이 자습서에서는 toouse Azure 알림 허브 toosend 특정 장치에서 알림을 tooa 특정 응용 프로그램 사용자를 강제 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="55eef-108">ASP.NET WebAPI 백엔드 tooauthenticate 사용 되는 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="55eef-109">Hello를 사용 하 여 클라이언트 사용자를 인증 하 고 hello 백 엔드 toonotification 등록 하 여 태그를 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="55eef-110">이 태그는 특정 사용자에 대 한 hello 백 엔드 toogenerate 알림에 의해 사용 되는 toosend 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="55eef-111">Hello 지침 항목을 참조 하는 앱 백 엔드를 사용 하 여 알림에 등록 하는 방법에 대 한 자세한 내용은 [앱 백 엔드에서 등록](http://msdn.microsoft.com/library/dn743807.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="55eef-112">이 자습서는 hello 알림 허브와 hello에서 만든 프로젝트에 빌드 [알림 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="55eef-113">이 자습서는 또한 hello 필수 toohello [푸시 Secure] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="55eef-114">이 자습서에서는 hello 단계를 완료 한 후 toohello 진행할 수 있습니다 [푸시 Secure] toomodify hello 코드가 방식이 자습서 toosend에 푸시 알림을 안전 하 게 보여 주는 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="55eef-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="55eef-115">Before you begin</span></span>
<span data-ttu-id="55eef-116">사용자 의견을 진지하게 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-116">We do take your feedback seriously.</span></span> <span data-ttu-id="55eef-117">이 항목 또는이 콘텐츠를 개선 하기 위한 권장 사항을 완료 하는 데 문제가 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="55eef-118">이 자습서를 완료 하는 hello 코드 GitHub에서 확인할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="55eef-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="55eef-119">Prerequisites</span></span>
<span data-ttu-id="55eef-120">이 자습서를 시작하려면 먼저 다음 모바일 서비스 자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="55eef-121">[알림 허브 시작]</span><span class="sxs-lookup"><span data-stu-id="55eef-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="55eef-122">알림 허브와 만들고 hello 응용 프로그램 이름 예약,이 자습서에서는 tooreceive 알림을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="55eef-123">이 자습서에서는 다음 단계를 이미 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="55eef-124">그렇지 않은 경우의 hello 단계를 수행 하십시오 [(Windows 스토어) 알림 허브 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), 특히 섹션 hello [hello Windows 스토어에 대 한 앱을 등록](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) 및 [구성 알림 허브](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="55eef-125">특히 hello를 입력 했는지 확인 **패키지 SID** 및 **클라이언트 암호** hello 포털 hello에 대 한 값 **구성** 알림 허브에 대 한 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="55eef-126">이 구성 절차 hello 섹션에 설명 되어 [알림 허브 구성](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="55eef-127">이 중요 한 단계: hello 포털에서 자격 증명 hello 일치 하지 않으면 지정 된 hello 앱 이름을 선택 하면에 대 한 푸시 알림 hello에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="55eef-128">백 엔드 서비스로 Azure 앱 서비스에서 모바일 앱을 사용 하는 경우 참조 hello [모바일 앱 버전](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) 이 자습서의 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="55eef-129">Hello 클라이언트 프로젝트에 대 한 hello 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="55eef-129">Update hello code for hello client project</span></span>
<span data-ttu-id="55eef-130">Hello에 대 한 완료 하는 hello 프로젝트에서 hello 코드를 업데이트 하면이 섹션에서는 [알림 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="55eef-131">이미 hello hello 저장소와 연결 된 고 알림 허브에 대해 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="55eef-132">이 섹션에서는 코드 toocall hello 새 WebAPI 백 엔드를 추가 하 고 등록 하 고 알림을 보낼에 대 한 사용.</span><span class="sxs-lookup"><span data-stu-id="55eef-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="55eef-133">Visual Studio에서 만든 hello에 대 한 hello hello 솔루션을 엽니다 [알림 허브 시작] 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="55eef-134">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **(Windows 8.1)** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="55eef-135">Hello 왼쪽에 클릭 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="55eef-136">Hello에 **검색** 상자에서 입력 **Http 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="55eef-137">Hello 결과 목록에서 클릭 **Microsoft HTTP 클라이언트 라이브러리**, 클릭 하 고 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="55eef-138">Hello 설치를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-138">Complete hello installation.</span></span>
6. <span data-ttu-id="55eef-139">NuGet hello에 다시 **검색** 상자에서 입력 **Json.net**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="55eef-140">Hello 설치 **Json.NET** 패키지 및 종가 hello NuGet 패키지 관리자 창.</span><span class="sxs-lookup"><span data-stu-id="55eef-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="55eef-141">Hello에 대 한 위의 hello 단계를 반복 **(Windows Phone 8.1)** 프로젝트 tooinstall hello **JSON.NET** hello Windows Phone 프로젝트에 대 한 NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="55eef-142">Hello의 솔루션 탐색기에서 **(Windows 8.1)** 두 번 클릭 **MainPage.xaml** tooopen hello Visual Studio 편집기에서.</span><span class="sxs-lookup"><span data-stu-id="55eef-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="55eef-143">Hello에 **MainPage.xaml** XML 코드를 바꾸기 hello `<Grid>` 코드 다음 hello로 섹션.</span><span class="sxs-lookup"><span data-stu-id="55eef-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="55eef-144">이 코드를 추가 hello 사용자는 사용자 이름 및 암호 텍스트 상자에 인증 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="55eef-145">또한 hello 알림 메시지 및 hello 알림을 받아야 하는 hello username 태그에 대 한 입력란을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="55eef-146">Hello의 솔루션 탐색기에서 **(Windows Phone 8.1)** 프로젝트, 열기 **MainPage.xaml** 및 Windows Phone 8.1 hello 바꾸기 `<Grid>` 위의 같은 코드를 사용 하 여 섹션.</span><span class="sxs-lookup"><span data-stu-id="55eef-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="55eef-147">hello 인터페이스 아래에 표시 된 유사한 toowhats 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="55eef-148">솔루션 탐색기에서 엽니다 hello **MainPage.xaml.cs** hello에 대 한 파일 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="55eef-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="55eef-149">Hello 다음 추가 `using` hello 위쪽 두 파일의 문:</span><span class="sxs-lookup"><span data-stu-id="55eef-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="55eef-150">**MainPage.xaml.cs** hello에 대 한 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트, 추가 멤버 toohello 다음 hello `MainPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="55eef-151">수 있는지 tooreplace `<Enter Your Backend Endpoint>` hello로 실제 백 엔드 끝점 이전에 얻은 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="55eef-152">예: `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="55eef-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="55eef-153">Hello에 toohello MainPage 클래스 아래에 코드 추가 **MainPage.xaml.cs** hello에 대 한 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="55eef-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="55eef-154">hello `PushClick` 메서드는 hello 클릭 hello에 대 한 처리기 **푸시 보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="55eef-155">Hello 백 엔드 tootrigger 알림 tooall hello와 일치 하는 사용자 이름 태그를 사용 하 여 장치 호출 `to_tag` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="55eef-156">hello 알림 메시지가 hello 요청 본문의 JSON 내용으로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="55eef-157">hello `LoginAndRegisterClick` 메서드는 hello 클릭 hello에 대 한 처리기 **에 로그인 하 고 등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="55eef-158">Hello basic 저장 로컬 저장소 (이 인증 체계를 사용 하는 모든 토큰 참고)에서 인증 토큰을 사용 하 여 `RegisterClient` tooregister hello 백 엔드를 사용 하 여 알림에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="55eef-159">솔루션 탐색기에서 hello **Shared** 프로젝트, 열기 hello **App.xaml.cs** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="55eef-160">너무 hello 호출을 찾으려면`InitNotificationsAsync()` hello에 `OnLaunched()` 이벤트 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="55eef-161">주석으로 처리 하거나 너무 hello 호출 삭제`InitNotificationsAsync()`합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="55eef-162">hello 단추 처리기 위에 추가 알림 등록을 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="55eef-163">솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Shared** 프로젝트를 선택한 다음 클릭 **추가**, 클릭 하 고 **클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="55eef-164">Hello 클래스 이름을 **RegisterClient.cs**, 클릭 **확인** toogenerate hello 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="55eef-165">이 클래스에 푸시 알림을 순서 tooregister hello REST 호출 필요한 toocontact hello 앱 백 엔드를, 줄 바꿈됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="55eef-166">또한 로컬로 hello 저장 *registrationIds* 알림 허브에 설명 된 대로 hello에서 만든 [앱 백 엔드에서 등록](http://msdn.microsoft.com/library/dn743807.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="55eef-167">Hello를 클릭할 때 로컬 저장소에 저장 하는 권한 부여 토큰을 사용 하 여 참고 **에 로그인 하 고 등록** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="55eef-168">Hello 다음 추가 `using` hello RegisterClient.cs 파일의 맨 위에 hello에 문을:</span><span class="sxs-lookup"><span data-stu-id="55eef-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="55eef-169">Hello hello 내부에서 코드를 다음 추가 `RegisterClient` 클래스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="55eef-170">변경 내용을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="55eef-171">Hello 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="55eef-171">Testing hello Application</span></span>
1. <span data-ttu-id="55eef-172">Windows 8.1 및 Windows Phone 8.1 모두에 hello 응용 프로그램을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="55eef-173">Windows Phone 8.1에 대 한 hello 인스턴스 hello 에뮬레이터 나 실제 장치에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="55eef-174">Hello 앱의 Windows 8.1 hello 인스턴스를 입력 한 **Username** 및 **암호** hello 화면 아래에 표시 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="55eef-175">Hello 사용자 이름 및 Windows Phone 입력 한 암호가에서 다를 수는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="55eef-176">**Log in and register(로그인 및 등록)** 를 클릭하고 대화 상자에 로그인되었다고 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="55eef-177">이렇게 하면 hello 사용도 **푸시 보낼** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="55eef-178">Windows Phone 8.1 hello 인스턴스 두 hello에 사용자 이름 문자열로 입력 **Username** 및 **암호** 필드를 클릭 한 다음 **로그인 및 등록**합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="55eef-179">Hello 그런 다음 **받는 사용자 이름 태그** 필드에, Windows 8.1 등록 하는 hello 사용자 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="55eef-180">알림 메시지를 입력하고 **Send Push(푸시 전송)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="55eef-181">일치 하는 사용자 이름 태그 hello 등록 hello 장치만 hello 알림 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="55eef-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55eef-182">Next Steps</span></span>
* <span data-ttu-id="55eef-183">Toosegment 관심 그룹으로 사용자, 참조 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="55eef-184">toouse 알림 허브 참조 하는 방법에 대 한 자세한 toolearn [알림 허브 지침]합니다.</span><span class="sxs-lookup"><span data-stu-id="55eef-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[알림 허브 시작]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[푸시 Secure]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[최신 뉴스 사용 하 여 알림 허브 toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx
