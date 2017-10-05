---
title: "C#에서 Azure Service Fabric Reliable Service 만들기"
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
ms.openlocfilehash: f93298e6483fd8c9dfda835964aeebd1a430af69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="585b5-103">첫 번째 C# Service Fabric 상태 저장 Reliable Services 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="585b5-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="585b5-104">Windows에서 첫 번째 .NET용 Service Fabric 응용 프로그램을 몇 분 안에 배포하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-104">Learn how to deploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="585b5-105">완료된 경우 로컬 클러스터가 Reliable Service 응용 프로그램과 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="585b5-106">필수 조건</span><span class="sxs-lookup"><span data-stu-id="585b5-106">Prerequisites</span></span>

<span data-ttu-id="585b5-107">시작하기 전에 [개발 환경을 설정](service-fabric-get-started.md)하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="585b5-108">Service Fabric SDK 및 Visual Studio 2017 또는 2015 설치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-108">This includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="585b5-109">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="585b5-109">Create the application</span></span>

<span data-ttu-id="585b5-110">**관리자** 권한으로 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="585b5-111">`CTRL`+`SHIFT`+`N`를 사용하여 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="585b5-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="585b5-112">**새 프로젝트** 대화 상자에서 **클라우드 > Service Fabric 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-112">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="585b5-113">응용 프로그램의 이름을 **MyApplication**으로 지정하고 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-113">Name the application **MyApplication** and press **OK**.</span></span>

   
![Visual Studio의 새 프로젝트 대화 상자][1]

<span data-ttu-id="585b5-115">다음 대화 상자에서 모든 형식의 Service Fabric 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-115">You can create any type of Service Fabric application from the next dialog.</span></span> <span data-ttu-id="585b5-116">이 빠른 시작에서 **상태 저장 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="585b5-117">서비스 이름을 **MyStatefulService**로 지정하고 **확인**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-117">Name the service **MyStatefulService** and press **OK**.</span></span>

![Visual Studio의 새 서비스 대화 상자][2]


<span data-ttu-id="585b5-119">Visual Studio는 응용 프로그램 프로젝트 및 상태 저장 서비스 프로젝트를 만들고 솔루션 탐색기에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-119">Visual Studio creates the application project and the stateful service project and displays them in Solution Explorer.</span></span>

![상태 저장 서비스를 사용하여 응용 프로그램 만들기를 수행하는 솔루션 탐색기][3]

<span data-ttu-id="585b5-121">응용 프로그램 프로젝트(**MyApplication**)는 코드를 직접 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-121">The application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="585b5-122">대신 서비스 프로젝트의 집합을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="585b5-123">추가로 3가지 다른 형식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="585b5-124">**게시 프로필**</span><span class="sxs-lookup"><span data-stu-id="585b5-124">**Publish profiles**</span></span>  
<span data-ttu-id="585b5-125">다양한 환경에 배포하기 위한 프로필</span><span class="sxs-lookup"><span data-stu-id="585b5-125">Profiles for deploying to different environments.</span></span>

* <span data-ttu-id="585b5-126">**스크립트**</span><span class="sxs-lookup"><span data-stu-id="585b5-126">**Scripts**</span></span>  
<span data-ttu-id="585b5-127">응용 프로그램을 배포/업그레이드하기 위한 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="585b5-128">**응용 프로그램 정의**</span><span class="sxs-lookup"><span data-stu-id="585b5-128">**Application definition**</span></span>  
<span data-ttu-id="585b5-129">*ApplicationPackageRoot* 아래에 있는 ApplicationManifest.xml 파일을 포함하며 이는 응용 프로그램의 컴퍼지션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-129">Includes the ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="585b5-130">연결된 응용 프로그램 매개 변수 파일은 *ApplicationParameters* 아래에 있으며 환경 관련 매개 변수를 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-130">Associated application parameter files are under *ApplicationParameters*, which can be used to specify environment-specific parameters.</span></span> <span data-ttu-id="585b5-131">Visual Studio는 특정 환경에 배포하는 동안 연결된 게시 프로필에 지정된 응용 프로그램 매개 변수 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-131">Visual Studio selects an application parameter file that's specified in the associated publish profile during deployment to a specific environment.</span></span>
    
<span data-ttu-id="585b5-132">서비스 프로젝트의 내용에 대한 개요는 [Reliable Services 시작](service-fabric-reliable-services-quick-start.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="585b5-132">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-the-application"></a><span data-ttu-id="585b5-133">응용 프로그램 배포 및 디버깅</span><span class="sxs-lookup"><span data-stu-id="585b5-133">Deploy and debug the application</span></span>

<span data-ttu-id="585b5-134">이제 응용 프로그램이 설치되었으니 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="585b5-135">Visual Studio에서 `F5`를 눌러 응용 프로그램을 디버깅하기 위해 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-135">In Visual Studio, press `F5` to deploy the application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="585b5-136">로컬에서 처음으로 응용 프로그램을 실행하고 배포할 때 Visual Studio는 디버깅을 위해 로컬 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-136">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="585b5-137">다소 시간이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-137">This may take some time.</span></span> <span data-ttu-id="585b5-138">Visual Studio 출력 창에 클러스터 생성 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-138">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="585b5-139">클러스터가 준비되면 SDK를 포함한 로컬 클러스터 시스템 트레이 관리자 응용 프로그램에서 알림을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-139">When the cluster is ready, you get a notification from the local cluster system tray manager application included with the SDK.</span></span>
   
![로컬 클러스터 시스템 트레이 알림][4]

<span data-ttu-id="585b5-141">응용 프로그램이 시작되면 Visual Studio는 **진단 이벤트 뷰어**를 자동으로 표시하며 서비스에서 추적 출력을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-141">Once the application starts, Visual Studio automatically brings up the **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![진단 이벤트 뷰어][5]

<span data-ttu-id="585b5-143">사용한 상태 저장 서비스 템플릿에서는 **MyStatefulService.cs**의 `RunAsync` 메서드에서 증분하는 카운터 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-143">The stateful service template we used simply shows a counter value incrementing in the `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="585b5-144">코드가 실행되는 노드를 포함하여 자세한 정보를 보려면 이벤트 중 하나를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-144">Expand one of the events to see more details, including the node where the code is running.</span></span> <span data-ttu-id="585b5-145">이 경우에 \_Node\_2이지만 컴퓨터에서 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![진단 이벤트 뷰어 세부 정보][6]

<span data-ttu-id="585b5-147">로컬 클러스터는 단일 컴퓨터에서 호스트되는 다섯 개의 노드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-147">The local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="585b5-148">프로덕션 환경에서 각 노드는 고유한 물리적 컴퓨터 또는 가상 컴퓨터에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="585b5-149">컴퓨터의 손실을 시뮬레이션하는 동시에 Visual Studio 디버거를 실행하기 위해 로컬 클러스터의 노드 중 하나를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-149">To simulate the loss of a machine while exercising the Visual Studio debugger at the same time, let's take down one of the nodes on the local cluster.</span></span>

<span data-ttu-id="585b5-150">**솔루션 탐색기** 창에서 **MyStatefulService.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-150">In the **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="585b5-151">`RunAsync` 메서드를 찾고 메서드의 첫 번째 줄에서 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-151">Find the `RunAsync` method and set a breakpoint on the first line of the method.</span></span>

![상태 저장 서비스 RunAsync 메서드의 중단점][7]

<span data-ttu-id="585b5-153">**로컬 클러스터 관리자** 시스템 트레이 응용 프로그램을 마우스 오른쪽 단추로 클릭하여 **Service Fabric Explorer** 도구를 시작하고 **로컬 클러스터 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-153">Launch the **Service Fabric Explorer** tool by right-clicking on the **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![로컬 클러스터 관리자에서 서비스 패브릭 탐색기 시작][systray-launch-sfx]

<span data-ttu-id="585b5-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md)는 클러스터의 시각적 표현을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="585b5-156">배포된 응용 프로그램 집합 및 구성하는 실제 노드 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-156">It includes the set of applications deployed to it and the set of physical nodes that make it up.</span></span>

<span data-ttu-id="585b5-157">왼쪽 창에서 **클러스터 > 노드**를 확장하고 코드가 실행될 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-157">In the left pane, expand **Cluster > Nodes** and find the node where your code is running.</span></span>

<span data-ttu-id="585b5-158">**작업 > 비활성화(다시 시작)**를 클릭하여 컴퓨터 다시 시작을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-158">Click **Actions > Deactivate (Restart)** to simulate a machine restarting.</span></span>

![서비스 패브릭 탐색기에서 노드 중지][sfx-stop-node]

<span data-ttu-id="585b5-160">한 노드에서 원활하게 수행한 계산이 다른 노드에 장애 조치되면 일시적으로 Visual Studio에서 중단점을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-160">Momentarily, you should see your breakpoint hit in Visual Studio as the computation you were doing on one node seamlessly fails over to another.</span></span>


<span data-ttu-id="585b5-161">다음으로 진단 이벤트 뷰어로 돌아가서 메시지를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-161">Next, return to the Diagnostic Events Viewer and observe the messages.</span></span> <span data-ttu-id="585b5-162">실제로 다른 노드에서 이벤트가 들어오더라도 카운터는 계속 증분합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-162">The counter has continued incrementing, even though the events are actually coming from a different node.</span></span>

![장애 조치 후 진단 이벤트 뷰어][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-the-local-cluster-optional"></a><span data-ttu-id="585b5-164">로컬 클러스터 정리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="585b5-164">Cleaning up the local cluster (optional)</span></span>

<span data-ttu-id="585b5-165">이 로컬 클러스터는 실제입니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="585b5-166">디버거를 중지하면 응용 프로그램 인스턴스를 제거하고 응용 프로그램 형식의 등록을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-166">Stopping the debugger removes your application instance and unregisters the application type.</span></span> <span data-ttu-id="585b5-167">하지만 클러스터는 백그라운드에서 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-167">However, the cluster continues to run in the background.</span></span> <span data-ttu-id="585b5-168">로컬 클러스터를 중지할 준비가 되면 몇 가지 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-168">When you're ready to stop the local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="585b5-169">응용 프로그램 및 추적 데이터 유지</span><span class="sxs-lookup"><span data-stu-id="585b5-169">Keep application and trace data</span></span>

<span data-ttu-id="585b5-170">**로컬 클러스터 관리자** 시스템 트레이 응용 프로그램을 마우스 오른쪽 단추로 클릭하여 클러스터를 중단하고 **로컬 클러스터 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-170">Shut down the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-the-cluster-and-all-data"></a><span data-ttu-id="585b5-171">클러스터 및 모든 데이터 삭제</span><span class="sxs-lookup"><span data-stu-id="585b5-171">Delete the cluster and all data</span></span>

<span data-ttu-id="585b5-172">**로컬 클러스터 관리자** 시스템 트레이 응용 프로그램을 마우스 오른쪽 단추로 클릭하여 클러스터를 제거하고 **로컬 클러스터 제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-172">Remove the cluster by right-clicking on the **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="585b5-173">이 옵션을 선택하면 Visual Studio에서는 다음에 응용 프로그램을 실행할 때 클러스터를 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-173">If you choose this option, Visual Studio will redeploy the cluster the next time your run the application.</span></span> <span data-ttu-id="585b5-174">일정 시간 동안 로컬 클러스터를 사용하지 않거나 또는 리소스를 확보해야 하는 경우 이 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="585b5-174">Choose this option if you don't intend to use the local cluster for some time or if you need to reclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="585b5-175">다음 단계</span><span class="sxs-lookup"><span data-stu-id="585b5-175">Next steps</span></span>
<span data-ttu-id="585b5-176">[Reliable Services](service-fabric-reliable-services-introduction.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="585b5-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
