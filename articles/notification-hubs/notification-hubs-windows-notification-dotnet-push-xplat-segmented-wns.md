---
title: "알림 허브를 사용하여 속보 보내기(Windows Universal)"
description: "등록된 태그와 함께 Azure 알림 허브를 사용하여 범용 Windows 앱에 최신 뉴스를 보낼 수 있습니다."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="95982-103">알림 허브를 사용하여 속보 보내기</span><span class="sxs-lookup"><span data-stu-id="95982-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="95982-104">개요</span><span class="sxs-lookup"><span data-stu-id="95982-104">Overview</span></span>
<span data-ttu-id="95982-105">이 항목에서는 Azure 알림 허브를 사용하여 Windows 스토어 또는 Windows Phone 8.1(비 Silverlight) 앱에 속보 알림을 브로드캐스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95982-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="95982-106">Windows Phone 8.1 Silverlight를 대상으로 하는 경우 [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) 버전을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95982-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="95982-107">완료하면, 관심이 있는 속보 범주를 등록하고 해당 범주의 푸시 알림만 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="95982-108">이 시나리오는 RSS 수집기, 음악 애호가를 위한 앱 등 이전에 관심을 보인 사용자 그룹에 알림을 보내야 하는 많은 앱에 공통된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="95982-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="95982-109">브로드캐스트 시나리오를 사용하려면 알림 허브에서 등록을 만들 때 하나 이상의 *태그*를 포함하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="95982-110">태그에 알림이 전송되면 태그에 대해 등록된 모든 장치에서 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="95982-111">태그는 단순히 문자열이므로 사전에 프로비전해야 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="95982-112">태그에 대한 자세한 내용은 [알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95982-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="95982-113">Windows 스토어 및 Windows Phone 프로젝트 버전 8.1 및 이전 버전은 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="95982-114">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95982-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="95982-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95982-115">Prerequisites</span></span>
<span data-ttu-id="95982-116">이 항목은 [Notification Hubs 시작][get-started]에서 만든 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="95982-117">이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="95982-118">앱에 범주 선택 추가</span><span class="sxs-lookup"><span data-stu-id="95982-118">Add category selection to the app</span></span>
<span data-ttu-id="95982-119">첫 번째 단계는 기존의 기본 페이지에 사용자가 등록할 범주를 선택할 수 있도록 하는 UI 요소를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95982-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="95982-120">사용자가 선택한 범주는 장치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="95982-121">앱을 시작하면 장치 등록이 선택한 범주와 함께 태그로서 알림 허브에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="95982-122">MainPage.xaml 프로젝트 파일을 열고 **Grid** 요소에서 다음 코드를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="95982-123">**Shared** 프로젝트에서 **Notifications**라는 이름의 새 클래스를 만들고, 클래스 정의에 **public** 한정자를 추가하고, 다음 **using** 문을 새 코드 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="95982-124">다음 코드를 새 **Notifications** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-124">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="95982-125">이 클래스는 로컬 저장소를 사용하여, 이 장치에서 받아야 할 뉴스의 범주를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="95982-126">*RegisterNativeAsync* 메서드를 호출하는 대신 템플릿 등록을 사용하여 범주에 등록하는 *RegisterTemplateAsync*를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="95982-127">또한 알림 메시지용 템플릿, 타일 알림용 템플릿 등 여러 템플릿을 등록할 수도 있으므로 템플릿의 이름("simpleWNSTemplateExample")을 제공합니다. 그런 다음 템플릿을 업데이트하거나 삭제하려면 해당 이름을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="95982-128">장치에서 동일한 태그로 여러 템플릿을 등록한 경우 해당 태그를 대상으로 하는 수신 메시지는 템플릿별로 하나씩 여러 알림을 장치에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="95982-129">이 동작은 동일한 논리 메시지로 여러 시각적 알림을 나타내야 하는 경우(예: Windows 스토어 응용 프로그램에 배지와 알림을 모두 표시해야 하는 경우)에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="95982-130">템플릿 사용에 대한 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95982-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="95982-131">App.xaml.cs 프로젝트 파일에서 **App** 클래스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="95982-132">이 속성은 **Notifications** 인스턴스를 만들고 액세스하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="95982-133">위 코드에서 `<hub name>`과 `<connection string with listen access>` 자리 표시자를 알림 허브 이름과 앞서 얻었던 *DefaultListenSharedAccessSignature*의 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="95982-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95982-134">클라이언트 앱과 함께 배포되는 자격 증명은 일반적으로 안전하지 않기 때문에 클라이언트 앱과 함께 listen access용 키만 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="95982-135">Listen access를 통해 앱에서 알림을 등록할 수 있지만, 기존 등록을 수정할 수 없으며 알림을 전송할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="95982-136">안전한 백 엔드 서비스에서 알림을 보내고 기존 등록을 변경하는 데에는 모든 액세스 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="95982-137">MainPage.xaml.cs에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="95982-138">MainPage.xaml.cs 프로젝트 파일에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="95982-139">이 메서드는 범주 목록을 만들고 **Notifications** 클래스를 사용하여, 로컬 저장소에 목록을 저장하고 알림 허브에 해당 태그를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="95982-140">범주가 변경되면 새 범주로 등록이 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="95982-141">이제 사용자가 범주 선택을 변경할 때마다 앱은 범주 집합을 장치의 로컬 저장소에 저장하고 알림 허브에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="95982-142">알림 등록</span><span class="sxs-lookup"><span data-stu-id="95982-142">Register for notifications</span></span>
<span data-ttu-id="95982-143">다음 단계에서는 로컬 저장소에 저장된 범주를 사용하여 시작 시 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="95982-144">WNS(Windows 알림 서비스)에서 할당하는 채널 URI는 언제든지 변경될 수 있으므로 알림 실패를 피하려면 알림을 자주 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="95982-145">이 예제에서는 앱이 시작될 때마다 알림을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="95982-146">자주(하루 두 번 이상) 실행되는 앱에서는 이전 등록 이후 만 하루가 지나지 않은 경우 대역폭 유지를 위한 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="95982-147">App.xaml.cs 파일을 열고 범주를 기반으로 구독하는 `notifications` 클래스를 사용하도록 **InitNotificationsAsync** 메서드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="95982-148">이제 앱이 시작될 때마다 로컬 저장소에서 범주를 검색하고, 이러한 범주에 대한 등록을 요청하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="95982-149">**InitNotificationsAsync** 메서드는 [Notification Hubs 시작][get-started] 자습서의 일부로 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="95982-150">MainPage.xaml.cs 프로젝트 파일의 *OnNavigatedTo* 메서드에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="95982-151">전에 저장한 범주의 상태를 기반으로 기본 페이지가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="95982-152">이제 앱이 완료되며, 사용자가 범주 선택을 변경할 때마다 알림 허브 등록에 사용된 장치의 로컬 저장소에 범주 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="95982-153">다음에는 범주 알림을 이 앱에 보낼 수 있는 백 엔드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="95982-154">태그가 지정된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="95982-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="95982-155">앱 실행 및 알림 생성</span><span class="sxs-lookup"><span data-stu-id="95982-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="95982-156">Visual Studio에서 F5 키를 눌러 앱을 컴파일 및 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="95982-157">앱 UI는 구독할 범주를 선택하도록 하는 토글 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="95982-158">하나 이상의 범주 토글을 사용하도록 설정한 후 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="95982-159">앱은 선택한 범주를 태그로 변환하고 알림 허브에서 선택한 태그에 대한 새로운 장치 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="95982-160">등록된 범주가 반환되어 대화 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="95982-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="95982-161">다음 방법 중 하나로 백 엔드에서 새 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="95982-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="95982-162">**콘솔 앱:** 콘솔 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="95982-163">**Java/PHP:** 앱/스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="95982-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="95982-164">선택한 범주에 대한 알림이 알림 메시지로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="95982-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="95982-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95982-165">Next steps</span></span>
<span data-ttu-id="95982-166">이 자습서에서는 범주별로 속보를 브로드캐스트하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="95982-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="95982-167">이제 기타 고급 알림 허브 시나리오를 다루는 다음 자습서 중 하나를 완료해 보세요.</span><span class="sxs-lookup"><span data-stu-id="95982-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="95982-168">[알림 허브를 사용하여 지역화된 속보 브로드캐스트]</span><span class="sxs-lookup"><span data-stu-id="95982-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="95982-169">지역화된 알림을 보낼 수 있도록 속보 앱을 확장하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="95982-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
<span data-ttu-id="95982-170">[알림 허브를 사용하여 지역화된 속보 브로드캐스트]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="95982-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
