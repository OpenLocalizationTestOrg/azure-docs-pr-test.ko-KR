---
title: "클라우드 서비스 수명 주기 이벤트 aaaHandle | Microsoft Docs"
description: ".NET에서 클라우드 서비스 역할의 hello 수명 주기 메서드를 사용할 수 있는 방법을 알아봅니다"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a><span data-ttu-id="6ec76-103">Hello.NET에서 웹 또는 작업자 역할의 수명 주기를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="6ec76-103">Customize hello Lifecycle of a Web or Worker role in .NET</span></span>
<span data-ttu-id="6ec76-104">Hello를 확장 하는 작업자 역할을 만들 때 [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) toooverride 수 있는 사용자에 대 한 메서드를 제공 하는 클래스 toolifecycle 이벤트에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-104">When you create a worker role, you extend hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class which provides methods for you toooverride that let you respond toolifecycle events.</span></span> <span data-ttu-id="6ec76-105">웹 역할에 대 한이 클래스는 선택 사항 이므로 toorespond toolifecycle 이벤트 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-105">For web roles this class is optional, so you must use it toorespond toolifecycle events.</span></span>

## <a name="extend-hello-roleentrypoint-class"></a><span data-ttu-id="6ec76-106">Hello RoleEntryPoint 클래스 확장</span><span class="sxs-lookup"><span data-stu-id="6ec76-106">Extend hello RoleEntryPoint class</span></span>
<span data-ttu-id="6ec76-107">hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) 클래스 Azure에 의해 호출 된 메서드가 포함 됩니다 때 것 **시작**, **실행**, 또는 **중지** 웹 또는 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-107">hello [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) class includes methods that are called by Azure when it **starts**, **runs**, or **stops** a web or worker role.</span></span> <span data-ttu-id="6ec76-108">필요에 따라 이러한 방법 toomanage 역할 초기화, 역할 종료 시퀀스 또는 hello 역할의 hello 실행 스레드를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-108">You can optionally override these methods toomanage role initialization, role shutdown sequences, or hello execution thread of hello role.</span></span> 

<span data-ttu-id="6ec76-109">확장 하면 **RoleEntryPoint**, hello 메서드의 동작을 수행 하는 hello 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-109">When extending **RoleEntryPoint**, you should be aware of hello following behaviors of hello methods:</span></span>

* <span data-ttu-id="6ec76-110">hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) 및 [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) 가능한 tooreturn 되기 때문 메서드는 부울 값을 반환 **false** 이러한 방법 중에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-110">hello [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) and [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) methods return a boolean value, so it is possible tooreturn **false** from these methods.</span></span>
  
   <span data-ttu-id="6ec76-111">코드를 반환 하는 경우 **false**, 갑자기 종료 된 hello 역할 프로세스, 종료 시퀀스가 실행 하지 않고 현재 위치에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-111">If your code returns **false**, hello role process is abruptly terminated, without running any shutdown sequence you may have in place.</span></span> <span data-ttu-id="6ec76-112">반환 되지 않도록 해야 일반적으로 **false** hello에서 **OnStart** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ec76-112">In general, you should avoid returning **false** from hello **OnStart** method.</span></span>
* <span data-ttu-id="6ec76-113">**RoleEntryPoint** 메서드의 오버 로드 내 확인할 수 없는 예외는 처리되지 않는 예외로 취급됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-113">Any uncaught exception within an overload of a **RoleEntryPoint** method is treated as an unhandled exception.</span></span>
  
   <span data-ttu-id="6ec76-114">Azure에서 hello hello 수명 주기 메서드 중 하나에서 예외가 발생 하는 경우 발생 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 이벤트를 다음 hello 프로세스가 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-114">If an exception occurs within one of hello lifecycle methods, Azure will raise hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event, and then hello process is terminated.</span></span> <span data-ttu-id="6ec76-115">역할이 오프라인 상태가 되었거나, Azure에서 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-115">After your role has been taken offline, it will be restarted by Azure.</span></span> <span data-ttu-id="6ec76-116">처리 되지 않은 예외가 발생할 때 hello [중지](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) 이벤트 발생 하지 않은 및 hello **OnStop** 메서드가 호출 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-116">When an unhandled exception occurs, hello [Stopping](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) event is not raised, and hello **OnStop** method is not called.</span></span>

<span data-ttu-id="6ec76-117">역할이 시작 되지 않으면 또는 hello 초기화, 사용 중 및 중지 중 상태 사이 재활용 되는 경우 코드 각 시간 hello 역할이 다시 시작 하는 hello 수명 주기 이벤트 중 하나에서 처리 되지 않은 예외를 throw 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-117">If your role does not start, or is recycling between hello initializing, busy, and stopping states, your code may be throwing an unhandled exception within one of hello lifecycle events each time hello role restarts.</span></span> <span data-ttu-id="6ec76-118">이 경우 hello를 사용 하 여 [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) 이벤트 toodetermine hello hello 예외를 발생 하 고 적절 하 게 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-118">In this case, use hello [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) event toodetermine hello cause of hello exception and handle it appropriately.</span></span> <span data-ttu-id="6ec76-119">사용자의 역할 hello에서 반환 될 수도 있으며 [실행](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) hello 역할 toorestart 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-119">Your role may also be returning from hello [Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, which causes hello role toorestart.</span></span> <span data-ttu-id="6ec76-120">배포 상태에 대 한 자세한 내용은 참조 [일반적인 문제는 원인 역할 tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-120">For more information about deployment states, see [Common Issues Which Cause Roles tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6ec76-121">Hello를 사용 하는 경우 **Azure Tools for Microsoft Visual Studio** toodevelop 응용 프로그램 역할 프로젝트 템플릿은 hello hello 자동 확장 **RoleEntryPoint** 클래스를 hello에*WebRole.cs* 및 *WorkerRole.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-121">If you are using hello **Azure Tools for Microsoft Visual Studio** toodevelop your application, hello role project templates automatically extend hello **RoleEntryPoint** class for you, in hello *WebRole.cs* and *WorkerRole.cs* files.</span></span>
> 
> 

## <a name="onstart-method"></a><span data-ttu-id="6ec76-122">Onstart 메서드</span><span class="sxs-lookup"><span data-stu-id="6ec76-122">OnStart method</span></span>
<span data-ttu-id="6ec76-123">hello **OnStart** 역할 인스턴스가 Azure에서 온라인 상태가 되 면 메서드가 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-123">hello **OnStart** method is called when your role instance is brought online by Azure.</span></span> <span data-ttu-id="6ec76-124">Hello 역할 인스턴스가로 표시 되어 hello OnStart 코드가 실행 되는 동안 **Busy** 외부 트래픽을 hello 부하 분산 장치에 의해 지정 된 tooit 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-124">While hello OnStart code is executing, hello role instance is marked as **Busy** and no external traffic will be directed tooit by hello load balancer.</span></span> <span data-ttu-id="6ec76-125">이벤트 처리기를 구현 하 고 시작 등이 메서드 tooperform 초기화 작업을 재정의할 수 [Azure 진단](cloud-services-how-to-monitor.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-125">You can override this method tooperform initialization work, such as implementing event handlers and starting [Azure Diagnostics](cloud-services-how-to-monitor.md).</span></span>

<span data-ttu-id="6ec76-126">경우 **OnStart** 반환 **true**, hello 인스턴스가 초기화 되 고 호출 하는 Azure hello **RoleEntryPoint.Run** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ec76-126">If **OnStart** returns **true**, hello instance is successfully initialized and Azure calls hello **RoleEntryPoint.Run** method.</span></span> <span data-ttu-id="6ec76-127">경우 **OnStart** 반환 **false**, hello 역할 계획된 된 종료 시퀀스를 실행 하지 않고 즉시 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-127">If **OnStart** returns **false**, hello role terminates immediately, without executing any planned shutdown sequences.</span></span>

<span data-ttu-id="6ec76-128">코드 예제에서 보여 주는 방법을 다음 hello toooverride hello **OnStart** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ec76-128">hello following code example shows how toooverride hello **OnStart** method.</span></span> <span data-ttu-id="6ec76-129">이 메서드를 구성 하 고 hello 역할 인스턴스가 시작 되 고 tooa 저장소 계정 데이터 로깅의 전송을 설정할 때 진단 모니터를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-129">This method configures and starts a diagnostic monitor when hello role instance starts and sets up a transfer of logging data tooa storage account:</span></span>

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a><span data-ttu-id="6ec76-130">OnStop 메서드</span><span class="sxs-lookup"><span data-stu-id="6ec76-130">OnStop method</span></span>
<span data-ttu-id="6ec76-131">hello **OnStop** 메서드 후 역할 인스턴스가 되었습니다에서 오프 라인 Azure hello 프로세스 종료 되기 전에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-131">hello **OnStop** method is called after a role instance has been taken offline by Azure and before hello process exits.</span></span> <span data-ttu-id="6ec76-132">이 메서드 toocall 코드를 종료 하 여 역할 인스턴스 toocleanly에 필요한 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-132">You can override this method toocall code required for your role instance toocleanly shut down.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ec76-133">Hello에서 실행 되는 코드 **OnStop** 사용자가 시작한 종료 이외의 이유로 호출 될 때 메서드에 제한 된 시간 toofinish 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-133">Code running in hello **OnStop** method has a limited time toofinish when it is called for reasons other than a user-initiated shutdown.</span></span> <span data-ttu-id="6ec76-134">이 시간이 지난 후 hello 프로세스 종료 되므로 해야 하며 해당 코드 hello에 **OnStop** 메서드 신속 하 게 실행 하거나 실행 되지 않는 toocompletion 것을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-134">After this time elapses, hello process is terminated, so you must make sure that code in hello **OnStop** method can run quickly or tolerates not running toocompletion.</span></span> <span data-ttu-id="6ec76-135">hello **OnStop** hello 후 메서드는 **중지** 이벤트가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-135">hello **OnStop** method is called after hello **Stopping** event is raised.</span></span>
> 
> 

## <a name="run-method"></a><span data-ttu-id="6ec76-136">Run 메서드</span><span class="sxs-lookup"><span data-stu-id="6ec76-136">Run method</span></span>
<span data-ttu-id="6ec76-137">Hello를 재정의할 수 **실행** 메서드 tooimplement 역할 인스턴스에 대 한 장기 실행 스레드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-137">You can override hello **Run** method tooimplement a long-running thread for your role instance.</span></span>

<span data-ttu-id="6ec76-138">Hello 재정의 **실행** 메서드는 필요 하지 않으면 hello 기본 구현은 영원히 중지 되는 스레드를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-138">Overriding hello **Run** method is not required; hello default implementation starts a thread that sleeps forever.</span></span> <span data-ttu-id="6ec76-139">Hello를 재정의 하는 경우 **실행** 메서드를 코드 무기한으로 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-139">If you do override hello **Run** method, your code should block indefinitely.</span></span> <span data-ttu-id="6ec76-140">경우 hello **실행** hello 역할이 자동으로 정상적으로 재활용 됩니다; Azure 발생 하는 즉, 메서드가 반환 hello **중지** 이벤트 및 호출 hello **OnStop** 메서드 하므로 오프 라인 종료 시퀀스가 hello 역할 하기 전에 실행 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-140">If hello **Run** method returns, hello role is automatically gracefully recycled; in other words, Azure raises hello **Stopping** event and calls hello **OnStop** method so that your shutdown sequences may be executed before hello role is taken offline.</span></span>

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a><span data-ttu-id="6ec76-141">웹 역할에 대 한 hello ASP.NET 수명 주기 메서드 구현</span><span class="sxs-lookup"><span data-stu-id="6ec76-141">Implementing hello ASP.NET lifecycle methods for a web role</span></span>
<span data-ttu-id="6ec76-142">또한 toothose hello가 제공 hello ASP.NET 수명 주기 메서드를 사용할 수 있습니다 **RoleEntryPoint** 클래스를 웹 역할에 대 한 toomanage 초기화 및 종료 시퀀스입니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-142">You can use hello ASP.NET lifecycle methods, in addition toothose provided by hello **RoleEntryPoint** class, toomanage initialization and shutdown sequences for a web role.</span></span> <span data-ttu-id="6ec76-143">이 기존 ASP.NET 응용 프로그램 tooAzure 이식 하는 경우 호환성을 위해 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-143">This may be useful for compatibility purposes if you are porting an existing ASP.NET application tooAzure.</span></span> <span data-ttu-id="6ec76-144">hello ASP.NET 수명 주기 메서드는 hello 내에서 호출 **RoleEntryPoint** 메서드.</span><span class="sxs-lookup"><span data-stu-id="6ec76-144">hello ASP.NET lifecycle methods are called from within hello **RoleEntryPoint** methods.</span></span> <span data-ttu-id="6ec76-145">hello **응용 프로그램\_시작** hello 후 메서드는 **RoleEntryPoint.OnStart** 메서드가 완료 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-145">hello **Application\_Start** method is called after hello **RoleEntryPoint.OnStart** method finishes.</span></span> <span data-ttu-id="6ec76-146">hello **응용 프로그램\_끝** hello 전에 메서드가 호출 되 **RoleEntryPoint.OnStop** 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-146">hello **Application\_End** method is called before hello **RoleEntryPoint.OnStop** method is called.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ec76-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ec76-147">Next steps</span></span>
<span data-ttu-id="6ec76-148">너무 방법에 대해 알아봅니다[클라우드 서비스 패키지 만들기](cloud-services-model-and-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ec76-148">Learn how too[create a cloud service package](cloud-services-model-and-package.md).</span></span>

