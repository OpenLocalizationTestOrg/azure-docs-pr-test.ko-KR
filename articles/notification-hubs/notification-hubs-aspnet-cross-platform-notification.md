---
title: "알림 허브 (ASP.NET)와 aaaSend 플랫폼 간 알림 toousers"
description: "자세한 내용은 방법 toouse 알림 허브 템플릿 toosend 단일 요청에서 모든 플랫폼을 대상 플랫폼 제약 없는 알림입니다."
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>알림 허브와 toousers 플랫폼 간 알림 보내기
Hello 이전 자습서에서 [알림 허브와 사용자에 게 알림], toopush 알림 tooall 장치는 특정 인증 된 사용자가 등록 하는 방법을 배웠습니다. 이 자습서에서는 여러 요청 필요한 toosend 알림 tooeach 지원 클라이언트 플랫폼 이었습니다. 알림 허브 수 있는 템플릿을 지 원하는 특정 장치 tooreceive 알림을가 하는 방법을 지정 합니다. 이 경우 크로스 플랫폼 알림 전송이 간소화됩니다. 이 항목에서 설명 방법을 단일 요청에서 모든 플랫폼을 대상 플랫폼 제약 없는 알림 템플릿 toosend tootake 활용 합니다. 템플릿에 대한 자세한 내용은 [Azure Notification Hubs 개요][Templates]를 참조하세요.
> [!IMPORTANT]
> Windows Phone 프로젝트 8.1 및 이전 버전은 Visual Studio 2017에서 지원되지 않습니다. 자세한 내용은 [Visual Studio 2017 플랫폼 대상 지정 및 호환성](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs)을 참조하세요.

> [!NOTE]
> 알림 허브 사용 하면 장치 tooregister hello 사용 하 여 여러 템플릿을 같은 태그입니다. 이 경우 들어오는 메시지에서 여러 개의 알림이 태그에 결과 대상으로 배달 각 템플릿에 대해 하나 toohello 장치. Toodisplay 있습니다 hello 배지로 Windows 스토어 앱에 알림 메시지 둘 다 등의 여러 시각적 알림의 동일 메시지 따라서 수 있습니다.
> 
> 

Hello 단계 toosend 플랫폼 간 알림 템플릿을 사용 하 여 다음을 완료 합니다.

1. Hello Visual Studio의 솔루션 탐색기에서에서 확장 hello **컨트롤러** 폴더를 다음 열기 hello RegisterController.cs 파일입니다.
2. Hello에 hello 코드 블록을 찾아 **배치** 새 등록을 만드는 메서드를 대체 hello `switch` 코드 다음 hello를 사용 하 여 콘텐츠:
   
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
   
    이 코드는 hello 플랫폼별 메서드 toocreate 네이티브 등록 하는 대신 템플릿 등록을 호출합니다. 템플릿 등록은 기본 등록에서 파생되므로 기존 등록을 수정할 필요는 없습니다.
3. Hello에 **알림** 컨트롤러, replace hello **sendNotification** 메서드 코드 다음 hello로:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    이 코드 tooall 플랫폼 알림을 전송에서 hello 동일한 시간 및 toospecify 필요 없이 원시 페이로드입니다. 알림 허브 빌드되고 제공 제공 hello로 올바른 페이로드 tooevery 장치 hello *태그* hello 등록 서식 파일에 지정 된 값입니다.
4. WebApi 백 엔드 프로젝트를 다시 게시합니다.
5. Hello 클라이언트 응용 프로그램을 다시 실행 하 고 등록에 성공 했는지 확인 합니다.
6. (선택 사항) Hello 클라이언트 응용 프로그램 tooa 두 번째 장치를 배포한 다음 hello 응용 프로그램을 실행 합니다.
   
    각 장치에 알림이 표시됩니다.

## <a name="next-steps"></a>다음 단계
이 자습서를 마쳤습니다. 이제 다음 항목에서 알림 허브 및 템플릿에 대해 자세히 알아보십시오.

* **[알림 허브 toosend 최신 뉴스를 사용 하 여]** <br/>다른 템플릿 사용 시나리오를 보여 줍니다.
* **[Azure Notification Hubs 개요][Templates]**<br/>개요 항목에는 템플릿에 대한 세부 정보가 포함되어 있습니다.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[알림 허브 toosend 최신 뉴스를 사용 하 여]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[알림 허브와 사용자에 게 알림]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
