---
title: "Azure Functions Notification Hub 바인딩 | Microsoft Docs"
description: "Azure Functions에서 Azure 알림 허브 바인딩을 사용하는 방법을 파악합니다."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, 동적 계산, 서버를 사용하지 않는 아키텍처"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="d02b0-104">Azure Functions 알림 허브 출력 바인딩</span><span class="sxs-lookup"><span data-stu-id="d02b0-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d02b0-105">이 문서에서는 Azure Functions에서 Azure 알림 허브 바인딩을 구성하고 코딩하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="d02b0-106">함수는 몇 줄의 코드로 구성된 Azure 알림 허브를 사용하여 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="d02b0-107">그러나 Azure 알림 허브는 사용하려는 PNS(플랫폼 알림 서비스)에 대해 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="d02b0-108">Azure 알림 허브를 구성하고 알림 수신을 위해 등록하는 클라이언트 응용 프로그램을 개발하는 데 대한 자세한 내용은 [알림 허브 시작](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 을 참조하고 맨 위에 있는 대상 클라이언트 플랫폼을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="d02b0-109">보내는 알림은 기본 알림 또는 템플릿 알림일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="d02b0-110">기본 알림은 출력 바인딩의 `platform` 속성에 구성된 특정 알림 플랫폼을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="d02b0-111">템플릿 알림은 여러 플랫폼을 대상으로 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="d02b0-112">알림 허브 출력 바인딩 속성</span><span class="sxs-lookup"><span data-stu-id="d02b0-112">Notification hub output binding properties</span></span>
<span data-ttu-id="d02b0-113">function.json 파일은 다음 속성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="d02b0-114">`name` : 알림 허브 메시지에 대한 함수 코드에 사용되는 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="d02b0-115">`type` : *"notificationHub"*로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="d02b0-116">`tagExpression` : 태그 식을 사용하면 알림을 태그 식과 일치하는 알림을 수신하도록 등록된 일련의 장치에 배달하도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="d02b0-117">자세한 내용은 [라우팅 및 태그 식](../notification-hubs/notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="d02b0-118">`hubName` : Azure 포털에서 알림 허브 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="d02b0-119">`connection` : 이 연결 문자열은 알림 허브에 대한 **DefaultFullSharedAccessSignature** 값으로 설정된 *응용 프로그램 설정* 연결 문자열이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="d02b0-120">`direction` : *"out"*으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="d02b0-121">`platform`: 플랫폼 속성은 알림의 대상으로 지정된 알림 플랫폼을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="d02b0-122">다음 값 중 하나여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="d02b0-123">기본적으로 출력 바인딩에서 platform 속성을 생략하면 템플릿 알림을 사용하여 Azure Notification Hub에 구성된 플랫폼을 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="d02b0-124">일반적으로 Azure 알림 허브 알림에서 템플릿을 사용하여 플랫폼 간 알림을 보내는 방법에 대한 자세한 내용은 [템플릿](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="d02b0-125">`apns`: Apple Push Notification Service입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="d02b0-126">APNS에 대한 알림 허브를 구성하고 클라이언트 앱에서 알림을 받는 방법에 대한 자세한 내용은 [Azure 알림 허브를 사용하여 iOS에 푸시 알림 보내기](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="d02b0-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging)입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="d02b0-128">ADM에 대한 알림 허브를 구성하고 Kindle 앱에서 알림을 받는 방법에 대한 자세한 내용은 [Kindle 앱에 대한 알림 허브 시작](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="d02b0-129">`gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/)입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="d02b0-130">새 버전의 GCM인 Firebase Cloud Messaging도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="d02b0-131">GCM/FCM에 대한 알림 허브를 구성하고 Android 클라이언트 앱에서 알림을 받는 방법에 대한 자세한 내용은 [Azure 알림 허브를 사용하여 Android에 푸시 알림 보내기](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="d02b0-132">`wns`: Windows 플랫폼을 대상으로 하는 [Windows 푸시 알림 서비스](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="d02b0-133">Windows Phone 8.1 이상도 WNS에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="d02b0-134">WNS에 대한 알림 허브를 구성하고 UWP(유니버설 Windows 플랫폼) 앱에서 알림을 받는 방법에 대한 자세한 내용은 [유니버설 Windows 플랫폼 앱에 대한 알림 허브 시작](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="d02b0-135">`mpns`: [Microsoft 푸시 알림 서비스](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx)입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="d02b0-136">이 플랫폼은 Windows Phone 8 및 이전 Windows Phone 플랫폼을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="d02b0-137">MPNS에 대한 알림 허브를 구성하고 Windows Phone 앱에서 알림을 받는 방법에 대한 자세한 내용은 [Windows Phone에서 Azure 알림 허브를 사용하여 푸시 알림 보내기](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d02b0-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="d02b0-138">예제 function.json:</span><span class="sxs-lookup"><span data-stu-id="d02b0-138">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="d02b0-139">알림 허브 연결 문자열 설정</span><span class="sxs-lookup"><span data-stu-id="d02b0-139">Notification hub connection string setup</span></span>
<span data-ttu-id="d02b0-140">알림 허브 출력 바인딩을 사용하려면 허브에 대한 연결 문자열을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="d02b0-141">*통합* 탭에서 알림 허브를 선택하거나 새로 만들어서 이를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="d02b0-142">알림 허브에 *DefaultFullSharedAccessSignature* 에 대한 연결 문자열을 추가하여 기존 허브에 대한 연결 문자열을 수동으로 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="d02b0-143">이 연결 문자열에서는 알림 메시지를 보내는 함수 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="d02b0-144">*DefaultFullSharedAccessSignature* 연결 문자열 값은 Azure 포털의 알림 허브 리소스의 주 블레이드에 있는 **키** 단추에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="d02b0-145">허브에 대한 연결 문자열을 수동으로 추가하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="d02b0-146">Azure Portal의 **함수 앱** 블레이드에서 **함수 앱 설정 > App Service 설정으로 이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="d02b0-147">**설정** 블레이드에서 **응용 프로그램 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="d02b0-148">**앱 설정** 섹션까지 아래로 스크롤하여 알림 허브에 *DefaultFullSharedAccessSignature* 값에 대한 명명된 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="d02b0-149">출력 바인딩에서 앱 설정 문자열 이름을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="d02b0-150">위의 예제에서 사용된 **MyHubConnectionString** 과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="d02b0-151">C# 큐 트리거를 사용한 APNS 기본 알림</span><span class="sxs-lookup"><span data-stu-id="d02b0-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="d02b0-152">이 예제에서는 [Microsoft Azure Notification Hubs 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)에 정의된 형식을 사용하여 기본 APNS 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="d02b0-153">C# 큐 트리거를 사용한 GCM 기본 알림</span><span class="sxs-lookup"><span data-stu-id="d02b0-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="d02b0-154">이 예제에서는 [Microsoft Azure Notification Hubs 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)에 정의된 형식을 사용하여 기본 GCM 알림을 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="d02b0-155">C# 큐 트리거를 사용한 WNS 기본 알림</span><span class="sxs-lookup"><span data-stu-id="d02b0-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="d02b0-156">이 예제에서는 [Microsoft Azure Notification Hubs 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)에 정의된 형식을 사용하여 기본 WNS 알림 메시지를 보내는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="d02b0-157">Node.js 타이머 트리거에 대한 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="d02b0-158">이 예제에서는 `location` 및 `message`을 포함하는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="d02b0-159">F# 타이머 트리거에 대한 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="d02b0-160">이 예제에서는 `location` 및 `message`을 포함하는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="d02b0-161">out 매개 변수를 사용하는 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-161">Template example using an out parameter</span></span>
<span data-ttu-id="d02b0-162">이 예제에서는 템플릿에 `message` 자리 표시자가 포함된 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="d02b0-163">비동기 함수를 사용하는 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-163">Template example with asynchronous function</span></span>
<span data-ttu-id="d02b0-164">비동기 코드를 사용하는 경우 out 매개 변수가 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="d02b0-165">이 경우 `IAsyncCollector`를 사용하여 템플릿 알림을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="d02b0-166">다음 코드는 위 코드의 비동기 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="d02b0-167">JSON을 사용하는 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-167">Template example using JSON</span></span>
<span data-ttu-id="d02b0-168">이 예제에서는 유효한 JSON 문자열을 사용하여 템플릿에 `message` 자리 표시자가 포함된 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="d02b0-169">알림 허브 라이브러리 형식을 사용하는 템플릿 예제</span><span class="sxs-lookup"><span data-stu-id="d02b0-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="d02b0-170">이 예제에서는 [Microsoft Azure Notification Hubs 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)에 정의된 형식을 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d02b0-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="d02b0-171">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d02b0-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

