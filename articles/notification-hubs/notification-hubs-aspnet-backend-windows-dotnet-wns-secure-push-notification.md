---
title: "알림 허브 푸시 Secure aaaAzure"
description: "어떻게 toosend 보안의 푸시 알림 Azure에 알아봅니다. Hello.NET API를 사용 하 여 C#으로 작성 된 코드 샘플입니다."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure 알림 허브 보안 푸시
> [!div class="op_single_selector"]
> * [Windows 범용](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>개요
Microsoft Azure에서 푸시 알림 지원을 사용 하면 tooaccess 크게 간소화 됩니다. 모바일 앱을 위해 소비자 및 엔터프라이즈 응용 프로그램에서 푸시 알림의 hello 구현 하는 사용 하기 쉬운, 다중 플랫폼, 수평 확장 된 푸시 인프라 플랫폼입니다.

때로는 tooregulatory 또는 보안 제약 조건 때문 응용 프로그램에서 hello 표준 푸시 알림 인프라를 통해 전송 될 수 없는 hello 알림 tooinclude를 할 수도 있습니다. 이 자습서에서는 tooachieve hello 클라이언트 장치 및 앱 백 엔드에서 hello 간에 안전 하 고 인증 된 연결을 통해 중요 한 정보를 전송 하 여 동일한 환경을 hello 하는 방법을 설명 합니다.

상위 수준 hello 흐름은 다음과 같습니다.

1. hello 앱 백 엔드에서:
   * 백 엔드 데이터베이스에 보안 페이로드를 저장합니다.
   * 이 알림 toohello 장치 (보안 정보 없음 전송 됨)의 hello ID를 전송 합니다.
2. 응용 프로그램에 액세스 hello 알림을 받은 경우 hello 장치 hello:
   * hello 장치가 hello 백 엔드에서 요청 hello 보안 페이로드를 연결합니다.
   * hello 앱 hello 장치에 대 한 알림으로 hello 페이로드를 표시할 수 있습니다.

hello 사용자가 로그인 한 후 toonote 하의 hello 흐름 이전 (및이 자습서에서는) 가정 hello 장치 로컬 저장소에 인증 토큰을 저장 합니다. 이 hello 장치는이 토큰을 사용 하 여 hello 알림 보안 페이로드를 검색할 수 있는 완전히 원활한 환경을 보장 합니다. 응용 프로그램에서 hello 장치에서 인증 토큰을 저장 하지 않으면 이러한 토큰을 만료 될 수 있습니다를 hello hello 알림을 받으면 장치 응용 프로그램 해야 표시 제네릭 알림을 hello 사용자 toolaunch hello 앱 메시지를 표시 합니다. 그런 다음 hello 앱 hello 사용자를 인증 하 고 hello 알림 페이로드를 보여 줍니다.

이 보안 밀어넣기 자습서에서는 어떻게 toosend 푸시 알림 안전 하 게 합니다. hello을 기반으로 하는 hello 자습서 [사용자에 게 알림](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) 자습서에서는 하므로 먼저 해당 자습서의 hello 단계를 완료 해야 합니다.

> [!NOTE]
> 이 자습서에서는 [알림 허브 시작(Windows 스토어)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다.
> 또한 Windows Phone 8.1에 Windows(Windows Phone이 아님) 자격 증명이 필요하며, 백그라운드 작업은 Windows Phone 8.0 또는 Silverlight 8.1에서 작동하지 않습니다. Windows 스토어 응용 프로그램에 대 한 알림을 받을 수 있습니다는 백그라운드 작업을 통해 hello 앱은 잠금 화면을 사용 하는 경우에 (hello Appmanifest hello 확인란 클릭).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Hello Windows Phone 프로젝트를 수정 합니다.
1. Hello에 **NotifyUserWindowsPhone** 프로젝트에서 코드 tooApp.xaml.cs tooregister hello 푸시 백그라운드 작업을 수행 하는 hello를 추가 합니다. 다음 코드의 hello hello 끝에 줄을 hello 추가 `OnLaunched()` 메서드:
   
        RegisterBackgroundTask();
2. App.xaml.cs에서 hello hello 직후 코드를 다음 추가 `OnLaunched()` 메서드:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Hello 다음 추가 `using` hello App.xaml.cs 파일의 맨 위에 hello에 문을:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Hello에서 **파일** Visual Studio에서 메뉴를 클릭 **모두 저장**합니다.

## <a name="create-hello-push-background-component"></a>Hello 푸시 배경 구성 요소 만들기
hello 다음 단계 toocreate hello 푸시 배경 구성 요소입니다.

1. 솔루션 탐색기에서 hello hello 솔루션의 최상위 노드를 마우스 오른쪽 단추로 (**솔루션 SecurePush** 이 경우)를 클릭 한 다음 **추가**, 클릭 **새 프로젝트**합니다.
2. **스토어 앱**을 확장하고 **Windows Phone 앱**, **Windows 런타임 구성 요소(Windows Phone)**를 차례로 클릭합니다. 이름 hello 프로젝트 **PushBackgroundComponent**, 클릭 하 고 **확인** toocreate hello 프로젝트.
   
    ![][12]
3. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **PushBackgroundComponent (Windows Phone 8.1)** 프로젝트를 선택한 다음 클릭 **추가**, 클릭 **클래스**합니다. Hello 새 클래스 이름을 **PushBackgroundTask.cs**합니다. 클릭 **추가** toogenerate hello 클래스입니다.
4. Hello의 전체 내용을 hello 대체 **PushBackgroundComponent** 코드 다음, hello 자리 표시자를 대체 하는 hello로 네임 스페이스 정의 `{back-end endpoint}` 배포 하는 동안 가져온 hello 백 엔드 끝점을 사용 하면 백 엔드:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. 솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 hello **PushBackgroundComponent (Windows Phone 8.1)** 프로젝트를 마우스 클릭 **NuGet 패키지 관리**합니다.
6. Hello 왼쪽에 클릭 **온라인**합니다.
7. Hello에 **검색** 상자에서 입력 **Http 클라이언트**합니다.
8. Hello 결과 목록에서 클릭 **Microsoft HTTP 클라이언트 라이브러리**, 클릭 하 고 **설치**합니다. Hello 설치를 완료 합니다.
9. NuGet hello에 다시 **검색** 상자에서 입력 **Json.net**합니다. Hello 설치 **Json.NET** 패키지를 다음 닫기 hello NuGet 패키지 관리자 창.
10. Hello 다음 추가 `using` hello 위쪽 hello에 문을 **PushBackgroundTask.cs** 파일:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. Hello의 솔루션 탐색기에서 **NotifyUserWindowsPhone (Windows Phone 8.1)** 프로젝트를 마우스 오른쪽 단추로 클릭 **참조**, 클릭 **참조 추가...** . Hello 참조 관리자 대화 상자에서 확인란 hello 다음 너무**PushBackgroundComponent**, 클릭 하 고 **확인**합니다.
12. 솔루션 탐색기에서 두 번 클릭 **Package.appxmanifest** hello에 **NotifyUserWindowsPhone (Windows Phone 8.1)** 프로젝트. 아래 **알림**설정, **알림 가능** 너무**예**합니다.
    
    ![][3]
13. 여전히 **Package.appxmanifest**, hello 클릭 **선언** hello 위쪽 메뉴. Hello에 **사용 가능한 선언** 드롭다운을 클릭 하 여 **백그라운드 작업**, 클릭 하 고 **추가**합니다.
14. **Package.appxmanifest**의 **속성**에서 **푸시 알림**을 선택합니다.
15. **Package.appxmanifest**아래 **앱 설정**, 형식 **PushBackgroundComponent.PushBackgroundTask** hello에 **진입점** 필드입니다.
    
    ![][13]
16. Hello에서 **파일** 메뉴를 클릭 하 여 **모두 저장**합니다.

## <a name="run-hello-application"></a>Hello 응용 프로그램 실행
toorun hello 응용 프로그램, 다음 hello지 않습니다.

1. Visual Studio에서 실행 hello **AppBackend** Web API 응용 프로그램입니다. ASP.NET 웹 페이지가 표시됩니다.
2. Visual Studio에서 실행 hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone 응용 프로그램입니다. hello Windows Phone 에뮬레이터를 실행 하 고 hello 앱을 자동으로 로드 합니다.
3. Hello에 **NotifyUserWindowsPhone** 앱 UI를 사용자 이름 및 암호를 입력 합니다. 모든 문자열을 지정할 수 있습니다 이러한 있지만 해야만 해당 hello 동일한 값입니다.
4. Hello에 **NotifyUserWindowsPhone** 앱 UI를 클릭 하 여 **에 로그인 하 고 등록**합니다. 그리고 나서 **푸시 보내기**를 클릭합니다.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
