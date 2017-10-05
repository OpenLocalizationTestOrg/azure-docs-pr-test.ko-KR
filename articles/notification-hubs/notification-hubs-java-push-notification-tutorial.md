---
title: "Java에서 알림 허브를 사용하는 방법"
description: "Java 백 엔드에서 Azure 알림 허브를 사용하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="3b533-103">Java에서 알림 허브를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="3b533-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="3b533-104">이 항목에서는 완전히 지원되는 새 공식 Azure 알림 허브 Java SDK의 주요 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="3b533-105">이 SDK는 오픈 소스 프로젝트이며 [Java SDK]에서 전체 SDK 코드를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="3b533-106">일반적으로는 MSDN 항목 [알림 허브 REST API](http://msdn.microsoft.com/library/dn223264.aspx)에서 설명하는 것처럼 알림 허브 REST 인터페이스를 사용하여 Java/PHP/Python/Ruby 백 엔드에서 모든 알림 허브 기능에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="3b533-107">이 Java SDK는 Java에서 이러한 REST 인터페이스에 대한 씬 래퍼를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="3b533-108">현재 SDK에 포함되어 있는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-108">The SDK supports currently:</span></span>

* <span data-ttu-id="3b533-109">알림 허브에 대한 CRUD</span><span class="sxs-lookup"><span data-stu-id="3b533-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="3b533-110">등록에 대한 CRUD</span><span class="sxs-lookup"><span data-stu-id="3b533-110">CRUD on Registrations</span></span>
* <span data-ttu-id="3b533-111">설치 관리</span><span class="sxs-lookup"><span data-stu-id="3b533-111">Installation Management</span></span>
* <span data-ttu-id="3b533-112">등록 가져오기/내보내기</span><span class="sxs-lookup"><span data-stu-id="3b533-112">Import/Export Registrations</span></span>
* <span data-ttu-id="3b533-113">일반 보내기</span><span class="sxs-lookup"><span data-stu-id="3b533-113">Regular Sends</span></span>
* <span data-ttu-id="3b533-114">예약된 보내기</span><span class="sxs-lookup"><span data-stu-id="3b533-114">Scheduled Sends</span></span>
* <span data-ttu-id="3b533-115">Java NIO를 통한 비동기 작업</span><span class="sxs-lookup"><span data-stu-id="3b533-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="3b533-116">지원되는 플랫폼: APNS(iOS), GCM(Android), WNS(Windows 스토어 앱), MPNS(Windows Phone), ADM(Amazon Kindle Fire), Baidu(Google 서비스가 포함되지 않은 Android)</span><span class="sxs-lookup"><span data-stu-id="3b533-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="3b533-117">SDK 사용</span><span class="sxs-lookup"><span data-stu-id="3b533-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="3b533-118">컴파일 및 빌드</span><span class="sxs-lookup"><span data-stu-id="3b533-118">Compile and build</span></span>
<span data-ttu-id="3b533-119">[Maven]</span><span class="sxs-lookup"><span data-stu-id="3b533-119">Use [Maven]</span></span>

<span data-ttu-id="3b533-120">빌드하려면 다음 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="3b533-121">코드</span><span class="sxs-lookup"><span data-stu-id="3b533-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="3b533-122">알림 허브 CRUD</span><span class="sxs-lookup"><span data-stu-id="3b533-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="3b533-123">**NamespaceManager 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="3b533-124">**알림 허브 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="3b533-125">또는</span><span class="sxs-lookup"><span data-stu-id="3b533-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="3b533-126">**알림 허브 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="3b533-127">**알림 허브 업데이트:**</span><span class="sxs-lookup"><span data-stu-id="3b533-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="3b533-128">**알림 허브 삭제:**</span><span class="sxs-lookup"><span data-stu-id="3b533-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="3b533-129">등록 CRUD</span><span class="sxs-lookup"><span data-stu-id="3b533-129">Registration CRUDs</span></span>
<span data-ttu-id="3b533-130">**알림 허브 클라이언트 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="3b533-131">**Windows 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="3b533-132">**iOS 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="3b533-133">마찬가지로 Android(GCM), Windows Phone(MPNS) 및 Kindle Fire(ADM)에 대한 등록도 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="3b533-134">**템플릿 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="3b533-135">**create registrationid + upsert 패턴을 사용하여 등록 만들기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="3b533-136">장치에 등록 ID를 저장하는 경우 응답 손실로 인한 중복 항목을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="3b533-137">**등록 업데이트:**</span><span class="sxs-lookup"><span data-stu-id="3b533-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="3b533-138">**등록 삭제:**</span><span class="sxs-lookup"><span data-stu-id="3b533-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="3b533-139">**등록 쿼리:**</span><span class="sxs-lookup"><span data-stu-id="3b533-139">**Query registrations:**</span></span>

* <span data-ttu-id="3b533-140">**단일 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="3b533-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="3b533-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="3b533-142">**허브에서 모든 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="3b533-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="3b533-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="3b533-144">**태그가 포함된 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="3b533-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="3b533-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="3b533-146">**채널별 등록 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="3b533-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="3b533-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="3b533-148">모든 컬렉션 쿼리는 $top 및 연속 토큰을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="3b533-149">설치 API 사용</span><span class="sxs-lookup"><span data-stu-id="3b533-149">Installation API usage</span></span>
<span data-ttu-id="3b533-150">설치 API는 등록 관리 대신 사용할 수 있는 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="3b533-151">올바르지 않거나 비효율적인 방식으로 수행하기 쉬운 중요한 등록을 여러 개 유지 관리하는 대신 이제는 단일 설치 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="3b533-152">이 경우 설치에는 푸시 채널(장치 토큰), 태그, 템플릿, 보조 타일(WNS 및 APNS의 경우) 등 필요한 모든 항목이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="3b533-153">더 이상 ID를 가져오기 위해 서비스를 호출할 필요가 없으며 GUID나 다른 식별자를 생성하여 장치에 저장한 다음 푸시 채널(장치 토큰)과 함께 백 엔드로 전송하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="3b533-154">백 엔드에서는 CreateOrUpdateInstallation만 단일 호출하면 됩니다. 이 호출은 완전 멱등 방식이므로 필요한 경우 다시 시도해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="3b533-155">Amazon Kindle Fire의 경우 이 호출은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="3b533-156">이 호출을 다음과 같이 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="3b533-157">고급 시나리오용으로 설치 개체의 특정 속성만 수정할 수 있는 부분 업데이트 기능도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="3b533-158">기본적으로 부분 업데이트는 설치 개체에 대해 실행할 수 있는 JSON 패치 작업의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="3b533-159">설치 삭제:</span><span class="sxs-lookup"><span data-stu-id="3b533-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="3b533-160">CreateOrUpdate, Patch 및 Delete의 최종 결과는 Get과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="3b533-161">요청한 작업은 호출 중에 시스템 큐로 전송되어 백그라운드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="3b533-162">Get은 기본 런타임 시나리오용이 아니며 디버그 및 문제 해결 전용이므로 서비스에서 엄격하게 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="3b533-163">설치의 전송 흐름은 등록에서도 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="3b533-164">특정 설치에만 알림을 보내려는 경우의 옵션으로는 "InstallationId:{desired-id}" 태그를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="3b533-165">위 코드의 경우 이 태그가 포함된 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="3b533-166">여러 템플릿 중에서 하나 선택:</span><span class="sxs-lookup"><span data-stu-id="3b533-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="3b533-167">알림 예약(표준 계층에 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="3b533-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="3b533-168">일반 전송과 같지만 알림을 배달해야 하는 시간을 지정하는 scheduledTime 매개 변수가 추가로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="3b533-169">서비스에서는 현재 시간 + 5분 및 현재 날짜 + 7일 사이의 모든 지정 시간을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="3b533-170">**Windows 기본 알림 예약:**</span><span class="sxs-lookup"><span data-stu-id="3b533-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="3b533-171">가져오기/내보내기(표준 계층에 사용 가능)</span><span class="sxs-lookup"><span data-stu-id="3b533-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="3b533-172">등록에 대해 대량 작업을 수행해야 하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="3b533-173">일반적으로는 다른 시스템과 통합할 때나 태그 업데이트 등의 대량 수정을 수행하는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="3b533-174">등록 수가 매우 많은 경우에는 Get/Update 흐름을 사용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="3b533-175">이러한 시나리오에서는 가져오기/내보내기 기능을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="3b533-176">기본적으로는 들어오는 데이터의 원본과 출력의 위치로 사용할 저장소 계정의 특정 Blob 컨테이너에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="3b533-177">**내보내기 작업 제출:**</span><span class="sxs-lookup"><span data-stu-id="3b533-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="3b533-178">**가져오기 작업 제출:**</span><span class="sxs-lookup"><span data-stu-id="3b533-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="3b533-179">**작업 완료 시까지 대기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="3b533-180">**모든 작업 가져오기:**</span><span class="sxs-lookup"><span data-stu-id="3b533-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="3b533-181">**SAS 서명이 포함된 URI:** 특정 Blob 파일이나 Blob 컨테이너의 URL에 사용 권한, 만료 시간 등의 매개 변수 집합과 계정 SAS 키를 사용하여 작성된 이러한 모든 항목의 서명이 결합된 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="3b533-182">Azure 저장소 Java SDK에는 이러한 종류의 URI 만들기를 비롯하여 다양한 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="3b533-183">작업을 간단하게 수행하려는 경우 github 위치에서 매우 기본적이고 간단한 서명 알고리즘 구현을 포함하는 ImportExportE2E 테스트 클래스를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="3b533-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="3b533-184">알림 보내기</span><span class="sxs-lookup"><span data-stu-id="3b533-184">Send Notifications</span></span>
<span data-ttu-id="3b533-185">알림 개체는 헤더, 네이티브 코드 작성 시 사용되는 몇 가지 유틸리티 메서드 및 템플릿 알림 개체를 포함하는 본문입니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="3b533-186">**Windows 스토어 및 Windows Phone 8.1(비 Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="3b533-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="3b533-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="3b533-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="3b533-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="3b533-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="3b533-189">**Windows Phone 8.0 및 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="3b533-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="3b533-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="3b533-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="3b533-191">**태그로 보내기**</span><span class="sxs-lookup"><span data-stu-id="3b533-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="3b533-192">**태그 식으로 보내기**</span><span class="sxs-lookup"><span data-stu-id="3b533-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="3b533-193">**템플릿 알림 보내기**</span><span class="sxs-lookup"><span data-stu-id="3b533-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="3b533-194">이제 Java 코드를 실행하면 대상 장치에 나타나는 알림이 생성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="3b533-195"><a name="next-steps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="3b533-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="3b533-196">이 항목에서는 알림 허브에 대한 단순한 Java REST 클라이언트를 만드는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="3b533-197">여기에서 다음을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-197">From here you can:</span></span>

* <span data-ttu-id="3b533-198">전체 SDK 코드가 포함된 전체 [Java SDK]를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="3b533-199">다음 샘플을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="3b533-199">Play with the samples:</span></span>
  * <span data-ttu-id="3b533-200">[알림 허브 시작]</span><span class="sxs-lookup"><span data-stu-id="3b533-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="3b533-201">[속보 보내기]</span><span class="sxs-lookup"><span data-stu-id="3b533-201">[Send breaking news]</span></span>
  * <span data-ttu-id="3b533-202">[지역화된 속보 보내기]</span><span class="sxs-lookup"><span data-stu-id="3b533-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="3b533-203">[인증된 사용자에게 알림 보내기]</span><span class="sxs-lookup"><span data-stu-id="3b533-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="3b533-204">[인증된 사용자에게 플랫폼 간 알림 보내기]</span><span class="sxs-lookup"><span data-stu-id="3b533-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="3b533-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="3b533-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="3b533-206">[알림 허브 시작]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="3b533-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="3b533-207">[속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="3b533-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="3b533-208">[지역화된 속보 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="3b533-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="3b533-209">[인증된 사용자에게 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="3b533-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="3b533-210">[인증된 사용자에게 플랫폼 간 알림 보내기]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="3b533-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="3b533-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="3b533-211">[Maven]: http://maven.apache.org/</span></span>

