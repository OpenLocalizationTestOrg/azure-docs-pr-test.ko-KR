---
title: "aaaNotification 허브 지역화 주요 속보 자습서"
description: "Azure 알림 허브 toosend toouse 최신 알림을 지역화 하는 방법에 대해 알아봅니다."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>알림 허브 지역화 toosend 주요 뉴스를 사용 하 여
> [!div class="op_single_selector"]
> * [Windows 스토어 C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>개요
이 항목에서는 toouse hello **템플릿** 언어 및 장치에서 지역화 된 알림을 주요 Azure 알림 허브 toobroadcast의 기능입니다. 이 자습서에서 만든 hello Windows 스토어 앱 시작 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다. 완료 되 면에 관심이 있는 범주에 대 한 수 tooregister 됩니다, 한 tooreceive hello 알림이에서 언어를 지정 하 고 해당 언어로 hello 선택한 범주에 대 한 푸시 알림을 수신 합니다.

두 개의 부분 toothis 시나리오는 있습니다.

* 장치 toospecify는 언어 및 뉴스 범주; 주요 toosubscribe toodifferent hello Windows 스토어 앱 클라이언트를 허용
* hello 백 엔드를 브로드캐스팅합니다. hello를 사용 하 여 hello 알림을, **태그** 및 **템플릿** Azure 알림 허브의 기능입니다.

## <a name="prerequisites"></a>필수 조건
이미 완료 한 상태 여야 hello [최신 뉴스 사용 하 여 알림 허브 toosend] 자습서와이 자습서에서는 해당 코드에 직접 작성 때문 hello 코드를 사용할 수 있어야 합니다.

Visual Studio 2012 이상도 필요합니다.

## <a name="template-concepts"></a>템플릿 개념
[최신 뉴스 사용 하 여 알림 허브 toosend] 사용 하는 응용 프로그램을 빌드한 **태그** toosubscribe toonotifications 다른 뉴스 범주에 대 한 합니다.
하지만 대부분의 앱은 여러 시장을 대상으로 하므로 지역화해야 합니다. 이 hello 알림 자체의 hello 콘텐츠 지역화 toobe 있고 의미 배달된 toohello 장치 집합을 수정 합니다.
이 항목에서는 보여줍니다 어떻게 toouse hello **템플릿** tooeasily 배달 알림 허브의 기능에는 최신 알림을 지역화 합니다.

참고:는 한 가지 방법은 toosend 지역화 된 알림 toocreate 각 태그의 여러 버전을 됩니다. 예를 들어, toosupport 영어, 프랑스어, 및 북경어, 세계 뉴스에 대 한 세 개의 서로 다른 태그가 필요 합니다: "world_en", "world_fr" 및 "world_ch"입니다. 에서는 다음 것이 toosend 이러한 태그의 hello world 뉴스 tooeach의 지역화 된 버전입니다. 이 항목에 태그의 템플릿 tooavoid hello 급증 및 여러 메시지를 보내는의 hello 요구 사항을 사용 합니다.

상위 수준 템플릿은 방식으로 toospecify 어떻게 특정 장치에 알림을 받아야 합니다. hello 템플릿은 앱 백 엔드에서 보낸 hello 메시지의 일부인 tooproperties 참조 하 여 hello 정확한 페이로드 형식을 지정 합니다. 여기서는 모든 지원되는 언어를 포함하는 로캘을 알 수 없는 메시지를 보냅니다.

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

다음에서는 사용 하면 장치 등록 toohello 올바른 속성을 참조 하는 템플릿을 사용 하 여 합니다. 예를 들어, tooreceive를가 하는 Windows 스토어 앱의 간단한 알림 메시지를 등록 합니다 해당 태그가 있는 서식 파일을 다음 hello:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



템플릿은 매우 강력한 기능입니다. 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md) 문서를 참조하세요. 

## <a name="hello-app-user-interface"></a>hello 응용 프로그램 사용자 인터페이스
에서는 이제 hello 항목에서 만든 hello 최신 뉴스 앱을 수정 합니다 [최신 뉴스 사용 하 여 알림 허브 toosend] toosend 템플릿을 사용 하 여 최신 뉴스를 지역화 합니다.

Windows 스토어 앱에서

프로그램 MainPage.xaml tooinclude 로캘 combobox를 변경 합니다.

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a>Hello Windows 스토어 클라이언트 응용 프로그램 빌드
1. 알림 클래스에 추가 로캘 매개 변수 tooyour *StoreCategoriesAndSubscribe* 및 *SubscribeToCateories* 메서드.
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    호출 hello 대신 *RegisterNativeAsync* 이라고 하는 메서드 *RegisterTemplateAsync*:는 hello 서식 파일에 따라 달라 지 hello 로캘 특정 알림 형식을 등록 하는 것입니다. 주문 toobe 수 tooupdate tooregister (예를 들어 알림 메시지 하나) 및 타일에 대 한 템플릿을 여러 개 좋습니다 tooname 필요 하기 때문에도 hello 템플릿 ("localizedWNSTemplateExample")에 대 한 이름을 제공 하거나 삭제 합니다.
   
    Note 장치 hello 같은 태그, 태그 발생 않을 것임을 대상으로 하는 들어오는 메시지를 여러 서식 파일을 등록 하는 경우 여러 알림을 배달 toohello 장치 (각 템플릿에 대해 하나). 이 동작은 hello 동일한 논리 메시지에 tooresult 예를 들어 Windows 스토어 응용 프로그램에서 배지와 알림 메시지를 표시 하는 여러 시각적 알림 때 유용 합니다.
2. 다음 메서드 tooretrieve hello 저장 된 로캘 hello를 추가 합니다.
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. MainPage.xaml.cs에에서 업데이트 단추 hello hello 로캘 콤보 상자의 현재 값을 검색 하 고 표시 된 것 처럼 toohello 호출 toohello 알림을 클래스를 제공 하 여 처리기를 클릭 합니다.
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. 마지막으로, App.xaml.cs 파일에 있는지 tooupdate 확인 프로그램 `InitNotificationsAsync` 메서드 tooretrieve 로캘 hello 및 구독할 때 사용할:
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a>백 엔드에서 지역화된 알림 보내기
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[최신 뉴스 사용 하 여 알림 허브 toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
