---
title: "알림 허브를 통해 사용자에게 크로스 플랫폼 알림 보내기(ASP.NET)"
description: "알림 허브 템플릿을 사용하여 모든 플랫폼을 대상으로 하는 플랫폼 중립적인 알림을 단일 요청으로 보내는 방법을 보여 줍니다."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="31f47-103">알림 허브를 통해 사용자에게 크로스 플랫폼 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="31f47-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="31f47-104">이전 자습서인 [알림 허브를 통해 사용자에게 알림]에서는 인증된 특정 사용자가 등록한 모든 장치에 알림을 푸시하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="31f47-105">해당 자습서에서는 지원되는 각 클라이언트 플랫폼에 알림을 보내기 위해 여러 요청이 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="31f47-106">알림 허브는 특정 장치가 알림을 받는 방법을 지정할 수 있는 템플릿을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="31f47-107">이 경우 크로스 플랫폼 알림 전송이 간소화됩니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="31f47-108">이 항목에서는 템플릿을 사용하여 단일 요청으로 모든 플랫폼을 대상으로 하는, 플랫폼을 알 수 없는 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="31f47-109">템플릿에 대한 자세한 내용은 [Azure Notification Hubs 개요][Templates]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31f47-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31f47-110">Windows Phone 프로젝트 8.1 및 이전 버전은 Visual Studio 2017에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="31f47-111">자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31f47-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="31f47-112">알림 허브를 사용하면 장치가 동일한 태그로 여러 템플릿을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="31f47-113">이 경우 해당 태그를 대상으로 들어오는 메시지가 있으면 각 템플릿에 대해 하나씩 여러 개의 알림이 장치에 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="31f47-114">이런 방식으로 Windows 스토어 앱에 알림 메시지와 배지 둘 다로 표시하는 등 여러 시각적 알림에 동일한 메시지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="31f47-115">템플릿을 사용하여 크로스 플랫폼 알림을 보내려면 다음 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="31f47-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="31f47-116">Visual Studio의 솔루션 탐색기에서 **컨트롤러** 폴더를 확장한 다음 RegisterController.cs 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="31f47-117">**Put** 메서드에서 새 등록을 만드는 코드 블록을 찾아서 `switch`의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    <span data-ttu-id="31f47-118">이 코드는 플랫폼 특정 메서드를 호출하여 기본 등록이 아니라 템플릿 등록을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="31f47-119">템플릿 등록은 기본 등록에서 파생되므로 기존 등록을 수정할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="31f47-120">**알림** 컨트롤러에서 **sendNotification** 메서드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="31f47-121">이 코드는 네이티브 페이로드를 지정할 필요 없이 동시에 모든 플랫폼에 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="31f47-122">Notification Hubs는 등록된 템플릿에 지정된 대로 올바른 페이로드를 작성하고 제공된 *태그* 값을 가진 모든 장치에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="31f47-123">WebApi 백 엔드 프로젝트를 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="31f47-124">클라이언트 앱을 다시 실행하고 등록이 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="31f47-125">(옵션) 클라이언트 앱을 두 번째 장치에 배포한 후 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="31f47-126">각 장치에 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f47-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="31f47-127">Next Steps</span></span>
<span data-ttu-id="31f47-128">이 자습서를 마쳤습니다. 이제 다음 항목에서 알림 허브 및 템플릿에 대해 자세히 알아보십시오.</span><span class="sxs-lookup"><span data-stu-id="31f47-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="31f47-129">**[Notification Hubs를 사용하여 뉴스 속보 보내기]**</span><span class="sxs-lookup"><span data-stu-id="31f47-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="31f47-130">다른 템플릿 사용 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="31f47-131">**[Azure Notification Hubs 개요][Templates]**</span><span class="sxs-lookup"><span data-stu-id="31f47-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="31f47-132">개요 항목에는 템플릿에 대한 세부 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31f47-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="31f47-133">[Notification Hubs를 사용하여 뉴스 속보 보내기]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="31f47-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="31f47-134">[알림 허브를 통해 사용자에게 알림]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="31f47-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
