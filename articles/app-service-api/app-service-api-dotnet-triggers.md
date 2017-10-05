---
title: "App Service API 앱 트리거 | Microsoft Docs"
description: "Azure 앱 서비스의 API 앱에서 트리거 구현 방법"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="074cd-103">Azure 앱 서비스 API 앱 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="074cd-104">이 버전의 문서는 API 앱 2014-12-01-preview 스키마 버전에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="074cd-105">개요</span><span class="sxs-lookup"><span data-stu-id="074cd-105">Overview</span></span>
<span data-ttu-id="074cd-106">이 문서에서는 API 앱 트리거를 구현하고 논리 앱에서 이를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="074cd-107">[FileWatcher API 앱 코드 샘플](http://go.microsoft.com/fwlink/?LinkId=534802)에서 이 항목의 모든 코드 조각을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="074cd-108">이 문서의 코드를 빌드 및 실행하려면 nuget 패키지 [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/)를 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="074cd-109">API 앱 트리거 정의</span><span class="sxs-lookup"><span data-stu-id="074cd-109">What are API app triggers?</span></span>
<span data-ttu-id="074cd-110">일반적으로 API 앱은 API 앱 클라이언트가 이벤트에 대한 응답으로 적절한 조치를 취할 수 있도록 이벤트를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="074cd-111">이 시나리오를 지원하는 REST API 기반 메커니즘을 API 앱 트리거라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="074cd-112">예를 들어 클라이언트 코드에서 [Twitter Connector API 앱](../connectors/connectors-create-api-twitter.md) 을 사용하는 경우 코드는 특정 단어가 포함된 새 트윗을 기반으로 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="074cd-113">이 경우 밀어넣기 또는 끌어오기 트리거를 설정하면 용이할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="074cd-114">폴링 트리거와 밀어넣기 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="074cd-115">현재 다음 두 가지 유형의 트리거가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="074cd-116">폴링 트리거 - 클라이언트가 발생한 이벤트의 알림에 대해 API 앱을 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="074cd-117">밀어넣기 트리거 - 이벤트가 발생한 경우 API 앱에서 클라이언트로 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="074cd-118">폴링 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-118">Poll trigger</span></span>
<span data-ttu-id="074cd-119">폴링 트리거는 일반 REST API로 구현되며, 해당 클라이언트(예: 논리 앱)는 알림을 받기 위해 이를 폴링해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="074cd-120">클라이언트는 상태를 유지 관리할 수 있지만 폴링 트리거 자체는 상태 비저장입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="074cd-121">요청 및 응답 패킷에 대한 다음 정보는 폴링 트리거 계약의 몇 가지 주요 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="074cd-122">요청</span><span class="sxs-lookup"><span data-stu-id="074cd-122">Request</span></span>
  * <span data-ttu-id="074cd-123">HTTP 메서드: GET</span><span class="sxs-lookup"><span data-stu-id="074cd-123">HTTP method: GET</span></span>
  * <span data-ttu-id="074cd-124">매개 변수</span><span class="sxs-lookup"><span data-stu-id="074cd-124">Parameters</span></span>
    * <span data-ttu-id="074cd-125">triggerState - 이 선택적 매개 변수는 폴링 트리거가 지정된 상태를 기반으로 알림 반환 여부를 적절히 결정할 수 있도록 클라이언트가 해당 상태를 지정할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="074cd-126">API 관련 매개 변수</span><span class="sxs-lookup"><span data-stu-id="074cd-126">API-specific parameters</span></span>
* <span data-ttu-id="074cd-127">응답</span><span class="sxs-lookup"><span data-stu-id="074cd-127">Response</span></span>
  * <span data-ttu-id="074cd-128">상태 코드 **200** - 요청이 유효하며 트리거로부터의 알림이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="074cd-129">알림 내용이 응답 본문이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="074cd-130">응답의 "Retry-After" 헤더는 후속 요청 호출을 통해 추가 알림 데이터를 검색해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="074cd-131">상태 코드 **202** - 요청이 유효하지만 트리거로부터의 새 알림이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="074cd-132">상태 코드 **4xx** - 요청이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="074cd-133">클라이언트가 요청을 다시 시도할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="074cd-134">상태 코드 **5xx** - 요청 시 내부 서버 오류 및/또는 일시적인 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="074cd-135">클라이언트가 요청을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-135">The client should retry the request.</span></span>

<span data-ttu-id="074cd-136">다음 코드 조각은 폴링 트리거를 구현하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="074cd-137">이 폴링 트리거를 테스트하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="074cd-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="074cd-138">**공용(익명)**인증 설정으로 API 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="074cd-139">**touch** 작업을 호출하여 파일을 터치합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="074cd-140">다음 그림에서는 Postman을 통한 샘플 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="074cd-141">![Postman을 통해 Touch 작업 호출](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="074cd-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="074cd-142">2단계 이전의 타임스탬프로 설정된 **triggerState** 매개 변수 집합을 사용하여 폴링 트리거를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="074cd-143">다음 그림에서는 Postman을 통한 샘플 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="074cd-144">![Postman을 통해 폴링 트리거 호출](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="074cd-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="074cd-145">밀어넣기 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-145">Push trigger</span></span>
<span data-ttu-id="074cd-146">밀어넣기 트리거는 특정 이벤트가 발생하면 알림을 받도록 등록된 클라이언트로 알림을 푸시하는 일반 REST API로 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="074cd-147">요청 및 응답 패킷에 대한 다음 정보는 밀어넣기 트리거 계약의 몇 가지 주요 측면을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="074cd-148">요청</span><span class="sxs-lookup"><span data-stu-id="074cd-148">Request</span></span>
  * <span data-ttu-id="074cd-149">HTTP 메서드: PUT</span><span class="sxs-lookup"><span data-stu-id="074cd-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="074cd-150">매개 변수</span><span class="sxs-lookup"><span data-stu-id="074cd-150">Parameters</span></span>
    * <span data-ttu-id="074cd-151">triggerId: 필수 - 밀어넣기 트리거의 등록을 나타내는 불투명 문자열(예: GUID)입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="074cd-152">callbackUrl: 필수 - 이벤트가 발생하면 호출할 콜백의 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="074cd-153">호출은 간단한 POST HTTP 호출입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="074cd-154">API 관련 매개 변수</span><span class="sxs-lookup"><span data-stu-id="074cd-154">API-specific parameters</span></span>
* <span data-ttu-id="074cd-155">응답</span><span class="sxs-lookup"><span data-stu-id="074cd-155">Response</span></span>
  * <span data-ttu-id="074cd-156">상태 코드 **200** - 클라이언트 등록 요청에 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="074cd-157">상태 코드 **4xx** - 요청이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="074cd-158">클라이언트가 요청을 다시 시도할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="074cd-159">상태 코드 **5xx** - 요청 시 내부 서버 오류 및/또는 일시적인 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="074cd-160">클라이언트가 요청을 다시 시도해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-160">The client should retry the request.</span></span>
* <span data-ttu-id="074cd-161">콜백</span><span class="sxs-lookup"><span data-stu-id="074cd-161">Callback</span></span>
  * <span data-ttu-id="074cd-162">HTTP 메서드: POST</span><span class="sxs-lookup"><span data-stu-id="074cd-162">HTTP method: POST</span></span>
  * <span data-ttu-id="074cd-163">요청 본문: 알림 내용</span><span class="sxs-lookup"><span data-stu-id="074cd-163">Request body: Notification content.</span></span>

<span data-ttu-id="074cd-164">다음 코드 조각은 밀어넣기 트리거를 구현하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="074cd-165">이 폴링 트리거를 테스트하려면 다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="074cd-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="074cd-166">**공용(익명)**인증 설정으로 API 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="074cd-167">[http://requestb.in/](http://requestb.in/) 을 찾아서 콜백 URL로 사용할 RequestBin을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="074cd-168">**triggerId**를 GUID로 사용하고 **callbackUrl**을 RequestBin URL로 사용하여 밀어넣기 트리거를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="074cd-169">![Postman을 통해 밀어넣기 트리거 호출](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="074cd-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="074cd-170">**touch** 작업을 호출하여 파일을 터치합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="074cd-171">다음 그림에서는 Postman을 통한 샘플 요청을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="074cd-172">![Postman을 통해 Touch 작업 호출](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="074cd-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="074cd-173">RequestBin을 검사하여 밀어넣기 트리거 콜백이 속성 출력으로 호출되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="074cd-174">![Postman을 통해 폴링 트리거 호출](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="074cd-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="074cd-175">API 정의에서 트리거 설명</span><span class="sxs-lookup"><span data-stu-id="074cd-175">Describe triggers in API definition</span></span>
<span data-ttu-id="074cd-176">트리거를 구현하고 API 앱을 Azure에 배포한 후에는 Azure Preview 포털에서 **API 정의** 블레이드로 이동하여 API 앱의 Swagger 2.0 API 정의로 구동되는 UI에서 트리거가 자동으로 인식되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![API 정의 블레이드](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="074cd-178">**Swagger 다운로드** 단추를 클릭하고 JSON 파일을 열면 다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="074cd-179">확장 속성 **x-ms-schedular-trigger** 는 API 정의에서 트리거를 설명하는 방식이며, 게이트웨이 통해 API 정의를 요청할 때 다음 조건 중 하나에 해당하는 경우 API 앱 게이트웨이에 의해 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="074cd-180">이 속성을 수동으로 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="074cd-181">폴링 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-181">Poll trigger</span></span>
  * <span data-ttu-id="074cd-182">HTTP 메서드가 **GET**인 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="074cd-183">**operationId** 속성에 문자열 **trigger**가 포함된 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="074cd-184">**parameters** 속성에 **name** 속성이 **triggerState**로 설정된 매개 변수가 포함된 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="074cd-185">밀어넣기 트리거</span><span class="sxs-lookup"><span data-stu-id="074cd-185">Push trigger</span></span>
  * <span data-ttu-id="074cd-186">HTTP 메서드가 **PUT**인 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="074cd-187">**operationId** 속성에 문자열 **trigger**가 포함된 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="074cd-188">**parameters** 속성에 **name** 속성이 **triggerId**로 설정된 매개 변수가 포함된 경우</span><span class="sxs-lookup"><span data-stu-id="074cd-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="074cd-189">논리 앱에서 API 앱 트리거 사용</span><span class="sxs-lookup"><span data-stu-id="074cd-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="074cd-190">논리 앱 디자이너에서 API 앱 트리거 나열 및 구성</span><span class="sxs-lookup"><span data-stu-id="074cd-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="074cd-191">API 앱과 동일한 리소스 그룹에서 논리 앱을 만든 경우 클릭 작업만으로 디자이너 캔버스에 간단히 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="074cd-192">다음 그림에서는 이 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-192">The following images illustrate this:</span></span>

![논리 앱 디자이너의 트리거](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![논리 앱 디자이너에서 폴링 트리거 구성](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![논리 앱 디자이너에서 밀어넣기 트리거 구성](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="074cd-196">논리 앱에 맞게 API 앱 트리거 최적화</span><span class="sxs-lookup"><span data-stu-id="074cd-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="074cd-197">API 앱에 트리거를 추가한 후에는 몇 가지 작업을 통해 논리 앱에서 API 앱을 사용할 때 환경을 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="074cd-198">예를 들어 논리 앱에서 폴링 트리거의 **triggerState** 매개 변수를 다음 식으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="074cd-199">이 식은 논리 앱의 마지막 트리거 호출을 평가하여 해당 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="074cd-200">참고: 위 식에서 사용된 함수에 대한 설명은 [논리 앱 워크플로 정의 언어](https://msdn.microsoft.com/library/azure/dn948512.aspx)의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="074cd-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="074cd-201">논리 앱 사용자는 트리거를 사용하는 동안 위 식을 **triggerState** 매개 변수로 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="074cd-202">확장 속성 **x-ms-scheduler-recommendation**을 통해 논리 앱 디자이너가 이 값을 미리 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="074cd-203">매개 변수 자체가 디자이너에 표시되지 않도록 **x-ms-visibility** 확장 속성을 *internal* 값으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="074cd-204">다음 코드에서는 이러한 설정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="074cd-205">밀어넣기 트리거의 경우 **triggerId** 매개 변수는 논리 앱을 고유하게 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="074cd-206">다음 식을 사용하여 이 속성을 워크플로 이름으로 설정하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="074cd-207">해당 API 정의에서 **x-ms-scheduler-recommendation** 및 **x-ms-visibility** 확장 속성을 사용하면 API 앱이 논리 앱 디자이너로 전달하여 사용자를 위해 이 식을 자동으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="074cd-208">API 정의에서 확장 속성 추가</span><span class="sxs-lookup"><span data-stu-id="074cd-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="074cd-209">**x-ms-scheduler-recommendation** 및 **x-ms-visibility** 확장 속성과 같은 추가 메타데이터 정보를 정적 또는 동적으로 API 정의에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="074cd-210">정적 메타데이터의 경우 프로젝트에서 직접 */metadata/apiDefinition.swagger.json* 파일을 편집하고 속성을 수동으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="074cd-211">동적 메타데이터를 사용하는 API 앱의 경우 SwaggerConfig.cs 파일을 편집하여 이러한 확장을 추가할 수 있는 작업 필터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="074cd-212">다음은 동적 메타데이터 시나리오를 용이하게 하기 위해 이 클래스를 구현할 수 있는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="074cd-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
