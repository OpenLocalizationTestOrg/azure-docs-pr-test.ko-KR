---
title: "Visual Studio에서 Azure 코드 aaaOptimizing | Microsoft Docs"
description: "Visual Studio에서 Azure 코드 최적화 도구를 사용하여 더욱 강력하고 성능이 뛰어난 코드를 만드는 방법에 대해 알아보세요."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="27417-103">Azure 코드 최적화</span><span class="sxs-lookup"><span data-stu-id="27417-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="27417-104">Microsoft Azure를 사용 하는 앱을 프로그래밍할 때의 앱 확장성, 동작 및 클라우드 환경에서 성능 문제를 방지 하는 일부 코딩 방법을 toohelp 따라야 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="27417-105">Microsoft는 이와 같이 자주 발생하는 문제를 인식 및 식별하고 해결해 주는 Azure 코드 분석 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="27417-106">NuGet 통해 Visual Studio의 hello 도구를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="27417-107">Azure 코드 분석 규칙</span><span class="sxs-lookup"><span data-stu-id="27417-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="27417-108">hello Azure 코드 분석 도구 규칙 tooautomatically 플래그입니다. Azure 코드 성능에 영향을 주는 알려진된 문제를 발견 하면 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="27417-109">감지된 문제는 경고 또는 컴파일러 오류로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="27417-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="27417-110">코드 수정 또는 제안 사항은 tooresolve hello 경고 또는 오류가 종종 전구 아이콘을 통해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="27417-111">기본(In-Process) 세션 상태 모드 방지</span><span class="sxs-lookup"><span data-stu-id="27417-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="27417-112">ID</span><span class="sxs-lookup"><span data-stu-id="27417-112">ID</span></span>
<span data-ttu-id="27417-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="27417-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="27417-114">설명</span><span class="sxs-lookup"><span data-stu-id="27417-114">Description</span></span>
<span data-ttu-id="27417-115">클라우드 응용 프로그램에 대 한 hello 기본 (in-process) 세션 상태 모드를 사용 하는 경우 세션 상태를 잃을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="27417-116">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-117">이유</span><span class="sxs-lookup"><span data-stu-id="27417-117">Reason</span></span>
<span data-ttu-id="27417-118">기본적으로 hello 세션 상태 모드 hello web.config 파일에 지정 된 프로세스에는 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="27417-119">또한 경우 hello 구성 파일에 지정 된 항목이, hello 세션 상태 모드 tooin 프로세스 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="27417-120">hello in-process 모드 hello 웹 서버의 메모리에 세션 상태를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="27417-121">인스턴스를 다시 시작 또는 새 인스턴스를 부하 분산 또는 장애 조치 지원을 사용 되는 경우에 hello 웹 서버의 메모리에 저장 된 hello 세션 상태가 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="27417-122">이러한 상황을 확장할 hello 클라우드 hello 응용 프로그램을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="27417-123">ASP.NET 세션 상태는 세션 상태 데이터에 대해 다양한 저장소 옵션(InProc, StateServer, SQLServer, 사용자 지정, 해제)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="27417-124">사용 하는 사용자 지정 모드 toohost 데이터에 대해 외부 세션 상태 저장소와 같은 것이 좋습니다. [Redis 용 Azure 세션 상태 공급자](http://go.microsoft.com/fwlink/?LinkId=401521)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="27417-125">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-125">Solution</span></span>
<span data-ttu-id="27417-126">하나의 권장된 솔루션은 관리 캐시 서비스에서 toostore 세션 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="27417-127">자세한 내용은 방법 toouse [Redis 용 Azure 세션 상태 공급자](http://go.microsoft.com/fwlink/?LinkId=401521) toostore 세션 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="27417-128">또한 저장소 세션 명시할 수 다른 장소 tooensure에 hello 클라우드에서 응용 프로그램은 확장 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="27417-129">toolearn 읽으십시오 대체 솔루션에 대 한 자세한 [세션 상태 모드](https://msdn.microsoft.com/library/ms178586)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="27417-130">실행 메서드는 비동기가 아니어야 함</span><span class="sxs-lookup"><span data-stu-id="27417-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="27417-131">ID</span><span class="sxs-lookup"><span data-stu-id="27417-131">ID</span></span>
<span data-ttu-id="27417-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="27417-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="27417-133">설명</span><span class="sxs-lookup"><span data-stu-id="27417-133">Description</span></span>
<span data-ttu-id="27417-134">비동기 메서드를 만듭니다 (같은 [await](https://msdn.microsoft.com/library/hh156528.aspx)) hello 외부 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드 및에서 hello 비동기 메서드를 호출 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="27417-135">Hello 선언 [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 비동기 메서드로 인해 hello 작업자 역할 tooenter 다시 시작 루프입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="27417-136">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-137">이유</span><span class="sxs-lookup"><span data-stu-id="27417-137">Reason</span></span>
<span data-ttu-id="27417-138">Hello 내에서 비동기 메서드 호출 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드를 사용 하면 hello 클라우드 서비스 런타임 toorecycle hello 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="27417-139">모든 프로그램 실행은 hello 내에서 수행 작업자 역할이 시작 될 때 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="27417-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="27417-140">기존 hello [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드로 인해 hello 작업자 역할 toorestart 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="27417-141">Hello 작업자 역할 런타임이 비동기 메서드에 hello에 도달 hello 비동기 메서드의 한 후 모든 작업을 디스패치 하 고 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="27417-142">이 인해 hello 작업자 역할 tooexit hello에서 [ [ [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드 및 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="27417-143">실행의 다음 반복 hello에서에서 hello 작업자 역할에는 hello 비동기 메서드를 다시 및 장치 재시작을 일으키는 hello 작업자 역할 toorecycle도 다시 적중 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-144">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-144">Solution</span></span>
<span data-ttu-id="27417-145">Hello 이외의 모든 비동기 작업을 배치 [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 메서드.</span><span class="sxs-lookup"><span data-stu-id="27417-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="27417-146">그런 다음에서 리팩터링 hello 비동기 메서드를 호출 hello 내 [ [run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) RunAsync ().wait 등의 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="27417-147">hello Azure 코드 분석 도구입니다.이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="27417-148">다음 코드 조각 hello hello 코드이 문제 해결을 위해이 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27417-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="27417-149">서비스 버스 공유 액세스 서명 인증 사용</span><span class="sxs-lookup"><span data-stu-id="27417-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="27417-150">ID</span><span class="sxs-lookup"><span data-stu-id="27417-150">ID</span></span>
<span data-ttu-id="27417-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="27417-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="27417-152">설명</span><span class="sxs-lookup"><span data-stu-id="27417-152">Description</span></span>
<span data-ttu-id="27417-153">인증에 SAS(공유 액세스 서명)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="27417-154">서비스 버스 인증에 ACS(액세스 제어 서비스)를 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="27417-155">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-156">이유</span><span class="sxs-lookup"><span data-stu-id="27417-156">Reason</span></span>
<span data-ttu-id="27417-157">보안 강화를 위해 Azure Active Directory에서 ACS 인증을 SAS 인증으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="27417-158">참조 [Azure Active Directory ACS의 향후 hello는](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) hello 전환 계획에 대 한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-159">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-159">Solution</span></span>
<span data-ttu-id="27417-160">앱에 SAS 인증을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="27417-161">다음 예제는 hello 네임 스페이스 또는 엔터티에 toouse는 기존 SAS 토큰 tooaccess 서비스 버스 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27417-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="27417-162">다음 항목에 대 한 자세한 내용은 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="27417-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="27417-163">개요를 보려면 [서비스 버스를 사용한 공유 액세스 서명 인증](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="27417-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="27417-164">어떻게 toouse 서비스 버스를 통해 공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="27417-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="27417-165">샘플 프로젝트를 보려면 [서비스 버스를 사용한 SAS(공유 액세스 서명) 인증 사용](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="27417-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="27417-166">"수신 루프" OnMessage 메서드 tooavoid를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="27417-167">ID</span><span class="sxs-lookup"><span data-stu-id="27417-167">ID</span></span>
<span data-ttu-id="27417-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="27417-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="27417-169">설명</span><span class="sxs-lookup"><span data-stu-id="27417-169">Description</span></span>
<span data-ttu-id="27417-170">"수신 루프"으로 옮기기 tooavoid 호출 hello **OnMessage** 메서드는 호출 hello 보다 메시지를 받기 위한 더 나은 솔루션 **수신** 메서드.</span><span class="sxs-lookup"><span data-stu-id="27417-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="27417-171">그러나 hello를 사용 해야 할 경우 **수신** 메서드를 기본이 아닌 서버 대기 시간을 지정 hello 서버 대기 시간은 1 분 이상 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="27417-172">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-173">이유</span><span class="sxs-lookup"><span data-stu-id="27417-173">Reason</span></span>
<span data-ttu-id="27417-174">호출할 때 **OnMessage**, hello 클라이언트 hello 큐 또는 구독을 지속적으로 폴링하는 내부 메시지 펌프를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="27417-175">이 메시지 펌프 tooreceive 메시지 호출을 실행 하는 무한 루프가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="27417-176">Hello 호출 시간이 초과 되 면 새 호출이 발급 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="27417-177">hello 제한 시간 간격의 hello hello 값에 의해 결정 됩니다 [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) hello 속성 [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)사용 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="27417-178">사용 시의 이점은 hello **OnMessage** 너무 비교**수신** 가 메시지에 대 한 폴링, 예외 처리, 병렬로 여러 메시지를 처리 및 hello 완료 toomanually을 갖지 못하도록은 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="27417-179">호출 하는 경우 **수신** 기본값을 사용 하지 않고도 수 있는지 hello *ServerWaitTime* 값은 1 분 보다 길어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="27417-180">설정 *ServerWaitTime* 1 분 보다 toomore hello 메시지가 완전히 수신 되기 전에 초과 hello 서버를 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-181">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-181">Solution</span></span>
<span data-ttu-id="27417-182">권장된 사용법에 대 한 코드 예제를 따르는 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="27417-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="27417-183">자세한 내용은 [QueueClient.OnMessage 메서드(Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) 및 [QueueClient.Receive 메서드(Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="27417-184">hello Azure 메시징 인프라의 tooimprove hello 성능 디자인 패턴 hello 참조 [비동기 메시징 입문서](https://msdn.microsoft.com/library/dn589781.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="27417-185">hello 다음은 사용 하는 예제 **OnMessage** tooreceive 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="27417-186">hello 다음은 사용 하는 예제 **수신** hello 기본 서버와 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="27417-187">hello 다음은 사용 하는 예제 **수신** 기본이 아닌 서버 대기 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="27417-188">비동기 서비스 버스 메서드 사용 고려</span><span class="sxs-lookup"><span data-stu-id="27417-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="27417-189">ID</span><span class="sxs-lookup"><span data-stu-id="27417-189">ID</span></span>
<span data-ttu-id="27417-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="27417-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="27417-191">설명</span><span class="sxs-lookup"><span data-stu-id="27417-191">Description</span></span>
<span data-ttu-id="27417-192">비동기 서비스 버스 메서드 tooimprove 성능 조정 된 메시징을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="27417-193">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-194">이유</span><span class="sxs-lookup"><span data-stu-id="27417-194">Reason</span></span>
<span data-ttu-id="27417-195">비동기 메서드를 사용 하 여 hello 주 스레드를 차단 하지 않는 각 호출을 실행 하기 때문에 응용 프로그램 동시성이 보장을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="27417-196">서비스 버스 메시징 메서드를 사용할 때 작업(보내기, 받기, 삭제 등)을 수행하면 다소 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="27417-197">이 시간 hello 요청과 hello 회신의 추가 toohello 대기 시간에 서비스 버스 서비스 hello 하 여 hello hello 작업 처리를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="27417-198">시간당 작업 tooincrease hello 번호 작업이 동시에 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="27417-199">자세한 내용은 참조 하십시오 너무[성능 향상을 사용 하 여 서비스 버스 조정 된 메시징에 대 한 유용한](https://msdn.microsoft.com/library/azure/hh528527.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="27417-200">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-200">Solution</span></span>
<span data-ttu-id="27417-201">참조 [QueueClient 클래스 (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) toouse hello 비동기 메서드를 권장 하는 방법에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="27417-202">hello Azure 메시징 인프라의 tooimprove hello 성능 디자인 패턴 hello 참조 [비동기 메시징 입문서](https://msdn.microsoft.com/library/dn589781.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="27417-203">서비스 버스 큐 및 토픽 분할 고려</span><span class="sxs-lookup"><span data-stu-id="27417-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="27417-204">ID</span><span class="sxs-lookup"><span data-stu-id="27417-204">ID</span></span>
<span data-ttu-id="27417-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="27417-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="27417-206">설명</span><span class="sxs-lookup"><span data-stu-id="27417-206">Description</span></span>
<span data-ttu-id="27417-207">서비스 버스 메시징에서 성능을 향상하려면 서비스 버스 큐와 토픽을 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="27417-208">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-209">이유</span><span class="sxs-lookup"><span data-stu-id="27417-209">Reason</span></span>
<span data-ttu-id="27417-210">서비스 버스 큐 및 항목 분할 제한 되기 때문에 hello 분할 된 큐 또는 항목의 전체 처리량은 더 이상 단일 메시지 브로커 또는 메시징 저장소의 hello 성능으로 성능 처리량 및 서비스 가용성이 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="27417-211">또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 토픽을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="27417-212">자세한 내용은 [메시징 엔터티 분할](https://msdn.microsoft.com/library/azure/dn520246.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="27417-213">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-213">Solution</span></span>
<span data-ttu-id="27417-214">어떻게 코드 조각에 나와 있는 다음 hello toopartition 메시징 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="27417-215">자세한 내용은 참조 [분할 서비스 버스 큐 및 항목 | Microsoft Azure 블로그](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) 하 고 체크 아웃 hello [Microsoft Azure 서비스 버스 분할 된 큐](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) 샘플.</span><span class="sxs-lookup"><span data-stu-id="27417-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="27417-216">SharedAccessStartTime을 설정하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="27417-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="27417-217">ID</span><span class="sxs-lookup"><span data-stu-id="27417-217">ID</span></span>
<span data-ttu-id="27417-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="27417-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="27417-219">설명</span><span class="sxs-lookup"><span data-stu-id="27417-219">Description</span></span>
<span data-ttu-id="27417-220">SharedAccessStartTimeset toohello tooimmediately hello 공유 액세스 정책을 시작 하는 현재 시간을 사용 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="27417-221">필요할 때만 tooset이이 속성 toostart hello 공유 액세스 정책을 나중에 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="27417-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="27417-222">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-223">이유</span><span class="sxs-lookup"><span data-stu-id="27417-223">Reason</span></span>
<span data-ttu-id="27417-224">클록 동기화는 데이터 센터 간 약간의 시간 차이를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="27417-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="27417-225">예를 들어 논리적으로 겠 설정을 hello 시작 시간의 저장소 SAS 정책의 hello DateTime.Now 또는 비슷한 메서드를 사용 하 여 현재 시간 하면 hello SAS 정책 tootake 효과 즉시으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="27417-226">그러나 데이터 센터 간에 시간이 약간씩 차이점 hello 일부 데이터 센터 시간이 조금 늦은 hello 시작 시간 보다 이후 될 수에 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="27417-227">신속 하 게 (또는 심지어 즉시) hello 정책 SAS 만료 될 수 있습니다 결과적으로, hello 정책 수명을 너무 짧게 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="27417-228">Azure 저장소에서 공유 액세스 서명을 사용 하 여에 대 한 자세한 지침을 참조 하십시오. [소개 테이블 SAS (공유 액세스 서명), 큐 SAS 및 업데이트 tooBlob SAS-Microsoft Azure 저장소 팀 블로그-사이트 홈-MSDN 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="27417-229">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-229">Solution</span></span>
<span data-ttu-id="27417-230">Hello 공유 액세스 정책의 hello 시작 시간을 설정 하는 hello 문을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="27417-231">hello Azure 코드 분석 도구는이 문제에 대 한 수정 프로그램을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="27417-232">보안 관리에 대 한 자세한 내용은 디자인 패턴 hello를 참조 하십시오 [Valet 키 패턴](https://msdn.microsoft.com/library/dn568102.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="27417-233">다음 코드 조각 hello이이 문제에 대 한 hello 코드 수정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27417-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="27417-234">공유 액세스 정책 만료 시간은 5분을 초과해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="27417-235">ID</span><span class="sxs-lookup"><span data-stu-id="27417-235">ID</span></span>
<span data-ttu-id="27417-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="27417-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="27417-237">설명</span><span class="sxs-lookup"><span data-stu-id="27417-237">Description</span></span>
<span data-ttu-id="27417-238">시계 "클록 스큐입니다." 이라는 tooa 조건 인해 서로 다른 위치에 있는 데이터 센터 간에 최대 5 분의 시간 차이 만큼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="27417-239">tooprevent hello SAS 정책 토큰이 만료 되는 작업이 계획 hello 만료 시간 toobe 5 분 이상 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="27417-240">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-241">이유</span><span class="sxs-lookup"><span data-stu-id="27417-241">Reason</span></span>
<span data-ttu-id="27417-242">Hello 전 세계 서로 다른 위치에 있는 데이터 센터는 클록 신호 여 동기화합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="27417-243">클록 신호 tootravel toodifferent 위치에 대 한 시간을 사용 하기 때문에 있을 수 있습니다 서로 다른 지리적 위치에 있는 데이터 센터 간에 시간 차이가 모든 항목이 동기화 된다고 있지만.</span><span class="sxs-lookup"><span data-stu-id="27417-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="27417-244">이 시간 차이 hello는 공유 액세스 정책 시작 시간 및 만료 간격에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="27417-245">따라서 tooensure 공유 액세스 정책을 즉시 적용, hello 시작 시간은 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="27417-246">또한 hello 만료 시간에는 5 분 tooprevent 초기 제한 시간 보다 더 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="27417-247">Azure 저장소에서 공유 액세스 서명을 사용 하는 방법에 대 한 자세한 내용은 참조 [소개 테이블 SAS (공유 액세스 서명), 큐 SAS 및 업데이트 tooBlob SAS-Microsoft Azure 저장소 팀 블로그-사이트 홈-MSDN 블로그](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="27417-248">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-248">Solution</span></span>
<span data-ttu-id="27417-249">보안 관리에 대 한 자세한 내용은 hello 디자인 패턴을 참조 하십시오. [Valet 키 패턴](https://msdn.microsoft.com/library/dn568102.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="27417-250">hello 다음은 공유 액세스 정책 시작 시간을 지정 하지 않는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="27417-251">hello 다음은 정책 만료 기간이 5 분 보다 큰 공유 액세스 정책 시작 시간을 지정 하는 예로입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="27417-252">자세한 내용은 [공유 액세스 서명 만들기 및 사용](https://msdn.microsoft.com/library/azure/jj721951.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="27417-253">CloudConfigurationManager 사용</span><span class="sxs-lookup"><span data-stu-id="27417-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="27417-254">ID</span><span class="sxs-lookup"><span data-stu-id="27417-254">ID</span></span>
<span data-ttu-id="27417-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="27417-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="27417-256">설명</span><span class="sxs-lookup"><span data-stu-id="27417-256">Description</span></span>
<span data-ttu-id="27417-257">Hello를 사용 하 여 [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) Azure 웹 사이트와 Azure 모바일 서비스에 런타임 문제가 발생 하지 않습니다와 같은 프로젝트에 대 한 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="27417-258">그러나 모범 사례로, 것이 좋습니다 toouse 클라우드[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) 모든 Azure 클라우드 응용 프로그램에 대 한 구성을 관리 하는 단일화 된 방법을으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="27417-259">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-260">이유</span><span class="sxs-lookup"><span data-stu-id="27417-260">Reason</span></span>
<span data-ttu-id="27417-261">CloudConfigurationManager는 hello 구성 파일의 적절 한 toohello 응용 프로그램 환경을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="27417-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="27417-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="27417-263">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-263">Solution</span></span>
<span data-ttu-id="27417-264">리팩터링 코드 toouse hello [CloudConfigurationManager 클래스](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="27417-265">이 문제에 대 한 코드 수정 hello Azure 코드 분석 도구에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="27417-266">다음 코드 조각 hello이이 문제에 대 한 hello 코드 수정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27417-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="27417-267">Replace</span><span class="sxs-lookup"><span data-stu-id="27417-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="27417-268">다음으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="27417-269">어떻게 toostore hello App.config 또는 Web.config 파일에서 구성 설정의 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="27417-270">Hello 구성 파일의 hello 설정 toohello appSettings 섹션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="27417-271">hello 다음은 이전 코드 예제의 hello에 대 한 hello Web.config 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="27417-272">하드 코드된 연결 문자열을 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="27417-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="27417-273">ID</span><span class="sxs-lookup"><span data-stu-id="27417-273">ID</span></span>
<span data-ttu-id="27417-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="27417-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="27417-275">설명</span><span class="sxs-lookup"><span data-stu-id="27417-275">Description</span></span>
<span data-ttu-id="27417-276">하드 코드 된 연결 문자열을 사용 하 고 필요한 tooupdate toomake 변경 tooyour 소스 코드가 있는 hello 응용 프로그램을 다시 컴파일해야 하는 나중에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="27417-277">그러나 구성 파일에서 연결 문자열을 저장 하는 경우 변경할 수 있습니다에 나중에 간단히 hello 구성 파일을 업데이트 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="27417-278">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-279">이유</span><span class="sxs-lookup"><span data-stu-id="27417-279">Reason</span></span>
<span data-ttu-id="27417-280">하드 코딩 연결 문자열은 연결 문자열 toobe 신속 하 게 변경 해야 하는 경우 문제를 유발 하기 때문에 좋지 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="27417-281">또한 hello 프로젝트 체크 인 toosource 컨트롤 toobe를 필요한 경우 하드 코드 된 연결 문자열 있으므로 보안이 취약해를 집니다 hello 문자열 hello 소스 코드에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-282">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-282">Solution</span></span>
<span data-ttu-id="27417-283">Hello 구성 파일 또는 Azure 환경에 연결 문자열을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="27417-284">독립 실행형 응용 프로그램에 대 한 app.config toostore 연결 문자열 설정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="27417-285">IIS에서 호스트 웹 응용 프로그램에 대 한 web.config toostore 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="27417-286">ASP.NET vNext 응용 프로그램의 경우 configuration.json toostore 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="27417-287">web.config 또는 app.config와 같은 구성 파일을 사용하는 방법은 [ASP.NET 웹 구성 지침](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="27417-288">Azure 환경 변수의 작동 방식에 대해서는 [Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="27417-289">연결 문자열을 소스 제어에 저장하는 방법에 대한 자세한 내용은 [연결 문자열과 같은 민감한 정보를 소스 코드 리포지토리에 저장된 파일에 두지 않는 방식](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="27417-290">진단 구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="27417-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="27417-291">ID</span><span class="sxs-lookup"><span data-stu-id="27417-291">ID</span></span>
<span data-ttu-id="27417-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="27417-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="27417-293">설명</span><span class="sxs-lookup"><span data-stu-id="27417-293">Description</span></span>
<span data-ttu-id="27417-294">Hello Microsoft.WindowsAzure.Diagnostics 프로그래밍 API를 사용 하 여과 같은 코드에서 진단 설정을 구성 하는 대신, hello diagnostics.wadcfg 파일의 진단 설정을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="27417-295">Azure SDK 2.5를 사용하는 경우에는 diagnostics.wadcfgx를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="27417-296">이 통해 코드 toorecompile 필요 없이 진단 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="27417-297">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-298">이유</span><span class="sxs-lookup"><span data-stu-id="27417-298">Reason</span></span>
<span data-ttu-id="27417-299">먼저 여러 가지 방법을 사용 하 여 WAD (Azure 진단), Azure SDK 2.5 (사용 하 여 Azure 진단 1.3)를 구성할 수 없습니다: 추가 toohello 구성 blob 저장소의 명령적 코드, 선언 구성 또는 hello default를 사용 하 여 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="27417-300">그러나 hello 방식으로 tooconfigure diagnostics toouse hello 응용 프로그램 프로젝트에서 XML 구성 파일 (diagnostics.wadcfg 또는 SDK 2.5 이상 버전 이상의 경우)에 기본 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="27417-301">이 방법에서는 hello diagnostics.wadcfg 파일 완전히 hello 구성을 정의 및 업데이트 되어를 다시 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="27417-302">Hello를 사용 하 여 구성을 설정 하는 프로그래밍 방법도 hello와 hello diagnostics.wadcfg 구성 파일의 hello 사용을 혼합 [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)또는 [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) 클래스는 tooconfusion을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="27417-303">자세한 내용은 [Azure 진단 구성 초기화 또는 변경](https://msdn.microsoft.com/library/azure/hh411537.aspx) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="27417-304">(Azure SDK 2.5에 포함) WAD 1.3 부터는 것은 더 이상 가능한 toouse 코드 tooconfigure 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="27417-305">결과적으로, hello 구성 적용 하거나 hello 진단 확장을 업데이트할 때 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-306">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-306">Solution</span></span>
<span data-ttu-id="27417-307">Hello 진단 구성 디자이너 toomove 진단 설정을 toohello 진단 구성 파일 (diagnositcs.wadcfg 또는 SDK 2.5 이상 버전 이상의 경우)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="27417-308">설치 하는 것이 좋습니다 [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) hello 최신 진단 기능을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="27417-309">Hello tooconfigure hello 역할에 대 한 바로 가기 메뉴에서 속성을 선택 하 고 hello 구성 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="27417-310">Hello에 **진단** 섹션에, 해당 hello 반드시 **진단 사용** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="27417-311">Hello 선택 **구성** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="27417-311">Choose hello **Configure** button.</span></span>

   ![Hello 진단 사용 옵션 액세스](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="27417-313">자세한 내용은 [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27417-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="27417-314">DbContext 개체를 정적으로 선언하지 마십시오</span><span class="sxs-lookup"><span data-stu-id="27417-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="27417-315">ID</span><span class="sxs-lookup"><span data-stu-id="27417-315">ID</span></span>
<span data-ttu-id="27417-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="27417-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="27417-317">설명</span><span class="sxs-lookup"><span data-stu-id="27417-317">Description</span></span>
<span data-ttu-id="27417-318">toosave 메모리 DBContext 개체를 정적으로 선언 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="27417-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="27417-319">[Azure 코드 분석 의견](http://go.microsoft.com/fwlink/?LinkId=403771)에서 아이디어와 의견을 공유해 주세요.</span><span class="sxs-lookup"><span data-stu-id="27417-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="27417-320">이유</span><span class="sxs-lookup"><span data-stu-id="27417-320">Reason</span></span>
<span data-ttu-id="27417-321">DBContext 개체 hello 각 호출에서 쿼리 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="27417-322">DBContext 개체를 정적 hello 응용 프로그램 도메인이 언로드될 때까지 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="27417-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="27417-323">따라서 정적 DBContext 개체는 많은 양의 메모리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27417-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="27417-324">해결 방법</span><span class="sxs-lookup"><span data-stu-id="27417-324">Solution</span></span>
<span data-ttu-id="27417-325">DBContext를 지역 변수 또는 비정적 인스턴스 필드로 선언하고 작업에 사용한 다음 사용 후 삭제되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="27417-326">다음 예제에서는 MVC 컨트롤러 클래스 hello toouse DBContext 개체 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="27417-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="27417-327">다음 단계</span><span class="sxs-lookup"><span data-stu-id="27417-327">Next steps</span></span>
<span data-ttu-id="27417-328">Azure 응용 프로그램 문제 해결 및 최적화에 대해 자세히 toolearn 참조 [Visual Studio를 사용 하 여 Azure 앱 서비스의 웹 앱의 문제를 해결](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="27417-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
