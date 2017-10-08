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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="51e87-103">어떻게 toouse Java에서 알림 허브</span><span class="sxs-lookup"><span data-stu-id="51e87-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="51e87-104">이 항목에서는 hello 완벽 하 게 지원 hello 새 공식의 주요 기능 설명 Azure 알림 허브 Java SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="51e87-105">오픈 소스 프로젝트 이며 hello SDK 코드 전체에서 볼 수 있습니다 [Java SDK]합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="51e87-106">일반적으로 Java/PHP/Python/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 있습니다 hello MSDN 항목에 설명 된 대로 hello 알림 허브 REST 인터페이스를 사용 하 여 [알림 허브 REST Api](http://msdn.microsoft.com/library/dn223264.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="51e87-107">이 Java SDK는 Java에서 이러한 REST 인터페이스에 대한 씬 래퍼를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="51e87-108">hello SDK에서 지 원하는 현재:</span><span class="sxs-lookup"><span data-stu-id="51e87-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="51e87-109">알림 허브에 대한 CRUD</span><span class="sxs-lookup"><span data-stu-id="51e87-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="51e87-110">등록에 대한 CRUD</span><span class="sxs-lookup"><span data-stu-id="51e87-110">CRUD on Registrations</span></span>
* <span data-ttu-id="51e87-111">설치 관리</span><span class="sxs-lookup"><span data-stu-id="51e87-111">Installation Management</span></span>
* <span data-ttu-id="51e87-112">등록 가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="51e87-112">Import/Export Registrations</span></span>
* <span data-ttu-id="51e87-113">일반 보내기</span><span class="sxs-lookup"><span data-stu-id="51e87-113">Regular Sends</span></span>
* <span data-ttu-id="51e87-114">예약된 보내기</span><span class="sxs-lookup"><span data-stu-id="51e87-114">Scheduled Sends</span></span>
* <span data-ttu-id="51e87-115">Java NIO를 통한 비동기 작업</span><span class="sxs-lookup"><span data-stu-id="51e87-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="51e87-116">지원되는 플랫폼: APNS(iOS), GCM(Android), WNS(Windows 스토어 앱), MPNS(Windows Phone), ADM(Amazon Kindle Fire), Baidu(Google 서비스가 포함되지 않은 Android)</span><span class="sxs-lookup"><span data-stu-id="51e87-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="51e87-117">SDK 사용</span><span class="sxs-lookup"><span data-stu-id="51e87-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="51e87-118">컴파일 및 빌드</span><span class="sxs-lookup"><span data-stu-id="51e87-118">Compile and build</span></span>
<span data-ttu-id="51e87-119">[Maven]</span><span class="sxs-lookup"><span data-stu-id="51e87-119">Use [Maven]</span></span>

<span data-ttu-id="51e87-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="51e87-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="51e87-121">코드</span><span class="sxs-lookup"><span data-stu-id="51e87-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="51e87-122">알림 허브 CRUD</span><span class="sxs-lookup"><span data-stu-id="51e87-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="51e87-123">**NamespaceManager 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="51e87-124">**알림 허브 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="51e87-125">또는</span><span class="sxs-lookup"><span data-stu-id="51e87-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="51e87-126">**알림 허브 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="51e87-127">**알림 허브 업데이트:**</span><span class="sxs-lookup"><span data-stu-id="51e87-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="51e87-128">**알림 허브 삭제:**</span><span class="sxs-lookup"><span data-stu-id="51e87-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="51e87-129">등록 CRUD</span><span class="sxs-lookup"><span data-stu-id="51e87-129">Registration CRUDs</span></span>
<span data-ttu-id="51e87-130">**알림 허브 클라이언트 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="51e87-131">**Windows 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="51e87-132">**iOS 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="51e87-133">마찬가지로 Android(GCM), Windows Phone(MPNS) 및 Kindle Fire(ADM)에 대한 등록도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="51e87-134">**템플릿 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="51e87-135">**create registrationid + upsert 패턴을 사용하여 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="51e87-136">Hello 장치의 등록 id를 저장 하는 경우 분실 tooany 응답 인해 중복을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="51e87-137">**등록 업데이트:**</span><span class="sxs-lookup"><span data-stu-id="51e87-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="51e87-138">**등록 삭제:**</span><span class="sxs-lookup"><span data-stu-id="51e87-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="51e87-139">**등록 쿼리:**</span><span class="sxs-lookup"><span data-stu-id="51e87-139">**Query registrations:**</span></span>

* <span data-ttu-id="51e87-140">**단일 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="51e87-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="51e87-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="51e87-142">**허브에서 모든 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="51e87-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="51e87-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="51e87-144">**태그가 포함된 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="51e87-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="51e87-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="51e87-146">**채널별 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="51e87-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="51e87-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="51e87-148">모든 컬렉션 쿼리는 $top 및 연속 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="51e87-149">설치 API 사용</span><span class="sxs-lookup"><span data-stu-id="51e87-149">Installation API usage</span></span>
<span data-ttu-id="51e87-150">설치 API는 등록 관리 대신 사용할 수 있는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="51e87-151">Trivial 되지 않으며 잘못 또는 비효율적으로 쉽게 설정할 수 있는 여러 등록을 유지 하는 대신 이제를 가능한 toouse 단일 설치 개체.</span><span class="sxs-lookup"><span data-stu-id="51e87-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="51e87-152">이 경우 설치에는 푸시 채널(장치 토큰), 태그, 템플릿, 보조 타일(WNS 및 APNS의 경우) 등 필요한 모든 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="51e87-153">Toocall hello 서비스 tooget Id를 더 이상 필요 없는-방금 생성 GUID 또는 다른 식별자, 장치에 유지 및 tooyour 백 엔드 푸시 채널 (장치 토큰)와 함께 보내기.</span><span class="sxs-lookup"><span data-stu-id="51e87-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="51e87-154">Hello 백 엔드에만 수행 해야 한 번만 호출: 필요한 경우 무료 tooretry 바랍니다 CreateOrUpdateInstallation, 것은 완벽 하 게 idempotent입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="51e87-155">Amazon Kindle Fire의 경우 이 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="51e87-156">Tooupdate 하려는 경우 해당:</span><span class="sxs-lookup"><span data-stu-id="51e87-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="51e87-157">우리는 고급 시나리오에 대 한 hello 설치 개체의 특정 속성에만 toomodify 수 있는 부분 업데이트 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="51e87-158">기본적으로 부분 업데이트는 설치 개체에 대해 실행할 수 있는 JSON 패치 작업의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="51e87-159">설치 삭제:</span><span class="sxs-lookup"><span data-stu-id="51e87-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="51e87-160">CreateOrUpdate, Patch 및 Delete의 최종 결과는 Get과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="51e87-161">방금 요청 된 작업 toohello 시스템 큐 hello 호출 동안 들어가고 백그라운드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="51e87-162">Note 디버그 및 문제 해결을 위해에 대해서만 하지만 주 런타임 시나리오에 대 한 Get 설계 되지 않았습니다, hello 서비스에 의해 제한 밀접 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="51e87-163">등록에 대 한 설치에 대 한 송신 흐름 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="51e87-164">방금 옵션 tootarget 알림 toohello 도입 했습니다 특정 설치-사용할 태그 "InstallationId: {원하는 id}"입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="51e87-165">위 코드의 경우 이 태그가 포함된 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="51e87-166">여러 템플릿 중에서 하나 선택:</span><span class="sxs-lookup"><span data-stu-id="51e87-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="51e87-167">알림 예약(표준 계층에 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="51e87-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="51e87-168">일반 송신 같지만 하나 추가 매개 변수-알림 배달 되도록 라는 scheduledTime hello 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="51e87-169">서비스에서는 현재 시간 + 5분 및 현재 날짜 + 7일 사이의 모든 지정 시간을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="51e87-170">**Windows 기본 알림 예약:**</span><span class="sxs-lookup"><span data-stu-id="51e87-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="51e87-171">가져오기/내보내기(표준 계층에 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="51e87-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="51e87-172">경우에 따라 등록에 대해 필요한 tooperform 대량 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="51e87-173">일반적으로 다른 시스템 또는는 대규모 수정 toosay 업데이트 hello 태그와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="51e87-174">수천 개의 등록에 대 한 논의 하 고 경우 Get/업데이트 흐름 toouse 하지 강력 하 게 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="51e87-175">가져오기/내보내기 기능은 설계 된 toocover hello 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="51e87-176">기본적으로 제공 하는 액세스 toosome blob 컨테이너 저장소 계정에서 들어오는 데이터 및 출력에 대 한 위치에 대 한 소스로 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="51e87-177">**내보내기 작업 제출:**</span><span class="sxs-lookup"><span data-stu-id="51e87-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="51e87-178">**가져오기 작업 제출:**</span><span class="sxs-lookup"><span data-stu-id="51e87-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="51e87-179">**작업 완료 시까지 대기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="51e87-180">**모든 작업 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="51e87-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="51e87-181">**와 SAS 서명 URI:** 일부 blob 파일 또는 blob 컨테이너의 URL을 hello와 같은 사용 권한 및 만료 시간 매개 변수 집합과 계정의 SAS 키를 사용 하 여 이러한 모든 작업의 시그니처입니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="51e87-182">Azure 저장소 Java SDK에는 이러한 종류의 URI 만들기를 비롯하여 다양한 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="51e87-183">간단한 대신 ImportExportE2E 서명 알고리즘의 기본 하 고 압축 구현에 (hello github 위치)에서 테스트 클래스에서 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="51e87-184">알림 보내기</span><span class="sxs-lookup"><span data-stu-id="51e87-184">Send Notifications</span></span>
<span data-ttu-id="51e87-185">hello 알림 개체는 헤더와 본문 단순히에 hello 기본 등록과 템플릿 알림을 개체 작성의 일부 유틸리티 메서드가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="51e87-186">**Windows 스토어 및 Windows Phone 8.1(비 Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="51e87-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="51e87-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="51e87-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="51e87-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="51e87-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="51e87-189">**Windows Phone 8.0 및 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="51e87-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="51e87-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="51e87-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="51e87-191">**TooTags 보내기**</span><span class="sxs-lookup"><span data-stu-id="51e87-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="51e87-192">**Tootag 식 보내기**</span><span class="sxs-lookup"><span data-stu-id="51e87-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="51e87-193">**템플릿 알림 보내기**</span><span class="sxs-lookup"><span data-stu-id="51e87-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="51e87-194">이제 Java 코드를 실행하면 대상 장치에 나타나는 알림이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="51e87-195"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="51e87-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="51e87-196">이 항목에서 소개 된 방법을 toocreate 간단한 Java REST 클라이언트 알림 허브에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="51e87-197">여기에서 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-197">From here you can:</span></span>

* <span data-ttu-id="51e87-198">전체 hello 다운로드 [Java SDK], hello 전체 SDK 코드가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51e87-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="51e87-199">Hello 샘플을 사용할:</span><span class="sxs-lookup"><span data-stu-id="51e87-199">Play with hello samples:</span></span>
  * <span data-ttu-id="51e87-200">[registerNativeWithDeviceToken]</span><span class="sxs-lookup"><span data-stu-id="51e87-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="51e87-201">[속보 보내기]</span><span class="sxs-lookup"><span data-stu-id="51e87-201">[Send breaking news]</span></span>
  * <span data-ttu-id="51e87-202">[지역화된 속보 보내기]</span><span class="sxs-lookup"><span data-stu-id="51e87-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="51e87-203">[Tooauthenticated 사용자 알림 보내기]</span><span class="sxs-lookup"><span data-stu-id="51e87-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="51e87-204">[Tooauthenticated 사용자 크로스 플랫폼 알림 보내기]</span><span class="sxs-lookup"><span data-stu-id="51e87-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[registerNativeWithDeviceToken]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[지역화된 속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Tooauthenticated 사용자 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Tooauthenticated 사용자 크로스 플랫폼 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

