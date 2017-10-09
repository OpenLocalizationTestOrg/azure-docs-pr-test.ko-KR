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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>.NET 백엔드를 통한 Azure 알림 허브의 사용자 알림
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>개요
Azure의 푸시 알림 지원을 사용 하면 tooaccess는 사용 하기 쉬운, 다중 플랫폼, 및 수평 확장형 푸시 인프라를 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에 대 한 푸시 알림 hello 구현이 크게 간소화 플랫폼입니다. 이 자습서에서는 toouse Azure 알림 허브 toosend 특정 장치에서 알림을 tooa 특정 응용 프로그램 사용자를 강제 하는 방법을 보여 줍니다. ASP.NET WebAPI 백엔드 tooauthenticate 사용 되는 클라이언트입니다. Hello를 사용 하 여 클라이언트 사용자를 인증 하 고 hello 백 엔드 toonotification 등록 하 여 태그를 자동으로 추가 됩니다. 이 태그는 특정 사용자에 대 한 hello 백 엔드 toogenerate 알림에 의해 사용 되는 toosend 됩니다. Hello 지침 항목을 참조 하는 앱 백 엔드를 사용 하 여 알림에 등록 하는 방법에 대 한 자세한 내용은 [앱 백 엔드에서 등록](http://msdn.microsoft.com/library/dn743807.aspx)합니다. 이 자습서는 hello 알림 허브와 hello에서 만든 프로젝트에 빌드 [알림 허브 시작] 자습서입니다.

이 자습서는 또한 hello 필수 toohello [푸시 Secure] 자습서입니다. 이 자습서에서는 hello 단계를 완료 한 후 toohello 진행할 수 있습니다 [푸시 Secure] toomodify hello 코드가 방식이 자습서 toosend에 푸시 알림을 안전 하 게 보여 주는 자습서입니다.

## <a name="before-you-begin"></a>시작하기 전에
사용자 의견을 진지하게 고려합니다. 이 항목 또는이 콘텐츠를 개선 하기 위한 권장 사항을 완료 하는 데 문제가 있는 경우 hello hello 페이지 맨 아래에 사용자 의견 보내 주셔서 감사 합니다.

이 자습서를 완료 하는 hello 코드 GitHub에서 확인할 수 있습니다 [여기](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers)합니다. 

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하려면 먼저 다음 모바일 서비스 자습서를 완료해야 합니다.

* [알림 허브 시작]<br/>알림 허브와 만들고 hello 응용 프로그램 이름 예약,이 자습서에서는 tooreceive 알림을 등록 합니다. 이 자습서에서는 다음 단계를 이미 완료했다고 가정합니다. 그렇지 않은 경우의 hello 단계를 수행 하십시오 [(Windows 스토어) 알림 허브 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), 특히 섹션 hello [hello Windows 스토어에 대 한 앱을 등록](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) 및 [구성 알림 허브](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)합니다. 특히 hello를 입력 했는지 확인 **패키지 SID** 및 **클라이언트 암호** hello 포털 hello에 대 한 값 **구성** 알림 허브에 대 한 탭 합니다. 이 구성 절차 hello 섹션에 설명 되어 [알림 허브 구성](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub)합니다. 이 중요 한 단계: hello 포털에서 자격 증명 hello 일치 하지 않으면 지정 된 hello 앱 이름을 선택 하면에 대 한 푸시 알림 hello에 실패 합니다.

> [!NOTE]
> 백 엔드 서비스로 Azure 앱 서비스에서 모바일 앱을 사용 하는 경우 참조 hello [모바일 앱 버전](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) 이 자습서의 합니다.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Hello 클라이언트 프로젝트에 대 한 hello 코드 업데이트
Hello에 대 한 완료 하는 hello 프로젝트에서 hello 코드를 업데이트 하면이 섹션에서는 [알림 허브 시작] 자습서입니다. 이미 hello hello 저장소와 연결 된 고 알림 허브에 대해 구성 해야 합니다. 이 섹션에서는 코드 toocall hello 새 WebAPI 백 엔드를 추가 하 고 등록 하 고 알림을 보낼에 대 한 사용.

1. Visual Studio에서 만든 hello에 대 한 hello hello 솔루션을 엽니다 [알림 허브 시작] 자습서입니다.
2. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **(Windows 8.1)** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
3. Hello 왼쪽에 클릭 **온라인**합니다.
4. Hello에 **검색** 상자에서 입력 **Http 클라이언트**합니다.
5. Hello 결과 목록에서 클릭 **Microsoft HTTP 클라이언트 라이브러리**, 클릭 하 고 **설치**합니다. Hello 설치를 완료 합니다.
6. NuGet hello에 다시 **검색** 상자에서 입력 **Json.net**합니다. Hello 설치 **Json.NET** 패키지 및 종가 hello NuGet 패키지 관리자 창.
7. Hello에 대 한 위의 hello 단계를 반복 **(Windows Phone 8.1)** 프로젝트 tooinstall hello **JSON.NET** hello Windows Phone 프로젝트에 대 한 NuGet 패키지 합니다.
8. Hello의 솔루션 탐색기에서 **(Windows 8.1)** 두 번 클릭 **MainPage.xaml** tooopen hello Visual Studio 편집기에서.
9. Hello에 **MainPage.xaml** XML 코드를 바꾸기 hello `<Grid>` 코드 다음 hello로 섹션. 이 코드를 추가 hello 사용자는 사용자 이름 및 암호 텍스트 상자에 인증 됩니다. 또한 hello 알림 메시지 및 hello 알림을 받아야 하는 hello username 태그에 대 한 입력란을 추가 합니다.
   
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
10. Hello의 솔루션 탐색기에서 **(Windows Phone 8.1)** 프로젝트, 열기 **MainPage.xaml** 및 Windows Phone 8.1 hello 바꾸기 `<Grid>` 위의 같은 코드를 사용 하 여 섹션. hello 인터페이스 아래에 표시 된 유사한 toowhats 찾아야 합니다.
    
    ![][13]
11. 솔루션 탐색기에서 엽니다 hello **MainPage.xaml.cs** hello에 대 한 파일 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트. Hello 다음 추가 `using` hello 위쪽 두 파일의 문:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. **MainPage.xaml.cs** hello에 대 한 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트, 추가 멤버 toohello 다음 hello `MainPage` 클래스입니다. 수 있는지 tooreplace `<Enter Your Backend Endpoint>` hello로 실제 백 엔드 끝점 이전에 얻은 합니다. 예: `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Hello에 toohello MainPage 클래스 아래에 코드 추가 **MainPage.xaml.cs** hello에 대 한 **(Windows 8.1)** 및 **(Windows Phone 8.1)** 프로젝트.
    
    hello `PushClick` 메서드는 hello 클릭 hello에 대 한 처리기 **푸시 보낼** 단추입니다. Hello 백 엔드 tootrigger 알림 tooall hello와 일치 하는 사용자 이름 태그를 사용 하 여 장치 호출 `to_tag` 매개 변수입니다. hello 알림 메시지가 hello 요청 본문의 JSON 내용으로 전달 됩니다.
    
    hello `LoginAndRegisterClick` 메서드는 hello 클릭 hello에 대 한 처리기 **에 로그인 하 고 등록** 단추입니다. Hello basic 저장 로컬 저장소 (이 인증 체계를 사용 하는 모든 토큰 참고)에서 인증 토큰을 사용 하 여 `RegisterClient` tooregister hello 백 엔드를 사용 하 여 알림에 대 한 합니다.

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



1. 솔루션 탐색기에서 hello **Shared** 프로젝트, 열기 hello **App.xaml.cs** 파일입니다. 너무 hello 호출을 찾으려면`InitNotificationsAsync()` hello에 `OnLaunched()` 이벤트 처리기입니다. 주석으로 처리 하거나 너무 hello 호출 삭제`InitNotificationsAsync()`합니다. hello 단추 처리기 위에 추가 알림 등록을 초기화 합니다.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **Shared** 프로젝트를 선택한 다음 클릭 **추가**, 클릭 하 고 **클래스**합니다. Hello 클래스 이름을 **RegisterClient.cs**, 클릭 **확인** toogenerate hello 클래스입니다.
   
   이 클래스에 푸시 알림을 순서 tooregister hello REST 호출 필요한 toocontact hello 앱 백 엔드를, 줄 바꿈됩니다. 또한 로컬로 hello 저장 *registrationIds* 알림 허브에 설명 된 대로 hello에서 만든 [앱 백 엔드에서 등록](http://msdn.microsoft.com/library/dn743807.aspx)합니다. Hello를 클릭할 때 로컬 저장소에 저장 하는 권한 부여 토큰을 사용 하 여 참고 **에 로그인 하 고 등록** 단추입니다.
2. Hello 다음 추가 `using` hello RegisterClient.cs 파일의 맨 위에 hello에 문을:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Hello hello 내부에서 코드를 다음 추가 `RegisterClient` 클래스 정의 합니다.
   
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
4. 변경 내용을 모두 저장합니다.

## <a name="testing-hello-application"></a>Hello 응용 프로그램 테스트
1. Windows 8.1 및 Windows Phone 8.1 모두에 hello 응용 프로그램을 시작 합니다. Windows Phone 8.1에 대 한 hello 인스턴스 hello 에뮬레이터 나 실제 장치에서 실행할 수 있습니다.
2. Hello 앱의 Windows 8.1 hello 인스턴스를 입력 한 **Username** 및 **암호** hello 화면 아래에 표시 된 대로 합니다. Hello 사용자 이름 및 Windows Phone 입력 한 암호가에서 다를 수는 것입니다.
3. **Log in and register(로그인 및 등록)** 를 클릭하고 대화 상자에 로그인되었다고 표시되는지 확인합니다. 이렇게 하면 hello 사용도 **푸시 보낼** 단추입니다.
   
    ![][14]
4. Windows Phone 8.1 hello 인스턴스 두 hello에 사용자 이름 문자열로 입력 **Username** 및 **암호** 필드를 클릭 한 다음 **로그인 및 등록**합니다.
5. Hello 그런 다음 **받는 사용자 이름 태그** 필드에, Windows 8.1 등록 하는 hello 사용자 이름을 입력 합니다. 알림 메시지를 입력하고 **Send Push(푸시 전송)**를 클릭합니다.
   
    ![][16]
6. 일치 하는 사용자 이름 태그 hello 등록 hello 장치만 hello 알림 메시지가 표시 됩니다.
   
    ![][15]

## <a name="next-steps"></a>다음 단계
* Toosegment 관심 그룹으로 사용자, 참조 [최신 뉴스 사용 하 여 알림 허브 toosend]합니다.
* toouse 알림 허브 참조 하는 방법에 대 한 자세한 toolearn [알림 허브 지침]합니다.

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
