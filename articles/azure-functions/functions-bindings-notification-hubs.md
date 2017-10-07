---
title: "알림 허브 함수 바인딩 aaaAzure | Microsoft Docs"
description: "이해 어떻게 Azure 함수에서 toouse Azure 알림 허브 바인딩."
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
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Azure Functions 알림 허브 출력 바인딩
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

이 문서에서는 설명 어떻게 Azure 함수에서 tooconfigure 및 코드 Azure 알림 허브 바인딩. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

함수는 몇 줄의 코드로 구성된 Azure 알림 허브를 사용하여 푸시 알림을 보낼 수 있습니다. 그러나 hello Azure 알림 허브는 알림 서비스 PNS (플랫폼) toouse 원하는 hello에 대 한 구성 되어야 합니다. Azure 알림 허브를 구성 하 고 tooreceive 알림을 등록 하는 클라이언트 응용 프로그램 개발에 대 한 자세한 내용은 참조 하십시오. [알림 허브 시작](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) hello에 대상 클라이언트 플랫폼을 클릭 하 고 맨 위로.

기본 알림 또는 템플릿 알림을 hello 알림을 보낼 수 있습니다. Hello에 구성 된 대로 특정 알림 플랫폼을 대상으로 기본 알림을 `platform` hello의 속성이 출력 바인딩이 있습니다. 템플릿 알림을 여러 플랫폼 사용된 tootarget를 수 있습니다.   

## <a name="notification-hub-output-binding-properties"></a>알림 허브 출력 바인딩 속성
hello function.json 파일 hello를 다음과 같은 속성을 제공 합니다.

* `name`: 알림 허브 hello 메시지에 대 한 함수 코드에서 사용 되는 변수 이름입니다.
* `type`: 너무 설정 되어 있어야*"notificationHub"*합니다.
* `tagExpression`: 태그 식을 사용 하면 toospecify 알림을 tooa 일련의 hello 태그 식과 일치 하는 tooreceive 알림을 등록 한 장치를 배달할 수 있습니다.  자세한 내용은 [라우팅 및 태그 식](../notification-hubs/notification-hubs-tags-segment-push-message.md)을 참조하세요.
* `hubName`: Hello Azure 포털에에서 hello 알림 허브 리소스의 이름입니다.
* `connection`:이 연결 문자열 이어야 합니다는 **응용 프로그램 설정** 연결 문자열이 설정 toohello *DefaultFullSharedAccessSignature* 알림 허브에 대 한 값입니다.
* `direction`: 너무 설정 되어 있어야*"out"*합니다. 
* `platform`: hello 플랫폼 속성 hello 알림을 플랫폼 알림 대상인을 나타냅니다. Hello 다음 값 중 하나 여야 합니다.
  * 기본적으로 hello 플랫폼 속성 바인딩을 hello 출력에서 생략 된 경우 템플릿 알림을 수 사용된 tootarget hello Azure 알림 허브에 구성 된 모든 플랫폼입니다. Azure 알림 허브를 사용 하 여 플랫폼 알림 크로스 toosend 일반적 템플릿을 사용 하 여 대 한 자세한 내용은 참조 [템플릿](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)합니다.
  * `apns`: Apple Push Notification Service입니다. APNS에 대 한 hello 알림 허브를 구성 및 클라이언트 앱에서 hello 알림을 받는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 알림 허브와 보내는 푸시 알림 tooiOS](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging)입니다. ADM에 대 한 hello 알림 허브를 구성 하 고 hello 알림을 Kindle 응용 프로그램에서 받은에 대 한 자세한 내용은 참조 하세요. [Kindle 앱에 대 한 알림 허브 시작](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Google Cloud Messaging](https://developers.google.com/cloud-messaging/)입니다. Firebase 클라우드 메시징, 즉 hello GCM의 새 버전 에서도 지원 됩니다. GCM/FCM에 대 한 hello 알림 허브를 구성 하 고 Android 클라이언트 앱에서 hello 알림 받기에 대 한 자세한 내용은 참조 하십시오. [Azure 알림 허브와 보내는 푸시 알림 tooAndroid](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: Windows 플랫폼을 대상으로 하는 [Windows 푸시 알림 서비스](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview)입니다. Windows Phone 8.1 이상도 WNS에서 지원됩니다. Wns hello 알림 허브를 구성 및 유니버설 Windows 플랫폼 (UWP) 응용 프로그램에서 hello 알림을 받는 방법에 대 한 자세한 내용은 참조 하세요. [알림 허브에 대 한 Windows 유니버설 플랫폼 앱 시작](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [Microsoft 푸시 알림 서비스](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx)입니다. 이 플랫폼은 Windows Phone 8 및 이전 Windows Phone 플랫폼을 지원합니다. MPNS에 대 한 hello 알림 허브를 구성 및 Windows Phone 앱에서 hello 알림을 받는 방법에 대 한 자세한 내용은 참조 하십시오. [Azure 알림 허브에서 Windows Phone 푸시 알림 보내기](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

예제 function.json:

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

## <a name="notification-hub-connection-string-setup"></a>알림 허브 연결 문자열 설정
알림 허브 toouse 출력 바인딩이 hello 허브에 대 한 hello 연결 문자열을 구성 해야 합니다. Hello에 이렇게 *통합* 알림 허브를 선택 하거나 새로 만드는 하 여 탭 합니다. 

Hello에 대 한 연결 문자열을 추가 하 여 기존 허브에 대 한 연결 문자열을 수동으로 추가할 수 있습니다 *DefaultFullSharedAccessSignature* tooyour 알림 허브입니다. 이 연결 문자열 기능 액세스 권한을 toosend 알림 메시지를 제공합니다. hello *DefaultFullSharedAccessSignature* hello에서 연결 문자열 값에 액세스할 수 **키** hello Azure 포털에서에서 알림 허브 리소스의 hello 주 블레이드에서 단추입니다. toomanually 허브를 사용 하 여 hello 다음 단계에 대 한 연결 문자열을 추가 합니다. 

1. Hello에 **함수 앱** hello Azure 포털의 블레이드에서 클릭 **함수 응용 프로그램 설정 > tooApp 서비스 설정 이동**합니다.
2. Hello에 **설정** 블레이드에서 클릭 **응용 프로그램 설정**합니다.
3. Toohello 아래로 스크롤하여 **앱 설정** 섹션에 대 한 명명 된 항목 추가 및 *DefaultFullSharedAccessSignature* 알림 허브에 대 한 값입니다.
4. 출력 바인딩 hello에 문자열 이름을 설정 하는 응용 프로그램을 참조 합니다. 비슷한 너무**MyHubConnectionString** 위의 hello 예제에서 사용 합니다.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>C# 큐 트리거를 사용한 APNS 기본 알림
이 예제에서는 hello에 toouse 형식을 정의 하는 방법을 보여 줍니다. [Microsoft Azure 알림 허브 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend 기본 APNS 알림 합니다. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>C# 큐 트리거를 사용한 GCM 기본 알림
이 예제에서는 hello에 toouse 형식을 정의 하는 방법을 보여 줍니다. [Microsoft Azure 알림 허브 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend 기본 GCM 알림 합니다. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>C# 큐 트리거를 사용한 WNS 기본 알림
이 예제에서는 hello에 toouse 형식을 정의 하는 방법을 보여 줍니다. [Microsoft Azure 알림 허브 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend 네이티브 WNS 알림 메시지입니다. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
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
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Node.js 타이머 트리거에 대한 템플릿 예제
이 예제에서는 `location` 및 `message`을 포함하는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.

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

## <a name="template-example-for-f-timer-triggers"></a>F# 타이머 트리거에 대한 템플릿 예제
이 예제에서는 `location` 및 `message`을 포함하는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md)에 대한 알림을 보냅니다.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>out 매개 변수를 사용하는 템플릿 예제
이 예제에 대 한 알림을 보냅니다는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) 를 포함 하는 `message` hello 서식 파일에서 자리 표시자입니다.

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

## <a name="template-example-with-asynchronous-function"></a>비동기 함수를 사용하는 템플릿 예제
비동기 코드를 사용하는 경우 out 매개 변수가 허용되지 않습니다. 이 경우 사용 `IAsyncCollector` tooreturn 템플릿 알림을 합니다. hello 다음 코드는 비동기 위의 hello 코드의 예입니다. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>JSON을 사용하는 템플릿 예제
이 예제에 대 한 알림을 보냅니다는 [템플릿 등록](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) 를 포함 하는 `message` 유효한 JSON 문자열을 사용 하 여 hello 서식 파일에서 자리 표시자입니다.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>알림 허브 라이브러리 형식을 사용하는 템플릿 예제
이 예제에서는 hello에 toouse 형식을 정의 하는 방법을 보여 줍니다. [Microsoft Azure 알림 허브 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다. 

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

## <a name="next-steps"></a>다음 단계
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

