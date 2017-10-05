---
title: ".NET 백엔드를 통한 Azure 알림 허브의 사용자 알림"
description: "Azure에서 보안 푸시 알림을 보내는 방법에 대해 알아봅니다. 코드 샘플은 .NET API를 사용하여 C#으로 작성되었습니다."
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
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="9746a-104">.NET 백엔드를 통한 Azure 알림 허브의 사용자 알림</span><span class="sxs-lookup"><span data-stu-id="9746a-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="9746a-105">개요</span><span class="sxs-lookup"><span data-stu-id="9746a-105">Overview</span></span>
<span data-ttu-id="9746a-106">Azure의 푸시 알림 지원을 통해 사용하기 쉬운 다중 플랫폼 및 규모 확장 푸시 인프라에 액세스할 수 있어, 모바일 플랫폼용 소비자 응용 프로그램 및 엔터프라이즈 응용 프로그램 모두에 대한 푸시 알림을 매우 간단하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="9746a-107">이 자습서에서는 Azure 알림 허브를 사용하여 특정 장치에서 특정 앱 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="9746a-108">ASP.NET WebAPI 백 엔드는 클라이언트를 인증하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="9746a-109">인증된 클라이언트 사용자를 사용하면 백 엔드에 의해 태그가 자동으로 알림 등록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="9746a-110">이 태그는 백 엔드에서 특정 사용자에 대해 알림을 생성하고 보내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="9746a-111">앱 백 엔드를 사용하여 알림에 등록하는 방법에 대한 자세한 내용은 지침 항목 [앱 백 엔드에서 등록](http://msdn.microsoft.com/library/dn743807.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9746a-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="9746a-112">이 자습서는 [알림 허브 시작] 자습서에서 만든 알림 허브 및 프로젝트를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="9746a-113">이 자습서는 [보안 푸시] 자습서의 필수 조건이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="9746a-114">이 자습서의 단계를 완료해야 푸시 알림을 안전하게 보내도록 이 자습서의 코드를 수정하는 방법을 보여주는 [보안 푸시] 자습서를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9746a-115">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9746a-115">Before you begin</span></span>
<span data-ttu-id="9746a-116">사용자 의견을 진지하게 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-116">We do take your feedback seriously.</span></span> <span data-ttu-id="9746a-117">이 항목을 완료하기가 어렵거나 이 콘텐츠를 개선할 사항이 있는 경우 페이지의 맨 아래에 의견을 보내주시면 감사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="9746a-118">이 자습서에 대해 완료된 코드는 GitHub의 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9746a-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9746a-119">Prerequisites</span></span>
<span data-ttu-id="9746a-120">이 자습서를 시작하려면 먼저 다음 모바일 서비스 자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="9746a-121">[알림 허브 시작]</span><span class="sxs-lookup"><span data-stu-id="9746a-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="9746a-122">알림 허브를 만들고 앱 이름을 예약하고 이 자습서의 알림을 받도록 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="9746a-123">이 자습서에서는 다음 단계를 이미 완료했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="9746a-124">그렇지 않은 경우 [Notification Hubs 시작(Windows 스토어)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), 특히 [Windows 스토어에 앱 등록](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) 및 [Notification Hub 구성](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub) 섹션의 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="9746a-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="9746a-125">특히 알림 허브의 **구성** 탭에서 포털의 **패키지 SID** 및 **클라이언트 암호** 값을 입력했어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="9746a-126">이 구성 절차는 [Notification Hub 구성](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub) 섹션에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="9746a-127">이는 중요한 단계입니다. 포털의 자격 증명이 선택한 앱 이름에 대해 지정된 자격 증명과 일치하지 않으면 푸시 알림이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="9746a-128">Azure App Service의 Mobile Apps를 백 엔드 서비스로 사용 중인 경우 이 자습서의 [Mobile Apps 버전](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9746a-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="9746a-129">클라이언트 프로젝트에 대한 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="9746a-129">Update the code for the client project</span></span>
<span data-ttu-id="9746a-130">이 섹션에서는 [알림 허브 시작] 자습서에 대해 완료한 프로젝트의 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="9746a-131">이미 저장소와 연결되어 알림 허브에 대해 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="9746a-132">이 섹션에서는 새 WebAPI 백 엔드를 호출할 코드를 추가하고, 알림을 등록하고 보내는 데 이 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="9746a-133">Visual Studio에서 [알림 허브 시작] 자습서에 대해 만든 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="9746a-134">솔루션 탐색기에서 **(Windows 8.1)** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="9746a-135">왼쪽에서 **온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="9746a-136">**검색** 상자에 **Http 클라이언트**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="9746a-137">결과 목록에서 **Microsoft HTTP 클라이언트 라이브러리**를 클릭하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="9746a-138">설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-138">Complete the installation.</span></span>
6. <span data-ttu-id="9746a-139">다시 NuGet **검색** 상자에 **Json.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="9746a-140">**Json.NET** 패키지를 설치하고 NuGet 패키지 관리자 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="9746a-141">**(Windows Phone 8.1)** 프로젝트에 대해 위의 단계를 반복하여 Windows Phone 프로젝트에 대해 **JSON.NET** NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="9746a-142">솔루션 탐색기의 **(Windows 8.1)** 프로젝트에서 **MainPage.xaml**을 두 번 클릭하여 Visual Studio 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="9746a-143">**MainPage.xaml** XML 코드에서 `<Grid>` 섹션을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="9746a-144">이 코드는 사용자가 인증하는 데 사용할 사용자 이름 및 암호 텍스트 상자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="9746a-145">또한 알림 메시지 및 알림을 받을 사용자 이름 태그용 텍스트 상자도 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
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
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="9746a-146">솔루션 탐색기의 **(Windows Phone 8.1)** 프로젝트에서 **MainPage.xaml**을 열고 Windows Phone 8.1 `<Grid>` 바꾸기 섹션을 위와 동일한 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="9746a-147">인터페이스는 아래 표시된 것과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="9746a-148">솔루션 탐색기에서 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트의 **MainPage.xaml.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="9746a-149">두 파일의 맨 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="9746a-150">**(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트의 **MainPage.xaml.cs**에서 다음 멤버를 `MainPage` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="9746a-151">`<Enter Your Backend Endpoint>` 을 이전에 얻은 실제 백 엔드 끝점으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="9746a-152">예: `http://mybackend.azurewebsites.net`</span><span class="sxs-lookup"><span data-stu-id="9746a-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="9746a-153">**(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트의 **MainPage.xaml.cs**에서 아래 코드를 MainPage 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="9746a-154">`PushClick` 메서드는 **Send Push(푸시 전송)** 단추의 클릭 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="9746a-155">`to_tag` 매개 변수와 일치하는 사용자 이름 태그가 있는 모든 장치로 알림을 트리거하도록 백 엔드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="9746a-156">알림 메시지는 요청 본문의 JSON 콘텐츠로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="9746a-157">`LoginAndRegisterClick` 메서드는 **Log in and register(로그인 및 등록)** 단추의 클릭 처리기입니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="9746a-158">기본 인증 토큰(이는 인증 체계에서 사용하는 모든 토큰을 나타냄)을 로컬 저장소에 저장하고 `RegisterClient` 를 사용하여 백 엔드가 사용되는 알림에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

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
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
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



1. <span data-ttu-id="9746a-159">솔루션 탐색기의 **공유** 프로젝트 아래에서 **App.xaml.cs** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="9746a-160">`InitNotificationsAsync()` in the `OnLaunched()` 에 대한 호출을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="9746a-161">`InitNotificationsAsync()`에 대한 호출을 주석으로 처리하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="9746a-162">위에서 추가한 단추 처리기는 알림 등록을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="9746a-163">솔루션 탐색기에서 **공유** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="9746a-164">클래스 이름을 **RegisterClient.cs**로 지정하고 **확인**을 클릭하여 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="9746a-165">이 클래스는 푸시 알림에 등록하기 위해 앱 백 엔드에 접속하는 데 필요한 REST 호출을 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="9746a-166">또한 *앱 백 엔드에서 등록* 에 설명된 대로 알림 허브에서 생성된 [registrationId](http://msdn.microsoft.com/library/dn743807.aspx)를 로컬로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="9746a-167">이 구성 요소는 **로그인 및 등록** 단추를 클릭할 때 로컬 저장소에 저장된 인증 토큰을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="9746a-168">RegisterClient.cs 파일의 맨 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="9746a-169">다음 코드를 `RegisterClient` 클래스 정의 내에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="9746a-170">변경 내용을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="9746a-171">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="9746a-171">Testing the Application</span></span>
1. <span data-ttu-id="9746a-172">Windows 8.1 및 Windows Phone 8.1 모두에서 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="9746a-173">Windows Phone 8.1의 경우 에뮬레이터 또는 실제 장치에서 인스턴스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="9746a-174">앱의 Windows 8.1 인스턴스에서 아래 화면에 표시된 것처럼 **사용자 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="9746a-175">Windows Phone에서 입력하는 사용자 이름 및 암호와 달라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="9746a-176">**Log in and register(로그인 및 등록)** 를 클릭하고 대화 상자에 로그인되었다고 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="9746a-177">이렇게 하면 **Send Push(푸시 전송)** 단추도 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="9746a-178">Windows Phone 8.1 인스턴스에서 **사용자 이름** 및 **암호** 필드 모두에 사용자 이름 문자열을 입력하고 **Log in and register(로그인 및 등록)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="9746a-179">그런 다음 **받는 사람 사용자 이름 태그** 필드에 Windows 8.1에서 등록한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="9746a-180">알림 메시지를 입력하고 **Send Push(푸시 전송)**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="9746a-181">일치하는 사용자 이름 태그로 등록된 장치만 이 알림 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9746a-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="9746a-182">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9746a-182">Next Steps</span></span>
* <span data-ttu-id="9746a-183">사용자를 관심 그룹별로 분할하려면 [알림 허브를 사용하여 뉴스 속보 보내기](영문)를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9746a-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="9746a-184">알림 허브에 대한 자세한 내용은 [알림 허브 지침]을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="9746a-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="9746a-185">[알림 허브 시작]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="9746a-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="9746a-186">[보안 푸시]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="9746a-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="9746a-187">[알림 허브를 사용하여 뉴스 속보 보내기]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="9746a-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="9746a-188">[알림 허브 지침]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="9746a-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
