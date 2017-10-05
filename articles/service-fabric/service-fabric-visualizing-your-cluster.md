---
title: "Service Fabric Explorer를 사용하여 클러스터 시각화 | Microsoft Docs"
description: "서비스 패브릭 탐색기는 Microsoft Azure 서비스 패브릭 클러스터에서 클라우드 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 789793a7f50170188d688881a9178546c3074018
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="f1307-103">서비스 패브릭 탐색기로 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="f1307-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="f1307-104">서비스 패브릭 탐색기는 Azure 서비스 패브릭 클러스터에서 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="f1307-105">클러스터의 실행 여부와 관계없이 항상 사용할 수 있도록 서비스 패브릭 탐색기가 클러스터 내에서 직접 호스트됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-105">Service Fabric Explorer is hosted directly within the cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="f1307-106">비디오 자습서</span><span class="sxs-lookup"><span data-stu-id="f1307-106">Video tutorial</span></span>

<span data-ttu-id="f1307-107">Service Fabric Explorer를 사용하는 방법을 알아보려면 다음 Microsoft Virtual Academy 비디오를 시청하세요.</span><span class="sxs-lookup"><span data-stu-id="f1307-107">To learn how to use Service Fabric Explorer, watch the following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-to-service-fabric-explorer"></a><span data-ttu-id="f1307-108">서비스 패브릭 탐색기에 연결</span><span class="sxs-lookup"><span data-stu-id="f1307-108">Connect to Service Fabric Explorer</span></span>
<span data-ttu-id="f1307-109">[개발 환경 준비](service-fabric-get-started.md)에 대한 지침을 따른 경우 http://localhost:19080/Explorer로 이동하여 로컬 클러스터에서 Service Fabric Explorer를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-109">If you have followed the instructions to [prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating to http://localhost:19080/Explorer.</span></span>

## <a name="understand-the-service-fabric-explorer-layout"></a><span data-ttu-id="f1307-110">서비스 패브릭 탐색기 레이아웃 이해</span><span class="sxs-lookup"><span data-stu-id="f1307-110">Understand the Service Fabric Explorer layout</span></span>
<span data-ttu-id="f1307-111">왼쪽의 트리를 사용하여 서비스 패브릭 탐색기를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-111">You can navigate through Service Fabric Explorer by using the tree on the left.</span></span> <span data-ttu-id="f1307-112">트리의 루트에서 클러스터 대시보드는 응용 프로그램 및 노드 상태에 대한 요약을 포함하여 클러스터에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-112">At the root of the tree, the cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![서비스 패브릭 탐색기 클러스터 대시보드][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a><span data-ttu-id="f1307-114">클러스터의 레이아웃 보기</span><span class="sxs-lookup"><span data-stu-id="f1307-114">View the cluster's layout</span></span>
<span data-ttu-id="f1307-115">서비스 패브릭 클러스터의 노드는 장애 도메인 및 업그레이드 도메인의 2차원 그리드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="f1307-116">이렇게 배치하면 하드웨어 오류와 응용 프로그램 업그레이드가 있는 상태에서 응용 프로그램을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-116">This placement ensures that your applications remain available in the presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="f1307-117">클러스터 맵을 사용하여 현재 클러스터의 레이아웃 방식을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-117">You can view how the current cluster is laid out by using the cluster map.</span></span>

![서비스 패브릭 탐색기 클러스터 맵][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="f1307-119">응용 프로그램 및 서비스 보기</span><span class="sxs-lookup"><span data-stu-id="f1307-119">View applications and services</span></span>
<span data-ttu-id="f1307-120">클러스터에는 두 개의 하위 트리가 포함되어 있습니다. 하나는 응용 프로그램용이고 다른 하나는 노드용입니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-120">The cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="f1307-121">응용 프로그램 보기를 사용하여 서비스 패브릭의 논리 계층 구조인 응용 프로그램, 서비스, 파티션 및 복제를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-121">You can use the application view to navigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="f1307-122">아래 예제에서 응용 프로그램 **MyApp**은 두 개의 서비스, **MyStatefulService**와 **WebService**로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-122">In the example below, the application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="f1307-123">**MyStatefulService** 는 상태 저장이므로 한 개의 주 복제본과 두 개의 보조 복제본이 있는 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="f1307-124">이와 반대로 WebSvcService는 상태 비저장이며 단일 인스턴스가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![서비스 패브릭 탐색기 응용 프로그램 보기][sfx-application-tree]

<span data-ttu-id="f1307-126">트리의 각 수준에서 주 창은 항목에 대한 관련 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-126">At each level of the tree, the main pane shows pertinent information about the item.</span></span> <span data-ttu-id="f1307-127">예를 들어 특정 서비스에 대한 상태 및 버전을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-127">For example, you can see the health status and version for a particular service.</span></span>

![서비스 패브릭 탐색기 기능 창][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a><span data-ttu-id="f1307-129">클러스터의 노드 보기</span><span class="sxs-lookup"><span data-stu-id="f1307-129">View the cluster's nodes</span></span>
<span data-ttu-id="f1307-130">노드 보기는 클러스터의 물리적 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-130">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="f1307-131">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="f1307-132">특히 현재 실행되고 있는 복제본을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="f1307-133">작업</span><span class="sxs-lookup"><span data-stu-id="f1307-133">Actions</span></span>
<span data-ttu-id="f1307-134">서비스 패브릭 탐색기는 클러스터 내에서 노드, 응용 프로그램 및 서비스에 대한 작업을 호출하는 빠른 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-134">Service Fabric Explorer offers a quick way to invoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="f1307-135">예를 들어 응용 프로그램 인스턴스를 삭제하려면 왼쪽 트리에서 응용 프로그램을 선택한 다음 **작업** > **응용 프로그램 삭제**로 이동하여 로컬 클러스터에서 Service Fabric 탐색기를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-135">For example, to delete an application instance, choose the application from the tree on the left, and then choose **Actions** > **Delete Application**.</span></span>

![서비스 패브릭 탐색기에서 응용 프로그램 삭제][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="f1307-137">각 요소 옆의 줄임표를 클릭하여 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-137">You can perform the same actions by clicking the ellipsis next to each element.</span></span>
>
>

<span data-ttu-id="f1307-138">다음 테이블에서는 각 엔터티에 사용할 수 있는 작업을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-138">The following table lists the actions available for each entity:</span></span>

| <span data-ttu-id="f1307-139">**엔터티**</span><span class="sxs-lookup"><span data-stu-id="f1307-139">**Entity**</span></span> | <span data-ttu-id="f1307-140">**작업**</span><span class="sxs-lookup"><span data-stu-id="f1307-140">**Action**</span></span> | <span data-ttu-id="f1307-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="f1307-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f1307-142">응용 프로그램 형식</span><span class="sxs-lookup"><span data-stu-id="f1307-142">Application type</span></span> |<span data-ttu-id="f1307-143">프로 비전 해제 형식</span><span class="sxs-lookup"><span data-stu-id="f1307-143">Unprovision type</span></span> |<span data-ttu-id="f1307-144">클러스터의 이미지 저장소에서 응용 프로그램 패키지 제거</span><span class="sxs-lookup"><span data-stu-id="f1307-144">Removes the application package from the cluster's image store.</span></span> <span data-ttu-id="f1307-145">해당 형식의 모든 응용 프로그램을 먼저 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-145">Requires all applications of that type to be removed first.</span></span> |
| <span data-ttu-id="f1307-146">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="f1307-146">Application</span></span> |<span data-ttu-id="f1307-147">응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="f1307-147">Delete Application</span></span> |<span data-ttu-id="f1307-148">모든 서비스와 해당 상태를 포함하여(있는 경우) 응용 프로그램을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-148">Delete the application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="f1307-149">부여</span><span class="sxs-lookup"><span data-stu-id="f1307-149">Service</span></span> |<span data-ttu-id="f1307-150">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="f1307-150">Delete Service</span></span> |<span data-ttu-id="f1307-151">서비스 및 해당 상태(있는 경우)를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-151">Delete the service and its state (if any).</span></span> |
| <span data-ttu-id="f1307-152">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-152">Node</span></span> |<span data-ttu-id="f1307-153">활성화</span><span class="sxs-lookup"><span data-stu-id="f1307-153">Activate</span></span> |<span data-ttu-id="f1307-154">노드 활성화</span><span class="sxs-lookup"><span data-stu-id="f1307-154">Activate the node.</span></span> |
| <span data-ttu-id="f1307-155">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-155">Node</span></span> | <span data-ttu-id="f1307-156">비활성화(일시 중지)</span><span class="sxs-lookup"><span data-stu-id="f1307-156">Deactivate (pause)</span></span> | <span data-ttu-id="f1307-157">현재 상태에서 노드를 일시 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-157">Pause the node in its current state.</span></span> <span data-ttu-id="f1307-158">서비스는 계속 실행하지만 가동 중단 또는 데이터 불일치를 방지하는 데 필요한 경우가 아니면 서비스 패브릭은 아무것도 사전에 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-158">Services continue to run but Service Fabric does not proactively move anything onto or off it unless it is required to prevent an outage or data inconsistency.</span></span> <span data-ttu-id="f1307-159">이 작업은 검사하는 동안 이동하지 않도록 특정 노드에 디버깅 서비스를 사용하도록 설정하는 데 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-159">This action is typically used to enable debugging services on a specific node to ensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="f1307-160">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-160">Node</span></span> | <span data-ttu-id="f1307-161">비활성화(다시 시작)</span><span class="sxs-lookup"><span data-stu-id="f1307-161">Deactivate (restart)</span></span> | <span data-ttu-id="f1307-162">안전하게 노드에서 모든 메모리 내 서비스를 이동하고 영구 서비스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="f1307-163">호스트 프로세스 또는 컴퓨터를 다시 시작해야 할 때 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-163">Typically used when the host processes or machine need to be restarted.</span></span> | |
| <span data-ttu-id="f1307-164">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-164">Node</span></span> | <span data-ttu-id="f1307-165">비활성화(데이터 제거)</span><span class="sxs-lookup"><span data-stu-id="f1307-165">Deactivate (remove data)</span></span> | <span data-ttu-id="f1307-166">안전하게 충분한 예비 복제본을 작성한 후에 노드에 실행하는 모든 서비스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-166">Safely close all services running on the node after building sufficient spare replicas.</span></span> <span data-ttu-id="f1307-167">노드(또는 최소한 저장소)가 위원회에서 영구적으로 제거될 때 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="f1307-168">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-168">Node</span></span> | <span data-ttu-id="f1307-169">노드 상태 제거</span><span class="sxs-lookup"><span data-stu-id="f1307-169">Remove node state</span></span> | <span data-ttu-id="f1307-170">클러스터에서 노드의 복제본에 대한 정보를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-170">Remove knowledge of a node's replicas from the cluster.</span></span> <span data-ttu-id="f1307-171">이미 실패한 노드를 복구할 수 없다고 간주하는 경우 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="f1307-172">노드</span><span class="sxs-lookup"><span data-stu-id="f1307-172">Node</span></span> | <span data-ttu-id="f1307-173">다시 시작</span><span class="sxs-lookup"><span data-stu-id="f1307-173">Restart</span></span> | <span data-ttu-id="f1307-174">노드를 다시 시작하여 노드 오류를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-174">Simulate a node failure by restarting the node.</span></span> <span data-ttu-id="f1307-175">자세한 내용은 [여기](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1307-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="f1307-176">많은 작업이 안전하지 않으므로 작업이 완료되기 전에 실행할 것인지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-176">Since many actions are destructive, you may be asked to confirm your intent before the action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="f1307-177">서비스 패브릭 탐색기를 통해 수행할 수 있는 모든 작업은 PowerShell 또는 REST API를 통해 수행할 수 있으므로 자동화를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, to enable automation.</span></span>
>
>

<span data-ttu-id="f1307-178">또한 Service Fabric Explorer를 사용하여 지정된 응용 프로그램 형식 및 버전에 대한 응용 프로그램 인스턴스를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-178">You can also use Service Fabric Explorer to create application instances for a given application type and version.</span></span> <span data-ttu-id="f1307-179">트리 보기에서 응용 프로그램 형식을 선택하고 오른쪽 창에서 원하는 버전 옆의 **앱 인스턴스 만들기** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-179">Choose the application type in the tree view, then click the **Create app instance** link next to the version you'd like in the right pane.</span></span>

![Service Fabric Explorer에서 응용 프로그램 인스턴스 만들기][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="f1307-181">Service Fabric Explorer를 통해 만든 응용 프로그램 인스턴스는 현재 매개 변수화될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="f1307-182">이러한 프로그램은 기본 매개 변수 값을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-to-a-remote-service-fabric-cluster"></a><span data-ttu-id="f1307-183">원격 서비스 패브릭 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f1307-183">Connect to a remote Service Fabric cluster</span></span>
<span data-ttu-id="f1307-184">클러스터의 끝점을 알고 있고 충분한 권한이 있으면 어느 브라우저에서든 Service Fabric Explorer에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-184">If you know the cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="f1307-185">Service Fabric Explorer는 클러스터에서 실행되는 또 다른 서비스이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-185">This is because Service Fabric Explorer is just another service that runs in the cluster.</span></span>

### <a name="discover-the-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="f1307-186">서비스 패브릭 탐색기에서 원격 클러스터의 끝점 검색</span><span class="sxs-lookup"><span data-stu-id="f1307-186">Discover the Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="f1307-187">지정된 클러스터를 위한 Service Fabric Explorer에 도달하려면 브라우저를 다음으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-187">To reach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="f1307-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="f1307-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="f1307-189">Azure 클러스터의 경우 Azure Portal의 클러스터 필수 창에서도 전체 URL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-189">For Azure clusters, the full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="f1307-190">보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="f1307-190">Connect to a secure cluster</span></span>
<span data-ttu-id="f1307-191">인증서 또는 AAD(Azure Active Directory)를 사용하여 서비스 패브릭 클라이언트에 대한 클라이언트 액세스를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-191">You can control client access to your Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="f1307-192">보안 클러스터에 Service Fabric Explorer를 연결하려고 하는 경우 클러스터의 구성에 따라 클라이언트 인증서를 제시하거나 AAD를 사용하여 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1307-192">If you attempt to connect to Service Fabric Explorer on a secure cluster, then depending on the cluster's configuration you'll be required to present a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1307-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f1307-193">Next steps</span></span>
* [<span data-ttu-id="f1307-194">테스트 용이성 개요</span><span class="sxs-lookup"><span data-stu-id="f1307-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="f1307-195">Visual Studio에서 서비스 패브릭 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="f1307-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="f1307-196">PowerShell을 사용하여 서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="f1307-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
