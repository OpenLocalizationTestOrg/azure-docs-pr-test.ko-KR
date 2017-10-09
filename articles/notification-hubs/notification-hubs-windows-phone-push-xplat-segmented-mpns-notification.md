---
title: "aaaUse 알림 허브 toosend 최신 뉴스 (Windows Phone)"
description: "Azure 알림 허브 toouse 태그를 사용 하 여 등록 toosend 뉴스 tooa Windows Phone 응용 프로그램 수준에서."
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
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>알림 허브 toosend 최신 뉴스를 사용 하 여
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>개요
이 항목에서는 toouse Azure 알림 허브 toobroadcast 주요 뉴스 알림 tooa Windows Phone 8.0/8.1 Silverlight 앱입니다. Windows 스토어 또는 Windows Phone 8.1 앱을 대상으로 경우 tootoohello를 참조 하십시오 [Windows 유니버설](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) 버전입니다. 완료 되 면에 관심이 있는 뉴스 범주 파괴 수 tooregister 수 및 해당 범주에 대 한 푸시 알림을 수신 합니다. 이 시나리오는 알림을 그 예: RSS 수집기, 음악 팬 속도 등에 대 한 앱에 대 한 관심 선언 이전에 사용자의 전송 toobe toogroups 있는 많은 응용 프로그램에 대 한 일반적인 패턴입니다.

브로드캐스트 시나리오 하나 이상 포함 하 여 설정 된 *태그* hello 알림 허브의 등록을 만들 때. 알림을 tooa 태그를 보내면 hello 태그에 대 한 모든 장치를 등록 한 hello 알림을 받게 됩니다. 태그는 단순히 문자열을 하기 때문에 미리 프로 비전 toobe를 갖지 않습니다. 태그에 대 한 자세한 내용은 참조 너무[알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)합니다.

## <a name="prerequisites"></a>필수 조건
이 항목에서는에서 만든 hello 앱 [시작 알림 허브]합니다. 이 자습서를 시작하기 전에 먼저 [시작 알림 허브]을 완료해야 합니다.

## <a name="add-category-selection-toohello-app"></a>범주 선택 toohello 앱 추가
hello 첫 번째 단계는 tooadd hello UI 요소 tooyour 기존 기본 페이지 hello 사용자 tooselect 범주 tooregister 수 있도록 하는 것입니다. 사용자가 선택한 hello 범주 hello 장치에 저장 됩니다. Hello 앱이 시작 되 면 태그로 hello 선택한 범주와 알림 허브에 장치 등록이 만들어집니다.

1. Hello MainPage.xaml 프로젝트 파일을 연 다음 hello 대체 **그리드** 이라는 요소 `TitlePanel` 및 `ContentPanel` 코드 다음 hello로:
   
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
2. Hello 프로젝트에서 이라는 새 클래스를 만들어 **알림**, hello 추가 **공용** 한정자 toohello 클래스 정의 다음 hello 다음 추가 **를 사용 하 여** 문 toohello 새 코드 파일:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. 복사 hello 다음 새 hello에 코드 **알림** 클래스:
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
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
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
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
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
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
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    이 클래스는이 장치가 tooreceive 인지 뉴스의 hello 격리 된 저장소 toostore hello 범주를 사용 합니다. 사용 하 여 이러한 범주에 대 한 메서드 tooregister도 포함 되어는 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 알림 등록 합니다.


1. Hello App.xaml.cs 프로젝트 파일에서 추가 속성 toohello 다음 hello **앱** 클래스입니다. Hello 대체 `<hub name>` 및 `<connection string with listen access>` 와 알림 허브 이름 및 hello 연결 문자열에 대 한 자리 표시자 *DefaultListenSharedAccessSignature* 이전에 얻은입니다.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > 클라이언트 응용 프로그램과 함께 배포 되는 자격 증명에 일반적으로 안전 하지 않으므로 클라이언트 응용 프로그램과 함께 수신 액세스에 대 한 hello 키만 배포 해야 합니다. 알림, 하지만 기존 등록에 대 한 응용 프로그램 tooregister 프로그램을 수정할 수 없는 액세스 활성화를 수신 하 고 알림을 보낼 수 없습니다. hello 전체 액세스 키를 사용 하 여 보안 된 백 엔드 서비스 알림을 전송 하 고 기존 등록을 변경 합니다.
   > 
   > 
2. MainPage.xaml.cs에 hello 다음 줄을 추가 합니다.
   
        using Windows.UI.Popups;
3. Hello MainPage.xaml.cs 프로젝트 파일에서 메서드를 다음 hello를 추가 합니다.
   
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
   
    이 메서드가 만드는 범주 및 사용 하 여 hello 목록이 **알림** toostore hello 목록 hello 로컬 저장소에 클래스 및 해당 태그 hello 알림 허브에 등록 합니다. 범주 변경 되 면 hello 등록 hello 새 범주와 다시 만들어집니다.

앱은 hello 장치의 로컬 저장소에 수 toostore 범주 집합에 포함 되었습니다 및 hello 사용자 변경 내용을 hello 범주의 선택 될 때마다 hello 알림 허브에 등록 합니다.

## <a name="register-for-notifications"></a>알림 등록
이러한 단계는 시작할 때 로컬 저장소에 저장 된 hello 범주를 사용 하 여 hello 알림 허브를 등록 합니다.

> [!NOTE]
> Hello 채널 hello Microsoft 푸시 알림 서비스 (MPNS)에 의해 할당 되는 URI를 언제 든 지 변경할 수 있으므로 등록 알림에 대 한 자주 tooavoid 알림 오류가 발생 했습니다. 이 예에서는 hello 이러한 앱이 시작 될 때마다 알림을 등록 합니다. 자주 실행 되는 응용 프로그램의 경우 하루에 한 번 이상 건너뛸 수 있습니다 아마도 등록 toopreserve 대역폭 hello 이전 등록 이후 1 일 미만 경과한 경우.
> 
> 

1. Hello App.xaml.cs 파일을 열고 hello 추가 **비동기** 한정자 너무**Application_Launching** 메서드 및 바꾸기 hello 알림 허브 등록의 코드에서 추가한 [시작 알림 허브] 코드 다음 hello로:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    이렇게 하면 hello 앱 시작 될 때마다 로컬 저장소에서 검색 하는 hello 범주를 이러한 범주에 대 한 등록을 요청 합니다.
2. Hello MainPage.xaml.cs 프로젝트 파일에서 추가 hello를 구현 하는 코드를 다음 hello **OnNavigatedTo** 메서드:
   
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
   
    이전에의 hello 상태에 따라이 업데이트 hello 주 페이지 범주를 저장 합니다.

hello 앱 완료 되며 hello 사용자 변경 내용을 hello 범주의 선택 될 때마다 hello 알림 허브와 장치 사용 되는 로컬 저장소 tooregister hello 범주 집합을 저장할 수 있습니다. 다음으로, 알림 toothis 앱 범주를 보낼 수 있는 백 엔드를 정의 하겠습니다.

## <a name="sending-tagged-notifications"></a>태그가 지정된 알림 보내기
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Hello 앱을 실행 하 고 알림 생성
1. Visual Studio에서 F5 toocompile 누르고 hello 응용 프로그램을 시작 합니다.
   
    ![][1]
   
    참고 hello 앱 UI의 집합을 제공 하는 설정/해제를 hello 범주 toosubscribe를 선택할 수 있습니다.
2. 하나 이상의 범주 토글을 사용하도록 설정한 후 **구독**을 클릭합니다.
   
    hello 앱 태그에 hello 선택한 범주를 변환 하 고 hello 알림 허브에서 선택 하는 hello 태그에 대 한 새 장치 등록을 요청 합니다. hello 등록 된 범주는 반환 된 없으며는 대화 상자에 표시 합니다.
   
    ![][2]
3. 사용자 범주 구독을 완료 했는지 확인 메시지를 받은 후 각 범주에 대 한 hello 콘솔 앱 toosend 알림을 실행 합니다. 받기만 hello 범주를 구독에 대 한 알림을 확인 합니다.
   
    ![][3]

이 항목을 완료했습니다.

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[시작 알림 허브]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

