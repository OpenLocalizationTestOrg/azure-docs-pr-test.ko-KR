---
title: "aaaCreate C#과 함께 사용 되는 Azure 서비스 패브릭 신뢰할 수 있는 서비스"
description: "Visual Studio를 사용하여 Azure Service Fabric을 기반으로 하는 Reliable Service 응용 프로그램을 만들고, 배포하고, 디버깅합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="91cdd-103">첫 번째 C# Service Fabric 상태 저장 Reliable Services 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="91cdd-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="91cdd-104">자세한 내용은 방법 toodeploy 첫 번째 서비스 패브릭 응용 프로그램을 Windows에서.NET 단 몇 분 후에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="91cdd-105">완료된 경우 로컬 클러스터가 Reliable Service 응용 프로그램과 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91cdd-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="91cdd-106">Prerequisites</span></span>

<span data-ttu-id="91cdd-107">시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="91cdd-108">여기에 hello 서비스 패브릭 SDK 및 Visual Studio 2017 또는 2015를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="91cdd-109">Hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="91cdd-109">Create hello application</span></span>

<span data-ttu-id="91cdd-110">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="91cdd-111">`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="91cdd-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="91cdd-112">Hello에 **새 프로젝트** 대화 상자에서 선택 **클라우드 > 서비스 패브릭 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="91cdd-113">Hello 응용 프로그램 이름을 **MyApplication** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Visual Studio의 새 프로젝트 대화 상자][1]

<span data-ttu-id="91cdd-115">Hello 다음 대화 상자에서 모든 유형의 서비스 패브릭 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="91cdd-116">이 빠른 시작에서 **상태 저장 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="91cdd-117">Hello 서비스 이름을 **MyStatefulService** 누릅니다 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Visual Studio의 새 서비스 대화 상자][2]


<span data-ttu-id="91cdd-119">Visual Studio hello 응용 프로그램 프로젝트 만들고 hello 상태 저장 서비스 프로젝트 및 솔루션 탐색기에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![상태 저장 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기][3]

<span data-ttu-id="91cdd-121">hello 응용 프로그램 프로젝트 (**MyApplication**) 코드는 직접 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="91cdd-122">대신 서비스 프로젝트의 집합을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="91cdd-123">추가로 3가지 다른 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="91cdd-124">**게시 프로필**</span><span class="sxs-lookup"><span data-stu-id="91cdd-124">**Publish profiles**</span></span>  
<span data-ttu-id="91cdd-125">Toodifferent 환경 배포에 대 한 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="91cdd-126">**스크립트**</span><span class="sxs-lookup"><span data-stu-id="91cdd-126">**Scripts**</span></span>  
<span data-ttu-id="91cdd-127">응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="91cdd-128">**응용 프로그램 정의**</span><span class="sxs-lookup"><span data-stu-id="91cdd-128">**Application definition**</span></span>  
<span data-ttu-id="91cdd-129">Hello ApplicationManifest.xml 파일에서 포함 *ApplicationPackageRoot* 설명 하는 응용 프로그램의 컴퍼지션입니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="91cdd-130">아래에서 관련된 응용 프로그램 매개 변수 파일은 *ApplicationParameters*역할 환경 관련 매개 변수로 사용 되는 toospecify를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="91cdd-131">Visual Studio가 선택 되어 hello에 지정 된 응용 프로그램 매개 변수 파일에 연결 된 게시 프로필 배포 tooa 특정 환경 중.</span><span class="sxs-lookup"><span data-stu-id="91cdd-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="91cdd-132">Hello 서비스 프로젝트의 hello 내용에 대 한 개요를 참조 하십시오. [신뢰할 수 있는 서비스 시작](service-fabric-reliable-services-quick-start.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="91cdd-133">배포 및 hello 응용 프로그램 디버깅</span><span class="sxs-lookup"><span data-stu-id="91cdd-133">Deploy and debug hello application</span></span>

<span data-ttu-id="91cdd-134">이제 응용 프로그램이 설치되었으니 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="91cdd-135">키를 눌러 Visual Studio에서 `F5` toodeploy hello 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="91cdd-136">hello 처음으로 실행 하 고 hello 응용 프로그램 배포를 로컬로 Visual Studio 디버깅에 대 한 로컬 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="91cdd-137">다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-137">This may take some time.</span></span> <span data-ttu-id="91cdd-138">hello 클러스터 만들기 상태 hello Visual Studio 출력 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="91cdd-139">Hello 클러스터 준비 되 면 hello 로컬 클러스터 시스템 트레이 관리자 응용 프로그램 으로부터 hello SDK에 포함 된 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![로컬 클러스터 시스템 트레이 알림][4]

<span data-ttu-id="91cdd-141">한 번 hello 응용 프로그램이 시작 Visual Studio 자동으로 표시 hello **진단 이벤트 뷰어**서비스에서 추적 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![진단 이벤트 뷰어][5]

<span data-ttu-id="91cdd-143">hello 사용 하는 상태 저장 서비스 템플릿을 보여 줍니다 hello에 카운터 값 증분 `RunAsync` 방식의 **MyStatefulService.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="91cdd-144">Hello 코드가 실행 되 고 hello 노드를 포함 한 자세한 정보를 hello 이벤트 toosee 중 하나를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="91cdd-145">이 경우에 \_Node\_2이지만 컴퓨터에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![진단 이벤트 뷰어 세부 정보][6]

<span data-ttu-id="91cdd-147">hello 로컬 클러스터에는 단일 컴퓨터에서 호스트 되는 5 개의 노드가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="91cdd-148">프로덕션 환경에서 각 노드는 고유한 물리적 컴퓨터 또는 가상 컴퓨터에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="91cdd-149">hello에서 toosimulate hello 손실 hello Visual Studio를 실행 하는 동안 컴퓨터의 디버거 같은 시간, hello 로컬 클러스터에 있는 hello 노드 중 하나를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="91cdd-150">Hello에 **솔루션 탐색기** 창을 열어 **MyStatefulService.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="91cdd-151">Hello `RunAsync` 메서드와 hello hello 메서드의 첫 번째 줄에 중단점을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![상태 저장 서비스 RunAsync 메서드의 중단점][7]

<span data-ttu-id="91cdd-153">Hello 시작 **서비스 패브릭 탐색기** hello를 마우스 오른쪽 단추로 클릭 하 여 도구 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램을 선택 하 고 **로컬 클러스터 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Hello 로컬 클러스터 관리자에서에서 서비스 패브릭 탐색기를 실행 합니다.][systray-launch-sfx]

<span data-ttu-id="91cdd-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md)는 클러스터의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="91cdd-156">배포 된 응용 프로그램 tooit 집합이 hello 및 hello 구성 하는 실제 노드 집합이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="91cdd-157">Hello 왼쪽된 창에서 **클러스터 > 노드** 및 코드를 실행 하는 찾기 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="91cdd-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="91cdd-158">클릭 **작업 > 비활성화 (다시 시작)** toosimulate 컴퓨터 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![서비스 패브릭 탐색기에서 노드 중지][sfx-stop-node]

<span data-ttu-id="91cdd-160">중단점을 일시적으로 표시 되어야 tooanother로 장애 조치를 수행 하 고 한 노드에서 원활 하 게 hello 계산 하는 대로 Visual Studio에서 적중 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="91cdd-161">다음을 toohello 진단 이벤트 뷰어를 반환 하 고 hello 메시지를 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="91cdd-162">hello 카운터 지속적 증가 hello 이벤트가 실제로 다른 노드에서 들어오는 경우에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![장애 조치 후 진단 이벤트 뷰어][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="91cdd-164">(옵션) 로컬 클러스터 hello 정리</span><span class="sxs-lookup"><span data-stu-id="91cdd-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="91cdd-165">이 로컬 클러스터는 실제입니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="91cdd-166">Hello 디버거를 중지 합니다. 응용 프로그램 인스턴스를 제거 하 고 hello 응용 프로그램 종류의 등록을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="91cdd-167">그러나 hello 클러스터 toorun hello 백그라운드에서 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="91cdd-168">준비 toostop hello 로컬 클러스터를 사용 하는 경우에 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="91cdd-169">응용 프로그램 및 추적 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="91cdd-169">Keep application and trace data</span></span>

<span data-ttu-id="91cdd-170">Hello를 마우스 오른쪽 단추로 클릭 하 여 hello 클러스터를 종료 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램 선택 **로컬 클러스터 중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="91cdd-171">Hello 클러스터 및 모든 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="91cdd-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="91cdd-172">Hello를 마우스 오른쪽 단추로 클릭 하 여 hello 클러스터를 제거 **로컬 클러스터 관리자** 시스템 트레이 응용 프로그램 선택 **로컬 클러스터 제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="91cdd-173">이 옵션을 선택 하면 다음 번 실행 하면 응용 프로그램 hello Visual Studio hello 클러스터 hello를 재배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="91cdd-174">일정 시간 동안 toouse hello 로컬 클러스터 않으려는 경우 또는 tooreclaim 리소스가 필요한 경우이 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="91cdd-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91cdd-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="91cdd-175">Next steps</span></span>
<span data-ttu-id="91cdd-176">[Reliable Services](service-fabric-reliable-services-introduction.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="91cdd-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
