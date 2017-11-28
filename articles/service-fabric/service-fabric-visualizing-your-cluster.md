---
title: "aaaVisualizing 서비스 패브릭 탐색기를 사용 하 여 클러스터 | Microsoft Docs"
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
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="efb4f-103">서비스 패브릭 탐색기로 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="efb4f-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="efb4f-104">서비스 패브릭 탐색기는 Azure 서비스 패브릭 클러스터에서 응용 프로그램 및 노드를 검사 및 관리하기 위한 웹 기반 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="efb4f-105">서비스 패브릭 탐색기 클러스터 실행 되 고 있는 관계 없이 사용할 수는 항상 hello 클러스터 내에서 직접 호스트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="efb4f-106">비디오 자습서</span><span class="sxs-lookup"><span data-stu-id="efb4f-106">Video tutorial</span></span>

<span data-ttu-id="efb4f-107">서비스 패브릭 탐색기 toouse 시청 어떻게 toolearn Microsoft Virtual Academy 비디오 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="efb4f-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="efb4f-108">TooService 패브릭 탐색기를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="efb4f-109">너무 hello 지시를 따른 경우[개발 환경을 준비](service-fabric-get-started.md), toohttp://localhost:19080 이동 하 여 로컬 클러스터에 대해 서비스 패브릭 탐색기를 시작할 수 있습니다 / 탐색기.</span><span class="sxs-lookup"><span data-stu-id="efb4f-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="efb4f-110">서비스 패브릭 탐색기 레이아웃 hello 이해</span><span class="sxs-lookup"><span data-stu-id="efb4f-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="efb4f-111">서비스 패브릭 탐색기 hello 왼쪽에 hello 트리를 사용 하 여 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="efb4f-112">Hello hello 트리의 루트에 hello 클러스터 대시보드는 응용 프로그램 및 노드 상태 요약을 포함 하 여 클러스터에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![서비스 패브릭 탐색기 클러스터 대시보드][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="efb4f-114">Hello 클러스터의 레이아웃을 보려면</span><span class="sxs-lookup"><span data-stu-id="efb4f-114">View hello cluster's layout</span></span>
<span data-ttu-id="efb4f-115">서비스 패브릭 클러스터의 노드는 장애 도메인 및 업그레이드 도메인의 2차원 그리드에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="efb4f-116">이 배치 응용 프로그램의 하드웨어 오류 및 응용 프로그램 업그레이드 hello 현재 상태에서 사용할 수 있는 남아 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="efb4f-117">Hello 클러스터 맵을 사용 하 여 hello 현재 클러스터 레이아웃 방법을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![서비스 패브릭 탐색기 클러스터 맵][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="efb4f-119">응용 프로그램 및 서비스 보기</span><span class="sxs-lookup"><span data-stu-id="efb4f-119">View applications and services</span></span>
<span data-ttu-id="efb4f-120">hello 클러스터에 두 개의 하위: 응용 프로그램 및 노드 관리를 위한 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="efb4f-121">서비스 패브릭의 논리적 계층 구조를 통해 응용 프로그램 보기 toonavigate hello를 사용할 수 있습니다: 응용 프로그램, 서비스, 파티션 및 복제본입니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="efb4f-122">Hello 아래의 예제에서는 응용 프로그램을 hello **MyApp** 두 서비스의 구성 **MyStatefulService** 및 **WebService**합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="efb4f-123">**MyStatefulService** 는 상태 저장이므로 한 개의 주 복제본과 두 개의 보조 복제본이 있는 파티션을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="efb4f-124">이와 반대로 WebSvcService는 상태 비저장이며 단일 인스턴스가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![서비스 패브릭 탐색기 응용 프로그램 보기][sfx-application-tree]

<span data-ttu-id="efb4f-126">Hello 트리의 각 수준 hello 주 창 hello 항목에 대 한 관련 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="efb4f-127">예를 들어 hello 상태 및 특정 서비스에 대 한 버전을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-127">For example, you can see hello health status and version for a particular service.</span></span>

![서비스 패브릭 탐색기 기능 창][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="efb4f-129">Hello 클러스터의 노드를 확인</span><span class="sxs-lookup"><span data-stu-id="efb4f-129">View hello cluster's nodes</span></span>
<span data-ttu-id="efb4f-130">hello 노드 보기 hello hello 클러스터의 실제 레이아웃을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="efb4f-131">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="efb4f-132">특히 현재 실행되고 있는 복제본을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="efb4f-133">작업</span><span class="sxs-lookup"><span data-stu-id="efb4f-133">Actions</span></span>
<span data-ttu-id="efb4f-134">서비스 패브릭 탐색기 신속 하 게 tooinvoke 노드, 응용 프로그램 및 클러스터 서비스에 대 한 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="efb4f-135">예를 들어 toodelete 응용 프로그램 인스턴스 hello 응용 프로그램 hello 왼쪽에 hello 트리에서 선택한 다음 선택 **동작** > **응용 프로그램 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![서비스 패브릭 탐색기에서 응용 프로그램 삭제][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="efb4f-137">수행할 수 있습니다 hello 줄임표 다음 tooeach 요소를 클릭 하 여 동일한 작업을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="efb4f-138">hello 다음 표에 각 엔터티에 대해 사용할 수 있는 hello 작업.</span><span class="sxs-lookup"><span data-stu-id="efb4f-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="efb4f-139">**엔터티**</span><span class="sxs-lookup"><span data-stu-id="efb4f-139">**Entity**</span></span> | <span data-ttu-id="efb4f-140">**작업**</span><span class="sxs-lookup"><span data-stu-id="efb4f-140">**Action**</span></span> | <span data-ttu-id="efb4f-141">**설명**</span><span class="sxs-lookup"><span data-stu-id="efb4f-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efb4f-142">응용 프로그램 형식</span><span class="sxs-lookup"><span data-stu-id="efb4f-142">Application type</span></span> |<span data-ttu-id="efb4f-143">프로 비전 해제 형식</span><span class="sxs-lookup"><span data-stu-id="efb4f-143">Unprovision type</span></span> |<span data-ttu-id="efb4f-144">Hello 클러스터 이미지 저장소에서 hello 응용 프로그램 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="efb4f-145">모든 응용 프로그램의 해당 형식 toobe 먼저 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="efb4f-146">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="efb4f-146">Application</span></span> |<span data-ttu-id="efb4f-147">응용 프로그램 삭제</span><span class="sxs-lookup"><span data-stu-id="efb4f-147">Delete Application</span></span> |<span data-ttu-id="efb4f-148">(있는 경우) 모든 서비스와 해당 상태를 포함 하 여 hello 응용 프로그램을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="efb4f-149">부여</span><span class="sxs-lookup"><span data-stu-id="efb4f-149">Service</span></span> |<span data-ttu-id="efb4f-150">서비스 삭제</span><span class="sxs-lookup"><span data-stu-id="efb4f-150">Delete Service</span></span> |<span data-ttu-id="efb4f-151">(있는 경우) hello 서비스 및 해당 상태를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="efb4f-152">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-152">Node</span></span> |<span data-ttu-id="efb4f-153">활성화</span><span class="sxs-lookup"><span data-stu-id="efb4f-153">Activate</span></span> |<span data-ttu-id="efb4f-154">Hello 노드를 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-154">Activate hello node.</span></span> |
| <span data-ttu-id="efb4f-155">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-155">Node</span></span> | <span data-ttu-id="efb4f-156">비활성화(일시 중지)</span><span class="sxs-lookup"><span data-stu-id="efb4f-156">Deactivate (pause)</span></span> | <span data-ttu-id="efb4f-157">현재 상태의 hello 노드를 일시 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-157">Pause hello node in its current state.</span></span> <span data-ttu-id="efb4f-158">서비스 계속 toorun 하지만 서비스 패브릭 이동 하지 않습니다 사전 아무 것도으로 끌거나 것 필요한 tooprevent 가동 중단 또는 데이터 불일치가 아닌 경우.</span><span class="sxs-lookup"><span data-stu-id="efb4f-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="efb4f-159">이 작업은 일반적으로 사용 되는 tooenable 검사 하는 동안 이동 하지 않는 특정 노드 tooensure에서 서비스를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="efb4f-160">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-160">Node</span></span> | <span data-ttu-id="efb4f-161">비활성화(다시 시작)</span><span class="sxs-lookup"><span data-stu-id="efb4f-161">Deactivate (restart)</span></span> | <span data-ttu-id="efb4f-162">안전하게 노드에서 모든 메모리 내 서비스를 이동하고 영구 서비스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="efb4f-163">일반적으로 컴퓨터 필요 toobe 또는 hello 호스트 프로세스 다시 시작 될 때 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="efb4f-164">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-164">Node</span></span> | <span data-ttu-id="efb4f-165">비활성화(데이터 제거)</span><span class="sxs-lookup"><span data-stu-id="efb4f-165">Deactivate (remove data)</span></span> | <span data-ttu-id="efb4f-166">안전 하 게 충분 한 예비 복제본을 빌드한 후 hello 노드에서 실행 되는 모든 서비스를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="efb4f-167">노드(또는 최소한 저장소)가 위원회에서 영구적으로 제거될 때 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="efb4f-168">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-168">Node</span></span> | <span data-ttu-id="efb4f-169">노드 상태 제거</span><span class="sxs-lookup"><span data-stu-id="efb4f-169">Remove node state</span></span> | <span data-ttu-id="efb4f-170">Hello 클러스터에서 기술 노드의 복제본을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="efb4f-171">이미 실패한 노드를 복구할 수 없다고 간주하는 경우 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="efb4f-172">노드</span><span class="sxs-lookup"><span data-stu-id="efb4f-172">Node</span></span> | <span data-ttu-id="efb4f-173">다시 시작</span><span class="sxs-lookup"><span data-stu-id="efb4f-173">Restart</span></span> | <span data-ttu-id="efb4f-174">Hello 노드를 다시 시작 하 여 노드 오류를 시뮬레이트하십시오.</span><span class="sxs-lookup"><span data-stu-id="efb4f-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="efb4f-175">자세한 내용은 [여기](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="efb4f-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="efb4f-176">파괴적 많은 작업 이므로 수 전에 질문을 tooconfirm 의도 했던 hello 동작이 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="efb4f-177">서비스 패브릭 탐색기를 통해 수행할 수 있는 모든 작업은 PowerShell 또는 REST API를 tooenable 자동화를 통해 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="efb4f-178">또한 특정된 응용 프로그램 유형 및 버전에 대 한 서비스 패브릭 탐색기 toocreate 응용 프로그램 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="efb4f-179">Hello 트리 뷰에서 hello 응용 프로그램 유형을 선택 하 고 hello 클릭 **앱 인스턴스 만들기** hello 오른쪽 창에서 원하는 링크 다음 toohello 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Service Fabric Explorer에서 응용 프로그램 인스턴스 만들기][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="efb4f-181">Service Fabric Explorer를 통해 만든 응용 프로그램 인스턴스는 현재 매개 변수화될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="efb4f-182">이러한 프로그램은 기본 매개 변수 값을 사용하여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="efb4f-183">Tooa 원격 서비스 패브릭 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="efb4f-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="efb4f-184">Hello 클러스터 끝점을 알고 있고 충분 한 권한이 있으면 모든 브라우저에서 서비스 패브릭 탐색기를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="efb4f-185">서비스 패브릭 탐색기는 hello 클러스터에서 실행 되는 또 다른 서비스 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="efb4f-186">원격 클러스터에 대 한 hello 서비스 패브릭 탐색기 끝점을 검색</span><span class="sxs-lookup"><span data-stu-id="efb4f-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="efb4f-187">서비스 패브릭 탐색기 tooreach 특정된 클러스터에 대 한 브라우저를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="efb4f-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="efb4f-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="efb4f-189">Azure의 클러스터에 대 한 전체 URL hello hello Azure 포털의 hello 클러스터 essentials 창에서 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="efb4f-190">Tooa 보안 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="efb4f-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="efb4f-191">인증서 또는 Azure Active Directory (AAD)를 사용 하 여 사용 하 여 클라이언트 액세스 tooyour 서비스 패브릭 클러스터를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="efb4f-192">Tooconnect tooService 패브릭 탐색기 보안 클러스터에서 사용 하려는 경우 한 다음 hello 클러스터 구성에 따라 됩니다 클라이언트 인증서 필요 toopresent 여야 하거나 AAD를 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="efb4f-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efb4f-193">다음 단계</span><span class="sxs-lookup"><span data-stu-id="efb4f-193">Next steps</span></span>
* [<span data-ttu-id="efb4f-194">테스트 용이성 개요</span><span class="sxs-lookup"><span data-stu-id="efb4f-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="efb4f-195">Visual Studio에서 서비스 패브릭 응용 프로그램 관리</span><span class="sxs-lookup"><span data-stu-id="efb4f-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="efb4f-196">PowerShell을 사용하여 서비스 패브릭 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="efb4f-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
