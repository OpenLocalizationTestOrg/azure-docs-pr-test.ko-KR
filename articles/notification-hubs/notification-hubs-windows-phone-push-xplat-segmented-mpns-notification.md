---
title: "알림 허브를 사용하여 속보 보내기(Windows Phone)"
description: "등록된 태그와 함께 Azure Notification Hubs를 사용하여 Windows Phone 앱에 최신 뉴스를 보낼 수 있습니다."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="2e580-103">알림 허브를 사용하여 속보 보내기</span><span class="sxs-lookup"><span data-stu-id="2e580-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="2e580-104">개요</span><span class="sxs-lookup"><span data-stu-id="2e580-104">Overview</span></span>
<span data-ttu-id="2e580-105">이 항목에서는 Azure 알림 허브를 사용하여 Windows Phone 8.0/8.1 Silverlight 앱에 속보 알림을 브로드캐스트하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="2e580-106">Windows 스토어 또는 Windows Phone 8.1 앱을 대상으로 하는 경우 [Windows 범용](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e580-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="2e580-107">완료하면, 관심이 있는 속보 범주를 등록하고 해당 범주의 푸시 알림만 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="2e580-108">이 시나리오는 RSS 수집기, 음악 애호가를 위한 앱 등 이전에 관심을 보인 사용자 그룹에 알림을 보내야 하는 많은 앱에 공통된 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="2e580-109">브로드캐스트 시나리오를 사용하려면 알림 허브에서 등록을 만들 때 하나 이상의 *태그*를 포함하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="2e580-110">태그에 알림이 전송되면 태그에 대해 등록된 모든 장치에서 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="2e580-111">태그는 단순히 문자열이므로 사전에 프로비전해야 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="2e580-112">태그에 대한 자세한 내용은 [알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2e580-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e580-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="2e580-113">Prerequisites</span></span>
<span data-ttu-id="2e580-114">이 항목은 [Notification Hubs 시작]에서 만든 앱을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="2e580-115">이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작]을 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="2e580-116">앱에 범주 선택 추가</span><span class="sxs-lookup"><span data-stu-id="2e580-116">Add category selection to the app</span></span>
<span data-ttu-id="2e580-117">첫 번째 단계는 기존의 기본 페이지에 사용자가 등록할 범주를 선택할 수 있도록 하는 UI 요소를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="2e580-118">사용자가 선택한 범주는 장치에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="2e580-119">앱을 시작하면 장치 등록이 선택한 범주와 함께 태그로서 알림 허브에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="2e580-120">MainPage.xaml 프로젝트 파일을 열고 `TitlePanel` 및 `ContentPanel`이라는 **Grid** 요소를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="2e580-121">프로젝트에서 **Notifications**라는 이름의 새 클래스를 만들고, 클래스 정의에 **public** 한정자를 추가하고, 다음 **using** 문을 새 코드 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="2e580-122">다음 코드를 새 **Notifications** 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="2e580-123">이 클래스는 격리된 저장소를 사용하여, 이 장치에서 받아야 할 뉴스의 범주를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="2e580-124">또한 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 알림 등록을 사용하여 이러한 범주에 등록하는 메서드가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="2e580-125">App.xaml.cs 프로젝트 파일에서 **App** 클래스에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="2e580-126">`<hub name>`과 `<connection string with listen access>` 자리 표시자를 알림 허브 이름과 앞서 얻었던 *DefaultListenSharedAccessSignature*의 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="2e580-127">클라이언트 앱과 함께 배포되는 자격 증명은 일반적으로 안전하지 않기 때문에 클라이언트 앱과 함께 listen access용 키만 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="2e580-128">Listen access를 통해 앱에서 알림을 등록할 수 있지만, 기존 등록을 수정할 수 없으며 알림을 전송할 수도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="2e580-129">안전한 백 엔드 서비스에서 알림을 보내고 기존 등록을 변경하는 데에는 모든 액세스 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="2e580-130">MainPage.xaml.cs에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="2e580-131">MainPage.xaml.cs 프로젝트 파일에 다음 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="2e580-132">이 메서드는 범주 목록을 만들고 **Notifications** 클래스를 사용하여, 로컬 저장소에 목록을 저장하고 알림 허브에 해당 태그를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="2e580-133">범주가 변경되면 새 범주로 등록이 다시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="2e580-134">이제 사용자가 범주 선택을 변경할 때마다 앱은 범주 집합을 장치의 로컬 저장소에 저장하고 알림 허브에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="2e580-135">알림 등록</span><span class="sxs-lookup"><span data-stu-id="2e580-135">Register for notifications</span></span>
<span data-ttu-id="2e580-136">다음 단계에서는 로컬 저장소에 저장된 범주를 사용하여 시작 시 알림 허브에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="2e580-137">MPNS(Microsoft 푸시 알림 서비스)에서 할당하는 채널 URI는 언제든지 변경될 수 있으므로 알림 실패를 피하려면 알림을 자주 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="2e580-138">이 예제에서는 앱이 시작될 때마다 알림을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="2e580-139">자주(하루 두 번 이상) 실행되는 앱에서는 이전 등록 이후 만 하루가 지나지 않은 경우 대역폭 유지를 위한 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="2e580-140">App.xaml.cs 파일을 열고 **async** 한정자를 **Application_Launching** 메서드에 추가하고 [Notification Hubs 시작]에서 추가한 Notification Hubs 등록 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="2e580-141">이제 앱이 시작될 때마다 로컬 저장소에서 범주를 검색하고, 이러한 범주에 대한 등록을 요청하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="2e580-142">MainPage.xaml.cs 프로젝트 파일에서 **OnNavigatedTo** 메서드를 구현하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="2e580-143">전에 저장한 범주의 상태를 기반으로 기본 페이지가 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="2e580-144">이제 앱이 완료되며, 사용자가 범주 선택을 변경할 때마다 알림 허브 등록에 사용된 장치의 로컬 저장소에 범주 집합을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="2e580-145">다음에는 범주 알림을 이 앱에 보낼 수 있는 백 엔드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="2e580-146">태그가 지정된 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="2e580-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="2e580-147">앱 실행 및 알림 생성</span><span class="sxs-lookup"><span data-stu-id="2e580-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="2e580-148">Visual Studio에서 F5 키를 눌러 앱을 컴파일 및 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="2e580-149">앱 UI는 구독할 범주를 선택하도록 하는 토글 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="2e580-150">하나 이상의 범주 토글을 사용하도록 설정한 후 **구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="2e580-151">앱은 선택한 범주를 태그로 변환하고 알림 허브에서 선택한 태그에 대한 새로운 장치 등록을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="2e580-152">등록된 범주가 반환되어 대화 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="2e580-153">범주가 구독 완료되었다는 확인을 받은 후 각 범주에 대한 알림을 보내는 콘솔 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="2e580-154">구독한 범주에 대한 알림만 받는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="2e580-155">이 항목을 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e580-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="2e580-156">[Notification Hubs 시작]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="2e580-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

