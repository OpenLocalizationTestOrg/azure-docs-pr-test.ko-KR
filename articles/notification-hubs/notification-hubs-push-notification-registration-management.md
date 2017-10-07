---
title: "aaaRegistration 관리"
description: "이 항목에서는 순서 tooreceive에서 알림 허브를 사용 하 여 tooregister 장치 푸시 알림 방법을 설명 합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>등록 관리
## <a name="overview"></a>개요
이 항목에서는 순서 tooreceive에서 알림 허브를 사용 하 여 tooregister 장치 푸시 알림 방법을 설명 합니다. hello 항목 높은 수준에서 등록 한 다음 장치를 등록 하기 위한 두 hello 주 패턴이 도입: hello 장치에서 등록 직접 toohello 알림 허브를 통해 등록 하는 응용 프로그램 백 엔드 합니다. 

## <a name="what-is-device-registration"></a>장치 등록이란?
Notification Hub에 장치 등록은 **등록** 또는 **설치**를 사용하여 수행됩니다.

#### <a name="registrations"></a>등록
등록 하는 태그 및 템플릿을 사용 하 여 장치에 대 한 서비스 PNS (플랫폼 알림) 처리 하는 hello에 연결 합니다. ChannelURI, 장치 토큰 또는 GCM 등록 id hello PNS 핸들 수 있습니다. 태그는 사용 되는 tooroute 알림 toohello 올바른 장치 핸들 집합입니다. 자세한 내용은 [라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요. 템플릿은 등록 당 변환을 사용 하는 tooimplement입니다. 자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md)을 사용하세요.

#### <a name="installations"></a>설치
설치는 푸시 모음 관련 속성을 포함하고 있는 향상된 등록입니다. 장치를 최신 하 고 가장 좋은 방법은 tooregistering hello 이며 그러나 아직 클라이언트 쪽 .NET SDK([백 엔드 작업을 위한 알림 허브 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/))에서는 지원되지 않습니다.  즉, toouse hello 갖기 hello 클라이언트 장치 자체에서 등록 하는 경우 [알림 허브 REST API](https://msdn.microsoft.com/library/mt621153.aspx) toosupport 설치에 접근 합니다. 백 엔드 서비스를 사용 하는 경우 수 toouse 있어야 [백 엔드 작업에 대 한 알림 허브 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.

hello 다음은 몇 가지 주요 이점은 toousing 설치입니다.

* 설치 만들기 또는 업데이트가 완전히 멱등 상태입니다. 따라서 중복 등록을 걱정할 필요 없이 재시도할 수 있습니다.
* hello 설치 모델을 사용 하면 쉽게 toodo 개별 푸시-특정 장치를 대상으로 지정 합니다. 시스템 태그 **"$InstallationId:[installationId]"** 는 각 설치 기반 등록에 자동으로 추가됩니다. 따라서 호출할 수 있습니다 송신 toothis 태그 tootarget 특정 장치 필요 toodo 추가 코딩 없이 합니다.
* 또한 설치를 사용 하 여 toodo 부분 등록 업데이트 수 있습니다. hello 부분 업데이트를 설치 하는 요청 된 hello를 사용 하 여 패치 메서드로 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902)합니다. Tooupdate 태그 hello 등록 하려는 경우 특히 유용 합니다. 없습니다 toopull hello 전체 등록 다운 하 고 모든 hello 이전 태그 다시 보내십시오.

설치 된 hello hello 다음과 같은 속성을 포함할 수 있습니다. Hello 설치 속성 참조의 전체 목록을 보려면 [만들기 또는 REST api 설치를 덮어쓸](https://msdn.microsoft.com/library/azure/mt621153.aspx) 또는 [설치 속성](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) hello에 대 한 합니다.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



것이 더 이상 만료 등록 및 기본적으로 설치 하는 중요 한 toonote 합니다.

등록 및 설치는 각 장치/채널에 대한 유효한 PNS 핸들을 포함해야 합니다. Hello 장치에서 클라이언트 응용 프로그램에서 PNS 핸들을 가져올 수만, 한 패턴 hello 클라이언트 응용 프로그램으로 해당 장치에 직접 tooregister은입니다. Hello 다른 손, 보안 고려 사항 및 비즈니스 논리 관련 tootags toomanage 장치 등록 hello 앱 백 엔드에 필요할 수 있습니다. 

#### <a name="templates"></a>템플릿
Toouse 하려는 경우 [템플릿](notification-hubs-templates-cross-platform-push-messages.md), hello 장치 설치 json에서 해당 장치와 연결 된 모든 템플릿을 포함할 형식 (위의 예제 참조). hello 템플릿 이름 도움말 hello에 대 한 서로 다른 템플릿을 대상으로 동일한 장치입니다.

각 템플릿 이름이 매핑됨을 tooa 템플릿 본문 및 선택적 태그 집합을 참고 합니다. 또한 각 플랫폼이 추가 템플릿 속성을 가질 수 있습니다. (WNS를 사용 하 여) Windows 스토어 및 Windows Phone 8 (MPNS를 사용 하 여)에 대 한 추가 헤더 집합이 hello 서식 파일의 일부를 수 있습니다. APNs의 경우 hello 만료 속성 tooeither 상수 또는 tooa 템플릿 식을 설정할 수 있습니다. Hello 설치 속성 참조의 전체 목록을 보려면 [만들거나 rest 설치를 덮어쓸](https://msdn.microsoft.com/library/azure/mt621153.aspx) 항목입니다.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Windows 스토어 앱용 보조 타일
Windows 스토어 클라이언트 응용 프로그램에 대 한 toosecondary 타일은 알림을 보내는 hello 동일 보내 toohello 기본으로 합니다. 이 기능은 설치에서도 지원됩니다. 보조 타일 클라이언트 앱에는 hello SDK에서 투명 하 게 처리 하는 다른 ChannelUri 한지 확인 합니다.

hello SecondaryTiles 사전을 사용 하 여 hello 동일한 TileId Windows 스토어 앱에 사용 되는 toocreate hello SecondaryTiles 개체입니다.
처럼 hello 기본 ChannelUri, 보조 타일의 Channeluri 언제 든 지 변경할 수 있습니다. Hello 알림 허브를 업데이트에서 tookeep hello 설치 순서에에서 hello 장치를 새로 고쳐야 하 hello로 hello 보조 타일의 최신 Channeluri 합니다.

## <a name="registration-management-from-hello-device"></a>Hello 장치에서 등록 관리
클라이언트 앱에서 장치 등록을 관리 하는 경우 hello 백 엔드는 알림 전송만 합니다. 클라이언트 앱을 toodate, PNS 핸들을 유지 하 고 태그를 등록 합니다. 다음 그림 hello이이 패턴을 보여 줍니다.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

hello 장치는 먼저 hello PNS에서에서 PNS 핸들과 hello 검색 다음 hello 알림 허브에 직접 등록 합니다. Hello 등록 되 면 hello 앱 백 엔드에서 해당 등록을 대상으로 하는 알림을 보낼 수 있습니다. 방법에 대 한 자세한 내용은 toosend 알림을 참조 [라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)합니다.
이 예에서 사용할 참고의 hello 장치에서 알림 허브 권한 tooaccess를만 수신 대기 합니다. 자세한 내용은 [보안](notification-hubs-push-notification-security.md)을 참조하세요.

Hello 장치에서 등록 된 hello 가장 간단한 방법은 수도 있지만 몇 가지 단점이 있습니다.
hello 첫 번째 단점은 클라이언트 앱 hello 앱 활성화 된 경우 해당 태그 업데이트할만 수입니다. 예를 들어 사용자는 추가 태그 (예를 들어 Seahawks) hello 첫 번째 장치를 등록 하는 경우 태그 관련된 toosport 팀을 등록 하는 두 개의 장치를 두 번째 장치 hello hello Seahawks에 대 한 hello 알림을 때까지 나타나지 않습니다 hello에 hello 앱 두 번째 장치를 두 번 실행 됩니다. 보다 일반적으로 태그를 여러 장치에 영향을 받는 hello 백 엔드에서 태그 관리 경우 알맞은 방법 있습니다.
hello 두 번째의 단점은 hello 클라이언트 응용 프로그램에서 등록을 관리 하는 앱을 해킹 가능 하므로 특별히 주의 해야 hello 등록 toospecific 태그를 보호 하려면 즉, "태그 수준 보안 합니다." hello 섹션에 설명 된 대로

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>설치를 사용 하는 장치에서 알림 허브와 예제 코드 tooregister
이 때만 지원 됩니다 hello를 사용 하 여 [알림 허브 REST API](https://msdn.microsoft.com/library/mt621153.aspx)합니다.

Hello를 사용 하 여 hello 패치 메서드를 사용할 수도 있습니다 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902) hello 설치를 업데이트 합니다.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>등록을 사용 하는 장치에서 알림 허브와 예제 코드 tooregister
이러한 메서드 만들기 또는 호출 된 hello 장치에 대 한 등록을 업데이트 합니다. 즉, 순서-tooupdate hello 핸들 또는 hello 태그에 hello 전체 등록 덮어쓰기 해야 합니다. 등록은 일시적인 항목 이므로 특정 장치에 필요한 hello 현재 태그와 신뢰할 수 있는 저장소는 항상 있어야 기억 합니다.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>백 엔드에서 등록 관리
Hello 백 엔드에서 등록을 관리 하려면 추가 코드를 작성 해야 합니다. hello 앱 태그 및 템플릿) (함께 시작 될 때마다 업데이트 된 PNS 핸들 toohello 백 엔드 hello 및 hello 백 엔드 hello 알림 허브에서이 핸들을 업데이트 해야 hello 앱 hello 장치에서 제공 해야 합니다. hello 다음 그림에 이러한 디자인이 나와 있습니다.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

hello hello 백 엔드에서 등록을 관리의 이점 중 hello 기능 toomodify 태그 tooregistrations hello hello 장치에서 해당 앱이 비활성, 경우에 있고 tooauthenticate hello에 대 한 클라이언트 응용 프로그램을 tooits 등록 하는 태그를 추가 하기 전에입니다.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>설치를 사용 하는 백 엔드에서 알림 허브와 예제 코드 tooregister
hello 클라이언트 장치 여전히 정의와 PNS 핸들 및 관련 된 설치 속성 이전과 가져오고 등 hello 백 엔드 태그를 삽입 hello 등록을 수행 하 고 권한을 부여할 수 있는 hello 백 엔드에 사용자 지정 API 호출 hello를 활용할 수 [용 알림 허브 SDK 백 엔드 작업](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.

Hello를 사용 하 여 hello 패치 메서드를 사용할 수도 있습니다 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902) hello 설치를 업데이트 합니다.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>등록 id를 사용 하는 장치에서 알림 허브와 예제 코드 tooregister
앱 백 엔드에서 등록에 대해 기본 CRUDS 작업을 수행할 수 있습니다. 예:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


hello 백 엔드 등록 업데이트 간의 동시성을 처리 해야 합니다. 서비스 버스는 등록 관리를 위해 낙관적 동시성 제어를 제공합니다. Hello HTTP 수준에서 등록 관리 작업에서 ETag의 hello 사용으로 구현 됩니다. 이 기능은 동시성 문제로 인해 업데이트가 거부될 경우 예외를 throw하는 Microsoft SDK에 의해 투명하게 사용됩니다. hello 앱 백 엔드는 이러한 예외를 처리 하 고 필요한 경우 hello 업데이트를 다시 시도 하는 일을 담당 합니다.

