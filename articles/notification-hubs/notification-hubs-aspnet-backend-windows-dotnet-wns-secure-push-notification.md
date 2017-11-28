---
title: "Azure 알림 허브 보안 푸시"
description: "Azure에서 보안 푸시 알림을 보내는 방법에 대해 알아봅니다. 코드 샘플은 .NET API를 사용하여 C#으로 작성되었습니다."
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="f8947-104">Azure 알림 허브 보안 푸시</span><span class="sxs-lookup"><span data-stu-id="f8947-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8947-105">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="f8947-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="f8947-106">iOS</span><span class="sxs-lookup"><span data-stu-id="f8947-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="f8947-107">Android</span><span class="sxs-lookup"><span data-stu-id="f8947-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="f8947-108">개요</span><span class="sxs-lookup"><span data-stu-id="f8947-108">Overview</span></span>
<span data-ttu-id="f8947-109">Microsoft Azure의 푸시 알림 지원을 통해 사용하기 쉬운 다중 플랫폼 및 규모 확장 푸시 인프라에 액세스할 수 있어, 모바일 플랫폼용 소비자 응용 프로그램 및 엔터프라이즈 응용 프로그램 모두에 대한 푸시 알림을 매우 간단하게 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="f8947-110">규제나 보안 제약 조건 때문에 응용 프로그램의 알림에 표준 푸시 알림 인프라를 통해 전송할 수 없는 어떤 항목을 포함해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="f8947-111">이 자습서에서는 클라이언트 장치와 앱 백 엔드 간에 인증된 보안 연결을 통해 중요한 정보를 전송하여 동일한 경험을 얻는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="f8947-112">개략적으로 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="f8947-113">앱 백 엔드:</span><span class="sxs-lookup"><span data-stu-id="f8947-113">The app back-end:</span></span>
   * <span data-ttu-id="f8947-114">백 엔드 데이터베이스에 보안 페이로드를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="f8947-115">이 알림의 ID를 장치에 보냅니다(보안 정보는 전송되지 않음).</span><span class="sxs-lookup"><span data-stu-id="f8947-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="f8947-116">알림 수신 시 장치의 앱:</span><span class="sxs-lookup"><span data-stu-id="f8947-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="f8947-117">장치가 보안 페이로드를 요청하는 백 엔드에 접속합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="f8947-118">앱이 장치에서 페이로드를 알림으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="f8947-119">앞의 흐름과 이 자습서에서는 사용자가 로그인한 후 장치가 인증 토큰을 로컬 저장소에 저장한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="f8947-120">이렇게 하면 장치가 이 토큰을 사용하여 알림의 보안 페이로드를 검색할 수 있으므로 매우 원활한 환경이 보장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="f8947-121">응용 프로그램이 인증 토큰을 장치에 저장하지 않거나 이 토큰이 만료될 수 없으면 알림 수신 시 장치 앱은 사용자에게 앱을 시작할지 묻는 메시지가 포함된 일반 알림을 표시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="f8947-122">그리고 나서 앱은 사용자를 인증하고 알림 페이로드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="f8947-123">이 보안 푸시 자습서에서는 푸시 알림을 안전하게 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="f8947-124">이 자습서는 [사용자에게 알림](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) 자습서를 기반으로 빌드되므로 해당 자습서의 단계를 먼저 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="f8947-125">이 자습서에서는 [알림 허브 시작(Windows 스토어)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)에 설명된 대로 알림 허브를 만들고 구성했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="f8947-126">또한 Windows Phone 8.1에 Windows(Windows Phone이 아님) 자격 증명이 필요하며, 백그라운드 작업은 Windows Phone 8.0 또는 Silverlight 8.1에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="f8947-127">Windows 스토어 응용 프로그램은 앱에서 잠금 화면이 사용되는 경우(Appmanifest에서 확인란 클릭)에만 백그라운드 작업을 통해 알림을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="f8947-128">Windows Phone 프로젝트 수정</span><span class="sxs-lookup"><span data-stu-id="f8947-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="f8947-129">**NotifyUserWindowsPhone** 프로젝트에서 App.xaml.cs에 다음 코드를 추가하여 푸시 백그라운드 작업을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="f8947-130">다음 코드 줄을 `OnLaunched()` 메서드의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="f8947-131">App.xaml.cs에서 `OnLaunched()` 메서드의 바로 뒤에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="f8947-132">App.xaml.cs 파일의 맨 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="f8947-133">Visual Studio의 **파일** 메뉴에서 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="f8947-134">푸시 백그라운드 구성 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="f8947-134">Create the Push Background Component</span></span>
<span data-ttu-id="f8947-135">다음은 푸시 백그라운드 구성 요소를 만드는 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="f8947-136">솔루션 탐색기에서 솔루션의 최상위 노드(이 경우 **Solution SecurePush**)를 마우스 오른쪽 단추로 클릭하고 **추가**, **새 프로젝트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="f8947-137">**스토어 앱**을 확장하고 **Windows Phone 앱**, **Windows 런타임 구성 요소(Windows Phone)**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="f8947-138">프로젝트 이름을 **PushBackgroundComponent**로 지정하고 **확인**을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="f8947-139">솔루션 탐색기에서 **PushBackgroundComponent(Windows Phone 8.1)** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="f8947-140">새 클래스 이름을 **PushBackgroundTask.cs**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="f8947-141">**추가** 를 클릭하여 클래스를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="f8947-142">**PushBackgroundComponent** 네임스페이스 정의의 전체 콘텐츠를 다음 코드로 바꾸고 자리 표시자 `{back-end endpoint}`를 백 엔드 배포 시 얻은 백 엔드 끝점으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="f8947-143">솔루션 탐색기에서 **PushBackgroundComponent(Windows Phone 8.1)** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="f8947-144">왼쪽에서 **온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="f8947-145">**검색** 상자에 **Http 클라이언트**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="f8947-146">결과 목록에서 **Microsoft HTTP 클라이언트 라이브러리**를 클릭하고 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="f8947-147">설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-147">Complete the installation.</span></span>
9. <span data-ttu-id="f8947-148">다시 NuGet **검색** 상자에 **Json.net**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="f8947-149">**Json.NET** 패키지를 설치하고 NuGet 패키지 관리자 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="f8947-150">**PushBackgroundTask.cs** 파일의 맨 위에 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="f8947-151">솔루션 탐색기의 **NotifyUserWindowsPhone(Windows Phone 8.1)** 프로젝트에서 **참조**를 마우스 오른쪽 단추로 클릭하고 **참조 추가...**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="f8947-152">참조 관리자 대화 상자에서 **PushBackgroundComponent** 옆의 상자를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="f8947-153">솔루션 탐색기의 **NotifyUserWindowsPhone(Windows Phone 8.1)** 프로젝트에서 **Package.appxmanifest**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="f8947-154">**알림**에서 **알림 가능**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="f8947-155">계속 **Package.appxmanifest**에서 맨 위 근처에서 **선언**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="f8947-156">**사용 가능한 선언** 드롭다운에서 **백그라운드 태스크**, **추가**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="f8947-157">**Package.appxmanifest**의 **속성**에서 **푸시 알림**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="f8947-158">**Package.appxmanifest**의 **앱 설정**에서 **진입점** 필드에 **PushBackgroundComponent.PushBackgroundTask**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="f8947-159">**파일** 메뉴에서 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="f8947-160">응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="f8947-160">Run the Application</span></span>
<span data-ttu-id="f8947-161">응용 프로그램을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="f8947-162">Visual Studio에서 **AppBackend** Web API 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="f8947-163">ASP.NET 웹 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="f8947-164">Visual Studio에서 **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="f8947-165">Windows Phone 에뮬레이터가 실행되고 자동으로 앱을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="f8947-166">**NotifyUserWindowsPhone** 앱 UI에서 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="f8947-167">이는 임의 문자열일 수 있지만 같은 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="f8947-168">**NotifyUserWindowsPhone** 앱 UI에서 **로그인 및 등록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="f8947-169">그리고 나서 **푸시 보내기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f8947-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
