---
title: "aaaHow toouse Java 통해 알림 허브"
description: "자세한 내용은 방법 toouse Azure 알림 허브는 Java 백 엔드에서 합니다."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>어떻게 toouse Java에서 알림 허브
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

이 항목에서는 hello 완벽 하 게 지원 hello 새 공식의 주요 기능 설명 Azure 알림 허브 Java SDK입니다. 오픈 소스 프로젝트 이며 hello SDK 코드 전체에서 볼 수 있습니다 [Java SDK]합니다. 

일반적으로 Java/PHP/Python/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 있습니다 hello MSDN 항목에 설명 된 대로 hello 알림 허브 REST 인터페이스를 사용 하 여 [알림 허브 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)합니다. 이 Java SDK는 Java에서 이러한 REST 인터페이스에 대한 씬 래퍼를 제공합니다. 

hello SDK에서 지 원하는 현재:

* 알림 허브에 대한 CRUD 
* 등록에 대한 CRUD
* 설치 관리
* 등록 가져오기/내보내기
* 일반 보내기
* 예약된 보내기
* Java NIO를 통한 비동기 작업
* 지원되는 플랫폼: APNS(iOS), GCM(Android), WNS(Windows 스토어 앱), MPNS(Windows Phone), ADM(Amazon Kindle Fire), Baidu(Google 서비스가 포함되지 않은 Android) 

## <a name="sdk-usage"></a>SDK 사용
### <a name="compile-and-build"></a>컴파일 및 빌드
[Maven]

toobuild:

    mvn package

## <a name="code"></a>코드
### <a name="notification-hub-cruds"></a>알림 허브 CRUD
**NamespaceManager 만들기:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**알림 허브 만들기:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 또는

    hub = new NotificationHub("connection string", "hubname");

**알림 허브 가져오기:**

    hub = namespaceManager.getNotificationHub("hubname");

**알림 허브 업데이트:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**알림 허브 삭제:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>등록 CRUD
**알림 허브 클라이언트 만들기:**

    hub = new NotificationHub("connection string", "hubname");

**Windows 등록 만들기:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**iOS 등록 만들기:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

마찬가지로 Android(GCM), Windows Phone(MPNS) 및 Kindle Fire(ADM)에 대한 등록도 만들 수 있습니다.

**템플릿 등록 만들기:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**create registrationid + upsert 패턴을 사용하여 등록 만들기:**

Hello 장치의 등록 id를 저장 하는 경우 분실 tooany 응답 인해 중복을 제거 합니다.

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**등록 업데이트:**

    hub.updateRegistration(reg);

**등록 삭제:**

    hub.deleteRegistration(regid);

**등록 쿼리:**

* **단일 등록 가져오기:**
  
    hub.getRegistration(regid);
* **허브에서 모든 등록 가져오기:**
  
    hub.getRegistrations();
* **태그가 포함된 등록 가져오기:**
  
    hub.getRegistrationsByTag("myTag");
* **채널별 등록 가져오기:**
  
    hub.getRegistrationsByChannel("devicetoken");

모든 컬렉션 쿼리는 $top 및 연속 토큰을 지원합니다.

### <a name="installation-api-usage"></a>설치 API 사용
설치 API는 등록 관리 대신 사용할 수 있는 메커니즘입니다. Trivial 되지 않으며 잘못 또는 비효율적으로 쉽게 설정할 수 있는 여러 등록을 유지 하는 대신 이제를 가능한 toouse 단일 설치 개체. 이 경우 설치에는 푸시 채널(장치 토큰), 태그, 템플릿, 보조 타일(WNS 및 APNS의 경우) 등 필요한 모든 항목이 포함됩니다. Toocall hello 서비스 tooget Id를 더 이상 필요 없는-방금 생성 GUID 또는 다른 식별자, 장치에 유지 및 tooyour 백 엔드 푸시 채널 (장치 토큰)와 함께 보내기. Hello 백 엔드에만 수행 해야 한 번만 호출: 필요한 경우 무료 tooretry 바랍니다 CreateOrUpdateInstallation, 것은 완벽 하 게 idempotent입니다.

Amazon Kindle Fire의 경우 이 호출은 다음과 같습니다.

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Tooupdate 하려는 경우 해당: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

우리는 고급 시나리오에 대 한 hello 설치 개체의 특정 속성에만 toomodify 수 있는 부분 업데이트 기능이 있습니다. 기본적으로 부분 업데이트는 설치 개체에 대해 실행할 수 있는 JSON 패치 작업의 하위 집합입니다.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

설치 삭제:

    hub.deleteInstallation(installation.getInstallationId());

CreateOrUpdate, Patch 및 Delete의 최종 결과는 Get과 동일합니다. 방금 요청 된 작업 toohello 시스템 큐 hello 호출 동안 들어가고 백그라운드에서 실행 됩니다. Note 디버그 및 문제 해결을 위해에 대해서만 하지만 주 런타임 시나리오에 대 한 Get 설계 되지 않았습니다, hello 서비스에 의해 제한 밀접 하 게 됩니다.

등록에 대 한 설치에 대 한 송신 흐름 동일 hello 됩니다. 방금 옵션 tootarget 알림 toohello 도입 했습니다 특정 설치-사용할 태그 "InstallationId: {원하는 id}"입니다. 위 코드의 경우 이 태그가 포함된 형식은 다음과 같습니다.

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

여러 템플릿 중에서 하나 선택:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>알림 예약(표준 계층에 사용 가능)
일반 송신 같지만 하나 추가 매개 변수-알림 배달 되도록 라는 scheduledTime hello 동일 합니다. 서비스에서는 현재 시간 + 5분 및 현재 날짜 + 7일 사이의 모든 지정 시간을 사용할 수 있습니다.

**Windows 기본 알림 예약:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>가져오기/내보내기(표준 계층에 사용 가능)
경우에 따라 등록에 대해 필요한 tooperform 대량 작업입니다. 일반적으로 다른 시스템 또는는 대규모 수정 toosay 업데이트 hello 태그와 통합 됩니다. 수천 개의 등록에 대 한 논의 하 고 경우 Get/업데이트 흐름 toouse 하지 강력 하 게 좋습니다. 가져오기/내보내기 기능은 설계 된 toocover hello 시나리오입니다. 기본적으로 제공 하는 액세스 toosome blob 컨테이너 저장소 계정에서 들어오는 데이터 및 출력에 대 한 위치에 대 한 소스로 합니다.

**내보내기 작업 제출:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**가져오기 작업 제출:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**작업 완료 시까지 대기:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**모든 작업 가져오기:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**와 SAS 서명 URI:** 일부 blob 파일 또는 blob 컨테이너의 URL을 hello와 같은 사용 권한 및 만료 시간 매개 변수 집합과 계정의 SAS 키를 사용 하 여 이러한 모든 작업의 시그니처입니다. Azure 저장소 Java SDK에는 이러한 종류의 URI 만들기를 비롯하여 다양한 기능이 포함되어 있습니다. 간단한 대신 ImportExportE2E 서명 알고리즘의 기본 하 고 압축 구현에 (hello github 위치)에서 테스트 클래스에서 검토할 수 있습니다.

### <a name="send-notifications"></a>알림 보내기
hello 알림 개체는 헤더와 본문 단순히에 hello 기본 등록과 템플릿 알림을 개체 작성의 일부 유틸리티 메서드가 수 있습니다.

* **Windows 스토어 및 Windows Phone 8.1(비 Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Windows Phone 8.0 및 8.1 Silverlight**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **TooTags 보내기**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Tootag 식 보내기**       
  
        hub.sendNotification(n, "foo && ! bar");
* **템플릿 알림 보내기**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

이제 Java 코드를 실행하면 대상 장치에 나타나는 알림이 생성되어야 합니다.

## <a name="next-steps"></a>다음 단계
이 항목에서 소개 된 방법을 toocreate 간단한 Java REST 클라이언트 알림 허브에 대 한 합니다. 여기에서 다음을 할 수 있습니다.

* 전체 hello 다운로드 [Java SDK], hello 전체 SDK 코드가 포함 되어 있습니다. 
* Hello 샘플을 사용할:
  * [registerNativeWithDeviceToken]
  * [속보 보내기]
  * [지역화된 속보 보내기]
  * [Tooauthenticated 사용자 알림 보내기]
  * [Tooauthenticated 사용자 크로스 플랫폼 알림 보내기]

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[registerNativeWithDeviceToken]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[지역화된 속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Tooauthenticated 사용자 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Tooauthenticated 사용자 크로스 플랫폼 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

