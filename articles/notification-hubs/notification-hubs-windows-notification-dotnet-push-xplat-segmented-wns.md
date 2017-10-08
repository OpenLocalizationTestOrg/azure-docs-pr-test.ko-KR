---
title: "aaaUse 알림 허브 toosend 최신 뉴스 (Windows 유니버설)"
description: "Azure 알림 허브를 사용 하 여 hello 등록 toosend 뉴스 tooa 유니버설 Windows 앱 수준에서 태그를 사용 합니다."
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
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>알림 허브 toosend 최신 뉴스를 사용 하 여
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>개요
이 항목에서는 toouse Azure 알림 허브 toobroadcast 뉴스 알림 tooa Windows 스토어 또는 Windows Phone 8.1 (Silverlight가 아닌) 앱을 분리 합니다. Windows Phone 8.1 Silverlight 대상으로 하는 경우 toohello 참조 [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) 버전입니다. 완료 되 면에 관심이 있는 뉴스 범주 파괴 수 tooregister 수 및 해당 범주에 대 한 푸시 알림을 수신 합니다. 이 시나리오는 알림을 그 예: RSS 수집기 음악 팬 속도 대 한 응용 프로그램에서 관심 있는 선언한 이전에 사용자의 전송 toobe toogroups 있는 많은 응용 프로그램에 대 한 일반적인 패턴입니다. 

브로드캐스트 시나리오 하나 이상 포함 하 여 설정 된 *태그* hello 알림 허브의 등록을 만들 때. 알림을 tooa 태그를 보내면 hello 태그에 대 한 모든 장치를 등록 한 hello 알림을 받게 됩니다. 태그는 단순히 문자열을 하기 때문에 미리 프로 비전 toobe를 갖지 않습니다. 태그에 대 한 자세한 내용은 참조 너무[알림 허브 라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)합니다.

> [!NOTE]
> Windows 스토어 및 Windows Phone 프로젝트 버전 8.1 및 이전 버전은 Visual Studio 2017에서 지원되지 않습니다.  자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요. 

## <a name="prerequisites"></a>필수 조건
이 항목에서는에서 만든 hello 앱 [알림 허브 시작][get-started]합니다. 이 자습서를 시작하기 전에 먼저 [Notification Hubs 시작][get-started]을 완료해야 합니다.

## <a name="add-category-selection-toohello-app"></a>범주 선택 toohello 앱 추가
hello 첫 번째 단계는 tooadd hello UI 요소 tooyour 기존 기본 페이지 hello 사용자 tooselect 범주 tooregister 수 있도록 하는 것입니다. 사용자가 선택한 hello 범주 hello 장치에 저장 됩니다. Hello 앱이 시작 되 면 태그로 hello 선택한 범주와 알림 허브에 장치 등록이 만들어집니다.

1. Hello에 대 한 코드 다음 복사 hello hello MainPage.xaml 프로젝트 파일을 엽니다 **그리드** 요소:
   
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
2. Hello를 마우스 오른쪽 단추로 클릭 **Shared** 라는 새 클래스를 추가 하 고 프로젝트 **알림**, hello 추가 **공용** 한정자 toohello 클래스 정의 다음 hello 다음 를추가합니다.**를 사용 하 여** 문 toohello 새 코드 파일:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. 복사 hello 다음 새 hello에 코드 **알림** 클래스:
   
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
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    이 클래스는이 장치에는 tooreceive 뉴스의 hello toostore hello 범주를 로컬 저장소를 사용 합니다. 호출 hello 대신 *RegisterNativeAsync* 이라고 메서드 *RegisterTemplateAsync* tooregister 템플릿 등록을 사용 하 여 hello 범주에 대 한 합니다. 
   
    주문 toobe 수 tooupdate tooregister (예를 들어 알림 메시지 하나) 및 타일에 대 한 템플릿을 여러 개 좋습니다 tooname 필요 하기 때문에도 hello 템플릿 ("simpleWNSTemplateExample")에 대 한 이름을 제공 하거나 삭제 합니다.
   
    Note 장치 hello 같은 태그, 태그 발생 않을 것임을 대상으로 하는 들어오는 메시지를 여러 서식 파일을 등록 하는 경우 여러 알림을 배달 toohello 장치 (각 템플릿에 대해 하나). 이 동작은 hello 동일한 논리 메시지에 tooresult 예를 들어 Windows 스토어 응용 프로그램에서 배지와 알림 메시지를 표시 하는 여러 시각적 알림 때 유용 합니다.
   
    템플릿 사용에 대한 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.
4. Hello App.xaml.cs 프로젝트 파일에서 추가 속성 toohello 다음 hello **앱** 클래스:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    이 속성은 사용 되는 toocreate 및 액세스는 **알림** 인스턴스.
   
    코드 위의 hello, 바꿉니다 hello `<hub name>` 및 `<connection string with listen access>` 와 알림 허브 이름 및 hello 연결 문자열에 대 한 자리 표시자 *DefaultListenSharedAccessSignature* 이전에 얻은입니다.
   
   > [!NOTE]
   > 클라이언트 응용 프로그램과 함께 배포 되는 자격 증명에 일반적으로 안전 하지 않으므로 클라이언트 응용 프로그램과 함께 수신 액세스에 대 한 hello 키만 배포 해야 합니다. 알림, 하지만 기존 등록에 대 한 응용 프로그램 tooregister 프로그램을 수정할 수 없는 액세스 활성화를 수신 하 고 알림을 보낼 수 없습니다. hello 전체 액세스 키를 사용 하 여 보안 된 백 엔드 서비스 알림을 전송 하 고 기존 등록을 변경 합니다.
   > 
   > 
5. MainPage.xaml.cs에 hello 다음 줄을 추가 합니다.
   
        using Windows.UI.Popups;
6. Hello MainPage.xaml.cs 프로젝트 파일에서 메서드를 다음 hello를 추가 합니다.
   
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
   
    이 메서드가 만드는 범주 및 사용 하 여 hello 목록이 **알림** toostore hello 목록 hello 로컬 저장소에 클래스 및 해당 태그 hello 알림 허브에 등록 합니다. 범주 변경 되 면 hello 등록 hello 새 범주와 다시 만들어집니다.

앱은 hello 장치의 로컬 저장소에 수 toostore 범주 집합에 포함 되었습니다 및 hello 사용자 변경 내용을 hello 범주의 선택 될 때마다 hello 알림 허브에 등록 합니다.

## <a name="register-for-notifications"></a>알림 등록
이러한 단계는 시작할 때 로컬 저장소에 저장 된 hello 범주를 사용 하 여 hello 알림 허브를 등록 합니다.

> [!NOTE]
> Hello 채널 hello 알림 WNS (Windows 서비스)에서 할당 하는 URI를 언제 든 지 변경할 수 있으므로 등록 알림에 대 한 자주 tooavoid 알림 오류가 발생 했습니다. 이 예제에서는 hello 이러한 앱이 시작 될 때마다 알림을 등록 합니다. 자주 실행 되는 응용 프로그램의 경우 하루에 한 번 이상 건너뛸 수 있습니다 아마도 등록 toopreserve 대역폭 hello 이전 등록 이후 1 일 미만 경과한 경우.
> 
> 

1. 열기 hello App.xaml.cs 파일과 업데이트 hello **InitNotificationsAsync** 메서드 toouse hello `notifications` 클래스 toosubscribe 범주를 기반 합니다.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    이렇게 하면 hello 앱 시작 될 때마다 로컬 저장소에서 검색 하는 hello 범주를 이러한 범주에 대 한 등록을 요청 합니다. hello **InitNotificationsAsync** hello의 일부로 메서드를 만들 [알림 허브 시작] [ get-started] 자습서입니다.
2. Hello MainPage.xaml.cs 프로젝트 파일에 다음 코드 toohello hello 추가 *OnNavigatedTo* 메서드:
   
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
   
    ![][19]
3. Hello 같은 방법으로 다음 중 하나에 hello 백 엔드에서 새 알림 보내기:
   
   * **콘솔 응용 프로그램:** hello 콘솔 응용 프로그램을 시작 합니다.
   * **Java/PHP:** 앱/스크립트를 실행합니다.
     
     알림 메시지 hello 선택한 범주에 대 한 알림이 표시 됩니다.
     
     ![][14]

## <a name="next-steps"></a>다음 단계
이 자습서에서는 이전에 배운 것 어떻게 toobroadcast 최신 뉴스 범주별으로 보여 줍니다. 기타 고급 알림 허브 시나리오를 강조 표시 하는 자습서를 따라 hello 중 하나를 완료 하는 것이 좋습니다.

* [알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]
  
    뉴스 앱 tooenable 보내는 주요 tooexpand hello 알림을 지역화 하는 방법에 대해 알아봅니다.

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[알림 허브 지역화 toobroadcast 주요 뉴스를 사용 하 여]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
